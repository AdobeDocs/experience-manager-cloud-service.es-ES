---
title: Claves administradas por el cliente para AEM as a Cloud Service
description: Obtenga información sobre cómo configurar las claves de cifrado para AEM as a Cloud Service
feature: Security
role: Admin
exl-id: 100ddbf2-9c63-406f-a78d-22862501a085
source-git-commit: 424c679f6da1aaa0f40df598f4d0d1517a3e8c5b
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 32%

---

# Configuración de claves gestionadas por el cliente para AEM as a Cloud Service {#customer-managed-keys-for-aem-as-a-cloud-service}

AEM as a Cloud Service almacena actualmente datos de cliente en Azure Blob Storage y MongoDB, utilizando claves de cifrado administradas por el proveedor de forma predeterminada para proteger los datos. Aunque esta configuración satisface las necesidades de seguridad de muchas organizaciones, las empresas de industrias reguladas o las que requieren una mayor seguridad de los datos buscan un mayor control sobre sus prácticas de cifrado. En el caso de las organizaciones que dan prioridad a la seguridad de los datos, al cumplimiento normativo y a la posibilidad de administrar sus claves de cifrado, la solución CMK (Claves administradas por el cliente) ofrece una mejora esencial.

>[!NOTE]
>
>Antes de configurar Azure Key Vault, primero debe habilitar CMK para el programa de Cloud Service en Cloud Manager. CMK está habilitado en la ficha **Seguridad** durante la creación del programa de producción o al editar un programa existente.
>
>Ver [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) o [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).


## Finalidad de esta solución {#the-problem-being-solved}

Las claves administradas por el proveedor pueden crear dificultades para las empresas que requieren privacidad e integridad adicionales. Si no tienen el control sobre la administración de claves, las organizaciones se enfrentan a desafíos a la hora de cumplir los requisitos de conformidad, implementar políticas de seguridad personalizadas y garantizar una total seguridad de los datos.

La introducción de claves administradas por el cliente (CMK) soluciona estos problemas al otorgar a los clientes de AEM el control total de sus claves de cifrado. Al autenticarse mediante Microsoft Entra ID (anteriormente Azure Active Directory), AEM CS se conecta de forma segura al Azure Key Vault del cliente, lo que les permite administrar el ciclo de vida de sus claves de cifrado, incluida la creación, rotación y revocación de claves.

CMK ofrece varias ventajas:

* **Administrar datos y cifrado de aplicaciones:** Aumente la seguridad con el control directo de su aplicación de AEM y las claves criptográficas de datos.
* **Mejore la confidencialidad y la integridad:** Reduzca la probabilidad de acceso involuntario y la divulgación de datos confidenciales o privados con una completa administración de cifrado.
* **Compatibilidad con Azure Key Vault:** El uso de Azure Key Vault permite el almacenamiento de claves, el procesamiento de operaciones secretas y la realización de rotaciones de claves.

Al adoptar CMK, los clientes pueden aumentar el control sobre sus prácticas de seguridad y cifrado de datos, mejorando la seguridad y mitigando los riesgos, manteniendo al mismo tiempo la escalabilidad y flexibilidad de AEM CS.

AEM as a Cloud Service le permite utilizar sus propias claves de cifrado para cifrar datos en reposo. Esta guía proporciona los pasos para configurar una clave administrada por el cliente (CMK) en Azure Key Vault para AEM as a Cloud Service.

>[!WARNING]
>
>Después de configurar CMK, no podrá volver a las claves administradas por el sistema. Es su responsabilidad administrar sus claves de forma segura y proporcionar acceso a Key Vault, la clave y la aplicación CMK dentro de Azure para evitar la pérdida de acceso a sus datos.

Esta guía proporciona los siguientes pasos para crear y configurar la infraestructura necesaria:

1. Configurar su entorno
1. Obtener un ID de aplicación de Adobe
1. Crear un nuevo grupo de recursos
1. Crear un almacén de claves
1. Conceder a Adobe acceso al almacén de claves
1. Crear una clave de cifrado

