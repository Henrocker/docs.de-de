---
title: 'Lernprogramm: Erstellen eines Typanbieters (F#)'
description: Erfahren Sie, wie eigene f#-Typanbieter in f# 3.0 zu erstellen, indem mehrere einfache Typanbieter, um die grundlegenden Konzepte veranschaulicht untersuchen.
keywords: Visual F#, F#, funktionale Programmierung
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 82bec076-19d4-470c-979f-6c3a14b7c70a
ms.openlocfilehash: a1d6315c2546de12e85efdd06cf2520605cb6e91
ms.sourcegitcommit: a19548e5167cbe7e9e58df4ffd8c3b23f17d5c7a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/02/2017
---
# <a name="tutorial-creating-a-type-provider"></a><span data-ttu-id="78ccc-104">Lernprogramm: Erstellen eines Typanbieters</span><span class="sxs-lookup"><span data-stu-id="78ccc-104">Tutorial: Creating a Type Provider</span></span>

> [!NOTE]
<span data-ttu-id="78ccc-105">Dieses Handbuch wurde für f# 3.0 geschrieben und wird aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-105">This guide was written for F# 3.0 and will be updated.</span></span>

<span data-ttu-id="78ccc-106">Der Typanbietermechanismus in F# 3.0 ist ein wesentlicher Bestandteil der Unterstützung für die informationsreiche Programmierung.</span><span class="sxs-lookup"><span data-stu-id="78ccc-106">The type provider mechanism in F# 3.0 is a significant part of its support for information rich programming.</span></span> <span data-ttu-id="78ccc-107">In diesem Lernprogramm wird erläutert, wie Sie eigene Typanbieter erstellen können, indem Schritt für Schritt mehrere einfache Typanbieter entwickelt und an diesen die grundlegenden Konzepte veranschaulicht werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-107">This tutorial explains how to create your own type providers by walking you through the development of several simple type providers to illustrate the basic concepts.</span></span> <span data-ttu-id="78ccc-108">Weitere Informationen zu den typanbietermechanismus in F# erläutert werden, finden Sie unter [Typanbieter](index.md).</span><span class="sxs-lookup"><span data-stu-id="78ccc-108">For more information about the type provider mechanism in F#, see [Type Providers](index.md).</span></span>

<span data-ttu-id="78ccc-109">F# 3.0 enthält mehrere integrierte Typanbieter für Datendienste, die im Internet und in Unternehmen häufig zur Anwendung kommen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-109">F# 3.0 contains several built-in type providers for commonly used Internet and enterprise data services.</span></span> <span data-ttu-id="78ccc-110">Diese Typanbieter erlauben einen einfachen und für alle üblichen Aufgaben ausreichenden Zugriff auf relationale SQL-Datenbanken und auf netzwerkbasierte OData- und WSDL-Dienste.</span><span class="sxs-lookup"><span data-stu-id="78ccc-110">These type providers give simple and regular access to SQL relational databases and network-based OData and WSDL services.</span></span> <span data-ttu-id="78ccc-111">Diese Anbieter unterstützen außerdem die Verwendung von F# LINQ-Abfragen für diese Datenquellen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-111">These providers also support the use of F# LINQ queries against these data sources.</span></span>

<span data-ttu-id="78ccc-112">Bei Bedarf können Sie eigene benutzerdefinierte Typanbieter erstellen oder auf Typanbieter verweisen, die von anderen Entwicklern erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-112">Where necessary, you can create custom type providers, or you can reference type providers that others have created.</span></span> <span data-ttu-id="78ccc-113">Angenommen, in einer Organisation wird ein Datendienst verwendet, der eine große und wachsende Anzahl von benannten Datasets bereitstellt, die alle ein eigenes, stabiles Datenschema verwenden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-113">For example, your organization could have a data service that provides a large and growing number of named data sets, each with its own stable data schema.</span></span> <span data-ttu-id="78ccc-114">Für diesen Dienst können Sie einen Typanbieter erstellen, der die Schemas liest und dem Programmierer alle aktuellen Datasets mit starker Typisierung zur Verfügung stellt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-114">You can create a type provider that reads the schemas and presents the current data sets to the programmer in a strongly typed way.</span></span>


## <a name="before-you-start"></a><span data-ttu-id="78ccc-115">Vor der Installation</span><span class="sxs-lookup"><span data-stu-id="78ccc-115">Before You Start</span></span>
<span data-ttu-id="78ccc-116">Der Typanbietermechanismus ist hauptsächlich für das Einfügen von stabilen Räumen für Daten- und Dienstinformationen in die F#-Programmierung vorgesehen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-116">The type provider mechanism is primarily designed for injecting stable data and service information spaces into the F# programming experience.</span></span>

<span data-ttu-id="78ccc-117">Der Mechanismus ist nicht für das Einfügen von Informationsräumen gedacht, deren Schemas während der Programmausführung Änderungen unterliegen, die für die Programmlogik relevant sind.</span><span class="sxs-lookup"><span data-stu-id="78ccc-117">This mechanism isn’t designed for injecting information spaces whose schema changes during program execution in ways that are relevant to program logic.</span></span> <span data-ttu-id="78ccc-118">Auch die sprachübergreifende Metaprogrammierung gehört nicht zu den Entwurfszielen für diesen Mechanismus, obwohl solche Szenerien in einigen Fällen durchaus auftreten können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-118">Also, the mechanism isn't designed for intra-language meta-programming, even though that domain contains some valid uses.</span></span> <span data-ttu-id="78ccc-119">Sie sollten diesen Mechanismus nur verwenden, wenn dies erforderlich ist und sich durch die Entwicklung eines Typanbieters ein deutlicher Mehrwert für die Programmierung erreichen lässt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-119">You should use this mechanism only where necessary and where the development of a type provider yields very high value.</span></span>

<span data-ttu-id="78ccc-120">Schreiben Sie keinen Typanbieter in Situationen, in denen kein Schema verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-120">You should avoid writing a type provider where a schema isn't available.</span></span> <span data-ttu-id="78ccc-121">Entsprechend sollten Sie den Einsatz eines Typanbieters auch dann vermeiden, wenn eine gewöhnliche (oder sogar schon vorhandene) .NET-Bibliothek ausreichen würde.</span><span class="sxs-lookup"><span data-stu-id="78ccc-121">Likewise, you should avoid writing a type provider where an ordinary (or even an existing) .NET library would suffice.</span></span>

<span data-ttu-id="78ccc-122">Bevor Sie beginnen, stellen Sie sich die folgenden Fragen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-122">Before you start, you might ask the following questions:</span></span>


- <span data-ttu-id="78ccc-123">Steht ein Schema für die Informationsquelle zur Verfügung?</span><span class="sxs-lookup"><span data-stu-id="78ccc-123">Do you have a schema for your information source?</span></span> <span data-ttu-id="78ccc-124">Wenn dies der Fall ist, wie erfolgt die Zuordnung in das Typsystem von F# und .NET?</span><span class="sxs-lookup"><span data-stu-id="78ccc-124">If so, what’s the mapping into the F# and .NET type system?</span></span>

- <span data-ttu-id="78ccc-125">Kann eine vorhandene (dynamisch typisierte) API als Ausgangspunkt für die Implementierung verwendet werden?</span><span class="sxs-lookup"><span data-stu-id="78ccc-125">Can you use an existing (dynamically typed) API as a starting point for your implementation?</span></span>

- <span data-ttu-id="78ccc-126">Haben Sie und die Organisation genügend Verwendungsfälle definieren können, sodass der Aufwand für die Entwicklung eines Typanbieters gerechtfertigt ist?</span><span class="sxs-lookup"><span data-stu-id="78ccc-126">Will you and your organization have enough uses of the type provider to make writing it worthwhile?</span></span> <span data-ttu-id="78ccc-127">Würde eine normale .NET-Bibliothek den Anforderungen ebenso genügen?</span><span class="sxs-lookup"><span data-stu-id="78ccc-127">Would a normal .NET library meet your needs?</span></span>

- <span data-ttu-id="78ccc-128">Wie häufig und wie umfassend wird sich das Schema ändern?</span><span class="sxs-lookup"><span data-stu-id="78ccc-128">How much will your schema change?</span></span>

- <span data-ttu-id="78ccc-129">Ändert es sich während der Programmierungsphase?</span><span class="sxs-lookup"><span data-stu-id="78ccc-129">Will it change during coding?</span></span>

- <span data-ttu-id="78ccc-130">Ändert es sich während einzelner Programmierungssitzungen?</span><span class="sxs-lookup"><span data-stu-id="78ccc-130">Will it change between coding sessions?</span></span>

- <span data-ttu-id="78ccc-131">Ändert es sich während der Programmausführung?</span><span class="sxs-lookup"><span data-stu-id="78ccc-131">Will it change during program execution?</span></span>

<span data-ttu-id="78ccc-132">Typanbieter sind für Situationen geeignet, in denen das Schema zur Laufzeit und während der Lebensdauer des kompilierten Codes stabil ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-132">Type providers are best suited to situations where the schema is stable at runtime and during the lifetime of compiled code.</span></span>


