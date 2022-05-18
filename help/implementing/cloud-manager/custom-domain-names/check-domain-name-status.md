---
title: Comprobación del estado del nombre de dominio
description: Obtenga información sobre cómo determinar si Cloud Manager ha verificado correctamente su nombre de dominio personalizado.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# Comprobación del estado del nombre de dominio {#check-status}

Puede determinar el estado del nombre de dominio personalizado en Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Entornos** de la **Información general** página.

1. Haga clic en **Configuración de dominio** en el panel de navegación izquierdo.

1. Haga clic en el **Estado** para el nombre de dominio.

Cloud Manager verificará la propiedad del dominio mediante el valor TXT y mostrará uno de los siguientes mensajes de estado.

* **Error en la comprobación del dominio** - Falta el valor TXT o se detecta con errores.

   * Siga las instrucciones proporcionadas para resolver el problema.
   * Cuando esté listo, debe seleccionar la opción **Verificar de nuevo** junto al estado .

* **Verificación de dominio en curso** - La verificación está en curso.

   * Este estado suele verse después de seleccionar la variable **Verificar de nuevo** junto al estado .

* **Verificado, Error De Implementación** : la verificación TXT se realizó correctamente, pero la implementación de CDN falló.

   * En tales casos, póngase en contacto con su representante del Adobe.

* **Dominio verificado e implementado** : este estado indica que el nombre de dominio personalizado está listo para utilizarse.

   * En este punto, su nombre de dominio personalizado está listo para la prueba y se dirigirá al nombre de dominio de Cloud Manager.
   * Consulte el documento [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) para obtener más información.

* **Eliminación** - La eliminación de un nombre de dominio personalizado está en curso.

* **Error de eliminación** - Error al eliminar el nombre de dominio personalizado y se debe volver a intentar.

   * Consulte el documento [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información.

Cloud Manager almacenará en déclencheur automáticamente una verificación TXT al seleccionar **Guardar** sobre la fase de verificación del **Agregar dominio personalizado** asistente. Para las verificaciones posteriores, debe seleccionar activamente el icono de verificación de nuevo situado junto al estado .

## Errores de nombre de dominio {#domain-error}

En esta sección se explican los errores que podría ver y cómo resolverlos.

**Dominio no instalado** - Recibe este error durante la validación del dominio del registro TXT incluso después de comprobar que el registro se ha actualizado correctamente.

**Explicación del error** - Enciende un dominio a la cuenta inicial que lo registró y ninguna otra cuenta puede registrar un subdominio sin solicitar permiso. Además, solo permite asignar un dominio de ápice y subdominios asociados a un servicio y una cuenta de Afinidad. Si tiene una cuenta existente de Facebook que vincula los mismos apex y subdominios utilizados para sus dominios de AEM Cloud Service, verá este error.

**Resolución de errores** - El error se corrige de la siguiente manera:

* Elimine la ápice y los subdominios de la cuenta existente antes de instalar el dominio en Cloud Manager. Utilice esta opción para vincular el dominio de ápice y todos los subdominios a la cuenta de AEM as a Cloud Service de FPrimera. Consulte [Uso de dominios en la documentación rápida](https://docs.fastly.com/en/guides/working-with-domains) para obtener más información.

* Si el dominio de apex tiene varios subdominios para AEM sitios as a Cloud Service as a Cloud Service y no AEM que desee vincular a distintas cuentas de Ffront, intente instalar el dominio en Cloud Manager y, si la instalación del dominio falla, cree un ticket de asistencia al cliente con Finfinito para que podamos realizar el seguimiento con Finfinito en su nombre.

>[!NOTE]
>
>NOTA: No enrute el DNS del sitio a direcciones IP as a Cloud Service AEM si el dominio no se instaló correctamente.

## Configuraciones preexistentes de CDN para nombres de dominio personalizados {#pre-existing-cdn}

Si tiene una configuración de CDN preexistente para sus nombres de dominio personalizados, habrá un mensaje informativo en la variable **Nombres de dominio personalizados** y **Entorno** , lo que le anima a añadir estas configuraciones a través de la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario de . El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte el documento [Adición de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información.
