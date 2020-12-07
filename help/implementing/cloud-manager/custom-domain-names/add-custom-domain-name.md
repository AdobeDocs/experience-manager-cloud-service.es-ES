---
title: Añadir un nombre de dominio personalizado
description: Añadir un nombre de dominio personalizado
translation-type: tm+mt
source-git-commit: 6571c11cedbc0d81fbdfd8072a39b1327bdba10b
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Añadir un nombre de dominio personalizado {#adding-cdn}

Un usuario debe ser propietario de una empresa o administrador de implementación para poder agregar un nombre de dominio personalizado en Cloud Manager.

>[!NOTE]
>Antes de agregar un nombre de dominio personalizado, se debe instalar en el Programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte Instalación de un certificado SSL para obtener más información.

Solo se puede agregar un nombre de dominio a la vez. Sin embargo, los usuarios pueden agregar caracteres comodín, por ejemplo, `*.wknd.com` como nombre de dominio, lo que permitiría que varios subdominios se alojaran con un único registro TXT.
Cada Entorno de Cloud Manager puede alojar hasta un máximo de 50 dominios personalizados por entorno.
El mismo nombre de dominio no se puede usar en más de un entorno.

## Añadir un nombre de dominio personalizado de la página Configuración de dominio {#adding-cdn-settings}

Siga los pasos a continuación para agregar un nombre de dominio personalizado desde la página Configuración de dominio:

1. Vaya a la página Configuración de dominio desde la **Página Entornos**

1. Seleccione **Añadir nombre de dominio personalizado** para iniciar el asistente para agregar nombre de dominio personalizado.

1. Escriba el nombre de dominio personalizado.

   >[!NOTE]
   >No debe incluir `http://`, `https://` ni espacios al ingresar en el dominio.

1. Seleccione el Entorno cuyo servicio de publicación se asociará al nombre de dominio.

1. Seleccione el certificado SSL en la lista desplegable y seleccione Continuar.

1. Esto lo llevará a la pantalla Verificación del nombre de dominio para su Entorno. Consulte Añadir un registro TXT para obtener más información.

   >[!NOTE]
   >Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno.

1. Seleccione Continuar.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.
1. Vaya a Comprobación del estado del nombre de dominio personalizado para obtener más información sobre los distintos estados y la dirección.

   >[!NOTE]
   >La prueba de DNS puede tardar hasta unas horas en reconocerse debido a retrasos en la propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado, que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más detalles.

## Añadir un nombre de dominio personalizado de la página Entornos {#adding-cdn-environments}

1. Vaya a la página Detalle de Entorno para ver el entorno de intereses.
1. Utilice los campos de entrada en la parte superior de la tabla Nombres de dominio para enviar el nombre de dominio personalizado, certificado SSL. A continuación, seleccione Añadir.
1. Se iniciará el asistente para Añadir el nombre de dominio personalizado con el nombre de Entorno previamente rellenado.
1. Escriba el nombre de dominio personalizado. Nota: No incluya `http://`, `https://` ni espacios al ingresar en el dominio. Seleccione Continuar.
1. Esto lo llevará a la pantalla Verificación del nombre de dominio para su Entorno. Consulte Verificación de dominio (Añadir registro TXT) para obtener más información.

   >[!NOTE]
   >Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno.

1. Seleccione Continuar.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.

En este punto, el nombre de dominio personalizado está listo para la prueba y `CNAME` para señalarlo. Consulte Estado del nombre de dominio para obtener más información sobre los distintos estados y la dirección.

>[!NOTE]
>La prueba de DNS puede tardar hasta unas horas en reconocerse debido a retrasos en la propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado, que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más información.
