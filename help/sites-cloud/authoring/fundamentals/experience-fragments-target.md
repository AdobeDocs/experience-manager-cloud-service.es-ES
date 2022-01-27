---
title: Exportación de fragmentos de experiencias a Adobe Target
description: Exportación de fragmentos de experiencias a Adobe Target
source-git-commit: 4b83fdbe4c0c260a609734b3c460ce884f0c8c9e
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---

# Exportación de fragmentos de experiencias a Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* Los AEM fragmentos de experiencias se exportan al espacio de trabajo predeterminado de Adobe Target.
>* AEM debe integrarse con Adobe Target según las instrucciones de [Integración con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).


Puede exportar [Fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md), creado en Adobe Experience Manager as a Cloud Service (AEM), en Adobe Target (Target). Luego pueden utilizarse como ofertas en actividades de Target para probar y personalizar experiencias a escala.

Hay tres opciones de formato disponibles para exportar un fragmento de experiencia a Adobe Target:

* HTML (predeterminado): Compatibilidad con la entrega de contenido web e híbrido
* JSON: Compatibilidad con entrega de contenido sin encabezado
* HTML y JSON

Después [Integración con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) AEM fragmentos de experiencias se pueden exportar al espacio de trabajo predeterminado en Adobe Target o a espacios de trabajo definidos por el usuario para Adobe Target.

>[!NOTE]
>
>Los espacios de trabajo de Adobe Target no existen en Adobe Target. Se definen y administran en Adobe IMS (Identity Management System) y, a continuación, se seleccionan para su uso en todas las soluciones mediante integraciones de Adobe I/O.

>[!NOTE]
>
>Los espacios de trabajo de Adobe Target se pueden utilizar para permitir a los miembros de una organización (grupo) crear y administrar ofertas y actividades solo para esta organización; sin dar acceso a otros usuarios. Por ejemplo, las organizaciones específicas de los países dentro de una preocupación mundial.

