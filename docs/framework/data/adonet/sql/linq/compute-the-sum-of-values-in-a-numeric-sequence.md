---
title: "C&#243;mo: Calcular la suma de los valores de una secuencia num&#233;rica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24e335b0-984e-4825-8721-0a91b533b7c3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# C&#243;mo: Calcular la suma de los valores de una secuencia num&#233;rica
Utilice el operador <xref:System.Linq.Enumerable.Sum%2A> para calcular la suma de los valores numéricos de una secuencia.  
  
 Tenga en cuenta las características siguientes del operador `Sum` en [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:  
  
-   El operador de consulta estándar de agregado `Sum` se evalúa como cero para una secuencia vacía o una secuencia que solo contiene valores nulos.  En [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], la semántica de SQL se mantiene invariable.  Por esta razón, `Sum` se evalúa como Null en lugar de cero en el caso de secuencias vacías o secuencias que solo contienen valores nulos.  
  
-   En [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] se aplican las restricciones de SQL para los agregados en los resultados intermedios.  La suma de cantidades enteras de 32 bits no se calcula utilizando resultados de 64 bits, y puede producirse un desbordamiento en la conversión que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] realiza de `Sum`.  Esta posibilidad existe aun cuando la implementación del operador de consulta estándar no produzca un desbordamiento para la secuencia en memoria correspondiente.  
  
## Ejemplo  
 En el ejemplo siguiente se busca el flete total de todos los pedidos de la tabla `Order`.  
  
 Si ejecuta esta consulta en la base de datos de ejemplo Northwind, el resultado es: `64942.6900`.  
  
 [!code-csharp[DLinqQueryExamples#12](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#12)]
 [!code-vb[DLinqQueryExamples#12](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#12)]  
  
## Ejemplo  
 En el ejemplo siguiente se busca el número total de unidades pedidas para todos los productos.  
  
 Si ejecuta esta consulta en la base de datos de ejemplo Northwind, el resultado es: `780`.  
  
 Tenga en cuenta que debe convertir los tipos `short` \(por ejemplo, `UnitsOnOrder`\) porque `Sum` no tiene una sobrecarga para ellos.  
  
 [!code-csharp[DLinqQueryExamples#13](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryExamples/cs/Program.cs#13)]
 [!code-vb[DLinqQueryExamples#13](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryExamples/vb/Module1.vb#13)]  
  
## Vea también  
 [Consultas de agregado](../../../../../../docs/framework/data/adonet/sql/linq/aggregate-queries.md)   
 [Descargar bases de datos de ejemplo](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)