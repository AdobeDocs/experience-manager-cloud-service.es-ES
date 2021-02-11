---
title: Comprobación del estado del registro DNS
description: Comprobación del estado del registro DNS
translation-type: tm+mt
source-git-commit: b76a22469f248dde316dcaa514a906fe4361afd1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# Comprobando el estado del registro DNS {#check-dns-record-status}

Para determinar si el nombre de dominio se resuelve correctamente en el AEM como sitio web de un Cloud Service, haga clic en el icono Estado del registro DNS en la tabla de los Entornos de la página Configuración de dominio.

Cloud Manager déclencheur automáticamente una búsqueda DNS cuando el nombre de dominio personalizado se verifique e implemente por primera vez correctamente. Para los intentos posteriores, debe seleccionar activamente el icono **resolver de nuevo** junto al estado.

Cloud Manager realiza una búsqueda DNS del nombre de dominio y muestra uno de los siguientes mensajes de estado:

* **Estado de DNS no**
detectadoEl estado de DNS no se detectará hasta que el nombre de dominio personalizado se haya verificado e implementado correctamente. Este estado también se observa cuando el nombre de dominio personalizado se está eliminando.

* **Resoluciones DNS**
incorrectasIndica que la configuración de registros DNS no se ha resuelto/señalado o es errónea. Se notificará automáticamente a un representante de Adobe.

   >[!NOTE]
   >Debe configurar una `CNAME` o `A-record` siguiendo las instrucciones correspondientes. Consulte Configuración de DNS para obtener más información. Cuando esté listo, debe seleccionar el icono **resolver nuevamente** junto al estado.

* **La resolución de DNS en**
cursoLa resolución está en curso. Este estado suele aparecer después de seleccionar el icono &quot;resolver nuevamente&quot; junto al estado.

* **Resoluciones DNS**
correctamenteLa configuración de DNS está correctamente configurada. Su sitio está sirviendo visitantes.
