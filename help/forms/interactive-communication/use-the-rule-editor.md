---
title: Crear reglas en el editor de comunicaciones interactivas
description: La creación de reglas en el Editor de comunicaciones interactivas permite a los autores definir comportamientos dinámicos que hacen que las comunicaciones sean interactivas e inteligentes.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: b2b85d1e802c7f287b875d53a9347ca07ea2b806
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 10%

---


# Editor de reglas en el editor de comunicaciones interactivas


>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.


>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.


## &#x200B;1. Introducción


El Editor de reglas del Editor de comunicaciones interactivas permite a los autores definir comportamientos dinámicos que hacen que las comunicaciones sean interactivas e inteligentes. Las reglas controlan cómo se comportan, muestran o calculan los campos en función de las acciones del usuario o los datos subyacentes, lo que garantiza que cada comunicación esté personalizada y tenga en cuenta el contexto.


Desde configuraciones sencillas de visibilidad hasta lógicas condicionales complejas, las reglas permiten a los autores ofrecer experiencias que se adaptan en tiempo real, lo que mejora la facilidad de uso, la precisión y la participación.


![Buscar documento CI](/help/forms/interactive-communication/assets/rule-creation.png)


## &#x200B;2. Propiedades


2.1 Configuración de propiedades y comportamientos de los campos


- **Tipos de entrada:** Defina el tipo de datos que acepta un campo, como texto, números, fechas o valores booleanos, lo que garantiza la validación y el formato adecuados.


- **Reglas de visibilidad:** controla si un campo es visible, está oculto o se muestra dinámicamente en función de condiciones (por ejemplo, &quot;Mostrar campo de descuento solo si se aplica código de promoción&quot;).


- **Valores predeterminados:** predefine valores en campos (por ejemplo, la fecha de hoy, el nombre del cliente del modelo de datos) para ahorrar tiempo y mejorar la precisión.


2.2 Implementar cálculos, validaciones y lógica de regla


- **Lógica de campo:** Automatice los cálculos y las relaciones de campo, como el cálculo de importes de factura o el rellenado automático de campos dependientes.


- **Reglas personalizadas:** Cree lógica avanzada usando el Editor de reglas para escenarios complejos como comprobaciones de elegibilidad o precios basados en niveles.


- **Acciones condicionales:** Defina déclencheur que respondan a los valores de datos o a los datos introducidos por el usuario, como habilitar o deshabilitar campos, mostrar mensajes o bifurcar a secciones diferentes.


![Buscar documento CI](/help/forms/interactive-communication/assets/rule-creation1.png)


## &#x200B;3. Uso


El editor de reglas se utiliza ampliamente para garantizar que los formularios y las comunicaciones sean adaptables y estén basados en el contexto:


- **Visualización dinámica:** ocultar o mostrar secciones basadas en el tipo de cliente o en las opciones seleccionadas.


- **Validación:** Evite errores comprobando formatos, intervalos o entradas obligatorias.


- **Cálculos automáticos:** Simplifique las tareas de usuario con fórmulas (por ejemplo, impuestos, totales o descuentos).


- **Control de flujo de trabajo:** Habilite botones, campos o acciones específicos solo cuando se cumplan los requisitos previos.


- **Personalization:** Adapte la comunicación al perfil, las preferencias o los criterios de idoneidad del destinatario.


## &#x200B;4. Prácticas recomendadas


- **Mantenga las reglas simples:** Divida la lógica compleja en reglas modulares más pequeñas para facilitar el mantenimiento.


- **Priorizar la lógica de visibilidad:** Oculte los campos innecesarios antes de tiempo para optimizar la experiencia del usuario.


- **Realizar pruebas exhaustivas:** previsualizar reglas con varios conjuntos de datos para confirmar la precisión y evitar conflictos.


- **Use correctamente los valores predeterminados:** Rellene previamente campos que cambian con poca frecuencia, pero que permiten flexibilidad para las ediciones.


- **Aproveche las acciones condicionales:** Aplíquelas para mejorar la interactividad, pero evite abrumar a los usuarios.


- **Reglas de documento:** Mantenga un registro de lógica empresarial para garantizar la claridad de los desarrolladores y las partes interesadas.


Al configurar las reglas con cuidado, los autores pueden crear comunicaciones que respondan de forma inteligente a los datos y a las acciones del usuario, lo que optimiza los procesos, reduce los errores y ofrece una experiencia personalizada y sin problemas.



