---
title: Adición de un nombre de dominio personalizado
description: Obtenga información sobre cómo agregar un nombre de dominio personalizado mediante Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Adición de un nombre de dominio personalizado {#adding-cdn}

Puede agregar un nombre de dominio personalizado desde dos ubicaciones en Cloud Manager:

* [Desde la página Configuración de dominio](#adding-cdn-settings)
* [Desde la página Entornos](#adding-cdn-environments)

>[!NOTE]
>
>Un usuario debe tener la variable **Propietario empresarial** o **Administrador de implementación** para agregar un nombre de dominio personalizado en Cloud Manager

## Adición de un nombre de dominio personalizado desde la página Configuración de dominio {#adding-cdn-settings}

Siga estos pasos para agregar un nombre de dominio personalizado desde el **Configuración de dominio** página.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Entornos** de la **Información general** página.

1. Haga clic en **Configuración de dominio** en el panel de navegación izquierdo.

   ![La ventana Configuración de dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Haga clic en el **Agregar dominio** en la parte superior derecha para abrir **Agregar nombre de dominio** diálogo.

   ![Cuadro de diálogo Agregar dominio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. Escriba el nombre de dominio personalizado en la variable **Nombre de dominio** campo .

   >[!NOTE]
   >
   >No incluir `http://`, `https://`o espacios al introducir en el dominio.

1. Seleccione el **Entorno** cuyo servicio se asociará con el nombre de dominio.

1. Seleccione o bien **Publicación** o **Vista previa** servicio.

1. Seleccione el **Certificado SSL de dominio** asociado al nombre de dominio en la lista desplegable y seleccione **Continuar**.

1. La variable **Agregar nombre de dominio** y le llevará al proceso de verificación del nombre de dominio. Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno. Haga clic en **Crear**.

   ![Verificación del nombre del dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.

Consulte el documento [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y cómo abordar los problemas potenciales.

>[!NOTE]
>
>La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.
>
>Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte el documento [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.

>[!TIP]
>
>Consulte [Adición de un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información sobre los registros TXT.

## Adición de un nombre de dominio personalizado desde la página Entornos {#adding-cdn-environments}

Siga estos pasos para agregar un nombre de dominio personalizado desde el **Entornos** página.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a **Detalle de entornos** para el entorno de interés.

   ![Introducción del nombre de dominio en la página Detalles del entorno](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilice la variable **Nombres de dominio** para enviar el nombre de dominio personalizado.

   1. Introduzca el nombre de dominio personalizado.
   1. Seleccione el certificado SSL asociado a este nombre en la lista desplegable.
   1. Haga clic en **+Añadir**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Compruebe los valores seleccionados en la variable **Agregar nombre de dominio** y haga clic en **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >No incluir `http://`, `https://`o espacios al introducir en el nombre de dominio.

1. La variable **Agregar nombre de dominio** y le llevará al proceso de verificación del nombre de dominio. Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno. Haga clic en **Crear**.

   ![Verificación del nombre del dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.

Consulte el documento [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y cómo abordar los problemas potenciales.

>[!NOTE]
>
>La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.
>
>Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte el documento [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.

>[!TIP]
>
>Consulte [Adición de un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información sobre los registros TXT.
