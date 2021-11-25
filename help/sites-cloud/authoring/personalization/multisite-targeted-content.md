---
title: Uso del contenido de destino de varios sitios
description: Si necesita administrar el contenido de destino, como actividades, experiencias y ofertas entre sus sitios, puede aprovechar la compatibilidad multisitio integrada de AEM, para el contenido de destino.
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
source-git-commit: 7dd3a658a88cae98732820ab92da0d27d21beb6f
workflow-type: tm+mt
source-wordcount: '2893'
ht-degree: 88%

---

# Uso del contenido de destino de varios sitios {#working-with-targeted-content-in-multisites}

Si necesita administrar el contenido de destino, como actividades, experiencias y ofertas entre sus sitios, puede aprovechar la compatibilidad multisitio integrada de AEM, para el contenido de destino.

>[!NOTE]
>
>El trabajo con la compatibilidad multisitio para el contenido de destino es una característica avanzada. Para utilizar esta característica, debe estar familiarizado con el [Administrador de varios sitios](/help/sites-cloud/administering/msm/overview.md) y la [integración de Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) con AEM.

En este documento se describe lo siguiente:

* Proporciona información general breve de la compatibilidad multisitio de AEM, para el contenido de destino.
* Describe algunas situaciones en las que se indica cómo se pueden vincular sitios (en una marca).
* Proporciona una guía detallada de ejemplo sobre cómo los especialistas en marketing pueden usar esta característica.
* Instrucciones detalladas sobre cómo implementar la compatibilidad multisitio del contenido de destino.

Para configurar la forma en que los sitios comparten el contenido personalizado, debe realizar los pasos siguientes:

