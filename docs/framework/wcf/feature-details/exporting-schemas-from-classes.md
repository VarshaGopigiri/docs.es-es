---
title: "Exportaci&#243;n de esquemas desde las clases | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, importación y exportación de esquemas"
  - "esquemas [WCF], exportación desde las clases"
  - "esquemas [WCF]"
  - "Clase XsdDataContractExporter "
  - "Clase XsdDataContractImporter"
ms.assetid: bb57b962-70c1-45a9-93d5-e721e340a13f
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Exportaci&#243;n de esquemas desde las clases
Para generar esquemas \(XSD\) de lenguaje de definición de esquemas XML a partir de las clases utilizadas en el modelo de contrato de datos, utilice la clase <xref:System.Runtime.Serialization.XsdDataContractExporter>. En este tema se describe el proceso para crear los esquemas.  
  
## Proceso de exportación  
 El proceso de exportación de esquema se inicia con uno o más tipos y genera un <xref:System.Xml.Schema.XmlSchemaSet> que describe la proyección de XML de estos tipos.  
  
 `XmlSchemaSet` forma parte del Modelo de objetos de esquemas  \(SOM\)[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] que representa un conjunto de documentos esquema XSD. Para crear documentos XSD a partir de `XmlSchemaSet`, utilice la colección de esquemas de la propiedad <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> de la clase `XmlSchemaSet`. A continuación, serialice cada objeto <xref:System.Xml.Schema.XmlSchema> mediante <xref:System.Xml.Serialization.XmlSerializer>.  
  
#### Exportar esquemas  
  
1.  Cree una instancia de <xref:System.Runtime.Serialization.XsdDataContractExporter>.  
  
2.  Opcional. Pase <xref:System.Xml.Schema.XmlSchemaSet> en el constructor. En este caso, el esquema generado durante la exportación del esquema se agrega a esta instancia <xref:System.Xml.Schema.XmlSchemaSet> en lugar de iniciarse con un <xref:System.Xml.Schema.XmlSchemaSet> en blanco.  
  
3.  Opcional. Llame a uno de los métodos <xref:System.Runtime.Serialization.XsdDataContractExporter.CanExport%2A>. El método determina si se puede exportar el tipo especificado. El método tiene las mismas sobrecargas que el método `Export` en el siguiente paso.  
  
4.  Llame a uno de los métodos <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A>. Hay tres sobrecargas que toman <xref:System.Type>, <xref:System.Collections.Generic.List%601> de los objetos `Type`, o <xref:System.Collections.Generic.List%601> de los objetos <xref:System.Reflection.Assembly>. En el último caso, se exportan todos los tipos de todos los ensamblados determinados.  
  
     Varias llamadas al método `Export` produce como resultado varios elementos que se agregan al mismo `XmlSchemaSet`. Un tipo no se genera en `XmlSchemaSet` si ya existe en este. Por consiguiente, llamar varias veces `Export`  en el mismo `XsdDataContractExporter` es preferible a crear varias instancias de la clase `XsdDataContractExporter`. Esto evita que se generen tipos de esquema duplicados.  
  
    > [!NOTE]
    >  Si se produce un error durante la exportación, `XmlSchemaSet` estará en un estado imprevisible.  
  
5.  Obtenga acceso a <xref:System.Xml.Schema.XmlSchemaSet> a través de la propiedad <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A>.  
  
## Exportar opciones.  
 Puede establecer la propiedad <xref:System.Runtime.Serialization.XsdDataContractExporter.Options%2A> de <xref:System.Runtime.Serialization.XsdDataContractExporter> a una instancia de <xref:System.Runtime.Serialization.ExportOptions> para administrar varios aspectos del proceso de exportación. En concreto, puede establecer las opciones siguientes:  
  
-   <xref:System.Runtime.Serialization.ExportOptions.KnownTypes%2A>. Esta colección de `Type` representa los tipos conocidos para los tipos que se van a exportar. \([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Tipos conocidos de contratos de datos](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)\). Estos tipos conocidos se exportan en cada llamada `Export` además de los tipos pasados al método `Export`.  
  
-   <xref:System.Runtime.Serialization.ExportOptions.DataContractSurrogate%2A>.<xref:System.Runtime.Serialization.IDataContractSurrogate> se puede proporcionar a través de esta propiedad que personalizará el proceso de exportación.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Suplentes de contratos de datos](../../../../docs/framework/wcf/extending/data-contract-surrogates.md). De forma predeterminada, no se utiliza ningún suplente.  
  
## Métodos auxiliares  
 Además de su función primaria de exportar el esquema, `XsdDataContractExporter` proporciona varios métodos auxiliares útiles que proporcionan información sobre los tipos. Se incluyen los siguientes:  
  
-   Método <xref:System.Runtime.Serialization.XsdDataContractExporter.GetRootElementName%2A>. Este método toma `Type` y devuelve <xref:System.Xml.XmlQualifiedName> que representa el nombre del elemento raíz y espacio de nombres que se utilizarían si este tipo se serializara como objeto raíz.  
  
-   Método <xref:System.Runtime.Serialization.XsdDataContractExporter.GetSchemaTypeName%2A>. Este método toma `Type` y devuelve <xref:System.Xml.XmlQualifiedName> que representa el nombre del tipo de esquema XSD que se utilizaría si este tipo se exportara al esquema. Para los tipos <xref:System.Xml.Serialization.IXmlSerializable> representados como tipos anónimos en el esquema, este método devuelve `null`.  
  
-   Método <xref:System.Runtime.Serialization.XsdDataContractExporter.GetSchemaType%2A>. Este método solo funciona con tipos <xref:System.Xml.Serialization.IXmlSerializable> representados como tipos anónimos en el esquema y devuelve `null` para el resto de tipos. Para los tipos anónimos, este método devuelve <xref:System.Xml.Schema.XmlSchemaType> que representa un `Type`determinado.  
  
 Las opciones de exportación afectan a todos estos métodos.  
  
## Vea también  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 <xref:System.Runtime.Serialization.XsdDataContractExporter>   
 [Importación y exportación de esquemas](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md)   
 [Importación del esquema para generar clases](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)