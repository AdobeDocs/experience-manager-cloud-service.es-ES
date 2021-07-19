---
title: Adición de un nombre de dominio personalizado
description: Adición de un nombre de dominio personalizado
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Adición de un nombre de dominio personalizado {#adding-cdn}

Un usuario debe ser propietario empresarial o administrador de implementación para poder agregar un nombre de dominio personalizado en Cloud Manager.

## Consideraciones importantes {#important-considerations}

* Antes de agregar un nombre de dominio personalizado, debe instalarse en el programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte [Adición de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización en ejecución asociada a esos entornos.

* Solo se puede agregar un nombre de dominio a la vez. Sin embargo, los dominios no pueden contener comodines. Los dominios personalizados del lado del autor no son compatibles.

* AEM como Cloud Service no admite dominios comodín.

* Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno.

* No se puede usar el mismo nombre de dominio en más de un entorno.

## Adición de un nombre de dominio personalizado desde la página Configuración de dominio {#adding-cdn-settings}

Siga los pasos a continuación para agregar un nombre de dominio personalizado desde la página Configuración de dominio :

1. Vaya a la pantalla **Environments** desde la página **Overview**.

1. Haga clic en **Configuración de dominio** en el menú de navegación de la izquierda.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Haga clic en el botón **Agregar dominio** para abrir el cuadro de diálogo **Agregar nombre de dominio**.

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Introduzca el nombre de dominio personalizado en **Domain Name**.

   >[!NOTE]
   >No debe incluir `http://`, `https://` ni espacios al introducir en el dominio.

1. Seleccione el **Entorno** cuyo servicio de publicación estará asociado con el nombre de dominio.

1. Seleccione el servicio como **Publish** o **Preview**.

   >[!NOTE]
   >Los nombres de dominio personalizados ahora se admiten en los programas de Cloud Manager para sitios tanto para los servicios de publicación como de vista previa. Cada entorno de Cloud Manager puede alojar hasta un máximo de 250 dominios personalizados por entorno. Para obtener más información sobre el servicio de vista previa, consulte [Servicio de vista previa](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. Seleccione el **Domain SSL Certificate** en la lista desplegable y seleccione **Continue**.

1. **Aparece el cuadro de diálogo Agregar** nombre de dominio . Esto lo llevará a la pantalla Verificación del nombre de dominio para su entorno . Consulte [Adición de un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información.

   Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno:

1. Haga clic en **Crear**.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica con el estado **Verificado e implementado**.
Vaya a [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y cómo hacerlo.

   >[!NOTE]
   >La prueba de DNS puede tardar hasta unas horas en reconocerse, debido a los retrasos de propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más información.

## Adición de un nombre de dominio personalizado desde la página Entornos {#adding-cdn-environments}

1. Vaya a la página Detalles de entornos para el entorno de interés.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilice los campos de entrada de la parte superior de la tabla Nombres de dominio para enviar el nombre de dominio personalizado y seleccionar el certificado SSL en la lista desplegable. Haga clic en **+ Agregar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Compruebe los campos en el cuadro de diálogo **Add Domain Name** y haga clic en **Continue**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >No incluya `http://`, `https://` ni espacios al introducir en su dominio.

1. Se muestra la pantalla Verificación del nombre de dominio para el entorno .

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Consulte [Verificación del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información. Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno.

1. Haga clic en **Crear**.

1. La implementación del nombre de dominio personalizado requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica con el estado **Verificado e implementado**.

En este punto, su nombre de dominio personalizado está listo para la prueba y un `CNAME` para apuntarlo. Consulte [Estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y la dirección.

>[!NOTE]
>La prueba de DNS puede tardar hasta unas horas en reconocerse, debido a los retrasos de propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más información.
