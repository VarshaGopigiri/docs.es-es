---
title: "Compilar una aplicaci&#243;n de WPF (WPF) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "aplicación WPF, compilar"
ms.assetid: a58696fd-bdad-4b55-9759-136dfdf8b91c
caps.latest.revision: 45
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 42
---
# Compilar una aplicaci&#243;n de WPF (WPF)
Las aplicaciones de [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] pueden compilarse como aplicaciones ejecutables de [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] \(.exe\), bibliotecas \(.dll\) o una combinación de ambos tipos de ensamblados.  En este tema se ofrece una introducción a la compilación de aplicaciones [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] y se describen los pasos clave del proceso de compilación.  
  
   
  
<a name="Building_a_WPF_Application_using_Command_Line"></a>   
## Compilar una aplicación WPF  
 Una aplicación WPF se puede compilar de las maneras siguientes:  
  
-   Línea de comandos.  La aplicación debe contener sólo el código \(sin XAML\) y un archivo de definición de aplicación.  Para obtener más información, vea [Compilar la línea de comandos con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md) o [Compilar desde la línea de comandos \(Visual Basic\)](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md).  
  
-   Microsoft Build Engine \(MSBuild\).  Además del código y los archivos XAML, la aplicación debe contener un archivo de proyecto de MSBuild.  Para obtener más información, vea [MSBuild](../Topic/MSBuild1.md).  
  
-   Visual Studio.  Visual Studio es un entorno de desarrollo integrado que compila las aplicaciones WPF con MSBuild e incluye un diseñador visual para crear la interfaz de usuario.  Para obtener más información, vea [Desarrollo de aplicaciones en Visual Studio](http://msdn.microsoft.com/es-es/97490c1b-a247-41fb-8f2c-bc4c201eff68) y [WPF Designer](http://msdn.microsoft.com/es-es/c6c65214-8411-4e16-b254-163ed4099c26).  
  
<a name="The_Windows_Presentation_Foundation_Build_Pipeline"></a>   
## Canalización de compilación de WPF  
 Cuando se compila un proyecto de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], se invoca la combinación de destinos específicos del lenguaje y de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  El proceso de ejecución de estos destinos se denomina canalización de compilación y los pasos principales se muestran en la siguiente ilustración.  
  
 ![Proceso de compilación de WPF](../../../../docs/framework/wpf/app-development/media/wpfbuildsystem-figure1.png "WPFBuildSystem\_Figure1")  
  
<a name="Pre_Build_Initializations"></a>   
### Inicializaciones previas a la compilación  
 Antes de compilar, [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] determina la ubicación de herramientas y bibliotecas importantes, entre las que se incluyen las siguientes:  
  
-   [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)].  
  
-   Los directorios de [!INCLUDE[TLA2#tla_wcsdk](../../../../includes/tla2sharptla-wcsdk-md.md)].  
  
-   La ubicación de los ensamblados de referencia de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].  
  
-   La propiedad de las rutas de búsqueda de ensamblados.  
  
 La primera ubicación en la que [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] busca los ensamblados es el directorio de ensamblados de referencia \(%ProgramFiles%\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\\).  Durante este paso, el proceso de compilación inicializa también las distintas propiedades y grupos de elementos, y efectúa el trabajo de limpieza necesario.  
  
<a name="Resolving_references"></a>   
### Resolver referencias  
 El proceso de compilación busca y enlaza los ensamblados necesarios para generar el proyecto de aplicación.  Esta lógica se incluye en la tarea `ResolveAssemblyReference`.  Todos los ensamblados declarados como `Reference` en el archivo de proyecto se proporcionan a la tarea junto con información sobre las rutas de búsqueda y los metadatos de los ensamblados que ya están instalados en el sistema.  La tarea busca los ensamblados y utiliza los metadatos del ensamblado instalado para filtrar los ensamblados de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] básicos que no deben mostrarse en los manifiestos de salida.  Esto es necesario para evitar información redundante en los manifiestos de ClickOnce.  Por ejemplo, como PresentationFramework.dll se puede considerar representativo de una compilación de aplicación y de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] y, puesto que todos los ensamblados de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] están en la misma ubicación en cada equipo que tiene [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] instalado, no hay necesidad de incluir toda la información sobre todos los ensamblados de referencia de [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] en los manifiestos.  
  
<a name="Markup_Compilation___Pass_1"></a>   
### Generación del marcado: Paso 1  
 En este paso, los archivos de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] se analizan y generan para que el motor en tiempo de ejecución no tenga que encargarse de analizar [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] y validar los valores de propiedad.  El archivo de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] generado se convierte en un token para que pueda cargarse mucho más rápido en tiempo de ejecución.  
  
 Durante este paso, se realizan las siguientes operaciones para cada archivo de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que es un elemento de compilación `Page`:  
  
1.  El compilador de marcado analiza el archivo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)].  
  
2.  Se crea una representación generada para el [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] y se copia a la carpeta obj\\Release.  
  
