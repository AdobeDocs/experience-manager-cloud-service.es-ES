---
title: Aplicación de ejemplo de SecurBank para el editor universal
description: Obtenga información sobre el editor universal con experiencia práctica mediante el uso de la aplicación SecurBank, diseñada para mostrar la potencia, flexibilidad y facilidad de uso del editor universal para acelerar la creación de contenido.
exl-id: 97e1395f-b51e-4cee-b1d0-2466a08f96af
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---

# Aplicación de ejemplo de SecurBank para el editor universal {#securbank}

Obtenga información sobre el editor universal con experiencia práctica mediante el uso de la aplicación SecurBank, diseñada para mostrar la potencia, flexibilidad y facilidad de uso del editor universal para acelerar la creación de contenido.

## Requisitos previos {#prerequisites}

* Se le debe asignar al **AEM Administrador de** [perfil de producto](/help/journey-onboarding/assign-profiles-aem.md) para instalar la aplicación de SecurBank.
* Debe tener [Node.js](https://nodejs.org) versión 20 o superior instalada para el desarrollo local.

## Instalación de SecurBank {#installation}

AEM La instalación de la aplicación de SecurBank es sencilla, pero debido a que afecta a muchas áreas de la aplicación as a Cloud Service, hay que seguir una serie de pasos. A continuación se ofrece una descripción general de los pasos principales.

1. [Cree un programa de zona protegida en Cloud Manager.](#create-sandbox-program)
1. [AEM Clone el repositorio de Git del programa y actualícelo con el contenido del proyecto de SecurBank.](#clone-and-update)
1. [AEM Ejecute la canalización para implementar el proyecto de SecurBank.](#run-pipeline)
1. [Recupere las credenciales de Cloud Manager para el desarrollo de aplicaciones web locales.](#retrieve-credentials)
1. [Descargue y configure la aplicación web de SecurBank.](#download-web-app)
1. [Ejecute la aplicación web de SecurBank.](#run-web-app)

Las siguientes secciones detallan las tareas individuales necesarias.

### Cree un programa de zona protegida en Cloud Manager. {#create-sandbox-program}

Necesitará un nuevo programa de Cloud Manager en el que pueda instalar SecurBank.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Cree un nuevo programa de zona protegida para la aplicación SecurBank.

   * Utilice las opciones predeterminadas al seleccionar **Soluciones y complementos**.
   * Para obtener más información sobre cómo crear un programa de zona protegida, consulte el documento [Creación de programas de zona protegida.](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)

### AEM Clone el repositorio de Git del programa y actualícelo con el contenido del proyecto de SecurBank. {#clone-and-update}

1. Una vez creado el programa, ábralo y en la **Repositorios** pestaña, toque o haga clic en **Acceder a info del repositorio** para abrir el **Información del repositorio** y vea las credenciales necesarias para acceder al repositorio de Git para el entorno de zona protegida.

   * Para obtener más información sobre cómo acceder a la información del repositorio, consulte el documento [Acceder a repositorios.](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. Uso de las credenciales en la **Información del repositorio** , clone el repositorio en el equipo local.

1. Busque la carpeta del clon local, ábrala y elimine todo el contenido excepto los archivos ocultos/de puntos.

1. AEM Recupere el código de proyecto de SecurBank más reciente de GitHub enGitHub, en [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425-securbank) haciendo clic en **Código** y luego **Descargar ZIP** en el menú desplegable.

1. Descomprima el contenido del archivo zip en el sistema de archivos local y muévalo a la carpeta, ahora vacía, del clon local del programa de zona protegida.

1. Con el terminal, cambie a la carpeta del proyecto clonado y confirme todo el contenido e instálelo en Git.

   1. `git add --all`
   1. `git commit -m "Adding SecurBank app code"`
   1. `git push`

### AEM Ejecute la canalización para implementar el proyecto de SecurBank. {#run-pipeline}

AEM Una vez que el proyecto de seguridad para SecurBank esté comprometido con el repositorio de la zona protegida, se puede implementar con una canalización.

1. Vuelva a la **Información general** de su programa de zona protegida en Cloud Manager y ejecute la canalización de no producción de pila completa.

   * Desmarque todas las opciones para la ejecución de la canalización.
   * Para obtener más información sobre la ejecución de canalizaciones, consulte el documento [Administración de canalizaciones.](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)

### Recupere las credenciales de Cloud Manager para el desarrollo de aplicaciones web locales. {#retrieve-credentials}

Antes de poder ejecutar la aplicación de SecurBank, necesitará las credenciales de Cloud Manager para conectar la aplicación a Cloud Manager.

1. Mientras se ejecuta la canalización, vuelva a la **Información general** en Cloud Manager y toque o haga clic en el botón de puntos suspensivos situado junto al nombre del entorno y seleccione **Developer Console**.

1. En Developer Console, seleccione **Integraciones** luego la pestaña **Token local** y toque o haga clic en **Obtener token de desarrollo local**.

1. Se genera un archivo JSON con el token de acceso. Copie solo el token en sí (el JSON restante no es necesario) a una ubicación segura para utilizarlo en un paso futuro antes de cerrar Developer Console y regresar a Cloud Manager.

1. Vuelva a Cloud Manager, en la **Información general** , haga clic con el botón derecho en la URL del entorno para copiarlo y guardarlo en una ubicación segura para utilizarlo en un paso futuro.

### Descargue y configure la aplicación web de SecurBank. {#download-web-app}

Ahora puede descargar y configurar la aplicación web de SecurBank.

1. Recupere el último código de la aplicación SecurBank de GitHub en [`https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events`](https://github.com/Adobe-Marketing-Cloud/summit-2024-l425/tree/ue-z-final-with-events) haciendo clic en **Código** y luego **Descargar ZIP** en el menú desplegable.

1. Descomprima el contenido del archivo zip en el sistema de archivos local.

1. Inicie el editor de código que prefiera y abra el archivo de entorno oculto en el proyecto de aplicación de SecurBank en `summit-2024-l425-ue-z-final-with-events/react-app/.env`.

1. Realice los siguientes cambios en la `.env` y guarde los cambios.

   * Para `REACT_APP_HOST_URI` pegue el valor de la URL previamente copiada de su entorno.
   * Para `REACT_APP_DEV_TOKEN` pegue el valor del token de desarrollo local copiado anteriormente.

### Ejecute la aplicación web de SecurBank. {#run-web-app}

Con todo configurado tanto en Cloud Manager como localmente, puede ejecutar la aplicación web de SecurBank.

1. En la línea de comandos del equipo local, vaya a la `react-app` carpeta del proyecto de aplicación de SecurBank que ha descargado y descomprimido.

1. En su `react-app` carpeta instale la aplicación de SecurBank con el `node -i` comando.

1. Una vez instalada, inicie la aplicación de SecurBank con el `npm start` comando.

1. Si la instalación y el inicio se han realizado correctamente, verá lo siguiente:

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

      * Tenga en cuenta que esto es para fines de desarrollo y, como tal, no se proporciona ningún certificado válido. Como tal, es posible que deba informar al explorador para que pueda acceder a la página.

Enhorabuena. Ahora debería ver la aplicación de SecurBank ejecutándose correctamente en el explorador.

Si el contenido aún no aparece, asegúrese de que la variable **Implementar en desarrollo** la canalización que ha ejecutado se ha completado correctamente.

![Aplicación de SecurBank en el explorador](assets/securbank.png)
