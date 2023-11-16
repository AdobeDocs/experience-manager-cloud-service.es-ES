---
title: New Relic One
description: Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 90%

---


# New Relic One {#user-access}

Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.

## Introducción {#introduction}

Adobe pone un gran énfasis en la monitorización, la disponibilidad y el rendimiento de su aplicación. AEM as a Cloud Service proporciona acceso a un grupo de monitorización de New Relic One personalizado como parte de la oferta de productos estándar para garantizar que sus equipos tengan la máxima visibilidad de su sistema de AEM as a Cloud Service de y sus métricas de rendimiento del entorno.

En este documento se describe cómo administrar el acceso a las características de monitorización del rendimiento de la aplicación (APM) de New Relic One habilitadas en los entornos de AEM as a Cloud Service para ayudar a soportar el rendimiento y permitirle sacar el máximo provecho de AEM as a Cloud Service.

Cuando se crea un nuevo programa de producción, se crea automáticamente la cuenta secundaria de New Relic One asociada a su programa de AEM as a Cloud Service.

## Características {#transaction-monitoring}

New Relic One APM para AEM as a Cloud Service tiene muchas características.

* Acceso directo a una cuenta específica de New Relic One

* Agente de APM de New Relic One que muestra llamadas de método exactas con números de línea, incluidas dependencias externas y bases de datos

* Optimización del rendimiento integral mediante la combinación de métricas clave de la monitorización a nivel de infraestructura y la monitorización de aplicaciones (Adobe Experience Manager)

* Exposición de JMX Mbeans de AEM as a Cloud Service y comprobaciones de salud directamente dentro de las métricas de New Relic Insights, lo que permite una inspección profunda del rendimiento de la pila de aplicaciones y las métricas de salud.

## Administrar usuarios de New Relic One {#manage-users}

Siga los siguientes pasos para definir los usuarios de la cuenta secundaria de New Relic One asociada a su programa de AEM as a Cloud Service.

>[!NOTE]
>
>Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** debe iniciar sesión para administrar los usuarios de New Relic One.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desee administrar los usuarios de New Relic One.

1. En la parte inferior de la tarjeta **Entornos**, en la página Información general del programa, haga clic en el botón de los tres puntos y seleccione **Administrar usuarios**.

   ![Administrar usuarios](assets/newrelic-manage-users.png)

   * También puede acceder a la opción **Administrar usuarios** mediante el botón de los tres puntos de la parte superior de la pantalla **Entornos** de su programa.

1. En el cuadro de diálogo **Administrar usuarios de New Relic**, escriba el nombre y los apellidos del usuario que desea agregar y haga clic en el botón **Agregar**. Repita este paso para todos los usuarios que desee agregar.

   ![Agregar usuarios](assets/newrelic-add-users.png)

1. Para eliminar un usuario de New Relic One, haga clic en el botón eliminar situado en el extremo derecho de la fila que representa al usuario.

1. Haga clic en **Guardar** para crear los usuarios.

Una vez definidos los usuarios, New Relic enviará un correo electrónico de confirmación a cada usuario al que se haya concedido el acceso para que pueda completar el proceso de configuración e iniciar sesión.

>[!NOTE]
>
>Si está administrando a los usuarios de New Relic One, también debe agregarse como usuario para tener acceso. Ser el **Propietario del negocio** o el **Administrador de implementación** no es suficiente para tener acceso a New Relic One. También debe crearse un usuario.

## Activar la cuenta de usuario de New Relic One {#activate-account}

