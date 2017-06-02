---
title: "&lt;&lt;reliableSession&gt;&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 129b4a59-37f0-4030-b664-03795d257d29
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# &lt;&lt;reliableSession&gt;&gt;
Define el valor para los mensajes de confianza de WS.  Cuando este elemento se agrega a un enlace personalizado, el canal resultante puede admitir las convicciones de la entrega exactamente una vez.  
  
## Sintaxis  
  
```  
  
<reliableSession acknowledgementInterval="TimeSpan"  
        flowControlEnabled="Boolean"   
    inactivityTimeout="TimeSpan"  
    maxPendingChannels="Integer"  
    maxRetryCount="Integer"   
        maxTransferWindowSize="Integer"  
    reliableMessagingVersion="Default/WSReliableMessagingFebruary2005/WSReliableMessaging11"  
    ordered="Boolean" />  
```  
  
## Atributos y elementos  
 En las siguientes secciones se describen los atributos, los elementos secundarios y los elementos primarios.  
  
### Atributos  
  
|Atributo|Descripción|  
|--------------|-----------------|  
|acknowledgementInterval|<xref:System.TimeSpan> que contiene el intervalo de tiempo máximo que el canal va a esperar para enviar un reconocimiento para los mensajes recibidos hasta ese punto.  El valor predeterminado es 00:00:02.|  
|flowControlEnabled|Un valor booleano que indica si se activa el control de flujo avanzado, una implementación específica de Microsoft de control de flujo para la mensajería de confianza de WS.  De manera predeterminada, es `true`.|  
|inactivityTimeOut|Un <xref:System.TimeSpan> que especifica el tiempo máximo durante el cual el canal va a permitir a la otra parte de la comunicación no enviar ningún mensaje sin que se produzca un error.  El valor predeterminado es 00:10:00.<br /><br /> La actividad en un canal se define como la recepción de una aplicación o mensajes de infraestructura.  Esta propiedad controla el tiempo máximo para mantener activa una sesión inactiva.  Si transcurre más tiempo sin actividad, la sesión es finalizada por la infraestructura y los errores del canal. **Note:**  No es necesario que la aplicación envíe periódicamente mensajes para mantener la conexión viva.|  
|maxPendingChannels|Un entero que especifica el número máximo de canales que pueden esperar en el agente de escucha para ser aceptados.  Este valor debe estar comprendido entre 1 y 16384, ambos inclusive.  El valor predeterminado es 4.<br /><br /> Los canales están pendientes cuando esperan a ser aceptados.  Una vez alcanzado ese límite, no se crea ningún canal.  Más bien, se colocan en modo pendiente hasta que este número baje \(al aceptar los canales pendientes\).  Éste es un límite por generador.<br /><br /> Cuando se alcanza el umbral y una aplicación remota intenta establecer una nueva sesión fiable, se deniega la solicitud y falla la operación abierta que pidió confirmación.  Este límite no se aplica al número de canales pendientes de la salida.|  
|maxRetryCount|Un entero que especifica el número máximo de horas que un canal fiable intenta retransmitir un mensaje para el que no ha recibido reconocimiento, yendo a Enviar en su canal subyacente.<br /><br /> Este valor debería ser mayor que cero.  El valor predeterminado es 8.<br /><br /> Este valor debería ser un entero mayor que cero.  Si un reconocimiento no se recibe después de la última retransmisión, el canal falla.<br /><br /> Se considera que un mensaje es transferido si el destinatario ha confirmado su entrega.<br /><br /> Si no se ha recibido reconocimiento tras un cierto tiempo de un mensaje que se ha transmitido, la infraestructura retransmite automáticamente el mensaje.  La infraestructura intenta reenviar el mensaje el máximo número de veces especificado por esta propiedad.  Si un reconocimiento no se recibe después de la última retransmisión, el canal falla.<br /><br /> La infraestructura utiliza un algoritmo de espera exponencial para determinar cuándo retransmitir, en función del tiempo medio calculado de ida y vuelta.  El tiempo empieza inicialmente 1 segundo antes de la retransmisión y duplica el retraso en cada intento, lo que da como resultado aproximadamente 8,5 minutos que pasan entre el primer intento de la transmisión y el último intento de la retransmisión.  El tiempo del primer intento de retransmisión se ajusta al cálculo del tiempo de ida y vuelta y varía según el período de tiempo adicional que resulta del número de intentos que se necesitan.  Esto permite que el tiempo de retransmisión se adapte dinámicamente a las condiciones variantes de la red.|  
|maxTransferWindowSize|Un entero que especifica el tamaño máximo del búfer.  Los valores válidos están comprendidos entre 1 y 4096, ambos incluidos.<br /><br /> En lo que respecta al cliente, este atributo define el tamaño máximo del búfer utilizado por un canal fiable para contener mensajes no confirmados todavía por el receptor.  La unidad de la cuota es un mensaje.  Si el búfer está lleno, las operaciones de ENVÍO siguientes se bloquean.<br /><br /> En lo que respecta al receptor, este atributo define el tamaño máximo del búfer utilizado por el canal para almacenar mensajes entrantes no distribuidos en la aplicación.  Si el búfer está lleno, los mensajes siguientes son quitados por el receptor y requieren la retransmisión del cliente.|  
|ordered|Un booleano que especifica si se garantiza que los mensajes lleguen en el orden en el que fueron enviados.  Si este valor es `false`, los mensajes pueden llegar desordenados.  De manera predeterminada, es `true`.|  
|reliableMessagingVersion|Un valor válido de <xref:System.ServiceModel.ReliableMessagingVersion> que especifica la versión WS\-ReliableMessaging que se va a utilizar.|  
  
