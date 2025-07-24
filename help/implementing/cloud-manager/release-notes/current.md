---
title: Notas de la versión 2025.7.0 de Cloud Manager
description: Obtenga información sobre la versión 2025.7.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f3e31d1f17283086cd6fe9e73d67feac938d6567
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 98%

---

# Notas de la versión 2025.7.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre la versión 2025.7.0 de Cloud Manager en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.7.0 en AEM as a Cloud Service fue el jueves, 10 de julio de 2025.

La próxima versión está planificada para el jueves, 7 de agosto de 2025.

## Novedades {#what-is-new}

* **Cloud Manager añade compatibilidad con los certificados SSL de ECDSA (Elliptic Curve Digital Signature Algorithm)**

  Cloud Manager ahora admite certificados ECDSA. La función ofrece una gran seguridad con tamaños de clave más pequeños, lo que permite a los clientes aplicar criptografía moderna y ligera en sus configuraciones de CDN. <!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **Descarga del informe de uso de licencia del sitio**

  En la página **Detalles de uso de los sitios** (en Cloud Manager, haga clic en **Licencia**. En la tabla Soluciones, en la fila **Sitios**, haga clic en **Ver detalles de uso**), los clientes ahora pueden hacer clic en **Descargar informe** para exportar sus datos como un archivo CSV. Esta descarga simplifica el análisis y el uso compartido de las tendencias de uso. <!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![Página de detalles de uso de los sitios](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

  Consulte el [panel de control de licencias](/help/implementing/cloud-manager/license-dashboard.md).

## Programas de Alpha/Beta {#private-beta-program}

Participe en los programas alfa y beta de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades:

### Reversión en un solo clic para implementaciones de canalización {#one-click-rollback}

Vuelva rápidamente a una implementación anterior si el código fuente del cliente más reciente no funciona como se esperaba; no es necesario volver a ejecutar la canalización completa ni revertir las confirmaciones manualmente.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Restaurar código fuente del cliente desde la tarjeta Entornos](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *La tarjeta Entornos muestra la opción **Restaurar**>**Código anterior implementado**&#x200B;para un entorno seleccionado.*


![Cuadro de diálogo Restaurar código anterior implementado](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*En el cuadro de diálogo **Restaurar código anterior implementado**, revise la versión implementada actualmente y la versión que desea restaurar, luego haga clic en **Confirmar***.


![Activación de Restaurando](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager revierte el entorno a la versión anterior, mantiene el contenido y la configuración intactos y marca el entorno **Restaurando**&#x200B;hasta que finalice la implementación.*


![Versión del código fuente en uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *La vista de detalles del entorno, vista desde arriba, ahora también muestra la versión activa del código fuente en uso.*

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [restorecode@adobe.com](mailto:restorecode@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

Consulte [Restaurar el código anterior implementado en AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulte [Restauración de contenido en AEM as a Cloud Service](/help/operations/restore.md).


### Entorno de pruebas especializadas {#specialized-test-environment}

Cloud Manager ahora admite la adición de un nuevo tipo de entorno denominado **Entorno de prueba especializado**. El entorno está diseñado para ayudar a los equipos a validar las funciones en condiciones casi de producción antes de su lanzamiento. Este tipo de entorno es distinto de los entornos *Producción + Fase*, *Desarrollo* o *Desarrollo rápido*, y ofrece un espacio dedicado para ejecutar escenarios de validación avanzados.

Mejora reciente: Ahora puede configurar entornos de prueba especializados en una canalización que no sea de producción a través de un flujo de trabajo más sencillo e intuitivo. La configuración optimizada acelera la finalización y reduce los errores de configuración.

Consulte [Adición de un entorno de prueba especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Cuadro de diálogo Añadir entorno con el botón de opción Entorno de prueba especializado seleccionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.


### Traiga su propio Git (BYOG), ahora compatible con Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Los clientes ahora pueden incorporar sus repositorios Git de Azure DevOps en Cloud Manager, con compatibilidad tanto con los repositorios modernos de Azure DevOps como con los repositorios heredados de VSTS (Visual Studio Team Services).

* Para los usuarios de Edge Delivery Services, el repositorio incorporado se puede utilizar para sincronizar e implementar el código del sitio.
* Para los usuarios de AEM as a Cloud Service y Adobe Managed Services (AMS), el repositorio se puede vincular a canalizaciones de pila completa y de front-end.

La compatibilidad con tipos de canalización adicionales y la validación de solicitudes de extracción a través de canalizaciones de calidad de código estará disponible pronto.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privado/público o de empresa.


**Preguntas frecuentes sobre BYOG**

| Pregunta | Respuesta |
|---|---|
| *¿Cómo puede un proyecto volver al repositorio de Git administrado por Adobe si es necesario?* | Volver atrás es sencillo. [Actualice las canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para que apunten al repositorio de Adobe y quite el repositorio externo si ya no es necesario. |
| *¿Es posible configurar diferentes repositorios para diferentes entornos (por ejemplo, no producción frente a producción) para permitir primero las pruebas en no producción?* | Sí, se pueden configurar diferentes repositorios para entornos independientes. Por ejemplo, la canalización de desarrollo o de calidad del código puede apuntar a un repositorio externo, mientras que la canalización de producción permanece conectada al repositorio de Adobe. Asegúrese de que el trabajo de sincronización entre los dos repositorios permanece activo durante esta configuración. |
| *¿Continúa funcionando la configuración existente, como las listas de IP permitidas?* | Sí, las listas de IP permitidas existentes siguen funcionando como de costumbre. Sin embargo, si el repositorio de Git externo está protegido por un firewall, las [direcciones IP de Adobe necesarias deben añadirse a la lista de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *¿Funcionan todas las URL del repositorio de GitLab? La URL del repositorio en uso sigue el formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difiere del ejemplo de la documentación.* | Sí, se admite cualquier repositorio de GitLab que admita API V3 o V4, incluidas las URL de GitLab autoalojado como la descrita en [Añadir repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Administrar tókenes de acceso{#manage-access-tokens}

Use **Administrar tokens de acceso** en Cloud Manager para ver, cambiar el nombre y eliminar los tokens de acceso asociados con repositorios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket y Azure DevOps.

Consulte [Administración de tokens de acceso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. 


### Añadir canalización de configuración de Edge Delivery {#add-eds-pipeline}

Ahora se admiten las canalizaciones de configuración para los sitios creados con Edge Delivery Services, lo que amplía esta capacidad más allá de los entornos de Cloud Service. Puede usar las **canalizaciones de configuración** para administrar las configuraciones como las reglas de filtrado de tráfico y las configuraciones WAF cuando corresponda. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

![Añadir canalización de Edge Delivery a la lista desplegable Añadir canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Adición de una canalización de Edge Delivery desde la página **Información general del programa**, tarjeta **Canalizaciones**.*

![Cuadro de diálogo Añadir canalización de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Cuadro de diálogo Añadir canalización de Edge Delivery.*

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.


## Correcciones de errores

* Cloud Manager ahora actualiza la versión de lanzamiento para todas las canalizaciones durante las actualizaciones del entorno, lo que garantiza un seguimiento coherente de las versiones en todos los tipos de canalizaciones. <!-- CMGR-69043 -->
* La interfaz de usuario ahora muestra el estado y los mensajes de error detallados cuando falla un certificado SSL de validación de dominio (DV), lo que ayuda a comprender y resolver problemas de certificado. <!-- CMGR-68872 -->
* Al editar una asignación de dominio, ahora la interfaz de usuario evita seleccionar certificados SSL que no coinciden con el dominio elegido, lo que reduce las configuraciones incorrectas y mejora la fiabilidad durante la configuración. <!-- CMGR-64307 -->
* En algunas situaciones, los certificados no se eliminaban correctamente, por lo que el mantenimiento del dominio sigue activo. <!-- CMGR-69867 -->
* Se ha corregido un problema que podía bloquear las actualizaciones de *Adobe Assets* a *Adobe Assets Ultimate* en algunos casos. Las transiciones son ahora más suaves y fiables. <!-- CMGR-69506 -->
* Se ha resuelto un problema en el cual los campos de región clave se establecen automáticamente al crear entornos de varias regiones para admitir servicios e implementaciones posteriores sin problemas. <!-- CMGR-69471 -->
* Se ha resuelto un problema en el cual algunas canalizaciones de configuración no se detenían correctamente después de la ejecución. Ahora, las canalizaciones se completan correctamente y se cierran según lo esperado, lo que mejora la fiabilidad. <!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->

