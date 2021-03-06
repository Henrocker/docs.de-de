---
title: "Gewusst wie: Ermitteln der gedrückten Modifizierertaste"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboard input
- shift keys
- events [Windows Forms], mouse
- Keys.ControlKey enumeration member
- keys [Windows Forms], control keys
- user input [Windows Forms], checking for keyboard
- keys [Windows Forms], determining last pressed
- keys [Windows Forms], shift keys
- keys [Windows Forms], modifier keys
- control keys
- keys [Windows Forms], alt keys
- alt keys
- Keys.Shift enumeration member
- events [Windows Forms], keyboard
- keyboards [Windows Forms], keyboard input
- Keys.Alt enumeration member
- modifier keys
ms.assetid: 1e184048-0ae3-4067-a200-d4ba31dbc2cb
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: d5f749d22c09d166e81ea08068f760f24960ec83
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-determine-which-modifier-key-was-pressed"></a>Gewusst wie: Ermitteln der gedrückten Modifizierertaste
Wenn Sie eine Anwendung, die Tastatureingaben des Benutzers annimmt erstellen, können Sie auch für Zusatztasten z. B. die Tasten UMSCHALT, ALT und STRG überwachen möchten. Wenn eine Taste in Kombination mit anderen Schlüsseln oder Mausklicks gedrückt wird, kann Ihre Anwendung entsprechend reagieren. Z. B. wenn die Buchstaben S gedrückt wird, einfach dadurch möglicherweise eines "s" auf dem Bildschirm angezeigt werden, aber wenn Sie die Tasten STRG + S gedrückt werden, kann das aktuelle Dokument gespeichert werden. Wenn Sie behandeln die <xref:System.Windows.Forms.Control.KeyDown> -Ereignis der <xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> Eigenschaft von der <xref:System.Windows.Forms.KeyEventArgs> empfangen vom Ereignis Handler gibt an, welche Modifizierertasten. Alternativ können Sie die <xref:System.Windows.Forms.KeyEventArgs.KeyData%2A> Eigenschaft <xref:System.Windows.Forms.KeyEventArgs> gibt das Zeichen an, die auch alle mit einem bitweisen OR kombinierten Zusatztasten gedrückt wurde. Jedoch, wenn Sie behandeln die <xref:System.Windows.Forms.Control.KeyPress> Ereignis oder ein Mausereignis der Ereignishandler empfängt diese Informationen nicht. In diesem Fall müssen Sie verwenden die <xref:System.Windows.Forms.Control.ModifierKeys%2A> Eigenschaft von der <xref:System.Windows.Forms.Control> Klasse. In beiden Fällen müssen Sie eine bitweise AND-Operation der entsprechenden ausführen <xref:System.Windows.Forms.Keys> Wert und der zu überprüfende Wert. Die <xref:System.Windows.Forms.Keys> Enumeration bietet Variationen des jeweiligen Schlüssels Modifizierer, daher ist es wichtig, dass Sie den bitweisen ausführen und mit dem richtigen Wert. Beispielsweise wird durch die UMSCHALTTASTE gedrückt dargestellt <xref:System.Windows.Forms.Keys.Shift>, <xref:System.Windows.Forms.Keys.ShiftKey>, <xref:System.Windows.Forms.Keys.RShiftKey> und <xref:System.Windows.Forms.Keys.LShiftKey> den richtigen Wert UMSCHALT zu testen, wie eine Modifizierertaste ist <xref:System.Windows.Forms.Keys.Shift>. Auf ähnliche Weise, STRG und ALT als Modifizierer Sie testen, die zu verwendende der <xref:System.Windows.Forms.Keys.Control> und <xref:System.Windows.Forms.Keys.Alt> bzw. die Werte.  
  
> [!NOTE]
>  Visual Basic-Programmierer können auch Zugriff auf wichtige Informationen über die <xref:Microsoft.VisualBasic.Devices.Computer.Keyboard%2A> Eigenschaft  
  
### <a name="to-determine-which-modifier-key-was-pressed"></a>Zum Ermitteln der gedrückten Modifizierertaste wurde  
  
-   Verwenden Sie den bitweisen `AND` -Operator mit dem <xref:System.Windows.Forms.Control.ModifierKeys%2A> Eigenschaft und den Wert der <xref:System.Windows.Forms.Keys> Enumeration, um zu bestimmen, ob eine bestimmte Taste gedrückt wird. Im folgenden Codebeispiel wird veranschaulicht, um festzustellen, ob die UMSCHALTTASTE, innerhalb gedrückt wird einer <xref:System.Windows.Forms.Control.KeyPress> -Ereignishandler.  
  
     [!code-cpp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/VB/form1.vb#5)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.Keys>  
 <xref:System.Windows.Forms.Control.ModifierKeys%2A>  
 [Tastatureingaben in einer Windows Forms-Anwendung](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)  
 [Vorgehensweise: Bestimmen Sie, ob die FESTSTELLTASTE aktiviert ist, in Visual Basic](http://msdn.microsoft.com/library/91e60f5c-dd61-4222-ba5f-39af803afd8c)
