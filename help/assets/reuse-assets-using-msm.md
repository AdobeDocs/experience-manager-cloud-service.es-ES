---
title: Reutilización de recursos mediante MSM
description: Utilice recursos en varias páginas o carpetas que se deriven de recursos principales y estén vinculadas a ellos. Los recursos permanecen sincronizados con una copia principal y, con unos pocos clics, reciben las actualizaciones de los recursos principales.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: a71aebdf-8e46-4c2d-8960-d188b14aaae9
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '3403'
ht-degree: 12%

---

# Reutilización de recursos mediante MSM para [!DNL Assets] {#reuse-assets-using-msm-for-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html) |
| AEM as a Cloud Service | Este artículo |

Funcionalidad de Administrador de varios sitios (MSM) en [!DNL Adobe Experience Manager] permite a los usuarios reutilizar contenido que se crea una vez y se reutiliza en varias ubicaciones web. La misma funcionalidad está disponible para los recursos digitales con el nombre MSM para [!DNL Assets]. Uso de MSM para [!DNL Assets], puede:

* Cree recursos una vez y luego haga copias de estos para reutilizarlos en otras áreas del sitio.
* Mantenga varias copias en sincronización y actualice la copia principal original una vez para insertar los cambios en las copias secundarias.
* Realice cambios locales suspendiendo temporal o permanentemente la vinculación entre los recursos principales y secundarios.

>[!NOTE]
>
>El MSM para [!DNL Assets] funcionalidad incluye fragmentos de contenido, que se almacenan como [!DNL Assets] (aunque se considera una función de Sites).

>[!CAUTION]
>
>MSM para fragmentos de contenido solo está disponible cuando se utilizan fragmentos de contenido a través de **[!UICONTROL Assets]** consola.
>
>La funcionalidad de MSM es *no* disponible al usar el **[!UICONTROL Fragmentos de contenido]** consola.

## Comprender las ventajas y los conceptos de MSM {#concepts}

### Cómo funciona y sus ventajas {#how-it-works-and-the-benefits}

Para comprender los escenarios de uso para reutilizar el mismo contenido (texto y recursos) en varias ubicaciones web, consulte [posibles escenarios de MSM](/help/sites-cloud/administering/msm/overview.md). [!DNL Experience Manager] mantiene un vínculo entre el recurso original y sus copias vinculadas, denominado Live Copies (LC). La vinculación mantenida permite insertar cambios centralizados en muchas Live Copies. Esto permite realizar actualizaciones más rápidas, pero elimina las limitaciones de administrar copias duplicadas. La propagación de cambios está libre de errores y centralizada. La funcionalidad permite espacio para actualizaciones que se limitan a copias en directo seleccionadas. Los usuarios pueden desasociar el vínculo, es decir, interrumpir la herencia, y realizar ediciones locales que no se sobrescriban la próxima vez que se actualice la copia principal y se implementen los cambios. La desasociación se puede realizar para algunos campos de metadatos seleccionados o para un recurso completo. Permite la flexibilidad para actualizar localmente los recursos que se heredan originalmente de una copia principal.

MSM mantiene una relación activa entre el recurso de origen y sus Live Copies para lo siguiente:

* Los cambios en los recursos de origen también se aplican (despliegan) a las Live Copies, es decir, las Live Copies se sincronizan con el origen.
* Puede actualizar las Live Copies suspendiendo la relación activa o eliminando la herencia para algunos campos limitados. Las modificaciones en el origen ya no se aplican a la Live Copy.

### Glosario de MSM para [!DNL Assets] condiciones {#glossary}

**Fuente:** Los recursos o carpetas originales. Copia principal de la que se derivan Live Copies.

**Live Copy:** La copia de los recursos o carpetas de origen que está en sincronización con su origen. Live Copies puede ser una fuente de Live Copies adicionales. Consulte cómo crear LC.