Una vez que cree una cuenta de usuario de New Relic One como se describe en la sección [Administrar usuarios de New Relic One](#manage-users), New Relic enviará a esos usuarios un correo electrónico de confirmación a la dirección proporcionada. Para utilizar esas cuentas, los usuarios deben activarlas primero con New Relic y restablecer sus contraseñas.

Siga estos pasos para activar su cuenta como usuario de New Relic.

1. Haga clic en el vínculo proporcionado en el correo electrónico desde New Relic. Esto abre el explorador a la página de inicio de sesión de New Relic.

1. En la página de inicio de sesión de New Relic seleccione **¿Olvidó su contraseña?**.

   ![Iniciar sesión en New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Introduzca la dirección de correo electrónico donde recibió el correo de confirmación y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic le enviará un correo electrónico con un vínculo para confirmar la cuenta.

Si no recibe un correo electrónico de confirmación de New Relic, consulte la [sección de resolución de problemas.](#troubshooting)

## Acceder a New Relic One {#accessing-new-relic}

Una vez que haya [activado su nueva cuenta de New Relic,](#activate-account) puede acceder a New Relic One a través de Cloud Manager o directamente.

Para acceder a New Relic One a través de Cloud Manager, haga lo siguiente:

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea acceder a New Relic One.

1. En la parte inferior de la tarjeta **Entornos** en la página de información general del programa, haga clic en el botón de los tres puntos y seleccione **Abrir New Relic**.

   ![Administrar usuarios](assets/newrelic-access.png)

   * También puede acceder a New Relic a través del botón de los tres puntos de la parte superior de la pantalla **Entornos** de su programa.

1. En la nueva pestaña del explorador que se abre, inicie sesión en New Relic One.

Para acceder directamente a New Relic One haga lo siguiente:

1. Navegue hasta la página de inicio de sesión de New Relic en [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Inicie sesión en New Relic One.

### Verificar el correo electrónico {#verify-email}

Si se le solicita que verifique su correo electrónico durante el inicio de sesión en New Relic One, significa que su correo electrónico está asociado a varias cuentas. Esto le permite elegir a qué cuenta acceder.

Si no verifica su dirección de correo electrónico, New Relic intentará iniciar sesión con el registro de usuario creado más recientemente y asociado a su dirección de correo electrónico. Para evitar verificar el correo electrónico durante cada inicio de sesión, haga clic en la casilla de verificación **Recordarme** de la pantalla de inicio de sesión.

Para obtener más ayuda, abra un ticket de asistencia a través del [Portal de asistencia de AEM](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

## Solución de problemas de acceso a New Relic One {#troubleshooting}

Si se le agregó como nuevo usuario de New Relic One, tal como se describe en la sección [Administrar usuarios de New Relic One](#manage-users) y no puede localizar el correo electrónico de confirmación de la cuenta original, siga estos pasos.

1. Navegue hasta la página de inicio de sesión de New Relic en [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Seleccione **¿Olvidó su contraseña?**.

   ![Iniciar sesión en New Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Escriba la dirección de correo electrónico que utilizó para crear la cuenta y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic le enviará un correo electrónico con un vínculo para confirmar la cuenta.

Si completa el proceso de registro y no puede iniciar sesión en su cuenta debido a mensajes de error de correo electrónico o contraseña, registre un ticket de asistencia a través de [Admin Console.](https://adminconsole.adobe.com/)

Si no recibe un correo electrónico de New Relic, haga lo siguiente:

* Compruebe sus [filtros de correo no deseado](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Si procede, [agregue New Relic a la lista de correos electrónicos permitidos](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Si ninguna de estas sugerencias ayuda, envíe sus comentarios en el ticket de asistencia, el equipo de soporte de Adobe podrá ayudarle.

## Restricciones {#limitations}

Las siguientes limitaciones se aplican a la adición de usuarios a New Relic One:

* Se puede agregar un máximo de 30 usuarios. Si se ha alcanzado el número máximo de usuarios, elimine algunos para poder añadir nuevos.
* Los usuarios añadidos a New Relic son de tipo **Restringido**, consulte [la documentación de New Relic para obtener más información.](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20individuals%20who,change)
* AEM as a Cloud Service solo ofrece la solución de APM New Relic One y no proporciona soporte para alertas, registros o integraciones de la API.

>[!NOTE]
>
>Si no se detecta ninguna actividad en su cuenta de New Relic One durante 90 días o más, se detendrá el agente de APM.
>
>Abra un ticket de asistencia a través de la [AEM Portal de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) si desea volver a habilitar el agente de APM para sus entornos de AEMaaCS.

Para obtener más ayuda o instrucciones adicionales sobre las ofertas de New Relic One para su programa de AEM as a Cloud Service, abra un ticket de asistencia a través del [Portal de asistencia de AEM](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

## Preguntas más frecuentes sobre New Relic One {#faqs}

### ¿Qué monitoriza Adobe con New Relic One? {#adobe-monitor}

Adobe monitoriza los servicios de autor, publicación y vista previa (cuando están disponibles) de AEM as a Cloud Service de a través del complemento Java de New Relic One. Adobe permite la telemetría y monitorización personalizada de APM New Relic One en entornos de AEM as a Cloud Service que sean de producción y de no producción.

La cuenta de New Relic One se adjunta a una cuenta principal mantenida por Adobe y tiene varias aplicaciones: tres por entorno de AEM as a Cloud Service.

* Una aplicación para el servicio de autor por entorno
* Una aplicación para el servicio de publicación por entorno (incluido Golden Publish)
* Una aplicación para el servicio de vista previa por entorno

Nota:

* Cada aplicación utiliza una clave de licencia.
* Los entornos de AEM as a Cloud Service solo informan a una cuenta de New Relic One.
* Las métricas y los eventos de monitorización completos para New Relic One se conservarán durante siete días.

### ¿Adobe envía notificaciones de alerta desde New Relic One? {#alerting-new-relic}

El Adobe de proporciona acceso a New Relic One únicamente para fines de observación y no lo utiliza para alertas del cliente o alertas operativas internas. Las notificaciones de cualquier incidente se envían mediante [perfiles de notificación de usuarios.](/help/journey-onboarding/notification-profiles.md)

### ¿Quién puede acceder a los datos del servicio en la nube de New Relic One? {#access-new-relic-cloud}

Se concede acceso de lectura completo hasta 30 miembros de su equipo. El acceso de lectura incluirá todas las métricas de APM recopiladas por el agente de New Relic One.

### ¿Se admite la configuración de SSO personalizada? {#custom-sso}

La configuración de SSO personalizada no es compatible con la cuenta de New Relic One aprovisionada por Adobe.

### ¿Qué sucede si ya tengo una suscripción a New Relic local? {#new-relic-subscription}

New Relic One es la nueva plataforma de observabilidad de New Relic y permite al soporte de Adobe y a sus equipos observar, monitorear y ver métricas y eventos, todo en un solo lugar.

New Relic One ofrece a los usuarios la capacidad de buscar en todas las cuentas donde tengan acceso y visualizar los datos de todos los servicios y hosts de un solo vistazo.

Mientras que el soporte de Adobe supervisa la aplicación de AEM as a Cloud Service mediante New Relic One y otras herramientas internas como parte de su servicio, sus equipos pueden seguir utilizando New Relic para servicios e infraestructura alojados localmente. Pueden visualizar los datos tanto de la cuenta de Adobe New Relic One como de las cuentas de New Relic administradas por el cliente.

>[!NOTE]
>
>Para ver ambos conjuntos de datos dentro de New Relic One, un usuario debe tener los permisos adecuados y utilizar la misma metodología de inicio de sesión para ambas cuentas (Adobe New Relic One y las cuentas de New Relic administradas por el cliente).

### El agente de APM de mi cuenta de New Relic One está detenido. ¿Qué pasó? {#deactivated}

[Los agentes de APM están detenidos](#limitations) si no se detecta ninguna actividad durante 90 días o más. Abra un ticket de asistencia a través de la [AEM Portal de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) si desea volver a habilitar el agente de APM para sus entornos de AEMaaCS.
