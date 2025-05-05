---
title: Carga masiva de identidades a IMS después de usar CTT
description: Información general sobre la carga masiva de archivos para grupos y usuarios, y cómo utilizarlos en Admin Console para crear grupos y usuarios en IMS.
exl-id: 43ebd6f1-1492-461a-8d9b-2b55dcde9052
source-git-commit: b9c739a03b358de7c011e50ddbdd609c90f86b6f
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 3%

---

# Carga masiva de identidades principales en IMS después de usar CTT {#bulk-principal-uploading}

>[!CONTEXTUALHELP]
>id="bulk-principal-uploading"
>title="Carga masiva de identidades principales"
>abstract="Información general sobre la carga masiva de archivos para grupos y usuarios, y cómo utilizarlos en Admin Console para crear grupos y usuarios en IMS."
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="Documentación del Admin Console de AEM"
>additional-url="https://adminconsole.adobe.com/" text="Admin Console de AEM"

## Introducción {#introduction}

La migración de contenido a la nube mediante CTT y CAM crea grupos en la instancia de nube de AEM, pero no puede hacer nada para colocar grupos o usuarios en IMS. Deben existir en IMS para que los clientes los administren correctamente. Afortunadamente, Admin Console proporciona funcionalidad para crear grupos y usuarios de IMS de forma masiva. La introducción de CAM facilita este proceso al guardar archivos de entrada para esta creación masiva, lo que permite a los clientes completar esta acción de Admin Console como parte de su proceso de migración general. Se crean dos tipos de archivos de carga masiva: uno para grupos y otro para usuarios.

