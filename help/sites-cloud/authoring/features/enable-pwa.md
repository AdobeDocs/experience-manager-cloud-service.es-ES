---
title: Activación de las funciones progresivas de la aplicación web
description: AEM Sites permite al autor del contenido activar las funciones de aplicación web progresiva en cualquier sitio mediante una configuración sencilla en lugar de codificar.
hide: true
hidefromtoc: true
translation-type: tm+mt
source-git-commit: 071eefa3b6f5e9636ace612e968b6a9627c98550
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# Activación de las funciones progresivas de la aplicación Web {#enabling-pwa}

A través de una configuración sencilla, un autor de contenido ahora puede activar las funciones de aplicación web progresiva (PWA) para las experiencias creadas en AEM Sites.

>[!CAUTION]
>
>Se trata de una función avanzada que requiere:
>
>* Conocimientos de los PWA
>* Conocimiento del sitio y estructura de contenido
>* Comprensión de las estrategias de almacenamiento en caché
>* Asistencia de su equipo de desarrollo

>
>
Antes de utilizar esta función, se recomienda que lo comente con su equipo de desarrollo para definir la mejor manera de aprovecharla para su proyecto.

## Introducción {#introduction}

[Las aplicaciones web progresivas (PWA)](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) permiten crear experiencias de aplicación envolventes para los sitios AEM, ya que permiten almacenarlas localmente en el equipo de un usuario y acceder a ellas sin conexión. Un usuario puede navegar por un sitio mientras está en movimiento, incluso si pierde una conexión a Internet. Los PWA permiten experiencias sin fisuras incluso si la red se pierde o es inestable.

En lugar de requerir que se vuelva a codificar el sitio, un autor de contenido puede configurar las propiedades de PWA como una ficha adicional en las [propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) de un sitio.

