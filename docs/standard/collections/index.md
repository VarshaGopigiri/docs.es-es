---
title: Colecciones y estructuras de datos
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- grouping data in collections
- objects [.NET Framework], grouping in collections
- Array class, grouping data in collections
- threading [.NET Framework], safety
- Collections classes
- collections [.NET Framework]
ms.assetid: 60cc581f-1db5-445b-ba04-a173396bf872
caps.latest.revision: 36
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2538f300ef2af6051c2750e749674c8ea7145530
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="collections-and-data-structures"></a>Colecciones y estructuras de datos
A menudo, los datos similares pueden controlarse de forma más eficaz si se almacenan y manipulan como si fuesen una colección. Puede usar la clase <xref:System.Array?displayProperty=fullName> o las clases de los espacios de nombres <xref:System.Collections>, <xref:System.Collections.Generic>, <xref:System.Collections.Concurrent> y System.Collections.Immutable para agregar, quitar y modificar elementos individuales o intervalos de elementos de una colección.  
  
 Hay dos tipos principales de colecciones: las colecciones genéricas y las colecciones no genéricas. Las colecciones genéricas se agregaron en la versión 2.0 de.NET Framework y son colecciones con seguridad de tipos en tiempo de compilación. Debido a esto, las colecciones genéricas normalmente ofrecen un mejor rendimiento. Las colecciones genéricas aceptan un parámetro de tipo cuando se construyen y no requieren conversiones con el tipo <xref:System.Object> al agregar o quitar elementos de la colección.  Además, la mayoría de colecciones genéricas son compatibles con aplicaciones de la [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)]. Las colecciones no genéricas almacenan elementos como <xref:System.Object>, requieren conversión y la mayoría no son compatibles con el desarrollo de aplicaciones de la [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)]. Sin embargo, puede que vea colecciones no genéricas en código antiguo.  
  
 A partir de [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], las colecciones del espacio de nombres <xref:System.Collections.Concurrent> proporcionan operaciones eficaces y seguras para subprocesos con el fin de obtener acceso a los elementos de la colección desde varios subprocesos. Las clases de colección inmutables en el espacio de nombres System.Collections.Immutable ([NuGet package](https://www.nuget.org/packages/System.Collections.Immutable)) son intrínsecamente seguras para los subprocesos, ya que las operaciones se realizan en una copia de la colección original, mientras que la colección original no se puede modificar.  
  
  
<a name="BKMK_Commoncollectionfeatures"></a>   
## <a name="common-collection-features"></a>Características comunes de las colecciones  
 Todas las colecciones ofrecen métodos para agregar, quitar o buscar elementos en la colección. Además, todas las colecciones que implementan directa o indirectamente las interfaces <xref:System.Collections.ICollection> o <xref:System.Collections.Generic.ICollection%601> comparten estas características:  
  
-   **Capacidad para enumerar la colección**  
  
     Las colecciones de .NET Framework implementan <xref:System.Collections.IEnumerable?displayProperty=fullName> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> para permitir procesar una iteración en la colección. Un enumerador puede considerarse como un puntero móvil para cualquier elemento de la colección. Las instrucciones [foreach, in](~/docs/csharp/language-reference/keywords/foreach-in.md) y [For Each...Next](~/docs/visual-basic/language-reference/statements/for-each-next-statement.md) usan el enumerador expuesto por el método <xref:System.Collections.IEnumerable.GetEnumerator%2A> y ocultan la complejidad que supone manipular el enumerador. Además, cualquier colección que implementa <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> se considera un *tipo consultable* y se puede consultar con LINQ. Las consultas LINQ proporcionan un modelo común para acceder a los datos. Por lo general, son más concisas y legibles que los bucles `foreach` estándar y ofrecen capacidad de filtrado, ordenación y agrupación. Las consultas LINQ también pueden mejorar el rendimiento. Para más información, consulte [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9), [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md) e [Introducción a las consultas LINQ (C#)](~/docs/csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
-   **Capacidad de copiar el contenido de la colección en una matriz**  
  
     Todas las colecciones se pueden copiar en una matriz mediante el método **CopyTo**; sin embargo, el orden de los elementos de la nueva matriz se basa en la secuencia en la que los devuelve el enumerador. La matriz resultante siempre es unidimensional con un límite inferior de cero.  
  
 Además, muchas clases de colecciones contienen las siguientes características:  
  
-   **Propiedades de capacidad y recuento**  
  
     La capacidad de una colección es el número de elementos que puede contener. El recuento de una colección es el número de elementos que realmente contiene. Algunas colecciones ocultan la capacidad, el recuento, o ambos.  
  
     La mayoría de las colecciones expanden automáticamente su capacidad cuando se alcanza la capacidad actual. La memoria se reasigna y los elementos de la antigua colección se copian en la nueva. Esto reduce el código necesario para utilizar la colección; sin embargo, el rendimiento de la colección podría verse afectado negativamente. Por ejemplo, en <xref:System.Collections.Generic.List%601>, si <xref:System.Collections.Generic.List%601.Count%2A> es menor que <xref:System.Collections.Generic.List%601.Capacity%2A>, el agregar un elemento supone una operación O(1). Si es necesario aumentar la capacidad para alojar el nuevo elemento, agregar un elemento se convierte en una operación O(n), donde n es <xref:System.Collections.Generic.List%601.Count%2A>. La mejor manera de evitar el rendimiento deficiente provocado por múltiples reasignaciones es establecer la capacidad inicial el tamaño estimado de la colección.  
  
     <xref:System.Collections.BitArray> es un caso especial; su capacidad es igual que su longitud, que es la misma que su recuento.  
  
-   **Límite inferior coherente**  
  
     El límite inferior de una colección es el índice de su primer elemento. Todas las colecciones indizadas en el espacio de nombres <xref:System.Collections> tienen un límite inferior de cero, lo que significa que están indizadas en 0. De forma predeterminada, <xref:System.Array> tiene un límite inferior de cero, pero se puede definir un límite inferior diferente mediante la creación de una instancia de la clase **Array** con <xref:System.Array.CreateInstance%2A?displayProperty=fullName>.  
  
-   **Sincronización para el acceso de varios subprocesos** (solo clases <xref:System.Collections>).  
  
     Los tipos de colecciones no genéricas del espacio de nombres <xref:System.Collections> proporcionan una seguridad de subprocesos con sincronización; normalmente se exponen a través de los miembros <xref:System.Collections.ICollection.SyncRoot%2A> y <xref:System.Collections.ICollection.IsSynchronized%2A>. Estas colecciones no son seguras para subprocesos de forma predeterminada. Si necesita un acceso multiproceso escalable y eficaz a una colección, utilice una de las clases del espacio de nombres <xref:System.Collections.Concurrent> o considere el uso de una colección inmutable. Para obtener más información, consulte [Colecciones seguras para subprocesos](../../../docs/standard/collections/thread-safe/index.md).  
  
<a name="BKMK_Choosingacollection"></a>   
## <a name="choosing-a-collection"></a>Elegir una colección  
 En general, debería utilizar colecciones genéricas. En la tabla siguiente se describen algunos escenarios habituales de las colecciones y las clases de colección que puede utilizar en esos escenarios. Si es la primera vez que usa colecciones genéricas, con esta tabla le será más fácil elegir la colección genérica que funciona mejor para su tarea.  
<!-- todo: All code-formatted API refs in the table need to be changed into links -->  
|Deseo...|Opciones de colección genérica|Opciones de colección no genérica|Opciones de colección de subprocesos o inmutable|  
|-|-|-|-|  
|Almacenar elementos como pares clave/valor para una consulta rápida por clave|<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>|<xref:System.Collections.Hashtable><br /><br /> (Colección de pares clave/valor que se organizan en función del código hash de la clave).|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName><br /><br /> <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=fullName><br /><br /> `ImmutableDictionary(TKey, TValue) Class`|  
|Acceso a elementos por índice|<xref:System.Collections.Generic.List%601?displayProperty=fullName>|<xref:System.Array?displayProperty=fullName><br /><br /> <xref:System.Collections.ArrayList?displayProperty=fullName>|`ImmutableList(T) Class`<br /><br /> `ImmutableArray Class`|  
|Utilizar elementos FIFO (el primero en entrar es el primero en salir)|<xref:System.Collections.Generic.Queue%601?displayProperty=fullName>|<xref:System.Collections.Queue?displayProperty=fullName>|<xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=fullName><br /><br /> `ImmutableQueue(T) Class`|  
|Utilizar datos LIFO (el último en entrar es el primero en salir)|<xref:System.Collections.Generic.Stack%601?displayProperty=fullName>|<xref:System.Collections.Stack?displayProperty=fullName>|<xref:System.Collections.Concurrent.ConcurrentStack%601?displayProperty=fullName><br /><br /> `ImmutableStack(T) Class`|  
|Acceso a elementos de forma secuencial|<xref:System.Collections.Generic.LinkedList%601?displayProperty=fullName>|Sin recomendación|Sin recomendación|  
|Recibir notificaciones cuando se quitan o se agregan elementos a la colección. (implementa <xref:System.ComponentModel.INotifyPropertyChanged> y <xref:System.Collections.Specialized.INotifyCollectionChanged?displayProperty=fullName>)|<xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=fullName>|Sin recomendación|Sin recomendación|  
|Una colección ordenada|<xref:System.Collections.Generic.SortedList%602?displayProperty=fullName>|<xref:System.Collections.SortedList?displayProperty=fullName>|`ImmutableSortedDictionary(TKey, TValue) Class`<br /><br /> `ImmutableSortedSet(T) Class`|  
|Un conjunto de funciones matemáticas|<xref:System.Collections.Generic.HashSet%601?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.SortedSet%601?displayProperty=fullName>|Sin recomendación|`ImmutableHashSet(T) Class`<br /><br /> `ImmutableSortedSet(T) Class`|  
  
<a name="BKMK_RelatedTopics"></a>   
## <a name="related-topics"></a>Temas relacionados  
  
|Título|Descripción|  
|-----------|-----------------|  
|[Seleccionar una clase de colección](../../../docs/standard/collections/selecting-a-collection-class.md)|Describe las diferentes colecciones y le ayuda a seleccionar una para su escenario.|  
|[Tipos de colección utilizados normalmente](../../../docs/standard/collections/commonly-used-collection-types.md)|Describe los tipos de colección genéricos y no genéricos más utilizados, como <xref:System.Array?displayProperty=fullName>, <xref:System.Collections.Generic.List%601?displayProperty=fullName> y <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>.|  
|[Cuándo utilizar colecciones genéricas](../../../docs/standard/collections/when-to-use-generic-collections.md)|Describe el uso de los tipos de colección genéricos.|  
|[Comparaciones y ordenaciones en colecciones](../../../docs/standard/collections/comparisons-and-sorts-within-collections.md)|Describe el uso de las comparaciones de igualdad y ordenación en las colecciones.|  
|[Tipos de colecciones ordenadas](../../../docs/standard/collections/sorted-collection-types.md)|Describe las características y el funcionamiento de colecciones ordenadas.|  
|[Tipos de las colecciones Hashtable y Dictionary](../../../docs/standard/collections/hashtable-and-dictionary-collection-types.md)|Describe las características de los tipos de diccionarios basados en hash genéricos y no genéricos.|  
|[Colecciones seguras para subprocesos](../../../docs/standard/collections/thread-safe/index.md)|Describe los tipos de colección, como <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=fullName> y <xref:System.Collections.Concurrent.ConcurrentBag%601?displayProperty=fullName>, que admiten un acceso simultáneo seguro y eficaz desde varios subprocesos.|  
|System.Collections.Immutable|Presenta las colecciones inalterables y proporciona vínculos a los tipos de colección.|  
  
<a name="BKMK_Reference"></a>   
## <a name="reference"></a>Referencia  
 <xref:System.Array?displayProperty=fullName>  
  
 <xref:System.Collections?displayProperty=fullName>  
  
 <xref:System.Collections.Concurrent?displayProperty=fullName>  
  
 <xref:System.Collections.Generic?displayProperty=fullName>  
  
 <xref:System.Collections.Specialized?displayProperty=fullName>  
  
 <xref:System.Linq?displayProperty=fullName>  
  
 System.Collections.Immutable

