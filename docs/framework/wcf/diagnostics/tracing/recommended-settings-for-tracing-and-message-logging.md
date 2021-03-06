---
title: "Configuraci&#243;n recomendada para el seguimiento y el registro de mensajes | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6aca6e8-704e-4779-a9ef-50c46850249e
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Configuraci&#243;n recomendada para el seguimiento y el registro de mensajes
En este tema se describen la traza recomendada y configuración del registro de mensajes para los entornos operativos diferentes.  
  
## Configuración recomendada para un entorno de producción  
 Para un entorno de producción, si está utilizando los orígenes de seguimiento de WCF, establezca `switchValue` a Advertencia.  Si está utilizando el origen de seguimiento de WCF `System.ServiceModel`, establezca el atributo `switchValue` a `Warning` y el atributo `propagateActivity` a `true`.  Si está utilizando un origen de seguimiento definido por un usuario, establezca el atributo `switchValue` a `Warning, ActivityTracing`.  Esto se puede hacer manualmente con [Herramienta del editor de configuración \(SvcConfigEditor.exe\)](../../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).  Si no visualiza una repercusión en el rendimiento, puede establecer el atributo `switchValue` en `Information` en todos los casos mencionados previamente, lo cual genera una cantidad bastante grande de información de seguimiento.  El ejemplo siguiente muestra estos valores recomendados.  
  
```  
<configuration>  
 <system.diagnostics>  
  <sources>  
    <source name="System.ServiceModel"  
            switchValue="Warning"  
            propagateActivity="true" >  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="myUserTraceSource"  
            switchValue="Warning, ActivityTracing">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
  </sources>  
  <sharedListeners>  
    <add name="xml"  
         type="System.Diagnostics.XmlWriterTraceListener"  
               initializeData="C:\logs\Traces.svclog" />  
  </sharedListeners>  
 </system.diagnostics>  
  
<system.serviceModel>  
  <diagnostics wmiProviderEnabled="true">  
  </diagnostics>  
 </system.serviceModel>  
</configuration>  
```  
  
## Configuración recomendada para la implementación o depurando  
 Para la implementar o depurar el entorno, elija `Information` o `Verbose`, junto con `ActivityTracing` para o un origen de seguimiento definido por el usuario o `System.ServiceModel`.  Para mejorar la depuración, debería agregar también un origen de seguimiento adicional \(`System.ServiceModel.MessageLogging`\) a la configuración para habilitar el registro de mensajes.  Tenga en cuenta que el atributo `switchValue` no tiene ningún impacto en este origen de seguimiento.  
  
 El ejemplo siguiente muestra los valores recomendados, mediante un agente de escucha compartido que utiliza `XmlWriterTraceListener`.  
  
```  
<configuration>  
 <system.diagnostics>  
  <sources>  
    <source name="System.ServiceModel"  
            switchValue="Information, ActivityTracing"  
            propagateActivity="true" >  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="System.ServiceModel.MessageLogging">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="myUserTraceSource"  
            switchValue="Information, ActivityTracing">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
  </sources>  
  <sharedListeners>  
    <add name="xml"  
         type="System.Diagnostics.XmlWriterTraceListener"  
               initializeData="C:\logs\Traces.svclog" />  
  </sharedListeners>  
 </system.diagnostics>  
  
 <system.serviceModel>  
  <diagnostics wmiProviderEnabled="true">  
      <messageLogging   
           logEntireMessage="true"   
           logMalformedMessages="true"  
           logMessagesAtServiceLevel="true"   
           logMessagesAtTransportLevel="true"  
           maxMessagesToLog="3000"   
       />  
  </diagnostics>  
 </system.serviceModel>  
</configuration>  
```  
  
## Utilizar WMI para modificar la configuración  
 Puede utilizar WMI para cambiar la configuración en el tiempo de ejecución \(habilitando el atributo `wmiProviderEnabled` en la configuración, tal y como se ha mostrado previamente en el ejemplo de configuración\).  Por ejemplo, puede utilizar WMI dentro del CIM Studio para cambiar el origen de seguimiento desde Advertencia a Información en tiempo de ejecución.  Debe ser consciente de que el coste del rendimiento de la depuración activa de este modo puede ser muy elevado.  Para obtener más información sobre el uso de WMI, consulte el tema [Utilización del instrumental de administración de Windows \(WMI\) para diagnósticos](../../../../../docs/framework/wcf/diagnostics/wmi/index.md).  
  
## Habilitación de eventos correlativos en el seguimiento ASP.NET  
 Los eventos ASP.NET no establecen el id. de correlación \(ActivityID\) a menos que esté activado el seguimiento de evento ASP.NET.  Para visualizar correctamente eventos correlativos, debe activar el seguimiento de eventos ASP.NET mediante el siguiente comando de la consola de comandos, al que se puede llamar mediante **Inicio**, **Ejecutar** y escribiendo **cmd**,  
  
```  
logman start mytrace -pf logman.providers -o test.etl –ets  
```  
  
 Para desactivar el seguimiento de eventos ASP.NET, utilice el siguiente comando,  
  
```  
logman stop mytrace -ets  
```  
  
## Vea también  
 [Utilización del instrumental de administración de Windows \(WMI\) para diagnósticos](../../../../../docs/framework/wcf/diagnostics/wmi/index.md)