---
title: Aplicación de muestra SecurBank para el editor universal
description: Obtenga información sobre el editor universal con experiencia práctica mediante el uso de la aplicación SecurBank, diseñada para mostrar la potencia, flexibilidad y facilidad de uso del editor universal con el fin de acelerar la creación de contenido.
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 100%

---

# Aplicación de muestra SecurBank para el editor universal {#securbank}

Obtenga información sobre el editor universal con experiencia práctica mediante el uso de la aplicación SecurBank, diseñada para mostrar la potencia, flexibilidad y facilidad de uso del editor universal con el fin de acelerar la creación de contenido.

## Requisitos previos {#prerequisites}

* Debe estar asignado al [perfil de producto](/help/journey-onboarding/assign-profiles-aem.md) de **Administrador de AEM** para instalar la aplicación SecurBank.
* Debe tener [Node.js](https://nodejs.org) versión 20 o superiores instalado para el desarrollo local.

## Instalación de SecurBank {#installation}

La instalación de la aplicación SecurBank es sencilla, pero como afecta a muchas áreas de AEM as a Cloud Service, hay que seguir una serie de pasos. A continuación se ofrece información general sobre los pasos principales.

1. [Cree un programa de zona protegida en Cloud Manager](#create-sandbox-program).
1. [Clone el repositorio Git del programa y actualícelo con el contenido del proyecto de AEM de SecurBank](#clone-and-update).
1. [Ejecute la canalización para implementar el proyecto de AEM de SecurBank](#run-pipeline).
1. [Recupere las credenciales de Cloud Manager para el desarrollo local de aplicaciones web](#retrieve-credentials).
1. [Descargue y configure la aplicación web de SecurBank](#download-web-app).
1. [Ejecute la aplicación web de SecurBank](#run-web-app).

Las siguientes secciones detallan las tareas individuales necesarias.

### Cree un programa de zona protegida en Cloud Manager. {#create-sandbox-program}

Necesitará un nuevo programa de Cloud Manager donde pueda instalar SecurBank.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Cree un nuevo programa de zona protegida para la aplicación SecurBank.

   * Use las opciones predeterminadas al seleccionar **Soluciones y complementos**.
   * Para obtener más información sobre cómo crear un programa de zona protegida, consulte el documento [Creación de programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).

### Clone el repositorio Git del programa y actualícelo con el contenido del proyecto de AEM de SecurBank. {#clone-and-update}

1. Una vez creado el programa, ábralo y en la pestaña **Repositorios**, toque o haga clic en el botón **Acceder a la información del repositorio** para abrir el cuadro de diálogo **Información del repositorio** y ver las credenciales necesarias para acceder al repositorio de Git para el entorno de zona protegida.

   * Para obtener más información sobre cómo acceder a la información del repositorio, consulte el documento [Acceso a repositorios](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Con las credenciales del cuadro de diálogo **Información del repositorio**, clone el repositorio en el equipo local.

1. Busque la carpeta del clon local, ábrala y elimine todo el contenido excepto los archivos ocultos/con punto.

1. Recupere el código más reciente del proyecto de AEM de SecurBank desde GitHub en [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) haciendo clic en **Código** y, a continuación, **Descargar ZIP** en el menú desplegable.

1. Descomprima el contenido del archivo ZIP en el sistema de archivos local y muévalo a la carpeta, ahora vacía, del clon local del programa de zona protegida.

1. Con el terminal, cambie a la carpeta del proyecto clonado y confirme todo el contenido y envíelo a Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### Ejecute la canalización para implementar el proyecto de AEM de SecurBank. {#run-pipeline}

Con el proyecto de AEM para SecurBank confirmado en el repositorio de la zona protegida, se puede implementar con una canalización.

1. Vuelva a la pestaña **Información general** de su programa de zona protegida en Cloud Manager y ejecute la canalización de no producción de pila completa.

   * Desmarque todas las opciones para la ejecución de la canalización.
   * Para obtener más información sobre la ejecución de canalizaciones, consulte el documento [Administración de canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines).

### Recupere las credenciales de Cloud Manager para el desarrollo de aplicaciones web locales. {#retrieve-credentials}

Antes de poder ejecutar la aplicación SecurBank, necesitará las credenciales de Cloud Manager para conectar la aplicación a Cloud Manager.

1. Mientras se ejecuta la canalización, vuelva a la pestaña **Información general** de Cloud Manager y toque o haga clic en el botón de puntos suspensivos situado junto al nombre del entorno y seleccione **Developer Console**.

1. En Developer Console, seleccione la pestaña **Integraciones**, luego la pestaña **Token local** y toque o haga clic en **Obtener token de desarrollo local**.

1. Se genera un archivo JSON con el token de acceso. Copie solo el token en sí (el JSON restante no es necesario) a una ubicación segura para su uso en un paso futuro antes de cerrar Developer Console y volver a Cloud Manager.

1. De nuevo en Cloud Manager, en la pestaña **Información general**, haga clic con el botón derecho en la URL del entorno para copiarla y guardarla en una ubicación segura y usarla en un paso futuro.

### Descargue y configure la aplicación web SecurBank. {#download-web-app}

Ahora puede descargar y configurar la aplicación web SecurBank.

1. Recupere el último código de la aplicación SecurBank de GitHub en [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) haciendo clic en **Código** y luego en **Descargar ZIP** en el menú desplegable.

1. Descomprima el contenido del archivo ZIP en su sistema de archivos local. 

1. Inicie el editor de código que prefiera y abra el archivo de entorno oculto en el proyecto de la aplicación SecurBank en `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Realice los cambios siguientes en el archivo `.env` y guárdelos.

   * Para `REACT_APP_HOST_URI`, pegue el valor de la URL del entorno copiada antes.
   * Para `REACT_APP_DEV_TOKEN`, pegue el valor del token de desarrollo local copiado antes.

### Ejecute la aplicación web SecurBank. {#run-web-app}

Con todo configurado tanto en Cloud Manager como localmente, puede ejecutar la aplicación web de SecurBank.

1. En la línea de comandos de su equipo local, vaya a la carpeta `react-app` del proyecto de la aplicación SecurBank que descargó y descomprimió.

1. En la carpeta `react-app`, instale la aplicación SecurBank con el comando `node -i`.

1. Una vez instalada, inicie la aplicación SecurBank con el comando `npm start`.

1. Si la instalación y el inicio se han realizado de forma correcta, verá lo siguiente:

* La siguiente salida en el terminal.

  ```text
  Compiled successfully!
  
  You can now view securbank in the browser.
  
    Local:            https://localhost:3000
    On Your Network:  https://192.168.1.15:3000
  
  Note that the development build is not optimized.
  To create a production build, use npm run build.
  
  webpack compiled successfully
  ```

   * Y una ventana del explorador abierta a la dirección URL `https://localhost:3000`.

      * Tenga en cuenta que esto es para fines de desarrollo y, por ello, no se proporciona ningún certificado válido. Así, es posible que deba informar al explorador para que pueda acceder a la página.

¡Enhorabuena! Ahora debería ver la aplicación SecurBank ejecutándose correctamente en el explorador.

Si el contenido aún no aparece, asegúrese de que la canalización **Implementar en desarrollo** que ejecutó se haya completado.

![Aplicación SecurBank en el explorador](assets/securbank.png)

{{ue-headless-auth}}

