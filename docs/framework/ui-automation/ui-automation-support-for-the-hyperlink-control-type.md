---
title: "UI Automation Support for the Hyperlink Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Hyperlink control type"
  - "UI Automation, Hyperlink control type"
  - "control types, Hyperlink"
ms.assetid: 110cceea-5932-4955-a1a6-13afc51422b2
caps.latest.revision: 22
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 22
---
# UI Automation Support for the Hyperlink Control Type
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para ver la información más reciente acerca de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: automatización de la interfaz de usuario](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 En este tema se ofrece información sobre la compatibilidad de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] con el tipo de control Hyperlink. En [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], un tipo de control es un conjunto de condiciones que debe cumplir un control para poder usar la propiedad <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Entre las condiciones se incluyen instrucciones específicas para la estructura de árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], los patrones de control y los valores de propiedad de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
 Los controles de hipervínculo permiten que los usuarios puedan navegar dentro de una página, de una página a otra y que abran ventanas.  
  
 En las secciones siguientes se definen la estructura de árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] necesaria, las propiedades, los patrones de control y los eventos para el tipo de control Hyperlink. Los requisitos de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] se aplican a todos los controles de hipervínculo, ya sean [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Estructura de árbol de Automatización de la interfaz de usuario necesaria  
 En la tabla siguiente se describe la vista de control y la vista de contenido del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que pertenece a los controles de hipervínculo y se describe lo que puede incluirse en cada vista. Para más información sobre el árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vea [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
|Vista de control|Vista de contenido|  
|----------------------|------------------------|  
|Hipervínculo|Hipervínculo|  
  
<a name="Required_UI_Automation_Properties"></a>   
## Propiedades de Automatización de la interfaz de usuario necesarias  
 En la tabla siguiente se muestran las propiedades de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que tienen un valor o una definición que es especialmente relevante para el tipo de control Hyperlink. Para más información sobre las propiedades de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vea [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Propiedad [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valor|Notas|  
|-------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Vea las notas.|El valor de esta propiedad debe ser único en todos los controles de una aplicación.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Vea las notas.|El rectángulo exterior que contiene el control completo.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vea las notas.|Se admite si hay un rectángulo delimitador. Si no todos los puntos que se encuentran dentro del rectángulo delimitador son seleccionables, y realiza pruebas de aciertos especializadas, invalide y ofrezca un punto en el que hacer clic.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Vea las notas.|Si el control puede recibir el enfoque del teclado, debe admitir esta propiedad.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Vea las notas.|El nombre del control de hipervínculo es el texto que se muestra en la pantalla como subrayado.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Vea las notas.|El punto donde hacer clic del control de hipervínculo debe ser un punto que inicie el hipervínculo si hace clic con el puntero del mouse.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Vea las notas.|Si hay una etiqueta de texto estático, esta propiedad debe exponer una referencia a ese control.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Hipervínculo|Este valor es el mismo para todos los marcos de trabajo de [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"hipervínculo"|Cadena localizada que corresponde al tipo de control Hyperlink.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|El control de hipervínculo siempre se incluye en la vista de contenido del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|El control de hipervínculo siempre se incluye en la vista de control del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## Propiedades y patrones de control de Automatización de la interfaz de usuario necesarios  
 En la tabla siguiente se muestran los patrones de control de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que deben admitir todos los controles de hipervínculo. Para más información sobre los patrones de control, vea [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Patrón de control\/propiedad de patrón|Soporte técnico\/valor|Notas|  
|--------------------------------------------|----------------------------|-----------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Sí|Todos los controles de hipervínculo deben admitir el patrón Invoke.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|Depende|Los controles de hipervínculo deben admitir el patrón de control Value si el vínculo contiene información que es utilizable y significativa para el usuario.|  
|<xref:System.Windows.Automation.Provider.IValueProvider.Value>|Por ejemplo, "http:\/\/www...."|Una dirección URL para una dirección de Internet o Intranet es un ejemplo de un hipervínculo que contiene información significativa para el usuario. Sin embargo, un vínculo programático solo es significativo para una aplicación y no se recomienda para la propiedad Value.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Eventos de Automatización de la interfaz de usuario necesarios  
 En la tabla siguiente se muestran los eventos de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que deben admitir todos los controles de hipervínculo. Para más información sobre los eventos, vea [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Evento [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Compatibilidad|Notas|  
|----------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>|Requerido|Ninguna|  
|Evento cambiado por propiedad <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>.|Obligatorio|Ninguna|  
|Evento cambiado por propiedad <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>.|Obligatorio|Ninguna|  
|Evento cambiado por propiedad <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>.|Obligatorio|Ninguno|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Requerido|Ninguna|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Requerido|Ninguna|  
  
## Vea también  
 <xref:System.Windows.Automation.ControlType.Hyperlink>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)