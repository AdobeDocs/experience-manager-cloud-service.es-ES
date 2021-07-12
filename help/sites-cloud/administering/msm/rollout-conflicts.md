---
title: Despliegue de conflictos
description: Obtenga información sobre cómo administrar y resolver conflictos de implementación del administrador de varios sitios.
feature: Administrador de varios sitios
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 2%

---

# Despliegue de conflictos {#msm-rollout-conflicts}

Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre de página en la rama del modelo y en una rama de Live Copy dependiente. Estos conflictos deben manejarse y resolverse en el momento de su implementación.

## Gestión de conflictos {#conflict-handling}

Cuando existen páginas en conflicto (en las ramas de modelo y Live Copy), MSM le permite definir cómo deben manejarse (o incluso si).

Para garantizar que el despliegue no esté bloqueado, las definiciones posibles pueden incluir:

* Qué página (modelo o Live Copy) tendrá prioridad durante el lanzamiento
* ¿Qué páginas se cambiarán de nombre (y cómo)?
* Cómo afectará esto a cualquier contenido publicado

El comportamiento predeterminado de AEM listo para usar es que el contenido publicado no se verá afectado. Por lo tanto, si se ha publicado una página creada manualmente en la rama de Live Copy, dicho contenido se publicará después de la gestión y el despliegue del conflicto.

Además de la funcionalidad estándar, se pueden agregar controladores de conflicto personalizados para implementar distintas reglas. También pueden permitir acciones de publicación como un proceso individual.

### Ejemplo de escenario {#example-scenario}

En las secciones siguientes utilizamos el ejemplo de una nueva página `b`, creada tanto en el modelo como en la rama de Live Copy (creada manualmente), para ilustrar los distintos métodos de resolución de conflictos:

* modelo: `/b`

   Una página de formato con 1 página secundaria, `bp-level-1`

* Live Copy: `/b`

   Una página creada manualmente en la rama de Live Copy con una página secundaria, `lc-level-1`

   * Se activa en la publicación como `/b`, junto con la página secundaria

#### Antes de la implementación {#before-rollout}

|  | Modelo antes de la implementación | Live Copy antes del lanzamiento | Publicar antes del lanzamiento |
|---|---|---|---|
| Value | `b` | `b` | `b` |
| Comentario | Creado en rama de modelo, listo para su despliegue | Creado manualmente en la rama de Live Copy | Contiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy |
| Valor | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentario |  | Creado manualmente en la rama de Live Copy | contiene el contenido de la página `child-level-1` que se creó manualmente en la rama de Live Copy |

## Gestor de implementación y gestión de conflictos {#rollout-manager-and-conflict-handling}

El administrador de implementación le permite activar o desactivar la administración de conflictos.

Esto se realiza mediante la [configuración OSGi](/help/implementing/deploying/configuring-osgi.md) del **administrador de implementación de CQ WCM de día**. Establezca el valor **Handle conflict with manualmente created Pages** ( `rolloutmgr.conflicthandling.enabled`) en true si el administrador de lanzamientos debe gestionar los conflictos de una página creada en Live Copy con un nombre que exista en el modelo.

