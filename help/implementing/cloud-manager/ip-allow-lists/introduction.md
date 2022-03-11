---
title: 'Introducción: Listas de permitidos IP en Cloud Manager'
description: 'Introducción: Listas de permitidos IP en Cloud Manager'
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
source-git-commit: 1875920ae5180074dcad98fb5c10242b6baa76c7
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 3%

---

# Introducción {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Administrar Listas de permitidos IP"
>abstract="AEM as a cloud service está abierto a Internet y la seguridad se gestiona mediante la autenticación y autorización de usuarios. La lista de IP permitidas es una función de Cloud Manager que se utiliza para limitar y controlar el acceso solo a usuarios de confianza. Esta función permite a los usuarios con permisos crear listas de permitidos de direcciones IP de confianza desde las que los usuarios de sus sitios pueden acceder a sus dominios de AEM."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists.html" text="Añadir una Lista de permitidos IP"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/view-update-ip-allow-list.html" text="Ver y actualizar una Lista de permitidos IP"

AEM as a cloud service está abierto a Internet y la seguridad se gestiona mediante la autenticación y autorización de usuarios. La lista de IP permitidas es una función de Cloud Manager que se utiliza para limitar y controlar el acceso solo a usuarios de confianza. Esta función permite a los usuarios con permisos crear listas de permitidos de direcciones IP de confianza desde las que los usuarios de sus sitios pueden acceder a sus dominios de AEM.

>[!NOTE]
>Se puede añadir un máximo de 50 Listas de permitidos IP en el programa y se puede añadir un máximo de 50 direcciones IP/CIDR a cada Lista de permitidos IP.

Las Listas de permitidos IP se pueden agregar una vez y aplicar/dejar de aplicar varias veces como unidad o entidad a un servicio de Author o Publisher en un entorno.

>[!NOTE]
>Los nombres de las Listas de permitidos IP se admiten en Cloud Manager para Autor o servicio de publicación en un entorno.

Mediante la página de Lista de permitidos IP de la interfaz de usuario de Cloud Manager o la página Detalles del entorno , un usuario con permisos de puede realizar varias tareas para administrar las Listas de permitidos IP de sus entornos, entre las que se incluyen:

* [Adición de una lista de permitidos de IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md)
   >[!NOTE]
   > Puede agregar una vez y reutilizar o aplicar la regla cualquier cantidad de veces entre los servicios de entorno del programa.
* [Visualización o actualización de una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/view-update-ip-allow-list.md)
* [Aplicación o cancelación de la aplicación de una Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)
* [Eliminación de una lista de permitidos de IP](/help/implementing/cloud-manager/ip-allow-lists/delete-ip-allow-list.md)
