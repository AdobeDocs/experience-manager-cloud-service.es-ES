---
title: Crear formulario mediante el editor universal
description: Crear un formulario adaptable para probar la lista desplegable en cascada mediante las integraciones de la API
feature: Edge Delivery Services
role: User
source-git-commit: 53e476981874597bfb7f9293e67b2d135c72b318
workflow-type: ht
source-wordcount: '202'
ht-degree: 100%

---

# Crear formulario mediante el editor universal

Cree el siguiente formulario mediante el editor universal. El formulario tiene 3 listas desplegables, cuyos valores se rellenan mediante la integración de la API
![adaptive-form](assets/address-form.png)

## País de residencia

En la inicialización, la lista desplegable del país de residencia se rellenará con los resultados de la llamada de API.
![initialize-event](assets/initialize-event.png)

## Controlador de éxito

El controlador de éxito se definió para establecer los enum y enumNames de la lista desplegable del país con los valores adecuados de la matriz geonames. La matriz geonames está disponible en la opción Carga útil de evento
![event-payload](assets/event-payload.png)
![success-handler](assets/success-handler.png)

## Recuperar valores secundarios

La lista desplegable de estado o provincia se rellena cuando el usuario realiza una selección en la lista desplegable País de residencia. El geonameId asociado con el país seleccionado se pasa como parámetro de entrada a la integración de la API GetChildren

![get-children](assets/invoke-service-get-children.png)

Se definió el controlador de éxito para establecer los enum/enumNames del campo desplegable StateOrProvince
![get-children-success-handler](assets/child-success-handler.png)

Cuando se selecciona el estado o la provincia, puede rellenar la lista desplegable de la ciudad siguiendo el patrón mencionado anteriormente utilizado para rellenar la lista desplegable del estado o la provincia.