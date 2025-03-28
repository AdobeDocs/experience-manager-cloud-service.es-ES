---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 32%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión X {#X}

A continuación se resumen las mejoras continuas para la versión X de mantenimiento, que se publicó el 1 de abril de 2025. La versión de mantenimiento anterior fue la 19823.

La activación de funcionalidades 2025.4.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-X}

FORMS-19068: se ha agregado compatibilidad con las acciones de envío del conector de AEP en las API de Forms Manager para mejorar las capacidades de integración de datos de formulario.

FORMS-18513: se ha implementado compatibilidad con la transformación del árbol de datos en AEP Connector para mejorar la funcionalidad del asistente y las capacidades de administración de datos.

FORMS-18432: se ha implementado la configuración de relleno previo del lado del cliente específica del formulario (basada en regex) para habilitar la funcionalidad de relleno previo selectivo sin cambios en el nivel OSGI.

FORMS-17551: se ha agregado compatibilidad con el documento de registro (DoR) para integraciones de listas de SharePoint.

### Problemas solucionados {#fixed-issues-X}

FORMS-19028: La funcionalidad de relleno previo del lado del cliente interrumpe la administración de eventos del formulario, lo que evita que los eventos Value commit y DOMContentLoaded se activen correctamente al cargar el formulario.

FORMS-18360: administración mejorada del ámbito de la lista de SharePoint para equipos y sitios en Forms Document Management para mejorar la organización de los datos y el control de acceso.

FORMS-18325: Se ha añadido la configuración de nube de Adobe Experience Platform (AEP) para mejorar la integración de datos de formulario y las capacidades de procesamiento.

FORMS-18213: se ha implementado la funcionalidad para ocultar/excluir campos deshabilitados del documento de registro (DoR) para mejorar la claridad del documento y la experiencia del usuario.

FORMS-18189: se ha modificado la administración de funciones personalizadas para evitar el registro de errores en bibliotecas de cliente vacías y mejorar la visualización de errores en la IU.

FORMS-18426: La funcionalidad de búsqueda de listas de SharePoint falla cuando los nombres de lista contienen caracteres especiales (por ejemplo, &quot;-&quot;), lo que afecta a la integración de formularios con listas de SharePoint.

FORMS-18375: los formularios basados en componentes de base seleccionan incorrectamente las configuraciones de recaptcha de la carpeta `conf/global` cuando no se selecciona ningún contenedor de configuración específico.

FORMS-18304: los documentos de PDF/A-1b que pasan la validación en Acrobat y LiveCycle ES4 se marcan incorrectamente como no compatibles en AEM 6.5 Forms debido a errores de color dependientes del dispositivo.

FORMS-18271: el editor de temáticas de Forms muestra mensajes de error no localizados, lo que afecta a la experiencia del usuario en la configuración del formulario y la personalización de temáticas.

FORMS-18068: Problemas de procesamiento de texto en negrita en el documento de registro (DoR) para grupos de botones de opción y casillas de verificación que utilizan campos de texto enriquecido.

FORMS-7016: El orden de enfoque del teclado en el Editor de formularios no sigue la navegación lógica.

FORMS-6950: se han agregado los roles y atributos ARIA necesarios a los componentes de vista de árbol del navegador del sistema de archivos para mejorar la accesibilidad del lector de pantalla y cumplir con el estándar WCAG 4.1.2 Nombre, función, valor (nivel A).

### Problemas conocidos {#known-issues-X}

Ninguna.

### Características y API obsoletas {#deprecated-X}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-X}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda X vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-X}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
