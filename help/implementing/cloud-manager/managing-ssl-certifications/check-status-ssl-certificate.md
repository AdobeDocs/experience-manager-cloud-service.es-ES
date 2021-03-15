---
title: 'Comprobación del estado de un certificado SSL: Administración de certificados SSL'
description: 'Comprobación del estado de un certificado SSL: Administración de certificados SSL'
translation-type: tm+mt
source-git-commit: c6fe5e9dab0e119271c6cea272dddabe7babb1e4
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Comprobación del estado de un certificado SSL {#checking-status-an-ssl-certificate}

El estado de los certificados SSL se puede entender de un vistazo desde la página de certificados SSL.

Puede identificar el estado de un certificado SSL desde los siguientes esquemas de color:

* ****
VerdeIndica que el certificado es válido durante al menos 60 días en el futuro.

* ****
NaranjaIndica que el certificado caducará en menos de 60 días. Es hora de asegurarse de que tiene un plan para renovar su certificado y reemplazarlo a través de la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio. Cloud Manager enviará notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado.

* ****
RojoIndica que, a pesar de varias notificaciones, el certificado SSL ha caducado.

## Configuraciones preexistentes de CDN para Listas de permitidos IP {#pre-existing-cdn}

Los clientes con entornos que incluyan configuraciones de CDN preexistentes para Listas de permitidos IP, certificados SSL o nombres de dominio personalizados verán el siguiente mensaje en la página de detalles **IP Lista de permitidos** y **Environment**. El mensaje mostrado en la interfaz de usuario desaparecerá una vez que el cliente haya migrado completamente todas las configuraciones de entorno preexistentes a través de la interfaz de usuario y puede tardar entre 1 y 2 días hábiles en desaparecer el mensaje.

![](/help/implementing/cloud-manager/assets/ip-allow-list-1.png)

>[!NOTE]
>Para ver y administrar las configuraciones preexistentes, deben agregarse a través de la interfaz de usuario, como se muestra en la figura siguiente.

![](/help/implementing/cloud-manager/assets/ip-allow-list-2.png)