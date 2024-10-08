---
title: Integración de Content Credentials
description: Los contentes credentials, integrados en AEM Assets y presentados en la vista de Assets, pueden ofrecer contexto sobre el historial de un recurso, incluido cómo se creó y quién participó en su creación. Al igual que una etiqueta nutricional para el contenido digital, los Contentes credentials pueden ayudar a aumentar la transparencia y generar confianza con las audiencias.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Credenciales de contenido {#content-credentials}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación para desarrolladores de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

Las marcas están más preocupadas que nunca por la transparencia del contenido, la divulgación de la inteligencia artificial y la prevención de la manipulación de activos. La Iniciativa de autenticidad de contenido (CAI) del Adobe crea herramientas que cumplen con el estándar técnico de la [Coalición para la procedencia y autenticidad de contenido](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). Los contentes credentials, que son un nuevo tipo de metadatos cifrados y a prueba de manipulaciones, pueden ayudar a los espectadores a comprender el linaje del contenido y garantizar la integridad de los recursos de la marca. Pueden incluir una amplia gama de datos de procedencia que ofrecen una perspectiva del historial de un recurso digital.

Esta información puede incluir:

* **Emisor o firmante:** Información acerca de la entidad o compañía que emitió la firma digital para certificar los certificados o firmas del recurso.
* **Fecha del problema:** Fecha en la que se aplicó Content Credential al recurso.
* **Crédito y uso:** Información sobre el productor del recurso, incluidos el nombre, los identificadores de medios sociales u otra información relacionada con la identidad.
* **Proceso:** Registra las ediciones o modificaciones realizadas en el recurso.
* **Detalles del dispositivo:** Información sobre la aplicación o el dispositivo usado para crear o editar el recurso.
* **Herramienta de IA utilizada:** Si se utilizó IA generativa para editar o crear el recurso, se puede incluir el nombre del modelo utilizado.
* **Otra información relevante:** También se pueden incluir datos adicionales para ayudar a ofrecer más contexto sobre el historial de un recurso.

Para obtener una vista completa, [Verify](https://contentcredentials.org/verify) puede ofrecer una perspectiva más completa del historial de recursos.

Adobe Experience Manager Assets ahora es compatible con los Contentes credentials, lo que permite a los usuarios ver los Contentes credentials directamente en la vista de Assets AEM de los usuarios de la vista de la vista de la vista de la vista de la vista de la. Al observar los detalles del recurso, cualquier imagen con Contentes credentials (como las creadas con los servicios GenAI) muestra los detalles del manifiesto en un panel específico. Si el recurso se descarga, publica o comparte, los Contentes credentials permanecen intactos con el recurso.

![recursos](/help/assets/assets/content-credentials.png)

## Contentes credentials de acceso {#access-content-credentials}

1. Vaya a la interfaz de usuario de la vista Assets y haga clic en **Assets** en el panel izquierdo.
1. Vaya a una carpeta y seleccione el recurso que desee.
1. Haga clic en **Detalles** y seleccione `Cr pin` en el panel situado más a la derecha. La pestaña Contentes credentials muestra la siguiente información sobre el recurso.
   1. **Imagen generada:** Fecha y hora de aplicación de los Contentes credentials.
   1. **Resumen de contenido:** Indica si AI ha generado el recurso parcial o totalmente, o cómo se ha editado.
      ![contentes credentials](/help/assets/assets/content-credentials1.png)
   1. **Proceso:** detalla la aplicación, el dispositivo y la herramienta de IA (como el Adobe Firefly) que se usó para generar el recurso, así como los cambios realizados posteriormente.
      ![proceso](/help/assets/assets/CR-Process.png)
   1. **Acerca de estos Contentes credentials:** Nombre del emisor junto con la fecha y hora de emisión.
      ![emisor](/help/assets/assets/CR-issuer.png)
