---
title: Enumerationen (F#)
description: Informationen Sie zum F#-Enumerationen anstelle von literalen zu verwenden, um den Code besser lesbar und unterhaltbar zu gestalten.
keywords: Visual F#, F#, funktionale Programmierung
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 9272bf5a-9a9f-4314-9e34-a3248e5244f5
ms.openlocfilehash: de0273900b707c99e6fb1bcc84e5c2b9ef2bc725
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="enumerations"></a><span data-ttu-id="c2980-104">Enumerationen</span><span class="sxs-lookup"><span data-stu-id="c2980-104">Enumerations</span></span>

<span data-ttu-id="c2980-105">*Enumerationen*, auch bekannt als *Enumerationen*,, sind ganzzahlige Typen, in dem Bezeichnungen auf eine Teilmenge der Werte zugewiesen werden.</span><span class="sxs-lookup"><span data-stu-id="c2980-105">*Enumerations*, also known as *enums*, , are integral types where labels are assigned to a subset of the values.</span></span> <span data-ttu-id="c2980-106">Sie können diese anstelle von Literalen verwenden, um Code lesbarer und verwaltbarer zu machen.</span><span class="sxs-lookup"><span data-stu-id="c2980-106">You can use them in place of literals to make code more readable and maintainable.</span></span>


## <a name="syntax"></a><span data-ttu-id="c2980-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="c2980-107">Syntax</span></span>

```fsharp
type enum-name =
| value1 = integer-literal1
| value2 = integer-literal2
...
```

## <a name="remarks"></a><span data-ttu-id="c2980-108">Hinweise</span><span class="sxs-lookup"><span data-stu-id="c2980-108">Remarks</span></span>
<span data-ttu-id="c2980-109">Eine Enumeration sieht ähnlich wie eine Unterscheidungs-Union, die einfache Werte verfügt, mit dem Unterschied, dass die Werte angegeben werden können.</span><span class="sxs-lookup"><span data-stu-id="c2980-109">An enumeration looks much like a discriminated union that has simple values, except that the values can be specified.</span></span> <span data-ttu-id="c2980-110">Die Werte sind in der Regel ganze Zahlen, die mit 0 oder 1 beginnen, oder ganze Zahlen enthält, die Bitpositionen darstellen.</span><span class="sxs-lookup"><span data-stu-id="c2980-110">The values are typically integers that start at 0 or 1, or integers that represent bit positions.</span></span> <span data-ttu-id="c2980-111">Wenn eine Enumeration Bitpositionen darstellen soll, verwenden Sie zudem die [Flags](xref:System.FlagsAttribute) Attribut.</span><span class="sxs-lookup"><span data-stu-id="c2980-111">If an enumeration is intended to represent bit positions, you should also use the [Flags](xref:System.FlagsAttribute) attribute.</span></span>

<span data-ttu-id="c2980-112">Der zugrunde liegende Typ der Enumeration wird durch das Literal, das verwendet wird, bestimmt, sodass z. B. Sie z. B. Literale mit Suffix verwenden können `1u`, `2u`und so weiter für ganze Zahl ohne Vorzeichen (`uint32`) Typ.</span><span class="sxs-lookup"><span data-stu-id="c2980-112">The underlying type of the enumeration is determined from the literal that is used, so that, for example, you can use literals with a suffix, such as `1u`, `2u`, and so on, for an unsigned integer (`uint32`) type.</span></span>

<span data-ttu-id="c2980-113">Wenn Sie auf der benannten Werte verweisen, müssen Sie den Namen des Enumerationstyps selbst als verwenden einen Qualifizierer, also `enum-name.value1`, nicht nur `value1`.</span><span class="sxs-lookup"><span data-stu-id="c2980-113">When you refer to the named values, you must use the name of the enumeration type itself as a qualifier, that is, `enum-name.value1`, not just `value1`.</span></span> <span data-ttu-id="c2980-114">Dieses Verhalten unterscheidet sich von dem der Unterscheidungs-Unions.</span><span class="sxs-lookup"><span data-stu-id="c2980-114">This behavior differs from that of discriminated unions.</span></span> <span data-ttu-id="c2980-115">Dies ist immer Schreibberechtigung Enumerationen der [RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15) Attribut.</span><span class="sxs-lookup"><span data-stu-id="c2980-115">This is because enumerations always have the [RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15) attribute.</span></span>

<span data-ttu-id="c2980-116">Der folgende Code zeigt die Deklaration und Verwendung einer Enumeration.</span><span class="sxs-lookup"><span data-stu-id="c2980-116">The following code shows the declaration and use of an enumeration.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2101.fs)]

