---
title: Configuración de la segmentación con ContextHub
description: Obtenga información sobre cómo configurar la segmentación mediante ContextHub.
translation-type: tm+mt
source-git-commit: 82ad2cda70dd664ac9456a04f34e2d5831687fc1
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 2%

---


# Configuración de la segmentación con ContextHub{#configuring-segmentation-with-contexthub}

La segmentación es una consideración clave al crear una campaña. Consulte [Explicación de la segmentación](segmentation.md) para obtener información sobre cómo funciona la segmentación y los términos clave.

En función de la información que ya haya recopilado sobre los visitantes del sitio y los objetivos que desee alcanzar, deberá definir los segmentos y estrategias necesarios para el contenido objetivo.

Estos segmentos se utilizan para proporcionar un visitante con contenido dirigido específicamente. [Las actividades](activities.md) definidas aquí se pueden incluir en cualquier página y definir para qué segmento de visitante se aplica el contenido especializado.

AEM permite personalizar fácilmente las experiencias de los usuarios. También le permite verificar los resultados de las definiciones de segmentos.

## Acceso a segmentos {#accessing-segments}

La consola [Audiencias](audiences.md) se utiliza para administrar segmentos para ContextHub, así como audiencias para su cuenta de Adobe Target. Esta documentación cubre la administración de segmentos para ContextHub.

Para acceder a los segmentos, en la navegación global seleccione **Navegación > Personalización > Audiencias**.

![Administración de audiencias](/help/sites-cloud/authoring/assets/contexthub-segmentation-audiences.png)

## Editor de segmentos {#segment-editor}

