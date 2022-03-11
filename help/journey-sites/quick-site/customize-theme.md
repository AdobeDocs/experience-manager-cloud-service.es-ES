---
title: Personalizar el tema del sitio
description: Descubra cómo se crea el tema del sitio, cómo personalizarlo y cómo probarlo con contenido AEM en directo.
exl-id: b561bee0-3a64-4dd3-acb8-996f0ca5bfab
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Personalizar el tema del sitio {#customize-the-site-theme}

Descubra cómo se crea el tema del sitio, cómo personalizarlo y cómo probarlo con contenido AEM en directo.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Creación Rápida del Sitio de AEM, [Recuperar información de acceso al repositorio Git,](retrieve-access.md) ha aprendido cómo los usuarios de desarrolladores de front-end Cloud Manager acceden a la información del repositorio de Git, y ahora debería:

* Comprender en un nivel superior qué es Cloud Manager.
* Ha recuperado sus credenciales para acceder a la Git de AEM para que pueda confirmar sus personalizaciones.

Esta parte del recorrido da el siguiente paso y explora el tema del sitio y le muestra cómo personalizarlo y, a continuación, confirmar esas personalizaciones utilizando las credenciales de acceso que ha recuperado.

## Objetivo {#objective}

Este documento explica cómo se crea el tema del sitio AEM, cómo personalizarlo y cómo probarlo con contenido AEM en directo. Después de leer, debe:

* Comprender la estructura básica del tema del sitio y cómo editarlo.
* Consulte cómo probar las personalizaciones de temas mediante contenido AEM real a través de un proxy local.
* Obtenga información sobre cómo confirmar los cambios en el repositorio de Git de AEM.

## Función responsable {#responsible-role}

Esta parte del recorrido se aplica al desarrollador del front-end.

## Explicación de la estructura del tema {#understand-theme}

Extraiga el tema proporcionado por el administrador de AEM donde desee editar el tema y ábralo en su editor preferido.

![Edición del tema](assets/edit-theme.png)

Verá que el tema es un proyecto front-end típico. Las partes más importantes de la estructura son:

* `src/main.ts`: El punto de entrada principal del tema de JS y CSS
* `src/site`: Archivos JS y CSS que se aplican a todo el sitio
* `src/components`: Archivos JS y CSS específicos de componentes AEM
* `src/resources`: Archivos estáticos como iconos, logotipos y fuentes

>[!TIP]
>
>Si desea obtener más información sobre el tema estándar del sitio AEM, consulte el vínculo de GitHub en la sección [Recursos adicionales](#additional-resources) al final de este documento.

Una vez que esté cómodo con la estructura del proyecto de tema, inicie el proxy local para poder ver cualquier personalización de tema en tiempo real basada en el contenido de AEM real.

## Inicio del proxy local {#starting-proxy}

1. Desde la línea de comandos, vaya a la raíz del tema en el equipo local.
1. Ejecutar `npm install` y npm recupera dependencias e instala el proyecto.

   ![instalación de npm](assets/npm-install.png)

1. Ejecutar `npm run live` y se inicia el servidor proxy.

   ![npm run live](assets/npm-run-live.png)

1. Cuando se inicia el servidor proxy, se abre automáticamente un explorador a `http://localhost:7001/`. Toque o haga clic **INICIAR SESIÓN LOCALMENTE (SOLO TAREAS DE ADMINISTRACIÓN)** e inicie sesión con las credenciales del usuario proxy proporcionadas por el administrador de AEM.

   ![Iniciar sesión localmente](assets/sign-in-locally.png)

1. Una vez que haya iniciado sesión, cambie la dirección URL en el explorador para que apunte a la ruta del contenido de ejemplo que le proporcionó el administrador de AEM.

   * Por ejemplo, si la ruta proporcionada era `/content/<your-site>/en/home.html?wcmmode=disabled`
   * Cambiaría la dirección URL a `http://localhost:7001/content/<your-site>/en/home.html?wcmmode=disabled`

   ![Contenido de muestra proxido](assets/proxied-sample-content.png)

Puede navegar por el sitio para explorar el contenido. El sitio se extrae en vivo de la instancia de AEM en directo para que pueda realizar personalizaciones de temas con contenido real.

## Personalizar el tema {#customize-theme}

Ahora puede empezar a personalizar el tema. El siguiente es un ejemplo sencillo que ilustra cómo puede ver los cambios en vivo a través del proxy.

1. En el editor, abra el archivo . `<your-theme-sources>/src/site/_variables.scss`

   ![Editar tema](assets/edit-theme.png)

1. Editar la variable `$color-background` y configúrelo en un valor distinto de blanco. En este ejemplo, `orange` se utiliza.

   ![Tema editado](assets/edited-theme.png)

1. Cuando guarde el archivo, verá que el servidor proxy reconoce el cambio a través de la línea `[Browsersync] File event [change]`.

   ![Sincronización de navegadores proxy](assets/proxy-browsersync.png)

1. Al volver al explorador del servidor proxy, el cambio es visible inmediatamente.

   ![Tema naranja](assets/orange-theme.png)

Puede seguir personalizando el tema en función de los requisitos que le proporcione el administrador de AEM.

## Ejecución de los cambios {#committing-changes}

Una vez completadas las personalizaciones, puede enviarlas al repositorio de Git de AEM. Primero debe clonar el repositorio en el equipo local.

1. Desde la línea de comandos, vaya a donde desee clonar el repositorio.
1. Ejecute el comando [recuperado anteriormente de Cloud Manager.](retrieve-access.md) Debe ser similar a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`. Utilice el nombre de usuario y la contraseña de Git que [recuperó en la parte anterior de este recorrido.](retrieve-access.md)

   ![Clonar repo](assets/clone-repo.png)

1. Mueva el proyecto de tema que estaba editando al repositorio clonado con un comando similar al `mv <site-theme-sources> <cloned-repo>`
1. En el directorio del repositorio clonado, confirme los archivos de tema a los que acaba de moverse con los siguientes comandos.

   ```text
   git add .
   git commit -m "Adding theme sources"
   git push
   ```

1. Las personalizaciones se insertan en el repositorio de Git de AEM.

   ![Cambios comprometidos](assets/changes-committed.png)

Sus personalizaciones ahora se almacenan de forma segura en el repositorio de AEM Git.

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de creación rápida AEM sitio, debe:

* Comprender la estructura básica del tema del sitio y cómo editarlo.
* Consulte cómo probar las personalizaciones de temas mediante contenido AEM real a través de un proxy local.
* Obtenga información sobre cómo confirmar los cambios en el repositorio de Git de AEM.

Aproveche este conocimiento y continúe con su recorrido de Creación Rápida AEM Sitio revisando el documento [Implementar El Tema Personalizado,](deploy-theme.md) donde aprenderá a implementar el tema utilizando la canalización front-end.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida del sitio revisando el documento [Implementar El Tema Personalizado,](deploy-theme.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [AEM tema del sitio](https://github.com/adobe/aem-site-template-standard-theme-e2e) - Este es el repositorio de GitHub del tema del sitio AEM.
* [npm](https://www.npmjs.com) - AEM temas utilizados para construir sitios rápidamente se basan en npm.
* [webpack](https://webpack.js.org) - AEM temas utilizados para construir sitios rápidamente dependen del webpack.
