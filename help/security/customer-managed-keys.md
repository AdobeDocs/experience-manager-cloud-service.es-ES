---
title: Claves gestionadas por el cliente para AEM as a Cloud Service
description: Obtenga información sobre cómo administrar las claves de cifrado para AEM as a Cloud Service
feature: Security
role: Admin
hide: true
hidefromtoc: true
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 18fe0125351c635c226bebf0f309710634230e64
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Configuración de claves administradas por el cliente para AEM as a Cloud Service {#cusomer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service almacena actualmente datos de clientes en Azure Blob Storage y MongoDB, utilizando claves de cifrado administradas por el proveedor de forma predeterminada para proteger los datos. Aunque esta configuración satisface las necesidades de seguridad de muchas organizaciones, las empresas de industrias reguladas o las que requieren una soberanía de datos mejorada pueden buscar un mayor control sobre sus prácticas de cifrado. Para las organizaciones que dan prioridad a la seguridad de los datos, el cumplimiento normativo y la capacidad de administrar sus claves de cifrado, la solución Claves administradas por el cliente (CMK) ofrece una mejora fundamental.

## El problema que se está resolviendo {#the-problem-being-solved}

Las claves administradas por el proveedor pueden crear preocupaciones para las empresas en sectores como las finanzas, la atención médica y el gobierno, donde las regulaciones estrictas exigen un control exhaustivo sobre la seguridad de los datos. Sin control sobre la administración de claves, las organizaciones se enfrentan a desafíos para cumplir con los requisitos de cumplimiento, implementar políticas de seguridad personalizadas y garantizar la soberanía completa de los datos.

AEM La introducción de las claves administradas por el cliente (CMK) soluciona estos problemas al dar a los clientes de los servicios de cifrado un control total sobre sus claves de cifrado, lo que les permite dar a los clientes un control total sobre sus claves de cifrado. Al autenticarse mediante Microsoft AEM Entra ID (anteriormente Azure Active Directory), CS se conecta de forma segura al Azure Key Vault del cliente, lo que les permite administrar el ciclo de vida de sus claves de cifrado, lo que abarca la creación, la rotación y la revocación de claves.

CMK ofrece varias ventajas:

* **Seguridad mejorada:** Los clientes pueden asegurarse de que sus prácticas de cifrado cumplan los requisitos de seguridad específicos, lo que les proporciona tranquilidad respecto a la protección de datos.
* **Flexibilidad de cumplimiento:** Con un control total sobre el ciclo de vida clave, las empresas pueden adaptarse fácilmente a las cambiantes normas regulatorias como el RGPD, la HIPAA o la CCPA, lo que garantiza que su postura de cumplimiento se mantenga firme.
* AEM **Integración perfecta:** La solución CMK se integra directamente con Azure Blob Storage y MongoDB en CS, lo que garantiza que no se interrumpan las operaciones de almacenamiento ni la facilidad de uso y, al mismo tiempo, proporciona a los clientes potentes capacidades de cifrado.

AEM Al adoptar CMK, los clientes pueden aumentar el control sobre sus prácticas de seguridad de datos y cifrado, mejorando el cumplimiento y mitigando los riesgos, todo mientras siguen disfrutando de la escalabilidad y flexibilidad de los sistemas de cifrado de alta velocidad (CSC) de la que disponen los clientes.

AEM as a Cloud Service le permite traer sus propias claves de cifrado para cifrar datos en reposo. Esta guía proporciona los pasos para configurar una clave administrada por el cliente (CMK) en Azure Key Vault para AEM as a Cloud Service.

>[!WARNING]
>
>Después de configurar CMK, no puede volver a las claves administradas por el sistema. Usted es responsable de administrar sus claves de forma segura y de proporcionar acceso a su aplicación Key Vault, Key y CMK dentro de Azure para evitar la pérdida de acceso a sus datos.

También se le guiará a través de los siguientes pasos para crear y configurar la infraestructura necesaria:

1. Configurar su entorno
1. Obtener un ID de aplicación de la Adobe
1. Crear un nuevo grupo de recursos
1. Crear un kault de claves
1. Conceder acceso al Adobe a la clave kault
1. Creación de una clave de cifrado

Deberá compartir la dirección URL del almacén de claves, el nombre de la clave de cifrado y la información sobre el almacén de claves con el Adobe.

## Configure su entorno {#setup-your-environment}

La interfaz de línea de comandos (CLI) de Azure es el único requisito de esta guía. Si todavía no tiene la CLI de Azure instalada, siga las instrucciones de instalación oficiales [aquí](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli).

Antes de continuar con el resto de esta guía, inicie sesión en la CLI con `az login`.

>[!NOTE]
>
>Aunque esta guía utiliza la CLI de Azure, es posible realizar las mismas operaciones a través de la consola de Azure. Si prefiere usar la consola de Azure, utilice los comandos siguientes como referencia.

## Obtener un ID de aplicación del Adobe {#obtain-an-application-id-from-adobe}

Adobe le proporcionará un ID de aplicación de Entra que necesitará en el resto de esta guía. Si todavía no tiene un ID de aplicación, póngase en contacto con el Adobe de para obtener uno.

## Crear un nuevo grupo de recursos {#create-a-new-resource-group}

Cree un nuevo grupo de recursos en la ubicación que elija.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Si ya tiene un grupo de recursos, puede utilizarlo en su lugar. En el resto de esta guía, la ubicación del grupo de recursos y su nombre se identifican con `$location` y `$resourceGroup`, respectivamente.

## Crear un almacén de claves {#create-a-key-vault}

Deberá crear un almacén de claves para contener la clave de cifrado. El almacén de claves debe tener habilitada la protección contra purgas. La protección de purga es necesaria para cifrar datos en reposo desde otros servicios de Azure. El acceso a la red pública también debe estar habilitado para garantizar que el inquilino de Adobe pueda acceder al almacén de claves.

>[!IMPORTANT]
>La creación de Key Vault con acceso de red pública desactivado exige que todas las operaciones relacionadas con Key Vault, como la creación o rotación de claves, se ejecuten desde un entorno que tenga acceso de red a KeyVault, por ejemplo, una VM que pueda acceder a KeyVault.

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

## Conceder acceso de Adobe a Key Vault {#grant-adone-access-to-the-key-vault}

En este paso permitirá que el Adobe acceda a su almacén de claves a través de una aplicación Entra. El Adobe debería haber proporcionado ya el ID de la aplicación Entra.

En primer lugar, debe crear una entidad de seguridad de servicio adjunta a la aplicación Entra y asignarle los roles de **Reader de Key Vault** y **Usuario de Key Vault Crypto**. Las funciones se limitan al almacén de claves creado en esta guía.

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

Por último, puede crear una clave de cifrado en el almacén de claves. Tenga en cuenta que necesitará la función **Key Vault Crypto Officer** para completar este paso. Si el usuario que ha iniciado sesión no tiene esta función, póngase en contacto con el administrador del sistema para que se le otorgue esta función o pida a alguien que ya tenga esa función que complete este paso por usted.

Se requiere acceso de red al almacén de claves para crear la clave de cifrado. En primer lugar, compruebe que puede acceder al almacén de claves y continúe con la creación de la clave:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Chose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Compartir la información clave de Vault {#share-the-key-vault-information}

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

Revocar o deshabilitar el acceso a la aplicación Key Vault, key o CMK puede causar interrupciones significativas, que incluyen cambios importantes en las operaciones de la plataforma. Una vez deshabilitadas estas claves, es posible que no se pueda acceder a los datos en Platform y que las operaciones de flujo descendente que dependan de estos datos dejen de funcionar. Es crucial comprender completamente los impactos descendentes antes de realizar cambios en las configuraciones clave.

Si decide revocar el acceso de Platform a sus datos, puede hacerlo eliminando el rol de usuario asociado a la aplicación de Key Vault en Azure.

## Pasos siguientes {#next-steps}

Póngase en contacto con el Adobe y comparta:

* La dirección URL del almacén de claves. Lo recuperó en este paso y lo guardó en la variable `$keyVaultUri`.
* Nombre de la clave de cifrado. Ha creado la clave en un paso anterior y la ha guardado en la variable `$keyName`.
* Los `$resourceGroup`, `$subscriptionId` y `$tenantId` necesarios para configurar la conexión con el almacén de claves.

<!-- Alexandru: hiding this for now

### Private Link Approvals {#private-link-approvals}

>[!TIP]
>You can also consult the [Azure Documentation](https://learn.microsoft.com/en-us/azure/key-vault/general/private-link-service?tabs=portal#how-to-manage-a-private-endpoint-connection-to-key-vault-using-the-azure-portal) on how to approve a Private Endpoint Connection.

Afterwards, an Adobe Engineer assigned to you will contact you to confirm the creation of the private endpoints, and will request you to approve a set of required Connection Requests. The requests can be approved either using the Azure Portal UI, where you can go to **KeyVault > Settings > Networking > Private Endpoint Connections** and approve the requests with names similar to these: 

`mongodb-atlas-<REGION>-<NUMBER>`, `storage-account-private-endpoint` and `backup-storage-account-private-endpoint`. 

Notify the Adobe Engineer once this process is complete and the Private Endpoints show up as **Approved**. -->

## Claves gestionadas por el cliente en Private Beta {#customer-managed-keys-in-private-beta}

El equipo de ingeniería de Adobe está trabajando actualmente en una implementación mejorada de CMK que aprovecha el vínculo privado de Azure. La nueva implementación permitirá compartir su clave a través de la red troncal de Azure gracias a una conexión directa de vínculo privado entre el inquilino de Adobe y su almacén de claves.

Esta implementación mejorada se encuentra actualmente en Private Beta y se puede habilitar para clientes seleccionados que acepten suscribirse al programa de Private Beta y trabajar en estrecha colaboración con el departamento de ingeniería de Adobe. Si está interesado en el Private Beta para CMK mediante Private Link, póngase en contacto con el Adobe para obtener más información.