## <a name="a-simple-type-provider"></a><span data-ttu-id="78ccc-133">Ein einfacher Typanbieter</span><span class="sxs-lookup"><span data-stu-id="78ccc-133">A Simple Type Provider</span></span>
<span data-ttu-id="78ccc-134">In diesem Beispiel wird Samples.HelloWorldTypeProvider in die `SampleProviders\Providers` Verzeichnis die [f# 3.0 Beispielpaket](http://fsharp3sample.codeplex.com) auf der Codeplex-Website.</span><span class="sxs-lookup"><span data-stu-id="78ccc-134">This sample is Samples.HelloWorldTypeProvider in the `SampleProviders\Providers` directory of the [F# 3.0 Sample Pack](http://fsharp3sample.codeplex.com) on the Codeplex website.</span></span> <span data-ttu-id="78ccc-135">Der Anbieter stellt einen "Typenraum" mit 100 gelöschten Typen zur Verfügung, wie der folgenden Code zeigt, in dem F#-Signatursyntax verwendet wird und Details für alle Typen außer `Type1` weggelassen wurden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-135">The provider makes available a "type space" that contains 100 erased types, as the following code shows by using F# signature syntax and omitting the details for all except `Type1`.</span></span> <span data-ttu-id="78ccc-136">Weitere Informationen zu gelöschten Typen finden Sie unter [Details über bereitgestellte gelöschte Typen](#details-about-erased-provided-types) weiter unten in diesem Thema.</span><span class="sxs-lookup"><span data-stu-id="78ccc-136">For more information about erased types, see [Details About Erased Provided Types](#details-about-erased-provided-types) later in this topic.</span></span>

```fsharp
namespace Samples.HelloWorldTypeProvider

type Type1 =
    /// This is a static property.
    static member StaticProperty : string

    /// This constructor takes no arguments.
    new : unit -> Type1

    /// This constructor takes one argument.
    new : data:string -> Type1

    /// This is an instance property.
    member InstanceProperty : int

    /// This is an instance method.
    member InstanceMethod : x:int -> char

    /// This is an instance property.
    nested type NestedType = 
        /// This is StaticProperty1 on NestedType.
        static member StaticProperty1 : string
        …
        /// This is StaticProperty100 on NestedType.
        static member StaticProperty100 : string

type Type2 =
…
…

type Type100 =
…
```

<span data-ttu-id="78ccc-137">Beachten Sie, dass der Satz der bereitgestellten Typen und Member statisch verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-137">Note that the set of types and members provided is statically known.</span></span> <span data-ttu-id="78ccc-138">In diesem Beispiel wird die Möglichkeit von Anbietern, Typen abhängig von einem Schema bereitzustellen, nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-138">This example doesn't leverage the ability of providers to provide types that depend on a schema.</span></span> <span data-ttu-id="78ccc-139">Die Implementierung des Typanbieters wird im folgenden Code erläutert. Die Details werden in den folgenden Abschnitten dieses Themas behandelt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-139">The implementation of the type provider is outlined in the following code, and the details are covered in later sections of this topic.</span></span>


>[!WARNING] 
<span data-ttu-id="78ccc-140">Es kann ggf. vorkommen, dass dieser Code und die Onlinebeispiele kleinere Unterschiede in der Namensgebung aufweisen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-140">There may be some small naming differences between this code and the online samples.</span></span>

```fsharp
namespace Samples.FSharp.HelloWorldTypeProvider

open System
open System.Reflection
open Samples.FSharp.ProvidedTypes
open Microsoft.FSharp.Core.CompilerServices
open Microsoft.FSharp.Quotations

// This type defines the type provider. When compiled to a DLL, it can be added
// as a reference to an F# command-line compilation, script, or project.
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this = 

  // Inheriting from this type provides implementations of ITypeProvider 
  // in terms of the provided types below.
  inherit TypeProviderForNamespaces()

  let namespaceName = "Samples.HelloWorldTypeProvider"
  let thisAssembly = Assembly.GetExecutingAssembly()

  // Make one provided type, called TypeN.
  let makeOneProvidedType (n:int) = 
  …
  // Now generate 100 types
  let types = [ for i in 1 .. 100 -> makeOneProvidedType i ] 

  // And add them to the namespace
  do this.AddNamespace(namespaceName, types)

  [<assembly:TypeProviderAssembly>] 
  do()
```

<span data-ttu-id="78ccc-141">Zur Verwendung dieses Anbieters öffnen Sie eine separate Instanz von Visual Studio 2012, erstellen Sie ein F#-Skript, und fügen Sie einen Verweis an den Anbieter aus dem Skript anschließend mit #r wie im folgenden Code dargestellt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-141">To use this provider, open a separate instance of Visual Studio 2012, create an F# script, and then add a reference to the provider from your script by using #r as the following code shows:</span></span>

```fsharp
#r @".\bin\Debug\Samples.HelloWorldTypeProvider.dll"

let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")

let obj2 = Samples.HelloWorldTypeProvider.Type1("some other data")

obj1.InstanceProperty
obj2.InstanceProperty

[ for index in 0 .. obj1.InstanceProperty-1 -> obj1.InstanceMethod(index) ]
[ for index in 0 .. obj2.InstanceProperty-1 -> obj2.InstanceMethod(index) ]

let data1 = Samples.HelloWorldTypeProvider.Type1.NestedType.StaticProperty35
```

<span data-ttu-id="78ccc-142">Suchen Sie dann nach den Typen im `Samples.HelloWorldTypeProvider`-Namespace, der vom Typanbieter generiert wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-142">Then look for the types under the `Samples.HelloWorldTypeProvider` namespace that the type provider generated.</span></span>

<span data-ttu-id="78ccc-143">Bevor Sie den Anbieter neu kompilieren, stellen Sie sicher, dass alle Instanzen von Visual Studio und F# Interactive, die die Anbieter-DLL verwenden, geschlossen wurden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-143">Before you recompile the provider, make sure that you have closed all instances of Visual Studio and F# Interactive that are using the provider DLL.</span></span> <span data-ttu-id="78ccc-144">Andernfalls tritt ein Buildfehler auf, da die Ausgabe-DLL gesperrt ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-144">Otherwise, a build error will occur because the output DLL will be locked.</span></span>

<span data-ttu-id="78ccc-145">Zum Debuggen dieses Anbieters mithilfe von print-Anweisungen erstellen Sie ein Skript, das ein Problem mit dem Anbieter erzeugt, und verwenden Sie dann den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="78ccc-145">To debug this provider by using print statements, make a script that exposes a problem with the provider, and then use the following code:</span></span>

```fsharp
fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

<span data-ttu-id="78ccc-146">Um diesen Anbieter mit Visual Studio zu debuggen, öffnen Sie die Visual Studio-Eingabeaufforderung mit Administratorrechten, und führen Sie folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="78ccc-146">To debug this provider by using Visual Studio, open the Visual Studio command prompt with administrative credentials, and run the following command:</span></span>

```fsharp
devenv.exe /debugexe fsc.exe -r:bin\Debug\HelloWorldTypeProvider.dll script.fsx
```

<span data-ttu-id="78ccc-147">Als Alternative öffnen Sie Visual Studio, öffnen Sie im Menü Debuggen, wählen Sie `Debug/Attach to process…`, und fügen Sie zu einem anderen `devenv` Prozess, in dem Sie das Skript bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="78ccc-147">As an alternative, open Visual Studio, open the Debug menu, choose `Debug/Attach to process…`, and attach to another `devenv` process where you’re editing your script.</span></span> <span data-ttu-id="78ccc-148">Mit dieser Methode können Sie leichter eine ganz bestimmte Logik im Typanbieter überprüfen, da Sie in der zweiten Instanz interaktiv Ausdrücke eingeben können (mit vollständiger IntelliSense-Unterstützung und anderen Funktionen).</span><span class="sxs-lookup"><span data-stu-id="78ccc-148">By using this method, you can more easily target particular logic in the type provider by interactively typing expressions into the second instance (with full IntelliSense and other features).</span></span>

<span data-ttu-id="78ccc-149">Sie können die Debugging-Option Nur eigenen Code deaktivieren, um Fehler in generiertem Code besser identifizieren zu können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-149">You can disable Just My Code debugging to better identify errors in generated code.</span></span> <span data-ttu-id="78ccc-150">Informationen zum Aktivieren oder Deaktivieren dieses Feature finden Sie unter [Navigieren im Code mit dem Debugger](https://msdn.microsoft.com/library/y740d9d3.aspx).</span><span class="sxs-lookup"><span data-stu-id="78ccc-150">For information about how to enable or disable this feature, see [Navigating through Code with the Debugger](https://msdn.microsoft.com/library/y740d9d3.aspx).</span></span> <span data-ttu-id="78ccc-151">Darüber hinaus können Sie auch nicht abgefangene Ausnahme abfangen, indem Sie öffnen Festlegen der `Debug` Menü, und drücken Sie dann die `Exceptions` oder indem Sie die Tasten Strg + Alt + E öffnen auswählen der `Exceptions` (Dialogfeld).</span><span class="sxs-lookup"><span data-stu-id="78ccc-151">Also, you can also set first-chance exception catching by opening the `Debug` menu and then choosing `Exceptions` or by choosing the Ctrl+Alt+E keys to open the `Exceptions` dialog box.</span></span> <span data-ttu-id="78ccc-152">In diesem Dialogfeld unter `Common Language Runtime Exceptions`, wählen die `Thrown` Kontrollkästchen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-152">In that dialog box, under `Common Language Runtime Exceptions`, select the `Thrown` check box.</span></span>


### <a name="implementation-of-the-type-provider"></a><span data-ttu-id="78ccc-153">Implementierung des Typanbieters</span><span class="sxs-lookup"><span data-stu-id="78ccc-153">Implementation of the Type Provider</span></span>
<span data-ttu-id="78ccc-154">In diesem Abschnitt werden die wichtigsten Schritte bei der Implementierung eines Typanbieters erläutert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-154">This section walks you through the principal sections of the type provider implementation.</span></span> <span data-ttu-id="78ccc-155">Zuerst definieren Sie den Typ für den benutzerdefinierten Typanbieter selbst:</span><span class="sxs-lookup"><span data-stu-id="78ccc-155">First, you define the type for the custom type provider itself:</span></span>

```fsharp
[<TypeProvider>]
type SampleTypeProvider(config: TypeProviderConfig) as this =
```

<span data-ttu-id="78ccc-156">Dieser Typ muss öffentlich sein, und Sie müssen ihn mit Markieren der [TypeProvider](https://msdn.microsoft.com/library/bdf7b036-7490-4ace-b79f-c5f1b1b37947) Attribut, damit der Compiler den Typanbieter erkennt, wenn ein separates F#-Projekt die Assembly verweist, die den Typ enthält.</span><span class="sxs-lookup"><span data-stu-id="78ccc-156">This type must be public, and you must mark it with the [TypeProvider](https://msdn.microsoft.com/library/bdf7b036-7490-4ace-b79f-c5f1b1b37947) attribute so that the compiler will recognize the type provider when a separate F# project references the assembly that contains the type.</span></span> <span data-ttu-id="78ccc-157">Die *Config* Parameter ist optional, und enthält, wenn vorhanden, kontextkonfigurationsinformationen für die typanbieterinstanz, die f#-Compiler erstellt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-157">The *config* parameter is optional, and, if present, contains contextual configuration information for the type provider instance that the F# compiler creates.</span></span>

<span data-ttu-id="78ccc-158">Als Nächstes implementieren Sie die [ITypeProvider](https://msdn.microsoft.com/library/2c2b0571-843d-4a7d-95d4-0a7510ed5e2f) Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="78ccc-158">Next, you implement the [ITypeProvider](https://msdn.microsoft.com/library/2c2b0571-843d-4a7d-95d4-0a7510ed5e2f) interface.</span></span> <span data-ttu-id="78ccc-159">In diesem Fall verwenden Sie den `TypeProviderForNamespaces`-Typ aus der `ProvidedTypes`-API als Basistyp.</span><span class="sxs-lookup"><span data-stu-id="78ccc-159">In this case, you use the `TypeProviderForNamespaces` type from the `ProvidedTypes` API as a base type.</span></span> <span data-ttu-id="78ccc-160">Dieser Hilfstyp kann eine endliche Auflistung vorzeitig bereitgestellter Namespaces bereitstellen, von denen jeder direkt eine begrenzte Zahl fester, vorzeitig bereitgestellter Typen enthält.</span><span class="sxs-lookup"><span data-stu-id="78ccc-160">This helper type can provide a finite collection of eagerly provided namespaces, each of which directly contains a finite number of fixed, eagerly provided types.</span></span> <span data-ttu-id="78ccc-161">In diesem Kontext, den Anbieter *vorzeitig* Typen generiert, auch wenn sie benötigt oder verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-161">In this context, the provider *eagerly* generates types even if they aren't needed or used.</span></span>

```fsharp
inherit TypeProviderForNamespaces()
```

<span data-ttu-id="78ccc-162">Als Nächstes definieren Sie lokale private Werte, um den Namespace für die bereitgestellten Typen anzugeben, und suchen die eigentliche Typanbieterassembly.</span><span class="sxs-lookup"><span data-stu-id="78ccc-162">Next, define local private values that specify the namespace for the provided types, and find the type provider assembly itself.</span></span> <span data-ttu-id="78ccc-163">Diese Assembly wird später als logisch übergeordneter Typ der bereitgestellten gelöschten Typen verwendet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-163">This assembly is used later as the logical parent type of the erased types that are provided.</span></span>

```fsharp
let namespaceName = "Samples.HelloWorldTypeProvider"
let thisAssembly = Assembly.GetExecutingAssembly()
```

<span data-ttu-id="78ccc-164">Als Nächstes erstellen Sie eine Funktion, um jeden der Typen Type1 bis Type100 bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-164">Next, create a function to provide each of the types Type1…Type100.</span></span> <span data-ttu-id="78ccc-165">Diese Funktion wird weiter unten in diesem Thema ausführlicher erläutert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-165">This function is explained in more detail later in this topic.</span></span>

```fsharp
let makeOneProvidedType (n:int) = …
```

<span data-ttu-id="78ccc-166">Anschließend generieren Sie die 100 bereitgestellten Typen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-166">Next, generate the 100 provided types:</span></span>

```fsharp
let types = [ for i in 1 .. 100 -> makeOneProvidedType i ]
```

<span data-ttu-id="78ccc-167">Als Nächstes fügen Sie die Typen als bereitgestellten Namespace hinzu:</span><span class="sxs-lookup"><span data-stu-id="78ccc-167">Next, add the types as a provided namespace:</span></span>

```fsharp
do this.AddNamespace(namespaceName, types)
```

<span data-ttu-id="78ccc-168">Zum Schluss fügen Sie ein Assemblyattribut hinzu, das angibt, dass Sie eine Typanbieter-DLL erstellen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-168">Finally, add an assembly attribute that indicates that you are creating a type provider DLL:</span></span>

```fsharp
[<assembly:TypeProviderAssembly>] 
do()
```

### <a name="providing-one-type-and-its-members"></a><span data-ttu-id="78ccc-169">Bereitstellen eines einzelnen Typs und seiner Member</span><span class="sxs-lookup"><span data-stu-id="78ccc-169">Providing One Type And Its Members</span></span>
<span data-ttu-id="78ccc-170">Die `makeOneProvidedType`-Funktion übernimmt die eigentliche Verarbeitung bei der Bereitstellung eines Typs.</span><span class="sxs-lookup"><span data-stu-id="78ccc-170">The `makeOneProvidedType` function does the real work of providing one of the types.</span></span>

```fsharp
let makeOneProvidedType (n:int) = 
…
```

<span data-ttu-id="78ccc-171">In diesem Schritt wird die Implementierung dieser Funktion beschrieben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-171">This step explains the implementation of this function.</span></span> <span data-ttu-id="78ccc-172">Erstellen Sie zunächst den bereitgestellten Typ (beispielsweise Type1, wenn n=1, oder Type57, wenn n=57).</span><span class="sxs-lookup"><span data-stu-id="78ccc-172">First, create the provided type (for example, Type1, when n = 1, or Type57, when n = 57).</span></span>

```fsharp
// This is the provided type. It is an erased provided type and, in compiled code, 
// will appear as type 'obj'.
let t = ProvidedTypeDefinition(thisAssembly,namespaceName,
"Type" + string n,
baseType = Some typeof<obj>)
```

<span data-ttu-id="78ccc-173">Beachten Sie die folgenden Punkte:</span><span class="sxs-lookup"><span data-stu-id="78ccc-173">You should note the following points:</span></span>


- <span data-ttu-id="78ccc-174">Dieser bereitgestellte Typ wird gelöscht.</span><span class="sxs-lookup"><span data-stu-id="78ccc-174">This provided type is erased.</span></span>  <span data-ttu-id="78ccc-175">Da Sie angeben, dass der Basistyp `obj`, Instanzen erscheint als Werte des Typs [Obj](https://msdn.microsoft.com/library/dcf2430f-702b-40e5-a0a1-97518bf137f7) im kompilierten Code.</span><span class="sxs-lookup"><span data-stu-id="78ccc-175">Because you indicate that the base type is `obj`, instances will appear as values of type [obj](https://msdn.microsoft.com/library/dcf2430f-702b-40e5-a0a1-97518bf137f7) in compiled code.</span></span>
<br />

- <span data-ttu-id="78ccc-176">Wenn Sie einen nicht geschachtelten Typ angeben, müssen Sie die Assembly und den Namespace angeben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-176">When you specify a non-nested type, you must specify the assembly and namespace.</span></span> <span data-ttu-id="78ccc-177">Bei gelöschten Typen sollte die Assembly die Typanbieterassembly selbst sein.</span><span class="sxs-lookup"><span data-stu-id="78ccc-177">For erased types, the assembly should be the type provider assembly itself.</span></span>
<br />

<span data-ttu-id="78ccc-178">Als Nächstes fügen Sie dem Typ eine XML-Dokumentation hinzu.</span><span class="sxs-lookup"><span data-stu-id="78ccc-178">Next, add XML documentation to the type.</span></span> <span data-ttu-id="78ccc-179">Diese Dokumentation wird verzögert, d. h., sie wird erst bei Bedarf berechnet, wenn der Hostcompiler sie benötigt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-179">This documentation is delayed, that is, computed on-demand if the host compiler needs it.</span></span>

```fsharp
t.AddXmlDocDelayed (fun () -> sprintf "This provided type %s" ("Type" + string n))
```

<span data-ttu-id="78ccc-180">Als Nächstes fügen Sie dem Typ eine statische bereitgestellte Eigenschaft hinzu:</span><span class="sxs-lookup"><span data-stu-id="78ccc-180">Next you add a provided static property to the type:</span></span>

```fsharp
let staticProp = ProvidedProperty(propertyName = "StaticProperty", 
propertyType = typeof<string>, 
IsStatic=true,
GetterCode= (fun args -> <@@ "Hello!" @@>))
```

<span data-ttu-id="78ccc-181">Beim Abrufen dieser Eigenschaft wird immer die Zeichenfolge "Hello!" zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-181">Getting this property will always evaluate to the string "Hello!".</span></span> <span data-ttu-id="78ccc-182">Der `GetterCode` für die Eigenschaft verwendet ein F#-Zitat, das den Code darstellt, den der Hostcompiler zum Abrufen der Eigenschaft generiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-182">The `GetterCode` for the property uses an F# quotation, which represents the code that the host compiler generates for getting the property.</span></span> <span data-ttu-id="78ccc-183">Weitere Informationen zu Zitaten finden Sie unter [Zitieren von Code (f#)](https://msdn.microsoft.com/library/6f055397-a1f0-4f9a-927c-f0d7c6951155).</span><span class="sxs-lookup"><span data-stu-id="78ccc-183">For more information about quotations, see [Code Quotations (F#)](https://msdn.microsoft.com/library/6f055397-a1f0-4f9a-927c-f0d7c6951155).</span></span>

<span data-ttu-id="78ccc-184">Fügen Sie der Eigenschaft eine XML-Dokumentation hinzu.</span><span class="sxs-lookup"><span data-stu-id="78ccc-184">Add XML documentation to the property.</span></span>

```fsharp
staticProp.AddXmlDocDelayed(fun () -> "This is a static property")
```

<span data-ttu-id="78ccc-185">Fügen Sie jetzt die bereitgestellte Eigenschaft an den bereitgestellten Typ an.</span><span class="sxs-lookup"><span data-stu-id="78ccc-185">Now attach the provided property to the provided type.</span></span> <span data-ttu-id="78ccc-186">Sie müssen einen bereitgestellten Member an genau einen Typ anfügen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-186">You must attach a provided member to one and only one type.</span></span> <span data-ttu-id="78ccc-187">Andernfalls kann auf den Member nicht zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-187">Otherwise, the member will never be accessible.</span></span>

```fsharp
t.AddMember staticProp
```

<span data-ttu-id="78ccc-188">Erstellen Sie jetzt einen bereitgestellten Konstruktor ohne Parameter.</span><span class="sxs-lookup"><span data-stu-id="78ccc-188">Now create a provided constructor that takes no parameters.</span></span>

```fsharp
let ctor = ProvidedConstructor(parameters = [ ], 
InvokeCode= (fun args -> <@@ "The object data" :> obj @@>))
```

<span data-ttu-id="78ccc-189">Der `InvokeCode` für den Konstruktor gibt ein F#-Zitat zurück, das den Code darstellt, den der Hostcompiler generiert, wenn der Konstruktor aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-189">The `InvokeCode` for the constructor returns an F# quotation, which represents the code that the host compiler generates when the constructor is called.</span></span> <span data-ttu-id="78ccc-190">Sie können beispielsweise folgenden Konstruktor verwenden:</span><span class="sxs-lookup"><span data-stu-id="78ccc-190">For example, you can use the following constructor:</span></span>

```fsharp
new Type10()
```

<span data-ttu-id="78ccc-191">Eine Instanz des angegebenen Typs wird mit den ihm zugrunde liegenden Daten erstellt ("The object data").</span><span class="sxs-lookup"><span data-stu-id="78ccc-191">An instance of the provided type will be created with underlying data "The object data".</span></span> <span data-ttu-id="78ccc-192">Der zitierte Code enthält eine Konvertierung in [Obj](https://msdn.microsoft.com/library/dcf2430f-702b-40e5-a0a1-97518bf137f7) , da dieser Typ die Löschung eines ist dieses bereitgestellten Typs ist (wie bei den bereitgestellten Typ deklariert).</span><span class="sxs-lookup"><span data-stu-id="78ccc-192">The quoted code includes a conversion to [obj](https://msdn.microsoft.com/library/dcf2430f-702b-40e5-a0a1-97518bf137f7) because that type is the erasure of this provided type (as you specified when you declared the provided type).</span></span>

<span data-ttu-id="78ccc-193">Fügen Sie dem Konstruktor eine XML-Dokumentation hinzu, und fügen Sie dann den bereitgestellten Konstruktor dem bereitgestellten Typ hinzu:</span><span class="sxs-lookup"><span data-stu-id="78ccc-193">Add XML documentation to the constructor, and add the provided constructor to the provided type:</span></span>

```fsharp
ctor.AddXmlDocDelayed(fun () -> "This is a constructor")

t.AddMember ctor
```

<span data-ttu-id="78ccc-194">Erstellen Sie einen zweiten bereitgestellten Konstruktor mit einem Parameter:</span><span class="sxs-lookup"><span data-stu-id="78ccc-194">Create a second provided constructor that takes one parameter:</span></span>

```fsharp
let ctor2 = 
ProvidedConstructor(parameters = [ ProvidedParameter("data",typeof<string>) ], 
InvokeCode= (fun args -> <@@ (%%(args.[0]) : string) :> obj @@>))
```

<span data-ttu-id="78ccc-195">Der `InvokeCode` für den Konstruktor gibt erneut ein F#-Zitat zurück, das den Code darstellt, den der Hostcompiler bei einem Aufruf der Methode generiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-195">The `InvokeCode` for the constructor again returns an F# quotation, which represents the code that the host compiler generated for a call to the method.</span></span> <span data-ttu-id="78ccc-196">Sie können beispielsweise folgenden Konstruktor verwenden:</span><span class="sxs-lookup"><span data-stu-id="78ccc-196">For example, you can use the following constructor:</span></span>

```fsharp
new Type10("ten")
```

<span data-ttu-id="78ccc-197">Eine Instanz des bereitgestellten Typs wird mit den im zugrunde liegenden Daten erstellt ("ten").</span><span class="sxs-lookup"><span data-stu-id="78ccc-197">An instance of the provided type is created with underlying data "ten".</span></span> <span data-ttu-id="78ccc-198">Sie haben wahrscheinlich schon bemerkt, dass die `InvokeCode`-Funktion ein Zitat zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-198">You may have already noticed that the `InvokeCode` function returns a quotation.</span></span> <span data-ttu-id="78ccc-199">Die Eingabe für diese Funktion ist eine Liste von Ausdrücken: ein Ausdruck pro Konstruktorparameter.</span><span class="sxs-lookup"><span data-stu-id="78ccc-199">The input to this function is a list of expressions, one per constructor parameter.</span></span> <span data-ttu-id="78ccc-200">In diesem Fall ist in `args.[0]` ein Ausdruck verfügbar, der den einzelnen Parameterwert darstellt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-200">In this case, an expression that represents the single parameter value is available in `args.[0]`.</span></span> <span data-ttu-id="78ccc-201">Der Code für einen Aufruf des Konstruktors wandelt den Rückgabewert in den gelöschten Typ `obj` um.</span><span class="sxs-lookup"><span data-stu-id="78ccc-201">The code for a call to the constructor coerces the return value to the erased type `obj`.</span></span> <span data-ttu-id="78ccc-202">Nachdem Sie dem Typ den zweiten bereitgestellten Konstruktor hinzugefügt haben, erstellen Sie eine bereitgestellte Instanzeigenschaft:</span><span class="sxs-lookup"><span data-stu-id="78ccc-202">After you add the second provided constructor to the type, you create a provided instance property:</span></span>

```fsharp
let instanceProp = 
ProvidedProperty(propertyName = "InstanceProperty", 
propertyType = typeof<int>, 
GetterCode= (fun args -> 
<@@ ((%%(args.[0]) : obj) :?> string).Length @@>))
instanceProp.AddXmlDocDelayed(fun () -> "This is an instance property")
t.AddMember instanceProp
```

<span data-ttu-id="78ccc-203">Beim Abrufen dieser Eigenschaft wird die Länge der Zeichenfolge (des Darstellungsobjekts) zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-203">Getting this property will return the length of the string, which is the representation object.</span></span> <span data-ttu-id="78ccc-204">Die `GetterCode`-Eigenschaft gibt ein F#-Zitat zurück, das den Code angibt, der vom Hostcompiler zum Abrufen der Eigenschaft generiert wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-204">The `GetterCode` property returns an F# quotation that specifies the code that the host compiler generates to get the property.</span></span> <span data-ttu-id="78ccc-205">Wie `InvokeCode` gibt die `GetterCode`-Funktion ein Zitat zurück.</span><span class="sxs-lookup"><span data-stu-id="78ccc-205">Like `InvokeCode`, the `GetterCode` function returns a quotation.</span></span> <span data-ttu-id="78ccc-206">Der Hostcompiler ruft diese Funktion mit einer Argumentliste auf.</span><span class="sxs-lookup"><span data-stu-id="78ccc-206">The host compiler calls this function with a list of arguments.</span></span> <span data-ttu-id="78ccc-207">In diesem Fall enthalten die Argumente nur den einzelnen Ausdruck, der die Instanz darstellt, für die der Getter aufgerufen wird. Ein Zugriff ist über `args.[0]` möglich. Die Implementierung von `GetterCode` verarbeitet anschließend das Ergebniszitat des gelöschten Typs `obj` und verwendet eine Umwandlung, um dem Compilermechanismus für die Typüberprüfung zu entsprechen und das Objekt als Zeichenfolge darzustellen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-207">In this case, the arguments include just the single expression that represents the instance upon which the getter is being called, which you can access by using `args.[0]`.The implementation of `GetterCode` then splices into the result quotation at the erased type `obj`, and a cast is used to satisfy the compiler's mechanism for checking types that the object is a string.</span></span> <span data-ttu-id="78ccc-208">Der nächste Abschnitt von `makeOneProvidedType` stellt eine Instanzmethode mit einem Parameter bereit.</span><span class="sxs-lookup"><span data-stu-id="78ccc-208">The next part of `makeOneProvidedType` provides an instance method with one parameter.</span></span>

```fsharp
let instanceMeth = 
ProvidedMethod(methodName = "InstanceMethod", 
parameters = [ProvidedParameter("x",typeof<int>)], 
returnType = typeof<char>, 
InvokeCode = (fun args -> 
<@@ ((%%(args.[0]) : obj) :?> string).Chars(%%(args.[1]) : int) @@>))

instanceMeth.AddXmlDocDelayed(fun () -> "This is an instance method")
// Add the instance method to the type.
t.AddMember instanceMeth
```

<span data-ttu-id="78ccc-209">Zum Schluss wird ein geschachtelter Typ erstellt, der 100 geschachtelte Eigenschaften enthält.</span><span class="sxs-lookup"><span data-stu-id="78ccc-209">Finally, create a nested type that contains 100 nested properties.</span></span> <span data-ttu-id="78ccc-210">Die Erstellung dieses geschachtelten Typs und seiner Eigenschaften wird verzögert, d. h., er wird erst bei Bedarf berechnet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-210">The creation of this nested type and its properties is delayed, that is, computed on-demand.</span></span>

```fsharp
t.AddMembersDelayed(fun () -> 
let nestedType = ProvidedTypeDefinition("NestedType",
Some typeof<obj>

)

nestedType.AddMembersDelayed (fun () -> 
let staticPropsInNestedType = 
[ for i in 1 .. 100 do
let valueOfTheProperty = "I am string "  + string i

let p = ProvidedProperty(propertyName = "StaticProperty" + string i, 
propertyType = typeof<string>, 
IsStatic=true,
GetterCode= (fun args -> <@@ valueOfTheProperty @@>))

p.AddXmlDocDelayed(fun () -> 
sprintf "This is StaticProperty%d on NestedType" i)

yield p ]
staticPropsInNestedType)

[nestedType])

// The result of makeOneProvidedType is the type.
t
```

### <a name="details-about-erased-provided-types"></a><span data-ttu-id="78ccc-211">Details über gelöschte bereitgestellte Typen</span><span class="sxs-lookup"><span data-stu-id="78ccc-211">Details about Erased Provided Types</span></span>
<span data-ttu-id="78ccc-212">Im Beispiel in diesem Abschnitt bietet nur *gelöschte bereitgestellte Typen*, die in den folgenden Situationen besonders nützlich sind:</span><span class="sxs-lookup"><span data-stu-id="78ccc-212">The example in this section provides only *erased provided types*, which are particularly useful in the following situations:</span></span>


- <span data-ttu-id="78ccc-213">Wenn Sie einen Anbieter für einen Informationsraum schreiben, der nur Daten und Methoden enthält.</span><span class="sxs-lookup"><span data-stu-id="78ccc-213">When you are writing a provider for an information space that contains only data and methods.</span></span>
<br />

- <span data-ttu-id="78ccc-214">Wenn Sie einen Anbieter schreiben, bei dem zur Laufzeit für die Verwendung des Informationsraums keine exakte Typsemantik erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-214">When you are writing a provider where accurate runtime-type semantics aren't critical for practical use of the information space.</span></span>
<br />

- <span data-ttu-id="78ccc-215">Wenn Sie einen Anbieter für einen Informationsraum schreiben, der so groß ist und so viele Verbindungen verwendet, dass es technisch nicht möglich ist, echte .NET-Typen für den Informationsraum zu generieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-215">When you are writing a provider for an information space that is so large and interconnected that it isn’t technically feasible to generate real .NET types for the information space.</span></span>
<br />

<span data-ttu-id="78ccc-216">In diesem Beispiel wird jeder bereitgestellte Typ zu `obj` gelöscht, und alle Verwendungen des Typs erscheinen im kompilierten Code als `obj`.</span><span class="sxs-lookup"><span data-stu-id="78ccc-216">In this example, each provided type is erased to type `obj`, and all uses of the type will appear as type `obj` in compiled code.</span></span> <span data-ttu-id="78ccc-217">Tatsächlich sind die zugrunde liegenden Objekte in diesen Beispielen Zeichenfolgen, der Typ im kompilierten .NET-Code ist jedoch `System.Object`.</span><span class="sxs-lookup"><span data-stu-id="78ccc-217">In fact, the underlying objects in these examples are strings, but the type will appear as `System.Object` in .NET compiled code.</span></span> <span data-ttu-id="78ccc-218">Wie bei jeder Verwendung der Typlöschung können Sie explizites Boxing und Unboxing sowie Umwandlungen verwenden, um gelöschte Typen zu unterlaufen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-218">As with all uses of type erasure, you can use explicit boxing, unboxing, and casting to subvert erased types.</span></span> <span data-ttu-id="78ccc-219">In diesem Fall kann eine ungültige Umwandlungsausnahme auftreten, wenn das Objekt verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-219">In this case, a cast exception that isn’t valid may result when the object is used.</span></span> <span data-ttu-id="78ccc-220">Eine Anbieterlaufzeit kann ihren eigenen privaten Darstellungstyp definieren, um falsche Darstellungen zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-220">A provider runtime can define its own private representation type to help protect against false representations.</span></span> <span data-ttu-id="78ccc-221">In F# selbst können Sie keine gelöschten Typen definieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-221">You can’t define erased types in F# itself.</span></span> <span data-ttu-id="78ccc-222">Nur bereitgestellte Typen dürfen gelöscht werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-222">Only provided types may be erased.</span></span> <span data-ttu-id="78ccc-223">Sie müssen sich darüber im Klaren sein, welche Auswirkungen, sowohl praktisch als auch semantisch, die Verwendung von gelöschten Typen für Ihren Typanbieter hat, im Vergleich zu einem Anbieter, der selbst gelöschte Typen bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-223">You must understand the ramifications, both practical and semantic, of using either erased types for your type provider or a provider that provides erased types.</span></span> <span data-ttu-id="78ccc-224">Ein gelöschter Typ hat keinen tatsächlichen .NET-Typ.</span><span class="sxs-lookup"><span data-stu-id="78ccc-224">An erased type has no real .NET type.</span></span> <span data-ttu-id="78ccc-225">Daher können Sie keine genaue Reflektion über den Typ ausführen, und Sie unterlaufen möglicherweise gelöschte Typen, wenn Sie zur Laufzeit Umwandlungen oder andere Techniken verwenden, die zur Laufzeit eine exakte Typsemantik erfordern.</span><span class="sxs-lookup"><span data-stu-id="78ccc-225">Therefore, you cannot do accurate reflection over the type, and you might subvert erased types if you use runtime casts and other techniques that rely on exact runtime type semantics.</span></span> <span data-ttu-id="78ccc-226">Das Unterlaufen gelöschter Typen führt zur Laufzeit häufig zu Ausnahmen bei der Typumwandlung.</span><span class="sxs-lookup"><span data-stu-id="78ccc-226">Subversion of erased types frequently results in type cast exceptions at runtime.</span></span>


### <a name="choosing-representations-for-erased-provided-types"></a><span data-ttu-id="78ccc-227">Auswählen von Darstellungen für gelöschte bereitgestellte Typen</span><span class="sxs-lookup"><span data-stu-id="78ccc-227">Choosing Representations for Erased Provided Types</span></span>
<span data-ttu-id="78ccc-228">Für einige Verwendungen von gelöschten bereitgestellten Typen ist keine Darstellung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="78ccc-228">For some uses of erased provided types, no representation is required.</span></span> <span data-ttu-id="78ccc-229">Zum Beispiel kann der gelöschte bereitgestellte Typ ausschließlich statische Eigenschaften und Member enthalten, aber keine Konstruktoren, sodass keine Methoden oder Eigenschaften eine Instanz des Typs zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-229">For example, the erased provided type might contain only static properties and members and no constructors, and no methods or properties would return an instance of the type.</span></span> <span data-ttu-id="78ccc-230">Wenn Instanzen eines gelöschten bereitgestellten Typ verfügbar sind, berücksichtigen Sie die folgenden Fragen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-230">If you can reach instances of an erased provided type, you must consider the following questions:</span></span>


- <span data-ttu-id="78ccc-231">Was ist die Löschung eines bereitgestellten Typs?</span><span class="sxs-lookup"><span data-stu-id="78ccc-231">What is the erasure of a provided type?</span></span>
<br />
  - <span data-ttu-id="78ccc-232">Die Löschung eines bereitgestellten Typs bezeichnet die Darstellung des Typs im kompilierten .NET-Code.</span><span class="sxs-lookup"><span data-stu-id="78ccc-232">The erasure of a provided type is how the type appears in compiled .NET code.</span></span>
<br />

  - <span data-ttu-id="78ccc-233">Die Löschung eines bereitgestellten gelöschten Klassentyps ist immer der erste nicht gelöschte Basistyp in die Vererbungskette des Typs.</span><span class="sxs-lookup"><span data-stu-id="78ccc-233">The erasure of a provided erased class type is always the first non-erased base type in the inheritance chain of the type.</span></span>
<br />

  - <span data-ttu-id="78ccc-234">Die Löschung eines bereitgestellten gelöschten Schnittstellentyps ist immer `System.Object`.</span><span class="sxs-lookup"><span data-stu-id="78ccc-234">The erasure of a provided erased interface type is always `System.Object`.</span></span>
<br />

- <span data-ttu-id="78ccc-235">Was sind die Darstellungen eines bereitgestellten Typs?</span><span class="sxs-lookup"><span data-stu-id="78ccc-235">What are the representations of a provided type?</span></span>
<br />
  - <span data-ttu-id="78ccc-236">Der Satz möglicher Objekte für einen gelöschten bereitgestellten Typ wird als Darstellungen des Typs bezeichnet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-236">The set of possible objects for an erased provided type are called its representations.</span></span> <span data-ttu-id="78ccc-237">Im Beispiel in diesem Dokument sind die Darstellungen aller gelöschten bereitgestellten Typen `Type1..Type100` immer Zeichenfolgenobjekte.</span><span class="sxs-lookup"><span data-stu-id="78ccc-237">In the example in this document, the representations of all the erased provided types `Type1..Type100` are always string objects.</span></span>
<br />

<span data-ttu-id="78ccc-238">Alle Darstellungen eines angegebenen Typs müssen mit der Löschung des bereitgestellten Typs kompatibel sein.</span><span class="sxs-lookup"><span data-stu-id="78ccc-238">All representations of a provided type must be compatible with the erasure of the provided type.</span></span> <span data-ttu-id="78ccc-239">(Andernfalls gibt entweder der F#-Compiler einen Fehler aufgrund der Verwendung des Typanbieters aus, oder es wird nicht überprüfbarer und ungültiger .NET-Code generiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-239">(Otherwise, either the F# compiler will give an error for a use of the type provider, or unverifiable .NET code that isn't valid will be generated.</span></span> <span data-ttu-id="78ccc-240">Ein Typanbieter ist nicht gültig, wenn er Code zurückgibt, der eine ungültige Darstellung angibt.)</span><span class="sxs-lookup"><span data-stu-id="78ccc-240">A type provider isn’t valid if it returns code that gives a  representation that isn't valid.)</span></span>

<span data-ttu-id="78ccc-241">Sie können die Darstellung für bereitgestellte Objekte anhand eines der folgenden, häufig verwendeten Ansätze wählen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-241">You can choose a representation for provided objects by using either of the following approaches, both of which are very common:</span></span>


- <span data-ttu-id="78ccc-242">Wenn Sie einfach einen stark typisierten Wrapper für einen vorhandenen .NET-Typ bereitstellen, ist es meist sinnvoll, diesen .NET-Typ als Löschung für den Typ zu wählen, Instanzen dieses Typs als Darstellungen zu verwenden oder beide Wege zu wählen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-242">If you're simply providing a strongly typed wrapper over an existing .NET type, it often makes sense for your type to erase to that type, use instances of that type as representations, or both.</span></span> <span data-ttu-id="78ccc-243">Dieser Ansatz ist geeignet, wenn die meisten der vorhandenen Methoden für diesen Typ auch dann noch Sinn machen, wenn die stark typisierte Version verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-243">This approach is appropriate when most of the existing methods on that type still make sense when using the strongly typed version.</span></span>
<br />

- <span data-ttu-id="78ccc-244">Wenn Sie eine API erstellen möchten, die sich deutlich von allen vorhandenen .NET-APIs unterscheidet, ist es sinnvoll, Laufzeittypen zu erstellen, die als Typlöschungen und Darstellungen für die bereitgestellten Typen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-244">If you want to create an API that differs significantly from any existing .NET API, it makes sense to create runtime types that will be the type erasure and representations for the provided types.</span></span>
<br />

<span data-ttu-id="78ccc-245">Das Beispiel in diesem Dokument werden Zeichenfolgen als Darstellungen der bereitgestellten Objekte verwendet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-245">The example in this document uses strings as representations of provided objects.</span></span> <span data-ttu-id="78ccc-246">Häufig kann es sinnvoll sein, andere Objekte als Darstellungen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-246">Frequently, it may be appropriate to use other objects for representations.</span></span> <span data-ttu-id="78ccc-247">Beispielsweise können Sie ein Wörterbuch als Eigenschaftensammlung verwenden:</span><span class="sxs-lookup"><span data-stu-id="78ccc-247">For example, you may use a dictionary as a property bag:</span></span>

```fsharp
ProvidedConstructor(parameters = [], 
InvokeCode= (fun args -> <@@ (new Dictionary<string,obj>()) :> obj @@>))
```

<span data-ttu-id="78ccc-248">Alternativ können Sie einen Typ im Typanbieter definieren, der zur Laufzeit zusammen mit einem oder mehreren Laufzeitvorgängen verwendet wird, um die Darstellung zu bilden:</span><span class="sxs-lookup"><span data-stu-id="78ccc-248">As an alternative, you may define a type in your type provider that will be used at runtime to form the representation, along with one or more runtime operations:</span></span>

```fsharp
type DataObject() =
let data = Dictionary<string,obj>()
member x.RuntimeOperation() = data.Count
```

<span data-ttu-id="78ccc-249">Bereitgestellte Member können dann Instanzen dieses Objekttyps erstellen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-249">Provided members can then construct instances of this object type:</span></span>

```fsharp
ProvidedConstructor(parameters = [], 
InvokeCode= (fun args -> <@@ (new DataObject()) :> obj @@>))
```

<span data-ttu-id="78ccc-250">In diesem Fall können Sie (optional) diesen Typ als Typlöschung verwenden, indem Sie den Typ beim Erstellen der `baseType` als `ProvidedTypeDefinition` angeben:</span><span class="sxs-lookup"><span data-stu-id="78ccc-250">In this case, you may (optionally) use this type as the type erasure by specifying this type as the `baseType` when constructing the `ProvidedTypeDefinition`:</span></span>

```fsharp
ProvidedTypeDefinition(…, baseType = Some typeof<DataObject> )
…
ProvidedConstructor(…, InvokeCode = (fun args -> <@@ new DataObject() @@>), …)
```

`Key Lessons`

<span data-ttu-id="78ccc-251">Im vorherigen Abschnitt wurde das Erstellen eines einfachen gelöschten Typanbieters erläutert, der einen Typenbereich, Eigenschaften und Methoden bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-251">The previous section explained how to create a simple erasing type provider that provides a range of types, properties, and methods.</span></span> <span data-ttu-id="78ccc-252">Im Abschnitt wurde außerdem das Konzept der Typlöschung erläutert, und es wurden einige der Vor- und Nachteile beim Bereitstellen gelöschter Typen durch einen Typanbieter sowie mögliche Darstellungen für gelöschte Typen behandelt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-252">This section also explained the concept of type erasure, including some of the advantages and disadvantages of providing erased types from a type provider, and discussed representations of erased types.</span></span>


## <a name="a-type-provider-that-uses-static-parameters"></a><span data-ttu-id="78ccc-253">Ein Typanbieter, der statische Parameter verwendet</span><span class="sxs-lookup"><span data-stu-id="78ccc-253">A Type Provider That Uses Static Parameters</span></span>
<span data-ttu-id="78ccc-254">Die Möglichkeit, Typanbieter durch statische Daten zu parametrisieren, eröffnet viele interessante Szenarien, sogar in Fällen, in denen der Anbieter gar nicht auf lokale oder Remotedaten zugreifen muss.</span><span class="sxs-lookup"><span data-stu-id="78ccc-254">The ability to parameterize type providers by static data enables many interesting scenarios, even in cases when the provider doesn't need to access any local or remote data.</span></span> <span data-ttu-id="78ccc-255">In diesem Abschnitt lernen Sie einige der grundlegenden Techniken für den Entwurf eines solchen Anbieters kennen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-255">In this section, you’ll learn some basic techniques for putting together such a provider.</span></span>


### <a name="type-checked-regex-provider"></a><span data-ttu-id="78ccc-256">Typgeprüfter Regex-Anbieter</span><span class="sxs-lookup"><span data-stu-id="78ccc-256">Type Checked Regex Provider</span></span>
<span data-ttu-id="78ccc-257">Angenommen, Sie möchten einen Typanbieter für reguläre Ausdrücke implementieren, der die .NET-Bibliotheken von `System.Text.RegularExpressions.Regex` in einer Schnittstelle umschließt, die zur Laufzeit die folgenden Garantien bereitstellt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-257">Imagine that you want to implement a type provider for regular expressions that wraps the .NET `System.Text.RegularExpressions.Regex` libraries in an interface that provides the following compile-time guarantees:</span></span>


- <span data-ttu-id="78ccc-258">Überprüfen, ob ein regulärer Ausdruck gültig ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-258">Verifying whether a regular expression is valid.</span></span>
<br />

- <span data-ttu-id="78ccc-259">Bereitstellen benannter Eigenschaften für Übereinstimmungen, die auf vorhandenen Gruppennamen im regulären Ausdruck basieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-259">Providing named properties on matches that are based on any group names in the regular expression.</span></span>
<br />

<span data-ttu-id="78ccc-260">In diesem Abschnitt wird erläutert, wie Sie mit Typanbietern einen `RegExProviderType`-Typ erstellen, in dem über das reguläre Ausdrucksmuster Parameter erstellt werden, um die zuvor genannten Funktionen bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-260">This section shows you how to use type providers to create a `RegExProviderType` type that the regular expression pattern parameterizes to provide these benefits.</span></span> <span data-ttu-id="78ccc-261">Der Compiler meldet einen Fehler, wenn das angegebene Muster ungültig ist, und der Typanbieter kann die Gruppen aus dem Muster extrahieren und sie bei Übereinstimmungen als benannte Eigenschaften verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-261">The compiler will report an error if the supplied pattern isn't valid, and the type provider can extract the groups from the pattern so that you can access them by using named properties on matches.</span></span> <span data-ttu-id="78ccc-262">Wenn Sie einen Typanbieter entwerfen, sollten Sie berücksichtigen, in welcher Form die API den Endbenutzern zur Verfügung gestellt wird und wie der Entwurf in .NET-Code übersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-262">When you design a type provider, you should consider how its exposed API should look to end users and how this design will translate to .NET code.</span></span> <span data-ttu-id="78ccc-263">Im folgenden Beispiel wird gezeigt, wie eine solche API verwendet wird, um die Komponenten einer Ortskennzahl zu ermitteln:</span><span class="sxs-lookup"><span data-stu-id="78ccc-263">The following example shows how to use such an API to get the components of the area code:</span></span>

```fsharp
type T = RegexTyped< @"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)">
let reg = T()
let result = T.IsMatch("425-555-2345")
let r = reg.Match("425-555-2345").Group_AreaCode.Value //r equals "425"
```

<span data-ttu-id="78ccc-264">Im folgenden Beispiel wird gezeigt, wie der Typanbieter diese Aufrufe übersetzt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-264">The following example shows how the type provider translates these calls:</span></span>

```fsharp
let reg = new Regex(@"(?<AreaCode>^\d{3})-(?<PhoneNumber>\d{3}-\d{4}$)")
let result = reg.IsMatch("425-123-2345")
let r = reg.Match("425-123-2345").Groups.["AreaCode"].Value //r equals "425"
```

<span data-ttu-id="78ccc-265">Beachten Sie die folgenden Punkte:</span><span class="sxs-lookup"><span data-stu-id="78ccc-265">Note the following points:</span></span>


- <span data-ttu-id="78ccc-266">Der Regex-Standardtyp stellt den parametrisierten `RegexTyped`-Typ dar.</span><span class="sxs-lookup"><span data-stu-id="78ccc-266">The standard Regex type represents the parameterized `RegexTyped` type.</span></span>
<br />

- <span data-ttu-id="78ccc-267">Der `RegexTyped`-Konstruktor führt zu einem Aufruf des Regex-Konstruktors und übergibt als Muster das statische Argument.</span><span class="sxs-lookup"><span data-stu-id="78ccc-267">The `RegexTyped` constructor results in a call to the Regex constructor, passing in the static type argument for the pattern.</span></span>
<br />

- <span data-ttu-id="78ccc-268">Die Ergebnisse der `Match`-Methode werden durch den `System.Text.RegularExpressions.Match`-Standardtyp dargestellt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-268">The results of the `Match` method are represented by the standard `System.Text.RegularExpressions.Match` type.</span></span>
<br />

- <span data-ttu-id="78ccc-269">Für jede benannte Gruppe wird eine bereitgestellte Eigenschaft erzeugt, und bei einem Zugriff auf die Eigenschaft wird ein Indexer verwendet, um eine `Groups`-Auflistung der Übereinstimmungen abzurufen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-269">Each named group results in a provided property, and accessing the property results in a use of an indexer on a match’s `Groups` collection.</span></span>
<br />

<span data-ttu-id="78ccc-270">Der folgende Code enthält die Kernlogik für die Implementierung eines solchen Anbieters, wobei in diesem Beispiel allerdings das Hinzufügen der Member zum bereitgestellten Typ ausgelassen wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-270">The following code is the core of the logic to implement such a provider, and this example omits the addition of all members to the provided type.</span></span> <span data-ttu-id="78ccc-271">Weitere Informationen über die hinzugefügten Member finden Sie im entsprechenden Abschnitt weiter unten in diesem Thema.</span><span class="sxs-lookup"><span data-stu-id="78ccc-271">For information about each added member, see the appropriate section later in this topic.</span></span> <span data-ttu-id="78ccc-272">Den vollständigen Code, laden Sie das Beispiel aus der [f# 3.0 Beispielpaket](http://fsharp3sample.codeplex.com) auf der Codeplex-Website.</span><span class="sxs-lookup"><span data-stu-id="78ccc-272">For the full code, download the sample from the [F# 3.0 Sample Pack](http://fsharp3sample.codeplex.com) on the Codeplex website.</span></span>

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
inherit TypeProviderForNamespaces()

// Get the assembly and namespace used to house the provided types
let thisAssembly = Assembly.GetExecutingAssembly()
let rootNamespace = "Samples.FSharp.RegexTypeProvider"
let baseTy = typeof<obj>
let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

do regexTy.DefineStaticParameters(
parameters=staticParams, 
instantiationFunction=(fun typeName parameterValues ->

match parameterValues with 
| [| :? string as pattern|] -> 
// Create an instance of the regular expression. 
//
// This will fail with System.ArgumentException if the regular expression is not valid. 
// The exception will escape the type provider and be reported in client code.
let r = System.Text.RegularExpressions.Regex(pattern)            

// Declare the typed regex provided type.
// The type erasure of this type is 'obj', even though the representation will always be a Regex
// This, combined with hiding the object methods, makes the IntelliSense experience simpler.
let ty = ProvidedTypeDefinition(
thisAssembly, 
rootNamespace, 
typeName, 
baseType = Some baseTy)

...

ty
| _ -> failwith "unexpected parameter values")) 

do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

<span data-ttu-id="78ccc-273">Beachten Sie die folgenden Punkte:</span><span class="sxs-lookup"><span data-stu-id="78ccc-273">Note the following points:</span></span>


- <span data-ttu-id="78ccc-274">Der Typanbieter erwartet zwei statische Parameter: `pattern`, ein erforderlicher Parameter, und den optionalen Parameter `options` (für den ein Standardwert bereitgestellt wird).</span><span class="sxs-lookup"><span data-stu-id="78ccc-274">The type provider takes two static parameters: the `pattern`, which is mandatory, and the `options`, which are optional (because a default value is provided).</span></span>
<br />

- <span data-ttu-id="78ccc-275">Nachdem die statischen Argumente angegeben sind, erstellen Sie eine Instanz des regulären Ausdrucks.</span><span class="sxs-lookup"><span data-stu-id="78ccc-275">After the static arguments are supplied, you create an instance of the regular expression.</span></span> <span data-ttu-id="78ccc-276">Diese Instanz löst eine Ausnahme aus, wenn der Regex-Ausdruck fehlerhaft ist, und der Fehler wird den Benutzern gemeldet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-276">This instance will throw an exception if the Regex is malformed, and this error will be reported to users.</span></span>
<br />

- <span data-ttu-id="78ccc-277">Innerhalb des `DefineStaticParameters`-Rückrufs definieren Sie den Typ, der zurückgegeben wird, nachdem die Argumente angegeben wurden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-277">Within the `DefineStaticParameters` callback, you define the type that will be returned after the arguments are supplied.</span></span>
<br />

- <span data-ttu-id="78ccc-278">Diese Code legt `HideObjectMethods` fest, um die Methoden in der IntelliSense-Unterstützung zu unterdrücken.</span><span class="sxs-lookup"><span data-stu-id="78ccc-278">This code sets `HideObjectMethods` to true so that the IntelliSense experience will remain streamlined.</span></span> <span data-ttu-id="78ccc-279">Dieses Attribut führt dazu, dass die Member `Equals`, `GetHashCode`, `Finalize` und `GetType` nicht in den IntelliSense-Listen für ein bereitgestelltes Objekt angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-279">This attribute causes the `Equals`, `GetHashCode`, `Finalize`, and `GetType` members to be suppressed from IntelliSense lists for a provided object.</span></span>
<br />

- <span data-ttu-id="78ccc-280">Sie verwenden `obj` als Basistyp der Methode. Für die Laufzeitdarstellung dieses Typs wird jedoch ein `Regex`-Objekt verwendet, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-280">You use `obj` as the base type of the method, but you’ll use a `Regex` object as the runtime representation of this type, as the next example shows.</span></span>
<br />

- <span data-ttu-id="78ccc-281">Der Aufruf des `Regex`-Konstruktors löst eine `System.ArgumentException` aus, wenn ein regulärer Ausdruck ungültig ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-281">The call to the `Regex` constructor throws a `System.ArgumentException` when a regular expression isn’t valid.</span></span> <span data-ttu-id="78ccc-282">Der Compiler fängt diese Ausnahme ab und gibt im Visual Studio-Editor oder zur Kompilierzeit eine Fehlermeldung an den Benutzer aus.</span><span class="sxs-lookup"><span data-stu-id="78ccc-282">The compiler catches this exception and reports an error message to the user at compile time or in the Visual Studio editor.</span></span> <span data-ttu-id="78ccc-283">Diese Ausnahme ermöglicht es, reguläre Ausdrücke zu überprüfen, ohne die Anwendung ausführen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-283">This exception enables regular expressions to be validated without running an application.</span></span>
<br />

<span data-ttu-id="78ccc-284">Der oben definierte Typ ist bisher wenig nützlich, da er noch keine sinnvollen Methoden oder Eigenschaften enthält.</span><span class="sxs-lookup"><span data-stu-id="78ccc-284">The type defined above isn't useful yet because it doesn’t contain any meaningful methods or properties.</span></span> <span data-ttu-id="78ccc-285">Fügen Sie zuerst eine statische `IsMatch`-Methode hinzu:</span><span class="sxs-lookup"><span data-stu-id="78ccc-285">First, add a static `IsMatch` method:</span></span>

```fsharp
let isMatch = ProvidedMethod(
methodName = "IsMatch", 
parameters = [ProvidedParameter("input", typeof<string>)], 
returnType = typeof<bool>, 
IsStaticMethod = true,
InvokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>) 

isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string." 
ty.AddMember isMatch
```

<span data-ttu-id="78ccc-286">Der vorherige Code definiert eine `IsMatch`-Methode, die eine Zeichenfolge als Eingabe erwartet und `bool` zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-286">The previous code defines a method `IsMatch`, which takes a string as input and returns a `bool`.</span></span> <span data-ttu-id="78ccc-287">Der einzige schwierige Teil ist die Verwendung des `args`-Arguments innerhalb der `InvokeCode`-Definition.</span><span class="sxs-lookup"><span data-stu-id="78ccc-287">The only tricky part is the use of the `args` argument within the `InvokeCode` definition.</span></span> <span data-ttu-id="78ccc-288">In diesem Beispiel ist `args` eine Liste mit Zitaten, die die Argumente für diese Methode darstellen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-288">In this example, `args` is a list of quotations that represents the arguments to this method.</span></span> <span data-ttu-id="78ccc-289">Wenn die Methode eine Instanzmethode ist, stellt das erste Argument das `this`-Argument dar.</span><span class="sxs-lookup"><span data-stu-id="78ccc-289">If the method is an instance method, the first argument represents the `this` argument.</span></span> <span data-ttu-id="78ccc-290">Bei einer statischen Methode sind alle Argumente einfach nur die expliziten Argumente der Methode.</span><span class="sxs-lookup"><span data-stu-id="78ccc-290">However, for a static method, the arguments are all just the explicit arguments to the method.</span></span> <span data-ttu-id="78ccc-291">Beachten Sie, dass der Typ des zitierten Werts dem angegebenen Rückgabetyp entsprechen muss (in diesem Fall `bool`).</span><span class="sxs-lookup"><span data-stu-id="78ccc-291">Note that the type of the quoted value should match the specified return type (in this case, `bool`).</span></span> <span data-ttu-id="78ccc-292">Beachten Sie auch, dass dieser Code die `AddXmlDoc`-Methode verwendet, um sicherzustellen, dass die bereitgestellte Methode über eine sinnvolle Dokumentation verfügt, die Sie über IntelliSense zur Verfügung stellen können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-292">Also note that this code uses the `AddXmlDoc` method to make sure that the provided method also has useful documentation, which you can supply through IntelliSense.</span></span>

<span data-ttu-id="78ccc-293">Als Nächstes fügen Sie eine Instanz der Match-Methode hinzu.</span><span class="sxs-lookup"><span data-stu-id="78ccc-293">Next, add an instance Match method.</span></span> <span data-ttu-id="78ccc-294">Diese Methode muss jedoch einen Wert eines bereitgestellten `Match`-Typs zurückgeben, damit stark typisiert auf die Gruppen zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="78ccc-294">However, this method should return a value of a provided `Match` type so that the groups can be accessed in a strongly typed fashion.</span></span> <span data-ttu-id="78ccc-295">Daher deklarieren Sie zuerst den `Match`-Typ.</span><span class="sxs-lookup"><span data-stu-id="78ccc-295">Thus, you first declare the `Match` type.</span></span> <span data-ttu-id="78ccc-296">Da dieser Typ abhängig ist von dem Muster, das als statisches Argument übergeben wurde, muss dieser Typ innerhalb der parametrisierten Typdefinition geschachtelt werden:</span><span class="sxs-lookup"><span data-stu-id="78ccc-296">Because this type depends on the pattern that was supplied as a static argument, this type must be nested within the parameterized type definition:</span></span>

```fsharp
let matchTy = ProvidedTypeDefinition(
"MatchType", 
baseType = Some baseTy, 
HideObjectMethods = true)

ty.AddMember matchTy
```

<span data-ttu-id="78ccc-297">Anschließend fügen Sie dem Match-Typ für jede Gruppe eine Eigenschaft hinzu.</span><span class="sxs-lookup"><span data-stu-id="78ccc-297">You then add one property to the Match type for each group.</span></span> <span data-ttu-id="78ccc-298">Zur Laufzeit wird eine Übereinstimmung als `System.Text.RegularExpressions.Match`-Wert dargestellt, sodass das Zitat, das die Eigenschaft definiert, die indizierte `System.Text.RegularExpressions.Match.Groups`-Eigenschaft verwenden muss, um die entsprechende Gruppe abzurufen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-298">At runtime, a match is represented as a `System.Text.RegularExpressions.Match` value, so the quotation that defines the property must use the `System.Text.RegularExpressions.Match.Groups` indexed property to get the relevant group.</span></span>

```fsharp
for group in r.GetGroupNames() do
// Ignore the group named 0, which represents all input.
if group <> "0" then
let prop = ProvidedProperty(
propertyName = group, 
propertyType = typeof<Group>, 
GetterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
prop.AddXmlDoc(sprintf @"Gets the ""%s"" group from this match" group)
matchTy.AddMember prop
```

<span data-ttu-id="78ccc-299">Achten Sie auch hier darauf, dass der bereitgestellten Eigenschaft eine XML-Dokumentation hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-299">Again, note that you’re adding XML documentation to the provided property.</span></span> <span data-ttu-id="78ccc-300">Beachten Sie außerdem, dass eine Eigenschaft gelesen werden kann, wenn eine `GetterCode`-Funktion bereitgestellt wird, und dass Eigenschaft geschrieben werden kann, wenn eine `SetterCode`-Funktion bereitgestellt wird. Die resultierende Eigenschaft ist also schreibgeschützt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-300">Also note that a property can be read if a `GetterCode` function is provided, and the property can be written if a `SetterCode` function is provided, so the resulting property is read only.</span></span>

<span data-ttu-id="78ccc-301">Nun können Sie eine Instanzmethode erstellen, die einen Wert dieses `Match`-Typs zurückgibt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-301">Now you can create an instance method that returns a value of this `Match` type:</span></span>

```fsharp
let matchMethod = 
ProvidedMethod(
methodName = "Match", 
parameters = [ProvidedParameter("input", typeof<string>)], 
returnType = matchTy, 
InvokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)
matchMeth.AddXmlDoc "Searches the specified input string for the first ocurrence of this regular expression" 

ty.AddMember matchMeth
```

<span data-ttu-id="78ccc-302">Da Sie eine Instanzmethode erstellen, stellt `args.[0]` die `RegexTyped`-Instanz dar, für die die Methode aufgerufen wird, und `args.[1]` das Eingabeargument.</span><span class="sxs-lookup"><span data-stu-id="78ccc-302">Because you are creating an instance method, `args.[0]` represents the `RegexTyped` instance on which the method is being called, and `args.[1]` is the input argument.</span></span>

<span data-ttu-id="78ccc-303">Stellen Sie abschließend einen Konstruktor bereit, damit Instanzen des bereitgestellten Typs erstellt werden können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-303">Finally, provide a constructor so that instances of the provided type can be created.</span></span>

```fsharp
let ctor = ProvidedConstructor(
parameters = [], 
InvokeCode = fun args -> <@@ Regex(pattern, options) :> obj @@>)
ctor.AddXmlDoc("Initializes a regular expression instance.")

ty.AddMember ctor
```

<span data-ttu-id="78ccc-304">Der Konstruktor führt bei der Löschung zur Erstellung einer einfachen .NET Regex-Standardinstanz, die wiederum in einem Objekt geschachtelt wird, da `obj` die Löschung des bereitgestellten Typs ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-304">The constructor merely erases to the creation of a standard .NET Regex instance, which is again boxed to an object because `obj` is the erasure of the provided type.</span></span> <span data-ttu-id="78ccc-305">Mit dieser Änderung kann die API des Beispiels nun so verwendet werden, wie zuvor in diesem Thema beschrieben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-305">With that change, the sample API usage that specified earlier in the topic works as expected.</span></span> <span data-ttu-id="78ccc-306">Der folgende Code ist vollständig:</span><span class="sxs-lookup"><span data-stu-id="78ccc-306">The following code is complete and final:</span></span>

```fsharp
namespace Samples.FSharp.RegexTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open System.Text.RegularExpressions

[<TypeProvider>]
type public CheckedRegexProvider() as this =
inherit TypeProviderForNamespaces()

// Get the assembly and namespace used to house the provided types.
let thisAssembly = Assembly.GetExecutingAssembly()
let rootNamespace = "Samples.FSharp.RegexTypeProvider"
let baseTy = typeof<obj>
let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "RegexTyped", Some baseTy)

do regexTy.DefineStaticParameters(
parameters=staticParams, 
instantiationFunction=(fun typeName parameterValues ->

match parameterValues with 
| [| :? string as pattern|] -> 
// Create an instance of the regular expression. 




let r = System.Text.RegularExpressions.Regex(pattern)            

// Declare the typed regex provided type.



let ty = ProvidedTypeDefinition(
thisAssembly, 
rootNamespace, 
typeName, 
baseType = Some baseTy)

ty.AddXmlDoc "A strongly typed interface to the regular expression '%s'"

// Provide strongly typed version of Regex.IsMatch static method.
let isMatch = ProvidedMethod(
methodName = "IsMatch", 
parameters = [ProvidedParameter("input", typeof<string>)], 
returnType = typeof<bool>, 
IsStaticMethod = true,
InvokeCode = fun args -> <@@ Regex.IsMatch(%%args.[0], pattern) @@>) 

isMatch.AddXmlDoc "Indicates whether the regular expression finds a match in the specified input string"

ty.AddMember isMatch

// Provided type for matches
// Again, erase to obj even though the representation will always be a Match
let matchTy = ProvidedTypeDefinition(
"MatchType", 
baseType = Some baseTy, 
HideObjectMethods = true)

// Nest the match type within parameterized Regex type.
ty.AddMember matchTy

// Add group properties to match type
for group in r.GetGroupNames() do
// Ignore the group named 0, which represents all input.
if group <> "0" then
let prop = ProvidedProperty(
propertyName = group, 
propertyType = typeof<Group>, 
GetterCode = fun args -> <@@ ((%%args.[0]:obj) :?> Match).Groups.[group] @@>)
prop.AddXmlDoc(sprintf @"Gets the ""%s"" group from this match" group)
matchTy.AddMember(prop)

// Provide strongly typed version of Regex.Match instance method.
let matchMeth = ProvidedMethod(
methodName = "Match", 
parameters = [ProvidedParameter("input", typeof<string>)], 
returnType = matchTy, 
InvokeCode = fun args -> <@@ ((%%args.[0]:obj) :?> Regex).Match(%%args.[1]) :> obj @@>)
matchMeth.AddXmlDoc "Searches the specified input string for the first occurence of this regular expression"

ty.AddMember matchMeth

// Declare a constructor.
let ctor = ProvidedConstructor(
parameters = [], 
InvokeCode = fun args -> <@@ Regex(pattern) :> obj @@>)

// Add documentation to the constructor.
ctor.AddXmlDoc "Initializes a regular expression instance"

ty.AddMember ctor

ty
| _ -> failwith "unexpected parameter values")) 

do this.AddNamespace(rootNamespace, [regexTy])

[<TypeProviderAssembly>]
do ()
```

`Key Lessons`

<span data-ttu-id="78ccc-307">In diesem Abschnitt wird erläutert, wie ein Typanbieter erstellt wird, der seine statischen Parameter verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-307">This section explained how to create a type provider that operates on its static parameters.</span></span> <span data-ttu-id="78ccc-308">Der Anbieter überprüft den statischen Parameter und stellt Vorgänge auf Grundlage des ermittelten Werts bereit.</span><span class="sxs-lookup"><span data-stu-id="78ccc-308">The provider checks the static parameter and provides operations based on its value.</span></span>


## <a name="a-type-provider-that-is-backed-by-local-data"></a><span data-ttu-id="78ccc-309">Ein Typanbieter, der lokale Daten verarbeitet</span><span class="sxs-lookup"><span data-stu-id="78ccc-309">A Type Provider That Is Backed By Local Data</span></span>
<span data-ttu-id="78ccc-310">Häufig sollen mithilfe von Typanbietern APIs bereitgestellt werden, die nicht nur auf statischen Parametern, sondern zusätzlich auf Informationen von lokalen oder Remotesystemen basieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-310">Frequently you might want type providers to present APIs based on not only static parameters but also information from local or remote systems.</span></span> <span data-ttu-id="78ccc-311">In diesem Abschnitt werden Typanbieter erläutert, die auf lokalen Daten basieren, z. B. auf lokalen Datendateien.</span><span class="sxs-lookup"><span data-stu-id="78ccc-311">This section discusses type providers that are based on local data, such as local data files.</span></span>


### <a name="simple-csv-file-provider"></a><span data-ttu-id="78ccc-312">Einfacher CSV-Dateianbieter</span><span class="sxs-lookup"><span data-stu-id="78ccc-312">Simple CSV File Provider</span></span>
<span data-ttu-id="78ccc-313">Als einfaches Beispiel soll ein Typanbieter für den Zugriff auf wissenschaftliche Daten im CSV-Format (Comma Separated Value) betrachtet werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-313">As a simple example, consider a type provider for accessing scientific data in Comma Separated Value (CSV) format.</span></span> <span data-ttu-id="78ccc-314">In diesem Abschnitt wird davon ausgegangen, dass die CSV-Dateien eine Kopfzeile gefolgt von den Gleitkommadaten enthalten, wie in der folgenden Tabelle gezeigt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-314">This section assumes that the CSV files contain a header row followed by floating point data, as the following table illustrates:</span></span>



|<span data-ttu-id="78ccc-315">Abstand (Meter)</span><span class="sxs-lookup"><span data-stu-id="78ccc-315">Distance (meter)</span></span>|<span data-ttu-id="78ccc-316">Zeit (Sekunden)</span><span class="sxs-lookup"><span data-stu-id="78ccc-316">Time (second)</span></span>|
|----------------|-------------|
|<span data-ttu-id="78ccc-317">50.0</span><span class="sxs-lookup"><span data-stu-id="78ccc-317">50.0</span></span>|<span data-ttu-id="78ccc-318">3.7</span><span class="sxs-lookup"><span data-stu-id="78ccc-318">3.7</span></span>|
|<span data-ttu-id="78ccc-319">100.0</span><span class="sxs-lookup"><span data-stu-id="78ccc-319">100.0</span></span>|<span data-ttu-id="78ccc-320">5.2</span><span class="sxs-lookup"><span data-stu-id="78ccc-320">5.2</span></span>|
|<span data-ttu-id="78ccc-321">150.0</span><span class="sxs-lookup"><span data-stu-id="78ccc-321">150.0</span></span>|<span data-ttu-id="78ccc-322">6.4</span><span class="sxs-lookup"><span data-stu-id="78ccc-322">6.4</span></span>|
<span data-ttu-id="78ccc-323">In diesem Abschnitt wird erläutert, wie Sie einen Typ bereitstellen, mit dem Sie Zeilen mit einer `Distance`-Eigenschaft vom Typ `float<meter>` und einer `Time`-Eigenschaft vom Typ `float<second>` abrufen können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-323">This section shows how to provide a type that you can use to get rows with a `Distance` property of type `float<meter>` and a `Time` property of type `float<second>`.</span></span> <span data-ttu-id="78ccc-324">Der Einfachheit halber wird Folgendes vorausgesetzt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-324">For simplicity, the following assumptions are made:</span></span>


- <span data-ttu-id="78ccc-325">Namen der Kopfzeilen haben entweder Einheit oder haben das Format "Name (Einheit)" und enthalten keine Kommas.</span><span class="sxs-lookup"><span data-stu-id="78ccc-325">Header names are either unit-less or have the form "Name (unit)" and don't contain commas.</span></span>
<br />

- <span data-ttu-id="78ccc-326">Einheiten sind alle SI-Einheiten International (SI) Einheiten als die [Microsoft.FSharp.Data.UnitSystems.SI.UnitNames Module (f#)](https://msdn.microsoft.com/library/3cb43485-11f5-4aa7-a779-558f19d4013b) Modul definiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-326">Units are all Systeme International (SI) units as the [Microsoft.FSharp.Data.UnitSystems.SI.UnitNames Module (F#)](https://msdn.microsoft.com/library/3cb43485-11f5-4aa7-a779-558f19d4013b) module defines.</span></span>
<br />

- <span data-ttu-id="78ccc-327">Bei den Einheiten handelt es sich nur um einfache Einheiten (z. B. Meter) und nicht um zusammengesetzte Einheiten (z. B. Meter/Sekunde).</span><span class="sxs-lookup"><span data-stu-id="78ccc-327">Units are all simple (for example, meter) rather than compound (for example, meter/second).</span></span>
<br />

- <span data-ttu-id="78ccc-328">Alle Spalten enthalten Gleitkommadaten.</span><span class="sxs-lookup"><span data-stu-id="78ccc-328">All columns contain floating point data.</span></span>
<br />

<span data-ttu-id="78ccc-329">Bei einer umfassenderen Anbieterimplementierung könnten diese Einschränkungen gelockert werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-329">A more complete provider would loosen these restrictions.</span></span>

<span data-ttu-id="78ccc-330">Auch hier sollte im ersten Schritt überlegt werden, wie die fertige API aussehen soll.</span><span class="sxs-lookup"><span data-stu-id="78ccc-330">Again the first step is to consider how the API should look.</span></span> <span data-ttu-id="78ccc-331">Wenn die Datei `info.csv` mit dem Inhalt der vorherigen Tabelle vorliegt (in einem durch Trennzeichen getrennten Format), sollten Benutzer, die diesen Anbieter später verwenden, einen Code ähnlich dem folgenden Beispiel schreiben können:</span><span class="sxs-lookup"><span data-stu-id="78ccc-331">Given an `info.csv` file with the contents from the previous table (in comma-separated format), users of the provider should be able to write code that resembles the following example:</span></span>

```fsharp
let info = new MiniCsv<"info.csv">()
for row in info.Data do
let time = row.Time
printfn "%f" (float time)
```

<span data-ttu-id="78ccc-332">In diesem Fall sollte der Compiler diese Aufrufe ähnlich wie im folgenden Beispiel konvertieren:</span><span class="sxs-lookup"><span data-stu-id="78ccc-332">In this case, the compiler should convert these calls into something like the following example:</span></span>

```fsharp
let info = new MiniCsvFile("info.csv")
for row in info.Data do
let (time:float) = row.[1]
printfn "%f" (float time)
```

<span data-ttu-id="78ccc-333">Für eine optimale Übersetzung muss der Typanbieter einen echten `CsvFile`-Typ in der Assembly des Typanbieters definieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-333">The optimal translation will require the type provider to define a real `CsvFile` type in the type provider's assembly.</span></span> <span data-ttu-id="78ccc-334">Typanbieter basieren häufig auf einer Reihe von Hilfstypen und -methoden, um wichtige Logikabschnitte zu umschließen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-334">Type providers often rely on a few helper types and methods to wrap important logic.</span></span> <span data-ttu-id="78ccc-335">Da die Maßeinheiten zur Laufzeit gelöscht werden, können Sie `float[]` als gelöschten Typ für eine Zeile verwenden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-335">Because measures are erased at runtime, you can use a `float[]` as the erased type for a row.</span></span> <span data-ttu-id="78ccc-336">Der Compiler behandelt jede Spalte als eigenen Typ mit eigener Maßeinheit.</span><span class="sxs-lookup"><span data-stu-id="78ccc-336">The compiler will treat different columns as having different measure types.</span></span> <span data-ttu-id="78ccc-337">Zum Beispiel hat die erste Spalte im Beispiel den Typ `float<meter>`, die zweite den Typ `float<second>` usw.</span><span class="sxs-lookup"><span data-stu-id="78ccc-337">For example, the first column in our example has type `float<meter>`, and the second has `float<second>`.</span></span> <span data-ttu-id="78ccc-338">Dennoch kann die gelöschte Darstellung vergleichsweise einfach ausfallen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-338">However, the erased representation can remain quite simple.</span></span>

<span data-ttu-id="78ccc-339">Im folgenden Codebeispiel wird die Kernimplementierung veranschaulicht.</span><span class="sxs-lookup"><span data-stu-id="78ccc-339">The following code shows the core of the implementation.</span></span>

```fsharp
// Simple type wrapping CSV data
type CsvFile(filename) =
// Cache the sequence of all data lines (all lines but the first)
let data = 
seq { for line in File.ReadAllLines(filename) |> Seq.skip 1 do
yield line.Split(',') |> Array.map float }
|> Seq.cache
member __.Data = data

[<TypeProvider>]
type public MiniCsvProvider(cfg:TypeProviderConfig) as this =
inherit TypeProviderForNamespaces()

// Get the assembly and namespace used to house the provided types.
let asm = System.Reflection.Assembly.GetExecutingAssembly()
let ns = "Samples.FSharp.MiniCsvProvider"

// Create the main provided type.
let csvTy = ProvidedTypeDefinition(asm, ns, "MiniCsv", Some(typeof<obj>))

// Parameterize the type by the file to use as a template.
let filename = ProvidedStaticParameter("filename", typeof<string>)
do csvTy.DefineStaticParameters([filename], fun tyName [| :? string as filename |] ->

// Resolve the filename relative to the resolution folder.
let resolvedFilename = Path.Combine(cfg.ResolutionFolder, filename)

// Get the first line from the file.
let headerLine = File.ReadLines(resolvedFilename) |> Seq.head

// Define a provided type for each row, erasing to a float[].
let rowTy = ProvidedTypeDefinition("Row", Some(typeof<float[]>))

// Extract header names from the file, splitting on commas.
// use Regex matching to get the position in the row at which the field occurs
let headers = Regex.Matches(headerLine, "[^,]+")

// Add one property per CSV field.
for i in 0 .. headers.Count - 1 do
let headerText = headers.[i].Value

// Try to decompose this header into a name and unit.
let fieldName, fieldTy =
let m = Regex.Match(headerText, @"(?<field>.+) \((?<unit>.+)\)")
if m.Success then


let unitName = m.Groups.["unit"].Value
let units = ProvidedMeasureBuilder.Default.SI unitName
m.Groups.["field"].Value, ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>,[units])


else
// no units, just treat it as a normal float
headerText, typeof<float>

let prop = ProvidedProperty(fieldName, fieldTy, 
GetterCode = fun [row] -> <@@ (%%row:float[]).[i] @@>)

// Add metadata that defines the property's location in the referenced file.
prop.AddDefinitionLocation(1, headers.[i].Index + 1, filename)
rowTy.AddMember(prop) 

// Define the provided type, erasing to CsvFile.
let ty = ProvidedTypeDefinition(asm, ns, tyName, Some(typeof<CsvFile>))

// Add a parameterless constructor that loads the file that was used to define the schema.
let ctor0 = ProvidedConstructor([], 
InvokeCode = fun [] -> <@@ CsvFile(resolvedFilename) @@>)
ty.AddMember ctor0

// Add a constructor that takes the file name to load.
let ctor1 = ProvidedConstructor([ProvidedParameter("filename", typeof<string>)], 
InvokeCode = fun [filename] -> <@@ CsvFile(%%filename) @@>)
ty.AddMember ctor1

// Add a more strongly typed Data property, which uses the existing property at runtime.
let prop = ProvidedProperty("Data", typedefof<seq<_>>.MakeGenericType(rowTy), 
GetterCode = fun [csvFile] -> <@@ (%%csvFile:CsvFile).Data @@>)
ty.AddMember prop

// Add the row type as a nested type.
ty.AddMember rowTy
ty)

