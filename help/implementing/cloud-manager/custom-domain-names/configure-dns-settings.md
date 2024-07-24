---
title: Configuración de DNS
description: Obtenga información sobre cómo configurar DNS para que sus nombres de dominio personalizados permitan que su sitio sirva a los visitantes.
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 49%

---


# Configuración de DNS {#configure-dns}

Una vez que el nombre de dominio personalizado se haya [verificado e implementado correctamente](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md), estará listo para actualizar los registros DNS del nombre de dominio personalizado con el proveedor DNS. Al hacerlo, el sitio puede servir a los visitantes. Por lo tanto, esta actividad se suele realizar antes de activarse.

## ¿Qué es la configuración de DNS? {#dns-settings}

Un registro `CNAME` o A, una vez aprovisionado, enrutará todo el tráfico de Internet para el dominio a donde señale. Se produce una interrupción si esa ubicación no está preparada para abastecer el tráfico. Si no se ha probado, puede haber errores en el contenido. Esta es la razón por la que este paso siempre se realiza una vez finalizada la prueba y está listo para su lanzamiento.

Para establecer esta configuración, debe determinar si se debe configurar un registro `CNAME` o Apex para que apunte el nombre de dominio personalizado al nombre de dominio de Cloud Manager. Las siguientes secciones de este documento le ayudarán a determinar qué tipo de registro es apropiado para su configuración de DNS.

## Requisitos  {#requirements}

Debe cumplir estos requisitos antes de configurar los registros DNS.

* Debe identificar su host de dominio o registrador si aún no lo conoce.
* Debe poder editar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Ya debe haber comprobado el nombre de dominio personalizado configurado tal como se describe en el documento [Comprobación del estado del nombre de dominio.](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)

## Registro CNAME {#cname-record}

Un nombre canónico o registro CNAME es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com` al dominio que hospeda el contenido de ese subdominio.

Inicie sesión en el registrador de dominios y cree un registro `CNAME` para señalar el nombre de dominio personalizado al destino, como en la tabla siguiente.

| CNAME | Punto de nombre de dominio personalizado en Target |
|--- |--- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

## Registro Apex {#apex-record}

Un dominio Apex es un dominio personalizado que no contiene un subdominio, como `example.com`. Un dominio Apex está configurado con un registro `A`, `ALIAS` o `ANAME` a través de su proveedor DNS. Los dominios Apex deben apuntar a direcciones IP específicas.

Agregue los siguientes `A` registros a la configuración DNS de su dominio a través de su proveedor de dominios.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## Siguientes pasos {#next-steps}

Una vez configurados los registros DNS para el nombre de dominio personalizado, deberá comprobar esa configuración en Cloud Manager. Continúe con el documento [Comprobando el estado del registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) para finalizar su nombre de dominio personalizado.
