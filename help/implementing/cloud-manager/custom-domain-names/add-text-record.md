---
title: Agregar un registro TXT
description: Obtenga información sobre cómo agregar un registro TXT para agregar un nombre de dominio personalizado en Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 91%

---

# Agregar un registro TXT {#adding-txt}

Un registro TXT DNS autoriza a un dominio a alojarse en un servicio CDN. Debe crear un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio backend. Esta asociación está totalmente bajo su control y autoriza a Cloud Manager a servir contenido desde el servicio a un dominio. Esta autorización podrá concederse y retirarse. El registro TXT es específico del entorno Dominio y Cloud Manager.

Debe cumplir estos requisitos antes de agregar un registro TXT.

* Debe poder editar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Debe identificar su host de dominio o registrador si aún no lo conoce.

Al iniciar la verificación del dominio, Cloud Manager le dará el nombre y el valor TXT que debe utilizar para la verificación. Agregue un registro TXT al servidor DNS de su dominio con el nombre y valor especificados.

1. Inicie sesión en el host de dominio y busque la sección Registros DNS.
1. Agregue `_aemverification.[yourdomainname]` como el valor **Nombre** y agregue el valor TXT exactamente como aparece.

Consulte los ejemplos de esta tabla.

| Dominio | Nombre | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie todo el valor que se muestra en la interfaz de usuario de Cloud Manager. Esto es específico para el dominio y el entorno. Por ejemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copie todo el valor que se muestra en la interfaz de usuario de Cloud Manager. Esto es específico para el dominio y el entorno. Por ejemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

Cuando haya terminado, puede comprobar el resultado si ejecuta el siguiente comando

```shell
dig _aemverification.[yourdomainname] -t txt
```

El resultado esperado debería mostrar el valor TXT que se proporciona en la interfaz de usuario de Cloud Manager.

Por ejemplo, si el dominio es `example.com`, ejecute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Hay varios [Herramientas de búsqueda DNS](https://www.ultratools.com/tools/dnsLookup) disponible. Google DoH se puede usar para buscar entradas de registros TXT e identificar si el registro TXT falta o es erróneo.
