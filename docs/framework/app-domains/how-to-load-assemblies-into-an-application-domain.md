---
title: "Cómo: Cargar ensamblados en un dominio de aplicación"
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
- application domains, loading assemblies
- loading assemblies
ms.assetid: 1432aa2d-bd83-4346-bf3b-a1b7920e2aa9
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 934373d61407c8cc19b7d6424898a582880f9c21
ms.openlocfilehash: c319da0f8e6f3cdfb83e659a778136d668699834
ms.contentlocale: es-es
ms.lasthandoff: 08/10/2017

---
# <a name="how-to-load-assemblies-into-an-application-domain"></a>Cómo: Cargar ensamblados en un dominio de aplicación
Existen numerosas formas de cargar un ensamblado en un dominio de aplicación. El método recomendado consiste en usar el método <xref:System.Reflection.Assembly.Load%2A> `static` (`Shared` en Visual Basic) de la clase <xref:System.Reflection.Assembly?displayProperty=fullName>. A continuación se indican otras formas de cargar los ensamblados:  
  
-   El método <xref:System.Reflection.Assembly.LoadFrom%2A> de la clase <xref:System.Reflection.Assembly> carga un ensamblado a partir de la ubicación del archivo correspondiente. La carga de ensamblados mediante este método usa un contexto de carga distinto.  
  
-   Los métodos <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> y <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> cargan un ensamblado en el contexto de solo reflexión. Los ensamblados cargados en este contexto pueden examinarse, pero no ejecutarse, lo que permite examinar los ensamblados que tienen como destino otras plataformas. Consulte [Cómo: Cargar ensamblados en el contexto de solo reflexión](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).  
  
> [!NOTE]
>  El contexto de solo reflexión es nuevo en la versión 2.0 de .NET Framework.  
  
-   Los métodos como <xref:System.AppDomain.CreateInstance%2A> y <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> de la clase <xref:System.AppDomain> pueden cargar ensamblados en un dominio de aplicación.  
  
-   El método <xref:System.Type.GetType%2A> de la clase <xref:System.Type> puede cargar ensamblados.  
  
-   El método <xref:System.AppDomain.Load%2A> de la clase <xref:System.AppDomain?displayProperty=fullName> puede cargar ensamblados, pero se usa principalmente para la interoperabilidad COM. No se debe usar para cargar ensamblados en un dominio de aplicación que no sea el dominio de aplicación desde el que se llama.  
  
> [!NOTE]
>  A partir de la versión 2.0 de .NET Framework, el tiempo de ejecución no cargará ningún ensamblado compilado con una versión de .NET Framework que tenga un número de versión superior al tiempo de ejecución cargado actualmente. Esto se aplica a la combinación de los componentes principal y secundario del número de versión.  
  
 Puede especificar cómo se comparte entre los dominios de aplicación el código compilado Just-In-Time (JIT) de los ensamblados cargados. Para obtener más información, consulte [Dominios de aplicación y ensamblados](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346).  
  
## <a name="example"></a>Ejemplo  
 El siguiente código carga un ensamblado llamado "example.exe" o "example.dll" en el dominio de aplicación actual, obtiene del ensamblado un tipo llamado `Example`, obtiene un método sin parámetros llamado `MethodA` para dicho tipo y lo ejecuta. Para obtener una descripción completa sobre cómo obtener información de un ensamblado cargado, consulte [Dynamically Loading and Using Types](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md) (Cargar y usar tipos dinámicamente).  
  
 [!code-cpp[System.AppDomain.Load#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source2.cpp#2)] [!code-csharp[System.AppDomain.Load#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source2.cs#2)] [!code-vb[System.AppDomain.Load#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source2.vb#2)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>   
 [Programar con dominios de aplicación](http://msdn.microsoft.com/en-us/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [Reflexión](../../../docs/framework/reflection-and-codedom/reflection.md)   
 [Utilizar dominios de aplicación](../../../docs/framework/app-domains/use.md)   
 [Cómo: Cargar ensamblados en el contexto de solo reflexión](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)   
 [Dominios de aplicación y ensamblados](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346)

