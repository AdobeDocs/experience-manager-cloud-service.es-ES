---
title: Integración de [!DNL Experience Manager Assets] con  [!DNL Adobe Workfront]
description: Introducción a la integración entre  [!DNL Assets] y [!DNL Workfront]
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager] como una integración de [!DNL Cloud Service] [!DNL Assets] con [!DNL Adobe Workfront] {#assets-integration-overview}

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

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad del contenido y el tiempo de salida al mercado, conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

Adobe ofrece [integrar [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] de forma nativa (compatible con Assets Essentials y Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=es).

Con la integración nativa de Experience Manager, puede:

* Configure rápidamente la integración dentro de Workfront.

* Cree automáticamente carpetas vinculadas entre Workfront y Experience Manager.

* Sincronice fácilmente los metadatos de los recursos vinculados existentes.

* Actualizar automáticamente los metadatos del proyecto cuando se modifiquen en Workfront.

* Conecte sin problemas varios repositorios de Experience Manager Assets a un entorno de Workfront o varios entornos de Workfront a un repositorio de Experience Manager Assets en los ID de organización.


## Conector mejorado de Adobe Workfront para Experience Manager {#enhanced-connector-information}


A partir de junio de 2022, Adobe lanzó una nueva integración nativa para conectar Workfront con Adobe Experience Manager Assets as a Cloud Service. Esta integración se ha convertido en el método requerido para conectar estas dos soluciones. Cualquier nueva implementación futura del conector mejorado (1.9.8 y posterior) para conectar Workfront con AEM Assets as a Cloud Service está bloqueada. Para obtener más información sobre cómo configurar esta integración, consulte [Configuración de la integración de Experience Manager Assets as a Cloud Service](workfront-connector-configure.md).

>[!NOTE]
>
>Adobe no admite el uso del conector mejorado de Workfront para Experience Manager y la integración de Experience Manager en paralelo.

Para instalaciones anteriores a junio de 2022, los siguientes son algunos puntos que hay que tener en cuenta para la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* Adobe requiere la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
* Adobe puede publicar actualizaciones para [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hagan redundante este conector; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones mejoradas de instalación del conector](workfront-connector-install.md).
* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información sobre el examen, consulte [Guía para exámenes](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).