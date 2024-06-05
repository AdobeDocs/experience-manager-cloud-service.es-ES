---
title: Despliegue de conflictos
description: Obtenga información sobre cómo administrar y resolver conflictos de despliegue del Administrador de varios sitios.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 63%

---

# Despliegue de conflictos {#msm-rollout-conflicts}

Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre en la rama del modelo y en una rama de Live Copy dependiente. Estos conflictos deben gestionarse y resolverse en el momento del despliegue.

## Gestión de conflictos {#conflict-handling}

Cuando existen páginas en conflicto (en las ramas de modelo y Live Copy), MSM le permite definir cómo (o incluso si) deben gestionarse.

Para garantizar que el despliegue no esté bloqueado, las definiciones posibles pueden incluir las siguientes:

* Qué página (modelo o Live Copy) tiene prioridad durante el despliegue
* Qué páginas se cambian de nombre y cómo
* Cómo afecta esto a cualquier contenido publicado

El comportamiento predeterminado de Adobe Experience Manager AEM () es que el contenido publicado no se ve afectado. Por lo tanto, si se ha publicado una página creada manualmente en la rama de Live Copy, ese contenido se publica después de la gestión y el despliegue del conflicto.

Además de la funcionalidad estándar, se pueden agregar controladores de conflicto personalizados para implementar distintas reglas. También pueden permitir acciones de publicación como un proceso individual.

### Escenario de ejemplo {#example-scenario}

En las secciones siguientes, se muestra un ejemplo de una página nueva `b` se utiliza, creado tanto en el modelo como en la rama de Live Copy (creada manualmente), para ilustrar los distintos métodos de resolución de conflictos:

* modelo: `/b`

  Una página maestra con una página secundaria, `bp-level-1`

* Live Copy: `/b`

  Una página creada manualmente en la rama de Live Copy con una página secundaria, `lc-level-1`

   * Se activa durante la publicación como `/b`, junto con la página secundaria

#### Antes del despliegue {#before-rollout}

|  | Modelo antes del despliegue | Live Copy antes del despliegue | Publicar antes del despliegue |
|---|---|---|---|
| Value | `b` | `b` | `b` |
| Comentar | Creado en rama de modelo, listo para su despliegue | Creado manualmente en la rama de Live Copy | Aparece el contenido de la página `b` que se creó manualmente en la rama de Live Copy |
| Value | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  | Creado manualmente en la rama de Live Copy | aparece el contenido de la página `child-level-1` que se creó manualmente en la rama de Live Copy |

## Administrador de despliegue y gestión de conflictos {#rollout-manager-and-conflict-handling}

El administrador de despliegue le permite activar o desactivar la administración de conflictos.

Esto se realiza mediante la [configuración OSGi](/help/implementing/deploying/configuring-osgi.md) del **administrador de despliegue de gestión de contenido web CQ por día**. Establezca el valor **Gestión conflictos con páginas creadas manualmente** (`rolloutmgr.conflicthandling.enabled`) a true si el administrador de despliegue debe gestionar los conflictos de una página creada en Live Copy con un nombre que exista en el modelo.

