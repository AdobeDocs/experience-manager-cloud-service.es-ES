---
title: Implementar el código
description: Obtenga información sobre cómo implementar su código mediante canalizaciones de Cloud Manager en AEM as a Cloud Service.
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 14395cf97b23896e929e215e7e0b9e33620637eb
workflow-type: tm+mt
source-wordcount: '1221'
ht-degree: 97%

---


# Implementar el código {#deploy-your-code}

Obtenga información sobre cómo implementar su código en Producción mediante canalizaciones de Cloud Manager en AEM as a Cloud Service.

![Diagrama de la canalización de producción](./assets/configure-pipeline/production-pipeline-diagram.png)

La implementación del código en Fase y hasta Producción se realiza mediante una canalización de producción. La ejecución de la canalización de producción se divide en dos fases lógicas.

1. Implementación en el entorno de ensayo
   * El código se crea e implementa en el entorno de ensayo para pruebas funcionales automatizadas, pruebas de interfaz de usuario, auditoría de experiencias y pruebas de aceptación de usuarios (UAT).
1. Implementación en el entorno de producción
   * Una vez validada la generación en Fase y aprobada para su promoción en Production, el mismo artefacto de generación se implementa en el entorno Production.

_Solo el tipo de canalización de código de pila completa admite la digitalización de código, las pruebas de funciones, las pruebas de interfaz de usuario y la auditoría de experiencias._

## Implementar el código con Cloud Manager en AEM as a Cloud Service {#deploying-code-with-cloud-manager}

[Una vez configurada la canalización de producción](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) incluido repositorio, entorno y entorno de pruebas, estará listo para implementar el código.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desee implementar el código.

1. Haga clic en **Implementar** en la llamada a la acción en la pantalla **Información general** para iniciar el proceso de implementación.

   ![CTA](assets/deploy-code1.png)

1. Se mostrará la pantalla **Ejecutar canalización**. Haga clic en **Generar** para iniciar el proceso.

   ![Pantalla Ejecutar canalización](assets/deploy-code2.png)

El proceso de generación implementa el código en tres fases.

