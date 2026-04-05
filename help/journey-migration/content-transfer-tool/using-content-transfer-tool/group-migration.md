---
title: Migración de grupos
description: Información general sobre la migración de grupos en AEM as a Cloud Service.
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 3%

---


# Migración de grupos {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="Migración de grupos"
>abstract="La herramienta de transferencia de contenido le ayuda a copiar grupos de su sistema de Adobe Experience Manager (AEM) existente a AEM as a Cloud Service. "

>[!NOTE]
>Para ver las versiones anteriores de la herramienta de asignación de usuarios, consulte la [documentación heredada](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## Introducción {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="Los usuarios no se migran"
>abstract="La herramienta de transferencia de contenido ya no migra a los usuarios. Los usuarios deben administrarse en la Admin Console."
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentación del Admin Console de AEM"
>additional-url="https://adminconsole.adobe.com/" text="Admin Console de AEM"

Como parte del recorrido de transición a Adobe Experience Manager (AEM) as a Cloud Service, los grupos deben migrarse de los sistemas AEM existentes a AEM as a Cloud Service. Esta tarea la realiza la herramienta de transferencia de contenido.

Un cambio importante en AEM as a Cloud Service es el uso completamente integrado de los Adobe ID para acceder al nivel de Author. Este proceso requiere el uso de [Adobe Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html) para administrar usuarios y grupos de usuarios. La información de perfil de usuario está centralizada en Adobe Identity Management System (IMS), que proporciona un inicio de sesión único en todas las aplicaciones de la nube de Adobe. Para obtener más información, consulte [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html?lang=es#identity-management). Debido a este cambio, los usuarios se crean automáticamente en AEM la primera vez que inician sesión en él a través de IMS.  Por lo tanto, CTT no migra a los usuarios al sistema en la nube.  Los usuarios de IMS deben colocarse en grupos de IMS, que pueden ser grupos migrados o nuevos grupos colocados en los grupos de AEM a los que se ha concedido permiso para acceder al contenido de AEM que se está migrando.  De este modo, los usuarios del sistema en la nube tendrán el mismo acceso que tenían en el sistema AEM de origen.

## Detalles de migración del grupo {#group-migration-detail}

La herramienta de transferencia de contenido y Cloud Acceleration Manager migrarán todos los grupos asociados con el contenido que se está migrando al sistema de la nube. La herramienta de transferencia de contenido lo hace copiando todos los grupos del sistema AEM de origen durante el proceso de extracción. A continuación, Ingesta de CAM selecciona y migra solo ciertos grupos:

* Si un grupo se encuentra en una directiva ACL o CUG de contenido migrado, ese grupo se migrará, con algunas excepciones que se enumeran a continuación.
* Hay varios grupos integrados y ya presentes en el sistema de la nube de Target; no se migran nunca.
   * Algunos grupos integrados pueden incluir grupos de miembros que están integrados _no_; cualquier grupo de miembros (miembros directos o miembros de miembros, etc.) al que se haga referencia en una directiva ACL o CUG de contenido migrado se migrará para garantizar que los usuarios que sean miembros de estos grupos (directa o indirectamente) mantengan su acceso al contenido migrado.
* Otros grupos, como los que no se encuentran en una directiva ACL o CUG, los que ya están en el sistema de destino y los que tienen datos restringidos de exclusividad en el sistema de destino, no se migrarán.

Tenga en cuenta que la ruta registrada o registrada para un grupo es solo la primera ruta que activó la migración de ese grupo y que ese grupo también podría estar en otras rutas de contenido.

La mayoría de los grupos migrados están configurados para ser administrados por IMS.  Esto significa que un grupo en IMS con el mismo nombre se vinculará al grupo en AEM, y cualquier usuario de IMS en el grupo de IMS se convertirá en usuario de AEM y miembro del grupo en AEM.  Esto permite a estos usuarios tener acceso al contenido según las directivas ACL o CUG para el grupo.

Tenga en cuenta que los grupos migrados ya no se consideran &quot;grupos locales&quot; de AEM; son grupos listos para IMS en AEM, aunque es posible que aún no existan en IMS.  Se deben volver a crear por separado en IMS para que se puedan sincronizar entre AEM e IMS.  Los grupos se pueden crear en IMS mediante Admin Console, entre otros métodos, de forma individual o en lote.  Consulte [Administrar grupos de usuarios](https://helpx.adobe.com/es/enterprise/using/user-groups.html) para obtener más información sobre cómo crear grupos de forma individual o en masa en Admin Console.

La excepción a esta configuración de IMS es con grupos creados por colecciones y carpetas privadas de Assets. Cuando se crea una colección o una carpeta privada en AEM, se crean grupos para acceder a ese contenido; dichos grupos se migran al sistema en la nube, pero no se configuran para que los administre IMS.  Para agregar usuarios de IMS a estos grupos, deben agregarse en la página Propiedades del grupo de la interfaz de usuario de Assets, ya sea de forma individual o colectiva como parte de otro grupo de IMS.


## Excluirse de la migración de grupo {#group-migration-option}

La versión 3.0.20 y posteriores de CTT incluyen una opción para deshabilitar la migración de grupos.  Esto se configura en la consola OSGI de la siguiente manera:

* Abrir la configuración de OSGI `(http://<server>/system/console/configMgr)`
* Haga clic en la configuración llamada **Configuración del servicio de extracción de la herramienta de transferencia de contenido**
* Desmarque **Incluir grupos en la migración** para deshabilitar las migraciones de grupos
* Haga clic en **Guardar** para asegurarse de que la configuración esté guardada y activa en el servidor

Con esta configuración deshabilitada, los grupos no se migrarán y no habrá ningún informe de migración de principales ni informe de usuarios (ver a continuación).

## Informe de migración principal e informe de usuario {#principal-migration-report}

Cuando los grupos se incluyen durante la migración (opción predeterminada), se guarda un Informe de migración de principales que describe lo que sucede a cada grupo durante la migración.  Para descargar este informe después de una ingesta correcta:

* En CAM, vaya a Transferencia de contenido y seleccione Trabajos de ingesta.
* Haga clic en los puntos suspensivos (...) en la línea de la Ingesta en cuestión y seleccione &quot;Ver resumen principal&quot;.
* En el cuadro de diálogo que aparece, seleccione &quot;Informe de migración de principales&quot; en la lista desplegable debajo de &quot;Descargar un archivo...&quot; y haga clic en el botón Descargar.
* Guarde el archivo CSV resultante.

Parte de la información registrada por grupo es:

* Si se migra, la ruta a la primera ACL o CUG que provocó la migración del grupo.
* Si el grupo se migró anteriormente; si la ingesta actual es una ingesta sin borrado, es posible que algunos grupos se hayan migrado durante una ingesta anterior.
* Si el grupo es un grupo integrado; estos grupos no se migran porque siempre están en el entorno de AEMaaCS de destino.
* Si el grupo no formaba parte de una ACL o un CUG en el contenido migrado, no se habría migrado.
* Si el grupo era un grupo local, como un grupo creado por una colección de Assets, es posible que se haya migrado y, en este caso, se agrega la palabra &quot;local&quot; al informe de ese grupo.

Durante la migración, los usuarios no se migran, pero las relaciones entre usuarios y grupos en el sistema de origen se perderían a menos que se capturaran de algún modo. El proceso de Ingesta captura parte de esta información en formato de texto en un Informe del usuario, que se encuentra al final del Informe de migración principal.

### Informe del usuario {#user-report}

En la sección Informe de usuarios se informa de los usuarios (uno por línea) junto con su dirección de correo electrónico y una lista de grupos habilitados para IMS que se migraron durante esta ingesta.  Los grupos que no se migraron, que se migraron durante una ingesta anterior o que son grupos locales no se incluyen en la lista.   Si un usuario no está en ningún grupo migrado habilitado para IMS y no tiene notas adicionales que indiquen que es un caso especial (consulte **Notas** más abajo), ese usuario _no_ aparece en el informe. Los grupos notificados junto con cada usuario son aquellos a los que el usuario pertenece, directa o indirectamente, en el sistema de origen; como los grupos del sistema de origen pueden estar anidados mientras que en el de destino no lo están, esta lista de grupos admite la nueva estructura de grupos aplanados en IMS.

En el caso de una operación de borrado y, a continuación, de una ingesta sin borrado, los grupos de la lista de un usuario a partir de la operación de borrado solo serán aquellos grupos migrados durante la fase sin borrado.

#### Notas {#user-report-notes}

Además de los grupos de cada usuario, hay un campo en el Informe del usuario en el que se pueden proporcionar notas sobre el usuario (y también se incluye una descripción detallada del significado de la nota en el informe) con fines informativos.  Las notas posibles son:

* **Nota-A** Los usuarios a los que se hace referencia directamente en una ACL tendrán *Nota-A* en su sección de notas, ya que este no es un caso de uso recomendado ni una práctica recomendada.
* **Nota-B** Los usuarios que sean miembros directos de un grupo integrado tendrán *Nota-B* en su sección de notas, ya que tampoco es un caso de uso recomendado o una práctica recomendada.
* **Note-C** Los usuarios que sean miembros directos de un grupo local migrado (como un grupo creado por una colección Assets) tendrán *Note-C* en su sección de notas, ya que los grupos locales no están configurados para ser administrados por IMS.

Estos casos pueden ocurrir simultáneamente, y también al mismo tiempo que los casos anteriores.  _Para obtener información adicional sobre los grupos a los que hace referencia cada nota para cada usuario, consulte el registro de ingesta; informa de esta información para cada usuario._

El Informe de usuarios se agrega al final del Informe de migración principal (y, por lo tanto, forma parte de él) (vea [Resumen final e Informe](#final-summary-and-report) más abajo) para que los clientes comprendan mejor los grupos, los usuarios y sus relaciones.

## Archivos de carga masiva {#bulk-upload-files}

Como los grupos solo se migran a AEM as a Cloud Service, también se deben agregar a IMS para que puedan trabajar correctamente con AEM en la nube. Además, los usuarios no se migran, por lo que también deben añadirse a IMS. La herramienta de migración CTT/CAM no realiza este paso, pero el proceso de Ingesta crea dos archivos de carga masiva, uno para grupos y otro para usuarios. Estos archivos se pueden editar y utilizar, junto con la funcionalidad de carga masiva de Admin Console, para crear grupos y usuarios de IMS basados en los grupos y usuarios de AEM.

Consulte [Carga masiva de grupos y usuarios a IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md) para obtener detalles sobre cómo usar la carga masiva de archivos para crear usuarios y grupos mediante Admin Console.

Consulte también [Administrar usuarios](https://helpx.adobe.com/ca/enterprise/using/users.html) para obtener más información acerca de la administración de usuarios de AEM as a Cloud Service.

## Consideraciones adicionales {#additional-considerations}

* Si se establece la configuración **Borrar contenido existente en la instancia de Cloud antes de la ingesta**, los grupos transferidos anteriormente a la instancia de Cloud Service se eliminan junto con todo el repositorio existente; se crea un nuevo repositorio en el que se ingiere contenido. Este proceso también restablece todas las opciones de configuración, incluidos los permisos, en la instancia de Cloud Service de destino y se aplica al usuario agregado al grupo **administradores**. Se debe volver a agregar el usuario administrador al grupo **administradores** para recuperar el token de acceso para la ingesta de CTT/CAM.
* Cuando se realizan ingestas que no son de borrado (**Borrar contenido existente** no está establecido), si el contenido no se transfiere porque no ha cambiado desde la transferencia anterior, tampoco se transfieren los grupos asociados con ese contenido. Esta regla es verdadera incluso si los grupos han cambiado en el sistema de origen. Esto se debe a que los grupos solo se migran junto con el contenido con el que están asociados. Debido a esto, en este caso cualquier grupo que sea miembro de un grupo en el sistema de origen no se migrará a menos que forme parte de un grupo diferente que se esté migrando o en la ACL de contenido diferente que se esté migrando. Para migrar estos grupos posteriormente, considere la posibilidad de utilizar paquetes, eliminar grupos del destino y volver a migrar el contenido relevante, o volver a migrar mediante una ingesta de borrado.
* Durante una ingesta sin borrado, si existe un grupo con cualquiera de los mismos datos restringidos por unicidad (rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId) tanto en la instancia de AEM de origen como en la instancia de Cloud Service de AEM de destino, el grupo en cuestión se migra a _no_ y el grupo existente anteriormente en el sistema en la nube permanece sin cambios. Esto se registra en el Informe de migración de principales.
* Consulte [Migración de grupos de usuarios cerrados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para obtener consideraciones adicionales para los grupos utilizados en una directiva de grupo de usuarios cerrados (CUG).

## Resumen final e informe

Una vez que la extracción y la ingesta han finalizado correctamente, se genera un informe con los detalles de migración del grupo. Consulte [Cómo validar la migración de grupo](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration) para obtener más información.
