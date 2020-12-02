---
title: Uso de CRXDE Lite
description: CRXDE Lite es parte del inicio rápido AEM y está disponible para acceder y modificar el repositorio en sus entornos de desarrollo locales dentro del explorador.
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 3%

---


# Uso del CRXDE Lite {#using-crxde-lite}

CRXDE Lite es parte del inicio rápido AEM y está disponible para acceder y modificar el repositorio en sus entornos de desarrollo locales dentro del explorador. Con CRXDE Lite, puede editar archivos, carpetas, nodos y propiedades. Todo el repositorio es accesible para usted en esta interfaz fácil de usar.

>[!NOTE]
>
>CRXDE Lite sólo está disponible en sus entornos de desarrollo local. No está disponible en AEM como Cloud Service.

## Introducción a CRXDE Lite {#getting-started-with-crxde-lite}

Para empezar con CRXDE Lite:

1. Inicio el inicio rápido del desarrollo AEM local.
1. En el explorador, abra la dirección URL `https://<host>:<port>/crx/de`.
1. Introduzca su **nombre de usuario** y **contraseña**.
1. Haga clic en **Aceptar**.

La interfaz de usuario de CRXDE Lite tiene el siguiente aspecto en el explorador:

![La interfaz CRXDE Lite](assets/crxde-lite.png)

Ahora puede usar CRXDE Lite para desarrollar su aplicación.

>[!TIP]
>
>También puede acceder a CRXDE Lite desde el menú AEM. En el menú principal, seleccione **Herramientas** -> **General** -> **CRXDE Lite**.

## Información general sobre la interfaz de usuario {#overview-of-the-user-interface}

La interfaz de usuario del CRXDE Lite tiene muchas partes y muchas funciones.

### Barra de conmutación superior {#top-switcher-bar}

La barra del conmutador principal le permite cambiar rápidamente entre CRXDE Lite, administrador de paquetes y uso compartido de paquetes.

### Utilidad Ruta de nodo {#node-path-widget}

La Utilidad Ruta del nodo muestra la ruta al nodo seleccionado actualmente.

También puede utilizarla para saltar a un nodo introduciendo la ruta manualmente o pegándola desde otro lugar y pulsando Intro.

También proporciona soporte para buscar nodos con un nombre de nodo específico. Escriba el nombre del nodo que desee encontrar y espere (o seleccione el icono de búsqueda en el lado derecho). Si un nodo o nodos determinados se cargan en el panel del explorador, se mostrará la lista y puede seleccionar la ruta y pulsar Intro para desplazarse hasta ella. Tenga en cuenta que solo funciona con los nodos cargados actualmente en la aplicación cliente CRXDE en el navegador. Si desea buscar en todo el repositorio, utilice **Herramientas** -&amp;gt: **Consulta**.

### Panel del explorador {#explorer-pane}

El **Panel del explorador** muestra un árbol de todos los nodos del repositorio.

Haga clic en un nodo para mostrar sus propiedades en la ficha **Propiedades**. Después de hacer clic en un nodo, puede seleccionar una acción en la barra de herramientas. Vuelva a hacer clic en el nodo para cambiarle el nombre.

El filtro de navegación de árbol (el icono de binoculares) permite filtrar los nodos del repositorio cuyo nombre contiene el texto de entrada. Solo se aplica a los nodos que se han cargado localmente.

### Panel de edición {#edit-pane}

El **Panel de edición** permite la vista del contenido del archivo seleccionado actualmente en el repositorio. Cada archivo abierto se representará como su propia ficha en el panel.

La ficha **Inicio** le permite buscar contenido y/o documentación, y acceder a la documentación del desarrollador y a la compatibilidad con Adobe.

Haga clic con el doble en un archivo del **Panel del explorador** para mostrar su contenido en el **Panel de edición**. A continuación, puede modificarlo y guardar los cambios.

Una vez que se edita un archivo en el **Panel de edición**, las siguientes herramientas están disponibles en la barra de herramientas:

* **Mostrar en árbol** : muestra el archivo en el árbol del repositorio.
* **Buscar/Reemplazar** : realiza una búsqueda o un reemplazo.

Al hacer clic con el doble en la línea de estado del **Panel de edición** se abre el cuadro de diálogo **Ir a la línea** para que pueda introducir un número de línea específico.

### Ficha Propiedades {#properties-tab}

La ficha **Propiedades** muestra las propiedades del nodo que ha seleccionado. Puede agregar nuevas propiedades o eliminar las existentes.

### Ficha control de acceso {#access-control-tab}

