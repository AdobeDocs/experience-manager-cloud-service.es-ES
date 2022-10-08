---
title: Implementación del código
description: Obtenga información sobre cómo implementar su código mediante canalizaciones de Cloud Manager en AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 14395cf97b23896e929e215e7e0b9e33620637eb
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 2%

---


# Implementación del código {#deploy-your-code}

Obtenga información sobre cómo implementar su código en Producción mediante canalizaciones de Cloud Manager en AEM as a Cloud Service.

![Diagrama de canalización de producción](./assets/configure-pipeline/production-pipeline-diagram.png)

La implementación del código en Fase y luego hasta Producción se realiza mediante una canalización de producción. La ejecución de la canalización de producción se divide en dos fases lógicas.

1. Implementación en entorno de ensayo
   * El código se crea e implementa en el entorno de ensayo para pruebas funcionales automatizadas, pruebas de interfaz de usuario, auditoría de experiencias y pruebas de aceptación de usuarios (UAT).
1. Implementación en el entorno de producción
   * Una vez validada la compilación en Stage y aprobada para su promoción en Production, el mismo artefacto de compilación se implementa en el entorno Production.

_Solo el tipo de canalización de código de pila completa admite la digitalización de código, las pruebas de funciones, las pruebas de interfaz de usuario y la auditoría de experiencias._

## Implementación del código con Cloud Manager en AEM as a Cloud Service {#deploying-code-with-cloud-manager}

Una vez que haya [configuró la canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) incluido el repositorio, el entorno y el entorno de prueba, está listo para implementar su código.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea implementar el código.

1. Haga clic en **Implementación** de la llamada a la acción en la variable **Información general** para iniciar el proceso de implementación.

   ![CTA](assets/deploy-code1.png)

1. La variable **Ejecución de canalización** se abre. Haga clic en **Generar** para iniciar el proceso.

   ![Pantalla de ejecución de canalización](assets/deploy-code2.png)

El proceso de compilación implementa el código en tres fases.

