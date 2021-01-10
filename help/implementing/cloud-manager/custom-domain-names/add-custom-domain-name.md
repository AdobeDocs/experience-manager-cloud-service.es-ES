---
title: Añadir un nombre de dominio personalizado
description: Añadir un nombre de dominio personalizado
translation-type: tm+mt
source-git-commit: b336f361b496b672d26a5316952ee52ce828e201
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# Añadir un nombre de dominio personalizado {#adding-cdn}

Un usuario debe ser propietario de una empresa o administrador de implementación para poder agregar un nombre de dominio personalizado en Cloud Manager.

## Consideraciones importantes {#important-considerations}

* Antes de agregar un nombre de dominio personalizado, se debe instalar en el Programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte [Añadir un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización en ejecución asociada a esos entornos.

* Solo se puede agregar un nombre de dominio a la vez. Sin embargo, los dominios no pueden contener caracteres comodín. No se admiten los dominios personalizados del lado del autor.

* Cada Entorno de Cloud Manager puede alojar hasta un máximo de 100 dominios personalizados por entorno.

* El mismo nombre de dominio no se puede usar en más de un entorno.

## Añadir un nombre de dominio personalizado de la página Configuración de dominio {#adding-cdn-settings}

Siga los pasos a continuación para agregar un nombre de dominio personalizado desde la página Configuración de dominio:

1. Vaya a la pantalla **Entornos** desde la página **Información general**.

1. Haga clic en **Configuración de dominio** en el menú de navegación de la izquierda.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Haga clic en el botón **Añadir dominio** para abrir el cuadro de diálogo **Añadir nombre de dominio**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. Escriba el nombre de dominio personalizado en **Nombre de dominio**.

   >[!NOTE]
   >No debe incluir `http://`, `https://` ni espacios al ingresar en el dominio.

1. Seleccione el **Entorno** cuyo servicio de publicación se asociará con el nombre de dominio.

1. Seleccione el **Certificado SSL de dominio** en la lista desplegable y seleccione **Continuar**.

1. **Aparece el cuadro de diálogo añadir** nombre de dominio. Esto lo llevará a la pantalla Verificación del nombre de dominio para su Entorno. Consulte [Añadir un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información.
Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno.

1. Haga clic en **Crear**.
1. La implementación de CDN requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.
Vaya a [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información acerca de los distintos estados y la dirección.

   >[!NOTE]
   >La prueba de DNS puede tardar hasta unas horas en reconocerse debido a retrasos en la propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado, que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más detalles.

## Añadir un nombre de dominio personalizado de la página Entornos {#adding-cdn-environments}

1. Acceda a la página Detalles de Entornos para ver el entorno de intereses.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilice los campos de entrada en la parte superior de la tabla Nombres de dominio para enviar el nombre de dominio personalizado y seleccionar el certificado SSL en la lista desplegable. Haga clic en **+ Añadir**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. Marque los campos en el cuadro de diálogo **Añadir nombre de dominio** y haga clic en **Continuar**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >No incluya `http://`, `https://` ni espacios al ingresar en el dominio.

1. Se abre la pantalla Verificación del nombre de dominio para el Entorno.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   Consulte [Verificación del dominio](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información. Siga las instrucciones proporcionadas para probar la propiedad del dominio para su entorno.

1. Haga clic en **Crear**.

1. La implementación del nombre de dominio personalizado requiere un certificado SSL válido y una verificación TXT correcta. Esto se indica por estado **Verificado e implementado**.

En este punto, el nombre de dominio personalizado está listo para la prueba y `CNAME` para señalarlo. Consulte [Estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre los distintos estados y la forma de direccionar.

>[!NOTE]
>La prueba de DNS puede tardar hasta unas horas en reconocerse debido a retrasos en la propagación de DNS. Cloud Manager verificará la propiedad y actualizará el estado, que se puede ver en la tabla de configuración de dominio. Consulte Comprobación del estado del nombre de dominio para obtener más información.