La **ficha Control de acceso** muestra los permisos según la ruta, el repositorio o el principal actuales.

Los permisos se desglosan en las siguientes categorías.

* **Política**  de Control de acceso aplicable: las políticas que se pueden aplicar a la selección actual
* **Directivas**  de Control de acceso local: las políticas actuales aplicadas localmente a la selección actual
* **Directivas**  de Control de acceso efectivas: las políticas actuales aplicadas a la selección actual, que se pueden establecer localmente o heredar de los nodos principales

>[!NOTE]
Para poder ver la información de control de acceso, el usuario que ha iniciado sesión en el CRXDE Lite debe tener derechos para leer entradas ACL.

### Ficha Replicación {#replication-tab}

La **ficha Replicación** muestra el estado de replicación del nodo actual. Puede replicar y replicar la eliminación del nodo actual.

###  Ficha Consola {#console-tab}

La **ficha Consola** muestra los mensajes de registro. Puede configurar el nivel de registro, borrar la consola, fijar en la posición de desplazamiento seleccionada y habilitar/deshabilitar la visualización de mensajes.

### Ficha Información de compilación {#build-info-tab}

La **ficha Información de compilación** muestra información cuando se está generando un paquete.

### Botón Actualizar {#refresh-button}

El **Botón Actualizar** actualiza la selección actual. Los cambios de otros usuarios se actualizan en la vista del repositorio. Los cambios realizados no se verán afectados.

### Botón Guardar todo {#save-all-button}

El **Botón Guardar todo** guarda todos los cambios realizados. Hasta que decida guardar, los cambios son temporales y se perderán al salir de la consola.

* **Revertir** : descarta todos los cambios realizados en el nodo seleccionado desde la última acción de guardado y, a continuación, vuelve a cargar el estado actual del repositorio para el nodo seleccionado
* **Revertir todo** : descarta todos los cambios realizados en todo el repositorio desde la última acción de guardar y, a continuación, vuelve a cargar el estado actual del repositorio

### Botón Crear {#create-button}

El **Botón Crear** es un menú desplegable para crear lo siguiente bajo el nodo seleccionado:

* Nodo: nodo con un tipo de nodo arbitrario
* Archivo: un nodo `nt:file` y su subnodo nt:resource
* Carpeta: un nodo `nt:folder`

### Botón Eliminar {#delete-button}

El **Botón Eliminar** elimina el nodo seleccionado.

### Botón Copiar {#copy-button}

El **Botón Copiar** copia el nodo seleccionado.

## Botón Pegar {#paste-button}

El **Botón Pegar** pega el nodo copiado debajo del nodo seleccionado.

### Botón Mover {#move-button}

El **Botón Mover** mueve el nodo seleccionado al nodo configurado a través del cuadro de diálogo.

### Cambiar nombre {#rename-button}

El **Botón Cambiar nombre** cambia el nombre del nodo seleccionado.

### Mezclas {#mixins-button}

El **Botón de mezclas** permite agregar tipos de mezcla al tipo de nodo. Los tipos de mezclas se utilizan principalmente para añadir características avanzadas.

### Herramientas {#tools-button}

El **Botón Herramientas** es un menú desplegable con las siguientes herramientas disponibles:

* **Configuración**  del servidor: para acceder a la consola Felix (también disponible en  `https://<host>:<port>/system/console/configMgr`)
* **Consulta** : consulta del repositorio
* **Privilegios** : vista y adición de privilegios
* **Control de acceso**  de prueba: para probar el permiso de una ruta determinada y/o principal
* **Exportar tipo**  de nodo para exportar tipos de nodo en el sistema como notación CND
* **Importar tipo**  de nodo: para importar tipos de nodos con notación CND.

### Utilidad de inicio de sesión {#login-widget}

La **Utilidad de inicio de sesión** muestra el usuario que ha iniciado sesión.

Haga clic en él para iniciar sesión o volver a iniciarla como otro usuario. El `@crx.default` representa que se encuentra en el espacio de trabajo predeterminado (y único) del repositorio.

La opción **Preferencias** se puede utilizar para establecer el idioma de la interfaz de usuario y para la vista y personalización de las teclas de acceso directo para diversas acciones como guardar, buscar, crear notas, etc.

## Creación de una carpeta {#creating-a-folder}

Para crear una carpeta con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el panel Navegación, haga clic con el botón derecho en la carpeta en la que desea crear la nueva carpeta, seleccione **Crear...**, luego **Crear carpeta...**.

1. Introduzca la carpeta **Name** y haga clic en **OK**.

