---
title: Copiar y pegar en el editor de comunicaciones interactivas
description: Copiar y pegar en el editor de comunicaciones interactivas en AEM Forms permite a los autores duplicar una comunicación interactiva existente y reutilizarla en una carpeta o ubicación diferente.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: fe99fc4ddc1e2b3bdd1b2a5b583f2b4cb681dee9
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 12%

---


# Copiar y pegar en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

La función Copiar y pegar del editor de comunicaciones interactivas (CI) permite a los autores duplicar una comunicación interactiva existente y reutilizarla en una carpeta o ubicación diferente. Esta capacidad ayuda a los equipos a trabajar de forma eficaz al habilitar varias variaciones de una CI sin modificar la versión original.

Al crear una copia, los autores pueden realizar cambios de forma segura en diferentes casos de uso, clientes o escenarios empresariales, conservando al mismo tiempo la comunicación interactiva de origen.

## Qué se copia

Al copiar una comunicación interactiva, los siguientes elementos se duplican en la nueva CI:

- Diseño y estructura

- Componentes y fragmentos

- Enlaces de datos y reglas

- Configuraciones de estilo y marca

- A continuación, puede modificar cualquiera de estos elementos de forma independiente en la CI copiada.

## Copiar una comunicación interactiva

![Buscar documento CI](/help/forms/interactive-communication/assets/copy-in-ic.png)

Siga estos pasos para copiar una comunicación interactiva:

- Vaya a Forms y documentos en la interfaz de AEM.

- Busque la comunicación interactiva que desea copiar.

- Seleccione el IC.

- En la barra de herramientas o en el menú contextual, seleccione Copiar.

- Vaya a la carpeta o ubicación de destino.

- Seleccione Pegar para crear un duplicado de la comunicación interactiva.

- Se crea un nuevo IC con la misma configuración que el original.

## Editar y reutilizar la comunicación interactiva copiada

![Buscar documento CI](/help/forms/interactive-communication/assets/paste-in-ic.png)

Después de pegar la comunicación interactiva:

- Abra la CI copiada en el editor de comunicaciones interactivas.

- Actualice el contenido, las reglas, las asignaciones de datos o el diseño según sea necesario.

- Guarde y publique el IC cuando esté listo.

- Los cambios realizados en la CI copiada no afectan a la comunicación interactiva original.

## Prácticas recomendadas

- Mantener la CI original como una línea de base o versión maestra.

- Cambie el nombre de las CI copiadas para reflejar claramente su propósito o variación.

- Utilice copiar y pegar en combinación con versiones y comentarios para mejorar la trazabilidad.

- Revise los enlaces de datos y los canales de salida después de la copia para garantizar su corrección.

La función Copiar y pegar de la comunicación interactiva simplifica la reutilización y la personalización al permitir a los autores duplicar los IC existentes y modificarlos de forma independiente. Permite un desarrollo más rápido, una experimentación más segura y una entrega de comunicaciones coherentes, sin arriesgarse a realizar cambios en la comunicación interactiva original.

