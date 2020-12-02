---
title: Comprobación del estado de un certificado SSL - Administración de certificados SSL
description: Comprobación del estado de un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Comprobando el estado de un certificado SSL {#checking-status-an-ssl-certificate}

El estado de los certificados SSL se puede comprender de un vistazo desde la página de certificados SSL o desde la página de detalles del Entorno.

Puede identificar el estado de un certificado SSL desde los siguientes esquemas de color:

* ****
VerdeIndica que el certificado es válido durante al menos 60 días en el futuro.

* ****
NaranjaIndica que el certificado caducará en menos de 60 días. Es hora de asegurarse de que tiene un plan para renovar su certificado y reemplazarlo a través de la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio. Cloud Manager enviará notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado.

* ****
RojoIndica que, a pesar de varias notificaciones, el certificado SSL ha caducado.