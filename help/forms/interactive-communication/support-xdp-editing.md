---
title: Compatibilidad con la edición XDP en el editor de comunicaciones interactivas
description: La compatibilidad con la edición XDP en el Editor de comunicaciones interactivas permite editar los xdp existentes dentro del Editor de comunicaciones interactivas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 9adc7a5669d8bf1e64cc93998cb2f91ffa9d3dd6
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 13%

---


# Compatibilidad con la edición XDP en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## Introducción

El editor de comunicaciones interactivas (CI) ahora ofrece compatibilidad perfecta de **para editar archivos XDP (Paquete de datos XML)** en el entorno de creación. Esta mejora permite a los autores administrar, modificar y mantener las plantillas XDP sin esfuerzo, sin depender de herramientas externas. Con esta capacidad, los usuarios pueden cargar, ver y editar archivos XDP directamente en el editor de CI, lo que permite un flujo de trabajo de diseño a envío unificado y eficaz.

## Cómo utilizar la edición XDP de soporte en el editor de comunicaciones interactivas

![Buscar documento CI](/help/forms/interactive-communication/assets/support-xdp.png)

1. Vaya a **Forms > Forms y documentos**.

1. Cargue su archivo .xdp utilizando la opción **Crear > Cargar archivo**.

1. Abra el XDP en **Editor de comunicaciones interactivas**.

1. Realice los cambios necesarios de **diseño o enlace de datos**.

1. Guarde los cambios y las actualizaciones se reflejarán automáticamente en el archivo XDP de origen.

## Capacidades clave

- **Cargar y administrar archivos XDP:**
Cargar plantillas XDP mediante **Forms Manager**. Una vez cargados, estarán disponibles para su edición directa en el Editor de comunicaciones interactivas.

- **Editar mediante el editor de CI:**
Abra y edite XDP con el IC Editor, con acceso completo a las funciones de edición existentes, incluidos los ajustes de diseño, el enlace de datos, el estilo y la configuración de componentes.

- **Volver a guardar en Source:**
Cualquier modificación realizada mediante el Editor IC se guarda directamente en el archivo XDP original, manteniendo la integridad de la versión y simplificando el flujo de trabajo de diseño.

## Compatibilidad con fragmentos

- **Referencias de fragmento:**
Si un XDP hace referencia a un fragmento, ese fragmento debe existir en **AEM en la misma ruta relativa** tal como se define en el archivo XDP.
Si falta un fragmento, el editor muestra un **mensaje de advertencia** que indica que el fragmento requerido no está presente.

- **Reutilización de fragmentos en el editor:**
Todos los fragmentos XDP existentes aparecen en el **panel Fragmentos** del editor de CI.
Los autores pueden **arrastrar y soltar** estos fragmentos directamente en el lienzo. Las referencias se conservan, lo que garantiza que las actualizaciones de los fragmentos se propaguen en todos los XDP que las utilizan.

## Ventajas

- Elimina la dependencia de las herramientas externas para la modificación XDP.

- Conserva los enlaces de datos y las relaciones de fragmento existentes.

- Permite un diseño coherente y ciclos de iteración más rápidos.

## Prácticas recomendadas

- Asegúrese de que todos los fragmentos a los que se hace referencia existan en la ruta relativa correcta antes de editar.

- Utilice el control de versiones para administrar las actualizaciones entre XDP y dependencias de fragmento.

- Valide los enlaces de datos posteriores a la edición para confirmar que se representan correctamente.

