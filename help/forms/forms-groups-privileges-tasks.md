---
title: ¿Qué grupos de usuarios están disponibles de forma predeterminada en AEM Forms as a Cloud Service?
description: La lista de los grupos de usuarios y los permisos predeterminados asignados a cada grupo
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: bd66ce92-14d9-47fe-b5d3-022e3e468d25
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 81%

---

# Grupos y permisos {#aem-forms-on-osgi-groups-and-privileges}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/forms-groups-privileges-tasks.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Puede [crear grupos](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=es#accessing) y asignar políticas y [usuarios](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=es#accessing) a los grupos. Estas políticas controlan los permisos de los usuarios que forman parte del grupo.

Una vez configura [!DNL AEM Forms] as a Cloud Service, los grupos enumerados en la siguiente tabla, como [!DNL forms-users] y forms-power-user, están disponibles automáticamente para su asignación:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Permisos</td> 
  </tr>
  <tr>
   <td>[!DNL forms-users] <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
    <!-- <li>Create, preview, and publish interactive communications and document fragments</li> -->
     <li>Cargar recursos en una instancia de AEM</li> 
     <li>Crear temáticas</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>[!DNL forms-power-user]</td> 
   <td>
    <ul> 
     <li>Create, preview, publish, and submit Adaptive Forms</li> 
     <li>Create, preview, and publish interactive communications and document fragments</li> 
     <li>Create scripts for Adaptive Forms using code editor</li> 
     <li>Upload assets including scripts</li> 
     <li>Create themes</li> 
     <li>Import packages containing XDP</li> 
    </ul> </td> 
  </tr>
 <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Review submissions</li> 
     <li>Approve or reject submissions</li> 
    </ul> </td> 
  </tr> -->
  <tr>
   <td>[!DNL template-authors] <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Crear y previsualizar plantillas de formularios adaptables o <!-- or interactive communications --></li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>[!DNL fdm-authors]</p> </td> 
   <td>
    <ul> 
     <li>Crear y modificar un modelo de datos de formulario</li> 
    </ul> </td> 
  </tr>
  <!-- <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Access Correspondence Management letters or interactive communications using Agent UI</li> 
    </ul> </td> 
  </tr> --> 
  <!-- <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> -->
    <!-- <li>Create an inbox application</li>  -->
    <!-- <li>Create a workflow model</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL workflow-users]</td> 
   <td>
    <ul> 
     <li>Use AEM inbox applications<br /> -->
     <!-- 
     <strong>Note: </strong>You must have cm-agent-users and [!DNL workflow-users] group assignments to access Interactive Communications Agent UI in AEM inbox.</li>  -->
    </ul> </td> 
  </tr>
  <tr>
   <td>[!DNL fd-administrators]</td> 
   <td>
    <ul> 
     <!-- <li>Configure PDF Generator</li> --> 
     <!-- <li>Configure Watched folder</li> -->
     <li>Administrar aplicaciones de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## Aplicabilidad y casos de uso

### Seguro

## ¿Es AEM Forms de nivel empresarial para operaciones de seguro?

Sí. AEM Forms proporciona funciones empresariales como control de acceso basado en roles, pistas de auditoría, organización de flujos de trabajo, generación de documentos y flexibilidad de implementación, necesarias para las operaciones de seguro a escala.

## Consulte también

* [Incorporación al entorno de Cloud Service](/help/forms/setup-forms-cloud-service.md)
* [Configuración de un entorno de desarrollo local](/help/forms/setup-local-development-environment.md)
* [Migración de AEM 6.5 Forms a Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
* [Creación un formulario adaptable independiente](/help/forms/creating-adaptive-form-core-components.md)
* [Agregar un formulario adaptable de a la página de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

<!--

>[!MORELIKETHIS]
>
>* [Use AEM Forms workflow for business process automation](/help/forms/aem-forms-workflow.md)

-->
