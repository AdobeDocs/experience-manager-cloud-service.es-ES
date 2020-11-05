---
title: Comprobación del estado del nombre de dominio
description: Comprobación del estado del nombre de dominio
translation-type: tm+mt
source-git-commit: 5cd22d8af20bb947e4cdab448cf8f20c6596bb2e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---


# Comprobación del estado del nombre de dominio {#check-status}

Puede determinar si el nombre de dominio se ha comprobado correctamente haciendo clic en el icono Estado del nombre de dominio en la tabla de Entornos de la página Configuración de dominio.

>[!NOTE]
>Cloud Manager activará automáticamente una verificación TXT cuando seleccione Guardar en el paso de verificación del asistente Añadir dominio personalizado. Para las verificaciones posteriores, debe seleccionar activamente el icono &quot;verificar de nuevo&quot; junto al estado. INSERTAR IMAGEN

Cloud Manager verificará la propiedad del dominio mediante el valor TXT y mostrará uno de los siguientes mensajes de estado:

* **Error** de comprobación de dominio Falta el valor TXT o se detecta con errores. Siga las instrucciones y vuelva a intentarlo. Cuando esté listo, debe seleccionar el icono &#39;verificar nuevamente&#39; junto al estado.

* **Verificación del dominio en curso** Verificación en curso. Este estado suele aparecer después de seleccionar el icono &quot;verificar nuevamente&quot; junto al estado.

* **Se ha verificado que la verificación de TXT ha fallado** la implementación. Sin embargo, la implementación de CDN falló. Se notificará automáticamente a un representante de Adobe.

* **Dominio verificado e implementado** Este estado indica que el nombre de dominio personalizado está listo para usarse. Nota: En este punto, el nombre de dominio personalizado está listo para la prueba y se le dirigirá al nombre de dominio de Cloud Manager. Vaya a Configuración de DNS INSERT LINK para aprender a hacer esto.

* **Se está eliminando** la eliminación del nombre de dominio personalizado.

* **Error** al eliminar el nombre de dominio personalizado. Debe volver a intentarlo. Vaya a Eliminar nombre de dominio personalizado para obtener más información sobre el tema.


## Configuración de la configuración DNS {#configure-dns}

Una vez que el nombre de dominio personalizado se haya verificado e implementado correctamente, estará listo para actualizar los registros DNS del nombre de dominio personalizado con su proveedor DNS. Al hacerlo, el sitio puede servir visitantes. Por lo tanto, esta actividad se realiza normalmente antes de Go-live.

>[!NOTE]
>Usted o la persona adecuada de su organización deben poder iniciar sesión o ponerse en contacto con su proveedor DNS (la compañía a la que compró el dominio) y realizar actualizaciones en la configuración DNS.

Para ello, debe determinar si debe configurar la configuración de DNS en un registro `CNAME` o Apex que señale su nombre de dominio personalizado al nombre de dominio del Administrador de la nube. Un registro `CNAME` o un registro A, una vez aprovisionado, enrutará todo el tráfico de Internet para el dominio a donde esté apuntando. Si esa ubicación no está aprovisionada para atender el tráfico, habrá una interrupción. Si no se ha probado, puede que haya errores en el contenido. Por este motivo, este paso siempre se realiza una vez finalizada la prueba y el cliente está listo para Go-live.

### Registro CNAME {#cname-record}

Las siguientes secciones le ayudarán a determinar qué tipo de registro es adecuado para su configuración DNS.

Un nombre o `CNAME` registro canónico es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME suelen utilizarse para asignar un subdominio, como `www.example.com` el dominio que aloja el contenido de ese subdominio.

Inicie sesión en el Registrador de dominios y cree un registro CNAME para señalar el nombre de dominio personalizado al destinatario como se muestra a continuación:

| CNAME | Destinatario del punto de nombre de dominio personalizado |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

### Registro APEX {#apex-record}

Un dominio apex es un dominio personalizado que no contiene un subdominio, como ejemplo.com. Un dominio apex se configura con un `A` , `ALIAS` o `ANAME` registro a través de su proveedor DNS. Los dominios Apex deben apuntar a direcciones IP específicas.

Añada todos los siguientes registros A a la configuración DNS de su dominio a través de su proveedor de dominio:

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## Comprobación del estado del registro DNS {#check-status-dns-record}

Para determinar si el nombre de dominio se resuelve correctamente en el AEM como sitio web de un Cloud Service, haga clic en el icono Estado del registro DNS en la tabla de los Entornos de la página Configuración de dominio. Cloud Manager realiza una búsqueda DNS del nombre de dominio y muestra uno de los siguientes mensajes de estado:

>[!NOTE]
>El Administrador de nube activará automáticamente una búsqueda DNS cuando el nombre de dominio personalizado se verifique e implemente por primera vez correctamente. Para los intentos subsiguientes, debe seleccionar activamente el icono **resolver de nuevo** junto al estado. INSERTAR IMAGEN

* **No se detectará** el estado DNS hasta que el nombre de dominio personalizado se haya verificado e implementado correctamente. Este estado también se observa cuando el nombre de dominio personalizado se está eliminando.

* **DNS resuelve incorrectamente** Indica que la configuración de registros DNS no se ha resuelto/señalado o es errónea. Se notificará automáticamente a un representante de Adobe.

   >[!NOTE]
   >Debe configurar un `CNAME` o `A-record` siguiendo las instrucciones correspondientes. Vaya a Configuración de DNS INSERT LINK para obtener más información sobre el tema. Cuando esté listo, debe seleccionar el icono &#39;resolver de nuevo&#39; junto al estado.

* **La resolución de DNS en curso** está en curso. Este estado suele aparecer después de seleccionar el icono &quot;resolver nuevamente&quot; junto al estado.

* **Resoluciones DNS Correctamente** La configuración de DNS está correctamente configurada. Su sitio está sirviendo visitantes.
