---
title: Panel de realización de valor de AEM Forms
description: Supervise fácilmente los envíos de formularios en las instancias de AEM Forms con nuestro intuitivo panel de seguimiento.
feature: Adaptive Forms, Foundation Components, Core Components
role: Admin, Developer, Leader, User
hide: true
hidefromtoc: true
source-git-commit: 613adeee805069155881b1a26b247c3dec3eb593
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 22%

---


# Comprender el panel de realización de valores: Saque el máximo partido a Forms {#value-realization-dashboard}

Bienvenido a su ventanilla única para comprender el valor que aportan sus formularios. Este tablero le proporciona información valiosa para optimizar los formularios, optimizar los flujos de trabajo y, en última instancia, lograr los objetivos más rápido.

## ¿Qué hay en el panel? {#content-of-dashboard}

Este tablero es la ventana al mundo del uso del formulario. Este es un desglose de las secciones clave:

### Actividad de formulario con el tiempo:

* **Envíos de formularios**: vea las tendencias en la frecuencia con la que se completan los formularios.
* **Representaciones de documentos**: rastrea el número de documentos representados a lo largo del tiempo.
* **Forms creado y publicado**: monitorice la velocidad a la que se crean e implementan nuevos formularios.
* **Tiempos de creación y publicación de formularios**: Analice los tiempos promedio de creación y publicación de formularios para identificar áreas que se deben mejorar.

### Uso de fragmentos:

* **Número de fragmentos de formulario en uso**: consulte cuántas secciones de formulario reutilizables están incorporadas actualmente a formularios activos.
* **Número de reutilización de fragmentos de formulario**: Mida la frecuencia con la que estos fragmentos se utilizan en diferentes formularios.


## ¿Cómo Te Beneficia Esto? {#benefits-to-you}

Este tablero le permite tomar decisiones basadas en datos sobre sus formularios. A continuación se muestra cómo:

* **Identificación de Forms populares**: Las altas tasas de envío indican formularios valiosos. Analícelas para conocer las prácticas recomendadas y poder replicarlas en otros.
* **Optimizar creación de formularios**: Reduzca los tiempos de creación identificando cuellos de botella. Explore las plantillas creadas previamente para optimizar los flujos de trabajo.
* **Aumentar la reutilización de fragmentos**: Fomente la colaboración y la capacidad de detección de fragmentos reutilizables. Las bibliotecas de fragmentos bien organizadas pueden mejorar significativamente la eficacia.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="Rastreador de envíos de formularios"
>abstract="Este gráfico representa el recuento de los envíos de formularios adaptables durante períodos de tiempo específicos. El aumento de los envíos podría indicar que el formulario está ganando popularidad o que es necesario recopilar más datos de los usuarios. **Nota:** El gráfico proporciona datos específicos de la instancia actual, lo que le permite analizar rápidamente las tendencias y tomar decisiones informadas. Para enviar datos de otras instancias, acceda simplemente al panel de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="Rastreador de representaciones de documentos"
>abstract="Este gráfico representa el recuento de representaciones de documentos durante períodos de tiempo específicos. **Nota:** El gráfico proporciona datos específicos de la instancia actual, lo que le permite analizar rápidamente las tendencias y tomar decisiones informadas. Para enviar datos de otras instancias, acceda simplemente al panel de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="Nuevo rastreador de formularios"
>abstract="El gráfico proporciona información sobre el número de formularios recién creados durante períodos de tiempo específicos. **Nota:** El gráfico proporciona datos específicos de la instancia de autor actual de AEM Forms. Para ver datos de otras instancias, acceda al panel de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="Rastreador de formularios publicados"
>abstract="El gráfico proporciona información sobre el número de formularios que se han publicado correctamente durante períodos de tiempo específicos. **Nota:** El gráfico proporciona datos específicos de la instancia de publicación de AEM Forms actual. Para ver los datos de conversión de otras instancias, acceda al panel de la instancia correspondiente."


## Conversión de Insights en acción {#turning-insights-into-actions}

¡Traduzcamos estos hallazgos en pasos procesables!

* **¿Envíos bajos?** Investigue la claridad y la facilidad de uso del formulario. ¿Es demasiado largo o tiene preguntas confusas? Considere la posibilidad de revisar para mejorar la experiencia del usuario.
* **¿Tiempos de alta creación?** Desglose el proceso de creación. ¿Hay pasos o funciones innecesarios que no se utilizan de forma eficaz? Utilice funciones que ahorren tiempo, como plantillas.
* **¿Fragmentos infrautilizados?** Asegúrese de que los fragmentos estén bien organizados, que se puedan buscar y que sean fáciles de entender. Considere la posibilidad de promocionar el uso de fragmentos dentro de su equipo.

Al analizar estas tendencias, puede crear mejores formularios, ahorrar tiempo en la creación y aprovechar los componentes reutilizables. Esto se traduce en un flujo de trabajo más fluido, usuarios más felices y, en última instancia, un mayor retorno de su inversión.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="Duración media de la generación de formularios"
>abstract="El gráfico ilustra el tiempo medio necesario para crear un formulario. Cada barra del gráfico representa un formulario específico y la altura de la barra indica la duración media de creación del formulario durante ese lapso de tiempo. "

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="Duración media de creación de formularios"
>abstract="El gráfico muestra el tiempo medio que se tarda en crear y publicar un formulario, medido desde el día inicial en que se abrió el formulario para editarlo. **Nota:** El gráfico proporciona datos específicos de la instancia de autor actual de AEM Forms. Para ver datos de otras instancias, acceda al panel de la instancia correspondiente."


>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Rastreador de fragmentos de Forms"
>abstract="Este gráfico le ayuda a ver cuántos fragmentos de formulario está utilizando en los formularios. **Nota:** El gráfico proporciona datos específicos de la instancia de publicación de AEM Forms actual. Para ver los datos de conversión de otras instancias, acceda al panel de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Rastreador de tiempo promedio de fragmentos de formulario"
>abstract="El gráfico muestra el tiempo medio que se tarda en crear un fragmento de formulario, medido desde el día inicial en que se abrió el fragmento de formulario para editarlo. **Nota:** El gráfico proporciona datos específicos de la instancia de publicación de AEM Forms actual. Para ver los datos de conversión de otras instancias, acceda al panel de la instancia correspondiente."


## Sugerencias adicionales {#additional-tips}

* **Establecer metas:** Determine lo que desea lograr con los formularios. ¿Se trata de una mayor recopilación de datos, una generación más rápida de posibles clientes o una mejor satisfacción del cliente? Conocer sus objetivos guiará su análisis del panel.
* **Revisión regular:** Programe registros regulares con el panel para rastrear el progreso e identificar nuevas áreas para mejorar.
* **Experimentar y refinar:** No tenga miedo de experimentar con diferentes diseños de formulario y uso de fragmentos. El tablero le ayudará a medir la eficacia de sus cambios.

¡Recuerda, este tablero es tu aliado! Utilizándolo de forma eficaz, puede transformar sus formularios de herramientas sencillas de recopilación de datos en activos estratégicos que impulsen el éxito para usted y su empresa.
