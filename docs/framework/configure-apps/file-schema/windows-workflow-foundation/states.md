---
title: "&lt;states&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: ebea5e7c-ad58-43c5-8f2d-cca25ae1b721
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;states&gt;
Representa una colección de estados suscritos de la instancia de flujo de trabajo de la que se ha realizado el seguimiento cuando se crean los registros del seguimiento.  
  
 Para obtener más información sobre las consultas de los perfiles de seguimiento, consulte [Perfiles de seguimiento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)  
  
## Sintaxis  
  
```vb  
  
<tracking>  
   <trackingProfile name="Name">  
       <workflow>  
          <workflowInstanceQueries>  
             <workflowInstanceQuery>  
                <states>  
                   <state name="Name"/>  
                </states>  
            </workflowInstanceQuery>  
         </workflowInstanceQueries>  
       </workflow>  
   </trackingProfile>  
</tracking>  
  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### Atributos  
 Ninguno.  
  
### Elementos secundarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<state\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/states.md)|Un estado suscrito de la instancia de flujo de trabajo de la que se ha realizado el seguimiento cuando se crea el registro del seguimiento.|  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<workflowInstanceQuery\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/workflowinstancequery.md)|Una consulta que realiza el seguimiento de los cambios del ciclo de vida de la instancia de flujo de trabajo, como por ejemplo, un evento iniciado o completado.|  
  
## Comentarios  
 Los registros devueltos se filtran por los estados de esta colección.  
  
 En la siguiente tabla se describen los valores de estado posibles.  
  
|Estado|Descripción|  
|------------|-----------------|  
|Anulado|Se ha anulado la instancia de flujo de trabajo.|  
|Completado|Se ha completado la instancia de flujo de trabajo.|  
|Deleted|Se ha eliminado la instancia de flujo de trabajo.|  
|Inactivo|La instancia de flujo de trabajo está inactiva.|  
|Conservado|Se ha guardado la instancia de flujo de trabajo.|  
|Reanudado|Se ha reanudado la instancia de flujo de trabajo.|  
|Comenzado|Se ha iniciado la instancia de flujo de trabajo.|  
|UnhandledException|La instancia de flujo de trabajo ha detectado una excepción no controlada.|  
|Unloaded|Se ha descargado la instancia de flujo de trabajo.|  
|Cancelado|Se ha cancelado la instancia de flujo de trabajo.|  
|Suspendido|Se suspende la instancia de flujo de trabajo.|  
|Terminado|Se ha terminado la instancia de flujo de trabajo.|  
|No suspendido|No se suspende la instancia de flujo de trabajo.|  
  
## Ejemplo  
 La siguiente configuración se suscribe a los registros de seguimiento de nivel de instancia de flujo de trabajo del estado de instancia `Started` mediante esta consulta.  
  
```  
  
<workflowInstanceQueries>  
    <workflowInstanceQuery>  
      <states>  
        <state name="Started"/>  
      </states>  
    </workflowInstanceQuery>  
</workflowInstanceQueries>  
  
```  
  
## Vea también  
 [System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement](assetId:///System.ServiceModel.Activities.Tracking.Configuration.WorkflowInstanceQueryElement?qualifyHint=False&amp;autoUpgrade=True)   
 [System.ServiceModel.Activities.Tracking.Configuration.StateElementCollection](assetId:///System.ServiceModel.Activities.Tracking.Configuration.StateElementCollection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.Activities.Tracking.WorkflowInstanceQuery](assetId:///System.Activities.Tracking.WorkflowInstanceQuery?qualifyHint=False&amp;autoUpgrade=True)   
 [Seguimiento y traza del flujo de trabajo](../../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)   
 [Perfiles de seguimiento](../../../../../docs/framework/windows-workflow-foundation//tracking-profiles.md)