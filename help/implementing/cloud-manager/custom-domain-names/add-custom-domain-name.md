---
title: Añadir un nombre de dominio personalizado
description: Añadir un nombre de dominio personalizado
translation-type: tm+mt
source-git-commit: b6b1ef8f97413dc8bf9b1fa7f355a02bdaeebfd8
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Añadir un nombre de dominio personalizado {#adding-cdn}

Un usuario debe ser propietario de una empresa o administrador de implementación para poder agregar un nombre de dominio personalizado en Cloud Manager.

>[!NOTE]
>Antes de agregar un nombre de dominio personalizado, se debe instalar en el Programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte Instalación de un certificado SSL (INSERT LINK) para obtener más información.

Solo se puede agregar un nombre de dominio a la vez. Sin embargo, los usuarios pueden añadir caracteres comodín, por ejemplo, `*.wknd.com` como nombre de dominio, lo que permitiría alojar varios subdominios con un único registro TXT.
Cada Entorno de Cloud Manager puede alojar hasta un máximo de 50 dominios personalizados por entorno.
El mismo nombre de dominio no se puede usar en más de un entorno.

## Añadir un nombre de dominio personalizado desde la página Configuración de dominio {#adding-cdn-settings}

Siga los pasos a continuación para agregar un nombre de dominio personalizado desde la página Configuración de dominio:

1. En la página Entornos, vaya a la página Configuración de dominio.

1. Seleccionar Añadir nombre de dominio personalizadoSe iniciará el asistente para agregar nombre de dominio personalizado INSERTAR IMAGEN

1. Escriba el nombre de dominio personalizado. Nota: No incluya &#39;http://&#39;, &#39;https://&#39; o espacios al introducir en el dominio.

1. Seleccione el Entorno cuyo servicio de publicación se asociará al nombre de dominio.

1. Seleccione el certificado SSL en la lista desplegable y seleccione Continuar.

1. Esto lo llevará a la pantalla Verificación del nombre de dominio para su Entorno. Añada el registro TXT para obtener más información. INSERTAR IMAGEN

Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno:

1. Seleccione Continuar.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica con el estado &quot;Verificado e implementado&quot;.  INSERTAR IMAGEN
1. Vaya a Comprobación del estado del nombre de dominio personalizado INSERT LINK para obtener más información sobre los distintos estados y la dirección.

>[!NOTE]
>La prueba de DNS puede tardar hasta unas horas en reconocerse debido a retrasos en la propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado, que se puede ver en la tabla de configuración de dominio. Vaya a Comprobación del estado del nombre de dominio INSERT LINK para obtener más información.

## Añadir un nombre de dominio personalizado de la página Entornos {#adding-cdn-environments}

1. Vaya a la página Detalle de Entorno para ver el entorno de intereses.
1. Utilice los campos de entrada en la parte superior de la tabla Nombres de dominio para enviar el nombre de dominio personalizado, certificado SSL. A continuación, seleccione Añadir.
1. Se iniciará el asistente para Añadir el nombre de dominio personalizado con el nombre de Entorno previamente rellenado.
1. Escriba el nombre de dominio personalizado. Nota: No incluya `http://`ni `https://`espacios al introducir en el dominio. Seleccione Continuar.
1. Esto lo llevará a la pantalla Verificación del nombre de dominio para su Entorno. Vaya a Verificación de dominio (Añadir registro TXT) para obtener más información. INSERTAR IMAGEN

Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno:

1. Seleccione Continuar.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica con el estado &quot;Verificado e implementado&quot;.

En este punto, el nombre de dominio personalizado está listo para la prueba y `CNAME` para señalarlo. Vaya a Estado del nombre de dominio para obtener más información sobre los distintos estados y la dirección.

>[!NOTE]
>La prueba de DNS puede tardar hasta unas horas en reconocerse debido a retrasos en la propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado, que se puede ver en la tabla de configuración de dominio. Vaya a Comprobación del estado del nombre de dominio INSERT LINK para obtener más información.
