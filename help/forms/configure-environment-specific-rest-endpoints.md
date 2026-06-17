---
title: Configure puntos finales REST específicos del entorno para el mismo formulario adaptable | ADOBE EXPERIENCE MANAGER AS A CLOUD SERVICE
description: Aprenda a enrutar el mismo formulario adaptable a diferentes extremos de envío REST en los entornos de desarrollo, ensayo y producción sin cambiar el formulario.
feature: Adaptive Forms, Core Components
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: 40410875-96d0-4728-8cbd-b1e1dfa438c4
source-git-commit: 8d60f09ffd3912f4a14df01baccf1c368a518a91
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 3%

---


# Configure puntos finales REST específicos del entorno para el mismo formulario adaptable

Cuando se promociona un formulario adaptable de desarrollo a ensayo y a producción, este suele tener que enviarse a un extremo REST *diferente* en cada entorno, mientras que el propio formulario sigue siendo idéntico. Al codificar el extremo URL en la acción de envío del formulario, se interrumpe esto, ya que la misma URL viaja con el formulario a todos los entornos.

Este artículo describe cómo mantener un único formulario adaptable portátil y hacer que su acción [Enviar al extremo REST](/help/forms/configure-submit-action-restpoint.md) se resuelva en el extremo correcto en cada entorno. El formulario hace referencia a una configuración de REST *por nombre* en lugar de por dirección URL, y cada entorno proporciona su propio valor para esa configuración.

## Requisitos previos {#prerequisites}

