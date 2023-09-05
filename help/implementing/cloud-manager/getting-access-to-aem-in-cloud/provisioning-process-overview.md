---
title: 'Proceso de aprovisionamiento: información general'
description: 'Proceso de aprovisionamiento: información general'
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '330'
ht-degree: 100%

---


# AEM as a Cloud Service: Incorporación y acceso

En esta página se enumeran los recursos de autoayuda sobre procesos de aprovisionamiento para Experience Manager as a Cloud Service.

## Información general del proceso de aprovisionamiento de AEM as a Cloud Service

Esta sección muestra algunos de los artículos más importantes centrados en:

* Acceder a AEM as a Cloud Service
* Proceso de incorporación y aprovisionamiento de Adobe Experience Manager as a Cloud Service
* Ayuda y recursos


### Acceder a AEM as a Cloud Service

Una vez completado el aprovisionamiento automático:

* Derechos de acceso concedidos: Adobe creará una organización dentro del Sistema Identity Management de Adobe (IMS)
* El administrador designado tendrá permisos de administrador de forma predeterminada
* El administrador puede agregar usuarios y roles para otros integrantes del equipo a través de Admin Console
* Revise los permisos basados en roles para los usuarios con el fin de determinar las asignaciones de permisos en Cloud Manager

![processoverview.jpg](assets/processOverview.jpg)


Para obtener más información, consulte [Incorporación a Experience Manager as a Cloud Service en Experience League](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=es).

### Recursos y vínculos

* [Compatibilidad con IMS para AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=es)
* [Permisos basados en roles en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=es#what-is-required)
* [Acceder a Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=es#getting-access)


## Proceso de incorporación de Adobe Experience Manager as a Cloud Service

### 1. La orden de compra Desencadena el autoaprovisionamiento.

### 2. Incorporar organizaciones a Adobe Admin Console:

![processoverview2.jpg](assets/processOverview2.jpg)

* Administrador del sistema:
   * Aprovisionar programas y entornos de AEM.
   * Navegue hasta Admin Console para realizar tareas administrativas.
   * Reclamar un dominio para confirmar la propiedad del dominio respectivo
   * Configurar los directorios de usuario.
   * Configuración de IDP.
* Administrador de AEM:
   * Administrar grupos locales, permisos y privilegios.

### 3. Incorporar usuarios y administrar el acceso en Admin Console:

![processoverview3.jpg](assets/processOverview3.jpg)

Tres métodos para incorporar usuarios, según el tamaño y la preferencia:
* Crear usuarios manualmente en Admin Console
* Cargar archivo .csv
* Sincronizar usuarios de Enterprise Active Directory

### 4. El administrador configura la organización y concede a los usuarios y grupos acceso a los entornos

## Ayuda y recursos

* [Primer inicio de sesión: Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [Configurar el acceso a AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=es#accessing)
