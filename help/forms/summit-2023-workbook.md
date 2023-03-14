---
title: Cree una Forms atractiva con componentes principales y sin encabezado
seo-title: Build Engaging Forms Using Core Components and Headless
description: Cree una Forms atractiva con componentes principales y sin encabezado
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
source-git-commit: 8f3ffc72507be1d28bc437041579578d6a479e23
workflow-type: tm+mt
source-wordcount: '2453'
ht-degree: 1%

---


# Cree una Forms atractiva con componentes principales y sin encabezado

## Resumen de laboratorio

En este laboratorio práctico, aprenderá lo siguiente:

Aprenda a utilizar AEM Forms para crear fácilmente formularios adaptables mediante los componentes principales más recientes y coherentes con AEM Sites. Permita experiencias de captura de datos omnicanal al enviar formularios adaptables como formularios sin encabezado a la web, a dispositivos móviles y a chat. También aprenderá prácticas recomendadas sobre estilo, personalizaciones y desarrollo front-end.

## Puntos clave

* **Agilidad empresarial**: como usuario empresarial, puedo crear fácilmente experiencias de formulario para varios canales.

* **Potencia para desarrollador de front-end**: como desarrollador de front-end, puedo controlar la experiencia del usuario final mediante formularios sin encabezado.

* **Velocidad de desarrollador**: como desarrollador, puedo personalizar de forma fácil y coherente los componentes de Sites y Forms.

## Requisitos previos

AEM Forms como zona protegida de Cloud Service

## Lección 1

### Objetivo

Familiarícese con el entorno as a Cloud Service de AEM Forms.

### Contexto de lección

En esta lección, puede familiarizarse con el entorno as a Cloud Service de AEM Forms navegando por la interfaz de usuario.

### Ejercicio

