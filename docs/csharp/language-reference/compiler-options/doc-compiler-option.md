---
title: -doc (Opciones del compilador de C#)
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- FileProperties.BuildAction
- /doc
dev_langs:
- CSharp
helpviewer_keywords:
- comments, C# code
- XML documentation [C#], comments in source files
- doc compiler option [C#]
- Visual C#, XML documentation for
- -doc compiler option [C#]
- /doc compiler option [C#]
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
caps.latest.revision: 19
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
ms.openlocfilehash: 58608c1301b2df3286c1f8a1de189f6256b19052
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="doc-c-compiler-options"></a>/doc (Opciones del compilador de C#)
La opción **/doc** permite insertar comentarios de documentación en un archivo XML.  
  
## <a name="syntax"></a>Sintaxis  
  
```console  
/doc:file  
```  
  
## <a name="arguments"></a>Argumentos  
 `file`  
 Archivo de salida para XML, que se llena con los comentarios de los archivos de código fuente de la compilación.  
  
## <a name="remarks"></a>Comentarios  
 En los archivos de código fuente, es posible procesar y agregar al archivo XML los comentarios de documentación que preceden a lo siguiente:  
  
-   Tipos definidos por el usuario como una [clase](../../../csharp/language-reference/keywords/class.md), un [delegado](../../../csharp/language-reference/keywords/delegate.md) o una [interfaz](../../../csharp/language-reference/keywords/interface.md)  
  
-   Miembros como un campo, un [evento](../../../csharp/language-reference/keywords/event.md), una [propiedad](../../../csharp/programming-guide/classes-and-structs/using-properties.md) o un método  
  
 El archivo de código fuente que contiene Main es la primera salida del XML.  
  
 Para usar el archivo .xml generado con la función [IntelliSense](/visualstudio/ide/using-intellisense), deje que el nombre del archivo .xml sea igual que el del ensamblado que quiere admitir y, después, asegúrese de que el archivo .xml se encuentra en el mismo directorio que el ensamblado. De este modo, cuando se hace referencia al ensamblado en el proyecto de Visual Studio, también se encuentra el archivo .xml. Vea [Proporcionar comentarios del código](/visualstudio/ide/supplying-xml-code-comments) para obtener más información.  
  
 A menos que compile con [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), `file` contendrá etiquetas \<assembly>\</assembly> que especifican el nombre del archivo que contiene el manifiesto del ensamblado para el archivo de salida de la compilación.  
  
> [!NOTE]
>  La opción /doc se aplica a todos los archivos de entrada o, si se establece en la configuración del proyecto, a todos los archivos del proyecto. Para deshabilitar las advertencias relacionadas con los comentarios de documentación para un archivo específico o una sección de código, use [#pragma warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning.md).  
  
 Vea [Etiquetas recomendadas para comentarios de documentación ](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md) para conocer las maneras de generar documentación a partir de comentarios en el código.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para establecer esta opción del compilador en el entorno de desarrollo de Visual Studio  
  
1.  Abra la página **Propiedades** del proyecto.  
  
2.  Haga clic en la pestaña **Compilar**.  
  
3.  Modifique la propiedad **Archivo de documentación XML**.  
  
 Para obtener información sobre cómo establecer esta opción del compilador mediante programación, vea <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Opciones del compilador de C#](../../../csharp/language-reference/compiler-options/index.md)   
 [Administrar propiedades de soluciones y proyectos](/visualstudio/ide/managing-project-and-solution-properties)

