---
title: Operaciones de desarrollo empresarial
description: Obtenga información sobre los procesos, métodos y comunicaciones necesarios para facilitar la implementación y simplificar la colaboración.
translation-type: tm+mt
source-git-commit: 5fe4eb9f9cad4ad2f1d259ebb5fa0302ea5c515f
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# Operaciones de desarrollo empresarial{#enterprise-devops}

DevOps abarca los procesos, métodos y comunicaciones necesarios para:

* Facilite la implementación de su software en los distintos entornos.
* Simplifique la colaboración entre los equipos de desarrollo, prueba e implementación.

DevOps tiene como objetivo evitar problemas como:

* Errores manuales.
* Elementos olvidados; por ejemplo, archivos, detalles de configuración.
* Discrepancias; por ejemplo, entre el entorno local de un desarrollador y otros entornos.

## Entornos {#environments}

Adobe Experience Manager (AEM) como servicio de nube suele constar de varios entornos, utilizados para diferentes propósitos en diferentes niveles:

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

Los desarrolladores son responsables de desarrollar y personalizar el proyecto propuesto (ya sea sitio web, aplicaciones móviles, implementación de DAM, etc.), con toda la funcionalidad requerida. Estos procedimientos:

* desarrollar y personalizar los elementos necesarios; por ejemplo, plantillas, componentes, flujos de trabajo, aplicaciones
* realizar el diseño
* desarrollar los servicios y secuencias de comandos necesarios para implementar la funcionalidad requerida

La configuración del entorno de [desarrollo](/help/implementing/developing/introduction/development-guidelines.md) puede depender de diversos factores, aunque suele estar compuesta de:

* Un sistema de desarrollo integrado con control de versiones para proporcionar una base de código integrada. Se utiliza para combinar y consolidar código de los entornos de desarrollo individuales utilizados por cada desarrollador.
* Un entorno personal para cada desarrollador; normalmente residen en su equipo local. A intervalos adecuados, el código se sincroniza con el sistema de control de versiones

Según la escala del sistema, el entorno de desarrollo puede tener instancias de creación y publicación.

### Garantía de calidad {#quality-assurance}

Este entorno es utilizado por el equipo de garantía de la calidad para probar exhaustivamente su nuevo sistema; diseño y función. Debe tener entornos de creación y publicación, con contenido adecuado, y proporcionar todos los servicios necesarios para permitir un conjunto completo de pruebas.

### Ensayo {#staging}

El entorno de ensayo debe ser un reflejo del entorno de producción: configuración, código y contenido:

* Se utiliza para probar las secuencias de comandos utilizadas para implementar la implementación real.
* Puede utilizarse para pruebas finales (diseño, funcionalidad e interfaces) antes de implementarse en los entornos de producción.
* Aunque no siempre es posible tener el entorno de ensayo idéntico al entorno de producción, debe estar lo más cerca posible de habilitar las pruebas de rendimiento y carga.

### Producción: creación y publicación {#production-author-and-publish}

El entorno de producción consiste en los entornos necesarios para [crear y publicar](/help/sites-cloud/authoring/getting-started/concepts.md) realmente la implementación.

Un entorno de producción consta de al menos una instancia de autor y una instancia de publicación:

* Instancia de [creación](#author) para la entrada de contenido.
* Una instancia de [publicación](#publish) para el contenido que está disponible para los visitantes y usuarios.

Según la escala del proyecto, a menudo consta de varias instancias de autor y/o publicación. En un nivel inferior, el repositorio también se puede agrupar en varios casos.

#### Autor {#author}

Las instancias de autor generalmente se encuentran detrás del servidor de seguridad interno. Este es el entorno en el que usted y sus colegas realizarán tareas de creación, como:

* administrar todo el sistema
* introducir el contenido
* configurar el diseño y el diseño del contenido
* activar el contenido en el entorno de publicación

El contenido que se activó se empaqueta y se coloca en la cola de replicación del entorno del autor. A continuación, el proceso de replicación transporta ese contenido al entorno de publicación.

Para volver a replicar los datos generados en un entorno de publicación en el entorno de creación, un detector de replicación del entorno de autor sondeará el entorno de publicación y recuperará dicho contenido del buzón de salida de replicación inversa del entorno de publicación.

#### Publicación {#publish}

Normalmente, un entorno de publicación se encuentra en la zona desmilitarizada (DMZ). Este es el entorno en el que los visitantes accederán a su contenido (por ejemplo, a través de un sitio web o en forma de aplicación móvil) e interactuarán con él; ya sea pública o dentro de la intranet. Un entorno de publicación:

* contiene el contenido replicado desde el entorno de creación
* pone ese contenido a disposición de los visitantes
* almacena datos de usuario generados por sus visitantes, como comentarios u otros envíos de formularios
* puede configurarse para agregar esos datos de usuario a una bandeja de salida, para la replicación inversa de vuelta al entorno de creación

El entorno de publicación genera el contenido dinámicamente en tiempo real y el contenido se puede personalizar para cada usuario individual.

## Movimiento de código {#code-movement}

El código siempre debe propagarse de abajo a arriba:

* el código se desarrolla inicialmente en los entornos de desarrollo locales y luego integrados
* seguido de pruebas exhaustivas sobre los entornos de control de calidad
* a continuación, vuelva a probarse en los entornos de ensayo
* sólo entonces debe implementarse el código en los entornos de producción

El código (por ejemplo, las plantillas de diseño y la funcionalidad personalizada de la aplicación Web) se transfiere generalmente mediante la exportación e importación de paquetes entre los distintos repositorios de contenido. Cuando es significativa, esta replicación puede configurarse como un proceso automático.

Los proyectos de AEM como servicio de nube suelen activar la implementación de código:

* Automáticamente: para su transferencia a los entornos de desarrollo y control de calidad.
* Manualmente: los despliegues en los entornos de ensayo y producción se realizan de manera más controlada, a menudo manual; aunque la automatización es posible si es necesario.

![Movimiento de código](assets/code-movement.png)

## Movimiento de contenido {#content-movement}

El contenido que se esté creando para la producción **siempre** se debe crear en la instancia de creación de producción.

El contenido no debe seguir el movimiento del código de entornos inferiores a los superiores, ya que hacer que los autores creen contenido en máquinas locales o entornos inferiores y luego moverlo al entorno de producción no es una buena práctica y es probable que introduzca errores e incoherencias.

El contenido de producción debe trasladarse del entorno de producción al entorno de ensayo para garantizar que el entorno de ensayo proporcione un entorno de prueba eficaz y preciso.

>[!NOTE]
>
>Esto no significa que el contenido de ensayo tenga que sincronizarse continuamente con la producción; las actualizaciones regulares son suficientes, pero especialmente antes de probar una nueva iteración de código. El contenido del control de calidad y los entornos de desarrollo no necesitan actualizarse con tanta frecuencia, solo debe ser una buena representación del contenido de producción.

El contenido se puede transferir:

* Entre los distintos entornos: mediante la exportación e importación de paquetes.
* Entre diferentes instancias: replicando directamente (AEM como una replicación de servicio de nube) el contenido (mediante una conexión HTTP o HTTPS).

![Movimiento de contenido](assets/content-movement.png)