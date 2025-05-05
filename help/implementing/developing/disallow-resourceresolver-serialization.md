---
title: No permitir la serialización de ResourceResolvers mediante el exportador de modelos Sling
description: No permitir la serialización de ResourceResolvers mediante el exportador de modelos Sling
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 5%

---

# No permitir la serialización de ResourceResolvers mediante el exportador de modelos Sling {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

La función Exportador de modelos Sling permite serializar objetos del modelo Sling en formato JSON. SPA AEM Esta función se utiliza ampliamente, ya que permite a los usuarios de (aplicaciones de una sola página) acceder fácilmente a los datos de los usuarios de la página de inicio de sesión de la página de la página de inicio de sesión. En el lado de la implementación, se utiliza la biblioteca Jackson Databind para serializar estos objetos.

La serialización es una operación recursiva. Partiendo de un &quot;objeto raíz&quot;, se repite recursivamente a través de todos los objetos aptos y los serializa a ellos y a sus elementos secundarios. Puede encontrar una descripción de los campos que se serializan en el artículo [Jackson - Decidir qué campos se serializan/deserializan](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

Este método serializa todos los tipos de objetos en JSON. Naturalmente, también puede serializar un objeto Sling `ResourceResolver` si está cubierto por las reglas de serialización. Esto resulta problemático, ya que el servicio `ResourceResolver` (y, por lo tanto, también el objeto de servicio que lo representa) contiene información potencialmente confidencial, que no debería revelarse. Por ejemplo:

* El ID de usuario
* Las rutas de búsqueda para resolver las rutas relativas
* El `propertyMap`

Especialmente importante es `propertyMap` (consulte la documentación de la API de [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)), ya que es una estructura de datos interna que se puede usar para muchos fines, por ejemplo, para almacenar en caché objetos que comparten el mismo ciclo de vida que `ResourceResolver`. La serialización de estos datos puede filtrar detalles de implementación y tener un impacto potencial en la seguridad, ya que se exponen datos que no deben ser legibles y accesibles para un usuario final. Por ese motivo `ResourceResolvers` no debe serializarse en JSON.

Adobe planea deshabilitar la serialización de `ResourceResolvers` en un enfoque de dos pasos:

1. A partir del 14697 de la versión de AEM as a Cloud Service AEM, cada vez que se serialice un `ResourceResolver`, el usuario registrará un mensaje de advertencia. Se recomienda a todos los clientes que comprueben los registros de sus aplicaciones para ver si hay estas instrucciones de registro y adapten el código base en consecuencia.
1. En un momento posterior, el Adobe deshabilitará la serialización de `ResourceResolver` como JSON.

## Implementación {#implementation}

El mensaje ADVERTENCIA se registra tanto en AEM as a Cloud Service AEM como en instancias locales de SDK, y tiene el siguiente aspecto:

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

Este mensaje de registro significa que durante el proceso de serialización de `/content/…/page` en JSON, `ResourceResolver` ya se ha serializado. Al solicitar `/content/../page.model.json`, puede comprobar dónde se muestran exactamente los campos de `ResourceResolver` y utilizarlos para identificar la clase del modelo Sling que activa este comportamiento.


>[!NOTE]
>
>AEM Se ha validado que [componentes principales de la lista de &lbrace;0](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/introduction) no se ven afectados por este problema.

## Acción solicitada {#requested-action}

Adobe solicita a todos los clientes que comprueben sus registros de aplicaciones y bases de código para ver si se ven afectados por este problema y cambien la aplicación personalizada donde sea necesario, de modo que este mensaje de advertencia ya no aparezca en los registros.

Se da por hecho que, en la mayoría de los casos, estos cambios necesarios son directos. Los objetos `ResourceResolver` no son necesarios en la salida JSON, ya que la información que contienen normalmente no es necesaria para las aplicaciones de front-end, lo que significa que en la mayoría de los casos debería ser suficiente para excluir el objeto `ResourceResolver` de que Jackson lo considere (consulte las [reglas](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)).

Si este problema afecta a un modelo Sling pero no se cambia, la deshabilitación explícita de la serialización del objeto `ResourceResolver` (tal como lo ejecuta el Adobe como segundo paso) aplicará un cambio en la salida JSON.