// Add the type to the namespace.
do this.AddNamespace(ns, [csvTy])
```

<span data-ttu-id="78ccc-340">Beachten Sie die folgenden Punkte in der Implementierung:</span><span class="sxs-lookup"><span data-stu-id="78ccc-340">Note the following points about the implementation:</span></span>


- <span data-ttu-id="78ccc-341">Überladene Konstruktoren gestatten es, entweder die ursprüngliche Datei oder eine andere Datei mit einem identischen Schema zu laden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-341">Overloaded constructors allow either the original file or one that has an identical schema to be read.</span></span> <span data-ttu-id="78ccc-342">Dieses Vorgehen ist üblich, wenn Sie einen Typanbieter für lokale oder Remotedatenquellen schreiben. Es ermöglicht die Verwendung einer lokalen Datei als Vorlage für die Remotedaten.</span><span class="sxs-lookup"><span data-stu-id="78ccc-342">This pattern is common when you write a type provider for local or remote data sources, and this pattern allows a local file to be used as the template for remote data.</span></span>
<br />  <span data-ttu-id="78ccc-343">Sie können die [TypeProviderConfig](https://msdn.microsoft.com/library/1cda7b9a-3d07-475d-9315-d65e1c97eb44) -Wert, der im typanbieterkonstruktor um relative Dateinamen aufzulösen übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-343">You can use the [TypeProviderConfig](https://msdn.microsoft.com/library/1cda7b9a-3d07-475d-9315-d65e1c97eb44) value that’s passed in to the type provider constructor to resolve relative file names.</span></span>
<br />

- <span data-ttu-id="78ccc-344">Sie können die `AddDefinitionLocation`-Methode verwenden, um den Speicherort der bereitgestellten Eigenschaften zu definieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-344">You can use the `AddDefinitionLocation` method to define the location of the provided properties.</span></span> <span data-ttu-id="78ccc-345">Aus diesem Grund bei Verwendung von `Go To Definition` für eine angegebene Eigenschaft wird die CSV-Datei in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-345">Therefore, if you use `Go To Definition` on a provided property, the CSV file will open in Visual Studio.</span></span>
<br />

- <span data-ttu-id="78ccc-346">Sie können den `ProvidedMeasureBuilder`-Typ verwenden, um nach den SI-Einheiten zu suchen und die relevanten `float<_>`-Typen zu generieren.</span><span class="sxs-lookup"><span data-stu-id="78ccc-346">You can use the `ProvidedMeasureBuilder` type to look up the SI units and to generate the relevant `float<_>` types.</span></span>
<br />

`Key Lessons`

<span data-ttu-id="78ccc-347">In diesem Abschnitt wurde erläutert, wie ein Typanbieter für eine lokale Datenquelle mit einem einfachen Schema erstellt werden kann, wenn das Schema in der Datenquelle selbst enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-347">This section explained how to create a type provider for a local data source with a simple schema that's contained in the data source itself.</span></span>


## <a name="going-further"></a><span data-ttu-id="78ccc-348">Weiterführende Themen</span><span class="sxs-lookup"><span data-stu-id="78ccc-348">Going Further</span></span>
<span data-ttu-id="78ccc-349">Die folgenden Abschnitte enthalten Vorschläge für das weitere selbstständige Lernen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-349">The following sections include suggestions for further study.</span></span>


### <a name="a-look-at-the-compiled-code-for-erased-types"></a><span data-ttu-id="78ccc-350">Ein Blick auf den kompilierten Code für gelöschte Typen</span><span class="sxs-lookup"><span data-stu-id="78ccc-350">A Look at the Compiled Code for Erased Types</span></span>
<span data-ttu-id="78ccc-351">Damit Sie einen Eindruck davon bekommen, welchen Einfluss die Verwendung des Typanbieters auf den ausgegebenen Code hat, betrachten Sie die folgende Funktion unter Verwendung des `HelloWorldTypeProvider`, der weiter oben in diesem Thema verwendet wurde.</span><span class="sxs-lookup"><span data-stu-id="78ccc-351">To give you some idea of how the use of the type provider corresponds to the code that's emitted, look at the following function by using the `HelloWorldTypeProvider` that's used earlier in this topic.</span></span>

```fsharp
let function1 () = 
let obj1 = Samples.HelloWorldTypeProvider.Type1("some data")
obj1.InstanceProperty
```

<span data-ttu-id="78ccc-352">Im Folgenden sehen Sie eine Abbildung des resultierenden Codes, der mit ildasm.exe dekompiliert wurde:</span><span class="sxs-lookup"><span data-stu-id="78ccc-352">Here’s an image of the resulting code decompiled by using ildasm.exe:</span></span>

```
.class public abstract auto ansi sealed Module1
extends [mscorlib]System.Object
{
.custom instance void [FSharp.Core]Microsoft.FSharp.Core.CompilationMappingAtt
ribute::.ctor(valuetype [FSharp.Core]Microsoft.FSharp.Core.SourceConstructFlags)
= ( 01 00 07 00 00 00 00 00 )
.method public static int32  function1() cil managed
{
// Code size       24 (0x18)
.maxstack  3
.locals init ([0] object obj1)
IL_0000:  nop
IL_0001:  ldstr      "some data"
IL_0006:  unbox.any  [mscorlib]System.Object
IL_000b:  stloc.0
IL_000c:  ldloc.0
IL_000d:  call       !!0 [FSharp.Core_2]Microsoft.FSharp.Core.LanguagePrimit
ives/IntrinsicFunctions::UnboxGeneric<string>(object)
IL_0012:  callvirt   instance int32 [mscorlib_3]System.String::get_Length()
IL_0017:  ret
} // end of method Module1::function1

} // end of class Module1
```

<span data-ttu-id="78ccc-353">Wie das Beispiel zeigt, wurden alle Erwähnungen des Typs `Type1` und der `InstanceProperty`-Eigenschaft gelöscht, sodass nur noch die Vorgänge und Laufzeittypen vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="78ccc-353">As the example shows, all mentions of the type `Type1` and the `InstanceProperty` property have been erased, leaving only operations on the runtime types involved.</span></span>


### <a name="design-and-naming-conventions-for-type-providers"></a><span data-ttu-id="78ccc-354">Entwurf- und Namenskonventionen für Typanbieter</span><span class="sxs-lookup"><span data-stu-id="78ccc-354">Design and Naming Conventions for Type Providers</span></span>
<span data-ttu-id="78ccc-355">Beachten Sie die folgenden Konventionen, wenn Sie Typanbieter erstellen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-355">Observe the following conventions when authoring type providers.</span></span>


- `Providers for Connectivity Protocols`
<br />  <span data-ttu-id="78ccc-356">Im Allgemeinen sollten die Namen der meisten Anbieter-DLLs für Daten- und Dienstkonnektivitätsprotokolle, wie OData oder SQL-Verbindungen, auf `TypeProvider` oder `TypeProviders` enden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-356">In general, names of most provider DLLs for data and service connectivity protocols, such as OData or SQL connections, should end in `TypeProvider` or `TypeProviders`.</span></span> <span data-ttu-id="78ccc-357">Verwenden Sie z. B. einen DLL-Namen ähnlich der folgenden Zeichenfolge:</span><span class="sxs-lookup"><span data-stu-id="78ccc-357">For example, use a DLL name that resembles the following string:</span></span>
<br />

```
  Fabrikam.Management.BasicTypeProviders.dll
