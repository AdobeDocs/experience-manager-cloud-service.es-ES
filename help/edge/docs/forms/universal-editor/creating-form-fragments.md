---
title: Creación de fragmentos de formulario para la creación basada en WYSIWYG
description: Obtenga información sobre cómo crear fragmentos de formulario en el editor universal y añadirlos a formularios.
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: ht
source-wordcount: '1670'
ht-degree: 100%

---

# Creación de fragmentos de formulario en el editor universal

Los fragmentos de formulario son componentes reutilizables que eliminan el trabajo de desarrollo repetitivo y garantizan la coherencia en los formularios de la organización. En lugar de volver a crear secciones comunes como información de contacto, detalles de direcciones o acuerdos de consentimiento para cada formulario, puede generar estos elementos una vez como fragmentos y reutilizarlos en varios formularios.

**Objetivos de este artículo:**

- Comprender el valor empresarial y las capacidades técnicas de los fragmentos de formulario
- Crear fragmentos de formulario reutilizables mediante el editor universal
- Integrar fragmentos en formularios existentes con la configuración adecuada
- Administrar el ciclo vital de los fragmentos y mantener la coherencia en todos los formularios

**Beneficios para empresas:**

- **Tiempo de desarrollo reducido**: genere secciones de formulario comunes una vez y reutilícelas en todas partes
- **Coherencia mejorada**: diseños y contenido estandarizados en todos los formularios
- **Mantenimiento simplificado**: actualice un fragmento una vez para reflejar los cambios en todos los formularios que lo utilicen
- **Cumplimiento mejorado**: asegúrese de que las secciones normativas sigan siendo coherentes y estén actualizadas

Los fragmentos de formulario de Edge Delivery Services admiten funciones avanzadas que incluyen fragmentos anidados, varias instancias dentro de un solo formulario e integración perfecta con fuentes de datos.

## Comprensión de los fragmentos de formulario

Los fragmentos de formulario de Edge Delivery Services ofrecen potentes funciones para el desarrollo de formularios modulares:

**Funciones principales:**

- **Administración de coherencia**: los fragmentos mantienen diseños y contenido idénticos en varios formularios. Con un enfoque “cambiar una vez, reflejar en todas partes”, las actualizaciones realizadas en un fragmento se aplican automáticamente a todos los formularios en modo Previsualización.
- **Uso múltiple**: añada el mismo fragmento varias veces dentro de un solo formulario, cada vez con enlaces de datos independientes a diferentes fuentes de datos o elementos de esquema.
- **Estructuras anidadas**: cree jerarquías complejas incrustando fragmentos dentro de otros fragmentos para arquitecturas de formulario sofisticadas.

**Requisitos técnicos:**

- **Coherencia de URL de GitHub**: tanto el fragmento como cualquier formulario que lo utilice deben especificar la misma URL de repositorio de GitHub
- **Edición independiente**: los fragmentos solo se pueden modificar en su formulario independiente; no se pueden realizar cambios en el formulario host

**Comportamiento de publicación:**

>[!IMPORTANT]
>
>En el modo Previsualización, los cambios de fragmento se reflejarán inmediatamente en todos los formularios. En el modo Publicación, debe volver a publicar el fragmento y los formularios que lo utilicen para ver las actualizaciones.

>[!CAUTION]
>
>Evite las referencias de fragmento recursivas (anidar un fragmento dentro de sí mismo), ya que esto provoca errores de procesamiento y un comportamiento inesperado.

## Requisitos previos

**Requisitos de configuración técnica:**

- [Repositorio de GitHub configurado](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template) con conexión establecida entre su entorno de AEM y el repositorio de GitHub
- [Último bloque de formularios adaptables](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) añadido a su repositorio de GitHub (para proyectos de Edge Delivery Services existentes)
- Instancia de autor de AEM Forms con plantilla de Edge Delivery Services disponible
- Acceso a la URL de instancia de autor de AEM Forms as a Cloud Service y a la URL del repositorio de GitHub

