---
title: "C&#243;mo: Configurar un cliente WCF para interoperar con los servicios WSE3.0 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3dadd7f1-d207-4ea5-a73b-3e8aa44407f8
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# C&#243;mo: Configurar un cliente WCF para interoperar con los servicios WSE3.0
Los clientes de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] son compatibles en el nivel de conexión con Web Services Enhancements 3.0 para servicios de Microsoft .NET (WSE) cuando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] se configura para utilizar la versión de agosto de 2004 de la especificación WS-Addressing.  
  
### <a name="to-configure-a-wcf-client-to-interoperate-with-a-wse-30-web-service"></a>Configuración de un cliente WCF para interoperar con un servicio web WSE 3.0  
  
1.  Ejecute el [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) para crear un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] cliente para el servicio Web de WSE 3.0.  
  
     Para un servicio web WSE, se crea una clase de cliente de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
     Para obtener más información acerca de cómo crear un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] cliente, consulte la [Cómo: crear un cliente](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
2.  Cree una clase que represente un enlace que puede comunicarse con los servicios Web WSE 3.0.  
  
     La clase siguiente forma parte de la [interoperar con WSE](http://msdn.microsoft.com/es-es/f6816861-96a0-45f9-8736-8e4e82cd3a41) ejemplo.  
  
    1.  Cree una clase que deriva de la <xref:System.ServiceModel.Channels.Binding> clase.  
  
         En el ejemplo de código siguiente se crea una clase denominada `WseHttpBinding` que se deriva de la <xref:System.ServiceModel.Channels.Binding> clase.  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2.  Agregue propiedades a la clase que especifiquen la aserción de llave en mano WSE, si se requieren las claves derivadas, si se utilizan sesiones seguras, si se requieren confirmaciones de firmas, y la configuración de protección de mensajes.  
  
         En el ejemplo de código siguiente se define `SecurityAssertion,``RequireDerivedKeys, EstablishSecurityContext, MessageProtectionOrder` propiedades que especifican la aserción de llave en mano de WSE, si se requieren claves derivadas, si se utilizan sesiones seguras, si se requieren confirmaciones de firmas y la configuración de protección de mensajes, respectivamente.  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3.  Invalidar el <xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A> para establecer las propiedades de enlace.  
  
         El ejemplo de código siguiente especifica el transporte, codificación de mensajes y configuración de protección de mensajes obteniendo los valores de las propiedades `SecurityAssertion` y `MessageProtectionOrder`.  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3.  En el código de la aplicación cliente, agregue el código para definir las propiedades de enlace.  
  
     El ejemplo de código siguiente especifica que el cliente [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] debe utilizar protección de mensajes y autenticación tal y como define la aserción de seguridad de llave en mano `AnonymousForCertificate` de WSE 3.0. Además, se requieren sesiones seguras y claves derivadas.  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente define un enlace personalizado que expone propiedades que corresponden a las propiedades de una aserción de seguridad de llave en mano WSE 3.0. El enlace personalizado, que se denomina `WseHttpBinding`, se utiliza, a continuación, para especificar las propiedades de enlace de un cliente de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
  
[!code-csharp[c_WCFClientToWSEService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#0)]
[!code-vb[c_WCFClientToWSEService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#0)]  
  
## <a name="see-also"></a>Vea también  
 <xref:System.ServiceModel.Channels.Binding>   
 [Interoperar con WSE](http://msdn.microsoft.com/es-es/f6816861-96a0-45f9-8736-8e4e82cd3a41)