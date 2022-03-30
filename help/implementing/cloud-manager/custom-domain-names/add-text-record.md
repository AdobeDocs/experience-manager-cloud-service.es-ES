---
title: Adición de un registro TXT
description: Obtenga información sobre cómo agregar un registro TXT para agregar un nombre de dominio personalizado en Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: c80b7288b86ac62da17d5a83ec96cb882e36f687
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 4%

---

# Adición de un registro TXT {#adding-txt}

Un registro TXT DNS autoriza un dominio a alojarse en un servicio CDN. Debe crear un registro TXT de DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo su control y autoriza a Cloud Manager a servir contenido desde el servicio a un dominio. Esta autorización podrá concederse y retirarse.

Debe cumplir estos requisitos antes de agregar un registro TXT.

* Debe tener la capacidad de modificar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Debe identificar su host de dominio o registrador si todavía no lo conoce.

Al iniciar la verificación del dominio, Cloud Manager le da el nombre y el valor TXT que debe utilizar para la verificación. Agregue un registro TXT al servidor DNS de su dominio con el nombre y valor especificados.

1. Inicie sesión en el host de dominio y busque la sección Registros DNS .
1. Agregar `_aemverification.[yourdomainname]` como el **Nombre** y añada el valor TXT exactamente como aparece.

Consulte los ejemplos de esta tabla.

| Dominio | Nombre | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie todo el valor mostrado en la interfaz de usuario de Cloud Manager. Esto es específico para el dominio y el entorno. Por ejemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copie todo el valor mostrado en la interfaz de usuario de Cloud Manager. Esto es específico para el dominio y el entorno. Por ejemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

Cuando haya terminado, puede verificar el resultado ejecutando el siguiente comando

```shell
dig _aemverification.[yourdomainname] -t txt
```

El resultado esperado debería mostrar el valor TXT proporcionado en la interfaz de usuario de Cloud Manager.

Por ejemplo, si el dominio es `example.com`y luego ejecute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Existen varias [Herramientas de búsqueda DNS](https://www.ultratools.com/tools/dnsLookup) disponible. Google DoH se puede usar para buscar entradas de registros TXT e identificar si falta o si es erróneo el registro TXT.
