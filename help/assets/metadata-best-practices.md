---
title: Administración de metadatos y prácticas recomendadas
description: Conozca las prácticas recomendadas sobre metadatos para administrar sus recursos digitales de forma eficaz.
role: User, Admin
exl-id: d90519df-55a6-4e23-81ad-ff2365d71c0d
feature: Metadata, Best Practices
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 2%

---

<!-- Keywords to focus on:
metadata best practices
aem metadata 
experience manager metadata-->

# Administración de metadatos y prácticas recomendadas {#metadata-best-practices}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

Para que su empresa destaque y atraiga a más clientes, es crucial utilizar imágenes de alta calidad, como imágenes, vídeos y otros recursos digitales. Para conseguirlo, necesita un proceso que le permita añadir metadatos a todos los recursos digitales, facilitando su búsqueda. Los metadatos son los datos que proporcionan detalles esenciales sobre los recursos digitales, como el nombre, el tipo, la ubicación dentro de un repositorio, la fecha de modificación y las etiquetas asociadas. Los metadatos optimizan la administración de recursos, mejoran la capacidad de búsqueda y accesibilidad, y garantizan un control de versiones eficaz.

Aprenda a utilizar los metadatos en el sistema de administración de activos digitales (DAM) para [administrar de forma eficaz los metadatos de sus recursos digitales](manage-metadata.md).

## Tipos de metadatos

En función de los distintos aspectos de los datos, los metadatos se clasifican en metadatos técnicos, metadatos informativos y metadatos administrativos.

### Metadatos técnicos

Los metadatos técnicos comprenden los aspectos técnicos de un recurso. Este tipo de metadatos es crucial para que los usuarios comprendan las características inherentes de los recursos digitales, lo que facilita un procesamiento y una utilización eficientes.
Incluye detalles como:

* Tamaño del archivo
* Formato
* Resolución
* Dimensiones
* Modo de color

### Metadatos informativos

Los metadatos informativos incluyen información descriptiva que mejora la comprensión del contenido de un recurso. Estos metadatos son fundamentales para la detección de contenido, la búsqueda y la comprensión de la importancia del recurso. Los metadatos informativos incluyen palabras clave, subtítulos y descripciones.

Por ejemplo, al administrar un vídeo en Experience Manager Assets, podemos incluir los siguientes metadatos informativos:

* **Palabras clave**: Marketing, lanzamiento de producto, Promoción
* **Pie de ilustración**: Presentamos nuestro último producto con interesantes características
* **Descripción**: Una descripción detallada del contenido del vídeo.

Los usuarios que buscan contenido relacionado con el marketing pueden encontrar y comprender fácilmente la importancia del vídeo anterior.

### Metadatos administrativos

Los metadatos administrativos tratan los aspectos administrativos de los recursos digitales. Garantiza el control de acceso, el cumplimiento y la administración del ciclo de vida general de los recursos dentro del sistema de administración de recursos digitales. Incluye información relacionada con lo siguiente:

* Propiedad de activos
* Derechos de uso
* Permisos
* Otros detalles administrativos

Los metadatos administrativos garantizan la administración correcta de los recursos, el control del acceso y el cumplimiento normativo dentro del sistema de administración de recursos digitales.

## Prácticas recomendadas de metadatos

### Defina su estrategia de metadatos desde el principio

La administración de metadatos comienza con la definición de una estrategia de metadatos para proporcionar una base para evaluar el valor a largo plazo.

La creación de un esquema de metadatos personalizado según sus necesidades es crucial a la hora de planificar su estrategia de metadatos. Un esquema bien diseñado proporciona un marco de trabajo estructurado para categorizar y organizar los recursos en Experience Manager.

#### Vídeo: Agregar campos personalizados al esquema de metadatos

