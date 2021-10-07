---
title: Comprobación del estado de registro DNS
description: Comprobación del estado de registro DNS
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Comprobación del estado de registro DNS {#check-dns-record-status}

Para determinar si el nombre de dominio se resuelve correctamente en el sitio web as a Cloud Service de AEM, haga clic en el icono Estado del registro DNS de la tabla de la página Entornos de la página Configuración de dominio .

Cloud Manager déclencheur automáticamente una búsqueda DNS cuando el nombre de dominio personalizado se verifique e implemente por primera vez correctamente. Para los intentos posteriores, debe seleccionar activamente el icono **resolve again** situado junto al estado.

Cloud Manager realiza una búsqueda DNS del nombre de dominio y muestra uno de los siguientes mensajes de estado:

* **Estado de DNS no**
detectadoEl estado de DNS no se detectará hasta que el nombre de dominio personalizado se haya verificado e implementado correctamente. Este estado también se observa cuando el nombre de dominio personalizado está en proceso de eliminación.

* **DNS resuelve**
incorrectamenteIndica que la configuración de los registros DNS aún no se ha resuelto ni se ha señalado o que es errónea. Se notificará automáticamente a un representante de Adobe.

   >[!NOTE]
   >Debe configurar un `CNAME` o `A-record` siguiendo las instrucciones correspondientes. Consulte Configuración de DNS para obtener más información. Cuando esté listo, debe seleccionar el icono **resolve again** junto al estado.

* **La resolución de DNS en**
ProgressResolution está en curso. Este estado suele verse después de seleccionar el icono &quot;resolver de nuevo&quot; junto al estado.

* **Resoluciones de DNS**
correctamenteLa configuración de DNS es correcta. El sitio está sirviendo a los visitantes.