1. [Fase de implementación](#stage-deployment)
1. [Fase de prueba](#stage-testing)
1. [Implementación de producción](#production-deployment)

>[!TIP]
>
>Puede revisar los pasos de varios procesos de implementación si consulta los registros o revisa los resultados de los criterios de prueba.

## Fase de implementación {#stage-deployment}

La fase **Implementación de fase** fase consiste en estos pasos.

* **Validación**: Este paso garantiza que la canalización esté configurada para utilizar los recursos disponibles actualmente. por ejemplo, probar que la rama configurada existe y que los entornos están disponibles.
* **Prueba de generación y unidad**: Este paso ejecuta un proceso de generación en contenedores.
   * Consulte el documento [Generar detalles del entorno](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) para obtener más información sobre el entorno de generación.
* **Escanear código**: Este paso evalúa la calidad del código de la aplicación.
   * Consulte el documento [Probar la calidad del código](/help/implementing/cloud-manager/code-quality-testing.md) para obtener más información sobre el proceso de prueba.
* **Crear imágenes**: Este proceso es responsable de transformar el contenido y los paquetes de Dispatcher producidos por el paso de generación en imágenes Docker y configuraciones de Kubernetes.
* **Implementar en fase**: La imagen se implementa en el entorno de ensayo como preparación para la [Fase de prueba.](#stage-testing)

![Fase de implementación](assets/stage-deployment.png)

## Fase de prueba {#stage-testing}

La fase de **prueba** incluye los siguientes pasos.

* **Prueba funcional del producto**: la canalización de Cloud Manager ejecuta pruebas que se ejecutan en el entorno de ensayo.
   * Consulte el documento [Prueba funcional del producto](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) para obtener más información.

* **Pruebas funcionales personalizadas**: Este paso en la canalización siempre se ejecuta y no se puede omitir. Si la generación no produce JAR de prueba, la prueba se aprueba de forma predeterminada.
   * Consulte el documento [Pruebas funcionales personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) para obtener más información.

* **Pruebas de IU personalizadas**: Este paso es una característica opcional que ejecuta automáticamente las pruebas de IU creadas para aplicaciones personalizadas.
   * Las pruebas de interfaz de usuario son pruebas basadas en Selenium empaquetadas en una imagen Docker para permitir una amplia variedad de lenguajes y marcos de trabajo (como Java y Maven, Node y WebDriver.io, o cualquier otro marco de trabajo y tecnología creados en Selenium).
   * Consulte el documento [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) para obtener más información.

* **Auditoría de experiencias**: Este paso en la canalización siempre se ejecuta y no se puede omitir. A medida que se ejecuta una canalización de producción, se incluye un paso de auditoría de experiencias después de realizar pruebas funcionales personalizadas que ejecutarán las comprobaciones.
   * Las páginas configuradas se envían al servicio y se evalúan.
   * Los resultados son informativos y muestran las puntuaciones y el cambio entre la puntuación actual y la anterior.
   * Esta perspectiva es importante para determinar si hay una regresión que se introducirá con la implementación actual.
   * Consulte el documento [Comprender los resultados de la auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

![Fase de prueba](assets/stage-testing.png)

## Fase de implementación de producción {#deployment-production}

El proceso de implementación en topologías de producción difiere ligeramente para minimizar el impacto de los visitantes de un sitio AEM.

Las implementaciones de producción suelen seguir los mismos pasos que se describieron anteriormente, pero de forma gradual.

1. Implementar paquetes de AEM para crear.
1. Desasocie dispatcher1 del equilibrador de carga.
1. Implemente paquetes de AEM para publish1 y el paquete de Dispatcher para dispatcher1, vacíe la memoria caché de Dispatcher.
1. Vuelva a colocar dispatcher1 en el equilibrador de carga.
1. Una vez que dispatcher1 vuelva a estar en servicio, desasocie dispatcher2 del equilibrador de carga.
1. Implemente paquetes de AEM para publish2 y el paquete de Dispatcher para dispatcher2, vacíe la memoria caché de Dispatcher.
1. Vuelva a colocar dispatcher2 en el equilibrador de carga.

Este proceso continúa hasta que la implementación haya llegado a todos los editores y distribuidores de la topología.

![Fase de implementación de producción](assets/production-deployment.png)

## Tiempos de espera {#timeouts}

Los siguientes pasos agotarán el tiempo de espera si se deja a la espera de los comentarios del usuario:

| Paso | Tiempo de espera |
|--- |--- |
| Prueba de calidad del código | 14 días |
| Pruebas de seguridad | 14 días |
| Pruebas de rendimiento | 14 días |
| Solicitud de aprobación | 14 días |
| Programar implementación de producción | 14 días |
| Compatibilidad con CSE | 14 días |

## Proceso de implementación {#deployment-process}

Todas las implementaciones de Cloud Service siguen un proceso gradual para garantizar que no haya tiempo de espera. Consulte el documento [Funcionamiento de las implementaciones móviles](/help/implementing/deploying/overview.md#how-rolling-deployments-work) para obtener más información.

>[!NOTE]
>
>La caché de Dispatcher se borra en cada implementación. Posteriormente se calienta antes de que los nuevos nodos de publicación acepten el tráfico.

## Volver a ejecutar una implementación de producción {#Reexecute-Deployment}

Se puede volver a ejecutar el paso de implementación de producción en ejecuciones en las que se haya completado el paso de implementación de producción. El tipo de finalización no es importante: la implementación podría cancelarse o no tener éxito. Dicho esto, se espera que el caso de uso principal sean los casos en los que el paso de implementación de producción haya fallado por motivos transitorios. Volverla a ejecutar creará una nueva ejecución con la misma canalización. Esta nueva ejecución consta de tres pasos:

1. El paso de validación: es esencialmente la misma validación que se produce durante la ejecución normal de una canalización.
1. El paso de generación: en el contexto de una nueva ejecución, el paso de generación es copiar artefactos, no ejecutar realmente un proceso nuevo.
1. El paso de implementación de producción: utiliza la misma configuración y opciones que el paso de implementación de producción en una ejecución de canalización normal.

El paso de generación puede tener una etiqueta diferente en la interfaz de usuario para reflejar que está copiando artefactos, no reconstruyéndolos.

![Volver a implementar](assets/Re-deploy.png)

Restricciones:

* Volver a ejecutar el paso de implementación de producción solo será posible en la última ejecución.
* Volver a ejecutarlo no será posible para las ejecuciones de actualización push. Si la última ejecución es una ejecución de actualización push, no será posible volver a ejecutarla.
* Si la última ejecución es una ejecución de actualización push, no será posible volver a ejecutarla.
* Si la última ejecución ha fallado en cualquier momento antes del paso de implementación de producción, no será posible volver a ejecutarla.

### Volver a ejecutar la API {#Reexecute-API}

### Identificación de una ejecución que se ha vuelto a ejecutar

Para identificar si una ejecución se ha vuelto a ejecutar, se puede examinar el campo del activador. Su valor será *RE_EXECUTE*.

### Activar una ejecución nueva 

Para activar una ejecución nueva, se debe realizar una petición PUT al vínculo HAL &lt;(<https://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> en el estado del paso de implementación de producción. Si este vínculo está presente, la ejecución se puede reiniciar desde ese paso. Si está ausente, la ejecución no se puede reiniciar desde ese paso. En la versión inicial, este vínculo solo estará presente en el paso de implementación de producción, pero las versiones futuras pueden admitir el inicio de la canalización desde otros pasos. Ejemplo:

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


La sintaxis del valor _href_ del vínculo HAL anterior no debe utilizarse como punto de referencia. El valor real siempre debe leerse desde el vínculo HAL y no generarse.

Enviar una petición *PUT* a este extremo dará como resultado una respuesta *201* si es correcta y el cuerpo de la respuesta será la representación de la nueva ejecución. Esto es similar a iniciar una ejecución normal a través de la API.
