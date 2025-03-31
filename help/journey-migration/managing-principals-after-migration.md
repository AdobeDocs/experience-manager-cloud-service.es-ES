---
title: Administración de principales después de la migración
description: Obtenga información sobre cómo configurar usuarios y grupos en IMS y AEM
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: 50c8dd725e20cbd372a7d7858fc67b0f53a8d6d4
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 61%

---

# Administración de principales después de la migración {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Administración de principales después de la migración"
>abstract="Obtenga información sobre cómo configurar usuarios y grupos en IMS y AEM"

En este documento se describen los pasos de alto nivel que los clientes deben realizar para configurar los usuarios y grupos en IMS y AEM para trabajar con su entorno de AEM as a Cloud Service.

Para obtener información sobre la migración de grupos y el informe de migración de entidades principales disponible con cada ingesta, consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md).

Para obtener una guía sobre el uso de archivos de grupos y usuarios en masa en Admin Console, consulte [Carga masiva de identidades a IMS después de usar CTT](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md).

## Administración de principales {#managing-principals}

Para AEM as a Cloud Service, los usuarios y grupos deben administrarse principalmente mediante Admin Console. Al considerar una migración, algunas de estas tareas se pueden llevar a cabo antes de que se produzca la migración de contenido.  Básicamente, uno de estos grupos de tareas principales

* Crear usuarios y grupos en IMS
* Asignar usuarios a grupos en IMS
* Asignar grupos IMS a grupos AEM (si es necesario)

Las dos primeras se pueden realizar antes o después de la migración de contenido.  Son pasos que afectan únicamente a usuarios y grupos en IMS, incluyendo, posiblemente, la integración con un IDP externo como Active Directory o LDAP.  Estos pasos se describen en [Administración de principales en IMS con Admin Console](/help/journey-migration/managing-principals.md).

Una vez que el contenido se migra al entorno de AEM as a Cloud Service, se puede llevar a cabo el tercer paso.

### Migración de grupos

Durante la fase de ingesta de la migración, los grupos se migran si son necesarios para satisfacer las directivas de ACL o CUG en el contenido migrado.  Consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para obtener más información.

Los grupos migrados (los que no se crean mediante la recopilación de Assets o la creación de carpetas privadas; consulte Colecciones y carpetas privadas a continuación) se configuran como grupos de IMS.  Esto significa que cualquier grupo con el mismo nombre creado en IMS (a través de Admin Console, por ejemplo) se vinculará al grupo en AEM, y los usuarios que sean miembros del grupo de IMS también pasarán a ser miembros del grupo en AEM.  Para que se produzca esta vinculación, el grupo también debe crearse primero en IMS.  Utilice Admin Console para crear grupos, individualmente o en lotes, en su instancia de AEM, tal y como se describe en [Administración de principales en IMS con Admin Console](/help/journey-migration/managing-principals.md).

Utilice la interfaz de usuario de seguridad de AEM para asignar grupos de IMS a grupos locales de AEM. Para ello, vaya a la página Herramientas de AEM, haga clic en Seguridad y seleccione Grupos.

### Usuarios de IMS

Dado que los usuarios no se migran, deben crearse en IMS para que puedan utilizarse en AEM.  Hay varias formas de conseguirlo, pero es importante que los usuarios creados se asignen a los grupos de IMS correctos para que los usuarios tengan el mismo acceso al contenido que tenían en el sistema AEM anterior.  Una de las herramientas que se puede utilizar para esto es la funcionalidad de carga por lotes en Admin Console; utilice el cargador por lotes para cargar usuarios junto con grupos de los que deben ser miembros.  Antes de hacerlo, los grupos deben crearse primero en IMS, tal como se ha descrito anteriormente.

Para saber a qué grupos debe pertenecer cada usuario, puede usar el Informe de usuarios (consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  Este informe enumera los grupos a los que debe pertenecer cada usuario. Esta lista se incluirá normalmente en el archivo de entrada de usuario en masa para su uso con la funcionalidad de carga en masa de Admin Console.

### Colecciones y carpetas privadas

La creación de una colección de Assets o una carpeta privada también crea automáticamente algunos grupos para administrar el acceso a ese contenido de Assets.  Estos grupos se migran si se mencionan en el contenido migrado, pero no están configurados para vincularse directamente a grupos de IMS; en AEM siguen siendo &quot;grupos locales&quot; y no se pueden administrar a través de IMS.

Dado que estos grupos no están en IMS, la herramienta de carga por lotes no se puede utilizar para crear usuarios como miembros directos.  Los usuarios de IMS que también están en AEM pueden añadirse a estos grupos individualmente, pero hacerlo en lotes requiere un paso adicional.  Esta es una forma de hacerlo:
* Cree uno o varios grupos nuevos en Admin Console/IMS para acceder a colecciones o carpetas privadas y configúrelos para AEM.
* Inicie sesión como miembro del grupo o grupos para que estos se creen en AEM.
* En el caso de las colecciones migradas o las carpetas privadas, utilice la interfaz de usuario de Assets para agregar el nuevo grupo como editor/propietario/visualizador.
* Añada usuarios (o realice una carga por lotes) a los nuevos grupos de Admin Console.
* Cuando el usuario inicia sesión por primera vez, su usuario de IMS se crea en AEM y debe tener acceso a los nuevos grupos y, por lo tanto, a los grupos de carpetas privadas o de recopilación originales.

Nota: Para la asignación masiva de usuarios, se deben utilizar los pasos anteriores para crear los usuarios en IMS; los usuarios que ya existen en IMS no se pueden crear de nuevo mediante carga masiva, aunque el editor masivo se puede utilizar para realizar ese tipo de cambios (Consulte [Carga masiva de usuarios en Admin Console](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html) en **Editar detalles del usuario**).
