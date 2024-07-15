---
title: Creación de contenido orientado mediante el modo de Orientación
description: El modo segmentación y el componente de Target proporcionan herramientas para crear contenido para experiencias
exl-id: 8d80d867-2d0f-4ddb-8a06-f9441e6d85ce
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '5282'
ht-degree: 87%

---

# Creación de contenido orientado mediante el modo de Orientación {#authoring-targeted-content-using-targeting-mode}

Contenido orientado por el autor mediante el modo de segmentación de AEM. El modo segmentación y el componente de Target proporcionan herramientas para crear contenido para experiencias:

* Reconozca fácilmente el contenido de destino que se encuentra en la página. Una línea de puntos forma un borde alrededor de todo el contenido de destino.
* Seleccione una marca y una actividad para ver las experiencias.
* Añada o elimine experiencias de una actividad.
* Realice pruebas A/B y convierta a los ganadores (solo Adobe Target).
* Añada ofertas a una experiencia creando ofertas o utilizando ofertas de una biblioteca.
* Configure objetivos y supervise el rendimiento.
* Simule la experiencia del usuario.
* Para obtener más personalización, configure el componente de Target.

>[!NOTE]
>
>El modo de segmentación está disponible tanto en el Editor de páginas como en el Editor de fragmentos de experiencias.
>
>La siguiente documentación es aplicable a ambos (ya que ambos funcionan de la misma manera) aunque está escrita para el Editor de páginas.

>[!CAUTION]
>
>Al segmentar objetivos en el Editor de páginas, solo se pueden segmentar los componentes de Fragmento de experiencia.
>
>Otros tipos de componentes se pueden convertir en un Fragmento de experiencia utilizando el icono de **Convertir en variación de fragmento de experiencia** en la barra de herramientas de componentes.

<!--
>Other component types can be converted to an Experience Fragment using the **Convert to experience fragment variation** icon on the component toolbar:
>
>![Converting component to Experience Fragment](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)
-->

