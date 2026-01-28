---
title: Añadir un repositorio privado de GitHub en Cloud Manager
description: Obtenga información sobre cómo configurar Cloud Manager para que funcione con sus propios repositorios privados de GitHub.
exl-id: 5232bbf5-17a5-4567-add7-cffde531abda
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 892339482c009edf9f73560f2a4b66f4317843fe
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 34%

---

# Añadir un repositorio privado de GitHub Cloud en Cloud Manager {#private-repositories}

Si configura Cloud Manager para que se integre con su GitHub Cloud privado (repositorios alojados en `github.com`), podrá validar su código directamente en GitHub mediante Cloud Manager. Esta configuración elimina el requisito de sincronizar el código regularmente con el repositorio de Adobe.

>[!NOTE]
>
>También puede añadir los siguientes tipos de repositorios con los webhooks:
>
>* Repositorios de GitHub Enterprise Server (versión autoalojada de GitHub)
>* Repositorios de GitLab (tanto `gitlab.com` como versiones autohospedadas de GitLab).
>* Repositorios de Bitbucket (tanto `bitbucket.org` como Bitbucket Server, la versión autoalojada de BitBucket).
>* Repositorios de Azure DevOps (tanto [dev.azure.com](https://azure.microsoft.com/en-us/products/devops/?nav=min) como versiones autohospedadas de Azure DevOps).
>
>Consulte [Agregar repositorios externos en Cloud Manager - beta privada](/help/implementing/cloud-manager/managing-code/external-repositories.md).

<!-- CONSIDER ADDING MORE DETAIL... THE WHY. Some key points about this capability include the following:

* **Direct Integration**: With this setup, you can directly link your private GitHub repositories to Cloud Manager, allowing for seamless code validation, deployment, and CI/CD (Continuous Integration/Continuous Deployment) pipelines without needing to maintain a separate sync process with Adobe's default Git repository.

* **Customization and Autonomy**: Companies often prefer managing their own source code repositories for security, control, and integration purposes. "Build your own GitHub" allows organizations to maintain their internal development processes while leveraging the full functionality of Cloud Manager for building, testing, and deploying AEM (Adobe Experience Manager) applications.

* **Simplified Workflow**: It reduces the overhead of synchronizing code between multiple repositories by allowing Cloud Manager to access the organization's private repository directly, making the development cycle faster and more efficient.

* **CI/CD Pipelines**: Teams can still benefit from Adobe Cloud Manager's automated build, test, and deployment processes, as the integration allows the CI/CD pipelines to pull code from the organization's own GitHub repository.

In essence, a "Build your own GitHub" in Adobe Cloud Manager empowers teams to manage their own GitHub repositories while still using the robust deployment and validation capabilities of Cloud Manager.

>[!NOTE]
>
>This feature is exclusive to public GitHub. Support for self-hosted GitHub is not available. -->

## Configuración {#configuration}

La configuración de un repositorio privado de GitHub Cloud en Cloud Manager consta de dos pasos:

1. [Agregar un repositorio privado de GitHub Cloud](#add-repo) a un programa seleccionado.
1. A continuación, [valide la propiedad del repositorio privado de GitHub Cloud](#validate-ownership).



### Añadir un repositorio privado de GitHub Cloud a un programa {#add-repo}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa al que desea vincular un repositorio Git privado.

1. En el menú lateral, en **Servicios**, seleccione ![Icono de carpeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **Repositorios**.

   ![La página Repositorios](/help/implementing/cloud-manager/managing-code/assets/repositories-tab.png)

1. Cerca de la esquina superior derecha de la página **Repositorios**, haga clic en **Añadir repositorio**.

1. En el diálogo **Añadir repositorio**, seleccione **Repositorio privado** como el tipo de repositorio.

   ![Añadir su propio repositorio](/help/implementing/cloud-manager/assets/repos/add-own-github.png)

1. En cada campo respectivo, proporcione los siguientes detalles sobre el repositorio:

   | Campo | Descripción |
   | --- | --- |
   | Nombre del repositorio | Un nombre expresivo para el nuevo repositorio. |
   | URL del repositorio | La dirección URL del repositorio privado, que debe finalizar en `.git`.<br>Por ejemplo, *`https://github.com/org-name/repo-name.git`* (la ruta de URL es solo para fines ilustrativos). |
   | Descripción (opcional) | Breve descripción del repositorio. |

1. Seleccione **Guardar**.
Ahora, puede [validar la propiedad del repositorio privado](#validate-ownership).

>[!TIP]
>
>Para obtener más información sobre la administración de repositorios en Cloud Manager, consulte el documento [Repositorios de Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).


### Validar la propiedad de un repositorio privado de GitHub {#validate-ownership}

Cloud Manager ahora conoce su repositorio de GitHub, pero aún necesita acceso. Para otorgar acceso, debe instalar la aplicación de GitHub de Adobe y comprobar que es el propietario del repositorio especificado.

**Para validar la propiedad de un repositorio privado de GitHub:**

1. Después de agregar su propio repositorio, siga los pasos restantes del cuadro de diálogo **Validación de propiedad del repositorio privado**.

   ![Validación de propiedad de repositorio privado](/help/implementing/cloud-manager/assets/repos/private-repo-validate.png)

   |  | Descripción |
   | --- | --- |
   | **Paso 1: Aplicación GitHub** | Cloud Manager utiliza una aplicación de GitHub para interactuar con su repositorio privado de forma segura.<br>· Un propietario de su organización de GitHub debe instalar la aplicación ubicada en `https://github.com/apps/cloud-manager-for-aem` y conceder acceso al repositorio.<br>· Para obtener más información sobre cómo instalar y conceder acceso, consulte la documentación de GitHub. |
   | **Paso 2: Archivo Secreto** | Para mejorar la seguridad, debe crear un archivo secreto en la rama predeterminada del repositorio.<br>· Haga clic en **Generar** y luego haga clic en **Confirmar**. Cloud Manager genera el contenido del archivo privado en el campo de texto **Contenido de archivo secreto**.<br>· Haga clic en ![Icono de copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar el contenido de ese campo. El contenido del archivo secreto solo se mostrará una vez. Si no copia el contenido antes de cerrar este cuadro de diálogo, vuelva a generar el secreto. |

1. Cree un nuevo archivo en la rama predeterminada de su repositorio de GitHub llamado:

   `.well-known/adobe/cloud-manager-challenge`

1. Pegue el contenido del archivo secreto en el nuevo archivo que acaba de crear y guarde.

   Una vez que la aplicación esté instalada y el archivo secreto exista en el repositorio, continúe con el paso.

1. En el cuadro de diálogo **Validación de propiedad de repositorio privado**, haga clic en **Validar**.

La aplicación se puede instalar y se puede crear un archivo secreto en cualquier orden. Sin embargo, ambos pasos deben completarse antes de poder validar.

Hasta la validación, el repositorio se muestra con un icono rojo que indica que aún no se ha validado y que todavía no se puede utilizar.

![Repositorio no validado](/help/implementing/cloud-manager/assets/repos/unvalidated-repo.png)

La columna **Tipo** de la tabla de la página **Repositorios** identifica los repositorios proporcionados por Adobe (**Adobe**) y sus propios repositorios privados (**GitHub**).

Si necesita volver al repositorio más tarde para completar la validación, en la página **Repositorios**, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en la fila que representa el repositorio de GitHub que acaba de agregar. En la lista desplegable, seleccione **Validación de propiedad**.



## Uso de repositorios privados de GitHub Cloud con Cloud Manager {#using}

Una vez validado el repositorio de GitHub en Cloud Manager, la integración se completa. Puede utilizar el repositorio con Cloud Manager.

**Para usar repositorios de GitHub Cloud privados con Cloud Manager:**

1. Al crear una solicitud de extracción, se inicia automáticamente una comprobación de GitHub.

   ![Comprobaciones de GitHub](/help/implementing/cloud-manager/assets/repos/github-checks.png)

1. Para cada solicitud de extracción, se crea automáticamente una [canalización de calidad de código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md). Esta canalización se inicia en cada actualización de solicitud de extracción.

1. La comprobación de GitHub permanece en estado de ejecución hasta que se complete la comprobación de calidad del código. Los resultados de calidad del código se propagan a la comprobación de GitHub.

   ![Comprobaciones de calidad del código de GitHub](/help/implementing/cloud-manager/assets/repos/github-code-quality.png)

Cuando se combina o cierra la solicitud de extracción, la canalización de calidad del código de pila completa creada se elimina automáticamente.

>[!TIP]
>
>Consulte [Anotaciones de comprobación de GitHub](github-annotations.md) para obtener más información sobre la información que proporciona GitHub cuando se ejecutan las comprobaciones de solicitudes de extracción.

>[!TIP]
>
>Puede controlar las canalizaciones que se crean automáticamente para validar cada solicitud de extracción en un repositorio privado. Consulte el documento [Configuración de comprobación de GitHub para repositorios privados](github-check-config.md) para obtener más información.



## Asociar repositorios privados de GitHub Cloud con canalizaciones {#pipelines}

Los repositorios privados validados se pueden asociar a [canalizaciones de pila completa y front-end.](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)



## Limitaciones {#limitations}

Se aplican ciertas restricciones al usar repositorios privados con Cloud Manager.

* No se creará ni insertará ninguna etiqueta de Git al utilizar repositorios privados en canalizaciones de producción de pila completa.
* Si la aplicación de Adobe GitHub se elimina de su organización de GitHub, se elimina la función de validación de solicitudes de extracción de todos los repositorios.
* Las canalizaciones que utilizan repositorios privados de GitHub Cloud y el déclencheur de compilación &quot;en el momento de la confirmación&quot; no se inician automáticamente cuando se inserta una nueva confirmación en la rama seleccionada.
* La [funcionalidad de reutilización de artefactos](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) no se aplica a repositorios privados.
* No se puede pausar la validación de la solicitud de extracción mediante la comprobación de GitHub desde Cloud Manager. Si el repositorio de GitHub se valida en Cloud Manager, Cloud Manager siempre intenta validar las solicitudes de extracción creadas para ese repositorio.
* Si su organización de GitHub aplica restricciones de IP, abra un caso de asistencia para obtener la lista de direcciones IP que deben permitirse.
