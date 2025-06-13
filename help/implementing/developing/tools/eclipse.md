---
title: Herramientas para desarrolladores de AEM para Eclipse
description: Aprenda a utilizar AEM Developer Tools para Eclipse, un complemento de Eclipse basado en el complemento de Eclipse para Apache Sling.
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
feature: Developing
role: Admin, Architect, Developer
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 2%

---

# Herramientas para desarrolladores de AEM para Eclipse{#aem-developer-tools-for-eclipse}

![Logotipo de herramientas para desarrolladores de Experience Manager para Eclipse](assets/eclipse-logo.png)

## Información general {#overview}

_Experience Manager Developer Tools for Eclipse_ es un complemento de Eclipse basado en el complemento [Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lanzado bajo la licencia Apache 2.

Ofrece varias funciones que facilitan el desarrollo de AEM:

* Integración perfecta con las instancias de AEM a través del conector de servidor Eclipse
* Sincronización para paquetes OSGi y de contenido
* Compatibilidad de depuración con la capacidad de intercambio en caliente de código
* Bootstrap simple de proyectos de AEM mediante un asistente de creación de proyectos específico
* Edición sencilla de propiedades JCR

## Requisitos  {#requirements}

Antes de utilizar las herramientas para desarrolladores de AEM, debe hacer lo siguiente:

* Descargue e instale [Eclipse IDE para desarrolladores de Java™ empresariales](https://www.eclipse.org/downloads/packages/).
* Configure la instalación de Eclipse para asegurarse de que dispone de al menos 1 GB de memoria de pila editando el archivo de configuración `eclipse.ini` tal como se describe en las [Preguntas frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>En macOS, debes hacer clic con el botón derecho en **Eclipse.app** y, a continuación, seleccionar **Mostrar contenido del paquete** para encontrar tu `eclipse.ini`**.**

## Cómo instalar las herramientas para desarrolladores de AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Cuando haya cumplido los [requisitos](#requirements) anteriores, puede instalar el complemento de la siguiente manera:

1. Abra el [sitio web de herramientas para desarrolladores de AEM](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip). <!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Copie el **vínculo de instalación**.

   Como alternativa, puede descargar un archivo en lugar de utilizar el vínculo de instalación. Este método permite la instalación sin conexión, pero no recibe notificaciones de actualización automáticas faltantes de esta manera.

1. En Eclipse, abre el menú **Ayuda**.
1. Haga clic en **Instalar nuevo software**.
1. Haga clic en **Agregar...**.
1. En el campo **Nombre**, escriba `AEM Developer Tools`.
1. En el campo **Ubicación**, copie la URL de instalación.
1. Haga clic en **Agregar**.
1. Compruebe los complementos de **AEM** y **Sling**.
1. Haga clic en **Siguiente**.
1. En la ventana **Instalar detalles**, haga clic de nuevo en **Siguiente**.
1. Acepte los contratos de licencia y haga clic en **Finalizar**.
1. Haz clic en **Reiniciar ahora** para reiniciar Eclipse.

## La perspectiva de AEM {#the-aem-perspective}

En Eclipse, una perspectiva determina las acciones y vistas disponibles dentro de una ventana y permite la interacción orientada a tareas con recursos en Eclipse. Para obtener más información sobre Perspective, consulte la [documentación de Eclipse](https://help.eclipse.org/latest/index.jsp).

_Las herramientas de desarrollo de Experience Manager para Eclipse_ proporcionan una perspectiva de AEM que le ofrece control total sobre sus proyectos e instancias de AEM. Para abrir la Perspectiva de AEM:

1. En la barra de menús de Eclipse, seleccione **Ventana** > **Perspectiva** > **Abrir perspectiva** > **Otra**.
1. Seleccione **AEM** en el cuadro de diálogo y haga clic en **Abrir**.

![La perspectiva de AEM en Eclipse](assets/eclipse-aem-perspective.png)

## Ejemplo de proyecto de varios módulos {#sample-multi-module-project}

_Experience Manager Developer Tools for Eclipse_ incluye un proyecto de ejemplo de varios módulos que te ayudará a ponerte al día rápidamente con la configuración de un proyecto en Eclipse. También sirve como guía de prácticas recomendadas sobre varias funciones de AEM. [Más información sobre el tipo de archivo del proyecto](https://github.com/adobe/aem-project-archetype).

Siga estos pasos para crear el proyecto de ejemplo:

1. En el menú **Archivo** > **Nuevo** > **Proyecto**, vaya a la sección **AEM** y seleccione **Proyecto de módulo múltiple de muestra de AEM**.

   ![Proyecto de módulo múltiple de muestra de AEM](assets/aem-sample-project.png)

1. Haga clic en **Siguiente**.

   >[!NOTE]
   >
   >Este paso puede tardar un momento, ya que m2eclipse debe analizar los catálogos de tipo de archivo.

1. Elija `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` en el menú y luego haga clic en **Siguiente**.

   ![Seleccionar versión de tipo de archivo](assets/select-archetype.png)

1. Proporcione los siguientes campos para el proyecto de ejemplo:

   * **Nombre**
   * **Id. de grupo**
   * **Id. de artefacto**
   * **appId**: es posible que tenga que expandir las opciones de **Avanzado** para establecer este valor.
   * **appTitle**: es posible que tenga que expandir las opciones de **Advanced** para establecer este valor.
   * **Paquete**: es posible que tenga que expandir las opciones de **Avanzado** para establecer este valor.

   ![Definir propiedades de tipo de archivo](assets/archetype-properties.png)

1. Haga clic en **Siguiente**.

1. A continuación, configure un servidor de AEM al que se conecte Eclipse.

   Para utilizar la función del depurador, debe haber iniciado AEM en modo de depuración, lo que se puede lograr, por ejemplo, añadiendo lo siguiente a la línea de comandos:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Conectarse al servidor de AEM](assets/connect-server.png)

1. Haga clic en **Finalizar**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una instalación nueva (más específicamente, cuando las dependencias de Maven nunca se han descargado), puede obtener el proyecto creado con errores. En este caso, siga el procedimiento descrito en [Resolver definición de proyecto no válida](#resolving-invalid-project-definition).

## Cómo Importar Proyectos Existentes {#how-to-import-existing-projects}

Puede usar la característica **Nuevo proyecto** para crear la estructura adecuada:

1. Siga las instrucciones para crear un [Proyecto de módulo múltiple de muestra](#sample-multi-module-project) y tiene los siguientes proyectos creados para usted, que permiten una separación correcta de preocupaciones:

   * `PROJECT.ui.apps` para el contenido `/apps` y `/etc`
   * `PROJECT.ui.content` para `/content` creado
   * `PROJECT.core` para paquetes Java™ (se vuelven interesantes cuando desea agregar código Java™)
   * `PROJECT.it.launcher` y `PROJECT.it.tests` para pruebas de integración

1. Reemplace el contenido de su proyecto `PROJECT.ui.apps` por las carpetas `apps` y `etc` de su paquete:

   1. En el panel Explorador del proyecto, despliegue `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Haga clic con el botón derecho en la carpeta `apps` y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine las carpetas `apps` y `etc` que debería ver y coloque aquí las carpetas `apps` y `etc` de su paquete de contenido.
   1. En Eclipse, haga clic con el botón secundario en el proyecto `PROJECT.ui.apps` y elija **Actualizar**.

1. A continuación, haga lo mismo para `PROJECT.ui.content` y reemplace su carpeta de contenido por el de sus paquetes:

   1. En el panel Explorador del proyecto, despliegue `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Haga clic con el botón derecho en la carpeta de contenido más detallada y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine la carpeta de contenido que debería ver ahora y coloque aquí la carpeta de contenido de su paquete de contenido.
   1. En Eclipse, haga clic con el botón secundario en el proyecto `PROJECT.ui.content` y elija **Actualizar**.

1. Ahora tiene que actualizar los `filter.xml` archivos de estos dos proyectos para que se correspondan con el contenido del paquete de contenido. Para ello, abra el archivo `META-INF/vault/filter.xml` del paquete de contenido en un editor de texto/código independiente.

   * Este es un ejemplo del aspecto que puede tener el archivo `filter.xml`:

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

1. En cuanto al contenido del paquete que se dividió en dos proyectos, también debe dividir estas reglas de filtro en dos y actualizar en consecuencia los `filter.xml` archivos de los dos proyectos.

   1. En Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Reemplace el contenido del elemento `<workspaceFilter>` por las reglas del paquete que comiencen por `/apps` y `/etc`
      * Por ejemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Luego abra `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Reemplace las reglas por las del paquete que comiencen por `/content`.
      * Por ejemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Asegúrese de guardar todos los cambios. Ahora puede sincronizar ese nuevo contenido con la instancia de AEM.

1. En el panel Servidores, asegúrese de que la conexión se ha iniciado y, en caso contrario, iníciela.
1. Haga clic en el icono **Limpiar y publicar**.

Una vez finalizado, el paquete debería estar ejecutándose en la instancia y, al guardarlo, cualquier cambio se sincronizará automáticamente con la instancia.

Si desea volver a compilar un paquete a partir del proyecto, haga clic con el botón derecho en `PROJECT.ui.apps` o `PROJECT.ui.content` y elija **Ejecutar como** > **Instalación de Maven**.

Ahora tiene una carpeta de destino creada con el paquete dentro de (por ejemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Solución de problemas {#troubleshooting}

### Resolver definición de proyecto no válida {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón derecho.
1. En el menú contextual, seleccione **Maven** > **Actualizar proyectos**.
1. Compruebe **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **OK**.

Eclipse descarga las dependencias requeridas. Esto puede tardar un momento.

## Más información {#more-information}

La página web oficial de Apache Sling IDE tooling for Eclipse le proporciona información útil:

* La [**Guía del usuario de herramientas del IDE de Apache Sling para Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentación le guía a través de los conceptos generales, la integración del servidor y las capacidades de implementación admitidas por las herramientas de desarrollo de AEM.
* La [sección de solución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La siguiente documentación oficial de [Eclipse](https://www.eclipse.org/) puede ayudar a configurar su entorno:

* [Introducción a Eclipse](https://eclipseide.org/getting-started/)
* [Sistema de Ayuda de Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)
