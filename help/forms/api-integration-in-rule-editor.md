---
title: API de integración en el Editor de reglas para Forms
description: Obtenga información sobre las mejoras más recientes de Invocar servicio en el Editor de reglas, incluido cómo integrar API para Forms adaptable basadas en componentes principales sin utilizar un modelo de datos de formulario.
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
keywords: al integrar la API en el editor de reglas, invoque las mejoras del servicio
exl-id: fc51f86d-e672-4513-b473-6700757a0c3d
source-git-commit: 0dba0003d8b13631e91147fa08c3b986c11b61d3
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 3%

---

# Integración de API en el editor de reglas

<span>La API de integración en el editor de reglas se encuentra en el programa de usuario anticipado. Puede escribir a `aem-forms-ea@adobe.com` desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad.</span>

>[!NOTE]
>
> El editor de reglas visuales admite la integración de API en Forms adaptable en función de componentes principales y [Edge Delivery Services Forms creado en el editor universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

El Editor de reglas visual en Forms adaptable admite la integración directa de API sin crear un modelo de datos de formulario. Puede conectarse a un extremo de API introduciendo la dirección URL de la API (en formato JSON) o importando la configuración mediante un comando cURL. Una vez integrada, la acción **Invocar servicio** se puede usar para llamar a la API.

Los campos de formulario se pueden asignar directamente a los parámetros de entrada definidos en la configuración de la API. Del mismo modo, los parámetros de salida se pueden asignar a campos de formulario mediante la opción **carga útil de evento** para la respuesta de API correspondiente.

Además, el Editor de reglas visuales le permite definir **controladores de éxito** y **controladores de errores** al invocar un servicio. Los controladores de éxito especifican las acciones que se ejecutarán después de una llamada de API correcta, mientras que los controladores de error definen cómo debe responder el formulario cuando se produce un error.

## Comparación: métodos de integración de API

| Aspecto | Integración de API con el modelo de datos de formulario (FDM) | Integración API directa (mediante *Crear integración API*) |
|--------------------------------|---------------------------------------------------------------------|-----------------------------------------------------------|
| **Propósito** | Integración de API centralizada y reutilizable en varios formularios | Integración de API rápida y específica del formulario |
| **Ubicación de instalación** | Se crean y editan en el Editor del modelo de datos de formulario (consola AEM) | Se crean y editan directamente en el editor de reglas de formularios adaptables |
| **Complejidad** | Mayor esfuerzo de instalación (requiere asignación y configuración) | Sencillo y ligero |
| **Más Adecuado Para** | Casos de uso empresariales o a gran escala con varios formularios | Formularios pequeños, prototipos o llamadas API únicas |

## Configuración de integración de API

La captura de pantalla siguiente muestra la ventana de configuración de integración de API:

![Configuración de integración de API](/help/forms/assets/api-integration-configuration.png)

### Opciones de configuración clave

**Configuración de integración de API**

* **Importar desde cURL**: configure la integración de la API pegando un comando cURL listo para usar en lugar de introducir manualmente detalles como la URL de la API, el método HTTP, los encabezados y los parámetros.
* **Nombre para mostrar**: Nombre personalizado para el servicio API.
* **URL de API**: extremo del servicio de API.
* **Seleccionar método HTTP**: método de petición HTTP utilizado para llamar a la API.
* **Tipo de contenido**: Define el formato de solicitud y respuesta.
* **Se requiere cifrado**: (Opcional) Garantiza que los datos confidenciales se cifren durante la transmisión.
* **Ejecutar en el cliente**: cuando está habilitada, la llamada de API se realiza desde el cliente (explorador) en lugar del servidor.

**Tipo de autenticación**

* **Opciones**: Ninguno, Básico, Clave de API, OAuth 2.0.

**Parámetros de entrada**

* **Cargar JSON para la entrada**: cargue un archivo JSON de muestra para rellenar automáticamente las asignaciones de entrada.
   * **Nombre**: nombre del parámetro de entrada requerido por la API.
   * **Tipo**: Tipo de datos de entrada (cadena, número, booleano, etc.).
   * **En**: ubicación del parámetro (Consulta, Encabezado o Cuerpo).
   * **Valor predeterminado**: Valor precargado si no lo proporciona el usuario.
   * **Agregar**: opción para agregar parámetros de entrada adicionales.

**Parámetros de salida**

* **Cargar JSON para la salida**: cargue una respuesta de API de ejemplo para generar automáticamente asignaciones.
   * **Name**: nombre del parámetro de salida de la respuesta de API.
   * **Tipo**: tipo de datos esperado del parámetro de salida (cadena, número, etc.).
   * **En**: Define dónde se espera el valor asignado.
   * **Agregar/Eliminar**: Agregue nuevas asignaciones o elimine las existentes.

## Caso de uso: Rellenar campos de país en un formulario de solicitud de visa

>[!VIDEO](https://video.tv.adobe.com/v/3471606/rule-editor-api-integration/?quality=12&learn=on)

**Escenario**: una agencia gubernamental proporciona un formulario de solicitud de visa en línea con los siguientes campos:

1. Nombre completo (texto)
2. Fecha de nacimiento (fecha)
3. País de ciudadanía (lista desplegable)
4. Número de pasaporte (texto)
5. País de emisión de pasaporte (lista desplegable)
6. País de destino (menú desplegable)
7. Fecha prevista de llegada (fecha)

En lugar de mantener una lista estática de países, el formulario recupera dinámicamente información del país (continente, capital, códigos Alpha ISO, etc.) mediante la **API getcountry name**:

`https://secure.geonames.org/countryInfoJSON?username=aemforms`

Esto garantiza que los solicitantes siempre vean una lista actualizada y precisa de países mientras rellenan el formulario.

### Implementación mediante la integración de API en el editor de reglas

Puede integrar una API sin crear un modelo de datos de formulario haciendo clic en el botón **Crear integración de API** del Editor de reglas.

![Crear integración de API](/help/forms/assets/create-api-integration.png)

Se ha configurado un servicio API con el nombre **getcountry** en **Configuración de integración de API** en el Editor de reglas:

![Configuración del extremo de reposo de API](/help/forms/assets/api-restendpoint.png)

* **URL de extremo de API** → `https://secure.geonames.org/countryInfoJSON?username=aemforms`
* **Método HTTP** → GET
* **Tipo de contenido** → JSON
* **Entrada** → `username` pasada como parámetro de consulta (`aemforms`).
* **Salida** → campos de respuesta como `continent`, `capital`, `countrynames`, `isoAlpha3` y `languages` están asignados a campos de formulario.

En el **Formulario de solicitud de visa**, los tres campos desplegables, **País de ciudadanía**, **País de emisión de pasaporte** y **País de destino**, están enlazados a la acción **Invocar servicio**.

Cuando se carga el formulario, **Invocar servicio** obtiene la lista de países de la API. A continuación, la respuesta se asigna para rellenar automáticamente las opciones desplegables.

Por ejemplo, cuando el usuario abre **País de ciudadanía**, la lista de países se muestra dinámicamente desde la respuesta de la API.

![invoke-service-api-integration](/help/forms/assets/invoke-service-api-integration.png)

![Salida de integración de API](/help/forms/assets/api-integration-output.png)

Del mismo modo, **País de emisión de pasaporte** y **País de destino** utilizan la misma llamada de API, lo que garantiza datos coherentes y actualizados en los tres campos.

## Implementación del mecanismo de reintento para errores de API

Cuando falla una solicitud de API, a menudo resulta útil volver a intentar la solicitud antes de informar de un error al usuario. Puede implementar un mecanismo de sondeo y reintentos escribiendo código personalizado en el archivo **function.js**.

El siguiente ejemplo muestra cómo controlar los errores de API con hasta dos intentos de reintento y un retroceso exponencial entre reintentos:

```javascript
/**
 * Handles request retries with up to 2 retry attempts
 * @param {function} requestFn - The request function to execute
 * @return {Promise} A promise that resolves with the response or rejects after all retries
 */
function retryHandler(requestFn) {
    const MAX_RETRIES = 2;
    
    /**
     * Attempts the request with retry metadata
     * @param {number} retryCount - Current retry attempt count
     * @return {Promise} The request promise
     */
    function attemptRequest(retryCount = 0) {
        // Include retry metadata if this is a retry
        const requestOptions = retryCount > 0 ? {
            headers: {
                'X-Retry': 'true',
                'X-Retry-Count': retryCount.toString(),
                'X-Retry-Time': new Date().toISOString()
            },
            body: {
                retry: true,
                retryCount: retryCount,
                timestamp: Date.now()
            }
        } : undefined;

        return requestFn(requestOptions)
            .then(function(response) {
                if (response && response.status >= 400) {
                    console.warn('Request failed with status ' + response.status);
                    throw new Error('Request failed with status ' + response.status);
                }
                return response;
            })
            .catch(function(error) {
                console.warn('Request attempt ' + (retryCount + 1) + ' failed:', error.message);
                
                // Retry if max attempts not reached
                if (retryCount < MAX_RETRIES) {
                    console.log('Retrying request, attempt ' + (retryCount + 2) + ' of ' + (MAX_RETRIES + 1));
                    
                    // Exponential backoff delay: 1s, 2s, 4s...
                    const delay = Math.pow(2, retryCount) * 1000;
                    
                    return new Promise(function(resolve) {
                        setTimeout(resolve, delay);
                    }).then(function() {
                        return attemptRequest(retryCount + 1);
                    });
                } else {
                    // All retries exhausted
                    console.error('All retry attempts failed. Final error:', error.message);
                    throw new Error('Request failed after ' + (MAX_RETRIES + 1) + ' attempts: ' + error.message);
                }
            });
    }
    
    // Start the first attempt
    return attemptRequest(0);
}
```

En el código anterior, la función **retryHandler** administra las solicitudes de API con reintentos automáticos en caso de error. Toma una función de solicitud (requestFn) e intenta la solicitud hasta dos veces, añadiendo metadatos para cada reintento.

>[!NOTE]
>
> Para ver los pasos detallados sobre cómo agregar funciones personalizadas, consulte el artículo [Introducción a las funciones personalizadas para Forms adaptable basadas en componentes principales](/help/forms/create-and-use-custom-functions.md).

## Preguntas frecuentes

* **¿Necesito crear un modelo de datos de formulario para integrar una API en un Forms adaptable?**\
  No. Con el Editor de reglas visuales, puede integrar directamente las API usando la opción **Crear integración de API** sin crear un modelo de datos de formulario. Este método es más adecuado para casos de uso ligeros o específicos de formularios.

* **¿Puedo proteger las llamadas de API realizadas desde el Editor de reglas?**\
  Sí. La configuración de integración de API proporciona opciones de autenticación como **Básico, Clave de API y OAuth 2.0**. También puede habilitar **Se requiere cifrado** para garantizar que los datos confidenciales se transmitan de manera segura.
