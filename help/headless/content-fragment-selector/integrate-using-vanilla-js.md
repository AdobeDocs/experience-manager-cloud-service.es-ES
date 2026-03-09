---
title: Integración del selector de fragmentos de contenido mediante Vanilla JS
description: Integre el selector de fragmentos de contenido con varias aplicaciones de Adobe, que no sean de Adobe y de terceros.
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# Integración del selector de fragmentos de contenido mediante Vanilla JS {#integrate-content-fragment-selector-using-vanilla-js}

Puede integrar cualquier aplicación de Adobe o que no sea Adobe con el repositorio de Adobe Experience Manager (AEM) as a Cloud y seleccionar fragmentos de contenido desde esa aplicación.

La integración se realiza importando el paquete Selector de fragmentos de contenido y conectándose a AEM as a Cloud Service mediante la biblioteca de JavaScript de vainilla. Edite un `index.html` o cualquier archivo apropiado dentro de su aplicación para:

* Definición de los detalles de autenticación
* Acceso al repositorio de AEM as a Cloud Service
* Configurar las propiedades de visualización del Selector de fragmentos de contenido

Puede realizar la autenticación sin definir algunas de las propiedades de IMS, si:

* está integrando una aplicación de Adobe en [Unified Shell](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell)
* ya se ha generado un token de IMS para la autenticación
