---
title: "Creación de una biblioteca de clases con Visual Basic y .NET Core en Visual Studio 2017"
description: "Obtenga información sobre cómo crear una biblioteca de clases escrita en Visual Basic con Visual Studio 2017"
keywords: .NET Core, biblioteca de clases de .NET Standard, Visual Studio 2017, Visual Basic
author: rpetrusha
ms.author: ronpet
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-vb
ms.devlang: vb
ms.translationtype: HT
ms.sourcegitcommit: 3a25c1c3b540bac8ef963a8bbf708b0700c3e9e2
ms.openlocfilehash: a933e1eef6e4e9814aeba4206469a64563a7e91d
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---

# <a name="building-a-class-library-with-visual-basic-and-net-core-in-visual-studio-2017"></a>Creación de una biblioteca de clases con Visual Basic y .NET Core en Visual Studio 2017

Una *biblioteca de clases* define los tipos y los métodos que se llaman desde una aplicación. Una biblioteca de clases que tiene como destino .NET Standard 2.0, lo que permite que cualquier implementación .NET que admita esa versión de .NET Standard pueda llamar a su biblioteca. Cuando termine la biblioteca de clases, puede decidir si quiere distribuirla como un componente de terceros o si la quiere incluir como un componente empaquetado con una o varias aplicaciones.

> [!NOTE]
> Para ver una lista de las versiones de .NET Standard y las plataformas que admiten, vea [.NET Standard](../../standard/net-standard.md).

En este tema, se creará una sencilla biblioteca de utilidades que contiene un único método de control de cadenas. Se implementará como un [método de extensión](../../visual-basic/programming-guide/language-features/procedures/extension-methods.md) de modo que se pueda llamar como si fuera un miembro de la clase <xref:System.String>.

## <a name="creating-a-class-library-solution"></a>Creación de una solución de biblioteca de clases

Para empezar, se crea una solución para el proyecto de biblioteca de clases y sus proyectos relacionados. Una solución de Visual Studio solo sirve como contenedor de uno o varios proyectos. Para crear la solución:

1. En la barra de menús de Visual Studio, elija **Archivo** > **Nuevo** > **Proyecto**.

1. En el cuadro de diálogo **Nuevo proyecto**, expanda el nodo **Otros tipos de proyectos** y seleccione **Soluciones de Visual Studio**. Asigne a la solución el nombre "ClassLibraryProjects" y pulse el botón **Aceptar**.

   ![Cuadro de diálogo Nuevo proyecto](./media/library-with-visual-studio/newproject.png)

## <a name="creating-the-class-library-project"></a>Creación del proyecto de biblioteca de clases

Crear el proyecto de biblioteca de clases:

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el archivo de solución **ClassLibraryProjects** y seleccione **Agregar** > **Nuevo proyecto** en el menú contextual.

1. En el cuadro de diálogo **Agregar nuevo proyecto**, expanda el nodo **Visual Basic**, después seleccione el nodo **.NET Standard** seguido de la plantilla del proyecto **Biblioteca de clases (.NET Standard)**. En el cuadro de texto **Nombre**, escriba "StringLibrary" como nombre del proyecto. Pulse **Aceptar** para crear el proyecto de biblioteca de clases.

   ![Cuadro de diálogo Agregar nuevo proyecto](./media/vb-library-with-visual-studio/libproject.png)

   La ventana de código se abre después en el entorno de desarrollo de Visual Studio. 
 
   ![Ventana de aplicación de Visual Studio que muestra el código de plantilla de biblioteca de clases predeterminado](./media/vb-library-with-visual-studio/stringlibrary.png)

1. Compruebe para asegurarse de que la biblioteca tiene como destino la versión correcta de .NET Standard. Haga clic con el botón derecho en el proyecto de la biblioteca en las ventanas del **Explorador de soluciones** y, después, seleccione **Propiedades**. El cuadro de texto **Plataforma de destino** muestra que nos referimos a .NET Standard 2.0.

   ![Propiedades del proyecto para la biblioteca de clases](./media/library-with-visual-studio/properties.png)

1. Además en el cuadro de diálogo **Propiedades**, borre el texto del cuadro de texto **Espacio de nombres raíz**. Para cada proyecto, Visual Basic crea automáticamente un espacio de nombres que corresponde al nombre del proyecto, y cualquier espacio de nombres definido en los archivos de código fuente es un elemento primario de ese espacio de nombres. Queremos definir un espacio de nombres de nivel superior con la palabra clave [`namespace`](../../visual-basic/language-reference/statements/namespace-statement.md).
  
1. Reemplace el código de la ventana de código por el código siguiente y guarde el archivo:

  [!CODE-vb[ClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/stringlibrary.vb)]

   la biblioteca de clases, `UtilityLibraries.StringLibrary`, contiene un método llamado `StartsWithUpper`, que devuelve un valor <xref:System.Boolean> que indica si la instancia de cadena actual comienza con un carácter en mayúscula. El estándar Unicode distingue caracteres en mayúsculas de caracteres en minúsculas. El método <xref:System.Char.IsUpper(System.Char)?displayProperty=fullName> devuelve `true` si un carácter está en mayúsculas.

1. En la barra de menús, seleccione **Compilar** > **Compilar solución**. El proyecto se debería compilar sin errores.

   ![Panel de salida que muestra que la compilación se ha realizado correctamente](./media/library-with-visual-studio/buildsucceeds.png)



## <a name="next-step"></a>Paso siguiente

La biblioteca se ha creado correctamente. Como no se ha llamado a ninguno de los métodos, no se sabe si funciona como estaba previsto. El siguiente paso en el desarrollo de la biblioteca consiste en probarla mediante un [proyecto de prueba unitaria](testing-library-with-visual-studio.md).

