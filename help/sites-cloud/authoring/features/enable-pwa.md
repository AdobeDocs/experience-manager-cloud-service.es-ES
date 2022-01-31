---
title: Activación de las funciones progresivas de la aplicación web
description: AEM Sites permite al autor del contenido habilitar las funcionalidades de aplicación web progresiva en cualquier sitio a través de una configuración sencilla en lugar de la codificación.
exl-id: 1552a4ce-137a-4208-b7f6-2fc06db8dc39
source-git-commit: 3910b47c5d25679d03409380d91afaa6ff5ab265
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# Activación de las funciones progresivas de la aplicación web {#enabling-pwa}

A través de una configuración sencilla, un autor de contenido ahora puede habilitar las funciones de aplicación web progresiva (PWA) para las experiencias creadas en AEM Sites.

>[!CAUTION]
>
>Se trata de una característica avanzada que requiere:
>
>* Conocimiento de los PWA
>* Conocimiento del sitio y estructura de contenido
>* Comprensión de las estrategias de almacenamiento en caché
>* Asistencia de su equipo de desarrollo

>
>Antes de utilizar esta función, se recomienda discutirla con su equipo de desarrollo para definir la mejor manera de aprovecharla para su proyecto.

## Introducción {#introduction}

[Aplicaciones web progresivas (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) habilite experiencias de aplicación envolventes para sitios AEM, permitiéndoles almacenarse localmente en el equipo de un usuario y ser accesible sin conexión. Un usuario podía navegar por un sitio mientras estaba en marcha aunque se perdiera una conexión a Internet. Los PWA permiten experiencias sin fisuras incluso si la red se pierde o es inestable.

En lugar de requerir cualquier recodificación del sitio, un autor de contenido puede configurar las propiedades del PWA como una pestaña adicional en la [propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) de un sitio.

* Cuando se guarda o publica, esta configuración déclencheur un controlador de eventos que escribe el [archivos de manifiesto](https://developer.mozilla.org/en-US/docs/Web/Manifest) y [trabajador del servicio](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que habilitan características de PWA en el sitio.
* Las asignaciones de Sling también se mantienen para garantizar que el trabajo del servicio se proporcione desde la raíz de la aplicación para habilitar el contenido de proxy que permite las funciones sin conexión dentro de la aplicación.

Con PWA, el usuario tiene una copia local del sitio, lo que proporciona una experiencia similar a la de una aplicación incluso sin conexión a Internet.

>[!NOTE]
>
>Las aplicaciones web progresivas son una tecnología en evolución y son compatibles con la instalación de aplicaciones locales y otras funciones [depende del explorador que utilice.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Requisitos previos {#prerequisites}

Para poder utilizar las funciones de PWA del sitio, existen dos requisitos para el entorno del proyecto:

1. [Usar componentes principales](#adjust-components) para aprovechar esta función
1. [Ajuste de Dispatcher](#adjust-dispatcher) reglas para exponer los archivos necesarios

Estos son pasos técnicos que el autor deberá coordinar con el equipo de desarrollo. Estos pasos solo son necesarios una vez por sitio.

### Usar componentes principales {#adjust-components}

La versión 2.15.0 y posteriores de los componentes principales admiten completamente las funciones de PWA de AEM sitios. Dado que AEMaaCS siempre incluye la versión más reciente de los componentes principales, puede aprovechar las funciones de PWA listas para usar. El proyecto AEMaaCS cumple automáticamente este requisito.

>[!NOTE]
>
>El Adobe no recomienda utilizar las funciones de PWA en componentes personalizados o no en componentes personalizados [ampliado desde los componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
<!--
Your components need to include the [manifest files](https://developer.mozilla.org/en-US/docs/Web/Manifest) and [service worker,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) which supports the PWA features.

 To do this, the developer will need to add the following link to the `customheaderlibs.html` file of your page component.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

The developer will also need to add the following link to the `customfooterlibs.html` file of your page component.

```xml
<script>
        // Check that service workers are supported
        if ('serviceWorker' in navigator) {
            // Use the window load event to make sure the page load performs well
            window.addEventListener('load', () => {
                let serviceWorker = '/<projectName>sw.js';
                navigator.serviceWorker.register(serviceWorker);
            });
        }
</script>
```
-->

### Ajustar Dispatcher {#adjust-dispatcher}

La función de PWA genera y utiliza `/content/<sitename>/manifest.webmanifest` archivos. De forma predeterminada, [Dispatcher](/help/implementing/dispatcher/overview.md) no expone esos archivos. Para exponer estos archivos, el desarrollador debe agregar la siguiente configuración al proyecto del sitio.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

Según el proyecto, es posible que desee incluir distintos tipos de extensiones en las reglas de reescritura. La variable `webmanifest` puede resultar útil para incluir en las condiciones de reescritura al introducir una regla que oculte y redirija las solicitudes a `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Activación del PWA para el sitio {#enabling-pwa-for-your-site}

con [los requisitos previos](#prerequisites) Cuando se cumple, es muy fácil para un autor de contenido habilitar las funciones de PWA en un sitio. A continuación se muestra una descripción básica de cómo hacerlo. Las opciones individuales se detallan en la sección [Opciones detalladas.](#detailed-options)

1. Inicie sesión en AEM.
1. En el menú principal, toque o haga clic en **Navegación** -> **Sitios**.
1. Seleccione el proyecto Sitios y toque o haga clic en [**Propiedades**](/help/sites-cloud/authoring/fundamentals/page-properties.md) o utilice la tecla de acceso directo `p`.
1. Seleccione el **Aplicación web progresiva** y configure las propiedades aplicables. Como mínimo, debe:
   1. Seleccione la opción **Habilitar PWA**.
   1. Defina el **Dirección URL de inicio**.

      ![Habilitar PWA](../assets/pwa-enable.png)

   1. Cargue un icono de 512 x 512 png en DAM y haga referencia a él como icono de la aplicación.

      ![Icono Definir PWA](../assets/pwa-icon.png)

   1. Configure las rutas que desea que el trabajador de servicios desconecte. Las rutas habituales son:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Cualquier referencia de fuente de terceros
      * `/etc/clientlibs/<sitename>`

      ![Definir rutas sin conexión del PWA](../assets/pwa-offline.png)


1. Toque o haga clic **Guardar y cerrar**.

El sitio está configurado y puede [instálelo como una aplicación local.](#using-pwa-enabled-site)

## Uso del sitio habilitado para el PWA {#using-pwa-enabled-site}

Ahora que tiene [configuró su sitio para admitir a PWA,](#enabling-pwa-for-your-site) puedes experimentarlo tú mismo.

1. Acceda al sitio en un [navegador compatible.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Verá un nuevo icono en la barra de direcciones del explorador, que indica que el sitio se puede instalar como aplicación local.
   * Según el explorador, el icono puede variar y el explorador también puede mostrar una notificación (como un banner o un cuadro de diálogo) que indique que es posible realizar la instalación como aplicación local.
1. Instale la aplicación.
1. La aplicación se instalará en la pantalla principal del dispositivo.
1. Abra la aplicación, examine un poco y vea que las páginas están disponibles sin conexión.

## Opciones detalladas {#detailed-options}

La siguiente sección proporciona más detalles sobre las opciones disponibles cuando [configurar el sitio para PWA.](#enabling-pwa-for-your-site)

### Configurar experiencias instalables {#configure-installable-experience}

Estos ajustes permiten que el sitio se comporte como una aplicación nativa al hacerla instalable en la pantalla principal del visitante y estar disponible sin conexión.

* **Habilitar PWA** - Esta es la opción principal para habilitar el PWA para el sitio.
* **Dirección URL de inicio** - Esta es la [URL de inicio preferida](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) que la aplicación se abrirá cuando el usuario cargue la aplicación instalada localmente.
   * Puede ser cualquier ruta en la estructura de contenido.
   * No tiene que ser la raíz y es a menudo una página de bienvenida dedicada para la aplicación.
   * Si esta dirección URL es relativa, la dirección URL de manifiesto se utiliza como dirección URL base para resolverla.
   * Cuando se deja vacía, la función utiliza la dirección de la página web desde la que se instaló la aplicación web.
   * Se recomienda configurar un valor.
* **Modo de visualización** - Una aplicación habilitada para el PWA sigue siendo un sitio AEM entregado a través de un explorador. [Estas opciones de visualización](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) defina cómo se debe ocultar o presentar el navegador al usuario desde el dispositivo local.
   * **Independiente** : el navegador está completamente oculto para el usuario y parece una aplicación nativa. Este es el valor predeterminado.
      * Con esta opción, la navegación de la aplicación debe ser posible por completo a través del contenido mediante vínculos y componentes en las páginas del sitio sin utilizar los controles de navegación del explorador.
   * **Navegador** - El navegador aparece como lo haría normalmente al visitar el sitio.
   * **IU mínima** - El navegador está oculto, como una aplicación nativa, pero se exponen los controles básicos de navegación.
   * **Pantalla completa** - El navegador está completamente oculto, como una aplicación nativa, pero se procesa en modo de pantalla completa.
      * Con esta opción, la navegación de la aplicación debe ser posible por completo a través del contenido mediante vínculos y componentes en las páginas del sitio sin utilizar los controles de navegación del explorador.
* **Orientación de la pantalla** : como aplicación local, el PWA debe saber cómo gestionarla [orientaciones del dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Cualquiera** - La aplicación se ajusta a la orientación del dispositivo del usuario. Este es el valor predeterminado.
   * **Vertical** : esto fuerza a la aplicación a abrirse en formato vertical independientemente de la orientación del dispositivo del usuario.
   * **Horizontal** : esto fuerza a la aplicación a abrirse en un diseño horizontal independientemente de la orientación del dispositivo del usuario.
* **Color del tema** - Define el [color de la aplicación](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) que afecta a la forma en que el sistema operativo del usuario local muestra la barra de herramientas de la IU nativa y los controles de navegación. Según el explorador, puede afectar a otros elementos de presentación de la aplicación.
   * Utilice la ventana emergente de pozo de color para seleccionar un color.
   * El color también puede definirse por valor hexadecimal o RGB.
* **Color de fondo** - Define el [color de fondo de la aplicación,](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) que se muestra a medida que se carga la aplicación.
   * Utilice la ventana emergente de pozo de color para seleccionar un color.
   * El color también puede definirse por valor hexadecimal o RGB.
   * Determinados navegadores [crear una pantalla de inicio automáticamente](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) del nombre de la aplicación, el color de fondo y el icono.
* **Icono** - Esto define [el icono](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) que representa la aplicación en el dispositivo del usuario.
   * El icono debe ser un archivo png de tamaño 512 x 512 píxeles.
   * El icono debe ser [almacenado en DAM.](/help/assets/overview.md)

### Administración de caché (avanzado) {#offline-configuration}

Esta configuración hace que partes de este sitio estén disponibles sin conexión y disponibles localmente en el dispositivo del visitante. Esto permite controlar la caché de la aplicación web para optimizar las solicitudes de red y admitir experiencias sin conexión.

* **Estrategia de almacenamiento en caché y frecuencia de actualización del contenido** - Esta configuración define el modelo de almacenamiento en caché para su PWA.
   * **Moderadamente** - [Esta configuración](https://web.dev/stale-while-revalidate/) es el caso de la mayoría de los sitios y es el valor predeterminado.
      * Con esta configuración, el contenido que el usuario ve por primera vez se carga desde la caché y, mientras el usuario consume ese contenido, el resto del contenido de la caché se vuelve a validar.
   * **Frecuentes** - Este es el caso de los sitios que necesitan actualizaciones para ser muy rápidos, como las casas de subastas.
      * Con esta configuración, la aplicación buscará primero el contenido más reciente a través de la red y, si no está disponible, volverá a la caché local.
   * **Rara vez** - Este es el caso de los sitios que son casi estáticos, como las páginas de referencia.
      * Con esta configuración, la aplicación buscará primero el contenido en la caché y, si no está disponible, volverá a la red para recuperarlo.
* **Almacenamiento en caché previo de archivos** - Estos archivos alojados en AEM se guardarán en la caché del explorador local cuando el trabajador de servicios se instale y antes de que se utilice. Esto garantiza que la aplicación web funcione completamente cuando está sin conexión.
* **Inclusiones de rutas** - Las solicitudes de red para las rutas definidas se interceptan y el contenido almacenado en caché se devuelve de acuerdo con la configuración **Estrategia de almacenamiento en caché y frecuencia de actualización del contenido**.
* **Exclusiones de caché** - Estos archivos nunca se almacenarán en caché, independientemente de la configuración de **Almacenamiento en caché previo de archivos** y **Inclusiones de rutas**.

>[!TIP]
>
>Es probable que el equipo de desarrollador tenga datos valiosos sobre cómo se debe configurar la configuración sin conexión.

## Limitaciones y Recommendations {#limitations-recommendations}

No todas las funciones de PWA están disponibles para AEM Sites. Estas son algunas limitaciones importantes.

* Las páginas no se sincronizan ni actualizan automáticamente si el usuario no utiliza la aplicación.

Adobe también realiza las siguientes recomendaciones al implementar PWA.

### Reduzca al máximo el número de recursos que se van a prealmacenar en caché. {#minimize-precache}

Adobe recomienda limitar el número de páginas que se prealmacenarán en caché.

* Incruste bibliotecas para reducir el número de entradas que se van a administrar al prealmacenar en caché.
* Limite el número de variaciones de imagen a la caché previa.

### Active el PWA después de estabilizar las secuencias de comandos del proyecto y las hojas de estilo. {#pwa-stabilized}

Las bibliotecas de cliente se entregan con la adición de un selector de caché que observa el siguiente patrón `lc-<checksumHash>-lc`. Cada vez que cambia uno de los archivos (y dependencias) que componen una biblioteca, este selector. Si enumeró una biblioteca de cliente para que la almacene previamente en caché el trabajador de servicios y desea hacer referencia a una nueva versión, recupere y actualice manualmente la entrada. Como resultado, le recomendamos que configure su sitio para que sea PWA después de estabilizar los scripts de proyecto y las hojas de estilo.

### Minimice el número de variaciones de imagen. {#minimize-variations}

El componente de imagen de los componentes principales de AEM determina uno de los front-end la mejor representación que se debe recuperar. Este mecanismo también incluye una marca de tiempo que corresponde a la hora de la última modificación de ese recurso. Este mecanismo complica la configuración de la precaché del PWA.

Al configurar la caché previa, el usuario debe enumerar todas las variaciones de ruta que se pueden recuperar. Estas variaciones están compuestas de parámetros como calidad y anchura. Se recomienda reducir el número de estas variaciones a un máximo de tres: pequeñas, medianas y grandes. Puede hacerlo a través del cuadro de diálogo de política de contenido del [Componente de imagen.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

Si no se configura con cuidado, la memoria y el consumo de red pueden afectar gravemente al rendimiento de su PWA. Además, si tiene intención de prealmacenar, por ejemplo, 50 imágenes y tiene 3 anchos por imagen, el usuario que mantenga el sitio deberá mantener una lista de hasta 150 entradas en la sección precaché del PWA de las propiedades de página.

Adobe también le recomienda configurar su sitio para que sea PWA después de que el uso de imágenes en el proyecto se haya estabilizado.
