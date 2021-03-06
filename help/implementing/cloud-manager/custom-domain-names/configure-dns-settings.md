---
title: 'Configuración de DNS '
description: Configuración de DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 60b496024b3d012033309632999851c08f43c5d7
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Configuración de DNS {#configure-dns}

Una vez que el nombre de dominio personalizado se haya verificado e implementado correctamente, podrá actualizar los registros DNS del nombre de dominio personalizado con el proveedor DNS. Al hacerlo, el sitio puede servir a los visitantes. Por lo tanto, esta actividad se suele realizar antes de activarse.

## ¿Qué es la configuración de DNS? {#dns-settings}

A `CNAME` O Un registro, una vez aprovisionado, enrutará todo el tráfico de Internet para el dominio a donde señale. Si esa ubicación no está aprovisionada para servir el tráfico, se producirá una interrupción. Si no se ha probado, puede haber errores en el contenido. Esta es la razón por la que este paso siempre se realiza una vez finalizada la prueba y está listo para su lanzamiento.

Para configurar estos ajustes, debe determinar si una `CNAME` o el registro Apex debe configurarse para que apunte su nombre de dominio personalizado al nombre de dominio de Cloud Manager. Las siguientes secciones le ayudarán a determinar qué tipo de registro es apropiado para su configuración DNS.

>[!NOTE]
>
>Usted o la persona adecuada de su organización deben poder iniciar sesión o ponerse en contacto con su proveedor de DNS (la empresa desde la que compró el dominio) y realizar actualizaciones en la configuración de DNS.

## Registro CNAME {#cname-record}

Un nombre canónico o registro CNAME es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com` al dominio que hospeda el contenido de ese subdominio.

Inicie sesión en el registrador de dominios y cree un `CNAME` registro para señalar el nombre de dominio personalizado al destino, como en la tabla siguiente.

| CNAME | Punto de nombre de dominio personalizado en Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Registro APEX {#apex-record}

Un dominio apex es un dominio personalizado que no contiene un subdominio, como `example.com`. Un dominio de apex está configurado con un `A` , `ALIAS` o `ANAME` registre a través de su proveedor DNS. Los dominios de Apex deben apuntar a direcciones IP específicas.

Agregue todo lo siguiente `A` registra la configuración DNS de su dominio a través de su proveedor de dominios.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
