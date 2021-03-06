---
title: -target (C#-Compileroptionen)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /target
helpviewer_keywords:
- target compiler options [C#]
- /target compiler options [C#]
- assemblies [C#], compiling
- -target compiler options [C#]
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
caps.latest.revision: "22"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 4666f0305fc2de35c1fa594ccef3dd3a64c0f67c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="target-c-compiler-options"></a>/target (C#-Compileroptionen)
Die Compileroption **/target** kann in einem von vier Formaten angegeben werden:  
  
 [/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md)  
 So erstellen Sie eine EXE-Datei für [!INCLUDE[win8_appname_long](~/includes/win8-appname-long-md.md)]-Anwendungen.  
  
 [/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md)  
 So erstellen Sie eine EXE-Datei.  
  
 [/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md)  
 So erstellen Sie eine Codebibliothek.  
  
 [/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)  
 So erstellen Sie ein Modul.  
  
 [/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)  
 So erstellen Sie ein Windows-Programm.  
  
 [/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)  
 So erstellen Sie eine WINMDOBJ-Zwischendatei.  
  
 Wenn Sie nicht **/target:module** angegeben haben, verursacht **/target**, dass ein .NET Framework-Assemblymanifest in einer Ausgabedatei platziert wird. Weitere Informationen finden Sie unter [Assemblys in der Common Language Runtime](../../../framework/app-domains/assemblies-in-the-common-language-runtime.md) und [Häufige Attribute](../../programming-guide/concepts/attributes/common-attributes.md).  
  
 Das Assemblymanifest wird in der ersten EXE-Ausgabedatei in der Kompilierung oder in der ersten DLL platziert, falls es keine EXE-Ausgabedatei gibt. In der folgenden Befehlszeile wird das Manifest z.B. in `1.exe` platziert:  
  
```console  
csc /out:1.exe t1.cs /out:2.netmodule t2.cs  
```  
  
 Der Compiler erstellt nur ein Assemblymanifest pro Kompilierung. Informationen über alle Dateien in einer Kompilierung werden im Assemblymanifest platziert. Alle Ausgabedateien, außer diejenigen die mit **/target:module** erstellt wurden, können ein Assemblymanifest enthalten. Wenn mehrere Ausgabedateien in der Befehlszeile erstellt werden, kann nur ein Assemblymanifest erstellt werden, und es muss in die erste Ausgabedatei gehen, die in der Befehlszeile angegeben wurde. Unabhängig davon, was die erste Ausgabedatei ist (**/target:exe**, **/target:winexe**, **/target:library** oder **/target:module**), müssen alle anderen Ausgabedateien, die in der selben Kompilierung erzeugt wurden, Module sein (**/target:module**).  
  
 Wenn Sie eine Assembly erstellen, können Sie angeben, dass der ganze oder ein Teil des Codes mit dem <xref:System.CLSCompliantAttribute>-Attribut CLS-kompatibel ist.  
  
```csharp  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 Informationen zum programmgesteuerten Festlegen dieser Compileroption finden Sie unter <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="see-also"></a>Siehe auch  
 [C#-Compileroptionen](../../../csharp/language-reference/compiler-options/index.md)  
 [Verwalten von Projekt- und Projektmappeneigenschaften](/visualstudio/ide/managing-project-and-solution-properties)  
 [/subsystemversion (C#-Compileroptionen)](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)
