---
title: Fragmentos de experiencias
description: Extender el Adobe Experience Manager como fragmentos de experiencias Cloud Service.
translation-type: tm+mt
source-git-commit: 625e56efdab2f41026988fb90b72c31ff876db57
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 2%

---


# Fragmentos de experiencias{#experience-fragments}

## Conceptos básicos {#the-basics}

Un [fragmento de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) es un grupo de uno o varios componentes que incluye contenido y diseño que se puede consultar dentro de las páginas.

Un patrón de fragmentos de experiencia y/o una variante utiliza:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como no hay `/libs/cq/experience-fragments/components/xfpage/xfpage.html` se vuelve a

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Representación HTML sin formato {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition.

Está disponible desde el navegador, pero su principal objetivo es permitir que otras aplicaciones (por ejemplo, aplicaciones web de terceros, implementaciones móviles personalizadas) accedan al contenido del fragmento de experiencias directamente, utilizando solo la URL.

La representación HTML sin formato agrega el protocolo, el host y la ruta de contexto a las rutas que son:

* del tipo: `src`, `href`o `action`

* o finalizar con: `-src`, o `-href`

Por ejemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Los vínculos siempre hacen referencia a la instancia de publicación. Están pensados para ser consumidos por terceros, por lo que el vínculo siempre se llamará desde la instancia de publicación, no desde el autor.

![Representación HTML sin formato](assets/xf-14.png)

El selector de representación sin formato utiliza un transformador en lugar de secuencias de comandos adicionales; el [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) se utiliza como transformador. Se configura en

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variaciones sociales {#social-variations}

Las variantes sociales se pueden publicar en los medios sociales (texto e imagen). En AEM, estas variantes sociales pueden contener componentes; por ejemplo, componentes de texto, componentes de imagen.

La imagen y el texto del anuncio social se pueden tomar de cualquier tipo de recurso de imagen o de recurso de texto en cualquier nivel de profundidad (en el bloque de creación o en el contenedor de diseño).

Las variaciones sociales también permiten componentes básicos y los tienen en cuenta al realizar acciones sociales (en el entorno de publicación).

Para publicar el texto y la imagen correctos en la red de medios sociales, algunas convenciones deben respetarse si está desarrollando sus propios componentes personalizados.

Para ello, se deben utilizar las siguientes propiedades:

* Para extraer la imagen

   * `fileReference`
   * `fileName`

* Para extraer el texto

   * `text`

Los componentes que no utilicen esta convención no se tendrán en cuenta.

## Plantillas para fragmentos de experiencias {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Solo*** se admiten plantillas editables para fragmentos de experiencia.

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

Al desarrollar una nueva plantilla para fragmentos de experiencia, puede seguir las prácticas estándar de una plantilla editable.

<!-- When developing a new template for Experience Fragments you can follow follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Para crear una plantilla de fragmento de experiencia detectada por el asistente **Crear fragmento** de experiencia, debe seguir uno de estos conjuntos de reglas:

1. Ambas:

   1. El tipo de recurso de la plantilla (el nodo inicial) debe heredar de:
      `cq/experience-fragments/components/xfpage`

   1. Y el nombre de la plantilla debe comenzar por:
      `experience-fragments`
Esto permite a los usuarios crear fragmentos de experiencia en /content/experience-fragments, ya que la `cq:allowedTemplates` propiedad de esta carpeta incluye todas las plantillas con nombres que comienzan por `experience-fragment`. Los clientes pueden actualizar esta propiedad para incluir su propio esquema de nombres o ubicaciones de plantillas.
[Las plantillas](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) permitidas se pueden configurar en la consola Fragmentos de experiencia.

1. Componentes para fragmentos de experiencias {#components-for-experience-fragments}](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder)

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## El desarrollo de componentes para su uso con o en fragmentos de experiencia sigue las prácticas estándar.{#components-for-experience-fragments}

La única configuración adicional es asegurarse de que los componentes están permitidos en la plantilla; esto se logra con la directiva de contenido.

El proveedor de la reescritura de los vínculos de los fragmentos de experiencia: HTML {#the-experience-fragment-link-rewriter-provider-html}

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## En AEM puede crear fragmentos de experiencia. Un fragmento de experiencia:{#the-experience-fragment-link-rewriter-provider-html}

consiste en un grupo de componentes junto con una presentación,

* puede existir independientemente de una página de AEM.
* Uno de los casos de uso de estos grupos es para incrustar contenido en puntos de contacto de terceros, como Adobe Target.

Reescritura de vínculos predeterminada {#default-link-rewriting}

### Con la función Exportar a Destinatario, puede:{#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

crear un fragmento de experiencia,

* añadir componentes a la misma,
* y, a continuación, expórtela como una Oferta de Adobe Target, ya sea en formato HTML o JSON.
* Esta función se puede activar en una instancia de autor de AEM. Requiere una configuración de Adobe Target válida y configuraciones para el Externalizador de vínculos.

El Externalizador de vínculos se utiliza para determinar las direcciones URL correctas necesarias al crear la versión HTML de la Oferta de Destinatario, que se envía posteriormente a Adobe Target. Esto es necesario, ya que Adobe Target requiere que todos los vínculos dentro de la Oferta HTML de Destinatario puedan ser accesibles al público; esto significa que los recursos a los que hacen referencia los vínculos y el propio fragmento de experiencias deben publicarse antes de poder utilizarse.

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

De forma predeterminada, cuando se crea una Oferta HTML de Destinatario, se envía una solicitud a un selector de Sling personalizado en AEM. Se llama a este selector `.nocloudconfigs.html`. Como su nombre lo indica, crea una representación HTML sin formato de un fragmento de experiencias, pero no incluye configuraciones de nube (que sería información superflua).

Después de generar la página HTML, la canalización de Sling Rewriter realiza modificaciones en el resultado:`.nocloudconfigs.html`

Los elementos `html`, `head`y `body` se reemplazan por `div` elementos. Los elementos `meta`, `noscript` y `title` se eliminan (son elementos secundarios del `head` elemento original y no se tienen en cuenta cuando se reemplaza por el `div` elemento).

1. Esto se realiza para garantizar que la Oferta de Destinatario HTML se puede incluir en Actividades de Destinatario.`html``head``body``div``meta``noscript``title``head``div`

   AEM modifica los vínculos internos presentes en el HTML para que señalen a un recurso publicado.

2. Para determinar los vínculos que se van a modificar, AEM sigue este patrón para los atributos de los elementos HTML:

   `src` atributos

   1. `href` atributos
   2. `*-src` atributos (como data-src, custom-src, etc.)
   3. `*-href` atributos (como `data-href`, `custom-href`, `img-href`, etc.)
   4. [!NOTE]`data-href``custom-href``img-href`

   >[!NOTE]En la mayoría de los casos, los vínculos internos en el HTML son vínculos relativos, pero puede haber casos en los que los componentes personalizados proporcionen direcciones URL completas en el HTML. De forma predeterminada, AEM omite estas direcciones URL completas y no realiza ninguna modificación.
   >
   >Los vínculos de estos atributos se ejecutan a través del Externalizador de vínculos de AEM `publishLink()` para recrear la dirección URL como si estuviera en una instancia publicada y, como tal, disponible públicamente.

   Al utilizar una implementación lista para usar, el proceso descrito anteriormente debería ser suficiente para generar la Oferta de Destinatario a partir del fragmento de experiencias y luego exportarla a Adobe Target. Sin embargo, hay algunos casos de uso que no se tienen en cuenta en este proceso; entre ellos se incluyen:`publishLink()`

Asignación de Sling disponible solo en la instancia de publicación

* Redirecciones de Dispatcher
* En estos casos de uso, AEM proporciona la interfaz del proveedor de reescritores de vínculos.

Vincular interfaz de proveedor de reescritores {#link-rewriter-provider-interface}

### Para casos más complicados, no cubiertos por la [opción predeterminada](#default-link-rewriting), AEM oferta la interfaz del proveedor de reescritores de vínculos. Se trata de una `ConsumerType` interfaz que puede implementar en los paquetes, como un servicio. Omite las modificaciones que AEM realiza en los vínculos internos de una oferta HTML tal como se representa desde un fragmento de experiencia. Esta interfaz le permite personalizar el proceso de reescritura de los vínculos HTML internos para adaptarlos a sus necesidades comerciales.

Algunos ejemplos de casos de uso para implementar esta interfaz como servicio son:[](#default-link-rewriting)`ConsumerType`

Las asignaciones de desplazamiento están activadas en las instancias de publicación, pero no en la instancia de autor

* Un despachante o tecnología similar se utiliza para redireccionar las direcciones URL internamente
* Existen `sling:alias mechanisms` recursos
* [!NOTE]

>[!NOTE]Esta interfaz sólo procesa los vínculos HTML internos desde la Oferta de Destinatario generada.
>
>La interfaz del proveedor de reescritores de vínculos ( `ExperienceFragmentLinkRewriterProvider`) es la siguiente:

Cómo utilizar la interfaz del proveedor de reescritores de vínculos {#how-to-use-the-link-rewriter-provider-interface}

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Para utilizar la interfaz, primero debe crear un paquete que contenga un nuevo componente de servicio que implemente la interfaz del proveedor de reescritores de vínculos.{#how-to-use-the-link-rewriter-provider-interface}

Este servicio se utilizará para conectar la reescritura de la exportación de fragmentos de experiencia a Destinatario para tener acceso a los distintos vínculos.

Por ejemplo, `ComponentService`:

Para que el servicio funcione, ahora hay tres métodos que deben implementarse dentro del servicio:`ComponentService`

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

` [shouldRewrite](#shouldrewrite)`

* ` [rewriteLink](#rewritelink)`
* `rewriteLinkExample2`

   * ` [getPriority](#priorities-getpriority)`

* mustRewrite {#shouldrewrite}

#### Debe indicar al sistema si necesita reescribir los vínculos cuando se realiza una llamada para Exportar a Destinatario en una determinada variación de fragmento de experiencia. Para ello, implemente el método:{#shouldrewrite}

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`Por ejemplo:

Este método recibe, como parámetro, la variación del fragmento de experiencia que el sistema Exportar a Destinatario está reescribiendo.

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

En el ejemplo anterior, nos gustaría reescribir:

vínculos presentes en `src`

* `href` sólo atributos

* `href`para un fragmento de experiencia específico:


* `/content/experience-fragment/master`   `/content/experience-fragment/master`Cualquier otro fragmento de experiencia que pase por el sistema Exportar a Destinatario se ignora y no se ve afectado por los cambios implementados en este servicio.

rewriteLink {#rewritelink}

#### Para la variación del fragmento de experiencias que se ve afectada por el proceso de reescritura, el servicio podrá administrar la reescritura del vínculo. Cada vez que se encuentra un vínculo en el HTML interno, se invoca el siguiente método:{#rewritelink}

`rewriteLink(String link, String tag, String attribute)`

`rewriteLink(String link, String tag, String attribute)`Como entrada, el método recibe los parámetros:

`link`
La `String` representación del vínculo que se está procesando actualmente. Generalmente es una URL relativa que apunta al recurso en la instancia de autor.

* `tag`
Nombre del elemento HTML que se está procesando en este momento.
`attribute`
El nombre exacto del atributo.

* Si, por ejemplo, el sistema Exportar a Destinatario está procesando este elemento en este momento, puede definirlo `CSSInclude` como:

* La llamada al `rewriteLink()` método se realiza utilizando estos parámetros:

Al crear el servicio, puede tomar decisiones en función de la entrada dada y, a continuación, volver a escribir el vínculo en consecuencia.`CSSInclude`

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

Para nuestro ejemplo, nos gustaría quitar la parte `/etc.clientlibs` de la dirección URL y agregar el dominio externo apropiado. Para simplificar las cosas, consideraremos que tenemos acceso a un Resoltor de recursos para su servicio, como en `rewriteLinkExample2`:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

[!NOTE]

Para obtener más información sobre cómo obtener una resolución de recursos a través de un usuario de servicios, consulte Usuarios de servicios en AEM.`/etc.clientlibs``rewriteLinkExample2`

>[!NOTE]
>
>Si se devuelve el método anterior `null`, el sistema Exportar a Destinatario dejará el vínculo tal como está, un vínculo relativo a un recurso.

<!--
>For more information on how to get a resource resolver through a service user see [Service Users in AEM](/help/sites-administering/security-service-users.md).
-->

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>Prioridades - getPriority {#priorities-getpriority}
>
>No es raro necesitar varios servicios para atender diferentes tipos de fragmentos de experiencia, o incluso para tener un servicio genérico que gestione la externalización y la asignación de todos los fragmentos de experiencia. En estos casos, surgen conflictos sobre qué servicio utilizar, por lo que AEM ofrece la posibilidad de definir **prioridades** para distintos servicios. Las prioridades se especifican mediante el método:

#### `getPriority()`

Este método permite el uso de varios servicios en los que el `shouldRewrite()` método devuelve true para el mismo fragmento de experiencia. El servicio que devuelve el número más alto de su `getPriority()`método es el servicio que gestiona la variación del fragmento de experiencias.

* Por ejemplo, puede tener un `GenericLinkRewriterProvider` que gestione la asignación básica para todos los fragmentos de experiencia y cuando el `shouldRewrite()` método se devuelva `true` para todas las variaciones de fragmento de experiencia. Para varios fragmentos de experiencia específicos, es posible que desee una gestión especial, por lo que en este caso, puede proporcionar un `SpecificLinkRewriterProvider` método para el que el `shouldRewrite()` método devuelve true solo para algunas variaciones de fragmento de experiencia. Para asegurarse de que `SpecificLinkRewriterProvider` se elige gestionar esas variaciones de fragmento de experiencia, debe devolver en su `getPriority()` método un número mayor que `GenericLinkRewriterProvider.`

This method allows the use of several services where the `shouldRewrite()` method returns true for the same Experience Fragment. The service that returns the highest number from its `getPriority()`method is the service that handles the Experience Fragment Variation.

As an example, you can have a `GenericLinkRewriterProvider` that handles the basic mapping for all Experience Fragments and when the `shouldRewrite()` method returns `true` for all Experience Fragment Variations. For several specific Experience Fragments, you may want special handling, so in this case, you can provide a `SpecificLinkRewriterProvider` for which the `shouldRewrite()` method returns true only for some Experience Fragment Variations. To make sure that `SpecificLinkRewriterProvider` is chosen to handle those Experience Fragment Variations, it must return in its `getPriority()` method a higher number than `GenericLinkRewriterProvider.`