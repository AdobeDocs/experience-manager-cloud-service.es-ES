---
title: 'Introducción: Administración de certificados SSL'
description: 'Introducción: Administración de certificados SSL'
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Introducción {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Administrar certificados SSL"
>abstract="Cloud Manager proporciona a los clientes la capacidad de autoservicio para instalar certificados SSL a través de la interfaz de usuario de Cloud Manager. Cloud Manager utiliza un servicio de Platform TLS para administrar los certificados SSL y las claves privadas que son propiedad de los clientes y que normalmente se obtienen de entidades emisoras de certificados de terceros."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/view-update-replace-ssl-certificate.html" text="Ver, actualizar y reemplazar un certificado SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/check-status-ssl-certificate.html" text="Comprobar el estado de un certificado SSL"


Cloud Manager proporciona a los clientes la capacidad de autoservicio para instalar certificados SSL a través de la interfaz de usuario de Cloud Manager. Cloud Manager utiliza un servicio de Platform TLS para administrar los certificados SSL y las claves privadas que son propiedad de los clientes y que normalmente se obtienen de las autoridades de certificación de terceros, por ejemplo, *Vamos a cifrar*.

## Consideraciones importantes {#important-considerations}

* Cloud Manager no proporciona certificados SSL ni claves privadas. Estos deben obtenerse de entidades certificadoras de terceros. Consulte [Obtención de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obtener más información.

* AEM como Cloud Service solo admite `https` sitios seguros. Los clientes con varios dominios personalizados no querrán cargar un certificado cada vez que añadan un dominio. Por lo tanto, estos clientes se beneficiarán de obtener un certificado con varios dominios.

* AEM como Cloud Service solo aceptará certificados OV(Organization Validation) o EV(Extended Validation). No se aceptarán los certificados DV(Domain Validation). Además, cualquier certificado debe ser un certificado X.509 TLS de una entidad de certificación (CA) de confianza con una clave privada RSA de 2048 bits que coincida.

* AEM como Cloud Service aceptará certificados SSL comodín para un dominio.

Cloud Manager es compatible con los siguientes requisitos de certificado SSL de cliente:

* Un certificado SSL puede ser utilizado por varios entornos, es decir, agregar una vez y usar varias veces.
* Cada entorno de Cloud Manager puede utilizar varios certificados.
* Una clave privada puede emitir varios certificados SSL.
* Cada certificado generalmente contiene varios dominios.
* El servicio Platform TLS enruta las solicitudes al servicio CDN del cliente en función del certificado SSL utilizado para finalizar y el servicio CDN que aloja ese dominio.

Mediante la página Certificados SSL de la interfaz de usuario de Cloud Manager , un usuario con permisos puede realizar varias tareas para administrar los certificados SSL para un programa:

* [Adición de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualización, actualización o sustitución de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/view-update-replace-ssl-certificate.md)
   >[!NOTE]
   >Estas acciones permiten ver los detalles o reemplazar un certificado que está a punto de caducar.
* [Eliminación de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/delete-ssl-certificate.md)
