---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: f0dc0e0ccd196ab748e2bfcdb4ce404c1c91c213
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 20%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 12441 {#release-12441}

A continuación se resumen las mejoras continuas para la 12441 de la versión de mantenimiento, que se publicó el 27 de junio de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 12255 anterior.

La activación de funciones 2023.7.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Roadmap de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-12441}

- SITES-8769: Mejorar las llamadas de StyleImpl en ResponsiveGrid
- FORMS-5054: Se ha agregado compatibilidad con todas las [estatuas](https://opensource.adobe.com/acrobat-sign/acrobat_sign_events/webhookeventsagreements.html) compatible con Adobe Sign.

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
- FORMS-7648: La validación del campo Número máximo de dígitos no funciona para el componente Cuadro numérico.
- FORMS-8177: Cuando el servicio Forms está activo, el error &#39;com.adobe.aem.formsndocuments.publish.AssetReferenceProvider no pudo recuperar las dependencias del recurso.
- FORMS AEM-8300: Cuando un usuario intenta delegar una tarea después de abrirla, la respuesta delegada vuelve a cargar la tarea, en lugar de abrir la interfaz de usuario de la Bandeja de entrada de la Bandeja de entrada de la del usuario.
- FORMS-8500: En el explorador Microsoft® Edge con la opción IE Mode habilitada, HTML5 Forms no puede abrirse.
- FORMS-8541: Al procesar un Forms adaptable, se produce una excepción de puntero nulo.
- FORMS-8964: cuando se abre un formulario en un dispositivo Android™ en Google Chrome o Mozilla Firefox, el texto introducido en el componente Cuadro de texto no se puede quitar.
- FORMS-9026: Cuando un usuario crea un formulario adaptable basado en un esquema JSON complejo y válido, arrastra campos de esquema JSON relacionados al Editor de Forms adaptable para crear campos de Forms adaptables y actualiza la ventana Editor de Forms adaptable, todos los campos se eliminan y el editor de Forms adaptable aparece en blanco.
- FORMS-9263: Cuando el texto para mostrar de una opción de casilla de verificación contiene caracteres especiales, los usuarios no pueden seleccionar dichas casillas de verificación.
- FORMS-8668: Al procesar una previsualización de PDF de un formulario, algunos volcados de pila Java™ no necesarios aparecen en los registros de errores. Sin embargo, no hay problemas al procesar el formulario.
- FORMS-8116: Cuando se aplican reglas al componente Contenedor de Forms adaptable, las reglas aplicadas no se guardan.
- FORMS-7906: Cuando se agrega un formulario adaptable a un componente Contenedor de AEM Sites, el editor de reglas no se puede abrir.
- FORMS-8846: la propiedad Referencia de enlace no funciona para el componente Archivos adjuntos de Forms adaptable.
- FORMS-9072: Cuando busca un esquema al crear un fragmento de formulario, el resultado de la búsqueda no devuelve ningún esquema para la selección.
- FORMS: se han corregido varios errores relacionados con la accesibilidad para mejorar la accesibilidad de las funciones de AEM Forms.


### Problemas conocidos {#known-issues-12441}

Ninguna.

### Tecnologías integradas {#embedded-tech-12441}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.50-T20230405052634-f9df4aa | [API Oak 1.50.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.50.0/index.html) |
| API AEM SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.0 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