* Cuando se guarda o publica, esta configuración déclencheur un controlador de evento que escribe los [archivos de manifiesto](https://developer.mozilla.org/en-US/docs/Web/Manifest) y [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que habilitan las funciones de PWA en el sitio.
* El manifiesto y el trabajador de servicios se almacenan en [configuración según el contexto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/context-aware-configs.html) aplicable al sitio. Las asignaciones de Sling también se mantienen para garantizar que el trabajador de servicios se ofrezca desde la raíz de la aplicación para habilitar el contenido de proxying y permitir las funciones sin conexión dentro de la aplicación.

Con PWA, el usuario dispone de una copia local del sitio, lo que le permite disfrutar de una experiencia parecida a la aplicación, incluso sin conexión a Internet.

>[!NOTE]
>
>Las aplicaciones web progresivas son una tecnología en evolución y la compatibilidad con la instalación local de aplicaciones y otras funciones [depende del explorador que utilice.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)

## Requisitos previos {#prerequisites}

Para poder utilizar las funciones de PWA en el sitio, existen dos requisitos para el entorno del proyecto:

1. [Ajuste los ](#adjust-components) componentes para habilitar esta función
1. [Ajuste las reglas de ](#adjust-dispatcher) envío para exponer los archivos necesarios

Estos son pasos técnicos que el autor deberá coordinar con el equipo de desarrollo. Estos pasos sólo se requieren una vez por sitio.

### Ajustar los componentes {#adjust-components}

Los componentes deben incluir los [archivos de manifiesto](https://developer.mozilla.org/en-US/docs/Web/Manifest) y [programas de trabajo de servicio,](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) que admiten las funciones de PWA.

Para ello, el desarrollador deberá agregar el siguiente vínculo al archivo `customheaderlibs.html` del componente de página.

```xml
<link rel="manifest" href="/content/<projectName>/manifest.webmanifest" crossorigin="use-credentials"/>
```

El desarrollador también deberá agregar el siguiente vínculo al archivo `customfooterlibs.html` del componente de página.

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

>[!NOTE]
>
>Las versiones futuras de los [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) incluirán estas funciones automáticamente. Sin embargo, si utiliza componentes personalizados en lugar de componentes principales, siempre será necesario realizar estos ajustes.

### Ajustar el despachante {#adjust-dispatcher}

La función PWA genera y utiliza `/content/<sitename>/manifest.webmanifest` archivos. De forma predeterminada, [el despachante](/help/implementing/dispatcher/overview.md) no expone estos archivos. Para exponer estos archivos, el desarrollador debe agregar la siguiente configuración al proyecto del sitio.

```text
File location: [project directory]/dispatcher/src/conf.dispatcher.d/filters/filters.any >

# Allow webmanifest files
/0102 { /type "allow" /extension "webmanifest" /path "/content/*/manifest" }
```

>[!NOTE]
>
>Las versiones futuras del [AEM Arquetipo de proyecto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en#developing) incluirán esta configuración.

## Habilitación del PWA para su sitio {#enabling-pwa-for-your-site}

Con [los requisitos previos](#prerequisites) cumplidos, es muy fácil para un autor de contenido habilitar las funciones de PWA en un sitio. A continuación se muestra un esquema básico de cómo hacerlo. Las opciones individuales se detallan en la sección [Opciones detalladas.](#detailed-options)

1. Inicie sesión en AEM.
1. En el menú principal, toque o haga clic en **Navegación** -> **Sitios**.
1. Seleccione el proyecto del sitio y toque o haga clic en [**Propiedades**](/help/sites-cloud/authoring/fundamentals/page-properties.md) o utilice la tecla de acceso directo `p`.
1. Seleccione la ficha **Aplicación Web progresiva** y configure las propiedades aplicables. Como mínimo, querrá:
   1. Seleccione la opción **Habilitar PWA**.
   1. Defina la **URL de inicio**.

      ![Habilitar PWA](../assets/pwa-enable.png)

   1. Cargue un icono de 512 x 512 ping en el DAM y haga referencia a él como icono para la aplicación.

      ![Icono Definir PWA](../assets/pwa-icon.png)

   1. Configure las rutas que desea que el trabajador de servicios se desconecte. Las rutas típicas son:
      * `/content/<sitename>`
      * `/content/experiencefragements/<sitename>`
      * `/content/dam/<sitename>`
      * Referencias de fuentes de terceros
      * `/etc/clientlibs/<sitename>`

      ![Definir rutas sin conexión de PWA](../assets/pwa-offline.png)


1. Toque o haga clic en **Guardar y cerrar**.

Su sitio está configurado y puede [instalarlo como una aplicación local.](#using-pwa-enabled-site)

## Uso del sitio habilitado para PWA {#using-pwa-enabled-site}

Ahora que ha [configurado su sitio para admitir a PWA,](#enabling-pwa-for-your-site) puede experimentarlo usted mismo.

1. Acceda al sitio en un [navegador admitido.](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs#Summary)
1. Verá un icono `+` en la barra de direcciones del explorador, que indica que el sitio se puede instalar como una aplicación local.
   * Según el navegador, también puede mostrar una notificación (como un letrero o un cuadro de diálogo) que indique que es posible realizar la instalación como aplicación local.
1. Instale la aplicación.
1. La aplicación se instalará en la pantalla de inicio del dispositivo.
1. Abra la aplicación, navegue un poco y vea que las páginas están disponibles sin conexión.

## Opciones detalladas {#detailed-options}

La siguiente sección proporciona más detalles sobre las opciones disponibles al [configurar el sitio para PWA.](#enabling-pwa-for-your-site)

### Configurar experiencia instalable {#configure-installable-experience}

Esta configuración permite que el sitio se comporte como una aplicación nativa, ya que la puede instalar en la pantalla de inicio del visitante y está disponible sin conexión.

* **Habilitar PWA** : es la opción principal para habilitar el PWA para el sitio.
* **URL**  de inicio: esta es la  [URL de inicio ](https://developer.mozilla.org/en-US/docs/Web/Manifest/start_url) preferida que la aplicación se abrirá cuando el usuario cargue la aplicación instalada localmente.
   * Puede ser cualquier ruta de la estructura de contenido.
   * No tiene que ser la raíz y es a menudo una página de bienvenida dedicada para la aplicación.
   * Si esta dirección URL es relativa, la dirección URL de manifiesto se utiliza como dirección URL base para resolverla.
   * Cuando se deja vacía, la función utiliza la dirección de la página web desde la que se instaló la aplicación web.
   * Se recomienda establecer un valor.
* **Modo**  de visualización: una aplicación con PWA habilitado sigue siendo un sitio AEM entregado a través de un explorador. [Estas ](https://developer.mozilla.org/en-US/docs/Web/Manifest/display) opciones de visualización definen cómo se debe ocultar o presentar el explorador al usuario en el dispositivo local.
   * **Independiente** : el navegador está completamente oculto para el usuario y parece una aplicación nativa. Este es el valor predeterminado.
      * Con esta opción, la navegación de la aplicación debe ser posible por completo a través del contenido mediante vínculos y componentes en las páginas del sitio sin utilizar los controles de navegación del navegador.
   * **Explorador** : el explorador aparece como lo haría normalmente al visitar el sitio.
   * **IU**  mínima: el navegador está principalmente oculto, como una aplicación nativa, pero se exponen los controles de navegación básicos.
   * **Pantalla**  completa: el navegador está completamente oculto, como una aplicación nativa, pero se procesa en modo de pantalla completa.
      * Con esta opción, la navegación de la aplicación debe ser posible por completo a través del contenido mediante vínculos y componentes en las páginas del sitio sin utilizar los controles de navegación del navegador.
* **Orientación**  de pantalla: como aplicación local, el PWA debe saber cómo gestionar las orientaciones  [del dispositivo.](https://developer.mozilla.org/en-US/docs/Web/Manifest/orientation)
   * **Cualquiera** : la aplicación se ajusta a la orientación del dispositivo del usuario. Este es el valor predeterminado.
   * **Vertical** : esto fuerza a la aplicación a abrirse en diseño vertical independientemente de la orientación del dispositivo del usuario.
   * **Horizontal** : esto fuerza a la aplicación a abrirse en diseño horizontal independientemente de la orientación del dispositivo del usuario.
* **Color**  del tema: define el  [color de la ](https://developer.mozilla.org/en-US/docs/Web/Manifest/theme_color) aplicación que afecta al modo en que el sistema operativo del usuario local muestra la barra de herramientas de la interfaz de usuario nativa y los controles de navegación. Según el navegador, puede afectar a otros elementos de presentación de la aplicación.
   * Utilice la ventana emergente de pozo de color para seleccionar un color.
   * El color también se puede definir mediante valores hexadecimales o RGB.
* **Color**  de fondo: define el color de  [fondo de la aplicación, ](https://developer.mozilla.org/en-US/docs/Web/Manifest/background_color) que se muestra a medida que se carga la aplicación.
   * Utilice la ventana emergente de pozo de color para seleccionar un color.
   * El color también se puede definir mediante valores hexadecimales o RGB.
   * Algunos exploradores [crean una pantalla de bienvenida automáticamente](https://developer.mozilla.org/en-US/docs/Web/Manifest#Splash_screens) a partir del nombre de la aplicación, el color de fondo y el icono.
* **Icono** : define  [el ](https://developer.mozilla.org/en-US/docs/Web/Manifest/icons) icono que representa la aplicación en el dispositivo del usuario.
   * El icono debe ser un archivo png de tamaño de 512 x 512 píxeles.
   * El icono debe estar [almacenado en DAM.](/help/assets/overview.md)

### Administración de caché (avanzada) {#offline-configuration}

Esta configuración hace que partes de este sitio estén disponibles sin conexión y localmente en el dispositivo del visitante. Esto permite controlar la caché de la aplicación web para optimizar las solicitudes de red y admitir experiencias sin conexión.

* **Estrategia de almacenamiento en caché y frecuencia de actualización**  de contenido: esta configuración define el modelo de almacenamiento en caché para el PWA.
   * **Moderadamente** :  [Esta ](https://web.dev/stale-while-revalidate/) configuración es el caso de la mayoría de los sitios y es el valor predeterminado.
      * Con esta configuración, el contenido que el usuario ve por primera vez se carga desde la caché y, mientras que el usuario está consumiendo ese contenido, el resto del contenido de la caché se vuelve a validar.
   * **Frecuentemente** - Este es el caso de los sitios que necesitan actualizaciones para ser muy rápidos, como las casas de subastas.
      * Con este ajuste, la aplicación buscará primero el contenido más reciente a través de la red y, si no está disponible, volverá a la caché local.
   * **Raramente** : este es el caso de los sitios que son casi estáticos, como las páginas de referencia.
      * Con este ajuste, la aplicación buscará primero el contenido en la caché y, si no está disponible, volverá a la red para recuperarlo.
* **Almacenamiento previo**  de archivos: estos archivos alojados en AEM se guardarán en la caché del explorador local cuando se instale el programa de trabajo del servicio y antes de que se utilice. Esto garantiza que la aplicación web funcione completamente cuando esté sin conexión.
* **Inclusiones**  de rutas: las solicitudes de red para las rutas definidas se interceptan y el contenido en caché se devuelve de acuerdo con la estrategia de  **almacenamiento en caché configurada y la frecuencia de actualización** de contenido.
* **Exclusiones**  de caché: estos archivos nunca se almacenarán en la caché, independientemente de la configuración de  **Archivo anterior al** almacenamiento en caché e inclusiones  **de ruta**.

>[!TIP]
>
>Es probable que el equipo de desarrolladores tenga una valiosa información sobre cómo configurar la configuración sin conexión.

## Restricciones     {#limitations}

No todas las funciones de PWA están disponibles para AEM Sites. Estas son algunas limitaciones notables.

* Un usuario debe explorar la página al menos una vez antes de almacenarla en la caché sin conexión.
* Las páginas no se sincronizan ni actualizan automáticamente si el usuario no utiliza la aplicación.
