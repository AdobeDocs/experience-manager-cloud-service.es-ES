---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d2c26a122bd2a0a970af7578932d88e6f93487d5
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 13%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 25194 {#25194}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 25194, que se publicó el jueves, 01 de abril de 2026. La versión de mantenimiento anterior fue la 24678.

La activación de funciones 2026.4.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!NOTE]
>
>La 24893 de la versión se ha convertido en privada.

### Mejoras {#enhancements-25194}

* ASSETS-65127: Metadatos personalizados de eventos: se ha mejorado la administración de los nombres de los metadatos.
* ASSETS-63313: crear automáticamente vínculos relacionados para recursos exportados y principales basados en manifiestos de C2PA.
* ASSETS-10995: limitar el número de recursos en un zip de descarga.
* FORMS-24388: se ha agregado un entorno de desarrollo local para el editor de comunicaciones interactivas (CI) que permite a los desarrolladores crear y probar configuraciones sin depender de servidores compartidos. Esta mejora ayuda a los clientes empresariales a iterar más rápido, reducir las dependencias del entorno y mejorar la productividad general del desarrollo.
* FORMS-24014: se ha mejorado el Editor de reglas para los componentes de archivos adjuntos a fin de que admitan condiciones de combinación mediante la lógica &quot;Y&quot;, por ejemplo, para permitir reglas como &quot;Si el archivo adjunto se cambia y el panel es válido, hágalo&quot;. Anteriormente, no se podían utilizar condiciones adicionales con archivos adjuntos; esta actualización permite definiciones de reglas más complejas para admitir flujos de trabajo avanzados.
* FORMS-23571: se ha mejorado la vista gramatical simplificada existente para las reglas de eventos de déclencheur al añadir compatibilidad con eventos predeterminados (OOTB), además de con eventos personalizados. Anteriormente, los usuarios solo podían utilizar la gramática simplificada para eventos personalizados y tenían que cambiar entre las reglas &quot;CUANDO&quot; y &quot;EVENTO DE DÉCLENCHEUR ON&quot; para configurar OOTB y eventos personalizados por separado. Con esta actualización, tanto los eventos OOTB como los personalizados se pueden usar en la misma gramática simplificada, lo que optimiza la configuración de reglas y reduce la necesidad de cambiar de contexto.
* FORMS-24462: se ha agregado compatibilidad con el componente Firma manuscrita en los componentes React Vanilla para Forms adaptable sin encabezado (AF). Esta mejora permite a los usuarios capturar firmas manuscritas directamente en formularios basados en React, lo que admite flujos de trabajo de firma digital y cronologías de lanzamiento planificadas para clientes empresariales.
* FORMS-24343: se ha agregado la administración optimizada para `custom:setProperty` en el modelo de formulario Notación de objetos de JavaScript (JSON), lo que permite un procesamiento más rápido de las actualizaciones de propiedades dinámicas. Esta mejora mejora mejora el rendimiento de los Forms adaptables complejos (AF) que dependen de cambios frecuentes en el tiempo de ejecución, lo que da como resultado interacciones de usuario más suaves y tiempos de carga reducidos.
* FORMS-24358: se ha agregado compatibilidad para el uso de la propiedad `items` en la estructura de notación de objetos JavaScript (JSON) de modelo en lugar de `:items` y `:itemsOrder`. Esta mejora permite a los desarrolladores trabajar con un modelo de datos más limpio e intuitivo que se alinea mejor con las convenciones JSON comunes y simplifica la integración con sistemas externos.
* FORMS-24087: compatibilidad añadida para definir reglas y eventos directamente en contenedores de fragmento en Forms adaptable (AF). Esta mejora permite a los autores aplicar lógica condicional e interacciones en el nivel de contenedor, lo que mejora la reutilización y reduce la necesidad de duplicar reglas en campos de fragmento individuales.
* FORMS-24440: se ha añadido una nueva acción &quot;Quitar campo&quot; en la lista desplegable ENTONCES del Editor de reglas para el editor de comunicaciones interactivas que permite a los usuarios quitar completamente un componente seleccionado del formulario cuando se cumple una condición de regla. Esta mejora admite flujos de trabajo que requieren reestructurar dinámicamente los formularios en lugar de ocultar únicamente los campos, a la vez que se sigue activando el script `forms_ready` apropiado para lograr un comportamiento coherente.
* FORMS-23898: se ha agregado compatibilidad para definir variables mediante la notación `@` en el Editor de comunicaciones interactivas (IC), lo que permite a los usuarios configurar tablas dinámicas de forma más intuitiva. Esta mejora simplifica la configuración del contenido de tablas controladas por variables y mejora la claridad al administrar datos dinámicos en la experiencia de creación.
* FORMS-23702: se ha agregado autenticación basada en certificados para las conexiones de SharePoint List (SPList) que permite un acceso más seguro y controlado por certificados a los datos de SharePoint. Esta mejora ayuda a los clientes empresariales a cumplir con requisitos de seguridad y cumplimiento más estrictos, al tiempo que reduce la dependencia en la autenticación basada en contraseña.
* FORMS-23800: se ha agregado compatibilidad para anular las claves secretas reCAPTCHA en las configuraciones de sling, lo que permite a los clientes empresariales alinearse con sus propios requisitos de seguridad y conformidad. Esta mejora permite la administración de claves secretas específicas del entorno, de modo que los administradores puedan integrar de forma segura reCAPTCHA sin cambios en el código.

