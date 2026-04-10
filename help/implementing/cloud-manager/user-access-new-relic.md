---
title: New Relic One
description: Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 93d22e32dc2f21bddccf7ad1305aab7d22b8345a
workflow-type: tm+mt
source-wordcount: '2303'
ht-degree: 23%

---


# New Relic One {#user-access}

Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.

## Acerca de New Relic One {#introduction}

Adobe pone un gran énfasis en la monitorización, la disponibilidad y el rendimiento de su aplicación. AEM as a Cloud Service incluye acceso a la monitorización de New Relic One, lo que proporciona a los equipos una visibilidad completa de las métricas de rendimiento del sistema y del entorno como parte de la oferta de productos estándar.

Este artículo describe cómo administrar el acceso a las funciones de monitorización del rendimiento de las aplicaciones (APM) de New Relic One en entornos de AEM as a Cloud Service. La administración eficaz de estas funciones ofrece un rendimiento óptimo y maximiza las ventajas de AEM as a Cloud Service.

Cuando se crea un nuevo programa de producción, se crea automáticamente la cuenta secundaria de New Relic One asociada a su programa de AEM as a Cloud Service. [Se debe activar esta subcuenta](#activate-sub-account) para comenzar a ingerir datos.

## Características {#transaction-monitoring}

New Relic One APM para AEM as a Cloud Service tiene muchas características.

* Acceso directo a una cuenta específica de New Relic One.

* Agente de APM de New Relic One instrumentado que muestra llamadas de método exactas con números de línea, incluidas dependencias externas y bases de datos.

* Optimización del rendimiento holístico mediante la combinación de métricas clave de la monitorización a nivel de infraestructura y la monitorización de aplicaciones (Adobe Experience Manager).

* Rastreadores de cambios automáticos para ejecuciones de canalizaciones de Cloud Manager, actualizaciones de AEM y operaciones de restauración de código. Estos rastreadores permiten a los equipos correlacionar implementaciones con cambios de rendimiento de aplicaciones directamente en New Relic One.

## Activar la subcuenta de New Relic One {#activate-sub-account}

Para un programa recién creado, se crea una cuenta secundaria de New Relic One. Sin embargo, debe activarlo para que pueda introducir datos. Esta activación no es automática. Siga estos pasos para activar su subcuenta.

>[!NOTE]
>
>Un usuario con el rol **Propietario del negocio** debe iniciar sesión para administrar la subcuenta de New Relic One.

**Para activar su subcuenta de New Relic One:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
   1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
   1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee.
1. En la consola **Mis programas**, haga clic en un programa para el que desee administrar a los usuarios de New Relic One.
1. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de datos o Icono de entornos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.
1. En la página Entornos, cerca de la esquina superior derecha, haz clic en ![Más iconos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haz clic en **Activar New Relic**.

   ![Activar New Relic](/help/implementing/cloud-manager/assets/new-relic/new-relic-activate.png)

1. [Ejecute una canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines) para el mismo entorno para completar correctamente la activación de la subcuenta.

Cuando se desactiva la subcuenta, no se realiza ninguna ingesta de datos.

## Administrar usuarios de New Relic One {#manage-users}

Puede definir los usuarios de la subcuenta de New Relic One asociada a su programa de AEM as a Cloud Service.

>[!NOTE]
>
>Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** debe iniciar sesión para administrar usuarios de New Relic One.

**Para administrar usuarios de New Relic One:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
   1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
   1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee.
1. En la consola **Mis programas**, haga clic en un programa para el que desee administrar a los usuarios de New Relic One.
1. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de datos o Icono de entornos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.
1. En la página Entornos, cerca de la esquina superior derecha, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haga clic en **Administrar usuarios**.

   ![Administrar usuarios de New Relic](/help/implementing/cloud-manager/assets/new-relic/new-relic-manage-users.png)

1. En el cuadro de diálogo **Administrar usuarios de New Relic**, haga lo siguiente:

   * Introduzca el nombre y los apellidos del usuario que desea agregar
   * Introduzca la dirección de correo electrónico asociada
   * Haga clic en ![Agregar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Agregar**. Repita este paso para cada usuario que desee agregar.
   * Haga clic en ![Cerrar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) para quitar un usuario.

   ![Agregar usuarios](assets/newrelic-add-users.png)

1. Haga clic en **Guardar**.

Una vez definidos los usuarios, New Relic envía un correo electrónico de confirmación a cada uno. A partir de ahí, pueden completar el proceso de activación e iniciar sesión.

>[!NOTE]
>
>Si está administrando los usuarios de New Relic One, también debe agregarse como usuario de. Ser el **Propietario del negocio** o **Administrador de implementación** no es suficiente para tener acceso a New Relic One.

## Activar la cuenta de usuario de New Relic One {#activate-user-account}

Una vez creada una cuenta de usuario de New Relic One, tal como se describe en [Administrar usuarios de New Relic One](#manage-users), New Relic enviará a esos usuarios un correo electrónico de confirmación a la dirección proporcionada. Para utilizar esas cuentas, los usuarios deben activarlas primero con New Relic y restablecer sus contraseñas.

**Para activar su cuenta de usuario de New Relic One:**

1. Haga clic en el vínculo proporcionado en el correo electrónico desde New Relic.

1. En la página de inicio de sesión de New Relic, haga clic en **Olvidó su contraseña?**

   ![Iniciar sesión en New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Introduzca la dirección de correo electrónico donde recibió el correo de confirmación y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic le envía un correo electrónico con un vínculo para confirmar la cuenta.

Si no recibe un correo electrónico de confirmación de New Relic, consulte la [sección de solución de problemas](#troubshooting).

## Abrir New Relic One {#accessing-new-relic}

Una vez que haya [activado su cuenta de New Relic](#activate-account), puede abrir New Relic One a través de Cloud Manager o directamente.

**Para abrir New Relic One mediante Cloud Manager:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
   1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
   1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee.
1. En la consola **Mis programas**, haga clic en un programa para el que desee abrir New Relic One.
1. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de datos o Icono de entornos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.
1. En la página Entornos, cerca de la esquina superior derecha, haz clic en ![Más iconos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haz clic en **Abrir New Relic**.

   ![Abrir New Relic](/help/implementing/cloud-manager/assets/new-relic/new-relic-open-new-relic.png)

1. En la nueva pestaña del explorador que se abre, inicie sesión en New Relic One.

**Para abrir New Relic One directamente:**

1. Vaya a la [página de inicio de sesión de New Relic](https://login.newrelic.com/login).

1. Inicie sesión en New Relic One.

### Verifique su correo electrónico {#verify-email}

Si se le solicita que compruebe su correo electrónico durante el inicio de sesión en New Relic One, significa que su correo electrónico está asociado a varias cuentas. Puede elegir a qué cuenta acceder.

Si no verifica su dirección de correo electrónico, New Relic intentará iniciar sesión con el registro de usuario creado más recientemente y asociado a su dirección de correo electrónico. Para evitar verificar el correo electrónico durante cada inicio de sesión, haga clic en la casilla de verificación **Recordarme** de la pantalla de inicio de sesión.

Para obtener más ayuda, abra un ticket de asistencia a través del [Portal de asistencia de AEM](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

## Usar rastreador de cambios {#change-tracker}

Cloud Manager envía automáticamente rastreadores de cambios a New Relic One siempre que se completen las ejecuciones de canalización admitidas, las actualizaciones de AEM y la restauración de código. Estos rastreadores aparecen como eventos de cambio en la vista **Seguimiento de cambios** de New Relic, lo que permite que su equipo correlacione implementaciones con cambios en el rendimiento de las aplicaciones, las tasas de error y el rendimiento.

<!-- See also [Introduction to change tracking](https://docs.newrelic.com/docs/change-tracking/overview/) and [Record and view deployments](https://docs.newrelic.com/docs/apm/apm-ui-pages/events/record-deployments/). -->

### Canalizaciones y flujos de trabajo compatibles {#supported-pipelines}

Las siguientes canalizaciones de Cloud Manager y los dos últimos tipos de flujo de trabajo generan rastreadores de cambios en New Relic One:

| Tipo de canalización/flujo de trabajo | Descripción |
|---|---|
| **Pila completa (implementación CI_CD)** | Ejecuciones de canalización de pila completa. El seguimiento incluye el nombre de la canalización y el ID de ejecución. |
| **Configuración de nivel web** | Ejecuciones de canalización de configuración de nivel web. El seguimiento incluye el nombre de la canalización y el ID de ejecución. |
| **Front-end** | Ejecuciones de canalización front-end. El seguimiento incluye el nombre de la canalización y el ID de ejecución. |
| **Configuración** | Ejecuciones de canalización de configuración. El seguimiento incluye el nombre de la canalización y el ID de ejecución. |
| **Actualización de AEM** | Actualizaciones de la versión de AEM. Por ejemplo, de la versión {} a la versión {}. Los rastreadores se crean cuando se completa el evento de cambio de entorno. |
| **Código de restauración** | El código restaura las operaciones desde un repositorio y rama específicos. |

>[!NOTE]
>
>Actualmente, los rastreadores de cambios solo son compatibles con los entornos de Skyline. Las canalizaciones que están fuera de ámbito, como las canalizaciones de ampliación y las canalizaciones de Service Pack, no generan rastreadores.

### Visualización de rastreadores de cambios en New Relic One {#view-change-trackers}

Una vez finalizada la ejecución de una canalización admitida, puede ver el rastreador de cambios correspondiente en New Relic One.

**Para ver los rastreadores de cambios en New Relic One:**

1. [Acceder a New Relic One](#accessing-new-relic) mediante Cloud Manager o directamente.
1. Vaya a **APM y servicios** y seleccione la aplicación para el entorno correspondiente.
1. En la página de resumen de la aplicación, busque los indicadores del rastreador de cambios en el gráfico. Pase el ratón sobre un rastreador para ver los detalles de implementación.

   ![Cambiar indicadores de seguimiento en el gráfico de tiempo de transacciones web](/help/implementing/cloud-manager/assets/new-relic/new-relic-web-transactions-time.png)

1. Haga clic en cualquier evento de cambio del gráfico para abrir una vista detallada.

   ![Panel de atributos de implementación con la URL deepLink resaltada](/help/implementing/cloud-manager/assets/new-relic/new-relic-deeplink.png) <i>Vista detallada de un evento de cambio.</i>

   El panel **Cambiar detalles** de la derecha muestra, entre otras cosas, la entidad, la marca de tiempo, la época, la categoría, el ID de implementación y el tipo de API.

   Para cada rastreador de cambios que Cloud Manager envía a New Relic One, el panel **Atributos de implementación** de la parte inferior derecha muestra los siguientes atributos:

   | Atributo | Descripción |
   |---|---|
   | **versión** | Una cadena de descripción que incluye el nombre de la canalización y el ID de ejecución. |
   | **changelog** | Reservado para uso futuro. |
   | **confirmar** | Reservado para uso futuro. |
   | **vínculo profundo** | Haga clic en la URL para volver a vincular a la página de ejecución de la canalización en Cloud Manager. |

1. Para ver una lista completa de los rastreadores de cambios, en la barra lateral izquierda, bajo **Eventos**, haga clic en **Seguimiento de cambios**.

   La tabla **Cambiar eventos** muestra cada implementación con su marca de tiempo y descripción de la versión.

   ![Opción de seguimiento de cambios con tabla de eventos de cambios que muestra](/help/implementing/cloud-manager/assets/new-relic/new-relic-change-tracking.png)

>[!TIP]
>
>Utilice rastreadores de cambios junto con indicadores de rendimiento de New Relic One, como **Tiempo de respuesta** y **Rendimiento**. Estos indicadores le ayudan a identificar si una implementación en particular introdujo regresiones o mejoras de rendimiento. Puede comparar métricas de antes y después de una implementación directamente en la página de detalles del evento de cambio.

## Solucionar problemas de acceso de usuarios de New Relic One {#troubleshooting}

Si se le agregó como usuario de New Relic One, tal como se describe en [Administrar usuarios de New Relic One](#manage-users), y no puede encontrar el correo electrónico de confirmación de la cuenta original, puede realizar los siguientes pasos para solucionar problemas.

**Para solucionar problemas de acceso de usuarios de New Relic One:**

1. Navegue hasta la página de inicio de sesión de New Relic en [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Haga clic en **[!UICONTROL ¿Olvidó su contraseña?]**.

   ![Iniciar sesión en New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Escriba la dirección de correo electrónico que utilizó para crear la cuenta y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic le envía un correo electrónico con un vínculo para confirmar la cuenta.

Si completa el proceso de registro y no puede iniciar sesión en su cuenta debido a mensajes de error de correo electrónico o contraseña, registre un ticket de asistencia a través de [Admin Console](https://adminconsole.adobe.com/).

Si no recibe un correo electrónico de New Relic, haga lo siguiente:

* Compruebe sus [filtros de correo no deseado](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Si corresponde, [agregue New Relic a su lista de permitidos de correo electrónico](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Si ninguna de estas sugerencias ayuda, proporcione comentarios sobre el ticket de asistencia.

## Notas de uso {#usage-notes}

* Se puede agregar un máximo de 30 usuarios. Si se ha alcanzado el número máximo de usuarios, elimine algunos para poder añadir nuevos.
* Los usuarios agregados a New Relic son del tipo **Básico**. Consulte la [documentación de New Relic para obtener detalles](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-type/).
* AEM as a Cloud Service solo ofrece la solución de APM New Relic One y no proporciona soporte para alertas, registros o integraciones de la API.

>[!NOTE]
>
>Si no se detecta ninguna actividad **user login** en su subcuenta de New Relic One durante 30 días o más, se detendrá el agente de APM. No se envían datos de AEM Cloud Service a New Relic. *No se volverán a enviar los datos hasta que se reactive su cuenta secundaria.*
>
>Siga los mismos pasos en la sección [Activar la subcuenta de New Relic One](#activate-sub-account) de este documento para reactivar la subcuenta de New Relic One.

Para obtener más ayuda o instrucciones adicionales sobre las ofertas de New Relic One para su programa de AEM as a Cloud Service, abra un ticket de asistencia a través del [Portal de asistencia de AEM](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

## Preguntas frecuentes {#faqs}

+++**¿Qué monitoriza Adobe con New Relic One?**

Adobe monitoriza los servicios de autor, publicación y vista previa (cuando están disponibles) de AEM as a Cloud Service de a través del complemento Java de New Relic One. Adobe permite la telemetría y monitorización personalizada de APM New Relic One en entornos de AEM as a Cloud Service que sean de producción y de no producción.

La cuenta de New Relic One se adjunta a una cuenta principal mantenida por Adobe y tiene varias aplicaciones; tres por entorno de AEM as a Cloud Service.

* Una aplicación para el servicio de creación por entorno
* Una aplicación para el servicio `Publish` por entorno (incluido Golden Publish)
* Una aplicación para el servicio Vista previa por entorno

Nota:

* Cada aplicación utiliza una clave de licencia.
* Los entornos de AEM as a Cloud Service solo informan a una cuenta de New Relic One.
* Las métricas y los eventos de monitorización completos para New Relic One se conservan durante tres meses.

+++

+++**¿Adobe envía notificaciones de alerta desde New Relic One?**

Adobe proporciona acceso a New Relic One únicamente para fines de observación y no lo utiliza para alertas de cliente o alertas operativas internas. Las notificaciones de cualquier incidente se envían usando [perfiles de notificación de usuario](/help/journey-onboarding/notification-profiles.md).
+++

+++**¿Quién puede acceder a los datos del servicio en la nube de New Relic One?**

Se concede acceso de lectura completo hasta 30 miembros de su equipo. El acceso de lectura incluye todas las métricas de APM recopiladas por el agente de New Relic One.
+++

+++**¿Se admite la configuración de SSO personalizada?**

La configuración de SSO personalizada no es compatible con la cuenta de New Relic One aprovisionada por Adobe.
+++

+++**¿Qué sucede si ya tengo una suscripción a New Relic local?**

New Relic One es la nueva plataforma de observabilidad de New Relic y permite al soporte de Adobe y a sus equipos observar, monitorear y ver métricas y eventos, todo en un solo lugar.

New Relic One ofrece a los usuarios la capacidad de buscar en todas las cuentas donde tengan acceso y visualizar los datos de todos los servicios y hosts de un solo vistazo.

La compatibilidad con Adobe supervisa AEM as a Cloud Service con New Relic One y otras herramientas, mientras que sus equipos pueden seguir utilizando New Relic para servicios e infraestructura locales. Pueden visualizar los datos tanto de la cuenta de Adobe New Relic One como de las cuentas de New Relic administradas por el cliente.

>[!NOTE]
>
>Para ver ambos conjuntos de datos dentro de New Relic One, un usuario debe tener los permisos adecuados y utilizar la misma metodología de inicio de sesión para ambas cuentas (Adobe New Relic One y las cuentas de New Relic administradas por el cliente).

+++

+++**El agente de APM para mi cuenta de New Relic One está detenido. ¿Qué ha sucedido?**

[Los agentes de APM se detienen](#limitations) si no se detecta ninguna actividad durante 30 días o más. Siga los mismos pasos en la sección [Activar la subcuenta de New Relic One](#activate-sub-account) de este documento para reactivar la subcuenta de New Relic One.
+++
