---
title: "Conjuntos de nodos en transformaciones | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: ad034f0e-ff8b-4a71-9a4c-528c754263c4
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# Conjuntos de nodos en transformaciones
Los conjuntos de nodos son uno de los cuatro tipos de datos básicos devueltos por las expresiones XPath. Un conjunto de nodos, que es una colección no ordenada de nodos sin duplicados, creada por orden de documento, puede asignarse a una variable en una hoja de estilos.  
  
> [!NOTE]
>  La clase <xref:System.Xml.Xsl.XslTransform> es obsoleta en [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]. Puede llevar a cabo Extensible Stylesheet Language for Transformations \(XSLT\) mediante la clase <xref:System.Xml.Xsl.XslCompiledTransform>. Para obtener más información, vea [Uso de la clase XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) y [Migración desde la clase XslTransform](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md).  
  
 Los conjuntos de nodos son uno de los cuatro tipos de datos básicos devueltos por las expresiones XPath. Un conjunto de nodos, que es una colección no ordenada de nodos sin duplicados, creada por orden de documento, puede asignarse a una variable en una hoja de estilos. Este conjunto de nodos, que es el resultado de una expresión XPath utilizada en un atributo `select` de una transformación, se comporta del mismo modo que un conjunto de nodos de DOM. Puede navegar por un conjunto de nodos mediante el conjunto de métodos que se muestra en [Navegación por un conjunto de nodos con XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md), a diferencia del fragmento del árbol de resultados, que utiliza <xref:System.Xml.XPath.XPathNodeIterator> para navegar.  
  
 En el siguiente ejemplo de código se muestra la forma de iterar por un conjunto de nodos cuando un elemento `variable` o `parameter` de una hoja de estilos se evalúa como un conjunto de nodos.  
  
## Hoja de estilos  
  
```  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">  
  
    <xsl:variable name="x" select="bookstore/book/title"></xsl:variable>  
  
    <xsl:template match="/">  
        <xsl:for-each select="$x">  
            ******  
            <xsl:value-of select="."></xsl:value-of>  
            ******  
        </xsl:for-each>  
    </xsl:template>  
  
</xsl:stylesheet>  
```  
  
## Entrada  
  
```  
<bookstore>  
   <book style="autobiography">  
      <title>Seven Years in Trenton</title>  
   </book>  
  
   <book style="autobiography">  
      <title>Seven Years in Trenton2</title>  
   </book>  
  
   <book style="textbook">  
      <title>History of Trenton Vol 3</title>  
   </book>  
</bookstore>  
```  
  
## Salida  
  
```  
******  
Seven Years in Trenton  
******  
  
******  
Seven Years in Trenton2  
******  
  
******  
History of Trenton Vol 3  
******  
```  
  
## Vea también  
 <xref:System.Xml.XPath.XPathNodeIterator>   
 [Transformaciones XSLT con la clase XslTransform](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [La clase XslTransform implementa el procesador XSLT](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)