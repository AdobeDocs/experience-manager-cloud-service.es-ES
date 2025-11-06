---
title: Comprobar el estado del registro DNS
description: Obtenga información sobre cómo determinar si la configuración de DNS se resuelve correctamente con Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 25%

---


# Comprobar el estado del registro DNS {#check-dns-record-status}

Obtenga información sobre cómo determinar si la configuración de DNS se resuelve correctamente con Cloud Manager.

## Estado de registros DNS {#status}

Un nombre de dominio personalizado no puede servir tráfico en directo hasta que el DNS se resuelva correctamente. En Cloud Manager, puede determinar si su nombre de dominio se resuelve correctamente en el sitio web de AEM as a Cloud Service.

## Requisitos {#requirements}

Complete estos requisitos antes de comprobar el estado de un registro DNS mediante Cloud Manager.

Ya debe haber configurado la configuración DNS para su nombre de dominio personalizado como se describe en [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Comprobar el estado del registro DNS {#how-to}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en **Configuración de dominio** en el menú del lado izquierdo.

1. Haga clic en el icono **Estado** del nombre de dominio.

Cloud Manager realiza una búsqueda DNS del nombre de dominio y lo muestra [estado actual](#statuses).

Cloud Manager almacena automáticamente en déclencheur una búsqueda DNS cuando el nombre de dominio personalizado se verifica e implementa por primera vez correctamente. Para los intentos subsiguientes, debe seleccionar el icono **Resolver de nuevo** junto al estado.

## Estados DNS en Cloud Manager {#statuses}

Un dominio personalizado puede tener uno de los siguientes estados en Cloud Manager.

| Estado | Descripción |
| --- | --- |
| No se detecta el estado de la DNS | El estado DNS no se detectará hasta que el nombre de dominio personalizado se verifique e implemente correctamente. Este estado también se observa cuando el nombre de dominio personalizado está en proceso de eliminación. |
| Las DNS no se resuelven correctamente | Este estado indica que la configuración de los registros DNS no se ha resuelto o es errónea. Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información.<br>Cuando esté listo, debe seleccionar el icono **Resolver de nuevo** junto al estado. |
| Resolución de DNS en curso | La resolución está en curso. Este estado suele verse después de seleccionar el icono **Resolver de nuevo** junto al estado. |
| Las DNS se han resuelto correctamente | La configuración de DNS es correcta. El sitio está sirviendo a los visitantes. |

## Próximos pasos {#next-steps}

Ha configurado correctamente su dominio personalizado para utilizarlo con Cloud Manager. Consulte el documento [Administrar nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información sobre cómo administrar los nombres de dominio personalizados mediante Cloud Manager.
