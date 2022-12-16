---
title: Introducción y tutorial de SPA
description: Este artículo presenta los conceptos de un SPA y explica cómo utilizar una aplicación de SPA básica para la creación, mostrando cómo se relaciona con el AEM SPA Editor subyacente.
exl-id: 8dad48d5-fa90-467c-8bec-e4b76e057f80
source-git-commit: f201e8bf8a44db6b408edec5b77cc814c7e87abb
workflow-type: tm+mt
source-wordcount: '2076'
ht-degree: 2%

---

# Introducción y tutorial de SPA {#spa-introduction}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder crear sitios mediante marcos de SPA y los autores quieren editar contenido sin problemas dentro de AEM para un sitio creado con dichos marcos.

El SPA Editor ofrece una solución completa para admitir SPA dentro de AEM. Este artículo recorre mediante una aplicación de SPA básica para la creación y muestra cómo se relaciona con el AEM SPA Editor subyacente.

## Introducción {#introduction}

### Objetivo del artículo {#article-objective}

Este artículo presenta los conceptos básicos de SPA antes de guiar al lector a través de un tutorial del editor de SPA utilizando una sencilla aplicación SPA para demostrar la edición básica del contenido. A continuación, se profundiza en la construcción de la página y en cómo se relaciona la aplicación SPA con el AEM SPA Editor y cómo interactúa con ella.

El objetivo de esta introducción y tutorial es demostrar a un desarrollador AEM por qué los SPA son relevantes, cómo funcionan en general, cómo el editor de SPA gestiona un SPA y cómo es diferente de una aplicación AEM estándar.

## Requisitos  {#requirements}

El tutorial se basa en la funcionalidad AEM estándar y en la aplicación de proyecto WKND SPA de ejemplo. Para seguir con este tutorial, debe tener disponible lo siguiente.

* [Último SDK de desarrollo de AEMaaCS](/help/release-notes/release-notes-cloud/release-notes-current.md)
   * Debe ejecutarse como un entorno de desarrollo local.
   * Debe tener derechos de administrador en el sistema.
