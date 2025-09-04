---
title: Extraer solicitudes de comprobación de repositorios privados
description: Obtenga información sobre cómo controlar las canalizaciones que se crean automáticamente para validar cada solicitud de extracción en un repositorio privado.
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0ec47218d598aad6b225a9d5d8faeab20e606716
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 28%

---

# La solicitud de extracción comprueba los repositorios privados {#github-check-config}

Obtenga información sobre cómo controlar las canalizaciones que se crean automáticamente para validar cada solicitud de extracción en un repositorio privado.

## Configuración de comprobaciones de repositorios privados {#configuration}

Cuando se usan [repositorios privados](private-repositories.md#using), se crea automáticamente una [canalización de calidad de código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Esta canalización se inicia en cada actualización de solicitud de extracción.

Puede controlar estas comprobaciones creando un archivo de configuración de `.cloudmanager/pr_pipelines.yml` en la rama predeterminada del repositorio privado.

```yaml
pullRequest:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| Parámetro | Valores posibles | Predeterminado | Descripción |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` o `false` | `false` | Si se conserva solo el último comentario con los resultados del análisis de código de esta solicitud de extracción de GitHub o se conserva todo. Si se establece en `false` (predeterminado), no se eliminan los comentarios anteriores. |
| `shouldSkipCheckAnnotations` | `true` o `false` | `false` | Si se deben tener anotaciones adicionales presentes en la comprobación de solicitud de extracción de GitHub o no. Si se establece en `false` (predeterminado), las anotaciones de comprobación no se omiten y se incluyen en los comentarios. |
| `type` | `CI_CD` | N/D | Define el comportamiento de las configuraciones de canalización CI/CD (integración continua/implementación continua). |
| `template.programId` | Entero | No se reutilizan variables de canalización | Puede usarlo para reutilizar las [variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) establecidas en una canalización existente creada automáticamente por cada solicitud de extracción. |
| `template.pipelineId` | Entero | No se reutilizan variables de canalización | Puede usarlo para reutilizar las [variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) establecidas en una canalización existente creada automáticamente por cada solicitud de extracción. |
| `namePrefix` | Cadena | `Full Stack Code Quality Pipeline for PR` | Se utiliza para establecer el prefijo del nombre de la canalización que se crea automáticamente. |
| `importantMetricsFailureBehavior` | `CONTINUE` o `FAIL` o `PAUSE` | `CONTINUE` | Establece el comportamiento de la métrica importante de la canalización<br>`CONTINUE` = Si falla una métrica importante, la canalización avanza automáticamente<br>`FAIL` = La canalización termina con un estado FALLIDO si falla una métrica importante<br>`PAUSE` = El paso de análisis de código recibe un estado ESPERANDO cuando falla una métrica importante y debe reanudarse manualmente |




