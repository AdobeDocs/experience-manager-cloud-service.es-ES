---
title: Claves administradas por el cliente para AEM as a Cloud Service
description: Obtenga información sobre cómo configurar las claves de cifrado para AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: eb38369ee918851a9f792af811bafff9b2e49a53
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 86%

---

# Configuración de claves administradas por el cliente para AEM as a Cloud Service {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service almacena actualmente datos de cliente en Azure Blob Storage y MongoDB, utilizando claves de cifrado administradas por el proveedor de forma predeterminada para proteger los datos. Aunque esta configuración satisface las necesidades de seguridad de muchas organizaciones, las empresas de industrias reguladas o las que requieren una mayor seguridad de los datos pueden buscar un mayor control sobre sus prácticas de cifrado. En el caso de las organizaciones que dan prioridad a la seguridad de los datos, al cumplimiento normativo y a la posibilidad de administrar sus claves de cifrado, la solución CMK (Claves administradas por el cliente) ofrece una mejora esencial.

## Problema resuelto {#the-problem-being-solved}

Las claves administradas por el proveedor pueden crear preocupaciones para las empresas que requieren privacidad e integridad adicionales. Sin control sobre la administración de claves, las organizaciones se enfrentan a desafíos para cumplir con los requisitos de cumplimiento, implementar políticas de seguridad personalizadas y garantizar una seguridad de datos completa.

La introducción de claves administradas por el cliente (CMK) soluciona estos problemas al otorgar a los clientes de AEM el control total de sus claves de cifrado. Mediante la autenticación a través de Microsoft Entra ID (anteriormente Azure Active Directory), AEM CS se conecta de forma segura a Azure Key Vault del cliente, lo que les permite administrar el ciclo de vida de sus claves de cifrado, abarcando la creación, rotación y revocación de claves.

CMK ofrece varias ventajas:

* **Controlar datos y cifrado de aplicaciones:** Intensifique la seguridad con el control directo de la aplicación de AEM y las claves criptográficas de datos.
* **Aumentar la confidencialidad y la integridad:** Reduzca la probabilidad de acceso involuntario y la divulgación de datos confidenciales o privados con una administración completa del cifrado.
* **Compatibilidad con Azure Key Vault:** El uso de Azure Key Vault permite el almacenamiento de claves, el procesamiento de operaciones de secretos y la realización de rotaciones de claves.

Al adoptar CMK, los clientes pueden aumentar el control sobre sus prácticas de seguridad de datos y cifrado, mejorando la seguridad y mitigando los riesgos, todo mientras siguen disfrutando de la escalabilidad y flexibilidad de AEM CS.

AEM as a Cloud Service le permite traer sus propias claves de cifrado para cifrar datos en reposo. Esta guía proporciona los pasos necesarios para configurar una clave administrada por el cliente (CMK) en Azure Key Vault para AEM as a Cloud Service.

>[!WARNING]
>
>Después de configurar CMK, no podrá volver a las claves administradas por el sistema. Es su responsabilidad administrar sus claves de forma segura y proporcionar acceso a Key Vault, la clave y la aplicación CMK dentro de Azure para evitar la pérdida de acceso a sus datos.

También se le guiará a través de los siguientes pasos para crear y configurar la infraestructura necesaria:

1. Configurar su entorno
1. Obtener un ID de aplicación de Adobe
1. Crear un nuevo grupo de recursos
1. Crear un almacén de claves
1. Conceder a Adobe acceso al almacén de claves
1. Crear una clave de cifrado

Deberá compartir la dirección URL del almacén de claves, el nombre de la clave de cifrado y la información sobre el almacén de claves con Adobe.

## Configurar su entorno {#setup-your-environment}

