---
title: "C&#243;mo: Mejorar el tiempo de inicio de las aplicaciones cliente WCF mediante XmlSerializer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21093451-0bc3-4b1a-9a9d-05f7f71fa7d0
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# C&#243;mo: Mejorar el tiempo de inicio de las aplicaciones cliente WCF mediante XmlSerializer
Los servicios y las aplicaciones cliente que utilizan tipos de datos que son serializables utilizando <xref:System.Xml.Serialization.XmlSerializer> generan y compilan el código de la serialización para esos tipos de datos en el tiempo de ejecución, lo que se puede traducir en un rendimiento de inicio lento.  
  
> [!NOTE]
>  El código de serialización generado previamente solo puede usarse en aplicaciones cliente y no en servicios.  
  
 [Herramienta de utilidad de metadatos de ServiceModel \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) puede mejorar el rendimiento de inicio de estas aplicaciones generando el código de serialización necesario a partir de los ensamblados compilados para la aplicación.Svcutil.exe genera el código de serialización para todos los tipos de datos utilizados en contratos de servicios en el ensamblado de aplicación de compilación que se puede serializar utilizando <xref:System.Xml.Serialization.XmlSerializer>.Los contratos de operación y servicio que utiliza el <xref:System.Xml.Serialization.XmlSerializer> se marcan con <xref:System.ServiceModel.XmlSerializerFormatAttribute>.  
  
### Para generar el código de serialización de XmlSerializer  
  
1.  Compile su servicio o código de cliente en uno o más ensamblados.  
  
2.  Abra un símbolo del sistema de SDK.  
  
3.  En el símbolo del sistema, inicie la herramienta Svcutil.exe mediante el formato siguiente.  
  
    ```  
    svcutil.exe /t:xmlSerializer  <assemblyPath>*  
    ```  
  
     El argumento `assemblyPath` especifica la ruta de acceso a un ensamblado que contiene tipos de contrato de servicio.Svcutil.exe genera el código de serialización para todos los tipos de datos utilizados en contratos de servicios en el ensamblado de aplicación de compilación que se puede serializar utilizando <xref:System.Xml.Serialization.XmlSerializer>.  
  
     Svcutil.exe solo puede generar código de serialización de C\#.Un archivo de código fuente se genera para cada ensamblado de entrada.No puede usar el modificador **\/language** para cambiar el lenguaje del código generado.  
  
     Para especificar la ruta de acceso a ensamblados dependientes, use la opción **\/reference**.  
  
4.  Haga que el código de serialización generado esté disponible para su aplicación utilizando una de las opciones siguientes:  
  
    1.  Compile el código de serialización generado en un ensamblado independiente con el nombre \[*original assembly*\].XmlSerializers .dll \(por ejemplo, MyApp.XmlSerializers.dll\).Su aplicación debe poder cargar el ensamblado, que se debe firmar con la misma clave como el ensamblado original.Si vuelve a compilar el ensamblado original, debe volver a generar el ensamblado de serialización.  
  
    2.  Compile el código de serialización generado en un ensamblado independiente y utilice <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute> en el contrato de servicios que utiliza <xref:System.ServiceModel.XmlSerializerFormatAttribute>.Establezca las propiedades <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> o <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A> para señalar al ensamblado de serialización compilado.  
  
    3.  Compile el código de serialización generado en su ensamblado de aplicación y agregue el <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute> al contrato de servicios que utiliza el <xref:System.ServiceModel.XmlSerializerFormatAttribute>.No establezca las propiedades <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.AssemblyName%2A> ni <xref:System.Xml.Serialization.XmlSerializerAssemblyAttribute.CodeBase%2A>.Se supone que el ensamblado de serialización predeterminado es el ensamblado actual.  
  
## Ejemplo  
 El siguiente comando genera los tipos de serialización para los tipos de `XmlSerializer` utilizados por cualquier contrato de servicios en el ensamblado.  
  
```  
svcutil /t:xmlserializer myContractLibrary.exe  
```  
  
## Vea también  
 [Herramienta de utilidad de metadatos de ServiceModel \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)