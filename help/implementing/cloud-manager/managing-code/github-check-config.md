---
title: Configuración de comprobación de GitHub para repositorios privados
description: Obtenga información sobre cómo controlar las canalizaciones que se crean automáticamente para validar cada solicitud de extracción en un repositorio privado.
source-git-commit: 73bd693d47f37b453209208816dfed15d65e9e09
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# Configuración de comprobación de GitHub para repositorios privados {#github-check-config}

Obtenga información sobre cómo controlar las canalizaciones que se crean automáticamente para validar cada solicitud de extracción en un repositorio privado.

## Configuración de las comprobaciones de GitHub {#configuration}

Al utilizar [repositorios privados,](private-repositories.md#using) a [canalización de calidad de código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) se creará automáticamente. Esta canalización se inicia en cada actualización de solicitud de extracción.

Puede controlar estas comprobaciones creando un `.cloudmanager/pr_pipelines.yml` en la rama predeterminada del repositorio privado.

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| Parámetro | Valores posibles | Predeterminado | Descripción |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` o `false` | `false` | Si se conserva solo el último comentario con los resultados del escaneo de código de su solicitud de extracción de github o se conserva todo |
| `type` | `CI_CD` | N/D | Define el comportamiento de una canalización de CI/CD |
| `template.programID` | Entero | No se reutilizan variables de canalización | Se puede utilizar para reutilizar el [variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) que se establecen en una de las canalizaciones existentes que cada PR crea automáticamente. |
| `template.pipelineID` | Entero | No se reutilizan variables de canalización | Se puede utilizar para reutilizar el [variables de canalización](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) que se establecen en una de las canalizaciones existentes que cada PR crea automáticamente. |
| `namePrefix` | Cadena | `Full Stack Code Quality Pipeline for PR` | Se utiliza para establecer el nombre de la canalización que se crea automáticamente |
| `importantMetricsFailureBehavior` | `CONTINUE` o `FAIL` o `PAUSE` | `CONTINUE` | Establece el comportamiento de métrica importante de la canalización<br>`CONTINUE` = Si falla una métrica importante, la canalización avanzará automáticamente<br>`FAIL` = La canalización finalizará con el estado FALLIDO si falla una métrica importante<br>`PAUSE` = El paso de escaneo de código recibirá un estado de ESPERA cuando falle una métrica importante y se debe reanudar manualmente |
