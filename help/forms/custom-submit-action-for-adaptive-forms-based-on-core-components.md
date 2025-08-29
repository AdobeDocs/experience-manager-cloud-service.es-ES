---
title: Crear una acción de envío personalizada para un formulario adaptable basada en componentes principales
description: Obtenga información sobre cómo crear una acción de envío personalizada para un Forms adaptable para procesar datos antes de enviarlos mediante la acción de envío personalizada.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
exl-id: a369b585-d148-4b5a-8afe-d5673ea865d0
source-git-commit: 03e46bb43e684a6b7057045cf298f40f9f1fe622
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 23%

---

# Crear una acción de envío personalizada para un Forms adaptable (componentes principales)

Una acción de envío permite a los usuarios seleccionar el destino de los datos capturados desde un formulario y definir la funcionalidad adicional que se ejecutará al enviarlo. El formulario de AEM admite varias [acciones de envío listas para usar (OOTB)](/help/forms/configure-submit-actions-core-components.md), como enviar un correo electrónico o guardar datos en SharePoint o OneDrive.

También puede crear una acción de envío personalizada para agregar una funcionalidad que no esté incluida en las [opciones predeterminadas](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action). Por ejemplo, integre los datos del formulario con una aplicación de terceros o envíe un déclencheur de notificación SMS personalizado en función de los datos introducidos por el usuario.

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## Requisitos previos

Antes de empezar a crear la primera acción de envío personalizada para Forms adaptable, asegúrese de que dispone de lo siguiente:

* **Editor de texto sin formato (IDE)**: Aunque cualquier editor de texto sin formato puede funcionar, un entorno de desarrollo integrado (IDE) como Microsoft Visual Studio Code ofrece características avanzadas para facilitar la edición.

* **Git**: este sistema de control de versiones es necesario para administrar los cambios de código. Si no lo tiene instalado, descárguelo de https://git-scm.com.

## Creación de la primera acción de envío personalizada para el formulario

El diagrama siguiente muestra los pasos para crear una acción de envío personalizada para un formulario adaptable:

![Flujo de trabajo de acción de envío personalizado](/help/forms/assets/custom-submit-action-workflow.png){width=50%, height-50%}

### Clone el repositorio Git de AEM as a Cloud Service.

1. Abra la línea de comandos y seleccione un directorio para almacenar el repositorio de AEM as a Cloud Service, como `/cloud-service-repository/`.

