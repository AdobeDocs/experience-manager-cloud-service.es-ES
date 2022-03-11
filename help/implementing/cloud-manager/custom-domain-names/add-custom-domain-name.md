---
title: Adición de un nombre de dominio personalizado
description: Adición de un nombre de dominio personalizado
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 4%

---

# Adición de un nombre de dominio personalizado {#adding-cdn}

Un usuario debe ser propietario empresarial o administrador de implementación para poder agregar un nombre de dominio personalizado en Cloud Manager.

Los pasos siguientes deben completarse como se indica en la tabla siguiente:

| Etapa |  | Responsabilidad | Más información |
|--- |--- |--- |---|
| Agregar certificado SLL | Agregar certificado SLL | Cliente | [Adición de un certificado SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| Verificación del dominio | Añadir registro TXT | Cliente | [Adición de un registro TXT](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| Revisar estado de verificación del dominio |  | Cliente |  |
|  | Estado: Error de verificación del dominio | Cliente | [Comprobación del estado del nombre de dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | Estado: Verificado, Error De Implementación | Representante del Adobe de contacto | [Comprobación del estado del nombre de dominio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| Agregar registros DNS que apunten a AEM as a Cloud Service agregando registros CNAME o APEX | Configuración de DNS | Cliente | [Configuración de DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| Comprobar estado de registro DNS |  | Cliente | [Comprobación del estado de registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Estado: No se ha detectado el estado DNS | Cliente | [Comprobación del estado de registro DNS](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | Estado: El DNS se resuelve incorrectamente | Cliente |  |


## Consideraciones importantes {#important-considerations}

* Antes de agregar un nombre de dominio personalizado, debe instalarse en el programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte [Adición de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización en ejecución asociada a esos entornos.

* Solo se puede agregar un nombre de dominio a la vez. Los dominios personalizados del lado del autor no son compatibles.

* AEM as a Cloud Service no admite dominios comodín.

* Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno.

* No se puede usar el mismo nombre de dominio en más de un entorno.

## Adición de un nombre de dominio personalizado desde la página Configuración de dominio {#adding-cdn-settings}

Siga los pasos a continuación para agregar un nombre de dominio personalizado desde la página Configuración de dominio :

1. Vaya a **Entornos** pantalla de **Información general** página.

1. Haga clic en **Configuración de dominio** en el menú de navegación de la izquierda.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Haga clic en **Agregar dominio** botón para abrir **Agregar nombre de dominio** para abrir el Navegador.

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Escriba el nombre de dominio personalizado en **Nombre de dominio**.

   >[!NOTE]
   >No debe incluir `http://`, `https://`o espacios al introducir en el dominio.

1. Seleccione el **Entorno** cuyo servicio de publicación se asociará con el nombre de dominio.

1. Seleccione el servicio como **Publicación** o **Vista previa**.

   >[!NOTE]
   >Los nombres de dominio personalizados ahora se admiten en los programas de Cloud Manager para sitios tanto para los servicios de publicación como de vista previa. Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno. Para obtener más información sobre el servicio de vista previa, consulte [Servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. Seleccione el **Certificado SSL de dominio** en la lista desplegable y seleccione **Continuar**.

1. **Agregar nombre de dominio** aparece en el cuadro de diálogo. Esto lo llevará a la pantalla Verificación del nombre de dominio para su entorno . Consulte [Adición de un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información.

   Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno:

1. Haga clic en **Crear**.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.
Vaya a [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y cómo abordarlos.

   >[!NOTE]
   >La prueba de DNS puede tardar hasta unas horas en reconocerse, debido a los retrasos de propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más información.

## Adición de un nombre de dominio personalizado desde la página Entornos {#adding-cdn-environments}

1. Vaya a la página Detalles de entornos para el entorno de interés.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilice los campos de entrada de la parte superior de la tabla Nombres de dominio para enviar el nombre de dominio personalizado y seleccionar el certificado SSL en la lista desplegable. Haga clic en **+ Agregar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Compruebe los campos en el **Agregar nombre de dominio** y haga clic en **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >No incluir `http://`, `https://`o espacios al introducir en el dominio.

1. Se muestra la pantalla Verificación del nombre de dominio para el entorno .

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Consulte [Verificación del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información. Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno.

1. Haga clic en **Crear**.

1. La implementación del nombre de dominio personalizado requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.

En este punto, su nombre de dominio personalizado está listo para realizar pruebas y un `CNAME` para señalarlo. Consulte [Estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y cómo abordarlos.

>[!NOTE]
>La prueba de DNS puede tardar hasta unas horas en reconocerse, debido a los retrasos de propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más información.
