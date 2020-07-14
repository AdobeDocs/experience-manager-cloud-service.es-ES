---
title: Ventana HTTP de Adobe AEM Destinatario
description: 'Ventana HTTP de Adobe AEM Destinatario '
translation-type: tm+mt
source-git-commit: c193b38718622cd2e960a8e8833c2d295822dc33
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 4%

---


# Introducción {#introduction}

En esta página se describen los parámetros configurables presentes en la ventana HTTP de Adobe AEM Destinatario.

## Parámetros {#parameters}

![Ventana HTTP de Destinatario](assets/httpwindow.png "Ventana HTTP de Target")

La ventana contiene los siguientes parámetros configurables:

| Parámetro | Descripción |
|---|---|
| URL de API de Adobe Target | Dirección URL de la API de Adobe Target. |
| Habilitar dirección URL absoluta | Determina si se utiliza la parte host de la dirección URL o la dirección URL completa. Active la casilla de verificación si desea utilizar la dirección URL completa (sin abreviar). De forma predeterminada, la casilla de verificación está desactivada. |
| Tiempo de espera de conexión | Tiempo de espera (en milisegundos) hasta que se establece una conexión. El valor predeterminado es 60000 milisegundos. Un valor de 0 se interpreta como un tiempo de espera infinito. |
| Tiempo de espera de socket | Tiempo de espera (en milisegundos) para esperar los datos o un período máximo de inactividad entre dos paquetes de datos consecutivos. El valor predeterminado es 30000 milisegundos. |
| URL de Recomendaciones de Adobe Target Reemplazar token de regex | Controla el token en la dirección URL del extremo de Adobe Target que debe reemplazarse para que señale a la dirección URL de la API de Recomendaciones de Destinatario. |
| Sustitución de URL de Recomendaciones de Adobe Target por token | Sustitución del regex descrito en el parámetro anterior, de modo que la dirección URL resultante señalará a la API de Recomendaciones de Destinatario. |
