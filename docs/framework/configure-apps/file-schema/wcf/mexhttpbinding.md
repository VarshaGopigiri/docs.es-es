---
title: "&lt;mexHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e50b2e1f-9668-41a5-8077-dee7abff9f0f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# &lt;mexHttpBinding&gt;
Especifica los valores para un enlace utilizado para el intercambio de mensajes de WS\-MetadataExchange \(WS\-MEX\) sobre HTTP.  
  
## Sintaxis  
  
```  
  
<mexHttpBinding>  
   <binding   
       closeTimeout="TimeSpan"   
       name="string"   
       openTimeout="TimeSpan"   
       receiveTimeout="TimeSpan"  
       sendTimeout="TimeSpan">  
   </binding>  
</mexHttpBinding>  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|`closeTimeout`|Un valor <xref:System.TimeSpan> que especifica el intervalo de tiempo del que dispone una operación de cierre para completarse.  Este valor debe ser mayor o igual que <xref:System.TimeSpan.Zero>.  El valor predeterminado es 00:01:00.|  
|`name`|Cadena que contiene el nombre de configuración del enlace.  Este valor debe ser único porque se usa como identificación del enlace.  Cada enlace tiene los atributos `name` y `namespace` que, juntos, lo identifican de forma exclusiva en los metadatos del servicio.  Además, este nombre es único entre los enlaces del mismo tipo.  A partir de [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], no es necesario que los enlaces y los comportamientos tengan nombre.  Para obtener más información sobre la configuración predeterminada, así como sobre enlaces y comportamientos sin nombre, vea [Configuración simplificada](../../../../../docs/framework/wcf/simplified-configuration.md) y [Configuración simplificada de los servicios de WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|`openTimeout`|Valor de la estructura <xref:System.TimeSpan> que especifica el intervalo de tiempo del que dispone una operación de apertura para completarse.  Este valor debe ser mayor o igual que <xref:System.TimeSpan.Zero>.  El valor predeterminado es 00:01:00.|  
|`receiveTimeout`|Un valor <xref:System.TimeSpan> que especifica el intervalo de tiempo del que dispone una operación de recepción para completarse.  Este valor debe ser mayor o igual que <xref:System.TimeSpan.Zero>.  El valor predeterminado es 00:10:00.|  
|`sendTimeout`|Un valor <xref:System.TimeSpan> que especifica el intervalo de tiempo del que dispone una operación de envío para completarse.  Este valor debe ser mayor o igual que <xref:System.TimeSpan.Zero>.  El valor predeterminado es 00:01:00.|  
  
### Elementos secundarios  
 Ninguno.  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<enlaces\>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Este elemento contiene una colección de enlaces estándar y personalizados.|  
  
## Comentarios  
 Este enlace es esencialmente un enlace `WSHttpBinding` con la seguridad deshabilitada.  Admite la mayoría de las solicitudes de metadatos.  
  
## Vea también  
 <xref:System.ServiceModel.Description.MetadataExchangeBindings.CreateMexHttpBinding%2A>   
 <xref:System.ServiceModel.Configuration.MexHttpBindingElement>   
 [Cómo publicar metadatos para un servicio mediante un archivo de configuración](../../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [Publicación y recuperación de metadatos a través de un enlace personalizado](../../../../../docs/framework/wcf/extending/publishing-and-retrieving-metadata-over-a-custom-binding.md)   
 [Metadatos](../../../../../docs/framework/wcf/feature-details/metadata.md)   
 [Enlaces](../../../../../docs/framework/wcf/bindings.md)   
 [Configuración de enlaces proporcionados por el sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/es-es/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<enlace\>](../../../../../docs/framework/misc/binding.md)