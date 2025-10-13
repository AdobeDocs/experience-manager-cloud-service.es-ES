---
title: Crear un objeto de posible cliente de Salesforce mediante integración de API
description: Obtenga información sobre cómo crear un objeto de posible cliente de Salesforce mediante la integración de API.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: al integrar la API en el editor de reglas, invoque las mejoras del servicio
exl-id: 55835ffe-1b77-449b-b76d-16c0a343cf5c
hide: true
hidefromtoc: true
index: false
source-git-commit: 3a09a3fa9b8fb3dacef4c900979c4cc256551941
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 100%

---

# Crear un objeto de posible cliente de Salesforce mediante integración de API

Este caso de uso explica cómo crear un posible cliente en Salesforce mediante la integración de API. Al final del proceso, aprenderá a hacer lo siguiente:

Configurar una [aplicación conectada en Salesforce](https://help.salesforce.com/s/articleView?id=platform.ev_relay_create_connected_app.htm&type=5) para habilitar el acceso seguro a la API.

Configurar CORS (Intercambio de recursos de origen cruzado) para permitir que el código (como JavaScript) que se ejecuta en un explorador web se comunique con Salesforce desde un origen específico, añada el origen a la lista de permitidos como se muestra a continuación

![cors](assets/salesforce-cors.png)

## Configuración de aplicación conectada

En la aplicación conectada se utiliza la siguiente configuración. Puede asignar los ámbitos de OAuth según sus necesidades.
![connected-app-settings](assets/salesforce-connected-app-settings.png)

## Crear integración de API

| Nombre | Value |
|--------------------------------|------------------|
| URL de API | https://`<your-domain>`d.my.salesforce.com/services/data/v32.0/sobjects/Lead |
| ID del cliente | Específico de la aplicación conectada |
| Secreto de cliente | Específico de la aplicación conectada |
| URL de OAuth | https://login.salesforce.com/services/oauth2/authorize |
| URL de token de acceso | https://`<your-domain>`/services/oauth2/token |
| URL de token de actualización | https://`<your-domain>`/services/oauth2/token |
| Ámbito de autorización | api chatter_api full id openid refresh_token visualforce web |
| Encabezado de autorización | Portador de autorización |

![api-integration](assets/salesforce-api-integration-create-lead.png)

## Parámetros de entrada y salida

Defina los parámetros de entrada para la llamada de API y asigne los parámetros de salida mediante el siguiente json

```json
{
    "id": "00QKY000001LyJR2A0",
    "success": true
}
```

![input-output](assets/create-lead-api-integration-input-output.png)

## Crear un formulario

Cree un formulario adaptable simple con el editor universal para capturar los detalles del objeto de posible cliente como se muestra a continuación
![lead-object-form](assets/create-lead.png)

Controle el evento de clic en la casilla de verificación Crear posible cliente con el editor de reglas. Asigne los parámetros de entrada a los valores de los objetos de formulario adecuados, como se muestra a continuación. Mostrar el identificador del objeto de posible cliente recién creado en el objeto TextField `leadid`
![rule-editor](assets/create-leade-rule-editor.png)

## Prueba de la integración

- Obtener una vista previa del formulario
- Introducir algunos valores significativos
- Seleccione la casilla de verificación `Create Lead` para activar la llamada de API
- El identificador de posible cliente del objeto de posible cliente recién creado se mostrará en el campo de texto `Lead ID`.
