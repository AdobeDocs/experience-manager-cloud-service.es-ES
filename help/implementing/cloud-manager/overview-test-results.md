---
title: Información general sobre las pruebas de Cloud Manager
description: Obtenga información general sobre los tres tipos de pruebas que Cloud Manager ejecuta automáticamente para garantizar la calidad del código personalizado.
exl-id: 5f5c97b1-4180-4f49-af8b-257d4744766e
source-git-commit: a9303c659730022b7417fc9082dedd26d7cbccca
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 100%

---


# Información general sobre las pruebas de Cloud Manager {#overview}

Existen tres categorías de pruebas compatibles con las canalizaciones de Cloud Manager para Cloud Services.

1. [Prueba de calidad del código](/help/implementing/cloud-manager/code-quality-testing.md)

   * Las pruebas de calidad del código evalúan la calidad del código de la aplicación.
   * La canalización de la calidad del código se ejecuta inmediatamente después del paso de generación en todas las canalizaciones que sean y no sean de producción.
   * Las [reglas de calidad del código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md) que ejecuta Cloud Manager se crean en función de las prácticas recomendadas de AEM Engineering.

1. [Pruebas funcionales](/help/implementing/cloud-manager/functional-testing.md)

   * Las pruebas funcionales forman parte de la fase de prueba de una canalización de producción.

1. [Pruebas de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md)

   * Las pruebas de auditoría de experiencia están habilitadas en todas las canalizaciones de producción de Cloud Manager y no se pueden omitir.

Estas pruebas pueden ser:

* Escritas por el cliente
* Escritas por Adobe
* Creadas con herramientas de código abierto

>[!NOTE]
>
> Tanto las pruebas escritas por el cliente como las escritas por Adobe se ejecutan en una infraestructura de contenedores diseñada para ejecutar dichas pruebas.
