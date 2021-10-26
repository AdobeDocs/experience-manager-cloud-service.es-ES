---
title: 'Introducción a los programas de espacio aislado '
description: Introducción a los programas de espacio aislado
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1892900ea3f365e1b5f7d31ffae64d45256d2a3a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Introducción a los programas de espacio aislado {#sandbox-programs}

## Introducción {#introduction}

Un programa de espacio aislado es uno de los dos tipos de programas disponibles en AEM Cloud Service, mientras que el otro es un programa de producción.

Un Simulador para pruebas (Sandbox) se suele crear para servir a los fines de capacitación, administración de demostraciones, habilitación o prueba de concepto (POC). No están pensados para transportar tráfico en directo. No están sujetos al [AEM compromisos as a Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Los entornos creados en un Simulador para pruebas no están configurados para el escalado automático. Por lo tanto, estos entornos no son adecuados para pruebas de carga o rendimiento.

Los programas de espacio aislado incluyen [!DNL Sites] y [!DNL Assets] y se rellenan automáticamente con un repositorio de Git, un entorno de desarrollo y una canalización que no es de producción.  El repositorio de Git se rellena con un proyecto de muestra basado en el tipo de archivo del proyecto AEM.

>[!IMPORTANT]
>Un programa de espacio aislado solo tendrá un entorno de desarrollo.

>[!NOTE]
>Los dominios personalizados y las Listas de permitidos IP no están disponibles en los programas de simulación de pruebas.

Consulte [Explicación de programas y tipos de programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=en) para obtener más información sobre los tipos de programa.

### Atributos de los programas de Simulador para pruebas {#attributes-sandbox}

Los Programas del Simulador para pruebas tienen los siguientes atributos:

1. **Creación de programas:** La creación del programa de espacio aislado incluye:
   * configuración del proyecto con código de muestra y contenido
   * creación de un entorno de desarrollo
   * creación de canalización que no es de producción que se implementa en el entorno de desarrollo (implementación de la rama maestra en el entorno de desarrollo)

1. **Soluciones:** Los programas de espacio aislado incluyen AEM [!DNL Sites] y [!DNL Assets].

1. **AEM actualizaciones:** AEM actualizaciones se pueden aplicar manualmente a entornos en un programa de espacio aislado para pruebas y no se insertan automáticamente.
Consulte [AEM actualizaciones en entornos de espacio aislado](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) para obtener más información.

1. **Hibernación:** Los entornos de un programa de espacio aislado hibernan automáticamente si no se detecta ninguna actividad durante un período de tiempo determinado. Los entornos limitados se colocan en un nodo de hibernación después de 8 horas de inactividad, tras las cuales se puede anular la hibernación. Los entornos en hibernación se pueden anular de hibernación manualmente.
Consulte [Entornos de espacio aislado en hibernación y dehibernación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) para obtener más información.

1. **Eliminación**: Los entornos limitados se eliminan después de 6 meses de estar en modo de hibernación continua, después de lo cual se pueden volver a crear.
