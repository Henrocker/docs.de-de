---
title: 'Vorgehensweise: Abfragen von ArrayList mit LINQ (C#)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-csharp
ms.topic: article
ms.assetid: 2bfb471c-6e9a-4e60-bd83-4a1778abde11
caps.latest.revision: "3"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: fe1426bb77f4e958abda83814632e61ee9ce415c
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-query-an-arraylist-with-linq-c"></a>Vorgehensweise: Abfragen von ArrayList mit LINQ (C#)
Bei Verwendung von LINQ zum Abfragen nicht generischer <xref:System.Collections.IEnumerable>-Auflistungen wie z.B. <xref:System.Collections.ArrayList> müssen Sie den Typ der Bereichsvariablen entsprechend dem spezifischen Typ der Objekte in der Auflistung explizit deklarieren. Wenn Sie zum Beispiel eine <xref:System.Collections.ArrayList> mit `Student`-Objekten haben, sollte die [from-Klausel](../../../../csharp/language-reference/keywords/from-clause.md) wie folgt aussehen:  
  
```  
var query = from Student s in arrList  
...  
```  
  
 Indem Sie den Typ der Bereichsvariablen angeben, wandeln Sie jedes Element in der <xref:System.Collections.ArrayList> in ein `Student` um.  
  
 Die Verwendung einer explizit typisierten Bereichsvariablen in einem Abfrageausdruck entspricht dem Aufrufen der <xref:System.Linq.Enumerable.Cast%2A>-Methode. <xref:System.Linq.Enumerable.Cast%2A> löst eine Ausnahme aus, wenn bei der Umwandlung ein Fehler auftritt. <xref:System.Linq.Enumerable.Cast%2A> und <xref:System.Linq.Enumerable.OfType%2A> sind zwei Standardabfrageoperator-Methoden, die mit nicht generischen <xref:System.Collections.IEnumerable>-Typen arbeiten. Weitere Informationen finden Sie unter [Typbeziehungen in LINQ-Abfragevorgängen](../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird eine einfache Abfrage von <xref:System.Collections.ArrayList> veranschaulicht. Beachten Sie, dass in diesem Beispiel Objektinitialisierer verwendet werden, wenn der Code die <xref:System.Collections.ArrayList.Add%2A>-Methode aufruft, aber dies ist keine Voraussetzung.  
  
```csharp  
using System;  
using System.Collections;  
using System.Linq;  
  
namespace NonGenericLINQ  
{  
    public class Student  
    {  
        public string FirstName { get; set; }  
        public string LastName { get; set; }  
        public int[] Scores { get; set; }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ArrayList arrList = new ArrayList();  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Svetlana", LastName = "Omelchenko", Scores = new int[] { 98, 92, 81, 60 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Claire", LastName = "O’Donnell", Scores = new int[] { 75, 84, 91, 39 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Sven", LastName = "Mortensen", Scores = new int[] { 88, 94, 65, 91 }  
                    });  
            arrList.Add(  
                new Student  
                    {  
                        FirstName = "Cesar", LastName = "Garcia", Scores = new int[] { 97, 89, 85, 82 }  
                    });  
  
            var query = from Student student in arrList  
                        where student.Scores[0] > 95  
                        select student;  
  
            foreach (Student s in query)  
                Console.WriteLine(s.LastName + ": " + s.Scores[0]);  
  
            // Keep the console window open in debug mode.  
            Console.WriteLine("Press any key to exit.");  
            Console.ReadKey();  
        }  
    }  
}  
/* Output:   
    Omelchenko: 98  
    Garcia: 97  
*/  
```  
  
## <a name="see-also"></a>Siehe auch  
 [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)
