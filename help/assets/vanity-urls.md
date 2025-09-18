---
title: Creación de direcciones URL mnemónicas mediante Dynamic Media con funciones de OpenAPI
description: Utilice las funcionalidades de OpenAPI de Dynamic Media para transformar las URL de entrega de recursos largas en URL de vanidad cortas y de marca. Una URL de vanidad es una versión corta, limpia, fácil de recordar y legible de su URL de envío compleja. Puede incluir su nombre de marca, nombres de productos y palabras clave relevantes en la URL de vanidad para aumentar la visibilidad de su marca y la participación del usuario
role: Admin
feature: Asset Management, Publishing, Collaboration, Asset Processing
source-git-commit: c72966bff9220b681f8c1e4c534f19cb4b950700
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---


# ¿Usar URL de vanidad?{#vanity-urls}

Use [!DNL Dynamic Media OpenAPI capabilities] para transformar las URL de entrega de recursos largas en URL de vanidad cortas y con marca. Las direcciones URL de envío de recursos estándar incluyen UUID de recursos generados por el sistema que hacen que la dirección URL de envío sea compleja, difícil de recordar y compartir. Reemplace estos UUID de recurso con identificadores simples (ID de vanidad) para generar una URL de vanidad. Una URL de vanidad es una versión corta, limpia y legible de la URL de envío compleja.

