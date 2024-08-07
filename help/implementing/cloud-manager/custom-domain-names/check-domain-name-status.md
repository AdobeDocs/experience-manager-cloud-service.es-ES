---
title: Comprobar el estado del nombre de dominio
description: Obtenga información sobre cómo determinar si Cloud Manager ha verificado correctamente su nombre de dominio personalizado.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0c9328dc5be8f0a5e0924d0fc2ec59c9fce4141b
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 62%

---


# Comprobar el estado del nombre de dominio {#check-status}

Obtenga información sobre cómo determinar si Cloud Manager ha verificado correctamente su nombre de dominio personalizado.

## Requisitos  {#requirements}

Debe cumplir estos requisitos antes de comprobar el estado de su nombre de dominio en Cloud Manager.

* Primero debe agregar un registro TXT para el dominio personalizado como se describe en el documento [Agregar un registro TXT.](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)

## Cómo comprobar el estado del nombre de dominio personalizado {#how-to}

Puede determinar el estado del nombre de dominio personalizado en Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en **Configuración de dominio** en el panel de navegación izquierdo.

1. Haga clic en el icono **Estado** del nombre de dominio.

Se muestra el detalle del estado. Su dominio personalizado está listo para usarse cuando se muestre el estado **Dominio verificado e implementado**. Consulte la [siguiente sección](#statuses) para obtener detalles sobre los diferentes estados y qué significan.

>[!NOTE]
>
>Cloud Manager guardará automáticamente en déclencheur la verificación cuando seleccione **Crear** en el paso de verificación del asistente **Agregar dominio personalizado** al [agregar un nuevo nombre de dominio personalizado a Cloud Manager.](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) Para las verificaciones subsiguientes, debe seleccionar el icono Verificar de nuevo situado junto al estado.

## Explicación de los estados de verificación {#statuses}

Cloud Manager comprobará la propiedad del dominio mediante el [valor TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) y mostrará uno de los siguientes mensajes de estado.

* **Error en la comprobación del dominio**: falta el valor TXT o se detecta con errores.

   * Siga las instrucciones proporcionadas en el mensaje de estado para resolver el problema.
   * Cuando esté listo, debe seleccionar el icono **Verificar de nuevo** junto al estado.

* **Verificación de dominio en curso**: la verificación está en curso.

   * Este estado suele verse después de seleccionar el icono **Verificar de nuevo** junto al estado.
   * La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.

* **Verificado, Error De Implementación**: la verificación TXT se realizó correctamente, pero la implementación de CDN falló.

   * En tales casos, póngase en contacto con su representante de Adobe.

* **Dominio verificado e implementado**: este estado indica que el nombre de dominio personalizado está listo para utilizarse.

   * En este punto, su nombre de dominio personalizado está listo para la prueba y se dirigirá al nombre de dominio de Cloud Manager.
   * Consulte [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.

* **Eliminando**: la eliminación de un nombre de dominio personalizado está en curso.

* **Error de eliminación**: error al eliminar el nombre de dominio personalizado y se debe volver a intentar.

   * Consulte [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información.

## Errores de nombre de dominio {#domain-error}

A continuación se indican algunos errores comunes de verificación de nombres de dominio y sus resoluciones habituales.

### Error de dominio no instalado {#domain-not-installed}

Este error puede ocurrir durante la validación del dominio del registro TXT, incluso después de comprobar que el registro se haya actualizado correctamente.

#### Causa de error {#cause}

Fastly fija un dominio a la cuenta inicial que lo registró y ninguna otra cuenta puede registrar un subdominio sin solicitar permiso. Además, solo Fastly le permite asignar un dominio Apex y subdominios asociados a un servicio y una cuenta de Fastly. Si tiene una cuenta existente de Facebook que vincula los mismos Apex y subdominios utilizados para sus dominios de AEM Cloud Service, verá este error.

#### Resolución de errores {#resolution}

El error se corrige de la siguiente manera:

* Elimine el Apex y los subdominios de la cuenta existente antes de instalar el dominio en Cloud Manager.

* Utilice esta opción para vincular el dominio Apex y todos los subdominios a la cuenta de AEM as a Cloud Service de Fastly. Consulte [Uso de dominios en la documentación de Fastly](https://docs.fastly.com/en/guides/working-with-domains) para obtener más información.

* Si el dominio de Apex tiene varios subdominios para páginas tanto AEM as a Cloud Service como no AEM que desee vincular a distintas cuentas de Fastly, intente instalar el dominio en Cloud Manager. Si la instalación del dominio falla, cree un ticket de asistencia al cliente con Fastly para que Adobe pueda seguir con Fastly en su nombre.

>[!TIP]
>
>La solución de los problemas de delegación de dominios con Fastly suele tardar entre 1 y 2 días hábiles. Por este motivo, es muy recomendable instalar los dominios mucho antes de la fecha de lanzamiento.

>[!NOTE]
>
>No enrute el DNS del sitio a direcciones IP de AEM as a Cloud Service si el dominio no se instaló correctamente.

## Configuraciones preexistentes de CDN para nombres de dominio personalizados {#pre-existing-cdn}

Si tiene una configuración de CDN preexistente para sus nombres de dominio personalizados, hay un mensaje informativo en las páginas **Nombres de dominio personalizados** y **Entorno**, que le anima a agregar estas configuraciones a través de la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Adición de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información.

## Siguientes pasos {#next-steps}

Una vez que haya comprobado el estado del dominio en Cloud Manager, deberá configurar los ajustes de DNS agregando registros CNAME o APEX DNS que apunten a AEM as a Cloud Service. Continúe con el documento [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para seguir configurando el nombre de dominio personalizado.
