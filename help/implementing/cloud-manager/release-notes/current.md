---
title: Notas de la versión 2023.6.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.6.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 80a5f58119dc304161d324491cd65c50e981ccd4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 37%

---


# Notas de la versión 2023.6.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.6.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

AEM La fecha de lanzamiento de la versión 2023.6.0 de Cloud Manager en la versión as a Cloud Service de es el 8 de junio de 2023. La próxima versión está planificada para el 6 de julio de 2023.

## Novedades {#what-is-new}

* Al crear un nuevo [programa o entorno,](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) ahora, el nombre está restringido para aceptar solo caracteres alfanuméricos y un conjunto limitado de caracteres especiales.
* Al reanudar un [canalización de producción,](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) ahora se muestra un cuadro de diálogo de confirmación en el paso aprobar.
* Para el **[Pruebas funcionales del cliente](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)** y **[Pruebas de IU personalizadas](/help/implementing/cloud-manager/ui-testing.md)** pasos de canalización, un nuevo `INCOMPLETE` El estado ahora es posible, lo que indica que estas pruebas no estaban presentes y, por lo tanto, no se realizaron.
   * En estos casos, la canalización no falla y continúa con el siguiente paso.

## Correcciones de errores {#bug-fixes}

* El [canalización de configuración de nivel web](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipelines) ya no están activados incorrectamente para los programas solo de Assets.
* Se ha agregado una validación más sólida para evitar ciertos tipos de errores durante el aprovisionamiento del entorno.