Debe compartir la dirección URL del almacén de claves, el nombre de la clave de cifrado y la información sobre el almacén de claves con Adobe.

## Configurar su entorno {#setup-your-environment}

La interfaz de línea de comandos (CLI) de Azure es el único requisito de esta guía. Si todavía no tiene instalada la CLI de Azure, siga las instrucciones de instalación oficiales [aquí](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).

Antes de continuar con el resto de esta guía, inicie sesión en su CLI con `az login`.

>[!NOTE]
>
>Aunque esta guía utiliza la CLI de Azure, es posible realizar las mismas operaciones a través de la consola de Azure. Si prefiere usar la consola de Azure, utilice los comandos siguientes como referencia.


## Iniciar el proceso de configuración de CMK para AEM as a Cloud Service {#request-cmk-for-aem-as-a-cloud-service}

Debe solicitar la configuración de claves administradas por el cliente (CMK) para su entorno de AEM as a Cloud Service a través de la interfaz de usuario de. Para ello, vaya a la interfaz de usuario de AEM Home Security, en la sección **Claves administradas por el cliente**.
La página enumera todos los programas compatibles con CMK. A continuación, puede iniciar el proceso de incorporación haciendo clic en el botón Habilitar programa.

![Habilitar un programa para usar CMK](./assets/cmk/step0.png)

Si CMK se ha habilitado en Cloud Manager mientras se crea o edita un programa, haga clic en el botón Iniciar incorporación.

![Iniciar la incorporación de un sitio web mediante la interfaz de usuario de CMK](./assets/cmk/step1.png)


## Obtener un ID de aplicación de Adobe {#obtain-an-application-id-from-adobe}

Después de iniciar el proceso de incorporación, Adobe proporciona un ID de aplicación adicional. Este ID de aplicación es necesario para el resto de la guía y crea una entidad de seguridad de servicio que permite a Adobe acceder a su almacén de claves. Si todavía no tiene un ID de aplicación, espere hasta que Adobe lo proporcione.

![La solicitud se está procesando. Espere a que Adobe proporcione el identificador de aplicación de Entra](./assets/cmk/step2.png)

Una vez completada la solicitud, verá el ID de aplicación en la interfaz de usuario de CMK.

![Adobe ha proporcionado el identificador de aplicación de Entra](./assets/cmk/step3.png)

## Crear un nuevo grupo de recursos {#create-a-new-resource-group}

Cree un nuevo grupo de recursos en la ubicación que desee.

```powershell
# Choose a location and a name for the resource group.
$location="<AZURE LOCATION>"
$resourceGroup="<RESOURCE GROUP>"

# Create the resource group.
az group create --location $location --resource-group $resourceGroup
```

Si ya tiene un grupo de recursos, utilícelo en su lugar. En el resto de esta guía, la ubicación del grupo de recursos y su nombre se identifican con `$location` y `$resourceGroup`, respectivamente.

## Crear un almacén de claves {#create-a-key-vault}

Cree un almacén de claves para contener la clave de cifrado. El almacén de claves debe tener habilitada la protección contra depuración. La protección contra depuración es necesaria para cifrar datos en reposo desde otros servicios de Azure. El acceso a la red pública también debe estar habilitado para garantizar que los servicios de Adobe puedan acceder al almacén de claves.

>[!IMPORTANT]
>La desactivación del acceso a la red pública para Key Vault requiere la ejecución de operaciones como la creación o rotación de claves desde un entorno con acceso a la red de Key Vault. Por ejemplo, una VM que puede acceder a Key Vault.

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
  --default-action=Allow `
  --enable-purge-protection `
  --enable-rbac-authorization `
  --public-network-access Enabled
```

## Conceder a Adobe acceso al almacén de claves {#grant-adobe-access-to-the-key-vault}

