---
title: Bloqueo de plantilla en el Editor de comunicaciones interactivas
description: Bloqueo de plantilla en el Editor de comunicaciones interactivas permite a los autores de plantillas bloquear el diseño o el contenido para los autores de documentos.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 957944da363b506c34c2630aeedbe984442f34b8
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 10%

---


# Bloqueo de plantilla en el Editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

La función Bloqueo de plantilla del Editor de comunicaciones interactivas (IC) permite a los autores de plantillas restringir las modificaciones a elementos específicos de una plantilla de comunicación. Esto garantiza la coherencia del diseño, protege el contenido esencial e impone la gobernanza en todos los equipos que reutilizan plantillas para crear comunicaciones personalizadas.

Cuando se aplican, los componentes bloqueados aparecen visualmente distintos y los autores o colaboradores que siguen el flujo no pueden modificarlos, según el tipo de bloqueo configurado. Esta función ayuda a mantener los estándares de marca, la integridad de los datos y la uniformidad del diseño en todas las comunicaciones derivadas.

![Buscar documento CI](/help/forms/interactive-communication/assets/template-lock.png)

## &#x200B;2. Tipos de bloqueo

Los autores de plantillas pueden aplicar bloques de contenido y diseño, de forma individual o conjunta, para controlar los cambios de contenido y diseño en las plantillas de comunicaciones interactivas:

### 2.1 Bloqueo de contenido

Un Bloqueo de contenido restringe cualquier modificación del contenido o las propiedades del elemento seleccionado. Este tipo de bloqueo garantiza que los datos, el texto o las propiedades de diseño esenciales permanezcan sin cambios, incluso cuando se reutilizan en varias comunicaciones.

Cuando se aplica, los autores no pueden modificar:

- Contenido de texto o subtítulos

- Configuración de aspecto (fuente, color, fondo, bordes, etc.)

- Configuraciones de enlace de datos

- Elementos constitutivos dentro de un componente contenedor (como subformularios)

### 2.2 Bloqueo de diseño

Un Bloqueo de diseño restringe los cambios relacionados con la posición y el tamaño de un elemento. Esto garantiza que la alineación visual y la jerarquía de diseño sigan siendo coherentes con los estándares de marca o documento.

Cuando se aplica, los autores no pueden:

- Mover el elemento a una nueva posición en la página

- Cambiar el tamaño del ancho o alto del elemento

## &#x200B;3. Cómo utilizar el bloqueo de plantilla en el editor de comunicaciones interactivas

Siga los siguientes pasos para aplicar bloqueos de contenido o diseño en la plantilla de comunicación interactiva (CI):

1. Abra La Plantilla
Abra o cree una plantilla, siga la guía [Crear una plantilla de comunicación interactiva](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/interactive-communication/overview/create-interactive-communication-template)

1. Seleccione el componente
Haga clic en el componente (cuadro de texto, imagen o subformulario) que desee restringir.

1. Opciones de bloqueo de acceso
En el panel Propiedades, vaya a la sección Bloqueo.

1. Aplicar bloqueos

   1. Bloqueo de contenido: evita las ediciones de texto, estilo y datos.

   1. Bloqueo de diseño: Restringe el movimiento y el cambio de tamaño.

   1. Puede habilitar ambas opciones para obtener una protección total.

1. Guardar y verificar
Guarde la plantilla y cree un nuevo IC basado en ella para confirmar que los elementos bloqueados no se pueden modificar.

## &#x200B;4. Prácticas recomendadas

- **Bloquear componentes esenciales de forma anticipada:** aplique bloqueos a encabezados, pies de página, exenciones de responsabilidad legal y logotipos para preservar el cumplimiento y la identidad de la marca.

- **Use bloqueos de contenido para obtener precisión:** Proteja los campos enlazados a modelos de datos principales o a texto normativo.

- **Use bloqueos de diseño para mantener la coherencia:** Evite la falta de alineación o la distorsión visual en las plantillas que se reutilizan con frecuencia.

- **Comunicar el uso del bloqueo:** Asegúrese de que los usuarios intermedios sepan qué secciones están restringidas intencionalmente para evitar confusiones.