```

  <span data-ttu-id="78ccc-358">Stellen Sie sicher, dass die bereitgestellten Typen Member des richtigen Namespace sind, und geben Sie das Konnektivitätsprotokoll an, das Sie implementiert haben:</span><span class="sxs-lookup"><span data-stu-id="78ccc-358">Ensure that your provided types are members of the corresponding namespace, and indicate the connectivity protocol that you implemented:</span></span>
<br />

```
  Fabrikam.Management.BasicTypeProviders.WmiConnection<…>
  Fabrikam.Management.BasicTypeProviders.DataProtocolConnection<…>
```

- `Utility Providers for General Coding`
<br />  <span data-ttu-id="78ccc-359">Hilfstypanbieter, wie der zuvor erstellte Anbieter für reguläre Ausdrücke, können in einer Basisbibliothek enthalten sein, wie das folgende Beispiel zeigt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-359">For a utility type provider such as that for regular expressions, the type provider may be part of a base library, as the following example shows:</span></span>
<br />

```fsharp
  #r "Fabrikam.Core.Text.Utilities.dll"
```

  <span data-ttu-id="78ccc-360">In diesem Fall würde der bereitgestellte Typ an einer geeigneten Stelle entsprechend den normalen .NET-Entwurfskonventionen erscheinen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-360">In this case, the provided type would appear at an appropriate point according to normal .NET design conventions:</span></span>
<br />

```fsharp
  open Fabrikam.Core.Text.RegexTyped
  
  let regex = new RegexTyped<"a+b+a+b+">()
