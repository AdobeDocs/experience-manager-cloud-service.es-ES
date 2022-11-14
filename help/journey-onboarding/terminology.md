---
title: Terminología de AEM as a Cloud Service
description: Antes de iniciar sesión en AEMaaCS, es útil conocer parte de la terminología del sistema y su estructura básica.
exl-id: d02776a7-836a-4894-a5d5-ae88cc7e4e76
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 100%

---

# Terminología de AEM as a Cloud Service {#terminology}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá parte de la terminología de AEM as a Cloud Service y su estructura básica.

## Objetivo {#objective}

Ahora que comprende lo que ha llevado al proceso de incorporación al leer el documento [Preparar la incorporación,](preparation.md) es útil conocer parte de la terminología del sistema y su estructura básica antes de iniciar sesión.

AEM as a Cloud Service es una herramienta potente y flexible y para utilizar cualquier herramienta, debe estar familiarizado con su organización, la terminología y el lenguaje que se usa para describirla. Este documento resume algunos términos clave que debe comprender antes de comenzar a utilizar el sistema.

Tras leer este documento, comprenderá lo siguiente:

* Las diferentes capas que componen AEMaaCS.
* Conceptos básicos de lo que hace cada capa.

## Estructura de AEMaaCS {#structure}

A los efectos del presente recorrido de incorporación, no es necesario comprender plenamente la estructura de AEM as a Cloud Service. Sin embargo, estar familiarizado con los siguientes conceptos hará que sea más fácil seguirlos más adelante en el recorrido.

![Estructura de Cloud Manager](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **INQUILINO**: cada cliente está aprovisionado con un inquilino. Un inquilino también se denomina organización de IMS (más información sobre IMS más adelante en este recorrido)
* **PROGRAMAS**: cada inquilino tiene uno o más programas, que a menudo reflejan las soluciones con licencia del cliente.
* **ENTORNOS**: cada programa tiene múltiples entornos, como producción para contenido en directo, uno para ensayo y otro para desarrollo.
* **REPOSITORIO**: los entornos tienen repositorios Git donde se mantiene el código de la aplicación y del front-end.
* **HERRAMIENTAS Y FLUJOS DE TRABAJO**: las canalizaciones administran la implementación de código desde los repositorios a los entornos.

Un ejemplo suele ser útil para contextualizar esta jerarquía.

* Las empresas de viajes y aventura de WKND pueden ser un **inquilino** que se centra en medios relacionados con viajes.
* El inquilino de WKND Travel and Adventure Enterprises puede tener dos **programas**:
   * Un programa de One Sites para su división WKND Magazine
   * Un programa de Assets para la división WKND Media
* Los programas de WKND Magazine y WKND Media tendrían **entornos** de desarrollo, ensayo y producción.
* **Los repositorios** se utilizan para mantener el código personalizado y las aplicaciones para WKND Magazine y WKND Media.
* Varios **herramientas y flujos de trabajo** trabajan en todos los repositorios para implementar código mediante canalizaciones de CI/CD, registros de acceso, acceso de AEM, etc.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de incorporación de AEM, debería comprender lo siguiente:

* Las diferentes capas que componen AEMaaCS.
* Conceptos básicos de lo que hace cada capa.

Aproveche este conocimiento y continúe con su recorrido de incorporación de AEM al leer el documento [Acceso a Admin Console](admin-console.md), donde aprenderá a acceder a la consola y a verificar su estado como administrador del sistema.
