---
title: Eventos del editor universal
description: Obtenga información sobre los diferentes eventos que envía el editor universal y que puede utilizar para reaccionar ante los cambios de contenido o de interfaz de usuario en la aplicación remota.
exl-id: c9f7c284-f378-4725-a4e6-e4799f0f8175
feature: Developing
role: Admin, Architect, Developer
source-git-commit: fefbb01c786cc00a31602c4646ca8b015e16ed98
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 2%

---

# Eventos del editor universal {#events}

Obtenga información sobre los diferentes eventos que envía el editor universal y que puede utilizar para reaccionar ante los cambios de contenido o de interfaz de usuario en la aplicación remota.

## Introducción {#introduction}

Las aplicaciones pueden tener diferentes requisitos para las actualizaciones de páginas o componentes. Por lo tanto, el editor universal envía eventos definidos a aplicaciones remotas. Si la aplicación remota no tiene un detector de eventos personalizado para el evento enviado, se ejecuta un [detector de eventos de reserva](#fallback-listeners) proporcionado por el paquete `universal-editor-cors`.

Todos los eventos se invocan en el elemento DOM afectado de la página remota. Los eventos se propagan al elemento `BODY` donde está registrado el detector de eventos predeterminado proporcionado por el paquete `universal-editor-cors`. Hay eventos para el contenido y eventos para la interfaz de usuario.

Todos los eventos siguen una convención de nombres.

* `aue:<content-or-ui>-<event-name>`

Por ejemplo, `aue:content-update` y `aue:ui-select`

Los eventos incluyen la carga útil de la solicitud y la respuesta y se activan una vez que la llamada correspondiente se realiza correctamente. Para obtener más información acerca de las llamadas y ejemplos de sus cargas útiles, consulte el documento [Llamadas al editor universal](/help/implementing/universal-editor/calls.md).

## Eventos de actualización de contenido {#content-events}

### aue:content-add {#content-add}

El evento `aue:content-add` se activa cuando se agrega un nuevo componente a un contenedor.

La carga útil es contenido del servicio Editor universal, con contenido de reserva de la definición del componente.

```json
{
    details: {
        request: request payload;   // what is sent to the service
        response: {                 // what is returned by the service
            resource: string;       // newly created content resource
            updates: [{
                resource: string;   // resource to update
                type: string;       // type of instrumentation
                content?: string;   // content to replace
            }]
        }
    }
}
```

### aue:content-details {#content-details}

El evento `aue:content-details` se activa cuando se carga un componente en el panel de propiedades.

La carga útil es el contenido del componente y, opcionalmente, su esquema.

```json
{
    details: {
        content: object             // content object
        model: [object]             // model object
        request: request payload;   // what is sent to the service
        response: response payload; // what is returned by the service
    }
}
```

### aue:mover contenido {#content-move}

El evento `aue:content-move` se activa cuando se mueve un componente.

La carga útil es el componente, el contenedor de origen y el contenedor de destino.

```json
{
    details: {
        from: string;                   // container we move the component from
        component: string;              // component we move
        to: string;                     // container we move the component to
        before: string;                    // before which component shall we place the component
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-patch {#content-patch}

El evento `aue:content-patch` se activa cuando los datos de un componente se actualizan en el panel de propiedades.

La carga útil es un parche JSON de las propiedades actualizadas.

```json
{
    details: {
        patch: {
            name: string;               // attribute which is updated
            value: string;              // new value which is stored to the attribute
        },
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:eliminar contenido {#content-remove}

El evento `aue:content-remove` se activa cuando se quita un componente de un contenedor.

La carga útil es el ID del elemento del componente eliminado.

```json
{
    details: {
        resource: string;               // the resource which got removed
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service
    }
}
```

### aue:content-update {#content-update}

El evento `aue:content-update` se activa cuando las propiedades de un componente se actualizan en contexto.

La carga útil es el valor actualizado.

```json
{
    details: {
        value: string;                  // updated value
        request: request payload;       // what is sent to the service
        response: response payload;     // what is returned by the service 
    }
}
```

### Paso de cargas {#passing-payloads}

Para todos los eventos de actualización de contenido, la carga útil solicitada, así como la carga útil de respuesta, se pasan al evento. Por ejemplo, para una llamada de actualización:

Solicitar carga útil:

```json
{
  "connections": [
    {
      "name": "aemconnection",
      "protocol": "aem",
      "uri": "https://author-p7452-e12433.adobeaemcloud.com"
    }
  ],
  "target": {
    "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
    "type": "text",
    "prop": "title"
  },
  "value": "Alhoa Spirit Northern Norway!"
}
```

Carga de respuesta

```json
{
    "updates": [
        {
            "resource": "urn:aemconnection:/content/dam/wknd-shared/en/magazine/arctic-surfing/aloha-spirits-in-northern-norway/jcr:content/data/master",
            "prop": "title",
            "type": "text"
        }
    ]
}
```

## Eventos de IU {#ui-events}

### aue:ui-preview {#ui-preview}

El evento `aue:ui-preview` se activa cuando el modo de edición de la página se cambia a **Vista previa**.

La carga útil está vacía para este evento.

```json
{
    details: {}
}
```

### aue:ui-edit {#ui-edit}

El evento `aue:ui-edit` se activa cuando el modo de edición de la página se cambia a **Editar**.

La carga útil está vacía para este evento.

```json
{
    details: {}
}
```

### aue:ui-viewport-change {#ui-viewport-change}

El evento `aue:ui-viewport-change` se activa cuando se cambia el tamaño de la ventanilla móvil.

La carga útil son las dimensiones de la ventanilla móvil.

```json
{
    details: {
        height: number?;        // height of the viewport. Undefined when fullscreen
        width: number?;         // width of the viewport. Undefined when fullscreen
    }
}
```

### aue:inicializado {#initialized}

El evento `aue:initialized` se activa para informar a la página remota de que se ha cargado correctamente en el editor universal.

La carga útil está vacía para este evento.

```json
{
    details: {}
}
```

## Escuchadores de eventos de reserva {#fallback-listeners}

### Actualizaciones de contenido {#content-update-fallbacks}

| Evento | Comportamiento |
|---|---|
| `aue:content-add` | Recarga de página |
| `aue:content-details` | No hacer nada |
| `aue:content-move` | Mover el contenido o la estructura del componente al área de destino |
| `aue:content-patch` | Recarga de página |
| `aue:content-remove` | Eliminación del elemento DOM |
| `aue:content-update` | Actualizar `innerHTML` con la carga útil |

### Eventos de IU {#ui-event-fallbacks}

| Evento | Comportamiento |
|---|---|
| `aue:ui-select` | Desplazarse al elemento seleccionado |
| `aue:ui-preview` | Agregar `class="adobe-ue-preview"` a la etiqueta de HTML |
| `aue:ui-edit` | Agregar `class=adobe-ue-edit"` a la etiqueta de HTML |
| `aue:ui-viewport-change` | No hacer nada |
| `aue:initialized` | No hacer nada |

## Recursos adicionales {#additional-resources}

* [Llamadas del editor universal](/help/implementing/universal-editor/calls.md)