```

- `Singleton Data Sources`
<br />  <span data-ttu-id="78ccc-361">Einige Typanbieter stellen eine Verbindung mit einer einzelnen dedizierten Datenquelle her und machen ausschließlich Daten verfügbar.</span><span class="sxs-lookup"><span data-stu-id="78ccc-361">Some type providers connect to a single dedicated data source and provide only data.</span></span> <span data-ttu-id="78ccc-362">In diesem Fall sollten Sie das `TypeProvider`-Suffix weglassen und die normalen Konventionen für die .NET-Benennung befolgen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-362">In this case, you should drop the `TypeProvider` suffix and use normal conventions for .NET naming:</span></span>
<br />

```fsharp
  #r "Fabrikam.Data.Freebase.dll"
  
  let data = Fabrikam.Data.Freebase.Astronomy.Asteroids
```

  <span data-ttu-id="78ccc-363">Weitere Informationen finden Sie in der `GetConnection`-Entwurfskonvention, die weiter unten in diesem Thema beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-363">For more information, see the `GetConnection` design convention that's described later in this topic.</span></span>
<br />


### <a name="design-patterns-for-type-providers"></a><span data-ttu-id="78ccc-364">Entwurfsmuster für Typanbieter</span><span class="sxs-lookup"><span data-stu-id="78ccc-364">Design Patterns for Type Providers</span></span>
<span data-ttu-id="78ccc-365">In den folgenden Abschnitten werden Entwurfsmuster beschrieben, die Sie beim Erstellen von Typanbietern heranziehen können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-365">The following sections describe design patterns you can use when authoring type providers.</span></span>


#### <a name="the-getconnection-design-pattern"></a><span data-ttu-id="78ccc-366">Das Entwurfsmuster GetConnection</span><span class="sxs-lookup"><span data-stu-id="78ccc-366">The GetConnection Design Pattern</span></span>
<span data-ttu-id="78ccc-367">Die meisten Typanbieter sollten unter Beachtung des `GetConnection`-Musters geschrieben werden, das von den Typanbietern in FSharp.Data.TypeProviders.dll verwendet wird, wie im folgenden Beispiel gezeigt:</span><span class="sxs-lookup"><span data-stu-id="78ccc-367">Most type providers should be written to use the `GetConnection` pattern that's used by the type providers in FSharp.Data.TypeProviders.dll, as the following example shows:</span></span>

```fsharp
#r "Fabrikam.Data.WebDataStore.dll"

