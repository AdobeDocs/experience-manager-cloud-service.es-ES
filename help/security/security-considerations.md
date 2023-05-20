---
title: Consideraciones de seguridad de AEM as a Cloud Service Security
description: Obtenga información acerca de las consideraciones de seguridad importantes al utilizar AEM as a Cloud Service
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: 9cff6e94b38016f008fd8177be2e071a530d80b6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# Consideraciones de seguridad de AEM as a Cloud Service Security {#security-considerations}

## Almacén de confianza de AEM {#aem-trust-store}

Para admitir operaciones criptográficas asimétricas, AEM guarda certificados dentro del repositorio de contenido, en un almacén de confianza global. Sus contenidos son públicos y, de forma predeterminada, son accesibles de forma anónima por cualquiera en las instancias de editor.

### Características del almacén de confianza {#truststore-characteristics}

* El almacén de confianza se encuentra debajo de `/etc/truststore` y consta de un archivo de almacén de claves Java, su contraseña y los metadatos del repositorio. Tenga en cuenta que tanto la contraseña como el almacén de claves en sí están cifrados por motivos técnicos, aunque los certificados contenidos sean accesibles para todos de forma predeterminada a través de la API
* De forma predeterminada, los certificados se utilizan solo para la compatibilidad con HTTPS y SAML, y el almacén debe crearse manualmente primero
* Los clientes pueden usarlo en su propio código a través de la [API de almacén de claves](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* El almacén de confianza se puede administrar a través de la IU en **Herramientas** - **Seguridad** - **Almacén de confianza** o accediendo a *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, como se muestra a continuación:

   ![Administración del almacén de confianza](/help/security/assets/global-trust-store-modified.png)

* El acceso al almacén de confianza se puede restringir aún más mediante el control de acceso al repositorio, según el caso de uso.

>[!NOTE]
>
>Adobe recomienda que se utilicen los controles de acceso predeterminados para el almacén de confianza, lo que significa que queda accesible al público. Para una configuración más segura, puede usar una política de denegación de jcr:all para todos.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
