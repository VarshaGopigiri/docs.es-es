---
title: "C&#243;mo: Crear un formulario MDI con controles ToolStripPanel | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "formularios MDI"
  - "formularios MDI, crear"
  - "MDI, crear formularios"
  - "formularios de interfaz de múltiples documentos"
  - "ToolStrip (control) [Windows Forms]"
  - "ToolStripPanel (control) [Windows Forms]"
ms.assetid: d198ef8e-f7c4-4b3f-a7f5-ce858cb90cec
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# C&#243;mo: Crear un formulario MDI con controles ToolStripPanel
Puede crear un formulario de interfaz de múltiples documentos \(MDI\) que tenga controles <xref:System.Windows.Forms.ToolStrip> que lo enmarquen por los cuatro lados.  
  
## Ejemplo  
 El ejemplo de código siguiente muestra cómo utilizar controles <xref:System.Windows.Forms.ToolStripPanel> acoplados para enmarcar una ventana MDI con cuatro controles <xref:System.Windows.Forms.ToolStrip>.  
  
 En el ejemplo, el método <xref:System.Windows.Forms.ToolStripPanel.Join%2A> asocia los controles <xref:System.Windows.Forms.ToolStrip> a los controles <xref:System.Windows.Forms.ToolStripPanel> correspondientes.  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#10)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#10)]  
  
## Compilar el código  
 Para este ejemplo se necesita:  
  
-   Referencias a los ensamblados System.Drawing y System.Windows.Forms.  
  
 Para obtener información acerca de cómo generar este ejemplo desde la línea de comandos para [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], consulte [Compilar desde la línea de comandos](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) o [Compilar la línea de comandos con csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).  También puede compilar este ejemplo en [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] pegando el código en un nuevo proyecto.  Consulte también [Cómo: Compilar y ejecutar un ejemplo de código completo de Windows Forms en Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## Vea también  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripPanel>   
 <xref:System.Windows.Forms.ToolStripPanel.Join%2A>   
 <xref:System.Windows.Forms.ToolStripItem>   
 <xref:System.Windows.Forms.ToolStripMenuItem>   
 [ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)