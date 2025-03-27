---
title: Verificador de vínculos
description: Descubra cómo el Verificador de vínculos ayuda a los autores validando los vínculos a medida que se agregan al contenido y qué opciones de configuración ofrece.
feature: Operations
role: Admin
source-git-commit: cc8e242715faaef5cda25b428c315947ec3d7e06
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---


# Verificador de vínculos {#link-checker}

Descubra cómo el Verificador de vínculos ayuda a los autores validando los vínculos a medida que se agregan al contenido y qué opciones de configuración ofrece.

## Información general {#overview}

Los autores de contenido no deberían tener que preocuparse por validar cada vínculo que incluyen en su contenido. El Verificador de vínculos se ejecuta automáticamente para ayudar a los autores de contenido con sus vínculos, incluidos los siguientes:

* Validación de vínculos a medida que se añaden al contenido
* Mostrar una lista de todos los vínculos externos del contenido
* Realización de transformaciones de vínculos

El Verificador de vínculos tiene varias [opciones de configuración](#configuring), como definir la validación de vínculos internos, permitir que ciertos vínculos o patrones de vínculos se omitan de la validación y definir reglas de reescritura de vínculos.

El Verificador de vínculos valida [vínculos internos](#internal) y [vínculos externos.](#external)

>[!NOTE]
>
>Dado que el Verificador de vínculos comprueba los vínculos de todas las páginas de contenido, puede afectar al rendimiento de los repositorios grandes. En estos casos, es posible que tenga que [configurar la frecuencia con la que se ejecuta el Verificador de vínculos](#configuring) o [deshabilitarlo.](#disabling)

## Comprobación de vínculos internos {#internal}

Los vínculos internos son vínculos a otro contenido del repositorio de AEM. Los vínculos internos se pueden agregar mediante el selector de rutas, el editor de texto enriquecido o mediante un componente personalizado. Por ejemplo:

* Usted crea la página `/content/wknd/us/en/adventures/ski-touring`
* Esa página contiene un vínculo a `/content/wknd/us/en/adventures/extreme-ironing` en un [componente Texto.](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/text)

Los vínculos internos se validan en cuanto el autor de contenido añade un vínculo de este tipo a una página. Si el vínculo deja de ser válido:

* Se elimina del editor.
   * El vínculo en sí se elimina.
   * El texto del vínculo permanece.
* Se muestra como un vínculo roto en la interfaz de creación.

![Verificador de vínculos que comprueba los vínculos internos](assets/link-checker-internal.png)

## Comprobación de vínculos externos {#external}

Los vínculos externos son vínculos a contenido fuera del repositorio de AEM. Los vínculos externos se pueden agregar mediante el editor de texto enriquecido o mediante un componente personalizado. Por ejemplo:

* Usted crea la página `/content/wknd/us/en/adventures/ski-touring`
* Esa página contiene un vínculo a `https://bunwarmerthermalunderwear.com` en un [componente Texto.](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/text)

Los vínculos externos se validan para la sintaxis y comprobando su disponibilidad. Esta comprobación se realiza de forma asíncrona a un intervalo configurable. Si el Verificador de vínculos encuentra un vínculo externo no válido:

* Se elimina del editor.
   * El vínculo en sí se elimina.
   * El texto del vínculo permanece.
* Se muestra como un vínculo roto en la interfaz de creación.

![Verificador de vínculos que comprueba los vínculos externos](assets/link-checker-external.png)

### Funcionamiento del Comprobador de vínculos externos {#external-details}

El Verificador de vínculos externos se basa en varios servicios y comprender cómo funcionan le ayuda a comprender cómo [configurar el Verificador de vínculos para satisfacer sus necesidades.](#configuring)

1. Cada vez que un autor de contenido guarda un vínculo a una página, se activa un controlador de eventos.
1. El controlador de eventos recorre todo el contenido de `/content`, busca vínculos nuevos o actualizados y los agrega a una caché para el Verificador de vínculos.
1. A continuación, el **servicio Day CQ Link Checker** se ejecuta de forma regular para comprobar si las entradas de la caché contienen sintaxis válida.
1. Los vínculos validados por sintaxis aparecerán en la ventana [Comprobador de vínculos externos.](#external-using) Sin embargo, estarán en estado **Pendiente**.
1. A continuación, **la tarea Day CQ Link Checker Task** se ejecuta de forma regular para validar los vínculos mediante una llamada de GET.
1. La **tarea Day CQ Link Checker** actualiza las entradas de la [ventana External Link Checker](#external-using) con los resultados de las llamadas de GET.

### Uso del Comprobador de vínculos externos {#external-using}

El verificador de vínculos externos es una consola que proporciona una visión general de todos los vínculos externos del contenido de AEM. Para utilizar el Comprobador de vínculos externos:

1. En Navegación global, seleccione **Herramientas** -> **Sitios**.
1. Seleccione **Comprobador de vínculos externos** y se mostrará una lista de todos los vínculos externos.

![Comprobador de vínculos externos](assets/external-link-checker.png)

Cada entrada de la tabla representa un vínculo externo detectado por el servicio Link Checker. Se muestran las siguientes columnas:

* **Estado** - El estado de validación del vínculo que puede ser uno de los siguientes:
   * **Válido**: el verificador de vínculos puede acceder al vínculo externo.
   * **Pendiente**: el vínculo externo se agregó al contenido del sitio, pero el Verificador de vínculos aún no lo ha validado.
   * **No válido** - El verificador de vínculos no puede acceder al vínculo externo.
* **URL**: el vínculo externo
* **Referente**: la página de contenido que contiene el vínculo externo
   * Esto solo se rellena [si está configurado.](#configuring)
* **Última comprobación** - La última vez que el Verificador de vínculos validó el vínculo externo
   * La frecuencia con la que se comprueban los vínculos [ es configurable.](#configuring)
* **Último estado**: el último código de estado de HTML devuelto cuando el vínculo comprobado comprobó por última vez el vínculo externo
* **Última disponibilidad** - Tiempo desde la última vez que el vínculo estuvo disponible para el Verificador de vínculos
* **Último acceso**: tiempo transcurrido desde que se accedió por última vez a la página con el vínculo externo en la interfaz de creación

Puede manipular el contenido de la ventana mediante los dos botones situados en la parte superior de la lista de vínculos:

* **Actualizar** - Para actualizar el contenido de la lista
* **Comprobar** - Para comprobar un vínculo externo individual seleccionado en la lista

Todos los demás iconos de la ventana Comprobador de vínculos externos están inactivos.

## Configuración del Verificador de vínculos {#configuring}

El Verificador de vínculos está disponible de forma predeterminada en AEM. Sin embargo, hay varias configuraciones de OSGi que se pueden modificar para cambiar su comportamiento:

* **Servicio Day CQ Link Checker Info Storage**: este servicio define el tamaño de la caché del Verificador de vínculos en el repositorio.
* **Servicio Day CQ Link Checker**: este servicio realiza una comprobación asincrónica de la sintaxis de los vínculos externos.
   * Puede definir el periodo de comprobación y qué tipos de vínculos omite el verificador, entre otras opciones.
* **Tarea del verificador de vínculos CQ de día**: este servicio realiza la validación GET de los vínculos externos.
   * Permite definir por separado los intervalos para comprobar los vínculos buenos y malos, entre otras opciones.
* **Day CQ Link Checker Transformer**: este servicio convierte los vínculos según un conjunto de reglas definidas por el usuario.

Consulte el documento [Configuración de OSGi](/help/implementing/deploying/configuring-osgi.md) para obtener más información sobre cómo cambiar la configuración de OSGi.

## Desactivación del Verificador de vínculos {#disabling}

Puede optar por desactivar el Verificador de vínculos por completo. Para ello:

1. Abra la consola OSGi.
1. Editar el **transformador Day CQ Link Checker**
1. Marque las opciones que desee desactivar:
   * **Deshabilitar comprobación** - para deshabilitar la validación de vínculos
   * **Deshabilitar la reescritura** - para deshabilitar las transformaciones de vínculos
