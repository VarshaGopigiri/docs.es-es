---
title: "Extensi&#243;n de la capa de canales | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "extensión de canales [WCF]"
ms.assetid: 4238db74-2fb6-4dc8-a326-f58527230810
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Extensi&#243;n de la capa de canales
La capa de canales es responsable del intercambio de mensajes entre clientes y servicios.Las extensiones de canal pueden implementar nueva funcionalidad de protocolo, como seguridad o funcionalidad de transporte, como implementar un nuevo transporte de red para llevar los mensajes SOAP.  
  
## En esta sección  
 [Información general del modelo de canales](../../../../docs/framework/wcf/extending/channel-model-overview.md)  
 Proporciona una información general de alto nivel de qué canales son, las características que proporcionan y cómo funcionan tanto en una aplicación de servicio como de cliente.  
  
 [Desarrollo de canales](../../../../docs/framework/wcf/extending/developing-channels.md)  
 Describe a fondo las funciones que representan los diversos tipos de infraestructuras de canales, cómo funciona el motor de estado y el ciclo de vida de estado, cómo administrar excepciones y errores, cómo implementar la compatibilidad de metadatos y cómo funcionan los canales con codificadores de mensajes.  
  
 [Codificadores personalizados](../../../../docs/framework/wcf/extending/custom-encoders.md)  
 Describe el papel que los codificadores del mensaje juegan en los canales y cómo crear uno.  
  
 [Actualizaciones personalizadas de secuencias](../../../../docs/framework/wcf/extending/custom-stream-upgrades.md)  
 Describe el proceso de actualización de las secuencias proporcionadas mediante transportes orientados a secuencias.