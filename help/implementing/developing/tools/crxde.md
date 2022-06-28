---
title: Uso del CRXDE Lite
description: CRXDE Lite es parte del inicio rápido AEM y está disponible para que acceda y modifique el repositorio en los entornos de desarrollo local dentro del explorador.
exl-id: 1581a7e5-6f84-4a45-8e8f-c83692ea077a
source-git-commit: a9c646d24378e67df84c00a4355c692cac85e50b
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 3%

---

# Uso del CRXDE Lite {#using-crxde-lite}

CRXDE Lite es parte del inicio rápido AEM y está disponible para que acceda y modifique el repositorio en los entornos de desarrollo local dentro del explorador. Con CRXDE Lite, puede editar archivos, carpetas, nodos y propiedades. Todo el repositorio es accesible para usted en esta interfaz fácil de usar.

>[!NOTE]
>
>CRXDE Lite solo está disponible en los entornos de desarrollo local. No está disponible en AEM as a Cloud Service.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para empezar con CRXDE Lite:

1. Inicie el inicio rápido del desarrollo de AEM local.
1. En el explorador, abra la dirección URL `https://<host>:<port>/crx/de`.
1. Escriba la **username** y **password**.
1. Haga clic en **Aceptar**.

La interfaz de usuario del CRXDE Lite aparece de la siguiente manera en el explorador:

![La interfaz del CRXDE Lite](assets/crxde-lite.png)

>[!TIP]
>
>También puede acceder al CRXDE Lite desde el menú AEM. En el menú principal, seleccione **Herramientas** -> **General** -> **CRXDE Lite**.

## Descripción general de la interfaz de usuario {#overview-of-the-user-interface}

La interfaz de usuario del CRXDE Lite tiene muchas partes y muchas funciones.

### Barra de alternador superior {#top-switcher-bar}

La barra de cambio superior le permite cambiar rápidamente entre el CRXDE Lite y [Administrador de paquetes.](package-manager.md)

### Widget de ruta de acceso de nodo {#node-path-widget}

El widget Ruta de nodo muestra la ruta al nodo seleccionado actualmente.

También puede utilizarla para saltar a un nodo introduciendo la ruta manualmente o pegándola desde otro lugar y pulsando Intro.

También proporciona soporte para buscar nodos con un nombre de nodo específico. Introduzca el nombre del nodo que desea buscar y espere (o seleccione el icono de búsqueda en el lado derecho). Si un nodo o nodos dados se cargan en el panel del explorador, se mostrará la lista y puede seleccionar la ruta y pulsar Intro para desplazarse hasta ella. Tenga en cuenta que solo funciona para los nodos cargados actualmente en la aplicación cliente CRXDE en el explorador. Si desea buscar en todo el repositorio, utilice **Herramientas** ->: **Consulta**.

### Panel Explorador {#explorer-pane}

La variable **Panel Explorador** muestra un árbol de todos los nodos del repositorio.

Haga clic en un nodo para mostrar sus propiedades en la **Propiedades** pestaña . Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.

El filtro de navegación de árbol (el icono de binoculares) permite filtrar los nodos del repositorio para los que el nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.

### Panel Editar {#edit-pane}

La variable **Panel Editar** permite ver el contenido del archivo seleccionado actualmente en el repositorio. Cada archivo abierto se representará como su propia ficha en el panel.

La variable **Página principal** pestaña le permite buscar contenido o documentación y acceder a la documentación para desarrolladores y a la asistencia de Adobe.

Haga doble clic en un archivo de la **Panel Explorador** para mostrar su contenido en la **Panel Editar**. A continuación, puede modificarlo y guardar los cambios.

Una vez que se edita un archivo en la variable **Panel Editar**, las siguientes herramientas están disponibles en la barra de herramientas:

* **Mostrar en el árbol** - Muestra el archivo en el árbol del repositorio.
* **Buscar/Reemplazar** : realiza una búsqueda o un reemplazo.

Haga doble clic en la línea de estado de la variable **Panel Editar** abre el **Ir a la línea** para que pueda introducir un número de línea específico.