1. [Implementación de fase](#stage-deployment)
1. [Prueba de prueba](#stage-testing)
1. [Implementación de producción](#production-deployment)

>[!TIP]
>
>Puede revisar los pasos de varios procesos de implementación consultando los registros o revisando los resultados de los criterios de prueba.

## Fase de implementación de fase {#stage-deployment}

La variable **Implementación de fase** fase. implica estos pasos.

* **Validación**  : este paso garantiza que la canalización esté configurada para utilizar los recursos disponibles actualmente. por ejemplo, probar que la rama configurada existe y que los entornos están disponibles.
* **Prueba de compilación y unidad** - Este paso ejecuta un proceso de compilación en contenedores.
   * Consulte el documento [Generar detalles del entorno](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obtener más información sobre el entorno de compilación.
* **Escaneo de código** - Este paso evalúa la calidad del código de la aplicación.
   * Consulte el documento [Prueba de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md) para obtener más información sobre el proceso de prueba.
* **Crear imágenes** - Este proceso es responsable de transformar el contenido y los paquetes de Dispatcher producidos por el paso de compilación en imágenes Docker y configuraciones de Kubernetes.
* **Implementar en fase** - La imagen se implementa en el entorno de ensayo como preparación para la [Etapa de prueba de fase.](#stage-testing)

![Implementación de fase](assets/stage-deployment.png)

## Fase de prueba de fase {#stage-testing}

La variable **Prueba de fase** incluye estos pasos.

* **Prueba funcional del producto** : la canalización de Cloud Manager ejecuta pruebas que se ejecutan en el entorno de ensayo.
   * Consulte el documento [Prueba funcional del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obtener más información.

* **Pruebas funcionales personalizadas** - Este paso en la canalización siempre se ejecuta y no se puede omitir. Si la compilación no produce JAR de prueba, la prueba pasa de forma predeterminada.
   * Consulte el documento [Pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obtener más información.

* **Pruebas de IU personalizadas** : Este paso es una función opcional que ejecuta automáticamente las pruebas de IU creadas para aplicaciones personalizadas.
   * Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de idiomas y marcos (como Java y Maven, Node y WebDriver.io, o cualquier otro marco y tecnología creados en Selenium).
   * Consulte el documento [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) para obtener más información.

* **Auditoría de experiencias** - Este paso en la canalización siempre se ejecuta y no se puede omitir. A medida que se ejecuta una canalización de producción, se incluye un paso de auditoría de experiencias después de realizar pruebas funcionales personalizadas que ejecutarán las comprobaciones.
   * Las páginas configuradas se envían al servicio y se evalúan.
   * Los resultados son informativos y muestran las puntuaciones y el cambio entre las puntuaciones actual y anterior.
   * Esta perspectiva es valiosa para determinar si hay una regresión que se introducirá con la implementación actual.
   * Consulte el documento [Comprender los resultados de la auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

![Prueba de prueba](assets/stage-testing.png)

## Fase de implementación de producción {#deployment-production}

El proceso de implementación en topologías de producción difiere ligeramente para minimizar el impacto de los visitantes en un sitio AEM.

Las implementaciones de producción suelen seguir los mismos pasos que se describieron anteriormente, pero de forma gradual.

1. Implemente AEM paquetes para crear.
1. Desasocie Dispatcher1 del equilibrador de carga.
1. Implemente AEM paquetes para publicar1 y el paquete de Dispatcher para dispatcher1, vacíe la caché de Dispatcher.
1. Vuelva a colocar Dispatcher1 en el equilibrador de carga.
1. Una vez que Dispatcher1 vuelva a estar en servicio, separe Dispatcher2 del equilibrador de carga.
1. Implemente AEM paquetes para publicar2 y el paquete de Dispatcher para dispatcher2, vacíe la caché de Dispatcher.
1. Vuelva a colocar Dispatcher2 en el equilibrador de carga.

Este proceso continúa hasta que la implementación haya llegado a todos los editores y distribuidores de la topología.

![Fase de implementación de producción](assets/production-deployment.png)

## Tiempos de espera {#timeouts}

Los siguientes pasos agotarán el tiempo de espera si se deja esperando los comentarios del usuario:

| Etapa | Tiempo de espera |
|--- |--- |
| Prueba de calidad del código | 14 días |
| Pruebas de seguridad | 14 días |
| Pruebas de rendimiento | 14 días |
| Solicitud de aprobación | 14 días |
| Programar implementación de producción | 14 días |
| Compatibilidad con CSE | 14 días |

## Proceso de implementación {#deployment-process}

Todas las implementaciones de Cloud Service siguen un proceso gradual para garantizar que no haya downtime. Consulte el documento [Cómo funcionan las implementaciones móviles](/help/implementing/deploying/overview.md#how-rolling-deployments-work) para obtener más información.

>[!NOTE]
>
>La caché de Dispatcher se borra en cada implementación. Posteriormente se calienta antes de que los nuevos nodos de publicación acepten el tráfico.

## Volver a ejecutar una implementación de producción {#Reexecute-Deployment}

La reejecución del paso de implementación de producción se admite en ejecuciones en las que se haya completado el paso de implementación de producción. El tipo de finalización no es importante: la implementación podría cancelarse o no tener éxito. Dicho esto, se espera que el caso de uso principal sean los casos en los que el paso de implementación de producción haya fallado por motivos transitorios. La reejecución crea una nueva ejecución utilizando la misma canalización. Esta nueva ejecución consta de tres pasos:

1. El paso validate : esto es esencialmente la misma validación que se produce durante la ejecución normal de una canalización.
1. El paso de compilación : en el contexto de una nueva ejecución, el paso de compilación es copiar artefactos, no ejecutar realmente un nuevo proceso de compilación.
1. El paso de implementación de producción : utiliza la misma configuración y opciones que el paso de implementación de producción en una ejecución de canalización normal.

El paso de compilación puede tener una etiqueta ligeramente diferente en la interfaz de usuario para reflejar que está copiando artefactos, no reconstruyendo.

![Volver a implementar](assets/Re-deploy.png)

Restricciones:

* La ejecución del paso de implementación de producción solo estará disponible en la última ejecución.
* La reejecución no está disponible para las ejecuciones de actualización push. Si la última ejecución es una ejecución de actualización push, no es posible la reejecución.
* Si la última ejecución es una ejecución de actualización push, no es posible la reejecución.
* Si la última ejecución ha fallado en cualquier momento antes del paso de implementación de producción, la reejecución no es posible.

### Volver a ejecutar la API {#Reexecute-API}

### Identificación de una ejecución de nueva ejecución

Para identificar si una ejecución es una ejecución de nueva ejecución, se puede examinar el campo de déclencheur. Su valor será *RE_EXECUTE*.

### Activación de una nueva ejecución

Para déclencheur de una nueva ejecución, se debe realizar una solicitud de PUT al vínculo HAL &lt;(<https://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> en el estado del paso de implementación de producción. Si este vínculo está presente, la ejecución se puede reiniciar desde ese paso. Si está ausente, la ejecución no se puede reiniciar desde ese paso. En la versión inicial, este vínculo solo estará presente en el paso de implementación de producción, pero las versiones futuras pueden admitir el inicio de la canalización desde otros pasos. Ejemplo:

```Javascript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


La sintaxis del vínculo HAL _href_  no está previsto que se utilice como punto de referencia. El valor real siempre debe leerse desde el vínculo HAL y no generarse.

Envío de un *PUT* la solicitud a este extremo dará como resultado un *201* Si la respuesta es correcta, y el cuerpo de respuesta será la representación de la nueva ejecución. Esto es similar a iniciar una ejecución normal a través de la API.
