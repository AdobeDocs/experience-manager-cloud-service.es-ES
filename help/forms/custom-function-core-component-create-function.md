---
title: Crear y agregar funciones personalizadas en un formulario adaptable
description: AEM Forms admite funciones personalizadas, que permiten a los usuarios crear y utilizar sus propias funciones dentro del editor de reglas.
keywords: Agregar una función personalizada, utilizar una función personalizada, crear una función personalizada, utilizar una función personalizada en el editor de reglas.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: e7ab4233-2e91-45c6-9377-0c9204d03ee9
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 13%

---

# Crear una función personalizada para un formulario adaptable basado en componentes principales

Los Forms adaptables basados en componentes principales ofrecen experiencias de usuario dinámicas al ajustar el contenido y el comportamiento en función de los datos introducidos por el usuario. Las funciones personalizadas permiten a los desarrolladores ampliar la funcionalidad, lo que garantiza que los formularios puedan satisfacer requisitos específicos. Al integrar funciones personalizadas, los desarrolladores pueden implementar lógicas complejas, automatizar procesos e introducir interacciones únicas que se alineen con los requisitos comerciales específicos o las expectativas de los usuarios. Garantiza que los formularios no solo se adapten a condiciones diferentes, sino que también proporcionen una solución más precisa y eficaz para casos de uso diversos.
Este artículo le guía a través de los pasos para crear funciones personalizadas para Forms adaptable mediante componentes principales.

## Consideraciones

* `parameter type` y `return type` no admiten `None`.

* Las funciones que no se admiten en la lista de funciones personalizadas son:
   * Funciones del generador
   * Funciones asíncronas/de espera
   * Definiciones de método
   * Métodos de clase
   * Parámetros predeterminados
   * Parámetros REST

## Requisitos previos para crear una función personalizada

Antes de empezar a agregar una función personalizada a su Forms adaptable, asegúrese de que dispone de lo siguiente:

**Software:**

* **Editor de texto sin formato (IDE)**: Aunque cualquier editor de texto sin formato puede funcionar, un entorno de desarrollo integrado (IDE) como Microsoft Visual Studio Code ofrece características avanzadas para facilitar la edición.

* **Git:** Este sistema de control de versiones es necesario para administrar cambios de código. Si no lo tiene instalado, descárguelo de https://git-scm.com.


## Creación de una función personalizada