1. Abra el explorador e introduzca la URL del entorno de creación de Cloud Service. Por ejemplo:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Inicie sesión en el entorno de creación de Cloud Service según las credenciales compartidas. Por ejemplo: Nombre de usuario: [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
Contraseña: 
**¡Adobe 123!**

1. Una vez que haya iniciado sesión, vaya a la interfaz de usuario de AEM Forms. Clic **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Clic **Forms y documentos**. Descarte los elementos emergentes relacionados con las preferencias o la información.

   ![](/help/forms/assets/screenshot2028113929.png)

   Se muestran todos los formularios disponibles.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lección 2

### Objetivo

Cree un formulario adaptable con los componentes principales más recientes, configure y envíe el formulario.

## Contexto de lección

En esta lección, como usuario empresarial, creará un formulario adaptable para varios canales, como web, móvil y chat, mediante la creación de formularios adaptables con componentes principales OOTB estandarizados para la captura de datos.

## Ejercicio

1. Cree un punto final de envío para el formulario:

   1. Abrir <https://requestbin.com/> en una nueva pestaña del explorador.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Clic **Creación de una bandeja pública** y copie la dirección URL del extremo.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Crear un formulario adaptable mediante la interfaz del asistente:

   1. En la pestaña del explorador que se utiliza en la lección 1, vaya a AEM Forms como interfaz web del Cloud Service y luego a Forms y Documentos.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Clic **Crear** y seleccione Formulario adaptable.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Seleccione el **En blanco con componentes principales** plantilla de la pantalla de selección de plantillas como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Haga clic en **Estilo** y seleccione la pestaña **wknd-theme** tema como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Haga clic en **Envío** y seleccione la pestaña **Enviar al punto final REST** y especifique la bandeja pública en la
      **URL de la solicitud del POST** como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Haga clic en **Crear**. Especifique un nombre y un título para el formulario. Por ejemplo, **contacto**. Haga clic en **Crear**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Se abrirá el editor de formularios adaptables. Descarte los elementos emergentes o los cuadros de diálogo para ver las preferencias o la información. Haga clic en el explorador de componentes en el carril izquierdo y añada **Pie** al final del formulario en blanco.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. Añada el **Header** al principio del formulario.
      ![](/help/forms/assets/screenshot2028122029.png)

   1. Añadir un **Título** al centro del formulario.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Añadir un **Entrada de texto** después del componente de título.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Añadir un **Entrada de número** componente.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Añadir un **Botón Enviar** al formulario.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Haga clic en **Título** componente para que **menú emergente** se muestra. Haga clic en **Icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Entrar `Contact Us` como el texto del título.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Haga clic en **Entrada de texto** para que se muestre el menú emergente. Haga clic en **Icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Entrar **Nombre completo** como etiqueta de campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Haga clic en **Entrada de número** para que se muestre el menú emergente. Haga clic en **Icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Introduzca el **Número de teléfono** como etiqueta de campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Agregar validaciones al formulario:

   1. Haga clic en **Número de teléfono** para que se muestre el menú emergente. Haga clic en **Icono de llave inglesa** en el menú para configurar el campo.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Abra el **pestaña validaciones**, marque el campo **Requerido** y haga clic en **Listo**. Se muestra el mensaje de éxito.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Clic **Previsualizar** para obtener una vista previa del formulario desde la perspectiva del usuario final.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Rellene el formulario con datos ficticios
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Enviar el formulario
      ![](/help/forms/assets/screenshot2028125729.png)

   1. En la pestaña Bandeja de solicitudes, compruebe los datos enviados.
      ![](/help/forms/assets/screenshot2028125829.png)

Ahora, para los fines del ejercicio restante, utilice un formulario de registro creado previamente.

1. Abra la interfaz de administración de AEM Forms, por ejemplo,. `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`y seleccione el formulario de registro.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Haga clic en **Publicar**.

   ![](/help/forms/assets/screenshot2028115629.png)

   Se muestra el mensaje de éxito.

   ![](/help/forms/assets/screenshot2028115729.png)

   La URL de publicación del formulario sería similar a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Para ver el formulario publicado, reemplace el ID de programa (pXXXXXX) y el ID de entorno (eXXXXXX) en la URL anterior por los ID de su entorno.

## Lección 3

### Objetivo

Actualice los estilos utilizando las prácticas recomendadas de desarrollo de front-end.

### Contexto de lección

En esta lección, como desarrollador front-end, aprenderá a actualizar fácilmente el estilo del formulario adaptable creado anteriormente.

### Ejercicio

Configure el repositorio local de la temática:

1. Abra el símbolo del sistema o shell con derechos de administrador:

   ![](/help/forms/assets/screenshot2028115829.png)

1. En el Símbolo del sistema, utilice el siguiente comando para desplazarse a **c:\git** carpeta

   ```Shell
   cd c:\git
   ```

1. Utilice el siguiente comando para clonar el código de front-end del tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Utilice el siguiente comando en el orden indicado para ir a **aem-forms-theme-canvas** y abra Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Seleccionar **Confiar en los autores de todos los archivos de la carpeta principal** y haga clic en **Sí, confío en los autores**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Para procesar el formulario alojado en el entorno de publicación del servicio en la nube, cambie el nombre a `env_template` archivo.  Para cambiar el nombre del archivo, haga clic con el botón derecho en **env_template** y seleccione la opción **Cambiar nombre** opción.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Establezca los siguientes valores para las variables del archivo .env y guarde el archivo:

   * **AEM URL_DE_LA**: especifique el entorno de publicación del servicio en la nube. Por ejemplo, `https://publish-p105303-e986623.adobeaemcloud.com/`. 

   * **AEM FORMULARIO_ADAPTABLE_**: especifique la ruta del formulario. Por ejemplo, si la ruta del formulario es `/content/forms/af/registration`, el valor de esta variable sería `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)

   ![](/help/forms/assets/screenshot20228116569.png)


1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Si recibe un mensaje pidiéndole que actualice npm a través de `npm notice Run npm nstall -g npm@9.6.0`, ignore el mensaje.
   > * No ejecute otros comandos npm a menos que se le indique en el libro.


1. Ahora ejecute el siguiente comando para obtener una vista previa del formulario.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Una vez ejecutado el comando anterior, espere a que `webpack compiled` Mensaje. El formulario se muestra en una pestaña del explorador.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el explorador después de ejecutar el `npm run live` comando, cambiar `localhost` en la URL del explorador 127.0.0.1 y pulse **Entrar**.



   ![](/help/forms/assets/screenshot2028115129.png)


1. En Código de Visual Studio, abra el `PROJECT\src\site\_variables.scss` archivo. Observe el `$error` el color es un tono de ROJO.

   ![](/help/forms/assets/screenshot2028120729.png)

1. En el explorador, envíe el formulario para ver el color rojo en la **Nombre** field.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Configure las variables **$error** colorear a **#5736eb** y guarde el archivo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Actualice el explorador y envíe el formulario. Observe que el color del error en el campo de nombre ha cambiado en consecuencia.

   ![](/help/forms/assets/screenshot2028121129.png)

1. En el Símbolo del sistema, presione **CTRL + C**, introduzca **Y** y pulse **Entrar** clave para finalizar el proceso npm. Es importante detener el servidor npm para que no entre en conflicto con el siguiente conjunto de ejercicios.
1. Cierre las ventanas Código y Símbolo del sistema de Visual Studio.

## Lección 4

### Objetivo

Procese el formulario en interfaces web/móviles y de otro tipo como un formulario sin encabezado.

### Contexto de lección

En esta lección, como desarrollador de front-end, aprenderá a procesar el formulario adaptable creado anteriormente como formulario sin encabezado mediante el marco de trabajo de diseño de espectro de React.

### Ejercicio

Configure el repositorio local mediante el proyecto de inicio react:

1. Abra el Símbolo del sistema con derechos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)

1. En el Símbolo del sistema, utilice el siguiente comando para desplazarse a **c:\git** carpeta

   ```Shell
   cd c:\git
   ```

1. Utilice el siguiente comando para clonar el proyecto de inicio de reacción del formulario adaptable:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Utilice los siguientes comandos en el orden indicado para ir a **react-starter-kit-aem-headless-forms** y abra Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Se abrirá la ventana Código de Visual Studio.

   ![](/help/forms/assets/screenshot2028117429.png)

Para procesar el formulario alojado en el entorno de publicación del servicio en la nube:

1. Cambie el nombre del archivo env_template a archivo .env. Para cambiar el nombre, haga clic con el botón derecho en **env_template** y seleccione la opción **Cambiar nombre** opción.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Establezca los siguientes valores para las variables del archivo .env. Después de actualizar las variables, guarde el archivo.

   * **AEM URL_DE_LA**: especifique la URL del entorno de publicación del servicio en la nube. Por ejemplo, `https://publish-p105303-e986623.adobeaemcloud.com`. 

   * **AEM RUTA_FORMULARIO_DE_**: especifique la ruta del formulario adaptable creado en la lección anterior. Por ejemplo, `/content/forms/af/registration/`. 

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Abra la ventana de comandos, asegúrese de que está en el directorio react-starter-kit-aem-headless-forms y ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   AEM El comando anterior inicia un servidor de desarrollo local que procesaría la definición del formulario recuperada de forma sin encabezado mediante el uso de la biblioteca de front-end de react-spectrum.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el explorador después de ejecutar el `npm start` comando, cambiar `localhost` en la URL del explorador 127.0.0.1 y pulse **Entrar**.

   ![](/help/forms/assets/screenshot2028118229.png)

Vamos a comprobar la ejecución de reglas en este formulario sin encabezado:

1. Seleccione el **Marque la casilla para recibir un 5% de descuento** opción. La opción posterior para aplicar la tarjeta de crédito está desactivada.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Desmarcar **Marque la casilla para recibir un 5% de descuento** para activar la opción de tarjeta de crédito.

   ![](/help/forms/assets/screenshot2028126329.png)

Hagamos cambios en el formulario en el servidor como usuario empresarial y veamos los cambios reflejados en el formulario sin encabezado automáticamente.

1. Abra la interfaz de administración de AEM Forms en el explorador. Por ejemplo, [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Seleccione el **registro** y haga clic en **Editar.** Abre el formulario en el editor de formularios adaptables.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Seleccione el **Número de teléfono** y haga clic en el **Icono Editar (icono de lápiz)** en la barra de herramientas. Si no puede ver la barra de herramientas emergente, cambie al modo Editar haciendo clic en **Editar** botón en la parte superior derecha, de izquierda a derecha **Previsualizar** botón.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Cambie la etiqueta a Número móvil. Haga clic en cualquier espacio vacío del formulario y se guardarán los cambios realizados en él.

   ![](/help/forms/assets/screenshot2028119729.png)

Vamos a publicar el formulario actualizado para propagar los cambios en el entorno de publicación.

1. En la pestaña Interfaz de administración de AEM Forms, seleccione el formulario de registro y haga clic en **Cancelar publicación**. Si no ve el **Cancelar publicación** , vaya al paso 3 para publicar los cambios directamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Clic **Cancelar publicación**. Clic **Cerrar** en el cuadro de diálogo correspondiente.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Una vez que el explorador se actualice, seleccione el formulario de registro y haga clic en **Publish**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Haga clic en **Publicar**. Clic **Cerrar** en el cuadro de diálogo correspondiente.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Actualice la pestaña del explorador con el formulario sin encabezado mostrado. Tenga en cuenta que la etiqueta Número de teléfono ha cambiado a Número de teléfono móvil.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Abra la ventana del Símbolo del sistema que se utiliza para iniciar el **react-starter-kit-aem-headless-forms** proyecto, presione **CTRL + C**, luego introduzca **Y** y pulse la tecla Intro para finalizar el proceso npm. Es importante detener el servidor npm para que no entre en conflicto con el siguiente conjunto de ejercicios.

1. Cierre las ventanas Código y Símbolo del sistema de Visual Studio.


## Lección 5

### Objetivo

Procesar el formulario como un formulario sin encabezado mediante la interfaz de usuario de Google Material

### Contexto de lección

En esta lección, como desarrollador front-end, aprenderá a procesar el formulario adaptable creado anteriormente como formulario sin encabezado mediante la interfaz de usuario de Material de Google.

### Ejercicio

Configure el repositorio local mediante el proyecto de inicio de la IU de Material:

1. Abra el Símbolo del sistema con derechos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)


1. En el Símbolo del sistema, utilice el siguiente comando para desplazarse a **c:\git** carpeta:

   ```Shell
   cd c:\git
   ```

1. Ejecute los siguientes comandos en el orden indicado para crear una carpeta denominada mui y vaya a la carpeta mui mediante los siguientes comandos:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Utilice el siguiente comando para clonar el proyecto de inicio de reacción del formulario adaptable:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Utilice el siguiente comando en el orden indicado para ir a **react-starter-kit-aem-headless-forms** y abra el código en Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Para procesar el formulario alojado en el entorno de publicación del servicio en la nube:

1. Cambie el nombre del **env_template** archivo a **.env** archivo. Para cambiar el nombre, haga clic con el botón derecho en **env_template** archivo y seleccione **Cambiar nombre**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Establezca los siguientes valores para las variables del archivo .env. Después de actualizar las variables, guarde el archivo. Utilice el **CTRL + S** cambiar la combinación para guardar el archivo.

   * **AEM URL_DE_LA**: especifique la URL del entorno de publicación del servicio en la nube. Por ejemplo, [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM RUTA_FORMULARIO_DE_**: especifique la ruta del formulario adaptable creado en la lección anterior. Por ejemplo, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Abra la ventana de comandos y asegúrese de que está en la **react-starter-kit-aem-headless-forms** y ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   AEM El comando inicia un servidor de desarrollo local y procesa la definición del formulario recuperada de la interfaz de usuario de Google Material de forma sin encabezado mediante la biblioteca de front-end de la interfaz de usuario de.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el explorador después de ejecutar el `npm start` comando, cambiar `localhost` en la URL del explorador 127.0.0.1 y pulse **Entrar**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Para evaluar la ejecución de la misma lógica empresarial en esta representación de formulario:

   Seleccionar **Marque la casilla para recibir un 5% de descuento**. La opción siguiente **¿Desea solicitar el formulario de tarjeta de crédito corporativa de We.Finance?** se desactiva.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lección 6

### Objetivo

Cree una apariencia alternativa del formulario sin encabezado mediante las variaciones de los componentes de la interfaz de usuario de material

### Contexto de lección

En esta lección, como desarrollador front-end, aprenderá a crear una representación alternativa de diferentes componentes mediante la interfaz de usuario de Material para el formulario adaptable creado anteriormente por el usuario empresarial.

### Ejercicio

Actualice la variación de los componentes del proyecto sin encabezado. Para cambiar la variante del componente de entrada de texto de la IU de material a `OutlinedInput`:

1. En Código visual, desplácese hasta el componente de entrada de texto abriendo `index.tsx` archivo en `src/components/textinput/index.tsx`.

1. Añadir `//` al principio de la línea de código 103. Convierte la línea en un comentario.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Agregue lo siguiente en la línea 104 para utilizar una variante diferente del componente y guarde el archivo. Utilice el **CTRL + S** cambiar la combinación para guardar el archivo.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   Es esencial utilizar mayúsculas correctas para la variante &#39;OutinedInput&#39;; de lo contrario, la compilación fallaría. La compilación del entorno de desarrollo local comienza automáticamente en el símbolo del sistema. Espere hasta que vea el siguiente mensaje

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Actualice el explorador, si no se actualiza automáticamente, para ver cómo el componente de entrada de texto utiliza una variante diferente.

   ![](/help/forms/assets/screenshot2028127729.png)


   Este cambio se produce para los usuarios finales sin ningún cambio en la definición del formulario en AEM Forms Server y es específico para el canal sin encabezado que se está considerando. Por ejemplo, el canal Web de este laboratorio.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Cierre las ventanas Código y Símbolo del sistema de Visual Studio.

## Preguntas más frecuentes (FAQ)

+++ ¿El asistente de formularios adaptables está disponible públicamente?

Sí, está disponible con AEM Forms como Cloud Service.

+++


+++ ¿Los componentes principales están disponibles públicamente?

Sí, los componentes principales de Forms adaptable están disponibles con AEM Forms como Cloud Service.

+++

+++ ¿Los formularios sin encabezado están disponibles públicamente?

Sí, los formularios sin encabezado están disponibles con AEM Forms como Cloud Service.

+++

+++ ¿Los formularios sin encabezado requieren una licencia independiente?

No, los formularios sin encabezado utilizan la misma métrica de valor de licencia, número de envíos de formularios.

+++

+++ AEM ¿Están disponibles los componentes principales y los formularios sin encabezado con Forms de 6.5?

Sí, tanto los componentes principales de los formularios adaptables como los formularios sin encabezado están disponibles con AEM Forms 6.5 Service Pack 16 y posteriores.

+++


## Pasos siguientes

Ahora que ha aprendido a crear formularios adaptables y a enviarlos a varios canales mediante formularios sin encabezado, debe intentar poner en práctica sus nuevas habilidades. Diviértase y continúe creando y entregando experiencias de captura de datos excepcionales a sus usuarios finales, donde estén, a escala.

## Recursos

* [Introducción a los componentes principales del formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Crear formularios adaptables mediante componentes principales](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Actualizar el estilo para AF basado en componentes principales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Uso del kit de inicio React sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


