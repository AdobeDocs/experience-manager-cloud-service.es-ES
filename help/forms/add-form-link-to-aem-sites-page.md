---
title: ¿Cómo se agregan vínculos de formularios en la página de AEM Sites mediante el componente Vínculo al portal de Forms?
description: Obtenga información sobre cómo agregar vínculos de formularios a la página de AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
source-git-commit: 58533d9a950fa4dc0e043ef8cb935d65fc68d233
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 16%

---


# Agregar vínculos de formulario a la página Sitios

En el escenario del sitio web del banco, el componente **Vínculo** del portal de Forms mejora la navegación al guiar a los usuarios a formularios específicos en varias secciones del sitio. Proporciona referencias directas a formularios como solicitudes de préstamos, formularios de apertura de cuentas o encuestas de comentarios, ubicados estratégicamente en todo el sitio web. El componente **Link** inserta vínculos que dirigen a los usuarios a Forms adaptables específicos dentro de la página de Sites. Por ejemplo, en el sitio web del banco, los usuarios anónimos pueden acceder a un formulario de consulta general, mientras que los usuarios conectados pueden acceder directamente a formularios más seguros, como solicitudes de préstamos o formularios de autorización de transacciones.

![Icono de vínculo](/help/forms/assets/link-forms.png){width="250" align="center"}

## Requisito previo

Antes de explorar las distintas funcionalidades de un componente del portal de Forms, asegúrese de que los componentes principales estén habilitados para su entorno. Para obtener instrucciones detalladas sobre cómo habilitar los componentes principales para su entorno, [haga clic aquí](/help/forms/enable-adaptive-forms-core-components.md).

Después de implementar los componentes principales más recientes en su entorno, los componentes del portal de Forms pasan a ser accesibles en el entorno de creación.

## Añadir el componente Vínculo a la página de Sites

Para agregar el componente de portal **Link** a su página de Sites, realice los siguientes pasos:

1. Abra la página de AEM Sites en modo **Editar**.
1. Vaya a la **[!UICONTROL Información de la página]** > **[!UICONTROL Editar plantilla]**
   ![Editar directiva de plantilla](/help/forms/assets/save-form-as-draft-edit-template.png){width="250" align="center"}

1. AEM Haga clic en la **[!UICONTROL directiva]** y seleccione la casilla de verificación **[!UICONTROL Vínculo]** bajo el **[Nombre de proyecto de tipo de archivo de] - Portal de Forms y comunicaciones**.

   ![Selección de directiva](/help/forms/assets/add-link.png){width="250" align="center"}

1. Haga clic en **[!UICONTROL Listo]**.
1. A continuación, vuelva a abrir la página de AEM Sites en el modo Autor.
1. Busque la sección en el editor de páginas que le permite agregar el componente Portal de Forms.

1. Haga clic en el icono **Agregar**. El icono es un signo más (+) que significa la opción de agregar nuevos componentes.

   Al hacer clic en el icono **Agregar**, se muestra un cuadro de diálogo **Insertar nuevo componente** que muestra varios componentes para su inserción.

   >[!NOTE]
   >
   > También puede arrastrar y soltar el componente.

1. Examine los componentes disponibles en el cuadro de diálogo y seleccione el componente que desee en la lista. Por ejemplo, seleccione el componente **Link** de la lista para agregar el componente **Link** Forms Portal.

   ![Componente de vínculo](/help/forms/assets/add-link-in-sites.png){width="250" align="center"}

Ahora, configure las propiedades del componente **Link**.

## Comprender las propiedades del componente Vínculo

Puede personalizar fácilmente las propiedades del componente **Link** mediante el Cuadro de diálogo de configuración para una experiencia de usuario perfecta. Para configurarlo, seleccione el componente y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png). Se abre el cuadro de diálogo **[!UICONTROL Vínculo]**.

### Pestaña Mostrar

![Ficha de visualización](/help/forms/assets/link-asset-tab.png){width="250" align="center"}

En la pestaña **[!UICONTROL Mostrar]**, proporcione el pie de ilustración del vínculo y la información del objeto para facilitar la identificación de los formularios representados por el vínculo.

### Pestaña Información del recurso

![Ficha Información de Assets](/help/forms/assets/link-asset-info.png){width="250" align="center"}

En la pestaña **[!UICONTROL Información del activo]**, especifique la ruta del repositorio donde se almacena el activo.

### Pestaña Parámetros de consulta

![Ficha Parámetros de consulta](/help/forms/assets/link-query-tab.png){width="250" align="center"}

En la pestaña **[!UICONTROL Parámetros de consulta]**, especifique los parámetros adicionales en el formato de par clave-valor. Cuando se hace clic en el vínculo, estos parámetros adicionales se pasan junto con el formulario.

## Ver vínculos de formularios en la página de Sites mediante el componente Vínculo

Obtenga una vista previa de la página de Sites para ver el vínculo a un formulario adaptable, que se especifica en la pestaña de propiedades de **Información de Assets** del componente **Vínculo**. Al hacer clic en el vínculo, se muestra el formulario en pantalla para los usuarios, que pueden acceder a él en función de los permisos.

![Ficha Parámetros de consulta](/help/forms/assets/link-forms.png){width="250" align="center"}

## Artículos relacionados

{{forms-portal-see-also}}

## Consulte también {#see-also}

{{see-also}}
