---
title: Creación y administración de ofertas (consola Ofertas)
description: Utilice la consola Ofertas para crear ofertas que se pueden usar en las experiencias de actividad
exl-id: 81d2fda2-06a9-48f6-820a-dd9e11d94fcc
source-git-commit: c27870c39da80d664f208d658994eec83a19589f
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 49%

---

# Creación y administración de ofertas (consola Ofertas) {#creating-and-managing-offers}

La consola **Ofertas** quedará obsoleta en el futuro. Así que, a partir de ahora, es:

* Solo está disponible para los clientes que poseen ofertas *heredadas* ya definidas (es decir, preexistentes)
* Se recomienda convertir estas ofertas heredadas en ofertas de Fragmento de experiencia
   * Tan pronto como se convierta/elimine la última oferta heredada, la consola **Ofertas** ya no estará disponible.

![Consolas de personalización](/help/sites-cloud/authoring/assets/offers-consoles.png)

>[!NOTE]
>
>Los clientes que tengan ofertas preexistentes heredadas aún pueden usar la consola **Ofertas** para ver las ofertas existentes y crear nuevas ofertas heredadas.
>
>Los clientes que no tengan ofertas preexistentes heredadas no verán la consola **Ofertas**.
>
>Todos los clientes pueden utilizar **Ofertas de fragmentos de experiencias** para crear y administrar ofertas.

## Conversión de una oferta heredada en un Fragmento de experiencia {#convert-legacy-offer-to-experience-fragment}

Se han implementado una opción **Convertir en variación de Fragmento de experiencia** y un flujo de trabajo se han implementado para ayudarle a convertir su oferta heredada en un Fragmento de experiencia:

>[!NOTE]
>
>Este es el flujo de trabajo recomendado para convertir ofertas heredadas en Fragmentos de experiencia.

>[!NOTE]
>
>También puede crear un nuevo Fragmento de experiencia, transferir manualmente el contenido de la oferta heredada al fragmento y, a continuación, eliminar la oferta heredada.

>[!CAUTION]
>
>La opción **Convertir en variación de Fragmento de experiencia** está disponible para todos los Componentes principales.
>
>Esta opción no se admitirá en los componentes personalizados. Para estos componentes, debe convertir manualmente el contenido en un Fragmento de experiencia.

>[!CAUTION]
>
>En cuanto se convierte/elimina la última oferta heredada:
>
>* La consola **Ofertas** ya no estará disponible.
>* El icono de destino dentro de la barra de herramientas de cualquier otro componente afectado ya no aparecerá.


1. Abra una página que contenga la oferta para editarla.

1. Cambie al modo de **Segmentación** para esa página.

1. Seleccione **Iniciar segmentación**.

1. Seleccione el componente apropiado (de destino).

1. La barra de herramientas de componentes proporcionará una opción para **Convertir en variación de Fragmento de experiencia**:

   ![Conversión de ofertas heredadas a Fragmentos de experiencia](/help/sites-cloud/authoring/assets/offers-convert-legacy-icon.png)

1. Se mostrará un cuadro de diálogo. Aquí puede seleccionar la **Acción** requerida:

   * Crear un nuevo fragmento de experiencia
   * Añadir el contenido a un Fragmento de experiencia existente

   Para este escenario, seleccione **Crear un nuevo Fragmento de experiencia**.

   ![Convertir en cuadro de diálogo de Variación de Fragmento de experiencia](/help/sites-cloud/authoring/assets/offers-convert-dialog.png)

1. Rellene los campos obligatorios del cuadro de diálogo:

   * **Ruta principal**
Especificar la ruta principal del nuevo Fragmento de experiencia
   * **Plantilla**
Seleccione la plantilla que desea utilizar para crear el Fragmento de experiencia.
   * **Título del fragmento**
Especifique el título.
   * **Etiquetas de fragmento**
Agregue etiquetas, si es necesario.

1. Confirme con **Listo**.

   Si ahora va a la consola **Ofertas de Fragmento de experiencia**, verá su nuevo fragmento de experiencia, junto con sus variaciones asociadas.

