---
title: Trabajo con Publicación selectiva en Dynamic Media
description: Aprenda a trabajar con Publicación selectiva en Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Publishing,Dynamic Media
role: User
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '2946'
ht-degree: 3%

---

# Configuración de la publicación selectiva en el nivel de carpeta en Dynamic Media {#selective-publish-configure-folder}

Puede optar por publicar recursos o cancelar la publicación de estos en Adobe Experience Manager o Dynamic Media. Puede hacerlo en el nivel de carpeta, usando **[!UICONTROL Administrar publicación]** o **[!UICONTROL Publicación rápida]**. Este método de publicación es útil porque no se basa únicamente en la **[!UICONTROL configuración de Dynamic Media]** cuya configuración es global para todas las carpetas de la instancia de Dynamic Media.

Por ejemplo, con la publicación selectiva puede trabajar en los recursos de los productos que aún no están activos. En tal caso, un equipo de marketing puede acceder a las imágenes de recorte inteligente y a las representaciones dinámicas sincronizadas con Dynamic Media. Pueden crear materiales promocionales, sin necesidad de publicar estos recursos en Dynamic Media para su publicación global.

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Al copiar* recursos en y desde carpetas, se borra el estado de publicación de esos recursos. Sin embargo, cuando *mueve* recursos a y desde carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

Si más tarde decide cambiar la configuración de **[!UICONTROL Publicación selectiva]** en una carpeta, esos cambios solo afectarán a los nuevos recursos que cargue en esa carpeta a partir de ese momento. El estado de publicación de los recursos existentes en la carpeta se mantendrá tal cual hasta que los cambie manualmente desde **[!UICONTROL Publicación rápida]** o el cuadro de diálogo **[!UICONTROL Administrar publicación]**.

La opción del nivel de carpeta **[!UICONTROL Modo de publicación de Dynamic Media]** siempre toma como valor predeterminado el valor que se encuentra en la configuración de **[!UICONTROL Publicar Assets]** de su **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, los siguientes pasos de este tema le muestran cómo cambiar manualmente este valor predeterminado en el nivel de carpeta (como se describe en los pasos siguientes) para anular el valor **[!UICONTROL Configuración de Dynamic Media]**.

Independientemente de si confía en:

* El valor de **[!UICONTROL Publish Assets]** establecido en **[!UICONTROL Configuración de Dynamic Media]**
* O el valor **[!UICONTROL Modo de publicación de medios dinámicos]** establecido en las propiedades de nivel de carpeta

Todavía puede elegir **[!UICONTROL Inmediatamente]**, **[!UICONTROL Tras la activación]** o **[!UICONTROL Publicación selectiva]**. Por ejemplo, puede establecer el valor de **[!UICONTROL Publicar Assets]** en su **[!UICONTROL Configuración de Dynamic Media]** en **[!UICONTROL Al activarlo]**. Además, puede establecer el valor del modo **[!UICONTROL Publicación de medios dinámicos]** en el nivel de carpeta en **[!UICONTROL Publicación selectiva]**, a la inversa, etc.

Después de configurar la publicación selectiva en una carpeta, puede realizar cualquiera de las siguientes acciones:

