---
title: "Profilerstellung für globale statische Funktionen"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- global static functions [.NET Framework profiling]
- profiling global static functions [.NET Framework]
- unmanaged global static functions [.NET Framework], profiling
ms.assetid: 08a13a57-dc49-488d-b937-31e3051fda97
caps.latest.revision: "14"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 4da4509a6e8b87490cee076b403f3fa525de91e0
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="profiling-global-static-functions"></a><span data-ttu-id="05b8a-102">Profilerstellung für globale statische Funktionen</span><span class="sxs-lookup"><span data-stu-id="05b8a-102">Profiling Global Static Functions</span></span>
<span data-ttu-id="05b8a-103">In diesem Abschnitt wird beschrieben, die nicht verwalteten API-Funktionen, die die profilerstellungs-API verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="05b8a-103">This section describes the unmanaged API functions that the profiling API uses.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="05b8a-104">In diesem Abschnitt</span><span class="sxs-lookup"><span data-stu-id="05b8a-104">In This Section</span></span>  
  
## <a name="net-framework-version-1-profiling-functions"></a><span data-ttu-id="05b8a-105">Profilerstellung für .NET Framework Version 1-Funktionen</span><span class="sxs-lookup"><span data-stu-id="05b8a-105">.NET Framework version 1 Profiling Functions</span></span>  
 [<span data-ttu-id="05b8a-106">FunctionEnter-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-106">FunctionEnter Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionenter-function.md)  
 <span data-ttu-id="05b8a-107">Benachrichtigt den Profiler, dass Steuerelement an eine Funktion übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="05b8a-107">Notifies the profiler that control is being passed to a function.</span></span> <span data-ttu-id="05b8a-108">In .NET Framework 2.0 veraltet.</span><span class="sxs-lookup"><span data-stu-id="05b8a-108">Deprecated in the .NET Framework 2.0.</span></span>  
  
 [<span data-ttu-id="05b8a-109">FunctionLeave-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-109">FunctionLeave Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionleave-function.md)  
 <span data-ttu-id="05b8a-110">Benachrichtigt den Profiler, dass eine Funktion an den Aufrufer zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="05b8a-110">Notifies the profiler that a function is about to return to the caller.</span></span> <span data-ttu-id="05b8a-111">In .NET Framework 2.0 veraltet.</span><span class="sxs-lookup"><span data-stu-id="05b8a-111">Deprecated in the .NET Framework 2.0.</span></span>  
  
 [<span data-ttu-id="05b8a-112">FunctionTailcall-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-112">FunctionTailcall Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functiontailcall-function.md)  
 <span data-ttu-id="05b8a-113">Benachrichtigt den Profiler an, die gegenwärtig ausgeführte Funktion ist einen Endeaufruf an eine andere Funktion ausführen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-113">Notifies the profiler that the currently executing function is about to perform a tail call to another function.</span></span> <span data-ttu-id="05b8a-114">In .NET Framework 2.0 veraltet.</span><span class="sxs-lookup"><span data-stu-id="05b8a-114">Deprecated in the .NET Framework 2.0.</span></span>  
  
## <a name="net-framework-version-2-profiling-functions"></a><span data-ttu-id="05b8a-115">Profilerstellung für .NET Framework Version 2-Funktionen</span><span class="sxs-lookup"><span data-stu-id="05b8a-115">.NET Framework version 2 Profiling Functions</span></span>  
 [<span data-ttu-id="05b8a-116">FunctionIDMapper-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-116">FunctionIDMapper Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md)  
 <span data-ttu-id="05b8a-117">Benachrichtigt den Profiler, dass der angegebene Bezeichner einer Funktion einer alternativen ID zu verwendende zugeordnet werden kann die [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md), [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md), und [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md) Rückrufe für diese Funktion.</span><span class="sxs-lookup"><span data-stu-id="05b8a-117">Notifies the profiler that the given identifier of a function may be remapped to an alternative ID to be used in the [FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md), [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md), and [FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md) callbacks for that function.</span></span> <span data-ttu-id="05b8a-118">Außerdem ermöglicht es dem Profiler, um anzugeben, ob er Rückrufe für diese Funktion empfangen will</span><span class="sxs-lookup"><span data-stu-id="05b8a-118">Also enables the profiler to indicate whether it wants to receive callbacks for that function</span></span>  
  
 [<span data-ttu-id="05b8a-119">FunctionEnter2-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-119">FunctionEnter2 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)  
 <span data-ttu-id="05b8a-120">Benachrichtigt den Profiler, dass Steuerelement an eine Funktion übergeben werden und Informationen über den Stapelrahmen und die Funktionsargumente bietet.</span><span class="sxs-lookup"><span data-stu-id="05b8a-120">Notifies the profiler that control is being passed to a function and provides information about the stack frame and function arguments.</span></span> <span data-ttu-id="05b8a-121">Als veraltet markierte in der [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].</span><span class="sxs-lookup"><span data-stu-id="05b8a-121">Deprecated in the [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].</span></span>  
  
 [<span data-ttu-id="05b8a-122">FunctionLeave2-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-122">FunctionLeave2 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)  
 <span data-ttu-id="05b8a-123">Benachrichtigt den Profiler, dass eine Funktion an den Aufrufer zurückgegeben wird, und Informationen über den Stapel und -Rückgabewert enthält.</span><span class="sxs-lookup"><span data-stu-id="05b8a-123">Notifies the profiler that a function is about to return to the caller and provides information about the stack frame and function return value.</span></span> <span data-ttu-id="05b8a-124">Als veraltet markierte in der [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].</span><span class="sxs-lookup"><span data-stu-id="05b8a-124">Deprecated in the [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].</span></span>  
  
 [<span data-ttu-id="05b8a-125">FunctionTailcall2-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-125">FunctionTailcall2 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)  
 <span data-ttu-id="05b8a-126">Benachrichtigt den Profiler an, die gegenwärtig ausgeführte Funktion ist einen Endeaufruf an eine andere Funktion ausführen und enthält Informationen über den Stapelrahmen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-126">Notifies the profiler that the currently executing function is about to perform a tail call to another function and provides information about the stack frame.</span></span> <span data-ttu-id="05b8a-127">Als veraltet markierte in der [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].</span><span class="sxs-lookup"><span data-stu-id="05b8a-127">Deprecated in the [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)].</span></span>  
  
 [<span data-ttu-id="05b8a-128">StackSnapshotCallback-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-128">StackSnapshotCallback Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md)  
 <span data-ttu-id="05b8a-129">Stellt Informationen über jeden verwalteten Frame und jeder Ausführung von nicht verwalteten Frames auf dem Stapel während ein Stackwalk, die von initiiert wird der Profiler die [ICorProfilerInfo2:: DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="05b8a-129">Provides the profiler with information about each managed frame and each run of unmanaged frames on the stack during a stack walk, which is initiated by the [ICorProfilerInfo2::DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) method.</span></span>  
  
## <a name="net-framework-version-4-profiling-functions"></a><span data-ttu-id="05b8a-130">Profilerstellung für .NET Framework Version 4-Funktionen</span><span class="sxs-lookup"><span data-stu-id="05b8a-130">.NET Framework version 4 Profiling Functions</span></span>  
 [<span data-ttu-id="05b8a-131">FunctionIDMapper2-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-131">FunctionIDMapper2 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionidmapper2-function.md)  
 <span data-ttu-id="05b8a-132">Benachrichtigt den Profiler, dass der angegebene Bezeichner einer Funktion einer alternativen ID zu verwendende zugeordnet werden kann die [FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md), [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md), und [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md), oder[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md), [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md), und [FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md) Rückrufe für diese Funktion.</span><span class="sxs-lookup"><span data-stu-id="05b8a-132">Notifies the profiler that the given identifier of a function may be remapped to an alternative ID to be used in the [FunctionEnter3](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md), [FunctionLeave3](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md), and [FunctionTailcall3](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md), or[FunctionEnter3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md), [FunctionLeave3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md), and [FunctionTailcall3WithInfo](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md) callbacks for that function.</span></span> <span data-ttu-id="05b8a-133">Außerdem ermöglicht es dem Profiler, um anzugeben, ob er Rückrufe für diese Funktion empfangen will aus.</span><span class="sxs-lookup"><span data-stu-id="05b8a-133">Also enables the profiler to indicate whether it wants to receive callbacks for that function.</span></span>  
  
 <span data-ttu-id="05b8a-134">`FunctionIDMapper2`Erweitert die [FunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md) -Funktion mit einem `clientData` Parameter, den Profiler verwenden können, um Mehrdeutigkeiten zwischen Laufzeiten aufzulösen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-134">`FunctionIDMapper2` extends the [FunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/functionidmapper-function.md) function with a `clientData` parameter, which profilers may use to disambiguate among runtimes.</span></span>  
  
 [<span data-ttu-id="05b8a-135">FunctionEnter3-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-135">FunctionEnter3 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)  
 <span data-ttu-id="05b8a-136">Benachrichtigt den Profiler, dass Steuerelement an eine Funktion übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="05b8a-136">Notifies the profiler that control is being passed to a function.</span></span>  
  
 [<span data-ttu-id="05b8a-137">FunctionEnter3WithInfo-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-137">FunctionEnter3WithInfo Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)  
 <span data-ttu-id="05b8a-138">Benachrichtigt den Profiler, dass die Steuerung an eine Funktion übergeben wird, und stellt ein Handle, das übergeben werden kann [ICorProfilerInfo3:: Getfunctionenter3info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md) auf den Stapel und die Funktionsargumente abzurufen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-138">Notifies the profiler that control is being passed to a function, and provides a handle that can be passed to [ICorProfilerInfo3::GetFunctionEnter3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionenter3info-method.md) to retrieve the stack frame and function arguments.</span></span>  
  
 [<span data-ttu-id="05b8a-139">FunctionLeave3-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-139">FunctionLeave3 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)  
 <span data-ttu-id="05b8a-140">Benachrichtigt den Profiler, Steuerung von einer Funktion zurückgegeben wird.</span><span class="sxs-lookup"><span data-stu-id="05b8a-140">Notifies the profiler that control is being returned from a function.</span></span>  
  
 [<span data-ttu-id="05b8a-141">FunctionLeave3WithInfo-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-141">FunctionLeave3WithInfo Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)  
 <span data-ttu-id="05b8a-142">Benachrichtigt den Profiler, Steuerung von einer Funktion zurückgegeben wird, und stellt ein Handle, das übergeben werden kann [ICorProfilerInfo3:: Getfunctionleave3info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md) auf den Stapelrahmen und den Rückgabewert abzurufen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-142">Notifies the profiler that control is being returned from a function, and provides a handle that can be passed to [ICorProfilerInfo3::GetFunctionLeave3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctionleave3info-method.md) to retrieve the stack frame and the return value.</span></span>  
  
 [<span data-ttu-id="05b8a-143">FunctionTailcall3-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-143">FunctionTailcall3 Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3-function.md)  
 <span data-ttu-id="05b8a-144">Benachrichtigt den Profiler an, die gegenwärtig ausgeführte Funktion ist einen Endeaufruf an eine andere Funktion ausführen.</span><span class="sxs-lookup"><span data-stu-id="05b8a-144">Notifies the profiler that the currently executing function is about to perform a tail call to another function.</span></span>  
  
 [<span data-ttu-id="05b8a-145">FunctionTailcall3WithInfo-Funktion</span><span class="sxs-lookup"><span data-stu-id="05b8a-145">FunctionTailcall3WithInfo Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)  
 <span data-ttu-id="05b8a-146">Benachrichtigt den Profiler, die aktuell ausgeführte Funktion ist einen Endeaufruf an eine andere Funktion ausführen, und stellt ein Handle, das übergeben werden kann [ICorProfilerInfo3:: Getfunctiontailcall3info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md) zum Abrufen des Stapelrahmens.</span><span class="sxs-lookup"><span data-stu-id="05b8a-146">Notifies the profiler that the currently executing function is about to perform a tail call to another function, and provides a handle that can be passed to [ICorProfilerInfo3::GetFunctionTailcall3Info](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getfunctiontailcall3info-method.md) to retrieve the stack frame.</span></span>  
  
## <a name="related-sections"></a><span data-ttu-id="05b8a-147">Verwandte Abschnitte</span><span class="sxs-lookup"><span data-stu-id="05b8a-147">Related Sections</span></span>  
 [<span data-ttu-id="05b8a-148">Übersicht über die profilerstellung</span><span class="sxs-lookup"><span data-stu-id="05b8a-148">Profiling Overview</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-overview.md)  
  
 [<span data-ttu-id="05b8a-149">Profilerstellungsschnittstellen</span><span class="sxs-lookup"><span data-stu-id="05b8a-149">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
  
 [<span data-ttu-id="05b8a-150">Profilerstellungsenumerationen</span><span class="sxs-lookup"><span data-stu-id="05b8a-150">Profiling Enumerations</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)  
  
 [<span data-ttu-id="05b8a-151">Profilerstellungsstrukturen</span><span class="sxs-lookup"><span data-stu-id="05b8a-151">Profiling Structures</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-structures.md)