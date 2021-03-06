---
title: Agrupar los resultados de consultas
description: "Cómo agrupar los resultados."
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 2e4ec27f-06fb-4de7-8973-0189906d4520
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1c1639651699afbe5fb768db26b98a9b2d734315
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="group-query-results"></a>Agrupar los resultados de consultas

La agrupación es una de las capacidades más eficaces de LINQ. Los ejemplos siguientes muestran cómo agrupar datos de varias maneras:  
  
-   Por una sola propiedad.  
  
-   Por la primera letra de una propiedad de cadena.  
  
-   Por un intervalo numérico calculado.  
  
-   Por un predicado booleano u otra expresión.  
  
-   Por una clave compuesta.  
  
 Además, las dos últimas consultas proyectan sus resultados en un nuevo tipo anónimo que solo contiene el nombre y los apellidos del estudiante. Para obtener más información, vea la [cláusula group](../language-reference/keywords/group-clause.md).  
  
## <a name="example"></a>Ejemplo  
 Todos los ejemplos de este tema usan los siguientes orígenes de datos y clases auxiliares.  
  
 [!code-cs[csProgGuideLINQ#15](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_1.cs)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo agrupar elementos de origen mediante una propiedad única del elemento como la clave de grupo. En este caso, la clave es una `string`, el apellido del alumno. También es posible usar una subcadena para la clave. La operación de agrupación usa al comparador de igualdad predeterminado para el tipo.  
  
 Pegue el método siguiente en la clase `StudentClass`. Cambie la instrucción de llamada en el método `Main` por `sc.GroupBySingleProperty()`.  
  
 [!code-cs[csProgGuideLINQ#17](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_2.cs)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo agrupar elementos de origen mediante algo distinto a una propiedad del objeto para la clave de grupo. En este ejemplo, la clave es la primera letra del apellido del alumno.  
  
 Pegue el método siguiente en la clase `StudentClass`. Cambie la instrucción de llamada en el método `Main` por `sc.GroupBySubstring()`.  
  
 [!code-cs[csProgGuideLINQ#18](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_3.cs)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo agrupar elementos de origen mediante un intervalo numérico como la clave de grupo. Después, la consulta proyecta los resultados en un tipo anónimo que solo contiene el nombre, los apellidos y el intervalo de percentil al que pertenece el alumno. Se usa un tipo anónimo porque no es necesario usar el objeto `Student` completo para mostrar los resultados. `GetPercentile` es una función auxiliar que calcula un percentil basado en la puntuación media del alumno. El método devuelve un entero entre 0 y 10.  
  
 [!code-cs[csProgGuideLINQ#50](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_4.cs)]  
  
 Pegue el método siguiente en la clase `StudentClass`. Cambie la instrucción de llamada en el método `Main` por `sc.GroupByRange()`.  
  
 [!code-cs[csProgGuideLINQ#19](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_5.cs)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo agrupar elementos de origen usando una expresión de comparación booleana. En este ejemplo, la expresión booleana comprueba si la puntuación media del examen de un alumno es mayor de 75. Como en los ejemplos anteriores, los resultados se proyectan en un tipo anónimo porque el elemento de origen completo no es necesario. Tenga en cuenta que las propiedades del tipo anónimo se convierten en propiedades en el miembro `Key` y puede tener acceso a ellas por nombre cuando se ejecuta la consulta.  
  
 Pegue el método siguiente en la clase `StudentClass`. Cambie la instrucción de llamada en el método `Main` por `sc.GroupByBoolean()`.  
  
 [!code-cs[csProgGuideLINQ#20](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_6.cs)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo usar un tipo anónimo para encapsular una clave que contiene varios valores. En este ejemplo, el primer valor de clave es la primera letra del apellido del alumno. El segundo valor de clave es un valor booleano que especifica si el alumno obtuvo una nota superior a 85 en el primer examen. Los grupos se pueden ordenar por cualquier propiedad de la clave.  
  
 Pegue el método siguiente en la clase `StudentClass`. Cambie la instrucción de llamada en el método `Main` por `sc.GroupByCompositeKey()`.  
  
 [!code-cs[csProgGuideLINQ#21](../../../samples/snippets/csharp/concepts/linq/how-to-group-query-results_7.cs)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.Linq.Enumerable.GroupBy%2A>   
 <xref:System.Linq.IGrouping%602>   
 [Expresiones de consulta LINQ](index.md)   
 [group (Cláusula)](../language-reference/keywords/group-clause.md)   
 [Tipos anónimos](../programming-guide/classes-and-structs/anonymous-types.md)   
 [Realizar una subconsulta en una operación de agrupación](perform-a-subquery-on-a-grouping-operation.md)   
 [Crear un grupo anidado](create-a-nested-group.md)   
 [Agrupación de datos](../programming-guide/concepts/linq/grouping-data.md)

