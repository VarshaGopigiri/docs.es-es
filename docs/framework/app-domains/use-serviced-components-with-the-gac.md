---
title: "Utilizar componentes con servicio junto con la memoria caché global de ensamblados"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache), serviced components
- serviced components, global assembly cache
- global assembly cache, serviced components
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 493ca9a2da4a06528eab9b87db78a5b7a49a2f1d
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="using-serviced-components-with-the-global-assembly-cache"></a>Utilizar componentes con servicio junto con la memoria caché global de ensamblados
Los componentes con servicio (componentes COM+ de código administrado) deben colocarse en la caché global de ensamblados. En algunos escenarios, Common Language Runtime y COM + Services pueden controlar componentes con servicio que no están en la caché global de ensamblados; en otros escenarios, no es posible. Estos escenarios ilustran lo siguiente:  
  
-   Para los componentes con servicio en una aplicación de COM+ Server, el ensamblado que contiene los componentes debe estar en la caché global de ensamblados, porque Dllhost.exe no se ejecuta en el mismo directorio que contiene los componentes con servicio.  
  
-   Para los componentes con servicio en una aplicación de COM+ Library, Common Language Runtime y COM+ Services pueden resolver la referencia al ensamblado que contiene los componentes buscando en el directorio actual. En este caso, el ensamblado no tiene que estar en la caché global de ensamblados.  
  
-   Para los componentes con servicio en una aplicación ASP.NET, la situación es distinta. Si coloca el ensamblado que contiene los componentes con servicio en el directorio bin de la base de la aplicación y utiliza el registro a petición, se copiará una instantánea del ensamblado en la caché de descarga porque ASP.NET aprovecha las funcionalidades de copia de Common Language Runtime.  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con ensamblados y la memoria caché global de ensamblados](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)   
 [Gacutil.exe (Herramienta Caché global de ensamblados)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)

