---
title: Requisitos previos para la herramienta de transferencia de contenido
description: Requisitos previos para la herramienta de transferencia de contenido
source-git-commit: 0d664997a66d790d5662e10ac0afd0dca7cc7fac
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 2%

---

# Requisitos previos para la herramienta de transferencia de contenido {#prerequisites}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_prereqs"
>title="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>abstract="Revise consideraciones importantes para utilizar la herramienta de transferencia de contenido, incluidas las versiones de Java y AEM, los tipos de almacén de datos admitidos, las consideraciones de grupos de usuarios y más."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#pre-reqs" text="Consideraciones importantes sobre el uso de la herramienta de transferencia de contenido"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en#best-practices" text="Prácticas recomendadas y directrices"

En la tabla siguiente se resumen los requisitos previos para utilizar la herramienta de transferencia de contenido.

Revise todas las consideraciones enumeradas a continuación:

| Consideraciones | ¿Qué es compatible actualmente? |
|--- |--- |
| Versión de AEM | La herramienta de transferencia de contenido solo se puede ejecutar en AEM versión 6.3 o posterior. Para poder usar la herramienta de transferencia de contenido con AEM versión 6.2 o anteriores, se requiere una actualización in situ del repositorio de contenido a AEM 6.5. No es necesario actualizar el código a AEM 6.5 para esto. |
| Tamaño del almacén de segmentos | Actualmente, la herramienta de transferencia de contenido admite hasta 83 GB en *Author* y 31 GB en *Publish*. |
| Tamaño total del repositorio de contenido <br>*(almacén de segmentos + almacén de datos)* | La herramienta de transferencia de contenido está diseñada para transferir contenido de hasta 10 TB. Actualmente no se admite cualquier valor superior a 10 TB. Cree un ticket de asistencia con el Servicio de atención al cliente de Adobe para analizar las opciones de contenido de más de 10 TB. |
| Contenido en rutas inmutables | La herramienta de transferencia de contenido no se puede usar para migrar contenido en rutas inmutables como `“/etc”`. Hay ciertas `"/etc"` rutas permitidas para seleccionarse, pero solo para admitir [AEM Forms a AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/migrate-to-forms-as-a-cloud-service.html?lang=en#paths-of-various-aem-forms-specific-assets). Para todos los demás casos de uso, consulte [Reestructuración común de repositorios](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/restructuring/all-repository-restructuring-in-aem-6-4.html?lang=en#restructuring) para obtener más información sobre la reestructuración de repositorios. |

## Siguientes {#whats-next}

Una vez que haya revisado los requisitos previos y haya determinado si puede utilizar la herramienta de transferencia de contenido en su proyecto de migración, consulte [Prácticas recomendadas adicionales y consideraciones](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md) mientras utiliza la herramienta de transferencia de contenido.
