---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 25af1b0d99f7c5971245f99a95c74d04ca943936
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 17%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13099 {#release-13099}

A continuación se resumen las mejoras continuas para la 13099 de la versión de mantenimiento, que se publicó el 15 de agosto de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 12874 anterior.

La activación de funciones 2023.8.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Roadmap de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13099}

- SITES-13906: GraphQL: actualice a graphql-java 20.1.
- SITES-8972: GraphQL: agregue la etiqueta de opción en JSON para el tipo de datos de enumeración.
- SITES-9689: GraphQL: agregue el título y la descripción en JSON para el tipo de datos de referencia de contenido.
- SITES-13052: Fragmentos de contenido: exporte fragmentos de contenido a Adobe Target.

### Problemas corregidos {#fixed-issues-13099}

- SITES-14937: MSM: Heredar configuraciones de despliegue del valor principal se activa al pulsar Guardar y cerrar en Live Copies.
- SITES-14847: Fragmentos de contenido: los vínculos de fragmentos de contenido no están resaltados.
- SITES-11620: Fragmentos de contenido: la ruta de referencias se corta ligeramente en la interfaz de usuario.
- SITES-14171: GraphQL: Las referencias circulares no se rompen para los datos almacenados en caché en algunos casos.
- SITES-14577: Fragmentos de experiencias: la publicación en lote no funciona para Live Copies.
- SITES-14341: IU de administración: comportamiento incoherente del botón &quot;Propiedades&quot; cuando se eliminan permisos de eliminación.
- SITES-11000: IU de administración - Referencias: Faltan vínculos entrantes en algunas páginas.
- SITES-11559: IU de administración - Referencias: Los vínculos entrantes muestran páginas incorrectas.
- SITES-14337: IU de administración: al abrir la página del editor se produce un error en casos específicos.
- SITES-13425: ContextHub: la barra de menús no se muestra al hacer clic en el botón de ContextHub.
- FORMS-9971: Cuando se procesa un formulario adaptable en una configuración regional diferente, la visibilidad de los componentes se interpreta y aplica de forma inexacta.
- FORMS-9888: Cuando un formulario adaptable se configura para redireccionarse a una URL externa (página de agradecimiento) al enviar el formulario, no se redirige a la URL externa.
- FORMS-9845: Después de borrar una lista desplegable usando el editor de reglas, los valores proporcionados anteriormente persisten, a pesar de la supuesta autorización.
- FORMS-9263: Cuando la etiqueta de una casilla de verificación contiene caracteres especiales y un usuario hace clic en la casilla de verificación, la casilla de verificación correspondiente no está seleccionada.
- FORMS-9254: a medida que un usuario se desplaza por el texto del componente Términos y condiciones, la casilla de verificación dentro del componente se habilita automáticamente incluso antes de que el usuario se haya desplazado por todo el texto.
- FORMS-9045: la etiqueta de script no resuelve las referencias de fragmento externas en el XDP base.
- FORMS-9026: Al intentar crear un formulario adaptable con un esquema JSON que tiene Enumeraciones con cadenas vacías y valida sin errores, el proceso genera un error. A continuación, al actualizar la página, el formulario no se carga correctamente, lo que muestra un formulario en blanco junto con un error en los registros.
- FORMS-8964: en Android™ Chrome/Firefox, el texto no se puede editar en el componente Cuadro de texto si se alcanza el límite máximo de caracteres.
- FORMS-8668: Excesivos volcados de pila de Java™ en registros de errores, a pesar del procesamiento de formularios funcionales, lo que provoca un hinchamiento del archivo de registro.
- FORMS-8554: la Forms adaptable con la carga diferida habilitada no funciona en el modo de vista previa de la instancia de autor.
- FORMS-8177: Cuando el servicio de Forms está activo, se produjo una excepción &quot;com.adobe.aem.formsndocuments.publish.AssetReferenceProvider no se pudieron recuperar las dependencias del recurso.&quot; ocurre. El error desaparece al deshabilitar el servicio de Forms.
- FORMS-3691: Faltan ámbitos de IIFE (expresión de función invocada inmediatamente) en algunos objetos. El propósito principal de utilizar un IIFE es crear un ámbito para las variables dentro de la función, evitando que esas variables contaminen el ámbito global.


### Problemas conocidos {#known-issues-13099}

- SITES-15359: Fragmentos de contenido: el patrón de nombre de variación no coincide correctamente con las variaciones que tienen ```'_'``` en sus nombres de recursos.
- SITES-15463: Plantillas de sitios: las plantillas no se pueden publicar (solución: utilice la consola de distribución).
- CQ-4354191: Flujos de trabajo: el iniciador personalizado puede entrar en déclencheur muchas veces debido a los metadatos de replicación presentes en los nodos nt:unstructured (solución alternativa: actualice los iniciadores para excluir las propiedades de metadatos de replicación para evitar la superposición).

### Tecnologías integradas {#embedded-tech-13099}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,52-T20230629133256-25c01b8 | [API Oak 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
