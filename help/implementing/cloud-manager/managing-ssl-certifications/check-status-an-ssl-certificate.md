---
title: Comprobación del estado de un certificado SSL - Administración de certificados SSL
description: Comprobación del estado de un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: 295519e8969daec256e5007357b179a30a7932ce
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# Comprobación del estado de un certificado SSL {#checking-status-an-ssl-certificate}

El estado de los certificados SSL se puede comprender de un vistazo desde la página de certificados SSL o desde la página de detalles del Entorno.

Puede identificar el estado de un certificado SSL desde los siguientes esquemas de color:

* **Verde** Indica que el certificado es válido durante al menos 60 días en el futuro.

* **Naranja** Indica que el certificado caducará en menos de 60 días. Es hora de asegurarse de que tiene un plan para renovar su certificado y reemplazarlo a través de la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio. Cloud Manager enviará notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado.

* **Rojo** Indica que, a pesar de varias notificaciones, el certificado SSL ha caducado.