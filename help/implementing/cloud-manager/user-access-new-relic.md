---
title: Nueva reliquia uno
description: Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 09049213eaf92830dc0e0d4c0885017c69a5d56e
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 1%

---


# Nueva reliquia uno {#user-access}

Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.

## Introducción {#introduction}

El Adobe pone un bueno énfasis en el monitoreo, la disponibilidad y el performance de su aplicación. AEM as a Cloud Service proporciona acceso a un nuevo grupo de monitorización relic 1 personalizado como parte de la oferta de productos estándar para garantizar que sus equipos tengan la máxima visibilidad de sus métricas de rendimiento de entorno y del sistema as a Cloud Service de AEM.

En este documento se describe cómo administrar el acceso a las funciones de supervisión del rendimiento de la aplicación (APM) de la Nueva Reliquia Uno habilitadas en los entornos as a Cloud Service AEM para ayudar a soportar el rendimiento y permitirle sacar el máximo provecho de AEM as a Cloud Service.

Cuando se crea un nuevo programa de producción, se crea automáticamente la subcuenta New Relic One asociada a su Programa as a Cloud Service AEM.

## Características {#transaction-monitoring}

Nueva reliquia Una APM para AEM as a Cloud Service tiene muchas características.

* Acceso directo a una cuenta específica de New Relic One (acceso administrado por la asistencia de Adobe)

* Agente de nueva relación con la aplicación instrumentada Un APM que muestra llamadas de método exactas con números de línea, incluidas dependencias externas y bases de datos

* Optimización del rendimiento holístico mediante la combinación de métricas clave de la monitorización a nivel de infraestructura y la monitorización de aplicaciones (Adobe Experience Manager)

* Exposición de AEM as a Cloud Service mazones de JMX y comprobaciones de estado directamente dentro de las métricas de New Relic Insights, lo que permite una inspección profunda del rendimiento de la pila de aplicaciones y las métricas de estado.

## Administrar nuevos usuarios de reliquia {#manage-users}

Siga estos pasos para definir los usuarios de la subcuenta New Relic One asociada a su Programa as a Cloud Service AEM.

>[!NOTE]
>
>Un usuario en **Propietario empresarial** o **Administrador de implementación** debe iniciar sesión para administrar los usuarios de la Nueva relación uno.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el cual desea administrar sus nuevos usuarios de Relic One.

1. Cambie a la **Entornos** de la variable **Información general del programa** haciendo clic en el botón **Entornos** en la parte superior de la pantalla.

1. En el **Entornos** , haga clic en el botón de puntos suspensivos en la parte superior de la pantalla junto a la **Agregar entorno** botón.

1. En el menú elipsis, haga clic en **Administración de usuarios**.

   ![Administración de usuarios](assets/newrelic-manage-users.png)

1. En el **Administrar nuevos usuarios de Reic** , introduzca el nombre y los apellidos del usuario que desea añadir y haga clic en el botón **Agregar** botón. Repita este paso para todos los usuarios que desee agregar.

   ![Agregar usuarios](assets/newrelic-add-users.png)

1. Para eliminar un usuario de Nueva relación, haga clic en el botón eliminar situado en el extremo derecho de la fila que representa al usuario.

1. Haga clic en **Guardar** para crear los usuarios.

Una vez definidos los usuarios, New Relic envía un correo electrónico de confirmación a cada usuario al que se ha concedido el acceso para que el usuario pueda completar el proceso de configuración e iniciar sesión.

>[!NOTE]
>
>Si está administrando los usuarios de Nueva reliquia uno, también debe agregarse como usuario para tener acceso a él. Ser el **Propietario empresarial** o **Administrador de implementación** no es suficiente para tener acceso a la nueva reliquia uno. También debe crearse como usuario.

## Activar la nueva cuenta de usuario de Relic One {#activate-account}

