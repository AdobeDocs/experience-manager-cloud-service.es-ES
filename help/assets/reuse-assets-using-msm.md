---
title: Reutilización de recursos mediante MSM
description: Utilice recursos en varias páginas o carpetas que se deriven de recursos principales y estén vinculadas a ellos. Los recursos permanecen sincronizados con una copia principal y, con unos pocos clics, reciben las actualizaciones de los recursos principales.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: a71aebdf-8e46-4c2d-8960-d188b14aaae9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '3221'
ht-degree: 10%

---

# Reutilizar recursos con MSM para [!DNL Assets] {#reuse-assets-using-msm-for-assets}

Funcionalidad de Multi Site Manager (MSM) en [!DNL Adobe Experience Manager] permite a los usuarios reutilizar contenido creado una vez y reutilizado en varias ubicaciones web. La misma funcionalidad está disponible para los recursos digitales por el nombre MSM para [!DNL Assets]. Uso de MSM para [!DNL Assets], puede:

* Cree recursos una vez y, a continuación, haga copias de estos recursos para reutilizarlos en otras áreas del sitio.
* Mantenga varias copias en sincronización y actualice la copia principal original una vez para insertar los cambios en las copias secundarias.
* Realice cambios locales suspendiendo temporal o permanentemente la vinculación entre recursos principales y secundarios.

## Comprender los beneficios y los conceptos de F.M. {#concepts}

### Cómo funciona y los beneficios {#how-it-works-and-the-benefits}

Para comprender los escenarios de uso para reutilizar el mismo contenido (texto y recursos) en varias ubicaciones web, consulte [posibles escenarios MSM](/help/sites-cloud/administering/msm/overview.md). [!DNL Experience Manager] mantiene un vínculo entre el recurso original y sus copias vinculadas, denominadas Live Copies (LC). La vinculación mantenida permite insertar cambios centralizados en muchas Live Copies. Esto permite realizar actualizaciones más rápidas mientras se eliminan las limitaciones de la administración de copias duplicadas. La propagación de los cambios está libre de errores y centralizada. La funcionalidad permite disponer de espacio para actualizaciones que se limitan a copias en vivo seleccionadas. Los usuarios pueden desasociar la vinculación, es decir, interrumpir la herencia, y realizar ediciones locales que no se sobrescriban la próxima vez que se actualice la copia principal y se implementen los cambios. La desvinculación se puede realizar para unos pocos campos de metadatos seleccionados o para todo un recurso. Permite flexibilidad para actualizar localmente los recursos que se heredan originalmente de una copia principal.

MSM mantiene una relación activa entre el recurso de origen y sus Live Copies, de modo que:

* Los cambios en los recursos de origen se aplican (se implementan) también a las Live Copies, es decir, las Live Copies se sincronizan con el origen.
* Puede actualizar las Live Copies suspendiendo la relación activa o eliminando la herencia de algunos campos limitados. Las modificaciones al origen ya no se aplican a la Live Copy.

### Glosario de MSM para [!DNL Assets] términos {#glossary}

**Fuente:** Los recursos o carpetas originales. Copia principal de la que provienen las Live Copies.

**Live Copy:** Copia de los recursos o carpetas de origen que están en sincronización con su origen. Las Live Copies pueden ser una fuente de más Live Copies. Consulte cómo crear LC.

**Herencia:** Un vínculo/referencia entre un recurso o carpeta de Live Copy y su origen que el sistema utiliza para recordar dónde enviar las actualizaciones. La herencia existe a nivel granular para los campos de metadatos. La herencia se puede eliminar para campos de metadatos selectivos, preservando al mismo tiempo la relación activa entre el origen y su Live Copy.

**Despliegue:** Acción que impulsa las modificaciones realizadas en el flujo descendente de origen a sus Live Copies. Es posible actualizar una o más Live Copies en una misma vez mediante la acción de despliegue. Consulte despliegue.

**Configuración de lanzamiento:** Reglas que determinan qué propiedades se sincronizan, cómo y cuándo. Estas configuraciones se aplican al crear Live Copies; se puede editar más adelante; y un elemento secundario puede heredar la configuración de lanzamiento de su recurso principal. Para MSM para [!DNL Assets], utilice solo la configuración de lanzamiento estándar . Las demás configuraciones de implementación no están disponibles para MSM para [!DNL Assets].

