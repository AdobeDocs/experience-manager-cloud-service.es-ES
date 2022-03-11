---
title: Comprobación del estado de registro DNS
description: Comprobación del estado de registro DNS
exl-id: 76ca1584-e21d-4e3a-a08a-82b2779167cf
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 5%

---

# Comprobación del estado de registro DNS {#check-dns-record-status}

Para determinar si el nombre de dominio se resuelve correctamente en el sitio web as a Cloud Service de AEM, haga clic en el icono Estado del registro DNS de la tabla de la página Entornos de la página Configuración de dominio .

Cloud Manager déclencheur automáticamente una búsqueda DNS cuando el nombre de dominio personalizado se verifique e implemente por primera vez correctamente. Para los intentos subsiguientes, debe seleccionar activamente la variable **resolver de nuevo** junto al estado .

Cloud Manager realiza una búsqueda DNS del nombre de dominio y muestra uno de los siguientes mensajes de estado:

* **No se ha detectado el estado DNS**
El estado de DNS no se detectará hasta que el nombre de dominio personalizado se haya verificado e implementado correctamente. Este estado también se observa cuando el nombre de dominio personalizado está en proceso de eliminación.

* **La resolución de DNS es incorrecta**
Esto indica que la configuración de los registros DNS aún no se ha resuelto/señalado o es errónea.

   >[!NOTE]
   >Debe configurar una `CNAME` o `A-record` siguiendo las instrucciones correspondientes. Consulte Configuración de DNS para obtener más información. Cuando esté listo, debe seleccionar la opción **resolver de nuevo** junto al estado .

* **Resolución DNS en curso**
La resolución está en curso. Este estado suele verse después de seleccionar el icono &quot;resolver de nuevo&quot; junto al estado.

* **La resolución de DNS es correcta**
La configuración de DNS es correcta. El sitio está sirviendo a los visitantes.
