---
title: "C&#243;mo: Generar el modelo de objetos en Visual Basic o C# | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a0c73b33-5650-420c-b9dc-f49310c201ee
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# C&#243;mo: Generar el modelo de objetos en Visual Basic o C# #
En [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], un modelo de objetos en un lenguaje de programación se asigna a una base de datos relacional.  Hay dos herramientas disponibles para generar automáticamente un modelo de [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\# a partir de los metadatos de una base de datos existente.  
  
-   Si programa en [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], puede utilizar el [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] para generar un modelo de objetos.  [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] proporciona una interfaz de usuario completa que le ayuda a generar un modelo de objetos de [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
-   Herramienta de línea de comandos SQLMetal  Para obtener más información, consulte [SqlMetal.exe \(Herramienta de generación de código\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
    > [!NOTE]
    >  Si no tiene una base de datos existente y desear crear una a partir de un modelo de objetos, puede crear el modelo de objetos mediante el editor de código y <xref:System.Data.Linq.DataContext.CreateDatabase%2A>.  Para obtener más información, consulte [Cómo: Crear dinámicamente una base de datos](../../../../../../docs/framework/data/adonet/sql/linq/how-to-dynamically-create-a-database.md).  
  
 La documentación de [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] proporciona ejemplos de cómo generar un modelo de objetos de [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] or C\# con [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)].  En la información siguiente se proporcionan ejemplos del uso de la herramienta de línea de comandos de SQLMetal.  Para obtener más información, consulte [SqlMetal.exe \(Herramienta de generación de código\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Ejemplo  
 La línea de comandos de SQLMetal mostrada en el ejemplo siguiente genera código de [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] como el modelo de objetos basado en atributos de la base de datos de ejemplo Northwind.  Se presentan también los procedimientos almacenados y las funciones.  
  
```  
sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions  
```  
  
## Ejemplo  
 La línea de comandos de SQLMetal mostrada en el ejemplo siguiente genera código de C\# como el modelo de objetos basado en atributos de la base de datos de ejemplo Northwind.  Se presentan también los procedimientos almacenados y las funciones, y los nombres de tabla se pluralizan automáticamente.  
  
```  
sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize  
```  
  
## Vea también  
 [Guía de programación](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)   
 [Modelo de objetos de LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [Aprender mediante tutoriales](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)   
 [Cómo: Personalizar clases de entidad mediante el editor de código](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)   
 [Asignación basada en atributos](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md)   
 [SqlMetal.exe \(Herramienta de generación de código\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)   
 [Asignación externa](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md)   
 [Descargar bases de datos de ejemplo](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [Crear el modelo de objetos](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)