**Sincronizar:** Otra acción, además del despliegue, que trae paridad entre el origen y su Live Copy al enviar las actualizaciones del origen a las Live Copies. Se inicia una sincronización para una Live Copy concreta y la acción extrae los cambios del origen. Con esta acción, solo es posible actualizar una de las Live Copies. Consulte Sincronizar acción.

**Suspender:** Elimine temporalmente la relación activa entre una Live Copy y su recurso/carpeta de origen. Puede reanudar la relación. Consulte suspender acción.

**Reanudar:** Reanude la relación activa para que una Live Copy vuelva a recibir las actualizaciones del origen. Consulte Reanudar acción.

**Restablecer:** La acción Reset hace que la Live Copy vuelva a ser una réplica del origen sobrescribiendo los cambios locales. También elimina las cancelaciones de herencia y restablece la herencia en todos los campos de metadatos. Para realizar modificaciones locales en el futuro, debe cancelar de nuevo la herencia de campos específicos. Consulte modificaciones locales a la LC.

**Desasociar:** Elimine irrevocablemente la relación activa de una carpeta o un recurso de Live Copy. Después de la acción de desasociar, las Live Copies nunca pueden recibir actualizaciones del origen y deja de ser una Live Copy. Consulte quitar relación.

## Crear una Live Copy de un recurso {#create-livecopy}

Para crear Live Copy desde uno o varios recursos o carpetas de origen, siga uno de los siguientes pasos:

* Método 1: Seleccione los recursos de origen y haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]** en la barra de herramientas de la parte superior.
* Método 2: En [!DNL Experience Manager] interfaz de usuario, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]** desde la esquina superior derecha de la interfaz.

Puede crear Live Copies de un recurso o de una carpeta de a una. Puede crear Live Copies que se deriven de un recurso o de una carpeta que sea una Live Copy en sí. Los fragmentos de contenido (CF) no son compatibles con el caso de uso. Al intentar crear sus Live Copies, los CF se copian tal cual sin ninguna relación. Los CF copiados son una instantánea a tiempo y no se actualizan cuando se actualizan los CF originales.

Para crear Live Copies con el primer método, siga estos pasos:

1. Seleccione los recursos o carpetas de origen. En la barra de herramientas, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]**.

   ![Crear Live Copy desde [!DNL Experience Manager] interfaz](assets/create_lc1.png)

   *Figura: Crear Live Copy desde [!DNL Experience Manager] interfaz.*

1. Seleccione una carpeta de destino. Haga clic en **[!UICONTROL Siguiente]**. 
1. Proporcione título y nombre. Los activos no tienen elementos secundarios. Al crear una Live Copy de carpetas, puede elegir incluir o excluir elementos secundarios.
1. Seleccione una configuración de lanzamiento. Haga clic en **[!UICONTROL Crear]**.

Para crear Live Copies con el segundo método, siga estos pasos:

1. En [!DNL Experience Manager] interfaz, en la esquina superior derecha, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]**.

   ![Crear Live Copy desde [!DNL Experience Manager] interfaz](assets/create_lc2.png)

   *Figura: Crear Live Copy desde [!DNL Experience Manager] interfaz.*

1. Seleccione la carpeta o el recurso de origen. Haga clic en **[!UICONTROL Siguiente]**. 
1. Seleccione la carpeta de destino. Haga clic en **[!UICONTROL Siguiente]**. 
1. Proporcione título y nombre. Los activos no tienen elementos secundarios. Al crear una Live Copy de carpetas, puede elegir incluir o excluir elementos secundarios.
1. Seleccione una configuración de lanzamiento. Haga clic en **[!UICONTROL Crear]**.

>[!NOTE]
>
>Cuando se mueve un origen o una Live Copy, las relaciones se conservan. Cuando se elimina una Live Copy, se eliminan las relaciones.

## Ver varias propiedades y estados del origen y la Live Copy {#properties}

Puede ver la información y los estados relacionados con MSM de Live Copy, como la relación, la sincronización, los lanzamientos, etc., desde las distintas áreas de la [!DNL Experience Manager] interfaz de usuario.

Los dos métodos siguientes funcionan para los recursos y las carpetas:

* Seleccione un recurso de Live Copy y busque la información en su página Propiedades.
* Seleccione la carpeta de origen y busque la información detallada de cada Live Copy desde el [!UICONTROL Consola Live Copy].

