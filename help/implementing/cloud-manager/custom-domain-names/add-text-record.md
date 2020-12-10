---
title: Añadir un registro TXT
description: Añadir un nombre de dominio personalizado
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Añadir un registro TXT {#adding-txt}

Un registro TXT DNS autoriza a un dominio a alojarse en un servicio CDN. El cliente debe crear un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo el control del cliente y autoriza a Cloud Manager a ofrecer contenido desde el servicio a un dominio. Dicha autorización podrá concederse y retirarse.

Debe seguir los pasos a continuación antes de crear un registro TXT:

* Tener la capacidad de modificar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Identifique su host de dominio o registrador si aún no lo conoce.

Al iniciar la verificación de dominio, Cloud Manager le proporciona el nombre y el valor TXT que se utilizarán para la verificación. Añada un registro TXT en el servidor DNS de su dominio mediante el nombre y el valor especificados.

1. Inicie sesión en el host de dominio y visite la sección de registros DNS.
1. Añada `_aemverification.[yourdomainname]` como Nombre y agregue el valor TXT tal como aparece.
Consulte los ejemplos de la tabla siguiente.

| Dominio | Nombre | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Se muestra en la interfaz de usuario de Cloud Manager y es específica para el dominio y el entorno de Cloud Manager |
| `test.example.com` | `_aemverification.test.example.com` | Se muestra en la interfaz de usuario de Cloud Manager y es específica para el dominio y el entorno de Cloud Manager |

Cuando haya terminado, puede comprobar el resultado ejecutando: `dig _aemverification.[yourdomainname] -t txt`.
El resultado esperado debería mostrar el valor TXT proporcionado en la interfaz de usuario del Administrador de nube.

Por ejemplo, si el dominio es `example.com`, ejecute: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>También existen varias [herramientas de búsqueda DNS](https://www.ultratools.com/tools/dnsLookup); Google DoH puede utilizarse para buscar entradas de registros TXT e identificar si falta el registro TXT o si es erróneo.

