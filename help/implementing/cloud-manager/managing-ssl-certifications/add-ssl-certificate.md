---
title: Añadir un certificado SSL - Administración de certificados SSL
description: Añadir un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: e27e5302802e68dce2a5713626950896bb35420a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# Añadir un certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>El certificado tarda unos días en proporcionarse y se recomienda que se aprovisione el certificado incluso con meses de anticipación. Ir a Cómo obtener un certificado SSL para obtener más información.INSERTAR VÍNCULO

## Formato de certificado {#certificate-format}

Los archivos SSL deben tener formato PEM para poder instalarse en Cloud Manager. Las extensiones de archivo comunes que están dentro del formato PEM incluyen .pem, .crt, .cer y .cert.

Siga los pasos a continuación para convertir el formato de sus archivos SSL a PEM:

1. Convertir PFX a PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. Convertir P7B a PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. Convertir DER a PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Añadir el certificado {#adding-certificate}

>[!NOTE]
>* Un usuario debe estar en la función Propietario de la empresa o Administrador de implementación para poder instalar un certificado SSL en Cloud Manager.
>* En cualquier momento dado, Cloud Manager permitirá un máximo de 5 certificados SSL que se pueden asociar con uno o más entornos en el Programa, incluso si un certificado ha caducado. Sin embargo, la interfaz de usuario del Administrador de nube permitirá instalar hasta 50 certificados SSL en el programa con esta restricción.


1. Inicie sesión en Cloud Manager.
1. Acceda a la pantalla Entornos desde la página Información general.
1. Acceda a la pantalla Certificados SSL desde el menú de navegación de la izquierda. En esta pantalla se mostrará una tabla con los detalles de los certificados SSL existentes.INSERTAR IMAGEN
1. Seleccione el botón **Añadir certificado** para iniciar un asistente.
1. Escriba un nombre para el certificado. Puede ser cualquier nombre que le ayude a hacer referencia fácilmente a su certificado.
1. Pegue el contenido de Certificado, Clave privada y Cadena en sus respectivos campos. Utilice el icono de pegado a la derecha del cuadro de entrada.
1. Seleccione **Guardar**.

   >[!NOTE]
   >Se mostrarán todos los errores detectados. Debe corregir todos los errores antes de guardar el certificado. Consulte Errores del VÍNCULO INSERT del certificado para obtener más información sobre cómo solucionar errores comunes.

   Una vez que envíe el certificado, lo verá como una nueva fila en la tabla.

## Errores de certificado {#certificate-errors}

### Corregir orden de certificados {#correct-certificate-order}

El motivo más común para que una implementación de certificado falle es que los certificados intermedios o de cadena no están en el orden correcto. Específicamente, los archivos de certificados intermedios deben terminar con el certificado raíz o el certificado más cercano a la raíz y estar en orden descendente desde el `main/server` certificado hasta la raíz.

Puede determinar el orden de los archivos intermedios mediante el siguiente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Puede comprobar que la clave privada y el certificado `main/server` coinciden utilizando los siguientes comandos:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>El resultado de estos dos comandos debe ser exactamente el mismo. Si no puede encontrar una clave privada coincidente en el certificado, se le solicitará que vuelva a escribir el certificado generando un nuevo CSR y/o solicitando un certificado actualizado a su proveedor SSL. `main/server`

### Fechas de validez del certificado {#certificate-validity-dates}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días en el futuro

Compruebe la validez de la cadena de certificados.
