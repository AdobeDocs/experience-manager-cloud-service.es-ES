---
title: Herramientas para desarrolladores de AEM para Eclipse
description: Herramientas para desarrolladores de AEM para Eclipse
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---


# Herramientas para desarrolladores de AEM para Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Información general {#overview}

AEM Developer Tools para Eclipse es un complemento Eclipse basado en el [complemento Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) publicado bajo la Licencia Apache 2.

Oferta varias características que facilitan el desarrollo de AEM:

* Integración perfecta con instancias de AEM mediante el conector de servidor Eclipse
* Sincronización para paquetes de contenido y OSGi
* Compatibilidad con depuración con capacidad de intercambio de código en caliente
* Arranque simple de AEM proyectos mediante un Asistente para la creación de proyectos específico
* Fácil edición de las propiedades de JCR

## Requisitos {#requirements}

Antes de utilizar las herramientas de desarrollo de AEM, debe:

* Descargue e instale [Eclipse IDE para desarrolladores de Java empresariales](https://www.eclipse.org/downloads/packages/).
* Configure la instalación de eclipse para asegurarse de que tiene al menos 1 gigabyte de memoria de pila editando su archivo de configuración `eclipse.ini` como se describe en las [Preguntas más frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>En macOS, debe hacer clic con el botón derecho en **Eclipse.app** y luego seleccionar **Mostrar contenido del paquete** para encontrar su `eclipse.ini`**.**

## Cómo instalar las herramientas para desarrolladores de AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Una vez que haya cumplido los [requisitos](#requirements) anteriores, puede instalar el complemento de la siguiente manera:

1. Abra el [sitio Web de herramientas para desarrolladores de AEM.](https://eclipse.adobe.com/aem/dev-tools/)

1. Copie el **Vínculo de instalación**.

   Tenga en cuenta que, como alternativa, puede descargar un archivo en lugar de utilizar el vínculo de instalación. Esto permite la instalación sin conexión, pero se perderán las notificaciones de actualización automática de esta manera.

1. En Eclipse, abra el menú **Ayuda**.
1. Haga clic en **Instalar nuevo software**.
1. Haga clic en **Agregar...**.
1. En **Nombre** escriba `AEM Developer Tools`.
1. En **Ubicación** copie la dirección URL de instalación.
1. Haga clic en **Agregar**.
1. Compruebe los complementos **AEM** y **Sling**.
1. Haga clic en **Siguiente**. 
1. En la ventana **Instalar detalles**, haga clic en **Siguiente** nuevamente.
1. Acepte los acuerdos de licencia y haga clic en **Finalizar**.
1. Haga clic en **RestartNow** para reiniciar Eclipse.

## La perspectiva AEM {#the-aem-perspective}

En Eclipse, una perspectiva determina las acciones y vistas disponibles en una ventana y permite la interacción orientada a la tarea con los recursos en Eclipse. Para obtener más información sobre Perspectiva, consulte la documentación de [Eclipse.](https://help.eclipse.org)

Las Herramientas de desarrollo AEM para Eclipse proporcionan una Perspectiva AEM que le oferta el control total sobre sus proyectos e instancias de AEM. Para abrir la Perspectiva de AEM:

1. En la barra de menús Eclipse, seleccione **Ventana** -> **Perspectiva** -> **Abrir perspectiva** -> **Otro**.
1. Seleccione **AEM** en el cuadro de diálogo y haga clic en **Abrir**.

![La perspectiva AEM en Eclipse](assets/eclipse-aem-perspective.png)

## Proyecto de módulo múltiple de muestra {#sample-multi-module-project}

Las herramientas para desarrolladores de AEM para Eclipse incluyen un proyecto multimódulo de muestra que le ayuda a ponerse al día rápidamente con la configuración de un proyecto en Eclipse, además de servir como guía de prácticas recomendadas para varias funciones de AEM. [Obtenga más información sobre el arquetipo](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) del proyecto.

Siga estos pasos para crear el proyecto de ejemplo:

1. En el menú **Archivo** > **Nuevo** > **Proyecto**, vaya a la sección **AEM** y seleccione **AEM Ejemplo de proyecto de módulos múltiples**.

   ![AEM ejemplo de proyecto multimódulo](assets/aem-sample-project.png)

1. Haga clic en **Siguiente**. 

   >[!NOTE]
   >
   >Este paso puede tardar un momento, ya que m2eclipse necesita analizar los catálogos de arquetipos.

1. Elija `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` en el menú y haga clic en **Siguiente**.

   ![Seleccionar versión de arquetipo](assets/select-archetype.png)

1. Proporcione los siguientes campos para el proyecto de ejemplo:

   * **Nombre**
   * **Id. de grupo**
   * **ID del artefacto**
   * **appId** : es posible que tenga que expandir las opciones  **** avanzadas para establecer este valor.
   * **appTitle** : Es posible que tenga que expandir las opciones  **** avanzadas para establecer este valor.
   * **Paquete** : es posible que tenga que expandir las opciones  **** avanzadas para establecer este valor.

   ![Definir propiedades de arquetipo](assets/archetype-properties.png)

1. Haga clic en **Siguiente**. 

1. A continuación, configure un servidor AEM al que se conectará Eclipse.

   Para utilizar la función de depurador, debe haber empezado a AEM en modo de depuración, lo que se puede lograr, por ejemplo, añadiendo lo siguiente a la línea de comandos:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Conectar con AEM servidor](assets/connect-server.png)

1. Haga clic en **Finalizar**. Se crea la estructura del proyecto.

   >[!NOTE]
   >
   >En una instalación nueva (más concretamente, cuando nunca se han descargado dependencias), es posible que el proyecto se cree con errores. En este caso, siga el procedimiento descrito en [Resolución de definiciones de proyecto no válidas](#resolving-invalid-project-definition).

## Cómo importar proyectos existentes {#how-to-import-existing-projects}

Puede utilizar la función **Nuevo proyecto** para crear la estructura adecuada:

1. Siga las instrucciones para crear un [Proyecto Módulo múltiple de muestra](#sample-multi-module-project) y tendrá los siguientes proyectos creados para usted, lo que permitirá una saludable separación de preocupaciones:

   * `PROJECT.ui.apps` para  `/apps` y  `/etc` contenido
   * `PROJECT.ui.content` para  `/content` que se crea
   * `PROJECT.core` para los paquetes Java (se volverán interesantes en cuanto desee agregar código Java)
   * `PROJECT.it.launcher` y  `PROJECT.it.tests` para pruebas de integración

1. Reemplace el contenido del proyecto `PROJECT.ui.apps` por las carpetas `apps` y `etc` del paquete:

   1. En el panel Explorador de proyectos, despliegue `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Haga clic con el botón derecho en la carpeta `apps` y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine las carpetas `apps` y `etc` que debe ver y coloque aquí las carpetas `apps` y `etc` del paquete de contenido.
   1. En Eclipse, haga clic con el botón derecho en el proyecto `PROJECT.ui.apps` y elija **Actualizar**.

1. A continuación, haga lo mismo con el `PROJECT.ui.content` y sustituya su carpeta de contenido por la del paquete:

   1. En el panel Explorador de proyectos, despliegue `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Haga clic con el botón derecho en la carpeta de contenido más profunda y elija **Mostrar en** -> **Explorador del sistema**.
   1. Elimine la carpeta de contenido que debería ver y coloque aquí la carpeta de contenido del paquete de contenido.
   1. En Eclipse, haga clic con el botón derecho en el proyecto `PROJECT.ui.content` y elija **Actualizar**.

1. Ahora tiene que actualizar los `filter.xml` archivos de estos dos proyectos para que correspondan al contenido del paquete de contenido. Para ello, abra el archivo `META-INF/vault/filter.xml` del paquete de contenido en un editor de texto/código independiente.

   * Este es un ejemplo de cómo puede verse su archivo `filter.xml`:

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

1. En cuanto al contenido del paquete que se dividió en dos proyectos, también tendrá que dividir estas reglas de filtro en dos y actualizar en consecuencia los archivos `filter.xml` de los dos proyectos.

   1. En Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Reemplace el contenido del elemento `<workspaceFilter>` por las reglas del paquete que inicio con `/apps` y `/etc`
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
   1. Reemplace las reglas con las del paquete que inicio con `/content`.
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

1. En el panel Servidores, asegúrese de que la conexión se ha iniciado y, si no, de que no se ha iniciado el inicio.
1. Haga clic en el icono **Limpiar y publicar**.

Una vez finalizado, el paquete se debe ejecutar en la instancia y, al guardarlo, cualquier cambio se sincronizará automáticamente con la instancia.

Si desea volver a crear un paquete a partir de su proyecto, haga clic con el botón derecho en `PROJECT.ui.apps` o `PROJECT.ui.content` y elija **Ejecutar como** -> **Instalación de Maven**.

Ahora tiene una carpeta de destinatario que se ha creado con el paquete dentro (llamada, por ejemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Solución de problemas {#troubleshooting}

### Resolución de definiciones de proyecto no válidas {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón secundario.
1. En el menú contextual, seleccione **Maven** -> **Actualizar proyectos**.
1. Marque **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **Aceptar**.

Eclipse descarga las dependencias necesarias. Esto puede tomar un momento.

## Más información {#more-information}

El sitio web oficial del IDE de Apache Sling para Eclipse le proporciona información útil:

* La [**Guía del usuario del IDE de Apache Sling para Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html), esta documentación le guiará a través de los conceptos generales, la integración del servidor y las capacidades de implementación que soportan las Herramientas de desarrollo de AEM.
* La sección [Resolución de problemas](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* La [lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

La siguiente documentación oficial de [Eclipse](https://eclipse.org/) puede ayudarle a configurar su entorno:

* [Introducción a Eclipse](https://eclipse.org/users/)
* [Sistema de ayuda de Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)
