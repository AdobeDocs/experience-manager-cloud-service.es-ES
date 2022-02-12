---
title: Administrar extremos de GraphQL en AEM
description: Aprenda a administrar los extremos de GraphQL en Adobe Experience Manager as a Cloud Service para la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
source-git-commit: 4e37db128aa31d6e8e950be0d077eae921a27468
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---


# Administrar extremos de GraphQL en AEM {#graphql-aem-endpoint}

El punto final es la ruta utilizada para acceder a GraphQL para AEM. Al utilizar esta ruta, usted (o su aplicación) pueden:

* acceder al esquema de GraphQL,
* envíe sus consultas de GraphQL,
* reciba las respuestas (a sus consultas de GraphQL).

Hay dos tipos de extremos en AEM:

* Global
   * Disponible para su uso en todos los sitios.
   * Este extremo puede utilizar todos los modelos de fragmento de contenido de todas las configuraciones de sitios (definidas en la variable [Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
   * Si hay algún modelo de fragmento de contenido que debería compartirse entre las configuraciones de Sitios, estos deberían crearse en las configuraciones globales de Sitios.
* Configuraciones de sitios:
   * Corresponde a una configuración de Sites, tal como se define en la variable [Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * Específico de un sitio o proyecto especificado.
   * Un extremo específico de la configuración de Sitios usará los modelos de fragmento de contenido de esa configuración de Sitios específica junto con los de la configuración de Sitios global.

>[!CAUTION]
>
>El editor de fragmentos de contenido puede permitir que un fragmento de contenido de una configuración de sitios haga referencia a un fragmento de contenido de otra configuración de sitios (a través de políticas).
>
>En tal caso, no todo el contenido se podrá recuperar mediante un punto final específico de configuración de Sites.
>
>El autor del contenido debe controlar este escenario; por ejemplo, puede resultar útil considerar la posibilidad de colocar los modelos de fragmento de contenido compartido en la configuración de sitios globales.

La ruta del repositorio de GraphQL para AEM punto final global es:

`/content/cq:graphql/global/endpoint`

Para el cual su aplicación puede utilizar la siguiente ruta en la dirección URL de la solicitud:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar un punto final para GraphQL para AEM, debe:

* [Habilitar el extremo de GraphQL](#enabling-graphql-endpoint)
* [Publicar el extremo de GraphQL](#publishing-graphql-endpoint)

## Activación del extremo de GraphQL {#enabling-graphql-endpoint}

Para habilitar un extremo de GraphQL, primero debe tener una configuración adecuada. Consulte [Fragmentos de contenido: navegador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Si la variable [no se ha habilitado el uso de modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-configuration-browser.md), el **Crear** no estará disponible.

Para habilitar el punto final correspondiente:

1. Vaya a **Herramientas**, **Recursos** y, a continuación, seleccione **GraphQL**.
1. Seleccione **Crear**.
1. La variable **Crear nuevo extremo de GraphQL** se abrirá. Aquí puede especificar:
   * **Nombre**: nombre del extremo; puede escribir cualquier texto.
   * **Utilice el esquema GraphQL proporcionado por**: utilice la lista desplegable para seleccionar el sitio o proyecto requerido.

   >[!NOTE]
   >
   >La siguiente advertencia se muestra en el cuadro de diálogo:
   >
   >* *Los extremos de GraphQL pueden introducir problemas de rendimiento y seguridad de datos si no se administran con cuidado. Asegúrese de definir los permisos adecuados después de crear un extremo.*


1. Confirme con **Crear**.
1. La variable **Pasos siguientes** proporciona un vínculo directo a la consola de seguridad para que pueda asegurarse de que el extremo recién creado tenga los permisos adecuados.

   >[!CAUTION]
   >
   >El punto final es accesible para todos. Esto puede suponer un problema de seguridad, especialmente en las instancias de publicación, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
   >
   >Puede configurar ACL, según su caso de uso, en el punto final.

## Publicación del extremo de GraphQL {#publishing-graphql-endpoint}

Seleccione el nuevo punto final y **Publicación** para que esté totalmente disponible en todos los entornos.

>[!CAUTION]
>
>El punto final es accesible para todos.
>
>En instancias de publicación esto puede suponer un problema de seguridad, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
>
>Debe configurar [ACL adecuados para su caso de uso](/help/headless/security/permissions.md) en el punto final.