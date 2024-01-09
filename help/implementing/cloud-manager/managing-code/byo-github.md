---
title: Trabajar con sus propios repositorios de GitHub en Cloud Manager
description: Obtenga información sobre cómo configurar Cloud Manager para que funcione con sus propios repositorios de GitHub.
feature: Release Information
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: ce9d65179d9cc1f02f786516554e07c95a89484d
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 70%

---


# Trabajar con sus propios repositorios de GitHub en Cloud Manager {#byo-github}

Al configurar Cloud Manager para que funcione con sus propios repositorios de GitHub, puede validar el código directamente en su repositorio de GitHub a través de Cloud Manager, lo que elimina la necesidad de sincronizar de forma sistemática el código con el repositorio de Adobe.

>[!NOTE]
>
>Esta funcionalidad solo está disponible para [el programa de clientes pioneros.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Configuración {#configuration}

La configuración consta de dos pasos principales:

1. [Añadir repositorio](#add-repo)
1. [Validación de propiedad del repositorio privado](#validate-ownership)

### Añadir repositorio {#add-repo}

1. En Cloud Manager, desde el **Resumen del programa** , seleccione la **Repositorios** para cambiar a la pestaña **Repositorios** y haga clic en **Añadir repositorio**.

1. En el diálogo **Añadir repositorio**, seleccione **Repositorio privado** como el tipo de repositorio.

1. Proporcione los detalles del repositorio

   * **Nombre del repositorio**: un nombre expresivo
   * **URL del repositorio**: la URL de este, que debe finalizar en `.git`
   * **Descripción** (opcional): una descripción más larga del repositorio según sea necesario

   ![Añadir su propio repositorio](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. Seleccione **Guardar**.

>[!TIP]
>
>Para obtener más información sobre la administración de repositorios en Cloud Manager, consulte [Repositorios de Cloud Manager](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md).

### Validación de propiedad de repositorio privado {#validate-ownership}

Cloud Manager ahora conoce su repositorio de GitHub, pero aún necesita acceso. Para otorgar acceso, debe instalar la aplicación de GitHub de Adobe y comprobar que es el propietario del repositorio especificado.

1. Después de agregar su propio repositorio, la variable **Validación de propiedad de repositorio privado** se abre.

   ![Validación de propiedad de repositorio privado](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

1. Cloud Manager utiliza una aplicación de GitHub para interactuar de forma segura con el repositorio.
   * Un propietario de su organización de GitHub debe instalar la aplicación ubicada en `https://github.com/apps/cloud-manager-for-aem` y otorgar acceso al repositorio.
   * Consulte la documentación de GitHub para obtener más información sobre cómo hacerlo.

1. Para mejorar la seguridad, debe crear un archivo secreto en la rama predeterminada del repositorio. Seleccionar **Generar**.

1. Confirme la generación del archivo secreto pulsando o haciendo clic en **Confirmar**.

   ![Confirmar generación de secreto](/help/implementing/cloud-manager/assets/repos/confirm-generation.png)

1. De nuevo en la ventana **Validación de propiedad de repositorio privado**, Cloud Manager ha generado el contenido del archivo privado en el campo **Contenido de archivo secreto**. Copie el contenido de dicho campo.

   * El contenido del archivo secreto solo se mostrará una vez. Si no copia el contenido antes de cerrar esta ventana, vuelva a generar el secreto.

   ![Copiar contenido de archivo secreto](/help/implementing/cloud-manager/assets/repos/new-secret.png)

1. Cree un nuevo archivo en la rama predeterminada de su repositorio de GitHub denominado `.well-known/adobe/cloud-manager-challenge` y pegue el contenido del archivo secreto en ese archivo y guárdelo.

1. Una vez que la aplicación esté instalada y el archivo secreto exista en el repositorio, puede seleccionar **Validate** en el **Validación de propiedad de repositorio privado** diálogo.

La aplicación se puede instalar y el archivo secreto se puede crear en cualquier orden. Sin embargo, ambos pasos deben completarse antes de poder validar.

Hasta la validación, el repositorio se mostrará con un icono rojo que indica que aún no se ha validado y que no se puede utilizar.

![Repositorio no validado](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

El **Tipo** identifica fácilmente los repositorios proporcionados por el Adobe (**Adobe**) y sus propios repositorios de GitHub (**GitHub**).

Si necesita volver al repositorio en una fecha posterior para completar la validación, en la **Repositorios** , seleccione el botón de los tres puntos de la fila que representa el repositorio de GitHub que acaba de añadir y seleccione **Validación de propiedad** en el menú desplegable.

## Cómo utilizar sus propios repositorios de GitHub con Cloud Manager {#using}

Una vez validado el repositorio de GitHub en Cloud Manager, la integración se completa y puede utilizarlo con Cloud Manager.

1. Al crear una solicitud de extracción, se inicia automáticamente una comprobación de GitHub.

   ![Comprobaciones de GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Para cada solicitud de extracción, se crea automáticamente una [canalización de calidad de código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Esta canalización se inicia en cada actualización de solicitud de extracción.

1. La comprobación de GitHub permanece en estado de ejecución hasta que se completen las comprobaciones de calidad del código. Los resultados de calidad del código se propagan a la comprobación de GitHub.

   ![Comprobaciones de calidad del código de GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Cuando se cierra o se combina la solicitud de extracción, la canalización de calidad del código de pila completa creada se elimina automáticamente.

## Restricciones {#limitations}

Limitaciones al utilizar sus propios repositorios de GitHub con Cloud Manager.

* No puede usar los repositorios de GitHub como el origen del repositorio directo para las canalizaciones que administra.
   * Esta funcionalidad está planificada.
* No puede pausar la validación de la solicitud de extracción mediante la comprobación de GitHub desde Cloud Manager.
   * Si el repositorio de GitHub se valida en Cloud Manager, Cloud Manager siempre intentará validar las solicitudes de extracción creadas para ese repositorio.
Si la aplicación de GitHub de Adobe se quita de su organización de GitHub, se eliminará la función de validación de solicitudes de extracción de todos los repositorios.
