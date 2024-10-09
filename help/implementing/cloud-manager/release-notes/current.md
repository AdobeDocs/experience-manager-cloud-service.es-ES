---
title: Notas de la versión para Cloud Manager 2024.10.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información sobre las notas de la versión para Cloud Manager 2024.10.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---

# Notas de la versión para Cloud Manager 2024.10.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2024.10.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte las [notas de la versión actuales de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2024.10.0 en AEM as a Cloud Service es el 3 de octubre de 2024. 

La próxima versión está planificada para el 14 de noviembre de 2024.

## Novedades {#what-is-new}

* <!-- BOTH CS & AMS --> La versión del arquetipo de AEM utilizada en Cloud Manager se ha actualizado ya a la versión 26. Consulte [https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> Al añadir un nuevo dominio personalizado, el método de verificación anterior implicaba un largo proceso de validación de DNS. Adobe ha simplificado este proceso para los clientes. Ahora, solo debe proporcionar un certificado SSL válido (EV u OV), que sirva como prueba de propiedad. Ya no es necesario actualizar los registros TXT en DNS.

  >[!NOTE]
  >
  >Esta función solo se aplica a los certificados EV y OV administrados por el cliente. Los certificados DV administrados por Adobe siguen exigiendo la presencia de un registro CNAME.

  Consulte [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

  ![Verificar el dominio de un certificado EV/OV administrado por el cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> Al añadir o editar la infraestructura de red, los valores de los campos Dirección IP y Máscara de red se validan según las siguientes reglas:

   * El espacio de direcciones no debe superponerse a las direcciones definidas en el espacio de direcciones de conexión.
   * Las direcciones DNS deben pertenecer a la máscara de red definida en el espacio de direcciones de conexión o ser públicas.

  ![Cuadro de diálogo Añadir infraestructura de red](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> Se están realizando cambios en el formato de los registros de implementación del entorno para indexación, instalación de contenido mutable y transformación de trabajos.

  >[!NOTE]
  >
  >Este cambio está planificado para su despliegue gradual, con una fecha de finalización prevista en diciembre de 2024.

  ![Implementar en tarjeta de producción](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  El formato del registro va a cambiar de una entrada simple como la que se muestra a continuación:

  ![Archivo de registro mostrando entradas simples](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  A una entrada JSON como la que se muestra a continuación:

  ![Archivo de registro mostrando entradas JSON](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## Programa para primeros usuarios {#early-adoption}

Participe en nuestro programa para primeros usuarios de Cloud Manager y tenga la oportunidad de probar algunas de las próximas funciones.

### Usar su propio Git: ahora se admiten GitLab y Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La función **Usar su propio Git** se ha ampliado para incluir compatibilidad con repositorios externos como GitLab y Bitbucket. Esta nueva compatibilidad se suma a la compatibilidad ya existente con repositorios de GitHub privados y de empresa. Al añadir estos nuevos repositorios, también puede vincularlos directamente a sus canalizaciones. Puede alojar estos repositorios en plataformas públicas en la nube o dentro de su infraestructura o nube privada. Esta integración también elimina la necesidad de sincronización constante del código con el repositorio de Adobe y proporciona la capacidad de validar las solicitudes de extracción antes de combinarlas en una rama principal.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Actualmente, las comprobaciones de calidad del código de las solicitudes de extracción listas para usar son exclusivas de los repositorios alojados en GitHub, pero se está trabajando en una actualización para ampliar esta funcionalidad a otros proveedores de Git.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privado/público o de empresa.


<!-- ## Bug fixes




## Known issues {#known-issues} -->