**Herencia:** Un vínculo o referencia entre un recurso o una carpeta de Live Copy y su origen que el sistema utiliza para recordar dónde enviar las actualizaciones. La herencia existe a nivel granular para los campos de metadatos, también para las variaciones y los campos de fragmentos de contenido. La herencia se puede eliminar para los elementos seleccionados al tiempo que se conserva la relación activa entre el origen y su Live Copy.

**Despliegue:** Una acción que inserta las modificaciones realizadas en el origen descendente en sus Live Copies. Es posible actualizar una o más Live Copies de una sola vez mediante la acción de despliegue. Consulte Despliegue.

**Configuración de despliegue:** Reglas que determinan qué propiedades se sincronizan, cómo y cuándo. Estas configuraciones se aplican al crear Live Copies, se pueden editar más adelante y un elemento secundario puede heredar la configuración de despliegue de su recurso principal. Para MSM para [!DNL Assets], utilice únicamente la configuración de despliegue estándar. Las demás configuraciones de despliegue no están disponibles para MSM para [!DNL Assets].

**Sincronizar:** Otra acción, además del despliegue, que iguala el origen y su Live Copy al enviar las actualizaciones del origen a Live Copies. Se inicia una sincronización para una Live Copy determinada y la acción extrae los cambios del origen. Con esta acción, solo es posible actualizar una de las Live Copies. Consulte Acción de sincronización.

**Suspender:** Elimine temporalmente la relación activa entre una Live Copy y su recurso o carpeta de origen. Puede reanudar la relación. Consulte acción de suspensión.

**Reanudar:** Reanudar la relación dinámica para que una Live Copy vuelva a recibir las actualizaciones del origen. Consulte Acción de reanudar.

**Restablecer:** La acción Restablecer vuelve a convertir la Live Copy en una réplica del origen al sobrescribir los cambios locales. También elimina las cancelaciones de herencia y restablece la herencia en todos los campos de metadatos. Para realizar modificaciones locales en el futuro, debe cancelar de nuevo la herencia de campos específicos. Consulte modificaciones locales de la LC.

**Desasociar:** Eliminar irrevocablemente la relación activa de un recurso o una carpeta de Live Copy. Después de la acción de desasociar, las Live Copies nunca podrán recibir actualizaciones del origen y dejarán de ser una Live Copy. Consulte Eliminar relación.

## Crear una Live Copy de un recurso {#create-livecopy}

Para crear una Live Copy a partir de uno o varios recursos o carpetas de origen, siga uno de estos procedimientos:

* Método 1: seleccionar los recursos de origen y hacer clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]** en la barra de herramientas de la parte superior.
* Método 2: en [!DNL Experience Manager] interfaz de usuario, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]** desde la esquina superior derecha de la interfaz.

Puede crear Live Copies de un recurso o una carpeta a la vez. Puede crear Live Copies que se deriven de un recurso o una carpeta que sea una Live Copy en sí.

Para crear Live Copies mediante el primer método, siga estos pasos:

1. Seleccione los recursos o carpetas de origen. En la barra de herramientas, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]**.

   ![Crear Live Copy desde [!DNL Experience Manager] interfaz](assets/create_lc1.png)

   *Imagen: creación de una Live Copy desde [!DNL Experience Manager] interfaz.*

1. Seleccione una carpeta de destino. Haga clic en **[!UICONTROL Siguiente]**.
1. Proporcione un título y un nombre. Los recursos no tienen tareas secundarias. Al crear una Live Copy de carpetas, puede elegir incluir o excluir elementos secundarios.
1. Seleccione una configuración de despliegue. Haga clic en **[!UICONTROL Crear]**.

Para crear Live Copies mediante el segundo método, siga estos pasos:

1. Entrada [!DNL Experience Manager] interfaz, en la esquina superior derecha, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]**.

   ![Crear Live Copy desde [!DNL Experience Manager] interfaz](assets/create_lc2.png)

   *Imagen: creación de una Live Copy desde [!DNL Experience Manager] interfaz.*

