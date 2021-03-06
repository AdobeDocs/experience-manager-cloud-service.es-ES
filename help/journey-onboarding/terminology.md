---
title: Terminología as a Cloud Service AEM
description: Antes de iniciar sesión en AEMaaCS, es útil conocer parte de la terminología del sistema y su estructura básica.
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 18%

---


# Terminología as a Cloud Service AEM {#terminology}

En esta parte del [recorrido de incorporación,](overview.md) aprenderá parte de la terminología de AEM as a Cloud Service y su estructura básica.

## Objetivo {#objective}

Ahora que comprende lo que ha llevado al proceso de incorporación leyendo el documento [Preparación de la incorporación,](preparation.md) es útil conocer parte de la terminología del sistema y su estructura básica antes de iniciar sesión.

AEM as a Cloud Service es una herramienta potente y flexible y para utilizar cualquier herramienta que debería estar familiarizado con su organización y la terminología y el lenguaje usado para describirla. Este documento resume algunos términos clave que debe comprender antes de comenzar a utilizar el sistema.

Tras leer este documento, comprenderá:

* Las diferentes capas que componen AEMaaCS.
* Conceptos básicos de lo que hace cada capa.

## Estructura de AEMaaCS {#structure}

A los efectos del presente recorrido de incorporación, no es necesario comprender plenamente la estructura de AEM as a Cloud Service. Sin embargo, la familiaridad con los siguientes conceptos hará que sea más fácil seguirlos más adelante en el recorrido.

![Estructura de Cloud Manager](/help/journey-sites/quick-site/assets/cloud-manager-structure.png)

* **INQUILINO**: cada cliente está aprovisionado con un inquilino. Un inquilino también se denomina organización de IMS (más información sobre IMS más adelante en este recorrido)
* **PROGRAMAS**: cada inquilino tiene uno o más programas, que a menudo reflejan las soluciones con licencia del cliente.
* **ENTORNOS**: cada programa tiene múltiples entornos, como producción para contenido en directo, uno para ensayo y otro para desarrollo.
* **REPOSITORIO** - Los entornos tienen uno o más repositorios Git donde se mantiene el código de la aplicación y del front-end.
* **HERRAMIENTAS Y FLUJOS DE TRABAJO**: las canalizaciones administran la implementación de código desde los repositorios a los entornos.

Un ejemplo suele ser útil para contextualizar esta jerarquía.

* Las empresas de viajes y aventura de WKND pueden ser un **inquilino** que se centra en medios relacionados con viajes.
* El inquilino de WKND Travel and Adventure Enterprises puede tener dos **programas**:
   * Programa One Sites para su división WKND Magazine
   * Un programa de activos para la división WKND Media
* Los programas WKND Magazine y WKND Media tendrían desarrollo, ensayo y producción **entornos**.
* **Repositorios** se utilizan para mantener el código personalizado y las aplicaciones para WKND Magazine y WKND Media.
* Varios **herramientas y flujos de trabajo** trabaje en todas las repositorios para implementar código usando canalizaciones CI/CD, registros de acceso, AEM de acceso, etc.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de AEM de incorporación, debe comprender:

* Las diferentes capas que componen AEMaaCS.
* Conceptos básicos de lo que hace cada capa.

Aproveche este conocimiento y continúe con su recorrido de incorporación AEM leyendo el documento [Acceso al Admin Console](admin-console.md), donde aprenderá a acceder a la consola y a verificar su estado como administrador del sistema.
