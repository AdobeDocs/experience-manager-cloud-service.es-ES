---
title: No permitir la serialización de ResourceResolvers mediante el exportador de modelos Sling
description: No permitir la serialización de ResourceResolvers mediante el exportador de modelos Sling
source-git-commit: 4543a4646719f8433df7589b21344433c43ab432
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# No permitir la serialización de ResourceResolvers mediante el exportador de modelos Sling {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

La función Exportador de modelos Sling permite serializar objetos de modelos Sling en formato JSON. SPA AEM Esta función se utiliza ampliamente, ya que permite a los usuarios de (aplicaciones de una sola página) acceder fácilmente a los datos de los usuarios de la página de inicio de sesión de la página de la página de inicio de sesión. En el lado de la implementación, la biblioteca Jacson Databind se utiliza para serializar estos objetos.

La serialización es una operación recursiva. Partiendo de un &quot;objeto raíz&quot;, se repite recursivamente a través de todos los objetos aptos y los serializa a ellos y a sus elementos secundarios. Puede encontrar una descripción de los campos en los que se serializan [este artículo](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Este método serializa todo tipo de objetos en JSON y, naturalmente, también puede serializar un Sling `ResourceResolver` objeto, si está cubierto por las reglas de serialización. Esto resulta problemático, ya que `ResourceResolver` El servicio (y, por lo tanto, también el objeto de servicio que lo representa) contiene información potencialmente sensible, que no debe ser revelada. Por ejemplo:

* El ID de usuario
* Las rutas de búsqueda para resolver las rutas relativas
* El `propertyMap`.

Especialmente sensible es el `propertyMap` (consulte la documentación de API de [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), ya que es una estructura de datos interna, que puede utilizarse para muchos fines, por ejemplo, para almacenar en caché objetos que comparten el mismo ciclo de vida que `ResourceResolver`. La serialización de estos datos puede filtrar detalles de implementación y tener un impacto potencial en la seguridad, ya que se exponen datos que no deberían ser legibles y accesibles para un usuario final. Por esa razón `ResourceResolvers` no se debe serializar en JSON.

Adobe planea deshabilitar la serialización de `ResourceResolvers` en un enfoque de 2 pasos:

1. AEM Comenzando por la 14697 de liberación as a Cloud Service de la, siempre que `ResourceResolver` AEM está serializado registrará un mensaje de advertencia. Se recomienda a todos los clientes que comprueben los registros de sus aplicaciones para ver si hay estas instrucciones de registro y adapten el código base en consecuencia.
1. En un momento posterior, el Adobe deshabilitará la serialización de ResourceResolvers como JSON.

## Implementación {#implementation}

AEM El mensaje ADVERTENCIA se registra tanto en instancias de SDK as a Cloud Service AEM como en instancias de SDK de la local y tiene el siguiente aspecto:

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Este mensaje de registro significa que durante el proceso de serialización del `/content/…/page` en JSON a `ResourceResolver` ya se ha serializado. Mediante solicitud `/content/../page.model.json` puede comprobar dónde están exactamente los campos del `ResourceResolver` se están mostrando y utilícelo para identificar la clase de modelo de Sling que realmente activa este comportamiento.


>[!NOTE]
>
>AEM Se ha validado que los componentes principales no se ven afectados por este problema.

## Acción solicitada {#requested-action}

Adobe solicita a todos sus clientes que comprueben los registros de sus aplicaciones y las bases de código para ver si se ven afectados por este problema y cambien la aplicación personalizada donde sea necesario, de modo que este mensaje ADVERTENCIA ya no aparezca.

Se da por hecho que, en la mayoría de los casos, estos cambios necesarios son directos, ya que `ResourceResolver` Los objetos de no son necesarios en la salida JSON, ya que la información contenida allí normalmente no es necesaria para las aplicaciones de front-end. Esto significa que, en la mayoría de los casos, debería ser suficiente excluir la `ResourceResolver` objeto de ser considerado por Jackson (consulte la [reglas](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

En caso de que un modelo Sling se vea afectado por este problema pero no se cambie, la deshabilitación explícita de la serialización del `ResourceResolver` (ejecutado por el Adobe como segundo paso) aplicará un cambio en la salida JSON.



