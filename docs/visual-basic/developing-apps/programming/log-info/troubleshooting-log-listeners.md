---
title: 'Solucionar problemas: Agentes de escucha del Registro (Visual Basic)'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0542aef4dc60821939e85760e6fadf0dfb528dec
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="troubleshooting-log-listeners-visual-basic"></a>Solucionar problemas: Agentes de escucha del Registro (Visual Basic)
Puede usar los objetos `My.Application.Log` y `My.Log` para registrar información sobre los eventos que se producen en su aplicación.  
  
 Para determinar qué agentes de escucha de registro reciben esos mensajes, vea [Tutorial: Determinar el lugar en el que My.Application.Log escribe la información](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).  
  
 El objeto `Log` puede usar el filtrado del registro para limitar la cantidad de información que registra. Si los filtros se configuran de manera incorrecta, los registros pueden contener información equivocada. Para obtener más información sobre los filtros, vea [Tutorial: Filtrar el resultado de My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md).  
  
 En cambio, si un registro se configura incorrectamente, puede necesitar más información sobre su configuración actual. Puede obtener esta información mediante la propiedad `TraceSource` avanzada del registro.  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a>Para determinar los agentes de escucha de registro del objeto Log con código  
  
1.  Importe el espacio de nombres <xref:System.Diagnostics> al principio del archivo de código. Para obtener más información, consulte [Instrucción Imports (Tipo y espacio de nombres de .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
     [!code-vb[VbVbalrMyApplicationLog#13](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_1.vb)]  
  
2.  Cree una función que devuelva una cadena compuesta por información de cada uno de los agentes de escucha del registro.  
  
     [!code-vb[VbVbalrMyApplicationLog#14](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_2.vb)]  
  
3.  Pase la colección de los agentes de escucha de seguimiento del registro a la función `GetListeners` y muestre el valor devuelto.  
  
     [!code-vb[VbVbalrMyApplicationLog#19](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_3.vb)]  
  
     Para obtener más información, consulta <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Trabajar con registros de aplicaciones](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Tutorial: Determinar el lugar en el que My.Application.Log escribe la información](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)

