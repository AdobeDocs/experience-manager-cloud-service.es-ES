---
title: Introducción a los certificados SSL
description: Descubra cómo Cloud Manager le proporciona herramientas de autoservicio para instalar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 34%

---


# Introducción a los certificados SSL{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Administrar certificados SSL"
>abstract="Descubra la forma en la que Cloud Manager le proporciona herramientas de autoservicio para instalar y administrar certificados SSL con el fin de proteger su sitio en beneficio de sus usuarios. Cloud Manager utiliza un servicio TLS de plataforma para administrar certificados SSL y claves privadas propiedad de clientes y obtenidas de autoridades de certificación de terceros."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Ver, actualizar y reemplazar un certificado SSL"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Comprobar el estado de un certificado SSL"


Cloud Manager ofrece herramientas de autoservicio para instalar y administrar certificados SSL (Secure Socket Layer), lo que garantiza la seguridad del sitio para los usuarios. Se admiten los dos casos de uso siguientes:

<!-- CQDOC-21758, #1 -->

| | Caso de uso | Descripción |
| --- | --- | --- |
| 1 | **Certificado administrado por el Adobe (DV)** | Cloud Manager permite a los usuarios configurar un certificado DV (validación de dominio) que proviene del Adobe para configurar dominios rápidamente. Los certificados DV son el nivel más básico de certificación SSL y se utilizan a menudo para fines de prueba o para proteger sitios web con cifrado básico. Los certificados DV están disponibles tanto en [programas de producción como en programas de zonas protegidas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md). Una vez creado el certificado DV, el Adobe lo renueva automáticamente cada tres meses, a menos que se elimine. |
| 2 | **Certificado administrado por el cliente (OV/EV)** | Cloud Manager usa un servicio TLS (Transport Layer Security) de plataforma para administrar certificados SSL de propiedad del cliente y claves privadas de autoridades de certificación de terceros, como *Let&#39;s Encrypt*. |

>[!NOTE]
>
>Los clientes no pueden cargar certificados DV (validación de dominio).


## Introducción a los certificados SSL {#certificates}

Las empresas y organizaciones utilizan certificados SSL para proteger sus sitios web y permitir a sus clientes confiar en ellos. Para utilizar el protocolo SSL, un servidor web requiere el uso de un certificado SSL.

Cuando una entidad, como una organización o una empresa, solicita un certificado de una entidad emisora de certificados (CA), esta completa un proceso de verificación. Este proceso puede abarcar desde verificar el control de nombres de dominio hasta recopilar documentos de registro de empresas y acuerdos de suscriptores. Una vez verificada la información de una entidad, la CA firma su clave pública con la clave privada de la CA. Dado que todas las autoridades de certificación principales tienen certificados raíz en los exploradores web, el certificado de la entidad se vincula a través de una *cadena de confianza* y el explorador web lo reconoce como un certificado de confianza.

>[!IMPORTANT]
>
>Cloud Manager no proporciona certificados SSL ni claves privadas. Estas cosas deben obtenerse de una entidad de certificación, una organización de terceros de confianza. Algunas autoridades de certificación conocidas son *DigiCert*, *Let&#39;s Encrypt*, *GlobalSign*, *Entrust* y *Verisign*.

Cloud Manager es compatible con las siguientes opciones de uso de certificados SSL de cliente.

* Varios entornos pueden utilizar un certificado SSL. Es decir, se puede agregar una vez, pero se puede utilizar varias veces.
* Cada entorno de Cloud Manager puede utilizar varios certificados.
* Una clave privada puede emitir varios certificados SSL.
* Cada certificado suele contener varios dominios.
* El servicio TLS de plataforma enruta las solicitudes al servicio CDN del cliente en función del certificado SSL utilizado para finalizar y el servicio CDN que aloja ese dominio.
* AEM as a Cloud Service acepta certificados SSL comodín para un dominio.

AEM as a Cloud Service solo admite sitios `https` seguros. Los clientes con varios dominios personalizados no desean cargar un certificado cada vez que agregan un dominio. Estos clientes se benefician de obtener un certificado con varios dominios.

## Requisitos de certificado SSL {#requirements}

* AEM as a Cloud Service acepta certificados que se ajustan a la directiva OV (validación de organización), EV (validación extendida) o DV (validación de dominio). <!-- CQDOC-21758, #2 -->
* Cualquier certificado debe ser un certificado TLS X.509 de una autoridad de certificación de confianza con una clave privada RSA de 2048 bits que corresponda.
* No se aceptan los certificados firmados automáticamente.

Los certificados OV y EV ofrecen información validada por CA. Esta información ayuda a los usuarios a comprobar si se puede confiar en el propietario del sitio web, el remitente del correo electrónico o la firma digital de los documentos de código o PDF. Los certificados DV no permiten esta verificación de propiedad.

### Formato de certificado SSL administrado por el cliente {#certificate-format}

<!-- CQDOC-21758, #3 -->

Los archivos de certificado SSL deben tener el formato PEM para que se instalen con Cloud Manager. Las extensiones de archivo comunes del formato PEM incluyen `.pem,`. .`crt`, `.cer`, y `.cert`.

Los siguientes comandos `openssl` se pueden utilizar para convertir certificados que no sean PEM.

* Convertir PFX a PEM

  ```shell
  openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
  ```

* Convertir P7B a PEM

  ```shell
  openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
  ```

* Convertir DER a PEM

  ```shell
  openssl x509 -inform der -in certificate.cer -out certificate.pem
  ```

## Limitación del número de certificados SSL instalados {#limitations}

En cualquier momento dado, Cloud Manager permite un máximo de 50 certificados SSL instalados. Estos certificados se pueden asociar a uno o más entornos de su programa e incluir también certificados caducados.

Si ha alcanzado el límite, revise los certificados y considere la posibilidad de eliminar cualquier certificado caducado. O bien, agrupe varios dominios en el mismo certificado, ya que un certificado puede abarcar varios dominios (hasta 100 SAN).

## Más información {#learn-more}

Un usuario con los permisos necesarios puede utilizar Cloud Manager para administrar los certificados SSL de un programa. Consulte los siguientes documentos para obtener más información sobre el uso de estas características.

* [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

