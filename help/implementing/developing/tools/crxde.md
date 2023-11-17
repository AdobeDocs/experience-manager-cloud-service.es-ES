---
title: Uso del CRXDE Lite
description: El CRXDE Lite AEM forma parte del inicio rápido de la y está disponible para acceder y modificar el repositorio en los entornos de desarrollo local dentro del explorador.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: e2505c0fec1da8395930f131bfc55e1e2ce05881
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 2%

---

# Uso del CRXDE Lite {#using-crxde-lite}

El CRXDE Lite AEM forma parte del inicio rápido de la y está disponible para acceder y modificar el repositorio en los entornos de desarrollo local dentro del explorador. Con CRXDE Lite, puede editar archivos, carpetas, nodos y propiedades. Todo el repositorio es accesible para usted en esta interfaz fácil de usar.

>[!NOTE]
>
>CRXDE Lite solo está disponible en los entornos de desarrollo local. AEM No está disponible en el as a Cloud Service de la.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para empezar a usar CRXDE Lite:

1. AEM Inicie el inicio rápido del desarrollo de la local.
1. En el explorador, abra la dirección URL `https://<host>:<port>/crx/de`.
1. Introduzca su **nombre de usuario** y **contraseña**.
1. Haga clic en **Aceptar**.

La interfaz de usuario del CRXDE Lite aparece de la siguiente manera en el explorador:

