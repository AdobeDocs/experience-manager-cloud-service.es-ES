---
title: Comprobación del estado del nombre de dominio
description: Comprobación del estado del nombre de dominio
translation-type: tm+mt
source-git-commit: 91b06bcd96fe8a37c3fb20ef90e1684f6d19183f
workflow-type: tm+mt
source-wordcount: '519'
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
