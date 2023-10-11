---
title: ¿Cómo se agrega texto de marcador de posición a los campos de formulario?
description: El texto de marcador de posición está diseñado para ayudar al usuario con la introducción de datos cuando el control no tiene valor. Puede ser un valor de muestra o una breve descripción del formato esperado.
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 96%

---


# Texto de marcador de posición de [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

El texto de marcador de posición representa una palabra o una frase corta. Está diseñado para ayudar al usuario a introducir los datos cuando el control no tiene valor. Un texto de marcador de posición puede ser un valor de muestra o una breve descripción del formato esperado. El texto de marcador de posición se muestra antes de que el usuario introduzca un valor, y se quita cuando el usuario introduce o selecciona un valor.

>[!NOTE]
>
>Si se especifica, el texto del marcador de posición debe tener un valor que no contenga caracteres de nueva línea.

![Componente de fecha con y sin texto de marcador de posición](assets/dat-picker-place-holder-text.png)

**A.** Componente de fecha con texto de marcador de posición **B.** Componente de fecha sin texto de marcador de posición

[!DNL AEM Forms] admite texto de marcador de posición en los campos Cuadro de contraseña, Selector de fecha, Cuadro numérico y Cuadro de texto.\
Los textos de los marcadores de posición no son compatibles con el widget de fecha HTML5 nativo. Para especificar un texto de marcador de posición:

1. Haga clic con el botón derecho en un componente que admita texto de marcador de posición y haga clic en **Editar**. Aparecerá el cuadro de diálogo Editar componente.

1. Abra la pestaña **Título y texto**.
1. Especifique una palabra o una frase corta en el **Cuadro de texto de marcador de posición**. Haga clic en **Aceptar**.

>[!NOTE]
>
>El texto de marcador de posición no es compatible con [!DNL Microsoft Internet Explorer 9].

