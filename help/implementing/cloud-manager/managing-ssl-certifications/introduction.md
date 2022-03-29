---
title: Introducción a la administración de certificados SSL
description: Descubra cómo Cloud Manager le proporciona herramientas de autoservicio para instalar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: 898f7bc46a3f1b0ac93ee43fbf7b60a11682a073
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---


# Introducción a la administración de certificados SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Administrar certificados SSL"
>abstract="Descubra cómo Cloud Manager le proporciona herramientas de autoservicio para instalar y administrar certificados SSL con el fin de proteger su sitio para los usuarios. Cloud Manager utiliza un servicio TLS de plataforma para administrar certificados SSL y claves privadas propiedad de clientes y obtenidas de autoridades de certificación de terceros."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Ver, actualizar y reemplazar un certificado SSL"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Comprobar el estado de un certificado SSL"

Cloud Manager le proporciona herramientas de autoservicio para instalar y administrar certificados SSL con el fin de proteger su sitio para los usuarios. Cloud Manager utiliza un servicio TLS de plataforma para administrar los certificados SSL y las claves privadas que son propiedad de los clientes y que se obtienen de entidades de certificación de terceros, como Let&#39;s Encrypt.

## Introducción a los certificados {#certificates}

Las empresas utilizan certificados SSL para proteger sus sitios web y permitir a sus clientes depositar confianza en ellos. Para utilizar el protocolo SSL, un servidor web requiere el uso de un certificado SSL.

Cuando una entidad solicita un certificado de una entidad emisora de certificados, esta completa un proceso de verificación. Esto puede abarcar desde verificar el control de nombres de dominio hasta recopilar documentos de registro de empresas y acuerdos de suscriptores. Una vez verificada la información de una entidad, la entidad emisora de certificados firmará su clave pública utilizando la clave privada de la entidad emisora de certificados. Dado que todas las autoridades de certificados principales tienen certificados raíz en los exploradores web, el certificado de la entidad se vinculará a través de un *cadena de confianza* y el explorador web lo reconocerá como un certificado de confianza.

>[!IMPORTANT]
>
>Cloud Manager no proporciona certificados SSL ni claves privadas. Deben obtenerse de las Entidades de certificación (CA).

## Funciones de administración de SSL de Cloud Manager {#features}

Cloud Manager es compatible con las siguientes opciones de uso de certificados SSL de cliente.

* Un certificado SSL puede ser utilizado por varios entornos. Es decir, se puede añadir una vez y utilizar varias veces.
* Cada entorno de Cloud Manager puede utilizar varios certificados.
* Una clave privada puede emitir varios certificados SSL.
* Cada certificado suele contener varios dominios.
* El servicio TLS de plataforma enruta las solicitudes al servicio CDN del cliente en función del certificado SSL utilizado para finalizar y el servicio CDN que aloja ese dominio.
* AEM as a Cloud Service acepta certificados SSL comodín para un dominio.

## Recomendaciones {#recommendations}

AEM as a Cloud Service solo admite seguro `https` sitios web.

* Los clientes con varios dominios personalizados no querrán cargar un certificado cada vez que añadan un dominio.
* Estos clientes se beneficiarán de obtener un certificado con varios dominios.

## Requisitos {#requirements}

* AEM as a Cloud Service solo aceptará certificados que se ajusten a la directiva OV (validación de organización) o EV (validación extendida).
* Cualquier certificado debe ser un certificado TLS X.509 de una entidad de certificación (CA) de confianza con una clave privada RSA de 2048 bits que corresponda.
* No se acepta la directiva DV (validación de dominio).
* No se aceptan certificados con firma personal.

Los certificados OV y EV proporcionan a los usuarios información adicional validada por CA que puede utilizarse para decidir si el propietario de un sitio web, el remitente de un correo electrónico o la firma digital de un código ejecutable o de documentos PDF es fiable. Los certificados DV no permiten esta verificación de propiedad.

## Restricciones     {#limitations}

En cualquier momento dado, Cloud Manager permitirá la instalación de un máximo de 50 certificados SSL. Pueden asociarse con uno o más entornos de su programa e incluir también certificados caducados.

Si ha alcanzado el límite, revise los certificados y considere:

* Eliminando cualquier certificado caducado.
* Agrupar varios dominios en el mismo certificado, ya que un certificado puede abarcar varios dominios (hasta 100 SANs).

## Más información {#learn-more}

Un usuario con los permisos necesarios puede utilizar Cloud Manager para administrar los certificados SSL de un programa. Consulte los siguientes documentos para obtener más información sobre el uso de estas funciones.

* [Adición de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visualización, actualización o sustitución de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [Eliminación de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
