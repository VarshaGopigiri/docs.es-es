---
title: "Entity Data Model: Tipos de datos primitivos | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7635168e-0566-4fdd-8391-7941b0d9f787
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Entity Data Model: Tipos de datos primitivos
Entity Data Model \(EDM\) admite un conjunto de tipos de datos primitivos abstractos \(como String, Boolean, Int32, etc.\) que se usan para definir [propiedades](../../../../docs/framework/data/adonet/property.md) en un modelo conceptual.  Estos tipos de datos primitivos son representantes de los tipos de datos primitivos reales compatibles con el entorno de almacenamiento o de hospedaje, como una base de datos de SQL Server o Common Language Runtime \(CLR\).  EDM no define la semántica de las operaciones o conversiones sobre los tipos de datos primitivos; es el propio entorno de almacenamiento o de hospedaje el que lo hace.  Normalmente, los tipos de datos primitivos de EDM se asignan a los tipos de datos primitivos correspondientes del entorno de almacenamiento o de hospedaje.  Para obtener información sobre cómo asigna Entity Framework tipos primitivos de EDM a tipos de datos de SQL Server, vea [Tipos de SqlClient para Entity Framework](../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md).  
  
> [!NOTE]
>  EDM no admite colecciones de tipos de datos primitivos.  
  
 Para obtener información sobre los tipos de datos estructurados de EDM, vea [tipo de entidad](../../../../docs/framework/data/adonet/entity-type.md) y [tipo complejo](../../../../docs/framework/data/adonet/complex-type.md).  
  
## Tipos de datos primitivos admitidos en Entity Data Model  
 En la tabla siguiente se enumeran los tipos de datos primitivos admitidos por EDM.  Dicha tabla también incluye las [facetas](../../../../docs/framework/data/adonet/facet.md) que se pueden aplicar a cada uno de los tipos.  
  
|Tipo de datos primitivo|Descripción|Facetas aplicables|  
|-----------------------------|-----------------|------------------------|  
|Binary|Contiene datos binarios.|MaxLength, FixedLength, Nullable, Default|  
|Boolean|Contiene el valor `true` o `false`.|Nullable, Default|  
|Byte|Contiene un valor entero de 8 bits sin signo.|Precision, Nullable, Default|  
|DateTime|Representa una fecha y hora.|Precision, Nullable, Default|  
|DateTimeOffset|Contiene una fecha y hora como un desplazamiento en minutos con respecto a GMT.|Precision, Nullable, Default|  
|Decimal|Contiene un valor numérico con una precisión y escala fijas.|Precision, Nullable, Default|  
|Double|Contiene un número de punto flotante con una precisión de 15 dígitos.|Precision, Nullable, Default|  
|Float|Contiene un número de punto flotante con una precisión de siete dígitos.|Precision, Nullable, Default|  
|Guid|Contiene un identificador único de 16 bytes.|Precision, Nullable, Default|  
|Int16|Contiene un valor entero de 16 bits con signo.|Precision, Nullable, Default|  
|Int32|Contiene un valor entero de 32 bits con signo.|Precision, Nullable, Default|  
|Int64|Contiene un valor entero de 64 bits con signo.|Precision, Nullable, Default|  
|SByte|Contiene un valor entero de 8 bits con signo.|Precision, Nullable, Default|  
|String|Contiene datos de caracteres.|Unicode, FixedLength, MaxLength, Collation, Precision, Nullable, Default|  
|Hora|Contiene una hora del día.|Precision, Nullable, Default|  
  
## Vea también  
 [Conceptos clave de Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)