### Pestaña Propiedades {#properties-tab}

La variable **Ficha Propiedades** muestra las propiedades del nodo seleccionado. Puede agregar nuevas propiedades o eliminar las existentes.

### Ficha Control de acceso {#access-control-tab}

La variable **Ficha Control de acceso** muestra los permisos en función de la ruta actual, el repositorio o el principal.

Los permisos se dividen en las siguientes categorías.

* **Política de control de acceso aplicable** - Las políticas que se pueden aplicar a la selección actual
* **Políticas de control de acceso local** - Las políticas actuales aplicadas localmente a la selección actual
* **Políticas de control de acceso efectivas** - Las políticas actuales aplicadas a la selección actual, que pueden establecerse localmente o heredarse de los nodos principales

>[!NOTE]
Para poder ver la información de control de acceso, el usuario que ha iniciado sesión en el CRXDE Lite debe tener derechos para leer entradas ACL.

### Pestaña Replicación {#replication-tab}

La variable **Pestaña Replicación** muestra el estado de replicación del nodo actual. Puede replicar y replicar la eliminación del nodo actual.

### Ficha Consola {#console-tab}

La variable **Ficha Consola** muestra los mensajes de &quot;logs&quot;. Puede configurar el nivel de registro, borrar la consola, fijar en la posición de desplazamiento seleccionada y activar o desactivar la visualización de los mensajes.

### Ficha Información de compilación {#build-info-tab}

La variable **Ficha Información de compilación** muestra información cuando se crea un paquete.

### Botón Actualizar {#refresh-button}

La variable **Botón Actualizar** actualiza la selección actual. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios realizados no se ven afectados.

### Botón Guardar todo {#save-all-button}

La variable **Botón Guardar todo** guarda todos los cambios realizados. Hasta que elija guardar, los cambios son temporales y se perderán al salir de la consola.

* **Revertir** : descarta todos los cambios realizados en el nodo seleccionado desde la última acción de guardado y luego vuelve a cargar el estado actual del repositorio para el nodo seleccionado
* **Revertir todo** : descarta todos los cambios realizados en todo el repositorio desde la última acción de guardado y luego vuelve a cargar el estado actual del repositorio

### Botón Crear {#create-button}

La variable **Botón Crear** es un menú desplegable para crear lo siguiente en el nodo seleccionado:

* Nodo: un nodo con un tipo de nodo arbitrario
* Archivo: un `nt:file` node y su subnodo nt:resource
* Carpeta: una `nt:folder` node

### Botón Eliminar {#delete-button}

La variable **Botón Eliminar** elimina el nodo seleccionado.

### Botón Copiar {#copy-button}

La variable **Botón Copiar** copia el nodo seleccionado.

## Botón Pegar {#paste-button}

La variable **Botón Pegar** pega el nodo copiado debajo del nodo seleccionado.

### Botón Mover {#move-button}

La variable **Botón Mover** mueve el nodo seleccionado al nodo configurado a través del cuadro de diálogo.

### Cambiar nombre {#rename-button}

La variable **Botón Cambiar nombre** cambia el nombre del nodo seleccionado.

### Mezclas {#mixins-button}

La variable **Botón Mixs** permite añadir tipos de mezcla al tipo de nodo. Los tipos de mezcla se utilizan principalmente para añadir características avanzadas.

### Herramientas {#tools-button}

La variable **Botón Herramientas** es un menú desplegable con las siguientes herramientas disponibles:

* **Configuración del servidor** - para acceder a la Consola Felix (también disponible en `https://<host>:<port>/system/console/configMgr`)
* **Consulta** - para consultar el repositorio
* **Privilegios** - para ver y agregar privilegios
* **Control de acceso de prueba** - para probar el permiso de una ruta determinada y/o principal
* **Exportar tipo de nodo** - para exportar tipos de nodos en el sistema como notación CND
* **Importar tipo de nodo** - para importar tipos de nodos usando notación CND.

### Widget de inicio de sesión {#login-widget}

La variable **Widget de inicio de sesión** muestra el usuario que ha iniciado sesión.

