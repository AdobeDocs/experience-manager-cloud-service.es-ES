---
title: Solucionar errores de creación de formularios
description: Solucionar errores de creación de formularios en el entorno as a Cloud Service de AEM Forms.
feature: Adaptive Forms, Troubleshooting
role: User
source-git-commit: 5e7cd7015d68cc634fcf6a99dd552289abbaedcf
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# Problema {#form-creation-fails}

Después de que los usuarios actualicen a la versión as a Cloud Service de AEM Forms `2024.5.16461`:

**Algunos usuarios** puede tener problemas al crear formularios, de modo que cuando un usuario crea un formulario, aparece el siguiente mensaje de error en el cuadro de diálogo de creación:

`A server error occurred. Try again after sometime.`

## Causa {#cause-form-creation-fails}

El problema se produce porque el autor publica el formulario sin **primero, publicar la plantilla** se usa en él. Esto resulta en la adición de la variable `jcr:uuid` y otras propiedades protegidas y generadas por el sistema a `<template-path>/initial/jcr:content` , lo que provoca errores en la creación posterior de formularios.

## Solución alternativa {#resolution-form-creation-fails}

Para resolver el problema, realice los siguientes pasos:

1. Asegúrese de que la plantilla utilizada en el formulario no tenga el `jcr:uuid` y otras propiedades protegidas generadas por el sistema en la ruta `<template-path>/initial/jcr:content node`.
1. Publique la plantilla explícitamente mediante la consola de plantillas.
1. Ahora, cuando se publique la plantilla, intente crear nuevos formularios con la plantilla.
1. Si la plantilla utilizada se actualiza en futuras versiones, vuelva a publicarla (como se indica en el paso 2) para evitar problemas de error al crear el formulario.


<!--

# Issue {#form-creation-fails}

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->