Consulte los siguientes formatos de URL para comprender su diferencia:
* [URL de envío estándar](#standard-urls)
* [URL de vanidad](#vanity-url)

Las direcciones URL de envío estándar utilizan `aaid` seguidas de un UUID, mientras que las direcciones URL de vanidad utilizan `avid` seguidas de un identificador personalizado (identificador personalizado).

Utilice identificadores mnemónicos cortos y sencillos para que la dirección URL de envío sea corta, limpia, legible, fácil de recordar y compartir. Utilice su nombre de marca, nombres de productos y palabras clave relevantes como ID de vanidad para aumentar la visibilidad de su marca y la participación del usuario.

Cuando el usuario hace clic en la URL de vanidad, [!DNL Dynamic Media with OpenAPI] se asigna automáticamente a la ubicación del recurso original en el momento de la ingesta y los resuelve correctamente en el momento de la entrega para entregar el recurso al usuario.

Aprenda a [crear direcciones URL mnemónicas](#create-vanity-urls).

## URL de envío estándar{#standard-urls}

La dirección URL de entrega de recursos estándar [!DNL Dynamic Media with OpenAPI] incluye un identificador único generado por el sistema y sigue el siguiente formato.

***Formato:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:aaid:aem:<asset-uuid>/as/<seoname>.<format>`

La dirección URL de envío estándar incluye `aaid` (*identificador de recurso real*) después de `urn:` y un UUID entre `urn:aaid:aem:` y `/as/<seoname>.<format>`.

***Ejemplo:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:aaid:aem:43341ab1-4086-44d2-b7ce-ee546c35613b/as/check.jpeg`

En el ejemplo anterior, `43341ab1-4086-44d2-b7ce-ee546c35613b` es el UUID.

## URL de vanidad{#vanity-url}

Las URL de vanidad incluyen un identificador mnemónico en lugar del UUID del recurso y tienen el siguiente formato.

***Formato:*** `https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

La URL de vanidad incluye `avid` (*identificador de vanidad real*) después de `urn:` y su ID de vanidad entre `urn:avid:aem:` y `/<seoname>.<format>`.

***Ejemplo:*** `https://delivery-p30902-e145436.adobeaemcloud.com/adobe/assets/urn:avid:aem:VanityCheck/as/check.jpeg`

En el ejemplo anterior, `VanityCheck` es el identificador mnemónico que reemplazó al UUID.

## Explore las funcionalidades y ventajas clave{#capabilities-and-benefits-of-vanity-urls}

El uso de ID mnemónicos significativos para personalizar las URL de entrega de recursos estándar ofrece varias ventajas y un impacto mensurable. Algunas de las funciones y ventajas clave de las URL mnemónicas son las siguientes.

### Capacidades clave{#key-capabilities}

* **Personalización de URL:** Reemplace los identificadores largos (UUID de recursos) en la dirección URL de envío con alternativas más cortas y alineadas con la marca para generar una dirección URL de envío más limpia.
* **Redirección en tiempo real:** Las URL mnemónicas se redirigen a los UUID de recursos originales durante la ejecución sin interrumpir los flujos de trabajo. Los usuarios ven las direcciones URL limpias en la barra de direcciones mientras el sistema gestiona el enrutamiento técnico.
* **Administración sencilla de vínculos:** Personalice las direcciones URL personales en cualquier momento sin afectar el rendimiento de la entrega de recursos.

### Ventajas principales{#key-benefits}

* **Mejora la experiencia del usuario:** Las URL personales limpias y más cortas son legibles, fáciles de usar, fáciles de recordar y compartir.

* **Mejora la participación del usuario:** Las direcciones URL con marca mejoran la confianza del usuario. Los usuarios tienen más probabilidades de hacer clic en vínculos profesionales de marca, lo que da como resultado tasas de clics más altas.

* **Optimización de SEO:** Las direcciones URL que incluyen palabras clave relevantes mejoran la detección y clasificación de los motores de búsqueda.

* **Visibilidad mejorada de la marca:** Las direcciones URL específicas de la marca refuerzan la presencia de la marca en todos los canales de marketing, incluidos el correo electrónico, los medios sociales y las campañas publicitarias.
Además, el uso coherente de direcciones URL con marca en todas las comunicaciones refuerza la identidad y el reconocimiento de la marca.

* **Seguimiento y análisis de campañas:** Use direcciones URL personales únicas para diferentes campañas y canales a fin de obtener información detallada sobre las fuentes de tráfico y el rendimiento de conversión.

## Requisitos previos{#prerequisites-for-creating-vanity-id}

Para crear la URL de vanidad, asegúrate de que ya has [aprobado los recursos para la entrega pública](/help/assets/manage-organize-assets-view.md#manage-asset-status).

## Crear URL de vanidad{#create-vanity-urls}

Siga estos pasos para crear URL de vanidad:
1. [Configurar metadatos de recursos](#set-up-asset-metadata)
1. [Crear y asignar una variable de entorno de Cloud Manager](#map-cloud-manager-environment-variable)
1. [Aprobar los recursos que requieren una URL de vanidad para la entrega](/help/assets/manage-organize-assets-view.md#manage-asset-status)
1. [Generar URL de vanidad](#generate-vanity-urls)

### Configurar metadatos de recursos{#set-up-asset-metadata}

Ejecute lo siguiente para configurar el ID mnemónico en el formulario de metadatos del recurso:
1. Vaya a la página de detalles de la carpeta que contiene los recursos para la entrega de [!DNL Dynamic Media with OpenAPI].
1. [Edite ese formulario de metadatos](/help/assets/metadata-assets-view.md#edit-metadata-forms) mediante uno de los procedimientos siguientes:
   * Añada un nuevo campo de metadatos y especifique el ID mnemónico requerido como valor de ese campo.
   * Actualice el campo existente reemplazando el valor de una propiedad de metadatos existente por el ID de vanidad requerido. Conozca las [prácticas recomendadas](#best-practices) para crear el ID de vanidad.
     ![ID de vanidad](/help/assets/assets/vanity-id-metadata.png)
Más información sobre [esquemas de metadatos](/help/assets/metadata-schemas.md).

     >[!NOTE]
     >
     > Un solo recurso puede tener varios ID de vanidad. [Póngase en contacto con el soporte técnico de Adobe](https://helpx.adobe.com/in/contact.html) y envíe una solicitud para generar los ID de vanidad necesarios.

Después de configurar el identificador personalizado en el formulario de metadatos del recurso, [asigne este campo de metadatos al mecanismo de envío del sistema](#map-cloud-manager-environment-variable).

### Crear y asignar una variable de entorno de Cloud Manager{#map-cloud-manager-environment-variable}

Ejecute los siguientes pasos para crear una variable de entorno y asignarla al campo de metadatos que contiene el ID de vanidad:

1. [Vaya a la página de configuraciones del entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) y haga lo siguiente:
   1. Agregar variable `ASSET_DELIVERY_VANITY_ID`. Esta es la clave.
   1. Utilice el campo de valor para asignar a la propiedad de metadatos que contiene el ID de vanidad. La asignación sigue el formato `dc:<your-metadata-property>`, donde el prefijo de asignación de metadatos (como dc:) varía según la propiedad de configuración de metadatos.
      ![variable ASSET_DELIVERY_VANITY_ID](/help/assets/assets/environment-config.png)
1. Guarde los cambios para reiniciar los pods en el entorno.

### Aprobar los recursos para su envío{#approve-assets-for-delivery}

Después de asignar la variable `ASSET_DELIVERY_VANITY_ID` en su entorno de Cloud Manager a la propiedad de metadatos del recurso que contiene el identificador mnemónico, [apruebe los recursos que requieren una URL mnemónica para la entrega](/help/assets/manage-organize-assets-view.md#manage-asset-status).

### Generar URL mnemónicas{#generate-vanity-urls}

Realice los siguientes reemplazos en la dirección URL de envío estándar para transformarla en una URL de vanidad:

* Reemplaza **UUID** por tu **ID de vanidad**.
* Reemplazar `aaid` por `avid`.

Consulte la [transformación de URL de estándar a URL de vanidad](#standard-urls) más arriba.
Aprenda a [copiar Dynamic Media con las URL de entrega de OpenAPI](/help/assets/approve-assets.md#copy-delivery-url-for-approved-assets) para sus recursos.

Cuando el usuario hace clic en la URL de vanidad, [!DNL Dynamic Media with OpenAPI] asigna automáticamente el ID de vanidad al UUID del recurso original en el momento de la ingesta y lo resuelve correctamente en el momento de la entrega para ofrecer el recurso al usuario sin ningún retraso. Puede personalizar la URL de vanidad en tiempo real sin afectar al rendimiento de entrega de los recursos.

[Mejore el impacto de sus URL personalizadas con las funcionalidades de personalización avanzada de AEM Cloud Service.](#scale-using-vanity-url)

## Escalar mediante URL de vanidad{#scale-using-vanity-url}

AEM as a Cloud Service le permite [personalizar los nombres DNS y CDN](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/introduction) en sus direcciones web. Use estas capacidades de AEM CS con sus URL personales para transformarlas en direcciones web únicas, limpias, descriptivas, con marca, intuitivas y que proporcionen los [beneficios mencionados](#key-benefits).

Consulte la siguiente URL de vanidad y sus componentes personalizables:

**Formato de URL de vanidad:**

`https://delivery-<tenant>.adobeaemcloud.com/adobe/assets/urn:avid:aem:<vanity-id>/<seoname>.<format>`

<table style="border-collapse:collapse; table-layout:auto; width:auto;">
<tr valign="top">
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>https://delivery&#8209;&lt;tenant&gt;.adobeaemcloud.com</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#customize-dns">Personalizar este DNS</a></div>
</td>
<td style="padding:0 6px; white-space:nowrap; text-align:center;">/</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>adobe/assets/urn:avid:aem:</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#rewrite-cdn-rules">Personalizar dirección URL con reglas de reescritura</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:center;">
<div style="text-align:left;"><code>&lt;vanity-id&gt;</code></div>
<div style="text-align:center;">↓</div>
<div style="text-align:center;"><a href="#create-vanity-urls">Crear ID de vanidad</a></div>
</td>
<td style="padding:0 4px; white-space:nowrap; text-align:left; width:1%;">
<code>/&lt;seoname&gt;.&lt;format&gt;</code>
</td>
</tr>
</table>

**Formato de URL de vanidad con nombres DNS y CDN personalizados:**

`https://<custom-dns>` `/` `dam/assets/` `<vanity-id>` `/<seoname>.<format>`

**Componentes de URL personalizables**

* ***[Nombre DNS (nombre de host):](#customize-DNS)*** `https://delivery-<tenant>.adobeaemcloud.com` es el dominio del servidor que hospeda los recursos. [Personalizar DNS para cambiar el nombre de host](#customize-DNS).
* ***[Reglas de reescritura de CDN:](#rewrite-cdn-rules)*** `adobe/assets/urn:avid:aem:` es la estructura de rutas que identifica los tipos de recursos y los métodos de entrega. [Vuelva a escribir las reglas de CDN](#rewrite-cdn-rules) para modificar la ruta de dominio.

### Personalizar DNS{#customize-dns}

[Solicite al soporte técnico de Adobe](https://helpx.adobe.com/in/contact.html) que genere el DNS personalizado necesario para su nivel de entrega. Siga estas [prácticas recomendadas](#best-practices) para crear nombres DNS personalizados.

### Reescribir reglas de CDN{#rewrite-cdn-rules}

Ejecute los siguientes pasos para reescribir las reglas de CDN para la entrega:

1. Vaya al repositorio de AEM para crear un archivo de configuración de YAML.
2. Ejecute los pasos de la sección [setup](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-error-pages#setup) para configurar las reglas de CDN e implementar la configuración a través de la canalización de configuración de Cloud Manager.
Siga estas [prácticas recomendadas](#best-practices) para crear su ruta de dominio.
   [Más información acerca de las reglas de reescritura de CDN](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#request-transformations).

A continuación se muestran ejemplos de reglas de reescritura para anexar nombres de archivo con extensiones en URL de vanidad. Personalice estas reglas de reescritura según sus necesidades específicas. [Póngase en contacto con el soporte técnico de Adobe](https://helpx.adobe.com/in/contact.html) para obtener más ayuda:

```- name: cdn-rewrite-rule
  when:
    allOf:
      - reqProperty: tier
        equals: delivery
```

#### Para SVG, GIF y PDF {#svg-gif-pdf}

```
    type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:svg|gif|pdf|docx|xlsx))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/original/as/\1\2
```

#### Para vídeo{#video}

Para vídeos que incluyen MP4, MOV, AVI y MKV

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.(?:mp4|mov|avi|mkv))(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/play\2
```

#### Para la imagen{#image}

Para todos los tipos de imagen, excluyendo SVG.

```
type: transform
      reqProperty: path
      op: replace
      match: ^/dam/assets/([^/]+\.[^/]+)(\?.*)?$
      replacement: /adobe/assets/urn:avid:aem:\1/as/\1\2
```

## Siga las prácticas recomendadas para crear URL mnemónicas limpias{#best-practices}

Siga estas prácticas recomendadas para crear ID de vanidad, DNS personalizados y nombres de dominio:

1. No utilice caracteres especiales en los ID de vanidad, como espacios, barras diagonales, guiones y mucho más. El sistema reemplaza los caracteres especiales de los ID de vanidad mediante una asignación predefinida.
1. Utilice su nombre de marca, nombres de producto y palabras clave relevantes en sus ID de vanidad, DNS personalizados y nombres de dominio para aumentar la visibilidad de su marca y la participación del usuario.
1. Utilice palabras o cadenas cortas y descriptivas que transmitan significado.
1. Utilice textos que inviten a usuarios a hacer clic.
