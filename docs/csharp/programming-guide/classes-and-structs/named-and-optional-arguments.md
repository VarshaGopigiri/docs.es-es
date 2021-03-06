---
title: "Argumentos opcionales y con nombre (Guía de programación de C#)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- namedParameter_CSharpKeyword
- cs_namedParameter
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], named
- named arguments [C#]
- arguments [C#], named
- optional arguments [C#]
- arguments [C#], optional
- parameters [C#], optional
- named and optional arguments [C#]
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
caps.latest.revision: 43
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
ms.sourcegitcommit: 0dc2fcee3903b80816c98bab47e2b9a2e5ef78b0
ms.openlocfilehash: a7f05e3e0b19bf6457989f8db2b46741cf6b28c1
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="named-and-optional-arguments-c-programming-guide"></a>Argumentos opcionales y con nombre (Guía de programación de C#)
[!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] introduce argumentos opcionales y con nombre. Los *argumentos con nombre* permiten especificar un argumento para un parámetro concreto asociando el argumento al nombre del parámetro y no a la posición del parámetro en la lista de parámetros. Los *argumentos opcionales* permiten omitir argumentos para algunos parámetros. Ambas técnicas se pueden usar con métodos, indexadores, constructores y delegados.  
  
 Cuando se usan argumentos opcionales y con nombre, los argumentos se evalúan por el orden en que aparecen en la lista de argumentos, no en la lista de parámetros.  
  
 Los parámetros opcionales y con nombre, cuando se usan conjuntamente, solo permiten especificar argumentos para algunos parámetros de una lista de parámetros opcionales. Esta funcionalidad facilita enormemente las llamadas a interfaces COM, como las API de automatización de Microsoft Office.  
  
## <a name="named-arguments"></a>Argumentos con nombre  
 Los argumentos con nombre le liberan de la necesidad de recordar o buscar el orden de los parámetros de la lista de parámetros de los métodos llamados. El parámetro de cada argumento se puede especificar por nombre de parámetro. Por ejemplo, una función que calcula el índice de masa corporal (IMC) se puede llamar de manera estándar enviando argumentos de peso y estatura por posición en el orden que define la función.  
  
 `CalculateBMI(123, 64);`  
  
 Si no recuerda el orden de los parámetros pero conoce sus nombres, puede enviar los argumentos en cualquier orden, primero el peso o primero la estatura.  
  
 `CalculateBMI(weight: 123, height: 64);`  
  
 `CalculateBMI(height: 64, weight: 123);`  
  
 Los argumentos con nombre también mejoran la legibilidad del código al identificar lo que cada argumento representa.  
  
 Un argumento con nombre puede seguir a los argumentos posicionales, tal y como se muestra aquí.  
  
 `CalculateBMI(123, height: 64);`  
  
 Pero un argumento posicional no puede seguir a un argumento con nombre. La instrucción siguiente genera un error del compilador.  
  
 `//CalculateBMI(weight: 123, 64);`  
  
## <a name="example"></a>Ejemplo  
 El código siguiente implementa los ejemplos de esta sección.  
  
 [!code-cs[csProgGuideNamedAndOptional#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_1.cs)]  
  
## <a name="optional-arguments"></a>Argumentos opcionales  
 La definición de un método, constructor, indexador o delegado puede especificar que sus parámetros son necesarios o que son opcionales. Todas las llamadas deben proporcionar argumentos para todos los parámetros necesarios, pero pueden omitir los argumentos para los parámetros opcionales.  
  
 Cada parámetro opcional tiene un valor predeterminado como parte de su definición. Si no se envía ningún argumento para ese parámetro, se usa el valor predeterminado. Un valor predeterminado debe ser uno de los siguientes tipos de expresiones:  
  
-   una expresión constante;  
  
-   una expresión con el formato `new ValType()`, donde `ValType` es un tipo de valor, como [enum](../../../csharp/language-reference/keywords/enum.md) o [struct](../../../csharp/programming-guide/classes-and-structs/structs.md);  
  
-   una expresión con el formato [default(ValType)](../../../csharp/programming-guide/statements-expressions-operators/default-value-expressions.md), donde `ValType` es un tipo de valor.  
  
 Los parámetros opcionales se definen al final de la lista de parámetros después de los parámetros necesarios. Si el autor de la llamada proporciona un argumento para algún parámetro de una sucesión de parámetros opcionales, debe proporcionar argumentos para todos los parámetros opcionales anteriores. No se admiten espacios separados por comas en la lista de argumentos. Por ejemplo, en el código siguiente, el método de instancia `ExampleMethod` se define con un parámetro necesario y dos opcionales.  
  
 [!code-cs[csProgGuideNamedAndOptional#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_2.cs)]  
  
 La llamada siguiente a `ExampleMethod` genera un error del compilador, porque se proporciona un argumento para el tercer parámetro pero no para el segundo.  
  
 `//anExample.ExampleMethod(3, ,4);`  
  
 Pero si conoce el nombre del tercer parámetro, puede usar un argumento con nombre para realizar la tarea.  
  
 `anExample.ExampleMethod(3, optionalint: 4);`  
  
 IntelliSense usa corchetes para indicar parámetros opcionales, tal y como se muestra en la ilustración siguiente.  
  
 ![Información rápida de IntelliSense para el método ExampleMethod.](../../../csharp/programming-guide/classes-and-structs/media/optional_parameters.png "Optional_Parameters")  
Parámetros opcionales en ExampleMethod  
  
> [!NOTE]
>  También puede declarar parámetros opcionales con la clase <xref:System.Runtime.InteropServices.OptionalAttribute> de .NET. Los parámetros `OptionalAttribute` no requieren un valor predeterminado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, el constructor de `ExampleClass` tiene un solo parámetro, que es opcional. El método de instancia `ExampleMethod` tiene un parámetro necesario, `required`, y dos parámetros opcionales, `optionalstr` y `optionalint`. El código de `Main` muestra las distintas formas en que se pueden invocar el constructor y el método.  
  
 [!code-cs[csProgGuideNamedAndOptional#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_3.cs)]  
  
## <a name="com-interfaces"></a>Interfaces COM  
 Los argumentos opcionales y con nombre, además de compatibilidad con objetos dinámicos y otros avances, mejoran considerablemente la interoperabilidad con las API de COM, como las API de automatización de Office.  
  
 Por ejemplo, el método [AutoFormat](http://go.microsoft.com/fwlink/?LinkId=148201) de la interfaz [Range](http://go.microsoft.com/fwlink/?LinkId=148196) de Microsoft Office Excel tiene siete parámetros, todos ellos opcionales. Estos parámetros se muestran en la siguiente ilustración.  
  
 ![Información rápida de IntelliSense para el método AutoFormat.](../../../csharp/programming-guide/classes-and-structs/media/autoformat_parameters.png "AutoFormat_Parameters")  
Parámetros de AutoFormat  
  
 En C# 3.0 y versiones anteriores, se requiere un argumento para cada parámetro, tal y como se muestra en el ejemplo siguiente.  
  
 [!code-cs[csProgGuideNamedAndOptional#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_4.cs)]  
  
 Pero la llamada a `AutoFormat` se puede simplificar considerablemente mediante argumentos opcionales y con nombre, que se introducen en C# 4.0. Los parámetros opcionales y con nombre permiten omitir el argumento de un parámetro opcional si no se quiere cambiar el valor predeterminado del parámetro. En la siguiente llamada, solo se especifica un valor para uno de los siete parámetros.  
  
 [!code-cs[csProgGuideNamedAndOptional#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_5.cs)]  
  
 Para obtener más información y ejemplos, vea [How to: Use Named and Optional Arguments in Office Programming](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md) [Cómo: Usar argumentos opcionales y con nombre en la programación de Office (Guía de programación de C#)] y [How to: Access Office Interop Objects by Using Visual C# Features](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md) [Cómo: Tener acceso a objetos de interoperabilidad de Office mediante las características de Visual C# (Guía de programación de C#)].  
  
## <a name="overload-resolution"></a>Overload Resolution  
 El uso de argumentos opcionales y con nombre afecta a la resolución de sobrecarga de las maneras siguientes:  
  
-   Un método, indexador o constructor es un candidato para la ejecución si cada uno de sus parámetros es opcional o corresponde, por nombre o por posición, a un solo argumento de la instrucción de llamada y el argumento se puede convertir al tipo del parámetro.  
  
-   Si se encuentra más de un candidato, se aplican las reglas de resolución de sobrecarga de las conversiones preferidas a los argumentos que se especifican explícitamente. Los argumentos omitidos en parámetros opcionales se ignoran.  
  
-   Si dos candidatos se consideran igualmente correctos, la preferencia pasa a un candidato que no tenga parámetros opcionales cuyos argumentos se hayan omitido en la llamada. Se trata de una consecuencia de una preferencia general en la resolución de sobrecarga para los candidatos con menos parámetros.  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [How to: Use Named and Optional Arguments in Office Programming](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)  [Cómo: Usar argumentos opcionales y con nombre en la programación de Office (Guía de programación de C#)]  
 [Uso de tipo dinámico](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [Using Constructors](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)  [Uso de constructores (Guía de programación de C#)]  
 [Utilizar indizadores](../../../csharp/programming-guide/indexers/using-indexers.md)

