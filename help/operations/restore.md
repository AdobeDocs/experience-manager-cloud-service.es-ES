---
title: Restaurar contenido en AEM como un Cloud Service
description: Obtenga información sobre cómo restaurar el contenido de AEM as a Cloud Service desde la copia de seguridad mediante Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: e6bd71cc56db766fcbab3a925baabb5901c97ee8
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 20%

---


# Restaurar contenido en AEM como un Cloud Service {#content-restore}

Puede restaurar su AEM como un contenido de Cloud Service desde copia de seguridad mediante Cloud Manager.



El proceso de restauración de autoservicio de Cloud Manager copia los datos de las copias de seguridad del sistema de Adobe y los restaura a su entorno original. Se realiza una restauración para devolver los datos que se han perdido, dañado o eliminado accidentalmente a su estado original.

El proceso de restauración solo afecta al contenido, no modifica el código ni la versión de AEM. Puede iniciar una operación de restauración de entornos individuales en cualquier momento.

Si necesita restaurar el código fuente implementado anteriormente de una manera fácil y rápida, sin la necesidad de inicio una nueva ejecución de canalización, puede usar [Restaurar el Anterior Code implementado](/help/operations/restore-previous-code-deployed.md).

Cloud Manager ofrece dos tipos de copias de seguridad desde las que puede restaurar contenido.

* **Momento dado (PIT):** Esta opción restaura las copias de seguridad continuas capturadas en las últimas 24 horas.
* **Última semana:** este tipo restaura de las copias de seguridad del sistema en los últimos siete días, excluyendo las 24 horas anteriores.

En ambos casos, la versión del código personalizado y la versión AEM permanecen sin cambios.

>[!TIP]
>
>También es posible restaurar copias de [seguridad utilizando la API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/) pública.

>[!WARNING]
>
>* Esta característica solo debe usarse cuando haya problemas graves con el código o contenido.
>* Al restaurar un copia de seguridad, se eliminan todos los datos agregados después de esa copia de seguridad. El ensayo también vuelve a su versión anterior.
>* Antes de iniciar una restauración contenido, considere otras opciones de restauración selectiva contenido.

## Opciones de restauración selectiva contenido {#selective-options}

Antes de restaurar a una restauración contenido completa, considere estas opciones para restaurar su contenido más fácilmente.

* Si hay disponible un paquete para la ruta eliminada, vuelva a instalarlo utilizando el [Administrador de paquetes](/help/implementing/developing/tools/package-manager.md).
* Si la ruta eliminada era un Página en Sites, utilice la [función](/help/sites-cloud/authoring/sites-console/page-versions.md) Restaurar árbol.
* Si la ruta eliminada era una carpeta de activos y los archivos originales están disponibles, vuelva a cargar a través [de la consola](/help/assets/add-assets.md) Assets.
* Si los contenido de eliminación fueran activos, considere la posibilidad [de restaurar versiones anteriores del activos](/help/assets/manage-digital-assets.md).

Si ninguna de las opciones anteriores funciona y el contenido de la ruta eliminada es significativo, realice una restauración contenido como se detalla en las siguientes secciones.

## Crear usuario función {#user-role}

De forma predeterminada, ningún usuario tiene permiso para ejecutar restauraciones contenido en entornos de desarrollo, producción o ensayo. Para delegar este permiso a usuarios o grupos específicos, siga los siguientes pasos generales.

1. Crear un perfil de producto con un nombre expresivo que hace referencia a contenido restauración.
1. Proporcione el permiso de acceso **al** programa en el programa requerido.
1. Proporcione la Crear **de restauración de** entorno permiso en el entorno necesario o en todos los entornos del programa, según su caso de uso.
1. Asigne usuarios a esa perfil.

Para obtener más información sobre la administración de permisos, consulte [Permisos personalizados](/help/implementing/cloud-manager/custom-permissions.md).

## Restaurar el contenido de una entorno {#restoring-content}

