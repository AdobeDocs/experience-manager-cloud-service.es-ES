---
title: Integración con Adobe Target
description: 'Integración con Adobe Target '
translation-type: tm+mt
source-git-commit: 8063a41d079b8b959b903aa0f97068a42a22d840
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 2%

---


# Integración con Adobe Target{#integrating-with-adobe-target}

Como parte del Adobe Marketing Cloud, Adobe Target le permite aumentar la relevancia del contenido mediante la determinación de objetivos y la medición en todos los canales. La integración de Adobe Target y AEM como Cloud Service requiere:

* uso de la IU táctil para crear una configuración de Analytics en AEM como Cloud Service (se requiere la configuración de IMS).
* agregar y configurar Adobe Analytics como una extensión en [Adobe Launch](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html).

La integración con Launch es necesaria para la &quot;segmentación de experiencias&quot;. Para la exportación de fragmentos de experiencia a Destinatario solo necesita la Configuración de Adobe Target y el IMS.

>[!NOTE]
>
>Adobe Experience Manager como cliente Cloud Service que no tiene una cuenta de Destinatario existente, puede solicitar acceso al Destinatario Foundation Pack para Experience Cloud.  Foundation Pack proporciona un uso limitado del Destinatario por volumen.

## Creación de la configuración de Adobe Target {#create-configuration}

1. Vaya a **Herramientas** → **Cloud Service**.
   ![](assets/cloudservice.png "NavegaciónNavegación")
2. Seleccione **Adobe Target**.
3. Haga clic en el botón **Crear** .
   ![](assets/tenant.png "CreateCreate")
4. Rellene los detalles (consulte a continuación) y seleccione **Connect**.
   ![](assets/open_screen.png "ConnectConnect")

### Configuración de IMS

Se necesita una configuración IMS tanto para Launch como para Destinatario para integrar correctamente Destinatario con AEM y Launch. Mientras que la configuración de IMS para Launch está preconfigurada en AEM como Cloud Service, se debe crear la configuración de IMS de Destinatario (después de aprovisionar Destinatario). Consulte [este vídeo](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) y [esta página](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html) para obtener información sobre cómo crear la configuración de IMS de Destinatario.

### Edición de la configuración de Destinatario {#edit-target-configuration}

Para editar la configuración de Destinatario, siga estos pasos:

1. Seleccione una configuración existente y haga clic en **Propiedades**.
2. Edite las propiedades.
3. Select **Re-connect to Adobe Target**.
   ![Volver a](assets/edit_config_page.png "conectarVolver a conectar")
4. Seleccione **Guardar y cerrar**.

### Añadir una configuración en un sitio {#add-configuration}

Para aplicar una configuración de IU táctil a un sitio, vaya a: **Sitios** → **Seleccione cualquier página** del sitio → **Propiedades** → **Avanzadas** → **Configuración** → Seleccione el inquilino de configuración.

## Integración de Adobe Target en sitios AEM mediante Adobe Launch {#integrate-target-launch}

AEM ofertas y la integración lista para usar con Experience Platform Launch. Al agregar la extensión de Adobe Target al Experience Platform Launch, puede utilizar las funciones de Adobe Target en AEM página web. Las bibliotecas de Destinatario solo se procesarán con Launch.

>[!NOTE]
>
>Los marcos existentes (heredados) siguen funcionando, pero no se pueden configurar en la IU táctil. Es aconsejable volver a compilar las configuraciones de asignación de variables en Launch.

>[!NOTE]
>
>Los marcos existentes (heredados) siguen funcionando, pero no se pueden configurar en la IU táctil. Es aconsejable volver a compilar las configuraciones de asignación de variables en Launch.

Como información general, los pasos de integración son:

1. Crear una propiedad de inicio
2. Añadir las extensiones requeridas
3. Creación de un elemento de datos (para capturar parámetros de concentrador de contexto)
4. Crear una regla de página
5. Generar y publicar

### Creación de una propiedad de inicio {#create-property}

Una propiedad es un contenedor que se rellenará con extensiones, reglas y elementos de datos.

1. Seleccione el botón **Nueva propiedad** .
2. Proporcione un nombre para la propiedad.
3. Como dominio, introduzca la dirección IP/host en la que desea cargar la biblioteca de inicio.
4. Seleccione el botón **Guardar** .
   ![](assets/properties_newproperty.png "LaunchpropertyLaunchproperty")

### Añadir las extensiones necesarias {#add-extension}

Extensiones es el contenedor que administra la configuración de la biblioteca principal. La extensión de Adobe Target admite implementaciones de cliente mediante el SDK de JavaScript de Destinatario para la web moderna, at.js. Debe agregar las extensiones **Adobe Target** y **Adobe de ContextHub** .

1. Seleccione la opción Catálogo de extensiones y busque Destinatarios en el filtro.
2. Seleccione **Adobe Target** at.js y haga clic en la opción Instalar.
   ![Búsqueda de Destinatario](assets/search_ext.png "SearchTarget")
3. Select the **Configure** button. Observe la ventana de configuración con las credenciales de cuenta de Destinatario importadas y la versión de at.js para esta extensión.
4. Seleccione **Guardar** para agregar la Extensión de grupo de destinatarios a la propiedad Launch. Debería poder ver la Extensión de grupo de destinatarios en la lista Extensiones **** instaladas.
   ![Guardar extensión](assets/configure_extension.png "ExtensionSave")
5. Repita los pasos anteriores para buscar la extensión de **Adobe ContextHub** e instalarla (esto es necesario para la integración con parámetros de contexto, según la cual se realizará la segmentación).

### Creación de un elemento de datos {#data-element}

Los elementos de datos son los marcadores de posición a los que se pueden asignar parámetros de concentrador de contexto.

1. Seleccione Elementos **de datos**.
2. Seleccione **Añadir elemento** de datos.
3. Proporcione el nombre del elemento de datos y asígnelo a un parámetro de concentrador de contexto.
4. select **Save**.
   ![Elemento Data](assets/data_elem.png "ElementData")

### Creación de una regla de página {#page-rule}

En Regla, definimos y ordenamos una secuencia de acciones, que se ejecutarán en el sitio, para lograr objetivos.

1. Añada un conjunto de acciones como se muestra en la captura de pantalla.
   ![](assets/rules.png "ActionsActions")
2. En Añadir parámetros a todos los mboxes, agregue el elemento de datos configurado anteriormente (consulte el elemento de datos anterior) al parámetro que se enviará en la llamada de mbox.
   ![](assets/map_data.png "MboxActions")

### Generar y publicar {#build-publish}

Para saber cómo crear y publicar, diríjase a esta [página](https://docs.adobe.com/content/help/en/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html).

## Cambios en la estructura de contenido entre las configuraciones de IU clásica y táctil {#changes-content-structure}

| **Cambiar** | **Configuración de IU clásica** | **Configuración de IU táctil** | **Consecuencias** |
|---|---|---|---|
| Ubicación de la Configuración de Destinatario. | /etc/cloudservices/testandtarget/ | /conf/inquilino/settings/cloudservices/destinatario | Anteriormente, había varias configuraciones presentes en /etc/cloudservices/testandtarget, pero ahora una sola configuración estará presente en un inquilino. |

>[!NOTE]
>
>Las configuraciones heredadas siguen siendo compatibles con los clientes existentes (sin la opción de editar o crear nuevas). Las configuraciones heredadas formarán parte de los paquetes de contenido cargados por el cliente mediante VSTS.
