---
title: Comprobación del estado de registro DNS
description: Obtenga información sobre cómo determinar si la configuración de DNS se resuelve correctamente mediante Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 96%

---

# Comprobación del estado de registro DNS {#check-dns-record-status}

En Cloud Manager puede determinar si su nombre de dominio se resuelve correctamente en su sitio web de AEM as a Cloud Service.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Clic **Configuración de dominio** en el panel de navegación izquierdo.

1. Haga clic en el icono **Estado** del nombre de dominio.

Cloud Manager realiza una búsqueda DNS del nombre de dominio y muestra uno de los siguientes mensajes de estado.

* **No se ha detectado el estado DNS**: el estado de DNS no se detectará hasta que el nombre de dominio personalizado se haya verificado e implementado correctamente.

   * Este estado también se observa cuando el nombre de dominio personalizado está en proceso de eliminación.

* **La resolución de DNS es incorrecta**: esto indica que la configuración de los registros DNS no se ha resuelto o es errónea.

   * Consulte [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.
   * Cuando esté listo, debe seleccionar el icono **Resolver de nuevo** junto al estado.

* **Resolución DNS en curso**: la resolución está en curso.

   * Este estado suele verse después de seleccionar el icono **Resolver de nuevo** junto al estado.

* **La resolución de DNS es correcta**: la configuración de DNS es correcta.

   * El sitio está sirviendo a los visitantes.

Cloud Manager activará automáticamente una búsqueda DNS cuando su nombre de dominio personalizado se verifique e implemente por primera vez correctamente. Para los intentos subsiguientes, debe seleccionar el icono **Resolver de nuevo** junto al estado.
