---
title: "CustomChannelsTester | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee1fa307-98b1-4647-8860-2e9217ba6082
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# CustomChannelsTester
El `CustomChannelsTester` es una herramienta que se utiliza para probar las implementaciones del canal personalizadas contra un conjunto de contratos de servicios predefinidos.  Puede seleccionar el conjunto de contratos de servicios y pasarlo a la herramienta utilizando un archivo XML.  La herramienta genera a continuación el servicio y el cliente que ejerce sus implementaciones del canal personalizadas durante el intercambio de mensajes.  
  
### Para compilar la herramienta  
  
1.  Para compilar la solución, siga las instrucciones de [Compilación de los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
2.  Al compilar la solución, se generan tres archivos: CustomChannelsTester.exe, TestSpec.xml y SampleRun.cmd.  SampleRun.cmd del archivo tiene una línea de comandos del ejemplo que muestra cómo utilizar esta herramienta para probar el ejemplo [Transporte: UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
### Para ejecutar la herramienta  
  
-   Escriba el siguiente comando en el símbolo del sistema:  
  
    ```  
    CustomChannelsTester.exe /binding:YourCustomBindngName /dll:TheAssemblyWhereThisTypeisDefined /testspec:XmlFileNameWhichContainsTestOptions  
    ```  
  
     Se requiere utilizar la opción `/binding`.  
  
     Se requiere `/dll` si "enlace" no es ningún enlace proporcionado por el sistema proporcionado por [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
     `/testspec` es opcional.  
  
     Esto crea el servidor y los clientes basados en las características técnicas de pruebas y el enlace.  
  
     Ejecuta el cliente y el servidor y devuelve los resultados.  
  
     A continuación, se muestra el ejemplo XML para la descripción de las características técnicas de pruebas \(testspec.xml\):  
  
    ```  
    <TestSpec xmlns="http://WCF/TestSpec" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >  
    <ServiceContract>  
    <!-- Test a contract which has oneway / twoway operations. If you set ExpandAll = true, both types of contracts are tested -->    <IsOneWay ExpandAll="true">true</IsOneWay>  
    <!-- Test a contract with Asynchronous / Synchronous Operations-->  
        <IsAsync>false</IsAsync>   
    <!-- Test a sessionful / sessionless contract-->      
        <IsSession ExpandAll="true">true</IsSession>  
    <!-- If the Service Contract includes a CallBack Contract-->      
        <IsCallBack ExpandAll="true">true</IsCallBack>  
    </ServiceContract>  
    <TestDetails>  
    <!-- Name of the machine that runs the server - required if you want to run the test crossmachine-->  
        <ServerName>ReplaceThisWithTheServerMachineName</ServerName>  
    <!-- Port Number - Optional-->  
        <Port>8000</Port>  
    <!--URI for the callBack address for the CLient. The client will receive the messages from the server on this address in case of a CallBack Contract-->  
        <ClientCallBackAddress/>      
    <!-- Duration (in sec) after the server has started, it times out - optional(default = 300sec) -->  
        <ServerTimeout>300</ServerTimeout>  
    <!-- Duration (in sec) before the Client initializes -optional(default = 60sec) -->  
        <ClientTimeout>60</ClientTimeout>  
    <!-- Number of clients for each service - optional(default = 1) -->  
        <NumberOfClients>1</NumberOfClients>  
    <!-- Number of messages each client sends to the service - optional(default = 1) -->  
        <MessagesPerClient>1</MessagesPerClient>  
    </TestDetails>  
    </TestSpec>  
    ```  
  
## Vea también