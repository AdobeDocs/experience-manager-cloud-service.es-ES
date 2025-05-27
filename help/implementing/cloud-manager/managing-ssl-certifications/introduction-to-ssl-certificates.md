---
title: Introducción a los certificados SSL
description: Obtenga información acerca de las herramientas de autoservicio que proporciona Cloud Manager para instalar y administrar certificados SSL.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b0c8769b5941ed772a91cf189e8c7355d1db766b
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 17%

---


# Introducción a los certificados SSL{#introduction}

Obtenga información acerca de las herramientas de autoservicio que proporciona Cloud Manager para instalar y administrar certificados SSL (Secure Socket Layer).

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Administrar certificados SSL"
>abstract="Descubra la forma en la que Cloud Manager proporciona herramientas de autoservicio para instalar y administrar certificados SSL con el fin de proteger su sitio en beneficio de sus usuarios. Cloud Manager utiliza un servicio TLS de plataforma para administrar certificados SSL y claves privadas propiedad de clientes y obtenidas de autoridades de certificación de terceros."
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Ver, actualizar y reemplazar un certificado SSL"
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Comprobar el estado de un certificado SSL"

## ¿Qué son los certificados SSL? {#overview}

Las empresas y organizaciones utilizan certificados SSL (Secure Socket Layer) para proteger sus sitios web y permitir a sus clientes confiar en ellos. Para utilizar el protocolo SSL, un servidor web requiere un certificado SSL.

Cuando una entidad, como una organización o una empresa, solicita un certificado de una entidad emisora de certificados (CA), esta completa un proceso de verificación. Este proceso puede abarcar desde verificar el control de nombres de dominio hasta recopilar documentos de registro de empresas y acuerdos de suscriptores. Una vez verificada la información de una entidad, la CA firma su clave pública con la clave privada de la CA. Dado que todas las autoridades de certificación principales tienen certificados raíz en los exploradores web, el certificado de la entidad se vincula a través de una *cadena de confianza* y el explorador web lo reconoce como un certificado de confianza.

>[!IMPORTANT]
>
>Cloud Manager no proporciona certificados SSL ni claves privadas. Estas partes deben obtenerse de una entidad de certificación, una organización de terceros de confianza. Algunas autoridades de certificación conocidas son *DigiCert*, *Let&#39;s Encrypt*, *GlobalSign*, *Entrust* y *Verisign*.

## Administración de certificados con Cloud Manager {#cloud-manager}

Cloud Manager ofrece herramientas de autoservicio para instalar y administrar certificados SSL, lo que garantiza la seguridad del sitio para los usuarios. Cloud Manager admite dos modelos para administrar los certificados.

