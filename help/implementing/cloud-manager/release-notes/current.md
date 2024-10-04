---
title: Notas de la versión para Cloud Manager 2024.10.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca de las notas de la versión para Cloud Manager 2024.10.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: aa8d4c8c69a96054492b886893414c3e82b2f4ad
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# Notas de la versión para Cloud Manager 2024.10.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2024.10.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte las [notas de la versión actuales de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2024.10.0 en AEM as a Cloud Service es el 3 de octubre de 2024.

La próxima versión está planificada para el viernes, 14 de noviembre de 2024.

## Novedades {#what-is-new}

* <!-- BOTH CS & AMS --> AEM La versión del tipo de archivo utilizada en Cloud Manager ahora se actualiza a la versión 26. Ver [https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> Al agregar un nuevo dominio personalizado, el método de verificación anterior implicaba un largo proceso de validación de DNS. El Adobe ha simplificado este proceso para los clientes de. Ahora, solo debe proporcionar un certificado SSL válido (EV u OV), que sirva como prueba de propiedad. Ya no es necesario actualizar los registros TXT en el DNS.

  >[!NOTE]
  >
  >Esta función solo se aplica a los certificados EV y OV administrados por el cliente. Los certificados DV administrados por el Adobe siguen exigiendo la presencia de un registro CNAME.

  Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

  ![Verificar el dominio de un certificado EV/OV administrado por el cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> Al agregar o editar la infraestructura de red, los valores de los campos Dirección IP y Máscara de red se validan según las siguientes reglas:

   * El espacio de direcciones no debe superponerse a las direcciones definidas en el espacio de direcciones de conexión.
   * Las direcciones DNS deben pertenecer a la máscara de red definida en el espacio de direcciones de conexión o ser públicas.

  ![Agregar cuadro de diálogo de infraestructura de red](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> Se están realizando cambios en el formato de los registros de implementación del entorno para la indexación, la instalación de contenido mutable y la transformación de trabajos.

  >[!NOTE]
  >
  >Este cambio está planificado para su despliegue gradual, con una fecha de finalización prevista en diciembre de 2024.

  ![Implementar en la tarjeta de producción](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  El formato del registro va a cambiar de una entrada simple como la que se muestra a continuación:

  ![Archivo de registro que muestra entradas simples](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  Para ver una entrada JSON en lo siguiente:

  ![Archivo de registro que muestra las entradas json](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## Programa para primeros usuarios {#early-adoption}

Forme parte del programa de adopción anticipada de Cloud Manager y tenga la oportunidad de probar las próximas funciones.

### Traiga su propio Git: ahora con soporte para GitLab y Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La función **Traer tu propio Git** se ha ampliado para incluir compatibilidad con repositorios externos como GitLab y Bitbucket. Esta nueva compatibilidad se suma a la compatibilidad ya existente con repositorios de GitHub privados y empresariales. Al añadir estos nuevos repositorios, también puede vincularlos directamente a sus canalizaciones. Puede alojar estos repositorios en plataformas de nube públicas o dentro de su infraestructura o nube privada. Esta integración también elimina la necesidad de una sincronización constante del código con el repositorio de Adobe y proporciona la capacidad de validar las solicitudes de extracción antes de combinarlas en una rama principal.

Consulte [Agregar repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Agregar repositorio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Actualmente, las comprobaciones de calidad del código de las solicitudes de extracción listas para usar son exclusivas de los repositorios alojados en GitHub, pero se está trabajando en una actualización para ampliar esta funcionalidad a otros proveedores de Git.

Si está interesado en probar esta nueva característica y compartir sus comentarios, envíe un mensaje de correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privada/pública o empresarial.


<!-- ## Bug fixes




## Known Issues {#known-issues} -->
