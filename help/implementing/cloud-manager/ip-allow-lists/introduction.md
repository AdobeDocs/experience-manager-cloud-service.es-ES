---
title: Introducción a las listas de IP permitidas
description: Descubra cómo las Listas de permitidos IP pueden limitar desde qué direcciones pueden acceder los usuarios a los dominios en AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 20%

---


# Introducción a las listas de IP permitidas {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Administrar listas de IP permitidas"
>abstract="AEM as a Cloud Service es accesible a través de Internet y está protegido mediante la autenticación y autorización de los usuarios. Las Listas de permitidos IP de Cloud Manager se pueden utilizar para limitar y controlar el acceso solo a direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden crear listas de permisos con direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de AEM."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Agregar una lista de IP permitidas"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Visualización y actualización de una Lista de permitidos IP"

AEM as a cloud service es accesible de forma predeterminada a través de Internet. Mientras que la seguridad se gestiona mediante la autenticación y autorización de usuarios, la inclusión en las listas de IP permitidas es una forma de limitar el acceso solo a direcciones IP de confianza.

Las Listas de permitidos IP de Cloud Manager se pueden utilizar para limitar y controlar el acceso a solo aquellas direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden [crear Lista de permitidos AEM IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de la red de confianza.

Después de agregar, [las Listas de permitidos IP se pueden aplicar o dejar de aplicar](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) varias veces como unidad o entidad a un servicio de autor, de editor o a ambos en un entorno.

>[!NOTE]
>
>Si no se aplica ninguna Lista de permitidos IP, de forma predeterminada se permiten todas las direcciones IP. Cuando se aplica una Lista de permitidos IP, no se permiten direcciones IP, excepto direcciones en la Lista de permitidos IP.

## Limitaciones {#limitations}

Las Listas de permitidos IP tienen varias limitaciones que se deben tener en cuenta.

* Se puede agregar un máximo de 50 Listas de permitidos IP en el programa.
* Se puede añadir un máximo de 50 direcciones IP/CIDR a cada Lista de permitidos IP.
* Los nombres de Lista de permitidos IP son compatibles con Cloud Manager para el servicio de autor, el servicio de publicación o ambos en un entorno.