![La interfaz del CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>También puede acceder a CRXDE Lite AEM desde el menú de. En el menú principal, seleccione **Herramientas** -> **General** -> **CRXDE Lite**.

## Información general sobre la interfaz de usuario {#overview-of-the-user-interface}

La interfaz de usuario del CRXDE Lite tiene muchas partes y muchas funciones.

### Barra de conmutación superior {#top-switcher-bar}

La barra de cambio superior le permite cambiar rápidamente entre CRXDE Lite y [Administrador de paquetes.](package-manager.md)

### Widget de ruta del nodo {#node-path-widget}

El widget Ruta del nodo muestra la ruta al nodo seleccionado actualmente.

También puede usarlo para saltar a un nodo al introducir la ruta a mano o pegarla desde otro lugar y pulsar Intro.

También es compatible con la búsqueda de nodos con un nombre de nodo específico. Introduzca el nombre del nodo que desea buscar y espere (o seleccione el icono de búsqueda en el lado derecho). Si se carga un nodo o nodos determinados en el panel del explorador, se muestra la lista y puede seleccionar la ruta y pulsar Entrar para desplazarse hasta ella. Tenga en cuenta que solo funciona para los nodos cargados actualmente en la aplicación cliente CRXDE en el explorador. Si desea buscar en todo el repositorio, utilice **Herramientas** ->: **Consulta**.

### Panel del explorador {#explorer-pane}

El **Panel del explorador** muestra un árbol de todos los nodos del repositorio.

Haga clic en un nodo para mostrar sus propiedades en la **Propiedades** pestaña. Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.

El filtro de navegación de árbol (el icono de prismáticos) permite filtrar los nodos del repositorio para los que el nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.

### Panel de edición {#edit-pane}

El **Panel de edición** permite ver el contenido del archivo seleccionado actualmente en el repositorio. Cada archivo abierto se representa como su propia pestaña en el panel.

El **Inicio** La pestaña permite buscar contenido o documentación y acceder a documentación para desarrolladores y a asistencia de Adobe.

Haga doble clic en un archivo de **Panel del explorador** para mostrar su contenido en la **Panel de edición**. A continuación, puede modificarla y guardar los cambios.

Una vez editado un archivo en la **Panel de edición**, las siguientes herramientas están disponibles en la barra de herramientas:

* **Mostrar en el árbol** - Muestra el archivo en el árbol del repositorio.
* **Buscar/Reemplazar** : realiza una búsqueda o un reemplazo.

Haga doble clic en la línea de estado del **Panel de edición** abre el **Ir a línea** para que pueda introducir un número de línea específico.

### Pestaña Propiedades {#properties-tab}

El **Pestaña Propiedades** muestra las propiedades del nodo que ha seleccionado. Puede añadir nuevas propiedades o eliminar las existentes.

### Pestaña Control de acceso {#access-control-tab}

El **Pestaña Control de acceso** muestra los permisos en función de la ruta, repositorio o principal actual.

Los permisos se dividen en las siguientes categorías.

* **Política de control de acceso aplicable** - Las directivas que se pueden aplicar a la selección actual
* **Políticas de control de acceso local** - Las políticas actuales aplicadas localmente a la selección actual
* **Políticas de control de acceso efectivas** : las directivas actuales aplicadas a la selección actual, que pueden configurarse localmente o heredarse de nodos principales

>[!NOTE]
>
Para poder ver la información de control de acceso, el usuario que ha iniciado sesión en el CRXDE Lite debe tener derechos para leer las entradas ACL.

### Pestaña Replicación {#replication-tab}

El **Pestaña Replicación** muestra el estado de replicación del nodo actual. Puede replicar y replicar y eliminar el nodo actual.

### Pestaña Consola {#console-tab}

El **Pestaña Consola** muestra los mensajes de registros. Puede configurar el nivel de registro, borrar la consola, fijar la posición de desplazamiento seleccionada y activar o desactivar la visualización de mensajes.

### Pestaña Información de compilación {#build-info-tab}

El **Pestaña Información de compilación** muestra información cuando se está creando un paquete.

### Botón Actualizar {#refresh-button}

El **Botón Actualizar** actualiza la selección actual. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios que ha realizado no se ven afectados.

### Botón Guardar todo {#save-all-button}

El **Botón Guardar todo** guarda todos los cambios realizados. Hasta que elija guardar, los cambios son temporales y se pierden al salir de la consola.

* **Revertir** - Descarta todos los cambios realizados en el nodo seleccionado desde la última acción de guardado y vuelve a cargar el estado actual del repositorio para el nodo seleccionado
* **Revertir todo** - Descarta todos los cambios realizados en todo el repositorio desde la última acción de guardado y vuelve a cargar el estado actual del repositorio

### Botón Crear {#create-button}

El **Botón Crear** es un menú desplegable para crear lo siguiente en el nodo seleccionado:

* Nodo: un nodo con un tipo de nodo arbitrario.
* Archivo: un `nt:file` nodo y su subnodo nt:resource
* Carpeta: una `nt:folder` nodo

### Botón Eliminar {#delete-button}

El **Botón Eliminar** elimina el nodo seleccionado.

### Botón Copiar {#copy-button}

El **Botón Copiar** copia el nodo seleccionado.

## Botón Pegar {#paste-button}

El **Botón Pegar** pega el nodo copiado bajo el nodo seleccionado.

### Botón Mover {#move-button}

El **Botón Mover** mueve el nodo seleccionado al nodo definido mediante el cuadro de diálogo.

### Cambiar nombre {#rename-button}

El **Botón Cambiar nombre** cambia el nombre del nodo seleccionado.

### Mixins {#mixins-button}

El **Botón Mixins** permite añadir tipos de mezcla al tipo de nodo. Los tipos de mixin se utilizan principalmente para añadir funciones avanzadas.

### Herramientas {#tools-button}

El **Botón Herramientas** es un menú desplegable con las siguientes herramientas disponibles:

* **Configuración del servidor** - para acceder a la consola Felix (también disponible en `https://<host>:<port>/system/console/configMgr`)
* **Consulta** - para consultar el repositorio
* **Privilegios** : para ver y agregar privilegios
* **Probar control de acceso** : para probar el permiso para una ruta o principal determinados
* **Exportar tipo de nodo** - para exportar tipos de nodo en el sistema como notación CDN
* **Importar tipo de nodo** : para importar tipos de nodos utilizando la notación CDN.

### Widget de inicio {#login-widget}

El **Widget de inicio** muestra el usuario que ha iniciado sesión actualmente.

Haga clic en él para iniciar sesión o volver a iniciarla como otro usuario. El `@crx.default` representa que se encuentra en el espacio de trabajo predeterminado (y solo) del repositorio.

El **Preferencias** se puede utilizar para establecer el idioma de la interfaz de usuario y para ver y personalizar las teclas de marcación rápida para varias acciones como guardar, buscar, crear notas, etc.

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desea crear la nueva carpeta y seleccione **Crear...**, entonces **Crear carpeta...**.

1. Introduzca la carpeta **Nombre** y haga clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de un nodo {#creating-a-node}

Para crear un nodo con un CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el [**Panel Explorador**,](#explorer-pane) haga clic con el botón derecho en el nodo en el que desee crear el nuevo nodo y seleccione **Crear**, entonces **Crear nodo**.
1. Introduzca el **Nombre** y seleccione la **Tipo**.
1. Haga clic en **Aceptar**.
1. Haga clic en [**Botón Guardar todo**](#save-all-button) para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nuevos nodos.

>[!NOTE]
>
La mayoría de las operaciones de edición, incluidas **Crear nodo**, guarda todos los cambios en la memoria y solo los almacena en el repositorio al guardarlos (mediante el [**Botón Guardar todo**](#save-all-button)). Sin embargo, algunas operaciones, como mover, persisten automáticamente.
>
El repositorio también lleva a cabo la validación con respecto a si el tipo de nodo del nodo principal permite el nodo recién creado al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un `nt:unstructured` nodo como elemento secundario de `nt:folder` node).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el [**Panel Explorador**,](#explorer-pane) seleccione el nodo en el que desea agregar la nueva propiedad.
1. En el [**Pestaña Propiedades**](#properties-tab) en el panel inferior, introduzca la variable **Nombre**, el **Tipo**, y el **Valor**.
1. Clic **Añadir**.
1. Haga clic en [**Botón Guardar todo**](#save-all-button) para guardar los cambios en el servidor.

## Creación de un archivo {#creating-a-file}

Para crear un archivo con el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. En el [**Panel Explorador**,](#explorer-pane) haga clic con el botón derecho en el componente donde desee crear el archivo y seleccione **Crear**, entonces **Crear archivo**.
1. Introduzca el archivo **Nombre** incluida su extensión.
1. Haga clic en **Aceptar**.
1. El nuevo archivo se abre como una pestaña en la [**Panel de edición**.](#edit-pane)
1. Edite el archivo.
1. Haga clic en [**Botón Guardar todo**](#save-all-button) para guardar los cambios.

## Exportación e importación de tipos de nodo {#exporting-and-importing-node-types}

Con CRXDE Lite puede importar o exportar definiciones de tipo de nodo en [Notación Compact Namespace y Node Type Definition (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar una definición de tipo de nodo en el CRXDE Lite:

1. Abra el CRXDE Lite en el explorador.
1. Seleccione el nodo requerido.
1. Seleccionar **Herramientas** entonces **Exportar tipo de nodo**.
1. La definición se muestra en notación CDN en una nueva pestaña del explorador.
1. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra el CRXDE Lite en el explorador.
1. Seleccionar **Herramientas** entonces **Importar tipo de nodo**.
1. Se abre una nueva pestaña en [**Panel de edición**](#edit-pane) etiquetado **Importar tipo de nodo**.
1. Introduzca la notación CDN para la definición en el cuadro de texto de **Importar tipo de nodo** pestaña.
1. Marque **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con CRXDE Lite puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos en `<aem-install-dir>/crx-quickstart/logs` y filtrarlo con el nivel de registro adecuado. Proceda como se indica a continuación:

1. Abra el CRXDE Lite en el explorador.
1. En, en el menú desplegable de la derecha de [**Pestaña Consola**](#console-tab) en la parte inferior de la ventana, seleccione **Registros de servidor**.
1. Haga clic en **Detener** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Felix haciendo clic en el **Configuraciones de registro** icono.
* Borre los mensajes haciendo clic en el **Borrar consola** icono.
* Anclar el mensaje en la selección actual haciendo clic en **Fijar consola** icono.
* Habilite o deshabilite la visualización de mensajes haciendo clic en **Detener** icono.
