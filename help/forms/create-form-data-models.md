---
title: ¿Cómo se crea el modelo de datos de formulario?
description: La integración de datos de Experience Manager Forms proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Aprenda a crear modelos de datos de formulario con o sin fuentes de datos configuradas.
feature: Form Data Model
role: User, Developer
level: Beginner, Intermediate
exl-id: b17b7441-912c-44c7-a835-809f014a8c86
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 1%

---

# Crear modelo de datos de formulario {#create-form-data-model}

![Integración de datos](do-not-localize/data-integeration.png)

[!DNL Experience Manager Forms] la integración de datos proporciona una interfaz de usuario intuitiva para crear y trabajar con modelos de datos de formulario. Un modelo de datos de formulario se basa en fuentes de datos para el intercambio de datos; sin embargo, puede crear un modelo de datos de formulario con o sin un origen de datos. Existen dos métodos para crear un desde el modelo de datos en función de si ha configurado fuentes de datos:

* **Uso de fuentes de datos preconfiguradas**: Si ha configurado las fuentes de datos tal como se describe en [Configuración de fuentes de datos](configure-data-sources.md), puede seleccionarlos al crear un modelo de datos de formulario. Incorpora todos los objetos, propiedades y servicios del modelo de datos de los orígenes de datos seleccionados que se pueden utilizar en el modelo de datos de formulario.

* **Sin fuentes de datos**: Si no ha configurado orígenes de datos para el modelo de datos de formulario, puede crearlos sin orígenes de datos. Puede utilizar el Modelo de datos de formulario para crear Forms adaptable <!--and interactive communication--> y pruébelas utilizando datos de ejemplo. Cuando hay orígenes de datos disponibles, puede enlazar el Modelo de datos de formulario con orígenes de datos, que se refleja automáticamente en el Forms adaptable asociado<!--and interactive communications-->.

>[!NOTE]
>
>Debe ser miembro de ambas **fdm-author** y **forms-user** grupos para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con su [!DNL Experience Manager] administrador para convertirse en miembro de los grupos.

## Crear modelo de datos de formulario {#data-sources}

Asegúrese de haber configurado los orígenes de datos que desea utilizar en el Modelo de datos de formulario como se describe en [Configuración de fuentes de datos](configure-data-sources.md). Para crear un Modelo de datos de formulario basado en orígenes de datos configurados, haga lo siguiente:

1. En [!DNL Experience Manager] instancia de autor, vaya a **[!UICONTROL Forms > Integraciones de datos]**.
1. Toque **[!UICONTROL Crear > Modelo de datos de formulario]**.
1. En el cuadro de diálogo Crear modelo de datos de formulario:

   * Especifique un nombre para el modelo de datos del formulario.
   * (**Opcional**) Especifique el título, la descripción y las etiquetas del modelo de datos del formulario.
   * (**Opcional y aplicable solo si se configuran fuentes de datos**) Pulse el icono de visto situado junto a la **[!UICONTROL Configuración de fuente de datos]** y seleccione el nodo de configuración donde residen los servicios en la nube para los orígenes de datos que desea utilizar. Restringe la lista de fuentes de datos disponibles para su selección en la página siguiente a las disponibles en el nodo de configuración seleccionado. Sin embargo, cualquier base de datos JDBC y [!DNL Experience Manager] las fuentes de datos de perfil de usuario se enumeran de forma predeterminada. Si no selecciona un nodo de configuración, se enumeran las fuentes de datos de todos los nodos de configuración.

1. Toque **[!UICONTROL Siguiente]**.

