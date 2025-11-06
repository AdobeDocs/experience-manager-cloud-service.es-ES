---
title: Introducción a los programas de producción
description: Conozca qué son los programas de producción y sugerencias para configurar los suyos.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 83%

---


# Introducción a los programas de producción {#production-programs}

Un programa de producción está pensado para un equipo que esté listo para empezar a escribir, generar y probar código con el objetivo de implementarlo para alojar el tráfico en vivo.

Después de [crear su programa de producción](creating-production-programs.md), un [asistente para la creación de programas](using-the-wizard.md) guiará al usuario a través de las selecciones según el objetivo del usuario al crear el programa.

## Opciones de creación de programas {#program-creation-options}

Su contrato con Adobe define el número y los tipos de soluciones disponibles para su organización específica al crear programas de producción. Puede controlar cómo asignar las soluciones disponibles a los programas de Cloud Manager.

En la siguiente tabla se describen los escenarios comunes de las soluciones disponibles y los programas de producción típicos creados en base a ellas.

| Soluciones disponibles | Opciones de programa | Novedades incluidas | Cuándo usarlas | Ejemplos |
|---------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 Solución de Sites | Crear 1 programa exclusivo de Sites | 1 producción + 1 fase, 1 desarrollo, 1 desarrollo rápido | N/D | N/D |
| 1 Solución de Assets | Crear 1 programa exclusivo de Assets | 1 producción + 1 fase, 1 desarrollo, 1 desarrollo rápido | N/D | N/D |
| 1 Sites +1 Assets | Crear un programa: <br>1 Programa de Sites y Assets | 1 producción + 1 fase, 2 desarrollo, 2 desarrollo rápido | Cuando la mayoría de los recursos digitales se utilizan para que sea compatible la implementación de sitios.<br>En estos casos, la mayoría de los recursos digitales están en estado terminado, listos para utilizarse para experiencias entre canales a través de Sites.<br>Normalmente, un solo equipo se encarga de administrar el contenido tanto de Sites como de Assets. | Imágenes que se utilizan principalmente para un sitio web.<br>Un portal interno integrado en AEM Sites distribuye archivos PDF. |
| 1 Sites +1 Assets | Cree programas separados:<br>1 Programa exclusivo de Sites y 1 programa exclusivo de Assets | 1 Producción + 1 Fase, 1 Desarrollo, 1 Desarrollo rápido<br>1 Producción + 1 Fase, 1 Desarrollo, 1 Desarrollo rápido | Cuando muchos recursos digitales no admiten directamente la implementación de Sites.<br> En estos casos, los recursos se encuentran en varios estados, incluidos los tipos de archivo sin procesar y los trabajos en curso.<br>Un equipo creativo dedicado administra los recursos digitales a través de su ciclo de vida y tiene flujos de trabajo y ciclos de publicación independientes del equipo de administración de contenido de Sites. | Las imágenes sin procesar de una sesión fotográfica se almacenan en el programa Assets y solo se utilizan unas pocas en la implementación de Sites.<br>Un gran número de tipos de archivos de Creative Cloud, como Photoshop e Illustrator, se administran en AEM Assets y pasan por su propio flujo de trabajo de aprobación antes de que se genere un recurso terminado.<br>Considere utilizar [Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) en esos casos. |
| 1 Sites + 1 Sites | Cree programas separados:<br>1 Programa exclusivo de Sites y 1 Programa exclusivo de Sites | 1 Producción + 1 Fase, 1 Desarrollo, 1 Desarrollo rápido<br>1 Producción + 1 Fase, 1 Desarrollo, 1 Desarrollo rápido | Para implementaciones de sitios de varios usuarios.<br>En estos casos, se deben administrar varios sitios con su propia programación de versiones y equipos de contenido y desarrollo. | Dos marcas comerciales con sitios web dedicados y equipos de desarrollo independientes |


>[!NOTE]
>
>Los programas de producción [se pueden editar pero no eliminar](editing-programs.md).