En este paso, permite a Adobe acceder a su almacén de claves a través de una aplicación Entra. Adobe ya debería haber proporcionado el ID de la aplicación Entra.

En primer lugar, debe crear una entidad de seguridad de servicio adjunta a la aplicación Entra y asignarle los roles **Key Vault Reader** y **Key Vault Crypto User**. Las funciones se limitan al almacén de claves creado en esta guía.

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

## Crear una clave de cifrado {#create-an-encryption-key}

Por último, puede crear una clave de cifrado en el almacén de claves. Necesita el rol de **Key Vault Crypto Officer** para completar este paso. Para que se le otorgue esta función, póngase en contacto con el administrador del sistema si el usuario que ha iniciado sesión no tiene esta función. También puede pedir a una persona que ya tenga esa función que complete este paso por usted.

Se requiere acceso de red al almacén de claves para crear la clave de cifrado. En primer lugar, compruebe que puede acceder al almacén de claves y continúe con la creación de la clave:

```powershell
# Reuse this information from the previous steps.
$keyVaultName="<KEY VAULT NAME>"

# Choose a name for your key.
$keyName="<KEY NAME>"

# Create the key.
az keyvault key create --vault-name $keyVaultName --name $keyName
```

## Compartir la información clave del almacén {#share-the-key-vault-information}

En este punto, la configuración ha finalizado. Comparta la información necesaria a través de la interfaz de usuario de CMK, que inicia el proceso de configuración del entorno.

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

Proporcione esta información en la interfaz de usuario de CMK:
![Rellene la información de la interfaz de usuario](./assets/cmk/step3a.png)

## Implicaciones de revocar el acceso a claves {#implications-of-revoking-key-access}

Revocar o deshabilitar el acceso a la aplicación Key Vault, key o CMK puede causar interrupciones operacionales significativas en su entorno de AEM as a Cloud Service. Una vez deshabilitadas estas claves, los datos de AEM as a Cloud Service se vuelven inaccesibles y las operaciones de flujo descendente que dependen de estos datos dejan de funcionar. Es crucial comprender los impactos potenciales antes de realizar cambios en las configuraciones clave.

Si decide revocar el acceso de AEM as a Cloud Service a sus datos, puede hacerlo eliminando la función de usuario asociada a la aplicación de Key Vault dentro de Azure.

## Configuración de CMK de ensayo {#stage-cmk-setup}

Después de proporcionar la información necesaria en la interfaz de usuario de CMK, Adobe inicia el proceso de configuración del entorno de ensayo de AEM as a Cloud Service. Este proceso requiere tiempo y se le notifica una vez que se ha completado.

![Espere a que Adobe configure el entorno de ensayo](./assets/cmk/step4.png)

## Configuración de CMK de producción {#prod-cmk-setup}

Una vez completada la configuración de fase, debe realizar una validación completa de extremo-2-extremo. Si todo funciona correctamente, debe confirmar que el entorno de producción se puede configurar en consecuencia.

![Confirmar el entorno de producción](./assets/cmk/step5.png)

Después de confirmarlo en la interfaz de usuario de CMK, Adobe inicia el proceso de configuración para el entorno de AEM as a Cloud Service Prod. Este proceso requiere tiempo y se le notifica una vez que se ha completado.

![Espere a que Adobe configure el entorno de producción](./assets/cmk/step6.png)


## Completar la configuración de CMK {#complete-the-cmk-setup}

Una vez completado el proceso de configuración, puede ver el estado de la configuración de CMK en la interfaz de usuario. También puede ver el almacén de claves y la clave de cifrado.
![El proceso se ha completado](./assets/cmk/step7.png)

## Preguntas y asistencia {#questions-and-support}

Póngase en contacto con Adobe si tiene alguna pregunta, duda o necesita ayuda con la configuración de claves administradas por el cliente para AEM as a Cloud Service. El Soporte de Adobe soluciona cualquier pregunta que tenga.
