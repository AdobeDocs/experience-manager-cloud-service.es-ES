---
title: Configuración de DNS
description: Obtenga información sobre cómo configurar DNS para los nombres de dominio personalizados.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 9fd7c17fce8c11809eabcc6387cbace0ebdc64a2
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 84%

---

# Configuración de DNS {#configure-dns}

Una vez que el nombre de dominio personalizado se haya verificado e implementado correctamente, podrá actualizar los registros DNS del nombre de dominio personalizado con el proveedor DNS. Al hacerlo, el sitio puede servir a los visitantes. Por lo tanto, esta actividad se suele realizar antes de activarse.

## ¿Qué es la configuración de DNS? {#dns-settings}

Un registro `CNAME` o A, una vez aprovisionado, enrutará todo el tráfico de Internet para el dominio a donde señale. Si esa ubicación no está aprovisionada para servir el tráfico, se produce una interrupción. Si no se ha probado, puede haber errores en el contenido. Esta es la razón por la que este paso siempre se realiza una vez finalizada la prueba y está listo para su lanzamiento.

Para establecer esta configuración, debe determinar si una variable `CNAME` o el registro Apex debe configurarse para que apunte su nombre de dominio personalizado al nombre de dominio de Cloud Manager. Las siguientes secciones le ayudarán a determinar qué tipo de registro es apropiado para su configuración de DNS.

>[!NOTE]
>
>Usted o la persona adecuada de su organización deben poder iniciar sesión o ponerse en contacto con su proveedor de DNS (la empresa desde la que compró el dominio) y realizar actualizaciones en la configuración de DNS.

## Registro CNAME {#cname-record}

Un nombre canónico o registro CNAME es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com` al dominio que hospeda el contenido de ese subdominio.

Inicie sesión en el registrador de dominios y cree un registro `CNAME` para señalar el nombre de dominio personalizado al destino, como en la tabla siguiente.

| CNAME | Punto de nombre de dominio personalizado en Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Registro Apex {#apex-record}

Un dominio Apex es un dominio personalizado que no contiene un subdominio, como `example.com`. Un dominio Apex está configurado con un registro `A`, `ALIAS` o `ANAME` a través de su proveedor DNS. Los dominios Apex deben apuntar a direcciones IP específicas.

Agregue todo lo siguiente `A` registra la configuración DNS de su dominio a través de su proveedor de dominios.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
