---
title: 'Información general sobre los resultados de la prueba: Cloud Services'
description: 'Información general sobre los resultados de la prueba: Cloud Services'
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 16%

---


# Información general {#overview}

Las ejecuciones de canalizaciones de Cloud Manager para Cloud Services admitirán la ejecución de pruebas que se ejecuten con el entorno de ensayo. Esto contrasta con las pruebas que se ejecutan durante el paso Generar y Prueba de unidades que se ejecutan sin conexión, sin acceso a ningún entorno de AEM en ejecución.

Existen tres categorías generales de pruebas admitidas por Cloud Manager for Cloud Services Pipeline:

1. [Prueba de calidad del código](/help/implementing/cloud-manager/code-quality-testing.md)
1. [Prueba funcional](/help/implementing/cloud-manager/functional-testing.md)
1. [Prueba de auditoría de contenido](/help/implementing/cloud-manager/content-audit-testing.md)

Estas pruebas pueden ser:

* Escrito por el cliente
* Escrito en Adobe
* Herramienta de código abierto (con tecnología Lighthouse de Google)

   >[!NOTE]
   > Tanto las pruebas escritas por el cliente como las pruebas por Adobe se ejecutan en una infraestructura de contenedores diseñada para ejecutar estos tipos de pruebas.

