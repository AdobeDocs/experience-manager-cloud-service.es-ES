---
title: Adobe AEM ventana HTTP de Target
description: 'Adobe AEM ventana HTTP de Target '
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# Introducción {#introduction}

Esta página describe los parámetros configurables presentes en la ventana HTTP de Adobe AEM Target.

## Parámetros {#parameters}

![Ventana HTTP de Target](assets/httpwindow.png "Ventana HTTP de Target")

La ventana contiene los siguientes parámetros configurables:

| Parámetro | Descripción |
|---|---|
| URL de la API de Adobe Target | La URL de la API de Adobe Target. |
| Habilitar dirección URL absoluta | Determina si se utiliza la parte host de la dirección URL o la dirección URL completa. Active la casilla de verificación si desea utilizar la URL completa (sin abreviar). De forma predeterminada, la casilla de verificación está desactivada. |
| Tiempo de espera de conexión | Tiempo de espera (en milisegundos) hasta que se establezca una conexión. El valor predeterminado es 60 000 milisegundos. Un valor de 0 se interpreta como un tiempo de espera infinito. |
| Tiempo de espera de socket | Tiempo de espera (en milisegundos) para esperar datos o un período máximo de inactividad entre dos paquetes de datos consecutivos. El valor predeterminado es 30 000 milisegundos. |
| Token de regex de reemplazo de URL de Adobe Target Recommendations | Controla el token en la dirección URL de extremo de Adobe Target que debe reemplazarse para que apunte a la dirección URL de la API de Recomendaciones de Target. |
| Sustitución de URL de Adobe Target Recommendations con token | Reemplace la regex descrita en el parámetro anterior, por lo que la URL resultante apuntará a la API de Recomendaciones de Target. |
