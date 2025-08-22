---
title: ¿Cómo se añaden vínculos de formularios en la página de AEM Sites mediante el componente de vínculo del Portal de formularios?
description: Obtenga información sobre cómo añadir vínculos de formularios a la página de AEM Sites.
feature: Adaptive Forms, Core Components
role: User, Developer, Admin
exl-id: a55d0776-8827-46cc-9625-5d6f5f6bda3b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 97%

---

# Añadir vínculos de formularios a una página de AEM Sites

En el escenario del sitio web del banco, el componente **Vínculo** del Portal de formularios mejora la navegación al guiar a los usuarios a formularios específicos en varias secciones del sitio. Proporciona referencias directas a formularios como solicitudes de préstamos, formularios de apertura de cuentas o encuestas de comentarios, ubicados estratégicamente en todo el sitio web. El componente **Vínculo** inserta vínculos que dirigen a los usuarios a formularios adaptables específicos dentro de la página de Sites. Por ejemplo, en el sitio web del banco, los usuarios anónimos pueden acceder a un formulario de consulta general, mientras que los usuarios conectados pueden acceder directamente a formularios más seguros, como solicitudes de préstamos o formularios de autorización de transacciones.

![Icono de vínculo](/help/forms/assets/link-forms.png)

## Requisito previo

Antes de explorar las distintas funcionalidades de un componente del Portal de formularios, asegúrese de que los componentes principales estén habilitados para su entorno. Instale la última versión para habilitar los componentes principales adaptables de Forms para su entorno de AEM Cloud Service.

Después de implementar los componentes principales más recientes en su entorno, los componentes del Portal de formularios pasan a ser accesibles en el entorno de creación.

## Añadir el componente Vínculo a la página de Sites

Para añadir el componente de portal **Vínculo** a su página de Sites, siga estos pasos:

1. Abra la página de AEM Sites en el modo **Editar**.
1. Vaya a la **[!UICONTROL Información de la página]** > **[!UICONTROL Editar plantilla]**
   ![Editar la política de plantilla](/help/forms/assets/save-form-as-draft-edit-template.png)

1. Haga clic en la **[!UICONTROL Política]** y seleccione la casilla de verificación **[!UICONTROL Vínculo]** bajo el **[Nombre del proyecto de tipo de archivo de AEM] - Portal de formularios y comunicaciones**.

   ![Selección de política](/help/forms/assets/add-link.png)

1. Haga clic en **[!UICONTROL Listo]**.
1. A continuación, vuelva a abrir la página de AEM Sites en el modo de creación.
1. Busque la sección en el editor de páginas que le permite añadir el componente del Portal de formularios.

1. Haga clic en el icono **Añadir**. El icono es un signo más (+) que representa la opción de añadir nuevos componentes.

   Al hacer clic en el icono **Añadir** aparece un cuadro de diálogo **Insertar nuevo componente** que muestra varios componentes para su inserción.

   >[!NOTE]
   >
   > También puede arrastrar y soltar el componente.

1. Examine los componentes disponibles en el cuadro de diálogo y seleccione el componente que desee en la lista. Por ejemplo, seleccione el componente **Vínculo** de la lista para añadir el componente **Vínculo** del Portal de formularios.

   ![Componente Vínculo](/help/forms/assets/add-link-in-sites.png)

Ahora, configure las propiedades del componente **Vínculo**.

## Comprender las propiedades del componente Vínculo

Puede personalizar fácilmente las propiedades del componente **Vínculo** mediante el cuadro de diálogo de configuración para garantizar una experiencia del usuario perfecta. Para configurarlo, seleccione el componente y, a continuación, seleccione el icono ![Configurar](assets/configure_icon.png). Se abrirá el cuadro de diálogo **[!UICONTROL Vínculo]**.

### Pestaña Mostrar

![Pestaña Mostrar](/help/forms/assets/link-asset-tab.png)

En la pestaña **[!UICONTROL Mostrar]**, proporcione el pie de ilustración del vínculo y la información del objeto para facilitar la identificación de los formularios representados por el vínculo.

### Pestaña Información del recurso

![Pestaña Información del recurso](/help/forms/assets/link-asset-info.png)

En la pestaña **[!UICONTROL Información del activo]**, especifique la ruta del repositorio donde se almacena el activo.

### Pestaña Parámetros de consulta

![Pestaña Parámetros de consulta](/help/forms/assets/link-query-tab.png)

En la pestaña **[!UICONTROL Parámetros de consulta]**, especifique los parámetros adicionales en el formato de par clave-valor. Cuando se hace clic en el vínculo, estos parámetros adicionales se pasan junto con el formulario.

## Ver los vínculos de formularios en la página de Sites mediante el componente Vínculo

Obtenga una vista previa de la página de Sites para ver el vínculo a un formulario adaptable, que se especifica en la pestaña de propiedades de **Información de recursos** del componente **Vínculo**. Al hacer clic en el vínculo, se muestra el formulario en pantalla para los usuarios, que pueden acceder a él en función de los permisos.

![Ficha Parámetros de consulta](/help/forms/assets/link-forms.png)

## Artículos relacionados

{{forms-portal-see-also}}

## Consulte también {#see-also}

{{see-also}}
