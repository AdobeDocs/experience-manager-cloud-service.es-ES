---
title: Activación de la protección de enlaces interactivos en Dynamic Media
description: Obtenga información sobre cómo activar la protección de los vínculos interactivos en Dynamic Media.
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 13%

---

# Activación de la protección de enlaces interactivos en Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

La vinculación activa se produce cuando un sitio web de terceros utiliza código HTML para mostrar una imagen del sitio web. Utilizan el ancho de banda cada vez que se solicita la imagen, ya que el explorador del visitante accede a ella directamente desde el servidor. La protección de vínculos interactivos *protection* es un método para evitar que otros sitios web se vinculen directamente a imágenes, CSS o JavaScript en sus páginas web. Este tipo de escudo ayuda a reducir el uso innecesario del ancho de banda en su cuenta de Dynamic Media.

[Atención al cliente de Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=es#home) puede configurar un filtro de referente a nivel de CDN. Al hacerlo, se garantiza que el contenido de Dynamic Media solo se proporcione a los sitios web de la lista de sitios web permitidos para el dominio.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada que está integrada en Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada. Para activar la protección de vínculos interactivos, un administrador debe crear un ticket de asistencia para solicitar el cambio de configuración en su cuenta de Dynamic Media. La activación de la protección de vínculos interactivos no supone ningún coste adicional.
