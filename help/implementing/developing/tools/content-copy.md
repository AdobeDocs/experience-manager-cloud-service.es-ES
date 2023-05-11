---
title: La herramienta Copia de contenido
description: La herramienta de copia de contenido permite a los usuarios copiar contenido mutable bajo demanda desde sus entornos de producción as a Cloud Service AEM a entornos más bajos con fines de prueba.
source-git-commit: 4a5470ae8fe5a8e7f615009bf5f6b180aee4669b
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 64%

---


# La herramienta Copia de contenido {#content-copy}

La herramienta de copia de contenido permite a los usuarios copiar contenido mutable bajo demanda desde sus entornos de producción as a Cloud Service AEM a entornos más bajos con fines de prueba.

## Introducción {#introduction}

Los datos actuales y reales son valiosos para las pruebas, la validación y la aceptación de usuarios. La herramienta de copia de contenido le permite copiar contenido de un entorno de AEM de producción a un entorno de ensayo, desarrollo o [Entorno de desarrollo rápido (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) entorno para dichas pruebas.

El contenido que se va a copiar se define mediante un conjunto de contenido. Un conjunto de contenido consta de una lista de rutas JCR que contienen el contenido mutable que se copiará de un entorno de servicio de creación de origen a un entorno de servicio de creación de destino dentro del mismo programa de Cloud Manager. Se permiten las siguientes rutas en un conjunto de contenido.

```text
/content
/conf/**/settings/wcm
/conf/**/settings/dam/cfm/models
/conf/**/settings/graphql/persistentQueries
/etc/clientlibs/fd/themes
```

Al copiar contenido, el entorno de origen es la fuente de información.

* Si el contenido se ha modificado en el entorno de destino, se sobrescribirá con el contenido en el origen, si las rutas son las mismas.
* Si las rutas son diferentes, el contenido del origen se combinará con el contenido del destino.

## Permisos {#permissions}

Para utilizar la herramienta de copia de contenido, se necesitan determinados permisos tanto en los entornos de origen como de destino.

| Función de copia de contenido | AEM grupo de administradores | Función Administrador de implementación |
|---|---|---|
| Crear y modificar [conjuntos de contenido](#create-content-set) | Requerido | No necesario |
| Iniciar o cancelar el [proceso de copia de contenido](#copy-content) | Requerido | Requerido |

## Creación de un conjunto de contenido {#create-content-set}

Para poder copiar contenido, debe definirse un conjunto de contenido. Una vez definidos, los conjuntos de contenido se pueden reutilizar para copiar contenido. Siga estos pasos para crear un conjunto de contenido.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Vaya a la página **Conjuntos de contenido** en la pantalla **Entornos**.

1. Pulse o haga clic en el botón **Añadir conjunto de contenido** en la parte superior derecha de la pantalla.

   ![Conjuntos de contenido](assets/content-sets.png)

1. En el **Detalles** del asistente, proporcione un nombre y una descripción para el conjunto de contenido y toque o haga clic en **Continuar**.

   ![Detalles del conjunto de contenido](assets/add-content-set-details.png)

1. En la pestaña **Rutas de contenido** del asistente, especifique las rutas del contenido mutable que se incluirán en el conjunto de contenido.

   1. Introduzca la ruta en el campo **Añadir ruta de inclusión**.
   1. Pulse o haga clic en el botón **Añadir ruta** para agregar la ruta al conjunto de contenido.
   1. Pulse o haga clic de nuevo en el botón **Añadir ruta** cuando sea necesario.
      * Se permiten hasta cincuenta trayectos.

   ![Añadir rutas al conjunto de contenido](assets/add-content-set-paths.png)

1. Si es necesario precisar o restringir el conjunto de contenido, se pueden excluir las subrutas.

   1. En la lista de rutas incluidas, pulse o haga clic en el botón **Añadir subrutas de exclusión** junto a la ruta que debe restringir.
   1. Introduzca la subruta que se excluirá debajo de la ruta seleccionada.
   1. Pulse o haga clic en **Excluir ruta**.
   1. Pulse o haga clic en **Añadir subrutas de exclusión** para agregar rutas adicionales para excluir según sea necesario.
      * Las rutas excluidas deben ser relativas a la ruta incluida.
      * No hay límite en el número de rutas excluidas.

   ![Exclusión de rutas](assets/add-content-set-paths-excluded.png)

1. Si es necesario, puede modificar las rutas especificadas.

   1. Pulse o haga clic en la X situada junto a las subrutas excluidas para eliminarlas.
   1. Pulse o haga clic en el botón de puntos suspensivos situado junto a las rutas para mostrar las opciones **Editar** y **Eliminar**.

   ![Edición de la lista de rutas](assets/add-content-set-excluded-paths.png)

1. Pulse o haga clic en **Crear** para crear el conjunto de contenido.

A partir de ahora, se puede utilizar el conjunto de contenido para copiar contenido entre entornos.

## Edición de un conjunto de contenido {#edit-content-set}

Siga los mismos pasos que para la creación de un paso de contenido. En lugar de pulsar o hacer clic en **Añadir conjunto de contenido**, seleccione un conjunto existente de la consola y seleccione **Editar** en el menú de puntos suspensivos.

![Editar conjunto de contenido](assets/edit-content-set.png)

Tenga en cuenta que, al editar su conjunto de contenido, es posible que tenga que expandir las rutas configuradas para mostrar las subrutas excluidas.

## Copia de contenido {#copy-content}

Una vez creado un conjunto de contenido, puede utilizarlo para copiar contenido. Siga estos pasos para copiar contenido.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Vaya a la página **Conjuntos de contenidos** en la pantalla **Entornos**.

1. Seleccione un conjunto de contenido de la consola y seleccione **Copiar contenido** en el menú de puntos suspensivos.

   ![Copia de contenido](assets/copy-content.png)

   >[!NOTE]
   >
   >Es posible que no se pueda seleccionar un entorno si ocurre lo siguiente:
   >
   >* El usuario no tiene los permisos adecuados.
   >* El entorno tiene una canalización en ejecución o una operación de copia de contenido en curso.
   >* El entorno está hibernando o iniciando.


1. En el diálogo **Copiar contenido**, especifique el origen y el destino de la acción de copia de contenido.

   ![Copia de contenido](assets/copying-content.png)

   * El contenido solo se puede copiar de un entorno superior a un entorno inferior o entre entornos de desarrollo/RDE donde la jerarquía de entornos es la siguiente (de mayor a menor):
      * Producción
      * Ensayo
      * Desarrollo/RDE

1. Si es necesario, también puede elegir **Incluir listas de control de acceso** en el proceso de copia.

1. Pulse o haga clic en **Copiar**.

Se inicia el proceso de copia. El estado del proceso de copia se refleja en la consola del conjunto de contenido seleccionado.

## Actividad de la copia de contenido {#copy-activity}

Puede controlar el estado de los procesos de la copia en la página **Copiar actividad de contenido**.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Vaya a la página **Copiar actividad de contenido** en la pantalla **Entornos**.

![Actividad de la copia de contenido](assets/copy-content-activity.png)

### Estados de la copia de contenido {#statuses}

Una vez que empiece a copiar contenido, el proceso puede tener uno de los siguientes estados.

| Estado | Descripción |
|---|---|
| En curso | La operación de copia de contenido está en curso |
| Error | Error en la operación de copia de contenido |
| Completado | La operación de copia de contenido se ha completado correctamente |
| Cancelado | El usuario cancela una operación de copia de contenido después de iniciarla |

### Cancelación de un proceso de copia {#cancelling}

Si necesita cancelar una operación de copia de contenido después de iniciarla, tiene la opción de cancelarla.

Para ello, en la **Copiar actividad de contenido** seleccione **Cancelar** acción del menú elipsis del proceso de copia iniciado anteriormente.

![Cancelar copia de contenido](assets/content-copy-cancel.png)

>[!NOTE]
>
>Al cancelar una operación de copia de contenido, puede resultar en una copia parcial del contenido en el entorno de destino. Esto puede dejar el entorno de destino en un estado no utilizable.
>
>Si su entorno se encuentra en un estado de este tipo debido a una cancelación, póngase en contacto con el Servicio de atención al cliente de Adobe para obtener ayuda.

## Restricciones {#limitations}

La herramienta de copia de contenido tiene las siguientes limitaciones.

* El contenido no se puede copiar de un entorno inferior a un entorno superior.
* El contenido solo se puede copiar desde y hacia los servicios de creación.
* No es posible copiar contenido entre programas.
* No es posible ejecutar operaciones de copia de contenido simultáneas en el mismo entorno.
* Se pueden especificar hasta cincuenta rutas por cada conjunto de contenido. No hay limitación en las rutas excluidas.
* La herramienta de copia de contenido no debe utilizarse como una herramienta de clonación o reflejo, ya que no puede rastrear el contenido movido o eliminado del origen.
* La herramienta de copia de contenido no tiene capacidad de creación de versiones y no puede detectar automáticamente contenido modificado o recién creado en el entorno de origen en un conjunto de contenido desde la última operación de copia de contenido.
   * Si desea actualizar el entorno de destino con cambios de contenido solo desde la última operación de copia de contenido, debe crear un conjunto de contenido y especificar las rutas en la instancia de origen en la que se realizaron cambios desde la última operación de copia de contenido.
* La información de la versión no se incluye en una copia de contenido.