* Un formulario adaptable basado en componentes principales.
* Un [contenedor de configuración](/help/implementing/developing/introduction/configurations.md) creado a través del Explorador de configuración (**Herramientas** > **General** > **Explorador de configuración**) con **Configuraciones de nube** habilitadas.
* Permiso para acceder a **Herramientas** > **Cloud Services** y, para promocionarlo, a [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) en cada entorno (o una [canalización de implementación de Cloud Manager](/help/implementing/deploying/overview.md#deploying-content-packages-via-cloud-manager-and-package-manager)).

## Crear la configuración del servicio RESTful en ensayo {#create-rest-configuration}

>[!VIDEO](https://video.tv.adobe.com/v/3492383)

En la instancia de autor de ensayo, cree la configuración con nombre a la que hace referencia el formulario. Establezca la **URL de extremo de servicio** en el extremo REST o webhook para el ensayo.

1. Vaya a **Herramientas** > **Cloud Services** > **Fuentes de datos**.

1. Seleccione su contenedor de configuración y luego seleccione **Crear**.

1. En la ficha **General**, proporcione un **Nombre** para la configuración (por ejemplo, `restTest`). Use el nombre *same* en cada entorno para que el formulario se resuelva de manera consistente después de la promoción.

1. En la ficha **Configuración de autenticación**, configure lo siguiente:

   * **Seleccionar servicio RESTful**: **Extremo de servicio**.
   * **Tipo de método**: **POST**.
   * **URL de extremo de servicio**: la URL del extremo de ensayo (por ejemplo, una URL de gancho web que use para probar los envíos de ensayo).
   * **Tipo de contenido**: por ejemplo, **Datos de formulario de varias partes**.
   * **Tipo de autenticación**: como lo requiere su extremo (por ejemplo, **Ninguno** o **Autenticación básica**).

1. Seleccione **Guardar y cerrar**.

## Apuntar el formulario adaptable al contenedor de configuración {#set-configuration-container}

>[!VIDEO](https://video.tv.adobe.com/v/3492384)

En el ensayo, asocie el formulario con el contenedor de configuración que contiene la configuración de REST.

1. En **Forms y documentos**, seleccione su formulario adaptable y abra **Propiedades**.

1. En la ficha **Básico**, establezca **Contenedor de configuración** en el contenedor que contiene la configuración del servicio RESTful (por ejemplo, `/conf/restConfigTest`).

1. Seleccione **Guardar y cerrar**.

## Configurar la acción Enviar al extremo REST {#configure-submit-action}

>[!VIDEO](https://video.tv.adobe.com/v/3492385)

En el entorno de ensayo, configure el formulario para que se envíe mediante la configuración de REST con nombre en lugar de una URL codificada. Para obtener la referencia de acción de envío completa, consulte [Configurar un formulario adaptable para la acción de envío del extremo REST](/help/forms/configure-submit-action-restpoint.md).

1. Abra el formulario adaptable para editarlo, seleccione el componente **Contenedor de guía** y abra sus propiedades **Contenedor de formulario adaptable**.

1. Abra la pestaña **Envío** y, en la lista desplegable **Enviar acción**, seleccione **Enviar al extremo REST**.

1. En **Configuración de la acción**, seleccione **Habilitar solicitud POST**.

1. Para **Seleccionar una opción**, elija **Configuración** (no **URL**).

1. Seleccione la configuración con nombre (por ejemplo, `restTest`) en la lista.

1. Seleccione **Listo**.

El formulario ahora resuelve su punto final de envío mediante la configuración con nombre en lugar de una URL fija.

## Promocionar el formulario de ensayo a producción {#promote-across-environments}

Después de configurar y probar el ensayo, mueva el mismo formulario y el contenedor de configuración a producción. Puede utilizar cualquiera de los siguientes métodos.

### Opción 1: enfoque de autor y paquete {#option-package}

>[!VIDEO](https://video.tv.adobe.com/v/3492386)

Utilícelo cuando los autores mantengan el formulario y la configuración directamente en cada entorno.

1. En la instancia de autor **staging**, cree un paquete de contenido en [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md) que incluya el formulario y su contenedor de configuración, por ejemplo:

   * `/content/dam/formsanddocuments/<your-form-path>`
   * `/content/forms/af/<your-form-path>`
   * `/conf/<your-config-container>` (que contiene `.../settings/cloudconfigs/fdm/<your-config>`)

1. Descargue el paquete e instálelo en la instancia de autor **production**.

>[!IMPORTANT]
>
>El paquete instala la misma configuración en producción, incluida la **URL del extremo de servicio** desde el ensayo. No deje esa URL de ensayo en su lugar durante la producción. Actualice el extremo en producción después de la instalación, tal como se describe en la sección siguiente.

### Opción 2: enfoque de anulación según el contexto (recomendado para la automatización) {#option-context-aware}

Utilice esto cuando desee una configuración empaquetada cuyo punto de conexión, nombre de usuario y contraseña se resuelvan automáticamente por entorno, sin edición manual después de la implementación. Este método anula las propiedades de configuración que utilizan variables de entorno de Cloud Manager.

Para las configuraciones de REST, normalmente se crean variables de entorno para las propiedades `serviceEndPoint`, `userName` y `password`, y después se hace referencia a ellas desde un archivo de configuración `OsgiConfigurationOverrideProvider` del proyecto.

Para ver el procedimiento completo, consulte [Configuraciones de nube según el contexto](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/context-aware-fdm).

## Actualizar la dirección URL del extremo en producción {#configure-endpoint-on-production}

>[!VIDEO](https://video.tv.adobe.com/v/3492387)

Después de instalar el paquete en producción, el formulario adaptable y la configuración de REST **name** (por ejemplo, `restTest`) coinciden con el ensayo. La **URL de extremo de servicio** de esa configuración aún señala al extremo de ensayo del paquete. Abra la configuración en producción y sustitúyala por la URL del punto de conexión de producción.

1. En la instancia de autor de **production**, vaya a **Herramientas** > **Cloud Services** > **Fuentes de datos**.

1. Seleccione el contenedor de configuración que ha implementado (por ejemplo, `restConfigTest`) y, a continuación, abra la configuración con nombre (por ejemplo, `restTest`).

1. En la ficha **Configuración de autenticación**, establezca **URL de extremo de servicio** en el extremo de REST o webhook de producción.

1. Seleccione **Guardar y cerrar**.

Durante la prueba, un inspector de solicitudes, como un servicio de captura de ganchos web, le proporciona una URL única por entorno para que pueda confirmar qué extremo recibe cada envío.

## Comprobar el enrutamiento {#verify}

>[!VIDEO](https://video.tv.adobe.com/v/3492388)

Envíe el mismo formulario desde ensayo y producción y confirme que cada entorno publica en su propio punto final, no en la URL del otro entorno.

1. En la instancia de autor **staging**, abra el formulario adaptable y envíelo con datos de prueba (por ejemplo, escriba `stagetest` en un campo de texto). Confirme que la solicitud de POST llega a la **URL del extremo de servicio** **de ensayo** que configuró en el ensayo.

1. En la instancia de autor **production**, abra el mismo formulario adaptable y envíelo con datos de prueba (por ejemplo, escriba `prodtest` en un campo de texto). Confirme que la solicitud POST llega a la **URL del extremo de servicio** **de producción** que configuró en producción, no a la URL de ensayo.

1. Confirme que cada solicitud utiliza el tipo de contenido esperado (por ejemplo, **Datos de formulario de varias partes**) e incluye los datos de formulario enviados. Utilice un extremo real y seguro (HTTPS) para la producción.

## Prácticas recomendadas {#best-practices}

* Use una configuración idéntica **name** en cada entorno para que el formulario se resuelva de manera consistente después de la promoción.
* Mantenga el extremo **value** específico del entorno. Nunca codificar una sola URL de entorno en la acción de envío del formulario.
* En el caso de los extremos de producción, asegúrese de que la dirección URL sea segura (HTTPS) y de que la ruta de recepción esté configurada para gestionar correctamente la petición POST para su modelo de autenticación.
* Prefiera el método de anulación según el contexto cuando desee que la implementación sea repetible y no contenga ediciones manuales posteriores a la implementación.

## Artículos relacionados {#related-articles}

* [Configurar un formulario adaptable para la acción de envío del punto final REST](/help/forms/configure-submit-action-restpoint.md)
* [Configuración de las fuentes de datos](/help/forms/configure-data-sources.md)
* [Configuraciones de nube según el contexto](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/forms/developing-for-cloud-service/context-aware-fdm)
* [Acción de envío de un formulario adaptable](/help/forms/aem-forms-submit-action.md)