type Service = Fabrikam.Data.WebDataStore<…static connection parameters…>

let connection = Service.GetConnection(…dynamic connection parameters…)

let data = connection.Astronomy.Asteroids
```

#### <a name="type-providers-backed-by-remote-data-and-services"></a><span data-ttu-id="78ccc-368">Typanbieter, die auf Remotedaten und -dienste zugreifen</span><span class="sxs-lookup"><span data-stu-id="78ccc-368">Type Providers Backed By Remote Data and Services</span></span>
<span data-ttu-id="78ccc-369">Bevor Sie einen Typanbieter erstellen, der auf Remotedaten und -dienste zugreift, müssen Sie einige Probleme berücksichtigen, die bei der Programmierung von Verbindungen auftreten können.</span><span class="sxs-lookup"><span data-stu-id="78ccc-369">Before you create a type provider that's backed by remote data and services, you must consider a range of issues that are inherent in connected programming.</span></span> <span data-ttu-id="78ccc-370">Folgende Überlegungen sollten Sie berücksichtigen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-370">These issues include the following considerations:</span></span>


- <span data-ttu-id="78ccc-371">Schemazuordnung</span><span class="sxs-lookup"><span data-stu-id="78ccc-371">schema mapping</span></span>
<br />

- <span data-ttu-id="78ccc-372">Aktivität und Ungültigkeit bei Schemaänderungen</span><span class="sxs-lookup"><span data-stu-id="78ccc-372">liveness and invalidation in the presence of schema change</span></span>
<br />

- <span data-ttu-id="78ccc-373">Zwischenspeicherung von Schemas</span><span class="sxs-lookup"><span data-stu-id="78ccc-373">schema caching</span></span>
<br />

- <span data-ttu-id="78ccc-374">Asynchrone Implementierungen von Datenzugriffsvorgängen</span><span class="sxs-lookup"><span data-stu-id="78ccc-374">asynchronous implementations of data access operations</span></span>
<br />

- <span data-ttu-id="78ccc-375">Unterstützen von Abfragen, einschließlich LINQ-Abfragen</span><span class="sxs-lookup"><span data-stu-id="78ccc-375">supporting queries, including LINQ queries</span></span>
<br />

- <span data-ttu-id="78ccc-376">Anmeldeinformationen und Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="78ccc-376">credentials and authentication</span></span>
<br />

<span data-ttu-id="78ccc-377">Die Probleme werden in diesem Thema nicht weiter im Detail erläutert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-377">This topic doesn't explore these issues further.</span></span>


### <a name="additional-authoring-techniques"></a><span data-ttu-id="78ccc-378">Weitere Techniken für Entwurf und Erstellung</span><span class="sxs-lookup"><span data-stu-id="78ccc-378">Additional Authoring Techniques</span></span>
<span data-ttu-id="78ccc-379">Wenn Sie eigene Typanbieter schreiben, können die folgenden zusätzlichen Techniken ebenfalls hilfreich sein.</span><span class="sxs-lookup"><span data-stu-id="78ccc-379">When you write your own type providers, you might want to use the following additional techniques.</span></span>


- `Creating Types and Members On-Demand`
<br />  <span data-ttu-id="78ccc-380">Die ProvidedType-API stellt verzögerte Versionen von AddMember zur Verfügung.</span><span class="sxs-lookup"><span data-stu-id="78ccc-380">The ProvidedType API has delayed versions of AddMember.</span></span>
<br />

```fsharp
  type ProvidedType =
  member AddMemberDelayed  : (unit -> MemberInfo)      -> unit
  member AddMembersDelayed : (unit -> MemberInfo list) -> unit
