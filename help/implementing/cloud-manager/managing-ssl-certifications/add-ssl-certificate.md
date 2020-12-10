---
title: Añadir un certificado SSL - Administración de certificados SSL
description: Añadir un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Añadir un certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM como Cloud Service solo aceptará certificados OV (validación de organización) o EV (validación extendida). No se aceptarán los certificados DV (validación de dominio).

El certificado tarda unos días en proporcionarse y se recomienda que se aprovisione el certificado incluso con meses de anticipación. Consulte [Obtención de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obtener más detalles.

## Formato de certificado {#certificate-format}

Los archivos SSL deben tener formato PEM para poder instalarse en Cloud Manager. Las extensiones de archivo comunes que están dentro del formato PEM incluyen `.pem,` .`crt`,  `.cer`, y  `.cert`.

Siga los pasos a continuación para convertir el formato de sus archivos SSL a PEM:

1. Convertir PFX a PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. Convertir P7B a PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. Convertir DER a PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Consideraciones importantes {#important-considerations}

* Un usuario debe estar en la función Propietario de la empresa o Administrador de implementación para poder instalar un certificado SSL en Cloud Manager.

* En cualquier momento dado, Cloud Manager permitirá un máximo de 10 certificados SSL que se pueden asociar con uno o más entornos en el Programa, incluso si un certificado ha caducado. Sin embargo, la interfaz de usuario del Administrador de nube permitirá instalar hasta 50 certificados SSL en el programa con esta restricción.

## Añadir un certificado {#adding-a-cert}

Siga los pasos a continuación para agregar un certificado:

1. Inicie sesión en Cloud Manager.
1. Vaya a la pantalla **Entornos** desde la página **Información general**.
1. Haga clic en **Certificados SSL** en el menú de navegación de la izquierda. En esta pantalla se mostrará una tabla con detalles de los certificados SSL existentes.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)
1. Seleccione el botón **Añadir certificado** para abrir el cuadro de diálogo **Añadir certificado SSL**.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
   1. Escriba un nombre para el certificado en **Nombre del certificado**. Puede ser cualquier nombre que le ayude a hacer referencia fácilmente a su certificado.
   1. Pegue la **cadena de certificados**, **clave privada** y **cadena de certificados** en sus respectivos campos. Utilice el icono de pegado a la derecha del cuadro de entrada.
Los tres campos no son opcionales y deben incluirse.

1. Haga clic en **Guardar** para enviar el certificado. Verá que se muestra como una fila nueva en la tabla.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
   >[!NOTE]
   >Se mostrarán todos los errores detectados. Debe corregir todos los errores antes de guardar el certificado. Consulte [Errores de certificado](#certificate-errors) para obtener más información sobre cómo solucionar errores comunes.

## Errores de certificado {#certificate-errors}

### Corrección del pedido de certificado {#correct-certificate-order}

El motivo más común para que una implementación de certificado falle es que los certificados intermedios o de cadena no están en el orden correcto. Específicamente, los archivos de certificados intermedios deben terminar con el certificado raíz o el certificado más cercano a la raíz y estar en orden descendente desde el certificado `main/server` a la raíz.

Puede determinar el orden de los archivos intermedios mediante el siguiente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Puede comprobar que la clave privada y el certificado `main/server` coinciden utilizando los siguientes comandos:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>El resultado de estos dos comandos debe ser exactamente el mismo. Si no puede encontrar una clave privada coincidente en el certificado `main/server`, se le solicitará que vuelva a escribir la clave del certificado generando un nuevo CSR o solicitando un certificado actualizado a su proveedor SSL.

### Fechas de validez del certificado {#certificate-validity-dates}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días en el futuro

Compruebe la validez de la cadena de certificados.
