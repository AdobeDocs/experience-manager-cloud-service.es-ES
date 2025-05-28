---
title: Uso de la extensión de referencias externas de AJO de fragmentos de contenido
description: Obtenga información acerca de la extensión de referencias externas de AJO del fragmento de contenido
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
source-git-commit: f755a5c621b68b3110642e6cfe150798555b6707
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# La extensión de referencias externas del fragmento de contenido AJO {#content-fragment-external-references-extension}

Para obtener una vista previa de las experiencias de AEM en otro producto de Adobe, puede habilitar la extensión de la interfaz de usuario:

* **Referencias externas de AJO**

La extensión de referencias externas de AJO funciona recuperando referencias a fragmentos de contenido de todas las organizaciones y zonas protegidas asociadas con etiquetas predefinidas. A continuación, la extensión muestra los detalles.

Por ejemplo, para una integración con Adobe Journey Optimizer (AJO), los detalles dependen de si la referencia es una campaña, un Recorrido o una plantilla.

>[!NOTE]
>
>Para obtener más información sobre cómo habilitar la extensión, consulte [Extension Manager en AEM Experience Manager.](https://developer.adobe.com/uix/docs/extension-manager/)

Por ejemplo, para utilizar la extensión con AJO:

>[!NOTE]
>
>Consulte también [Integración de AJO](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/integrations/aem-fragments).

1. Abra la [consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

1. Vaya al fragmento de contenido: el fragmento creado y utilizado en varios canales de AJO.

1. Abra el fragmento de contenido en [editor](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment).

1. La extensión Referencias externas de AJO está disponible como pestaña en el panel derecho. Seleccione la pestaña para abrir la extensión:

   ![Extensión de referencias externas de AJO](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   Una vez seleccionado un tipo de referencia, la extensión muestra las referencias externas correspondientes como una tabla con las columnas:

   * **Nombre**: nombre de la referencia donde se usa el fragmento de contenido
   * **Vista previa** seleccione este vínculo para iniciar la vista previa
   * **Estado**: el estado de la referencia

1. Puede seleccionar **Tipo de referencia** de la lista desplegable para cambiar entre tres tipos de referencia:

   * **Campaña**
      * Muestra una lista de todas las campañas con vínculos al fragmento de contenido actual.
      * A continuación, puede previsualizar una campaña seleccionada.
      * Predeterminado
   * **Recorrido**
      * Muestra el Recorrido más reciente.
      * Puede seleccionar y previsualizar un Recorrido seleccionado.
   * **Plantilla**
      * Muestra las plantillas relacionadas con el fragmento de contenido.
      * A continuación, puede seleccionar y previsualizar una plantilla seleccionada.