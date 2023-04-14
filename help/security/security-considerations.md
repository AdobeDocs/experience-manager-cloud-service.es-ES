---
title: Consideraciones de seguridad as a Cloud Service AEM
description: Obtenga información sobre las consideraciones de seguridad importantes al utilizar AEM as a Cloud Service
hidefromtoc: true
hide: true
source-git-commit: 39ffd826f5d1e9cea2e6a03a74f39c16647b45fa
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Consideraciones de seguridad as a Cloud Service AEM {#security-considerations}

## Almacén de confianza de AEM {#aem-trust-store}

Para admitir operaciones criptográficas asimétricas, AEM almacena certificados dentro del repositorio de contenido, en un almacén de confianza global. Sus contenidos son públicos y, de forma predeterminada, son accesibles de forma anónima por todos en las instancias de editor.

### Características del almacén de confianza {#truststore-characteristics}

* El almacén de confianza se encuentra a continuación `/etc/truststore` y consta de un archivo de almacén de claves Java, la contraseña del almacén de claves y los metadatos del repositorio. Tenga en cuenta que tanto la contraseña como el almacén de claves en sí están cifrados por motivos técnicos, aunque los certificados contenidos sean accesibles para todos de forma predeterminada a través de la API
* De forma predeterminada, los certificados se utilizan solo para la compatibilidad con HTTPS y SAML, y el almacén debe crearse manualmente primero
* Los clientes pueden usarlo en su propio código a través de la variable [API de almacén de claves](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* El almacén de confianza se puede administrar a través de la interfaz de usuario en **Herramientas** - **Seguridad** - **Almacén de confianza** o accediendo a *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, como se muestra a continuación:

   ![Administración del almacén de confianza](/help/security/assets/global-trust-store-modified.png)

* El acceso al almacén de confianza se puede restringir aún más mediante el control de acceso al repositorio, según el caso de uso.

>[!NOTE]
>
>Adobe recomienda que se utilicen los controles de acceso predeterminados para el almacén de confianza, lo que significa que permanece accesible al público. Para la configuración más segura, puede usar una política de denegación de jcr:all para todos.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
