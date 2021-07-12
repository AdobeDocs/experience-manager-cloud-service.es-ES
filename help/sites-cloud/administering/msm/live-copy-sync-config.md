---
title: Configuración de la sincronización de Live Copy
description: Obtenga información sobre las potentes opciones de sincronización de Live Copy disponibles y cómo puede configurarlas y personalizarlas según las necesidades de su proyecto.
feature: Administrador de varios sitios
role: Admin
exl-id: 0c97652c-edac-436e-9b5b-58000bccf534
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 29%

---

# Configuración de la sincronización de Live Copy {#configuring-live-copy-synchronization}

Adobe Experience Manager proporciona una serie de configuraciones de sincronización listas para usar. Antes de usar Live Copies, debe tener en cuenta lo siguiente para definir cómo y cuándo se sincronizan las Live Copies con su contenido de origen.

1. Decida si las configuraciones de lanzamiento existentes cumplen los requisitos
1. Si las configuraciones de lanzamiento existentes no lo hacen, decida si necesita crear las suyas.
1. Especifique las opciones de configuración de lanzamiento que se utilizarán para las Live Copies.

## Opciones de configuración de lanzamiento personalizadas e instaladas {#installed-and-custom-rollout-configurations}

Esta sección proporciona información sobre las opciones de configuración de lanzamiento instaladas y las acciones de sincronización que utilizan, así como información para crear opciones de configuración personalizadas si es necesario.

>[!CAUTION]
>
>Se recomienda actualizar o cambiar una configuración de lanzamiento predeterminada **no**. Si hay un requisito para una acción en directo personalizada, debe agregarse en una configuración de lanzamiento personalizada.

### Activadores de lanzamiento {#rollout-triggers}

Cada configuración de lanzamiento utiliza un activador de lanzamiento que hace que se produzca el lanzamiento. En las opciones de configuración de lanzamiento se puede utilizar uno de los siguientes activadores:

* **Al despliegue**: El  **** comando Desplegar se utiliza en la página de impresión azul o el comando  **** Sincronizar se utiliza en la página Live Copy.
* **En la modificación**: la página de origen se modifica.
* **En la activación**: la página de origen se activa.
* **En la desactivación**: la página de origen se desactiva.

