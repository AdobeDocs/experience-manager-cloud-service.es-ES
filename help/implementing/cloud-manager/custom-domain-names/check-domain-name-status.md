---
title: Comprobar estado del nombre de dominio
description: Obtenga información sobre cómo comprobar que Cloud Manager ha confirmado correctamente su nombre de dominio personalizado.
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d35610b204cc2e06fefa93e048c16940cf1c47c
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 20%

---


# Comprobar estado del nombre de dominio {#check-status}

Obtenga información sobre cómo comprobar que Cloud Manager ha confirmado correctamente su nombre de dominio personalizado.

## Comprobar el estado de un nombre de dominio personalizado {#how-to}

Antes de comprobar el estado de su nombre de dominio en Cloud Manager, asegúrese de haber agregado un certificado SSL administrado por el cliente (OV/EV) para su dominio personalizado como se describe en [Agregar un certificado SSL administrado por el cliente](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md##add-customer-managed-ssl-cert).

**Para comprobar el estado de un nombre de dominio personalizado:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en **Configuración de dominio** en el menú del lado izquierdo.

1. Haga clic en el icono **Estado** del nombre de dominio.

Se muestra el detalle del estado. Su dominio personalizado está listo para usarse cuando se muestre el estado **Dominio verificado e implementado**. Consulte la [siguiente sección](#statuses) para obtener detalles sobre los diferentes estados y qué significan.

>[!NOTE]
>
>Si usa un *certificado SSL administrado por Adobe (DV)* con el dominio, Cloud Manager registra automáticamente la verificación de déclencheur al hacer clic en **Verificar** en el cuadro de diálogo Verificar dominio al [agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
>
>Si planea usar un certificado SSL **administrado por el cliente (OV/EV)**, su dominio se verifica *después de* de [agregar el certificado SSL OV/EV](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).


## Estados de verificación {#statuses}

Cloud Manager verifica la propiedad del dominio a través del certificado SSL administrado por el cliente (OV/EV). Cuando termina, muestra uno de los siguientes mensajes de estado:

| Estado | Descripción |
| --- | --- |
| Error de verificación de dominio | Falta el certificado EV/OV administrado por el cliente o se detecta con errores.<br> Siga las instrucciones proporcionadas en el mensaje de estado para resolver el problema. Cuando esté listo, debe seleccionar el icono **Verificar de nuevo** junto al estado. |
| Verificación del dominio en curso | La verificación está en curso.<br>Este estado suele verse después de seleccionar el icono **Verificar de nuevo** junto al estado. La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS. |
| Verificado: error de implementación | La verificación del certificado EV/OV se realizó correctamente, pero la implementación de CDN falló.<br>En estos casos, póngase en contacto con su representante de Adobe. |
| Dominio verificado e implementado | Este estado indica que el nombre de dominio personalizado está listo para utilizarse.<br>En este momento, su nombre de dominio personalizado está listo para la prueba y se dirigirá al nombre de dominio de Cloud Manager. Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información. |
| Eliminando | La eliminación de un nombre de dominio personalizado está en curso. |
| Error de eliminación | Error al eliminar un nombre de dominio personalizado y se debe volver a intentar.<br>Vea [Administrar nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información. |


## Errores de nombre de dominio {#domain-error}

A continuación se indican algunos errores comunes de verificación de nombres de dominio y sus resoluciones habituales.

### Error de dominio no instalado {#domain-not-installed}

Este error puede producirse durante la validación del dominio del certificado EV/OV incluso después de comprobar que el certificado se ha actualizado correctamente.

#### Causa de error {#cause}

Fastly fija un dominio a la cuenta que lo registra primero, y otras cuentas deben solicitar permiso para registrar un subdominio. Además, solo Fastly le permite asignar un dominio Apex y subdominios asociados a un servicio y una cuenta de Fastly. Si tiene una cuenta existente de Facebook que vincula los mismos Apex y subdominios utilizados para sus dominios de AEM Cloud Service, verá este error.

#### Resolución de errores {#resolution}

El error se corrige de la siguiente manera:

* Elimine el Apex y los subdominios de la cuenta existente antes de instalar el dominio en Cloud Manager.

* Utilice esta opción para vincular el dominio Apex y todos los subdominios a la cuenta de AEM as a Cloud Service de Fastly. Consulte [Uso de dominios en la documentación de Fastly](https://docs.fastly.com/en/guides/working-with-domains) para obtener más información.

* Si el dominio Apex tiene varios subdominios para sitios de AEM as a Cloud Service y que no sean de AEM que necesitan vincularse a diferentes cuentas de Fastly, intente instalar el dominio en Cloud Manager. Este proceso ayuda a administrar las conexiones de subdominios en diferentes cuentas de Fastly. Si la instalación del dominio falla, cree un ticket de asistencia al cliente con Fastly para que Adobe pueda realizar el seguimiento con Fastly en su nombre.

>[!TIP]
>
>La solución de los problemas de delegación de dominios con Fastly suele tardar entre 1 y 2 días hábiles. Por este motivo, se recomienda instalar los dominios mucho antes de la fecha de lanzamiento.

>[!NOTE]
>
>No enrute el DNS del sitio a direcciones IP de AEM as a Cloud Service si el dominio no se instaló correctamente.

## Configuraciones preexistentes de CDN para nombres de dominio personalizados {#pre-existing-cdn}

Si ya tiene una configuración de CDN (red de distribución de contenido) para sus nombres de dominio personalizados, aparecerá un mensaje informativo en las páginas **Nombres de dominio personalizados** y **Entorno**. Le anima a añadir estas configuraciones a través de la interfaz de usuario para que se puedan administrar y ver en Cloud Manager.

El mensaje desaparece después de migrar todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para obtener más información.

## Pasos siguientes {#next-steps}

Después de comprobar el estado del dominio en Cloud Manager, configure las opciones de DNS agregando registros DNS, CNAME o APEX que apunten a AEM as a Cloud Service. Continúe con el documento [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para continuar configurando el nombre de dominio personalizado.
