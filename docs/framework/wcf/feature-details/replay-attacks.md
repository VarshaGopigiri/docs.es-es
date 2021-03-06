---
title: "Ataques por repetici&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7a17e040-93cd-4432-81b9-9f62fec78c8f
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Ataques por repetici&#243;n
Un *ataque por repetición* se produce cuando un atacante copia una secuencia de mensajes entre dos partes y reproduce la secuencia a una o más partes.A menos que se mitigue, el equipo objeto del ataque procesa la secuencia como mensajes legítimos, produciendo una gama de malas consecuencias, como pedidos redundantes de un elemento.  
  
## Los enlaces pueden estar sujetos a ataques de reflexión  
 Los *ataques de reflexión* son repeticiones de mensajes devueltos a un remitente como si procedieran del receptor como la respuesta.La *detección de la repetición* estándar en el mecanismo de [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] no trata esto de forma automática.  
  
 Los ataques de reflexión se mitigan de forma predeterminada porque el modelo del servicio de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] agrega un Id. de mensaje firmado a los mensajes de solicitud y espera un encabezado `relates-to` firmado en los mensajes de respuesta.Por consiguiente, el mensaje de solicitud no se puede volver a reproducir como una respuesta.En los escenarios de mensaje confiables \(RM\) seguros, los ataques de reflexión se mitigan porque:  
  
-   Los esquemas de la secuencia de creación y los del mensaje de respuesta de la secuencia de creación son diferentes.  
  
-   Para las secuencias símplex, los mensajes de secuencias que envía el cliente no se pueden volver a reproducir porque el cliente no puede entender tales mensajes.  
  
-   Para las secuencias dúplex, los dos Id. de secuencia deben ser únicos.Así, un mensaje de secuencia saliente no se puede volver a reproducir como un mensaje de secuencia de entrada \(todos los encabezados de secuencia y cuerpos también se firman\).  
  
 Los únicos enlaces que son susceptibles a los ataques de reflexión son aquellos sin WS\-Addressing: los enlaces personalizados que tienen WS\-Addressing deshabilitado y utilizan la seguridad basada en clave simétrica.El <xref:System.ServiceModel.BasicHttpBinding> no utiliza WS\-Addressing de forma predeterminada, pero no utiliza la seguridad basada en clave simétrica de tal modo que puede ser vulnerable a este ataque.  
  
 La mitigación para los enlaces personalizados consiste no establecer el contexto de seguridad o requerir encabezados WS\-Addressing.  
  
## Batería de servidores web: El atacante vuelve a reproducir la solicitud en varios nodos  
 Un cliente utiliza un servicio que se implementa en una batería de servidores web.Un atacante vuelve a reproducir una solicitud que se envió de un nodo de la batería a otro nodo de la batería.Además, si se reinicia un servicio, se vacía la caché de repetición, lo que capacita a un atacante para volver a realizar la solicitud.\(La caché contiene valores de firmas de mensajes utilizados y vistos con anterioridad y evita las repeticiones de modo que esas firmas solo se puedan utilizar una vez.Las memorias caché de repetición no se comparten en una batería de servidores web\).  
  
 Las mitigaciones incluyen:  
  
-   Utilice la seguridad de modo de mensaje con tokens de contexto de seguridad con estado \(con o sin conversación segura habilitada\).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Cómo: Crear un token de contexto de seguridad para una sesión segura](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
-   Configure el servicio para utilizar la seguridad de nivel de transporte.  
  
## Vea también  
 [Consideraciones de seguridad](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)   
 [Divulgación de información](../../../../docs/framework/wcf/feature-details/information-disclosure.md)   
 [Elevación de privilegio](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)   
 [Denegación de servicio](../../../../docs/framework/wcf/feature-details/denial-of-service.md)   
 [Manipulación](../../../../docs/framework/wcf/feature-details/tampering.md)   
 [Escenarios no admitidos](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)