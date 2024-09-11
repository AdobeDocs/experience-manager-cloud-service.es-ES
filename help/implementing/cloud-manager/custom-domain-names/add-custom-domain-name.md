---
title: Agregar un nombre de dominio personalizado
description: Obtenga información sobre cómo agregar un nombre de dominio personalizado mediante Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: dd696580758e7ab9a5427d47fda4275f9ad7997f
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 20%

---


# Agregar un nombre de dominio personalizado {#adding-cdn}

Obtenga información sobre cómo agregar un nombre de dominio personalizado mediante Cloud Manager.

## Requisitos  {#requirements}

Complete estos requisitos antes de agregar un nombre de dominio personalizado en Cloud Manager.

* Debe haber agregado un certificado SSL de dominio para el dominio que desea agregar antes de agregar un nombre de dominio personalizado como se describe en el documento [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Debe tener la función **Propietario del negocio** o **Administrador de implementación** para agregar un nombre de dominio personalizado en Cloud Manager.
* Utilice la CDN de Fastly.

>[!IMPORTANT]
>
>Incluso si utiliza una CDN que no sea de Adobe, debe agregar su dominio a Cloud Manager.

## Dónde agregar nombres de dominio personalizados {#}

Puede agregar un nombre de dominio personalizado desde dos ubicaciones en Cloud Manager:

* [Desde la página Configuración de dominio](#adding-cdn-settings)
* [Desde la página Entornos](#adding-cdn-environments)

Al agregar un nombre de dominio personalizado, el dominio se proporciona utilizando el certificado más específico y válido. Si varios certificados tienen el mismo dominio, se elige el actualizado más recientemente. El Adobe recomienda administrar los certificados de modo que no haya dominios superpuestos.

Los pasos para cualquiera de los métodos descritos en este documento se basan en Fastly. Si ha utilizado una CDN diferente, configure el dominio con la CDN que ha elegido utilizar.

## Agregar un nombre de dominio personalizado desde la página Configuración de dominio {#adding-cdn-settings}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En el panel de navegación izquierdo, seleccione la ficha **Configuración de dominio**

   ![La ventana Configuración de dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Cerca de la esquina superior derecha de la página **Configuración de dominio**, haga clic en **Agregar dominio**.

1. En el cuadro de diálogo **Agregar dominio**, en el campo **Nombre de dominio**, escriba el nombre de dominio personalizado que está utilizando.
No incluya `http://`, `https://` ni espacios al introducir el dominio.

1. Haga clic en **Crear**.

1. En el cuadro de diálogo **Verificar dominio**, en **¿Qué tipo de certificado planea usar con este dominio?**, seleccione una de las siguientes opciones:

   | Tipo de certificado | Descripción |
   | --- | --- |
   | Certificado administrado por Adobe | Seleccione si desea utilizar un certificado DV (validación de dominio). Esta opción es ideal para la mayoría de los casos, ya que proporciona una validación básica del dominio. El Adobe administra y renueva el certificado automáticamente. |
   | Certificado administrado por el cliente | Seleccione si desea utilizar un certificado EV/OV. Esta opción ofrece una seguridad mejorada con EV (validación extendida) u OV (validación de organización). Utilícelo si se requiere una verificación más estricta, niveles de confianza más altos o control personalizado de los certificados. |

1. En el cuadro de diálogo **Verificar dominio**, en función del tipo de certificado seleccionado, realice una de las siguientes acciones:

   | Si seleccionó el tipo de certificado | Descripción |
   | --- | ---  |
   | Certificado administrado por Adobe | Complete los [pasos del certificado administrado por el Adobe](#abobe-managed-cert-steps) antes de continuar con el siguiente paso. |
   | Certificado administrado por el cliente | Complete los [pasos del certificado administrado por el cliente](#customer-managed-cert-steps) antes de continuar con el siguiente paso. |

1. Haga clic en **Verificar**.

1. Ya está listo para [agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

   >[!NOTE]
   >
   >Si usa un certificado SSL autoadministrado y un proveedor de CDN autoadministrado, puede omitir este paso e ir directamente a [Agregar una configuración de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md) cuando esté listo.



### Pasos del certificado administrado de Adobe {#adobe-managed-cert-steps}

Si seleccionó el tipo de certificado *certificado administrado por el Adobe*, complete los siguientes pasos en el cuadro de diálogo **Verificar dominio**.

![Pasos de certificado administrado de Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Para verificar el dominio en uso, es necesario agregar y verificar un CNAME.

Un registro `CNAME` o A, una vez aprovisionado, enruta todo el tráfico de Internet para el dominio a donde señale. Se produce una interrupción si esa ubicación no está preparada para abastecer el tráfico. Si no se ha probado, puede haber errores en el contenido. Por este motivo, este paso siempre se realiza una vez finalizada la prueba y está listo para su lanzamiento.

Para establecer esta configuración, determine si se debe configurar un registro `CNAME` o Apex para que apunte el nombre de dominio personalizado al nombre de dominio de Cloud Manager. Las siguientes secciones de este documento pueden ayudarle a determinar qué tipo de registro es apropiado para su configuración de DNS.

>[!NOTE]
>
>En el caso de las CDN administradas por Adobe, al utilizar certificados DV (validación de dominio), solo se permiten sitios con validación ACME.

#### Requisitos  {#dv-requirements}

Complete estos requisitos antes de configurar los registros DNS.

* Identifique el host de dominio o el registrador si aún no lo conoce.
* Puede editar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Ya debe haber verificado el nombre de dominio personalizado configurado tal como se describe en el documento [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

#### Registro CNAME {#cname-record}

Un nombre canónico o registro CNAME es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com` al dominio que hospeda el contenido de ese subdominio.

Inicie sesión en el proveedor de servicios DNS y cree un registro `CNAME` para apuntar el nombre de dominio personalizado al destino, como en la tabla siguiente.

| CNAME | Punto de dominio personalizado de dominio a destino |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### registro APEX {#apex-record}

Un dominio Apex es un dominio personalizado que no contiene un subdominio, como `example.com`. Un dominio Apex está configurado con un registro `A`, `ALIAS` o `ANAME` a través de su proveedor DNS. Los dominios Apex deben apuntar a direcciones IP específicas.

Agregue los siguientes `A` registros a la configuración DNS de su dominio a través de su proveedor de dominios.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`



### Pasos del certificado administrado por el cliente {#customer-managed-cert-steps}

Si seleccionó el tipo de certificado *Certificado administrado por el cliente*, complete los siguientes pasos en el cuadro de diálogo **Verificar dominio**.

![Pasos de certificado administrado por el cliente](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

Para comprobar el dominio en uso, es necesario agregar y comprobar un registro TXT.

Un registro de texto (también conocido como registro TXT) es un tipo de registro de recursos del Sistema de nombres de dominio (DNS). Permite asociar texto arbitrario con un nombre de host. Este texto puede incluir detalles legibles en lenguaje natural, como información del servidor o de la red.

Cloud Manager utiliza un registro TXT específico para autorizar a un dominio a alojarse en un servicio CDN. Cree un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo su control y autoriza a Cloud Manager a servir contenido desde el servicio a un dominio. Esta autorización podrá concederse y retirarse. El registro TXT es específico del dominio y del entorno de Cloud Manager.

## Requisitos  {#requirements-customer-cert}

Complete estos requisitos antes de agregar un registro TXT.

* Identifique el host de dominio o el registrador si aún no lo conoce.
* Puede editar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* En primer lugar, agregue un nombre de dominio personalizado como se describió anteriormente en este artículo.

## Agregar un registro TXT para la verificación {#verification}

1. En el cuadro de diálogo **Verificar dominio**, Cloud Manager muestra el nombre y el valor TXT que se utilizarán para la verificación. Copie este valor.

1. Inicie sesión en el proveedor de servicios DNS y busque la sección Registros DNS.

1. Agregue `aemverification.[yourdomainname]` como **Nombre** del valor y agregue el valor TXT exactamente como aparece en el campo **Nombre de dominio**.

   **ejemplos de registro TXT**

   | Dominio | Nombre | Valor TXT |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copie todo el valor que se muestra en la interfaz de usuario de Cloud Manager. Este valor es específico del dominio y del entorno. Por ejemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copie todo el valor que se muestra en la interfaz de usuario de Cloud Manager. Este valor es específico del dominio y del entorno. Por ejemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Guarde el registro TXT en el host de dominio.

## Verificar registro TXT {#verify}

Cuando haya terminado, puede comprobar el resultado ejecutando el siguiente comando.

```shell
dig _aemverification.[yourdomainname] -t txt
```

El resultado esperado debería mostrar el valor TXT proporcionado en la ficha **Verificación** del cuadro de diálogo **Agregar nombre de dominio** de la interfaz de usuario de Cloud Manager.

Por ejemplo, si el dominio es `example.com`, ejecute:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Hay varias [herramientas de búsqueda DNS](https://www.ultratools.com/tools/dnsLookup) disponibles. Google DoH se puede utilizar para buscar entradas de registro TXT e identificar si el registro TXT falta o es erróneo.

>[!NOTE]
>
>La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.
>
>Cloud Manager comprueba la propiedad y actualiza el estado, que se puede ver en la tabla Configuración de dominio. Consulte [Comprobar el estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.

<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->

>[!TIP]
>
>La entrada TXT y el CNAME o un registro se pueden configurar simultáneamente en el servidor DNS de control, lo que ahorra tiempo.
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


## Agregar un nombre de dominio personalizado desde la página Entornos {#adding-cdn-environments}

Los pasos para agregar un nombre de dominio personalizado desde la página **Entornos** son los mismos que cuando [agrega un nombre de dominio personalizado desde la página Configuración de dominio](#adding-cdn-settings), pero el punto de entrada difiere. Siga estos pasos para agregar un nombre de dominio personalizado desde la página **Entornos**.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la página de detalles de **Entornos** para el entorno de interés.

   ![Introducción del nombre de dominio en la página Detalles del entorno](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. Utilice la variable **Nombres de dominio** para enviar el nombre de dominio personalizado.

   1. Introduzca el nombre de dominio personalizado.
   1. Seleccione el certificado SSL asociado a este nombre en la lista desplegable.
   1. Haga clic en **+Agregar**.

   ![Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. El cuadro de diálogo **Agregar nombre de dominio** se abre a la ficha **Nombre de dominio**. Continúe como lo haría para [agregar un nombre de dominio personalizado desde la página Configuración de dominio](#adding-cdn-settings). —>
