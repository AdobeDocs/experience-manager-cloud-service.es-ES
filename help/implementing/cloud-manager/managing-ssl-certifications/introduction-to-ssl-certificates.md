---
title: Introducción a los certificados SSL
description: Obtenga información acerca de las herramientas de autoservicio que proporciona Cloud Manager para instalar y administrar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 484f7b0fd8917902d028434451964dd9df3e3445
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 23%

---


# Introducción a los certificados SSL{#introduction}

Obtenga información acerca de las herramientas de autoservicio que proporciona Cloud Manager para instalar y administrar certificados SSL.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Administrar certificados SSL"
>abstract="Descubra la forma en la que Cloud Manager le proporciona herramientas de autoservicio para instalar y administrar certificados SSL con el fin de proteger su sitio en beneficio de sus usuarios. Cloud Manager utiliza un servicio TLS de plataforma para administrar certificados SSL y claves privadas propiedad de clientes y obtenidas de autoridades de certificación de terceros."
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Ver, actualizar y reemplazar un certificado SSL"
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Comprobar el estado de un certificado SSL"

## ¿Qué son los certificados SSL? {#overview}

Las empresas y organizaciones utilizan certificados SSL (Secure Socket Layer) para proteger sus sitios web y permitir a sus clientes confiar en ellos. Para utilizar el protocolo SSL, un servidor web requiere un certificado SSL.

Cuando una entidad, como una organización o una empresa, solicita un certificado de una entidad emisora de certificados (CA), esta completa un proceso de verificación. Este proceso puede abarcar desde verificar el control de nombres de dominio hasta recopilar documentos de registro de empresas y acuerdos de suscriptores. Una vez verificada la información de una entidad, la CA firma su clave pública con la clave privada de la CA. Dado que todas las autoridades de certificación principales tienen certificados raíz en los exploradores web, el certificado de la entidad se vincula a través de una *cadena de confianza* y el explorador web lo reconoce como un certificado de confianza.

>[!IMPORTANT]
>
>Cloud Manager no proporciona certificados SSL ni claves privadas. Deben obtenerse de una entidad de certificación, una organización de terceros de confianza. Algunas autoridades de certificación conocidas son *DigiCert*, *Let&#39;s Encrypt*, *GlobalSign*, *Entrust* y *Verisign*.

## Administración de certificados con Cloud Manager {#cloud-manager}

Cloud Manager ofrece herramientas de autoservicio para instalar y administrar certificados SSL, lo que garantiza la seguridad del sitio para los usuarios. Cloud Manager admite dos modelos para administrar los certificados.

| | Modelo | Descripción |
| --- | --- | --- |
| 1 | **[Certificado administrado por el Adobe (DV)](#adobe-managed)** | Cloud Manager permite a los usuarios configurar los certificados DV (validación de dominio) que proporciona Adobe para configurar rápidamente los dominios. |
| 2 | **[Certificado administrado por el cliente (OV/EV)](#customer-managed)** | Cloud Manager ofrece un servicio TLS (Transport Layer Security) para permitirle administrar los certificados SSL OV y EV de su propiedad, así como las claves privadas de autoridades de certificación de terceros, como *Let&#39;s Encrypt*. |

Ambos modelos ofrecen las siguientes características generales.

* Cada entorno de Cloud Manager puede utilizar varios certificados.
* Una clave privada puede emitir varios certificados SSL.
* El servicio TLS de plataforma enruta las solicitudes al servicio CDN del cliente en función del certificado SSL utilizado para finalizar y el servicio CDN que aloja ese dominio.

>[!IMPORTANT]
>
>[Para agregar y asociar un dominio personalizado a un entorno,](/help/implementing/cloud-manager/custom-domain-names/introduction.md) debe tener un certificado SSL válido que cubra el dominio.

### Adobe de certificados administrados {#adobe-managed}

Los certificados DV son el nivel más básico de certificación SSL y se utilizan a menudo para fines de prueba o para proteger sitios web con cifrado básico. Los certificados DV están disponibles tanto en [programas de producción como en programas de zonas protegidas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

Una vez creado el certificado DV, el Adobe lo renueva automáticamente cada tres meses, a menos que se elimine.

### Certificados administrados por el cliente {#customer-managed}

Los certificados OV y EV ofrecen información validada por CA. Esta información ayuda a los usuarios a comprobar si se puede confiar en el propietario del sitio web, el remitente del correo electrónico o la firma digital de los documentos de código o PDF. Los certificados DV no permiten esta verificación de propiedad.

Además, OV y EV ofrecen estas características con respecto a los certificados DV de Cloud Manager.

* Varios entornos pueden utilizar un certificado OV/EV.
   * Es decir, se puede agregar una vez, pero se puede utilizar varias veces.
* Cada certificado OV/EV suele contener varios dominios.
* Cloud Manager acepta certificados OV/EV comodín para un dominio.

>[!TIP]
>
>Si tiene varios dominios personalizados y no desea cargar un certificado cada vez que agregue un dominio, puede beneficiarse de obtener un certificado con varios dominios.

>[!NOTE]
>
>Si se instalan dos certificados que cubren el mismo dominio, se aplica el que es más exacto.
>
>Por ejemplo, si su dominio es `dev.adobe.com` y tiene un certificado que cubre `*.adobe.com` y un certificado que cubre `dev.adobe.com`, se aplicará este último porque es más exacto.

#### Requisitos para los certificados administrados por el cliente {#requirements}

Si decide cargar su propio certificado EV/OV, debe cumplir los siguientes requisitos.

* AEM as a Cloud Service acepta certificados que se ajustan a la directiva OV (validación de organización) o EV (validación extendida).
   * Cloud Manager no admite la carga de sus propios certificados DV (validación de dominio).
* Cualquier certificado debe ser un certificado TLS X.509 de una autoridad de certificación de confianza con una clave privada RSA de 2048 bits que corresponda.
* No se aceptan los certificados firmados automáticamente.

#### Formato para certificados administrados por el cliente {#certificate-format}

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