1. (**Aplicable únicamente si se han configurado fuentes de datos**). **[!UICONTROL Seleccionar origen de datos]** lista las fuentes de datos disponibles, si las hay. Seleccione los orígenes de datos que desee utilizar en el modelo de datos de formulario.
1. Toque **[!UICONTROL Crear]** y en el cuadro de diálogo de confirmación, pulse **[!UICONTROL Apertura]** para abrir el editor Modelo de datos de formulario.

   Vamos a revisar los diferentes componentes de la interfaz de usuario del editor del Modelo de datos de formulario.

   ![Modelo de datos de formulario con tres fuentes de datos: un servicio RESTful, [!DNL Experience Manager] perfil de usuario y un RDBMS](assets/fdm-ui.png)

   A. **[!UICONTROL Fuentes de datos]** Muestra los orígenes de datos en un modelo de datos de formulario. Expanda un origen de datos para ver los objetos y servicios del modelo de datos.

   B. **[!UICONTROL Actualizar definiciones de fuentes de datos]** Recupera cualquier cambio en las definiciones de orígenes de datos de orígenes de datos configurados y los actualiza en la ficha Fuentes de datos del editor del Modelo de datos de formulario.

   C. **[!UICONTROL Modelo]** Área de contenido en la que aparecen los objetos del modelo de datos añadidos.

   D. **[!UICONTROL Servicios]** Área de contenido en la que aparecen las operaciones o los servicios de fuentes de datos añadidos.

   E. **[!UICONTROL Barra de herramientas]** Herramientas para trabajar con el modelo de datos de formulario. La barra de herramientas muestra más opciones en función del objeto seleccionado en el modelo de datos de formulario.

   F. **[!UICONTROL Agregar selección]** Agrega objetos y servicios del modelo de datos seleccionado al modelo de datos de formulario.

Para obtener más información sobre el editor del Modelo de datos de formulario y cómo se puede trabajar con él para editar y configurar el modelo de datos de formulario, consulte [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md).

## Actualización de fuentes de datos {#update}

Haga lo siguiente para agregar o actualizar orígenes de datos a un modelo de datos de formulario existente.

1. Vaya a **[!UICONTROL Forms > Integraciones de datos]**, seleccione el Modelo de datos de formulario en el que desea agregar o actualizar orígenes de datos y pulse **[!UICONTROL Propiedades]**.
1. En las propiedades del Modelo de datos de formulario, vaya a **[!UICONTROL Actualizar origen]** pestaña .

   En el **[!UICONTROL Actualizar origen]** pestaña:

   * Toque el icono Examinar en la **[!UICONTROL Configuración según el contexto]** y seleccione un nodo de configuración en el que reside la configuración de nube para la fuente de datos que desea añadir. Si no selecciona ningún nodo, las configuraciones de nube solo residen en la variable `global` los nodos se enumeran al pulsar **[!UICONTROL Agregar fuentes]**.

   * Para agregar una fuente de datos nueva, pulse **[!UICONTROL Agregar fuentes]** y seleccione los orígenes de datos que desea agregar al modelo de datos de formulario. Todas las fuentes de datos configuradas en `global` y se muestra el nodo de configuración seleccionado, si lo hay.

   * Para reemplazar una fuente de datos existente por otra fuente de datos del mismo tipo, pulse el botón **[!UICONTROL Editar]** para la fuente de datos y seleccione en la lista de fuentes de datos disponibles.
   * Para eliminar una fuente de datos existente, pulse la tecla **[!UICONTROL Eliminar]** para la fuente de datos. El icono Eliminar está desactivado si se agrega un objeto de modelo de datos en el origen de datos en el modelo de datos del formulario.

      ![fdm-properties](assets/fdm-properties.png)

1. Toque **[!UICONTROL Guardar y cerrar]** para guardar las actualizaciones.

>[!NOTE]
>
>Una vez que agregue nuevas fuentes de datos o actualice las fuentes de datos existentes en un modelo de datos de formulario, asegúrese de actualizar las referencias de enlace, según corresponda, en Forms adaptable<!--and interactive communications--> que utilizan el modelo de datos de formulario actualizado.

## Pasos siguientes {#next-steps}

Ahora tiene un modelo de datos de formulario con orígenes de datos agregados. A continuación, puede editar el Modelo de datos de formulario para agregar y configurar objetos y servicios del modelo de datos, agregar asociaciones entre objetos del modelo de datos, editar propiedades, agregar objetos y propiedades del modelo de datos personalizado, generar datos de ejemplo, etc.

Para obtener más información, consulte [Trabajo con el modelo de datos de formulario](work-with-form-data-model.md).
