---
title: "Sesiones seguras | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7b50602f-d7b5-42e9-8e92-1f0413df0d8b
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# Sesiones seguras
Una característica de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] son las sesiones fiables que garantizan que los mensajes se reciben en el orden que se enviaron.Los temas de esta sección discuten las implicaciones de seguridad a tener en cuenta a la hora de crear una sesión confiable.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] sesiones confiables, vea [Uso de sesiones](../../../../docs/framework/wcf/using-sessions.md).  
  
> [!NOTE]
>  Si se requiere la suplantación en Windows XP, utilice una sesión segura sin un token de contexto de seguridad con estado \(SCT\).Cuando se utilizan SCT con estado con suplantación, se produce una <xref:System.InvalidOperationException>.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Escenarios no admitidos](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md).  
  
## En esta sección  
  
|||  
|-|-|  
|[Conversaciones y sesiones seguras](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)|Las conversaciones seguras y las sesiones seguras hacen referencia al mismo concepto.En este tema se explica la manera en la que funciona una conversación segura, así como cuándo y por qué utilizar el modelo.|  
|[Cómo: Crear una sesión segura](../../../../docs/framework/wcf/feature-details/how-to-create-a-secure-session.md)|Tutorial sobre los fundamentos de la creación de sesiones seguras.|  
|[Cómo: Crear un token de contexto de seguridad para una sesión segura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)|Describe los pasos necesarios para la creación de una batería de servidores web que mantendrán estado y sesiones con clientes.|  
|[Consideraciones de seguridad para sesiones seguras](../../../../docs/framework/wcf/feature-details/security-considerations-for-secure-sessions.md)|Describe consideraciones especiales de las sesiones seguras.|  
  
## Referencia  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
## Secciones relacionadas  
 [Sesiones, creación de instancias y simultaneidad](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)  
  
 [Diseño e implementación de servicios](../../../../docs/framework/wcf/designing-and-implementing-services.md)  
  
## Vea también  
 [Cómo: Habilitar la detección de repetición de mensajes](../../../../docs/framework/wcf/feature-details/how-to-enable-message-replay-detection.md)   
 [Ataques por repetición](../../../../docs/framework/wcf/feature-details/replay-attacks.md)   
 [Cómo crear un servicio que requiere sesiones](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)