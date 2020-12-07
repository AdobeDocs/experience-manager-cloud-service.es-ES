---
title: 'Configuración de la configuración DNS '
description: Configuración de la configuración DNS
translation-type: tm+mt
source-git-commit: 1c51560886515e092680c23db3e128758dcd7d99
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Configuración de DNS {#configure-dns}

Una vez que el nombre de dominio personalizado se haya verificado e implementado correctamente, estará listo para actualizar los registros DNS del nombre de dominio personalizado con su proveedor DNS. Al hacerlo, el sitio puede servir visitantes. Por lo tanto, esta actividad se realiza normalmente antes de Go-live.

>[!NOTE]
>Usted o la persona adecuada de su organización deben poder iniciar sesión o ponerse en contacto con su proveedor DNS (la compañía a la que compró el dominio) y realizar actualizaciones en la configuración DNS.

Para ello, debe determinar si debe configurar la configuración DNS en un registro `CNAME` o Apex que apunte su nombre de dominio personalizado al nombre de dominio del Administrador de la nube. Un `CNAME` o registro A, una vez aprovisionado, enrutará todo el tráfico de Internet del dominio a donde esté apuntando. Si esa ubicación no está aprovisionada para atender el tráfico, habrá una interrupción. Si no se ha probado, puede que haya errores en el contenido. Por este motivo, este paso siempre se realiza una vez finalizada la prueba y el cliente está listo para Go-live.

## Registro CNAME {#cname-record}

Las siguientes secciones le ayudarán a determinar qué tipo de registro es adecuado para su configuración DNS.

Un registro de nombre canónico o `CNAME` es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com` al dominio que aloja el contenido de ese subdominio.

Inicie sesión en el Registrador de dominios y cree un registro CNAME para señalar el nombre de dominio personalizado al destinatario como se muestra a continuación:

| CNAME | Destinatario del punto de nombre de dominio personalizado |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## Registro APEX {#apex-record}

Un dominio apex es un dominio personalizado que no contiene un subdominio, como ejemplo.com. Un dominio apex está configurado con un registro `A` , `ALIAS` o `ANAME` a través de su proveedor DNS. Los dominios Apex deben apuntar a direcciones IP específicas.

Añada todos los siguientes registros A a la configuración DNS de su dominio a través de su proveedor de dominio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