1. Seleccione el recurso o la carpeta de origen. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione la carpeta de destino. Haga clic en **[!UICONTROL Siguiente]**.
1. Proporcione un título y un nombre. Los recursos no tienen tareas secundarias. Al crear una Live Copy de carpetas, puede elegir incluir o excluir elementos secundarios.
1. Seleccione una configuración de despliegue. Haga clic en **[!UICONTROL Crear]**.

>[!NOTE]
>
>Cuando se mueve un origen o una Live Copy, las relaciones se conservan. Cuando se elimina una Live Copy, se eliminan las relaciones.

## Ver varias propiedades y estados de origen y Live Copy {#properties}

Puede ver la información y los estados relacionados con MSM de la Live Copy, como la relación, la sincronización, los despliegues y mucho más, desde las distintas áreas de la [!DNL Experience Manager] interfaz de usuario.

Los dos métodos siguientes funcionan para recursos y carpetas:

* Seleccione el recurso de Live Copy y busque la información en su página Propiedades.
* Seleccione la carpeta de origen y busque la información detallada de cada Live Copy en la [!UICONTROL Consola Live Copy].

>[!TIP]
>
>Para comprobar el estado de algunas Live Copies independientes, utilice el primer método para comprobar la **[!UICONTROL Propiedades]** página. Para comprobar los estados de muchas Live Copies, utilice el segundo método para comprobar las **[!UICONTROL Estado de relación]** página.

### Información y estado de una Live Copy {#status-lc-asset}

Para comprobar la información y los estados de un recurso de Live Copy o una carpeta, siga estos pasos.

1. Seleccione un recurso de Live Copy o una carpeta. Clic **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar el método abreviado de teclado `p`.
1. Clic **[!UICONTROL Live Copy]**. Puede comprobar la ruta del origen, el estado de suspensión, el estado de sincronización, la fecha del último despliegue y el usuario que realizó el último.

   ![La información y los estados de Live Copy se muestran en una consola en Propiedades](assets/lcfolder_info_properties.png)

   *Imagen: información y estados de Live Copy.*

1. Puede habilitar o deshabilitar si los recursos secundarios toman prestada la configuración de Live Copy.

1. Puede elegir la opción para que Live Copy herede la configuración de despliegue del elemento principal o cambie la configuración.

### Información y estados de todas las Live Copies de una carpeta {#status-lc-folder}

[!DNL Experience Manager] proporciona una consola para comprobar los estados de todas las Live Copies de una carpeta de origen. Esta consola muestra el estado de todos los recursos secundarios.

1. Seleccione una carpeta de origen. Clic **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Para abrir la consola, haga clic en **[!UICONTROL Descripción general de Live Copy]**. Este tablero proporciona un estado de nivel superior de todos los recursos secundarios.

   ![Ver los estados de las Live Copies en la consola Live Copy de origen](assets/livecopy-statuses.png)

   *Imagen: visualización de los estados de Live Copies en [!UICONTROL Consola Live Copy] de origen.*

1. Para ver la información detallada sobre cada recurso en la carpeta Live Copy, seleccione un recurso y haga clic en **[!UICONTROL Estado de relación]** en la barra de herramientas.

   ![Información detallada y estado de un recurso secundario de Live Copy en una carpeta](assets/livecopy_relationship_status.png)

   Información detallada y estado de un recurso secundario de Live Copy en una carpeta

>[!TIP]
>
>Puede ver rápidamente los estados de las Live Copies de otras carpetas sin tener que examinar demasiado. Cambie la carpeta desde la parte superior central del **[!UICONTROL Información general de Live Copy]** interfaz.

### Acciones rápidas del carril Referencias para el origen {#ref-rail-source}

Para un recurso o carpeta de origen, puede ver la siguiente información y realizar las siguientes acciones directamente desde el carril Referencias:

