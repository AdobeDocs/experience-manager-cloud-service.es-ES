---
title: Administración de principales después de la migración
description: Obtenga información sobre cómo configurar usuarios y grupos en IMS y AEM
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: a5bec2c05b46f8db55762b7ee1f346f3bb099d24
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 5%

---

# Administración de principales después de la migración {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="Administración de principales después de la migración"
>abstract="Obtenga información sobre cómo configurar usuarios y grupos en IMS y AEM"

AEM En este documento se describen los pasos de alto nivel que los clientes deben realizar para configurar sus usuarios y grupos en IMS y para trabajar con su entorno de AEM as a Cloud Service en el que se encuentran.

## Administración de principales {#managing-principals}

Para AEM as a Cloud Service, los usuarios y grupos deben administrarse principalmente mediante el Admin Console.  Al considerar una migración, algunas de estas tareas se pueden llevar a cabo antes de que se produzca la migración de contenido.  Básicamente, uno de estos grupos de tareas principales

* Creación de usuarios y grupos en IMS
* Asignar usuarios a grupos en IMS
* AEM Asignar grupos de IMS a grupos de (si es necesario)

las dos primeras se pueden llevar a cabo antes o después de la migración de contenido.  Son pasos que afectan únicamente a usuarios y grupos en IMS, incluyendo posiblemente la integración con un IDP externo como Active Directory o LDAP.  Estos pasos se describen en [Administración de identidades en IMS con el Admin Console](/help/journey-migration/managing-principals.md).

Una vez que el contenido se migra al entorno de AEM as a Cloud Service, se puede llevar a cabo el tercer paso.

### Migración de grupos

Durante la fase de ingesta de la migración, los grupos se migran si son necesarios para satisfacer las directivas ACL o CUG en el contenido migrado.  Consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para obtener más detalles.

Los grupos migrados (los que no se crearon mediante la creación de colecciones de Assets; consulte Colecciones a continuación) se configuran como grupos de IMS.  Esto significa que cualquier grupo del mismo nombre creado en IMS (a través del Admin Console AEM AEM, por ejemplo) se vinculará al grupo en, y los usuarios que sean miembros del grupo IMS también se convertirán en miembros del grupo en, así como en el grupo en cuestión de.  Para que se produzca esta vinculación, el grupo también debe crearse primero en IMS.  Utilice el Admin Console AEM para crear grupos, de forma individual o en lotes, en su instancia de la instancia de la, tal como se describe en [Administración de identidades en IMS con el Admin Console](/help/journey-migration/managing-principals.md).

AEM AEM Utilice la interfaz de usuario de seguridad de la para asignar grupos de IMS a grupos de usuarios locales.  Consulte [Creación y configuración de grupos](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/setup-organize-users/creating-configuring-groups#edit-a-group).  AEM Aunque este documento es para la versión 6.5, también se aplica a la adición de grupos a otros grupos en AEM as a Cloud Service.

### Usuarios de IMS

AEM Dado que los usuarios no se migran, deben crearse en IMS para que puedan utilizarse en los flujos de trabajo de la interfaz de usuario de.  AEM Existen varias formas de conseguirlo, pero es importante que los usuarios creados se asignen a los grupos de IMS correctos para que los usuarios tengan el mismo acceso al contenido que tenían en el sistema de gestión de contenido anterior  Una de las herramientas que se puede utilizar para esto es la funcionalidad de carga masiva en el Admin Console; utilice el cargador masivo para cargar usuarios junto con grupos de los que deben ser miembros.  Antes de hacerlo, los grupos deben crearse primero en IMS, tal como se ha descrito anteriormente.

Para saber a qué grupos debe pertenecer cada usuario, puede usar el Informe de usuarios (consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)).  Este informe enumera los grupos a los que debe pertenecer cada usuario y esta lista se puede incluir en el archivo de entrada de la funcionalidad de carga masiva de Admin Console.

### Colecciones

La creación de una colección Assets también crea automáticamente algunos grupos para administrar el acceso a esa colección.  AEM Estos grupos se migran si se mencionan en colecciones migradas, pero no están configurados para vincularse directamente a grupos de IMS; en el caso de que sigan siendo &quot;grupos locales&quot;, y no se pueden administrar a través de IMS.

Dado que estos grupos no están en IMS, la herramienta de carga masiva no se puede utilizar para crear usuarios como miembros directos.  AEM Los usuarios de IMS que también se encuentran en la fase de creación de informes pueden agregarse a estos grupos de forma individual, pero para hacerlo de forma masiva se requiere un paso adicional.  A continuación se muestra una forma de hacerlo:
* Cree uno o varios grupos nuevos en Admin Console AEM/IMS para acceder a las colecciones y configúrelos para su.
* AEM Inicie sesión como miembro del grupo o grupos para que los grupos se creen en el sitio de inicio de sesión de la cuenta de usuario de la cuenta de.
* Para las colecciones migradas, utilice la interfaz de usuario de Assets Collections para agregar el nuevo grupo como editor/propietario/visualizador.
* Añada usuarios (o realice una carga masiva) a los nuevos grupos de Admin Console.
* AEM Cuando el usuario inicia sesión por primera vez, su usuario de IMS se crea en y debe tener acceso a los grupos nuevos y, por lo tanto, a los grupos de recopilación originales.

Nota: Para la asignación masiva de usuarios, se deben utilizar los pasos anteriores para crear los usuarios en IMS; los usuarios que ya existen en IMS no se pueden crear de nuevo mediante carga masiva.
