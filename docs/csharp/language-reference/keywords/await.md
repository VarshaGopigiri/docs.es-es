---
title: await (Referencia de C#)
ms.date: 2017-05-22
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- await_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- await keyword [C#]
- await [C#]
ms.assetid: 50725c24-ac76-4ca7-bca1-dd57642ffedb
caps.latest.revision: 36
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
ms.openlocfilehash: 28be25d2f467ea5df4de50516bfa03347c77081e
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="await-c-reference"></a>await (Referencia de C#)
El operador `await` se aplica a una tarea de un método asincrónico para insertar un punto de suspensión en la ejecución del método hasta que la tarea en espera se complete. La tarea representa el trabajo en curso.  
  
`await` solo puede usarse en un método asincrónico que se ha modificado mediante la palabra clave [async](../../../csharp/language-reference/keywords/async.md). Este tipo de método, que se define mediante el modificador `async` y que generalmente contiene una o más expresiones `await`, se denomina *método asincrónico*.  
  
> [!NOTE]
>  Las palabras clave `async` y `await` se han incluido en C# 5. Para obtener una introducción a la programación asincrónica, vea [Programación asincrónica con async y await](../../../csharp/programming-guide/concepts/async/index.md).  
  
La tarea a la que se aplica el operador `await` se devuelve normalmente mediante una llamada a un método que implementa el [patrón asincrónico basado en tareas](../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md). Incluyen métodos que devuelven objetos <xref:System.Threading.Tasks.Task>, <xref:System.Threading.Tasks.Task%601> y `System.Threading.Tasks.ValueType<TResult>`.  

  
 En el siguiente ejemplo, el método <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A?displayProperty=fullName> devuelve un `Task<byte[]>`. La tarea garantiza que la matriz de bytes real se generará cuando finalice la tarea. El operador `await` suspende la ejecución hasta que el trabajo del método <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A> se completa. Mientras tanto, el control vuelve al llamador de `GetPageSizeAsync`. Cuando la tarea finaliza la ejecución, la expresión `await` se evalúa como una matriz de bytes.  

[!code-cs[await-example](../../../../samples/snippets/csharp/language-reference/keywords/await/await1.cs)]  

> [!IMPORTANT]
>  Para obtener el ejemplo completo, vea [Walkthrough: Accessing the Web by Using Async and Await](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) (Tutorial: Acceso a la web usando Async y Await). Puede descargar el ejemplo desde [Ejemplos de código para desarrolladores](http://go.microsoft.com/fwlink/?LinkID=255191&clcid=0x409) en el sitio web de Microsoft. El ejemplo está en el proyecto AsyncWalkthrough_HttpClient.  
  
Tal y como se muestra en el ejemplo anterior, si `await` se aplica al resultado de una llamada al método que devuelve `Task<TResult>`, el tipo de la expresión `await` es `TResult`. Si `await` se aplica al resultado de una llamada al método que devuelve `Task`, el tipo de la expresión `await` es `void`. En el siguiente ejemplo se ilustra la diferencia.  
  
```csharp  
// await keyword used with a method that returns a Task<TResult>.  
TResult result = await AsyncMethodThatReturnsTaskTResult();  
  
// await keyword used with a method that returns a Task.  
await AsyncMethodThatReturnsTask();  

// await keyword used with a method that returns a ValueTask<TResult>.
TResult result = await AsyncMethodThatReturnsValueTaskTResult();
```  
  
Una expresión `await` no bloquea el subproceso en el que se ejecuta. En su lugar, hace que el compilador suscriba el resto del método asincrónico como una continuación de la tarea esperada. A continuación, el control vuelve al llamador del método asincrónico. Cuando la tarea se completa, invoca su continuación y la ejecución del método asincrónico se reanuda donde se quedó.  
  
Una expresión `await` solo puede aparecer en el cuerpo de su método envolvente, en una expresión lambda o en un método anónimo que debe marcarse con un modificador `async`. El término *await* solo sirve como palabra clave en ese contexto. En cualquier otra parte, se interpretará como identificador. Dentro del método, expresión lambda o método anónimo, una expresión `await` no se puede producir en el cuerpo de una función sincrónica, en una expresión de consulta, en el bloque de una [instrucción lock](../../../csharp/language-reference/keywords/lock-statement.md), ni en un contexto [unsafe](../../../csharp/language-reference/keywords/unsafe.md).  
  
## <a name="exceptions"></a>Excepciones  
La mayoría de los métodos asincrónicos devuelven un objeto <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>. Las propiedades de la tarea devuelta llevan información acerca de su estado e historial, por ejemplo, si la tarea se ha completado, si el método asincrónico produjo una excepción o si se ha cancelado y cuál es el resultado final. El operador `await` tiene acceso a esas propiedades llamando a métodos en el objeto devuelto mediante el método `GetAwaiter`.  
  
Si espera un método asincrónico que devuelve una tarea y causa una excepción, el operador `await` volverá a generar la excepción.  
  
Si espera un método asincrónico que devuelve una tarea y se cancela, el operador `await` volverá a generar <xref:System.OperationCanceledException>.  
  
Una única tarea en estado de error puede reflejar varias excepciones. Por ejemplo, la tarea podría ser el resultado de una llamada a <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=fullName>. Cuando espera dicha tarea, la operación await vuelve a generar únicamente una de las excepciones. Sin embargo, no se puede predecir cuál de las excepciones se vuelve a generar.  
  
Para obtener ejemplos de control de errores en métodos asincrónicos, vea [try-catch](../../../csharp/language-reference/keywords/try-catch.md).  
  
## <a name="example"></a>Ejemplo  
En el ejemplo siguiente se devuelve el número total de caracteres en las páginas cuyas direcciones URL se pasan como argumentos de línea de comandos. En el ejemplo se llama al método `GetPageLengthsAsync`, que se marca con la palabra clave `async`. El método `GetPageLengthsAsync` a su vez usa la palabra clave `await` para esperar llamadas del método <xref:System.Net.Http.HttpClient.GetStringAsync%2A?displayProperty=fullName>.  

[!code-cs[await-example](../../../../samples/snippets/csharp/language-reference/keywords/await/await2.cs)]  

Como no se admite el uso de `async` y `await` en un punto de entrada de la aplicación, no podemos aplicar el atributo `async` al método `Main`, ni podemos esperar la llamada al método `GetPageLengthsAsync`. Podemos garantizar que el método `Main` espera a que se complete la operación asincrónica recuperando el valor de la propiedad <xref:System.Threading.Tasks.Task%601.Result?displayProperty=fullName>. Para las tareas que no devuelven un valor, puede llamar al método <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=fullName>. 

## <a name="see-also"></a>Vea también  
[Programación asincrónica con async y await](../../../csharp/programming-guide/concepts/async/index.md)   
[Walkthrough: Accessing the Web by Using Async and Await](../../../csharp/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)  (Tutorial: Acceso a la web con Async y Await)  
[async](../../../csharp/language-reference/keywords/async.md)

