---
title: Añadir un nombre de dominio personalizado
description: Obtenga información sobre cómo agregar un nombre de dominio personalizado mediante Configuración de dominio en Cloud Manager.
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d6d34c2818ecb07c9d610844f6b868fe6a5918c6
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 15%

---


# Añadir un nombre de dominio personalizado {#adding-custom-domain-name}

Aprenda a agregar un nombre de dominio personalizado mediante **Configuración de dominio** en Cloud Manager.

## Requisitos  {#requirements}

Complete estos requisitos antes de agregar un nombre de dominio personalizado en Cloud Manager.

* Debe haber agregado un certificado SSL de dominio para el dominio que desea agregar *antes de* agregar un nombre de dominio personalizado como se describe en el documento [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Debe tener la función **Propietario del negocio** o **Administrador de implementación** para agregar un nombre de dominio personalizado en Cloud Manager.
* Utilice Fastly u otra CDN (red de distribución de contenido).

>[!IMPORTANT]
>
>Si utiliza una CDN administrada por Adobe, aún debe agregar su dominio a Cloud Manager.

## Dónde agregar nombres de dominio personalizados {#where-to-add-custom-domain-name}

Puede agregar un nombre de dominio personalizado desde la [página Configuración de dominio](#adding-cdn-settings) en Cloud Manager.

Al agregar un nombre de dominio personalizado, el dominio se proporciona utilizando el certificado más específico y válido. Si varios certificados tienen el mismo dominio, se elige el actualizado más recientemente. Adobe recomienda administrar los certificados de modo que no haya dominios superpuestos.

Los pasos para cualquiera de los métodos descritos en este documento se basan en Fastly. Si ha utilizado una CDN (red de distribución de contenido) diferente, configure su dominio con la CDN que ha elegido utilizar.

## Añadir un nombre de dominio personalizado {#adding-custom-domain-name-settings}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En el menú lateral, en **Servicios**, haga clic en ![Icono de configuración](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) **Configuración de dominio**.

   ![La ventana Configuración de dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. Cerca de la esquina superior derecha de la página **Configuración de dominio**, haga clic en **Agregar dominio**.

1. En el cuadro de diálogo **Agregar dominio**, en el campo **Nombre de dominio**, escriba el nombre de dominio personalizado que está utilizando.
Al escribir el nombre de dominio, no incluya `http://`, `https://` ni espacios.

   >[!NOTE]
   >
   >Si necesita las versiones `www` y `non-www` de un dominio, debe agregarlas por separado. Por ejemplo, `example.com` y `www.example.com`.
   <!-- Marius Petria on SLACK tmp-skyline-cdn-certificates - Actually  my opinion is that this option should be explicit in UI (that was present in the initial mocks of the design but for some reason it was dropped). I think when adding a domain there should be a check mark to also add www.domain. When adding example.com Customer should be prompted with the following options: Do you also want to add www.example.com and have a redirect example.com -> www.example.com?Do you also want to add www.example.com and have a redirect www.example.com -> example.com? -->

1. Haga clic en **Crear**.

1. En el cuadro de diálogo **Verificar dominio**, en **¿Qué tipo de certificado planea usar con este dominio?**, seleccione una de las siguientes opciones:

   | Opción de tipo de certificado | Descripción |
   | --- | --- |
   | Certificado SSL administrado por Adobe (DV) | Seleccione este tipo de certificado si desea utilizar un certificado DV (validación de dominio). Esta opción es ideal para la mayoría de los casos, ya que proporciona una validación básica del dominio. Adobe administra y renueva el certificado automáticamente. |
   | Certificado SSL administrado por el cliente (OV/EV) | Seleccione este tipo de certificado si desea utilizar un certificado SSL EV/OV para proteger el dominio. Esta opción ofrece una seguridad mejorada con OV (validación de organización) o EV (validación extendida). Utilícelo si se requiere una verificación más estricta, niveles de confianza más altos o control personalizado de los certificados. |

1. En el cuadro de diálogo **Verificar dominio**, en función del tipo de certificado seleccionado, realice una de las siguientes acciones:

   | Si seleccionó el tipo de certificado | Descripción |
   | --- | ---  |
   | Certificado administrado por Adobe | a. Complete los [pasos de certificado administrado por Adobe](#adobe-managed-cert-steps) a continuación. Cuando complete los pasos, en el cuadro de diálogo **Verificar dominio**, haga clic en **Verificar**.<ul><li>La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.</li><li>Cloud Manager finalmente verifica la propiedad del nombre de dominio y actualiza el estado en la tabla **Configuración de dominio**. Consulte [Comprobar el estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.</li>![Verificar el estado del dominio](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. Ya está listo para [agregar un certificado SSL administrado por Adobe (DV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Certificado administrado por el cliente | a. Haga clic en **Aceptar**.<br>b. Ya está listo para [agregar un certificado SSL administrado por el cliente (OV/EV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert).<br>Después de agregar el certificado, el nombre de dominio se marca como verificado en la tabla **Configuración de dominio**. Consulte [Comprobar el estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.</li></ul><br>![Verificar el dominio de un certificado EV/OV administrado por el cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |

   >[!NOTE]
   >
   >Si utiliza su propio certificado SSL administrado por el cliente (OV/EV o DV), no es necesario que agregue un certificado SSL. Esta regla también se aplica si planea usar un CDN (red de distribución de contenido) administrado por el cliente ***proveedor***. En su lugar, vaya directamente a [Agregar una asignación de dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) cuando esté listo.


### Pasos del certificado administrado por Adobe {#adobe-managed-cert-steps}

Si seleccionó el tipo de certificado *Certificado administrado por Adobe*, complete el siguiente paso en el cuadro de diálogo **Verificar dominio**.

![Pasos de certificado administrado por Adobe](/help/implementing/cloud-manager/assets/cdn/cdn-create-adobe-dv-cert.png)

Para verificar el dominio en uso, es necesario agregar y verificar un CNAME.

Un tipo de registro `CNAME` o un tipo de registro `A`, una vez aprovisionado, enruta todo el tráfico de Internet para el dominio a donde señale. Se produce una interrupción si esa ubicación no está preparada para abastecer el tráfico. Si no se ha probado, puede haber errores en el contenido. Por este motivo, este paso siempre se realiza una vez finalizada la prueba y está listo para su lanzamiento.

Para establecer esta configuración, determine si se debe configurar un registro `CNAME` o Apex para que apunte el nombre de dominio personalizado al nombre de dominio de Cloud Manager. Las siguientes secciones de este documento pueden ayudarle a determinar qué tipo de registro es apropiado para su configuración de DNS.

>[!NOTE]
>
>Para los CDN administrados por Adobe, al utilizar certificados DV (validación de dominio), solo se permiten sitios con validación ACME.


### Configurar DNS{#config-dns}

>[!WARNING]
>
>El principio de &quot;registrarse antes de anunciar&quot; se aplica aquí. Es decir, la configuración de DNS solo se debe realizar *después de* de haber agregado correctamente la asignación de dominio. Al hacerlo, se asegura de que Cloud Manager reconozca y valide que el dominio existe en su propia configuración para poder responder a las solicitudes que le realicen. También evita cualquier intento de adquisición de dominio.

Asegúrese de cumplir los siguientes requisitos *antes* de configurar los registros DNS:

* Identifique el host de dominio o el registrador si aún no lo conoce.
* Puede editar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Ya ha verificado su nombre de dominio personalizado configurado como se describe en el documento [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

#### Registro CNAME {#adobe-managed-cert-cname-record}

Un nombre canónico o registro CNAME es un tipo de registro DNS que asigna un nombre de alias a un nombre de dominio verdadero o canónico. Los registros CNAME generalmente se utilizan para asignar un subdominio como `www.example.com` al dominio que hospeda el contenido de ese subdominio.

Inicie sesión en el proveedor de servicios DNS y cree un registro `CNAME` para apuntar el nombre de dominio personalizado al destino, como en la tabla siguiente.

| CNAME | Punto de dominio personalizado de dominio a destino |
| --- | --- |
| `www.customdomain.com` | `cdn.adobeaemcloud.com` |

#### registro APEX {#adobe-managed-cert-apex-record}

Un dominio Apex es un dominio personalizado que no contiene un subdominio, como `example.com`. Un dominio Apex está configurado con un registro `A`, `ALIAS` o `ANAME` a través de su proveedor DNS. Los dominios Apex deben apuntar a direcciones IP específicas.

Agregue los siguientes `A` registros a la configuración DNS de su dominio a través de su proveedor de dominios.

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

>[!TIP]
>
>El *registro CNAME* o *Un registro* se puede establecer en el servidor DNS de administración para ahorrarle tiempo.

<!--
![Customer managed certificate steps](/help/implementing/cloud-manager/assets/cdn/cdn-create-customer-cert.png)

To verify the domain in use, you are required to add and verify a TXT record.

A text record (also known as a TXT record) is a type of resource record in the Domain Name System (DNS). It lets you associate arbitrary text with a hostname. This text could include human-readable details like server or network information.

Cloud Manager uses a specific TXT record to authorize a domain to be hosted in a CDN service. Create a DNS TXT record in the zone that authorizes Cloud Manager to deploy the CDN service with the custom domain and associate it with the backend service. This association is entirely under your control and authorizes Cloud Manager to serve content from the service to a domain. This authorization may be granted and withdrawn. The TXT record is specific to the domain and the Cloud Manager environment.

#### Requirements {#customer-managed-cert-requirements}

Fulfill these requirements before adding a TXT record.

* Identify your domain host or registrar if you do not know it already.
* Be able to edit the DNS records for your organization's domain, or contact the appropriate person who can.
* First, add a custom domain name as described earlier in this article.

#### Add a TXT record for verification {#customer-managed-cert-verification}

1. In the **Verify domain** dialog box, Cloud Manager displays the name and TXT value to use for verification. Copy this value.

1. Log in to your DNS service provider and find the DNS records section. 

1. Add `aemverification.[yourdomainname]` as the **Name** of the value and add the TXT value exactly as it appears in the **Domain Name** field.

   **TXT record examples**

   | Domain | Name | TXT Value |
   | --- | --- | --- |
   | `example.com` | `_aemverification.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
   | `www.example.com` | `_aemverification.www.example.com` | Copy the entire value displayed in the Cloud Manager UI. This value is specific to the domain and the environment. For example:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

1. Save the TXT record to your domain host.

#### Verify TXT record {#customer-managed-cert-verify}

When you are done, you can verify the result by running the following command.

```shell
dig _aemverification.[yourdomainname] -t txt
```

The expected result should display the TXT value provided on the **Verification** tab of the **Add Domain Name** dialog of the Cloud Manager UI.

For example, if your domain is `example.com`, then run:

```shell
dig TXT _aemverification.example.com -t txt
```


>[!TIP]
>
>There are several [DNS lookup tools](https://www.ultratools.com/tools/dnsLookup) available. Google DoH can be used to look up TXT record entries and identify if the TXT record is missing or erroneous.

-->



<!--
## Next Steps {#next-steps}

Now that you created your TXT entry, you can verify your domain name status. Proceed to the document [Checking Domain Name Status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) to continue setting up your custom domain name. -->


><!-- The TXT entry and the CNAME or A Record can be set simultaneously on the governing DNS server, thus saving time. -->
>
><!-- To do this, review the entire process of setting up a custom domain name as detailed in the document [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) taking special note of the document [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) and update your DNS settings appropriately. -->


