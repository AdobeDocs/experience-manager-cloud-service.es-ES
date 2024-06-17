---
title: Reutilización de fragmentos de contenido mediante MSM y Live Copies
description: Obtenga información acerca del uso de la funcionalidad Live Copy de MSM para utilizar el mismo contenido de fragmento de contenido, o similar, en varias ubicaciones, mientras se sincroniza con el contenido de origen.
exl-id: f050b2d1-856c-4cdb-ac74-bc78016f144a
feature: Content Fragments
role: User
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# Reutilización de fragmentos de contenido mediante MSM {#reuse-content-fragments-using-msm}

El Administrador de varios sitios (MSM) y la funcionalidad de Live Copy le permiten utilizar el mismo contenido en varias ubicaciones y, al mismo tiempo, sincronizarse con el contenido de origen.

* Con Live Copies de MSM puede:
   * Crear contenido una vez y después
   * Reutilice este contenido en otras áreas del mismo sitio u otros sitios, o aplicaciones.
* A continuación, MSM mantiene las relaciones activas entre el contenido de origen y sus Live Copies para lo siguiente:
   * Al cambiar el contenido de origen, se sincronizan el origen y las Live Copies.
   * Puede hacer ajustes solo en el contenido de las Live Copies desconectando la relación activa para subpáginas o componentes individuales.

Para obtener una descripción detallada de los conceptos de MSM, consulte [Reutilización del contenido: administrador de varios sitios y Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[Administrador de varios sitios (MSM)](/help/sites-cloud/administering/msm/overview.md) La funcionalidad de Adobe Experience Manager permite a los usuarios reutilizar contenido creado una vez y reutilizado en varias ubicaciones web.

Con MSM para fragmentos de contenido puede:

* Cree fragmentos de contenido una vez y luego realice copias (vinculadas) de estos fragmentos para reutilizarlos en otras áreas del sitio o la aplicación.
* Mantenga varias copias sincronizadas actualizando la copia de origen una vez y, a continuación, inserte los cambios en las copias (activas).
* Realice cambios locales suspendiendo temporal o permanentemente el vínculo entre los fragmentos principales y secundarios, ya sea por completo o para sus variaciones o campos.

MSM para fragmentos de contenido, combinado con la funcionalidad dentro del Editor de fragmentos de contenido, le permite romper y restablecer la herencia en el nivel de campo.

>[!CAUTION]
>
>MSM para fragmentos de contenido solo está disponible cuando se utilizan fragmentos de contenido a través de **Assets** consola.
>
>La funcionalidad de MSM es *no* disponible al usar el **Fragmentos de contenido** consola.

## Cómo. {#how-to}

Consulte la siguiente documentación para obtener más información sobre el uso de MSM para fragmentos de contenido (también aplicable a Recursos):

* Cómo usar [MSM para fragmentos de contenido (y recursos)](/help/assets/reuse-assets-using-msm.md)

* [Creación de una Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >Si desea utilizar MSM para crear copias de Fragmentos de contenido), cualquier **Único** Las restricciones de deben eliminarse de cualquier tipo de datos utilizado en el [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md).

* [Ver las propiedades y el estado del origen y la Live Copy](/help/assets/reuse-assets-using-msm.md#properties)
* [Propagación de modificaciones desde el origen a Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* Cancelar y restablecer la herencia para:
   * campos y variaciones en el [Editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [metadatos de recursos relacionados](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [Suspender y reanudar la relación](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [Eliminar la relación activa](/help/assets/reuse-assets-using-msm.md#detach)
* [Comparar MSM para fragmentos de contenido (y recursos) con MSM para sitios](/help/assets/reuse-assets-using-msm.md#comparison)

## Restricciones {#limitations}

* Los déclencheur al modificar y la configuración de despliegue asociada no existen para los fragmentos de contenido.
