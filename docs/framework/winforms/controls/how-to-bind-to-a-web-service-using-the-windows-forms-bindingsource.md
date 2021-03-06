---
title: "C&#243;mo: Enlazar a un servicio Web mediante el componente BindingSource de formularios Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingSource (componente) [Windows Forms], enlazar a un servicio Web"
  - "BindingSource (componente) [Windows Forms], ejemplos"
  - "controles [Windows Forms], enlazar a un servicio Web"
  - "ejemplos [Windows Forms], BindingSource (componente)"
  - "servicios Web, enlazar controles"
ms.assetid: ee261207-4573-4cb9-a8cb-5185037e0fba
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# C&#243;mo: Enlazar a un servicio Web mediante el componente BindingSource de formularios Windows Forms
Si quiere enlazar un control de Windows Forms a los resultados obtenidos de la llamada a un servicio Web XML, puede usar un componente <xref:System.Windows.Forms.BindingSource>.  Este procedimiento es similar a enlazar un componente <xref:System.Windows.Forms.BindingSource> a un tipo.  Debe crear un proxy de cliente que contenga los métodos y los tipos expuestos por el servicio Web.  El proxy de cliente se genera desde el propio servicio Web \(.asmx\) o desde su archivo de lenguaje de descripción de servicios Web \(WSDL\).  Además, el proxy de cliente debe exponer los campos de tipos complejos usados por el servicio Web como propiedades públicas.  Después, enlace el <xref:System.Windows.Forms.BindingSource> a uno de los tipos expuestos en el proxy de servicio Web.  
  
### Para crear y enlazar a un proxy de cliente  
  
1.  Cree Windows Form en el directorio que elija, con un espacio de nombres adecuado.  
  
2.  Agregue un componente <xref:System.Windows.Forms.BindingSource> al formulario.  
  
3.  Abra el símbolo del sistema de [!INCLUDE[winsdklong](../../../../includes/winsdklong-md.md)] y vaya al mismo directorio donde se encuentra el formulario.  
  
4.  En la herramienta WSDL, escriba `wsdl` y la dirección URL del archivo .asmx o WSDL del servicio Web, seguido por el espacio de nombres de la aplicación y, opcionalmente, el lenguaje con el que está trabajando.  
  
     En el ejemplo de código siguiente se usa el servicio Web situado en http:\/\/webservices.eraserver.  net\/zipcoderesolver\/zipcoderesolver.asmx.  Por ejemplo, para C\# escriba `wsdl http://webservices.eraserver.net.zipcoderesolver/zipcoderesolver.asmx /n:BindToWebService`, o para Visual Basic escriba `wsdl http://webservices.eraserver.net.zipcoderesolver/zipcoderesolver.asmx /n:BindToWebService /language:VB`.  Al pasar la ruta de acceso como un argumento a la herramienta WSDL, se generará un proxy de cliente en el mismo directorio y espacio de nombres que la aplicación, en el lenguaje especificado.  Si usa [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], agregue el archivo al proyecto.  
  
5.  En el proxy de cliente, seleccione el tipo al que se enlazará.  
  
     Suele ser un tipo devuelto por un método proporcionado por el servicio Web.  Los campos del tipo elegido se deben exponer como propiedades públicas con fines de enlace.  
  
     [!code-cpp[System.Windows.Forms.DataConnectorWebService#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#4)]
     [!code-csharp[System.Windows.Forms.DataConnectorWebService#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.DataConnectorWebService#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#4)]  
  
6.  Establezca la propiedad <xref:System.Windows.Forms.BindingSource.DataSource%2A> del <xref:System.Windows.Forms.BindingSource> en el tipo que quiera que esté contenido en el proxy de cliente del servicio Web.  
  
     [!code-cpp[System.Windows.Forms.DataConnectorWebService#2](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#2)]
     [!code-csharp[System.Windows.Forms.DataConnectorWebService#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#2)]
     [!code-vb[System.Windows.Forms.DataConnectorWebService#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#2)]  
  
### Para enlazar controles al BindingSource que está enlazado a un servicio Web  
  
-   Enlace controles al <xref:System.Windows.Forms.BindingSource>, pasando como parámetro la propiedad pública del tipo de servicio Web que desee.  
  
     [!code-cpp[System.Windows.Forms.DataConnectorWebService#3](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#3)]
     [!code-csharp[System.Windows.Forms.DataConnectorWebService#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#3)]
     [!code-vb[System.Windows.Forms.DataConnectorWebService#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#3)]  
  
## Ejemplo  
 En el ejemplo de código siguiente se muestra cómo enlazar un componente <xref:System.Windows.Forms.BindingSource> a un servicio Web y, después, cómo enlazar un cuadro de texto al componente <xref:System.Windows.Forms.BindingSource>.  Al hacer clic en el botón, se llama a un método de servicio Web y el resultado se mostrarán en `textbox1`.  
  
 [!code-cpp[System.Windows.Forms.DataConnectorWebService#1](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CPP/form1.cpp#1)]
 [!code-csharp[System.Windows.Forms.DataConnectorWebService#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/CS/form1.cs#1)]
 [!code-vb[System.Windows.Forms.DataConnectorWebService#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataConnectorWebService/VB/form1.vb#1)]  
  
## Compilar el código  
 Este es un ejemplo completo que incluye un método `Main` y una versión reducida del código del proxy de cliente.  
  
 Para este ejemplo se necesita:  
  
-   Referencias a los ensamblados System, System.Drawing, System.Web.Services, System.Windows.Forms y System.Xml.  
  
 Para obtener información acerca de cómo compilar este ejemplo desde la línea de comandos para [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], consulte [Compilar desde la línea de comandos](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilar la línea de comandos con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  También puede compilar este ejemplo en [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] pegando el código en un nuevo proyecto.  Consulte también [Cómo: Compilar y ejecutar un ejemplo de código completo de Windows Forms en Visual Studio](http://msdn.microsoft.com/library/Bb129228%20\(v=vs.110\)).  
  
## Vea también  
 [BindingSource \(Componente\)](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [Cómo: Enlazar un control de Windows Forms a un tipo](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)