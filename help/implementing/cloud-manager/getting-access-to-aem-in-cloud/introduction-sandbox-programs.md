---
title: 'Introducción a los programas de espacio aislado '
description: Descubra cuáles son las diferencias entre los programas de simulación de pruebas y los programas de producción.
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: b74a0dbb1c9fdb74941f7b71bed9215853b63666
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Introducción a los programas de espacio aislado {#sandbox-programs}

Descubra cuáles son las diferencias entre los programas de simulación de pruebas y los programas de producción.

## Introducción {#introduction}

Un programa de simulación de pruebas se suele crear para servir a los fines de formación, ejecución de demostraciones, habilitación o prueba de conceptos (POC) y, por lo tanto, no están pensados para transportar tráfico en directo.

Un programa de simulación de pruebas es uno de los dos tipos de programas disponibles en AEM Cloud Service, siendo el otro un [programa de producción.](introduction-production-programs.md) Consulte el documento [Explicación de programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obtener más información sobre los tipos de programas.

## Creación automática {#auto-creation}

Los programas de espacio aislado incluyen la creación automática. Siempre que cree un nuevo programa de espacio aislado, Cloud Manager automáticamente:

* Añade AEM Sites y AEM Assets como soluciones en su programa.
* Establece un repositorio de Git de proyecto con un proyecto de ejemplo basado en la variable [AEM tipo de archivo del proyecto.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* Crea un entorno de desarrollo.
* Crea una canalización que no es de producción y se implementa en el entorno de desarrollo.

Un programa de simulación de pruebas solo tendrá un entorno de desarrollo.

## Limitaciones y condiciones {#limitations}

Debido a que no están pensados para el tráfico en directo, los programas de entornos limitados tienen ciertas limitaciones y condiciones de uso, lo que los diferencia de los programas de producción.

### Sin tráfico activo {#live-traffic}

Los programas de espacio aislado no están pensados para transportar tráfico en directo y, por lo tanto, no están sujetos a [AEM Compromisos as a Cloud Service.](https://www.adobe.com/legal/service-commitments.html)

### Sin escalado automático {#auto-scaling}

Los entornos creados en un programa de simulación de pruebas no están configurados para el escalado automático. Por lo tanto, estos entornos no son adecuados para pruebas de carga o rendimiento.

### Sin dominios personalizados ni Listas de permitidos IP {#ip-allow}

Los dominios personalizados y las listas de permitidos IP no están disponibles en los programas de entornos limitados.

### Actualizaciones AEM manuales {#updates}

AEM actualizaciones no se insertan automáticamente en los programas de simulación de pruebas, pero se pueden aplicar manualmente a los entornos del programa de simulación de pruebas.

* Una actualización manual solo se puede ejecutar cuando el entorno de destino tiene una canalización configurada correctamente.
* Una actualización manual de un entorno de ensayo o producción actualizará automáticamente el otro. El conjunto de entornos Producción+Fase debe estar en la misma versión de AEM.

Consulte el documento [AEM actualizaciones de la versión](/help/implementing/deploying/aem-version-updates.md) para obtener más información.

Consulte el documento [Actualización del entorno](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment) para aprender a actualizar un entorno.

### Hibernación y eliminación {#hibernation}

Los entornos de un programa de simulación de pruebas hibernan automáticamente después de 8 horas de inactividad. Una vez hibernados, se pueden anular manualmente la hibernación.

Los programas de espacio aislado se eliminan después de 6 meses de estar en modo de hibernación continua, después de lo cual se pueden volver a crear.

Consulte [Entornos de espacio aislado en hibernación y dehibernación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-environments.md) para obtener más información.
