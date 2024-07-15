---
title: Adición de repositorios privados en Cloud Manager
description: Obtenga información sobre cómo configurar Cloud Manager para que funcione con sus propios repositorios privados de GitHub.
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 77%

---

# Adición de repositorios privados en Cloud Manager {#private-repositories}

Al configurar Cloud Manager para que funcione con sus propios repositorios privados de GitHub, puede validar el código directamente en su repositorio de GitHub a través de Cloud Manager, lo que elimina la necesidad de sincronizar de forma sistemática el código con el repositorio de Adobe.

>[!NOTE]
>
>Esta funcionalidad es exclusiva de GitHub público. La compatibilidad con GitHub autoalojado no está disponible.

## Configuración {#configuration}

La configuración consta de dos pasos principales:

1. [Añadir repositorio](#add-repo)
1. [Validación de propiedad del repositorio privado](#validate-ownership)

### Añadir repositorio {#add-repo}

1. En Cloud Manager, en la página **Resumen del programa**, seleccione la pestaña **Repositorios** para cambiar a la página **Repositorios** y haga clic en **Agregar repositorio**.

1. En el diálogo **Añadir repositorio**, seleccione **Repositorio privado** como el tipo de repositorio.

1. Proporcione los detalles del repositorio

   * **Nombre del repositorio**: un nombre expresivo
   * **URL del repositorio**: la URL de este, que debe finalizar en `.git`
   * **Descripción** (opcional): una descripción más larga del repositorio según sea necesario

   ![Añadir su propio repositorio](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Seleccione **Guardar**.

>[!TIP]
>
>Para obtener más información sobre la administración de repositorios en Cloud Manager, consulte [Repositorios de Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).

### Validación de propiedad de repositorio privado {#validate-ownership}

Cloud Manager ahora conoce su repositorio de GitHub, pero aún necesita acceso. Para otorgar acceso, debe instalar la aplicación de GitHub de Adobe y comprobar que es el propietario del repositorio especificado.

1. Después de agregar su propio repositorio, se abre el cuadro de diálogo **Validación de propiedad del repositorio privado**.

   ![Validación de propiedad de repositorio privado](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager utiliza una aplicación de GitHub para interactuar de forma segura con el repositorio.
   * Un propietario de su organización de GitHub debe instalar la aplicación ubicada en `https://github.com/apps/cloud-manager-for-aem` y otorgar acceso al repositorio.
   * Consulte la documentación de GitHub para obtener más información sobre cómo hacerlo.

1. Para mejorar la seguridad, debe crear un archivo secreto en la rama predeterminada del repositorio. Seleccione **Generar**.

1. Confirme la generación del archivo secreto pulsando o haciendo clic en **Confirmar**.

   ![Confirmar generación de secreto](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. De nuevo en la ventana **Validación de propiedad de repositorio privado**, Cloud Manager ha generado el contenido del archivo privado en el campo **Contenido de archivo secreto**. Copie el contenido de dicho campo.

   * El contenido del archivo secreto solo se mostrará una vez. Si no copia el contenido antes de cerrar esta ventana, vuelva a generar el secreto.

   ![Copiar contenido de archivo secreto](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. Cree un nuevo archivo en la rama predeterminada de su repositorio de GitHub denominado `.well-known/adobe/cloud-manager-challenge` y pegue el contenido del archivo secreto en ese archivo y guárdelo.

1. Una vez que la aplicación esté instalada y el archivo secreto exista en el repositorio, puede seleccionar **Validar** en el cuadro de diálogo **Validación de propiedad del repositorio privado**.

La aplicación se puede instalar y el archivo secreto se puede crear en cualquier orden. Sin embargo, ambos pasos deben completarse antes de poder validar.

Hasta la validación, el repositorio se mostrará con un icono rojo que indica que aún no se ha validado y que no se puede utilizar.

![Repositorio no validado](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

La columna **Tipo** identifica fácilmente los repositorios proporcionados por el Adobe (**Adobe**) y sus propios repositorios de GitHub (**GitHub**).

Si necesita volver al repositorio más adelante para completar la validación, en la página **Repositorios**, seleccione el botón de los tres puntos de la fila que representa el repositorio de GitHub que acaba de agregar y seleccione **Validación de propiedad** en el menú desplegable.

## Uso de repositorios privados con Cloud Manager {#using}

Una vez validado el repositorio de GitHub en Cloud Manager, la integración se completa y puede utilizarlo con Cloud Manager.

1. Al crear una solicitud de extracción, se inicia automáticamente una comprobación de GitHub.

   ![Comprobaciones de GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Para cada solicitud de extracción, se crea automáticamente una [canalización de calidad de código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Esta canalización se inicia en cada actualización de solicitud de extracción.

1. La comprobación de GitHub permanece en estado de ejecución hasta que se completen las comprobaciones de calidad del código. Los resultados de calidad del código se propagan a la comprobación de GitHub.

   ![Comprobaciones de calidad del código de GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Cuando se cierra o se combina la solicitud de extracción, la canalización de calidad del código de pila completa creada se elimina automáticamente.

>[!TIP]
>
>Consulte el documento [Anotaciones de comprobación de GitHub](github-annotations.md) para obtener más información sobre la información proporcionada a través de GitHub cuando se ejecutan comprobaciones de solicitudes de extracción.

>[!TIP]
>
>Puede controlar las canalizaciones que se crean automáticamente para validar cada solicitud de extracción en un repositorio privado. Consulte el documento [Configuración de comprobación de GitHub para repositorios privados](github-check-config.md) para obtener más información.

## Asociación de repositorios privados con canalizaciones {#pipelines}

Los repositorios privados validados se pueden asociar con [canalizaciones de pila completa y front-end.](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)

>[!NOTE]
>
>Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados.

## Restricciones {#limitations}

Se aplican ciertas restricciones al usar repositorios privados con Cloud Manager.

* No puede pausar la validación de la solicitud de extracción utilizando la comprobación de GitHub desde Cloud Manager.
   * Si el repositorio de GitHub se valida en Cloud Manager, Cloud Manager siempre intentará validar las solicitudes de extracción creadas para ese repositorio.
* Si la aplicación de GitHub de Adobe se quita de su organización de GitHub, se quitará la función de validación de solicitudes de extracción de todos los repositorios.
* Las canalizaciones de configuración de nivel web no son compatibles con los repositorios privados.
* No se creará ni insertará ninguna etiqueta de Git al utilizar repositorios privados en canalizaciones de producción de pila completa.
* Las canalizaciones que utilizan repositorios privados y el activador de compilación de compromiso no se inician automáticamente cuando se inserta un nuevo compromiso en la rama seleccionada.
* La [funcionalidad de reutilización de artefactos](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) no se aplica a repositorios privados.