### Problemas solucionados {#fixed-issues-25194}

* ASSETS-62882: vista de administrador: la información sobre herramientas se interrumpe cuando se cargan varios nombres de archivo no válidos.
* ASSETS-63642: El vínculo Compartir no puede procesar recursos en algunos entornos de desarrollo (SLA3).
* ASSETS-59267: NPE al cargar metadatos de aplicación para la carga útil de entrega.
* ASSETS-59227: exportación de metadatos: las propiedades no seleccionadas ya no se incluyen debido a la coincidencia de regex.
* ASSETS-65187: Vista previa del CSV en la nube cuando los datos de columna contienen comas de escape.
* ASSETS-63441: Asegúrese de que todos los usuarios tengan permisos para leer la configuración de Assets Omnisearch.
* SITES-40095: Editor de metadatos: referencias de fragmentos de contenido local más allá de 10 entradas.
* FORMS-24811: Los usuarios han experimentado problemas al administrar las reglas lógicas de formulario. Cuando intentaban modificar las reglas creadas anteriormente, el editor de reglas no permitía realizar cambios, lo que obligaba a los usuarios a volver a crear las reglas desde cero y ralentizaba el mantenimiento del formulario.
* FORMS-24720: Los usuarios experimentaron problemas al configurar variables recién creadas en Forms adaptable (AF). Cuando agregaban reglas a variables enlazadas a datos o no enlazadas, las reglas no se guardaban según lo esperado, lo que obligaba a los usuarios a volver a crear su lógica y ralentizaba los flujos de trabajo de creación de formularios.
* FORMS-24195: Los usuarios experimentaron un comportamiento incoherente al restablecer los campos desplegables en Forms adaptable (AF). Cuando un menú desplegable tenía un marcador de posición configurado y se restablecía el formulario o componente, el campo se quedaba en blanco en lugar de volver al valor del marcador de posición, lo que provocaba confusión sobre las selecciones requeridas.
* FORMS-24718: Los usuarios experimentaron problemas de navegación en el editor de comunicaciones interactivas (IC) al seleccionar el botón Inicio. En lugar de volver a la interfaz principal de Adobe Experience Manager (AEM), el botón no se redireccionaba como se esperaba, lo que afectaba al flujo de trabajo de los usuarios al pasar de la edición IC a la pantalla de inicio de AEM.
* FORMS-24810: Los usuarios experimentaron errores intermitentes al cargar la interfaz de usuario adaptable (AUI) para formularios en el primer intento. En algunas sesiones, la página inicial no se representaba correctamente, lo que obligaba a los usuarios a actualizar o volver a intentarlo antes de poder empezar a rellenar sus formularios.
* FORMS-24520: Los usuarios experimentaron la falta de números de página en la vista previa de impresión (IU) de la interfaz de usuario del agente para formularios que utilizan la interfaz de usuario adaptable (AUI). Cuando los agentes abrían la vista preliminar, el campo de número de página aparecía vacío, lo que dificultaba la referencia a páginas específicas mientras se revisaban o compartían copias impresas.
* FORMS-24532: Los usuarios experimentaron errores al utilizar el prerrellenado del Modelo de datos de formulario (FDM) con las configuraciones de lista de SharePoint `/teams`. Las organizaciones gubernamentales que dependían de estas listas vieron cómo los formularios se cargaban sin los datos rellenados previamente esperados, lo que interrumpió los flujos de trabajo de recopilación de datos y aumentó el esfuerzo de entrada manual.
* FORMS-24516: Los usuarios experimentaron la falta de datos de firma de anotaciones en el documento de registro (DoR) después de una actualización de SDK en AEM Forms as a Cloud Service. Cuando los formularios se firmaban con la opción de garabatos, el DoR generado no mostraba la firma capturada, lo que provocaba confusión y registros incompletos para los clientes empresariales.
* FORMS-18631: Los usuarios experimentaron problemas de accesibilidad con los diseños de cuadrícula en las vistas de escritorio, de tableta de diseño web interactivo (RWD) y de móvil RWD. Cuando se utilizaba Chrome en Windows 11 con el lector de pantalla NVDA (NonVisual Desktop Access), a las cuadrículas les faltaban funciones y atributos adecuados, lo que dificultaba a las tecnologías de asistencia interpretar y navegar por el contenido correctamente.
* FORMS-24798: Los usuarios experimentaron un comportamiento incoherente al utilizar `else` condiciones en reglas de Forms adaptable (AF) dentro de la interfaz de usuario (IU) de AEM Forms. Cuando no se cumplía la condición de regla principal, no se ejecutaban las acciones de `else` asociadas, lo que provocaba que la lógica del formulario y la visibilidad del campo se comportaran de forma diferente a lo que los autores configuraban.
* FORMS-24334: Los usuarios experimentaron errores de relleno previo y problemas de combinación de Notación de objetos de JavaScript (JSON) al trabajar con un formulario adaptable (AF) incrustado en Adobe Experience Manager (AEM) Forms as a Cloud Service. Al cargar formularios migrados, no aparecían los datos rellenados previamente esperados y el contenido JSON combinado estaba incompleto o era incorrecto. Esto bloqueó la migración de AEM 6.5 local a AEM Forms as a Cloud Service para los entornos afectados.
* FORMS-24441: Los usuarios experimentaron problemas con la configuración de la plantilla del documento de registro (DoR) en Adobe Experience Manager (AEM) Forms as a Cloud Service. Cuando guardaban una plantilla de documento de registro personalizada en el entorno de desarrollo rápido, esta volvía a la versión predeterminada, lo que les impedía conservar el diseño y la configuración deseados.
* FORMS-24393: Los usuarios experimentaban confusión cuando las plantillas antiguas seguían apareciendo como &quot;Sin título&quot; en lugar de mostrar nombres significativos. Esto dificultaba la distinción y reutilización de las plantillas existentes durante el trabajo diario de creación.
* FORMS-24163: Los usuarios experimentaron problemas al obtener una vista previa de los formularios de la versión 2 que contenían fragmentos. En el modo de vista previa, el contenido del formulario no se representaba según lo esperado, lo que impedía a los usuarios validar el diseño y el comportamiento antes de publicar.
* FORMS-24328: Los usuarios experimentaron que los envíos de formularios no se completaban al utilizar reCAPTCHA v2 invisible con la opción &quot;Validar CAPTCHA en una acción del usuario&quot;. Los clientes empresariales vieron que los formularios de los entornos afectados no se enviaban según lo esperado, lo que perturbaba los flujos de trabajo de contacto y solicitud de propuestas.