>[!NOTE]
>
>El uso del déclencheur **On Modification** puede afectar al rendimiento. Consulte [las prácticas recomendadas de MSM](best-practices.md#onmodify) para obtener más información.

### Opciones de configuración del lanzamiento {#rollout-configurations}

En la tabla siguiente se enumeran las configuraciones de lanzamiento que se proporcionan de forma predeterminada con AEM. La tabla incluye las acciones de activación y sincronización de cada configuración de lanzamiento.

<!--
If the installed rollout configuration actions do not meet your requirements, you can [create a new rollout configuration](#creating-a-rollout-configuration).
-->

| Nombre | Descripción | Activador | [Acciones de sincronización](#synchronization-actions) |
|---|---|---|---|
| Configuración de lanzamiento estándar | La configuración de lanzamiento estándar permite iniciar procesos de lanzamiento con el activador de lanzamientos, y ejecuta acciones como crear, actualizar, eliminar contenido y ordenar nodos secundarios | En el lanzamiento | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`productUpdate`<br>`orderChildren` |
| Activar si se activa el modelo | Publica Live Copy cuando se publica el origen | En la activación | `targetActivate` |
| Desactivar si se desactiva el modelo | Desactiva Live Copy cuando se desactiva el origen | Al desactivar | `targetDeactivate` |
| Insertar al modificar | Inserta el contenido en Live Copy cuando se modifica el origen<br>Utilice esta configuración de lanzamiento con moderación, ya que utiliza el déclencheur On Modification. | En la modificación | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren` |
| Insertar al modificar (superficial) | Inserta contenido en Live Copy cuando se modifica la página del modelo sin actualizar referencias (por ejemplo, para copias superficiales)<br>Utilice esta configuración de lanzamiento con moderación, ya que utiliza el déclencheur On Modification. | En la modificación | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`orderChildren` |
| Lanzamiento de promoción | Configuración del lanzamiento estándar para promocionar páginas de inicio con dicho fin. | En el lanzamiento | `contentUpdate`<br>`contentCopy`<br>`contentDelete`<br>`referencesUpdate`<br>`orderChildren`<br>`markLiveRelationship` |

### Acciones de sincronización {#synchronization-actions}

En la tabla siguiente se enumeran las acciones de sincronización que se proporcionan listas para usar con AEM.

<!--If the installed actions do not meet your requirements, you can [Create a New Synchronization Action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).-->

| Nombre de la acción | Descripción | Propiedades |
|---|---|---|
| `contentCopy` | Cuando los nodos del origen no existen en Live Copy, esta acción copia los nodos en Live Copy. [Configure el servicio de copia de contenido de  **CQ MSM** ](#excluding-properties-and-node-types-from-synchronization) para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. |  |
| `contentDelete` | Esta acción elimina los nodos de Live Copy que no existen en el origen. [Configure la acción de eliminación de contenido de  **CQ MSM** ](#excluding-properties-and-node-types-from-synchronization) para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. |  |
| `contentUpdate` | Esta acción actualiza el contenido de Live Copy con los cambios del origen. [Configure el servicio de actualización de contenido de  **CQ MSM** ](#excluding-properties-and-node-types-from-synchronization) para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. |  |
| `editProperties` | Esta acción edita las propiedades de Live Copy. La propiedad `editMap` determina qué propiedades se editan y su valor. El valor de la propiedad `editMap` debe utilizar el siguiente formato:<br>`[property_name_n]#[current_value]#[new_value]`<br>`current_value` y `new_value` son expresiones regulares y `n` es un número entero incrementado.<br>Por ejemplo, considere el siguiente valor para  `editMap`:<br>`sling:resourceType#/(contentpage``homepage)#/mobilecontentpage,cq:template#/contentpage#/mobilecontentpage`<br>Este valor edita las propiedades de los nodos de Live Copy como se indica a continuación:<br>Las  `sling:resourceType` propiedades que se establecen en  `contentpage` o en  `homepage` se establecen en  `mobilecontentpage`.<br>Las  `cq:template` propiedades definidas en  `contentpage` se establecen en  `mobilecontentpage`. | `editMap: (String)` identifica la propiedad, el valor actual y el nuevo valor. Consulte la descripción para obtener más información. |
| `notify` | Esta acción envía un evento de página que indica que la página se ha desplegado. Para recibir notificaciones, primero debe suscribirse a eventos de lanzamiento. |  |
| `orderChildren` | Esta acción ordena los nodos secundarios según el orden del modelo. |  |
| `referencesUpdate` | Esta acción de sincronización actualiza las referencias en Live Copy.<br>Busca rutas en las páginas de Live Copy que apuntan a un recurso dentro del modelo. Cuando se encuentra, actualiza la ruta para que apunte al recurso relacionado dentro de Live Copy. Las referencias que tienen los destinos fuera del modelo no cambian. <br>[Configure la acción de actualización de referencias de  **CQ MSM** ](#excluding-properties-and-node-types-from-synchronization) para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán. |  |
| `targetVersion` | Esta acción crea una versión de Live Copy.<br>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento. |  |
| `targetActivate` | Esta acción activa Live Copy.<br>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento. |  |
| `targetDeactivate` | Esta acción desactiva Live Copy.<br>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento. |  |
| `workflow` | Esta acción inicia el flujo de trabajo definido por la propiedad de destino (solo para páginas) y toma Live Copy como carga útil.<br>La ruta de destino es la ruta del nodo del modelo. | `target: (String)` es la ruta al modelo de flujo de trabajo. |
| `mandatory` | Esta acción establece el permiso de varias ACL en la página Live Copy como de solo lectura para un grupo de usuarios específico. Las siguientes ACL están configuradas:<br>`ActionSet.ACTION_NAME_REMOVE`<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Utilice esta acción solo para páginas. | `target: (String)` es el ID del grupo para el que se configuran los permisos. |
| `mandatoryContent` | Esta acción establece el permiso de varias ACL en la página Live Copy como de solo lectura para un grupo de usuarios específico. Las siguientes ACL están configuradas:<br>`ActionSet.ACTION_NAME_SET_PROPERTY`<br>`ActionSet.ACTION_NAME_ACL_MODIFY`<br>Utilice esta acción solo para páginas. | `target: (String)` es el ID del grupo para el que se configuran los permisos. |
| `mandatoryStructure` | Esta acción establece el permiso de la `ActionSet.ACTION_NAME_REMOVE` ACL en la página Live Copy como de solo lectura para un grupo de usuarios específico.<br>Utilice esta acción solo para páginas. | `target: (String)` es el ID del grupo para el que se configuran los permisos. |
| `VersionCopyAction` | Si el modelo o la página de origen se han publicado al menos una vez, esta acción crea una página de Live Copy con la versión publicada. Nota: esta acción solo está disponible para crear una página de Live Copy basada en una página de origen publicada, no para actualizar una página de Live Copy existente. |  |
| `PageMoveAction` | El `PageMoveAction` se aplica cuando una página se ha movido en el modelo.<br>La acción copia la página Live Copy (relacionada) en lugar de moverla de la ubicación anterior al traslado a la ubicación posterior.<br>La  `PageMoveAction` no cambia la página Live Copy en la ubicación anterior al desplazamiento. Por lo tanto, para las configuraciones de lanzamiento consecutivas, tiene el estado de una relación activa sin un modelo.<br>[Configure  **CQ MSM Page Move** ](#excluding-properties-and-node-types-from-synchronization) Action para especificar los tipos de nodo, los elementos de párrafo y las propiedades de página que se excluirán.<br>Esta acción debe ser la única acción de sincronización incluida en una configuración de lanzamiento. | Establezca `prop_referenceUpdate: (Boolean)` en true (predeterminado) para actualizar las referencias. |
| `markLiveRelationship` | Esta acción Indica que existe una relación activa con el contenido creado para el lanzamiento. |  |

<!--
### Creating a Rollout Configuration {#creating-a-rollout-configuration}

You can [create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) when the installed rollout configurations do not meet your application requirements by performing the following steps.

1. [Create the rollout configuration](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
1. [Add synchronization actions to the rollout configuration](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

The new rollout configuration is then available to you when configuring rollout configurations on a blueprint or Live Copy page.
-->

### Exclusión de propiedades y tipos de nodos de la sincronización {#excluding-properties-and-node-types-from-synchronization}

Puede configurar varios servicios de OSGi que admitan las acciones de sincronización correspondientes para que no afecten a los tipos de nodos y propiedades específicos. Por ejemplo, muchas propiedades y subnodos relacionados con el funcionamiento interno de AEM no deben incluirse en una Live Copy. Solo se debe copiar el contenido relevante para el usuario de la página.

Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios. Consulte [Configuración de OSGi](/help/implementing/deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

En la tabla siguiente se enumeran las acciones de sincronización para las que se pueden especificar los nodos que se excluirán. La tabla proporciona los nombres de los servicios que se configuran mediante la consola web y el PID para configurar el uso de un nodo del repositorio.

| Acción de sincronización | Nombre del servicio en la consola web | PID de servicio |
|---|---|---|
| `contentCopy` | Acción de copia de contenido de CQ MSM | `com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory` |
| `contentDelete` | Acción de eliminación de contenido de CQ MSM | `com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory` |
| `contentUpdate` | Acción de actualización de contenido de CQ MSM | `com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory` |
| `PageMoveAction` | Acción de movimiento de página de CQ MSM | `com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory` |
| `referencesUpdate` | Acción de actualización de referencias de CQ MSM | `com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory` |

En la tabla siguiente se describen las propiedades que se pueden configurar:

| Propiedad de la consola web | OSGi (propiedad) | Descripción |
|---|---|---|
| Tipos de nodos excluidos | `cq.wcm.msm.action.excludednodetypes` | Expresión regular que coincide con los tipos de nodo que se van a excluir de la acción de sincronización. |
| Elementos de párrafo excluidos | `cq.wcm.msm.action.excludedparagraphitems` | Expresión regular que coincide con los elementos de párrafo que se van a excluir de la acción de sincronización. |
| Propiedades de página excluidas | `cq.wcm.msm.action.excludedprops` | Expresión regular que coincide con las propiedades de página que se van a excluir de la acción de sincronización. |
| Tipos de nodos de Mixin ignorados | `cq.wcm.msm.action.ignoredMixin` | Expresión regular que coincide con los nombres de los tipos de nodos de mezcla que se van a excluir de la acción de sincronización (solo disponible para la acción `contentUpdate`) |

#### Acción de actualización de contenido de CQ MSM: exclusiones {#cq-msm-content-update-action-exclusions}

Algunas propiedades y tipos de nodo se excluyen de forma predeterminada. Estos se definen en la configuración de OSGi de la **acción de actualización de contenido de CQ MSM**, en **Propiedades de página excluidas**.

De forma predeterminada, las propiedades que coinciden con las siguientes expresiones regulares se excluyen (es decir, no se actualizan) del lanzamiento:

![Regímenes de exclusión de Live Copy](../assets/live-copy-exclude.png)

Puede cambiar las expresiones que definen la lista de exclusión según sea necesario.

Por ejemplo, si quiere que el **título** de la página se incluya en los cambios considerados para el lanzamiento, elimine `jcr:title` de las exclusiones. Por ejemplo, con la expresión regular:

`jcr:(?!(title)$).*`

### Configuración de la sincronización de actualización de referencias {#configuring-synchronization-for-updating-references}

Puede configurar varios servicios de OSGi que admitan las acciones de sincronización correspondientes relacionadas con la actualización de referencias.

Al trabajar con AEM hay varios métodos para administrar los ajustes de configuración de dichos servicios. Consulte [Configuración de OSGi](/help/implementing/deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

En la siguiente tabla se enumeran las acciones de sincronización para las que se puede especificar la actualización de referencia. La tabla proporciona los nombres de los servicios que se configuran mediante la consola web y el PID para configurar el uso de un nodo del repositorio.

| Propiedad de la consola web | OSGi (propiedad) | Descripción |
|---|---|---|
| Actualizar referencia en LiveCopies anidadas | `cq.wcm.msm.impl.action.referencesupdate.prop_updateNested` | Seleccione esta opción en la consola web o establezca esta propiedad booleana como `true` utilizando la configuración del repositorio para reemplazar referencias que se dirijan a cualquier recurso que se encuentre dentro de la rama de la Live Copy más importante. Solo disponible para la acción `referencesUpdate`. |
| Actualizar páginas de referencia | `cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate` | Seleccione esta opción en la consola web o establezca esta propiedad booleana como `true` utilizando la configuración del repositorio para actualizar cualquier referencia que utilice la página original en lugar de hacer referencia a la página de Live Copy. Solo disponible para `PageMoveAction`. |

## Especificación de las opciones de configuración de lanzamiento que se van a utilizar {#specifying-the-rollout-configurations-to-use}

MSM le permite especificar conjuntos de configuraciones de lanzamiento que se utilizan generalmente y, cuando sea necesario, puede anularlos para Live Copies específicas. MSM proporciona varias ubicaciones para especificar las opciones de configuración de lanzamiento que se deben utilizar. La ubicación determina si la configuración se aplica a una Live Copy específica.

La siguiente lista de ubicaciones en las que puede especificar las opciones de configuración de lanzamiento que desea utilizar describe cómo MSM determina qué opciones de configuración de lanzamiento utilizar para una Live Copy:

* **[Propiedades de página de Live Copy](live-copy-sync-config.md#setting-the-rollout-configurations-for-a-live-copy-page):** cuando una página de Live Copy está configurada para utilizar una o más configuraciones de lanzamiento, MSM utiliza esas configuraciones de lanzamiento.
* **[Propiedades de página de modelo](live-copy-sync-config.md#setting-the-rollout-configuration-for-a-blueprint-page):** cuando una Live Copy se basa en un modelo y la página Live Copy no está configurada con una configuración de lanzamiento, se utiliza la configuración de lanzamiento asociada a la página de origen del modelo.
* **Propiedades de la página principal de Live Copy:**  cuando ni la página de Live Copy ni la página de origen del modelo están configuradas con una configuración de lanzamiento, se utiliza la configuración de lanzamiento que se aplica a la página principal de la página de Live Copy.
* **[Sistema predeterminado](live-copy-sync-config.md#setting-the-system-default-rollout-configuration):** cuando no se puede determinar la configuración de lanzamiento de la página principal de Live Copy, se utiliza la configuración de lanzamiento predeterminada del sistema.

Por ejemplo, un modelo utiliza el [tutorial de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) sitio como contenido de origen. Se crea un sitio a partir del modelo. Cada elemento de la lista siguiente describe un escenario diferente respecto al uso de las opciones de configuración de lanzamiento:

* Ninguna de las páginas de modelo o las páginas de Live Copy están configuradas para utilizar una configuración de lanzamiento. MSM utiliza la configuración de lanzamiento predeterminada del sistema para todas las páginas de Live Copy.
* La página raíz del sitio WKND se configura con varias configuraciones de lanzamiento. MSM utiliza estas configuraciones de lanzamiento para todas las páginas de Live Copy.
* La página raíz del sitio WKND se configura con varias configuraciones de lanzamiento y la página raíz del sitio Live Copy se configura con un conjunto diferente de configuraciones de lanzamiento. MSM utiliza las configuraciones de lanzamiento configuradas en la página raíz del sitio de Live Copy.

### Configuración de las opciones de configuración de lanzamiento para una página de Live Copy {#setting-the-rollout-configurations-for-a-live-copy-page}

Configure una página Live Copy con las opciones de configuración de lanzamiento que se usarán cuando se implemente la página de origen. Las páginas secundarias heredan la configuración de forma predeterminada. Al configurar la configuración de lanzamiento para su uso, anula la configuración que la página Live Copy hereda de su elemento principal.

También puede configurar las opciones de configuración de lanzamiento para una página de Live Copy cuando [cree la Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page).

1. Utilice la consola **Sites** para seleccionar la página Live Copy.
1. En la barra de herramientas, seleccione **Propiedades**.
1. Abra la pestaña **Live Copy**.

   La sección **Configuración** muestra las opciones de configuración de lanzamiento que hereda la página.

   ![Herencia de Live Copy de la página principal](../assets/live-copy-inherit.png)

1. Si es necesario, ajuste la marca de **Herencia de Live Copy**. Si se selecciona, la configuración de Live Copy es efectiva en todos los elementos secundarios.

1. Desactive la propiedad **Heredar configuración de lanzamiento del elemento principal** y, a continuación, seleccione una o varias opciones de configuración de lanzamiento de la lista.

   Las opciones de configuración de lanzamiento seleccionadas se muestran debajo de la lista desplegable.

   ![Anulación de la herencia de configuración de Live Copy](../assets/live-copy-inherit-override.png)

1. Toque o haga clic en **Guardar y cerrar**.

### Opciones de la configuración de lanzamiento para una página de modelo {#setting-the-rollout-configuration-for-a-blueprint-page}

Configure una página de modelo con las opciones de configuración de lanzamiento que se usarán cuando se lance la página de modelo.

Tenga en cuenta que las páginas secundarias de la página de modelo heredan la configuración. Al establecer la configuración de lanzamiento para su uso, podría anular la configuración que la página hereda de su elemento principal.

1. Utilice la consola **Sites** para seleccionar la página raíz del modelo.
1. En la barra de herramientas, seleccione **Propiedades**.
1. Abra la pestaña **Modelo**.
1. Seleccione una o más **opciones de configuración de lanzamiento** con el selector desplegable.
1. Para almacenar las actualizaciones, seleccione **Guardar**.

### Opciones de la configuración de lanzamiento predeterminada del sistema {#setting-the-system-default-rollout-configuration}

Para especificar una configuración de lanzamiento que se utilizará como predeterminada del sistema, configure el siguiente servicio OSGi.

* **Day CQ WCM Live Relationship** Manager con el servicio PID  `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

Configure el servicio mediante la [consola web](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un [nodo de repositorio](/help/implementing/deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* En la consola web, el nombre de la propiedad que se va a configurar es **Configuración de lanzamiento predeterminada**.
* Mediante un nodo del repositorio, el nombre de la propiedad que se va a configurar es `liverelationshipmgr.relationsconfig.default`.

Establezca este valor de la propiedad en la ruta de la configuración de lanzamiento que se utilizará como valor predeterminado del sistema. El valor predeterminado es `/libs/msm/wcm/rolloutconfigs/default`, que es la **Configuración de lanzamiento estándar**.
