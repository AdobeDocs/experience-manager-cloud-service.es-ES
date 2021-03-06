---
title: API de REST
description: Screens as a Cloud Service proporciona una sencilla API RESTful que sigue la especificación Siren. Siga esta página para aprender a desplazarse por la estructura de contenido y enviar comandos a los dispositivos del entorno.
exl-id: 2c52583f-0dd9-4fa3-880b-7671442989ae
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---

# API de REST {#rest-apis}

AEM Screens proporciona una sencilla API RESTful que sigue a la [Siren](https://github.com/kevinswiber/siren) especificación. Permite desplazarse por la estructura de contenido y enviar comandos a dispositivos en el entorno.

Se puede acceder a la API desde [*http://localhost:4502/api/screens.json*](http://localhost:4502/api/screens.json).

## Desplazamiento por la estructura de contenido {#navigating-content-structure}

El JSON devuelto por las llamadas a la API enumera las entidades relacionadas con el recurso actual. Después del autovínculo enumerado, se vuelve a acceder a cada una de estas entidades como recurso REST.

Por ejemplo, para acceder a las pantallas de nuestra ubicación de señalización de demostración, puede llamar a:

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship.json HTTP/1.1
Host: http://localhost:4502
```

O utilizando curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json
```

El resultado sería el siguiente:

```xml
{
  "class": [
    "aem-io/screens/location"
  ],
  "links": [
    {
      "rel": [
        "self"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship.json"
    },
    {
      "rel": [
        "parent"
      ],
      "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo.json"
    }
  ],
  "properties": {…},
  "entities": [
    {
      "class": [
        "aem-io/screens/display"
      ],
      "links": [
        {
          "rel": [
            "self"
          ],
          "href": "http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json"
        }
      ],
      "rel": [
        "child"
      ],
      "properties": {
        "title": "Single Screen Display",
        "height": 1440,
        "description": "Demo location of a single screen display.",
        "name": "single",
        "width": 2560,
        "idletimeout": 300,
        "layoutrows": 1,
        "layoutcols": 1
      }
    },
    …
  ]
}
```

A continuación, para acceder a la visualización de una sola pantalla, puede llamar a:

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

## Ejecución de acciones en el recurso {#executing-actions-on-the-resource}

El JSON devuelto por las llamadas a la API puede contener una lista de acciones disponibles en el recurso.

La visualización, por ejemplo, enumera una *broadcast-command* acción que permite enviar un comando a todos los dispositivos asignados a esa pantalla.

```xml
GET /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502
```

O utilizando curl:

```xml
curl -u admin:admin http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```

***Resultado:***

```xml
{
  "class": [
    "aem-io/screens/display"
  ],
  "links": […],
  "properties": {…},
  "entities": […],
  "actions": [
    {
      "title": "",
      "name": "broadcast-command",
      "method": "POST",
      "href": "/api/screens/content/screens/we-retail/locations/demo/flagship/single",
      "fields": [
        {
          "name": ":operation",
          "value": "broadcast-command",
          "type": "hidden"
        },
        {
          "name": "msg",
          "type": "text"
        }
      ]
    }
  ]
}
```

Para almacenar en déclencheur esta acción, se llamaría a:

```xml
POST /api/screens/content/screens/we-retail/locations/demo/flagship/single.json HTTP/1.1
Host: http://localhost:4502

:operation=broadcast-command&msg=reboot
```

O utilizando curl:

```xml
curl -u admin:admin -X POST -d ':operation=broadcast-command&msg=reboot' http://localhost:4502/api/screens/content/screens/we-retail/locations/demo/flagship/single.json
```