1. [Cree una nueva área](#creating-new-areas) o [cree una nueva área como Live Copy](#creating-new-areas). Un área incluye todas las actividades disponibles para *un área* de la página; es decir, la ubicación de la página donde se indica el componente. Al crear un área nueva, se crea otra área vacía; si crea un área como Live Copy podrá heredar contenido entre las estructuras del sitio.

1. [Vincular el sitio o la página](#linking-sites-to-an-area) a un área.

Puede suspender o restaurar en cualquier momento la herencia. Además, si no desea suspender la herencia, también puede crear experiencias locales. De forma predeterminada, todas las páginas usan el área principal, a menos que se especifique lo contrario.

## Introducción a la compatibilidad multisitio del contenido de destino {#introduction-to-multisite-support-for-targeted-content}

La compatibilidad multisitio del contenido de destino ya está disponible y le permite enviar contenido de destino desde la página maestra que administra a través de MSM a una local de tipo Live Copy, o le permite administrar modificaciones globales y locales de dicho contenido.

Administre esto en un **Área**. Las áreas separan el contenido de destino (actividades, experiencias y ofertas) que se usa en diferentes sitios y proporcionan un mecanismo basado en MSM para crear y administrar la herencia del contenido de destino junto a la herencia del sitio. Esto evita que tenga que volver a crear contenido de destino en sitios heredados.

En un área, solo las actividades vinculadas a ella se añaden a las Live Copies. De forma predeterminada, se selecciona el área principal. Después de crear las áreas adicionales, se pueden vincular a sus sitios o páginas para indicar qué contenido de destino se ha usado.

Un sitio o Live Copy que vincula a un área que contiene las actividades que deben estar disponibles en ese sitio o Live Copy. De forma predeterminada, el sitio o Live Copy se vincula al área principal, pero también puede vincular otras áreas además de las áreas principales.

>[!NOTE]
>
>Recuerde lo siguiente cuando use la compatibilidad multisitio del contenido de destino:
>
>* Cuando utilice lanzamientos o Live Copies, necesitará una licencia MSM.
>* Cuando utilice la función de sincronización a Adobe Target, necesitará una licencia de Adobe Target.

>


## Casos de uso {#use-cases}

Puede configurar la compatibilidad multisitio para el contenido de destino de varias formas, según el caso de uso. En esta sección se describe cómo puede funcionar esta opción, en teoría, con una marca. Además, en [Ejemplo: Contenido de destino según la ubicación geográfica](#example-targeting-content-based-on-geography), puede ver una aplicación real de contenido de destino en varios sitios.

El contenido de destino se agrupa en tales áreas, las cuales definen el ámbito de los sitios o las páginas. Estas áreas se definen en el nivel de la marca. Una marca puede contener varias áreas. Las áreas pueden ser diferentes entre marcas. Si bien una marca solo puede contener el área principal y, por lo tanto, se comparte entre todas las marcas, otra marca puede contener varias marcas (por ejemplo, según la región). Las marcas, por tanto, no necesitan duplicar el conjunto de áreas entre ellas.

Gracias a la compatibilidad multisitio del contenido de destino puede, por ejemplo, tener dos o más sitios con **una** sola marca que consta de lo siguiente:

* Un conjunto de contenido de destino totalmente *distinto*: si edita el contenido de destino en uno no afectará al otro. Los sitios vinculados a áreas diferentes leen y escriben en su propia área configurada. Por ejemplo:
   * El sitio A está vinculado al área X
   * El sitio B está vinculado al área Y
* Un conjunto *compartido* de contenido de destino: editar en uno tiene un impacto directo en ambos sitios; puede configurar esto teniendo dos sitios que se refieren a la misma área. Los sitios vinculados a la misma área comparten el contenido dirigido del área. Por ejemplo:
   * El sitio A está vinculado al área X
   * El sitio B está vinculado al área X
* Un conjunto distinto de contenido de destino *heredado* desde otro sitio a través de MSM: el contenido se puede desplegar unidireccionalmente de una copia maestra a una Live Copy. Por ejemplo:
   * El sitio A está vinculado al área X
   * El sitio B está vinculado al área X (que es una Live Copy del área X)

Asimismo, también puede tener **varias** marcas para usarlas en un sitio, aunque esto puede ser más complejo que este ejemplo.

![Ejemplo de varios sitios](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Para obtener más información técnica sobre esta función, consulte [Cómo se estructura la administración de diversos sitios para el contenido de destino](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Ejemplo: segmentación del contenido según el área geográfica {#example-targeting-content-based-on-geography}

Al utilizar varios sitios para el contenido de destino, puede compartir, mostrar o aislar el contenido de personalización. Para ilustrar mejor cómo se usa esta característica, puede plantearse un escenario en el que desee controlar la manera de implementar el contenido de destino según la geografía, tal como se muestra en el siguiente escenario:

Existen cuatro versiones del mismo sitio en función del área geográfica:

* El sitio **Estados Unidos** está en la esquina superior izquierda y es el sitio principal. En este ejemplo, se abre en el modo Segmentación.
* Las otras tres versiones de este sitio son **Canadá**, **Reino Unido** y **Australia**, que son todas Live Copies. Estos sitios están abiertos en el modo de vista previa.

![Versiones de varios sitios](/help/sites-cloud/authoring/assets/multisite-versions.png)

Cada sitio comparte el contenido personalizado en zonas geográficas:

* Canadá comparte el área principal con los Estados Unidos.
* La buena Gran Bretaña está vinculada a la zona europea y hereda de la zona principal.
* Australia, porque se encuentra en el hemisferio sur y los productos de temporada no se aplicarían; además, tiene su propio contenido personalizado.

![Diagrama de varios sitios](/help/sites-cloud/authoring/assets/multisite-diagram.png)

Para el hemisferio norte, contamos con una actividad de invierno que se creó para una audiencia masculina, pero al vendedor de Norteamérica le gustaría tener una imagen de invierno diferente, por lo que la cambia en el sitio de Estados Unidos.

![Versión de Estados Unidos](/help/sites-cloud/authoring/assets/multisite-us.png)

Después de actualizar la ficha, el sitio canadiense cambia a la nueva imagen sin que deba realizarse ninguna acción más. Realiza esta acción porque comparte el área principal con los Estados Unidos. En los sitios Buenos de Gran Bretaña y Australia, la imagen no cambia.

![Cambio de versiones](/help/sites-cloud/authoring/assets/multisite-us-change.png)

El especialista en marketing quiere aplicar estos cambios en la región europea, y [despliega la Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md); para ello, hace clic o pulsa **Desplegar página**. Después de actualizar la ficha, el sitio de Gran Bretaña tiene la nueva imagen, mientras que el área de Europa la hereda del área principal (tras el lanzamiento).

![Desplegar Live Copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

La imagen del sitio de Australia permanecerá sin cambios, lo cual es el comportamiento deseado, ya que es verano en Australia y especialista en marketing no desea cambiar el contenido. El sitio de Australia no cambia, ya que no comparte un área con ninguna otra región ni es una Live Copy de otra región. El especialista en marketing nunca tendrá que preocuparse de que el contenido de destino del sitio de Australia se sobrescriba.

Además, para Gran Bretaña, cuya área es una Live Copy del área principal, puede ver el estado de la herencia según el indicador de color verde que está junto al nombre de la actividad. Si hereda una actividad, no es posible modificarla a menos que suspenda o desasocie la Live Copy.

Puede suspender en cualquier momento la herencia o desasociarla completamente También puede añadir experiencias locales que solo están disponibles para esa experiencia, sin tener que suspender la herencia.

>[!NOTE]
>
>Para obtener más información técnica sobre esta función, consulte [Cómo se estructura la administración de diversos sitios para el contenido de destino](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Crear una nueva área frente a crear una nueva área como Live Copy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

En AEM, tiene la opción de crear una nueva área o crear nuevas áreas como Live Copy. Crear una nueva área de actividades de grupos y cualquier cosa que pertenezca a dichas actividades como, por ejemplo, ofertas, experiencias, etc. Cree un área nueva cuando quiera crear un conjunto de contenido de destino completamente distinto o cuando quiera compartir un conjunto de contenido de destino.

Sin embargo, si configuró la herencia mediante MSM entre los dos sitios, puede que quiera heredar las actividades. En este caso, se crea una nueva área como una Live Copy, donde Y es una Live Copy de X y, por lo tanto, hereda todas las actividades.

>[!NOTE]
>
>El despliegue predeterminado déclencheur los lanzamientos subsiguientes del contenido de destino siempre que una página sea una Live Copy vinculada a un área que en sí es una Live Copy del área vinculada al modelo Páginas.

Por ejemplo, en el siguiente diagrama, hay cuatro sitios donde dos de ellos comparten el área principal (y todas las actividades que forman parte de esa área), uno que tiene un área que es una Live Copy de un área, por lo que comparte las actividades durante el despliegue, y un sitio que es completamente independiente (y que, por lo tanto, requiere un área para sus actividades).

![Detalles del diagrama](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

Para lograr esto en AEM, haga lo siguiente:

* El sitio A está vinculado al área principal; no es necesario crear ningún área. El área principal está seleccionada de manera predeterminada en AEM. El sitio A y el sitio B comparten actividades, y así sucesivamente.
* El sitio B está vinculado al área principal; no es necesario crear ningún área. El área principal está seleccionada de manera predeterminada en AEM. El sitio A y el sitio B comparten actividades, y así sucesivamente.
* El sitio C está vinculado al área heredada, la cual es una Live Copy del área principal; cree un área como Live Copy en el lugar donde cree una Live Copy basada en el área principal. El área heredada hereda las actividades del área principal una vez realizado el despliegue.
* El sitio D está vinculado a su propia área aislada; cree el área donde creó un área completa sin actividades definidas. El área aislada no compartirá las actividades con ningún otro sitio.

## Crear nuevas áreas {#creating-new-areas}

Las áreas pueden abarcar actividades y ofertas. Una vez que haya creado un área en alguno de ellos (por ejemplo, actividades), también tendrá el área disponible en la otra (por ejemplo, ofertas).

>[!NOTE]
>
>El área predeterminada denominada Área maestra se contrae de forma predeterminada al pulsar o hacer clic en el nombre de una marca **hasta** crear otra área. A continuación, cuando selecciona una marca en la consola **Actividad** u **Ofertas**, llegará a la consola **Área**.

Para crear una nueva área:

1. Vaya a **Personalización** > **Actividades** u **Ofertas** y, a continuación, a su marca.
1. Haga clic o pulse **Crear área**.

   ![Crear área](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Haga clic en el icono **Área** y en **Siguiente**.
1. En el campo **Título**, especifique un nombre para la nueva área. De forma opcional, seleccione etiquetas.
1. Haga clic o pulse **Crear**.

   AEM redirige a la ventana de marca, donde se enumeran las áreas creadas. Si hay otra área además del área principal, puede crear áreas directamente desde la consola de marca.

   ![Crear](/help/sites-cloud/authoring/assets/multisite-create.png)

## Crear áreas como Live Copies {#creating-areas-as-live-copies}

Cree una zona como una Live Copy para heredar el contenido de destino a través las estructuras de sitios.

Para crear un área como una Live Copy:

1. Vaya a **Personalización** > **Actividades** u **Ofertas** y, a continuación, a su marca.
1. Haga clic o pulse **Crear área como Live Copy**.

   ![Crear área como Live Copy](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Seleccione el área de la que desea realizar una Live Copy y haga clic en **Siguiente**.

   ![Crear Live Copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. En el campo **Nombre**, introduzca un nombre para la Live Copy. De forma predeterminada, se incluyen las páginas secundarias; para excluirlas, seleccione la casilla de verificación **Excluir páginas secundarias**.

   ![Crear Live Copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. En el menú desplegable, seleccione **Lanzar configuración** y escoja la configuración adecuada.

   Consulte [Configuración de despliegue instalada](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations) para obtener descripciones acerca de cada opción.

   Consulte [Crear y sincronizar copias de Live Copy](/help/sites-cloud/administering/msm/creating-live-copies.md) para obtener más información sobre copias de Live Copy.

   >[!NOTE]
   >
   >Cuando una página se transforma en una Live Copy y el área configurada de la página modelo resulta ser también el modelo del área configurada para las Live Copy de las páginas, el valor de LiveAction **personalizationContentRollout** activa un elemento subRollout sincrónico, que forma parte de la **configuración de despliegue estándar**.

1. Haga clic o pulse **Crear**.

   AEM redirige a la ventana de marca, donde se enumeran las áreas creadas. Si hay otra área además del área principal, puede crear áreas directamente desde la ventana de marca.

   ![Crear área](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Vincular sitios a un área {#linking-sites-to-an-area}

Puede vincular áreas a las páginas o a un sitio. Las áreas las heredan todas las subpáginas a menos que dichas páginas se superpongan con una asignación en una subpágina. Sin embargo, normalmente se establece el vínculo en el nivel del sitio.

Cuando establezca un vínculo, solo las actividades, experiencias y ofertas del área seleccionada estarán disponibles. De este modo evitará que se mezcle de forma accidental el contenido que se administra por separado. Si no se ha configurado ninguna otra área, se usará el área principal de cada marca.

>[!NOTE]
>
>Las páginas o sitios que hacen referencia a la misma área utilizan la variable *same* conjunto compartido de actividades, experiencias y ofertas. Si edita una actividad, experiencia u oferta que compartan varios sitios, esto afectará a todos los sitios.

Para vincular un sitio a un área:

1. Desplácese al sitio (o página) que desea vincular con un área.
1. Seleccione el sitio o la página y haga clic o pulse **Ver propiedades**.
1. Haga clic o pulse la ficha **Personalización.**
1. En el menú **Marca**, seleccione la marca que desea vincular al área. Después de seleccionar la marca, las áreas estarán disponibles en el menú **Referencia de área**.

   ![Vinculación de sitios](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Seleccione el área del menú desplegable **Referencia de área** y haga clic o pulse **Guardar**.

   ![Referencia de área](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Desasociar Live Copy o suspender la herencia del contenido de destino {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Puede suspender o desasociar la herencia del contenido de destino. La función de suspender o desasociar la Live Copy se realiza según la actividad. Por ejemplo, es posible que quiera personalizar las experiencias de actividad, pero si dicha actividad aún está vinculada a la copia heredada, no es posible modificar la experiencia o las propiedades de la actividades.

La función de suspender la Live Copy rompe temporalmente la herencia, pero podrá volver a restaurar en el futuro. Si desasocia Live Copy, suspenderá permanentemente la herencia.

Suspenda o desasocie la herencia del contenido de destino; para ello, restáurelo en una actividad. Si una página o sitio vincula un área de tipo Live Copy, puede ver el estado de herencia de una actividad.

Una actividad que se hereda de otro sitio aparece en color verde junto al nombre de la actividad. Un legado suspendido se marca en rojo y una actividad creada localmente no tiene ningún icono.

>[!NOTE]
>
>* Solo se pueden suspender o desasociar Live Copies en una actividad.
>* No es necesario suspender o desasociar Live Copies para expandir una actividad heredada. También puede crear **nuevas** experiencias y ofertas locales para dicha actividad. Si desea modificar una actividad existente, deberá suspender la herencia.

>


### Suspender la herencia {#suspending-inheritance}

Para suspender o desasociar la herencia del contenido de destino en una actividad:

1. Desplácese a la página donde desee separar o suspender la herencia y haga clic o pulse el modo **Segmentación** en el menú desplegable.
1. Si la página está vinculada a un área que es una Live Copy, verá el estado de la herencia. Haga clic o pulse **Iniciar segmentación**.
1. Para suspender una actividad, realice una de las acciones siguientes:

   1. Seleccione un elemento de la actividad, como la audiencia. AEM muestra automáticamente la casilla de confirmación Suspender Live Copy. (Puede suspender Live Copy si pulsa o hacer clic en cualquier elemento durante el proceso de establecimiento de objetivos).
   1. Seleccione **Suspender Live Copy** en el menú desplegable de la barra de herramientas.

   ![Suspender Live Copy](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Toque o haga clic **Suspender** para suspender la actividad. Las actividades suspendidas están marcadas en rojo.

   ![Copia activa suspendida](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### División de herencia {#breaking-inheritance}

Para cancelar la herencia del contenido de destino en una actividad:

1. Desplácese a la página donde desee separar la Live Copy de la copia principal y haga clic o pulse el modo **Segmentación** en el menú desplegable.
1. Si la página está vinculada a un área que es una Live Copy, verá el estado de la herencia. Haga clic o pulse **Iniciar segmentación**.
1. Seleccione **Separar Live Copy** en el menú desplegable de la barra de herramientas. AEM confirma que desea separar la Live Copy.
1. Haga clic o pulse **Desasociar** para separar la Live Copy de la actividad. Después de quitarla, el menú desplegable de la herencia deja de visualizarse. La actividad es ahora una actividad local.

   ![Actividad local](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Restaurar la herencia del contenido de destino {#restoring-inheritance-of-targeted-content}

Si suspendió la herencia del contenido de destino en una actividad, puede restaurarla en cualquier momento. Sin embargo, si ha desasociado la Live Copy, no se puede restaurar la herencia.

Para restaurar la herencia del contenido de destino en una actividad:

1. Vaya a la página donde desee restaurar la herencia y toque o haga clic en **Segmentación** en el menú desplegable de modo .
1. Haga clic o pulse **Iniciar segmentación**.
1. Seleccione **Reanudar Live Copy** en el menú desplegable de la barra de herramientas.

   ![Reanudar Live Copy](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Haga clic o pulse **Reanudar** para confirmar que desea reanudar la herencia de Live Copy. Si se reanuda la herencia, se pierden las modificaciones realizadas en la actividad actual.

## Eliminar áreas {#deleting-areas}

Cuando elimine un área, deberá eliminar todas las actividades de la misma. AEM le advierte antes de poder eliminar un área. Si elimina un área a la que está vinculado un sitio, la asignación para esta marca se reasignará automáticamente al área principal.

Para eliminar un área:

1. Vaya a **Personalización** > **Actividades** o **Ofertas** y luego su marca.
1. Haga clic o pulse el icono que está al lado del área que desee eliminar.
1. Haga clic o pulse **Eliminar** y confirme que desea eliminar el área.
