---
title: 'Gewusst wie: Sortieren von Abfrageergebnissen unter Verwendung von LINQ (Visual Basic)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- sorting query results, multiple columns
- sorting data [Visual Basic]
- sorting data [LINQ in Visual Basic]
- sorting query results [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], sorting results
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: 07a4584d-9fd8-4a1d-b7d9-ccf2efa5c84e
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 5e034548a61b91eededd8dc21445beb7ac68007e
ms.sourcegitcommit: 34ec7753acf76f90a0fa845235ef06663dc9e36e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="how-to-sort-query-results-by-using-linq-visual-basic"></a>Gewusst wie: Sortieren von Abfrageergebnissen unter Verwendung von LINQ (Visual Basic)
Language-Integrated Query (LINQ) erleichtert die Datenbankinformationen zugreifen und Ausführen von Abfragen.  
  
 Im folgende Beispiel wird gezeigt, wie eine neue Anwendung erstellen, führt Abfragen in einer SQL Server-Datenbank, und sortiert die Ergebnisse nach mehreren Feldern mithilfe, der `Order By` Klausel. Die Sortierreihenfolge für jedes Feld kann aufsteigend oder absteigend werden. Weitere Informationen finden Sie unter [Order By-Klausel](../../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
 In den Beispielen in diesem Thema verwenden die Beispieldatenbank Northwind. Wenn Sie die Beispieldatenbank Northwind nicht auf Ihrem Computer verfügen, können Sie laden Sie es der [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088) Website. Anweisungen hierzu finden Sie unter [Herunterladen von Beispieldatenbanken](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>So erstellen eine Verbindung mit einer Datenbank  
  
1.  Öffnen Sie in Visual Studio **Server-Explorer**/**Datenbank-Explorer** durch Klicken auf **Server-Explorer**/**Datenbank Explorer** auf die **Ansicht** Menü.  
  
2.  Mit der rechten Maustaste **Datenverbindungen** in **Server-Explorer**/**Datenbank-Explorer** , und klicken Sie dann auf **Verbindung hinzufügen**.  
  
3.  Geben Sie eine gültige Verbindung mit der Beispieldatenbank Northwind.  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>Ein Projekt hinzufügen, die eine LINQ to SQL-Datei enthält.  
  
1.  Zeigen Sie in Visual Studio im Menü **Datei** auf **Neu**, und klicken Sie auf **Projekt**. Wählen Sie Visual Basic **Windows Forms-Anwendung** als Projekttyp.  
  
2.  Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**. Wählen Sie die **LINQ to SQL-Klassen** Elementvorlage.  
  
3.  Nennen Sie die Datei `northwind.dbml`. Klicken Sie auf **Hinzufügen**. Der Object Relational Designer (O/R-Designer) wird für die Datei northwind.dbml geöffnet.  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>Hinzufügen von Tabellen zu Abfragen in den O/R-Designer  
  
1.  In **Server-Explorer**/**Datenbank-Explorer**, erweitern Sie die Verbindung mit der Datenbank Northwind. Erweitern Sie die **Tabellen** Ordner.  
  
     Wenn Sie im O/R-Designer geschlossen haben, können Sie es durch Doppelklicken auf die Datei northwind.dbml, die Sie zuvor hinzugefügt haben erneut öffnen.  
  
2.  Klicken Sie auf der Customers-Tabelle, und ziehen Sie es in den linken Bereich des Designers. Klicken Sie auf die Orders-Tabelle, und ziehen Sie es in den linken Bereich des Designers.  
  
     Der Designer erstellt neue `Customer` und `Order` Objekte für das Projekt. Beachten Sie, dass der Designer Beziehungen zwischen den Tabellen erkennt automatisch und untergeordneten Eigenschaften für verwandte Objekte erstellt. Z. B. IntelliSense wird angezeigt, die `Customer` Objekt verfügt über eine `Orders` -Eigenschaft für alle Aufträge im Zusammenhang mit diesen Kunden.  
  
3.  Speichern Sie die Änderungen zu und schließen Sie den Designer.  
  
4.  Speichern Sie das Projekt.  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>Hinzufügen von Code aus, um die Datenbank abzufragen und die Ergebnisse werden angezeigt.  
  
1.  Aus der **Toolbox**, ziehen Sie eine <xref:System.Windows.Forms.DataGridView> -Steuerelement auf die Standard-Windows Form für das Projekt, Form1.  
  
2.  Doppelklicken Sie auf Form1, um zum Hinzufügen von Code die `Load` -Ereignis des Formulars.  
  
3.  Wenn Sie Tabellen in den O/R-Designer hinzugefügt haben, wird der Designer hinzugefügt ein <xref:System.Data.Linq.DataContext> -Objekt, das Projekt. Dieses Objekt enthält den Code, den Sie benötigen Zugriff auf diese Tabellen und den Zugriff auf einzelne Objekte und Sammlungen für jede Tabelle. Die <xref:System.Data.Linq.DataContext> Objekt für das Projekt mit der Bezeichnung wird anhand des Namens der DBML-Datei. Für dieses Projekt die <xref:System.Data.Linq.DataContext> Objekt heißt `northwindDataContext`.  
  
     Erstellen eine Instanz von der <xref:System.Data.Linq.DataContext> in Ihren Code und die Abfrage die Tabellen, die vom O/R-Designer angegeben.  
  
     Fügen Sie folgenden Code, der `Load` Ereignis, um die Tabellen Abfragen, die als Eigenschaften des Datenkontexts verfügbar gemacht und die Ergebnisse sortieren. Die Abfrage sortiert die Ergebnisse durch die Anzahl der Bestellungen für Kunden, in absteigender Reihenfolge. Kunden, die die gleiche von Bestellungen Anzahl sind nach Firmennamen in aufsteigender Reihenfolge (Standard) sortiert.  
  
     [!code-vb[VbLINQToSQLHowTos#10](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-sort-query-results-by-using-linq_1.vb)]  
  
4.  Drücken Sie F5, um das Projekt auszuführen und die Ergebnisse anzuzeigen.  
  
## <a name="see-also"></a>Siehe auch  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)  
 [Abfragen](../../../../visual-basic/language-reference/queries/queries.md)  
 [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)  
 [DataContext-Methoden (O/R-Designer)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
