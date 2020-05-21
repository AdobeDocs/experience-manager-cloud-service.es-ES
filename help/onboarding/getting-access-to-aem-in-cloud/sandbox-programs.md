---
title: Programas de Simulador para pruebas - Servicio de nube
description: Programas de Simulador para pruebas - Servicio de nube
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# Programas de Simulador para pruebas {#sandbox-programs}

## Introducción {#introduction}

Un programa de Simulador para pruebas es uno de los dos tipos de programas disponibles en el servicio de nube de AEM; el otro es un programa normal.

Generalmente, se crea un Simulador para pruebas para fines de capacitación, administración de demostraciones, habilitación o puntos de interés. No tienen la intención de transportar tráfico en directo.

Los programas del Simulador para pruebas incluyen Sitios y Recursos y se entregarán automáticamente con una rama Git que incluye código de muestra, un entorno de desarrollo y una canalización sin producción.

Para obtener más información sobre los tipos de programas, consulte [Explicación de los Programas y los tipos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)de Programas.

### Atributos de los Programas de Simulador para pruebas {#attributes-sandbox}

Los Programas de Simulador para pruebas tienen los atributos siguientes:

1. **Creación de Programas:** La creación del programa del Simulador para pruebas incluye:
   * configuración del proyecto con código de muestra y contenido
   * creación de entornos de desarrollo
   * creación de canalizaciones sin producción que se implementan en el entorno de desarrollo (implementación de ramificaciones maestras en el entorno de desarrollo)

1. **Las soluciones incluyen:** Los programas del Simulador para pruebas incluyen Sitios y recursos.

1. **Actualizaciones de AEM:** Las actualizaciones de AEM se pueden aplicar manualmente a entornos en un programa de Simulador para pruebas y no se insertan automáticamente.

1. **Hibernación:** Los Entornos de un programa de Simulador para pruebas se hibernarán automáticamente si no se detecta ninguna actividad durante un período de tiempo determinado. Los entornos hibernados se pueden deshibernar manualmente.

### Creación de un programa de Simulador para pruebas {#creating-sandbox-program}

Un asistente para la creación de programas pedirá al usuario que envíe los detalles.

Para obtener información sobre cómo crear un programa de simulación de pruebas, consulte [Creación de un Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)de Simulador para pruebas.

### Creación de Entornos de Simulador para pruebas {#creating-sandbox-environments}

Los programas de Simulador para pruebas se entregarán como un entorno de desarrollo en el momento de la creación del programa de una manera creada automáticamente. El entorno de desarrollo viene con un autor y un nivel de publicación de forma predeterminada.

El conjunto de entornos Producción-Fase se puede agregar manualmente al programa Simulador para pruebas cuando el usuario esté listo para configurar una canalización de producción.

Para obtener información sobre cómo crear manualmente un entorno, consulte [Añadir Entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments).

### Eliminación de Entornos de Simulador para pruebas  {#deleting-sandbox-environments}

El usuario con los permisos necesarios podrá eliminar un entorno/conjunto de desarrollo o producción/fase.

Para obtener información sobre cómo eliminar un entorno, consulte [Eliminación de Entornos](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment).


## Hibernación y deshibernación de Entornos de Simulador para pruebas {#hibernating-introduction}

Los entornos de programa de Simulador para pruebas entrarán en un modo *de* hibernación después de un período de inactividad.

>[!NOTE]
>La hibernación es única para los entornos de programa de simulación de pruebas. Los entornos de programa normales no se hibernarán.

### Hibernación {#hibernation-introduction}

La hibernación puede producirse de forma automática o manual. Un entorno puede tardar hasta unos minutos en hibernarse. Los datos se conservan durante la hibernación.

La hibernación se clasifica como:

* **Los entornos de programa automático** de Simulador para pruebas se hibernan automáticamente tras ocho horas de inactividad, lo que significa que ni el autor ni los servicios de publicación reciben la solicitud.

* **Manual**: Los clientes pueden hibernar manualmente un entorno de programa de simulación de pruebas, aunque no es necesario hacerlo, ya que la hibernación se producirá automáticamente tras un período de inactividad.

#### Uso de la hibernación manual {#using-manual-hibernation}


La hibernación manual se puede realizar desde cualquiera de las dos pantallas de la consola del desarrollador.

Siga los pasos a continuación para hibernar manualmente los entornos de programa:

1. Vaya a la Consola de programadores.
1. Haga clic en Hibernar
1. Haga clic en Hibernar para confirmar.
1. Cuando la hibernación se realice correctamente, verá la siguiente pantalla.
1. En la pantalla Lista de entornos, que se muestra a continuación y a la que se puede acceder haciendo clic en el vínculo Entornos de la pantalla de detalles del entorno, se puede hacer clic en el botón Hibernar en la fila del entorno deseado. Aparecerá una pantalla de confirmación.

### Deshibernación {#de-hibernation-introduction}

>[!IMPORTANT]
>El acceso a la consola de desarrollador está definido por &quot;Cloud Manager - Función de desarrollador&quot; en la Consola de administración. Con ese permiso, un usuario puede anular la hibernación de un entorno.

### Acceso a un Entorno hibernado {#accessing-hibernated-environment}

Al realizar solicitudes de navegador contra la capa de creación o publicación de un entorno hibernado, el usuario encontrará una página de aterrizaje que describe el estado de hibernación del entorno, como se ilustra a continuación:

Un usuario con la función de desarrollador &quot;Administrador de nube&quot; puede hacer clic en el botón Consola de desarrollador para acceder a la consola de desarrollador y anular la hibernación del entorno. Encontrará información sobre la configuración de roles en la documentación de Cloud Manager.

Si un usuario de una organización no puede hacer clic en el botón de la consola de desarrollador para que se le lleve a la consola de desarrollador, es probable que tenga que recibir la &quot;Cloud Manager - Función de desarrollador&quot;.




## Actualizaciones de AEM en entornos de Simulador para pruebas {#aem-updates-sandbox}


Consulte las actualizaciones [de la versión de](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates)AEM.

El usuario puede aplicar manualmente las actualizaciones de AEM a los entornos de un programa de Simulador para pruebas (véase la figura siguiente). Esto se puede hacer cuando el estado mostrado esté DISPONIBLE ACTUALIZAR. La opción de actualización estará disponible en el menú desplegable de la tarjeta de Entornos. También se puede seleccionar en el menú Administrar de la pantalla ENTORNOS.

>[!NOTE]
>Debe configurarse una canalización que no sea de producción y que se implemente en el entorno de intereses de desarrollo para que se inicie una canalización de actualización manual.

>[!NOTE]
>Se debe configurar una canalización de producción para que se inicie una canalización de actualización manual al conjunto de entornos Producción+Fase.

>[!NOTE]
>La actualización manual de Producción o entorno de Fase actualizará automáticamente el otro. El conjunto de entornos Producción+Fase debe estar en la misma versión de AEM.





