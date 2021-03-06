---
title: "C&#243;mo: Especificar un enlace de servicio en el c&#243;digo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 67ab5dd8-79c1-4e62-aa75-828ea918a53a
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# C&#243;mo: Especificar un enlace de servicio en el c&#243;digo
En este ejemplo, se define un contrato de `ICalculator` para un servicio de la calculadora, el servicio se implementa en la clase `CalculatorService` y a continuación, su extremo se define mediante código, donde se especifica que el servicio debe utilizar la clase <xref:System.ServiceModel.BasicHttpBinding>.  
  
 Normalmente es el mejor procedimiento para especificar el enlace y la información de dirección de forma declarativa en configuración en lugar de hacerlo de forma imperativa en código.Normalmente, no resulta muy práctico definir los extremos en el código ya que los enlaces y las direcciones de un servicio implementado son, por lo general, diferentes de los utilizados durante el desarrollo del servicio.Más generalmente, manteniendo el enlace y la información de dirección fuera del código permite cambiarlos sin tener que recompilar o implementar la aplicación.  
  
 Para una descripción de cómo configurar este servicio utilizando elementos de configuración en lugar de código, vea [Cómo: Especificar un enlace de servicio en la configuración](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md).  
  
### Para especificar mediante código que se use BasicHttpBinding para el servicio  
  
1.  Defina un contrato de servicios para el tipo de servicio.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[C_HowTo_CodeServiceBinding#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2.  Implemente el contrato de servicios en una clase de servicio.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[C_HowTo_CodeServiceBinding#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3.  En la aplicación de alojamiento, cree la dirección base que han de utilizar el servicio y el enlace con el servicio.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[C_HowTo_CodeServiceBinding#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4.  Cree el host para el servicio, agregue el extremo y, a continuación, abra el host.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#4)]
     [!code-vb[C_HowTo_CodeServiceBinding#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#4)]  
  
### Para modificar los valores predeterminados de las propiedades de enlace  
  
1.  Para modificar uno de los valores predeterminados de propiedades de la clase <xref:System.ServiceModel.BasicHttpBinding>, establezca el valor de propiedad del enlace en el nuevo valor antes de crear el host.Por ejemplo, para cambiar los valores predeterminados de tiempos de espera de apertura y cierre de 1 a 2 minutos, utilice lo siguiente.  
  
     [!code-csharp[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#5)]
     [!code-vb[C_HowTo_CodeServiceBinding#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#5)]  
  
## Vea también  
 [Utilización de enlaces para configurar servicios y clientes](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Especificación de una dirección de extremo](../../../docs/framework/wcf/specifying-an-endpoint-address.md)