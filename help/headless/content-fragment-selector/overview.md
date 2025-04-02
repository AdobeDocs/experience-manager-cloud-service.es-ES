---
title: Selector de fragmentos de contenido de Micro-FrontEnd para Adobe Experience Manager as a Cloud Service
description: Utilice el Selector de fragmentos de contenido de Micro-FrontEnd para buscar, buscar y recuperar fragmentos de contenido de su aplicación.
role: Admin, User
source-git-commit: 32e1b3cef768b420f32b70202ddadc80db2b74e8
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 11%

---


# Selector de fragmentos de contenido de Micro-FrontEnd {#micro-frontend-content-fragment-selector}

El Selector de fragmentos de contenido de Micro-FrontEnd proporciona una interfaz de usuario que se integra fácilmente con el repositorio de as a Cloud Service de Adobe Experience Manager (AEM). La interfaz de permite examinar o buscar fragmentos de contenido en el repositorio y utilizarlos en la aplicación.

La interfaz de usuario de Micro-FrontEnd está disponible en su aplicación mediante el paquete Selector de fragmentos de contenido. Las actualizaciones del paquete se importan y cargan automáticamente en la aplicación.

![Selector de fragmentos de contenido de Micro-Frontend: información general](/help/headless/assets/content-fragment-selector-overview.png)

El Selector de fragmentos de contenido ofrece muchas ventajas, como las siguientes:

* Facilidad de integración con cualquiera de las aplicaciones de Adobe.
* Es fácil de mantener, ya que las actualizaciones del paquete Selector de fragmentos de contenido se implementan automáticamente en el Selector de fragmentos de contenido disponible para su aplicación. Esto significa que la aplicación no necesita realizar ninguna acción para cargar las modificaciones más recientes.
* Facilidad de personalización, al utilizar propiedades que controlan la visualización del Selector de fragmentos de contenido dentro de la aplicación.
* La búsqueda de texto completo, junto con filtros personalizables, permiten la navegación rápida de los fragmentos de contenido dentro de la experiencia de creación.
* Capacidad para cambiar repositorios dentro de una organización IMS para la selección de fragmentos de contenido.
* Capacidad para ordenar fragmentos de contenido y verlos en la vista seleccionada.

## Requisitos previos {#prerequisites}

### Autenticación IMS {#ims-authentication}

Si necesita el flujo de trabajo de autenticación IMS, debe asegurarse de que:

* La aplicación se está ejecutando en `HTTPS`.
* La dirección URL de la aplicación está en la lista de direcciones URL de redireccionamiento permitidas para el cliente IMS.
* El flujo de inicio de sesión de IMS se configura y se representa mediante una ventana emergente en el explorador web. Por lo tanto, las ventanas emergentes deben habilitarse o permitirse en el explorador de destino.

Alternativamente, si la aplicación ya está autenticada con el flujo de trabajo de IMS, puede añadir la información de IMS adecuada en su lugar.

## Instalación {#installation}

Usar el componente `ContentFragmentSelector`. Hay varias opciones de instalación:

1. NPM Registry (Registro privado de Adobe)

   * Agregar lo siguiente a `.npmrc`:

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * A continuación, instale

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Repositorio Git

   * Agregue lo siguiente a `package.json` dependencias:

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## Uso del selector de fragmentos de contenido {#using-the-Content-Fragment-selector}

Una vez configurado y autenticado el Selector de fragmentos de contenido para utilizar el Selector de fragmentos de contenido con la aplicación de AEM as a Cloud Service, puede seleccionar Fragmentos de contenido o realizar otras operaciones para buscar los fragmentos en el repositorio:

![Selector de fragmentos de contenido](/help/headless/assets/content-fragment-selector-using.png)

* Con el selector **Repositorio** en la parte superior derecha, puede seleccionar el repositorio que desee usar
* En el panel del extremo izquierdo puede:
   * Ocultar o mostrar carpetas del repositorio seleccionado
   * Seleccione una carpeta específica para mostrar los fragmentos de contenido de esa carpeta
* En el panel principal puede:
   * Seleccionar fragmentos de contenido
   * Buscar fragmentos de contenido
   * Ordenar la lista actual según varias columnas, tanto en orden ascendente como descendente
   * Consulte el indicador de formato de vista
   * Mostrar, ocultar y especificar filtros

### Ocultar/Mostrar panel {#hide-show-panel}

Para ocultar carpetas en el panel de navegación izquierdo, haga clic en el icono **Ocultar carpetas**. Para deshacer los cambios, haga clic en el icono **Ocultar carpetas** de nuevo.

### Conmutador de repositorios {#repository-switcher}

El Selector de fragmentos de contenido le permite seleccionar un repositorio para la selección de fragmentos.

Puede seleccionar el repositorio que desee en la lista desplegable **Repositorio**, disponible en la parte superior del panel principal.

![Selector de fragmentos de contenido](/help/headless/assets/content-fragment-repository-selector.png)

Las opciones del repositorio disponibles en la lista desplegable se basan en la propiedad `repositoryId` definida en el archivo `index.html`. Esta propiedad se basa en el entorno de la organización de IMS seleccionada, a la que accede el usuario que ha iniciado sesión actualmente.

Los consumidores pueden pasar un `repositoryID` preferido para procesar fragmentos de un repositorio específico y detener el procesamiento del conmutador de repositorios.

### Carpetas de fragmentos de contenido {#content-fragments-folders}

El repositorio de fragmentos de contenido es una colección de carpetas de fragmentos de contenido que puede utilizar para realizar operaciones.

### Filtros {#filters}

El Selector de fragmentos de contenido también proporciona opciones de filtro listas para usar para restringir los resultados de búsqueda. Hay varios filtros disponibles, entre ellos:

* **Modelo de fragmento**
* **Localización**
* **Estado**: el estado actual del fragmento; `New`, `Draft`, `Published`, `Modified`, `Unpublished`
* Etiquetas
* Usuarios
* Horas y fechas

![Opciones de filtro](/help/headless/assets/content-selector-filters.png)

También puede crear un filtro de búsqueda predeterminado para guardarlo para utilizarlo en el futuro. Para crear filtros de búsqueda personalizados para los fragmentos de contenido, puede utilizar la propiedad `filterSchema`.

### Barra de búsqueda {#search-bar}

El Selector de fragmentos de contenido permite realizar una búsqueda de texto completo de los fragmentos dentro del repositorio seleccionado. Por ejemplo, si escribe la palabra clave `wave` en la barra de búsqueda, se muestran todos los fragmentos con la palabra clave `wave` mencionada en cualquiera de las propiedades de metadatos.

### Ordenación {#sorting}

Puede ordenar los fragmentos en el Selector de fragmentos de contenido por varias propiedades. También puede ordenar los fragmentos en orden ascendente o descendente.

### Tipo de vista {#view-type}

El Selector de fragmentos de contenido permite ver el fragmento en:

* **Vista de tabla**
