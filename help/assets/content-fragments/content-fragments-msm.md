---
title: Reutilizar fragmentos de contenido usando MSM y Live Copies
description: Obtenga información sobre el uso de la Live Copy funcionalidad de MSM para utilizar los mismos contenido de fragmento de contenido o similares en varias ubicaciones, mientras sincroniza con el contenido de origen.
source-git-commit: 3ce1a982055c2f9c900edbd88e079deb6d3a036a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 10%

---

# Reutilizar fragmentos de contenido usando MSM {#reuse-content-fragments-using-msm}

Multi Site Manager (MSM) y el Live Copy funcionalidad le permite utilizar el mismo contenido en varias ubicaciones, mientras se sincroniza con el contenido de origen.

* Con Live Copies de MSM puede:
   * Crear contenido una vez y después
   * Reutilice este contenido en otras áreas del mismo sitio o de otras aplicaciones.
* A continuación, MSM mantiene las relaciones activas entre el contenido de origen y sus Live Copies para lo siguiente:
   * Al cambiar el contenido de origen, el origen y las Live Copies se sincronizan.
   * Puede hacer ajustes solo en el contenido de las Live Copies desconectando la relación activa para subpáginas o componentes individuales.

Para obtener información general detallada sobre los conceptos de MSM, consulte [Reutilización de contenido: Administrador de sitios múltiples y Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[La funcionalidad de Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) en Adobe Experience Manager permite a los usuarios reutilizar contenido que se crean una vez y luego se reutilizan en múltiples ubicaciones web.

Al utilizar MSM para los fragmentos de contenido puede:

* Crear fragmentos de contenido una vez y luego hacer copias (vinculadas) de estos fragmentos para reutilizarlos en otras áreas del sitio o aplicación.
* Mantenga varias copias sincronizadas actualizando la copia de origen una vez y, a continuación, inserte los cambios en las copias (activas).
* Realice cambios locales suspendiendo temporal o permanentemente el vínculo entre los fragmentos principales y secundarios, ya sea por completo o para sus variaciones o campos.

El MSM para fragmentos de contenido, combinado con funcionalidad dentro del editor de fragmentos de contenido, permite dividir y restablecer la herencia en el nivel de campo.

>[!CAUTION]
>
>MSM para fragmentos de contenido solo está disponible cuando se utilizan fragmentos de contenido a través de la **consola Assets** .
>
>La funcionalidad MSM no *está* disponible cuando se utiliza la consola de **fragmentos de** contenido.

## Cómo {#how-to}

Consulte la siguiente documentación para obtener más detalles sobre el uso de MSM para fragmentos de contenido (también aplicable a Assets):

* Cómo usar [MSM para fragmentos de contenido (y Assets)](/help/assets/reuse-assets-using-msm.md)

* [Crear una Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >Si desea utilizar MSM para crear copias de fragmentos de contenido), entonces cualquier restricción única **debe eliminarse de cualquier** tipo de datos utilizado en los respectivos [modelos](/help/assets/content-fragments/content-fragments-models.md) de fragmento de contenido.

* [Ver propiedades y estado del origen y del Live Copy](/help/assets/reuse-assets-using-msm.md#properties)
* [Propagación de modificaciones desde el origen a Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* Cancelar y restablecer la herencia para:
   * campos y variaciones en el editor de fragmentos de [contenido](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [metadatos de activos relacionados](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [Suspender y reanudar la relación](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [Quitar la relación activa](/help/assets/reuse-assets-using-msm.md#detach)
* [Comparar MSM para fragmentos de contenido (y Assets) con MSM para Sites](/help/assets/reuse-assets-using-msm.md#comparison)

## Restricciones {#limitations}

* Los activadores durante la modificación y la configuración despliegue asociada no existen para los fragmentos de contenido.