>[!TIP]
>
>Para comprobar el estado de algunas Live Copies independientes, utilice el primer método para comprobar el **[!UICONTROL Propiedades]** página. Para comprobar los estados de muchas Live Copies, utilice el segundo método para comprobar el **[!UICONTROL Estado de la relación]** página.

### Información y estado de una Live Copy {#status-lc-asset}

Para comprobar la información y los estados de un recurso de Live Copy o de una carpeta, siga estos pasos.

1. Seleccione un recurso de Live Copy o una carpeta. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar la combinación de teclas `p`.
1. Haga clic en **[!UICONTROL Live Copy]**. Puede comprobar la ruta del origen, el estado de la suspensión, el estado de la sincronización, la última fecha de lanzamiento y el usuario que realizó la última implementación.

   ![La información y los estados de Live Copy se muestran en una consola en Propiedades](assets/lcfolder_info_properties.png)

   *Figura: Información y estados de Live Copy.*

1. Puede habilitar o deshabilitar si los recursos secundarios piden prestado la configuración de Live Copy.

1. Puede elegir la opción de la Live Copy para heredar la configuración de lanzamiento del elemento principal o cambiar la configuración.

### Información y estados de todas las Live Copies de una carpeta {#status-lc-folder}

[!DNL Experience Manager] proporciona una consola para comprobar los estados de todas las Live Copies de una carpeta de origen. Esta consola muestra el estado de todos los recursos secundarios.

1. Seleccione una carpeta de origen. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar la combinación de teclas `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Para abrir la consola, haga clic en **[!UICONTROL Descripción general de Live Copy]**. Este tablero proporciona un estado de nivel superior de todos los recursos secundarios.

   ![Ver estados de Live Copy en la consola de origen de Live Copy](assets/livecopy-statuses.png)

   *Figura: Ver estados de Live Copies en [!UICONTROL Consola Live Copy] de origen.*

1. Para ver la información detallada sobre cada recurso en la carpeta Live Copy, seleccione un recurso y haga clic en **[!UICONTROL Estado de relación]** en la barra de herramientas.

   ![Información detallada y estado de un recurso secundario de Live Copy en una carpeta](assets/livecopy_relationship_status.png)

   Información detallada y estado de un recurso secundario de Live Copy en una carpeta

>[!TIP]
>
>Puede ver rápidamente los estados de las Live Copies de otras carpetas sin tener que examinar demasiado. Cambie la carpeta de la parte superior media de la **[!UICONTROL Información general de Live Copy]** interfaz.

### Acciones rápidas del carril Referencias para el origen {#ref-rail-source}

Para un recurso o carpeta de origen, puede ver la siguiente información y realizar las siguientes acciones directamente desde el carril Referencias:

* Consulte las rutas de las Live Copies.
* Abrir o mostrar una Live Copy específica en [!DNL Experience Manager] interfaz de usuario.
* Sincronice las actualizaciones con una Live Copy específica.
* Suspenda la relación o cambie la configuración de lanzamiento para una Live Copy específica.
* Acceda a la consola de información general de Live Copy.

Seleccione la carpeta o el recurso de origen, abra el carril izquierdo y haga clic en **[!UICONTROL Referencias]**. También puede seleccionar un recurso o una carpeta y utilizar la combinación de teclas `Alt + 4`. 

![Acciones e información disponible en el carril Referencias para el origen seleccionado](assets/referencerail_source.png)

*Figura: Acciones e información disponible en el carril Referencias para el origen seleccionado.*

Para una Live Copy específica, haga clic en **[!UICONTROL Editar Live Copy]** para suspender la relación o cambiar la configuración de lanzamiento.

![Para una Live Copy específica, se puede acceder a la opción de suspender la relación o cambiar la configuración de lanzamiento desde el carril Referencias cuando se selecciona el recurso de origen](assets/referencerail_editlc_options.png)

*Figura: Suspenda la relación o cambie la configuración de lanzamiento de una Live Copy específica.*

### Acciones rápidas del carril Referencias para la Live Copy {#ref-rail-lc}

Para una carpeta o un recurso de Live Copy, puede ver la siguiente información y realizar las siguientes acciones directamente desde el carril Referencias:

* Consulte la ruta de su origen.
* Abrir o mostrar una Live Copy específica en [!DNL Experience Manager] interfaz de usuario.
* Despliegue las actualizaciones.

Seleccione una carpeta o un recurso de Live Copy, abra el carril izquierdo y haga clic en **[!UICONTROL Referencias]**. También puede seleccionar un recurso o una carpeta y utilizar la combinación de teclas `Alt + 4`. 

![Acciones disponibles en el carril Referencias para la Live Copy seleccionada](assets/referencerail_livecopy.png)

*Figura: Acciones disponibles en el carril Referencias para la Live Copy seleccionada.*

## Propagación de modificaciones del origen a Live Copies {#rollout-sync}

Una vez modificado el origen, los cambios se pueden propagar a las Live Copies mediante una acción de sincronización o de despliegue. Para comprender la diferencia entre ambas acciones, consulte [glosario](#glossary).

### Acción de despliegue {#rollout}

Puede iniciar una acción de despliegue desde el recurso de origen y actualizar todas o algunas Live Copies seleccionadas.

1. Seleccione un recurso de Live Copy o una carpeta. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar la combinación de teclas `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Haga clic en **[!UICONTROL Despliegue]** en la barra de herramientas.
1. Seleccione las Live Copies que desee actualizar. Haga clic en **[!UICONTROL Despliegue]**.
1. Para implementar las actualizaciones realizadas en los recursos secundarios, seleccione **[!UICONTROL Implementar la fuente y todos los elementos secundarios]**.

   ![Implementar las modificaciones del origen en algunas o todas las Live Copies](assets/livecopy_rollout_page.png)

   *Figura: Lleve a cabo las modificaciones del origen en algunas o en todas las Live Copies.*

