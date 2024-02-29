---
description: Este tutorial incluye instrucciones para hacer que una sección de un formulario sea repetible
title: Secciones repetibles en Edge Delivery Services
feature: Edge Delivery Services
source-git-commit: 3b24d0cd4099e0b8eb48c977f460b25c168af220
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Secciones repetibles en la entrega de Edge

Una sección repetible es un componente de un formulario que se duplica o replica varias veces para recopilar información de varias apariciones de los mismos datos.

Por ejemplo, considere un formulario utilizado para recopilar información de los usuarios que solicitan un préstamo. El formulario permite a los usuarios proporcionar información personal, incluidos los detalles de los prestadores. Los usuarios pueden introducir detalles para los co-solicitantes, con esta sección como repetible.

![Secciones repetibles en formularios](/help/forms/assets/eds-repeatable.png)

## Requisitos previos

AEM Configure el proyecto de Github del servicio de entrega perimetral (EDS) mediante plantillas de palabras clave de y clone el repositorio de Github correspondiente en el equipo local. Consulte [tutorial para desarrolladores](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/build/tutorial.html) para obtener más información.

## Secciones repetibles en la entrega de Edge

Veamos un ejemplo de un formulario de solicitud de préstamo. El formulario permite a los usuarios enviar información personal. Puede incluir detalles del cosolicitante utilizando secciones repetibles, con la opción de añadir un mínimo y un máximo de tres secciones del cosolicitante.

>[!NOTE]
>
> * Puede crear un Excel de Microsoft en el sitio de SharePoint o en la unidad de Google para que los conjuntos de campos sean repetibles en un formulario.
> * En este caso, estamos tomando como ejemplo un SharePoint de Microsoft. Para hacer que la carpeta SharePoint sea la fuente de contenido, siga los pasos que se explican en [Cómo usar Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint).


Para añadir secciones repetibles en la entrega de Edge:

1. [Crear un formulario con Microsoft Excel](#author-form)
2. [Previsualización y publicación del formulario](#preview-form)

### Crear un formulario con Microsoft Excel {#author-form}

1. Vaya a su cuenta de Microsoft SharePoint AEM y abra o cree el directorio de proyectos de entrega de Edge de la aplicación de.
2. Abra un archivo existente de Microsoft Excel o cree uno nuevo.
En este ejemplo, se utiliza una hoja de Excel denominada `loan-application.xlsx` creado en Microsoft SharePoint Site.
3. Añadir nuevas columnas etiquetadas como `Repeatable`, `Min`, y `Max` en el archivo de Microsoft Excel.
4. Especifique el valor de `Repeatable` columna como `True` para el conjunto de campos que desea que sea repetible.
5. Especifique los valores para la variable `Min` y `Max` columnas. El `Min` representa el número mínimo de apariciones para las que se repite el panel, mientras que la variable `Max` el valor representa el número máximo de ocurrencias para las que se repite el panel.
6. Guarde el archivo de Microsoft Excel.

>[!NOTE]
>
> Aquí está la [Solicitud de préstamo](/help/forms/assets/loan-application.xlsx) hoja de excel para su referencia.

### Vista previa o publicación del formulario con el servicio de envío de Edge

1. Abra o cree un nuevo archivo de documento en un sitio de Microsoft SharePoint para incrustar la hoja de Excel en él mediante una `Form Block`. Por ejemplo, abra el `index` y añada un `Form Block`.
2. AEM Abra el símbolo del sistema, vaya al directorio del proyecto Entrega perimetral de la cuenta de usuario en el equipo local y ejecute el comando como `aem up`.

Se puede acceder al formulario en `https://localhost:3000`, donde al hacer clic en `Add` El botón añade una nueva sección repetible para introducir los detalles del solicitante. También puede eliminar la sección repetible haciendo clic en el `Delete` botón.

>[!NOTE]
>
> Si aparece el error &quot;Página no encontrada&quot; al acceder al formulario en localhost, agregue el nombre de directorio del sitio de SharePoint de Microsoft delante de la dirección URL donde se encuentra el formulario. Por ejemplo, `http://localhost:3000/<dir-name>/`