1. Haga clic en **Guardar todo** para guardar los cambios en el servidor.

## Creación de un nodo {#creating-a-node}

Para crear un nodo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el [**Panel de exploración**,](#explorer-pane) haga clic con el botón secundario en el nodo en el que desee crear el nuevo nodo, seleccione **Crear** y, a continuación, **Crear nodo**.
1. Escriba el **Nombre** y seleccione el **Tipo**.
1. Haga clic en **Aceptar**.
1. Haga clic en el [**Botón Guardar todo**](#save-all-button) para guardar los cambios en el servidor.

Ahora puede adaptar el nodo a sus necesidades modificando propiedades o creando nuevos nodos.

>[!NOTE]
La mayoría de las operaciones de edición, incluido **Crear nodo**, mantienen todos los cambios en la memoria y sólo los almacena en el repositorio al guardarlos (mediante el [**Botón Guardar todo**](#save-all-button)). Sin embargo, algunas operaciones como mover se mantienen automáticamente.
La validación con respecto a si el tipo de nodo del nodo principal permite el nodo recién creado también la realiza el repositorio al guardar los cambios. Si recibe un mensaje de error al guardar un nodo, compruebe si la estructura de contenido es válida (por ejemplo, no puede crear un nodo `nt:unstructured` como secundario de `nt:folder` nodo).

## Creación de una propiedad {#creating-a-property}

Para crear una propiedad con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el [**Panel de exploración**,](#explorer-pane) seleccione el nodo donde desee agregar la nueva propiedad.
1. En la [**ficha Propiedades**](#properties-tab) del panel inferior, introduzca **Nombre**, el **Tipo** y el **Valor**.
1. Haga clic en **Agregar**.
1. Haga clic en el [**Botón Guardar todo**](#save-all-button) para guardar los cambios en el servidor.

## Creación de un archivo {#creating-a-file}

Para crear un nuevo archivo con CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. En el [**Panel de exploración**,](#explorer-pane) haga clic con el botón secundario en el componente donde desee crear el archivo, seleccione **Crear** y, a continuación, **Crear archivo**.
1. Introduzca el archivo **Name**, incluida su extensión.
1. Haga clic en **Aceptar**.
1. El nuevo archivo se abre como una ficha en el [**Panel de edición**.](#edit-pane)
1. Edite el archivo.
1. Haga clic en el [**Botón Guardar todo**](#save-all-button) para guardar los cambios.

## Exportación e importación de tipos de nodos {#exporting-and-importing-node-types}

Con CRXDE Lite puede importar y/o exportar definiciones de tipo de nodo en la notación [Compact Área de nombres y Definición de tipo de nodo (CND)](https://jackrabbit.apache.org/jcr/node-type-notation.html).

Para exportar una definición de tipo de nodo en CRXDE Lite:

1. Abra CRXDE Lite en el navegador 
1. Seleccione el nodo requerido.
1. Seleccione **Herramientas** y luego **Exportar tipo de nodo**.
1. La definición se mostrará en notación CND en una nueva ficha del explorador.
1. Guarde la información si es necesario.

Para importar una definición de tipo de nodo:

1. Abra CRXDE Lite en el navegador 
1. Seleccione **Herramientas** y luego **Importar tipo de nodo**.
1. Se abre una nueva ficha en el [**Panel de edición**](#edit-pane) etiquetado **Tipo de nodo de importación**.
1. Introduzca la notación CND para la definición en el cuadro de texto de la ficha **Importar tipo de nodo**.
1. Seleccione **Permitir actualización** si está actualizando una definición existente.
1. Haga clic en **Importar**.

## Registro {#logging}

Con CRXDE Lite puede mostrar el archivo `error.log` que se encuentra en el sistema de archivos en `<aem-install-dir>/crx-quickstart/logs` y filtrarlo con el nivel de registro adecuado. Proceda de la siguiente manera:

1. Abra CRXDE Lite en el navegador 
1. En el menú desplegable de la derecha de la [**ficha Consola**](#console-tab) en la parte inferior de la ventana, seleccione **Registros de servidor**.
1. Haga clic en el icono **Detener** para mostrar los mensajes.

Puede hacer lo siguiente:

* Ajuste los parámetros de registro en la consola Félix haciendo clic en el icono **Configuraciones de registro**.
* Para borrar los mensajes, haga clic en el icono **Borrar consola**.
* Anclar el mensaje en la selección actual haciendo clic en el icono **Fijar consola**.
* Habilite o deshabilite la visualización de mensajes haciendo clic en el icono **Detener**.
