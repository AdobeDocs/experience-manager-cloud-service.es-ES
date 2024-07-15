---
title: Uso del contenido de destino de varios sitios
description: Si necesita administrar contenido de destino, como actividades, experiencias y ofertas, entre sus sitios, puede aprovechar el soporte integrado con varios sitios para el contenido de destino
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '2844'
ht-degree: 89%

---

# Uso del contenido de destino de varios sitios {#working-with-targeted-content-in-multisites}

Si necesita administrar contenido de destino, como actividades, experiencias y ofertas, entre sus sitios, puede aprovechar el soporte integrado con varios sitios de AEM para el contenido de destino.

>[!NOTE]
>
>El trabajo con la compatibilidad con varios sitios para el contenido de destino es una característica avanzada. Para utilizar esta característica, debe estar familiarizado con el [Administrador de varios sitios](/help/sites-cloud/administering/msm/overview.md) y la [integración de Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) con AEM.

Este documento describe lo siguiente:

* Proporciona información general breve de la compatibilidad con varios sitios de AEM para el contenido segmentado.
* Describe algunos escenarios de uso posibles sobre cómo vincular sitios (en una marca).
* Proporciona una guía detallada de ejemplo sobre cómo los especialistas en marketing pueden usar esta característica.
* Instrucciones detalladas sobre cómo implementar la compatibilidad con varios sitios para el contenido de destino.

Para configurar cómo sus sitios comparten contenido personalizado, debe realizar los pasos siguientes:

