---
title: 'Introducción a los programas de espacio aislado '
description: 'Introducción a los programas de espacio aislado '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introducción a los Programas de Sandbox {#sandbox-programs}

## Introducción {#introduction}

Un programa de espacio aislado es uno de los dos tipos de programas disponibles en AEM Cloud Service, mientras que el otro es un programa de producción.

Un Simulador para pruebas (Sandbox) se suele crear para servir a los fines de capacitación, administración de demostraciones, habilitación o prueba de concepto (POC). No están pensados para transportar tráfico en directo. No están sujetos al [AEM como compromisos de Cloud Service](https://www.adobe.com/legal/service-commitments.html).

Los entornos creados en un Simulador para pruebas no están configurados para el escalado automático. Por lo tanto, estos entornos no son adecuados para pruebas de carga o rendimiento.

Los programas de espacio aislado incluyen Sites y Assets y se rellenan automáticamente con un repositorio de Git, un entorno de desarrollo y una canalización que no es de producción.  El repositorio de Git se rellena con un proyecto de muestra basado en el tipo de archivo del proyecto AEM.

Consulte [Explicación de los programas y tipos de programas](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md) para obtener más información sobre los tipos de programas.

### Atributos de los programas de Sandbox {#attributes-sandbox}

Los Programas del Simulador para pruebas tienen los siguientes atributos:

1. **Creación de programas:**  la creación del programa de espacio aislado incluye:
   * configuración del proyecto con código de muestra y contenido
   * creación de un entorno de desarrollo
   * creación de canalización que no es de producción que se implementa en el entorno de desarrollo (implementación de la rama maestra en el entorno de desarrollo)

1. **Soluciones:** los programas de espacio aislado incluyen AEM Sites y Recursos.

1. **AEM actualizaciones:** AEM las actualizaciones se pueden aplicar manualmente a los entornos de un programa de espacio aislado para pruebas y no se insertan automáticamente.
Consulte [AEM Actualizaciones a entornos de espacio aislado](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) para obtener más información.

1. **Hibernación:** los entornos de un programa de espacio aislado hibernan automáticamente si no se detecta ninguna actividad durante un período de tiempo determinado. Los entornos en hibernación se pueden anular de hibernación manualmente.
Consulte [Entorno de espacio aislado en hibernación y dehibernación](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) para obtener más información.