---
title: Agregar un nombre de dominio personalizado
description: Obtenga información sobre cómo agregar un nombre de dominio personalizado mediante Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 27%

---


# Agregar un nombre de dominio personalizado {#adding-cdn}

Obtenga información sobre cómo agregar un nombre de dominio personalizado mediante Cloud Manager.

## Requisitos  {#requirements}

Complete estos requisitos antes de agregar un nombre de dominio personalizado en Cloud Manager.

* Debe haber agregado un certificado SSL de dominio para el dominio que desea agregar antes de agregar un nombre de dominio personalizado como se describe en el documento [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Debe tener la función **Propietario del negocio** o **Administrador de implementación** para agregar un nombre de dominio personalizado en Cloud Manager.
* Utilice la CDN de Fastly.

## Dónde agregar nombres de dominio personalizados {#where}

Puede agregar un nombre de dominio personalizado desde dos ubicaciones en Cloud Manager:

* [Desde la página Configuración de dominio](#adding-cdn-settings)
* [Desde la página Entornos](#adding-cdn-environments)

Al agregar un nombre de dominio personalizado, el dominio se proporciona utilizando el certificado más específico y válido. Si varios certificados tienen el mismo dominio, se elige el actualizado más recientemente. El Adobe recomienda administrar los certificados de modo que no haya dominios superpuestos.

Los pasos descritos en este documento se basan en Fastly. Si ha utilizado una CDN diferente, configure el dominio con la CDN que ha elegido utilizar.

## Agregar un nombre de dominio personalizado desde la página Configuración de dominio {#adding-cdn-settings}

Siga estos pasos para agregar un nombre de dominio personalizado desde la página **Configuración de dominio**.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Vaya a la pestaña **Configuración de dominio** del panel de navegación izquierdo.

   ![La ventana Configuración de dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Haga clic en el botón **Agregar dominio** en la parte superior derecha para abrir el cuadro de diálogo **Agregar nombre de dominio**.

   ![Cuadro de diálogo Agregar dominio](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. En la ficha **Nombre de dominio**, escriba el nombre de dominio personalizado en el campo **Nombre de dominio**.

   >[!NOTE]
   >
   >No incluya `http://`, `https://` ni espacios al introducir el dominio.

1. Seleccione el **entorno** cuyo servicio se asocia con el nombre de dominio.

1. Seleccione el servicio **Publicación** o **Vista previa**.

1. Seleccione el **Certificado SSL de dominio** asociado al nombre de dominio en la lista desplegable y seleccione **Continuar**.

1. Aparecerá la ficha **Verificación**.

   ![Verificación del nombre del dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * La ficha **Verificación** describe los pasos siguientes para configurar el nombre de dominio personalizado, que está creando un registro TXT necesario.
   * Puede realizar este paso inmediatamente (antes de hacer clic en **Crear** en el cuadro de diálogo) o después de hacer clic en **Crear** en el cuadro de diálogo.
   * A continuación se describen las opciones y los pasos siguientes.

1. Haga clic en **Crear** para guardar el nombre de dominio personalizado en Cloud Manager.

Cuando selecciona **Crear** en el asistente **Agregar dominio personalizado**, Cloud Manager déclencheur una verificación TXT. Cree el registro TXT al configurar el nombre de dominio personalizado en Cloud Manager. Sin embargo, este paso no es obligatorio. Para las verificaciones posteriores, debe seleccionar el icono **Verificar de nuevo** junto al estado.

El nombre no estará activo hasta que Cloud Manager verifique que se ha añadido y verificado la entrada TXT. El estado de **Verificado e implementado** indica que la verificación TXT se realizó correctamente.

* Consulte [Agregar un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para obtener más información sobre los registros TXT.
* Consulte [Comprobar el estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información sobre cómo Cloud Manager verifica el nombre de dominio personalizado y su entrada TXT.

## Pasos siguientes {#next-steps}

Después de crear el nombre de dominio personalizado en Cloud Manager, agregue una entrada TXT para comprobar la propiedad del dominio. Continúe con el documento [Agregar un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) para continuar configurando el nombre de dominio personalizado.

## Agregar un nombre de dominio personalizado desde la página Entornos {#adding-cdn-environments}

Los pasos para agregar un nombre de dominio personalizado desde la página **Entornos** son los mismos que cuando [agrega un nombre de dominio personalizado desde la página Configuración de dominio](#adding-cdn-settings), pero el punto de entrada difiere. Siga estos pasos para agregar un nombre de dominio personalizado desde la página **Entornos**.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la página **Detalles de entornos** para el entorno de interés.

   ![Introducción del nombre de dominio en la página Detalles del entorno](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilice la variable **Nombres de dominio** para enviar el nombre de dominio personalizado.

   1. Introduzca el nombre de dominio personalizado.
   1. Seleccione el certificado SSL asociado a este nombre en la lista desplegable.
   1. Haga clic en **+Agregar**.

   ![Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. El cuadro de diálogo **Agregar nombre de dominio** se abre a la ficha **Nombre de dominio**. Continúe como lo haría para [agregar un nombre de dominio personalizado desde la página Configuración de dominio](#adding-cdn-settings).