<!--The **Segment Editor** allows you to easily modify a segment. To edit a segment, select a segment in the [list of segments](/help/sites-administering/segmentation.md#accessing-segments) and click the **Edit** button.-->
El Editor **** de segmentos le permite modificar fácilmente un segmento. Para editar un segmento, seleccione un segmento en la lista de segmentos y haga clic en el botón **Editar** .

![Editor de segmentos](/help/sites-cloud/authoring/assets/contexthub-segment-editor.png)

Con el navegador de componentes, puede agregar contenedores **Y** y **O** para definir la lógica del segmento, luego agregar componentes adicionales para comparar propiedades y valores o secuencias de comandos de referencia y otros segmentos para definir los criterios de selección (consulte [Creación de un nuevo segmento](#creating-a-new-segment)) para definir el escenario exacto para seleccionar el segmento.

Cuando toda la instrucción se evalúa como true, el segmento se ha resuelto. En el evento de que se apliquen varios segmentos, también se utiliza el factor de **ampliación** . Consulte [Creación de un nuevo segmento](#creating-a-new-segment) para obtener más información sobre el factor de ampliación.

>[!CAUTION]
>
>El editor de segmentos no comprueba la existencia de referencias circulares. Por ejemplo, el segmento A hace referencia a otro segmento B, que a su vez hace referencia al segmento A. Debe asegurarse de que los segmentos no contengan referencias circulares.

### Containers {#containers}

Los siguientes contenedores están disponibles de forma predeterminada y permiten agrupar comparaciones y referencias para la evaluación booleana. Se pueden arrastrar del navegador de componentes al editor. Consulte la siguiente sección [Uso de los Contenedores](#using-and-and-or-containers) Y y O para obtener más información.

|  |  |
|---|---|
| Contenedor Y | Operador Y booleano |
| Contenedor O | El operador booleano OR |

### Comparaciones {#comparisons}

Las siguientes comparaciones de segmentos están disponibles de forma predeterminada para evaluar las propiedades de los mismos. Se pueden arrastrar del navegador de componentes al editor.

|  |  |
|---|---|
| Propiedad-Valor | Compara una propiedad de un almacén con un valor definido |
| Propiedad | Compara una propiedad de un almacén con otra propiedad |
| Referencia de propiedad-segmento | Compara una propiedad de un almacén con otro segmento al que se hace referencia |
| Referencia de secuencias de comandos de propiedad | Compara una propiedad de un almacén con los resultados de una secuencia de comandos |
| Referencia de secuencias de comandos de referencia de segmentos | Compara un segmento referenciado con los resultados de una secuencia de comandos |

>[!NOTE]
>
>Al comparar valores, si el tipo de datos de la comparación no está establecido (es decir, configurado para detección automática), el motor de segmentación de ContextHub simplemente comparará los valores como lo haría javascript. No arroja valores a sus tipos esperados, lo que puede llevar a resultados engañosos. Por ejemplo:
>
>`null < 30 // will return true`
>
>Por lo tanto, al [crear un segmento](#creating-a-new-segment), debe seleccionar un tipo **de** datos siempre que se conozcan los tipos de valores comparados. Por ejemplo:
>
>Al comparar la propiedad `profile/age`, ya sabe que el tipo comparado será **número**, por lo que incluso si no `profile/age` se establece, una comparación `profile/age` menor que 30 devolverá **falso**, como es de esperar.

### Referencias {#references}

Las siguientes referencias están disponibles de forma predeterminada para vincularse directamente a una secuencia de comandos u otro segmento. Se pueden arrastrar del navegador de componentes al editor.

|  |  |
|---|---|
| Referencia del segmento | Evaluar el segmento al que se hace referencia |
| Referencia de script | Evalúe la secuencia de comandos a la que se hace referencia. Consulte la siguiente sección [Uso de referencias](#using-script-references) de secuencias de comandos para obtener más información. |

## Creating a New Segment {#creating-a-new-segment}

Para definir el nuevo segmento:

1. Después de [acceder a los segmentos](#accessing-segments), toque o haga clic en el botón Crear y seleccione **Crear segmento** de ContextHub.

   ![Añadir segmento](/help/sites-cloud/authoring/assets/contexthub-create-segment.png)

1. En el **nuevo segmento** de ContextHub, escriba un título para el segmento, así como un valor de ampliación si es necesario y, a continuación, toque o haga clic en **Crear**.

   ![Nuevo segmento](/help/sites-cloud/authoring/assets/contexthub-new-segment.png)

   Cada segmento tiene un parámetro de ampliación que se utiliza como factor de ponderación. Un número mayor indica que el segmento se seleccionará en lugar de un segmento con un número menor en las instancias en las que varios segmentos son válidos.

   * Minimum value: `0`
   * Maximum value: `1000000`

1. Desde la consola de segmentos, edite el segmento recién creado para abrirlo en el editor de segmentos.
1. Arrastre una comparación o referencia al editor de segmentos que aparecerá en el contenedor Y predeterminado.
1. Haga clic con el doble o toque la opción de configuración de la nueva referencia o segmento para editar los parámetros específicos. En este ejemplo, estamos probando personas en Basilea.

   ![Pruebas para personas en Basilea](/help/sites-cloud/authoring/assets/contexthub-comparing-property-value.png)

   Configure siempre un tipo **de** datos si es posible para asegurarse de que las comparaciones se evalúan correctamente. Consulte [Comparaciones](#comparisons) para obtener más información.

1. Click **Done** to save your definition:
1. Agregue más componentes según sea necesario. Puede formular expresiones booleanas utilizando los componentes de contenedor para las comparaciones Y y O (consulte [Uso de Contenedores](#using-and-and-or-containers) Y y O más adelante). Con el editor de segmentos puede eliminar componentes que ya no se necesitan o arrastrarlos a nuevas posiciones dentro de la instrucción.

### Uso de Contenedores Y y O {#using-and-and-or-containers}

Con los componentes de contenedor Y y O, puede construir segmentos complejos en AEM. Al hacer esto, ayuda tener en cuenta algunos puntos básicos:

* El nivel superior de la definición es siempre el contenedor AND que se crea inicialmente. Esto no se puede cambiar, pero no afecta al resto de la definición del segmento.
* Asegúrese de que la anidación del contenedor tenga sentido. Los contenedores se pueden ver como corchetes de la expresión booleana.

El siguiente ejemplo se utiliza para seleccionar visitantes que se consideran en nuestro grupo destinatario suizo:

```text
 People in Basel

 OR

 People in Zürich
```

El inicio se realiza colocando un componente de contenedor O dentro del contenedor Y predeterminado. En el contenedor O puede agregar la propiedad o los componentes de referencia.

![Segmento con operador O](/help/sites-cloud/authoring/assets/contexthub-or-operator.png)

Puede anidar varios operadores Y y O según sea necesario.

### Uso de referencias de script {#using-script-references}

Mediante el componente Referencia de secuencia de comandos, la evaluación de una propiedad de segmento se puede delegar en una secuencia de comandos externa. Una vez configurada correctamente la secuencia de comandos, puede utilizarse como cualquier otro componente de una condición de segmento.

#### Definición de una secuencia de comandos para referencia {#defining-a-script-to-reference}

1. Añadir archivo a `contexthub.segment-engine.scripts` clientlib.
1. Implemente una función que devuelva un valor. Por ejemplo:

   ```javascript
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. Registre la secuencia de comandos con `ContextHub.SegmentEngine.ScriptManager.register`.

Si la secuencia de comandos depende de propiedades adicionales, la secuencia de comandos debe llamar `this.dependOn()`. Por ejemplo, si la secuencia de comandos depende de `profile/age`:

```javascript
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### Referencia a un script {#referencing-a-script}

1. Cree un segmento de ContextHub.
1. Añada el componente Referencia **de** secuencia de comandos en el lugar deseado del segmento.
1. Abra el cuadro de diálogo de edición del componente Referencia **de** secuencia de comandos. Si está [correctamente configurado](#defining-a-script-to-reference), la secuencia de comandos debe estar disponible en la lista desplegable de nombres **de** secuencia de comandos.

## Prueba de la aplicación de un segmento {#testing-the-application-of-a-segment}

Una vez definido el segmento, los posibles resultados se pueden probar con la ayuda de **[ContextHub](contexthub.md).**

1. Previsualización de una página
1. Haga clic en el icono de ContextHub para mostrar la barra de herramientas de ContextHub
1. Seleccione una persona que coincida con el segmento que ha creado
1. ContextHub resolverá los segmentos aplicables para la persona seleccionada

Por ejemplo: nuestra definición de segmento simple para identificar usuarios en Basilea se basa en la ubicación del usuario. Al cargar una persona específica que coincida con esos criterios, se muestra si el segmento se ha resuelto correctamente:

![Segmento que se resuelve](/help/sites-cloud/authoring/assets/contexthub-segment-resolve.png)

O si no se resuelve:

![Segmento que no se resuelve](/help/sites-cloud/authoring/assets/contexthub-segment-doesnt-resolve.png)

>[!NOTE]
>
>Todas las características se resuelven inmediatamente, aunque la mayoría solo cambia al volver a cargar la página.

Estas pruebas también se pueden realizar en páginas de contenido y en combinación con contenido de destino y **Actividades** y **experiencias** relacionadas.

Si ha configurado una actividad y experiencia, puede probar fácilmente el segmento con la actividad. Para obtener más información sobre la configuración de una actividad, consulte la [documentación relacionada con la creación de contenido](targeted-content.md)de destino.

1. En el modo de edición de una página en la que haya configurado contenido de destino, puede ver que el contenido se dirige mediante un icono de flecha en el contenido.
1. Cambie al modo de previsualización y, con el concentrador de contexto, cambie a una persona que no coincida con la segmentación configurada para la experiencia.
1. Cambie a una persona que no coincida con la segmentación configurada para la experiencia y observe que la experiencia cambia en consecuencia.

## Uso del segmento {#using-your-segment}

Los segmentos se utilizan para controlar el contenido real que ven audiencias de destinatario específicas. Consulte [Administración de Audiencias](audiences.md) para obtener más información sobre audiencias y segmentos y [Creación de contenido](targeted-content.md) de destino sobre el uso de audiencias y segmentos para destinatario de contenido.
