---
title: Concesión de acceso al desarrollador front-end
description: Incorpore a los desarrolladores front-end en Cloud Manager para que tengan acceso al repositorio de Git y a la canalización del sitio de AEM.
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 91%

---

# Concesión de acceso al desarrollador front-end {#grant-fed-access}

Incorpore a los desarrolladores front-end en Cloud Manager para que tengan acceso al repositorio de Git y a la canalización del sitio de AEM.

## La historia hasta ahora {#story-so-far}

En el documento anterior del Recorrido de creación rápida de sitios de AEM, [Configuración de la canalización,](pipeline-setup.md) ha aprendido a crear una canalización front-end para administrar la personalización del tema de su sitio y ahora debería hacer lo siguiente:

* Comprender qué es una canalización front-end.
* Saber cómo configurar una canalización front-end en Cloud Manager.

Ahora debe otorgar a su desarrollador front-end acceso a Cloud Manager a través del proceso de incorporación para que pueda entrar en el repositorio de Git de AEM y a la canalización que ha creado.

## Objetivo {#objective}

El proceso de conceder acceso a Cloud Manager y asignar funciones de usuario a los usuarios se llama “incorporación”. En este documento se ofrece una descripción general de los pasos más importantes para incorporar a un desarrollador front-end y, después de leerlo, sabrá lo siguiente:

* Cómo añadir un desarrollador front-end como usuario.
* Cómo conceder las funciones necesarias al desarrollador front-end.

>[!TIP]
>
>Si necesita detalles adicionales acerca del proceso, hay un recorrido de documentación completo dedicado a la incorporación de su equipo en AEM as a Cloud Service, en la [sección Recursos adicionales](#additional-resources) de este documento.

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica al administrador de Cloud Manager.

## Requisitos  {#requirements}

* Debe ser miembro de la función **Propietario de la empresa** en Cloud Manager.
* Debe ser **Administrador de sistemas** en Cloud Manager.
* Debe tener acceso a Admin Console.

## Adición del desarrollador front-end como usuario {#add-fed-user}

En primer lugar, debe añadir al desarrollador front-end como usuario mediante Admin Console.

1. Inicie sesión en Admin Console en [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).

1. Una vez que haya iniciado sesión, aparecerá una página de información general similar a la de la siguiente imagen.

   ![Información general de Admin Console](assets/admin-console.png)

1. Asegúrese de que está en la organización adecuada: compruebe el nombre en la esquina superior derecha de la pantalla.

   ![Comprobación del nombre de la organización](assets/correct-org.png)

1. Seleccione **Adobe Experience Manager as a Cloud Service** en la tarjeta **Productos y servicios**.

   ![Seleccione AEMaaCS](assets/select-aemaacs.png)

1. Verá la lista de perfiles de producto preconfigurados de Cloud Manager. Si no ve estos perfiles, póngase en contacto con el administrador de Cloud Manager, ya que es posible que no tenga los permisos correctos en su organización.

   ![Perfiles de producto](assets/product-profiles.png)

1. Para asignar al desarrollador front-end a los perfiles correctos, seleccione la **Usuarios** y, a continuación, la **Añadir usuario** botón.

   ![Adición del usuario](assets/add-user.png)

1. En el cuadro de diálogo **Añadir usuarios a su equipo**, escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

   ![Adición de un usuario al equipo](assets/add-to-team.png)

1. En el **Product** , seleccione el signo más y, a continuación, seleccione **Adobe Experience Manager as a Cloud Service** y asigne el **Administrador de implementación** y **Desarrollador** perfiles de producto para el usuario.

   ![Asignación de perfiles de equipo](assets/assign-team.png)

1. Seleccionar **Guardar** y se enviará un correo electrónico de bienvenida al desarrollador front-end que añadió como usuario.

El desarrollador front-end invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

## Envío al desarrollador front-end {#handover}

Una vez que la invitación a Cloud Manager enviada por correo electrónico al desarrollador front-end esté en camino, usted y el administrador de AEM pueden proporcionarle el resto de la información necesaria para comenzar la personalización.

* Una [ruta al contenido habitual](#example-page)
* La fuente del tema que [ha descargado](#download-theme)
* Las [credenciales de usuario de proxy](#proxy-user)
* El nombre del programa o la URL a este [copiados de Cloud Manager](pipeline-setup.md#login)
* Los requisitos del diseño front-end

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del Recorrido de creación rápida de sitios de AEM, debería saber lo siguiente:

* Cómo añadir un desarrollador front-end como usuario.
* Cómo conceder las funciones necesarias al desarrollador front-end.

Aproveche este conocimiento y continúe con su Recorrido de creación rápida de sitios de AEM. Revise el documento [Recuperación de información de acceso al repositorio de Git,](retrieve-access.md) que cambia la perspectiva exclusivamente al desarrollador front-end y explica cómo usa Cloud Manager para acceder a la información del repositorio de Git.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del Recorrido de creación rápida de sitios de AEM al revisar el documento [Recuperación de credenciales de desarrollador front-end,](retrieve-access.md) los siguientes son algunos recursos opcionales extra. Profundizan en varios conceptos mencionados en este documento, pero no son necesarios para continuar el recorrido.

* [Recorrido de incorporación](/help/journey-onboarding/overview.md): esta guía sirve como punto de partida para garantizar que sus equipos estén configurados y tengan acceso a AEM as a Cloud Service.
