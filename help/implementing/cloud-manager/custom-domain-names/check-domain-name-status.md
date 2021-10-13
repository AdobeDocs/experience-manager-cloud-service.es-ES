---
title: Comprobación del estado del nombre de dominio
description: Comprobación del estado del nombre de dominio
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: 4533cbc689d69cbe126791b4426123f890754507
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Comprobación del estado del nombre de dominio {#check-status}

Puede determinar si su nombre de dominio se ha verificado correctamente haciendo clic en el icono Estado del nombre de dominio en la tabla Entornos de la página Configuración de dominio .

>[!NOTE]
>Cloud Manager déclencheur automáticamente una verificación TXT cuando seleccione Guardar en el paso de verificación del asistente Añadir dominio personalizado . Para las verificaciones posteriores, debe seleccionar activamente el icono **verify again** junto al estado.

Cloud Manager verificará la propiedad del dominio mediante el valor TXT y mostrará uno de los siguientes mensajes de estado:

* **Falta el valor**
FailedTXT de verificación de dominio o se detecta con errores. Siga las instrucciones y vuelva a intentarlo. Cuando esté listo, debe seleccionar la opción 
*compruebe de nuevo* junto al estado .

* **Verificación del dominio en**
cursoVerificación en curso. Este estado suele verse después de seleccionar la variable 
*compruebe de nuevo* junto al estado .

* **Se ha verificado que la verificación de la implementación**
con error de TXT se ha realizado correctamente. Sin embargo, la implementación de la CDN falló. Póngase en contacto con su representante del Adobe.

* **Dominio verificado e**
implementadoEste estado indica que el nombre de dominio personalizado está listo para utilizarse.
   >[!NOTE]
   >En este punto, su nombre de dominio personalizado está listo para la prueba y se dirigirá al nombre de dominio de Cloud Manager. Consulte [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.

* ****
La eliminación del nombre de dominio personalizado está en proceso.

* **Error al eliminar**
el nombre de dominio personalizado. Debe volver a intentarlo. Consulte [Eliminación de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para obtener más información.


## Configuraciones preexistentes de CDN para nombres de dominio personalizados {#pre-existing-cdn}

Los clientes con entornos que incluyan configuraciones de CDN preexistentes para Listas de permitidos IP, certificados SSL o nombres de dominio personalizados verán el siguiente mensaje en la página de detalles **IP Lista de permitidos** y **Environment**. El mensaje mostrado en la interfaz de usuario desaparecerá una vez que el cliente haya migrado completamente todas las configuraciones de entorno preexistentes a través de la interfaz de usuario y puede tardar entre 1 y 2 días hábiles en desaparecer el mensaje.

>[!NOTE]
>Para ver y administrar las configuraciones preexistentes, deben agregarse mediante la interfaz de usuario de . Consulte [Adición de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
