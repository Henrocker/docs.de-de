---
title: 'Vorgehensweise: Paralleles Erstellen mehrerer Webanforderungen mit Async und Await (Visual Basic)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a894b99b-7cfd-4a38-adfb-20d24f986730
caps.latest.revision: "3"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: a9b96e8acf9f5453ac035769ea7b279c4fedadfb
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await-visual-basic"></a>Vorgehensweise: Paralleles Erstellen mehrerer Webanforderungen mit Async und Await (Visual Basic)
In einer asynchronen Methode werden Aufgaben gestartet, wenn sie erstellt werden. Die ["await"](../../../../visual-basic/language-reference/operators/await-operator.md) Operator angewendet wird, auf die Aufgabe an dem Punkt in der Methode, in denen die Verarbeitung nicht fortgesetzt, bis die Aufgabe abgeschlossen ist. Häufig wird eine Aufgabe erwartet, sobald sie erstellt wird, wie das folgende Beispiel zeigt.  
  
```vb  
Dim result = Await someWebAccessMethodAsync(url)  
```  
  
 Sie können das Erstellen der Aufgabe vom Erwarten der Aufgabe jedoch trennen, wenn das Programm weitere Arbeit durchführen muss, die nicht vom Abschluss der Aufgabe abhängig ist.  
  
```vb  
' The following line creates and starts the task.  
Dim myTask = someWebAccessMethodAsync(url)  
  
' While the task is running, you can do other work that does not depend  
' on the results of the task.  
' . . . . .  
  
' The application of Await suspends the rest of this method until the task is   
' complete.  
Dim result = Await myTask  
```  
  
 Zwischen dem Starten und dem Erwarten einer Aufgabe können Sie andere Aufgaben starten. Die weiteren Aufgaben werden implizit parallel ausgeführt, es werden jedoch keine weiteren Threads erstellt.  
  
 Das folgende Programm startet drei asynchrone Webdownloads und erwartet diese dann in der Reihenfolge, in der sie aufgerufen wurden. Beachten Sie, dass die Aufgaben beim Ausführen des Programms nicht immer in der Reihenfolge abgeschlossen werden, in der sie erstellt und erwartet werden. Sie beginnen mit der Ausführung, wenn sie erstellt werden, und eine oder mehrere Aufgaben werden u. U. abgeschlossen, bevor die Methode die await-Ausdrucke erreicht.  
  
