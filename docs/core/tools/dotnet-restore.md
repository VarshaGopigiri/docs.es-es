---
title: 'Comando dotnet restore: CLI de .NET Core'
description: "Aprenda a restaurar dependencias y herramientas específicas del proyecto con el comando dotnet restore."
keywords: dotnet-restore, CLI, comando de la CLI, .NET Core
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: e9f122c71330f93e02157e36f9fbbc92a0dddfce
ms.contentlocale: es-es
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-restore"></a>dotnet restore

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>Nombre

`dotnet restore`: restaura las dependencias y las herramientas de un proyecto.

## <a name="synopsis"></a>Sinopsis

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--force] [--ignore-failed-sources] [--no-cache] [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity]
dotnet restore [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```
dotnet restore [<ROOT>] [--configfile] [--disable-parallel] [--ignore-failed-sources] [--no-cache] [--no-dependencies] [--packages] [-r|--runtime] [-s|--source] [-v|--verbosity]
dotnet restore [-h|--help]
```

---

## <a name="description"></a>Descripción

El comando `dotnet restore` usa NuGet para restaurar las dependencias, así como las herramientas específicas del proyecto que se especifican en el archivo project.json. De forma predeterminada, la restauración de dependencias y herramientas se realiza en paralelo.

Para restaurar las dependencias, NuGet necesita las fuentes donde se encuentran los paquetes. Las fuente se proporcionan normalmente mediante el archivo de configuración *NuGet.config*. Cuando se instalan las herramientas de la CLI, se proporciona un archivo de configuración predeterminado. Puede especificar más fuentes creando su propio archivo *NuGet.config* en el directorio del proyecto. También puede especificar fuentes adicionales por invocación en un símbolo del sistema.

Para las dependencias, puede especificar dónde se colocan los paquetes restaurados durante la operación de restauración mediante el argumento `--packages`. Si no se especifica, se usa la caché de paquetes NuGet predeterminada, que se encuentra en el directorio `.nuget/packages` en el directorio de inicio del usuario en todos los sistemas operativos (por ejemplo, */home/user1* en Linux o *C:\Users\user1* en Windows).

Para herramientas específicas del proyecto, `dotnet restore` restaura primero el paquete en el que se empaqueta la herramienta y, a continuación, continúa con la restauración de las dependencias de la herramienta especificadas en su project.json.

El comportamiento del comando `dotnet restore` depende de algunas de las opciones de configuración del archivo *Nuget.Config*, si están presentes. Por ejemplo, establecer `globalPackagesFolder` en *NuGet.Config* coloca los paquetes NuGet restaurados en la carpeta especificada. Esta es una alternativa para especificar la opción `--packages` en el comando `dotnet restore`. Para obtener más información, vea la [referencia de NuGet.Config](/nuget/schema/nuget-config-file).

## <a name="arguments"></a>Argumentos

`ROOT`

Ruta de acceso opcional del archivo de proyecto para restaurar.

## <a name="options"></a>Opciones

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--configfile <FILE>`

El archivo de configuración (*NuGet.config*) que se usa para la operación de restauración.

`--disable-parallel`

Deshabilita la restauración de varios proyectos en paralelo.

`--force`

Fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente. Esto es equivalente a eliminar el archivo *project.assets.json*.

`-h|--help`

Imprime una corta ayuda para el comando.

`--ignore-failed-sources`

Solo se advierte sobre los orígenes con error si hay paquetes que satisfagan el requisito de versión.

`--no-cache`

Especifica que no se almacenen en caché los paquetes y las solicitudes HTTP.

`--no-dependencies`

Al restaurar un proyecto con referencias de proyecto a proyecto (P2P), se restaura el proyecto raíz y no las referencias.

`--packages <PACKAGES_DIRECTORY>`

Especifica el directorio de los paquetes restaurados.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Especifica un tiempo de ejecución para la restauración del paquete. Se usa para restaurar los paquetes con tiempos de ejecución que no se enumeran explícitamente en la etiqueta `<RuntimeIdentifiers>` del archivo *.csproj*. Para obtener una lista de identificadores de tiempo de ejecución (RID), consulte el [catálogo de RID](../rid-catalog.md). Para proporcionar varios RID; especifique esta opción varias veces.

`-s|--source <SOURCE>`

Especifica un origen de paquetes de NuGet que se usará durante la operación de restauración. Esto invalida todos los orígenes especificados en los archivos *NuGet.config*. Al especificar esta opción varias veces, se pueden proporcionar varios orígenes.

`--verbosity <LEVEL>`

Establece el nivel de detalle del comando. Los valores permitidos son `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` y `diag[nostic]`.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--configfile <FILE>`

El archivo de configuración (*NuGet.config*) que se usa para la operación de restauración.

`--disable-parallel`

Deshabilita la restauración de varios proyectos en paralelo.

`-h|--help`

Imprime una corta ayuda para el comando.

`--ignore-failed-sources`

Solo se advierte sobre los orígenes con error si hay paquetes que satisfagan el requisito de versión.

`--no-cache`

Especifica que no se almacenen en caché los paquetes y las solicitudes HTTP.

`--no-dependencies`

Al restaurar un proyecto con referencias de proyecto a proyecto (P2P), se restaura el proyecto raíz y no las referencias.

`--packages <PACKAGES_DIRECTORY>`

Especifica el directorio de los paquetes restaurados.

`-r|--runtime <RUNTIME_IDENTIFIER>`

Especifica un tiempo de ejecución para la restauración del paquete. Se usa para restaurar los paquetes con tiempos de ejecución que no se enumeran explícitamente en la etiqueta `<RuntimeIdentifiers>` del archivo *.csproj*. Para obtener una lista de identificadores de tiempo de ejecución (RID), consulte el [catálogo de RID](../rid-catalog.md). Para proporcionar varios RID; especifique esta opción varias veces.

`-s|--source <SOURCE>`

Especifica un origen de paquetes de NuGet que se usará durante la operación de restauración. Esto invalida todos los orígenes especificados en los archivos *NuGet.config*. Al especificar esta opción varias veces, se pueden proporcionar varios orígenes.

`--verbosity <LEVEL>`

Establece el nivel de detalle del comando. Los valores permitidos son `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` y `diag[nostic]`.

## <a name="examples"></a>Ejemplos

Restauración de dependencias y herramientas para el proyecto en el directorio actual:

`dotnet restore`

Restauración de dependencias y herramientas para el proyecto `app1` encontrado en la ruta de acceso dada:

`dotnet restore ~/projects/app1/app1.csproj`

Restaurar las dependencias y las herramientas para el proyecto en el directorio actual con la ruta de acceso de archivo proporcionada como origen:

`dotnet restore -s c:\packages\mypackages`

Restaurar las dependencias y las herramientas para el proyecto en el directorio actual mediante las dos rutas de acceso de archivo proporcionadas como orígenes:

`dotnet restore -s c:\packages\mypackages -s c:\packages\myotherpackages`

Restaurar las dependencias y herramientas para el proyecto en el directorio actual y mostrar únicamente la salida mínima:

`dotnet restore --verbosity minimal`
