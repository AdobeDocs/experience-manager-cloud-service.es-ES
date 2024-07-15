---
title: Uso de los adaptadores de Sling
description: Sling ofrece un patrón de adaptador para traducir convenientemente los objetos que implementan la interfaz adaptable
exl-id: 8ffe3bbd-01fe-44c2-bf60-7a4d25a6ba2b
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 3%

---

# Uso de los adaptadores de Sling {#using-sling-adapters}

[Sling](https://sling.apache.org) ofrece un [patrón de adaptador](https://sling.apache.org/documentation/the-sling-engine/adapters.html) para traducir convenientemente los objetos que implementan la interfaz [adaptable](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29). Esta interfaz proporciona un método [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) genérico que traduce el objeto al tipo de clase que se pasa como argumento.

Por ejemplo, para traducir un objeto Resource al objeto Node correspondiente, simplemente puede hacer lo siguiente:

```java
Node node = resource.adaptTo(Node.class);
```

## Casos de uso {#use-cases}

Hay los siguientes casos de uso:

* Obtenga objetos específicos de la implementación.

  Por ejemplo, una implementación basada en JCR de la interfaz genérica [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) proporciona acceso al JCR subyacente [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html).

* Creación de acceso directo de objetos que requieren que se pasen objetos de contexto interno.

  Por ejemplo, [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) basado en JCR contiene una referencia a [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html) de la solicitud, que a su vez es necesaria para muchos objetos que funcionan según esa sesión de solicitud, como [`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html) o [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html).

* Acceso directo a servicios.

  Un caso poco frecuente: `sling.getService()` es también sencillo.

### Valor devuelto nulo {#null-return-value}

`adaptTo()` puede devolver un valor nulo.

Existen varias razones para la devolución nula, entre ellas las siguientes:

* la implementación no admite el tipo de destinatario
* un fabricante de adaptadores que gestione este caso no está activo (por ejemplo, debido a la falta de referencias de servicio)
* error de condición interna
* el servicio no está disponible

Es importante que gestione correctamente el caso nulo. En el caso de las representaciones jsp, puede ser aceptable que jsp falle si el resultado es un fragmento de contenido vacío.

### Almacenamiento en caché {#caching}

Para mejorar el rendimiento, las implementaciones pueden almacenar en caché el objeto devuelto por una llamada a `obj.adaptTo()`. Si `obj` es el mismo, el objeto devuelto es el mismo.

Este almacenamiento en caché se realiza para todos los casos basados en `AdapterFactory`.

Sin embargo, no hay una regla general: el objeto podría ser una instancia nueva o una existente. Como tal, significa que no puede confiar en ninguno de los comportamientos. Por lo tanto, es importante, especialmente dentro de `AdapterFactory`, que los objetos se puedan reutilizar en este escenario.

### Funcionamiento {#how-it-works}

Hay varias maneras de implementar `Adaptable.adaptTo()`:

* Por el propio objeto; implementando el método en sí y asignándolo a determinados objetos.
* Por un [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html), que puede asignar objetos arbitrarios.

  Los objetos aún deben implementar la interfaz `Adaptable` y deben extender [`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/adapter/SlingAdaptable.html) (que pasa la llamada `adaptTo` a un administrador de adaptadores central).

  Este método permite vínculos en el mecanismo `adaptTo` para clases existentes, como `Resource`.

* Una combinación de ambos.

En el primer caso, los documentos de Java™ pueden indicar qué `adaptTo-targets` son posibles. Sin embargo, para subclases específicas como el recurso basado en JCR, esta instrucción no suele ser posible. En este último caso, las implementaciones de `AdapterFactory` suelen formar parte de las clases privadas de un paquete y, por lo tanto, no se exponen en una API de cliente ni se enumeran en documentos de Java™. En teoría, es posible acceder a todas las implementaciones de `AdapterFactory` desde el tiempo de ejecución del servicio [OSGi](/help/implementing/deploying/configuring-osgi.md) y ver sus configuraciones &quot;adaptables&quot; (fuentes y destinos), pero no asignarlas entre sí. Al final, depende de la lógica interna, que debe documentarse. De ahí esta referencia.

## Referencia {#reference}

### Sling {#sling}

[**El recurso**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Si es un recurso basado en nodos JCR o una propiedad JCR, que hace referencia a un nodo</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Property.html">Propiedad</a></td>
   <td>Si es un recurso basado en propiedades JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Item.html">Elemento</a></td>
   <td>Si es un recurso basado en JCR (nodo o propiedad)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Asignar</a></td>
   <td>Devuelve un mapa de las propiedades, si es un recurso basado en nodos JCR (u otro recurso que admita asignaciones de valores)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>Devuelve un mapa práctico de las propiedades, si es un recurso basado en nodos JCR (u otro recurso que admita asignaciones de valores). También se puede lograr (de manera más sencilla) utilizando <br /> <code><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> (controla mayúsculas y minúsculas nulas, etc.)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>Extensión de <a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> que permite contabilizar la jerarquía de recursos al buscar propiedades</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModillableValueMap</a></td>
   <td>Extensión de <a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>, que permite modificar las propiedades de ese nodo</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>Devuelve el contenido binario de un recurso de archivo (si es un recurso basado en nodos JCR y el tipo de nodo es <code>nt:file</code> o <code>nt:resource</code>; si es un recurso de paquete; contenido de archivo, si es un recurso del sistema de archivos). O bien, devuelve los datos de un recurso de propiedad JCR binario.</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>Devuelve una URL al recurso (URL del repositorio de este nodo si es un recurso basado en nodos JCR; URL del paquete jar si es un recurso del paquete; URL del archivo si es un recurso del sistema de archivos)</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">Archivo</a></td>
   <td>Si es un recurso del sistema de archivos</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>Si el recurso es una secuencia de comandos (por ejemplo, un archivo jsp) para la que se ha registrado un motor de secuencias de comandos con sling</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">Servlet</a></td>
   <td>Si el recurso es una secuencia de comandos (por ejemplo, un archivo jsp) para la que un motor de secuencias de comandos está registrado con sling o si es un recurso de servlet</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Double</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>Devuelve los valores si es un recurso basado en la propiedad JCR (y el valor se ajusta)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">EtiquetadoRecurso</a></td>
   <td>Si es un recurso basado en nodos JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html">Página</a></td>
   <td>Si es un recurso basado en nodos JCR y el nodo es un <code>cq:Page</code> (o <code>cq:PseudoPage</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html">Componente</a></td>
   <td>Si es un recurso de nodo <code>cq:Component</code></td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Design.html">Diseño</a></td>
   <td>Si es un nodo de diseño (<code>cq:Page</code>)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html">Plantilla</a></td>
   <td>Si es un recurso de nodo <code>cq:Template</code></td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">Modelo</a></td>
   <td>Si es un recurso de nodo <code>cq:Template</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Asset.html">Recurso</a></td>
   <td>Si es un recurso dam:Asset node</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/Rendition.html">Representación</a></td>
   <td>Si es una representación dam:Asset (nt:file bajo la carpeta de representación de una dam:Assert)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/Tag.html">Etiqueta</a></td>
   <td>Si es un recurso de nodo <code>cq:Tag</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>Se basa en la sesión JCR si es un recurso basado en JCR y el usuario tiene permisos para acceder a UserManager</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Con autorización</a></td>
   <td>El autorizable es la interfaz base común para usuarios y grupos</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuario</a></td>
   <td>El usuario es un autorizable especial que puede autenticarse y suplantarse</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>Realiza búsquedas debajo del recurso (o utiliza setSearchIn()) si es un recurso basado en JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>Estado del flujo de trabajo para la página o el nodo de carga útil del flujo de trabajo dado</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>Estado de replicación para el recurso determinado o su subnodo jcr:content (comprobado primero)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>Devuelve un recurso de conector adaptado para ciertos tipos, si es un recurso basado en nodos JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">Configuración</a></td>
   <td>Si es un recurso de nodo <code>cq:ContentSyncConfig</code></td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>Si está por debajo de un recurso de nodo <code>cq:ContentSyncConfig</code></td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/ResourceResolver.html) se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>La sesión JCR de la solicitud, si es una resolución de recursos basada en JCR (valor predeterminado)</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>En función de la sesión JCR, si es una resolución de recursos basada en JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>En función de la sesión JCR, si es una resolución de recursos basada en JCR</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager proporciona acceso a objetos autorizables y medios para mantenerlos, es decir, usuarios y grupos. UserManager está enlazado a una sesión en particular
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Autorizable</a> </td>
   <td>El usuario actual</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/jackrabbit/api/security/user/User.html">Usuario</a><br /> </td>
   <td>El usuario actual</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html">Externalizador</a></td>
   <td>Para externalizar direcciones URL absolutas, incluso sin el objeto de solicitud <br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) se adapta a:

Aún no hay destinos, pero implementa Adaptable y podría utilizarse como origen en un AdapterFactory personalizado.

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ControladorContenido</a><br /> (XML)</td>
   <td>Si es una respuesta de reescritura de sling</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[Página](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Page.html)** se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>Recurso de la página.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">EtiquetadoRecurso</a></td>
   <td>Recurso etiquetado (==).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo de la página.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Todo a lo que se puede adaptar el recurso de la página.</td>
  </tr>
 </tbody>
</table>

**[El componente](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/components/Component.html)** se adapta a:

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso del componente. |
|---|---|
| [RecursoEtiquetado](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html) | Recurso etiquetado (==). |
| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del componente. |
| ... | Todo a lo que se puede adaptar el recurso del componente. |

**[Plantilla](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/api/Template.html)** se adapta a:

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html">Recurso</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>Recurso de la plantilla.</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/LabeledResource.html">EtiquetadoRecurso</a></td>
   <td>Recurso etiquetado (==).</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html">Nodo</a></td>
   <td>Nodo de esta plantilla.</td>
  </tr>
  <tr>
   <td>...</td>
   <td>Todo a lo que se puede adaptar el recurso de la plantilla.</td>
  </tr>
 </tbody>
</table>

#### Seguridad {#security}

**Autorizable**, **Usuario** y **Grupo** se adaptan a:

| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Devuelve el nodo principal del usuario/grupo. |
|---|---|
| [EstadoDeReplicación](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/replication/ReplicationStatus.html) | Devuelve el estado de replicación del nodo principal del usuario/grupo. |

#### DAM  {#dam}

**El recurso** se adapta a:

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso del recurso. |
|---|---|
| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo del recurso. |
| ... | Todo a lo que se puede adaptar el recurso del recurso. |

#### Etiquetado {#tagging}

**Etiqueta** se adapta a:

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) | Recurso de la etiqueta. |
|---|---|
| [Nodo](https://developer.adobe.com/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/Node.html) | Nodo de la etiqueta. |
| ... | Todo a lo que se puede adaptar el recurso de la etiqueta. |

#### Otro {#other}

Además, Sling/JCR/OCM también proporciona [`AdapterFactory`](https://sling.apache.org/documentation/the-sling-engine/adapters.html) para los objetos OCM personalizados ([Asignación de contenido de objeto](https://jackrabbit.apache.org/jcr/object-content-mapping.html)).