| | Modelo | Descripción |
| --- | --- | --- |
| A | **[Certificado SSL administrado por Adobe (DV)](#adobe-managed)** | Cloud Manager permite a los usuarios configurar los certificados DV (validación de dominio) proporcionados por Adobe para configurar rápidamente el dominio. |
| B | **[Certificado SSL administrado por el cliente (OV/EV)](#customer-managed)** | Cloud Manager ofrece un servicio TLS (Transport Layer Security) para permitirle administrar los certificados SSL OV y EV de su propiedad y las claves privadas de autoridades de certificación de terceros, como *Let&#39;s Encrypt*. |

Ambos modelos ofrecen las siguientes funciones generales para administrar los certificados:

* Cada entorno de Cloud Manager puede utilizar varios certificados.
* Una clave privada puede emitir varios certificados SSL.
* El servicio TLS de plataforma enruta las solicitudes al servicio CDN del cliente en función del certificado SSL utilizado para finalizar y el servicio CDN que aloja ese dominio.

>[!IMPORTANT]
>
>[Para agregar y asociar un dominio personalizado con un entorno](/help/implementing/cloud-manager/custom-domain-names/introduction.md), debe tener un certificado SSL válido que cubra el dominio.

### Certificados SSL administrados por Adobe (DV) {#adobe-managed}

Los certificados DV son el nivel más básico de certificación SSL y se utilizan a menudo para fines de prueba o para proteger sitios web con cifrado básico. Los certificados DV están disponibles tanto en [programas de producción como en programas de zonas protegidas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

Una vez creado el certificado DV, Adobe lo renueva automáticamente cada tres meses, a menos que se elimine.

>[!IMPORTANT]
>
>Si su entorno utiliza certificados SSL (DV) con una validación basada en CNAME, tenga en cuenta que la eliminación del registro CNAME antes de la renovación automática de certificados puede provocar un error en la renovación. La eliminación puede provocar la caducidad del certificado y la interrupción del servicio. Para evitar este problema, asegúrese de que el registro CNAME permanece en su lugar durante todo el proceso de renovación. El proceso de renovación depende de la presencia del registro CNAME para la validación de la propiedad del dominio.

### Certificados SSL administrados por el cliente (OV/EV) {#customer-managed}

Los certificados OV y EV ofrecen información validada por CA. Esta información ayuda a los usuarios a comprobar si se puede confiar en el propietario del sitio web, el remitente del correo electrónico o la firma digital de los documentos de código o PDF. Los certificados DV no permiten esta verificación de propiedad.

Además, OV y EV ofrecen estas características con respecto a los certificados DV de Cloud Manager.

* Varios entornos pueden utilizar un certificado OV/EV. Es decir, se puede agregar una vez, pero se puede utilizar varias veces.
* Cada certificado OV/EV suele contener varios dominios.
* Cloud Manager acepta certificados OV/EV comodín para un dominio.

>[!TIP]
>
>Si tiene varios dominios personalizados, es posible que no desee cargar un certificado cada vez que agregue un nuevo dominio. En ese caso, podría beneficiarse de obtener un único certificado que abarque varios dominios.

#### Requisitos para los certificados SSL OV/EV administrados por el cliente {#requirements}

Si decide añadir su propio certificado SSL administrado por el cliente, debe cumplir los siguientes requisitos actualizados:

* No se admiten certificados de validación de dominio (DV) ni certificados autofirmados.
* El certificado debe cumplir las directivas OV (validación de organización) o EV (validación extendida).
* El certificado debe ser un certificado TLS X.509 emitido por una autoridad de certificación (CA) de confianza.
* Los tipos de clave criptográfica admitidos son los siguientes:

   * Soporte estándar RSA de 2048 bits.
Las claves RSA de más de 2048 bits (como las claves RSA de 3072 o 4096 bits) no son compatibles en este momento.
   * Claves de curva elíptica (EC) `prime256v1` (`secp256r1`) y `secp384r1`
   * Certificados ECDSA (Elliptic Curve Digital Signature Algorithm). Estos certificados son recomendados por Adobe sobre RSA para mejorar el rendimiento, la seguridad y la eficacia.

* Los certificados deben tener el formato correcto para pasar la validación. Las claves privadas deben tener el formato `PKCS#8`.

>[!NOTE]
>Si su organización requiere conformidad mediante claves RSA de 3072 bits, la alternativa recomendada por Adobe es utilizar certificados ECDSA (`secp256r1` o `secp384r1`).


#### Prácticas recomendadas para la administración de certificados

* **Evitar certificados superpuestos:**

   * Para garantizar una administración de certificados sin problemas, evite implementar certificados superpuestos que coincidan con el mismo dominio. Por ejemplo, tener un certificado comodín (*.example.com) junto con un certificado específico (dev.example.com) puede generar confusión.
   * La capa TLS da prioridad al certificado más específico y implementado recientemente.

  Casos de ejemplo:

   * El &quot;certificado de desarrollo&quot; cubre `dev.example.com` y se implementa como una asignación de dominio para `dev.example.com`.
   * El &quot;certificado de ensayo&quot; cubre `stage.example.com` y se implementa como una asignación de dominio para `stage.example.com`.
   * Si &quot;Certificado de ensayo&quot; se implementa o actualiza *después de* &quot;Certificado de desarrollador&quot;, también sirve solicitudes para `dev.example.com`.

     Para evitar estos conflictos, asegúrese de que los certificados tengan un ámbito cuidadoso en los dominios a los que están destinados.

* **Certificados comodín:**

  Aunque se admiten certificados comodín (por ejemplo, `*.example.com`), solo deben usarse cuando sea necesario. En casos de superposición, el certificado más específico tiene prioridad. Por ejemplo, el certificado específico sirve `dev.example.com` en lugar del comodín (`*.example.com`).

* **Validación y solución de problemas:**
Antes de intentar instalar un certificado con Cloud Manager, Adobe recomienda validar la integridad del certificado localmente mediante herramientas como `openssl`. Por ejemplo,

  `openssl verify -untrusted intermediate.pem certificate.pem`


<!--
>[!NOTE]
>
>If two certificates cover the same domain are installed, the one that is more exact is applied.
>
>For example, if your domain is `dev.adobe.com` and you have one certificate for `*.adobe.com` and another for `dev.adobe.com`, the more specific one (`dev.adobe.com`) is used.
-->

#### Formato de los certificados administrados por el cliente {#certificate-format}

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

En cualquier momento dado, Cloud Manager admite hasta 50 certificados instalados. Estos certificados se pueden asociar a uno o más entornos de su programa e incluir también certificados caducados.

Si ha alcanzado el límite, revise los certificados y considere la posibilidad de eliminar cualquier certificado caducado. O bien, agrupe varios dominios en el mismo certificado, ya que un certificado puede abarcar varios dominios (hasta 100 SAN).

## Más información {#learn-more}

Un usuario con los permisos necesarios puede utilizar Cloud Manager para administrar los certificados SSL de un programa. Consulte los siguientes documentos para obtener más información sobre el uso de estas características.

* [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