* [Publicar recursos de forma selectiva en Dynamic Media o Experience Manager mediante Administrar publicación](#selective-publish-manage-publication).
* [Cancele la publicación selectiva de recursos de Dynamic Media o Experience Manager mediante Administrar publicación](#selective-unpublish-manage-publication).
* [Publicar recursos en Dynamic Media o Experience Manager mediante Publicación rápida](#quick-publish-aem-dm).
* [Publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda](#selective-publish-unpublish-search-results).

**Para configurar la publicación selectiva en el nivel de carpeta en Dynamic Media:**

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas) y, a continuación, vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Realice una de las siguientes acciones:
   * Edite las propiedades de una carpeta existente: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, desplácese a una carpeta cuyas propiedades desee editar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
   * Edita las propiedades de una nueva carpeta: en **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, cerca de la esquina superior derecha de la página, ve a **[!UICONTROL Crear]** > **[!UICONTROL Carpeta]**. En el cuadro de diálogo **[!UICONTROL Crear carpeta]**, escriba un título (obligatorio) para la carpeta y, a continuación, seleccione **[!UICONTROL Crear]**. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.

1. En la lista desplegable **[!UICONTROL Modo de sincronización]**, seleccione una de las siguientes opciones:

   | Modo de sincronización | Descripción |
   | --- | --- |
   | **[!UICONTROL Heredado]** | No hay ningún valor de sincronización explícito en la carpeta; en su lugar, la carpeta hereda el valor de sincronización de una de sus carpetas antecesoras o del modo predeterminado establecido en **[!UICONTROL Configuración de Dynamic Media]**. El estado detallado de **[!UICONTROL Heredado]** se muestra a través de la información sobre herramientas. |
   | **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]** | Para que la publicación en Dynamic Media se realice correctamente, los recursos deben sincronizarse con Dynamic Media. Al seleccionar esta opción, se incluyen todos los recursos de este subárbol para sincronizarlos con Dynamic Media. La configuración específica de la carpeta anula la configuración predeterminada de **[!UICONTROL Configuración de Dynamic Media]**. |
   | **[!UICONTROL Excluir todo el contenido del subárbol de carpetas de la sincronización de Dynamic Media]** | Excluya todos los recursos de este subárbol de la sincronización con Dynamic Media. |

   ![Publicación selectiva de nivel de carpeta](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. En la lista desplegable **[!UICONTROL Modo de publicación de medios dinámicos]**, seleccione una opción. La opción **[!UICONTROL Modo de publicación de Dynamic Media]** siempre toma como valor predeterminado el valor establecido en la **[!UICONTROL Configuración de Dynamic Media]**. Sin embargo, puede invalidar manualmente este valor predeterminado de **[!UICONTROL configuración de Dynamic Media]** mediante una de las siguientes opciones.

   >[!IMPORTANT]
   >
   >Independientemente de la opción de modo de publicación de Dynamic Media que seleccione, de cualquier actualización que realice posteriormente en un recurso que ya esté *publicado*, esas actualizaciones se publican inmediatamente sin que el usuario tenga que realizar ninguna otra acción.

   | Opción de modo de publicación de Dynamic Media | Descripción |
   | --- | --- |
   | **[!UICONTROL Inmediatamente]** | Cuando los recursos se cargan en esta carpeta, el sistema los incorpora en Experience Manager y proporciona la URL o la incrustación de forma inmediata. Esta opción solo está vinculada a la publicación de Experience Manager y no es necesaria ninguna intervención del usuario para publicar los recursos.<br>Esta opción *no está disponible* si seleccionó **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** en **[!UICONTROL modo de sincronización]** en el paso anterior. |
   | **[!UICONTROL Tras la activación]** | Cuando los recursos se cargan en esta carpeta, primero debe publicarlos explícitamente antes de proporcionar un vínculo URL/incrustado. Esta opción solo está vinculada a la publicación de Experience Manager.<br>Esta opción *no está disponible* si seleccionó **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** en **[!UICONTROL modo de sincronización]** en el paso anterior. |
   | **[!UICONTROL Publicación selectiva]** | Assets se publica a su elección de Experience Manager o de Dynamic Media para su publicación en el dominio público. Ambos métodos de publicación son mutuamente excluyentes. Es decir, puede publicar recursos en DMS7 para poder utilizar funciones como Recorte inteligente o representaciones dinámicas. O bien, puede publicar recursos exclusivamente en Experience Manager para una previsualización segura; esos mismos recursos son *no* publicados en DMS7 para su envío en el dominio público. Esta opción no está disponible si seleccionó **[!UICONTROL Excluir todo en este subárbol de carpetas de la sincronización de Dynamic Media]** en **[!UICONTROL modo de sincronización]** en el paso anterior. |

1. En la esquina superior derecha de la página, selecciona **[!UICONTROL Guardar y cerrar]** y, a continuación, selecciona **[!UICONTROL Aceptar]** para volver a Experience Manager Assets.

## Publicar recursos de forma selectiva en Dynamic Media o Experience Manager as a Cloud Service mediante Administrar publicación{#selective-publish-manage-publication}

Antes de poder usar **[!UICONTROL Administrar publicación]** para publicar recursos de forma selectiva en Dynamic Media o Experience Manager, asegúrese de haber realizado una de las siguientes acciones:

* Establezca la opción **[!UICONTROL Publicar Assets]** en **[!UICONTROL Configuración de Dynamic Media]** en **[!UICONTROL Publicación selectiva]**.
* O bien, configure la publicación selectiva en el nivel de carpeta.

Consulte [Crear una configuración de Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configurar publicación selectiva en el nivel de carpeta en Dynamic Media](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*Al copiar* recursos en y desde carpetas, se borra el estado de publicación de esos recursos. Sin embargo, cuando *mueve* recursos a y desde carpetas cuya propiedad de carpeta está establecida en **[!UICONTROL Publicación selectiva]**, se mantiene el estado de publicación de esos recursos.

**Para publicar recursos de forma selectiva en Dynamic Media o Experience Manager as a Cloud Service mediante Administrar publicación:**

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas) y, a continuación, vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Use **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Use **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

     >[!NOTE]
     >
     >Si **[!UICONTROL Administrar publicación]** no aparece en la barra de herramientas, selecciona el botón de los tres puntos y, a continuación, selecciona **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En la página **[!UICONTROL Administrar publicación - Opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de activación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Publicar]** (en Experience Manager) | Para publicar recursos en Experience Manager para una previsualización segura, seleccione esta opción. |
   | **[!UICONTROL Publicar en Dynamic Media]** | Para publicar recursos en Dynamic Media para su envío en el dominio público o para que pueda utilizar funciones como Recorte inteligente o representaciones dinámicas, seleccione esta opción.<br>Esta opción solo está disponible si **[!UICONTROL Modo de publicación de Dynamic Media]** está establecido en **[!UICONTROL Publicación selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programar]**, establezca el tiempo de la publicación.

   | Programación | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para publicar los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para publicar los recursos en una fecha y hora determinadas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, seleccione **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Si es necesario, seleccione uno o varios recursos que desee eliminar de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, seleccione **[!UICONTROL Publicar]** o **[!UICONTROL Publicar en Dynamic Media]**.
1. Seleccione **[!UICONTROL Aceptar]**.

### Cancelar la publicación selectiva de recursos de Dynamic Media o Experience Manager mediante Administrar publicación {#selective-unpublish-manage-publication}

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global. En el lado izquierdo, seleccione el icono Navegación (justo encima del icono Herramientas) y, a continuación, vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee cancelar la publicación. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Use **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee cancelar la publicación. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Use **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

     >[!NOTE]
     >
     >Si **[!UICONTROL Administrar publicación]** no aparece en la barra de herramientas, selecciona el botón de los tres puntos y, a continuación, selecciona **[!UICONTROL Administrar publicación]** en el menú de la lista.

1. En la página **[!UICONTROL Administrar publicación - Opciones]**, en **[!UICONTROL Acción]**, seleccione el tipo de desactivación que desee.

   | Acción | Descripción |
   | --- | --- |
   | **[!UICONTROL Cancelar publicación]** (de Experience Manager) | Para cancelar la publicación de recursos desde Experience Manager, seleccione esta opción. |
   | **[!UICONTROL Cancelar publicación de medios dinámicos]** | Para cancelar la publicación de recursos desde Dynamic Media, seleccione esta opción.<br>Esta opción solo está disponible si **[!UICONTROL Modo de publicación de Dynamic Media]** está establecido en **[!UICONTROL Publicación selectiva]** en las propiedades de la carpeta. |

1. En **[!UICONTROL Programar]**, establezca el tiempo de desactivación.

   | Programación | Descripción |
   | --- | --- |
   | **[!UICONTROL Ahora]** | Seleccione para cancelar la publicación de los recursos inmediatamente. |
   | **[!UICONTROL Más tarde]** | Seleccione para cancelar la publicación de los recursos en una fecha y hora determinadas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación]**, seleccione **[!UICONTROL Siguiente]**.
1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar para cancelar la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, seleccione **[!UICONTROL Cancelar publicación]** o **[!UICONTROL Cancelar publicación de Dynamic Media]**.
1. Seleccione **[!UICONTROL Aceptar]**.

## Publicación de recursos en Dynamic Media o Experience Manager mediante Publicación rápida {#quick-publish-aem-dm}

Puede usar **[!UICONTROL Publicación rápida]** para casos de activación de recursos simples. **[!UICONTROL Publicación rápida]** publica los recursos seleccionados inmediatamente sin ninguna otra interacción del usuario. Las referencias no publicadas también se publican automáticamente.

>[!NOTE]
>
>Para usar **[!UICONTROL Publicación rápida]** para publicar recursos en Dynamic Media o Experience Manager, asegúrese de que **[!UICONTROL Publicación selectiva]** esté habilitada en su **[!UICONTROL Configuración de Dynamic Media]** o en las propiedades de carpeta de la carpeta seleccionada.

**Para publicar recursos en Dynamic Media o Experience Manager mediante Publicación rápida:**

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global. En la parte izquierda de la página, selecciona el icono Navegación (justo encima del icono Herramientas) y, a continuación, en la parte derecha de la página, ve a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]**, realice una de las siguientes acciones:
   * Vaya a una carpeta cuyos recursos desee publicar. Seleccione la carpeta y, en la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Use **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de una carpeta en particular.
   * Vaya a una carpeta cuyos recursos desee publicar. Abra la carpeta y seleccione uno o varios recursos. En la barra de herramientas, seleccione **[!UICONTROL Publicación rápida]**. Use **[!UICONTROL Vista de lista]** para poder comprobar más fácilmente el estado de publicación de un recurso en particular.

     >[!NOTE]
     >
     >Si no se ve **[!UICONTROL Publicación rápida]** en la barra de herramientas, selecciona el botón de puntos suspensivos y, a continuación, selecciona **[!UICONTROL Publicación rápida]** en el menú de lista.

     ![Publicación rápida en Dynamic Media a nivel de carpeta](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleccione una de las siguientes opciones en la lista de menú **[!UICONTROL Publicación rápida]**.

   | Opción Publicación rápida | Qué hace |
   | --- | --- |
   | Publicar en Experience Manager | Publica los recursos seleccionados inmediatamente en Experience Manager. |
   | Publicar en Brand Portal | Publica los recursos seleccionados inmediatamente en **[!UICONTROL Brand Portal]**.<br>Esta opción solo está disponible si la instancia de Experience Manager Assets ya tiene **[!UICONTROL Brand Portal]** configurado. |
   | Publicar en Dynamic Media | Publica los recursos seleccionados inmediatamente en Dynamic Media.<br>Ya se debe sincronizar un recurso con Dynamic Media. Si es necesario, asegúrate de que el **[!UICONTROL modo de sincronización]** en las propiedades de una carpeta ya esté establecido en **[!UICONTROL Sincronizar todo en este subárbol de carpetas con Dynamic Media]**. |

1. Seleccione **[!UICONTROL Aceptar]** y, a continuación, seleccione **[!UICONTROL Cerrar]**.

## Publicar o cancelar la publicación selectiva de recursos mediante resultados de búsqueda {#selective-publish-unpublish-search-results}

Los resultados de búsqueda pueden mostrar recursos de carpetas de recursos que tienen diferentes configuraciones de publicación de Dynamic Media. Si ha seleccionado uno o más recursos de los resultados de búsqueda y los recursos tienen diferentes configuraciones del modo de publicación de Dynamic Media, puede almacenar en déclencheur **[!UICONTROL Administrar publicación]** desde la barra de herramientas, para publicar o cancelar la publicación.

Consulte también [Buscar recursos en Experience Manager](/help/assets/search-assets.md).

**Para publicar o cancelar la publicación de recursos de forma selectiva mediante los resultados de búsqueda:**

1. En Experience Manager, en la esquina superior izquierda de la página, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global. En la parte izquierda de la página, selecciona el icono Navegación (justo encima del icono Herramientas) y luego ve a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En la barra de herramientas, cerca de la esquina superior derecha de la página, seleccione el icono Buscar (lupa).
1. En el campo de texto **[!UICONTROL Escriba para buscar]**, escriba una palabra clave y presione **[!UICONTROL Entrar]**.
1. Cerca de la esquina superior derecha de la página, seleccione el icono **[!UICONTROL Vista de lista]**.
1. Cerca de la esquina superior izquierda de la página, seleccione el icono **[!UICONTROL Filtros]**.

   ![Vista de lista y filtros en los resultados de búsqueda](/help/assets/assets-dm/select-publish-search-result.png)

1. En el panel izquierdo, expanda **[!UICONTROL Estado]** y luego expanda el predicado de búsqueda **[!UICONTROL Dynamic Media]**.
1. Utilice las casillas de verificación **[!UICONTROL Publicado]** y **[!UICONTROL No publicado]** para restringir aún más los resultados de búsqueda en función del estado publicado de los recursos de Dynamic Media.
De forma opcional, puede utilizar estas casillas de verificación con el predicado de búsqueda **[!UICONTROL Publish]** para restringir los resultados de búsqueda de los recursos de Experience Manager **[!UICONTROL Publicados]** y **[!UICONTROL No publicados]**.
1. Realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee publicar o cancelar la publicación.
   * Cerca de la esquina superior derecha de la página **[!UICONTROL Resultados de búsqueda]**, seleccione **[!UICONTROL Seleccionar todo]**.
1. En la barra de herramientas, seleccione **[!UICONTROL Administrar publicación]**. Si es necesario, seleccione el icono de puntos suspensivos en la barra de herramientas para ver **[!UICONTROL Administrar publicación]**.
1. En la página **[!UICONTROL Administrar publicación - Opciones]**, seleccione la acción que desee.

   | Acción seleccionada | Publicar la configuración de Assets en la configuración de Dynamic Media | Assets son |
   | --- | --- | --- |
   | Publicación | Inmediatamente o tras la activación | Publicado en Experience Manager y Dynamic Media. |
   | Publicación | Publicación selectiva | Publicado solo en Experience Manager. |
   | Cancelar la publicación | Inmediatamente o tras la activación | Publicación cancelada de Experience Manager y Dynamic Media. |
   | Cancelar la publicación | Publicación selectiva | Solo se ha cancelado la publicación de Experience Manager. |
   | Publicar en Dynamic Media | Inmediatamente o tras la activación | No se ha publicado en Experience Manager, Dynamic Media o ambos. |
   | Publicar en Dynamic Media | Publicación selectiva | Publicado solo en Dynamic Media. |
   | Cancelar la publicación de Dynamic Media | Inmediatamente o tras la activación | No se ha cancelado la publicación de Experience Manager, Dynamic Media o ambos. |
   | Cancelar la publicación de Dynamic Media | Publicación selectiva | Solo se ha cancelado la publicación de Dynamic Media. |

1. En **[!UICONTROL Programar]**, establezca el tiempo de desactivación.

   | Programación seleccionada | ¿Qué sucede? |
   | --- | --- |
   | Ahora | La acción seleccionada se realiza inmediatamente. |
   | Más tarde | La acción seleccionada se ejecuta en la fecha y la hora seleccionadas. |

1. En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Opciones]**, seleccione **[!UICONTROL Siguiente]**.
1. (Opcional) En la página **[!UICONTROL Administrar publicación - Ámbito]**, revise la columna **[!UICONTROL Destino de publicación]** de la tabla para los recursos seleccionados.

   | Publicar la configuración de Assets en la configuración de Dynamic Media | Acción seleccionada | Destino de publicación |
   | --- | --- | --- |
   | Inmediatamente o <br> tras la activación | Publicación | Experience Manager y Dynamic Media |
   | Inmediatamente o <br> tras la activación | Publicar en Dynamic Media | Ninguno |
   | Publicación selectiva | Publicación | Experience Manager |
   | Publicación selectiva | Publicar en Dynamic Media | Dynamic Media |
   | Inmediatamente o <br> tras la activación | Cancelar la publicación | Experience Manager y Dynamic Media |
   | Inmediatamente o <br> tras la activación | Cancelar la publicación de Dynamic Media | Ninguno |
   | Publicación selectiva | Cancelar la publicación | Experience Manager |
   | Publicación selectiva | Cancelar la publicación de Dynamic Media | Dynamic Media |

1. En la página **[!UICONTROL Administrar publicación - Ámbito]**, realice una de las siguientes acciones:
   * Seleccione uno o varios recursos que desee eliminar de la publicación o cancelación de la publicación.
   * En la esquina superior derecha de la página **[!UICONTROL Administrar publicación - Ámbito]**, seleccione **[!UICONTROL Publicar]** o **[!UICONTROL Cancelar la publicación]** para comenzar la acción.
1. Seleccione **[!UICONTROL Aceptar]**.

## Comprobar el estado de publicación de un recurso {#check-publish-status-of-asset}

Puede usar **[!UICONTROL Cronología]** con **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** en Experience Manager para comprobar rápidamente el estado de publicación de un recurso.

**Para comprobar el estado de publicación de un recurso:**

1. En Experience Manager, en la esquina superior izquierda de la página, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global. En la parte izquierda de la página, selecciona el icono Navegación (justo encima del icono Herramientas) y luego ve a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. En **[!UICONTROL Vista de tarjeta]**, **[!UICONTROL Vista de columna]** o **[!UICONTROL Vista de lista]** (la captura de pantalla siguiente muestra la **[!UICONTROL Vista de lista]**), abra una carpeta que contenga recursos que haya publicado o cuya publicación haya cancelado.
1. Seleccione un recurso para que aparezca con una marca de verificación. Vea la captura de pantalla siguiente para ver un ejemplo.
1. Cerca de la esquina superior izquierda de la página, en el menú desplegable, seleccione **[!UICONTROL Cronología]**. La región **[!UICONTROL Estado]** del panel izquierdo muestra el estado de publicación del recurso seleccionado.
Cuando usa **[!UICONTROL Vista de lista]**, aparece una columna adicional para el estado de publicación de **[!UICONTROL Dynamic Media]**.
   * Una carpeta configurada para sincronizarse con Dynamic Media muestra la columna **[!UICONTROL Dynamic Media]** de forma predeterminada.
   * Una carpeta *no* configurada para sincronizarse con Dynamic Media no muestra la columna Dynamic Media.
     ![Vista de lista y cronología](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Solucionar problemas de publicación selectiva {#selective-publish-troubleshoot}

Un recurso que no está sincronizado con Dynamic Media pero que tiene una acción de publicación de Dynamic Media activada en él da como resultado el siguiente mensaje de error y solución:

![Error de publicación selectiva](/help/assets/assets-dm/selective-publish-error.png)
