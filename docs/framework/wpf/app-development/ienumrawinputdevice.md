---
title: "IEnumRAWINPUTDEVICE | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "IEnumRAWINPUTDEVICE (interfaz)"
ms.assetid: 88c8b389-a48b-46b9-b895-8ed7b1e26fea
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# IEnumRAWINPUTDEVICE
Esta interfaz enumera los dispositivos de entrada sin formato y solo la utiliza PresentationHost.exe.  
  
> [!NOTE]
>  Esta API solo está destinada y es compatible con el equipo cliente local  
  
## Miembros  
  
|Miembro|Descripción|  
|-------------|-----------------|  
|[IEnumRAWINPUTDEVIC:Next](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-next.md)|Enumera los elementos `celt` siguientes \(es decir, las estructuras RAWINPUTDEVICE\) de la lista del enumerador y los devuelve en `rgelt` junto con el número real de elementos enumerados en `pceltFetched`.|  
|[IEnumRAWINPUTDEVIC:Skip](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-skip.md)|Indica al enumerador para omitir los elementos `celt` siguientes en la enumeración para que la siguiente llamada a [IEnumRAWINPUTDEVIC:Next](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-next.md) no devuelva dichos elementos.|  
|[IEnumRAWINPUTDEVIC:Reset](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-reset.md)|Restablece la secuencia de enumeración al principio.|  
|[IEnumRAWINPUTDEVIC:Clone](../../../../docs/framework/wpf/app-development/ienumrawinputdevic-clone.md)|Crea otro enumerador de dispositivo de entrada sin formato con el mismo estado que el enumerador actual para crear una iteración por la misma lista.|  
  
## Vea también  
 [Acerca de la entrada sin formato](http://msdn.microsoft.com/library/default.asp?url=/library/winui/winui/windowsuserinterface/userinput/rawinput/aboutrawinput.asp)