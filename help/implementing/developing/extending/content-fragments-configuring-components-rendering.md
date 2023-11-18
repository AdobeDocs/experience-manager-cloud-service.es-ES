---
title: Fragmentos de contenido Configurar componentes para procesamiento
description: Fragmentos de contenido Configurar componentes para procesamiento
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 6%

---

# Fragmentos de contenido Configurar componentes para procesamiento{#content-fragments-configuring-components-for-rendering}

Hay varios [servicios avanzados](#definition-of-advanced-services-that-need-configuration) relacionado con la renderización de fragmentos de contenido. Para utilizar estos servicios, los tipos de recurso de dichos componentes deben darse a conocer al marco de trabajo de fragmentos de contenido.

Esto se hace configurando la variable [Servicio OSGi: configuración del componente Fragmento de contenido](#osgi-service-content-fragment-component-configuration).

Esta información es necesaria cuando:

* Debe implementar su propio componente basado en fragmentos de contenido,
* Y necesita hacer uso de los servicios avanzados.

El Adobe recomienda utilizar los componentes principales.

>[!CAUTION]
>
>* **Si no necesita el [servicios avanzados](#definition-of-advanced-services-that-need-configuration)** Como se describe a continuación, puede ignorar esta configuración.
>
>* **Al ampliar o utilizar los componentes predeterminados de la aplicación** Sin embargo, no se recomienda cambiar la configuración de OSGi.
>
>* **Puede escribir un componente desde cero que utilice solo la API de fragmentos de contenido, sin servicios avanzados**. Sin embargo, en tal caso, deberá desarrollar el componente para que se ocupe del procesamiento adecuado.
>
>Por lo tanto, se recomienda utilizar los componentes principales.

## Definición de servicios avanzados que necesitan configuración {#definition-of-advanced-services-that-need-configuration}

Los servicios que requieren el registro de un componente son:

* Determinar correctamente las dependencias durante la publicación (es decir, asegurarse de que los fragmentos y modelos se puedan publicar automáticamente con una página si han cambiado desde la última publicación).
* Compatibilidad con fragmentos de contenido en la búsqueda de texto completo.
* La gestión/gestión de *contenido intermedio.*
* La gestión/gestión de *recursos de medios mixtos.*
* Vaciar Dispatcher para fragmentos a los que se hace referencia (si se vuelve a publicar una página que contiene un fragmento).
* Uso de la renderización basada en párrafos.

Si necesita una o más de estas funciones, (por lo general) es más fácil utilizar los Servicios avanzados predeterminados, en lugar de desarrollarlos desde cero.

## Servicio OSGi: configuración del componente Fragmento de contenido {#osgi-service-content-fragment-component-configuration}

La configuración debe estar enlazada al servicio OSGi **Configuración del componente Fragmento de contenido**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configuración de OSGi](/help/implementing/deploying/overview.md#osgi-configuration) para obtener más información.

Por ejemplo:

![Configuración de OSGi Configuración del componente de fragmento de contenido](assets/cf-component-configuration-osgi.png)

La configuración de OSGi es:

<table>
 <thead>
  <tr>
   <td>Etiqueta</td>
   <td>Configuración de OSGi<br /> </td>
   <td>Descripción</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>Tipo de medio</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>El tipo de recurso que se va a registrar; por ejemplo, <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Propiedad de referencia</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Nombre de la propiedad que contiene la referencia al fragmento; por ejemplo, <code>fragmentPath</code> o <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad de elemento(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Nombre de la propiedad que contiene los nombres de los elementos que se van a representar; por ejemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad de variación</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Nombre de la propiedad que contiene el nombre de la variación que se va a procesar; por ejemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algunas funciones, el componente deberá adherirse a las convenciones predefinidas. La siguiente tabla detalla las propiedades que debe definir el componente para cada párrafo (es decir, `jcr:paragraph` para cada instancia de componente) para que los servicios puedan detectarlos y procesarlos correctamente.

<table>
 <thead>
  <tr>
   <td>Nombre de la propiedad</td>
   <td>Descripción</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Una propiedad de cadena que define cómo se van a generar los párrafos si en <em>modo de procesamiento de elemento único</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para procesar todos los párrafos</li>
     <li><code>range</code> : para representar el intervalo de párrafos proporcionado por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Una propiedad de cadena que define el intervalo de párrafos de salida si en <em>modo de procesamiento de elemento único</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> o <code>1-3</code> o <code>1-3;6;7-8</code> o <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicador de rango</li>
       <li><code>;</code> separador de listas</li>
       <li><code>*</code> comodín</li>
     </ul>
     </li>
     <li>solo se evalúa si <code>paragraphScope</code> se establece en <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una propiedad booleana que define si los encabezados (por ejemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) se cuentan como párrafos (<code>true</code>) o no (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Ejemplos {#example}

AEM Por ejemplo, consulte lo siguiente (en una instancia de aplicación predeterminada de la interfaz de usuario de la interfaz de usuario de la aplicación de configuración de la aplicación de configuración de la aplicación de configuración de la aplicación):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contiene lo siguiente:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
