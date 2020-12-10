---
title: Comprobación del estado de un certificado SSL - Administración de certificados SSL
description: Comprobación del estado de un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: f426a9a653a3a3ae06abdbd2262e5d8f4beff277
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Comprobando el estado de un certificado SSL {#checking-status-an-ssl-certificate}

El estado de los certificados SSL se puede entender de un vistazo desde la página de certificados SSL.

Puede identificar el estado de un certificado SSL desde los siguientes esquemas de color:

* ****
VerdeIndica que el certificado es válido durante al menos 60 días en el futuro.

* ****
NaranjaIndica que el certificado caducará en menos de 60 días. Es hora de asegurarse de que tiene un plan para renovar su certificado y reemplazarlo a través de la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio. Cloud Manager enviará notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado.

* ****
RojoIndica que, a pesar de varias notificaciones, el certificado SSL ha caducado.