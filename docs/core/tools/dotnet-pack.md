---
title: 'Comando dotnet pack: CLI de .NET Core'
description: El comando dotnet pack crea paquetes de NuGet para el proyecto de .NET Core.
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 8594c863d67baf0237b63e61f28ca9ee315eeddf
ms.contentlocale: es-es
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-pack"></a>dotnet pack

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>Nombre

`dotnet pack`: empaqueta el código en un paquete de NuGet.

## <a name="synopsis"></a>Sinopsis

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```
dotnet pack [<PROJECT>] [-c|--configuration] [--force] [--include-source] [--include-symbols] [--no-build] [--no-dependencies] [--no-restore] [-o|--output] [--runtime] [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet pack [<PROJECT>] [-c|--configuration] [--include-source] [--include-symbols] [--no-build] [-o|--output] [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```
---

## <a name="description"></a>Descripción

El comando `dotnet pack` compila el proyecto y crea paquetes de NuGet. El resultado de este comando es un paquete de NuGet. Si la opción `--include-symbols` está presente, se crea otro paquete que contiene los símbolos de depuración.

Las dependencias de NuGet del proyecto empaquetado se agregan al archivo *.nuspec*, por lo que se pueden resolver adecuadamente cuando se instala el paquete. Las referencias de proyecto a proyecto no se empaquetan dentro del proyecto. Actualmente, debe disponer de un paquete por proyecto si tiene dependencias de proyecto a proyecto.

De forma predeterminada, `dotnet pack` compila primero el proyecto. Si desea evitar este comportamiento, pase la opción `--no-build`. A menudo resulta útil en escenarios de compilación de integración continua (CI) donde se conoce el código que se compiló anteriormente.

Puede proporcionar propiedades de MSBuild en el comando `dotnet pack` para el proceso de empaquetado. Para obtener más información, vea [Propiedades de metadatos de NuGet](csproj.md#nuget-metadata-properties) y la [Referencia de la línea de comandos de MSBuild](/visualstudio/msbuild/msbuild-command-line-reference).

## <a name="arguments"></a>Argumentos

`PROJECT`

El proyecto para empaquetar. O bien una ruta de acceso a un [archivo csproj](csproj.md) o a un directorio. Si se omite, se toma como predeterminado el directorio actual.

## <a name="options"></a>Opciones

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-c|--configuration {Debug|Release}`

Define la configuración de compilación. El valor predeterminado es `Debug`.

`--force`: fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente. Esto es equivalente a eliminar el archivo *project.assets.json*.

`-h|--help`

Imprime una corta ayuda para el comando.

`--include-source`

Incluye los archivos de origen en el paquete de NuGet. Los archivos de origen se incluyen en la carpeta `src` dentro de `nupkg`.

`--include-symbols`

Genera símbolos `nupkg`.

`--no-build`

No compila el proyecto antes de empaquetarlo.

`--no-dependencies`

Omite las referencias de proyecto a proyecto y solo restaura el proyecto raíz.

`--no-restore`

No realiza una restauración implícita al ejecutar el comando.

`-o|--output <OUTPUT_DIRECTORY>`

Coloca los paquetes compilados en el directorio especificado.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Especifica el tiempo de ejecución de destino para el que restaurar los paquetes. Para obtener una lista de identificadores de tiempo de ejecución (RID), consulte el [catálogo de RID](../rid-catalog.md).

`-s|--serviceable`

Establece la marca de servicio en el paquete. Para más información, consulte [.NET Blog: .NET 4.5.1 Supports Microsoft Security Updates for .NET NuGet Libraries](https://aka.ms/nupkgservicing) (Blog de .NET: .NET 4.5.1 admite actualizaciones de seguridad de Microsoft para bibliotecas NuGet de .NET).

`--version-suffix <VERSION_SUFFIX>`

Define el valor de la propiedad de `$(VersionSuffix)` en el proyecto.

`-v|--verbosity <LEVEL>`

Establece el nivel de detalle del comando. Los valores permitidos son `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` y `diag[nostic]`.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

Define la configuración de compilación. El valor predeterminado es `Debug`.

`-h|--help`

Imprime una corta ayuda para el comando.

`--include-source`

Incluye los archivos de origen en el paquete de NuGet. Los archivos de origen se incluyen en la carpeta `src` dentro de `nupkg`.

`--include-symbols`

Genera símbolos `nupkg`.

`--no-build`

No compila el proyecto antes de empaquetarlo.

`-o|--output <OUTPUT_DIRECTORY>`

Coloca los paquetes compilados en el directorio especificado.

`-s|--serviceable`

Establece la marca de servicio en el paquete. Para más información, consulte [.NET Blog: .NET 4.5.1 Supports Microsoft Security Updates for .NET NuGet Libraries](https://aka.ms/nupkgservicing) (Blog de .NET: .NET 4.5.1 admite actualizaciones de seguridad de Microsoft para bibliotecas NuGet de .NET).

`--version-suffix <VERSION_SUFFIX>`

Define el valor de la propiedad de `$(VersionSuffix)` en el proyecto.

`-v|--verbosity <LEVEL>`

Establece el nivel de detalle del comando. Los valores permitidos son `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` y `diag[nostic]`.

---

## <a name="examples"></a>Ejemplos

Empaquetado del proyecto en el directorio actual:

`dotnet pack`

Empaquetar el proyecto `app1`:

`dotnet pack ~/projects/app1/project.csproj`
    
Empaquetar el proyecto en el directorio actual y colocar los paquetes resultantes en la carpeta `nupkgs`:

`dotnet pack --output nupkgs`

Empaquetar el proyecto en el directorio actual en la carpeta `nupkgs` y omitir del paso de compilación:

`dotnet pack --no-build --output nupkgs`

Con el sufijo de la versión del proyecto configurado como `<VersionSuffix>$(VersionSuffix)</VersionSuffix>` en el archivo *.csproj*, empaquetar el proyecto actual y actualizar la versión del paquete resultante con el sufijo dado:

`dotnet pack --version-suffix "ci-1234"`

Establecer la versión del paquete en `2.1.0` con la propiedad de MSBuild `PackageVersion`:

`dotnet pack /p:PackageVersion=2.1.0`

