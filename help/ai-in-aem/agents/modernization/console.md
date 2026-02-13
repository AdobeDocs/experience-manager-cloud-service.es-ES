---
title: Consola de modernización de Experience
description: Guía de referencia para la interfaz y las funciones de la consola de modernización de Experience
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 43d8c124-fc87-4cec-a91d-ab12255ae321
source-git-commit: 76c0f41acb5c2e4e0f0a292f8205b0b9de5cda81
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---


# Consola de modernización de Experience {#console-reference}

Guía de referencia para la interfaz y las funciones de la consola de modernización de Experience

>[!NOTE]
>
>Si está interesado en utilizar la consola de modernización de experiencias, puede solicitar acceso para garantizar una experiencia de incorporación sin problemas.

## Información general {#overview}

La consola de modernización de la experiencia es un entorno de desarrollo alojado y asistido por IA para Edge Delivery Services, que se expone como interfaz web en [`aemcoder.adobe.io`.](https://aemcoder.adobe.io) Después de conectarse a su proyecto de GitHub, puede empezar a solicitar inmediatamente cambios en lenguaje natural sin tener que realizar más ajustes o configuraciones de entorno local.

>[!TIP]
>
>Si está interesado en empezar de inmediato con la consola, consulte el documento [Introducción al agente de modernización de experiencias.](/help/ai-in-aem/agents/modernization/getting-started.md)

## Capacidades {#capabilities}

Funciones principales de la consola:

* Panel de chat interactivo con el agente y sus aptitudes
* Vista previa de Live AEM para obtener comentarios visuales inmediatos sobre los cambios
* Explorador de archivos de contenido y visor de markdown
* Sincronización de contenido con [Document Authoring](https://da.live)
* Explorador de códigos y visor de diferencias para revisar los cambios realizados
* Integración de GitHub con capacidad para crear solicitudes de extracción a partir de cambios

Los desarrolladores conservan el control total sobre lo que se envía. Todos los cambios realizados a través de la consola requieren revisión y aprobación antes de la implementación, lo que garantiza el control, la coherencia de la marca y la seguridad.

## Navegación {#navigation}

Después de iniciar sesión en la consola a las [`aemcoder.adobe.io`,](https://aemcoder.adobe.io), llegará a la pantalla principal de la consola.

![Pantalla principal de la consola](assets/console-home.png)

### Barra de menús {#menu-bar}

La barra de menús superior proporciona lo siguiente:

* Un botón **Abrir menú** a la izquierda para expandir y contraer el detalle del panel lateral izquierdo
* Un botón **Account** a la derecha para cambiar al modo oscuro y cerrar sesión en la consola

### Barra lateral izquierda {#sidebar}

La barra lateral izquierda permite un acceso rápido a vistas importantes de la consola.

* **[Vista de página principal](#home-view)** (icono de la casa): el punto de partida para usar la consola
* **[Vista de contenido](#content-view)** (icono de archivo): contenido que ha importado
* **[Vista de código](#code-view)** (`</>` icono): código del sitio en el que está trabajando
* **[Vista de configuración](#settings-view)** (icono de engranaje): configuración de la consola

## Vista de inicio {#home-view}

La vista **Home** es el punto de partida para usar la consola.

* En la parte superior hay un [panel de solicitud](#prompt-panel) para realizar solicitudes de la consola.
* Debajo del panel de mensajes se sugieren mensajes que se deben utilizar para iniciar el proyecto.

### Panel Preguntar {#prompt-panel}

El panel de mensajes proporciona controles para interactuar con la IA.

* **Modos de planificación/ejecución** (iconos de bombilla y varita mágica): alternar entre los modos de planificación y ejecución, respectivamente
   * **Modo de planificación**: la IA analiza las solicitudes y describe un método sin realizar cambios, lo que resulta útil para comprender la estrategia antes de comprometerse.
   * **Modo de ejecución**: la API lleva a cabo el plan y realiza cambios en el archivo.
* **Adjuntar archivos** (icono de clip): cargue y adjunte archivos al mensaje para obtener contexto adicional (por ejemplo, diseños de referencia, capturas de pantalla, especificaciones técnicas)
* **Configuración** (icono de engranaje): elige omitir las preguntas de confirmación de la API
* **Borrar chat**: Esto restablece la conversación y borra la ventana de contexto de la IA. Utilice esta opción cuando inicie una nueva tarea que no esté relacionada con la conversación anterior.

## Vista de contenido {#content-view}

La **vista de contenido** proporciona herramientas para examinar y obtener una vista previa del contenido. De forma predeterminada, la vista se divide en tres paneles, de izquierda a derecha:

* Panel Preguntar para interactuar con la consola y el proyecto
* Explorador de archivos para obtener una descripción general de los archivos de contenido (alternar que muestra este panel con el icono de cheurón)
* Panel de vista previa para visualizar el contenido seleccionado en el explorador de archivos

![Vista de contenido](assets/content-imported.png)

El panel de vista previa ofrece tres modos:

* **Vista previa** (documento con lupa) para ver el contenido de HTML procesado
* **Vista de HTML** (icono de documento) para ver la estructura de contenido de creación de documentos subyacente, respectivamente
* **Modo de diseño** (icono de pincel) para seleccionar elementos de la página para el contexto del mensaje

Siempre puede hacer clic en el icono **Actualizar vista previa** para actualizar el panel de vista previa.

El botón **Cargar contenido** abre una ventana modal para cargar archivos en AEM Document Authoring.

* El campo **Organización** y **Repositorio** se han rellenado previamente si el proyecto tiene un archivo de `fstab.yaml`
* La selección de archivos proporciona rutas de destino editables
* No se admite la carga en JCR (para el editor universal)

![Cargar contenido](assets/upload-content.png)

## Vista de código {#code-view}

La **vista Código** proporciona herramientas para examinar el código y administrar los cambios en el código. La vista se divide en tres paneles, de izquierda a derecha:

* Panel Preguntar para interactuar con la consola y el proyecto
* Explorador de archivos para obtener una descripción general de los archivos de código o cambios como diferencias
* Panel de vista previa para ver un archivo de código o una comparación seleccionada en el explorador de archivos

![Vista de código](assets/code-view.png)

El panel de vista previa ofrece dos modos diferentes:

* **Archivos de Workspace** para examinar los archivos de código del área de trabajo actual
* **Cambios de Git** para ver las diferencias de los cambios de archivos creados por su trabajo en el proyecto
   * Haga clic en el icono `+` para almacenar en zona intermedia el archivo modificado
   * Haga clic en el icono de flecha para descartar el archivo modificado

El icono **Información** enumera tu cuenta y proyecto de GitHub conectado actualmente.

El menú **Acciones de GitHub** (parte superior derecha) proporciona operaciones del repositorio.

* **Conectar/Volver a conectar**: inicia OAuth en GitHub
* **Repositorio de cambios**: reemplaza el área de trabajo por un repositorio diferente. Se perderá cualquier trabajo no comprometido.
* **Cambiar rama**: cambia ramas dentro del mismo repositorio
* **Sincronizar**: extrae los cambios más recientes del origen remoto
* **Push**: abre un modal para insertar los cambios del espacio de trabajo en GitHub
* **Cerrar sesión**: se desconecta de GitHub

Al insertar cambios, primero debe tener cambios clasificados para incluirlos en la notificación push. Al insertar, puede elegir crear una nueva PR o insertar directamente en la rama actual

![Cambios push](assets/push-changes.png)

## Vista de configuración {#settings-view}

La vista de configuración permite administrar la configuración básica de la consola.

![Vista de configuración](assets/settings-view.png)

* **Credentials** le permite especificar un token de acceso personal para Figma para que la consola pueda acceder a los bloques de diseño de su proyecto.
* **Restablecer espacio de trabajo** revierte la consola a su estado inicial y se perderán todos los cambios no insertados o no cargados.
