---
title: Pruebas funcionales
description: Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el proceso de implementación de AEM as a Cloud Service para garantizar la calidad y fiabilidad de su código.
exl-id: 7eb50225-e638-4c05-a755-4647a00d8357
source-git-commit: 7d15440159a8e24314753acd5b37fcd2c5e8ec4c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 83%

---


# Pruebas funcionales {#functional-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_functionaltesting"
>title="Pruebas funcionales"
>abstract="Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el proceso de implementación de AEM as a Cloud Service para garantizar la calidad y fiabilidad de su código."

Obtenga información sobre los tres tipos diferentes de pruebas funcionales integradas en el [proceso de implementación de AEM as a Cloud Service](/help/implementing/cloud-manager/deploy-code.md) para garantizar la calidad y fiabilidad de su código.

## Ámbito

El propósito de los pasos de prueba funcional en la canalización de Cloud Manager es garantizar que la funcionalidad esencial de la aplicación funcione según lo esperado.

Esta fase de prueba es el último nivel de prueba automatizada antes de implementar el código en producción.

Las pruebas funcionales no deben reemplazar, sino complementar y ampliar otras estrategias de prueba, como las pruebas de unidades, las pruebas de integración o las pruebas funcionales realizadas fuera de la ejecución de la canalización en Cloud Manager.

## Información general {#overview}

Hay tres tipos diferentes de pruebas funcionales en AEM as a Cloud Service.

* [Prueba funcional del producto](#product-functional-testing)
* [Prueba funcional personalizada](#custom-functional-testing)
* [Prueba de IU personalizada](#custom-ui-testing)

Para todas las pruebas funcionales, los resultados detallados de las pruebas pueden descargarse como un `.zip` archivo mediante el botón **Descargar registro de generación** en la pantalla de información general de la generación como parte del [proceso de implementación.](/help/implementing/cloud-manager/deploy-code.md)

Estos registros no incluyen los registros del proceso del tiempo de ejecución de AEM real. Para acceder a esos registros, consulte el documento [Acceder y administrar registros](/help/implementing/cloud-manager/manage-logs.md) para obtener más información.

Tanto las pruebas funcionales del producto como las pruebas funcionales personalizadas de ejemplo se basan en la los [clientes de prueba de AEM.](https://github.com/adobe/aem-testing-clients)

### Prueba funcional del producto {#product-functional-testing}

Las pruebas funcionales del producto son un conjunto de pruebas de integración (TI) HTTP estables de funcionalidad central en AEM como las tareas de creación y replicación. Estas pruebas las mantiene Adobe y su objetivo es evitar que se implementen cambios en el código de aplicación personalizado si rompen la funcionalidad principal.

* [Canalizaciones de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md): pruebas funcionales del producto que se ejecutan automáticamente cada vez que implementa un código nuevo en Cloud Manager y no se pueden omitir.
* [Canalizaciones que no son de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md): las pruebas funcionales de producto se pueden seleccionar de forma opcional para que se ejecuten, siempre que ejecute la canalización que no sea de producción.

Las pruebas funcionales del producto se mantienen como un proyecto de código abierto. Consulte [pruebas funcionales del producto](https://github.com/adobe/aem-test-samples/tree/aem-cloud/smoke) en GitHub para obtener más información.

### Prueba funcional personalizada {#custom-functional-testing}

Aunque la prueba funcional del producto está definida por Adobe, puede escribir sus propias pruebas de calidad para su propia aplicación. Esto se ejecutará como prueba funcional personalizada como parte de la [canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) o una [canalización que no sea de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) para garantizar la calidad de la aplicación.

Las pruebas funcionales personalizadas se ejecutan tanto para implementaciones de código personalizado como para actualizaciones push, lo que hace especialmente importante escribir buenas pruebas funcionales que eviten que los cambios en el código de AEM rompan el código de la aplicación. El paso de prueba funcional personalizada siempre está presente y no se puede omitir.

Consulte la [Pruebas funcionales de Java](/help/implementing/cloud-manager/java-functional-testing.md) para obtener más información.


### Prueba de IU personalizada {#custom-ui-testing}

La prueba de IU personalizada es una característica opcional que le permite crear y ejecutar automáticamente pruebas de IU para sus aplicaciones. Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de lenguajes y marcos de trabajo como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium.

Consulte la [Pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md#custom-ui-testing) para obtener más información.

