---
title: Operaciones de desarrollo empresarial
description: Obtenga información sobre los procesos, métodos y comunicaciones necesarios para facilitar la implementación y la colaboración.
exl-id: c8da1fd7-fe3e-4c7b-8fe7-1f7faf02769c
source-git-commit: 1a4c5e618adaef99d82a00e1118d1a0f8536fc14
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 100%

---

# Operaciones de desarrollo empresarial{#enterprise-devops}

Las DevOps abarcan los procesos, métodos y comunicaciones necesarios para lo siguiente:

* Facilitar la implementación del software en los distintos entornos.
* Simplificar la colaboración entre los equipos de desarrollo, prueba e implementación.

Las operaciones de desarrollo empresarial tienen como objetivo evitar problemas como los siguientes:

* Errores manuales.
* Elementos olvidados; por ejemplo, archivos, detalles de configuración.
* Discrepancias; por ejemplo, entre el entorno local de un desarrollador y otros entornos.

## Entornos {#environments}

Adobe Experience Manager (AEM) as a Cloud Service suele consistir en varios entornos, que se utilizan para diferentes propósitos en diferentes niveles:

* [Desarrollo](#development)
* [Garantía de calidad](#quality-assurance)
* [Ensayo](#staging)
* [Producción](#production-author-and-publish)

>[!NOTE]
>
>El entorno de producción debe tener al menos un autor y un entorno de publicación.
>
>Se recomienda que todos los demás entornos también consten de un entorno de creación y publicación para reflejar el entorno de producción y permitir las pruebas tempranas.

### Desarrollo {#development}

Los desarrolladores son responsables de desarrollar y personalizar el proyecto propuesto (ya sea el sitio web, las aplicaciones móviles, la implementación de DAM, etc.), con todas las funcionalidades requeridas. Estos procedimientos:

* desarrollan y personalizan los elementos necesarios; por ejemplo, plantillas, componentes, flujos de trabajo, aplicaciones.
* Realizan el diseño.
* Desarrollan los servicios y secuencias de comandos necesarios para implementar las funcionalidades requeridas

La configuración del entorno de [desarrollo](/help/implementing/developing/introduction/development-guidelines.md) puede depender de varios factores, aunque normalmente se compone de lo siguiente:

* Un sistema de desarrollo integrado con control de versiones para proporcionar una base de código integrada. Esta base de código integrada se utiliza para combinar y consolidar código de los entornos de desarrollo individuales utilizados por cada desarrollador.
* Un entorno personal para cada desarrollador que normalmente reside en su equipo local. A intervalos adecuados, el código se sincroniza con el sistema de control de versiones

Según la escala del sistema, el entorno de desarrollo puede tener instancias de creación y publicación.

### Garantía de calidad {#quality-assurance}

El equipo de garantía de la calidad utiliza este entorno para probar exhaustivamente el sistema nuevo; el diseño y la función. Debe tener entornos de creación y de publicación, con contenido adecuado, y proporcionar todos los servicios necesarios para permitir un conjunto de todas las aplicaciones de pruebas.

### Ensayo {#staging}

El entorno de ensayo debe ser un reflejo del entorno de producción: configuración, código y contenido:

* Se utiliza para probar las secuencias de comandos utilizadas para implementar la implementación real.
* Puede utilizarse para pruebas finales (diseños, funcionalidades e interfaces) antes de implementarse en los entornos de producción.
* Aunque no siempre es posible que el entorno de ensayo sea idéntico al de producción, debería ser lo más parecido posible para permitir las pruebas de carga y rendimiento.

### Producción: creación y publicación {#production-author-and-publish}

El entorno de producción consiste en los entornos que [crean y publican](/help/sites-cloud/authoring/author-publish.md) la implementación.

Un entorno de producción consta de al menos una instancia de autor y una instancia de publicación:

* Instancia [de creación](#author) para la entrada de contenido.
* Una instancia de [publicación](#publish) para el contenido disponible para los visitantes y usuarios.

Según la escala del proyecto, a menudo consta de varios autores, editores o ambos. En un nivel inferior, el repositorio también se puede agrupar en varios casos.

#### Autor {#author}

Las instancias de autor generalmente se encuentran detrás del cortafuegos interno. Este cortafuegos interno es el entorno en el que usted y sus compañeros realizan las siguientes tareas de creación:

* administrar todo el sistema.
* Introducir el contenido.
* Configurar el diseño del contenido.
* Activar el contenido en el entorno de publicación.

El contenido que se activó se empaqueta y se coloca en la cola de replicación del entorno del autor. A continuación, el proceso de replicación transporta ese contenido al entorno de publicación.

Para volver a replicar los datos generados en un entorno de publicación en el entorno de creación, un detector de replicación del entorno de autor sondea el entorno de publicación y recupera dicho contenido del buzón de salida de replicación inversa del entorno de publicación.

#### Publicación {#publish}

Normalmente, un entorno de publicación se encuentra en la “zona desmilitarizada” (DMZ). Es el entorno en el que los visitantes acceden a su contenido (por ejemplo, a través de un sitio web o en forma de aplicación móvil) e interactúan con él; ya sea público o dentro de la intranet. El entorno de publicación:

* contiene el contenido replicado desde el entorno de creación.
* Pone ese contenido a disposición de los visitantes.
* Almacena los datos de usuario generados por sus visitantes, como comentarios u otros envíos de formularios.
* Puede configurarse para añadir esos datos de usuario a una bandeja de salida, para la replicación inversa de vuelta al entorno de creación.

El entorno de publicación genera el contenido dinámicamente en tiempo real y se puede personalizar para cada usuario.

## Movimiento de código {#code-movement}

Propagar siempre el código de abajo a arriba:

* el código se desarrolla inicialmente en el entorno de desarrollo local y luego en el entorno de desarrollo integrado
* seguido de pruebas exhaustivas en los entornos de control de calidad
* A continuación, se vuelve a probar en los entornos de ensayo.
* Solo entonces debe implementarse el código en los entornos de producción.

Normalmente, el código (por ejemplo, las plantillas de diseño y la funcionalidad de la aplicación web personalizadas) se transfiere normalmente por medio de la exportación e importación de paquetes entre los distintos repositorios de contenido. Cuando es significativa, esta replicación puede configurarse como un proceso automático.

Los proyectos en AEM as a Cloud Service suelen desencadenar la implementación de código.

* Automáticamente: para su transferencia a los entornos de desarrollo y control de calidad.
* Manualmente: las implementaciones en los entornos de ensayo y producción se realizan de manera más controlada, a menudo manual; aunque la automatización es posible si es necesario.

![Movimiento de código](assets/code-movement.png)

## Movimiento de contenido  {#content-movement}

El contenido que se esté creando para la producción **siempre** se debe crear en la instancia de creación de producción.

El contenido no debe seguir el código que se desplaza de entornos inferiores a otros superiores. Es decir, no es recomendable hacer que los autores creen contenido en equipos locales o entornos más bajos y, a continuación, moverlo al entorno de producción. La razón es que puede introducir errores e inconsistencias.

El contenido de producción debe trasladarse del entorno de producción al entorno de ensayo para garantizar que el entorno de ensayo proporcione un entorno de prueba eficaz y preciso.

>[!NOTE]
>
>Esto no significa que el contenido de ensayo tenga que sincronizarse continuamente con la producción; las actualizaciones regulares son suficientes, pero especialmente antes de probar una nueva iteración de código. No es necesario actualizar el contenido en los entornos de control de calidad y desarrollo con tanta frecuencia. Solo debe ser una buena representación del contenido de producción.

El contenido puede transferir lo siguiente:

* Entre los distintos entornos, mediante la exportación e importación de paquetes.
* Entre diferentes instancias: replicando directamente (replicación de AEM as a Cloud Service) el contenido (mediante una conexión HTTP o HTTPS).

![Movimiento de contenido](assets/content-movement.png)
