---
title: Verificación del dominio
description: Verificación del dominio
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Verificación del dominio {#verify-domain-name}

Un registro TXT DNS autoriza a un dominio a alojarse en un servicio CDN. El cliente debe crear un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo el control del cliente y autoriza a Cloud Manager a proporcionar contenido desde el servicio a un dominio. Dicha autorización podrá concederse y retirarse. El registro TXT es específico del entorno Dominio y Cloud Manager.

1. Inicie sesión en el host de dominio y visite la sección de registros DNS .
1. Copie y pegue la entrada TXT en la zona DNS donde se encuentra el dominio personalizado, exactamente como aparece. Si necesita un &quot;nombre&quot; para su entrada, asígnele `@`.

>[!NOTE]
>Varias herramientas de búsqueda DNS, como [Herramienta de búsqueda de DNS](https://www.ultratools.com/tools/dnsLookup), Google DoH se puede utilizar para buscar entradas de registros TXT e identificar si falta o si es erróneo el registro TXT.
