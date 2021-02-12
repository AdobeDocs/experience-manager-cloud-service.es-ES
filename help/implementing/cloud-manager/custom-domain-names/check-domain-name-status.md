---
title: Comprobación del estado del nombre de dominio
description: Comprobación del estado del nombre de dominio
translation-type: tm+mt
source-git-commit: f11cb3b56f51046779300626d1deb037dd687309
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Comprobando el estado del nombre de dominio {#check-status}

Puede determinar si el nombre de dominio se ha comprobado correctamente haciendo clic en el icono Estado del nombre de dominio en la tabla de Entornos de la página Configuración de dominio.

>[!NOTE]
>Cloud Manager déclencheur automáticamente una verificación TXT cuando seleccione Guardar en el paso de verificación del asistente Añadir dominio personalizado. Para las verificaciones posteriores, debe seleccionar activamente el icono **verificar nuevamente** junto al estado.

Cloud Manager verificará la propiedad del dominio mediante el valor TXT y mostrará uno de los siguientes mensajes de estado:

* **Falta el valor**
FailedTXT de verificación de dominio o se detecta con errores. Siga las instrucciones y vuelva a intentarlo. Cuando esté listo, debe seleccionar la variable 
*compruebe de* nuevo el icono junto al estado.

* **Verificación del dominio en**
cursoVerificación en curso. Este estado suele verse después de seleccionar la variable 
*compruebe de* nuevo el icono junto al estado.

* **Se ha verificado que la verificación de**
error de implementación de TXT se realizó correctamente. Sin embargo, la implementación de CDN falló. Se notificará automáticamente a un representante de Adobe.

* **Dominio verificado e**
implementadoEste estado indica que el nombre de dominio personalizado está listo para usarse.
   >[!NOTE]
   >En este punto, el nombre de dominio personalizado está listo para la prueba y se le dirigirá al nombre de dominio de Cloud Manager. Consulte [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.

* **Se está**
eliminando la eliminación del nombre de dominio personalizado.

* **Error al eliminar**
el nombre de dominio personalizado. Debe volver a intentarlo. Consulte [Eliminación de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para obtener más información.