Haga clic en él para iniciar sesión o volver a iniciarla como otro usuario. La variable `@crx.default` representa que está en el espacio de trabajo predeterminado (y solo) en el repositorio.

La variable **Preferencias** se puede usar para definir el idioma de la interfaz de usuario y para ver y personalizar las teclas de marcación rápida para diversas acciones como guardar, buscar, crear nota, etc.

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con el CRXDE Lite :

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desee crear la nueva carpeta y seleccione **Crear...**, luego **Crear carpeta ...**.

1. Introduzca la carpeta **Nombre** y haga clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de un nodo {#creating-a-node}

Para crear un nodo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el [**Panel Explorador**,](#explorer-pane) haga clic con el botón derecho en el nodo en el que desee crear el nuevo nodo, seleccione **Crear**, luego **Crear nodo**.
1. Introduzca la variable **Nombre** y seleccione **Tipo**.
1. Haga clic en **Aceptar**.
1. Haga clic en el [**Botón Guardar todo**](#save-all-button) para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nuevos nodos.

>[!NOTE]
La mayoría de las operaciones de edición, incluidas las **Crear nodo**, guarda todos los cambios en la memoria y solo los almacena en el repositorio al guardarlos (mediante el [**Botón Guardar todo**](#save-all-button)). Sin embargo, algunas operaciones como mover se mantienen automáticamente.
El repositorio también lleva a cabo la validación con respecto a si el tipo de nodo del nodo principal permite el nodo recién creado al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un `nt:unstructured` como nodo secundario de `nt:folder` nodo ).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el [**Panel Explorador**,](#explorer-pane) seleccione el nodo en el que desea añadir la nueva propiedad.
1. En el [**Ficha Propiedades**](#properties-tab) en el panel inferior, introduzca la variable **Nombre**, el **Tipo** y **Valor**.
1. Haga clic en **Agregar**.
1. Haga clic en el [**Botón Guardar todo**](#save-all-button) para guardar los cambios en el servidor.

## Creación de un archivo {#creating-a-file}

Para crear un nuevo archivo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el [**Panel Explorador**,](#explorer-pane) haga clic con el botón derecho en el componente donde desee crear el archivo, seleccione **Crear**, luego **Crear archivo**.
1. Introduzca el archivo **Nombre** incluida su extensión.
1. Haga clic en **Aceptar**.
1. El nuevo archivo se abre como una pestaña en la [**Panel Editar**.](#edit-pane)
1. Edite el archivo.
1. Haga clic en el [**Botón Guardar todo**](#save-all-button) para guardar los cambios.

## Exportación e importación de tipos de nodo {#exporting-and-importing-node-types}

Con el CRXDE Lite puede importar o exportar definiciones de tipo de nodo en [Notación de espacio de nombres compacto y definición de tipo de nodo (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar una definición de tipo de nodo en el CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. Seleccione el nodo requerido.
1. Select **Herramientas** then **Exportar tipo de nodo**.
1. La definición se muestra en notación CND en una nueva pestaña del navegador.
1. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Select **Herramientas** then **Importar tipo de nodo**.
1. Se abre una nueva pestaña en el [**Panel Editar**](#edit-pane) etiquetado **Importar tipo de nodo**.
1. Introduzca la notación CND para la definición en el cuadro de texto de la variable **Importar tipo de nodo** pestaña .
1. Marque **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con el CRXDE Lite puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos en `<aem-install-dir>/crx-quickstart/logs` y filtrarlo con el nivel de registro adecuado. Proceda de la siguiente manera:

1. Abra CRXDE Lite en el navegador 
1. En el menú desplegable de la derecha del [**Ficha Consola**](#console-tab) en la parte inferior de la ventana, seleccione **Registros del servidor**.
1. Haga clic en el **Stop** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Felix haciendo clic en el botón **Configuraciones de registro** icono.
* Para borrar los mensajes, haga clic en el botón **Borrar consola** icono.
* Para anclar el mensaje a la selección actual, haga clic en el botón **Fijar consola** icono.
* Para habilitar o deshabilitar la visualización de mensajes, haga clic en el botón **Stop** icono.
