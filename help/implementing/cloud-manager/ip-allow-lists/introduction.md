---
title: Introducción a las listas de IP permitidas
description: Descubra cómo las lista de permitidos AEM IP pueden limitar desde qué direcciones pueden acceder los usuarios a los dominios en el as a Cloud Service de la.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: f0edd0e3deeba89dcbd2dc1a07859138b24e2220
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 18%

---


# Introducción a las listas de IP permitidas {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Administrar listas de permitidos IP"
>abstract="AEM as a cloud service es accesible a través de internet y está protegido mediante la autenticación y autorización de los usuarios. Las listas de permitidos IP de Cloud Manager se pueden utilizar para limitar y controlar el acceso solo a direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden crear lista de permitidos AEM de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Agregar una lista de IP permitidas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists.html" text="Ver y actualizar una lista de IP permitidas"

AEM as a Cloud Service es accesible de forma predeterminada a través de Internet. Mientras que la seguridad se gestiona mediante la autenticación y autorización de usuarios, la inclusión en las listas de IP permitidas es una forma de limitar el acceso solo a direcciones IP de confianza.

Las listas de permitidos IP de Cloud Manager se pueden utilizar para limitar y controlar el acceso solo a dichas direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden [crear listas de permitidos](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) AEM de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios en la red de la red de la red de la red de la red de la red.

Después de agregar, [Las listas de permitidos IP se pueden aplicar/dejar de aplicar](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) varias veces como unidad o entidad a un servicio de autor o editor en un entorno.

>[!NOTE]
>
>Si no se aplica ninguna lista de permitidos IP, de forma predeterminada se permiten todas las direcciones IP. Cuando se aplica una lista de permitidos IP, no se permiten direcciones IP, excepto direcciones en la lista de permitidos IP.

## Restricciones {#limitations}

Las listas de permitidos IP tienen varias limitaciones que se deben tener en cuenta.

* Se puede agregar un máximo de 50 listas de permitidos IP en el programa
* Se puede añadir un máximo de 50 direcciones IP/CIDR a cada lista de permitidos IP.
* Los nombres de listas de permitidos IP son compatibles con Cloud Manager para crear, publicar o ambos servicios en un entorno.