Una vez que se crea una nueva relación, una cuenta de usuario se crea como se describe en la sección de vista previa [Administrar nuevos usuarios de reliquia](#manage-users), New Relic envía a esos usuarios un correo electrónico de confirmación a la dirección proporcionada. Para utilizar esas cuentas, los usuarios deben activar primero sus cuentas con Nueva relación restableciendo sus contraseñas.

Siga estos pasos para activar su cuenta como usuario de Nueva relación.

1. Haga clic en el vínculo proporcionado en el correo electrónico desde Nueva relación. Esto abre el navegador a la página de inicio de sesión Nueva reliquia .

1. En la página de inicio de sesión Nueva reliquia , seleccione **¿Olvidó su contraseña?**.

   ![Nuevo inicio de sesión de Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Introduzca la dirección de correo electrónico donde recibió el correo electrónico de confirmación y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic le enviará un correo electrónico que contiene un vínculo para confirmar la cuenta.

Si no recibe un correo electrónico de confirmación de New Relic, consulte la [sección resolución de problemas .](#troubshooting)

## Acceso a la nueva reliquia uno {#accessing-new-relic}

Una vez que haya [ha activado su nueva cuenta de Reic,](#activate-account) puede acceder a Nueva reliquia uno a través de Cloud Manager o directamente.

Para acceder a la nueva reliquia uno a través de Cloud Manager:

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa para el que desea acceder a la Nueva reliquia uno.

1. Cambie a la **Entornos** de la variable **Información general del programa** haciendo clic en el botón **Entornos** en la parte superior de la pantalla.

1. En el **Entornos** , haga clic en el botón de puntos suspensivos en la parte superior de la pantalla junto a la **Agregar entorno** botón.

1. En el menú elipsis, haga clic en **Abrir nueva reliquia**.

1. En la nueva ficha del explorador que se abre, inicie sesión en Nueva relación uno.

Para acceder directamente a la nueva reliquia uno:

1. Vaya a la página de inicio de sesión de Nueva reliquia en [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. Inicie sesión en la nueva reliquia uno.

### Verificación del correo electrónico {#verify-email}

Si se le pide que verifique su correo electrónico durante el inicio de sesión en la nueva relación uno, significa que su correo electrónico está asociado con varias cuentas. Esto le permite elegir a qué cuenta acceder.

Si no verifica su dirección de correo electrónico, New Relic intentará iniciar sesión con el registro de usuario creado más recientemente y asociado a su dirección de correo electrónico. Para evitar verificar el correo electrónico durante cada inicio de sesión, haga clic en el botón **Recordarme** en la pantalla de inicio de sesión.

Para obtener más ayuda, abra un ticket de asistencia a través de la [Portal de asistencia AEM](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).

## Solución de problemas de acceso único a la nueva relación de calidad {#troubleshooting}

Si se le agregó como un nuevo usuario de reliquia, tal como se describe en la sección [Administrar nuevos usuarios de reliquia](#manage-users) y no puede localizar el correo electrónico de confirmación de la cuenta original. Siga estos pasos.

1. Vaya a la página de inicio de sesión de Nueva reliquia en [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Select **¿Olvidó su contraseña?**.

   ![Nuevo inicio de sesión de Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Escriba la dirección de correo electrónico que se utilizó para crear la cuenta y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic le enviará un correo electrónico que contiene un vínculo para confirmar la cuenta.

Si completa el proceso de registro y no puede iniciar sesión en su cuenta debido a mensajes de error de correo electrónico o contraseña, registre un ticket de asistencia a través de la [Admin Console.](https://adminconsole.adobe.com/)

Si no recibe un correo electrónico de New Relic:

* Compruebe su [filtros de correo no deseado](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
* Si procede, [añadir nueva relación a la lista de permitidos de correo electrónico](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
* Si ninguna de estas sugerencias ayuda, sírvase proporcionar comentarios sobre el ticket de asistencia y el equipo de soporte de Adobe le ayudará a obtener más información.

## Restricciones     {#limitations}

Las siguientes limitaciones se aplican a la adición de usuarios a la Nueva relación uno:

* Se puede añadir un máximo de 25 usuarios. Si se ha alcanzado el número máximo de usuarios, elimine usuarios para poder agregar nuevos usuarios.
* Los usuarios agregados a Nueva reliquia serán del tipo **Restringido** consulte [la documentación Nueva reliquia para obtener más información.](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=One%20or%20more%20individuals%20who,change)%20any%20New%20Relic%20features.)
* AEM as a Cloud Service solo ofrece la solución New Relic One APM y no proporciona soporte para alertas, registros o integraciones de API.

Para obtener más ayuda o instrucciones adicionales sobre las nuevas ofertas de Relic Uno para su Programa as a Cloud Service AEM, abra un ticket de asistencia a través de la [Portal de asistencia AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Preguntas más frecuentes sobre la nueva reliquia uno {#faqs}

### ¿Qué monitoriza el Adobe con la nueva reliquia uno? {#adobe-monitor}

Adobe supervisa los servicios de creación, publicación y vista previa (cuando están disponibles) as a Cloud Service de AEM a través del complemento Java de New Relic One. Adobe permite la telemetría y monitorización personalizada de New Relic One APM en entornos as a Cloud Service que no sean de producción y producción AEM.

La nueva cuenta de Relic One está adjunta a una cuenta principal mantenida por Adobe y tiene varias aplicaciones informando al respecto: tres por AEM entorno as a Cloud Service.

* Una aplicación para el servicio de creación por entorno
* Una aplicación para el servicio de publicación por entorno (incluida la publicación de oro)
* Una aplicación para el servicio de vista previa por entorno

Importante:

* Cada aplicación utiliza una clave de licencia.
* AEM entornos as a Cloud Service solo informan de una cuenta nueva de Relic One.
* Las métricas y los eventos de monitorización completos para la Nueva reliquia uno se conservan durante siete días.

### ¿Quién puede acceder a los datos del servicio en la nube New Relic One? {#access-new-relic-cloud}

Se concederá acceso de lectura completo para hasta 10 miembros de su equipo. El acceso de lectura incluirá todas las métricas de APM recopiladas por el agente New Relic One.

### ¿Se admite la configuración de SSO personalizada? {#custom-sso}

La configuración de SSO personalizada no es compatible con la nueva cuenta de Relic One aprovisionada por Adobe.

### ¿Qué sucede si ya tengo una suscripción a New Relic local? {#new-relic-subscription}

Nueva reliquia uno es la nueva plataforma de observabilidad de Nueva reliquia y permite al soporte de Adobe y a sus equipos observar, monitorear y ver métricas y eventos, todo en un solo lugar.

La nueva reliquia uno ofrece a los usuarios la capacidad de buscar en todas las cuentas donde tengan acceso y visualizar los datos de todos los servicios y hosts de una sola vista.

Mientras que el soporte de Adobe supervisará la aplicación as a Cloud Service AEM utilizando New Relic One y otras herramientas internas como parte de su servicio, sus equipos pueden seguir aprovechando New Relic para servicios e infraestructura alojados in situ. Podrán visualizar los datos tanto de la cuenta de Adobe Nueva reliquia uno como de las cuentas de Nueva reliquia gestionadas por el cliente.

>[!NOTE]
>
>Para ver ambos conjuntos de datos dentro de la nueva relación uno, un usuario debe tener los permisos adecuados y utilizar la misma metodología de inicio de sesión para ambas cuentas (Adobe de la nueva relación uno y las cuentas de nueva relación gestionadas por el cliente).
