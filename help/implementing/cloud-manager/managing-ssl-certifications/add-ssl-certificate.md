---
title: 'Adición de un certificado SSL: administración de certificados SSL'
description: 'Adición de un certificado SSL: administración de certificados SSL'
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 3b4a9d7c04a5f4feecad0f34c27a894c187152e7
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Adición de un certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM como Cloud Service solo aceptará certificados OV(Organization Validation) o EV(Extended Validation). No se aceptarán los certificados DV(Domain Validation). Además, cualquier certificado debe ser un certificado X.509 TLS de una entidad de certificación (CA) de confianza con una clave privada RSA de 2048 bits que coincida. AEM como Cloud Service aceptará certificados SSL comodín para un dominio.

Un certificado tarda unos días en proporcionarse y se recomienda que se aprovisione el certificado incluso con meses de antelación. Consulte [Obtención de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obtener más información.

## Formato del certificado {#certificate-format}

Los archivos SSL deben tener formato PEM para poder instalarse en Cloud Manager. Las extensiones de archivo comunes que están dentro del formato PEM incluyen `.pem,` .`crt`,  `.cer`, y  `.cert`.

Siga los pasos a continuación para convertir el formato de sus archivos SSL a PEM:

* Convertir PFX a PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Convertir P7B a PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Convertir DER a PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Consideraciones importantes {#important-considerations}

* Un usuario debe tener la función Propietario empresarial o Administrador de implementación para poder instalar un certificado SSL en Cloud Manager.

* En cualquier momento dado, Cloud Manager permitirá un máximo de 10 certificados SSL que se pueden asociar con uno o más entornos en todo el programa, incluso si un certificado ha caducado. Sin embargo, la interfaz de usuario de Cloud Manager permitirá instalar hasta 50 certificados SSL en el programa con esta restricción. Normalmente, un certificado puede abarcar varios dominios (hasta 100 SANs), por lo que puede considerar la posibilidad de agrupar varios dominios en el mismo certificado para permanecer dentro de este límite.


## Adición de un certificado {#adding-a-cert}

Siga los pasos a continuación para añadir un certificado:

1. Inicie sesión en Cloud Manager.
1. Vaya a la pantalla **Environments** desde la página **Overview**.
1. Haga clic en **Certificados SSL** en el menú de navegación de la izquierda. En esta pantalla se mostrará una tabla con detalles de cualquier certificado SSL existente.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Haga clic en **Agregar certificado SSL** para abrir el cuadro de diálogo **Agregar certificado SSL**.

   * Escriba un nombre para el certificado en **Nombre del certificado**. Puede ser cualquier nombre que le ayude a hacer referencia al certificado fácilmente.
   * Pegue el **Certificado**, **Clave privada** y la **Cadena de certificados** en sus respectivos campos. Utilice el icono de pegado a la derecha del cuadro de entrada.
Los tres campos no son opcionales y deben incluirse.

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >Se mostrarán todos los errores detectados. Debe corregir todos los errores antes de guardar el certificado. Consulte [Errores de certificado](#certificate-errors) para obtener más información sobre la solución de errores comunes.

1. Haga clic en **Save** para enviar el certificado. Verá que se muestra como una fila nueva en la tabla.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## Errores de certificado {#certificate-errors}

### Orden de certificados correcto {#correct-certificate-order}

El motivo más común para que una implementación de certificado falle es que los certificados intermedios o de cadena no están en el orden correcto. En concreto, los archivos de certificado intermedios deben finalizar con el certificado raíz o el certificado más cercano a la raíz y estar en orden descendente desde el certificado `main/server` hasta la raíz.

Puede determinar el orden de los archivos intermedios mediante el siguiente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Puede comprobar que la clave privada y el certificado `main/server` coinciden utilizando los siguientes comandos:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>El resultado de estos dos comandos debe ser exactamente el mismo. Si no encuentra una clave privada coincidente en su certificado `main/server`, deberá volver a escribir el certificado generando un nuevo CSR o solicitando un certificado actualizado a su proveedor SSL.

### Fechas de validez del certificado {#certificate-validity-dates}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días en el futuro. Debe comprobar la validez de la cadena de certificados.
