---
title: Aptitud de creación de comunicación
description: Obtenga información acerca de la capacidad de creación de comunicaciones del agente de producción de experiencia y cómo utilizar el lenguaje natural para crear comunicaciones interactivas.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: dab727f81a8863ca82c7c531e65c365b29fd5c23
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---


# Aptitud de creación de comunicación {#ic-creation-skill}

>[!NOTE]
>
> La aptitud de creación de comunicaciones se encuentra actualmente en alfa. Si desea participar, envíe una solicitud desde su dirección de correo electrónico oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com).

Las comunicaciones interactivas son documentos personalizados basados en datos y diseñados para la correspondencia comercial, como extractos de cuentas, documentos de políticas, facturas, kits de bienvenida y avisos de beneficios. A diferencia de los formularios que recopilan entradas de los usuarios, las comunicaciones interactivas generan documentos de salida con contenido dinámico específico del destinatario.

La aptitud de creación de comunicaciones es una capacidad de Experience Production Agent que está diseñada para desarrollar comunicaciones interactivas mediante indicadores de lenguaje natural. Esta aptitud genera automáticamente correspondencia personalizada y basada en datos para su impresión (en formato PDF). La aptitud se muestra a través del asistente de IA.

Algunos de los beneficios clave de la habilidad de creación de comunicaciones incluyen:

* **Desarrollo acelerado de la comunicación**: cree comunicaciones rápidamente utilizando comandos sencillos de lenguaje natural, lo que elimina la necesidad de aprender interfaces de productos tradicionales.
* **Correspondencia coherente y sin marca**: cree comunicaciones que sigan las directrices de estilo, plantillas y marca de su organización mediante plantillas y estilos aprobados.
* **Barrera técnica inferior**: permite a los usuarios empresariales crear comunicaciones fácilmente, sin necesidad de conocimientos técnicos avanzados o de productos profundos.

## Capacidades {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The agent automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **Crear a partir de plantillas**: puede usar plantillas organizativas aprobadas para garantizar la coherencia de la marca y los estándares de cumplimiento. El agente aprovecha las plantillas existentes y las directrices de estilo para crear correspondencia dentro de la marca que cumpla los requisitos regulatorios.

* **Importar y convertir imágenes y documentos existentes en comunicaciones interactivas**: puede importar y transformar documentos existentes en comunicaciones interactivas. El agente analiza el contenido cargado para detectar campos, conservar diseños y crear correspondencia basada en datos con capacidades de contenido dinámico. Los formatos admitidos son PDF, imágenes (JPG, PNG) y plantillas dibujadas a mano.


## Ejemplos de peticiones de datos {#sample-prompts}

* *Cree una comunicación para un extracto de préstamo con la plantilla en https://[aem-author-url]/path/to/pdf/file*
* *Cree una comunicación desde PDF en https://[aem-author-url]/path/to/pdf/file*
* *Cree una comunicación a partir del archivo de imagen en https://[aem-author-url]/path/to/image/file*
* Cree una carta utilizando el archivo PDF en https://[aem-author-url]/path/to/pdf/file


## Refine la comunicación {#refine-with-ic-editor}


Después de crear la estructura de comunicación inicial mediante el Ayudante de IA, puede utilizar el Editor de comunicaciones interactivas para refinar y mejorar el documento. En el Editor de comunicaciones interactivas, puede proporcionar indicadores en lenguaje natural para lo siguiente:

* **Agregar campos y contenido**: agregue nuevos campos, bloques de texto, imágenes, gráficos, tablas y otros componentes a los documentos de comunicación utilizando indicaciones en lenguaje natural. El agente interpreta las instrucciones e inserta los elementos adecuados con la estructura y el formato adecuados.

* **Editar campos y contenido**: modifique los campos y el contenido existentes en los documentos de comunicación mediante comandos conversacionales. Actualice las propiedades del campo, cambie el contenido del texto, ajuste los enlaces de datos y perfeccione las configuraciones del componente.

* **Quitar campos y contenido**: elimine campos, componentes o secciones no deseados de los documentos de comunicación mediante instrucciones en lenguaje natural. El agente elimina los elementos especificados manteniendo al mismo tiempo la estructura del documento y la integridad del diseño.

* **Campos de estilo y contenido**: aplique formato y estilo a los campos y al contenido mediante mensajes en lenguaje natural. Ajuste fuentes, colores, alineación, espaciado y otras propiedades visuales para que coincidan con las directrices de marca y los requisitos de diseño.

### Ejemplos de peticiones de datos para perfeccionar las comunicaciones {#sample-prompts-refining}

* *Generar una carta de liquidación de reclamación de seguro de vehículo*
* *Poner en cursiva el texto de exención de responsabilidad*
* *Cambiar el tamaño de fuente del texto de exención de responsabilidad a 12*
* *Actualizar el color de fuente del texto de exención de responsabilidad a rojo*
* *Actualizar el color de fondo de los cuadros de texto de encabezado y pie de página a gris claro*
* *Agregar un nuevo panel de exención de responsabilidad con campos de firma y confirmación*
* *Quitar el campo de texto de confirmación*
* *Agregar una tabla de detalles de pago con tres columnas*
* *Actualizar la alineación del campo de número de directiva al centro*
* *Cambiar el interlineado de la sección de términos y condiciones a 1.5*

Para obtener más información sobre las capacidades del editor de comunicaciones interactivas, consulte [Documentación de comunicaciones interactivas](/help/forms/introduction-to-interactive-communication.md).
