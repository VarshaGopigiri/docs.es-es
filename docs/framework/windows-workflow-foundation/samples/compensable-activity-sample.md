---
title: "Ejemplo de actividad compensable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58f4898c-b2b8-44a4-9a73-3bef4da6d5ba
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Ejemplo de actividad compensable
En este ejemplo se muestra cómo utilizar la actividad `CompensableActivity` para definir el trabajo que se va a realizar para una acción determinada durante la ejecución normal y el trabajo que es necesario realizar para compensar dicha acción, si es necesario en un momento posterior.La primera parte del ejemplo muestra cómo se pueden definir las unidades de trabajo compensable en [!INCLUDE[wf](../../../../includes/wf-md.md)] utilizando una actividad `CompensableActivity` y cómo se ejecutan en una ejecución correcta.La segunda parte del ejemplo muestra cómo las mismas unidades de trabajo compensable se ocupan automáticamente de la compensación cuando se produce un evento inesperado y se cancela la instancia de flujo de trabajo.  
  
### Para configurar, compilar y ejecutar el ejemplo  
  
1.  Con Visual Studio 2010, abra CompensableActivity.sln.  
  
2.  Compile la solución presionando CTRL\+MAYÚS\+B.  
  
3.  Ejecute la aplicación presionando F5.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo.Compruebe el siguiente directorio \(valor predeterminado\) antes de continuar.  
>   
>  `<>InstallDrive:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a la página de [ejemplos de Windows Communication Foundation \(WCF\) y Windows Workflow Foundation \(WF\) Samples para .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los ejemplos de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] y [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<unidadDeInstalación>:\WF_WCF_Samples\WF\Basic\Compensation\BasicCompensableActivity`  
  
## Vea también