---
title: Adición de un registro TXT
description: Adición de un nombre de dominio personalizado
exl-id: d441de29-af41-4d3e-9155-531af9702841
translation-type: tm+mt
source-git-commit: 4903f97c1bf0e7c8e96d604feb005d9611a7d9bb
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Adición de un registro TXT {#adding-txt}

Un registro TXT DNS autoriza a un dominio a alojarse en un servicio CDN. El cliente debe crear un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo el control del cliente y autoriza a Cloud Manager a proporcionar contenido desde el servicio a un dominio. Dicha autorización podrá concederse y retirarse.

Debe seguir los pasos a continuación antes de crear un registro TXT:

* Tenga la capacidad de modificar los registros DNS del dominio de su organización o póngase en contacto con la persona adecuada que pueda.
* Identifique su host de dominio o registrador si todavía no lo conoce.

Al iniciar la verificación del dominio, Cloud Manager le da el nombre y el valor TXT que debe utilizar para la verificación. Agregue un registro TXT al servidor DNS de su dominio con el nombre y valor especificados.

1. Inicie sesión en el host de dominio y visite la sección de registros DNS .
1. Agregue `_aemverification.[yourdomainname]` como Nombre y añada el valor TXT exactamente como aparece.
Consulte los ejemplos de la tabla siguiente.

| Dominio | Nombre | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification` | Se muestra en la interfaz de usuario de Cloud Manager y es específico del dominio y del entorno de Cloud Manager |
| `test.example.com` | `_aemverification` | Se muestra en la interfaz de usuario de Cloud Manager y es específico del dominio y del entorno de Cloud Manager |

Cuando haya terminado, puede verificar el resultado ejecutando: `dig _aemverification.[yourdomainname] -t txt`.
El resultado esperado debería mostrar el valor TXT proporcionado en la interfaz de usuario de Cloud Manager.

Por ejemplo, si su dominio es `example.com`, ejecute: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>También hay varias [herramientas de búsqueda DNS](https://www.ultratools.com/tools/dnsLookup), Google DoH puede usarse para buscar entradas de registro TXT e identificar si falta el registro TXT o si es erróneo.
