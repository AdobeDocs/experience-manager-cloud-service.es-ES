---
title: 'Configuración de DNS '
description: Configuración de DNS
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 016954bc712a135886a6031deba05d92e7d5099c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 6%

---

# Configuración de DNS {#configure-dns}

Una vez que el nombre de dominio personalizado se haya verificado e implementado correctamente, podrá actualizar los registros DNS del nombre de dominio personalizado con el proveedor DNS. Al hacerlo, el sitio puede servir a los visitantes. Por lo tanto, esta actividad suele realizarse antes de Go-live.

>[!NOTE]
>Usted o la persona adecuada de su organización deben poder iniciar sesión o ponerse en contacto con su proveedor de DNS (la empresa desde la que compró el dominio) y realizar actualizaciones en la configuración de DNS.

Para ello, debe determinar si debe configurar la configuración de DNS en una `CNAME` o el registro Apex que señala su nombre de dominio personalizado al nombre de dominio de Cloud Manager. A `CNAME` O Un registro, una vez aprovisionado, enrutará todo el tráfico de Internet para el dominio a donde señale. Si esa ubicación no está aprovisionada para servir el tráfico, se producirá una interrupción. Si no se ha probado, puede haber errores en el contenido. Esta es la razón por la que este paso siempre se realiza una vez finalizada la prueba y el cliente está listo para Go-live.

Los pasos siguientes deben completarse como se indica en la tabla siguiente:

| Etapa |  | Responsabilidad | Más información |
|--- |--- |--- |---|
| Añadir certificado SSL | Añadir certificado SSL | Cliente | [Adición de un certificado SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Verificación del dominio | Añadir registro TXT | Cliente | [Adición de un registro TXT](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Revisar estado de verificación del dominio |  | Cliente |  |
|  | Estado: Error de verificación del dominio | Cliente | [Comprobación del estado del nombre de dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Estado: Verificado, Error De Implementación | Representante del Adobe de contacto | [Comprobación del estado del nombre de dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Agregar registros DNS que apunten a AEM as a Cloud Service agregando registros CNAME o APEX | Configuración de DNS | Cliente | [Configuración de DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Comprobar estado de registro DNS |  | Cliente | [Comprobación del estado de registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Estado: No se ha detectado el estado DNS | Cliente | [Comprobación del estado de registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Estado: El DNS se resuelve incorrectamente | Cliente |  |


## Registro CNAME {#cname-record}

Las siguientes secciones le ayudarán a determinar qué tipo de registro es apropiado para su configuración DNS.

Un nombre canónico o `CNAME` record es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com`  al dominio que hospeda el contenido de ese subdominio.

Inicie sesión en el Registrador de dominios y cree un registro CNAME para señalar su nombre de dominio personalizado al destino, como se muestra a continuación:

| CNAME | Punto de nombre de dominio personalizado en Target |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## Registro APEX {#apex-record}

Un dominio apex es un dominio personalizado que no contiene un subdominio, como ejemplo.com. Un dominio de apex está configurado con un `A` , `ALIAS` o `ANAME` registre a través de su proveedor DNS. Los dominios de Apex deben apuntar a direcciones IP específicas.

Agregue todos los siguientes registros A a la configuración DNS de su dominio a través del proveedor de dominios:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
