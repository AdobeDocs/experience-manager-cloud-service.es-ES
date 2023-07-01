---
title: Despliegue de conflictos
description: Obtenga información sobre cómo administrar y resolver conflictos de despliegue del Administrador de varios sitios.
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: a01583483fa89f89b60277c2ce4e1c440590e96c
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 96%

---

# Despliegue de conflictos {#msm-rollout-conflicts}

Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre en la rama del modelo y en una rama de Live Copy dependiente. Estos conflictos deben manejarse y resolverse en el momento del despliegue.

## Gestión de conflictos {#conflict-handling}

Cuando existen páginas en conflicto (en las ramas de modelo y Live Copy), MSM le permite definir cómo (o incluso si) deben gestionarse.

Para garantizar que el despliegue no esté bloqueado, las definiciones posibles pueden incluir las siguientes:

* Qué página (modelo o Live Copy) tendrá prioridad durante el despliegue
* Qué páginas se cambian de nombre y cómo
* Cómo afectará esto a cualquier contenido publicado

El comportamiento predeterminado de AEM es que el contenido publicado no se verá afectado. Por lo tanto, si se ha publicado una página creada manualmente en la rama de Live Copy, dicho contenido se publicará después de la gestión y el despliegue del conflicto.

Además de la funcionalidad estándar, se pueden agregar controladores de conflicto personalizados para implementar distintas reglas. También pueden permitir acciones de publicación como un proceso individual.

### Escenario de ejemplo {#example-scenario}

En las secciones siguientes utilizamos el ejemplo de la página nueva `b`, creada tanto en el modelo como en la rama de Live Copy (creada manualmente), para ilustrar los distintos métodos de resolución de conflictos:

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
* El mecanismo de clasificación de servicios que le permite establecer la prioridad de cada controlador individual
   * Se utiliza el servicio con la clasificación más alta.

### Controlador de conflictos predeterminado {#default-conflict-handler}

El controlador de conflictos predeterminado es `ResourceNameRolloutConflictHandler`

* Con este controlador, la página de modelo tiene prioridad.
* La clasificación de servicio de este controlador se establece en un nivel bajo, es decir, por debajo del valor predeterminado para `service.ranking` , ya que se supone que los controladores personalizados necesitarán una clasificación más alta. Sin embargo, la clasificación no está al nivel mínimo absoluto para garantizar la flexibilidad cuando sea necesario.

Este controlador de conflictos da prioridad al modelo. Por ejemplo, la página de Live Copy `/b` se mueve dentro de la rama de Live Copy a `/b_msm_moved`.

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
| Comentar |  | Tiene el contenido de la página de modelo `b` que se desplegó | Tiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy | Sin cambios, contiene el contenido de la página original `b` que se creó manualmente en la rama de Live Copy y ahora se llama `b_msm_moved` |
| Value | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  |  | Sin cambios | Sin cambios |

### Controladores personalizados {#customized-handlers}

Los controladores de conflicto personalizados le permiten implementar sus propias reglas. Con el mecanismo de clasificación de servicios también puede definir cómo interactúan con otros controladores.

Los controladores de conflictos personalizados pueden hacer lo siguiente:

* Nombrarse según sus necesidades.
* Desarrollarse/configurarse según sus necesidades.
   * Por ejemplo, puede desarrollar un controlador para que la página Live Copy tenga prioridad.
* Se puede diseñar para que se configure usando la [Configuración OSGi](/help/implementing/deploying/configuring-osgi.md). En particular:
   * La **clasificación de servicios** define el orden relacionado con otros controladores de conflictos (`service.ranking`).
      * El valor predeterminado es `0`.

### Comportamiento cuando los controladores de conflicto están desactivados {#behavior-when-conflict-handling-deactivated}

Si [desactiva los controladores de conflictos](#rollout-manager-and-conflict-handling) manualmente, AEM no realiza ninguna acción en ninguna página en conflicto. Las páginas que no entran en conflicto se despliegan según lo esperado.

>[!CAUTION]
>
>Cuando se desactivan los controladores de conflicto, AEM no da ninguna indicación de que se estén ignorando los conflictos. Dado que en estos casos este comportamiento debe configurarse explícitamente, se supone que es el comportamiento deseado.

En este caso, Live Copy tiene prioridad. La página de modelo `/b` no se copia y la página de Live Copy `/b` no se cambia.

* Modelo: `/b`

  No se copia en absoluto y se ignora.

* Live Copy: `/b`

  Permanece igual.

#### Después del despliegue {#after-rollout-no-conflict}

|  | Modelo después del despliegue | Live Copy después del despliegue | Publicación después del despliegue |
|---|---|---|---|
| Value | `b` | `b` | `b` |
| Comentar |  | Sin cambios, tiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy | Sin cambios, contiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy |
| Value | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentar |  | Sin cambios | Sin cambios |

### Clasificación de servicios {#service-rankings}

La clasificación del servicio [OSGi](https://www.osgi.org/) se puede utilizar para definir la prioridad de los controladores de conflictos individuales.
