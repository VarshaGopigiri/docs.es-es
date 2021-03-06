---
title: "Contratos de datos compatibles con el reenv&#237;o | Microsoft Docs"
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
helpviewer_keywords: 
  - "contratos de datos [WCF], compatibilidad con versiones posteriores"
ms.assetid: 413c9044-26f8-4ecb-968c-18495ea52cd9
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Contratos de datos compatibles con el reenv&#237;o
Una característica del sistema de contrato de datos de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] es que los contratos pueden evolucionar con el tiempo sin causar interrupciones.Es decir, un cliente con una versión anterior de un contrato de datos puede comunicarse con un servicio con una versión más reciente del mismo contrato de datos, o un cliente con una versión más reciente de un contrato de datos puede comunicarse con una versión anterior del mismo contrato de datos.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Procedimientos recomendados: Creación de versiones de contratos de datos](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
 Puede aplicar la mayoría de las características del control de versiones en la medida que se necesite cuando se crean las nuevas versiones de un contrato del dato existente.Sin embargo, una característica del control de versiones, *round\-tripping \(recorridos de ida y vuelta\)*, debe estar integrada en el tipo de la primera versión para que funcione correctamente.  
  
## Round\-Tripping \(recorrido de ida y vuelta\)  
 Round\-tripping tiene lugar cuando los datos pasan de una nueva versión a una versión anterior y de vuelta a la nueva versión de un contrato de datos.El round\-tripping garantiza que no se pierdan datos.Habilitar el round\-tripping hace que el tipo sea compatible por adelantado con cualquier cambio futuro admitido por el modelo de control de versiones del contrato de datos.  
  
 Para habilitar el round\-tripping para un tipo determinado, el tipo debe implementar la interfaz <xref:System.Runtime.Serialization.IExtensibleDataObject>.La interfaz contiene una propiedad, <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> \(que devuelve el tipo <xref:System.Runtime.Serialization.ExtensionDataObject> \).La propiedad almacena cualquier dato de las versiones futuras del contrato de datos que es desconocido para la versión actual.  
  
### Ejemplo  
 El siguiente contrato de datos no compatible por adelantado con los cambios futuros.  
  
 [!code-csharp[C_DataContract#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#7)]
 [!code-vb[C_DataContract#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#7)]  
  
 Para hacer que el tipo sea compatible con los cambios futuros \(como agregar un nuevo miembro de datos denominado "phoneNumber"\), implemente la interfaz <xref:System.Runtime.Serialization.IExtensibleDataObject>.  
  
 [!code-csharp[C_DataContract#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#8)]
 [!code-vb[C_DataContract#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#8)]  
  
 Cuando la infraestructura de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] encuentra datos que no forman parte del contrato de datos original, los datos se almacenan en la propiedad y se conservan.No se procesa para nada más, salvo para el almacenamiento temporal.Si el objeto se devuelve a donde se originó, se devuelven también los datos originales \(desconocidos\).Por consiguiente, los datos han realizado un viaje de ida y vuelta \(round trip\) hasta y desde el extremo de origen sin sufrir pérdidas.Tenga en cuenta, sin embargo, que si el extremo de origen exigiera que se procesasen los datos, la expectativa no se cumple, y el extremo debe detectar y adaptar el cambio de algún modo.  
  
 El tipo <xref:System.Runtime.Serialization.ExtensionDataObject> no contiene ningún método público ni propiedades.Por tanto, es imposible obtener acceso directo a los datos almacenados dentro de la propiedad <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>.  
  
 La característica de round\-tripping puede desactivarse, estableciendo `ignoreExtensionDataObject` en `true` en el constructor <xref:System.Runtime.Serialization.DataContractSerializer> o estableciendo la propiedad <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> en `true` en el <xref:System.ServiceModel.ServiceBehaviorAttribute>.Cuando esta característica está deshabilitada, el deserializador no rellenará la propiedad <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> y el serializador no emitirá el contenido de la propiedad.  
  
## Vea también  
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 <xref:System.Runtime.Serialization.ExtensionDataObject>   
 [Versiones de contratos de datos](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)   
 [Procedimientos recomendados: Creación de versiones de contratos de datos](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)