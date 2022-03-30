---
title: Comprobación del estado de registro DNS
description: Obtenga información sobre cómo determinar si la configuración de DNS se resuelve correctamente mediante Cloud Manager.
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 2278abcf0c34fd34a7730242ee27814d37b7d4d0
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---

# Comprobación del estado de registro DNS {#check-dns-record-status}

En Cloud Manager puede determinar si su nombre de dominio se resuelve correctamente en su sitio web as a Cloud Service AEM.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Entornos** de la **Información general** página.

1. Haga clic en **Configuración de dominio** en el panel de navegación izquierdo.

1. Haga clic en el **Estado** para el nombre de dominio.

Cloud Manager realiza una búsqueda DNS del nombre de dominio y muestra uno de los siguientes mensajes de estado.

* **No se ha detectado el estado DNS** - El estado de DNS no se detectará hasta que el nombre de dominio personalizado se haya verificado e implementado correctamente.

   * Este estado también se observa cuando el nombre de dominio personalizado está en proceso de eliminación.

* **La resolución de DNS es incorrecta** : esto indica que la configuración de los registros DNS no se ha resuelto o es errónea.

   * Consulte el documento [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.
   * Cuando esté listo, debe seleccionar la opción **Resolver de nuevo** junto al estado .

* **Resolución DNS en curso** - La resolución está en curso.

   * Este estado suele verse después de seleccionar la variable **Resolver de nuevo** junto al estado .

* **La resolución de DNS es correcta** - La configuración de DNS es correcta.

   * El sitio está sirviendo a los visitantes.

Cloud Manager déclencheur automáticamente una búsqueda DNS cuando su nombre de dominio personalizado se verifique e implemente por primera vez correctamente. Para los intentos subsiguientes, debe seleccionar activamente la variable **Resolver de nuevo** junto al estado .
