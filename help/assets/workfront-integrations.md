---
title: '[!DNL Experience Manager Assets] integración con [!DNL Adobe Workfront]'
description: Introducción a la integración entre [!DNL Assets] y [!DNL Workfront]
role: Admin,Leader,Architect
feature: Integrations
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: f295eead13bcdeed910ae6b8c82373e2b70f1224
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] integración con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | Este artículo |

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad del contenido y el tiempo de salida al mercado conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

ofertas de Adobe a [integrar [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] de forma nativa (compatible con Assets Essentials y Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html).

Con la integración nativa de Experience Manager, puede:

* Configure rápidamente la integración dentro de Workfront.

* Crea automáticamente carpetas vinculadas entre Workfront y Experience Manager.

* Sincronice fácilmente los metadatos de los recursos vinculados existentes.

* Actualizar automáticamente los metadatos del proyecto cuando se modifiquen en Workfront.

* Conecte sin problemas varios repositorios de Experience Manager Assets a un entorno de Workfront o varios entornos de Workfront a un repositorio de Experience Manager Assets en los ID de organización.


## Conector mejorado de Adobe Workfront para Experience Manager {#enhanced-connector-information}


A partir de junio de 2022, Adobe lanzó una nueva integración nativa para conectar Workfront con Adobe Experience Manager Assets as a Cloud Service. Esta integración se ha convertido en el método requerido para conectar estas dos soluciones. Cualquier nueva implementación futura del conector mejorado (1.9.8 y posterior) para conectar Workfront con AEM Assets as a Cloud Service está bloqueada. Para obtener más información sobre cómo configurar esta integración, consulte [Configuración de la integración as a Cloud Service de Experience Manager Assets](workfront-connector-configure.md).

>[!NOTE]
>
>El Adobe no admite el uso del conector mejorado de Workfront para Experience Manager y la integración de Experience Manager en paralelo.

Para las instalaciones anteriores a junio de 2022, los siguientes son algunos puntos a tener en cuenta para la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector]:

* El Adobe requiere la implementación y la configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con el Adobe.
* El Adobe puede publicar actualizaciones en [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hacen que este conector sea redundante; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
* El Adobe admite las versiones de conector mejoradas 1.7.4 y posteriores. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, consulte el paso 5(a) de [instrucciones de instalación del conector mejorado](workfront-connector-install.md).
* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener más información sobre el examen, consulte [Guía del examen](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).