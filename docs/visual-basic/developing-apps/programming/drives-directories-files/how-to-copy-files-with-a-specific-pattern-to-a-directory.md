---
title: "Cómo: Copiar archivos con un modelo específico en un directorio en Visual Basic"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My.Computer.FileSystem.CopyFile method, copying files [Visual Basic]
- files, copying
- CopyFile method, copying files in Visual Basic
- I/O [Visual Basic], copying files
ms.assetid: f205d2ad-bbe5-4d55-8a40-acda21aa82dd
caps.latest.revision: 15
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 812fd59769da386f8d0b81eb80a4cd93c9764534
ms.contentlocale: es-es
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-copy-files-with-a-specific-pattern-to-a-directory-in-visual-basic"></a>Cómo: Copiar archivos con un modelo específico en un directorio en Visual Basic
El método <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A> devuelve una colección de solo lectura de cadenas que representan los nombres de ruta de acceso de los archivos. Puede usar el parámetro `wildCards` para especificar un patrón concreto.  
  
 Si no se encuentran archivos coincidentes, se devuelve una colección vacía.  
  
 Puede usar el método <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A> para copiar los archivos en un directorio.  
  
### <a name="to-copy-files-with-a-specific-pattern-to-a-directory"></a>Para copiar archivos con un patrón específico en un directorio  
  
1.  Use le método `GetFiles` para devolver la lista de archivos. En este ejemplo se devuelven todos los archivos .rtf del directorio especificado.  
  
     [!code-vb[VbFileIOMisc#36](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_1.vb)]  
  
2.  Use el método `CopyFile` para copiar los archivos. En este ejemplo se copian los archivos en el directorio denominado `testdirectory`.  
  
     [!code-vb[VbVbcnMyFileSystem#88](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_2.vb)]  
  
3.  Cierre la instrucción `For` con una instrucción `Next` .  
  
     [!code-vb[VbVbcnMyFileSystem#89](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_3.vb)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, que presenta los fragmentos de código anteriores de forma completa, se copian todos los archivos .rtf del directorio especificado en el directorio denominado `testdirectory`.  
  
 [!code-vb[VbFileIOMisc#37](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/how-to-copy-files-with-a-specific-pattern-to-a-directory_4.vb)]  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework  
 Las condiciones siguientes pueden provocar una excepción:  
  
-   La ruta de acceso no es válida por una de las siguientes razones: es una cadena de longitud cero, solo contiene un espacio en blanco, contiene caracteres no válidos o es una ruta de acceso de dispositivo (empieza por \\\\.\\) (<xref:System.ArgumentException>).  
  
-   La ruta de acceso no es válida porque es `Nothing` (<xref:System.ArgumentNullException>).  
  
-   El directorio no existe (<xref:System.IO.DirectoryNotFoundException>).  
  
-   El directorio apunta a un archivo existente (<xref:System.IO.IOException>).  
  
-   La ruta supera la longitud máxima definida por el sistema (<xref:System.IO.PathTooLongException>).  
  
-   Un nombre de archivo o de directorio de la ruta de acceso contiene un signo de dos puntos (:) o tiene un formato no válido (<xref:System.NotSupportedException>).  
  
-   El usuario no tiene los permisos necesarios para ver la ruta de acceso (<xref:System.Security.SecurityException>). El usuario no tiene los permisos necesarios (<xref:System.UnauthorizedAccessException>).  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.CopyFile%2A>   
 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy.GetFiles%2A>   
 [How to: Find Subdirectories with a Specific Pattern](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-find-subdirectories-with-a-specific-pattern.md)  (Cómo: Buscar subdirectorios con un modelo concreto en Visual Basic)  
 [Solución de problemas: Leer y escribir en archivos de texto](../../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)   
 [Obtener la colección de archivos de un directorio](../../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-get-the-collection-of-files-in-a-directory.md)

