---
title: "Elemento &lt;transport&gt; de &lt;netMsmqBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72e1b338-39f0-4af1-a5d9-7a2fb79f6a0b
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Elemento &lt;transport&gt; de &lt;netMsmqBinding&gt;
Define la configuración de seguridad para el transporte.  
  
## Sintaxis  
  
```  
  
<netMsmqBinding>  
    <binding>  
    <security>  
         <transport msmqAuthenticationMode="None/WindowsDomain/Certificate"  
            msmqEncryptionAlgorithm="RC4Stream/AES"  
            msmqProtectionLevel="None/Sign/EncryptAndSign"  
            msmqSecureHashAlgorithm="MD5/SHA1/SHA256/SHA512" />  
    </security>  
   </binding>  
</netMsmqBinding>  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|msmqAuthenticationMode|Especifica cómo el transporte de MSMQ debe autenticar el mensaje.  Los valores válidos son los siguientes:<br /><br /> -   None: sin autenticación<br />-   WindowsDomain: el mecanismo de autenticación utiliza Active Directory para recuperar el certificado X.509 para el identificador de seguridad asociado al mensaje.  Esto se utiliza a continuación para comprobar el ACL de la cola para asegurarse que el usuario tiene el permiso de escritura para la cola.<br />-   Certificate: el canal recupera el certificado del almacén de certificados.<br /><br /> De manera predeterminada, es `WindowsDomain`.<br /><br /> Si este atributo se establece en `None`, el atributo `msmqProtectionLevel` también debe establecerse como `None`.  Este atributo es del tipo <xref:System.ServiceModel.MsmqAuthenticationMode>.|  
|msmqEncryptionAlgorithm|Especifica el algoritmo que se va a utilizar para el cifrado de mensajes en la conexión al transferir los mensajes entre los administradores de la cola de mensajes.  Los valores válidos son los siguientes:<br /><br /> -   RC4Stream<br />-   AES<br />-   El valor predeterminado es `RC4Stream`.  Este atributo es del tipo <xref:System.ServiceModel.MsmqEncryptionAlgorithm>.|  
|msmqProtectionLevel|Especifica la manera en que los mensajes se protegen en el nivel de transporte de MSMQ.  El cifrado asegura la integridad del mensaje, mientras que la firma y el cifrado aseguran la integridad del mensaje y el no repudio.  Es decir, el mensaje procedió del remitente y el remitente es quien dice ser.  Los valores válidos son los siguientes:<br /><br /> -   None: sin protección.<br />-   Sign: se firman los mensajes.<br />-   EncryptAndSign: Los mensajes se cifran y firman.<br />-   De manera predeterminada, es `Sign`.|  
|msmqSecureHashAlgorithm|Especifica el algoritmo hash que se va a utilizar para calcular la síntesis del mensaje.  Los valores válidos son los siguientes:<br /><br /> -   MD5<br />-   SHA1<br />-   SHA256<br />-   SHA512<br /><br /> De manera predeterminada, es `SHA1`.  Este atributo es del tipo <xref:System.ServiceModel.MsmqSecureHashAlgorithm>.|  
  
### Elementos secundarios  
 Ninguna  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<seguridad\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-netmsmqbinding.md)|Define los valores de seguridad de transporte para transportes en cola.|  
  
## Vea también  
 <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>   
 <xref:System.ServiceModel.Configuration.NetMsmqSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.NetMsmqSecurity.Transport%2A>   
 <xref:System.ServiceModel.MsmqTransportSecurity>   
 [Colas en WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Protección de servicios y clientes](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Enlaces](../../../../../docs/framework/wcf/bindings.md)   
 [Configuración de enlaces proporcionados por el sistema](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/es-es/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<enlace\>](../../../../../docs/framework/misc/binding.md)