* [La aplicación de proyecto WKND SPA de ejemplo está disponible en GitHub](https://github.com/adobe/aem-guides-wknd-spa)
   * Descargue el [última versión de la aplicación React](https://github.com/adobe/aem-guides-wknd-spa/releases) se denomina similar a `wknd-spa-react.all-X.Y.Z-SNAPSHOT.zip`.
   * Descargue el [últimas imágenes de ejemplo para la aplicación](https://github.com/adobe/aem-guides-wknd-spa/releases) se denomina similar a `wknd-spa-sample-images-X.Y.Z.zip`.
   * [Usar el gestor de paquetes](/help/implementing/developing/tools/package-manager.md) para instalar ambos paquetes como si se tratara de cualquier otro paquete en AEM.
   * No es necesario instalar la aplicación mediante Maven para realizar este tutorial.

>[!CAUTION]
>
>Este documento utiliza la variable [Aplicación de proyecto WKND SPA](https://github.com/adobe/aem-guides-wknd-spa) únicamente con fines de demostración. No debe utilizarse para ningún trabajo de proyecto.

>[!TIP]
>
>Cualquier proyecto AEM debería aprovechar el [Tipo de archivo del proyecto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es), que admite SPA proyectos que utilizan React o Angular y aprovecha el SDK de SPA.

### ¿Qué es un SPA? {#what-is-a-spa}

Una aplicación de una sola página (SPA) difiere de una página convencional en que se procesa en el lado del cliente y principalmente está dirigida por JavaScript, y se basa en llamadas Ajax para cargar datos y actualizar la página de forma dinámica. La mayoría o todo el contenido se recupera una vez en una única carga de página con recursos adicionales cargados asincrónicamente según sea necesario en función de la interacción del usuario con la página.

Esto reduce la necesidad de actualizar la página y presenta al usuario una experiencia que es fluida, rápida y se parece más a una experiencia nativa de la aplicación.

El AEM SPA Editor permite a los desarrolladores de front-end crear SPA que se pueden integrar en un sitio AEM, lo que permite a los autores de contenido editar el contenido SPA tan fácilmente como cualquier otro contenido AEM.

### ¿Por qué un SPA? {#why-a-spa}

Al ser más rápido, fluido y más parecido a una aplicación nativa, una SPA se convierte en una experiencia muy atractiva no solo para el visitante de la página web, sino también para los especialistas en marketing y desarrolladores debido a la naturaleza de cómo SPA funciona.

![SPA beneficios](assets/spa-benefits.png)

#### Visitantes {#visitors}

* Los visitantes desean experiencias nativas cuando interactúan con el contenido.
* Hay datos claros de que cuanto más rápida sea una página, más probable será que se produzca una conversión.

#### Especialistas en marketing {#marketers}

* Los especialistas en marketing desean ofrecer experiencias ricas y nativas para atraer visitantes a fin de que participen plenamente en el contenido.
* La personalización puede hacer que estas experiencias sean aún más atractivas.

#### Desarrolladores {#developers}

* Los desarrolladores quieren una separación clara de las preocupaciones entre el contenido y la presentación.
* La separación limpia hace que el sistema sea más extensible y permite el desarrollo independiente del front-end.

### ¿Cómo funciona un SPA? {#how-does-a-spa-work}

La idea principal detrás de una SPA es que las llamadas a un servidor y su dependencia se reducen para minimizar los retrasos causados por la latencia del servidor de modo que el SPA se aproxime a la capacidad de respuesta de una aplicación nativa.

En una página web secuencial tradicional, solo se cargan los datos necesarios para la página inmediata. Esto significa que cuando el visitante se mueve a otra página, se llama al servidor para obtener los recursos adicionales. Es posible que sea necesario realizar llamadas adicionales, ya que el visitante interactúa con elementos de la página. Estas llamadas múltiples pueden dar una sensación de retraso o retraso, ya que la página tiene que estar al día con las solicitudes del visitante.

![Experiencias secuenciales frente a fluidas](assets/spa-sequential-vs-fluid.png)

Para obtener una experiencia más fluida, que se acerca a lo que un visitante espera de las aplicaciones móviles nativas, un SPA carga todos los datos necesarios para el visitante en la primera carga. Aunque esto puede tardar un poco más al principio, elimina la necesidad de realizar llamadas al servidor adicionales.

Al realizar el procesamiento en el lado del cliente, los elementos de página reaccionan más rápido y las interacciones con la página por parte del visitante son inmediatas. Cualquier dato adicional que se necesite se llama asincrónicamente para maximizar la velocidad de la página.

>[!TIP]
>
>Para obtener detalles técnicos sobre cómo SPA funciona en AEM, consulte los artículos:
>* [Introducción a SPA en AEM con React](getting-started-react.md)
>* [Introducción a SPA en AEM Uso de Angular](getting-started-angular.md)
>
>Para obtener una vista más detallada del diseño, la arquitectura y el flujo de trabajo técnico del SPA Editor, consulte el artículo:
>* [Información general del editor de SPA](editor-overview.md).


## Experiencia de edición de contenido con SPA {#content-editing-experience-with-spa}

Cuando se crea un SPA para aprovechar el AEM SPA Editor, el autor del contenido no observa ninguna diferencia al editar y crear contenido. La funcionalidad de AEM común está disponible y no se requieren cambios en el flujo de trabajo del autor.

1. Edite la aplicación WKND SPA Project en AEM.

   `http://localhost:4502/editor.html/content/wknd-spa-react/us/en/home.html`

   ![Inicio del proyecto WKND SPA](assets/wknd-home.png)

1. Seleccione un componente de texto y observe que aparece una barra de herramientas como cualquier otro componente. Seleccione **Editar**.

   ![Seleccionar componente de texto](assets/wknd-text.png)

1. Edite el contenido como de costumbre dentro de AEM y tenga en cuenta que los cambios se mantienen.

   ![Editar texto](assets/wknd-edit-text.png)

1. Utilice el navegador de recursos para arrastrar y soltar una nueva imagen en un componente de imagen.

   ![Colocación de un recurso de imagen](assets/wkdn-drop-image.png)

1. El cambio se mantiene.

   ![Imagen persistida](assets/wknd-change-persisted.png)

Se admiten herramientas de creación adicionales, como arrastrar y soltar componentes adicionales en la página, reorganizar componentes y modificar el diseño, como en cualquier aplicación AEM que no sea de SPA.

>[!NOTE]
>
>El Editor de SPA no modifica el DOM de la aplicación. El propio SPA es responsable del DOM.
>
>Para ver cómo funciona esto, continúe con la siguiente sección de este artículo. [Aplicaciones SPA y el AEM SPA Editor](#spa-apps-and-the-aem-spa-editor).

## Aplicaciones SPA y el AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

Experimentar cómo se comporta un SPA para el usuario final y luego inspeccionar la página SPA ayuda a comprender mejor cómo funciona una aplicación SAP con el SPA Editor en AEM.

### Uso de una aplicación SPA {#using-an-spa-application}

1. Cargue la aplicación WKND SPA Project en el servidor de publicación o con la opción **Ver tal y como aparece publicado** de la variable **Información de la página** en el editor de páginas.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Vista previa del inicio del proyecto WKND SPA](assets/wknd-preview.png)

   Tenga en cuenta la estructura de las páginas, incluida la navegación a páginas secundarias, menú y tarjetas de artículos.

1. Vaya a una página secundaria mediante el menú y vea que la página se carga inmediatamente sin necesidad de actualizar.

   ![WKND SPA Project página 1](assets/wknd-page1.png)

1. Abra las herramientas de desarrollador integradas del explorador y supervise la actividad de red a medida que navega por las páginas secundarias.

   ![Actividad de red](assets/wknd-network-activity.png)

   Hay muy poco tráfico a medida que se mueve de página en página en la aplicación. La página no se vuelve a cargar y solo se solicitan las imágenes nuevas.

   El SPA administra el contenido y el enrutamiento por completo en el lado del cliente.

Por lo tanto, si la página no se vuelve a cargar al navegar por las páginas secundarias, ¿cómo se carga?

La siguiente sección, [Carga de una aplicación SPA](#loading-a-spa-application), profundiza en la mecánica de carga del SPA y en cómo se puede cargar el contenido sincrónica y asincrónicamente.

### Carga de una aplicación SPA {#loading-a-spa-application}

1. Si aún no se ha cargado, cargue la aplicación WKND SPA Project en el servidor de publicación o utilizando la opción **Ver tal y como aparece publicado** de la variable **Información de la página** en el editor de páginas.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.html`

   ![Vista previa del proyecto SPA WKND](assets/wknd-preview.png)

1. Utilice la herramienta integrada del navegador para ver el origen de la página.
1. Tenga en cuenta que el contenido de la fuente es limitado.
   * La página no tiene contenido dentro de su cuerpo. Se compone principalmente de hojas de estilo y una llamada a varios scripts como `clientlib-react.min.js`.
   * Estos scripts son los principales controladores de esta aplicación y son responsables de procesar todo el contenido.

1. Utilice las herramientas integradas del explorador para inspeccionar la página. Consulte el contenido del DOM completamente cargado.

   ![DOM del proyecto WKND SPA](assets/wknd-dom.png)

1. Cambie a la ficha Red (Network) en el Inspector y vuelva a cargar la página.

   Ignorando las solicitudes de imagen, tenga en cuenta que los recursos principales cargados para la página son la página en sí, CSS, React Javascript, sus dependencias, así como los datos JSON de la página.

   ![Actividad de red del proyecto WKND SPA](assets/wknd-network.png)

1. Cargue el `home.model.json` en una pestaña nueva.

   `http://<host>:<port>/content/wknd-spa-react/us/en/home.model.json`

   ![JSON de la página de inicio del proyecto WKND SPA](assets/wknd-json.png)

   El AEM SPA Editor aprovecha [Servicios de contenido AEM](/help/sites-cloud/administering/content-fragments/content-fragments.md) para entregar todo el contenido de la página como un modelo JSON.

   Al implementar interfaces específicas, los modelos Sling proporcionan la información necesaria para el SPA. El envío de los datos JSON se delega hacia abajo en cada componente (de página, párrafo, componente, etc.).

   Cada componente elige lo que expone y cómo se procesa (lado del servidor con HTL o lado del cliente con React o Angular). Este artículo se centra en la renderización del lado del cliente con React.

1. El modelo también puede agrupar las páginas de forma que se carguen sincrónicamente, lo que reduce el número de recargas de página necesarias.

   En el ejemplo de la aplicación WKND SPA Project, la variable `home`, `page-1`, `page-2`y `page-3` las páginas se cargan sincrónicamente, ya que los visitantes suelen visitar todas esas páginas.

   Este comportamiento no es obligatorio y es totalmente definible.

   ![WKND SPA Agrupación de elementos del proyecto](assets/wknd-pages.png)

1. Para ver esta diferencia de comportamiento, vuelva a cargar la variable `home` y borre la actividad de red del inspector. Vaya a `page-1` en el menú de página y vea que la única actividad de red es una solicitud de imagen de `page-1`. `page-1` no necesita cargarse.

   ![WKND SPA Proyecto página 1 Actividad de red](assets/wknd-page1-network.png)

### Interacción con el SPA Editor {#interaction-with-the-spa-editor}

Con la aplicación de proyecto WKND SPA de ejemplo, está claro cómo se comporta y se carga la aplicación cuando se publica, aprovechando los servicios de contenido para la entrega de contenido JSON, así como la carga asíncrona de recursos.

Además, para el autor del contenido, la creación de contenido mediante un editor de SPA es perfecta dentro de AEM.

En la siguiente sección analizaremos el contrato que permite al Editor de SPA relacionar componentes dentro del SPA con componentes de AEM y lograr esta experiencia de edición sin problemas.

1. Cargue la aplicación WKND SPA Project en el editor y cambie a **Vista previa** en el menú contextual.

   `http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`

1. Con las herramientas de desarrollador incorporadas del navegador, inspeccione el contenido de la página. Con la herramienta de selección, seleccione un componente editable en la página y vea los detalles del elemento.

   Tenga en cuenta que el componente tiene un nuevo atributo de datos `data-cq-data-path`.

   ![Inspección de elementos del proyecto WKND SPA](assets/wknd-inspector.png)

   Por ejemplo

   `data-cq-data-path="/content/wknd-spa-react/us/en/home/jcr:content/root/responsivegrid/text`

   Esta ruta permite la recuperación y asociación del objeto de configuración de contexto de edición de cada componente.

   Este es el único atributo de marcado necesario para que el editor reconozca este componente como editable dentro del SPA. En función de este atributo, el SPA Editor determinará qué configuración editable está asociada al componente, de modo que el marco, la barra de herramientas, etc. correctos. se carga.

   También se agregan algunos nombres de clase específicos para marcar marcadores de posición y para la funcionalidad de arrastrar y soltar recursos.

   >[!NOTE]
   >
   >Este comportamiento difiere de las páginas procesadas del lado del servidor en AEM, donde hay un `cq` elemento insertado para cada componente editable.
   >
   >Este método en el Editor de SPA elimina la necesidad de insertar elementos personalizados, ya que solo se basa en un atributo de datos adicional, lo que simplifica el marcado para el desarrollador de front-end.

## Encabezado y sin encabezado en AEM {#headful-headless}

SPA se pueden habilitar con niveles flexibles de integración dentro de AEM, incluso SPA desarrollarse y mantenerse fuera de AEM. Además, SPA se puede aprovechar dentro de AEM mientras también se utilizan AEM para ofrecer contenido a extremos adicionales sin objetivos.

>[!TIP]
>
>Consulte el documento [Con encabezado y sin encabezado en AEM](/help/implementing/developing/headful-headless.md) para obtener más información.

## Pasos siguientes {#next-steps}

Ahora que comprende la SPA experiencia de edición en AEM y cómo se relaciona un SPA con el Editor de SPA, profundiza en la comprensión de cómo se crea un SPA.

* [Introducción a SPA en AEM con React](getting-started-react.md) muestra cómo se crea una SPA básica para trabajar con el Editor de SPA en AEM con React
* [Introducción a SPA en AEM con Angular](getting-started-angular.md) muestra cómo se crea una SPA básica para trabajar con el Editor de SPA en AEM con Angular
* [Información general del Editor de SPA](editor-overview.md) profundiza en el modelo de comunicación entre AEM y el SPA.
* [Desarrollo de SPA para AEM](developing.md) describe cómo involucrar a los desarrolladores de front-end para que desarrollen un SPA para AEM, así como cómo SPA interactúan con AEM arquitectura.