>[!NOTE]
>
>Un usuario debe tener [los permisos apropiados](#user-role) para iniciar una operación de restauración.

**Para restaurar el contenido de una entorno:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en la programa para la que desea iniciar una restauración.

1. Enumere todos los entornos de la programa realizando una de las siguientes acciones:

   * En el menú del lado izquierdo, en Servicios, haga clic en **&#x200B;**&#x200B;Entornos del icono![&#x200B; &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)Datos **.**

     ![Pestaña Entornos](assets/environments-1.png)

   * En el menú de la izquierda, en Programa **, haga clic en**&#x200B;**Descripción general** y, a continuación, en el tarjeta Entornos **, haga clic en** el ![icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Flujo de trabajo Mostrar Todos.**

     ![Mostrar todas las opciones](assets/environments-2.png)

     >[!NOTE]
     >
     >La **tarjeta Entornos** enumera solo tres entornos. Haga clic en **Mostrar Todo** en la tarjeta para ver *todos los* entornos del programa.

1. En la tabla Entornos, a la derecha de un entorno cuyos contenido desee restaurar, haga clic en ![el icono Más o en el icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de menú de puntos suspensivos y, a continuación, haga clic en **Restaurar contenido**.

   ![Restaurar contenido opción desde el menú de puntos suspensivos](/help/operations/assets/environments-ellipsis-menu.png)

1. En la **pestaña Restaurar contenido** del Página del entorno, en la **lista desplegable Hora de restauración** , seleccione el lapso de tiempo de la restauración.

   ![Restaurar pestaña de contenido de una entorno](/help/operations/assets/environments-content-restore-tab.png)

   * Si selecciona **Últimas 24 horas**, en el campo Hora **contiguo**, especifique el tiempo exacto dentro de las últimas 24 horas para la restauración.
   * Si selecciona **Semana** pasada, en el campo Día contiguo **&#x200B;**, seleccione una fecha de los últimos siete días, excluyendo las 24 horas anteriores.

1. Una vez seleccionada una fecha o especificada una hora, la sección **Copias de seguridad disponibles**, más abajo, muestra una lista de las copias de seguridad disponibles que se pueden restaurar.

1. Haga clic en ![el icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Información junto a un copia de seguridad para ver su versión de código y AEM versión, luego sopese el impacto de la restauración antes de seleccionar un copia de seguridad (consulte [Elegir el copia de seguridad](#choosing-backup) correcto).

   ![Información de copia de seguridad](assets/backup-info.png)

   La marca de hora mostrada para las opciones de restauración se basa en la zona horaria del equipo de la usuario.

1. En el extremo derecho de la fila que representa la copia de seguridad que desea restaurar, haga clic en ![Rotar la negrita de CCW o restaurar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg) para inicio el proceso de restauración.

1. Revise los detalles del **cuadro de diálogo Restaurar contenido** y, a continuación, haga clic en **Restaurar**.

   ![Confirmar restauración](assets/backup-restore.png)

Se inicia el proceso copia de seguridad. Puede vista su estado en el **[lista Restaurar actividad](#restore-activity)** . El tiempo necesario para completar una operación de restauración depende del tamaño y el perfil del contenido que se está restaurando.

Cuando la restauración se completa correctamente, el entorno hace lo siguiente:

* Ejecuta el mismo código y AEM versión que en el momento de iniciar la operación de restauración.
* Tiene la misma contenido que estaba disponible en la marca de tiempo de la instantánea elegida, con los índices reconstruidos para que coincidan con el código actual.

## Elija la copia de seguridad correcta {#choosing-backup}

El proceso de restauración de autoservicio de Cloud Manager solo restaura contenido a AEM. Por este motivo, debe considerar cuidadosamente los cambios de código realizados entre el punto de restauración deseado y la hora actual. Revise el historial de confirmación entre el ID de confirmación actual y el que se está restaurando.

Existen varios escenarios.

* El entorno código personalizado y la restauración están en el mismo repositorio y en el mismo Rama.
* El entorno código personalizado y la restauración comparten una repositorio, utilizan un Rama independiente y se originan a partir de una confirmación común.
* El código personalizado entorno y la restauración se encuentran en repositorios diferentes.
   * En este caso, no se muestra ninguna ID de confirmación.
   * Adobe Systems recomienda encarecidamente que clone ambos repositorios y utilice un herramienta diff para comparar las ramas.

Además, tenga en cuenta que una restauración puede provocar que los entornos de producción y ensayo dejen de tener sincronizar. Usted es responsable de las consecuencias de restaurar contenido.

## Restaurar actividad {#restore-activity}

El **lista Actividad** de restauración muestra el estado de las diez solicitudes de restauración más recientes, incluidas las operaciones de restauración activas.

![Actividad de restauración](assets/backup-activity.png)

Al hacer clic en ![el icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Información de una copia de seguridad, puede descargar registros de esa copia de seguridad e inspeccionar los detalles del código, incluidas las diferencias entre la instantánea y los datos en el momento en que se inició la restauración.

## Fuera del sitio copia de seguridad {#offsite-backup}

Las copias de seguridad regulares cubren el riesgo de eliminaciones accidentales o fallos técnicos en AEM Cloud Services, pero pueden surgir riesgos adicionales debido al fallo de una zona. Además de la disponibilidad, el mayor riesgo en estas interrupciones de la región es la pérdida de datos.

AEM como Cloud Service mitiga este riesgo para todos los entornos de producción AEM. Es decir, copia continuamente todos los AEM contenido en un área geográfica remoto. Este proceso hace que el contenido esté disponible para la recuperación durante tres meses. Esta capacidad se conoce como copia de seguridad externa.

AEM Service Reliability Engineering restaura los entornos de ensayo y producción AEM Cloud Service a partir de copias de seguridad externas durante las interrupciones de área geográfica datos.

## Principios de asignación de regiones de datos {#data-region-mapping-principles}

Adobe Systems sigue un conjunto de directrices internas para determinar las asignaciones de área geográfica datos para **AEM como Cloud Service**. Estas directrices están diseñadas para respaldar la eficiencia operativa, garantizar el cumplimiento de los requisitos reglamentarios regionales y proporcionar una experiencia del cliente coherente en todos los mercados globales.

### Transparencia de asignación de regiones {#region-mapping-transparency}

Adobe Systems no divulga públicamente información cartográfica detallada de área geográfica a área geográfica.\
Si los clientes tienen preguntas específicas o justificadas sobre implementación regionales, residencia de datos o implicaciones de cumplimiento, se recomienda ponerse en contacto con Adobe Systems directamente a través de canales oficiales de soporte o cuenta.

### Principios básicos para la asignación de regiones de datos {#core-principles}

Al determinar una asignación de área geográfica de datos adecuada, Adobe Systems aplica varios criterios priorizados:

1. **No abandone el área geográfica global**\
   Las implementaciones permanecen dentro de una de las principales regiones globales: **APAC,**&#x200B;**EMEA** y **América.**

2. **No abandones el continente**\
   Siempre que sea posible, la replicación de datos y la conmutación por error permanecen en el mismo continente.

3. **No salgas del país**\
   Si es técnicamente factible, los datos permanecen dentro de las mismas fronteras nacionales.

### Gestión de excepciones {#handling-exceptions}

Cuando los criterios anteriores no puedan cumplirse debido a limitaciones técnicas o de infraestructura, Adobe Systems aplica consideraciones adicionales:

* **Directriz específica de Europa**\
  Las regiones secundarias o de copia de seguridad no deben estar ubicadas en países no pertenecientes a la UE.\
  (Lo contrario, usar un país de la UE como copia de seguridad para una primaria no perteneciente a la UE, puede ser aceptable si no existe una mejor opción para el mismo país).

* **Evite ciertas regiones**\
  Se deben evitar las regiones con políticas de datos restrictivas o con un mayor riesgo regulatorio como ubicaciones de copia de seguridad o conmutación por error.

Si los clientes requieren aclaración o tienen necesidades impulsadas por el cumplimiento, Adobe Systems recomienda comunicarse con el Adobe Systems cuenta equipo u organización de soporte para obtener orientación adaptada a su escenario específico.

## Restricciones     {#limitations}

El uso del mecanismo de restauración de autoservicio está sujeto a las siguientes limitaciones.

* Las operaciones de restauración están limitadas a siete días, lo que significa que no es posible restaurar una instantánea con más de esa antigüedad.
* Se permiten un máximo de diez restauraciones exitosas en todos los entornos de un programa por mes calendario.
* Después de la creación del entorno, la primera instantánea de copia de seguridad tarda seis horas en producirse. Hasta que se genera esta, no se puede llevar a cabo ninguna restauración en el entorno.
* No se inicia una operación de restauración si hay una canalización de configuración de pila completa o de nivel web ejecutándose para la entorno.
* No se puede iniciar una restauración si ya se está ejecutando otra restauración en el mismo entorno.
* En casos excepcionales, debido al límite de copias de seguridad de 24 horas y siete días, es posible que la copia de seguridad seleccionada no esté disponible por un retraso entre el momento en que se seleccionó y el momento en que se inició la restauración.
* Los datos de los entornos eliminados se pierden de forma permanente y no se pueden recuperar.
