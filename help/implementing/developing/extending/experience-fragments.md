---
title: Información general sobre fragmentos de experiencias
description: Ampliar fragmentos de experiencias de Adobe Experience Manager as a Cloud Service.
exl-id: bd4ea763-d17c-40a6-9a86-a24d7600229e
source-git-commit: d361ddc9a50a543cd1d5f260c09920c5a9d6d675
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 1%

---

# Fragmentos de experiencias{#experience-fragments}

## Conceptos básicos {#the-basics}

Un [Fragmento de experiencia](/help/sites-cloud/authoring/fundamentals/experience-fragments.md) es un grupo de uno o más componentes, incluido el contenido y el diseño, al que se puede hacer referencia en las páginas.

Un fragmento de experiencia principal, una variante o ambos utilizan:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Porque no hay `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, vuelve a

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## Representación HTML sin formato {#the-plain-html-rendition}

Uso del `.plain.` en la dirección URL, puede acceder a la representación del HTML sin formato.

Esta representación está disponible en el explorador. Sin embargo, su propósito principal es permitir que otras aplicaciones (por ejemplo, aplicaciones web de terceros o implementaciones móviles personalizadas) accedan al contenido del fragmento de experiencia directamente, únicamente mediante la dirección URL.

La representación de HTML sin formato agrega el protocolo, el host y la ruta de contexto a las rutas que son:

* del tipo: `src`, `href`, o `action`

* o finalizar con: `-src`, o `-href`

Por ejemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Los vínculos siempre hacen referencia a la instancia de publicación. Están pensados para que los consuman terceros, por lo que siempre se llama al vínculo desde la instancia de publicación, no desde la instancia de autor.

![Representación de HTML sin formato](assets/xf-14.png)

El selector de representación sin formato utiliza un transformador en lugar de scripts adicionales. El [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) se utiliza como transformador. Este transformador se configura en lo siguiente:

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configuración de la generación de representaciones del HTML {#configuring-html-rendition-generation}

La representación del HTML se genera mediante las canalizaciones de reescritura de Sling. La canalización se define en `/libs/experience-fragments/config/rewriter/experiencefragments`. El transformador de HTML admite las siguientes opciones:

* `allowedCssClasses`
   * Expresión de RegEx que coincide con las clases CSS que deben dejarse en la representación final.
   * Esta opción es útil si el cliente desea eliminar algunas clases CSS específicas
* `allowedTags`
   * Una lista de etiquetas de HTML que se permitirán en la representación final.
   * De forma predeterminada, se permiten las siguientes etiquetas (no se necesita configuración): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link y script

El Adobe recomienda configurar la reescritura mediante una superposición. Consulte [AEM Superposiciones en el as a Cloud Service](/help/implementing/developing/introduction/overlays.md).

## Plantillas para fragmentos de experiencias {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Solo*** Las plantillas editables son compatibles con los fragmentos de experiencias.

<!-- >***Only*** [editable templates](/help/sites-developing/page-templates-editable.md) are supported for Experience Fragments.
-->

Al desarrollar una nueva plantilla para fragmentos de experiencias, puede seguir las prácticas estándar para una plantilla editable.

<!-- When developing a new template for Experience Fragments you can follow the standard practices for an [editable template](/help/sites-developing/page-templates-editable.md).
-->

Para crear una plantilla de fragmento de experiencia que detecte el **Crear fragmento de experiencia** asistente, debe seguir uno de estos conjuntos de reglas:

1. Ambas:

   1. El tipo de recurso de la plantilla (el nodo inicial) debe heredar de:
      `cq/experience-fragments/components/xfpage`

   1. Y el nombre de la plantilla debe comenzar por:
      `experience-fragments`
Este patrón permite a los usuarios crear fragmentos de experiencias en /content/experience-fragments como `cq:allowedTemplates` de esta carpeta incluye todas las plantillas que tienen nombres que comienzan por `experience-fragment`. Los clientes pueden actualizar esta propiedad para incluir sus propios esquemas de nomenclatura o ubicaciones de plantillas.

1. [Plantillas permitidas](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#configure-allowed-templates-folder) se puede configurar en la consola Fragmentos de experiencias.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiencias {#components-for-experience-fragments}

El desarrollo de componentes para su uso con/en fragmentos de experiencias sigue las prácticas estándar.

La única configuración adicional es garantizar que los componentes estén permitidos en la plantilla. Esta asignación se logra con la Política de contenido.

<!--
[Developing components](/help/sites-developing/components.md) for use with/in Experience Fragments follow standard practices.

The only additional configuration is to ensure that the components are [allowed on the template, this is achieved with the Content Policy](/help/sites-developing/page-templates-editable.md#content-policies).
-->

## El proveedor de reescritura de vínculos de fragmentos de experiencia: HTML {#the-experience-fragment-link-rewriter-provider-html}

AEM En el caso de los fragmentos de experiencias, tiene la posibilidad de crear fragmentos de experiencias. Un fragmento de experiencia:

* consta de un grupo de componentes junto con un diseño,
* AEM puede existir de forma independiente de una página de.

Uno de los casos de uso de estos grupos es para incrustar contenido en puntos de contacto de terceros, como Adobe Target.

### Reescritura de vínculos predeterminados {#default-link-rewriting}

<!--Using the [Export to Target](/help/sites-administering/experience-fragments-target.md) feature, you can:
-->

Con la función Exportar a destino, puede:

* crear un fragmento de experiencia,
* añadir componentes a él,
* y, a continuación, exportarla como una oferta de Adobe Target, ya sea en formato de HTML o en formato JSON.

AEM Esta función se puede habilitar en una instancia de autor de. Requiere una configuración de Adobe Target válida y configuraciones para el externalizador de vínculos.

<!--
This feature can be [enabled on an author instance of AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). It requires a valid Adobe Target Configuration, and configurations for the Link Externalizer.
-->

El externalizador de vínculos se utiliza para determinar las direcciones URL correctas necesarias al crear la versión de HTML de la oferta de Target, que luego se envía a Adobe Target. Este proceso es necesario, ya que Adobe Target requiere que se pueda acceder públicamente a todos los vínculos dentro de la oferta de HTML de Target. Significa que cualquier recurso al que hagan referencia los vínculos, y el propio fragmento de experiencia, deben publicarse antes de poder utilizarse.

De forma predeterminada, al crear una oferta de HTML AEM de Target, se envía una solicitud a un selector de Sling personalizado en, que se encuentra en el menú de configuración de la. Este selector se llama `.nocloudconfigs.html`. Como su nombre indica, crea una representación HTML sin formato de un fragmento de experiencia, pero no incluye configuraciones de nube (lo que sería información superflua).

Después de generar la página de HTML, la canalización de reescritura de Sling se modifica a la salida:

1. El `html`, `head`, y `body` Los elementos de se sustituyen por `div` elementos. El `meta`, `noscript`, y `title` elementos se eliminan (son elementos secundarios del original) `head` y no se tienen en cuenta cuando se sustituyen por el elemento `div` element).

   Este proceso se realiza para garantizar que la oferta de HTML Target se pueda incluir en las actividades de Target.

2. AEM modifica cualquier vínculo interno presente en el HTML para que señale a un recurso publicado.

   AEM Para determinar los vínculos que se van a modificar, el modelo sigue este patrón para los atributos de los elementos de HTML:

   1. `src` atributos
   2. `href` atributos
   3. `*-src` atributos (como `data-src`, y `custom-src`)
   4. `*-href` atributos (como `data-href`, `custom-href`, y `img-href`)

   >[!NOTE]
   >
   >Los vínculos internos del HTML son vínculos relativos, pero puede haber casos en los que los componentes personalizados proporcionen direcciones URL completas en el HTML. AEM De forma predeterminada, no tiene en cuenta estas direcciones URL completas y no realiza ninguna modificación.

   AEM Los vínculos de estos atributos se ejecutan a través del Externalizador de vínculos de `publishLink()` para volver a crear la dirección URL como si estuviera en una instancia publicada y, como tal, disponible públicamente.

Al utilizar una implementación predeterminada, el proceso descrito anteriormente debe ser suficiente para generar la oferta de Target a partir del fragmento de experiencia y luego exportarla a Adobe Target. Sin embargo, hay algunos casos de uso que no se tienen en cuenta en este proceso. Algunos de estos casos que no se tienen en cuenta son los siguientes:

* Asignación de Sling solo disponible en la instancia de publicación
* Redirecciones de Dispatcher

AEM Para estos casos de uso, proporciona la interfaz del proveedor de reescritura de vínculos de manera de.

### Interfaz de proveedor de reescritura de vínculos {#link-rewriter-provider-interface}

Para casos más complicados, no cubiertos por la [predeterminado](#default-link-rewriting)AEM , ofrece la interfaz del proveedor de reescritura de vínculos. Esta interfaz es una `ConsumerType` que puede implementar en sus paquetes como servicio. AEM Evita las modificaciones que realiza en los vínculos internos de una oferta de HTML que se representan desde un fragmento de experiencia. Esta interfaz le permite personalizar el proceso de reescritura de vínculos de HTML internos para adaptarlos a sus necesidades comerciales.

Algunos ejemplos de casos de uso para implementar esta interfaz como servicio son:

* Las asignaciones de Sling están habilitadas en las instancias de publicación, pero no en la instancia de autor
* Se utiliza una tecnología de Dispatcher o similar para redirigir las URL internamente
* El `sling:alias mechanisms` ya existen para los recursos

>[!NOTE]
>
>Esta interfaz solo procesa los vínculos de HTML internos de la oferta de Target generada.

La Interfaz De Proveedor De Reescritura De Vínculos ( `ExperienceFragmentLinkRewriterProvider`) es el siguiente:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Cómo utilizar la interfaz del proveedor de reescritura de vínculos {#how-to-use-the-link-rewriter-provider-interface}

Para utilizar la interfaz, primero debe crear un paquete que contenga un nuevo componente de servicio que implemente la interfaz del proveedor de reescritura de vínculos.

Este servicio se utiliza para conectarse a la reescritura de Exportación de fragmentos de experiencias a Target para que pueda tener acceso a los distintos vínculos.

Por ejemplo, `ComponentService`:

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

Para que el servicio funcione, ahora hay tres métodos que deben implementarse dentro del servicio:

* `[shouldRewrite](#shouldrewrite)`
* `[rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* `[getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Indique al sistema si debe reescribir los vínculos cuando se realice una llamada para Exportar a Target en una variación determinada del fragmento de experiencia. Puede implementar el siguiente método:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por ejemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Este método recibe, como parámetro, la variación del fragmento de experiencia que el sistema Exportar a destino está reescribiendo.

En el ejemplo anterior, desea volver a escribir:

* vínculos presentes en `src`

* `href` solo atributos

* para un fragmento de experiencia específico:
  `/content/experience-fragment/master`

Cualquier otro fragmento de experiencia que pase por el sistema Exportar a destino se ignorará y no se verá afectado por los cambios implementados en este servicio.

#### rewriteLink {#rewritelink}

Para la variación del fragmento de experiencia afectada por el proceso de reescritura, permite al servicio gestionar la reescritura de vínculos. Cada vez que se encuentra un vínculo en el HTML interno, se invoca el siguiente método:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, el método recibe los parámetros:

* `link`
El `String` representación del vínculo que se está procesando. Esta representación suele ser una dirección URL relativa que señala al recurso de la instancia de autor.

* `tag`
Nombre del elemento HTML que se está procesando.

* `attribute`
El nombre exacto del atributo.

Por ejemplo, si el sistema Exportar a destino está procesando este elemento, puede definir lo siguiente `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

La llamada a la `rewriteLink()` El método se realiza utilizando estos parámetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Al crear el servicio, las decisiones se basan en la entrada dada y, a continuación, reescriba el vínculo en consecuencia.

En el ejemplo, desea eliminar la variable `/etc.clientlibs` forme parte de la dirección URL y añada el dominio externo correspondiente. Para simplificar las cosas, considere que tiene acceso a un Resource Resolver para su servicio, como en `rewriteLinkExample2`:

>[!NOTE]
>
>AEM Para obtener más información sobre cómo obtener un solucionador de recursos a través de un usuario de servicio, consulte Usuarios de servicio en la documentación de usuario de servicio en la documentación de la aplicación de usuario de servicio de.

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

>[!NOTE]
>
>Si el método anterior devuelve `null`, el sistema Exportar a Target deja el vínculo tal cual, un vínculo relativo a un recurso.

#### Prioridades: getPriority {#priorities-getpriority}

No es raro necesitar varios servicios para atender diferentes tipos de fragmentos de experiencias o incluso tener un servicio genérico que gestione la externalización y la asignación para todos los fragmentos de experiencias. AEM En estos casos, pueden surgir conflictos sobre el servicio que se va a utilizar, por lo que ofrece la posibilidad de definir lo siguiente: **Prioridades** para diferentes servicios. Las prioridades se especifican mediante el método:

* `getPriority()`

Este método permite el uso de varios servicios en los que la variable `shouldRewrite()` El método devuelve true para el mismo fragmento de experiencia. El servicio que devuelve el número más alto de su `getPriority()`es el servicio que administra la variación del fragmento de experiencia.

Por ejemplo, puede tener un `GenericLinkRewriterProvider` que administra la asignación básica para todos los fragmentos de experiencias y cuando la variable `shouldRewrite()` método devuelve `true` para todas las variaciones de fragmentos de experiencias. Para varios fragmentos de experiencias específicos, es posible que desee una administración especial, por lo que en este caso, puede proporcionar un `SpecificLinkRewriterProvider` para la cual el `shouldRewrite()` El método solo devuelve el valor &quot;True&quot; para algunas variaciones de fragmentos de experiencias. Para asegurarse de que `SpecificLinkRewriterProvider` para gestionar esas variaciones de fragmentos de experiencias, debe devolver en su `getPriority()` método un número mayor que `GenericLinkRewriterProvider.`