* Consulte las rutas de las Live Copies.
* Abra o muestre una Live Copy específica en [!DNL Experience Manager] interfaz de usuario.
* Sincronizar las actualizaciones con una Live Copy específica.
* Suspender la relación o cambiar la configuración de despliegue de una Live Copy específica.
* Acceda a la consola de información general de live copy.

Seleccione el recurso o la carpeta de origen, abra el carril izquierdo y haga clic en **[!UICONTROL Referencias]**. También puede seleccionar un recurso o una carpeta y utilizar la combinación de teclas `Alt + 4`. 

![Acciones e información disponible en el carril Referencias para la fuente seleccionada](assets/referencerail_source.png)

*Imagen: acciones e información disponible en el carril Referencias de la fuente seleccionada.*

Para una Live Copy específica, haga clic en **[!UICONTROL Editar Live Copy]** para suspender la relación o cambiar la configuración de despliegue.

![Para una Live Copy específica, la opción para suspender la relación o cambiar la configuración de despliegue es accesible desde el carril Referencias cuando se selecciona el recurso de origen](assets/referencerail_editlc_options.png)

*Imagen: suspensión de una relación o cambio de la configuración de despliegue de una Live Copy específica.*

### Acciones rápidas del carril Referencias para la Live Copy {#ref-rail-lc}

Para un recurso o una carpeta de Live Copy, puede ver la siguiente información y realizar las siguientes acciones directamente desde el carril Referencias:

* Consulte la ruta de su origen.
* Abra o muestre una Live Copy específica en [!DNL Experience Manager] interfaz de usuario.
* Despliegue las actualizaciones.

Seleccione una carpeta o un recurso de Live Copy, abra el carril izquierdo y haga clic en **[!UICONTROL Referencias]**. También puede seleccionar un recurso o una carpeta y utilizar la combinación de teclas `Alt + 4`. 

![Acciones disponibles en el carril Referencias para la Live Copy seleccionada](assets/referencerail_livecopy.png)

*Imagen: acciones disponibles en el carril Referencias para la Live Copy seleccionada.*

## Propagación de modificaciones desde el origen a Live Copies {#rollout-sync}

