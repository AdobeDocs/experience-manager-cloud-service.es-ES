---
title: 'Introducción: Administración de certificados SSL'
description: 'Introducción: Administración de certificados SSL'
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Introducción {#introduction}

Cloud Manager ofrece a los clientes la capacidad de autoservicio de instalar certificados SSL mediante la interfaz de usuario del Administrador de nube. Cloud Manager utiliza un servicio TLS de plataforma para administrar los certificados SSL y las claves privadas que son propiedad de los clientes y que normalmente se obtienen de terceros emisores de certificados, por ejemplo, Let’s Encrypt.

## Consideraciones importantes {#important-considerations}


* Cloud Manager no proporciona certificados SSL ni claves privadas. Estos deben obtenerse de entidades emisoras de certificados de terceros. Consulte [Obtención de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obtener más información.

* AEM como Cloud Service sólo admite sitios `https` seguros. Los clientes con varios dominios personalizados no querrán cargar un certificado cada vez que añadan un dominio. Por lo tanto, estos clientes se beneficiarán al obtener un certificado con varios dominios.

Cloud Manager admite los siguientes requisitos de certificado SSL de cliente:

* Un certificado SSL puede ser utilizado por varios Entornos, es decir, agregar una vez y usar varias veces.
* Cada Entorno de Cloud Manager puede utilizar varios certificados.
* Una clave privada puede emitir varios certificados SSL.
* Cada certificado contendrá normalmente varios dominios.
* El servicio TLS de plataforma enruta las solicitudes al servicio CDN del cliente según el certificado SSL utilizado para finalizar y el servicio CDN que aloja ese dominio.

Mediante la página Certificados SSL de la interfaz de usuario del Administrador de nube, un usuario con permisos puede realizar varias tareas para administrar los certificados SSL de un programa:

* [Añadir un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualización, actualización o sustitución de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >Estas acciones le permiten realizar vistas de detalles o reemplazar un certificado que está a punto de caducar.
* [Eliminación de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)