<span data-ttu-id="c2980-117">Sie können einfach Enumerationen in den zugrunde liegenden Typ konvertieren mit dem entsprechenden Operator, wie im folgenden Code gezeigt.</span><span class="sxs-lookup"><span data-stu-id="c2980-117">You can easily convert enumerations to the underlying type by using the appropriate operator, as shown in the following code.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2102.fs)]

<span data-ttu-id="c2980-118">Enumerationstypen können einen der folgenden zugrunde liegenden Typen aufweisen: `sbyte`, `byte`, `int16`, `uint16`, `int32`, `uint32`, `int64`, `uint16`, `uint64`, und `char`.</span><span class="sxs-lookup"><span data-stu-id="c2980-118">Enumerated types can have one of the following underlying types: `sbyte`, `byte`, `int16`, `uint16`, `int32`, `uint32`, `int64`, `uint16`, `uint64`, and `char`.</span></span> <span data-ttu-id="c2980-119">Enumerationstypen werden als Typen, die vom geerbt sind in .NET Framework dargestellt `System.Enum`, die wiederum geerbt wird von `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="c2980-119">Enumeration types are represented in the .NET Framework as types that are inherited from `System.Enum`, which in turn is inherited from `System.ValueType`.</span></span> <span data-ttu-id="c2980-120">Daher werden auf Werttypen, die auf dem Stapel oder Inline in dem Objekt gespeichert sind, und jeden Wert von der zugrunde liegende Typ ist ein gültiger Wert der Enumeration.</span><span class="sxs-lookup"><span data-stu-id="c2980-120">Thus, they are value types that are located on the stack or inline in the containing object, and any value of the underlying type is a valid value of the enumeration.</span></span> <span data-ttu-id="c2980-121">Dies ist wichtig, wenn einen Mustervergleich für Enumeration Werte, weil Sie müssen ein Muster angeben, der die unbenannten Werte abfängt.</span><span class="sxs-lookup"><span data-stu-id="c2980-121">This is significant when pattern matching on enumeration values, because you have to provide a pattern that catches the unnamed values.</span></span>

<span data-ttu-id="c2980-122">Die `enum` Funktion in der f#-Bibliothek dienen zum Generieren der einem Enumerationswert entspricht, auch einen anderen Wert als eine der vordefinierten benannten Werte.</span><span class="sxs-lookup"><span data-stu-id="c2980-122">The `enum` function in the F# library can be used to generate an enumeration value, even a value other than one of the predefined, named values.</span></span> <span data-ttu-id="c2980-123">Sie verwenden die `enum` -Funktion wie folgt.</span><span class="sxs-lookup"><span data-stu-id="c2980-123">You use the `enum` function as follows.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2103.fs)]

<span data-ttu-id="c2980-124">Die Standardeinstellung `enum` Funktion kann mit Datentyp `int32`.</span><span class="sxs-lookup"><span data-stu-id="c2980-124">The default `enum` function works with type `int32`.</span></span> <span data-ttu-id="c2980-125">Aus diesem Grund, Sie kann nicht mit Enumerationstypen verwendet werden, die andere zugrunde liegende Typen aufweisen.</span><span class="sxs-lookup"><span data-stu-id="c2980-125">Therefore, it cannot be used with enumeration types that have other underlying types.</span></span> <span data-ttu-id="c2980-126">Verwenden Sie stattdessen die folgenden Schritte aus.</span><span class="sxs-lookup"><span data-stu-id="c2980-126">Instead, use the following.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2104.fs)]
    
## <a name="see-also"></a><span data-ttu-id="c2980-127">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c2980-127">See Also</span></span>
[<span data-ttu-id="c2980-128">F#-Sprachreferenz</span><span class="sxs-lookup"><span data-stu-id="c2980-128">F# Language Reference</span></span>](index.md)

[<span data-ttu-id="c2980-129">Umwandlung und Konvertierungen</span><span class="sxs-lookup"><span data-stu-id="c2980-129">Casting and Conversions</span></span>](casting-and-conversions.md)