>[!VIDEO](https://video.tv.adobe.com/v/3425977)

Su estrategia de metadatos puede incluir la definición de lo siguiente:

* **Objetivos:** Describa claramente los objetivos y los resultados esperados de los metadatos. Identifique lo que desea lograr agregando metadatos.

* **Propósito:** Defina por qué está capturando metadatos. Especifique el valor que agrega a los procesos, sistemas u organización.

* **Plan de accesibilidad:** Cree un plan para que los metadatos sean fácilmente accesibles y detectables. Explique quién lo va a utilizar y las herramientas o métodos que se van a utilizar.

* **Propiedades de metadatos:** Identifique y defina cada propiedad de metadatos con cuidado. Asegúrese de que cada propiedad tenga una razón clara para incluirse, conectándose con los objetivos y el propósito.

Para garantizar resultados coherentes en todo el repositorio, planifique cuidadosamente la estrategia. Más información sobre [esquemas de metadatos](metadata-schemas.md).

### Creación de un plan de gobernanza de metadatos

La gobernanza de datos garantiza que los esfuerzos de administración de metadatos de la organización estén alineados con los objetivos empresariales generales.
La estrategia de gobernanza puede incluir:

* Establecer políticas y procedimientos para la gestión de datos y metadatos.
* Establecer estándares para la calidad y la integridad de los datos.
* Definición de funciones y responsabilidades en la administración de datos.

Determine de dónde proviene la información y examine los detalles de la estrategia de metadatos, incluidas las propiedades y sus fuentes. Puede ampliarse según la complejidad de la estrategia. En las grandes empresas, hay un sistema de gestión de metadatos principal que supervisa varios sistemas en la pila principal.

>[!NOTE]
>
>Aprenda a [administrar metadatos de sus recursos digitales](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html?lang=es).

### Ser coherente con la estrategia de metadatos

Una estrategia de metadatos uniforme garantiza la organización y recuperación eficaces de los recursos digitales. Adoptar un enfoque estratégico para capturar e implementar valores de metadatos, lo que permite la flexibilidad para la evolución sin cambios innecesarios. <br>

En la administración de metadatos en toda la empresa, la coherencia es importante a la hora de nombrar y hacer referencia a los recursos. Por ejemplo, cuando administre varios recursos simultáneamente, considere la posibilidad de agregar metadatos de forma masiva. <br>

Estas son algunas de las prácticas recomendadas a seguir:

* **Evitar valores duplicados:** Si tiene una colección de imágenes de una campaña de marketing, use nombres coherentes y evite duplicados.<br>
Por ejemplo, en lugar de usar nombres duplicados como *campaign_image_001* y *campaign_image_002*, implemente una convención de nombres sistemática como *event_promotion* y *product_launch*, que garantice una identificación clara y ordenada.

* **Use vocabularios controlados de forma eficaz:** Implemente vocabularios controlados empleando términos estandarizados para las etiquetas. Aprenda a implementar [AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md) de forma eficaz.  <br>
Por ejemplo, use términos como *product_launch* o *event_promotion* de forma consistente al etiquetar imágenes con temas para mantener una secuencia sistemática.

* **Mantener la precisión y la integridad:** Para mantener la coherencia, la precisión, la integridad y la alineación de los metadatos en varios orígenes son cruciales.
Por ejemplo, al agregar metadatos a un documento de PDF, compruebe que detalles como los nombres de autor y las palabras clave sean precisos y completos.

#### Vídeo: Añadir metadatos masivos a los recursos

>[!VIDEO](https://video.tv.adobe.com/v/3425978)

### Evaluar y mejorar la capacidad de búsqueda de metadatos

Evalúe la estrategia de metadatos para mejorar la capacidad de búsqueda. Simplifique los flujos de trabajo y mejore las capacidades de búsqueda para una reutilización eficiente. Evite tratar con metadatos que no tengan un propósito claro.

Puede tener en cuenta las siguientes prácticas recomendadas para optimizar la búsqueda de metadatos:

* **Optimización de palabras clave:** Mejore la capacidad de búsqueda de metadatos optimizando las palabras clave asociadas con los recursos. Puede mejorar la relevancia de las palabras clave para recursos concretos en [!UICONTROL Assets Manager] si sigue estos pasos:

   1. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivo]** > **[!UICONTROL [Carpeta de recursos]]**.
   1. Seleccione el recurso cuyos metadatos desea actualizar y, a continuación, haga clic en **[!UICONTROL Propiedades]**.
   1. Vaya a la ficha **[!UICONTROL Avanzado]** y, a continuación, haga clic en **[!UICONTROL Agregar]** en **[!UICONTROL Elevar para las palabras clave de búsqueda]**. <br>Debe usar el esquema de metadatos predeterminado para elevar las palabras clave de búsqueda.
   1. Escriba la palabra clave para la que desea aumentar la búsqueda y, a continuación, haga clic en **[!UICONTROL Agregar]**.<br>
Puede agregar varias palabras clave y organizarlas según su prioridad.
   1. Haga clic en **[!UICONTROL Guardar y cerrar]**.
Busque el recurso con las palabras clave agregadas. El recurso aparece entre los resultados de búsqueda principales.

  Aprenda a [aumentar la búsqueda en Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html?lang=es).

* **Campos de metadatos personalizados:** Personalice los campos de metadatos para capturar información adicional sobre los recursos. Por ejemplo, agregue campos específicos para los detalles del proyecto, la información de copyright o cualquier otro dato relevante que mejore las capacidades de búsqueda. Aprenda [a editar o agregar metadatos personalizados](meta-edit.md) en Experience Manager Assets.


* **Validación de metadatos:** Implemente comprobaciones de validación para las entradas de metadatos a fin de garantizar la coherencia y la precisión. El uso de vocabularios controlados hace que el proceso de validación sea más suave y reduce las posibilidades de que las entradas no sean claras o incoherentes. Esto puede implicar configurar directrices para determinadas propiedades de metadatos a fin de evitar información ambigua o incoherente.

* **Seguimiento del uso:** Evalúe la relevancia y el uso de distintas propiedades de metadatos a lo largo del tiempo. Identificar y priorizar los metadatos utilizados con frecuencia o contribuir de forma significativa a los procesos de búsqueda y recuperación.

#### Vídeo: Añadir palabras clave para mejorar la capacidad de búsqueda

>[!VIDEO](https://video.tv.adobe.com/v/3425979)

### Mantenga los metadatos simples y fáciles de entender

Simplifique los metadatos para mejorar la gobernanza y la adopción de usuarios. Sea directo y fácil de entender, lo que anima a los usuarios a añadir información esencial.
Pruebe las siguientes prácticas recomendadas para simplificar los metadatos:

* **Optimizar opciones de propiedad:** Céntrese en resaltar propiedades esenciales sin sobrecargar a los usuarios con demasiados campos de metadatos para rellenar. Por ejemplo, al añadir metadatos para una imagen, incluya solo campos clave como título, descripción y etiquetas para una categorización eficaz.

* **Elimine las propiedades predeterminadas innecesarias:** Simplifique el formulario de metadatos eliminando las propiedades predeterminadas que sean irrelevantes para su caso de uso. Elimine las propiedades predeterminadas poco utilizadas para conseguir una interfaz y una experiencia más limpias.

* **Revise y actualice los metadatos periódicamente:** Actualice los metadatos con regularidad y adapte a las cambiantes necesidades y tecnologías para garantizar que los usuarios proporcionen información valiosa a lo largo del tiempo.

### Analizar recorrido de contenido

Examine la cadena de suministro de contenido para encontrar fuentes de metadatos e incluir a todas las partes interesadas, empezando por la parte superior, para obtener un enfoque exhaustivo de las prácticas recomendadas. Incluir a diferentes miembros del personal para garantizar un apoyo completo en toda la organización. <br>Incorpore metadatos en varias etapas para compartir la responsabilidad de proporcionar detalles de recursos durante la carga. Por ejemplo, integrar [!DNL Experience Manager Assets] y [!DNL Workfront] ofrece beneficios sustanciales en términos de administración de metadatos, mejorando la eficiencia y la colaboración en la creación y administración de contenido. Esta integración garantiza la sincronización efectiva de los metadatos de los recursos vinculados, actualizando automáticamente los detalles del proyecto cuando se realizan cambios en [!DNL Workfront].

Comunicar los objetivos, el progreso, los hitos y los desafíos desde el principio para recibir las aportaciones y la cooperación de todas las partes interesadas. Fomente la colaboración en toda la organización para crear procesos eficientes y metadatos valiosos.

Obtenga más información acerca de [metadatos y sus conceptos relacionados](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-concepts.html?lang=es) para administrar de manera eficaz sus metadatos de Experience Manager.