>[!NOTE]
>
>Para obtener más información, consulte también:
>
>* [Desarrollo de Adobe Target](https://www.adobe.io/apis/experiencecloud/target.html)
>* [Componentes principales: fragmentos de experiencias](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
>* [Adobe Target: ¿Cómo Utilizo Los Fragmentos De Experiencia De Adobe Experience Manager (AEM)?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)


## Requisitos previos {#prerequisites}


Se requieren varias acciones:

1. Tiene que [integrar AEM con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).
2. Los fragmentos de experiencias se exportan desde la instancia de creación de AEM, por lo que debe [Configuración del externalizador de vínculos de AEM](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) en la instancia de autor para garantizar que todas las referencias dentro del fragmento de experiencia se externalicen para la entrega web.

   >[!NOTE]
   >
   >Para que la reescritura de vínculos no esté cubierta por el valor predeterminado, la variable [Proveedor de reescritura de vínculos de fragmentos de experiencia](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) está disponible. Con esto, se pueden desarrollar reglas personalizadas para su caso.

## Añadir la configuración de nube {#add-the-cloud-configuration}

Antes de exportar un fragmento, debe agregar la variable **Configuración de nube** para **Adobe Target** al fragmento o carpeta. Esto también le permite:

* especifique las opciones de formato que se utilizarán para la exportación
* seleccionar un espacio de trabajo de Target como destino
* seleccione un dominio externalizador para reescribir referencias en el fragmento de experiencia (opcional)

Las opciones requeridas se pueden seleccionar en **Propiedades de página** de la carpeta o fragmento necesarios; la especificación se hereda según sea necesario.

1. Vaya a la **Fragmentos de experiencias** consola.

1. Apertura **Propiedades de página** para la carpeta o fragmento correspondiente.

   >[!NOTE]
   >
   >Si agrega la configuración de nube a la carpeta principal del fragmento de experiencia, la configuración la heredan todos los elementos secundarios.
   >
   >
   >Si agrega la configuración de nube al propio fragmento de experiencia, esta se hereda de todas las variaciones.

1. Seleccione el **Cloud Services** pestaña .

1. En **Configuración del Cloud Service**, seleccione **Adobe Target** en la lista desplegable.

   >[!NOTE]
   >
   >El formato JSON de una oferta de fragmento de experiencia se puede personalizar. Para ello, defina un componente de fragmento de experiencia del cliente y, a continuación, anote cómo exportar sus propiedades en el componente Modelo Sling.
   >
   >Consulte el componente principal:
   >
   >[Componentes principales: fragmentos de experiencias](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   En **Adobe Target** seleccione:

   * la configuración adecuada
   * la opción de formato requerido
   * un espacio de trabajo de Adobe Target
   * si es necesario: el dominio externalizador

   >[!CAUTION]
   >
   >El dominio externalizador es opcional.
   >
   > Se configura un externalizador de AEM cuando desea que el contenido exportado apunte a un *publicar* dominio. Para obtener más información, consulte [Configuración del externalizador de vínculos AEM](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > Tenga en cuenta también que los dominios externalizadores solo son relevantes para el contenido del fragmento de experiencia que se envía a Target y no para los metadatos como Ver contenido de la oferta.

<!--
   For example, for a folder:

   ![Folder - Cloud Services](assets/xf-target-integration-01.png "Folder - Cloud Services")
-->

1. **Guardar y cerrar**.

## Exportación de un fragmento de experiencia a Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Para los recursos multimedia, como las imágenes, solo se exporta una referencia a Target. El recurso en sí permanece almacenado en AEM Assets y se entrega desde la instancia de publicación de AEM.
>
>Debido a esto, el fragmento de experiencia, con todos los recursos relacionados, debe publicarse antes de exportarse a Target.

Para exportar un fragmento de experiencia de AEM a Target (después de especificar la Configuración de nube):

1. Vaya a la consola Fragmento de experiencias .
1. Seleccione el fragmento de experiencia que desea exportar a target.

   >[!NOTE]
   >
   >Debe ser una variación web de fragmento de experiencia.

1. Toque o haga clic **Exportar a Adobe Target**.

   >[!NOTE]
   >
   >Si el fragmento de experiencia ya se ha exportado, seleccione **Actualización en Adobe Target**.

1. Toque o haga clic **Exportación sin publicación** o **Publicación** según sea necesario.

   >[!NOTE]
   >
   >Selección **Publicación** publicará de inmediato el fragmento de experiencia y lo enviará a Target.

1. Toque o haga clic **OK** en el cuadro de diálogo de confirmación.

   El fragmento de experiencia debería estar en Target.

   >[!NOTE]
   >
   >[Varios detalles](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) de la exportación se puede ver en **Vista de lista** de la consola y **Propiedades**.

   >[!NOTE]
   >
   >Al ver un fragmento de experiencia en Adobe Target, la variable *última modificación* la fecha en la que se ve es la fecha en la que se modificó por última vez el fragmento en AEM, no la fecha en la que se exportó por última vez a Adobe Target.

>[!NOTE]
>
>También puede realizar la exportación desde el editor de páginas utilizando comandos comparables en la variable [Información de la página](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) para abrir el Navegador.

## Uso de los fragmentos de experiencias en Adobe Target {#using-your-experience-fragments-in-adobe-target}

Después de realizar las tareas anteriores, el fragmento de experiencia se muestra en la página Ofertas de Target. Consulte el [documentación específica de Target](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) para aprender lo que se puede lograr allí.

>[!NOTE]
>
>Al ver un fragmento de experiencia en Adobe Target, la variable *última modificación* la fecha en la que se ve es la fecha en la que se modificó por última vez el fragmento en AEM, no la fecha en la que se exportó por última vez a Adobe Target.

## Eliminación de un fragmento de experiencia ya exportado a Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

La eliminación de un fragmento de experiencia que ya se ha exportado a Target puede causar problemas si el fragmento ya se está utilizando en una oferta de Target. Si se elimina el fragmento, la oferta quedaría inutilizable, ya que el contenido del fragmento lo AEM.

Para evitar estas situaciones:

* Si el fragmento de experiencia no se está utilizando en una actividad, AEM permite al usuario eliminar el fragmento sin un mensaje de advertencia.
* Si una actividad de Target está utilizando actualmente el fragmento de experiencia, un mensaje de error advierte al usuario AEM de las posibles consecuencias que tendrá la eliminación del fragmento en la actividad.

   El mensaje de error de AEM no impide que el usuario elimine (a la fuerza) el fragmento de experiencia. Si se elimina el fragmento de experiencia:

   * La oferta de Target con AEM fragmento de experiencia puede mostrar un comportamiento no deseado

      * Es probable que la oferta se siga procesando, ya que el HTML del fragmento de experiencia se insertó en Target
      * Puede que cualquier referencia en el fragmento de experiencia no funcione correctamente si también se eliminaron recursos a los que se hace referencia en AEM.
   * Por supuesto, cualquier modificación adicional en el fragmento de experiencia es imposible, ya que el fragmento de experiencia ya no existe en AEM.