Una vez modificado un origen, los cambios se pueden propagar a las Live Copies mediante una acción de sincronización o de despliegue. Para comprender la diferencia entre ambas acciones, consulte [glosario](#glossary).

### Acción de despliegue {#rollout}

Puede iniciar una acción de despliegue desde el recurso de origen y actualizar todas las Live Copies o algunas.

1. Seleccione un recurso de Live Copy o una carpeta. Clic **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Clic **[!UICONTROL Despliegue]** en la barra de herramientas.
1. Seleccione las Live Copies que desee actualizar. Clic **[!UICONTROL Despliegue]**.
1. Para desplegar las actualizaciones realizadas en los recursos secundarios, seleccione **[!UICONTROL Desplegar origen y elementos secundarios]**.

   ![Desplegar las modificaciones del origen en unas pocas o en todas las Live Copies](assets/livecopy_rollout_page.png)

   *Imagen: implementación de las modificaciones del origen en algunas o en todas las Live Copies.*

>[!NOTE]
>
>Las modificaciones realizadas en un recurso de origen solo se implementan en las Live Copies directamente relacionadas. Si una Live Copy se deriva de otra Live Copy, las modificaciones no se implementan en la Live Copy derivada.

También puede iniciar una acción de despliegue desde el carril Referencias después de seleccionar una Live Copy específica. Para obtener más información, consulte [Acciones rápidas del carril Referencias para la Live Copy](#ref-rail-lc). En este método de despliegue, solo se actualiza la Live Copy seleccionada y, opcionalmente, sus elementos secundarios.

![Desplegar las modificaciones del origen en la Live Copy seleccionada](assets/livecopy_rollout_dialog.png)

*Imagen: despliegue de las modificaciones del origen en la Live Copy seleccionada.*

### Acerca de la acción sincronizar {#about-sync}

Una acción de sincronización extrae las modificaciones de un origen solo para la Live Copy seleccionada. La acción de sincronización respeta y mantiene las modificaciones locales realizadas después de cancelar la herencia. Las modificaciones locales no se sobrescriben y la herencia cancelada no se restablece. Puede iniciar una acción de sincronización de tres formas.

| Dónde en [!DNL Experience Manager] interfaz | Cuándo y por qué utilizar | Utilización |
|---|---|---|
| [!UICONTROL Referencias] carril | Sincronice rápidamente cuando ya tenga seleccionado el origen. | Consulte [Acciones rápidas del carril Referencias para el origen](#ref-rail-source) |
| Barra de herramientas en [!UICONTROL Propiedades] página | Inicie una sincronización cuando ya tenga abiertas las propiedades de Live Copy. | Consulte [Sincronización de una Live Copy](#sync-lc) |
| [!UICONTROL Información general de Live Copy] consolar | Sincronizar rápidamente varios recursos (no necesariamente todos) cuando se selecciona la carpeta de origen o [!UICONTROL Información general de Live Copy] La consola de ya está abierta. La acción de sincronización se inicia para un recurso a la vez, pero es una forma más rápida de realizar la sincronización de varios recursos de una sola vez. | Consulte [Acciones en varios recursos de una carpeta de Live Copy](#bulk-actions) |

### Sincronización de una Live Copy {#sync-lc}

Para iniciar una acción de sincronización, abra la página **[!UICONTROL Propiedades]** de una Live Copy, haga clic en **[!UICONTROL Live Copy]** y, a continuación, seleccione la acción que desee en la barra de herramientas.

Para ver los estados y la información relacionados con una acción de sincronización, consulte [Información y estado de una Live Copy](#status-lc-asset) e [Información y estados de todas las Live Copy de una carpeta](#status-lc-folder).

![La acción Sincronizar extrae los cambios realizados en el origen](assets/livecopy_sync.png)

*Imagen: la acción Sincronizar extrae los cambios realizados en el origen.*

>[!NOTE]
>
>Si la relación está suspendida, la acción de sincronización no está disponible en la barra de herramientas. Mientras que la acción de sincronización está disponible en el carril Referencias, las modificaciones no se propagan ni siquiera tras un despliegue correcto.

## Cancelar y volver a habilitar la herencia para elementos individuales {#canceling-reenabling-inheritance-individual-items}

Puede cancelar la herencia de Live Copy para un:

* campo de metadatos
* Variación de fragmento de contenido
* Campo de datos del fragmento de contenido

Esto significa que el elemento ya no está sincronizado con el componente de origen. Si es necesario, puede habilitar la herencia en un momento posterior.

### Cancelar herencia {#cancel-inheritance}

Para cancelar la herencia:

1. Seleccione el **Cancelar herencia** junto al elemento requerido:

   ![La acción Sincronizar extrae los cambios realizados en el origen](assets/cancel-inheritance-icon.png)

1. En el cuadro de diálogo Cancelar herencia, confirme la acción con Sí.

### Volver a habilitar la herencia {#reenable-inheritance}

Para volver a habilitar la herencia:

1. Para habilitar la herencia para un elemento, seleccione la **Volver a habilitar la herencia** junto al elemento requerido:

   ![La acción Sincronizar extrae los cambios realizados en el origen](assets/re-enable-inheritance-icon.png)

   >[!NOTE]
   >
   >Al volver a habilitar la herencia, el elemento no se sincroniza automáticamente con el origen. Puede solicitar manualmente una sincronización si es necesario.

## Suspender y reanudar la relación {#suspend-resume}

Puede suspender temporalmente la relación para evitar que una Live Copy reciba modificaciones realizadas en el recurso o la carpeta de origen. La relación también se puede reanudar para que Live Copy empiece a recibir las modificaciones del origen.

Para suspender o reanudar, abra la página **[!UICONTROL Propiedades]** de una Live Copy, haga clic en **[!UICONTROL Live Copy]** y seleccione la acción que desee en la barra de herramientas.

También puede suspender o reanudar rápidamente las relaciones de varios recursos en una carpeta de Live Copy desde la consola **[!UICONTROL Información general de Live Copy]**. Consulte [Realizar acciones en varios recursos de las carpetas de Live Copy](#bulk-actions).

## Realización de modificaciones locales en una Live Copy {#local-mods}

Una Live Copy es una réplica del origen original cuando se crea. Los valores de metadatos de una Live Copy se heredan del origen. Los campos de metadatos mantienen individualmente la herencia con los campos respectivos del recurso de origen.

Sin embargo, tiene la flexibilidad de realizar modificaciones locales en una Live Copy para cambiar algunas propiedades seleccionadas. Para realizar modificaciones locales, cancele la herencia de la propiedad deseada. Cuando se cancela la herencia de uno o varios campos de metadatos, se conserva la relación activa del recurso y la herencia de los demás campos de metadatos. Cualquier sincronización o implementación no sobrescribe las modificaciones locales. Para ello, abra **[!UICONTROL Propiedades]** de un recurso de live copy, haga clic en **[!UICONTROL cancelar herencia]** junto a un campo de metadatos.

Puede deshacer todas las modificaciones locales y revertir el recurso al estado de su origen. La acción Restablecer anula de forma irrevocable e instantánea todas las modificaciones locales y restablece la herencia en todos los campos de metadatos. Para volver, en **[!UICONTROL Propiedades]** página de un recurso de live copy, haga clic en **[!UICONTROL Restablecer]** en la barra de herramientas.

![La acción Restablecer sobrescribe las ediciones locales y trae la Live Copy en parte con su origen.](assets/livecopy_reset.png)

*Imagen: la acción Restablecer sobrescribe las ediciones locales y trae la Live Copy en parte con su origen.*

## Quitar relación activa {#detach}

Puede eliminar por completo la relación entre un origen y una Live Copy mediante la acción Desasociar. La Live Copy se convierte en un recurso o carpeta independiente después de desasociarse. Se muestra como un nuevo recurso en [!DNL Experience Manager] interfaz, inmediatamente después de la desconexión. Para separar una Live Copy de su origen, siga estos pasos.

1. Seleccione una carpeta o un recurso de Live Copy. Clic **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar el método abreviado de teclado `p`.

1. Clic **[!UICONTROL Live Copy]**. Clic **[!UICONTROL Desasociar]** en la barra de herramientas. Clic **[!UICONTROL Desasociar]** del cuadro de diálogo presentado.

   ![La acción Desasociar elimina completamente la relación entre el origen y la Live Copy](assets/livecopy_detach.png)

   *Imagen: la acción Desasociar elimina completamente la relación entre el origen y la Live Copy.*

   >[!CAUTION]
   >
   >La relación se elimina inmediatamente al hacer clic en **[!UICONTROL Desasociar]** del cuadro de diálogo. No puede deshacer esta acción haciendo clic en **[!UICONTROL Cancelar]** en la página Propiedades.

También puede desasociar rápidamente varios recursos de una carpeta de Live Copy del **[!UICONTROL Información general de Live Copy]** consola. Consulte [Realizar acciones en varios recursos de las carpetas de Live Copy](#bulk-actions).

## Acciones masivas en una carpeta de Live Copy {#bulk-actions}

Si tiene varios recursos en una carpeta de Live Copy, iniciar acciones en cada recurso puede resultar tedioso. Puede iniciar rápidamente las acciones básicas en muchos recursos desde [!UICONTROL Consola Live Copy]. Los métodos anteriores siguen funcionando para recursos individuales.

1. Seleccione una carpeta de origen. Clic **[!UICONTROL Propiedades]** en la barra de herramientas. También puede utilizar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Para abrir la consola, haga clic en **[!UICONTROL Descripción general de Live Copy]**.
1. En este tablero, seleccione un recurso de Live Copy de una carpeta de Live Copy. Haga clic en las acciones que desee en la barra de herramientas. Las acciones disponibles son **[!UICONTROL Sincronizar]**, **[!UICONTROL Restablecer]**, **[!UICONTROL Suspender]** y **[!UICONTROL Desconectar]**. Puede iniciar rápidamente estas acciones en cualquier recurso de cualquier número de carpetas de Live Copy que estén en una relación activa con la carpeta de origen seleccionada.

   ![Actualice fácilmente muchos recursos en carpetas de Live Copy desde la consola Información general de Live Copy](assets/livecopyconsole_update_many_assets.png)

   *Imagen: actualice fácilmente muchos recursos en carpetas de Live Copy desde [!UICONTROL Información general de Live Copy] consola.*

<!-- TBD: Can MSM be extended using Java APIs in CS?

## Extend MSM for [!DNL Assets] {#extend-api}

[!DNL Experience Manager] lets you extend the functionality using the MSM Java APIs. For [!DNL Assets], the extending works just the same as it works with MSM for [!DNL Sites]. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Create a synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

-->

## Impacto de las tareas de administración de recursos en Live Copies {#manage-assets}

Las Live Copies y fuentes son recursos o carpetas que se pueden administrar, en cierta medida, como recursos digitales. Algunas tareas de administración de recursos en [!DNL Experience Manager] tener un impacto específico en live copies.

* Al copiar una Live Copy, se crea un recurso de Live Copy con el mismo origen que la primera Live Copy.
* Cuando mueve un origen o su Live Copy, la relación dinámica se conserva.
* La acción de edición no funciona para los recursos de Live Copy. Si el origen de una Live Copy es una Live Copy en sí misma, la acción de edición no funciona para ella.
* La acción de desprotección no está disponible para los recursos de Live Copy.
* Para la carpeta de origen, está disponible la opción para crear tareas de revisión.
* Al ver la lista de recursos en la vista de lista y la vista de columna, un recurso o carpeta de Live Copy muestra &quot;Live Copy&quot; en relación con ella. Ayuda a identificar fácilmente las Live Copies de una carpeta.

## Comparar MSM con [!DNL Assets] y [!DNL Sites] {#comparison}

En más escenarios, MSM para [!DNL Assets] coincide con el comportamiento de MSM para la funcionalidad de Sites. Algunas diferencias clave que hay que tener en cuenta son:

* Modelo en MSM para [!DNL Sites] se denomina origen de Live Copy en MSM para [!DNL Assets].
* En Sites, puede comparar un modelo y su Live Copy, pero no es posible en [!DNL Assets] para comparar un origen con su live copy.
* No se puede editar una Live Copy en [!DNL Assets].
* Los sitios suelen tener hijos, pero [!DNL Assets] no lo haga. La opción para incluir o excluir elementos secundarios no está presente al crear Live Copies de recursos individuales.
* MSM no admite la eliminación del paso de capítulos del asistente para crear sitios para [!DNL Assets].
* MSM no admite la configuración de bloqueos de MSM en propiedades de página para [!DNL Assets].
* Para MSM para [!DNL Assets], use solo el **[!UICONTROL Configuración de despliegue estándar]**. Las demás configuraciones de despliegue no están disponibles para MSM para [!DNL Assets].

>[!NOTE]
>
>Recuerde que MSM para fragmentos de contenido (al que se accede a través de la variable **[!UICONTROL Assets]** ) utiliza la funcionalidad Recursos, ya que se almacenan como Recursos (aunque se consideran una función de Sites).

## Limitaciones y problemas conocidos de MSM para [!DNL Assets] {#limitations}

A continuación se indican algunas limitaciones de MSM para [!DNL Assets].

* MSM no funciona con la reescritura de metadatos habilitada. Tras la reescritura, la herencia se interrumpe.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
