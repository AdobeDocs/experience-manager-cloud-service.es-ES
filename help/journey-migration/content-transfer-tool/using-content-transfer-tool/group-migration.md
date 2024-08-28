---
title: Migración de grupos
description: Información general sobre la migración de grupos en AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# Migración de grupos {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="Migración de grupos"
>abstract="La herramienta de transferencia de contenido le ayuda a copiar grupos de su sistema de Adobe Experience Manager AEM () existente en AEM as a Cloud Service."

>[!NOTE]
>Para ver las versiones anteriores de la herramienta de asignación de usuarios, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introducción {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="Los usuarios no se han migrado"
>abstract="La herramienta de transferencia de contenido ya no migra usuarios. Los usuarios deben administrarse en el Admin Console."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Documentación del Admin Console de"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console de la"
>
Como parte del recorrido de transición al as a Cloud Service AEM de Adobe Experience Manager AEM (), los grupos deben migrarse de los sistemas de existentes a AEM as a Cloud Service. Esta tarea la realiza la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los ID de Adobe para acceder al nivel de creación. Este proceso requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en el sistema Identity Management de Adobe (IMS), que proporciona un inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). AEM Debido a este cambio, los usuarios se crean automáticamente en el momento en que inician sesión en él por primera vez mediante IMS.  Por lo tanto, CTT no migra a los usuarios al sistema en la nube.  AEM AEM Los usuarios de IMS deben colocarse en grupos de IMS, que pueden ser grupos migrados o nuevos grupos colocados en los grupos de a los que se les ha concedido permiso para acceder al contenido de la migración que se está migrando en la.  AEM De este modo, los usuarios del sistema en la nube tendrán el mismo acceso que tenían en el sistema de origen de la.

## Detalles de migración del grupo {#group-migration-detail}

La herramienta de transferencia de contenido y Cloud Acceleration Manager migrarán todos los grupos asociados con el contenido que se está migrando al sistema de la nube. AEM La herramienta de transferencia de contenido lo hace copiando todos los grupos del sistema de fuentes de datos durante el proceso de extracción. A continuación, Ingesta de CAM selecciona y migra solo ciertos grupos:

* Hay varios grupos integrados y ya presentes en el sistema de la nube de Target; no se migran nunca.
* Se migrarán los grupos de miembros directos de cualquier grupo integrado al que se haga referencia directa o indirectamente en una directiva ACL o CUG de contenido migrado, para garantizar que los usuarios que sean miembros directos o indirectos de dichos grupos mantengan su acceso al contenido migrado.
* Si un grupo se encuentra en una directiva ACL o CUG de contenido migrado, ese grupo se migrará.
* Otros grupos, como los que no se encuentran en una directiva ACL o CUG, los que ya están en el sistema de destino y los que tienen datos restringidos de exclusividad en el sistema de destino, no se migrarán.

Tenga en cuenta que la ruta registrada o registrada para un grupo es solo la primera ruta que activó la migración de ese grupo y que ese grupo también podría estar en otras rutas de contenido.

La mayoría de los grupos migrados están configurados para ser administrados por IMS.  AEM AEM AEM Esto significa que un grupo en IMS con el mismo nombre se vinculará al grupo en el que se encuentra, y cualquier usuario de IMS en el grupo de IMS se convertirá en usuario y miembro del grupo en el que se encuentra el grupo en el que se encuentra el grupo en el que se encuentra el grupo en el que se encuentra el grupo en el que se encuentra el grupo en el que se encuentra el grupo en el que se encuentra el.  Esto permite a estos usuarios tener acceso al contenido según las directivas ACL o CUG para el grupo.

La excepción a esta configuración de IMS es con grupos creados por colecciones de Assets. AEM Cuando se crea una colección en la nube, se crean grupos para acceder a ella; estos grupos se migran al sistema en la nube, pero no se configuran para que los administre IMS.  Para agregar usuarios de IMS a estos grupos, deben agregarse en la página Propiedades del grupo de la interfaz de usuario de Assets, ya sea de forma individual o colectiva como parte de otro grupo de IMS.


## Excluirse de la migración de grupo {#group-migration-option}

La versión 3.0.20 y posteriores de CTT incluyen una opción para deshabilitar la migración de grupos.  Esto se configura en la consola OSGI de la siguiente manera:

