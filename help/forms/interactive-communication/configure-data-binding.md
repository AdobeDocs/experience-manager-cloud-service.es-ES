---
title: Crear un fragmento de comunicación interactiva
description: Cree fragmentos de comunicación interactiva en AEM Forms para crear bloques de contenido modulares y reutilizables que garanticen la coherencia, ahorren tiempo y admitan comunicaciones personalizadas basadas en datos.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: 19270498fa60f860b31400ad40705ecd2f821cf8
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 10%

---


# Enlace de datos en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

El enlace de datos en el editor de comunicaciones interactivas conecta los campos en lienzo con una capa de datos controlada, de modo que las comunicaciones se representen con información real y contextual. Al vincular componentes a un modelo de datos de formulario (FDM), los autores pueden garantizar la precisión, reducir el trabajo manual y ofrecer experiencias dinámicas y personalizadas.

Más allá de simplemente conectar valores, el enlace de datos en IC admite la asignación visual, el relleno previo y la sincronización, lo que permite a los autores diseñar más rápido y mantenerse alineados con los sistemas back-end y los modelos de datos.

![Buscar documento CI](/help/forms/interactive-communication/assets/data-binding1.png)

## &#x200B;2. Propiedades

2.1 Administración de conexiones de datos (FDM)

- **Seleccione el FDM:** Elija el modelo de datos de formulario adecuado (por ejemplo, clientes, cuentas o directivas). Esto establece el esquema autoritativo para campos, matrices y objetos utilizados en la comunicación.

- **Crear enlace de datos:** Una vez habilitados los enlaces, cada campo se puede asociar con rutas FDM, minimizando los errores y asegurando una integración coherente.

- **Campos de enlace al modelo de datos:** Asigne campos a nodos específicos (por ejemplo, customer.name, policy.holder.id) para impulsar la representación con datos activos y para admitir validaciones o lógica condicional.

2.2 Creación de enlaces de datos

- **Asignación visual:** La asignación de arrastrar y soltar entre campos y nodos de FDM ayuda a los usuarios no técnicos a evitar errores.

- **Asociación de campos:** Defina la ruta de destino, el tipo de datos (texto, número, fecha, booleano, imagen) y los formateadores opcionales (por ejemplo, máscara de fecha, moneda).

- **Vista previa de enlace:** probar enlaces con conjuntos de datos de ejemplo para validar el formato y la corrección antes de publicar.

## &#x200B;3. Uso

El enlace de datos se utiliza comúnmente cuando las comunicaciones deben mostrar registros autorizados o capturar entradas del usuario. Algunos ejemplos son:

- **Personalization:** Rellene detalles del cliente como el nombre, la dirección o el saldo de la cuenta.

- **Contenido condicional:** mostrar u ocultar secciones basadas en valores de modelo (por ejemplo, clientes activos o inactivos).

- **Colecciones y tablas:** Procesar historiales, transacciones o listas desglosadas de matrices.

- **Imágenes y medios:** vincule fotos de perfil, logotipos de compañía o imágenes de productos.

- **Revisar y firmar electrónicamente:** Rellenar previamente formularios con datos y permitir actualizaciones mediante sincronización bidireccional.

Los autores suelen seleccionar el FDM al principio del proyecto, asignar visualmente los campos durante el diseño y probar con los datos de ejemplo antes de la publicación.

## &#x200B;4. Prácticas recomendadas

- **Defina el esquema antes:** Finalice el FDM antes del enlace para evitar la reasignación más adelante.

- **Usar asignación visual:** Evite errores tipográficos y rutas de acceso no coincidentes mediante la función de arrastrar y soltar.

- **Validar tipos de datos:** Aplicar formateadores para moneda, fechas o números de teléfono para garantizar la coherencia.

- **Mantenga los enlaces explícitos:** Cada campo debe asignarse claramente a un solo nodo de datos.

- **Prueba con datos de ejemplo:** Vista previa de casos comunes y extremos (por ejemplo, valores vacíos, matrices largas).

- **Limitar sincronización bidireccional:** Úselo solamente cuando se requieran ediciones o aprobaciones.

- **Modularizar colecciones:** Utilice filas de plantilla para estructuras repetibles.

- **Proteger datos confidenciales:** Aplicar enmascaramiento, cifrado y acceso con menos privilegios para PII o detalles de pago.

Al configurar el enlace de datos con cuidado, los autores crean un puente fiable entre el diseño y los datos, lo que acelera la creación de comunicaciones, garantiza la precisión y ofrece experiencias altamente personalizadas a escala.