```

  <span data-ttu-id="78ccc-381">Diese Versionen werden verwendet, um Typenräume zu erstellen, die erst bei Bedarf generiert werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-381">These versions are used to create on-demand spaces of types.</span></span>
<br />

- `Providing Array, ByRef, and Pointer types`
<br />  <span data-ttu-id="78ccc-382">Sie können bereitgestellte Member (deren Signaturen Arraytypen, byref-Typen und Instanziierungen von generischen Typen enthalten) erstellen, indem Sie die normalen Typen `MakeArrayType`, `MakePointerType` und `MakeGenericType` einer beliebigen Instanz von System.Type verwenden, einschließlich `ProvidedTypeDefinitions`.</span><span class="sxs-lookup"><span data-stu-id="78ccc-382">You make provided members (whose signatures include array types, byref types, and instantiations of generic types) by using the normal `MakeArrayType`, `MakePointerType`, and `MakeGenericType` on any instance of System.Type, including `ProvidedTypeDefinitions`.</span></span>
<br />

- `Providing Unit of Measure Annotations`
<br />  <span data-ttu-id="78ccc-383">Die ProvidedTypes-API stellt Hilfsprogramme zur Angabe von Maßeinheiten für Werte bereit.</span><span class="sxs-lookup"><span data-stu-id="78ccc-383">The ProvidedTypes API provides helpers for providing measure annotations.</span></span> <span data-ttu-id="78ccc-384">Um beispielsweise den Typ `float<kg>` bereitzustellen, verwenden Sie folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="78ccc-384">For example, to provide the type `float<kg>`, use the following code:</span></span>
<br />

```fsharp
  let measures = ProvidedMeasureBuilder.Default
  let kg = measures.SI "kilogram"
  let m = measures.SI "meter"
  let float_kg = measures.AnnotateType(typeof<float>,[kg])
```

  <span data-ttu-id="78ccc-385">Um den Typ `Nullable<decimal<kg/m^2>>` bereitzustellen, verwenden Sie folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="78ccc-385">To provide the type `Nullable<decimal<kg/m^2>>`, use the following code:</span></span>
<br />

```fsharp
  let kgpm2 = measures.Ratio(kg, measures.Square m)
  let dkgpm2 = measures.AnnotateType(typeof<decimal>,[kgpm2])
  let nullableDecimal_kgpm2 = typedefof<System.Nullable<_>>.MakeGenericType [|dkgpm2 |]
```

- `Accessing Project-Local or Script-Local Resources`
<br />  <span data-ttu-id="78ccc-386">Jede Instanz eines Typanbieters kann während der Erstellung als `TypeProviderConfig`-Wert angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-386">Each instance of a type provider can be given a `TypeProviderConfig` value during construction.</span></span> <span data-ttu-id="78ccc-387">Dieser Wert enthält den „Auflösungsordner“ für den Anbieter (dass heißt, den Projektordner für die Kompilierung oder das Verzeichnis, das ein Skript enthält), die Liste der Assemblys, auf die verwiesen wird, und einige andere Informationen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-387">This value contains the "resolution folder" for the provider (that is, the project folder for the compilation or the directory that contains a script), the list of referenced assemblies, and other information.</span></span>
<br />

- `Invalidation`
<br />  <span data-ttu-id="78ccc-388">Anbieter können Signale zum Aufheben einer Validierung auslösen, um den F#-Sprachdienst zu benachrichtigen, dass sich die Schemaannahmen möglicherweise geändert haben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-388">Providers can raise invalidation signals to notify the F# language service that the schema assumptions may have changed.</span></span> <span data-ttu-id="78ccc-389">Bei einer Invalidierung wird die Typüberprüfung wiederholt, sofern der Anbieter in Visual Studio gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-389">When invalidation occurs, a typecheck is redone if the provider is being hosted in Visual Studio.</span></span> <span data-ttu-id="78ccc-390">Dieses Signal wird ignoriert, wenn der Anbieter in F# Interactive oder vom F#-Compiler (fsc.exe) gehostet wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-390">This signal will be ignored when the provider is hosted in F# Interactive or by the F# Compiler (fsc.exe).</span></span>
<br />

- `Caching Schema Information`
<br />  <span data-ttu-id="78ccc-391">Anbieter müssen für den Zugriff auf Schemainformationen häufig einen Cache verwenden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-391">Providers must often cache access to schema information.</span></span> <span data-ttu-id="78ccc-392">Die zwischengespeicherten Daten sollten unter einem Dateinamen gespeichert werden, der als statischer Parameter oder in den Benutzerdaten angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-392">The cached data should be stored by using a file name that's given as a static parameter or as user data.</span></span> <span data-ttu-id="78ccc-393">Ein Beispiel für die Schemazwischenspeicherung ist der `LocalSchemaFile`-Parameter in den Typanbietern in der `FSharp.Data.TypeProviders`-Assembly.</span><span class="sxs-lookup"><span data-stu-id="78ccc-393">An example of schema caching is the `LocalSchemaFile` parameter in the type providers in the `FSharp.Data.TypeProviders` assembly.</span></span> <span data-ttu-id="78ccc-394">In der Implementierung dieser Anbieter weist der statische Parameter den Typanbieter an, die Schemainformationen aus der angegebenen lokalen Datei abzurufen, anstatt über das Netzwerk auf die Datenquelle zuzugreifen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-394">In the implementation of these providers, this static parameter directs the type provider to use the schema information in the specified local file instead of accessing the data source over the network.</span></span> <span data-ttu-id="78ccc-395">Um zwischengespeicherte Schemainformationen verwenden zu können, müssen Sie außerdem den statischen Parameter `ForceUpdate` auf `false` festlegen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-395">To use cached schema information, you must also set the static parameter `ForceUpdate` to `false`.</span></span> <span data-ttu-id="78ccc-396">Sie können ein ähnliches Verfahren verwenden, um sowohl online als auch offline Datenzugriffe zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-396">You could use a similar technique to enable online and offline data access.</span></span>
<br />

- `Backing Assembly`
<br />  <span data-ttu-id="78ccc-397">Wenn Sie eine DLL- oder EXE-Datei kompilieren, wird die zugrunde liegende DLL-Datei für generierte Typen statisch in die resultierende Assembly verknüpft.</span><span class="sxs-lookup"><span data-stu-id="78ccc-397">When you compile a .dll or .exe file, the backing .dll file for generated types is statically linked into the resulting assembly.</span></span> <span data-ttu-id="78ccc-398">Dieser Link wird erstellt, indem die IL-Typdefinitionen (Intermediate Language) und alle verwalteten Ressourcen aus der Unterstützungsassembly in die endgültige Assembly kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-398">This link is created by copying the Intermediate Language (IL) type definitions and any managed resources from the backing assembly into the final assembly.</span></span> <span data-ttu-id="78ccc-399">Wenn Sie F# Interactive verwenden, wird die zugrunde liegende DLL-Datei nicht kopiert und stattdessen direkt in den F# Interactive-Prozess geladen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-399">When you use F# Interactive, the backing .dll file isn't copied and is instead loaded directly into the F# Interactive process.</span></span>
<br />

- `Exceptions and Diagnostics from Type Providers`
<br />  <span data-ttu-id="78ccc-400">Jede Verwendung der Member von bereitgestellten Typen kann eine Ausnahme auslösen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-400">All uses of all members from provided types may throw exceptions.</span></span> <span data-ttu-id="78ccc-401">Wenn ein Typanbieter eine Ausnahme auslöst, ordnet der Hostcompiler den Fehler immer einem bestimmten Typanbieter zu.</span><span class="sxs-lookup"><span data-stu-id="78ccc-401">In all cases, if a type provider throws an exception, the host compiler attributes the error to a specific type provider.</span></span>
<br />
  - <span data-ttu-id="78ccc-402">Typanbieterausnahmen sollten niemals zu internen Compilerfehlern führen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-402">Type provider exceptions should never result in internal compiler errors.</span></span>
<br />

  - <span data-ttu-id="78ccc-403">Typanbieter können keine Warnungen ausgeben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-403">Type providers can't report warnings.</span></span>
<br />

  - <span data-ttu-id="78ccc-404">Wenn ein Typanbieter im F#-Compiler, in einer F#-Entwicklungsumgebung oder in F# Interactive gehostet wird, werden alle Ausnahmen dieses Anbieters abgefangen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-404">When a type provider is hosted in the F# compiler, an F# development environment, or F# Interactive, all exceptions from that provider are caught.</span></span> <span data-ttu-id="78ccc-405">Die Message-Eigenschaft enthält dabei immer den Fehlertext, und es wird keine Stapelüberwachung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-405">The Message property is always the error text, and no stack trace appears.</span></span> <span data-ttu-id="78ccc-406">Wenn Sie eine Ausnahme auslösen möchten, können Sie hierzu die folgenden Beispiele verwenden:</span><span class="sxs-lookup"><span data-stu-id="78ccc-406">If you’re going to throw an exception, you can throw the following examples:</span></span>
<br />
    - `System.NotSupportedException`
<br />

    - `System.IO.IOException`
<br />

    - `System.Exception`
<br />


#### <a name="providing-generated-types"></a><span data-ttu-id="78ccc-407">Bereitstellen von generierten Typen</span><span class="sxs-lookup"><span data-stu-id="78ccc-407">Providing Generated Types</span></span>
<span data-ttu-id="78ccc-408">Bisher wurde in diesem Dokument erläutert, wie gelöschte Typen bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-408">So far, this document has explained how provide erased types.</span></span> <span data-ttu-id="78ccc-409">Sie können den Typanbietermechanismus in F# auch verwenden, um generierte Typen bereitzustellen, die als echte .NET-Typdefinitionen in das Programm des Benutzers übernommen werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-409">You can also use the type provider mechanism in F# to provide generated types, which are added as real .NET type definitions into the users' program.</span></span> <span data-ttu-id="78ccc-410">Auf generierte bereitgestellte Typen müssen Sie über die Typdefinition verweisen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-410">You must refer to generated provided types by using a type definition.</span></span>

```fsharp
open Microsoft.FSharp.TypeProviders 

