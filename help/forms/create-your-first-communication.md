---
title: Cree su primera comunicación interactiva
description: Diseñe comunicaciones dinámicas impulsadas por datos con facilidad con las comunicaciones interactivas de AEM Forms
feature: Release Information
role: Admin
hide: true
hidefromtoc: true
source-git-commit: a771aa7e683cfbcacc8a9d5765c63d50169a2756
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 48%

---


# Cree su primera comunicación interactiva


>[!VIDEO](https://video.tv.adobe.com/v/3444094/)

## Paso 1: Planificar la comunicación interactiva

El primer paso de la planificación de una comunicación interactiva es finalizar el contenido de la comunicación. Una vez finalizado, debe analizarlo para identificar los distintos tipos de recursos necesarios para crear la comunicación interactiva.

### Consideraciones sobre la planificación

Una comunicación interactiva contiene los siguientes elementos:

* El **texto estático** incluye principalmente las partes de la comunicación interactiva que son de naturaleza genérica y se incluyen en las comunicaciones de todos los clientes, como el encabezado, el pie de página, el saludo o las exenciones de responsabilidad legal.

* Los **datos procedentes de un sistema back-end (modelo de datos de formulario)** son específicos del cliente y se combinan dinámicamente con la comunicación interactiva. Por ejemplo, el número de póliza o la dirección pueden obtenerse mediante el modelo de datos de formulario.

* El **diseño o las plantillas** para la versión impresa y web de la comunicación interactiva.

* El **orden** en el que aparecen los distintos párrafos de texto en la comunicación interactiva.

* Los **datos condicionales** que se rellenan en función de condiciones predefinidas. Por ejemplo, la fecha en la que se genera la comunicación interactiva.

* Las **imágenes almacenadas en un repositorio**, como logotipos e imágenes de firma. Las imágenes como logotipos corporativos aparecerían en la mayoría o en todas las comunicaciones interactivas.

* Las **tablas y los gráficos** son necesarios para simplificar la representación de datos complejos en una comunicación interactiva.

### Estructura de la comunicación interactiva

Una vez finalizado el contenido y los elementos utilizados para crear la comunicación interactiva, puede crear la estructura de la comunicación interactiva. La estructura debe tener los detalles enumerados en la sección Consideraciones sobre la planificación. Por ejemplo, una estructura de la factura mensual que un operador de telecomunicaciones envía a sus clientes.

La estructura contiene datos con los siguientes modos de entrada:

* Texto estático
* Modelo de datos de formulario
* Datos condicionales
* Imágenes


## Paso 2: Crear un modelo de datos de formulario

Un modelo de datos de formulario permite conectar una comunicación interactiva a distintas fuentes de datos. Por ejemplo, un perfil de usuario de AEM, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Un modelo de datos de formulario es un esquema de representación de datos unificado de entidades y servicios empresariales disponibles en fuentes de datos conectadas. Puede utilizar el modelo de datos de formulario con una comunicación interactiva para recuperar datos de fuentes de datos conectadas. Para obtener información sobre el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](/help/forms/data-integration.md).

## Paso 3: Crear fragmentos

Los fragmentos de documento son componentes reutilizables de una correspondencia que se utilizan para componer una comunicación interactiva. Los fragmentos de documento son de tipo: Texto, Lista y Condición.


## Paso 4: Crear plantillas

El editor de comunicaciones interactivas proporciona varias plantillas OOTB. Puede modificar estas plantillas según los requisitos de su organización o crear una plantilla desde cero.


## Paso 5: Crear una comunicación interactiva

Una vez creados todos los componentes básicos, como el modelo de datos de formulario, los fragmentos de documento y las plantillas para la versión web, puede empezar a crear una comunicación interactiva. Para empezar a crear una comunicación interactiva:

1. Inicie sesión en su entorno as a Cloud Service de AEM Forms.
1. Vaya a Forms > Forms y documentos
1. Haga clic en **Crear** y seleccione **Documento de comunicación**. Se le mostrará una pantalla de configuración para configurar las siguientes opciones:

   | Campo | Descripción | Obligatorio |
   |-------|-------------|----------|
   | Nombre | Identificador único de la comunicación | Sí |
   | Título | Nombre para mostrar de la comunicación | Sí |
   | Descripción | Breve descripción del propósito de la comunicación | No |
   | Plantilla | Seleccione una plantilla preconfigurada o comience desde cero | Sí |
   | Etiquetas | Añadir etiquetas de metadatos para una mejor organización | No |

1. Vaya a la pestaña &quot;Ajustes preestablecidos&quot; y configure las siguientes opciones:

   | Campo | Descripción |
   |-------|-------------|
   | Lista preestablecida | Seleccione un ajuste preestablecido para el tamaño del documento. Las opciones comunes incluyen A4, Carta y más. |
   | Anchura preestablecida | Muestra la anchura del ajuste preestablecido para la lista de ajustes preestablecidos seleccionada. |
   | Altura preestablecida | Muestra la altura del ajuste preestablecido para la lista de ajustes preestablecidos seleccionados. |
   | Unidad preestablecida | Seleccione la unidad de medida de las dimensiones del documento (por ejemplo, milímetros, pulgadas). |
   | Orientación preestablecida | Elija la orientación del documento: Vertical u Horizontal. |

1. Haga clic en **Crear**. La comunicación se abre en el editor.
1. Arrastre y suelte los componentes y fragmentos para diseñar la comunicación interactiva.

   * Use **Página maestra** para el contenido común en todas las páginas. Las páginas maestras están diseñadas para dar formato a las páginas y ayudan a facilitar la coherencia del diseño, ya que pueden proporcionar un fondo y un formato de diseño para más de una página en un diseño de documento.

   * Use **Páginas** para diseñar el contenido y el diseño del documento. Cada página deriva su tamaño y orientación de una página maestra y, de forma predeterminada, cada página está asociada a la página maestra predeterminada que crea Designer.


1. Use la notación `@` para completar automáticamente los campos de datos basados en el modelo de datos conectado.
1. Utilice la opción `PDF Preview` para obtener una vista previa del documento junto con los datos. Necesita el archivo de datos en formato JSON.
