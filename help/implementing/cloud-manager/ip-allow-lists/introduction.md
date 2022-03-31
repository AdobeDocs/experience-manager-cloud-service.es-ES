---
title: Introducción a las Listas de permitidos IP
description: Descubra cómo las listas de permitidos IP pueden limitar desde qué direcciones los usuarios pueden acceder a sus dominios as a Cloud Service AEM.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 8d1680fa8dbaaefa297cf8c6698097b3c7acc48d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Introducción a las Listas de permitidos IP {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Administrar Listas de permitidos IP"
>abstract="AEM as a cloud service es accesible a través de Internet y está protegido mediante la autenticación y autorización de los usuarios. Las listas de permitidos IP de Cloud Manager se pueden usar para limitar y controlar el acceso solo a direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden crear listas de permitidos de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Añadir una Lista de permitidos IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Ver y actualizar una Lista de permitidos IP"

AEM as a cloud service es accesible a través de Internet y está protegido mediante la autenticación y autorización de los usuarios. Las listas de permitidos IP de Cloud Manager se pueden usar para limitar y controlar el acceso solo a direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden crear listas de permitidos de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de AEM.

Las listas de permitidos IP se pueden agregar una vez y aplicar/dejar de aplicar varias veces como unidad o entidad a un servicio de autor o editor en un entorno.

## Restricciones     {#limitations}

Existen varias limitaciones a la IP que permiten tener en cuenta las listas.

* Se puede añadir un máximo de 50 listas de permitidos IP en el programa
* Se puede añadir un máximo de 50 direcciones IP/CIDR a cada lista de permitidos IP.
* Los nombres de las listas de permitidos IP son compatibles con Cloud Manager para crear o publicar servicios en un entorno.
