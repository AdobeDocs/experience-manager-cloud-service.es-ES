---
title: 'Introducción a Adobe Experience Manager as a Cloud Service: terminología'
description: 'Introducción a Adobe Experience Manager as a Cloud Service: terminología.'
exl-id: a76f68f1-4f84-4844-a099-0952707cd96d
source-git-commit: 4067db2234b29e4ffbe3e76f25afd9d8642a1973
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 97%

---

# Adobe Experience Manager as a Cloud Service: terminología {#adobe-experience-manager-as-a-cloud-service-terminology}

Los siguientes términos se utilizan en relación con Adobe Experience Manager (AEM) as a Cloud Service:

## Productos {#products}

| Producto | Descripción |
|---|---|
| AEM as a Cloud Service | La forma nativa de la nube de aprovechar las aplicaciones de AEM |
| AEM Assets as a Cloud Service | Las funciones de administración de recursos digitales (DAM) son una solución con capacidad de adaptación y nativa de la nube que permite el consumo, el procesamiento y la gestión de recursos digitales, a la vez que se integra con el ecosistema de Adobe Experience Cloud y Adobe Creative Cloud. |
| AEM Sites as a Cloud Service | Una instancia de AEM as a Cloud Service con la aplicación de AEM Sites. |

## Instancias y canalizaciones {#instances-and-pipelines}

| Instancia | Descripción |
|---|---|
| Canalización de Adobe | Mecanismo para publicar contenido de Author en Publish. |
| Nivel de AEM Author | Describe el entorno de creación para Sites y Assets. |
| Nivel de vista previa de AEM | Describe el entorno de vista previa para Sites. |
| Nivel de AEM Publish | Describe el entorno de publicación para Sites. |


<!-- This section of the table must be alphabetic -->

## Terminología {#terminology}

| Término | Descripción |
|---|---|
| AEM Image | Un artefacto que se puede implementar y contiene el código de producto de AEM junto con el código de cliente. |
| Microservicios de recursos | Servicios de procesamiento de recursos digitales basados en la nube que se ocupan de diversos casos prácticos del procesamiento de recursos, como la generación de representaciones, los procesamientos de archivos PDF, la gestión de recursos secundarios, la extracción de texto, etc. Consulte la [descripción general de los microservicios de recursos](/help/assets/asset-microservices-overview.md) para obtener más información. |
| Repositorio de Git de Cloud Manager | Donde los clientes almacenan su código y la configuración. |
| Proveedor en la nube | Actualmente, AEM as a Cloud Service admite Azure. La compatibilidad con AWS es un elemento de hoja de ruta. |
| Red de entrega de contenido (CDN) | AEM as Cloud Service se envía con una CDN predeterminada. Su objetivo principal es reducir la latencia mediante la entrega de contenido procesable desde los nodos de CDN en el extremo, cerca del explorador. Está completamente administrado y configurado para un rendimiento óptimo de las aplicaciones AEM. |
| Repositorio de contenido | Lugar donde se almacena el contenido. |
| Aislamiento empresarial | Cada instancia de AEM as a Cloud Service está aislada de las demás instancias. |
| Nodo maestro | Nivel de AEM Publish. |
| Motor de organización | AEM as a Cloud Service usa un motor de orquestación para garantizar que todos los servicios de creación y publicación se adapten según sea necesario. |
