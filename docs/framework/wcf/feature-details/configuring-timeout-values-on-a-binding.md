---
title: "Configuraci&#243;n de los valores de tiempo de espera en un enlace | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5c825a2-b48f-444a-8659-61751ff11d34
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Configuraci&#243;n de los valores de tiempo de espera en un enlace
Hay varias configuraciones de tiempo de espera disponibles en los enlaces de WCF.  Establecer estas configuraciones de tiempo de espera correctamente puede mejorar no solo el rendimiento del servicio sino también desempeñar un papel en la facilidad de uso y la seguridad del servicio.  Los tiempos de espera siguientes están disponibles en los enlaces de WCF:  
  
1.  OpenTimeout  
  
2.  CloseTimeout  
  
3.  SendTimeout  
  
4.  ReceiveTimeout  
  
## Tiempos de espera de enlace de WCF  
 Cada uno de los valores descritos en este tema se crea en el propio enlace, en código o configuración.  El código siguiente muestra cómo establecer mediante programación los tiempos de espera en un enlace de WCF en el contexto de un servicio autohospedado.  
  
```csharp  
public static void Main()  
        {  
            Uri baseAddress = new Uri("http://localhost/MyServer/MyService");  
  
            try  
            {  
                ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService));  
  
                WSHttpBinding binding = new WSHttpBinding();  
                binding.OpenTimeout = new TimeSpan(0, 10, 0);  
                binding.CloseTimeout = new TimeSpan(0, 10, 0);  
                binding.SendTimeout = new TimeSpan(0, 10, 0);  
                binding.ReceiveTimeout = new TimeSpan(0, 10, 0);  
  
                serviceHost.AddServiceEndpoint("ICalculator", binding, baseAddress);  
                serviceHost.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
            }  
            catch (CommunicationException ex)  
            {  
                // Handle exception ...  
            }  
        }  
  
```  
  
 En el ejemplo siguiente se muestra cómo configurar tiempos de espera en un enlace en un archivo de configuración.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding openTimeout="00:10:00"   
                 closeTimeout="00:10:00"   
                 sendTimeout="00:10:00"   
                 receiveTimeout="00:10:00">  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
  </system.serviceModel>  
  
```  
  
 Se puede encontrar más información sobre estos valores en la documentación de la clase <xref:System.ServiceModel.Channels.Binding>.  
  
### Tiempos de espera del lado cliente  
 En el lado cliente:  
  
1.  SendTimeout – se usa para inicializar OperationTimeout, que controla el proceso completo de enviar un mensaje, incluido recibir un mensaje de respuesta para una operación de servicio de solicitud y respuesta.  Este tiempo de espera también se aplica al enviar mensajes de respuesta de un método de contrato de devolución de llamada.  
  
2.  OpenTimeout – se usa al abrir canales cuando no se especifica ningún valor de tiempo de espera explícito  
  
3.  CloseTimeout – se usa al cerrar canales cuando no se especifica ningún valor de tiempo de espera explícito  
  
4.  ReceiveTimeout – no se usa  
  
### Tiempos de espera del lado cliente  
 En el lado de servicio:  
  
1.  SendTimeout, OpentTimeout, CloseTimeout son iguales que en el cliente  
  
2.  ReceiveTimeout – lo usa el nivel de marco de trabajo de servicio para inicializar el tiempo de espera de sesión inactiva que controla cuánto tiempo puede estar inactiva una sesión antes de que se agote el tiempo de espera.