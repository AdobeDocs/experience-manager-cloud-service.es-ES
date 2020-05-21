---
title: Programas de Simulador para pruebas - Servicio de nube
description: Programas de Simulador para pruebas - Servicio de nube
translation-type: tm+mt
source-git-commit: 168b3d28a36e4ec5258b2d2f391af25c466be6c6
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---


# Programas de Simulador para pruebas {#sandbox-programs}

## Introducción {#introduction}

Un programa de Simulador para pruebas es uno de los dos tipos de programas disponibles en el servicio de nube de AEM; el otro es un programa normal.

Normalmente, un Simulador para pruebas se crea para servir los fines de capacitación, administración de demostraciones, habilitación o Prueba de conceptos (POC). No tienen la intención de transportar tráfico en directo.

Los programas del Simulador para pruebas incluyen Sitios y recursos y se rellenan automáticamente con una rama Git que incluye código de muestra, un entorno de desarrollo y una canalización sin producción.

Consulte [Explicación de los tipos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html) de Programas y Programas para obtener más información sobre los tipos de Programas.

### Atributos de los Programas de Simulador para pruebas {#attributes-sandbox}

Los Programas de Simulador para pruebas tienen los atributos siguientes:

1. **Creación de Programas:** La creación del programa del Simulador para pruebas incluye:
   * configuración del proyecto con código de muestra y contenido
   * creación de entornos de desarrollo
   * creación de una canalización sin producción que se implementa en el entorno de desarrollo (implementación de ramificaciones maestras en el entorno de desarrollo)

1. **Soluciones:** Los programas de Simulador para pruebas incluyen Recursos y Sitios AEM.

1. **Actualizaciones de AEM:** Las actualizaciones de AEM se pueden aplicar manualmente a entornos en un programa de Simulador para pruebas y no se insertan automáticamente.

1. **Hibernación:** Los Entornos de un programa de Simulador para pruebas se hibernan automáticamente si no se detecta ninguna actividad durante un período de tiempo determinado. Los entornos hibernados se pueden deshibernar manualmente.

### Creación de un Programa de Simulador para pruebas {#creating-sandbox-program}

Un asistente para la creación de programas permite crear un Programa de Simulador para pruebas.

Para obtener información sobre cómo crear un Programa de Simulador para pruebas, consulte [Creación de un Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)de Simulador para pruebas.

### Creación de Entornos de Simulador para pruebas {#creating-sandbox-environments}

Los Programas de Simulador para pruebas se entregan como entornos de desarrollo en el momento de la creación del programa de una manera creada automáticamente. El entorno de desarrollo incluye un autor y un nivel de publicación de forma predeterminada.

El conjunto de entornos Producción-Fase se puede agregar manualmente al Programa Simulador para pruebas cuando el usuario esté listo para configurar una canalización de producción.

Para obtener más información sobre cómo crear manualmente un entorno, consulte [Añadir Entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) para obtener más información.

### Eliminación de Entornos de Simulador para pruebas  {#deleting-sandbox-environments}

El usuario con los permisos necesarios puede eliminar un entorno o conjuntos de desarrollo o producción o etapa.

Para eliminar un entorno, consulte [Eliminación de Entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) para obtener más información.


## Hibernación y deshibernación de Entornos de Simulador para pruebas {#hibernating-introduction}

Los entornos de Programa de Simulador para pruebas entran en un modo *de* hibernación si no se detecta ninguna actividad durante un período de tiempo determinado.

>[!NOTE]
>La hibernación es exclusiva de los entornos de Programa de Simulador para pruebas. Los entornos de programa normales no hibernan.

### Hibernación {#hibernation-introduction}

La hibernación puede producirse de forma automática o manual. Los entornos de Programa de Simulador para pruebas pueden tardar hasta unos minutos en entrar en un modo *de* hibernación. Los datos se conservan durante la hibernación.

La hibernación se clasifica como:

* **Los entornos de Programa automático** de Simulador para pruebas se hibernan automáticamente tras ocho horas de inactividad, lo que significa que ni el autor ni los servicios de publicación reciben la solicitud.

