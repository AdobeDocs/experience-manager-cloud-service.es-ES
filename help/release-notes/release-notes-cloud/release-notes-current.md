---
title: Notas de la versión de 2020.8.0 [!DNL Adobe Experience Manager] de Cloud Service.
description: '[!DNL Adobe Experience Manager] como Cloud Service Notas de la versión 2020.8.0.'
translation-type: tm+mt
source-git-commit: dafdbffa96cd565379a700c696586222f43022c2
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 6%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.8.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.8.0.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* La función de la consola de producto ya está disponible. Esto permite a los especialistas en mercadotecnia/autores en AEM realizar vistas y navegar por categorías y productos almacenados en el servidor comercial. También se proporciona compatibilidad para propiedades de categorías y productos en la consola de producto.

* Se mejoraron los seleccionadores de productos y Categorías para permitir que los especialistas en marketing seleccionen el producto mediante SKU o seleccione la categoría mediante ID de categoría.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.8.0 is August 06, 2020.

### Novedades {#what-is-new-cloud-manager}

* La auditoría de contenido es una función habilitada en Cloud Manager Sites Producines. La configuración de la tubería de producción para programas con sitios ahora incluye una tercera ficha denominada Auditoría **del contenido**. Cada vez que se ejecute un flujo de producción, se incluirá un nuevo paso de auditoría de contenido en la canalización después de realizar pruebas funcionales personalizadas que evaluarán el sitio en relación con una serie de dimensiones, entre las que se incluyen rendimiento, SEO (Optimización de motores de búsqueda), accesibilidad, prácticas recomendadas y PWA (Aplicación web progresiva).

   Refer to [Content Audit Testing](/help/implementing/developing/introduction/understand-test-results.md#content-audit-testing) for more details.

* Los entornos recién creados en programas de Recursos ahora se configurarán automáticamente con Smart Content Services.

* Los entornos hibernados se pueden eliminar de la hibernación desde la página **Información general** del Administrador de nubes.

* Ahora se admiten repositorios privados de Maven enlazados a autenticación.

### Corrección de errores {#bug-fixes-cm}

* Algunos complementos innecesarios y no deseados de SonarQube se estaban ejecutando como parte de la exploración de calidad del código.

* En la página de ejecución de la canalización, el nombre de la ramificación tenía un formato incorrecto.

* En algunos casos, las ejecuciones de los trámites terminados no se registraban correctamente por haberse completado, lo que impedía la ejecución de los nuevos trámites.

* Ocasionalmente, las ejecuciones por tuberías se *quedaban atascadas* debido a problemas de comunicación interna.

* Al aprovisionar una nueva organización, a algunos usuarios con funciones administrativas distintas de los administradores del sistema se les daba acceso erróneamente a Cloud Manager.

* En determinadas condiciones, el trabajo de índices de actualización se inició varias veces en paralelo, lo que resultó en un error de implementación.

* La información sobre herramientas de las tarjetas de programa no era coherente.

* La interfaz de usuario permitía erróneamente que las operaciones se intentaran en un entorno mientras se eliminaba.

* Hubo una discordancia de color en la página **Información general** del Administrador de nube.

### Problemas conocidos {#known-issues-cm}

* Se incluyen páginas no válidas que llevan la puntuación promedio de auditoría de contenido por debajo de lo que deberían ser.

* La ficha Auditoría de contenido muestra incorrectamente la dirección URL base utilizando el dominio de autor en lugar del dominio de publicación.

* Para activar el paso Auditoría de contenido, los usuarios deben editar la canalización y, opcionalmente, agregar páginas. Si no se agrega ninguna página, se auditará la página principal.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de la versión v1.0.4 de la herramienta de transferencia de contenido.

### Novedades {#what-is-new-ctt}

* La herramienta de transferencia de contenido ahora es compatible con Shared S3 DataStore.

### Corrección de errores {#ctt-bug-fixes}

* Se han agregado tiempos de espera adicionales para que la herramienta complete las acciones.

* La IU de la versión anterior a veces mostraba una extracción correcta aunque el registro mostraba errores.

