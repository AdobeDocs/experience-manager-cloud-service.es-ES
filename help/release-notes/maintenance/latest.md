---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b147c80581bcb554ae0b4ac971c5f98e7160d1df
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 8%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13665 {#release-13665}

A continuación se resumen las mejoras continuas para la 13665 de la versión de mantenimiento, que se publicó el 27 de septiembre de 2023. Esta versión de mantenimiento sustituye a las 13420 de la versión.

La activación de funciones 2023.10.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13665}

* Varias mejoras en las API de fragmentos de contenido.
* ASSETS-26713: Panel de recursos: nuevo panel de IU de Experience ahora accesible desde la interfaz de usuario táctil.
* SITES-11206: Fragmentos de contenido: API de búsqueda para fragmentos de contenido.
* SITES-11262: Fragmentos de contenido: Botón para cambiar al nuevo Editor de fragmentos de contenido.
* SITES-15447: Componentes principales: versión 2.23.4.
* FORMS-9624: Presentado el componente CAPTCHA para Forms adaptable basado en componentes principales.
* FORMS-9913: se ha mejorado el servicio de invocación del editor visual al añadir la capacidad de validar campos y mostrar mensajes de error y éxito adecuados.
* FORMS-10106: la API GeneratePDFOutput mejorada para devolver el número de páginas contenidas en el documento generado.
* FORMS-2494: compatibilidad añadida para fragmentos de formulario para Forms adaptable basado en componentes principales.
* FORMS-9807: Se ha agregado compatibilidad para permitir la navegación a una URL de página que se devuelve como resultado de un envío correcto a través del editor de reglas del formulario adaptable.
* FORMS-10571: se ha agregado la capacidad de establecer una URL de redireccionamiento de la página de agradecimiento basada en la respuesta de un servicio utilizado en una acción de envío personalizada para Forms adaptable basada en componentes principales.

### Problemas corregidos {#fixed-issues-13665}

* Varias actualizaciones relacionadas con la traducción.
* CQ-4354428: Workflows: no se puede completar una tarea en la bandeja de entrada.
* SITES-9733: Fragmentos de contenido: las referencias de recurso en el panel de referencia de fragmentos de contenido muestran referencias 0 (cero).
* SITES-14561: Fragmentos de contenido: corregido y mejorado HTML a la conversión de Marcado.
* SITES-14882: Fragmentos de contenido: una vez que editamos un fragmento de contenido y cerramos la pestaña sin hacer clic en el botón Guardar o Cerrar, los valores se almacenan.
* SITES-15167: Fragmentos de contenido: Al aplicar parches a una variación con una carga útil no válida, se devuelven 400 pero 500.
* SITES-15514: Fragmentos de contenido: Salida de Markdown mal formada para la tabla dentro de RTE.
* SITES-15661: Fragmentos de contenido: no utilice restricciones únicas y reordene elementos en campos de referencias en la API de fragmentos.
* SITES-15730: Screens: La funcionalidad de vista previa de canal de Screens no funciona en el panel.
* SITES-15995: Fragmentos de contenido: Los tipos MIME de los campos de texto largo de modelo y fragmento están codificados.
* SITES-16074: Fragmentos de contenido: Etiquete campos que no sean de cadena[] no se puede recuperar de JCR.
* SITES-16084: Fragmentos de contenido: Falta el navegador de destino en CFHomeCardModelImpl.
* SITES-14773: Fragmentos de experiencia: La referencia de vínculo no se actualiza dentro del fragmento de experiencia.
* SITES-14899: Fragmentos de experiencias: Varias ofertas creadas para variaciones de XF en Target.
* SITES-8590: GraphQL: Problemas de codificación con variables en consultas persistentes.
* SITES-9224: GraphQL: La excepción &quot;Writer ya se ha cerrado&quot; en GraphQLServlet.
* SITES-14800: GraphQL: excepción en consultas de GraphQL persistentes con variables.
* SITES-15586: GraphQL: Problema con el filtrado de consultas persistentes con valores nulos.
* SITES-15622: GraphQL: Problema con consultas persistentes con números y parámetros booleanos.
* SITES-15654: GraphQL: Problema con uniones y propiedades con el mismo nombre.
* SITES-15267: Lanzamientos: la promoción no recoge las páginas de lanzamiento modificadas antes de modificar la configuración de lanzamiento.
* SITES-15406: Lanzamientos: No se puede añadir una página de lanzamiento.
* SITES-15427: Lanzamientos: comportamiento incoherente del ámbito &quot;Promocionar página actual y páginas secundarias&quot;.
* SITES-15429: Lanzamientos: las páginas de creación se eliminaron al promocionar lanzamientos.
* SITES-15462: Lanzamientos: el proceso de promoción automática publica páginas fuera del ámbito de la promoción.
* SITES-15815: Lanzamientos: la página eliminada del lanzamiento hace que este no se promocione correctamente.
* SITES-15223: Editor de páginas: no se pueden cambiar los componentes en el emulador de tamaño de tableta.
* SITES-15463: Plantillas de página: Las plantillas no se pueden publicar.
* FORMS-10700: Al utilizar el componente selector de fechas en un formulario adaptable creado en Componentes principales:
   * Cuando el usuario envía el formulario sin proporcionar ninguna entrada para el componente de fecha, se registra un error.
   * Al utilizar versiones localizadas del selector de fechas, algunos meses funcionan sin problemas y la selección de otros provoca un mal funcionamiento del componente.
