---
title: 'Texto del marcador de posición en [!DNL AEM Forms] '
description: El texto del marcador de posición está diseñado para ayudar al usuario con la introducción de datos cuando el control no tiene valor. Podría ser un valor de muestra o una breve descripción del formato esperado.
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Texto del marcador de posición en [!DNL AEM Forms] {#placeholder-text-in-aem-forms}

El texto del marcador de posición representa una palabra o una frase corta. Su objetivo es ayudar al usuario a introducir los datos cuando el control no tiene valor. Un texto de marcador de posición podría ser un valor de muestra o una breve descripción del formato esperado. El texto del marcador de posición se muestra antes de que el usuario introduzca un valor; se elimina cuando el usuario introduce o selecciona un valor.

>[!NOTE]
>
>Si se especifica, el texto del marcador de posición debe tener un valor que no contenga caracteres de línea nuevos.

![Componente de fecha con y sin texto de marcador de posición](assets/dat-picker-place-holder-text.png)

**A.** Componente de fecha con texto de marcador de posición **B.** Componente de fecha sin texto de marcador de posición

[!DNL AEM Forms] admiten el texto de marcador de posición para los campos Cuadro de contraseña, Selector de fecha, Cuadro numérico y Cuadro de texto.\
Los textos de los marcadores de posición no son compatibles con el widget de fecha HTML5 nativo. Para especificar un texto de marcador de posición:

1. Haga clic con el botón derecho en un componente que admita Texto de marcador de posición y haga clic en **Editar**. Aparecerá el cuadro de diálogo Editar componente.

1. Abra el **Título y texto** pestaña .
1. Especifique una palabra o una frase corta en la variable **Cuadro de texto Marcador de posición**. Haga clic en **Aceptar**.

>[!NOTE]
>
>El texto del marcador de posición no es compatible con [!DNL Microsoft Internet Explorer 9].

