---
title: "Miembros (Guía de programación de C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- types [C#], nested types
- C# language, type members
ms.assetid: 4a30a4ab-d690-4936-9124-92ce9448665a
caps.latest.revision: 20
author: BillWagner
ms.author: wiwagn
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
ms.openlocfilehash: 98446a2eb0415c92aa44cbddf8539477a00a2666
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="members-c-programming-guide"></a>Miembros (Guía de programación de C#)
Las clases y structs tienen miembros que representan sus datos y comportamiento. Los miembros de una clase incluyen todos los miembros declarados en la clase, junto con todos los miembros (excepto constructores y finalizadores) declarados en todas las clases de su jerarquía de herencia. Los miembros privados de clases base se heredan en las clases derivadas, pero estas no pueden tener acceso a ellos.  
  
 En la tabla siguiente se enumeran los tipos de miembros que puede contener una clase o struct:  
  
|Miembro|Descripción|  
|------------|-----------------|  
|[Campos](../../../csharp/programming-guide/classes-and-structs/fields.md)|Los campos son variables declaradas en el ámbito de clase. Un campo puede ser un tipo numérico integrado o una instancia de otra clase. Por ejemplo, una clase de calendario puede tener un campo con la fecha actual.|  
|[Constantes](../../../csharp/programming-guide/classes-and-structs/constants.md)|Las constantes son campos o propiedades cuyo valor se establece en tiempo de compilación y no se puede cambiar.|  
|[Propiedades](../../../csharp/programming-guide/classes-and-structs/properties.md)|Las propiedades son métodos de una clase a los que se obtiene acceso como si fueran campos de esa clase. Una propiedad puede proporcionar protección a un campo de clase con el fin de evitar que se cambie sin el conocimiento del objeto.|  
|[Métodos](../../../csharp/programming-guide/classes-and-structs/methods.md)|Los métodos definen las acciones que una clase puede realizar. Los métodos pueden aceptar parámetros que proporcionan datos de entrada y devolver datos de salida a través de parámetros. Los métodos también pueden devolver un valor directamente, sin usar ningún parámetro.|  
|[Eventos](../../../csharp/programming-guide/events/index.md)|Los eventos proporcionan a otros objetos notificaciones sobre lo que ocurre, como clics en botones o la realización correcta de un método. Los eventos se definen y desencadenan mediante delegados.|  
|[Operadores](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|Los operadores sobrecargados se consideran miembros de clase. Si se sobrecarga un operador, se define como método estático público en una clase. Los operadores predefinidos (`+`, `*`, `<`, etc.) no se consideran miembros. Para obtener más información, vea [Operadores sobrecargables](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md).|  
|[Indizadores](../../../csharp/programming-guide/indexers/index.md)|Los indizadores permiten indizar un objeto de manera similar a como se hace con las matrices.|  
|[Constructores](../../../csharp/programming-guide/classes-and-structs/constructors.md)|Los constructores son métodos a los que se llama cuando el objeto se crea por primera vez. Se usan a menudo para inicializar los datos de un objeto.|  
|[Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)|En C#, los finalizadores se usan en raras ocasiones. Son métodos a los que llama el motor de ejecución del runtime cuando el objeto está a punto de quitarse de la memoria. Generalmente se utilizan para asegurarse de que los recursos que se deben liberar se controlan apropiadamente.|  
|[Tipos anidados](../../../csharp/programming-guide/classes-and-structs/nested-types.md)|Los tipos anidados son tipos declarados dentro de otro tipo. Los tipos anidados se usan a menudo para describir objetos utilizados únicamente por los tipos que los contienen.|  
  
## <a name="see-also"></a>Vea también  
 [Guía de programación de C#](../../../csharp/programming-guide/index.md)   
 [Clases](../../../csharp/programming-guide/classes-and-structs/classes.md)   
 [Métodos](../../../csharp/programming-guide/classes-and-structs/methods.md)   
 [Constructors](../../../csharp/programming-guide/classes-and-structs/constructors.md)  (Constructores [Guía de programación de C#])  
 [Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)   
 [Propiedades](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [Campos](../../../csharp/programming-guide/classes-and-structs/fields.md)   
 [Indexers](../../../csharp/programming-guide/indexers/index.md)  (Indexadores)  
 [Eventos](../../../csharp/programming-guide/events/index.md)   
 [Tipos anidados](../../../csharp/programming-guide/classes-and-structs/nested-types.md)   
 [Operadores](../../../csharp/programming-guide/statements-expressions-operators/operators.md)   
 [Operadores sobrecargables](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)

