---
title: 'Introducción a los programas de producción '
description: Conozca qué son los programas de producción y sugerencias para configurar los suyos.
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: a6152a1529b5c70bcf056857204e7ff97fc614e4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 2%

---


# Introducción a los programas de producción {#production-programs}

Un programa de producción está pensado para un equipo que esté listo para empezar a escribir, crear y probar código con el objetivo de implementarlo para alojar el tráfico en vivo.

Tras [cree su programa de producción,](creating-production-programs.md) a [asistente de creación de programas](using-the-wizard.md) guía al usuario a través de selecciones según el objetivo del usuario al crear el programa.

## Opciones de creación de programas {#program-creation-options}

Su contrato con Adobe define el número y los tipos de soluciones disponibles para su organización específica al crear programas de producción. Tiene control sobre cómo asignar las soluciones disponibles a los programas de Cloud Manager.

En la tabla siguiente se describen los escenarios comunes de las soluciones disponibles y los programas de producción típicos creados en función de ellas.

| Soluciones disponibles | Opciones de programa | Novedades incluidas | Cuándo se utiliza | Ejemplos |
|--- |--- |--- |--- |---|
| 1 solución de Sites | Crear 1 programa solo de sitios | 1 producción + 1 fase, 1 desarrollo | N/D | N/D |
| 1 Solución de activos | Crear 1 programa solo de recursos | 1 producción + 1 fase, 1 desarrollo | N/D | N/D |
| 1 Sitios +1 Recursos | Crear un programa: <br>1 Programa Sites &amp; Assets | 1 producción + 1 fase, 2 desarrollo | Cuando la mayoría de los recursos digitales se utilizan para admitir la implementación de sitios.<br>En estos casos, la mayoría de los recursos digitales están en estado terminado, listos para utilizarse para experiencias entre canales a través de Sitios.<br>Normalmente, un solo equipo se encarga de administrar el contenido tanto de los sitios como de los recursos. | Imágenes que se utilizan principalmente para un sitio web.<br>PDF que se distribuirán mediante un portal interno integrado en AEM Sites. |
| 1 Sitios +1 Recursos | Cree programas separados:<br>1 Solo programa Sitios y 1 solo programa Activos | 1 producción + 1 fase, 1 desarrollo<br> 1 producción + 1 fase, 1 desarrollo | Cuando muchos recursos digitales no admiten directamente la implementación de sitios.<br> En estos casos, los recursos se encuentran en varios estados, incluidos los tipos de archivo sin procesar y las obras en curso.<br>Un equipo creativo dedicado gestiona los recursos digitales a través de su propio ciclo de vida y tiene flujos de trabajo y ciclos de publicación independientes que el equipo de administración de contenido de Sites. | Las imágenes sin procesar de una sesión fotográfica se almacenan en el programa Recursos y solo se utilizarán unas pocas en la implementación Sitios.<br>Un gran número de tipos de archivos Creative Cloud, como Photoshop y Illustrator, se administran en AEM Assets y pasan por su propio flujo de trabajo de aprobación antes de que se genere un recurso terminado.<br>Considere utilizar [Recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets) en tales casos. |
| 1 Sitios + 1 Sitios | Cree programas separados:<br>1 Solo programa Sitios y 1 solo programa Sitios | 1 producción + 1 fase, 1 desarrollo<br>1 producción + 1 fase, 1 desarrollo | Para implementaciones de sitios de varios inquilinos.<br>En estos casos, se deben administrar varios sitios con su propia programación de versiones y equipos de contenido y desarrollo dedicados. | Dos marcas comerciales con sitios web dedicados y equipos de desarrollo independientes |

>[!NOTE]
>
>Programas de producción [no se puede editar ni eliminar.](editing-programs.md)