### Elementos secundarios  
 Ninguna  
  
### Elementos primarios  
  
|Elemento|Descripción|  
|--------------|-----------------|  
|[\<enlace\>](../../../../../docs/framework/misc/binding.md)|Define todas las funcionalidades de enlace del enlace personalizado.|  
  
## Comentarios  
 Las sesiones fiables proporcionan las características para la mensajería y las sesiones de confianza.  La mensajería de confianza reintenta la comunicación en caso de error y permite especificar garantías de entrega, como la llegada en orden de los mensajes.  Las sesiones mantienen el estado de los clientes entre llamadas.  Este elemento también proporciona, de manera opcional, la entrega ordenada de mensajes.  Esta sesión implementada puede cruzar SOAP y los intermediarios de transporte.  
  
 Cada elemento de enlace representa un paso del procesamiento al enviar y recibir mensajes.  En tiempo de ejecución, los elementos de enlace crean los generadores de canales y las escuchas que son necesarios para compilar pilas de canal entrantes y salientes necesarias para enviar y recibir los mensajes.  `reliableSession` proporciona un nivel opcional en la pila que puede establecer una sesión confiable entre los extremos y configurar el comportamiento de esta sesión.  
  
 Para obtener más información, consulta [Sesiones de confianza](../../../../../docs/framework/wcf/feature-details/reliable-sessions.md).  
  
## Ejemplo  
 El ejemplo siguiente muestra cómo configurar un enlace personalizado con varios elementos de codificación de mensajes y transporte, habilitando sobre todo sesiones fiables, que mantienen el estado del cliente y especifican las garantías de la entrega en orden.  Esta característica se configura en los archivos de configuración de la aplicación para el cliente y el servicio.  El ejemplo muestra la configuración de servicio.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- This endpoint is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc  -->  
        <!-- specify customBinding binding and a binding configuration to use -->  
        <endpoint address=""  
                  binding="customBinding"  
                  bindingConfiguration="Binding1"   
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- The mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <!-- custom binding configuration - configures HTTP transport, reliable sessions -->  
    <bindings>  
      <customBinding>  
        <binding name="Binding1">  
          <reliableSession />  
          <security authenticationMode="SecureConversation"  
                     requireSecurityContextCancellation="true">  
          </security>  
          <compositeDuplex />  
          <oneWay />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8" />  
          <httpTransport authenticationScheme="Anonymous" bypassProxyOnLocal="false"  
                        hostNameComparisonMode="StrongWildcard"   
                        proxyAuthenticationScheme="Anonymous" realm=""   
                        useDefaultWebProxy="true" />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## Vea también  
 <xref:System.ServiceModel.Configuration.ReliableSessionElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>   
 [Sesiones de confianza](../../../../../docs/framework/wcf/feature-details/reliable-sessions.md)   
 [Enlaces](../../../../../docs/framework/wcf/bindings.md)   
 [Extensión de enlaces](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Enlaces personalizados](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)