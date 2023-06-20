---
title: Herramientas para desarrolladores de AEM para Eclipse
description: Herramientas para desarrolladores de AEM para Eclipse
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 3%

---

# Herramientas para desarrolladores de AEM para Eclipse{#aem-developer-tools-for-eclipse}

![Logotipo de Experience Manager Developer Tools para Eclipse](assets/eclipse-logo.png)

## Información general {#overview}

_Herramientas para desarrolladores de Experience Manager para Eclipse_ es un complemento de Eclipse basado en la variable [Complemento Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lanzado bajo la licencia Apache 2.

AEM Ofrece varias funciones que facilitan el desarrollo de la:

* AEM Integración perfecta con las instancias de la a través del conector del servidor Eclipse
* Sincronización para paquetes OSGi y de contenido
* Compatibilidad de depuración con la capacidad de intercambio en caliente de código
* Bootstrap AEM simple de proyectos de la mediante un asistente de creación de proyectos específico
* Edición sencilla de propiedades JCR

## Requisitos  {#requirements}

AEM Antes de usar las herramientas para desarrolladores de, debe hacer lo siguiente:

* Descargar e instalar [Eclipse IDE para desarrolladores de Enterprise Java™](https://www.eclipse.org/downloads/packages/).
* Configure la instalación de Eclipse para asegurarse de que tiene al menos 1 GB de memoria de pila editando su `eclipse.ini` como se describe en la sección [Preguntas frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>En macOS, debe hacer clic con el botón derecho en **Eclipse.app**, y luego seleccione **Mostrar contenido del paquete** para encontrar su `eclipse.ini`**.**

## AEM Cómo instalar las herramientas para desarrolladores de para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Cuando haya completado la [requisitos](#requirements) más arriba, puede instalar el complemento de la siguiente manera:

1. Abra el [AEM Sitio Web de herramientas para desarrolladores de](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip). <!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Copie el **Vínculo de instalación**.

   Como alternativa, puede descargar un archivo en lugar de utilizar el vínculo de instalación. Este método permite la instalación sin conexión, pero no recibe notificaciones de actualización automáticas faltantes de esta manera.

1. En Eclipse, abra el **Ayuda** menú.
1. Clic **Instalar nuevo software**.
1. Clic **Agregar...**.
1. En el **Nombre** , introduzca `AEM Developer Tools`.
1. En el **Ubicación** , copie la URL de instalación.
1. Clic **Añadir**.
1. Marque ambos **AEM** y **Sling** complementos.
1. Haga clic en **Siguiente**.
1. En el **Detalles de instalación** , haga clic en **Siguiente** otra vez.
1. Acepte los acuerdos de licencia y haga clic en **Finalizar**.
1. Clic **RestartNow** para reiniciar Eclipse.

## AEM La perspectiva de la {#the-aem-perspective}

En Eclipse, una perspectiva determina las acciones y vistas disponibles dentro de una ventana y permite la interacción orientada a tareas con recursos en Eclipse. Para obtener más información sobre Perspective, consulte la [Documentación de Eclipse.](https://help.eclipse.org/latest/index.jsp)

_Herramientas de desarrollo de Experience Manager para Eclipse_ AEM AEM Proporcione una Perspectiva de la que le ofrezca un control total sobre sus Proyectos e instancias de la aplicación. AEM Para abrir la Perspectiva de la:

1. En la barra de menús de Eclipse, seleccione **Ventana** -> **Perspectiva** -> **Abrir perspectiva** -> **Otros**.
1. Seleccionar **AEM** en el cuadro de diálogo y haga clic en **Abrir**.

![AEM La perspectiva de la en Eclipse](assets/eclipse-aem-perspective.png)

## Ejemplo de proyecto de varios módulos {#sample-multi-module-project}

El _Herramientas para desarrolladores de Experience Manager para Eclipse_ viene con un proyecto de muestra y varios módulos que le ayuda a ponerse al día rápidamente con la configuración de un proyecto en Eclipse. AEM También sirve como guía de prácticas recomendadas sobre varias funciones de la. [Más información sobre el Arquetipo del proyecto](https://github.com/adobe/aem-project-archetype).

Siga estos pasos para crear el proyecto de ejemplo:

1. En el **Archivo** > **Nuevo** > **Proyecto** , vaya a la **AEM** y seleccione **AEM Ejemplo de proyecto de varios módulos**.

   ![AEM Ejemplo de proyecto de varios módulos](assets/aem-sample-project.png)

1. Haga clic en **Siguiente**.

   >[!NOTE]
   >
   >Este paso puede tardar un momento, ya que m2eclipse necesita analizar los catálogos de arquetipos.

1. Elegir `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` en el menú, haga clic en **Siguiente**.

   ![Seleccionar versión de arquetipo](assets/select-archetype.png)

1. Proporcione los siguientes campos para el proyecto de ejemplo:

   * **Nombre**
   * **ID de grupo**
   * **ID de artefacto**
   * **appId** - Es posible que tenga que expandir el **Avanzadas** opciones para establecer este valor.
   * **appTitle** - Es posible que tenga que expandir el **Avanzadas** opciones para establecer este valor.
   * **Paquete** - Es posible que tenga que expandir el **Avanzadas** opciones para establecer este valor.

   ![Definir propiedades de arquetipo](assets/archetype-properties.png)

1. Haga clic en **Siguiente**.

1. AEM A continuación, configure un servidor de al que se conecte Eclipse.

   AEM Para utilizar la función del depurador, debe haber empezado a utilizar el modo de depuración, lo que se puede conseguir añadiendo lo siguiente a la línea de comandos:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![AEM Conectar con el servidor de](assets/connect-server.png)

1. Haga clic en **Finalizar**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una instalación nueva (más específicamente, cuando las dependencias de Maven nunca se han descargado), puede obtener el proyecto creado con errores. En este caso, siga el procedimiento descrito en [Resolver definición de proyecto no válida](#resolving-invalid-project-definition).

## Cómo Importar Proyectos Existentes {#how-to-import-existing-projects}

Puede usar el complemento **Nuevo proyecto** para crear la estructura adecuada para usted:

1. Siga las instrucciones para crear un [Ejemplo de proyecto de varios módulos](#sample-multi-module-project) y tiene los siguientes proyectos creados para usted, que permiten una saludable separación de preocupaciones:

   * `PROJECT.ui.apps` para `/apps` y `/etc` content
   * `PROJECT.ui.content` para `/content` que se ha creado
   * `PROJECT.core` para paquetes Java™ (se vuelven interesantes cuando desea agregar código Java™)
   * `PROJECT.it.launcher` y `PROJECT.it.tests` para pruebas de integración

1. Reemplace el contenido de su `PROJECT.ui.apps` proyecto con el `apps` y `etc` carpetas del paquete:

   1. En el panel Explorador de proyectos, despliegue `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Haga clic con el botón derecho en `apps` y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine el `apps` y `etc` carpetas que debería ver ahora y coloque aquí el `apps` y `etc` carpetas del paquete de contenido.
   1. En Eclipse, haga clic con el botón secundario en el `PROJECT.ui.apps` proyecto y elija **Actualizar**.

1. A continuación, haga lo mismo para el `PROJECT.ui.content` y reemplace su carpeta de contenido por la de sus paquetes:

   1. En el panel Explorador de proyectos, despliegue `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Haga clic con el botón derecho en la carpeta de contenido más profunda y elija **Mostrar en** -> **Explorador del sistema**.
   1. Elimine la carpeta de contenido que debería ver ahora y coloque aquí la carpeta de contenido de su paquete de contenido.
   1. En Eclipse, haga clic con el botón secundario en el `PROJECT.ui.content` proyecto y elija **Actualizar**.

1. Ahora tiene que actualizar el `filter.xml` archivos de estos dos proyectos para que se correspondan con el contenido del paquete de contenido. Para ello, abra el `META-INF/vault/filter.xml` del paquete de contenido en un editor de texto/código independiente.

   * Este es un ejemplo de cómo `filter.xml` el archivo puede tener un aspecto:

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

1. En cuanto al contenido del paquete, dividido en dos proyectos, también debe dividir estas reglas de filtro en dos y actualizar en consecuencia el `filter.xml` archivos de los dos proyectos.

   1. En Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Reemplace el contenido del `<workspaceFilter>` con las reglas del paquete que comienzan por `/apps` y `/etc`
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
   1. Reemplace las reglas por las del paquete que empiecen por `/content`.
      * Por ejemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Asegúrese de guardar todos los cambios. AEM Ahora puede sincronizar ese nuevo contenido con la instancia de la.

1. En el panel Servidores, asegúrese de que la conexión se ha iniciado y, en caso contrario, iníciela.
1. Haga clic en **Limpiar y publicar** icono.

Una vez finalizado, el paquete debería estar ejecutándose en la instancia y, al guardarlo, cualquier cambio se sincronizará automáticamente con la instancia.

Si desea volver a compilar un paquete a partir del proyecto, haga clic con el botón derecho en el `PROJECT.ui.apps` o `PROJECT.ui.content` y elija **Ejecutar como** -> **Instalación de Maven**.

Ahora tiene una carpeta de destino creada con el paquete dentro de (llamada, por ejemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Solución de problemas {#troubleshooting}

### Resolver definición de proyecto no válida {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón derecho.
1. En el menú contextual, seleccione **Maven** -> **Actualizar proyectos**.
1. Marque **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **Aceptar**.

Eclipse descarga las dependencias requeridas. Esto puede tardar un momento.

## Más información {#more-information}

La página web oficial de Apache Sling IDE tooling for Eclipse le proporciona información útil:

* El [**Herramientas del IDE de Apache Sling para Eclipse** Guía del usuario](https://sling.apache.org/documentation/development/ide-tooling.html)AEM , esta documentación le guía a través de los conceptos generales, la integración del servidor y las capacidades de implementación admitidas por las herramientas de desarrollo de la.
* El [Sección Resolución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* El [Lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

El siguiente funcionario [Eclipse](https://www.eclipse.org/) La documentación de puede ayudarle a configurar su entorno:

* [Introducción a Eclipse](https://www.eclipse.org/getting-started/)
* [Sistema de ayuda de Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)
