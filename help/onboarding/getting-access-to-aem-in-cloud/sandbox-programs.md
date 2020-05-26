---
title: Programas de Simulador para pruebas - Servicio de nube
description: Programas de Simulador para pruebas - Servicio de nube
translation-type: tm+mt
source-git-commit: 22c6a79e68bbcd7329c7b1774d8445c216cdf8a8
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---


# Programas de Simulador para pruebas {#sandbox-programs}

## Introducción {#introduction}

Un programa de Simulador para pruebas es uno de los dos tipos de programas disponibles en el servicio de nube de AEM; el otro es un programa normal.

Normalmente, un Simulador para pruebas se crea para servir los fines de capacitación, administración de demostraciones, habilitación o Prueba de conceptos (POC). No tienen la intención de transportar tráfico en directo. No están sujetos a [AEM como compromisos](https://www.adobe.com/legal/service-commitments.html)de servicio en la nube.

Los entornos creados en un Simulador para pruebas no están configurados para escalar automáticamente. Por lo tanto, no son adecuadas para el rendimiento o las pruebas de carga.

Los programas del Simulador para pruebas incluyen Sitios y Recursos y se rellenan automáticamente con un repositorio Git, un entorno de desarrollo y un canalizador que no es de producción.  El repositorio Git se rellena con un proyecto de muestra basado en el arquetipo del proyecto AEM.

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

Para obtener más información sobre cómo crear un Programa de Simulador para pruebas, consulte [Creación de un Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-sandbox-program) de Simulador para pruebas para pruebas.

### Creación de Entornos de Simulador para pruebas {#creating-sandbox-environments}

Los Programas del Simulador para pruebas se entregan a un entorno de desarrollo en el momento de la creación del programa de una forma creada automáticamente. El entorno de desarrollo incluye un autor y un nivel de publicación de forma predeterminada.

El conjunto de entornos Producción-Fase se puede agregar manualmente al Programa Simulador para pruebas cuando el usuario esté listo para configurar una canalización de producción.

Para obtener más información sobre cómo crear manualmente un entorno, consulte [Añadir Entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments) para obtener más información.

### Eliminación de Entornos de Simulador para pruebas {#deleting-sandbox-environments}

El usuario con los permisos necesarios puede eliminar un entorno o conjuntos de desarrollo o producción o etapa.

Para eliminar un entorno, consulte [Eliminación de Entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment) para obtener más información.


## Hibernación y deshibernación de Entornos de Simulador para pruebas {#hibernating-introduction}

Los entornos de Programa de Simulador para pruebas entran en un modo *de* hibernación si no se detecta ninguna actividad durante un período de tiempo determinado.

>[!NOTE]
>La hibernación es exclusiva de los entornos de Programa de Simulador para pruebas. Los entornos de programa normales no hibernan.

### Hibernación {#hibernation-introduction}

La hibernación puede producirse de forma automática o manual. Los entornos de Programa de Simulador para pruebas pueden tardar hasta unos minutos en entrar en un modo *de* hibernación. Los datos se conservan durante la hibernación.

La hibernación se clasifica como:

* **Los entornos de Programa automático** de Simulador para pruebas se hibernan automáticamente tras ocho horas de inactividad, lo que significa que ni el autor ni los servicios de publicación reciben solicitudes.

* **Manual**: Como usuario, puede hibernar manualmente un entorno de Programa de Simulador para pruebas, aunque no es necesario hacerlo, ya que la hibernación se producirá automáticamente tras un período determinado (ocho horas) de inactividad.

>[!CAUTION]
>En la última versión, la vinculación a la consola de desarrollador directamente desde Cloud Manager no le dará la opción de hibernar un entorno de Programa de Simulador para pruebas. La solución alternativa se encuentra una vez en la consola de desarrollador, agregue el siguiente patrón al final de la URL `#release-cm-p1234-e5678 where 1234` 1234 es su ID *de* Programa y 5678 es su ID *de* Entorno.

#### Uso de la hibernación manual {#using-manual-hibernation}

Puede hibernar manualmente el Programa de Simulador para pruebas desde la Consola de programadores de dos maneras diferentes, mediante:

* Pantalla de detalles del Entorno
* Pantalla de listado de Entornos

Siga los pasos a continuación para hibernar manualmente los entornos de Programa del Simulador para pruebas:

1. Vaya a **Developer Console**.
Consulte [Acceso a la consola](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) de desarrollador para obtener información sobre cómo acceder a la consola **de** desarrollador desde la tarjeta de **Entornos** .
   >[!IMPORTANT]
   >Vincular la consola **de** desarrollador directamente desde Cloud Manager no le dará la opción de hibernar un entorno de Programa de Simulador para pruebas. La solución alternativa se encuentra una vez en la consola de desarrollador, agregue el siguiente patrón al final de la URL `#release-cm-p1234-e5678 where 1234` 1234 es su ID *de* Programa y 5678 es su ID *de* Entorno.

1. Click **Hibernate**, as shown in the figure below:

   ![](assets/hibernate-1.png)

   O bien,

   Haga clic en el vínculo **Entornos** en la parte superior izquierda para realizar la vista de la lista de entornos y, a continuación, haga clic en **Hibernar**, como se muestra en la figura siguiente:

   ![](assets/hibernate-1b.png)

1. Haga clic en **Hibernar** para confirmar el paso.

   ![](assets/hibernate-2.png)

1. Cuando la hibernación se realice correctamente, verá la notificación de finalización del proceso de hibernación para el entorno en la pantalla de la consola **** del desarrollador.

   ![](assets/hibernate-4.png)


### Deshibernación {#de-hibernation-introduction}

1. Vaya a **Developer Console**.
Consulte [Acceso a la consola](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#accessing-developer-console) de desarrollador para obtener información sobre cómo acceder a la consola **de** desarrollador desde la tarjeta de **Entornos** .

   >[!IMPORTANT]
   >Vincular la consola **de** desarrollador directamente desde Cloud Manager no le dará la opción de deshibernar un entorno de Programa de Simulador para pruebas. La solución alternativa se encuentra una vez en la consola de desarrollador, agregue el siguiente patrón al final de la URL `#release-cm-p1234-e5678 where 1234` 1234 es su ID *de* Programa y 5678 es su ID *de* Entorno.

   >[!NOTE]
   >Como alternativa, puede desplazarse a la consola **de** desarrollador para anular la hibernación intentando acceder al servicio de creación o publicación de un entorno ya en estado de hibernación; en ese caso, aparecerá una página de aterrizaje con un vínculo a la consola de desarrollador. Consulte la sección Acceso a un Entorno hibernado más abajo.

   >[!IMPORTANT]
   >El acceso a la consola de desarrollador lo define el rol **Administrador de** nube - Desarrollador de la Consola **de administración**. Un usuario con permiso de función de desarrollador puede anular la hibernación de un entorno de Programa de Simulador para pruebas.

1. Haga clic en **Deshibernar**, como se muestra en la figura siguiente:

   ![](assets/de-hibernation-img1.png)

   O bien,

   Haga clic en el vínculo **Entornos** en la parte superior izquierda para vista de la lista de entornos y, a continuación, haga clic en **Deshibernar**, como se muestra en la figura siguiente

   ![](assets/de-hibernate-1b.png)


1. Haga clic en **De Hibernate** para confirmar el paso.

   ![](assets/de-hibernation-img2.png)

1. Recibirá la notificación de que se ha iniciado el proceso de deshibernación y se le actualizará con el progreso.

   ![](assets/de-hibernation-img3.png)

1. Una vez completado el proceso, el entorno de Programa del Simulador para pruebas vuelve a estar activo.

   ![](assets/de-hibernation-img4.png)

#### Permisos para deshibernar {#permissions-de-hibernate}

Cualquier usuario con un perfil de producto que les permita acceder a AEM como servicio de nube debe poder acceder a **Developer Console**, lo que le permitirá deshibernar el entorno.

Consulte [Añadir usuarios y funciones](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html) en Cloud Manager para obtener información sobre la configuración de los permisos de usuario.

#### Acceso a un Entorno hibernado {#accessing-hibernated-environment}

Al realizar cualquier solicitud de explorador en el nivel de autor o publicación de un entorno hibernado, el usuario encontrará una página de aterrizaje que describe el estado de hibernación del entorno, como se muestra en la figura siguiente:

![](assets/de-hibernation-img5.png)

### Consideraciones importantes {#important-considerations}

Pocas consideraciones clave relacionadas con los entornos hibernados y deshibernados son:

* Un usuario puede utilizar una canalización para implementar código personalizado en entornos hibernados. El entorno permanecerá en estado de hibernación y el nuevo código aparecerá en el entorno una vez que se haya deshibernado.

* Las actualizaciones de AEM se pueden aplicar a entornos hibernados, que los clientes pueden activar manualmente desde Cloud Manager. El entorno permanecerá en estado de hibernación y la nueva versión aparecerá en el entorno una vez que se haya deshibernado.

>[!NOTE]
>Actualmente, Cloud Manager no indica si un entorno está hibernado.

## Actualizaciones de AEM a Entornos de Simulador para pruebas {#aem-updates-sandbox}

Consulte las actualizaciones [de la versión de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates) AEM para obtener más información.

Un usuario puede aplicar manualmente las actualizaciones de AEM a los entornos de un Programa de Simulador para pruebas.

Consulte [Actualización de Entorno](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#updating-dev-environment) para obtener información sobre cómo actualizar un entorno.

>[!NOTE]
>* Una actualización manual solo se puede ejecutar cuando el entorno de destino tiene una canalización correctamente configurada.
>* Una actualización manual del entorno *de producción* o de *fase* se actualizará automáticamente al otro. El conjunto de entornos Producción+Fase debe estar en la misma versión de AEM.






