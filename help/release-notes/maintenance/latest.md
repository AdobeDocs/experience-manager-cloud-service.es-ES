---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: fd0b8ca281f35a92876f3c31baa4e17884f23948
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 41%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 12441 {#release-12441}

A continuación se resumen las mejoras continuas para la 12441 de la versión de mantenimiento, que se publicó el 27 de junio de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 12255 anterior.

La activación de funciones 2023.7.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Roadmap de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-12441}

- SITES-8769: Mejorar las llamadas de StyleImpl en ResponsiveGrid

### Problemas corregidos {#fixed-issues-12441}

- Varias actualizaciones relacionadas con la accesibilidad
- SITES-12688: Editor de páginas: Operador lógico O no funciona correctamente en la búsqueda del Buscador de recursos
- SITES-4951: Editor de páginas: La búsqueda de etiquetas en el editor de páginas no encuentra subetiquetas
- SITES-12465: Fragmentos de experiencias: Las teclas de dirección no funcionan en el cuadro de diálogo del componente Fragmento de experiencias
- SITES-12893: Fragmentos de experiencias: Aplicar validación de referencia circular para fragmentos de experiencias
- SITES-12715: Fragmentos de experiencias: Las configuraciones de Cloud Service aplicadas a la carpeta de fragmentos de experiencias no persisten
- SITES-13097: Fragmentos de experiencias: No se pueden añadir fragmentos de experiencias a un proyecto de traducción
- SITES-13165: GraphQL: Restaurar el comportamiento predeterminado para filtrar los valores nulos
- SITES-12577: Verificador de vínculos: el transformador no reescribe los vínculos intermitentemente
- SITES-13559: MSM: Excepción &quot;No se puede modificar&quot; lanzada al desplegar el componente
- SITES-11757: MSM: Heredar la configuración de despliegue de la página principal no se revierte para las páginas secundarias
- SITES-14073: Administración de sitios: El informe CSV falla con 500 al seleccionar ninguna propiedad para exportar

### Problemas conocidos {#known-issues-12441}

Ninguna.

### Tecnologías integradas {#embedded-tech-12441}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API AEM SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.0 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