AEM tiene [comportamiento predefinido cuando se ha desactivado la administración de conflictos.](#behavior-when-conflict-handling-deactivated)

## Controladores de conflictos {#conflict-handlers}

AEM utiliza controladores de conflictos para resolver cualquier conflicto de páginas que exista al implementar contenido desde un modelo a una Live Copy. Cambiar el nombre de las páginas es el método habitual (no solo) para resolver estos conflictos. Puede haber más de un controlador de conflictos en funcionamiento para permitir una selección de comportamientos diferentes.

AEM proporciona:

* El [controlador de conflicto predeterminado](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* La posibilidad de implementar un [controlador personalizado](#customized-handlers)
* El mecanismo de clasificación de servicios que le permite establecer la prioridad de cada controlador individual
   * Se utiliza el servicio con la clasificación más alta.

### Controlador de conflictos predeterminado {#default-conflict-handler}

El controlador de conflicto predeterminado es `ResourceNameRolloutConflictHandler`

* Con este controlador, la página de modelo tiene prioridad.
* La clasificación de servicio de este controlador se establece en un valor bajo, es decir, por debajo del valor predeterminado de la propiedad `service.ranking`, ya que se supone que los controladores personalizados necesitarán una clasificación más alta. Sin embargo, la clasificación no es el mínimo absoluto para garantizar la flexibilidad cuando sea necesario.

Este controlador de conflicto da prioridad al modelo. Por ejemplo, la página Live Copy `/b` se mueve dentro de la rama de Live Copy a `/b_msm_moved`.

* Live Copy: `/b`

   Se mueve dentro de Live Copy a `/b_msm_moved`. Esto actúa como una copia de seguridad y garantiza que no se pierda contenido.

   * `lc-level-1` no se mueve.

* Modelo: `/b`

   Se despliega en la página Live Copy `/b`.

   * `bp-level-1` se incluye en Live Copy.

#### Después de la implementación {#after-rollout}

|  | Modelo después de la implementación | Live Copy después del lanzamiento | Live Copy después del lanzamiento | Publicar después del lanzamiento |
|---|---|---|---|---|
| Valor | `b` | `b` | `b_msm_moved` | `b` |
| Comentario |  | Tiene el contenido de la página de modelo `b` que se presentó | Tiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy | Sin cambios, contiene el contenido de la página original `b` que se creó manualmente en la rama de Live Copy y ahora se denomina `b_msm_moved` |
| Valor | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentario |  |  | Sin cambio | Sin cambio |

### Controladores personalizados {#customized-handlers}

Los controladores de conflicto personalizados le permiten implementar sus propias reglas. Con el mecanismo de clasificación de servicios también puede definir cómo interactúan con otros controladores.

Los controladores de conflictos personalizados pueden:

* Reciba un nombre según sus necesidades.
* Desarrollarse/configurarse según sus necesidades.
   * Por ejemplo, puede desarrollar un controlador para que la página Live Copy tenga prioridad.
* Se puede diseñar para que se configure usando la [configuración OSGi](/help/implementing/deploying/configuring-osgi.md). En particular:
   * **Service** Rankingdefine el orden relacionado con otros controladores de conflictos (  `service.ranking`).
      * El valor predeterminado es `0`.

### Comportamiento cuando la administración de conflictos está desactivada {#behavior-when-conflict-handling-deactivated}

Si desactiva manualmente [la gestión de conflictos,](#rollout-manager-and-conflict-handling) no AEM ninguna acción en las páginas en conflicto. Las páginas que no entran en conflicto se despliegan según lo esperado.

>[!CAUTION]
>
>Cuando se desactiva la gestión de conflictos, AEM no da ninguna indicación de que se estén ignorando los conflictos. Dado que en estos casos este comportamiento debe configurarse explícitamente, se supone que es el comportamiento deseado.

En este caso, Live Copy tiene prioridad. La página de modelo `/b` no se copia y la página de Live Copy `/b` no se modifica.

* Modelo: `/b`

   No se copia, pero se ignora.

* Live Copy: `/b`

   Sigue igual.

#### Después de la implementación {#after-rollout-no-conflict}

|  | Modelo después de la implementación | Live Copy después del lanzamiento | Publicar después del lanzamiento |
|---|---|---|---|
| Valor | `b` | `b` | `b` |
| Comentario |  | Sin cambios, el contenido de la página `b` que se creó manualmente en la rama de Live Copy | Sin cambios, contiene el contenido de la página `b` que se creó manualmente en la rama de Live Copy |
| Valor | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| Comentario |  | Sin cambio | Sin cambio |

### Clasificación de servicios {#service-rankings}

La clasificación del servicio [OSGi](https://www.osgi.org/) se puede utilizar para definir la prioridad de los controladores de conflictos individuales.
