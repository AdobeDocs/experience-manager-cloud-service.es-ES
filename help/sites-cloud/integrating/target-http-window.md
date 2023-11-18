---
title: Ventana HTTP de Adobe AEM Target
description: Ventana HTTP de Adobe AEM Target
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 89%

---


# Introducción {#introduction}

Esta página describe los parámetros configurables presentes en la ventana HTTP de Adobe AEM Target.

## Parámetros {#parameters}

![Ventana HTTP de Target](assets/httpwindow.png "Ventana HTTP de Target")

La ventana contiene los siguientes parámetros configurables:

| Parámetro | Descripción |
|---|---|
| URL de la API de Adobe Target | La URL de la API de Adobe Target. |
| Habilitación de la URL absoluta | Determina si se utiliza la parte host de la URL o la URL completa. Active la casilla de verificación si desea utilizar la URL completa (sin abreviar). De forma predeterminada, la casilla de verificación está desactivada. |
| Tiempo de espera de conexión | El tiempo de espera (en milisegundos) hasta que se establece una conexión. El valor predeterminado es de 60 000 milisegundos. Un valor de cero se interpreta como un tiempo de espera infinito. |
| Tiempo de espera de socket | El tiempo de espera (en milisegundos) para esperar datos o un período máximo de inactividad entre dos paquetes de datos consecutivos. El valor predeterminado es 30 000 milisegundos. |
| Token de regex de reemplazo de URL de Adobe Target Recommendations | Controla el token en la dirección URL del extremo de Adobe Target que debe reemplazarse para que apunte a la dirección URL de la API de Target Recommendations. |
| Reemplazo de URL de Adobe Target Recommendations con token | Reemplaza la regex descrita en el parámetro anterior, por lo que la URL resultante apuntará a la API de Target Recommendations. |