**Conocimientos y permisos requeridos:**

- Comprensión básica de los conceptos de diseño de formulario y la jerarquía de componentes
- Familiaridad con la interfaz del editor universal y los flujos de trabajo de creación de formularios
- Permisos de nivel de autor en AEM Forms para crear y administrar recursos de formulario
- Comprensión de los estándares de formularios de su organización y los requisitos de componentes reutilizables

## Uso de fragmentos de formulario de Edge Delivery Services

Puede crear fragmentos de formulario de Edge Delivery Services en el editor universal y añadir los fragmentos creados a los formularios de Edge Delivery Services. Puede realizar las siguientes acciones con fragmentos de formulario de Edge Delivery Services:

- [Creación de fragmentos de formulario](#creating-form-fragments)
- [Adición de fragmentos de formulario a un formulario](#adding-form-fragments-to-a-form)
- [Administración de fragmentos de formulario](#managing-form-fragments)

+++ Creación de fragmentos de formulario

Para crear un fragmento de formulario en el editor universal, realice los siguientes pasos:

1. Inicie sesión en su instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Haga clic en **Crear > fragmento de formulario adaptable**.

   ![Crear fragmento](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   Aparece el asistente **Crear fragmento de formulario adaptable**.
1. Seleccione la plantilla basada en Edge Delivery Services en la pestaña **Seleccionar plantilla** y haga clic en **[!UICONTROL Siguiente]**.
   ![Seleccionar plantilla de Edge Delivery Services](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. Especifique el título, el nombre, la descripción y las etiquetas del fragmento. Asegúrese de especificar un nombre único para el fragmento. Si ya existe otro fragmento con el mismo nombre, el fragmento no se creará.
1. Especifique la **URL de GitHub**. Por ejemplo, si el repositorio de GitHub se llama `edsforms`, está ubicado en la cuenta `wkndforms` y la URL es `https://github.com/wkndforms/edsforms`.

   ![Propiedades básicas](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (Opcional) Haga clic para abrir la pestaña **modelo de formulario** y desde el menú desplegable **Seleccionar de**, seleccione uno de los siguientes modelos para el fragmento:

   ![Muestra el tipo de modelo en la pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **Modelo de datos de formulario (FDM)**: integre objetos y servicios de modelo de datos desde las fuentes de datos en su fragmento. Elija Modelo de datos de formulario (FDM) si el formulario requiere leer y escribir datos de varias fuentes.

   - **Esquema JSON**: integre su formulario con un sistema back-end asociando un esquema JSON que defina la estructura de datos. Le permite añadir contenido dinámico mediante los elementos de esquema.
   - **Ninguno**: especifica que se cree el fragmento desde cero sin usar ningún modelo de formulario.

   >[!NOTE]
   >
   > Para aprender a integrar formularios o fragmentos con un modelo de datos de formulario (FDM) en el editor universal para utilizar diversas fuentes de datos back-end, consulte [Integración de formularios con el modelo de datos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

1. (Opcional) Especifique la **fecha de publicación** o la **de cancelación de publicación** del fragmento en la pestaña **Avanzado**.

   ![Pestaña Avanzado](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. Haga clic en **Crear** para generar el fragmento. Aparecerá un cuadro de diálogo de éxito con opciones de edición.

   ![Editar fragmento](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. Haga clic en **Editar** para abrir el fragmento en el editor universal con la plantilla predeterminada aplicada.

   ![Fragmento del editor universal para la creación](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **Diseñar el contenido del fragmento**: añada componentes de formulario (campos de texto, listas desplegables, casillas de verificación) para generar la sección reutilizable. Para obtener instrucciones detalladas sobre los componentes, consulte [Introducción a Edge Delivery Services para AEM Forms con el editor universal (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg).

1. **Configurar propiedades del componente**: establezca los nombres de los campos, las reglas de validación y los valores predeterminados según sea necesario para su caso de uso.

1. **Guardar y previsualizar**: guarde el fragmento y use el modo Previsualización para comprobar el diseño y la funcionalidad.

   ![Captura de pantalla de un fragmento de formulario de detalles de contacto completado en el editor universal que muestra los campos para el nombre, teléfono, correo electrónico y dirección que pueden reutilizarse en varios formularios](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**Punto de comprobación de validación:**

- Cargas de fragmentos sin errores en el editor universal
- Todos los componentes del formulario se representan correctamente
- Las propiedades de campo y las reglas de validación funcionan según lo esperado
- El fragmento se guardará y estará disponible en la consola Formularios y documentos

Una vez completado el fragmento, puede [integrarlo en cualquier formulario de Edge Delivery Services](#adding-form-fragments-to-a-form).

+++


+++ Adición de fragmentos de formulario a un formulario

En este ejemplo se muestra la creación de un formulario `Employee Details` que utiliza el fragmento `Contact Details` para las secciones de información de empleados y supervisores. Este enfoque garantiza una recopilación de datos coherente y reduce los esfuerzos de desarrollo.

Para integrar un fragmento de formulario en el formulario:

1. Abra el formulario en modo de edición. 
1. Añada el componente Fragmento de formulario al formulario.
1. Abra el explorador de contenido y vaya al componente **[!UICONTROL Formulario adaptable]** en el **Árbol de contenido**.
1. Vaya a la sección, donde desea añadir un fragmento. Por ejemplo, vaya al panel **Detalles del empleado**.

   ![Navegar hasta la sección](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. Haga clic en el icono de **[!UICONTROL Añadir]** y añada el componente **[!UICONTROL Fragmento de formulario]** en la lista **Componentes de formularios adaptables**.
   ![Añadir fragmento de formulario](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   Al seleccionar el componente **[!UICONTROL Fragmento de formulario]**, el fragmento se añade a su formulario. Puede configurar las propiedades del fragmento añadido abriendo sus **Propiedades**. Por ejemplo, oculte el título del fragmento de sus **propiedades**.

   ![Configuración de las propiedades del fragmento](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. Seleccione la **Referencia de fragmento** en la pestaña **Básico**. Aparecerán todos los fragmentos disponibles para su formulario, según el modelo del formulario.

   Por ejemplo, vaya a `/content/forms/af` y seleccione el fragmento `Contact Details`.

   ![Seleccionar fragmento](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. Haga clic en **[!UICONTROL Seleccionar]**.

   El fragmento de formulario se añade por referencia al formulario y permanece sincronizado con el fragmento de formulario independiente. 

   ![Captura de pantalla que muestra el fragmento de detalles de contacto integrado correctamente en un formulario del empleado dentro del editor universal, que muestra cómo los fragmentos mantienen su estructura cuando se reutilizan](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   Puede obtener una vista previa del formulario para ver cómo aparece en el modo **Vista previa**.

   ![Vista previa](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   Del mismo modo, puede repetir los pasos 3 al 7 para insertar el fragmento `Contact Details` para el panel `Supervisor Details`.

   ![Formulario de detalles del empleado](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ Administración de fragmentos de formulario

Puede realizar varias operaciones en los fragmentos de formulario mediante la interfaz de usuario de AEM Forms.

1. Inicie sesión en su instancia de autor de AEM Forms as a Cloud Service.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.

1. Seleccione un fragmento de formulario y la barra de herramientas mostrará las siguientes operaciones que puede realizar en el fragmento seleccionado.

   ![Administrar fragmento](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>Operación</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
    </tr>
    <tr>
   <td><p>Editar</p> </td>
   <td><p>Abre el fragmento de formulario en el modo de edición.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Propiedades</p> </td>
   <td><p>Proporciona opciones para modificar las propiedades del fragmento de formulario.<br /> <br /> </p> </td>
    </tr>
    <td><p>Copiar</p> </td>
   <td><p> Proporciona opciones para copiar el fragmento de formulario y pegarlo en la ubicación deseada. <br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>Vista previa</p> </td>
   <td><p>Proporciona opciones para previsualizar el fragmento como HTML o realizar una vista previa personalizada combinando los datos de un archivo XML con el fragmento.<br /> </p> </td>
    </tr>
    <tr>
   <td><p>Descargar</p> </td>
   <td><p>Descarga el fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Iniciar revisión y Administrar revisión</p> </td>
   <td><p>Permite iniciar y administrar una revisión del fragmento seleccionado.<br /> <br />  </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>Publicar o cancelar la publicación</p> </td>
   <td><p>Publica/cancela la publicación del fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Eliminar</p> </td>
   <td><p>Elimina el fragmento seleccionado.<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>Comparar</p> </td>
   <td><p>Compara dos fragmentos de formulario diferentes para obtener una vista previa.<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

+++

## Prácticas recomendadas

**Diseño y nombre del fragmento:**

- **Usar nombres descriptivos y únicos**: elija nombres que indiquen claramente el propósito del fragmento (por ejemplo, “detalles de contacto con validación” en lugar de “fragmento1”)
- **Plan de reutilización**: diseñe fragmentos para que sean independientes del contexto y funcionen en diferentes tipos de formularios
- **Mantener los fragmentos centrados**: cree fragmentos de un solo propósito en lugar de componentes complejos multifunción

**Flujo de trabajo de desarrollo:**

- **Probar fragmentos de forma independiente**: compruebe la funcionalidad del fragmento antes de integrarlo en los formularios
- **Mantener URL de GitHub coherentes**: asegúrese de que se utiliza la misma URL de repositorio en todos los fragmentos y formularios relacionados
- **Propósito del fragmento de documento**: incluya descripciones y etiquetas claras para ayudar a los integrantes del equipo a comprender cuándo usar cada fragmento

**Publicación y mantenimiento:**

- **Coordinar publicación**: al actualizar fragmentos, planee volver a publicar todos los formularios dependientes simultáneamente
- **Control de versiones**: use mensajes de confirmación significativos al actualizar fragmentos para realizar un seguimiento de los cambios a lo largo del tiempo
- **Monitorizar dependencias**: haga un seguimiento de qué formularios utilizan cada fragmento para evaluar el impacto de la actualización

>[!TIP]
>
>Los estilos, scripts y expresiones de fragmento se conservan cuando se incrustan, por lo que debe realizar el diseño teniendo en cuenta esta herencia.

## Resumen

Ha aprendido correctamente a aprovechar los fragmentos de formulario en Edge Delivery Services para mejorar la eficacia del desarrollo y mantener la coherencia en los formularios de su organización.

**Logros clave:**

- **Comprensión**: se ha comprendido el valor comercial y las capacidades técnicas de los fragmentos de formulario
- **Creación**: fragmentos de formulario reutilizables creados usando el editor universal con la configuración adecuada
- **Integración**: se añadieron fragmentos a los formularios con la configuración de referencia y de propiedad correctas
- **Administración**: operaciones de ciclo de vida de fragmento exploradas y flujos de trabajo de mantenimiento

**Próximos pasos:**

- Crea una biblioteca de fragmentos de uso común para su organización
- Establecer convenciones de nomenclatura y políticas de gobernanza para el uso de fragmentos
- Explorar la integración avanzada con [modelos de datos de formulario](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) para fragmentos dinámicos impulsados por datos
- Implementar plantillas de formulario basadas en fragmentos para lograr experiencias de usuario coherentes

Ahora, sus formularios se benefician de una arquitectura modular y fácil de mantener que se adapta de manera eficiente a todos los proyectos, al tiempo que garantiza experiencias de usuario coherentes.


