---
title: 'Comprobación del estado de un certificado SSL: Administración de certificados SSL'
description: 'Comprobación del estado de un certificado SSL: Administración de certificados SSL'
exl-id: 59d81356-2fa9-43db-bfa5-c2896c530eaa
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---

# Comprobación del estado de un certificado SSL {#checking-status-an-ssl-certificate}

El estado de los certificados SSL se puede entender de un vistazo desde la página de certificados SSL.

Puede identificar el estado de un certificado SSL desde los siguientes esquemas de color:

* **Verde**
Indica que el certificado es válido durante al menos 60 días en el futuro.

* **Naranja**
Indica que el certificado caducará en menos de 60 días. Es hora de asegurarse de que tiene un plan para renovar su certificado y reemplazarlo a través de la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio. Cloud Manager enviará notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado.

* **Rojo**
Indica que, a pesar de varias notificaciones, el certificado SSL ha caducado.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Los clientes con entornos que incluyan configuraciones de CDN preexistentes para Listas de permitidos IP, certificados SSL o nombres de dominio personalizados verán el siguiente mensaje en la **LISTA DE PERMITIDOS IP** y **Entorno** página de detalles . El mensaje mostrado en la interfaz de usuario desaparecerá una vez que el cliente haya migrado completamente todas las configuraciones de entorno preexistentes a través de la interfaz de usuario y puede tardar entre 1 y 2 días hábiles en desaparecer el mensaje.

>[!NOTE]
>Para ver y administrar las configuraciones preexistentes, deben agregarse mediante la interfaz de usuario de . Consulte [Adición de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