### Segmentación con la plantilla de ofertas {#targeting-offers-template}

>[!CAUTION]
>
>Esta opción solo está disponible para clientes con ofertas heredadas preexistentes.
>
>Con la consola de **Ofertas**, ya no estará disponible:
>
>* una vez que la última oferta heredada se haya convertido en Fragmentos de experiencias
>* cuando las ofertas heredadas estén desaprobadas (en el futuro)
>
>Por lo tanto, la opción recomendada es utilizar Fragmentos de experiencia, no esta opción.

Para los clientes con ofertas heredadas preexistentes, las opciones de **Usar plantilla de oferta** estarán visibles al segmentar componentes que **no** son Fragmentos de experiencias:

![Convertir a cuadro de diálogo de variación de Fragmento de experiencia](/help/sites-cloud/authoring/assets/offers-legacy-target-non-experience-fragment.png)

## La consola Ofertas {#offers-console}

>[!CAUTION]
>
>Esta consola se va a desaprobar en el futuro, ya que ofrece una forma heredada de personalizar el contenido.
>
>Todavía tiene tiempo para prepararse. Consulte cómo [convertir las ofertas heredadas existentes en una oferta de Fragmento de experiencia](#convert-legacy-offer-to-experience-fragment).

Utilice la consola Ofertas para crear ofertas que pueda [uso en experiencias de actividad](/help/sites-cloud/authoring/personalization/targeted-content.md). La creación de ofertas en la consola Ofertas ahorra tiempo cuando varias experiencias requieren la misma oferta:

* Cree una oferta una vez en la biblioteca y utilícela en varias experiencias de las actividades de marca.
* Cambie la oferta en la biblioteca y el cambio afectará a todas las experiencias que la utilicen.

La consola Ofertas organiza las ofertas por marca. Cada marca contiene una biblioteca de ofertas que se pueden utilizar en las experiencias de una marca. Utilice carpetas para definir una estructura jerárquica y organizar las ofertas en cada biblioteca. Una estructura de carpetas lógica permite a los autores encontrar fácilmente ofertas mediante la exploración. Las herramientas de etiquetado y búsqueda también permiten a los autores encontrar ofertas.

### Añadir una marca mediante la consola Ofertas {#add-a-brand-using-the-offers-console}

Cree una marca con la que se asocien sus ofertas. Abra una marca en la consola de ofertas para acceder a la biblioteca de ofertas, donde podrá crear carpetas y ofertas.

Cuando crea una marca mediante la consola Ofertas, también aparece en la [Consola Actividades](/help/sites-cloud/authoring/personalization/activities.md) donde puede agregar y administrar actividades para la marca.

1. En la consola de navegación, pulse o haga clic en **Personalización** > **Ofertas**.

   ![Navegación a la consola Ofertas](/help/sites-cloud/authoring/assets/offers-navigation.png)

1. Haga clic o pulse en **Crear** y luego en **Crear** **marca**.
1. Seleccione la plantilla de marca y toque o haga clic en **Siguiente**.
1. Escriba un título para la marca tal como desea que aparezca en las consolas Ofertas y Actividades. De forma opcional, escriba o seleccione una o varias etiquetas para asociarlas a la marca.
1. Haga clic o pulse **Crear**.

### Añadir una carpeta a una biblioteca de ofertas {#add-a-folder-to-an-offer-library}

Añada una carpeta a la biblioteca de ofertas de una marca para organizar y almacenar ofertas. Puede crear una carpeta debajo de la marca o debajo de otras carpetas.

1. En la consola Ofertas, abra la ubicación donde desea crear la carpeta. Por ejemplo, abra la marca para crear una carpeta de nivel superior o abra otra carpeta de la biblioteca.
1. Haga clic o toque **Crear** > **Crear carpeta u oferta**.

   ![Creación de la carpeta de ofertas](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Seleccione **Carpeta** y haga clic en **Siguiente**.
1. Escriba un título para la carpeta tal y como desea que aparezca en la biblioteca de ofertas y escriba o seleccione las etiquetas.

   ![Definición de las propiedades de la carpeta](/help/sites-cloud/authoring/assets/offers-folder-properties.png)

1. Haga clic o pulse **Crear**.

### Añadir una oferta a una biblioteca de ofertas {#add-an-offer-to-an-offer-library}

Añada una oferta a la biblioteca de ofertas de una marca para que se pueda añadir a las experiencias de la marca. Al añadir una oferta, se proporciona un título. También puede asociar la oferta con una o más etiquetas para mejorar la capacidad de búsqueda.

Después de crear la oferta, puede abrirla para crear el contenido.

1. En la consola Ofertas, abra la ubicación donde desea crear la oferta. Por ejemplo, abra la marca para crear una oferta de nivel superior o abra una carpeta en la biblioteca.
1. Haga clic o toque **Crear** > **Crear carpeta u oferta**.

   ![Creación de la carpeta de ofertas](/help/sites-cloud/authoring/assets/offers-create-folder.png)

1. Seleccione el **Página de oferta** y toque o haga clic en **Siguiente**.
1. Escriba un título para la oferta y, opcionalmente, seleccione o escriba una o más etiquetas para asociarlas a la oferta. A continuación, toque o haga clic en **Crear**.
1. En el cuadro de diálogo de confirmación, para abrir la oferta y editarla, haga clic o pulse **Abrir página**.

### Edición de una oferta {#editing-an-offer}

Abra una oferta y edite el contenido tal como desea que aparezca en las experiencias que la utilizan. Cuando edita una oferta que se utiliza en cualquier experiencia, los cambios aparecen en las experiencias.

Puede abrir una oferta desde una carpeta de una biblioteca de ofertas o desde los resultados de búsqueda. También puede abrir una oferta desde una experiencia que utilice la oferta.

1. En la consola de Ofertas, toque o haga clic en el icono situado junto a la oferta y haga clic o pulse en **Editar**.
1. Añada componentes a la oferta y edite el contenido del componente como de costumbre.

### Eliminación de una oferta {#deleting-an-offer}

Elimine una oferta cuando ya no la necesite. Cuando intente eliminar una oferta que se utiliza en una experiencia, se le pedirá que confirme la eliminación. Al confirmar, se elimina la oferta y se elimina de las experiencias.

Puede eliminar una oferta mientras ve el contenido de cualquiera de las carpetas en una biblioteca de ofertas o los resultados de búsqueda.

1. En la consola de Ofertas, toque o haga clic en el icono situado junto a la oferta y haga clic o pulse en **Eliminar**.

   Seleccione la oferta y toque o haga clic en **Eliminar**.

1. En el cuadro de diálogo que aparece, toque o haga clic en **Eliminar** para confirmar la eliminación.
1. Si la oferta se utiliza en una o más experiencias, aparece un cuadro de diálogo para indicar que se hace referencia a la oferta:

   * Para eliminar la oferta y quitarla de las experiencias, toque o haga clic en **Forzar eliminación**.
   * Para conservar la oferta, toque o haga clic en **Cancelar**.

### Búsqueda de ofertas {#searching-for-offers}

Busque ofertas de cualquier marca utilizando palabras clave para hacer coincidir el título.

![Búsqueda de una oferta](/help/sites-cloud/authoring/assets/offers-search.png)

Los criterios de búsqueda actuales aparecen junto a los resultados. También puede ordenar los resultados por columna en orden ascendente o descendente. Puede realizar una búsqueda desde cualquier carpeta de cualquier biblioteca de ofertas. Los resultados de la búsqueda son los mismos independientemente de la carpeta actual.

Para buscar ofertas:

1. En la parte superior de la consola de ofertas, pulse o haga clic en el icono de la lupa. De forma predeterminada, la búsqueda se limita a las ofertas.
1. Escriba la palabra clave para buscar ofertas. Seleccione entre los resultados.
