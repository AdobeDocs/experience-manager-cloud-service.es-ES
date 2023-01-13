---
title: Herramientas para desarrolladores de AEM para Eclipse
description: Herramientas para desarrolladores de AEM para Eclipse
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: cac6692e10da4b271610edd495d4cb38507a726b
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 3%

---

# Herramientas para desarrolladores de AEM para Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Información general {#overview}

AEM Developer Tools para Eclipse es un complemento de Eclipse basado en el [Complemento Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) publicado con la licencia de Apache 2.

Ofrece varias funciones que facilitan el desarrollo de AEM:

* Integración perfecta con instancias AEM a través del conector del servidor Eclipse
* Sincronización para paquetes de contenido y OSGi
* Compatibilidad de depuración con la capacidad de intercambio en caliente de código
* Inicio sencillo de AEM proyectos a través de un Asistente específico para la creación de proyectos
* Fácil edición de las propiedades JCR

## Requisitos  {#requirements}

Antes de utilizar las herramientas para desarrolladores de AEM, debe:

* Descargar e instalar [Eclipse IDE para desarrolladores de Java empresariales](https://www.eclipse.org/downloads/packages/).
* Configure la instalación de eclipse para asegurarse de que tiene al menos 1 gigabyte de memoria acumulada editando su `eclipse.ini` archivo de configuración tal como se describe en la sección [Preguntas frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>En macOS, debe hacer clic con el botón derecho en **Eclipse.app** y, a continuación, seleccione **Mostrar contenido del paquete** para encontrar su `eclipse.ini`**.**

## Instalación de las herramientas para desarrolladores de AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Cuando haya cumplido, [requisitos](#requirements) anteriormente, puede instalar el complemento de la siguiente manera:

1. Abra el [Sitio Web de AEM Developer Tools](https://eclipse.adobe.com/aem/dev-tools/). <!-- RB: This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Copie el **Vínculo de instalación**.

   Tenga en cuenta que, de lo contrario, puede descargar un archivo en lugar de utilizar el vínculo de instalación. Este método permite la instalación sin conexión, pero no recibe notificaciones de actualización automática de esta manera.

1. En Eclipse, abra el **Ayuda** para abrir el Navegador.
1. Haga clic en **Instalar nuevo software**.
1. Haga clic en **Agregar...**.
1. En **Nombre** enter `AEM Developer Tools`.
1. En **Ubicación** copie la dirección URL de instalación.
1. Haga clic en **Agregar**.
1. Marque ambas **AEM** y **Sling** complementos.
1. Haga clic en **Siguiente**.
1. En el **Detalles de instalación** ventana, haga clic en **Siguiente** de nuevo.
1. Acepte los acuerdos de licencia y haga clic en **Finalizar**.
1. Haga clic en **RestartNow** para reiniciar Eclipse.

## La perspectiva AEM {#the-aem-perspective}

En Eclipse, una perspectiva determina las acciones y vistas disponibles en una ventana y permite la interacción orientada a tareas con los recursos en Eclipse. Para obtener más información sobre Perspectiva, consulte la [Documentación de Eclipse.](https://help.eclipse.org)

Las AEM herramientas de desarrollo para Eclipse proporcionan una perspectiva de AEM que le ofrece control total sobre sus proyectos e instancias de AEM. Para abrir la perspectiva de AEM:

1. En la barra de menús Eclipse , seleccione **Ventana** -> **Perspectiva** -> **Abrir perspectiva** -> **Otro**.
1. Select **AEM** en el cuadro de diálogo y haga clic en **Apertura**.

![La perspectiva AEM en Eclipse](assets/eclipse-aem-perspective.png)

## Proyecto de módulo múltiple de muestra {#sample-multi-module-project}

Las herramientas para desarrolladores de AEM para Eclipse incluyen un proyecto multimódulo de muestra que le ayuda a ponerse al día rápidamente con la configuración de un proyecto en Eclipse, así como que sirve como guía de prácticas recomendadas para varias funciones de AEM. [Obtenga más información sobre el tipo de archivo del proyecto](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Siga estos pasos para crear el proyecto de ejemplo:

1. En el **Archivo** > **Nuevo** > **Proyecto** , vaya a la **AEM** y seleccione **AEM proyecto de módulo múltiple de muestra**.

   ![AEM proyecto de módulo múltiple de muestra](assets/aem-sample-project.png)

1. Haga clic en **Siguiente**.

   >[!NOTE]
   >
   >Este paso puede tardar un momento, ya que m2eclipse necesita analizar los catálogos de arquetipos.

1. Choose `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` en el menú y, a continuación, haga clic en **Siguiente**.

   ![Seleccionar versión del tipo de archivo](assets/select-archetype.png)

1. Proporcione los siguientes campos para el proyecto de ejemplo:

   * **Nombre**
   * **ID de grupo**
   * **Id. de artefacto**
   * **appId** - Puede que necesite expandir el **Avanzadas** para establecer este valor.
   * **appTitle** - Puede que necesite expandir el **Avanzadas** para establecer este valor.
   * **Paquete** - Puede que necesite expandir el **Avanzadas** para establecer este valor.

   ![Definir propiedades de tipo de archivo](assets/archetype-properties.png)

1. Haga clic en **Siguiente**.

1. A continuación, configure un servidor AEM al que se conectará Eclipse.

   Para utilizar la función Debugger, debe haber empezado a AEM en modo de depuración, lo que se puede lograr, por ejemplo, añadiendo lo siguiente a la línea de comandos:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Conectarse al servidor de AEM](assets/connect-server.png)

1. Haga clic en **Finalizar**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una nueva instalación (más específicamente, cuando las dependencias maven nunca se han descargado), puede que el proyecto se cree con errores. En este caso, siga el procedimiento descrito en [Resolver definición de proyecto no válida](#resolving-invalid-project-definition).

## Cómo importar proyectos existentes {#how-to-import-existing-projects}

Puede usar la variable **Nuevo proyecto** para crear la estructura adecuada:

1. Siga las instrucciones para crear un [Proyecto de módulo múltiple de muestra](#sample-multi-module-project) y tendrá los siguientes proyectos creados para usted, que permitirán una separación saludable de las preocupaciones:

   * `PROJECT.ui.apps` para `/apps` y `/etc` contenido
   * `PROJECT.ui.content` para `/content` que se crea
   * `PROJECT.core` para paquetes Java (se volverán interesantes en cuanto desee agregar código Java)
   * `PROJECT.it.launcher` y `PROJECT.it.tests` para pruebas de integración

1. Reemplace el contenido de su `PROJECT.ui.apps` con el `apps` y `etc` carpetas del paquete:

   1. En el panel Explorador de proyectos, despliegue `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Haga clic con el botón derecho en el `apps` carpeta y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine el `apps` y `etc` carpetas que debería ver y colocar aquí la variable `apps` y `etc` carpetas del paquete de contenido.
   1. En Eclipse, haga clic con el botón derecho en el `PROJECT.ui.apps` proyecto y elija **Actualizar**.

1. A continuación, haga lo mismo para la variable `PROJECT.ui.content` y reemplace su carpeta de contenido por la de su paquete:

   1. En el panel Explorador de proyectos, despliegue `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Haga clic con el botón derecho en la carpeta de contenido más profunda y elija **Mostrar en** -> **Explorador del sistema**.
   1. Elimine la carpeta de contenido que debería ver y coloque aquí la carpeta de contenido del paquete de contenido.
   1. En Eclipse, haga clic con el botón derecho en el `PROJECT.ui.content` proyecto y elija **Actualizar**.

1. Ahora tiene que actualizar el `filter.xml` archivos de estos dos proyectos para que se correspondan con el contenido del paquete de contenido. Para ello, abra el `META-INF/vault/filter.xml` del paquete de contenido en un editor de texto/código independiente.

   * Este es un ejemplo de cómo `filter.xml` puede tener el siguiente aspecto:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. En cuanto al contenido del paquete que se dividió en dos proyectos, también tendrá que dividir estas reglas de filtro en dos y actualizar según corresponda la variable `filter.xml` archivos de los dos proyectos.

   1. En Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Reemplace el contenido del `<workspaceFilter>` elemento con las reglas del paquete que comienzan con `/apps` y `/etc`
      * Por ejemplo:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/apps/foo"/>
            <filter root="/apps/foundation/components/bar"/>
            <filter root="/etc/designs/foo"/>
         </workspaceFilter>
         ```
   1. A continuación, abra `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Sustituya las reglas por las del paquete que empiecen por `/content`.
      * Por ejemplo:

         ```xml
         <?xml version="1.0" encoding="UTF-8"?>
         <workspaceFilter version="1.0">
            <filter root="/content/foo"/>
            <filter root="/content/dam/foo"/>
            <filter root="/content/usergenerated/content/foo"/>
         </workspaceFilter>
         ```


1. Asegúrese de guardar todos los cambios. Ahora puede sincronizar ese nuevo contenido con su instancia de AEM.

1. En el panel Servidores, asegúrese de que la conexión se ha iniciado y, en caso contrario, iníciela.
1. Haga clic en el **Limpiar y publicar** icono.

Una vez finalizado, el paquete debe ejecutarse en la instancia y, al guardar, cualquier cambio se sincroniza automáticamente con la instancia.

Si desea volver a crear un paquete fuera del proyecto, haga clic con el botón derecho en el `PROJECT.ui.apps` o `PROJECT.ui.content` y elija **Ejecutar como** -> **Instalación de Maven**.

Ahora tiene una carpeta de destino creada con el paquete dentro de (llamada, por ejemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Solución de problemas {#troubleshooting}

### Resolver definición de proyecto no válida {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón derecho.
1. En el menú contextual, seleccione **Maven** -> **Actualizar proyectos**.
1. Marque **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **Aceptar**.

Eclipse descarga las dependencias necesarias. Esto puede tardar un momento.

## Más información {#more-information}

La herramienta oficial Apache Sling IDE para el sitio web Eclipse le proporciona información útil:

* La variable [**Herramientas Apache Sling IDE para Eclipse** Guía del usuario](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentación le guía a través de los conceptos generales, la integración del servidor y las funcionalidades de implementación compatibles con las herramientas de desarrollo de AEM.
* La variable [Sección Resolución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La variable [Lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

El siguiente funcionario [Eclipse](https://eclipse.org/) la documentación puede ayudarle a configurar su entorno:

* [Introducción a Eclipse](https://eclipse.org/users/)
* [Sistema de ayuda del Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)
