---
title: Administrar versiones del proyecto de Maven
description: 'Para implementaciones de ensayo y producción de AEM as a Cloud Service, Cloud Manager genera una versión única e incremental. '
exl-id: 658bcbed-0733-45da-a3e3-9a5f817099c5
source-git-commit: 21607fadf33dac038c7f794b933b92f60b8e20a9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 3%

---


# Administrar versiones del proyecto de Maven {#maven-project-version-handling}

Para implementaciones de ensayo y producción de AEM as a Cloud Service, Cloud Manager genera una versión única e incremental

Esta versión se ve en el [página de detalles de ejecución de canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) así como la página de actividad. Cuando se ejecuta una compilación, el proyecto Maven se actualiza para utilizar esta versión y se crea una etiqueta en el repositorio de Git con esa versión como su nombre.

Si la versión original del proyecto cumple ciertos criterios, la versión actualizada del proyecto Maven combinará la versión original del proyecto y la versión generada por Cloud Manager. Sin embargo, la etiqueta siempre utiliza la versión generada. Para que se produzca esta combinación, la versión original del proyecto debe estar formada con exactamente tres segmentos de versión, por ejemplo, `1.0.0` o `1.2.3`, pero no `1.0` o `1`, y la versión original no debe finalizar `-SNAPSHOT`.

>[!IMPORTANT]
>
>Este valor de versión del proyecto original debe establecerse de forma estática en la variable `<version>` elemento del nivel superior `pom.xml` en la rama del repositorio de git.

Si la versión original cumple estos criterios, la versión generada se añadirá a la versión original como segmento de nueva versión. La versión generada también se modificará ligeramente para incluir la ordenación y el control de versiones adecuados. Por ejemplo, suponiendo una versión generada de `2019.926.121356.0000020490` tendría los siguientes resultados.

| Versión | Versión en `pom.xml` | Comentario |
|---|---|---|
| `1.0.0` | `1.0.0.2019_0926_121356_0000020490` | Versión original correctamente formada |
| `1.0.0-SNAPSHOT` | `2019.926.121356.0000020490` | Versión de instantánea, sobrescrita |
| `1` | `2019.926.121356.0000020490` | Versión incompleta, sobrescrita |

>[!NOTE]
>
>Independientemente de si la versión original se incorporó o no a la versión inicializada por Cloud Manager, la versión original está disponible como propiedad Maven con el nombre `cloudManagerOriginalVersion`.
