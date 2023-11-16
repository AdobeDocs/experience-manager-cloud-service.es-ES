---
title: Comprobar el estado del nombre de dominio
description: Obtenga información sobre cómo determinar si Cloud Manager ha verificado correctamente su nombre de dominio personalizado.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 92%

---


# Comprobar el estado del nombre de dominio {#check-status}

Puede determinar el estado del nombre de dominio personalizado en Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Clic **Configuración de dominio** en el panel de navegación izquierdo.

1. Haga clic en el icono **Estado** del nombre de dominio.

Cloud Manager verificará la propiedad del dominio mediante el valor TXT y mostrará uno de los siguientes mensajes de estado.

* **Error en la comprobación del dominio**: falta el valor TXT o se detecta con errores.

   * Siga las instrucciones proporcionadas para resolver el problema.
   * Cuando esté listo, debe seleccionar el icono **Verificar de nuevo** junto al estado.

* **Verificación de dominio en curso**: la verificación está en curso.

   * Este estado suele verse después de seleccionar el icono **Verificar de nuevo** junto al estado.

* **Verificado, Error De Implementación**: la verificación TXT se realizó correctamente, pero la implementación de CDN falló.

   * En tales casos, póngase en contacto con su representante de Adobe.

* **Dominio verificado e implementado**: este estado indica que el nombre de dominio personalizado está listo para utilizarse.

   * En este punto, su nombre de dominio personalizado está listo para la prueba y se dirigirá al nombre de dominio de Cloud Manager.
   * Consulte [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.

* **Eliminando**: la eliminación de un nombre de dominio personalizado está en curso.

* **Error de eliminación**: error al eliminar el nombre de dominio personalizado y se debe volver a intentar.

   * Consulte [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información.

Cloud Manager activará automáticamente una verificación TXT al seleccionar **Guardar** sobre la fase de verificación del asistente **Agregar dominio personalizado**. Para las verificaciones posteriores, debe seleccionar el icono Verificar de nuevo situado junto al estado.

## Errores de nombre de dominio {#domain-error}

A continuación se indican algunos errores comunes de nombres de dominio y sus resoluciones habituales.

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

Si tiene una configuración de CDN preexistente para sus nombres de dominio personalizados, habrá un mensaje informativo en las páginas **Nombres de dominio personalizados** y **Entorno**, lo que le anima a añadir estas configuraciones a través de la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Adición de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información.
