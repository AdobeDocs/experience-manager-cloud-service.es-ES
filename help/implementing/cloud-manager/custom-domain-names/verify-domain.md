---
title: Comprobando dominio
description: Comprobando dominio
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Comprobando dominio {#verify-domain-name}

Un registro TXT DNS autoriza a un dominio a alojarse en un servicio CDN. El cliente debe crear un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo el control del cliente y autoriza a Cloud Manager a ofrecer contenido desde el servicio a un dominio. Dicha autorización podrá concederse y retirarse. El registro TXT es específico del dominio y del entorno del administrador de la nube.

1. Inicie sesión en el host de dominio y visite la sección de registros DNS.
1. Copie y pegue la entrada TXT en la zona DNS donde se encuentra el dominio personalizado, tal como aparece. Si necesita un &quot;nombre&quot; para su entrada, indíquelo `@`.

>[!NOTE]
>Varias herramientas de búsqueda DNS, como Herramienta [de búsqueda](https://www.ultratools.com/tools/dnsLookup)DNS, Google DoH, se pueden usar para buscar entradas de registros TXT e identificar si falta el registro TXT o si es erróneo.