* FORMS-9598: El componente incrustado de AEM Forms no funciona.
* FORMS-9579: No se puede pasar un valor booleano a una función mientras se usa el Editor de reglas.
* FORMS-9916: al marcar el campo como no válido, se activa de nuevo un evento de cambio en el mismo campo. Este evento inesperado déclencheur la regla una vez más, creando un bucle que se repite hasta alcanzar un límite máximo de 10 repeticiones.
* FORMS-10243: La opción Definir enfoque no funciona correctamente para Forms adaptable basado en componentes principales. Específicamente, cuando se hace clic en un botón de opción y la regla &quot;establecer enfoque&quot; está habilitada para un objeto de cuadro de texto, no se puede establecer el enfoque como se pretende, a pesar de que otras reglas funcionan correctamente.
* FORMS-10416: Para un formulario adaptable sin encabezado, cuando se incluye la propiedad &quot;:type&quot;, el componente de entrada de texto multilínea aparece como un componente de entrada de texto de una sola línea normal.
* FORMS-10015: Para un formulario adaptable basado en componentes principales, en el editor de reglas, cuando elegimos el objeto Formulario, pasa todo el objeto Instancia de campo a la función personalizada en lugar de solo el valor del campo.
* FORMS-9890: los usuarios del grupo de administradores en la nube, sin acceso de usuario de formularios, pueden crear fuentes de datos, formularios y modelos de datos de formulario. Sin embargo, no pueden ver los servicios disponibles en el sistema al utilizar &quot;Invocar servicio&quot; en el editor de reglas.
* FORMS-9075: Al enviar un formulario adaptable, los lectores de pantalla no anuncian todos los mensajes de error para los campos obligatorios.
* FORMS-9014: Se corrigieron los siguientes problemas de accesibilidad:
   * Al abrir el cuadro de firma de anotaciones, el cursor salta al siguiente componente, no dentro del propio cuadro. El equipo de accesibilidad ha confirmado este comportamiento como un problema.
   * Después de firmar, al presionar Entrar no se cierra el cuadro de diálogo; los usuarios deben hacer clic explícitamente en el botón Aceptar.
   * Después de la firma, el orden de tabulación se restablece a la parte superior, en lugar de permanecer en el componente de firma o pasar al siguiente.
   * La opción para borrar la firma, representada por un icono cruzado, no forma parte del orden de tabulación y solo aparece al pasar el ratón por encima.
   * No se puede acceder al cuadro de diálogo &quot;Borrar confirmación de firma&quot; mediante el teclado.
   * La etiqueta del botón de señal de teclado debe corregirse para una mayor claridad.
   * Los controles dentro de la firma manuscrita carecen de la relación de contraste recomendada.
   * El estado inactivo del botón Aceptar/marcar debe incluir el atributo &quot;aria-disabled&quot;.
   * El lector de pantalla no transmite el texto utilizado para crear la firma mecanografiada, lo que impide el acceso de los usuarios con problemas de visión.
* FORMS-9214: para Forms adaptable basado en componentes principales, la función personalizada no se invoca a menos que se utilice para modificar otro campo, como establecer el valor de un campo diferente.
* Para las API de generación de documentos, la ruta &quot;/content&quot; muestra incoherencia en su uso en la ruta de la plantilla, la raíz de contenido y los datos. Funciona correctamente en algunos casos, pero no de manera uniforme.
* FORMS-10718: compatibilidad añadida para la API resolveNode de GuideBridge para Forms adaptable basado en componentes principales.
* FORMS-9998: en Forms adaptable basado en componentes principales, las funciones &quot;Está vacío&quot; y &quot;No está vacío&quot; no funcionan como se espera al validar la entrada de texto mediante el Editor de reglas.
* FORMS-10236: El componente Archivo adjunto no funciona correctamente para Forms adaptable basado en componentes principales. Al utilizar el componente Archivo adjunto, las vistas previas de archivos funcionan inicialmente, pero si adjunta archivos adicionales de tipos o formatos similares o diferentes, la vista previa no funciona correctamente.
* FORMS-10470: en el componente Casilla de verificación, cuando el valor predeterminado está desmarcado (&quot;desactivado&quot;) y el tipo de datos es Cadena, el botón de envío no funciona.
* FORMS-10534: en Forms adaptable basado en componentes principales, la opción de operando booleano aparece a la izquierda, lo que indica que se puede seleccionar. Sin embargo, cuando un usuario intenta seleccionarlo, se produce un resaltado de error o alguna forma de indicación de error, lo que sugiere que la selección no funciona según lo esperado.
* FORMS-10248: en Forms adaptable basado en componentes principales, configurar el valor de un botón de opción o de una casilla de verificación cuando el tipo de valor de datos es booleano no funciona como se esperaba.
* FORMS-8114: El selector de fechas y el patrón no se leen correctamente en el lector de pantalla NVDA. En concreto, cuando se utiliza el lector de pantalla NVDA, el selector de fechas sin patrón se lee correctamente. Sin embargo, cuando se aplica un patrón al selector de fechas, se lee como una tabla en lugar de interpretarse correctamente.







### Problemas conocidos {#known-issues-13665}

Ninguno

### Tecnologías integradas {#embedded-tech-13665}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1,54-T20230817132355-3800a65 | [API Oak 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