* Abrir la configuración de OSGI `(http://<server> /system/console/configMgr)`
* Haga clic en la configuración llamada **Configuración del servicio de extracción de la herramienta de transferencia de contenido**
* Desmarque **Incluir grupos en la migración** para deshabilitar las migraciones de grupos
* Haga clic en **Guardar** para asegurarse de que la configuración esté guardada y activa en el servidor

Con esta configuración deshabilitada, los grupos no se migrarán y no habrá ningún informe de migración de principales ni informe de usuarios.

## Informe del usuario {#user-report}

Durante la migración, los usuarios no se migran, pero las relaciones entre usuarios y grupos en el sistema de origen se pierden a menos que se capturen de algún modo.  El Informe de usuarios captura parte de esta información en formato de texto en un Informe de usuarios. En él, se informa de cada usuario (uno por línea) junto con una lista de grupos a los que pertenece (pero los grupos no migrados no se incluyen en esta lista), a menos que su lista de grupos esté vacía, en cuyo caso el usuario no aparece. Los grupos notificados junto con cada usuario son aquellos a los que el usuario pertenece directa o indirectamente en el sistema de origen; como los grupos del sistema de origen pueden estar anidados mientras que en el de destino no lo están, esta lista de grupos admite la nueva estructura de grupos aplanados en IMS.

En el caso de un borrado y luego una ingesta sin borrado, los grupos de la lista de un usuario incluirán aquellos grupos migrados en cualquiera de las fases.

Además de los grupos de cada usuario, hay un campo en el informe en el que se pueden añadir notas para el usuario (y también se incluye en el informe una descripción detallada del significado de la nota).  Las notas posibles son:

* Los usuarios a los que se hace referencia directamente en una ACL tendrán *Note-A* en su sección de notas, ya que este no es un caso de uso recomendado ni una práctica recomendada.
* Los usuarios que sean miembros directos de un grupo integrado tendrán *Nota-B* en su sección de notas, ya que tampoco es un caso de uso recomendado ni una práctica recomendada.

Estos casos pueden ocurrir simultáneamente, y también al mismo tiempo que los casos anteriores.

El informe del usuario se agrega al final del informe de migración principal (y, por lo tanto, forma parte de él) (consulte [Resumen final e informe](#final-summary-and-report) más abajo).

## Consideraciones adicionales {#additional-considerations}

* Si se establece la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta**, los grupos transferidos anteriormente a la instancia de Cloud Service se eliminan junto con todo el repositorio existente; se crea un nuevo repositorio en el que se ingiere contenido. Este proceso también restablece todas las opciones de configuración, incluidos los permisos, en la instancia del Cloud Service de destino y se aplica a todos los usuarios agregados al grupo **administrators**. Se debe volver a agregar el usuario administrador al grupo **administradores** para recuperar el token de acceso para la ingesta de CTT/CAM.
* Cuando se realizan ingestas que no son de borrado (**Borrar contenido existente** no está establecido), si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, tampoco se transfieren los grupos asociados con ese contenido. Esta regla es verdadera incluso si los grupos han cambiado en el sistema de origen. Esto se debe a que los grupos solo se migran junto con el contenido con el que están asociados. Debido a esto, en este caso cualquier grupo que sea miembro de un grupo en el sistema de origen no se migrará a menos que forme parte de un grupo diferente que se esté migrando o en la ACL de contenido diferente que se esté migrando. Para migrar estos grupos posteriormente, considere la posibilidad de utilizar paquetes, eliminar grupos del destino y volver a migrar el contenido relevante, o volver a migrar mediante una ingesta de borrado.
* AEM Durante una ingesta sin borrado, si existe un grupo con cualquiera de los mismos datos restringidos por unicidad (rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId) tanto en la instancia de origen como en la instancia de AEM Cloud Service de destino, el grupo en cuestión se migra _no_ y el grupo existente anteriormente en el sistema en la nube permanece sin cambios. Esto se registra en el Informe de migración de principales.
* Consulte [Migración de grupos de usuarios cerrados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para obtener consideraciones adicionales para los grupos utilizados en una directiva de grupo de usuarios cerrados (CUG).

## Resumen final e informe

Una vez que la extracción y la ingesta han finalizado correctamente, se genera un informe con los detalles de migración del grupo. Consulte [Cómo validar la migración de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration) para obtener más información.