#### Guías de AEM {#guides-25194}

* GUIDES-38412 : Al editar un archivo de Schematron `(*.sch)` y utilizar la función de buscar y reemplazar, el panel buscar y reemplazar aparece parcialmente fuera de la pantalla en la parte inferior, lo que impide el acceso a sus campos y controles de entrada.
* GUIDES-37806: Cuando se reutiliza el mismo tema en varias asignaciones con diferentes ajustes preestablecidos condicionales, la publicación de la asignación más reciente en Salesforce sobrescribe el contenido del tema, lo que da como resultado que se muestren datos incorrectos a los usuarios de asignaciones publicadas anteriormente.
* GUIDES-39394: Cuando una imagen administrada inicialmente como un recurso específico de un idioma con una versión específica (por ejemplo, en `/en/`) se mueve a una carpeta global con una versión actualizada y se realiza una exportación de línea de base, la nueva línea de base sigue haciendo referencia a versiones obsoletas específicas del idioma de esa imagen, lo que provoca un error en la exportación de línea de base.
* GUIDES-39054: Al crear una línea de base dinámica, el editor a veces deja de responder debido a varias solicitudes de API simultáneas, lo que provoca que todas las demás operaciones se detengan.
* GUIDES-37781: Al asignar un usuario a una tarea de revisión, la lista desplegable muestra todos los usuarios, en lugar de solo aquellos asociados a los proyectos seleccionados, lo que da como resultado opciones de usuario no válidas.
* GUIDES-39385: Al abrir un informe para un mapa, se produce un retraso en la carga del panel Filtros.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-25194}

Ninguna.

### Características y API obsoletas {#deprecated-25194}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-25194}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 9 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-25194}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.90.0 | [API de Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
