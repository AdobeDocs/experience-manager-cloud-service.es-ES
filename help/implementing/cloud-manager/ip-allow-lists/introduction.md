---
title: Introducción a las listas de IP permitidas
description: Descubra cómo las Listas de permitidos IP pueden limitar desde qué direcciones pueden acceder los usuarios a los dominios en AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f3cd1bc761c513ebb85351185e7aa0b6f6eb6f33
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 7%

---


# Introducción a las listas de IP permitidas {#introduction}

Descubra cómo las Listas de permitidos IP pueden limitar desde qué direcciones pueden acceder los usuarios a los dominios en AEM as a Cloud Service.

<!-- Alexandru: contextual help links are broken, temporarily comminting this out until they,re fixed.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Manage IP Allow Lists"
>abstract="AEM as a Cloud Service is accessible by way of the Internet and is secured through user authentication and authorization. Cloud Manager's IP Allow Lists can be used to limit and control access only to trusted IP addresses. Cloud Manager users with appropriate permissions can create allowlists of trusted IP addresses from which their site's users can access their AEM domains."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Add an IP Allow List"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="View and update an IP Allow List"

-->

## Información general {#overview}

AEM as a Cloud Service es accesible de forma predeterminada a través de Internet. Mientras que la seguridad se gestiona mediante la autenticación y autorización de usuarios, la inclusión en las listas de IP permitidas es una forma de limitar el acceso solo a direcciones IP de confianza.

Las Listas de permitidos IP de Cloud Manager se pueden utilizar para limitar y controlar el acceso a solo aquellas direcciones IP de confianza. Los usuarios de Cloud Manager con los permisos adecuados pueden [crear y agregar Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) de direcciones IP de confianza desde las que los usuarios de su sitio pueden acceder a sus dominios de AEM.

Después de agregar, [las Listas de permitidos IP se pueden aplicar o dejar de aplicar](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) varias veces como unidad o entidad a un servicio de autor, de editor o a ambos en un entorno.

>[!NOTE]
>
>Si no se aplica ninguna Lista de permitidos IP, de forma predeterminada se permiten todas las direcciones IP. Cuando se aplica una Lista de permitidos IP, no se permiten direcciones IP, excepto direcciones en la Lista de permitidos IP.

## Notas de uso {#usage-notes}

* Se puede agregar un máximo de 50 Listas de permitidos IP al programa.
* Se puede añadir un máximo de 50 direcciones IP/CIDR a cada Lista de permitidos IP.
* Los nombres de Lista de permitidos IP son compatibles con Cloud Manager para el servicio de autor, el servicio de publicación o ambos en un entorno.

### Canalizaciones front-end y Listas de permitidos IP {#front-end-pipeline}

Si usa (o pretende usar) la canalización [front-end para desarrollar sitios](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md), se debe agregar de antemano la siguiente Lista de permitidos IP de Cloud Manager.

Cuando [agregue la Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist), asígnele el nombre *`Cloud Manager`* y, a continuación, copie la lista de direcciones que aparece a continuación y péguela en el cuadro de diálogo Lista de permitidos IP.

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

Para evitar interrupciones en la ejecución de la canalización front-end, asegúrese de añadir esta Lista de permitidos IP de Cloud Manager. A continuación, aplique la lista al entorno de creación *antes de* de habilitar la canalización.

Consulte [Aplicar Lista de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) y [Habilitar canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md) para obtener más información.

### El editor universal y las Listas de permitidos IP {#universal-editor}

Si tiene intención de utilizar el editor universal para crear contenido, debe añadir las direcciones IP que utiliza el servicio de editor universal a una Lista de permitidos y aplicarla.

1. Recupere las direcciones IP utilizadas por el servicio de editor universal desde el siguiente extremo de API: `http://universal-editor-service.adobe.io/ip-ranges`.
1. Cree una lista de permitidos con esas direcciones IP y asígnele el nombre `Universal Editor Service` o similar.
1. Aplicar la lista de permitidos `Universal Editor Service`.

La lista de direcciones IP que utiliza el servicio de editor universal está sujeta a cambios y debe actualizar la lista de permitidos en consecuencia.