1. [Crear un área nueva](#creating-new-areas) o [crear un área como Live Copy](#creating-new-areas). Un área incluye todas las actividades disponibles para un *área* de la página; es decir, la ubicación en la página a la que se dirige el componente. La creación de una nueva área crea una área vacía, mientras que la creación de una área como Live Copy permite heredar el contenido en las estructuras del sitio.

1. [Vincular el sitio o la página](#linking-sites-to-an-area) a un área.

En cualquier momento puede suspender o restaurar la herencia. Además, si no desea suspender la herencia, también puede crear experiencias locales. De forma predeterminada, todas las páginas utilizan el área principal a menos que se especifique lo contrario.

## Introducción a la compatibilidad con varios sitios para contenido de destino {#introduction-to-multisite-support-for-targeted-content}

La compatibilidad con varios sitios para el contenido del destino está disponible de forma predeterminada y le permite insertar contenido de destino desde la página maestra que administra mediante MSM en una Live Copy local o administrar las modificaciones globales y locales de dicho contenido.

Esto se administra en un **Área**. Las áreas separan el contenido de destino (actividades, experiencias y ofertas) que se usa en diferentes sitios y proporcionan un mecanismo basado en MSM para crear y administrar la herencia del contenido de destino junto a la herencia del sitio. Esto evita que tenga que volver a crear contenido de destino en sitios heredados.

En un área, solo las actividades vinculadas a ella se insertan en Live Copies. De forma predeterminada, el Área principal está seleccionada. Después de crear áreas adicionales, puede vincularlas a sus sitios o páginas para indicar qué contenido de destino se inserta.

Un sitio o Live Copy vincula un área que contiene las actividades que deben estar disponibles en ese sitio o Live Copy. De forma predeterminada, el sitio o Live Copy está vinculado al área principal, pero se pueden vincular otras áreas además de la principal.

>[!NOTE]
>
>Recuerde lo siguiente cuando utilice el soporte de varios sitios para el contenido de destino:
>
>* Cuando se utilizan despliegues o Live Copies, se requiere una licencia de MSM.
>* Cuando se utiliza la sincronización con Adobe Target, se requiere una licencia de Adobe Target.
>

## Casos de uso {#use-cases}

Puede configurar la compatibilidad de varios sitios para el contenido de destino de varias formas, según el caso de uso. En esta sección se describe cómo puede funcionar esta opción, en teoría, con una marca. Además, en [Ejemplo: segmentación de contenido basado en áreas geográficas](#example-targeting-content-based-on-geography), puede ver una aplicación real de segmentación de contenido en varios sitios.

El contenido de destino se agrupa en las denominadas áreas, que definen el ámbito de los sitios o las páginas. Estas áreas se definen en el nivel de la marca. Una marca puede contener varias áreas. Las áreas pueden ser diferentes entre marcas. Si bien una marca solo puede contener el área principal y, por lo tanto, se comparte entre todas las marcas, otra marca puede contener varias marcas (por ejemplo, según la región). Por lo tanto, las marcas no necesitan reflejar el conjunto de áreas entre ellas.

Gracias a la compatibilidad con varios sitios del contenido de destino puede, por ejemplo, tener dos o más sitios con **una** sola marca que consta de lo siguiente:

* Un conjunto de contenido de destino totalmente *distinto*: si edita el contenido de destino en uno no afectará al otro. Los sitios vinculados a áreas diferentes leen y escriben en su propia área configurada. Por ejemplo:
   * El sitio A está vinculado al área X
   * El sitio B está vinculado al área Y
* Un conjunto *compartido* de contenido de destino: editar en uno tiene un impacto directo en ambos sitios; puede configurar esto teniendo dos sitios que se refieren a la misma área. Los sitios vinculados a la misma área comparten el contenido dirigido del área. Por ejemplo:
   * El sitio A está vinculado al área X
   * El sitio B está vinculado al área X
* Un conjunto distinto de contenido de destino *heredado* de otro sitio mediante MSM: el contenido se puede trasladar unidireccionalmente desde una copia maestra a una Live Copy. Por ejemplo:
   * El sitio A está vinculado al área X
   * El sitio B está vinculado al área Y (que es una Live Copy del área X)

También podría tener **varias** marcas que se utilizan en un sitio, lo que podría ser más complejo que este ejemplo.

![Ejemplo del uso de varios sitios](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Para obtener información más técnica sobre esta característica, consulte [Cómo se estructura el sistema de administración de varios sitios para el contenido de destino](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Ejemplo: segmentación de contenido según el área geográfica {#example-targeting-content-based-on-geography}

El uso de varios sitios para el contenido de destino le permite compartir, desplegar o aislar contenido de personalización. Para ilustrar mejor cómo se utiliza esta función, puede plantearse un escenario en el que desee controlar la manera de implementar el contenido de destino en función del área geográfica, tal como se muestra en el siguiente escenario:

Existen cuatro versiones del mismo sitio en función del área geográfica:

* El sitio **Estados Unidos** se encuentra en el ángulo superior izquierdo y es el sitio principal. En este ejemplo, está abierto en el modo de segmentación.
* Las otras tres versiones de este sitio son **Canadá**, **Gran Bretaña** y **Australia**, que son todas Live Copies. Estos sitios se abren en el modo de vista previa.

![Versiones de varios sitios](/help/sites-cloud/authoring/assets/multisite-versions.png)

Cada sitio comparte contenido personalizado en regiones geográficas:

* Canadá comparte el área principal con los Estados Unidos.
* Gran Bretaña se vincula al área europea y hereda del área principal.
* Australia, porque se encuentra en el hemisferio sur y los productos de temporada no se aplicarían; además, tiene su propio contenido personalizado.

![Diagrama de varios sitios](/help/sites-cloud/authoring/assets/multisite-diagram.png)

Para el hemisferio norte, contamos con una actividad de invierno que se creó para una audiencia masculina, pero al vendedor de Norteamérica le gustaría tener una imagen de invierno diferente, por lo que la cambia en el sitio de los Estados Unidos.

![Versión de los Estados Unidos](/help/sites-cloud/authoring/assets/multisite-us.png)

Después de actualizar la pestaña, el sitio de Canadá cambia a la nueva imagen sin que deba realizarse ninguna acción por nuestra parte. Lo hace porque comparte el área principal con los Estados Unidos. En los sitios de Gran Bretaña y Australia, la imagen no cambia.

![Cambio de versiones](/help/sites-cloud/authoring/assets/multisite-us-change.png)

El experto en marketing desea implementar estos cambios en la región europea y [despliega la Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md) pulsando o haciendo clic en **Desplegar página**. Después de actualizar la pestaña, el sitio de Gran Bretaña contiene la nueva imagen, ya que el área de Europa hereda del área principal (después del despliegue).

![Desplegar Live Copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

La imagen del sitio de Australia permanece sin cambios, que es el comportamiento deseado, ya que es verano en Australia y el experto en marketing no desea cambiar ese contenido. El sitio de Australia no cambia porque no comparte un área con ninguna otra región ni es una Live Copy de otra región. El experto en marketing nunca tendrá preocuparse de que el contenido de destino del sitio de Australia se sobrescriba.

Además, para Gran Bretaña, cuyo área es una Live Copy del área principal, puede ver el estado de la herencia mediante el indicador verde que está junto al nombre de la actividad. Si se hereda una actividad, no puede modificarla a menos que suspenda o desasocie la Live Copy.

En cualquier momento, puede suspender la herencia o desasociar la herencia por completo. También puede añadir siempre experiencias locales que solo estén disponibles para esa experiencia sin suspender la herencia.

>[!NOTE]
>
>Para obtener información más técnica sobre esta característica, consulte [Cómo se estructura el sistema de administración de varios sitios para el contenido de destino](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Creación de una nueva área frente a la creación de una nueva como Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

En AEM, tiene la opción de crear una área nueva o crear una área nueva como Live Copy. Crear una nueva área agrupa actividades y todo lo que pertenezca a esas actividades, como ofertas, experiencias, etc. Puede crear un área cuando desee crear un conjunto de contenido de destino completamente distinto o cuando desee compartir un conjunto de contenido de destino.

Sin embargo, si ha configurado la herencia mediante MSM entre los dos sitios, puede que desee heredar las actividades. En este caso, se crea un área como Live Copy, donde Y es una Live Copy de X y, por lo tanto, hereda también todas las actividades.

>[!NOTE]
>
>La opción predeterminada de despliegue activa las opciones de despliegue siguientes que estén relacionadas con el contenido de destino, siempre que una página sea una Live Copy vinculada a un área que también sea una Live Copy del área vinculada al modelo Páginas.

Por ejemplo, en el siguiente diagrama, hay cuatro sitios donde dos de ellos comparten el área principal (y todas las actividades que forman parte de esa área), uno que tiene un área que es una Live Copy, por lo que comparte las actividades durante el despliegue, y un sitio que es completamente independiente (y que, por lo tanto, requiere un área para sus actividades).

![Detalles del diagrama](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

Para lograr esto en AEM, haga lo siguiente:

* El sitio A está vinculado al área principal; no es necesario crear ningún área. El área principal está seleccionada de manera predeterminada en AEM. El sitio A y el sitio B comparten actividades, y así sucesivamente.
* El sitio B está vinculado al área principal; no es necesario crear ningún área. El área principal está seleccionada de manera predeterminada en AEM. El sitio A y el sitio B comparten actividades, y así sucesivamente.
* El sitio C está vinculado al área heredada, que es una Live Copy del área principal; cree un área como Live Copy en el lugar donde cree una Live Copy basada en el área principal. El área heredada hereda las actividades del área principal durante el despliegue.
* El sitio D está vinculado a su propia área aislada; cree el área donde creó un área completa sin actividades definidas. El área aislada no compartirá actividades con ningún otro sitio.

## Creación de nuevas áreas {#creating-new-areas}

Las áreas pueden abarcar actividades y ofertas. Después de crear un área en alguno de ellos (por ejemplo, actividades), también tiene el área disponible en la otra (por ejemplo, ofertas).

>[!NOTE]
>
>El área predeterminada denominada Área maestra se contrae de forma predeterminada al seleccionar el nombre de una marca **hasta** que cree otra área. A continuación, cuando selecciona una marca en la consola **Actividad** u **Ofertas**, llegará a la consola **Área**.

Para crear un área:

1. Vaya a **Personalización** > **Actividades** u **Ofertas** y, a continuación, a su marca.
1. Seleccione **Crear área**.

   ![Crear área](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Haga clic en el icono **Área** y en **Siguiente**.
1. En el campo **Título**, especifique un nombre para la nueva área. Si lo desea, seleccione etiquetas.
1. Seleccione **Crear**.

   AEM redirige a la ventana de la marca, donde enumera las áreas creadas. Si hay otra área además del área principal, puede crear áreas directamente en la consola de marca.

   ![Crear](/help/sites-cloud/authoring/assets/multisite-create.png)

## Creación de áreas como Live Copies {#creating-areas-as-live-copies}

Cree una zona como una Live Copy para heredar el contenido de destino a través las estructuras de sitios.

Para crear un área como una Live Copy, haga lo siguiente:

1. Vaya a **Personalización** > **Actividades** u **Ofertas** y, a continuación, a su marca.
1. Seleccione **Crear área como Live Copy**.

   ![Crear área como Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Seleccione el área de la que desea realizar una Live Copy y haga clic en **Siguiente**.

   ![Crear Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. En el campo **Nombre**, introduzca un nombre para la Live Copy. De forma predeterminada, se incluyen las páginas secundarias; para excluirlas, seleccione la casilla de verificación **Excluir páginas secundarias**.

   ![Crear Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. En el menú desplegable, seleccione **Configuraciones de despliegue** y elija la configuración adecuada.

   Consulte [Configuraciones de despliegue instaladas](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations) para obtener las descripciones de cada opción.

   Consulte [Creación y sincronización de Live Copies](/help/sites-cloud/administering/msm/creating-live-copies.md) para obtener más información sobre Live Copies.

   >[!NOTE]
   >
   >Cuando una página se transforma en una Live Copy y el área configurada de la página modelo resulta ser también el modelo del área configurada para las Live Copy de las páginas, el valor de LiveAction **personalizationContentRollout** activa un elemento subRollout sincrónico, que forma parte de la **configuración de despliegue estándar**.

1. Seleccione **Crear**.

   AEM redirige a la ventana de la marca, donde enumera las áreas creadas. Si hay otra área además del área principal, puede crear áreas directamente desde la ventana de marca.

   ![Crear área](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Vincular sitios a un área {#linking-sites-to-an-area}

Puede vincular áreas a cualquiera de las páginas o a un sitio. Todas las subpáginas heredan las áreas, a no ser que dichas páginas se superpongan debido a una asignación en una subpágina. Sin embargo, normalmente se establece el vínculo en el nivel del sitio.

Al vincular, solo están disponibles las actividades, experiencias y ofertas del área seleccionada. Esto evita mezclar accidentalmente el contenido administrado de forma independiente. Si no se ha configurado otra área, se usa la principal de cada marca.

>[!NOTE]
>
>Las páginas o los sitios que hacen referencia a la misma área utilizan el *mismo* conjunto compartido de actividades, experiencias y ofertas. Si edita una actividad, experiencia u oferta que compartan varios sitios, esto afectará a todos los sitios.

Para vincular un sitio a un área:

1. Desplácese hasta el sitio (o página) que desee vincular a un área.
1. Seleccione el sitio o la página y seleccione **Ver propiedades**.
1. Seleccione la ficha **Personalization**.
1. En el menú **Marca**, seleccione la marca que desea vincular al área. Después de seleccionar la marca, las áreas están disponibles en el menú **Referencia de área**.

   ![Vinculación de sitios](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Seleccione el área del menú desplegable **Referencia de área** y seleccione **Guardar**.

   ![Referencia del área](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Desasociar una Live Copy o suspender la herencia del contenido de destino {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Puede que desee suspender o desasociar la herencia del contenido de destino. Suspender o desasociar la Live Copy se realiza según la actividad. Por ejemplo, es posible que desee modificar las experiencias de la actividad, pero si dicha actividad sigue vinculada a una copia heredada, no puede modificar la experiencia ni ninguna de las propiedades de la actividad.

La suspensión de la Live Copy interrumpe temporalmente la herencia, pero en el futuro puede restaurarla. Al desasociar la Live Copy, se interrumpe la herencia de forma permanente.

Suspenda o desasocie la herencia del contenido de destino; para ello, restáurelo en una actividad. Si una página o sitio vincula un área de tipo Live Copy, puede ver el estado de herencia de una actividad.

Una actividad que se hereda de otro sitio aparece en verde junto al nombre de la actividad. Una herencia suspendida se marca en rojo y una actividad creada localmente no tiene icono.

>[!NOTE]
>
>* Solo puede suspender o desasociar Live Copies en una actividad.
>* No es necesario suspender ni desasociar Live Copies para ampliar una actividad heredada. También puede crear **nuevas** experiencias y ofertas locales para dicha actividad. Si desea modificar una actividad existente, debe suspender la herencia.
>

### Suspender la herencia {#suspending-inheritance}

Para suspender o desasociar la herencia del contenido de destino en una actividad:

1. Vaya a la página en la que desea desasociar o suspender la herencia y seleccione **Segmentación** en el menú desplegable de modo.
1. Si la página está vinculada a un área que es una Live Copy, se ve el estado de la herencia. Seleccione **Iniciar segmentación**.
1. Para suspender una actividad, siga uno de estos procedimientos:

   1. Seleccione un elemento de la actividad, como el público. AEM muestra automáticamente el cuadro de diálogo de confirmación Suspender Live Copy. (Puede suspender Live Copy pulsando o haciendo clic en cualquier elemento durante el proceso de Segmentación).
   1. Seleccione **Suspender Live Copy** en el menú desplegable de la barra de herramientas.

   ![Suspender Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Seleccione **Suspender** para suspender la actividad. Las actividades suspendidas están marcadas en rojo.

   ![Live Copy suspendida](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Interrumpir la herencia {#breaking-inheritance}

Para interrumpir la herencia del contenido de destino en una actividad:

1. Vaya a la página en la que desee desasociar la Live Copy del patrón y seleccione **Segmentación** en el menú desplegable de modo.
1. Si la página está vinculada a un área que es una Live Copy, se ve el estado de la herencia. Seleccione **Iniciar segmentación**.
1. Seleccione **Separar Live Copy** en el menú desplegable de la barra de herramientas. AEM confirma que desea separar la Live Copy.
1. Seleccione **Desasociar** para desasociar la Live Copy de la actividad. Una vez desvinculada, ya no se muestra el menú desplegable de la herencia. La actividad es ahora una actividad local.

   ![Actividad local](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Restauración de la herencia del contenido de destino {#restoring-inheritance-of-targeted-content}

Si ha suspendido la herencia del contenido de destino en una actividad, puede restaurarla en cualquier momento. Sin embargo, si ha desvinculado la Live Copy, no podrá restaurar la herencia.

Para restaurar la herencia del contenido de destino de una actividad, haga lo siguiente:

1. Vaya a la página donde desea restaurar la herencia y seleccione **Segmentación** en el menú desplegable del modo.
1. Seleccione **Iniciar segmentación**.
1. Seleccione **Reanudar Live Copy** en el menú desplegable de la barra de herramientas.

   ![Reanudar Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Seleccione **Reanudar** para confirmar que desea reanudar la herencia de Live Copy. Las modificaciones realizadas en la actividad actual se pierden si se reanuda la herencia.

## Eliminación de áreas {#deleting-areas}

Cuando se elimina un área, se eliminan todas las actividades que contiene. AEM le avisa esto antes de que elimine el área. Si se elimina un área que tenga un sitio vinculado, la asignación de esta marca se reasignará automáticamente al área principal.

Para eliminar un área:

1. Desplácese a **Personalización** > **Actividades** o **Ofertas** y luego a su marca.
1. Seleccione el icono situado junto al área que desee eliminar.
1. Seleccione **Eliminar** y confirme que desea eliminar el área.