3.  Se crea una representación de CodeDOM de una nueva clase parcial y se copia a la carpeta obj\\Release.  
  
 Además, se genera un archivo de código específico del lenguaje para cada archivo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. Por ejemplo, para una página Page1.xaml de un proyecto escrito en [!INCLUDE[TLA2#tla_visualb](../../../../includes/tla2sharptla-visualb-md.md)], se genera un archivo Page1.g.vb; para una página Page1.xaml de un proyecto escrito en [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)], se genera un archivo Page1.g.cs.  ".g" en el nombre de archivo indica que el archivo es código generado que tiene una declaración de clase parcial para el elemento de nivel superior del archivo de marcado \(como `Page` o `Window`\).  La clase se declara con el modificador `partial` de [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] \(`Extends` en [!INCLUDE[TLA2#tla_visualb](../../../../includes/tla2sharptla-visualb-md.md)]\) para indicar que es otra declaración de la clase en otro lugar, normalmente en el archivo Page1.xaml.cs de código subyacente.  
  
 La clase parcial se extiende desde la clase base correspondiente \(como <xref:System.Windows.Controls.Page> para una página\) e implementa la interfaz <xref:System.Windows.Markup.IComponentConnector?displayProperty=fullName>.  La interfaz <xref:System.Windows.Markup.IComponentConnector> tiene métodos que inicializan un componente y conectan los nombres y eventos en elementos en su contenido.  Por consiguiente, el archivo de código generado tiene una implementación de métodos como la siguiente:  
  
```csharp  
public void InitializeComponent() {  
    if (_contentLoaded) {  
        return;  
    }  
    _contentLoaded = true;  
    System.Uri resourceLocater =   
        new System.Uri(  
            "window1.xaml",   
            System.UriKind.RelativeOrAbsolute);  
    System.Windows.Application.LoadComponent(this, resourceLocater);  
}  
```  
  
```vb  
Public Sub InitializeComponent() _  
  
    If _contentLoaded Then  
        Return  
    End If  
  
    _contentLoaded = True  
    Dim resourceLocater As System.Uri = _  
        New System.Uri("mainwindow.xaml", System.UriKind.Relative)  
  
    System.Windows.Application.LoadComponent(Me, resourceLocater)  
  
End Sub  
```  
  
 De forma predeterminada, la compilación del marcado se ejecuta en el mismo <xref:System.AppDomain> que el motor de [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)].  Esto proporciona una mejora del rendimiento importante.  Este comportamiento se puede activar o desactivar alternativamente con la propiedad `AlwaysCompileMarkupFilesInSeparateDomain`.  Esto presenta la ventaja de descargar todos los ensamblados de referencia descargando el objeto <xref:System.AppDomain> independiente.  
  
<a name="Pass_2_of_Markup_Compilation"></a>   
### Generación del marcado: Paso 2  
 No todas las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] se compilan en el paso 1 de la compilación de marcado.  Los archivos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que tienen referencias de tipos definidos localmente \(referencias a tipos definidos en el código en otro lugar del mismo proyecto\) no se compilan en este momento.  Esto se debe a que estos tipos definidos localmente sólo existen en el código fuente y aún no están generados.  Para determinar esto, el analizador utiliza heurística que implica la búsqueda de elementos como `x:Name` en el archivo de marcado.  Cuando se encuentra este tipo de instancia, la compilación del archivo de marcado se pospone hasta que se hayan generado los archivos de código y, en ese momento, el segundo paso de la compilación de marcado procesa estos archivos.  
  
<a name="File_Classification"></a>   
### Clasificación de archivos  
 El proceso de compilación coloca los archivos de salida en grupos de recursos diferentes en función del ensamblado de aplicación en el que se van a incluir.  En una aplicación no traducida típica, todos los archivos de datos marcados como `Resource` se colocan en el ensamblado principal \(ejecutable o biblioteca\).  Cuando `UICulture` se establece en el proyecto, todos los archivos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] generados y los recursos explícitamente marcados como específicos del lenguaje se colocan en el ensamblado de recursos satélite.  Asimismo, todos los recursos neutrales en cuanto al idioma se colocan en el ensamblado principal.  Esta determinación de ubicación de los archivos se realiza en este paso del proceso de compilación.  
  
 Las acciones de compilación de `ApplicationDefinition`, `Page` y `Resource` del archivo de proyecto se pueden incrementar con los metadatos de `Localizable` \(los valores permitidos son `true` y `false`\), que indican si el archivo es específico del idioma o neutral en cuanto al idioma.  
  
<a name="Core_Compilation"></a>   
### Compilación básica  
 El paso básico de compilación implica la compilación de los archivos de código.  Esta compilación está controlada por los archivos de destino específicos del lenguaje Microsoft.CSharp.targets y Microsoft.VisualBasic.targets.  Si la heurística ha determinado que basta con un solo paso del compilador de marcado, se genera el ensamblado principal.  Sin embargo, si uno o varios archivos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] del proyecto tienen referencias a tipos definidos localmente, se genera un archivo .dll temporal para que los ensamblados de aplicación finales se puedan crear una vez completado el segundo paso de compilación del marcado.  
  