Consulte también [Administrar usuarios](https://helpx.adobe.com/es/enterprise/using/users.html) para obtener más información acerca de la administración de usuarios de AEM as a Cloud Service.

## Reglas generales para la carga de archivos {#rules}

Existen algunas directrices generales para editar y utilizar ambos tipos de archivos de carga:

* Para poder seguir estas instrucciones, primero debe concederse acceso de administrador a Admin Console.
* Tenga en cuenta que hay varias formas diferentes de crear usuarios y grupos en IMS.  Consulte [Compatibilidad con IMS para Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/ims-support) para obtener más información sobre todas las opciones disponibles.  Aquí solo se describen los métodos de carga masiva de Admin Console.
* Hay tres tipos de identidad posibles en IMS: Adobe ID, Enterprise ID y Federated ID.  Las instrucciones de esta página se proporcionan solo para **Adobe ID**.  Si necesita usar Enterprise ID o Federated ID, consulte la [documentación completa de Admin Console](https://helpx.adobe.com/ca/enterprise/using/admin-console.html) y también la documentación específica para la [carga de grupos masivos de Admin Console](https://helpx.adobe.com/ca/enterprise/using/user-groups.html) y la [carga de usuarios masivos de Admin Console](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html).  Las especificaciones para los archivos de carga son algo diferentes para esos dos tipos de identidad.
* Si un solo campo CSV permite varias entradas (como varios perfiles de producto, varios grupos o varios administradores), las entradas deben estar contenidas entre comillas dobles y separadas por una coma, por ejemplo: `"profile 1,profile 2"`.

   * En este caso, se pueden utilizar comillas simples en lugar de comillas dobles, pero si edita el archivo en Microsoft Excel, pueden producirse problemas de análisis. Si utiliza Excel para editar estos archivos, asegúrese de utilizar comillas dobles en lugar de comillas simples.

## Carga de grupo en lotes {#group-upload}

#### Caso de uso: se han migrado grupos a AEM as a Cloud Service, pero esos grupos no están presentes en IMS/Admin Console, por lo que deben cargarse en IMS a través de Admin Console.

Para utilizar la funcionalidad de carga de grupos por lotes de Admin Console después de ejecutar una migración CTT/CAM, siga estos pasos:
1. Descargar el archivo de grupo en bloque desde CAM

   1. En CAM, vaya a **Transferencia de contenido** y seleccione **Trabajos de ingesta**.
   1. Haga clic en los puntos suspensivos (...) en la línea de la ingesta en cuestión y elija **Ver resumen principal**.
   1. En el cuadro de diálogo que aparece, seleccione **Archivo de grupo en lotes** de la lista desplegable bajo **Descargar un archivo...** y haga clic en el botón **Descargar**.
   1. Guarde el archivo CSV resultante.

1. Edición del archivo de grupo por lotes

   * Cada línea representa un grupo que se va a cargar y tiene cuatro campos (los nombres de los campos constituyen la primera línea del archivo):

      * _Nombre de grupo de usuarios_ - El nombre de grupo es obligatorio y puede contener un máximo de 255 caracteres.  Este nombre de grupo debe ser el mismo en IMS y AEM
      * _Descripción_: este campo es opcional y puede contener un máximo de 255 caracteres
      * _Administradores de grupos de usuarios_ - Se debe incluir al menos un administrador de grupos en este campo. Para asignar varios administradores, separe cada uno con una coma y escriba la lista entre comillas. La entrada para cada administrador debe incluir el tipo de identidad del usuario, seguido de un guion y, a continuación, la dirección de correo electrónico.  Por ejemplo

        `"Adobe ID-myAdmin@example.com,Adobe ID-myOtherAdmin@example.com"`. No incluya un espacio después de la coma que separa a los administradores. No puede incluir usuarios (como administradores) que actualmente no forman parte de la organización en Admin Console
      * _Perfiles de producto asignados_: este campo es opcional. Puede asignar varios perfiles de producto separando cada perfil con una coma y escribiendo la lista entre comillas. Sin embargo, los perfiles de producto que incluya ya deben estar configurados para la organización. Asegúrese de especificar el nombre del perfil de producto y no el nombre del producto.  La pertenencia de perfiles de producto asignados a un grupo la heredarán todos los usuarios ubicados en ese grupo.  Para buscar un perfil de producto:

         1. Ir a Admin Console
         1. Busque su producto (por ejemplo, Adobe Experience Manager as a Cloud Service) y haga clic en él
         1. Busque su entorno (instancia) y haga clic en él
         1. Enumere los perfiles de producto y haga clic en el de su entorno de AEM. El perfil del producto se encuentra en la parte superior, es decir, &quot;_Usuarios de AEM - autor - 12345 del programa - 012345 del entorno_&quot;.

   * Al editar el CSV, algunas aplicaciones pueden añadir comillas adicionales al guardar, lo que provoca que falle el procesamiento. Se recomienda inspeccionar el CSV sin procesar en un editor de texto simple para asegurarse de que cada campo tenga solo una comilla de apertura y una de cierre (y no deban ser &quot;comillas inteligentes&quot;).

1. Cargar el archivo de grupo por lotes en Admin Console

   1. En Admin Console, vaya a **Usuarios** y después a **Grupos de usuarios**
   1. En el lado derecho, haga clic en el botón &quot;...&quot;. Elija **Agregar grupos de usuarios mediante CSV** en el menú y elija el CSV que desea cargar. Haga clic en **Cargar**
   1. Recibirá una respuesta que indica que el CSV se ha cargado (en Admin Console), pero aún no se ha importado a IMS
   1. Vaya al mismo menú &quot;...&quot; y elija **Resultados de operaciones masivas**. Le mostrará una lista de los intentos de carga en lotes y le indicará (en **Estado**) si la carga en lotes se está procesando, se ha realizado correctamente o ha fallado

      * Al principio se mostrará Procesando, lo que indica que aún no ha finalizado
      * Una vez finalizado correctamente, haga clic en el vínculo **Agregar grupos de usuarios** para ver un mensaje de estado simple para cada línea.
      * Si, en su lugar, ha fallado, haga clic en el icono pequeño bajo **Archivo** y proporcionará un poco más de información sobre el motivo del error.  Se hace referencia a los números de línea de grupo a partir de la fila 1.
1. Utilice Admin Console para comprobar los cambios.

## Carga y edición por lotes de usuarios {#bulk-user}

Admin Console incluye dos acciones independientes para cargar y editar los detalles del usuario. Las instrucciones que aparecen inmediatamente a continuación son para añadir nuevos usuarios a IMS. Las instrucciones para editar usuarios de IMS existentes se encuentran en la siguiente sección llamada [Edición masiva de usuarios](#user-edit).

### Carga de usuarios en lotes {#user-upload}

#### Caso de uso: los grupos se han migrado a AEM as a Cloud Service y se han cargado mediante carga masiva u otro método.  Es posible que los usuarios no estén presentes en IMS/Admin Console, por lo que deben cargarse y vincularse a sus grupos en IMS mediante Admin Console.

>[!NOTE]
>
>Un usuario aparecerá en el archivo **Carga masiva de usuarios** si está en un grupo ingerido durante la misma ingesta desde la que se creó el archivo. También puede aparecer si el usuario está directamente en una ACL o CUG de contenido migrado, o si es miembro de un grupo integrado o de un grupo local que está en una ACL o CUG del contenido migrado. Consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para obtener más información sobre estos casos.

Para utilizar la funcionalidad de carga masiva de usuarios de Admin Console, siga estos pasos:

1. Descargar el archivo de usuario en bloque desde CAM
   1. En CAM, vaya a **Transferencia de contenido** y seleccione **Trabajos de ingesta**.
   1. Haga clic en los puntos suspensivos (...) en la línea de la ingesta en cuestión y elija **Ver resumen principal**.
   1. En el cuadro de diálogo que aparece, seleccione **Archivo de usuario en lotes** de la lista desplegable bajo **Descargar un archivo...** y haga clic en el botón **Descargar**.
   1. Guarde el archivo CSV resultante
1. Edición del archivo de usuario en bloque
   * Cada línea representa un usuario que se va a cargar y tiene quince campos (los nombres de los campos constituyen la primera línea del archivo). Algunos campos son opcionales y no se describen aquí. Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format).  Los campos son:

      * _Tipo de identidad_ - Opcional.  Si no se especifica, se creará como una Adobe ID
      * _Nombre de usuario_: opcional y no se usa para las cargas de Adobe ID
      * _Dominio_: opcional y no utilizado para cargas de Adobe ID
      * _Correo electrónico_ - Obligatorio.  La dirección de correo electrónico se utilizará para la verificación la primera vez que el usuario inicie sesión
      * _Nombre_ - Opcional.  Debe usarse porque aparece, con Apellidos, en varios lugares
      * _Apellido_ - Opcional.  Debe usarse porque aparece en varios lugares
      * _Código de país_: opcional y no se usa para las cargas de Adobe ID
      * _ID_: opcional y no se usa para las cargas de Adobe ID
      * _Configuraciones de producto_ - Opcional. Este campo también se heredará de cualquier grupo al que pertenezca el usuario
      * _Roles de administrador_ - Opcional. Utilice este campo si el usuario es administrador. Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información
      * _Configuraciones de producto administradas_ - Opcional.  Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información. Este campo también se heredará de cualquier grupo al que pertenezca el usuario
      * _Grupos de usuarios_ - Opcional. Lista de grupos a los que el usuario debe asignarse como miembro. Cada grupo debe ser un grupo de IMS ya existente. Cuando se descarga el archivo de usuario en bloque desde CAM, este campo se rellena previamente con los nombres de los grupos habilitados para IMS de los que el usuario era miembro (directa o indirectamente) antes de la migración
      * _Grupos de usuarios administrados_ - Opcional.  Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información. Este campo también se heredará de cualquier grupo al que pertenezca el usuario
      * _Productos administrados_ - Opcional.  Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información. Este campo también se heredará de cualquier grupo al que pertenezca el usuario
      * _Contratos administrados_ - Opcional.  Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información
      * _Acceso de desarrollador_ - Opcional.  Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información
      * _Productos asignados automáticamente_ - Opcional.  Consulte [Formato CSV de usuario en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format) para obtener más información

   * Al editar el CSV, algunas aplicaciones pueden añadir comillas adicionales al guardar, lo que provoca que falle el procesamiento. Se recomienda inspeccionar el CSV sin procesar en un editor de texto simple para asegurarse de que cada campo tenga solo una comilla de apertura y una de cierre (y no deban ser &quot;comillas inteligentes&quot;)

1. Utilice Admin Console para importar el archivo de usuario en bloque

   1. En Admin Console, vaya a Usuarios
   1. Haga clic en el botón **Agregar usuarios mediante CSV**
   1. Arrastre y suelte o seleccione un archivo CSV de usuario en bloque descargado de CAM
   1. Haga clic en el botón **Cargar**
   1. Recibirá una respuesta que indica que el CSV se ha cargado (en Admin Console), pero aún no se ha importado a IMS.
   1. Vaya al menú &quot;...&quot; de la derecha y elija **Resultados de operaciones masivas**.  Mostrará una lista de intentos de carga en lotes y mostrará (en **Estado**) si la carga en lotes se está procesando, se ha realizado correctamente o ha fallado.

      * Al principio se mostrará Procesando, lo que indica que aún no ha finalizado
      * Una vez finalizado correctamente, haga clic en el vínculo **Agregar usuarios** para ver un mensaje de estado simple para cada línea
      * Si en su lugar ha fallado, haga clic en el icono pequeño bajo **Archivo** y le dará un poco más de información sobre por qué falló. Se hace referencia a los números de línea del usuario a partir de la fila 1.

1. Utilice Admin Console para comprobar los cambios.

>[!NOTE]
>
>Después de una ingesta sin borrado, es posible que los usuarios migrados anteriormente y luego creados en IMS aparezcan en el archivo de carga de usuarios en lote. Esto podría deberse a muchas razones. En este caso, no se podrá volver a cargar el usuario. En su lugar, intente eliminar el usuario del archivo de carga de usuarios en lote y, si es necesario agregarlo a diferentes grupos, utilice el archivo de edición de usuarios en lote como se describe a continuación.

### Edición de usuario en masa {#user-edit}

#### Caso de uso: Se han migrado grupos y usuarios a AEM as a Cloud Service y se han cargado mediante carga masiva u otro método. Ahora es necesario realizar algunos cambios en varios usuarios a la vez, como añadirlos a un grupo de IMS existente.

Para utilizar la funcionalidad de edición masiva de usuarios de Admin Console, siga estos pasos:

1. Descargar el archivo de usuario en bloque desde Admin Console

   1. En Admin Console, vaya a Usuarios
   1. En el lado derecho, haga clic en el botón &quot;...&quot;.  Elija **Editar detalles de usuario mediante CSV** en el menú
   1. Haga clic en **Descargar plantilla CSV** y elija **Usuarios actuales**.  Debe aparecer un archivo CSV en la carpeta local Descargas.

1. Edición del archivo de usuario en bloque

   1. En Admin Console, vaya a Usuarios
   1. Edite el archivo CSV con un editor de texto (recomendado) o una aplicación de hoja de cálculo como Excel. El uso de una aplicación puede realizar cambios impredecibles en los datos, por lo que se recomienda que, después de realizar todas las ediciones, se utilice un editor de texto para comprobar el formato del archivo
   1. La descripción de los campos de este archivo es la misma que se muestra arriba, en Carga masiva de usuarios
   1. Quitar todos los usuarios que no se vayan a editar
   1. Si cambia el campo Grupos de usuarios, deje los grupos actuales y agregue nuevos según sea necesario. Si elimina un grupo existente, el usuario se eliminará de ese grupo en IMS
   1. Al editar el CSV, algunas aplicaciones pueden añadir comillas adicionales al guardar, lo que provoca que falle el procesamiento. Se recomienda inspeccionar el archivo CSV sin procesar en un editor de texto simple para asegurarse de que cada campo tenga solo una comilla de apertura y una de cierre (y no deban ser &quot;comillas inteligentes&quot;)

1. Cargar el archivo de usuario en bloque en Admin Console

   1. En Admin Console, vaya a Usuarios
   1. En el lado derecho, haga clic en el botón &quot;...&quot;. Elija **Editar detalles de usuario mediante CSV** en el menú
   1. Arrastre y suelte o seleccione el archivo CSV de usuario en bloque editado
   1. Haga clic en el botón Upload
   1. Recibirá una respuesta que indica que el CSV se ha cargado (en Admin Console), pero aún no se ha importado a IMS
   1. Vaya al menú &quot;...&quot; de la derecha y elija **Resultados de operaciones masivas**. Muestra una lista de los intentos de carga masiva y le informa (en Estado) de si la carga masiva se está procesando, se ha realizado correctamente o ha fallado.

      * Al principio se mostrará Procesando, lo que indica que aún no ha finalizado
      * Una vez finalizado correctamente, haga clic en el vínculo **Editar detalles del usuario** para ver un mensaje de estado simple para cada línea
      * Si en su lugar ha fallado, haga clic en el icono pequeño bajo **Archivo** y se mostrará un poco más de información sobre el motivo del error. Se hace referencia a los números de línea del usuario a partir de la fila 1.

1. Utilice Admin Console para comprobar los cambios.