type Service = ODataService<" http://services.odata.org/Northwind/Northwind.svc/">
```

<span data-ttu-id="78ccc-411">Der Hilfscode "ProvidedTypes-0.2", der Teil der Version 3.0 von F# ist, bietet nur eine eingeschränkte Unterstützung für das Bereitstellen von generierten Typen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-411">The ProvidedTypes-0.2 helper code that is part of the F# 3.0 release has only limited support for providing generated types.</span></span> <span data-ttu-id="78ccc-412">Die folgenden Aussagen müssen für eine generierte Typdefinition zutreffen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-412">The following statements must be true for a generated type definition:</span></span>


- <span data-ttu-id="78ccc-413">IsErased muss auf `false` festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-413">IsErased must be set to `false`.</span></span>
<br />

- <span data-ttu-id="78ccc-414">Der Anbieter muss über eine Assembly verfügen, der eine tatsächliche .NET-DLL-Datei mit einer entsprechenden, auf dem Datenträger verfügbaren DLL-Datei zugrunde liegt.</span><span class="sxs-lookup"><span data-stu-id="78ccc-414">The provider must have an assembly that has an actual backing .NET .dll file with a matching .dll file on disk.</span></span>
<br />

<span data-ttu-id="78ccc-415">Sie müssen `ConvertToGenerated` auch für einen übergeordneten Stammtyp aufrufen, dessen geschachtelte Typen einen vollständigen Satz von generierten Typen bilden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-415">You must also call `ConvertToGenerated` on a root provided type whose nested types form a closed set of generated types.</span></span> <span data-ttu-id="78ccc-416">Dieser Aufruf gibt die angegebene Definition für einen bereitgestellten Typ und die Definitionen der geschachtelten Typen in eine Assembly aus und passt die `Assembly`-Eigenschaft aller Typdefinitionen so an, dass die betreffende Assembly zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-416">This call emits the given provided type definition and its nested type definitions into an assembly and adjusts the `Assembly` property of all provided type definitions to return that assembly.</span></span> <span data-ttu-id="78ccc-417">Die Assembly wird nur ausgegeben, wenn zum ersten Mal auf die Assembly-Eigenschaft des Stammtyps zugegriffen wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-417">The assembly is emitted only when the Assembly property on the root type is accessed for the first time.</span></span> <span data-ttu-id="78ccc-418">Der F#-Hostcompiler greift auf diese Eigenschaft zu, sobald er eine generierende Typdeklaration für den Typ verarbeitet.</span><span class="sxs-lookup"><span data-stu-id="78ccc-418">The host F# compiler does access this property when it processes a generative type declaration for the type.</span></span>


## <a name="rules-and-limitations"></a><span data-ttu-id="78ccc-419">Regeln und Einschränkungen</span><span class="sxs-lookup"><span data-stu-id="78ccc-419">Rules and Limitations</span></span>
<span data-ttu-id="78ccc-420">Berücksichtigen Sie beim Schreiben von Typanbietern die folgenden Regeln und Einschränkungen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-420">When you write type providers, keep the following rules and limitations in mind.</span></span>


- `Provided types must be reachable.`
<br />  <span data-ttu-id="78ccc-421">Alle bereitgestellten Typen müssen für die nicht geschachtelten Typen erreichbar sein.</span><span class="sxs-lookup"><span data-stu-id="78ccc-421">All provided types should be reachable from the non-nested types.</span></span> <span data-ttu-id="78ccc-422">Die nicht geschachtelten Typen werden im Aufruf des `TypeProviderForNamespaces`-Konstruktors oder bei einem Aufruf von `AddNamespace` übergeben.</span><span class="sxs-lookup"><span data-stu-id="78ccc-422">The non-nested types are given in the call to the `TypeProviderForNamespaces` constructor or a call to `AddNamespace`.</span></span> <span data-ttu-id="78ccc-423">Wenn der Anbieter z. B. den Typ `StaticClass.P : T` bereitstellt, müssen Sie sicherstellen, dass T entweder ein nicht geschachtelter Typ ist oder unter einem Typ geschachtelt wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-423">For example, if the provider provides a type `StaticClass.P : T`, you must ensure that T is either a non-nested type or nested under one.</span></span>
<br />  <span data-ttu-id="78ccc-424">Einige Anbieter verwenden beispielsweise eine statische Klasse wie `DataTypes`, die diese `T1, T2, T3, ...`-Typen enthält.</span><span class="sxs-lookup"><span data-stu-id="78ccc-424">For example, some providers have a static class such as `DataTypes` that contain these `T1, T2, T3, ...` types.</span></span> <span data-ttu-id="78ccc-425">Andernfalls wird ein Fehler mit der Meldung ausgegeben, dass in der Assembly A ein Verweis auf den Typ T enthalten ist, der Typ aber in dieser Assembly nicht gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="78ccc-425">Otherwise, the error says that a reference to type T in assembly A was found, but the type couldn't be found in that assembly.</span></span> <span data-ttu-id="78ccc-426">Wenn dieser Fehler angezeigt wird, stellen Sie sicher, dass alle Untertypen für die Anbietertypen erreichbar sind.</span><span class="sxs-lookup"><span data-stu-id="78ccc-426">If this error appears, verify that all your subtypes can be reached from the provider types.</span></span> <span data-ttu-id="78ccc-427">Hinweis: Diese `T1, T2, T3...` Typen werden als bezeichnet den *auf dynamische* Typen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-427">Note: These `T1, T2, T3...` types are referred to as the *on-the-fly* types.</span></span> <span data-ttu-id="78ccc-428">Denken Sie daran, diese in einen erreichbaren Namespace oder in einen übergeordneten Typ einzufügen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-428">Remember to put them in an accessible namespace or a parent type.</span></span>
<br />

- `Limitations of the Type Provider Mechanism`
<br />  <span data-ttu-id="78ccc-429">Für den Typanbietermechanismus in F# gelten folgende Einschränkungen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-429">The type provider mechanism in F# has the following limitations:</span></span>
<br />
  - <span data-ttu-id="78ccc-430">Die zugrunde liegende Infrastruktur für Typanbieter in F# unterstützt keine generischen bereitgestellten Typen und keine generischen bereitgestellten Methoden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-430">The underlying infrastructure for type providers in F# doesn't support provided generic types or provided generic methods.</span></span>
<br />

  - <span data-ttu-id="78ccc-431">Der Mechanismus unterstützt keine geschachtelten Typen mit statischen Parametern.</span><span class="sxs-lookup"><span data-stu-id="78ccc-431">The mechanism doesn't support nested types with static parameters.</span></span>
<br />

- `Limitations of the ProvidedTypes Support Code`
<br />  <span data-ttu-id="78ccc-432">Für den `ProvidedTypes`-Unterstützungscode gelten folgende Regeln und Einschränkungen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-432">The `ProvidedTypes` support code has the following rules and limitations:</span></span>
<br />
  1. <span data-ttu-id="78ccc-433">Bereitgestellte Eigenschaften mit indizierten Gettern und Settern sind nicht implementiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-433">Provided properties with indexed getters and setters aren't implemented.</span></span>
<br />

  2. <span data-ttu-id="78ccc-434">Bereitgestellte Ereignisse sind nicht implementiert.</span><span class="sxs-lookup"><span data-stu-id="78ccc-434">Provided events aren't implemented.</span></span>
<br />

  3. <span data-ttu-id="78ccc-435">Die bereitgestellten Typen und Informationsobjekte dürfen nur für den Typanbietermechanismus in F# verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-435">The provided types and information objects should be used only for the type provider mechanism in F#.</span></span> <span data-ttu-id="78ccc-436">Sie können nicht als allgemeine System.Type-Objekte verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-436">They aren't more generally usable as System.Type objects.</span></span>
<br />

  4. <span data-ttu-id="78ccc-437">Die Konstrukte, die Sie in Zitaten zur Definition von Methodenimplementierungen verwenden können, unterliegen bestimmten Beschränkungen.</span><span class="sxs-lookup"><span data-stu-id="78ccc-437">The constructs that you can use in quotations that define method implementations have several limitations.</span></span> <span data-ttu-id="78ccc-438">Sie können auf den Quellcode für die ProvidedTypes - verweisen*Version* um festzustellen, welche Konstrukte in Anführungszeichen unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-438">You can refer to the source code for ProvidedTypes-*Version* to see which constructs are supported in quotations.</span></span>
<br />

- `Type providers must generate output assemblies that are .dll files, not .exe files.`
<br />


## <a name="development-tips"></a><span data-ttu-id="78ccc-439">Tipps für die Entwicklung</span><span class="sxs-lookup"><span data-stu-id="78ccc-439">Development Tips</span></span>
<span data-ttu-id="78ccc-440">Die folgenden Tipps können während des Entwicklungsprozesses hilfreich sein.</span><span class="sxs-lookup"><span data-stu-id="78ccc-440">You might find the following tips helpful during the development process.</span></span>


- <span data-ttu-id="78ccc-441">`Run Two Instances of Visual Studio.`Sie können den Typanbieter in einer Instanz entwickeln und Testen Sie den Anbieter in den anderen, da die Test-IDE eine Sperre für die DLL-Datei wird, die verhindert, dass den Typanbieter neu erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="78ccc-441">`Run Two Instances of Visual Studio.` You can develop the type provider in one instance and test the provider in the other because the test IDE will take a lock on the .dll file that prevents the type provider from being rebuilt.</span></span> <span data-ttu-id="78ccc-442">Daher müssen Sie die zweite Instanz von Visual Studio schließen, wenn der Anbieter in der ersten Instanz erstellt wird, und anschließend die zweite Instanz erneut öffnen, sobald die Erstellung abgeschlossen ist.</span><span class="sxs-lookup"><span data-stu-id="78ccc-442">Thus, you must close the second instance of Visual Studio while the provider is built in the first instance, and then you must reopen the second instance after the provider is built.</span></span>
<br />

- <span data-ttu-id="78ccc-443">`Debug type providers by using invocations of fsc.exe.`Sie können Typanbieter mit den folgenden Tools aufrufen:</span><span class="sxs-lookup"><span data-stu-id="78ccc-443">`Debug type providers by using invocations of fsc.exe.` You can invoke type providers by using the following tools:</span></span>
<br />
  - <span data-ttu-id="78ccc-444">fsc.exe (der F#-Befehlszeilencompiler)</span><span class="sxs-lookup"><span data-stu-id="78ccc-444">fsc.exe (The F# command line compiler)</span></span>
<br />

  - <span data-ttu-id="78ccc-445">fsi.exe (der F# Interactive-Compiler)</span><span class="sxs-lookup"><span data-stu-id="78ccc-445">fsi.exe (The F# Interactive compiler)</span></span>
<br />

  - <span data-ttu-id="78ccc-446">devenv.exe (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="78ccc-446">devenv.exe (Visual Studio)</span></span>
<br />

  <span data-ttu-id="78ccc-447">In vielen Fällen können Typanbieter am einfachsten debuggt werden, indem Sie fsc.exe zusammen mit einer Testskriptdatei verwenden (z. B. script.fsx).</span><span class="sxs-lookup"><span data-stu-id="78ccc-447">You can often debug type providers most easily by using fsc.exe on a test script file (for example, script.fsx).</span></span> <span data-ttu-id="78ccc-448">Sie können ein Debugger von einer Eingabeaufforderung aus starten.</span><span class="sxs-lookup"><span data-stu-id="78ccc-448">You can launch a debugger from a command prompt.</span></span>
<br />

```
  devenv /debugexe fsc.exe script.fsx
```

  <span data-ttu-id="78ccc-449">Zur Protokollierung können Sie die normale Ausgabe auf die Standardausgabe verwenden.</span><span class="sxs-lookup"><span data-stu-id="78ccc-449">You can use print-to-stdout logging.</span></span>
<br />


## <a name="see-also"></a><span data-ttu-id="78ccc-450">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="78ccc-450">See Also</span></span>
[<span data-ttu-id="78ccc-451">Typanbieter</span><span class="sxs-lookup"><span data-stu-id="78ccc-451">Type Providers</span></span>](index.md)