<a name="Manifest_generation"></a>   
### Generación de manifiestos  
 Al final del proceso de compilación, cuando todos los ensamblados de aplicación y archivos de contenido están listos, se generan los manifiestos de [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] para la aplicación.  
  
 El archivo de manifiesto de implementación describe el modelo de implementación: la versión actual, el comportamiento de actualización y la identidad del editor junto con la firma digital.  Se supone que este manifiesto lo crean los administradores que controlan la implementación.  La extensión de archivo es .xbap \(para [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]\) y .application para las aplicaciones instaladas.  La primera se indica a través de la propiedad `HostInBrowser` del proyecto y, como resultado, el manifiesto identifica la aplicación como hospedada en el explorador.  
  
 El manifiesto de aplicación \(un archivo .exe.manifest\) describe los ensamblados de la aplicación y las bibliotecas dependientes, e incluye los permisos necesarios para la aplicación.  Se supone que este archivo lo crea el desarrollador de la aplicación.  Para iniciar una aplicación [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)], un usuario abre el archivo de manifiesto de implementación de la aplicación.  
  
 Estos archivos de manifiesto siempre se crean para [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)].  Para las aplicaciones instaladas, no se crean a menos que la propiedad `GenerateManifests` se especifique en el archivo de proyecto con el valor `true`  
  
 Los [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] obtienen dos permisos adicionales además de los permisos asignados a las aplicaciones típicas de zona de Internet: <xref:System.Security.Permissions.WebBrowserPermission> y <xref:System.Security.Permissions.MediaPermission>.  El sistema de compilación de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] declara esos permisos en el manifiesto de la aplicación.  
  
<a name="Incremental_Build_Support"></a>   
## Compatibilidad con la compilación incremental  
 El sistema de compilación de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] proporciona compatibilidad con compilaciones incrementales.  Es bastante inteligente a la hora de detectar los cambios efectuados en el marcado o el código, y sólo detecta los artefactos afectados por el cambio.  El mecanismo de compilación incremental utiliza los archivos siguientes:  
  
-   Un archivo $\(*nombreDeEnsamblado*\)\_MarkupCompiler.Cache para mantener el estado del compilador.  
  
-   Un archivo $\(*nombreDeEnsamblado*\)\_MarkupCompiler.lref para almacenar en caché los archivos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] con referencias a tipos definidos localmente.  
  
 A continuación, se incluye un conjunto de reglas que rigen la compilación incremental:  
  
-   El archivo es la unidad más pequeña en la que el sistema de compilación detecta un cambio.  Por tanto, para un archivo de código, el sistema de compilación no puede determinar si se ha cambiado un tipo o se ha agregado código.  Lo mismo se aplica a los archivos de proyecto.  
  
-   El mecanismo de compilación incremental debe saber que una página [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] define una clase o utiliza otras clases.  
  
-   Si las entradas `Reference` cambian, vuelva a generar todas las páginas.  
  
-   Si un archivo de código cambia, vuelva a generar todas las páginas con referencias de tipos definidos localmente.  
  
-   Si un archivo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] cambia:  
  
    -   Si [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] se declara como `Page` en el proyecto: si [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] no tiene referencias de tipos definidos localmente, vuelva a generar ese [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] además de todas las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] con referencias locales; si [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] tiene referencias locales, vuelva a generar todas las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] con referencias locales.  
  
    -   Si [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] se declara como `ApplicationDefinition` en el proyecto: vuelva a generar todas las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] \(razón: cada [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] hace referencia a un tipo <xref:System.Windows.Application> que puede haber cambiado\).  
  
-   Si el archivo de proyecto declara un archivo de código como definición de aplicación en lugar de un archivo [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]:  
  
    -   Compruebe si el valor de `ApplicationClassName` en el archivo de proyecto ha cambiado \(¿hay un nuevo tipo de aplicación?\).  En ese caso, vuelva a generar toda la aplicación.  
  
    -   De lo contrario, vuelva a generar todas las páginas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] con referencias locales.  
  
-   Si un archivo de proyecto cambia: aplique todas las reglas anteriores y determine lo que tiene que volver a generar.  Los cambios en las propiedades siguientes desencadenan una recompilación completa: `AssemblyName`, `IntermediateOutputPath`, `RootNamespace` y `HostInBrowser`.  
  
 Las situaciones de recompilación posibles son las siguientes:  
  
-   Se vuelve a generar toda la aplicación.  
  
-   Sólo se vuelven a generar los archivos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que tienen referencias de tipos definidos localmente.  
  
-   No se vuelve a generar nada \(si no ha cambiado nada en el proyecto\).  
  
## Vea también  
 [Implementar una aplicación de WPF](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)   
 [Referencia de MSBuild para WPF](../Topic/WPF%20MSBuild%20Reference.md)   
 [Empaquetar URI en WPF](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)   
 [Archivos de recursos, contenido y datos de aplicaciones de WPF](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)