Puede utilizar AEM o Adobe Target como motor de orientación (para utilizar Adobe Target, debe tener una cuenta de Adobe Target válida). Si utiliza Adobe Target, primero debe configurar la integración. Consulte las [instrucciones para la integración con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

![Contenido de direccionamiento](../assets/targeted-content.png)

Las actividades y experiencias que ve en el modo de Target reflejan la [consola Actividades](/help/sites-cloud/authoring/personalization/activities.md):

* Los cambios que realice en las actividades y experiencias mediante el modo de segmentación se reflejan en la consola Actividades.
* Los cambios realizados en la consola Actividades se reflejan en el modo de segmentación.

>[!NOTE]
>
>Al crear una campaña en Adobe Target, se asigna una propiedad denominada `thirdPartyId` a cada campaña. Al eliminar la campaña en Adobe Target, thirdPartyId no se elimina. No puede volver a utilizar `thirdPartyId` para las campañas de distintos tipos (AB, XT) y no se puede quitar manualmente. Para evitar este problema, asigne a cada campaña un nombre único; los nombres de campaña no se pueden reutilizar en tipos de campaña diferentes.
>
>Si utiliza el mismo nombre en el mismo tipo de campaña, sobrescribirá la campaña existente.
>
>Si al sincronizar se muestra el mensaje de error “Se ha producido un error en la solicitud. `thirdPartyId` ya existe”, cambie el nombre de la campaña y vuelva a sincronizar.

>[!NOTE]
>
>Cuando se selecciona el destino, la combinación de personalización de marca y actividad se mantiene en el nivel de usuario, no de canal.

## Cambio al modo de segmentación {#switching-to-targeting-mode}

Cambie al modo de segmentación para acceder a las herramientas para crear contenido de destino.

Para cambiar al modo de segmentación, haga lo siguiente:

1. Abra la página para la que desea crear contenido de destino.
1. En la barra de herramientas situada en la parte superior de la página, seleccione el menú desplegable de modo para mostrar los tipos de modo disponibles.

   ![Modo Targeting](../assets/targeted-mode.png)

1. Seleccione **Segmentación**. Las opciones de orientación se muestran en la parte superior de la página.

   ![Barra de herramientas de direccionamiento](../assets/targeted-toolbar.png)

## Adición de una actividad mediante el modo de segmentación {#adding-an-activity-using-targeting-mode}

Utilice el modo de Orientación para añadir una actividad a una marca. Al añadir una actividad, contiene la experiencia predeterminada. Después de añadir la actividad, se inicia el proceso de segmentación de contenido para la actividad.

También puede crear y administrar actividades de Adobe Target desde AEM con la opción de seleccionar el motor de destino, con AEM o Adobe Target y seleccionando el tipo actividad: segmentación de experiencias o prueba A/B.

Además, puede administrar objetivos y métricas para todas las actividades de Adobe Target y administrar los públicos de Adobe Target. También se incluye la creación de informes de actividad de Adobe Target, incluida la conversión de ganadores para pruebas A/B.

Cuando se añade una actividad, también aparece en la [consola Actividades](/help/sites-cloud/authoring/personalization/activities.md).

Para añadir una actividad, haga lo siguiente:

1. Utilice el menú desplegable **Marca** para seleccionar la marca para la que desea crear la actividad.

   >[!NOTE]
   >
   >Se recomienda [crear marcas a través de la consola actividades](/help/sites-cloud/authoring/personalization/activities.md#creating-a-brand-using-the-activities-console).
   >
   >
   >Si crea una marca de cualquier otra manera, asegúrese de que el nodo `/campaigns/<brand>/master` existe o se producirá un error al intentar crear una actividad.

1. Seleccione + junto al menú desplegable **Actividad**.
1. Escriba un nombre para la actividad.

   >[!NOTE]
   >
   >Cuando crea una actividad y tiene una configuración de nube de Adobe Target AEM asociada a la página o a uno de sus elementos principales, supone automáticamente que Adobe Target es el motor de la actividad de, que se utiliza para crear una actividad de.

1. En el menú desplegable del motor de **Orientación**, seleccione el motor de orientación.

   * Si selecciona **ContextHub AEM**, los campos restantes se atenúan y no están disponibles. Seleccione **Crear**.

   * Si selecciona **Adobe Target**, puede seleccionar una configuración (de forma predeterminada, es la configuración que proporcionó al configurar la cuenta) y el tipo de actividad. <!--If you select **Adobe Target**, you can select a configuration (by default, it is the configuration you provided when you [configured the account](/help/sites-administering/opt-in.md)) and Activity Type.-->

1. En el menú Actividad, seleccione **Segmentación de experiencias** o **Pruebas A/B**.

   * Segmentación de experiencias: administre las actividades de Adobe Target desde AEM.
   * Pruebas A/B: cree/administre actividades de pruebas A/B en Adobe Target desde AEM.

## El proceso de segmentación: crear, segmentar y objetivos y configuración {#the-targeting-process-create-target-and-goals-settings}

El modo de Orientación le permite configurar diversas proporciones de una actividad. Utilice el siguiente proceso de tres pasos para crear contenido de destino para una actividad de marca:

1. [Crear](#create-authoring-the-experiences): añada o quite experiencias y añada ofertas para cada experiencia.
1. [Orientar](#target-configuring-the-audiences): especifique el público al que se orienta cada experiencia. Puede dirigirse a un público específico y, si utiliza las pruebas A/B, decidir qué porcentaje del tráfico se destina a cada experiencia.
1. [Objetivos y configuraciones](#goals-settings-configuring-the-activity-and-setting-goals): programe la actividad y establezca la prioridad. También puede establecer objetivos de métricas de éxito.

Utilice el siguiente procedimiento para iniciar el proceso de segmentación de contenido de una actividad.

>[!NOTE]
>
>Para utilizar el proceso de direccionamiento, debe ser miembro del grupo de usuarios Autores de actividades de Target.

Para añadir una actividad, haga lo siguiente:

1. En el menú desplegable **Marca**, seleccione la marca que contiene la actividad en la que está trabajando.
1. En el menú desplegable **Actividad**, seleccione la actividad para la que está creando contenido de destino.
1. Para mostrar los controles que lo guían a través del proceso de segmentación, seleccione **Iniciar segmentación**.

   ![Iniciar direccionamiento](../assets/targeted-start-targeting.png)

   >[!NOTE]
   >
   >Para cambiar la actividad con la que está trabajando, seleccione **Atrás**.

## Crear: creación de las experiencias {#create-authoring-the-experiences}

El paso Crear de la orientación del contenido implica la creación de experiencias. Durante este paso puede crear o eliminar las experiencias de la actividad y añadir ofertas a cada experiencia.

### Visualización de ofertas de experiencias en el modo de segmentación {#seeing-experience-offers-in-targeting-mode}

Después de [iniciar el proceso de orientación](#the-targeting-process-create-target-and-goals-settings), seleccione una experiencia para ver las ofertas que se proporcionan para esa experiencia. Al seleccionar una experiencia, los componentes de destino de la página cambian para mostrar la oferta de dicha experiencia.

>[!CAUTION]
>
>Tenga cuidado al deshabilitar la segmentación de un componente que ya está segmentado en la instancia de autor. La actividad correspondiente también se eliminará automáticamente de la instancia de publicación.

>[!NOTE]
>
>Una oferta es el contenido de un componente de destino.

Las experiencias se muestran en el panel Audiencies. En el siguiente ejemplo, las experiencias incluyen **Predeterminado**, **Mujer**, **Mujer mayor de 30 años** y **Mujer menor de 30 años**. Este ejemplo muestra la oferta predeterminada de un componente de **imagen** segmentado.

![Componente de imagen de destino](../assets/targeted-image-component.png)

Al seleccionar una experiencia distinta, el componente Imagen muestra la oferta para esa experiencia.

![Se ha cambiado el componente de imagen de destino](../assets/targeted-image-different.png)

Cuando se selecciona una experiencia y el componente segmentado no incluye una oferta para esa experiencia, el componente muestra la opción **Agregar oferta** superpuesta a la oferta predeterminada semitransparente. Cuando no se ha creado ninguna oferta para una experiencia, se muestra la oferta **predeterminada** para el segmento asignado a la experiencia.

![Agregar oferta](../assets/targeted-add-offer.png)

La experiencia predeterminada también se muestra cuando las propiedades del visitante no coinciden con ningún segmento asignado a las experiencias. Consulte [Adición de experiencias con el modo de direccionamiento](#adding-and-removing-experiences-using-targeting-mode).

### Ofertas personalizadas y ofertas de la biblioteca {#custom-offers-and-library-offers}

Las ofertas que [se crean en la página](#adding-a-custom-offer) y se utilizan para una experiencia única se denominan ofertas personalizadas. La siguiente imagen se superpone al contenido de una oferta personalizada:

![Icono de oferta personalizada](../assets/targeted-custom-offer-icon.png)

Las ofertas que [se añaden desde una biblioteca de ofertas](#adding-an-offer-from-an-offer-library) se superponen a la imagen siguiente:

![Icono de oferta de la biblioteca](../assets/targeted-library-offer-icon.png)

Puede guardar ofertas personalizadas en una biblioteca de ofertas si decide que quiere volver a utilizarlas. También puede convertir una oferta de la biblioteca en una oferta personalizada si desea modificar el contenido de una experiencia. Después de editar, puede volver a guardar la oferta en la biblioteca.

### Adición y eliminación de experiencias mediante el modo de segmentación {#adding-and-removing-experiences-using-targeting-mode}

Con el paso Crear del [proceso de orientación](#the-targeting-process-create-target-and-goals-settings), puede añadir y quitar experiencias. Además, puede duplicar una experiencia y también cambiarle el nombre.

#### Adición de experiencias con el modo de segmentación {#adding-experiences-using-targeting-mode}

Para añadir una experiencia, haga lo siguiente:

1. Para agregar una experiencia, seleccione **+** **Agregar segmentación de experiencias** que aparece debajo de las experiencias existentes en el panel **Audiencias**.
1. Seleccione un público. De forma predeterminada, ese nombre es el nombre de la experiencia. Puede escribir otro nombre, si lo desea. Seleccione **Aceptar**.

#### Eliminación de experiencias mediante el modo de segmentación {#removing-experiences-using-targeting-mode}

Para eliminar una experiencia, haga lo siguiente:

1. Seleccione la flecha situada junto al nombre de la experiencia.

   ![Eliminación y experiencia](../assets/targeted-delete-experiene.png)

1. Haga clic en **Eliminar**.

#### Cambiar el nombre de las experiencias mediante el modo de Orientación {#renaming-experiences-using-targeting-mode}

Para cambiar el nombre de las experiencias mediante el modo de Orientación, haga lo siguiente:

1. Seleccione la flecha situada junto al nombre de la experiencia.
1. Haga clic en **Cambiar nombre de experiencia** y escriba el nombre nuevo.
1. Seleccione en otro lugar de la pantalla para guardar los cambios.

#### Edición de audiencias mediante el modo de segmentación {#editing-audiences-using-targeting-mode}

Para editar el público mediante el modo de segmentación:

1. Seleccione la flecha situada junto al nombre de la experiencia.
1. Haga clic en **Editar audiencia** y seleccione una audiencia nueva.
1. Haga clic en **Aceptar**.

#### Duplicado de experiencias mediante el modo de segmentación {#duplicating-experiences-using-targeting-mode}

Para copiar experiencias mediante el modo de segmentación, haga lo siguiente:

1. Seleccione la flecha situada junto al nombre de la experiencia.
1. Haga clic en **Duplicar** y elija el público.
1. Cambie el nombre de la experiencia si lo desea y haga clic en **OK**.

### Creación de ofertas mediante el modo de segmentación {#creating-offers-using-targeting-mode}

Oriente un componente para crear ofertas para las experiencias. Los componentes segmentados proporcionan el contenido que se utiliza como ofertas para las experiencias.

* [Oriente un componente existente](#creating-a-default-offer-by-targeting-an-existing-component). El contenido se convierte en la oferta de la experiencia predeterminada.
* [Agregue un componente Target](#creating-an-offer-by-adding-a-target-component) y, a continuación, agregue contenido al componente.

Una vez identificado un componente, puede agregar ofertas para cada experiencia:

* [Agregar ofertas personalizadas](#adding-a-custom-offer).
* [Agregar ofertas desde una biblioteca](#adding-an-offer-from-an-offer-library).

Las siguientes herramientas están disponibles para trabajar con ofertas:

* [Añadir una oferta personalizada a una biblioteca de ofertas](#adding-a-custom-offer-to-a-library).
* [Convertir la oferta de la biblioteca en una oferta personalizada](#converting-a-library-offer-to-a-custom-library).
* [Abrir una oferta de la biblioteca y editar el contenido](#editing-a-library-offer).

#### Creación de una oferta predeterminada mediante la segmentación de un componente existente {#creating-a-default-offer-by-targeting-an-existing-component}

Oriente un componente de la página para utilizarlo como la oferta para la experiencia predeterminada de la actividad. Al segmentar un componente, se envuelve en un componente de Target y su contenido se convierte en la oferta para la experiencia predeterminada.

Al orientar un componente, solo ese componente se puede utilizar en la oferta. No se puede eliminar el componente de la oferta ni agregar otros componentes a la oferta.

Realice el siguiente procedimiento después de [iniciar el proceso de segmentación](#the-targeting-process-create-target-and-goals-settings).

1. Seleccione el componente al que desee destinarlo. Aparecerá la barra de herramientas del componente, de forma similar al siguiente ejemplo.

   ![Componente dirigido](../assets/targeted-component.png)

1. Seleccione el icono Target.

   ![Botón Target](../assets/targeted-target-button.png)

   El contenido del componente es la oferta para la experiencia predeterminada. Al orientar un componente, el nodo predeterminado se replicará para cada experiencia. Esto es necesario para editar el nodo de contenido adecuado durante la creación específica de la experiencia. Para estas experiencias no predeterminadas, [agregue una oferta personalizada](#adding-a-custom-offer) o [agregue una oferta de la biblioteca](#adding-an-offer-from-an-offer-library).

#### Creación de una oferta mediante la adición de un componente Target {#creating-an-offer-by-adding-a-target-component}

Añada un componente Target para crear la oferta para la experiencia predeterminada. El componente Target es un contenedor para otros componentes, y los componentes que se encuentran en él se orientan. Al utilizar el componente Target, puede añadir varios componentes para crear una oferta. Asimismo, puede utilizar distintos componentes en cada experiencia para crear diferentes ofertas.

Consulte [Configurar las opciones del componente Target](#configuring-target-component-options) para obtener información sobre cómo personalizar este componente.

>[!NOTE]
>
>Las ofertas que crea mediante la [consola Ofertas](/help/sites-cloud/authoring/personalization/offers.md) también pueden contener varios componentes. Estas ofertas pertenecen a una biblioteca de ofertas y pueden utilizarse para varias experiencias.

Como el componente de Target es un contenedor, aparece como un área de colocación para otros componentes.

En el modo de segmentación, el componente segmentado tiene un borde azul y el mensaje de destino indica la naturaleza de la segmentación.

![Zona de colocación de destino](../assets/targeted-drop-target.png)

En el modo de Edición, el componente Target tiene un icono de diana.

![Icono de zona de colocación de destino](../assets/targeted-drop-target-icon.png)

Los componentes que arrastra al componente Target son componentes orientados.

![Zona de colocación de destinos](../assets/targeted-drop-zone-populated.png)

Al añadir un componente al componente Target, proporciona contenido para una experiencia determinada. Para especificar la experiencia, debe seleccionar la experiencia antes de agregar los componentes.

Puede añadir un componente Target a la página en modo de Edición o en modo de Target. Puede añadir componentes al componente Target solo en modo de Target. El componente de Target pertenece al grupo de componentes Personalización.

Si edita contenido de destino, debe seleccionar **Iniciar segmentación** para poder hacerlo.

1. Arrastre el componente de Target a la página donde desea que aparezca la oferta.
1. De forma predeterminada, no se establece ningún identificador de ubicación. Seleccione la rueda dentada de configuración para definir la posición.

   >[!NOTE]
   >
   >Si la establece el administrador, es posible que deba definir la ubicación de forma explícita.
   >
   >Los administradores pueden decidir si esta configuración es necesaria en `https://<host>:<port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet`
   >
   >Para requerir que los usuarios introduzcan una ubicación, active la casilla de verificación **Forzar ubicación**.

1. Seleccione la experiencia para la que desea crear la oferta.
1. Cree la oferta:

   * Para la experiencia predeterminada, arrastre los componentes al área de colocación orientada y edite las propiedades de los componentes como de costumbre para crear el contenido de la oferta.
   * Para estas experiencias no predeterminadas, [agregue una oferta personalizada](#adding-a-custom-offer) o [una oferta de la biblioteca](#adding-an-offer-from-an-offer-library).

#### Agregar una oferta personalizada {#adding-a-custom-offer}

Para crear una oferta, cree el contenido de un componente orientado en modo de Orientación. Al crear una oferta personalizada, se utiliza como oferta para una experiencia única.

Si decide que la oferta se puede utilizar para otras experiencias, puede crear una oferta personalizada y [agregarla a la biblioteca](#adding-a-custom-offer-to-a-library). Para obtener información sobre el uso de la consola Ofertas para crear una oferta reutilizable, consulte [Agregar una oferta a una biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library).

1. Seleccione la experiencia a la que desea añadir la oferta.
1. Para mostrar el menú de componentes, seleccione el componente de destino al que desea añadir la oferta.

   ![Adición de una oferta](../assets/targeted-component-menu.png)

1. Seleccione el icono +.

   El contenido de la oferta predeterminada se utiliza como oferta para la experiencia actual.

1. Seleccione la oferta para mostrar el menú de oferta y, a continuación, seleccione el icono de edición.

   ![Barra de herramientas de componentes de Target](../assets/targeted-offer-menu.png)

1. Edite el componente de la oferta.

#### Agregar una oferta desde una biblioteca de ofertas {#adding-an-offer-from-an-offer-library}

Agregue una oferta de la [biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md) a una experiencia. Puede agregar cualquier oferta de la biblioteca de la marca que está actualmente orientando.

No puede añadir ofertas de la biblioteca a la experiencia predeterminada.

1. Seleccione la experiencia a la que desea añadir la oferta.
1. Para mostrar el menú de componentes, seleccione el componente de destino al que desea añadir la oferta.

   ![Oferta segmentada](../assets/targeted-add-offer-large.png)

1. Seleccione el icono de la carpeta.

   ![Icono de carpeta](../assets/targeted-folder-button.png)

1. Seleccione la oferta de la biblioteca y, a continuación, seleccione el icono de la marca de verificación.

   ![Biblioteca de ofertas](../assets/targeted-select-content.png)

   El selector de ofertas le permite examinar o filtrar las ofertas. Al examinar o filtrar, puede que también desee clasificar las ofertas y cambiar la manera de verlas. El número que aparece en la parte superior derecha indica cuántas ofertas hay disponibles en la biblioteca actual.

   * Seleccione **Examinar** para navegar a otra carpeta. Se abrirá el panel de navegación; haga clic en la flecha para navegar por las carpetas. Vuelva a seleccionar **Examinar** para cerrar el panel de navegación.

   ![Examinar contenido](../assets/targeted-select-content-browse.png)

   * Seleccione **Filter** para filtrar las ofertas por palabras clave o etiquetas. Introduzca palabras clave y seleccione etiquetas en el menú desplegable. Vuelva a seleccionar **Filtro** para cerrar el panel de filtrado.

   ![Filtrar contenido](../assets/targeted-filter.png)

   * Para cambiar la manera de ordenar las ofertas, toque o haga clic en la flecha al lado de **La más reciente a la más antigua**. Las ofertas se pueden ordenar de la más reciente a la más antigua o de la más antigua a la más reciente.

   ![Filtrar orden](../assets/targeted-filter-sort.png)

   Seleccione el icono junto a **Ver como** para ver las ofertas como mosaicos o como una lista.

   ![Ver como botón](../assets/targeted-view-as-button.png)

#### Añadir una oferta personalizada a una biblioteca {#adding-a-custom-offer-to-a-library}

Añada una oferta personalizada a la [biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md) cuando desee volver a utilizarla como la oferta para experiencias múltiples. Puede añadir ofertas a la biblioteca de la marca actual a la cual se está direccionando.

Para obtener información sobre el uso de la consola Ofertas para crear una oferta reutilizable, consulte [Agregar una oferta a una biblioteca de ofertas](/help/sites-cloud/authoring/personalization/offers.md#add-an-offer-to-an-offer-library).

1. Seleccione la experiencia para mostrar la oferta personalizada.
1. Seleccione la oferta personalizada para mostrar el menú de ofertas y, a continuación, seleccione el icono **Guardar oferta en la biblioteca de ofertas**.

   ![Guardar oferta en la biblioteca de ofertas](../assets/targeted-save-offer-library-button.png)

1. Escriba un nombre para la oferta, seleccione la biblioteca a la que desea añadir la oferta y, a continuación, seleccione el icono de la marca de verificación.

#### Conversión de una oferta de la biblioteca en una personalizada {#converting-a-library-offer-to-a-custom-library}

Convierta una oferta de la biblioteca en una personalizada para cambiar la oferta por la experiencia actual y sin cambiar la oferta en otras experiencias.

1. Seleccione la experiencia para mostrar la oferta de la biblioteca.
1. Seleccione la oferta de la biblioteca para mostrar el menú de oferta y, a continuación, seleccione el icono Convertir en oferta en línea.

   ![Convertir en oferta en línea](../assets/targeted-convert-inline.png)

#### Editar una oferta de la biblioteca {#editing-a-library-offer}

Abra una oferta de la biblioteca de una experiencia en modo de Orientación para editar la oferta. Los cambios que realice aparecerán en todas las experiencias que utilicen la oferta.

1. Seleccione la experiencia para mostrar la oferta de la biblioteca.
1. Convierta la oferta de la biblioteca en una oferta local o personalizada. Consulte [Conversión de una oferta de la biblioteca en una biblioteca personalizada](#converting-a-library-offer-to-a-custom-library).
1. Edite el contenido de la oferta.

1. Vuelva a guardarlo en la biblioteca. Consulte [Adición de una oferta personalizada a una biblioteca](#adding-a-custom-offer-to-a-library).

## Target: configuración de públicos {#target-configuring-the-audiences}

El paso Target del [proceso de orientación](#the-targeting-process-create-target-and-goals-settings) implica la asignación de públicos a las experiencias con que ha trabajado en el paso Crear. En la página Target se muestran los públicos a que se orienta cada experiencia. Puede especificar o cambiar el público para cada experiencia. Si utiliza Adobe Target, también puede crear pruebas A/B que le permitan dirigir un porcentaje del tráfico de un público a una experiencia concreta.

### Si usa el direccionamiento de AEM o Adobe Target (segmentación de experiencias)… {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

Los públicos aparecen en el lado izquierdo del diagrama de asignación, y las experiencias en el lado derecho.

![Asignación de audiencias](../assets/targeted-diagram.png)

Defina un público con un segmento. La configuración de nube de la página determina los segmentos que están disponibles. Cuando la página no está asociada a una configuración de nube de Adobe Target, los segmentos de AEM están disponibles para definir públicos. Cuando la página está asociada a una configuración de nube de Adobe Target, se utilizan segmentos de Target.

Para obtener información sobre los motores de segmentación, consulte el [Motor de segmentación](/help/sites-cloud/authoring/personalization/overview.md#targeting-engine).

Una experiencia no debe utilizar más de un público. Aparece un símbolo de advertencia junto a una experiencia cuando se asigna a un público asignado a otra experiencia.

![Icono de advertencia](../assets/targeted-warn.png)

### Asociación de experiencias con públicos (AEM o Adobe Target) {#associating-experiences-with-audiences-aem-or-adobe-target}

Utilice el siguiente procedimiento para asociar una experiencia con un público al usar la segmentación de experiencias de AEM (u segmentación de experiencias de Adobe Target):

1. Seleccione la flecha desplegable situada junto en el cuadro de audiencia que está asignado a la experiencia.
1. (Opcional) Seleccione **Editar** y luego escriba una palabra clave para buscar el segmento deseado.
1. En la lista de audiencias, seleccione la audiencia y seleccione **Aceptar**.

### Si utiliza la prueba A/B (Adobe Target)… {#if-you-are-using-a-b-testing-adobe-target}

Si tiene una actividad de pruebas A/B, los públicos están a la izquierda, el porcentaje de visualización de cada experiencia se encuentra en el medio y las experiencias a la derecha.

Puede cambiar los porcentajes, siempre que sumen el cien por ciento. Varias experiencias pueden utilizar un público en las pruebas A/B.

![Direccionamiento A/B](../assets/targeted-ab.png)

### Asociación de públicos y porcentajes de tráfico con pruebas A/B {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. Seleccione el cuadro desplegable situado junto a la audiencia asignada a la experiencia.
1. De manera opcional, haga clic en **Editar** y, a continuación, escriba una palabra clave para buscar el segmento que desee.
1. Seleccionar **Aceptar.**
1. Introduzca porcentajes para configurar la forma en que el tráfico del público se dirige a cada experiencia. El número total debe ser igual a 100.
1. (Opcional) Edite el nombre de la experiencia haciendo clic en el menú desplegable situado junto al nombre de la experiencia.

## Objetivos y configuración: configuración de la actividad y configuración de los objetivos {#goals-settings-configuring-the-activity-and-setting-goals}

El paso Objetivos y configuración del [proceso de direccionamiento](#the-targeting-process-create-target-and-goals-settings) consiste en configurar el comportamiento de la actividad de la marca. Especifique cuándo comienza y finaliza la actividad, así como la prioridad. Además, realiza un seguimiento de los objetivos. Específicamente, puede decidir lo que desea medir con sus actividades.

Las métricas de objetivo solo están disponibles si usa Adobe Target como motor de orientación. Debe definir al menos una métrica de objetivo. Si tiene Adobe Analytics configurado y una configuración de nube de A4T Analytics, puede seleccionar si desea que la fuente de informes sea Adobe Target o Adobe Analytics.

Las métricas de la meta solo se miden para la campaña publicada.

Si utiliza Adobe Target como motor de segmentación, haga lo siguiente:

![AEM como motor de destino](../assets/targeted-goals.png)

Si utiliza Adobe Target como motor de orientación:

![Adobe Target como motor de destino](../assets/targeted-engine.png)

Si utiliza Adobe Target como motor de determinación de objetivos y tiene A4T Analytics configurado en la cuenta, tiene un menú desplegable de **Fuente de informes** adicional:

![A4T](../assets/targeted-source.png)

Las métricas de éxito siguientes están disponibles (se utilizan para publicar únicamente):

| Métrica | Descripción | Opciones |
|---|---|---|
| Conversión | El porcentaje de visitantes que hicieron clic en cualquier parte de la experiencia que se está probando. Las conversiones se pueden contabilizar una vez por visitante o cada vez que un visitante completa una conversión. La métrica de conversión se configura en una de las siguientes | Visualizó una página: puede definir qué página ha visto la audiencia seleccionando la dirección URL y, a continuación, definiendo la dirección URL o varias direcciones URL, o bien seleccionando la dirección URL que contiene y añadiendo una ruta o palabra clave. Ha visto un mbox: puede definir el mbox que la audiencia ha visto introduciendo el nombre del mbox. Puede hacer clic en Añadir un Mbox para introducir varios mbox. |
| Ingresos | Ingresos generados por la visita. Puede elegir entre las métricas de ingresos enumeradas. Para cualquiera de estas opciones, si se ha visto un mbox indica que se ha alcanzado el objetivo. Puede definir uno o varios mbox. | Ingresos por visitante (RPV), Valor de pedido promedio (AOV), Ventas totales, Pedidos |
| Compromiso | Puede medir tres tipos de participación | Vistas de página, Puntuación personalizada, Tiempo en el sitio |

Además, hay configuraciones avanzadas que le permiten determinar cómo contar las métricas de éxito. Las opciones incluyen contar la métrica por impresión o una vez por visitante y elegir si desea mantener al usuario en la actividad o eliminarlo.

Use la configuración avanzada para determinar qué sucede **después** de que un usuario llegue a la métrica de objetivo. En la tabla siguiente se muestran las opciones disponibles.

| Cuando un usuario encuentra esta métrica de objetivo... | Selecciona lo siguiente para que suceda... |
|---|---|
| Aumentar recuento y mantener el usuario en la actividad | Especifique cómo se incrementa el recuento: Una vez por participante, en cada impresión, excluyendo las actualizaciones de página, En cada impresión |
| Aumentar recuento, liberar usuario y permitir la reentrada | Seleccione la experiencia que el visitante ve si vuelve a participar en la actividad: La misma experiencia, experiencia aleatoria, experiencia no vista |
| Recuento de incrementos, liberación de usuario y reentrada de barras | Determine lo que el usuario ve en lugar del contenido de la actividad: La misma experiencia, sin seguimiento, contenido predeterminado u otro contenido de actividad |

Consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es) para obtener más información sobre las métricas de éxito.

### Configuración (segmentación de AEM) {#configuring-settings-aem-targeting}

Para configurar las opciones de configuración, si utiliza la segmentación de AEM, haga lo siguiente:

1. Para especificar cuándo se inicia la actividad, utilice el menú desplegable **Inicio** para seleccionar uno de los siguientes valores:

   * **Cuando se activa**: la actividad se inicia cuando se activa la página que contiene el contenido segmentado.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, seleccione el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.

1. Para especificar cuándo termina la actividad, utilice el menú desplegable **Finalización** para seleccionar uno de los siguientes valores:

   * **Cuando se desactiva**: la actividad finaliza cuando se desactiva la página que contiene el contenido segmentado.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, seleccione el icono de calendario, seleccione una fecha y especifique la hora a la que desea finalizar la actividad.

1. Para especificar una prioridad para la actividad, utilice el regulador para seleccionar **Baja**, **Normal** o **Alta**.

### Configuración de metas y opciones (Adobe Target) {#configuring-goals-settings-adobe-target}

Para establecer las metas y la configuración, si utiliza Adobe Target, haga lo siguiente:

1. Para especificar cuándo se inicia la actividad, utilice el menú desplegable **Inicio** para seleccionar uno de los siguientes valores:

   * **Cuando se activa**: la actividad se inicia cuando se activa la página que contiene el contenido segmentado.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, seleccione el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.

1. Para especificar cuándo termina la actividad, utilice el menú desplegable **Finalización** para seleccionar uno de los siguientes valores:

   * **Cuando se desactiva**: la actividad finaliza cuando se desactiva la página que contiene el contenido segmentado.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, seleccione el icono de calendario, seleccione una fecha y especifique la hora a la que desea finalizar la actividad.

1. Para especificar una prioridad para la actividad, utilice el regulador para seleccionar **Baja**, **Normal** o **Alta**.
1. Si ha configurado Adobe Analytics con su cuenta de Adobe Target, verá el menú desplegable **Fuente de informes**. Seleccione **Adobe Target** o **Adobe Analytics** como fuente.

   Si selecciona **Adobe Analytics**, seleccione la empresa y el grupo de informes. Si selecciona **Adobe Target**, no se requiere ninguna acción.

   ![Fuente de creación de informes](../assets/targeted-reporting-source.png)

1. En el área **Métrica de objetivo**, en **Mi objetivo principal**, seleccione la métrica de éxito que desee rastrear (conversión, ingresos, participación) y especifique cómo se mide esa métrica (o qué acción toma la audiencia para indicar que se ha alcanzado un objetivo). Consulte la definición de las métricas de objetivo en la tabla anterior y consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es) sobre las métricas de éxito.

   Para cambiar el nombre del objetivo, haga clic en los tres puntos de la esquina superior derecha y seleccione **Cambiar nombre**.

   Si necesita borrar todos los campos, haga clic en los tres puntos de la esquina superior derecha y seleccione **Borrar todos los campos**.

   Todas las métricas también tienen configuraciones avanzadas que puede definir. Seleccione **Configuraciones avanzadas** para acceder a las mismas. Consulte la definición de cómo se cuentan las métricas de éxito en la tabla anterior y consulte la [documentación de Adobe Target](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=es).

   >[!NOTE]
   >
   >Debe tener un objetivo definido como mínimo.

   ![Métrica de objetivo](../assets/targeted-goal-metric.png)

   >[!NOTE]
   >
   >Si falta información en la métrica, esta tiene un círculo en rojo.

1. Haga clic en **Añadir una nueva métrica** para configurar las métricas de éxito adicionales.

   ![Métricas adicionales](../assets/targeted-additional-metrics.png)

   >[!NOTE]
   >
   >Para quitar los objetivos adicionales, toque o haga clic en los tres puntos y en **Eliminar**. AEM requiere que haya definido al menos una meta.

1. Si desea tener más control sobre cómo se cuentan las métricas de éxito, seleccione **Configuración avanzada** para acceder a las mismas.
1. Haga clic en **Guardar**.

Una vez configuradas, puede [ver el rendimiento de las actividades](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test) que usan Adobe Target (orientación de la experiencia o de la prueba A/B). Además, con el direccionamiento de pruebas A/B, puede [convertir los ganadores](/help/sites-cloud/authoring/personalization/activities.md#viewing-performance-and-converting-winning-experiences-a-b-test).

## Simulación de una experiencia {#simulating-an-experience}

Simule la experiencia de un visitante para comprobar que el contenido de la página se muestra como se espera según el diseño del contenido orientado. Al simular, cargue diferentes perfiles de usuario y vea el contenido de destino de ese usuario.

Los siguientes criterios determinan el contenido que aparece al simular la experiencia de un visitante:

* Los datos en el almacén de sesiones del usuario (a través de ContextHub).
* Las [Actividades que están activadas](/help/sites-cloud/authoring/personalization/activities.md).
* Las [reglas que definen los segmentos](/help/sites-cloud/authoring/personalization/segmentation.md).
* El contenido de las experiencias en los componentes de Target.
* La [configuración del motor de segmentación](/help/sites-cloud/authoring/personalization/activities.md).

Si aparece contenido inesperado en la página al cargar un perfil, compruebe la configuración de cada elemento de esta lista.

>[!NOTE]
>
>Si utiliza la prueba A/B, al simular, las experiencias se muestran según el porcentaje de tráfico. Esto se controla mediante Adobe Target, lo que puede dar lugar a resultados inesperados para los autores. (La actividad del autor se sincroniza con las configuraciones específicas que permiten volver a evaluar durante la simulación). Es posible que los autores tengan que actualizar para ver las otras experiencias en función de su configuración de tráfico.

 Para simular la experiencia del visitante, utilice las siguientes herramientas:

* La actividad Simulación en modo de Orientación: en la página se muestran las ofertas para el usuario seleccionado actualmente en ContextHub. Puede editar las ofertas dirigidas al usuario.
* Modo de vista previa: utilice ContextHub para seleccionar a los usuarios y las ubicaciones que cumplen los criterios de los segmentos en que están basadas las experiencias. Cuando cambian las selecciones de Context Hub, el contenido de destino cambia en consecuencia.

1. Para cambiar al modo de vista previa, en la barra de herramientas, seleccione **Vista previa**.
1. En la barra de herramientas, seleccione el icono de Context Hub.

   ![Botón ContextHub](../assets/targeted-contexthub-button.png)

1. Utilice ContextHub para cambiar las propiedades del contexto. Por ejemplo, seleccione la propiedad Persona para seleccionar un usuario diferente.

   ![Barra de herramientas de ContextHub](../assets/targeted-contexthub-toolbar.png)

   La página cambia para mostrar el contenido dirigido al contexto actual.

1. Para cambiar las ofertas que se muestran, cambie al modo de Orientación. Con la actividad de simulación seleccionada, edite las ofertas para el contexto configurado en el modo de vista previa.

## Configuración de opciones del componente de Target {#configuring-target-component-options}

Puede personalizar el componente de Target accediendo a las opciones del componente de una de las dos maneras siguientes:

1. Una vez que haya orientado el componente, en el componente Target, seleccione el componente y, a continuación, el icono de configuración (engranaje).

   ![Configuración de componentes](../assets/targeted-component-settings.png)

   AEM muestra la ventana de opciones del componente Target.

   ![Cuadro de diálogo Target](../assets/targeted-dialog.png)

1. Como alternativa, para acceder a estas configuraciones en modo de pantalla completa, en la ventana de opciones del componente Target, seleccione el icono de pantalla completa.

   ![Botón Pantalla completa](../assets/targeted-fullscreen.png)

   AEM muestra la ventana de opciones del componente Target a pantalla completa.

   ![Componente en pantalla completa](../assets/targeted-target-as-enging.png)

1. Configure el componente Target tal y como se describe en las tablas siguientes.

| Opción | Descripción |
|---|---|
| Lugar de residencia | La ubicación es una cadena que da un nombre a la ubicación del contenido de destino y conecta ofertas con lugares (o ubicaciones o componentes) en la página donde se deben colocar esas ofertas. Este campo es un valor genérico. Si introduce una oferta en un componente, la oferta recuerda el identificador de la ubicación. Al ejecutar la página, el motor evalúa los segmentos del usuario y, de acuerdo con ello, soluciona las experiencias de las campañas activas que deben mostrarse. A continuación, comprueba los ID de ubicación de la página e intenta hacer coincidir las ofertas con esos ID de ubicación con ellos. |
| Motor | Seleccione entre reglas del lado del cliente (sin seguimiento), Adobe Target, ContextHub y Adobe Campaign según el motor que desee utilizar. |

Si selecciona Adobe Target como motor:

![Objetivo como motor](../assets/targeted-target-as-enging.png)

| Opción | Descripción |
|---|---|
| Direccionamiento preciso | Al habilitar el direccionamiento preciso, se indica al componente que espere a que los datos de Client Context o Context Hub estén disponibles antes de enviar la solicitud a Adobe Target. Puede aumentar el tiempo de carga. Para la creación, la orientación precisa siempre está activada. Si selecciona la casilla Direccionamiento preciso, el mbox realiza primero un mboxDefine y después un mboxUpdate, lo que da como resultado una solicitud de Ajax una vez que los datos están disponibles. Si no selecciona la casilla Direccionamiento preciso, el mbox realiza un mboxCreate, con lo que se obtiene una solicitud sincrónica inmediatamente (en este caso, no todos los datos de contexto pueden estar disponibles aún). Nota: Activar o desactivar el direccionamiento preciso en un componente concreto no afecta a la configuración que haya establecido globalmente. Siempre puede seleccionar Orientación precisa en el componente para anular la configuración global. |
| Incluir segmentos resueltos | Al seleccionar esta casilla de verificación, se incluyen todos los segmentos resueltos en la llamada de mbox y todos los parámetros configurados en la página y en el marco de trabajo. Esto solo funciona en situaciones con XML API en que sincroniza segmentos de AEM. AEM Si tiene segmentos en el segmento que no son gestionados por Adobe Target AEM (como segmentos de script), esta opción le permite resolver el segmento en el que está activo y enviar información a Adobe Target en el que se indica que el segmento está activo. |
| Parámetros heredados de contexto | Enumera los parámetros de contexto heredados del marco de trabajo de Adobe Target, si los hay, asociados a la página seleccionada. |
| Parámetros de contexto | Seleccione Agregar campo para configurar parámetros de contexto adicionales (lo mismo que está disponible en el marco de trabajo de Target). Los parámetros de contexto añadidos al componente solo se aplican al componente y no a otros componentes, como sería el caso si hubiera añadido los parámetros de contexto directamente al marco de trabajo. |
| Parámetros estáticos | Seleccione Agregar campo para configurar parámetros estáticos adicionales (lo mismo que está disponible en el marco de trabajo de Target). Los parámetros estáticos añadidos al componente solo se aplican al componente y no a otros componentes, como sería el caso si hubiera añadido los parámetros estáticos directamente al marco de trabajo. Los parámetros estáticos no proceden del contexto (Client Context o ContextHub). |

>[!NOTE]
>
>Al seleccionar un componente y hacerlo orientable, AEM también reemplaza el componente e introduce un componente de Adobe Target. (El componente de Adobe Target no solo se utiliza cuando se añade manualmente a la página, sino también cuando se marca como objetivo un componente existente).
>
>Seleccione **Adobe Campaign** como motor si integra AEM con Adobe Campaign. Consulte Integración de AEM con Adobe Campaign para obtener más información.
>
>Seleccione **ContextHub** como motor si utiliza ContextHub para orientar. Consulte Configuración de ContextHub para obtener más información.
<!--You select **Adobe Campaign** as the engine if you are integrating AEM with Adobe Campaign. See [Integrating AEM with Adobe Campaign](/help/sites-administering/campaign.md) for more information.-->
<!--Select **ContextHub** as the engine if you are using ContextHub for targeting. See [Configuring ContextHub](/help/sites-administering/contexthub-config.md).-->
