---
title: Agregar un registro TXT
description: Obtenga información sobre cómo agregar un registro TXT para comprobar si es propietario de un dominio personalizado para utilizarlo con Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---


# Agregar un registro TXT {#adding-txt}

Obtenga información sobre cómo agregar un registro TXT para comprobar si es propietario de un dominio personalizado para utilizarlo con Cloud Manager.

## ¿Qué es un registro TXT? {#what-is}

Un registro de texto (también conocido como registro TXT) es un tipo de registro de recursos del Sistema de nombres de dominio (DNS). Proporciona la capacidad de asociar texto arbitrario con un nombre de host, como información legible en lenguaje natural sobre un nombre de host, como información de servidor o de red.

Cloud Manager utiliza un registro TXT específico para autorizar a un dominio a alojarse en un servicio CDN. Debe crear un registro TXT DNS en la zona que autorice a Cloud Manager a implementar el servicio CDN con el dominio personalizado y asociarlo al servicio back-end. Esta asociación está totalmente bajo su control y autoriza a Cloud Manager a servir contenido desde el servicio a un dominio. Esta autorización podrá concederse y retirarse. El registro TXT es específico del dominio y del entorno de Cloud Manager.

## Requisitos  {#requirements}

Debe cumplir estos requisitos antes de agregar un registro TXT.

* Debe identificar su host de dominio o registrador si aún no lo conoce.
* Debe poder editar los registros DNS del dominio de su organización o ponerse en contacto con la persona adecuada que pueda hacerlo.
* Primero debe agregar un nombre de dominio personalizado como se describe en el documento [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

## Agregar un registro TXT para verificación {#verification}

Se agrega un registro TXT como parte de la verificación de un nombre de dominio personalizado que se utilizará con Cloud Manager.

1. Primero debe agregar un nombre de dominio personalizado como se describe en el documento [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. En la ficha **Verificación** del cuadro de diálogo **Agregar nombre de dominio**, Cloud Manager muestra el nombre y el valor TXT que se utilizarán para la verificación. Copie este valor.

   ![Verificación del nombre del dominio](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. Inicie sesión en el host de dominio y busque la sección Registros DNS.

1. Agregue `_aemverification.[yourdomainname]` como **Nombre** del valor y agregue el valor TXT exactamente como aparece en el cuadro de diálogo **Agregar nombre de dominio**.

   * Vea los [ejemplos en la siguiente sección](#examples).

1. Guarde el registro TXT en el host de dominio.

## Ejemplos de registros TXT {#examples}

| Dominio | Nombre | Valor TXT |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Copie todo el valor que se muestra en la interfaz de usuario de Cloud Manager. Esto es específico para el dominio y el entorno. Por ejemplo:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Copie todo el valor que se muestra en la interfaz de usuario de Cloud Manager. Esto es específico para el dominio y el entorno. Por ejemplo:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

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
>Hay varias [herramientas de búsqueda DNS](https://www.ultratools.com/tools/dnsLookup) disponibles. Google DoH se puede usar para buscar entradas de registros TXT e identificar si el registro TXT falta o es erróneo.

>[!NOTE]
>
>La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.
>
>Cloud Manager verificará la propiedad y actualizará el estado que se puede ver en la tabla de configuración de dominio. Consulte [Comprobación del estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.

## Siguientes pasos {#next-steps}

Ahora que ha creado su entrada TXT, puede verificar el estado del nombre de dominio. Continúe con el documento [Comprobando el estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para seguir configurando el nombre de dominio personalizado.

>[!TIP]
>
>La entrada TXT y el registro CNAME o A se pueden configurar simultáneamente en el servidor DNS que controla, lo que ahorra tiempo.
>
>Si desea hacerlo, revise primero todo el proceso de configuración de un nombre de dominio personalizado como se detalla en el documento [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md), tomando nota especial del documento [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md), y actualice correctamente la configuración de DNS.