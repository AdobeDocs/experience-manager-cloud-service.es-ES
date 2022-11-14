---
title: Introducción a las listas de IP permitidas
description: Descubra cómo las listas de IP permitidas pueden limitar desde qué direcciones pueden acceder los usuarios a sus dominios de AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 18ecf3394ff575213756fced84a3b08795188240
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 56%

---


# Introducción a las listas de IP permitidas {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Administrar listas de IP permitidas"
>abstract="AEM as a Cloud Service es accesible a través de Internet y está protegido mediante la autenticación y autorización de los usuarios. Las listas de IP permitidas de Cloud Manager se pueden usar para limitar y controlar el acceso solo a direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden crear listas de permitidos con direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html?lang=es" text="Agregar una lista de IP permitidas"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html?lang=es" text="Ver y actualizar una lista de IP permitidas"

AEM as a cloud service es accesible de forma predeterminada a través de Internet. Mientras que la seguridad se gestiona mediante la autenticación y autorización de usuarios, las listas de IP permitidas son una forma de limitar el acceso solo a direcciones IP de confianza.

Las listas de permitidos IP de Cloud Manager se pueden usar para limitar y controlar el acceso solo a estas direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden [crear listas de permitidos](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de AEM.

Una vez añadida, [Las listas de permitidos IP se pueden aplicar/no aplicar](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) varias veces como unidad o entidad a un servicio de autor o editor en un entorno.

>[!NOTE]
>
>Si no se aplica ninguna lista de permitidos IP, de forma predeterminada se permiten todas las direcciones IP. Tan pronto como se aplica una lista de permitidos IP, no se permiten direcciones IP, excepto las de la lista de permitidos IP.

## Restricciones {#limitations}

Existen varias limitaciones a la IP que permiten tener en cuenta las listas.

* Se puede agregar un máximo de 50 listas de IP permitidas en el programa.
* Se puede agregar un máximo de 50 direcciones IP/CIDR a cada lista de IP permitidas.
* Los nombres de las listas de IP permitidas son compatibles con Cloud Manager para crear o publicar servicios en un entorno.