* **Manual**: Como usuario, puede hibernar manualmente un entorno de Programa de Simulador para pruebas, aunque no es necesario hacerlo, ya que la hibernación se producirá automáticamente después de cierto período (ocho horas) de inactividad.

#### Uso de la hibernación manual {#using-manual-hibernation}

Puede hibernar manualmente el Programa de Simulador para pruebas desde la Consola de programadores de dos maneras diferentes, mediante:

* Pantalla de detalles del Entorno
* Pantalla de listado de Entornos

Siga los pasos a continuación para hibernar manualmente los entornos de Programa del Simulador para pruebas:

1. Vaya a **Developer Console**.
Consulte [Acceso a la consola](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) de desarrollador para obtener información sobre cómo acceder a la consola **de** desarrollador desde la tarjeta de **Entornos** .

1. Haga clic en Hibernar, como se muestra en la figura siguiente

   ![](assets/hibernate-1.png)
1. Haga clic en **Hibernar** para confirmar el paso.

   ![](assets/hibernate-2.png)

1. Cuando la hibernación se realice correctamente, verá la notificación de finalización del proceso de hibernación para el entorno en la pantalla de la consola **** del desarrollador.

   ![](assets/hibernate-4.png)

#### Acceso a un Entorno hibernado {#accessing-hibernated-environment}

Al realizar solicitudes de navegador contra la capa de creación o publicación de un entorno hibernado, el usuario encontrará una página de aterrizaje que describe el estado de hibernación del entorno, como se ilustra a continuación:

Un usuario con el rol **Administrador de** nube - Función de desarrollador puede hacer clic en el botón Consola de desarrollador para acceder a la consola de desarrollador y anular la hibernación del entorno. Encontrará información sobre la configuración de roles en la documentación de Cloud Manager.

Si un usuario de una organización no puede hacer clic en el botón de la consola de desarrollador para que se le lleve a la consola de desarrollador, es probable que tenga que recibir la &quot;Cloud Manager - Función de desarrollador&quot;.


### Deshibernación {#de-hibernation-introduction}

1. Vaya a **Developer Console**.
Consulte [Acceso a la consola](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) de desarrollador para obtener información sobre cómo acceder a la consola **de** desarrollador desde la tarjeta de **Entornos** .

   >[!IMPORTANT]
   >El acceso a la consola de desarrollador lo define el rol **Administrador de** nube - Desarrollador de la Consola **de administración**. Un usuario con permiso de función de desarrollador puede anular la hibernación de un entorno de Programa de Simulador para pruebas.

1. Haga clic en **Deshibernar**, como se muestra en la figura siguiente:

   ![](assets/de-hibernation-img1.png)

1. Haga clic en **De Hibernate** para confirmar el paso.

   ![](assets/de-hibernation-img2.png)

1. Recibirá la notificación de que se ha iniciado el proceso de deshibernación y se le actualizará con el progreso.

   ![](assets/de-hibernation-img3.png)

1. Una vez completado el proceso, el entorno de Programa del Simulador para pruebas vuelve a estar activo.

   ![](assets/de-hibernation-img4.png)


## Actualizaciones de AEM a Entornos de Simulador para pruebas {#aem-updates-sandbox}


Consulte las actualizaciones [de la versión de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) AEM para obtener más información.

Un usuario puede aplicar manualmente las actualizaciones de AEM a los entornos de un Programa de Simulador para pruebas (ver la figura siguiente). Esto se puede hacer cuando el estado mostrado esté **DISPONIBLE** ACTUALIZAR.

La opción Actualizar está disponible en el menú desplegable de la tarjeta de **Entornos** . Esta opción también está disponible desde el botón **Administrar** , si hace clic en **Detalles** desde la tarjeta de **Entornos** .

>[!NOTE]
>Se debe configurar una canalización ** sin producción que se implemente en el entorno de intereses de desarrollo para que se inicie una canalización de actualización manual.

>[!NOTE]
>Se debe configurar una canalización *de producción* para que se inicie una canalización de actualización manual al conjunto de entornos Producción+Fase.

>[!NOTE]
>La actualización manual a *Producción* o a entorno de *etapa* se actualizará automáticamente a la otra. El conjunto de entornos Producción+Fase debe estar en la misma versión de AEM.





