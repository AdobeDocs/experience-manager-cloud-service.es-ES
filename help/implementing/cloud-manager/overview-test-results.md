---
title: 'Información general sobre los resultados de la prueba: Cloud Services'
description: 'Información general sobre los resultados de la prueba: Cloud Services'
translation-type: tm+mt
source-git-commit: b3548e3920fed45f6d1de54a49801d3971aa6bba
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Información general {#overview}

Existen tres categorías generales de pruebas admitidas por Cloud Manager for Cloud Services Pipeline:

1. [Prueba de calidad del código](/help/implementing/cloud-manager/code-quality-testing.md)

   La prueba de calidad del código evalúa la calidad del código de la aplicación. El flujo de calidad del código se ejecuta inmediatamente después del paso de generación en todos los gasoductos que no sean de producción y producción.

   Las reglas [de calidad de código](/help/implementing/cloud-manager/custom-code-quality-rules.md) personalizado ejecutadas por Cloud Manager se crean en función de las prácticas recomendadas de ingeniería de AEM.

1. [Prueba funcional](/help/implementing/cloud-manager/functional-testing.md)

   La prueba funcional forma parte de la fase de prueba de una canalización de producción.

1. [Prueba de auditoría de contenido](/help/implementing/cloud-manager/content-audit-testing.md)

   La prueba de auditoría de contenido está habilitada en todas las tuberías de producción de Cloud Manager y no se puede omitir.

Estas pruebas pueden ser:

* Escrito por el cliente
* Escrito en Adobe
* Herramienta de código abierto

   >[!NOTE]
   > Tanto las pruebas escritas por el cliente como las pruebas por Adobe se ejecutan en una infraestructura de contenedores diseñada para ejecutar estos tipos de pruebas.

