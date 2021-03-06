---
title: "How to: Register Callbacks for Cancellation Requests | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "cancellation, how to register callbacks"
ms.assetid: 8838dd75-18ed-4b8b-b322-cd4531faac64
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Register Callbacks for Cancellation Requests
En el ejemplo siguiente se muestra cómo registrar un delegado que se invoca cuando una propiedad <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> pasa a ser true debido a una llamada a <xref:System.Threading.CancellationTokenSource.Cancel%2A> en el objeto que creó el token.  Use esta técnica para cancelar operaciones asincrónicas que no admiten el marco de cancelación unificado de forma nativa, y para desbloquear métodos que podrían estar esperando que una operación asincrónica finalice.  
  
> [!NOTE]
>  Cuando está habilitada la opción "Solo mi código", en algunos casos, Visual Studio se interrumpe en la línea que produce la excepción y muestra el mensaje de error "Excepción no controlada por el código de usuario". Este error es benigno.  Puede presionar F5 para continuar y ver el comportamiento de control de excepciones que se muestra en estos ejemplos.  Para evitar que Visual Studio se interrumpa con el primer error, desactive la casilla «Solo mi código» en **Herramientas, Opciones, Depuración, General**.  
  
## Ejemplo  
 En el ejemplo siguiente, el método <xref:System.Net.WebClient.CancelAsync%2A> se registra como el método que se invocará cuando se solicite la cancelación mediante el token de cancelación.  
  
 [!code-csharp[Conceptual.Cancellation.Callback#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.cancellation.callback/cs/howtoexample1.cs#1)]
 [!code-vb[Conceptual.Cancellation.Callback#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.cancellation.callback/vb/howtoexample1.vb#1)]  
  
 Si ya ha solicitado la cancelación al registrar la devolución de llamada, aún se garantiza que se llamará a la devolución de llamada.  En este caso, el método <xref:System.Net.WebClient.CancelAsync%2A> no hará nada si no hay ninguna operación asincrónica en curso, por lo que siempre es seguro llamar al método.  
  
## Vea también  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)