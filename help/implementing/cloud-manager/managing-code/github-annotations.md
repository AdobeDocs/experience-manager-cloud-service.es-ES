---
title: Anotaciones de comprobación de GitHub
description: Descubra cómo GitHub comprueba las PR de anotación de sus repositorios privados para proporcionarle comentarios útiles.
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 'null'
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 52%

---


# Anotaciones de comprobación de GitHub {#github-annotations}

Descubra cómo GitHub comprueba las PR de anotación de sus repositorios privados para proporcionarle comentarios útiles.

## Información general {#overview}

Si está utilizando [repositorios privados](private-repositories.md) para su programa Cloud Manager, las comprobaciones en GitHub se ejecutan automáticamente para cada solicitud de extracción. Estas PR incluyen información útil para ayudarle a comprender los problemas con su código lo antes posible.

![Ejemplo de anotaciones de comprobación de GitHub](assets/github-check-annotations.png)

Los problemas de [calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) detectados por [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) se enumeran claramente.

![Ejemplo de anotación de problema de código](assets/github-check-annotations-example.png)

Se proporciona la línea de código exacta con el problema y puede seleccionarla para mostrar el código correspondiente. Estas anotaciones cubren problemas de código, no solo los de la solicitud de extracción.

![Ejemplo de anotación de problema de código](assets/github-check-annotations-example-code.png)

Todas las líneas anotadas se añaden a la pestaña **Archivos modificados** en la solicitud de extracción de GitHub. Las anotaciones para archivos de solicitud de extracción no modificados aparecen en su propia sección.

![Ejemplo de anotaciones en la pestaña de archivos modificados](assets/github-check-annotations-files-changed.png)

## Código de calidad de las canalizaciones {#code-quality-pipelines}

Los resultados de [calidad del código](/help/implementing/cloud-manager/code-quality-testing.md) también están visibles en la canalización que Cloud Manager almacena automáticamente en déclencheur en la parte inferior de la pestaña **Comprobaciones**. También se puede acceder a él desde los **detalles** de la comprobación de la solicitud de extracción.

![Ejemplo de anotaciones](assets/github-check-annotations-code-quality.png)

![Ejemplo de anotaciones](assets/github-check-annotations-code-quality-2.png)

También puede visualizar los problemas en formato CSV. Puede recuperar este CSV [viendo los detalles de la ejecución de la canalización en Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details).