1. Ejecute el siguiente comando para clonar el repositorio:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **¿Dónde se encuentra esta información?**

   Para obtener instrucciones paso a paso sobre cómo localizar estos detalles, consulte el artículo de Adobe Experience League “[Acceder a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git)”.

   **Su proyecto está listo.**

   Cuando el comando se complete correctamente, verá que se ha creado una nueva carpeta en su directorio local. Esta carpeta recibe el nombre de su aplicación (por ejemplo, app-id). Esta carpeta contiene todos los archivos y el código descargados del repositorio de Git de AEM as a Cloud Service. Puede encontrar `<appid>` para su proyecto de AEM en el archivo `archetype.properties`.

   ![Propiedades de tipo de archivo](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   En esta guía, nos referimos a esta carpeta como `[AEMaaCS project directory]`.

## Agregar nueva acción de envío

1. Abra la carpeta del repositorio en un editor.

   ![Repositorio clonado](/help/forms/assets/custom-submit-action-clone-repo.png)

1. Vaya al siguiente directorio dentro de su `[AEMaaCS project directory]`:

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **Importante**: reemplace `<app-id>` por su ID de aplicación real.

1. Cree una nueva carpeta para la acción de envío personalizada y asígnele un nombre de su elección. Por ejemplo, asigne a la carpeta el nombre `customsubmitaction`.

   ![Crear carpeta de acciones de envío personalizada](/help/forms/assets/custom-submit-action-create-folder.png)

1. Vaya al directorio de acciones de envío personalizado agregado.

   Dentro de su `[AEMaaCS project directory]`, vaya a la siguiente ruta:

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`: reemplace `<app-id>` por su ID de aplicación real.

1. Cree un nuevo archivo de configuración.
Dentro de la carpeta `customsubmitaction`, cree un nuevo archivo con el nombre `.content.xml`.

   ![Crear archivo de configuración](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. Abra este archivo y pegue el siguiente contenido; reemplace `[customsubmitaction]` por el nombre de su acción de envío

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   Por ejemplo, reemplace `[customsubmitaction]` por su nombre de acción de envío personalizado como `Custom Submit Action`.

   ![Crear archivo de configuración de acción de envío personalizado](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > Recuerde el nombre de [customsubmitaction], ya que el mismo nombre aparecerá en la lista desplegable `Submit action` durante la creación de un formulario.


**Incluir la nueva carpeta en`filter.xml`**

1. Vaya al archivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` en su [directorio del proyecto AEMaaCS].

1. Abra el archivo y añada la siguiente línea al final:

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   Por ejemplo, agregue la línea de código siguiente para agregar la carpeta `customsubmitaction` en el archivo `filter.xml`:

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![Agregue las carpetas creadas en el filter.xml](/help/forms/assets/custom-submit-action-filter-xml.png)

1. Guarde los cambios.

### Implemente el servicio para la acción de envío agregada.

1. Vaya al siguiente directorio dentro de su `[AEMaaCS project directory]`:
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`: reemplace `<app-id>` por su ID de aplicación real.
1. Cree un nuevo archivo Java para implementar el servicio para la acción de envío agregada. Por ejemplo, agregue el nuevo archivo Java como `CustomSubmitService.java`.

   ![Carpeta de acción de envío personalizada](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. Abra este archivo y agregue el código para la implementación de acción de envío personalizada.

   Por ejemplo, el siguiente código Java es un servicio OSGi que administra el envío del formulario registrando los datos enviados y devuelve un estado `OK`. Agregue el siguiente código al archivo `CustomSubmitService.java`:

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![Servicio de acción de envío personalizada](/help/forms/assets/custom-submit-action-service.png)

1. Guarde los cambios.

### Implemente el código de.

**Implementar código para el entorno de desarrollo local**

* Implemente AEM as a Cloud Service `[AEMaaCS project directory]` en el entorno de desarrollo local para probar la nueva acción de envío en el equipo local. Para implementarlo en su entorno de desarrollo local:

   1. Asegúrese de que el entorno de desarrollo local esté activo y en funcionamiento. Si aún no ha configurado un entorno de desarrollo local, consulte la guía de [Configuración de un entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Abra la ventana del terminal o el símbolo del sistema.

   1. Vaya a `[AEMaaCS project directory]`.

   1. Ejecute el siguiente comando:

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![Implementación local](/help/forms/assets/custom-submit-action-local-deployment.png)

**Implementar el código para el entorno de Cloud Service**

* Implemente AEM as a Cloud Service `[AEMaaCS project directory]` en su entorno de Cloud Service. Para implementarlo en el entorno de Cloud Service:

   1. Confirme los cambios:

      Después de agregar la nueva configuración de acción de envío personalizada, confirme los cambios con un mensaje Git claro. (Por ejemplo, &quot;Se ha añadido una nueva acción de envío personalizada&quot;).

   1. Implemente el código actualizado:

      Active una implementación del código a través de la [canalización de pila completa existente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline). Genera e implementa automáticamente el código actualizado con la nueva compatibilidad de acción de envío personalizada.

      Si aún no ha configurado una canalización, consulte la guía sobre [cómo configurar una canalización para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline).

      ![Implementación en la nube](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **¿Cómo confirmar la instalación?**

      Una vez que el proyecto se haya creado correctamente, la acción de envío personalizada aparece en la lista desplegable `Submit action` durante la creación de un formulario.

      ![Lista desplegable Acción de envío personalizada](/help/forms/assets/custom-submit-action-drop-down-list.png)

  Su entorno ya está listo para usar la acción de envío personalizada agregada al crear un formulario.

### Vista previa de un formulario adaptable con una acción de envío recién agregada

1. Inicie sesión en la instancia de AEM Forms as a Cloud Service.
1. Vaya a **Formularios** > **Formularios y documentos**.

   ![Forms y documentos](/help/forms/assets/custom-submit-action-fnd.png)

1. Seleccione un formulario adaptable y haga clic en **Editar**. El formulario se abrirá en modo de edición.

   ![Editar formulario](/help/forms/assets/custom-submit-action-edit-af.png)

1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Haga clic en la pestaña **[!UICONTROL Envío]**.
1. En la lista desplegable **[!UICONTROL Enviar acción]**, seleccione la acción de envío. Por ejemplo, seleccione la acción de envío como `Custom Submit Action`.

   ![Formulario de envío personalizado](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. Complete el formulario y envíelo.

   ![Enviar formulario](/help/forms/assets/custom-submit-action-submit-form.png)

   ![Mensaje de agradecimiento](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   Una vez que el formulario se haya enviado correctamente, puede comprobar la **configuración de la consola web de Adobe Experience Manager** para comprobar la acción de envío personalizada en el entorno de desarrollo local.
1. Vaya a `http://<host>:<port>/system/console/configMgr`.

1. Vaya a **Compatibilidad con registros de la consola web de Adobe Experience Manager** en `http://<host>:<port>/system/console/slinglog`.

   ![Administrador de configuración](/help/forms/assets/custom-submit-action-sling-log.png)

1. Haga clic en la opción `logs/error.log`.
   ![Abrir archivo error.log](/help/forms/assets/custom-submit-action-error-log.png)

1. Abra el archivo `error.log` para ver que se le han agregado los datos.

   ![archivo error.log](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > * Para ver los registros de errores en el entorno de AEM as a Cloud Service, puede utilizar Splunk.
   > * Si un servicio de acción de envío personalizada encuentra un error no controlado, AEM as a Cloud Service devuelve una página de error 502 HTML.


## Preguntas frecuentes

**Q: ¿Por qué mi formulario adaptable muestra una página de error 5.x.x después del envío?**
Error no controlado en el servicio de acción de envío personalizada. A continuación, AEM Cloud Service devuelve su página de error predeterminada.

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## Artículos relacionados

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->
