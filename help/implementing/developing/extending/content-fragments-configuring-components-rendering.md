---
title: Fragmentos de contenido Configurar componentes para procesamiento
description: Fragmentos de contenido Configurar componentes para procesamiento
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 6%

---

# Fragmentos de contenido Configurar componentes para procesamiento{#content-fragments-configuring-components-for-rendering}

Hay varias [servicios avanzados](#definition-of-advanced-services-that-need-configuration) relacionada con la renderización de fragmentos de contenido. Para utilizar estos servicios, los tipos de recurso de dichos componentes deben darse a conocer al marco de fragmentos de contenido.

Esto se hace configurando la variable [Servicio OSGi: Configuración de componentes de fragmento de contenido](#osgi-service-content-fragment-component-configuration).

Esta información es necesaria cuando:

* Debe implementar su propio componente basado en fragmentos de contenido,
* Y debe utilizar los servicios avanzados.

Se recomienda utilizar los componentes principales.

>[!CAUTION]
>
>* **Si no necesita la variable [servicios avanzados](#definition-of-advanced-services-that-need-configuration)** a continuación, puede ignorar esta configuración.
>
>* **Al ampliar o utilizar los componentes integrados**, no se recomienda cambiar la configuración de OSGi.
>
>* **Puede escribir un componente desde cero que utilice únicamente la API de fragmentos de contenido sin servicios avanzados**. Sin embargo, en tal caso, tendrá que desarrollar su componente para que gestione el procesamiento adecuado.
>
>Por lo tanto, se recomienda utilizar los componentes principales.

## Definición de servicios avanzados que necesitan configuración {#definition-of-advanced-services-that-need-configuration}

Los servicios que requieren el registro de un componente son:

* Determinar las dependencias correctamente durante la publicación (es decir, asegurarse de que los fragmentos y modelos se puedan publicar automáticamente con una página si han cambiado desde la última publicación).
* Compatibilidad con fragmentos de contenido en la búsqueda de texto completo.
* La gestión/gestión de *contenido intermedio.*
* La gestión/gestión de *recursos de medios mixtos.*
* Vaciado de Dispatcher para fragmentos referenciados (si se vuelve a publicar una página que contiene un fragmento).
* Uso de la renderización basada en párrafos.

Si necesita una o más de estas funciones, entonces (normalmente) es más fácil utilizar los servicios avanzados predeterminados, en lugar de desarrollarlos desde cero.

## Servicio OSGi: Configuración de componentes de fragmento de contenido {#osgi-service-content-fragment-component-configuration}

La configuración debe estar enlazada al servicio OSGi **Configuración del componente de fragmento de contenido**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configuración de OSGi](/help/implementing/deploying/overview.md#osgi-configuration) para obtener más información.

Por ejemplo:

![Configuración de OSGi Configuración de componentes de fragmento de contenido](assets/cf-component-configuration-osgi.png)

La configuración OSGi es:

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
   <td>El nombre de la propiedad que contiene la referencia al fragmento; por ejemplo, <code>fragmentPath</code> o <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad Element(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>El nombre de la propiedad que contiene los nombres de los elementos que se van a procesar; por ejemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propiedad de variación</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>El nombre de la propiedad que contiene el nombre de la variación que se va a procesar; por ejemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algunas funciones, el componente deberá adherirse a convenciones predefinidas. La siguiente tabla detalla las propiedades que su componente debe definir para cada párrafo (p. ej. `jcr:paragraph` para cada instancia de componente) para que los servicios puedan detectarlos y procesarlos correctamente.

<table>
 <thead>
  <tr>
   <td>Nombre de propiedad</td>
   <td>Descripción</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Una propiedad de cadena que define cómo se deben generar los párrafos si se encuentra en <em>modo de procesamiento de un solo elemento</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para procesar todos los párrafos</li>
     <li><code>range</code> : para representar el rango de párrafos proporcionado por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Una propiedad de cadena que define el rango de párrafos que se van a generar si se encuentra en <em>modo de procesamiento de un solo elemento</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> o <code>1-3</code> o <code>1-3;6;7-8</code> o <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> indicador de intervalo</li>
       <li><code>;</code> separador de lista</li>
       <li><code>*</code> comodín</li>
     </ul>
     </li>
     <li>solo se evalúa si <code>paragraphScope</code> está configurado como <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Una propiedad booleana que define si los encabezados (por ejemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) se cuentan como párrafos (<code>true</code>) o no (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Ejemplo {#example}

Como ejemplo, consulte lo siguiente (en una instancia de AEM predeterminada):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Contiene:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
