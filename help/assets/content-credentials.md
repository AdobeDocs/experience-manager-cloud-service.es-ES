---
title: Integración de Content Credentials
description: Content Credentials, integrado en los AEM Assets y destacado en la vista de Assets, puede ofrecer contexto sobre el historial de un recurso, incluido cómo se creó y quién participó en su creación. Al igual que una etiqueta nutricional para el contenido digital, Content Credentials puede ayudar a aumentar la transparencia y generar confianza con las audiencias.
role: User
exl-id: 27c25ae0-4477-40c3-85c8-3e0aa725aba7
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# Content Credentials {#content-credentials}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Las marcas están más preocupadas que nunca por la transparencia del contenido, la divulgación de la inteligencia artificial y la prevención de la manipulación de activos. La Iniciativa de autenticidad de contenido (CAI) de Adobe crea herramientas que cumplen con el estándar técnico de la [Coalición para la procedencia y autenticidad de contenido](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA). Content Credentials, un nuevo tipo de metadatos cifrados y a prueba de manipulaciones, puede ayudar a los espectadores a comprender el linaje del contenido y garantizar la integridad de los activos de la marca. Pueden incluir una amplia gama de datos de procedencia que ofrecen una perspectiva del historial de un recurso digital.

Esta información puede incluir:

* **Emisor o firmante:** Información acerca de la entidad o compañía que emitió la firma digital para certificar los certificados o firmas del recurso.
* **Fecha del problema:** Fecha en la que se aplicó Content Credential al recurso.
* **Crédito y uso:** Información sobre el productor del recurso, incluidos el nombre, los identificadores de medios sociales u otra información relacionada con la identidad.
* **Proceso:** Registra las ediciones o modificaciones realizadas en el recurso.
* **Detalles del dispositivo:** Información sobre la aplicación o el dispositivo usado para crear o editar el recurso.
* **Herramienta de IA utilizada:** Si se utilizó IA generativa para editar o crear el recurso, se puede incluir el nombre del modelo utilizado.
* **Otra información relevante:** También se pueden incluir datos adicionales para ayudar a ofrecer más contexto sobre el historial de un recurso.

Para obtener una vista completa, [Verify](https://contentcredentials.org/verify) puede ofrecer una perspectiva más completa del historial de recursos.

Adobe Experience Manager Assets ahora es compatible con Content Credentials, lo que permite a los usuarios ver Content Credentials directamente en la vista de Assets de AEM. Al observar los detalles del recurso, cualquier imagen con Content Credentials (como las creadas con los servicios GenAI) muestra los detalles del manifiesto en un panel dedicado. Si el recurso se descarga, publica o comparte, Content Credentials permanece intacto con el recurso.

![recursos](/help/assets/assets/content-credentials.png)

## Acceso a Content Credentials {#access-content-credentials}

1. Vaya a la interfaz de usuario de la vista Assets y haga clic en **Assets** en el panel izquierdo.
1. Vaya a una carpeta y seleccione el recurso que desee.
1. Haga clic en **Detalles** y seleccione `Cr pin` en el panel situado más a la derecha. La pestaña Content Credentials muestra la siguiente información sobre el recurso.
   1. **Imagen generada:** Fecha y hora en que se aplicó Content Credentials.
   1. **Resumen de contenido:** Indica si AI ha generado el recurso parcial o totalmente, o cómo se ha editado.

      ![credenciales de contenido](/help/assets/assets/content-credentials1.png)
   1. **Proceso:** detalla la aplicación, el dispositivo y la herramienta de IA (como Adobe Firefly) utilizados para generar el recurso, así como los cambios realizados posteriormente.

      ![proceso](/help/assets/assets/CR-Process.png)
   1. **Acerca de este Content Credentials:** Nombre del emisor junto con la fecha y hora de emisión.

      ![emisor](/help/assets/assets/CR-issuer.png)