>[!NOTE]
>
>Las modificaciones realizadas en un recurso de origen solo se implementan en las Live Copies directamente relacionadas. Si una Live Copy se deriva de otra Live Copy, las modificaciones no se implementan en la Live Copy derivada.

Como alternativa, puede iniciar una acción de despliegue desde el carril Referencias después de seleccionar una Live Copy específica. Para obtener más información, consulte [Acciones rápidas del carril Referencias para la Live Copy](#ref-rail-lc). En este método de implementación, solo se actualizan la Live Copy seleccionada y, opcionalmente, sus elementos secundarios.

![Implementar las modificaciones del origen en la Live Copy seleccionada](assets/livecopy_rollout_dialog.png)

*Figura: Despliegue las modificaciones del origen en la Live Copy seleccionada.*

### Acerca de la acción de sincronización {#about-sync}

Una acción de sincronización extrae las modificaciones de un origen solo a la Live Copy seleccionada. La acción de sincronización respeta y mantiene las modificaciones locales realizadas después de cancelar la herencia. Las modificaciones locales no se sobrescriben y la herencia cancelada no se restablece. Puede iniciar una acción de sincronización de tres formas.

| Donde [!DNL Experience Manager] interfaz | Cuándo y por qué utilizar | Utilización |
|---|---|---|
| [!UICONTROL Referencias] carril | Sincronice rápidamente cuando ya tenga seleccionado el origen. | Consulte [Acciones rápidas del carril Referencias para el origen](#ref-rail-source) |
| Barra de herramientas de [!UICONTROL Propiedades] página | Inicie una sincronización cuando ya tenga abiertas las propiedades de Live Copy. | Consulte [Sincronizar una Live Copy](#sync-lc) |
| [!UICONTROL Información general de Live Copy] consola | Sincronice rápidamente varios recursos (no necesariamente todos) cuando la carpeta de origen esté seleccionada o [!UICONTROL Información general de Live Copy] la consola ya está abierta. La acción de sincronización se inicia para un recurso a la vez, pero es una forma más rápida de sincronizar varios recursos de una sola vez. | Consulte [Acciones sobre muchos recursos de una carpeta de Live Copy](#bulk-actions) |

### Sincronizar una Live Copy {#sync-lc}

Para iniciar una acción de sincronización, abra la página **[!UICONTROL Propiedades]** de una Live Copy, haga clic en **[!UICONTROL Live Copy]** y, a continuación, seleccione la acción que desee en la barra de herramientas.

Para ver los estados y la información relacionados con una acción de sincronización, consulte [Información y estado de una Live Copy](#status-lc-asset) e [Información y estados de todas las Live Copy de una carpeta](#status-lc-folder).

![La acción Sincronizar extrae los cambios realizados en el origen](assets/livecopy_sync.png)

*Figura: La acción Sincronizar extrae los cambios realizados en el origen.*

>[!NOTE]
>
>Si la relación está suspendida, la acción de sincronización no está disponible en la barra de herramientas. Mientras que la acción de sincronización está disponible en el carril Referencias, las modificaciones no se propagan aunque la implementación se haya realizado correctamente.

## Suspender y reanudar la relación {#suspend-resume}

Puede suspender temporalmente la relación para evitar que una Live Copy reciba las modificaciones realizadas en la carpeta o el recurso de origen. La relación también se puede reanudar para que Live Copy empiece a recibir las modificaciones del origen.

Para suspender o reanudar, abra la página **[!UICONTROL Propiedades]** de una Live Copy, haga clic en **[!UICONTROL Live Copy]** y seleccione la acción que desee en la barra de herramientas.

También puede suspender o reanudar rápidamente las relaciones de varios recursos en una carpeta de Live Copy desde la consola **[!UICONTROL Información general de Live Copy]**. Consulte [Realizar acciones en varios recursos de las carpetas de Live Copy](#bulk-actions).

## Realizar modificaciones locales en una Live Copy {#local-mods}

Una Live Copy es una réplica del origen original cuando se crea. Los valores de metadatos de una Live Copy se heredan del origen. Los campos de metadatos mantienen individualmente la herencia con los respectivos campos del recurso de origen.

Sin embargo, tiene la flexibilidad de realizar modificaciones locales en una Live Copy para cambiar algunas propiedades seleccionadas. Para realizar modificaciones locales, cancele la herencia de la propiedad deseada. Cuando se cancela la herencia de uno o varios campos de metadatos, se conserva la relación activa del recurso y la herencia de los demás campos de metadatos. Cualquier sincronización o implementación no sobrescribe las modificaciones locales. Para ello, abra **[!UICONTROL Propiedades]** página de un recurso de Live Copy, haga clic en el botón **[!UICONTROL cancelar herencia]** junto a un campo de metadatos.

Puede deshacer todas las modificaciones locales y revertir el recurso al estado de su origen. La acción Restablecer anula de forma irrevocable e instantánea todas las modificaciones locales y restablece la herencia en todos los campos de metadatos. Para revertir, desde el **[!UICONTROL Propiedades]** página de un recurso de Live Copy, haga clic en **[!UICONTROL Restablecer]** en la barra de herramientas.

![La acción Restablecer sobrescribe las ediciones locales y trae la Live Copy en parte con su origen.](assets/livecopy_reset.png)

*Figura: La acción Restablecer sobrescribe las ediciones locales y trae la Live Copy en parte con su origen.*

## Quitar relación activa {#detach}

Puede eliminar completamente la relación entre un origen y una Live Copy mediante la acción Separar. La Live Copy se convierte en un recurso independiente o en una carpeta después de separarse. Se muestra como un nuevo recurso en [!DNL Experience Manager] , inmediatamente después de la desconexión. Para separar una Live Copy de su origen, siga estos pasos.

1. Seleccione una carpeta o un recurso de Live Copy. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar la combinación de teclas `p`.

1. Haga clic en **[!UICONTROL Live Copy]**. Haga clic en **[!UICONTROL Desasociar]** en la barra de herramientas. Haga clic en **[!UICONTROL Desasociar]** del cuadro de diálogo presentado.

   ![La acción Separar elimina completamente la relación entre el origen y la Live Copy](assets/livecopy_detach.png)

   *Figura: La acción Separar elimina completamente la relación entre el origen y la Live Copy.*

   >[!CAUTION]
   >
   >La relación se elimina inmediatamente al hacer clic en **[!UICONTROL Desasociar]** del cuadro de diálogo. No se puede deshacer haciendo clic en **[!UICONTROL Cancelar]** en la página Propiedades.

Como alternativa, puede separar rápidamente varios recursos de una carpeta de Live Copy de la **[!UICONTROL Información general de Live Copy]** consola. Consulte [Realizar acciones en varios recursos de las carpetas de Live Copy](#bulk-actions).

## Acciones masivas en una carpeta de Live Copy {#bulk-actions}

Si tiene varios recursos en una carpeta de Live Copy, iniciar acciones en cada recurso puede ser tedioso. Puede iniciar rápidamente las acciones básicas en muchos recursos desde [!UICONTROL Consola Live Copy]. Los métodos anteriores siguen funcionando con recursos individuales.

1. Seleccione una carpeta de origen. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar la combinación de teclas `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Para abrir la consola, haga clic en **[!UICONTROL Descripción general de Live Copy]**.
1. En este tablero, seleccione un recurso de Live Copy de una carpeta de Live Copy. Haga clic en las acciones que desee en la barra de herramientas. Las acciones disponibles son **[!UICONTROL Sincronizar]**, **[!UICONTROL Restablecer]**, **[!UICONTROL Suspender]** y **[!UICONTROL Desconectar]**. Puede iniciar rápidamente estas acciones en cualquier recurso en cualquier número de carpetas de Live Copy que estén en relación activa con la carpeta de origen seleccionada.

   ![Actualice fácilmente muchos recursos en carpetas de Live Copy desde la consola Información general de Live Copy](assets/livecopyconsole_update_many_assets.png)

   *Figura: Actualice fácilmente muchos recursos en carpetas de Live Copy desde la [!UICONTROL Información general de Live Copy] consola.*

<!-- TBD: Can MSM be extended using Java APIs in CS?

## Extend MSM for [!DNL Assets] {#extend-api}

[!DNL Experience Manager] lets you extend the functionality using the MSM Java APIs. For [!DNL Assets], the extending works just the same as it works with MSM for [!DNL Sites]. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Create a synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

-->

## Impacto de las tareas de administración de recursos en Live Copies {#manage-assets}

Las Live Copies y los orígenes son recursos o carpetas que se pueden administrar, en cierta medida, como recursos digitales. Algunas tareas de administración de recursos en [!DNL Experience Manager] tienen un impacto específico en las Live Copies.

* Al copiar una Live Copy, se crea un recurso de Live Copy con el mismo origen que la primera Live Copy.
* Al mover un origen o su Live Copy, se conserva la relación activa.
* La acción Editar no funciona para los recursos de Live Copy. Si la fuente de una Live Copy es una Live Copy en sí misma, la acción de edición no funciona para ella.
* La acción de desprotección no está disponible para los recursos de Live Copy.
* Para la carpeta de origen, está disponible la opción para crear tareas de revisión.
* Al ver el listado de recursos en la vista de lista y la vista de columna, un recurso de Live Copy o una carpeta muestra &quot;Live Copy&quot; en su contra. Ayuda a identificar fácilmente las Live Copies en una carpeta.

## Comparar MSM para [!DNL Assets] y [!DNL Sites] {#comparison}

En más escenarios, MSM para [!DNL Assets] coincide con el comportamiento de la funcionalidad de MSM para sitios . Algunas diferencias clave a tener en cuenta son:

* Modelo en MSM para [!DNL Sites] se denomina origen de Live Copy en MSM para [!DNL Assets].
* En Sites, puede comparar un modelo y su Live Copy, pero no es posible en [!DNL Assets] para comparar una fuente con su Live Copy.
* No se puede editar una Live Copy en [!DNL Assets].
* Los sitios suelen tener hijos, pero [!DNL Assets] no. La opción para incluir o excluir elementos secundarios no está presente al crear copias activas de recursos individuales.
* MSM no admite la eliminación del paso capítulos en el asistente de creación de sitios para [!DNL Assets].
* MSM no admite la configuración de bloqueos MSM en propiedades de página para [!DNL Assets].
* Para MSM para [!DNL Assets], use solo la variable **[!UICONTROL Configuración de lanzamiento estándar]**. Las demás configuraciones de implementación no están disponibles para MSM para [!DNL Assets].

## Limitaciones y problemas conocidos de MSM para [!DNL Assets] {#limitations}

A continuación se indican las limitaciones de MSM para [!DNL Assets].

* Los fragmentos de contenido no son compatibles. Al intentar crear las Live Copies, los fragmentos de contenido se copian tal cual sin ninguna relación. Los fragmentos de contenido copiados son una instantánea a tiempo y no se actualizan cuando se actualizan los fragmentos de contenido originales.

* MSM no funciona con la reescritura de metadatos habilitada. Al reescribir, la herencia se rompe.