Cree una biblioteca de cliente para llamar a funciones personalizadas en el editor de reglas. Para obtener más información, consulte [Uso de bibliotecas del lado del cliente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html?lang=es#developing).

Los pasos para crear funciones personalizadas son los siguientes:

1. [Crear una biblioteca de cliente](#create-client-library)
1. [Agregar una biblioteca de cliente a un formulario adaptable](#use-custom-function)

### Crear una biblioteca de cliente {#create-client-library}

Puede agregar funciones personalizadas agregando una biblioteca de cliente. Para crear una biblioteca de cliente, realice los siguientes pasos:

**Clonar el repositorio**

Clone su [Repositorio de AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git):

1. Abra la línea de comandos o la ventana de terminal.

1. Vaya a la ubicación deseada en el equipo donde desee almacenar el repositorio.

1. Ejecute el siguiente comando para clonar el repositorio:

   `git clone [Git Repository URL]`

Este comando descarga el repositorio y crea una carpeta local del repositorio clonado en el equipo. En esta guía, nos referimos a esta carpeta como el [directorio del proyecto AEMaaCS].

**Agregar una carpeta de biblioteca de cliente**

Para agregar una nueva carpeta de biblioteca de cliente al [directorio del proyecto AEMaaCS], siga estos pasos:

1. Abra [el directorio del proyecto AEMaaCS] en un editor.

   ![estructura de carpetas de funciones personalizadas](/help/forms/assets/custom-library-folder-structure.png)

1. Busque `ui.apps`.
1. Añada una carpeta nueva. Por ejemplo, agregue una carpeta denominada como `experience-league`.
1. Vaya a la carpeta `/experience-league/` y agregue un(a) `ClientLibraryFolder`. Por ejemplo, cree una carpeta de biblioteca de cliente llamada `customclientlibs`.

   `Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Agregar archivos y carpetas a la carpeta Biblioteca de cliente**

Agregue lo siguiente a la carpeta de biblioteca de cliente agregada:

* archivo .content.xml
* archivo js.txt
* carpeta js

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. En `.content.xml`, agregue las siguientes líneas de código:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > Puede elegir cualquier nombre para la propiedad `client library folder` y `categories`.

1. En `js.txt`, agregue las siguientes líneas de código:

   ```javascript
         #base=js
       function.js
   ```

1. En la carpeta `js`, agregue el archivo javascript como `function.js`, que incluye las funciones personalizadas:

   ```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */
   
    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();
   
    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();
   
    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }
   
    return age;
    }
   ```

1. Guarde los archivos.

![estructura de carpetas de funciones personalizadas](/help/forms/assets/custom-function-added-files.png)

**Incluir la nueva carpeta en filter.xml**:

1. Vaya al archivo `/ui.apps/src/main/content/META-INF/vault/filter.xml` en su [directorio del proyecto AEMaaCS].

1. Abra el archivo y añada la siguiente línea al final:

   `<filter root="/apps/experience-league" />`
1. Guarde el archivo.

![xml de filtro de función personalizada](/help/forms/assets/custom-function-filterxml.png)

**Implemente la carpeta de la biblioteca de cliente recién creada en su entorno de AEM**

Implemente AEM as a Cloud Service, [directorio del proyecto AEMaaCS], en su entorno de Cloud Service. Para implementarlo en el entorno de Cloud Service:

1. Confirme los cambios

   1. Añada, confirme e inserte los cambios en el repositorio mediante los siguientes comandos:

   ```javascript
       git add .
       git commit -a -m "Adding custom functions"
       git push
   ```

1. Implemente el código actualizado:

   1. Almacene en déclencheur una implementación del código a través de la canalización de pila completa existente. Esto crea e implementa automáticamente el código actualizado.

Si aún no ha configurado una canalización, consulte la guía sobre [cómo configurar una canalización para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline).

Una vez que la canalización se haya ejecutado correctamente, la función personalizada agregada en la biblioteca de cliente estará disponible en el [editor de reglas de formularios adaptables](/help/forms/rule-editor-core-components.md).

### Agregar una biblioteca de cliente a un formulario adaptable{#use-custom-function}

Una vez que haya implementado la biblioteca de cliente en el entorno de Forms CS, utilice sus funcionalidades en el formulario adaptable. Para agregar la biblioteca de cliente en el formulario adaptable

1. Abra el formulario en modo de edición. Para abrir un formulario en modo de edición, seleccione un formulario y seleccione **[!UICONTROL Editar]**.
1. Abra el Explorador de contenido y seleccione el componente **[!UICONTROL Contenedor de guía]** del formulario adaptable.
1. Haga clic en el icono de propiedades del contenedor de guía ![Propiedades de guía](/help/forms/assets/configure-icon.svg). Se abre el cuadro de diálogo Contenedor de formulario adaptable.
1. Abra la ficha **[!UICONTROL Básico]** y seleccione el nombre de la **[!UICONTROL categoría de biblioteca de cliente]** en la lista desplegable (en este caso, seleccione `customfunctionscategory`).

   ![Agregar la biblioteca de cliente de funciones personalizada](/help/forms/assets/clientlib-custom-function.png)

   >[!NOTE]
   >
   > Se pueden agregar varias categorías especificando una lista separada por comas dentro del campo **[!UICONTROL Categoría de biblioteca de cliente]**.

1. Haga clic en **[!UICONTROL Listo]**.

Puede usar la función personalizada en el [editor de reglas de un formulario adaptable](/help/forms/rule-editor-core-components.md) mediante las [anotaciones de JavaScript](##js-annotations).

## Usar una función personalizada en un formulario adaptable

En un formulario adaptable, puede usar [funciones personalizadas dentro del editor de reglas](/help/forms/rule-editor-core-components.md). Agregue el siguiente código al archivo JavaScript (archivo `Function.js`) para calcular la edad en función de la fecha de nacimiento (DD-MM-AAAA). Cree una función personalizada como `calculateAge()` que tome la fecha de nacimiento como entrada y devuelva la edad:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

En el ejemplo anterior, cuando el usuario introduce la fecha de nacimiento con el formato (AAAA-MM-DD), se invoca la función personalizada `calculateAge` y se devuelve la edad.

![Calcular función personalizada Agae en el editor de reglas](/help/forms/assets/custom-function-calculate-age.png)

Vamos a previsualizar el formulario para observar cómo se implementan las funciones personalizadas a través del editor de reglas:

![Calcular función personalizada Agae en la vista previa de formulario del Editor de reglas](/help/forms/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Puede hacer referencia a la carpeta [función personalizada](/help/forms/assets//customfunctions.zip) siguiente. Descargue e instale esta carpeta en su instancia de AEM mediante [Administrador de paquetes](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager).

## Características de las funciones personalizadas

Las funciones personalizadas de los formularios AEM ofrecen una solución sólida para ampliar y personalizar la funcionalidad de los formularios. Puede utilizar las funciones personalizadas para satisfacer las necesidades específicas de su organización.

Estas funciones admiten varias funciones, como trabajar con campos específicos, utilizar campos globales y operaciones asincrónicas, así como incorporar mecanismos de almacenamiento en caché. Esta flexibilidad garantiza que los formularios se puedan adaptar a requisitos complejos y ofrecer una experiencia de usuario eficiente y adaptada. Al aprovechar estas funciones avanzadas, puede mejorar las interacciones entre formularios y optimizar el rendimiento, lo que hace que los formularios de AEM sean más funcionales y adaptables.

Vamos a profundizar en las funciones personalizadas.

### Compatibilidad asíncrona en funciones personalizadas {#support-of-async-functions}

Puede implementar funciones asincrónicas en el editor de reglas mediante funciones personalizadas. Para obtener instrucciones sobre cómo hacerlo, consulte el artículo [Uso de funciones asincrónicas en un formulario adaptable](/help/forms/using-async-funct-in-rule-editor.md).

### Compatibilidad con objetos de ámbito global y de campo en funciones personalizadas {#support-field-and-global-objects}

Los objetos de campo hacen referencia a los componentes o elementos individuales de un formulario, como campos de texto o casillas de verificación. El objeto Globals contiene variables de solo lectura como la instancia de formulario, la instancia del campo de destino y los métodos para realizar modificaciones de formulario dentro de funciones personalizadas.

>[!NOTE]
>
> `param {scope} globals` debe ser el último parámetro y no se mostrará en el editor de reglas de un formulario adaptable.

Para obtener más información sobre los objetos de ámbito, vea el artículo [Objetos de ámbito en funciones personalizadas](/help/forms/custom-function-core-component-scope-function.md).

### Compatibilidad con el almacenamiento en caché en función personalizada

Los Forms adaptables implementan el almacenamiento en caché de funciones personalizadas para mejorar el tiempo de respuesta al recuperar la lista de funciones personalizadas en el editor de reglas. Aparece un mensaje como `Fetched following custom functions list from cache` en el archivo `error.log`.

![función personalizada con compatibilidad con caché](/help/forms/assets/custom-function-cache-error.png)

En caso de que se modifiquen las funciones personalizadas, el almacenamiento en caché se invalidará y se analizará.

## Resolución de problemas

* Si el archivo JavaScript que contiene código para funciones personalizadas tiene un error, las funciones personalizadas no aparecen en el editor de reglas de un formulario adaptable. Para comprobar la lista de funciones personalizadas, puede desplazarse al archivo `error.log` en busca del error. En caso de error, la lista de funciones personalizadas aparece vacía:

  ![archivo de registro de errores](/help/forms/assets/custom-function-list-error-file.png)

  En caso de que no haya ningún error, las funciones personalizadas se recuperan y aparecen en el archivo `error.log`. Aparece un mensaje como `Fetched following custom functions list` en el archivo `error.log`:

  ![archivo de registro de errores con la función personalizada adecuada](/help/forms/assets/custom-function-list-fetched-in-error.png)

## Siguiente paso

Veamos ahora varios [ejemplos de funciones personalizadas para un formulario adaptable basadas en componentes principales](/help/forms/custom-function-core-components-use-cases.md).

## Véase también

{{see-also-rule-editor}}
