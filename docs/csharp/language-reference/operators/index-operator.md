---
title: "Operador (Referencia de C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "[]_CSharpKeyword"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "operador de subíndice [C#]"
  - "[] (corchetes, operador) [C#]"
  - "[] (operador) [C#]"
  - "operador de indización [C#]"
ms.assetid: 5c16bb45-88f7-45ff-b42c-1af1972b042c
caps.latest.revision: 20
caps.handback.revision: 20
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Operador (Referencia de C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Los corchetes \(`[]`\) se utilizan para matrices, indizadores y atributos.  También se pueden utilizar con punteros.  
  
## Comentarios  
 Un tipo de matriz es un tipo seguido de `[]`:  
  
 [!code-cs[csRefOperators#43](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_1.cs)]  
  
 Para obtener acceso a un elemento de la matriz, el índice del elemento deseado se encierra entre corchetes:  
  
 [!code-cs[csRefOperators#44](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_2.cs)]  
  
 Se produce una excepción si el índice de la matriz está fuera del intervalo declarado.  
  
 El operador de indización de la matriz no se puede sobrecargar; no obstante, los tipos pueden definir indizadores y propiedades que aceptan uno o varios parámetros.  Los parámetros de indizador van entre corchetes, como los índices de matriz, pero en los primeros se puede declarar cualquier tipo de parámetro, mientras que los índices de matriz deben ser de tipo integral.  
  
 Por ejemplo, .NET Framework define un tipo `Hashtable` que asocia claves y valores de tipo arbitrario:  
  
 [!code-cs[csRefOperators#45](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_3.cs)]  
  
 Los corchetes también se utilizan para especificar [Atributos](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md):  
  
 [!code-cs[csRefOperators#46](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_4.cs)]  
  
 Puede utilizar los corchetes para indizar fuera de un puntero:  
  
 [!code-cs[csRefOperators#47](../../../csharp/language-reference/operators/codesnippet/CSharp/index-operator_5.cs)]  
  
 No obstante, tenga en cuenta que no se realiza una comprobación de los límites del índice.  
  
## Especificación del lenguaje C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Vea también  
 [Referencia de C\#](../../../csharp/language-reference/index.md)   
 [Guía de programación de C\#](../../../csharp/programming-guide/index.md)   
 [operadores de C\#](../../../csharp/language-reference/operators/index.md)   
 [Matrices](../../../csharp/programming-guide/arrays/index.md)   
 [Indizadores](../../../csharp/programming-guide/indexers/index.md)   
 [no seguras](../../../csharp/language-reference/keywords/unsafe.md)   
 [fixed \(Instrucción\)](../../../csharp/language-reference/keywords/fixed-statement.md)