La interfaz de línea de comandos (CLI) de Azure es el único requisito de esta guía. Si todavía no tiene instalada la CLI de Azure, siga las instrucciones de instalación oficiales [aquí](https://learn.microsoft.com/es-es/cli/azure/install-azure-cli).

Antes de continuar con el resto de esta guía, inicie sesión en la CLI con `az login`.

>[!NOTE]
>
>Aunque esta guía utiliza la CLI de Azure, es posible realizar las mismas operaciones a través de la consola de Azure. Si prefiere usar la consola de Azure, utilice los comandos siguientes como referencia.

## Obtener un ID de aplicación de Adobe {#obtain-an-application-id-from-adobe}

Adobe le proporcionará un ID de aplicación Entra que necesitará en el resto de esta guía. Si todavía no tiene un ID de aplicación, póngase en contacto con Adobe para obtener uno.

## Crear un nuevo grupo de recursos {#create-a-new-resource-group}

Cree un nuevo grupo de recursos en la ubicación que desee.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Si ya dispone de un grupo de recursos, no dude en utilizarlo en su lugar. En el resto de esta guía, la ubicación del grupo de recursos y su nombre se identifican con `$location` y `$resourceGroup`, respectivamente.

## Crear un almacén de claves {#create-a-key-vault}

Deberá crear un almacén de claves que contenga la clave de cifrado. El almacén de claves debe tener habilitada la protección contra depuración. La protección contra depuración es necesaria para cifrar datos en reposo desde otros servicios de Azure. El acceso a la red pública también debe estar habilitado para garantizar que el inquilino de Adobe pueda acceder al almacén de claves.

>[!IMPORTANT]
>La creación de Key Vault con el acceso a la red pública desactivado exige que todas las operaciones relacionadas con Key Vault, como la creación o rotación de claves, se ejecuten desde un entorno que tenga acceso de red a KeyVault, por ejemplo, una VM que pueda acceder a KeyVault.

```powershell
# Reuse this information from the previous step.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Choose a name for the key vault.
$keyVaultName="<KEY VAULT NAME>"

# Create the key vault.
az keyvault create `
  --location $location `
  --resource-group $resourceGroup `
  --name $keyVaultName `
  --default-action=Deny `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Enabled
```

## Conceder a Adobe acceso al almacén de claves {#grant-adobe-access-to-the-key-vault}

En este paso permitirá que Adobe acceda a su almacén de claves a través de una aplicación Entra. Adobe debería haber proporcionado ya el ID de la aplicación Entra.

En primer lugar, debe crear una entidad principal de servicio adjunta a la aplicación Entra y asignarle las funciones **Key Vault Reader** y **Key Vault Crypto User**. Las funciones se limitan al almacén de claves creado en esta guía.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# The application ID is provided by Adobe.
$appId="<APPLICATION ID>"

# Retrieve the ID of the key vault.
$keyVaultId=(az keyvault show --resource-group $resourceGroup --name $keyVaultName --query id --output tsv)

# Create a new service principal.
$servicePrincipalId=(az ad sp create --id $appId --query id --out tsv)

# Assign the roles to the service principal.
az role assignment create --assignee $servicePrincipalId --role "Key Vault Reader" --scope $keyVaultId
az role assignment create --assignee $servicePrincipalId --role "Key Vault Crypto User" --scope $keyVaultId
```

## Crear una clave de cifrado {#create-an-ecryption-key}

Por último, puede crear una clave de cifrado en el almacén de claves. Tenga en cuenta que necesitará la función **Key Vault Crypto Officer** para completar este paso. Si el usuario que ha iniciado sesión no dispone de esta función, póngase en contacto con el administrador del sistema para que se la otorgue o pida a alguien que ya la tenga que complete este paso por usted.

Se requiere acceso de red al almacén de claves para crear la clave de cifrado. En primer lugar, compruebe que puede acceder al almacén de claves y continúe con la creación de la clave:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Compartir la información de Key Vault {#share-the-key-vault-information}

En este punto, ya está todo listo. Solo tiene que compartir la información necesaria con Adobe, que se encargará de configurar su entorno.

```powershell
# Reuse this information from the previous steps.
$resourceGroup="<RESOURCE GROUP>"
$keyVaultName="<KEY VAULT NAME>"

# Retrieve the URL of your key vault.
$keyVaultUri=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.vaultUri `
    --output tsv)

# In addition we would need the tenantId and the subscriptionId in order to setup the connection.
$tenantId=(az keyvault show --name $keyVaultName `
    --resource-group $resourceGroup `
    --query properties.tenantId `
    --output tsv)
$subscriptionId="<Subscription ID>"
```


## Implicaciones de la revocación del acceso a claves {#implications-of-revoking-key-access}

La revocación o deshabilitación del acceso a Key Vault, a la clave o a la aplicación CMK puede causar interrupciones significativas, que incluyan cambios de última hora en las operaciones de la plataforma. Una vez deshabilitadas estas claves, los datos de la plataforma pueden volverse inaccesibles y cualquier operación posterior que dependa de estos datos dejará de funcionar. Es crucial comprender completamente las repercusiones posteriores antes de realizar cambios en las configuraciones clave.

Si decide revocar el acceso de la plataforma a sus datos, puede hacerlo eliminando la función de usuario asociada a la aplicación desde Key Vault en Azure.

## Pasos siguientes {#next-steps}

Póngase en contacto con Adobe y comparta:

* La dirección URL del almacén de claves. La ha recuperado en este paso y la ha guardado en la variable `$keyVaultUri`.
* El nombre de su clave de cifrado. Ha creado la clave en un paso anterior y la ha guardado en la variable `$keyName`.
* `$resourceGroup`, `$subscriptionId` y `$tenantId`, que son necesarios para configurar la conexión con el almacén de claves.

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Claves administradas por el cliente en Private Beta {#customer-managed-keys-in-private-beta}

El equipo de ingeniería de Adobe está trabajando actualmente en una implementación mejorada de CMK aprovechando el vínculo privado de Azure. La nueva implementación le permitirá compartir su clave a través de la red troncal de Azure gracias a una conexión directa de vínculo privado entre el inquilino de Adobe y su almacén de claves.

Esta implementación mejorada se encuentra actualmente en Private Beta y se puede habilitar para clientes seleccionados que acepten suscribirse al programa Private Beta y trabajar en estrecha colaboración con el departamento de ingeniería de Adobe. Si está interesado en Private Beta para CMK mediante un vínculo, póngase en contacto con Adobe para obtener más información.