> [!NOTE]
>  Zum Fertigstellen dieses Projekts muss Visual Studio 2012 oder höher sowie .NET Framework 4.5 oder höher auf dem Computer installiert sein.  
  
 Ein weiteres Beispiel, das mehrere Tasks gleichzeitig beginnt, finden Sie unter [wie: Erweitern der asynchronen Walkthrough mithilfe von "Task.WhenAll" (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md).  
  
 Sie können den Code für dieses Beispiel auf der Seite für [Codebeispiele für Entwickler](http://go.microsoft.com/fwlink/?LinkId=254906) herunterladen.  
  
### <a name="to-set-up-the-project"></a>So richten Sie das Projekt ein  
  
1.  Führen Sie die folgenden Schritte aus, um eine WPF-Anwendung einzurichten. Sie finden detaillierte Anweisungen für diese Schritte in [Exemplarische Vorgehensweise: Zugreifen auf das Web durch Verwenden von Async und Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md).  
  
    -   Erstellen Sie eine WPF-Anwendung, die ein Textfeld und eine Schaltfläche enthält. Benennen Sie die Schaltfläche mit `startButton` und das Textfeld mit `resultsTextBox`.  
  
    -   Fügen Sie einen Verweis für <xref:System.Net.Http> hinzu.  
  
    -   In der Datei "MainWindow.Xaml.vb" Hinzufügen einer `Imports` -Anweisung für `System.Net.Http`.  
  
### <a name="to-add-the-code"></a>So fügen Sie den Code hinzu  
  
1.  Doppelklicken Sie im Entwurfsfenster "MainWindow.xaml", auf die Schaltfläche zum Erstellen der `startButton_Click` -Ereignishandler in "MainWindow.Xaml.vb".  
  
2.  Kopieren Sie den folgenden Code, und fügen Sie ihn in den Text der `startButton_Click` in "MainWindow.Xaml.vb".  
  
    ```vb  
    resultsTextBox.Clear()  
    Await CreateMultipleTasksAsync()  
    resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    ```  
  
     Der Code ruft die asynchrone Methode `CreateMultipleTasksAsync` auf, die die Anwendung steuert.  
  
3.  Fügen Sie dem Projekt die folgenden Unterstützungsmethoden hinzu:  
  
    -   `ProcessURLAsync` verwendet eine <xref:System.Net.Http.HttpClient>-Methode, um die Inhalte einer Website als Bytearray herunterzuladen. Die Unterstützungsmethode `ProcessURLAsync` wird daraufhin angezeigt und gibt die Länge des Arrays zurück.  
  
    -   `DisplayResults` zeigt die Anzahl von Bytes im Bytearray für jede URL an. Diese Anzeige wird aufgerufen, wenn alle Aufgaben den Download abgeschlossen haben.  
  
     Kopieren Sie die folgenden Methoden, und fügen Sie sie nach der `startButton_Click` -Ereignishandler in "MainWindow.Xaml.vb".  
  
    ```vb  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
    ```  
  
4.  Definieren Sie schließlich die `CreateMultipleTasksAsync`-Methode, die die folgenden Schritte ausführt.  
  
    -   Die Methode deklariert ein `HttpClient`-Objekt, das Sie für den Zugriff auf die <xref:System.Net.Http.HttpClient.GetByteArrayAsync%2A>-Methode in `ProcessURLAsync` benötigen.  
  
    -   Die Methode erstellt und startet drei Aufgaben vom Typ <xref:System.Threading.Tasks.Task%601>, wobei `TResult` eine ganze Zahl ist. Beim Abschließen jeder Aufgabe zeigt `DisplayResults` die URL der Aufgabe sowie die Länge der heruntergeladenen Inhalte an. Da die Aufgaben asynchron ausgeführt werden, kann sich die Reihenfolge, in der die Ergebnisse angezeigt werden, von der Reihenfolge, in der sie deklariert wurden, unterscheiden.  
  
    -   Die Methode erwartet den Abschluss jeder Aufgabe. Jeder `Await`-Operator hält die Ausführung von `CreateMultipleTasksAsync` an, bis die erwartete Aufgabe abgeschlossen ist. Der Operator ruft außerdem den Rückgabewert des Aufrufs von `ProcessURLAsync` von jeder abgeschlossenen Aufgabe ab.  
  
    -   Wenn die Aufgaben abgeschlossen und die ganzzahligen Werte abgerufen wurden, werden die Längen der Websites von der Methode summiert, und das Ergebnis wird angezeigt.  
  
     Kopieren Sie die folgende Methode, und fügen Sie sie in Ihre Projektmappe ein.  
  
    ```vb  
    Private Async Function CreateMultipleTasksAsync() As Task  
  
        ' Declare an HttpClient object, and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Create and start the tasks. As each task finishes, DisplayResults   
        ' displays its length.  
        Dim download1 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com", client)  
        Dim download2 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)  
        Dim download3 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client)  
  
        ' Await each task.  
        Dim length1 As Integer = Await download1  
        Dim length2 As Integer = Await download2  
        Dim length3 As Integer = Await download3  
  
        Dim total As Integer = length1 + length2 + length3  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
    ```  
  
5.  Drücken Sie die Taste F5, um das Programm auszuführen, und klicken Sie dann auf die Schaltfläche **Starten** .  
  
     Führen Sie das Programm mehrmals aus, um sicherzustellen, dass die drei Aufgaben nicht immer in derselben Reihenfolge abgeschlossen werden und dass die Reihenfolge, in der sie abgeschlossen werden, nicht notwendigerweise der Reihenfolge entspricht, in der sie erstellt und erwartet werden.  
  
## <a name="example"></a>Beispiel  
 Der folgende Code umfasst das vollständige Beispiel.  
  
```vb  
' Add the following Imports statements, and add a reference for System.Net.Http.  
Imports System.Net.Http  
  
Class MainWindow  
  
    Async Sub startButton_Click(sender As Object, e As RoutedEventArgs) Handles startButton.Click  
        resultsTextBox.Clear()  
        Await CreateMultipleTasksAsync()  
        resultsTextBox.Text &= vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Private Async Function CreateMultipleTasksAsync() As Task  
  
        ' Declare an HttpClient object, and increase the buffer size. The  
        ' default buffer size is 65,536.  
        Dim client As HttpClient =  
            New HttpClient() With {.MaxResponseContentBufferSize = 1000000}  
  
        ' Create and start the tasks. As each task finishes, DisplayResults   
        ' displays its length.  
        Dim download1 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com", client)  
        Dim download2 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/hh156528(VS.110).aspx", client)  
        Dim download3 As Task(Of Integer) =  
            ProcessURLAsync("http://msdn.microsoft.com/library/67w7t67f.aspx", client)  
  
        ' Await each task.  
        Dim length1 As Integer = Await download1  
        Dim length2 As Integer = Await download2  
        Dim length3 As Integer = Await download3  
  
        Dim total As Integer = length1 + length2 + length3  
  
        ' Display the total count for all of the websites.  
        resultsTextBox.Text &= String.Format(vbCrLf & vbCrLf &  
                                             "Total bytes returned:  {0}" & vbCrLf, total)  
    End Function  
  
    Private Async Function ProcessURLAsync(url As String, client As HttpClient) As Task(Of Integer)  
  
        Dim byteArray = Await client.GetByteArrayAsync(url)  
        DisplayResults(url, byteArray)  
        Return byteArray.Length  
    End Function  
  
    Private Sub DisplayResults(url As String, content As Byte())  
  
        ' Display the length of each website. The string format   
        ' is designed to be used with a monospaced font, such as  
        ' Lucida Console or Global Monospace.  
        Dim bytes = content.Length  
        ' Strip off the "http://".  
        Dim displayURL = url.Replace("http://", "")  
        resultsTextBox.Text &= String.Format(vbCrLf & "{0,-58} {1,8}", displayURL, bytes)  
    End Sub  
End Class  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Walkthrough: Accessing the Web by Using Async and Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md) (Exemplarische Vorgehensweise: Zugreifen auf das Web mit Async und Await (Visual Basic))  
 [Asynchrone Programmierung mit „Async“ und „Await“ (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/index.md)  
 [How to: Extend the Async Walkthrough by Using Task.WhenAll (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md) (Gewusst wie: Erweitern der asynchronen exemplarischen Vorgehensweise mit Task.WhenAll (Visual Basic))