AEM tiene [comportamiento predefinido cuando la administración de conflictos se ha desactivado.](#behavior-when-conflict-handling-deactivated)

## Controladores de conflictos {#conflict-handlers}

AEM utiliza controladores de conflictos para resolver cualquier conflicto de páginas que surja al desplegar contenido desde un modelo a una Live Copy. Cambiar el nombre de las páginas es el método habitual (no el único) para resolver estos conflictos. Puede haber más de un controlador de conflictos en funcionamiento para permitir una selección de comportamientos diferentes.

AEM proporciona lo siguiente:

* El [controlador de conflictos predeterminado](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* La posibilidad de implementar un [controlador personalizado](#customized-handlers)
* Mecanismo de clasificación de servicios que permite establecer la prioridad de cada controlador individual
   * Se utiliza el servicio con la clasificación más alta.

### Controlador de conflictos predeterminado {#default-conflict-handler}

El controlador de conflictos predeterminado es `ResourceNameRolloutConflictHandler`

* Con este controlador, la página de modelo tiene prioridad.
* La clasificación de servicio de este controlador se ha establecido en un nivel bajo. Es decir, por debajo del valor predeterminado para `service.ranking` porque se supone que los controladores personalizados necesitan una clasificación más alta. Sin embargo, la clasificación no está al nivel mínimo absoluto para garantizar la flexibilidad cuando sea necesario.

Este controlador de conflictos da prioridad al modelo. Por ejemplo, la página Live Copy `/b` se mueve dentro de la rama de Live Copy a `/b_msm_moved`.

* Live Copy: `/b`

  Se mueve dentro de la Live Copy a `/b_msm_moved`. Esto actúa como una copia de seguridad y garantiza que no se pierda contenido.

   * `lc-level-1` no se mueve.

* Modelo: `/b`

  Se despliega en la página Live Copy `/b`.

   * `bp-level-1` se despliega en la Live Copy.

#### Después del despliegue {#after-rollout}

|  | Modelo después del despliegue | Live Copy después del despliegue | Live Copy después del despliegue | Publicación después del despliegue |
|---|---|---|---|---|
| Value | `b` | `b` | `b_msm_moved` | `b` |
| Comentar |  | Tiene el contenido de la página de modelo `b` que se desplegó | Tiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy | Sin cambios; contiene el contenido de la página original `b` que se creó manualmente en la rama de Live Copy y ahora se llama `b_msm_moved` |
| Value | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  |  | Sin cambios | Sin cambios |

### Controladores personalizados {#customized-handlers}

Los controladores de conflicto personalizados le permiten implementar sus propias reglas. Con el mecanismo de clasificación de servicios también puede definir cómo interactúan con otros controladores.

Los controladores de conflictos personalizados pueden hacer lo siguiente:

* Nombrarse según sus necesidades.
* Desarrollarse/configurarse según sus necesidades.
   * Por ejemplo, puede desarrollar un controlador para que la página Live Copy tenga prioridad.
* Se puede configurar utilizando la variable [Configuración de OSGi](/help/implementing/deploying/configuring-osgi.md). En particular:
   * La **clasificación de servicios** define el orden relacionado con otros controladores de conflictos (`service.ranking`).
      * El valor predeterminado es `0`.

### Comportamiento cuando los controladores de conflicto están desactivados {#behavior-when-conflict-handling-deactivated}

Si [desactiva los controladores de conflictos](#rollout-manager-and-conflict-handling) manualmente, AEM no realiza ninguna acción en ninguna página en conflicto. Las páginas que no entran en conflicto se despliegan según lo esperado.

>[!CAUTION]
>
>Cuando se desactivan los controladores de conflicto, AEM no da ninguna indicación de que se estén ignorando los conflictos. Dado que en estos casos este comportamiento debe configurarse explícitamente, se supone que es el comportamiento deseado.

En este caso, Live Copy tiene prioridad. La página de modelo `/b` no se copia y la página de Live Copy `/b` no se cambia.

* Modelo: `/b`

  No se copia en absoluto, pero se ignora.

* Live Copy: `/b`

  Sigue siendo el mismo.

#### Después del despliegue {#after-rollout-no-conflict}

|  | Modelo después del despliegue | Live Copy después del despliegue | Publicación después del despliegue |
|---|---|---|---|
| Value | `b` | `b` | `b` |
| Comentar |  | Sin cambios; tiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy | Sin cambios; contiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy |
| Value | `/bp-level-1,` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  | Sin cambios | Sin cambios |

### Clasificación de servicios {#service-rankings}

La clasificación del servicio [OSGi](https://www.osgi.org/) se puede utilizar para definir la prioridad de los controladores de conflictos individuales.
