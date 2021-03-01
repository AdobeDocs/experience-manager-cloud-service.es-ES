---
title: Activación de las funciones progresivas de la aplicación web
description: AEM Sites permite al autor del contenido habilitar las funciones de aplicación web progresiva en cualquier sitio a través de una configuración sencilla en lugar de la codificación.
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 54c4755207d84f6f11effea72e94e20027446ba9
workflow-type: tm+mt
source-wordcount: '2046'
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
>
Antes de utilizar esta función, se recomienda discutirla con su equipo de desarrollo para definir la mejor manera de aprovecharla para su proyecto.

>[!NOTE]
>
>Las funciones descritas en este documento están previstas para estar disponibles con la versión de [marzo de 2021 de AEM as a Cloud Service.](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)

## Introducción {#introduction}

[Las aplicaciones web progresivas (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)  permiten disfrutar de experiencias de aplicación envolventes en los sitios AEM, ya que permiten almacenarlas localmente en el equipo de un usuario y acceder a ellas sin conexión. Un usuario podía navegar por un sitio mientras estaba en marcha aunque se perdiera una conexión a Internet. Los PWA permiten experiencias sin problemas incluso si la red se pierde o es inestable.

En lugar de requerir cualquier recodificación del sitio, un autor de contenido puede configurar las propiedades de PWA como una pestaña adicional en las [propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) de un sitio.

* Cuando se guarda o se publica, esta configuración activa un controlador de eventos que escribe los [archivos de manifiesto](https://developer.mozilla.org/en-US/docs/Web/Manifest) y el [trabajador del servicio](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que habilitan las funciones de PWA en el sitio.
* Las asignaciones de Sling también se mantienen para garantizar que el trabajo del servicio se proporcione desde la raíz de la aplicación para habilitar el contenido de proxy que permite las funciones sin conexión dentro de la aplicación.

Con PWA, el usuario tiene una copia local del sitio, lo que proporciona una experiencia similar a la de una aplicación incluso sin conexión a Internet.

>[!NOTE]
>
>Las aplicaciones web progresivas son una tecnología y compatibilidad en evolución para la instalación de aplicaciones locales y otras funciones [depende del explorador que utilice.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Requisitos previos {#prerequisites}

Para poder usar las funciones de PWA en su sitio, existen dos requisitos para el entorno del proyecto:

1. [Usar ](#adjust-components) componentes principales para aprovechar esta función
1. [Ajuste las reglas de ](#adjust-dispatcher) Dispatcher para exponer los archivos necesarios

Estos son pasos técnicos que el autor deberá coordinar con el equipo de desarrollo. Estos pasos solo son necesarios una vez por sitio.

### Usar componentes principales {#adjust-components}

La versión 2.15.0 y posteriores de los componentes principales admiten completamente las funciones de PWA de los sitios de AEM. Dado que AEMaaCS siempre incluye la versión más reciente de los componentes principales, puede aprovechar las funciones de PWA integradas. El proyecto AEMaaCS cumple automáticamente este requisito.

>[!NOTE]
>
>Adobe no recomienda utilizar las funciones de PWA en componentes personalizados o componentes que no [se hayan ampliado desde los principales componentes.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
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

La función PWA genera y utiliza `/content/<sitename>/manifest.webmanifest` archivos. De forma predeterminada, [el despachante](/help/implementing/dispatcher/overview.md) no expone estos archivos. Para exponer estos archivos, el desarrollador debe agregar la siguiente configuración al proyecto del sitio.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

Según el proyecto, es posible que desee incluir distintos tipos de extensiones en las reglas de reescritura. La extensión `webmanifest` puede resultar útil para incluir en las condiciones de reescritura cuando introdujo una regla que oculta y redirige solicitudes a `/content/<projectName>`.

```text
RewriteCond %{REQUEST_URI} (.html|.jpe?g|.png|.svg|.webmanifest)$
```

## Habilitación de PWA para su sitio {#enabling-pwa-for-your-site}

Con [los requisitos previos](#prerequisites) cumplidos, es muy fácil para un autor de contenido habilitar las funciones de PWA en un sitio. A continuación se muestra una descripción básica de cómo hacerlo. Las opciones individuales se detallan en la sección [Opciones detalladas.](#detailed-options)

1. Inicie sesión en AEM.
1. En el menú principal, pulse o haga clic en **Navegación** -> **Sitios**.
1. Seleccione el proyecto del sitio y pulse o haga clic en [**Propiedades**](/help/sites-cloud/authoring/fundamentals/page-properties.md) o utilice la tecla de acceso directo `p`.
1. Seleccione la pestaña **Aplicación web progresiva** y configure las propiedades aplicables. Como mínimo, debe:
   1. Seleccione la opción **Habilitar PWA**.
   1. Defina la **URL de inicio**.

      ![Habilitar PWA](../assets/pwa-enable.png)

   1. Cargue un icono de 512 x 512 png en DAM y haga referencia a él como icono de la aplicación.

      ![Icono Definir PWA](../assets/pwa-icon.png)

   1. Configure las rutas que desea que el trabajador de servicios desconecte. Las rutas habituales son:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Cualquier referencia de fuente de terceros
      * `/etc/clientlibs/<sitename>`

      ![Definición de rutas sin conexión de PWA](../assets/pwa-offline.png)


1. Toque o haga clic en **Guardar y cerrar**.

El sitio ya está configurado y puede [instalarlo como una aplicación local.](#using-pwa-enabled-site)

## Uso del sitio habilitado para PWA {#using-pwa-enabled-site}

Ahora que ha [configurado su sitio para admitir PWA,](#enabling-pwa-for-your-site) puede experimentarlo usted mismo.

1. Acceda al sitio en un [explorador compatible.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Verá un nuevo icono en la barra de direcciones del explorador, que indica que el sitio se puede instalar como aplicación local.
   * Según el explorador, el icono puede variar y el explorador también puede mostrar una notificación (como un banner o un cuadro de diálogo) que indique que es posible realizar la instalación como aplicación local.
1. Instale la aplicación.
1. La aplicación se instalará en la pantalla principal del dispositivo.
1. Abra la aplicación, examine un poco y vea que las páginas están disponibles sin conexión.

## Opciones detalladas {#detailed-options}

La siguiente sección proporciona más detalles sobre las opciones disponibles al [configurar el sitio para PWA.](#enabling-pwa-for-your-site)

### Configurar la experiencia instalable {#configure-installable-experience}

Estos ajustes permiten que el sitio se comporte como una aplicación nativa al hacerla instalable en la pantalla principal del visitante y estar disponible sin conexión.

* **Habilitar PWA** : esta es la opción principal para habilitar PWA para el sitio.
* **URL de inicio** : es la  [URL de inicio ](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) preferida que la aplicación se abrirá cuando el usuario cargue la aplicación instalada localmente.
   * Puede ser cualquier ruta en la estructura de contenido.
   * No tiene que ser la raíz y es a menudo una página de bienvenida dedicada para la aplicación.
   * Si esta dirección URL es relativa, la dirección URL de manifiesto se utiliza como dirección URL base para resolverla.
   * Cuando se deja vacía, la función utiliza la dirección de la página web desde la que se instaló la aplicación web.
   * Se recomienda configurar un valor.
* **Modo de visualización** : una aplicación habilitada para PWA sigue siendo un sitio de AEM entregado a través de un explorador. [Estas ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) opciones de visualización definen cómo se debe ocultar el explorador o cómo se debe presentar al usuario en el dispositivo local.
   * **Independiente** : el navegador está completamente oculto para el usuario y parece una aplicación nativa. Este es el valor predeterminado.
      * Con esta opción, la navegación de la aplicación debe ser posible por completo a través del contenido mediante vínculos y componentes en las páginas del sitio sin utilizar los controles de navegación del explorador.
   * **Explorador** : el explorador aparece como lo haría normalmente al visitar el sitio.
   * **IU mínima** : el navegador está oculto, como una aplicación nativa, pero se exponen los controles de navegación básicos.
   * **Pantalla completa** : el navegador está completamente oculto, como una aplicación nativa, pero se procesa en modo de pantalla completa.
      * Con esta opción, la navegación de la aplicación debe ser posible por completo a través del contenido mediante vínculos y componentes en las páginas del sitio sin utilizar los controles de navegación del explorador.
* **Orientación de pantalla** : como aplicación local, el PWA debe saber cómo gestionar las orientaciones del  [dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Cualquiera** : la aplicación se ajusta a la orientación del dispositivo del usuario. Este es el valor predeterminado.
   * **Vertical** : esto fuerza a la aplicación a abrirse en formato vertical independientemente de la orientación del dispositivo del usuario.
   * **Horizontal** : esto fuerza a la aplicación a abrirse en un diseño horizontal independientemente de la orientación del dispositivo del usuario.
* **Color del tema** : define el  [color de la ](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) aplicación que afecta a cómo el sistema operativo del usuario local muestra la barra de herramientas de la IU nativa y los controles de navegación. Según el explorador, puede afectar a otros elementos de presentación de la aplicación.
   * Utilice la ventana emergente de pozo de color para seleccionar un color.
   * El color también se puede definir mediante valores hexadecimales o RGB.
* **Color de fondo** : define el color de  [fondo de la aplicación, ](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) que se muestra a medida que la aplicación se carga.
   * Utilice la ventana emergente de pozo de color para seleccionar un color.
   * El color también se puede definir mediante valores hexadecimales o RGB.
   * Algunos exploradores [crean una pantalla de inicio automáticamente](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) a partir del nombre de la aplicación, el color de fondo y el icono.
* **Icono** : define  [el ](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) icono que representa la aplicación en el dispositivo del usuario.
   * El icono debe ser un archivo png de tamaño 512 x 512 píxeles.
   * El icono debe estar [almacenado en DAM.](/help/assets/overview.md)

### Administración de caché (avanzada) {#offline-configuration}

Esta configuración hace que partes de este sitio estén disponibles sin conexión y disponibles localmente en el dispositivo del visitante. Esto permite controlar la caché de la aplicación web para optimizar las solicitudes de red y admitir experiencias sin conexión.

* **Estrategia de almacenamiento en caché y frecuencia de actualización de contenido** : esta configuración define el modelo de almacenamiento en caché para su PWA.
   * **Moderadamente** :  [esta ](https://web.dev/stale-while-revalidate/) configuración es la que se aplica a la mayoría de los sitios y es el valor predeterminado.
      * Con esta configuración, el contenido que el usuario ve por primera vez se carga desde la caché y, mientras el usuario consume ese contenido, el resto del contenido de la caché se vuelve a validar.
   * **Frecuentemente** : Este es el caso de los sitios que necesitan actualizaciones para ser muy rápidos, como las casas de subastas.
      * Con esta configuración, la aplicación buscará primero el contenido más reciente a través de la red y, si no está disponible, volverá a la caché local.
   * **Raramente** : este es el caso de los sitios que son casi estáticos, como las páginas de referencia.
      * Con esta configuración, la aplicación buscará primero el contenido en la caché y, si no está disponible, volverá a la red para recuperarlo.
* **Almacenamiento en caché previo de archivos** : Estos archivos alojados en AEM se guardarán en la caché del explorador local cuando el trabajador del servicio se instale y antes de utilizarse. Esto garantiza que la aplicación web funcione completamente cuando está sin conexión.
* **Inclusiones de rutas** : las solicitudes de red para las rutas definidas se interceptan y el contenido almacenado en caché se devuelve de acuerdo con la estrategia de  **almacenamiento en caché configurada y la frecuencia de actualización** del contenido.
* **Exclusiones de caché** : Estos archivos nunca se almacenarán en caché, independientemente de la configuración en  **File pre-** cachinging e  **Path inclusions**.

>[!TIP]
>
>Es probable que el equipo de desarrollador tenga datos valiosos sobre cómo se debe configurar la configuración sin conexión.

## Limitaciones y recomendaciones {#limitations-recommendations}

No todas las funciones de PWA están disponibles para AEM Sites. Estas son algunas limitaciones importantes.

* Un usuario debe navegar por la página al menos una vez antes de que se almacene en caché sin conexión.
* Las páginas no se sincronizan ni actualizan automáticamente si el usuario no utiliza la aplicación.

Adobe también realiza las siguientes recomendaciones al implementar PWA.

### Reduzca al máximo el número de recursos que se van a prealmacenar en caché. {#minimize-precache}

Adobe recomienda limitar el número de páginas que se prealmacenarán en caché.

* Incruste bibliotecas para reducir el número de entradas que se van a administrar al prealmacenar en caché.
* Limite el número de variaciones de imagen a la caché previa.

### Habilite PWA después de estabilizar los scripts de proyecto y las hojas de estilo. {#pwa-stabilized}

Las bibliotecas de cliente se entregan con la adición de un selector de caché que observa el siguiente patrón `lc-<checksumHash>-lc`. Cada vez que cambia uno de los archivos (y dependencias) que componen una biblioteca, este selector. Si enumeró una biblioteca de cliente para que la almacene previamente en caché el trabajador de servicios y desea hacer referencia a una nueva versión, recupere y actualice manualmente la entrada. Como resultado, le recomendamos que configure su sitio para que sea un PWA después de estabilizar los scripts de proyecto y las hojas de estilo.

### Minimice el número de variaciones de imagen. {#minimize-variations}

El componente de imagen de los componentes principales de AEM determina uno de los front-end la mejor representación que se debe recuperar. Este mecanismo también incluye una marca de tiempo que corresponde a la hora de la última modificación de ese recurso. Este mecanismo complica la configuración de la precaché de PWA.

Al configurar la caché previa, el usuario debe enumerar todas las variaciones de ruta que se pueden recuperar. Estas variaciones están compuestas de parámetros como calidad y anchura. Se recomienda reducir el número de estas variaciones a un máximo de tres: pequeñas, medianas y grandes. Puede hacerlo a través del cuadro de diálogo de política de contenido del [Componente de imagen.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html)

Si no se configura con cuidado, el consumo de memoria y de red puede afectar gravemente el rendimiento de su PWA. Además, si tiene intención de prealmacenar, por ejemplo, 50 imágenes y tiene 3 anchos por imagen, el usuario que mantenga el sitio deberá mantener una lista de hasta 150 entradas en la sección PWA de precaché de las propiedades de página.

Adobe también le recomienda configurar su sitio para que sea un PWA después de que el uso de imágenes en el proyecto se haya estabilizado.
