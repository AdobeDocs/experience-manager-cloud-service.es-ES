---
title: 'Introducción a los programas de producción '
description: Introducción a los programas de producción
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Introducción a los programas de producción {#production-programs}

Un programa *Production* está pensado para un usuario familiarizado con AEM y Cloud Manager y listo para empezar a escribir, crear y probar código con el objetivo de implementarlo en Producción.

>[!NOTE]
>No podrá eliminar un programa de producción.

Un asistente para la creación de programas guiará al usuario para que realice selecciones, según el objetivo del usuario al crear el programa. En función de las autorizaciones de solución no utilizadas disponibles para el cliente u organización específico, el usuario controla cómo asignar las autorizaciones de solución disponibles (no utilizadas) a los programas de Cloud Manager.

## Consideraciones sobre la creación de programas {#program-creation-considerations}

La tabla siguiente describe escenarios comunes que se deben tener en cuenta al crear programas en Cloud Manager:

| Derechos de solución no utilizados disponibles en la organización | Crear opciones de programa | Novedades incluidas | Cuándo usar y otras consideraciones |
|--- |--- |--- |--- |
| 1 solución de Sites | Crear 1 programa solo de Sites | 1 Producción + 1 Fase, 1 Desarrollo | ND |
| 1 Solución de activos | Crear 1 programa solo de activos | 1 Producción + 1 Fase, 1 Desarrollo | ND |
| 1 Sitios +1 Recursos | Crear un programa: 1 Programa Sites &amp; Assets | 1 producción + 1 fase, 2 desarrollo | La mayoría de los recursos digitales se utilizan para admitir la implementación de sitios. La mayoría de los recursos digitales se encuentran en un estado terminado, listos para utilizarse para experiencias entre canales a través de Sitios. Normalmente, un solo equipo se encarga de administrar el contenido tanto para Sitios como para Recursos. **Ejemplos** comunes: Imágenes que se utilizan principalmente para un sitio web. PDF que se distribuirán a través de un portal interno integrado en AEM Sites. |
| 1 Sitios +1 Recursos | Cree programas separados: 1 Solo programa Sitios y 1 solo programa Activos | 1 Producción + 1 Fase, 1 Desarrollo<br> 1 Producción + 1 Fase, 1 Desarrollo | Muchos recursos digitales no admiten directamente la implementación de sitios. Los recursos administrados se encuentran en varios estados, incluidos los tipos de archivo sin procesar y los trabajos en curso. Un equipo creativo dedicado gestiona los recursos digitales a través de su propio ciclo de vida y tiene flujos de trabajo y ciclos de publicación independientes que el equipo de administración de contenido de Sites. *Ejemplos* comunes: Las imágenes sin procesar de una sesión fotográfica se almacenan en el programa Recursos y solo se utilizarán unas pocas en la implementación Sitios. Un gran número de tipos de archivos Creative Cloud, como Photoshop y Illustrator, se administran en AEM Assets y pasan por su propio flujo de trabajo de aprobación antes de que se genere un recurso terminado. Funciones para aprovechar: [Recursos conectados](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html?lang=en#overview-of-connected-assets) |
| 1 Sitios + 1 Sitios | Cree programas separados: 1 Solo programa Sitios y 1 solo programa Sitios | 1 Producción + 1 Fase, 1 Desarrollo<br>1 Producción + 1 Fase, 1 Desarrollo | Implementaciones de sitios de varios inquilinos. Varios sitios con su propia programación de versiones y equipos de desarrollo y contenido dedicados. *Ejemplos* comunes: Dos marcas comerciales con sitios web dedicados y equipos de desarrollo independientes |
