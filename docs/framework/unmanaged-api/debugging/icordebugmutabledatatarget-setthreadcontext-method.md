---
title: ICorDebugMutableDataTarget::SetThreadContext Method
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 8c0d01d5-67e5-4522-9ccf-c8f3a78cb4fd
caps.latest.revision: "5"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 8c43ef5405ed582cc55af69d7f41887c0615965f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugmutabledatatargetsetthreadcontext-method"></a><span data-ttu-id="f21c5-102">ICorDebugMutableDataTarget::SetThreadContext Method</span><span class="sxs-lookup"><span data-stu-id="f21c5-102">ICorDebugMutableDataTarget::SetThreadContext Method</span></span>
<span data-ttu-id="f21c5-103">Legt den Kontext (Registerwerte) für einen Thread fest.</span><span class="sxs-lookup"><span data-stu-id="f21c5-103">Sets the context (register values) for a thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f21c5-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="f21c5-104">Syntax</span></span>  
  
```  
HRESULT SetThreadContext(  
   [in] DWORD dwThreadID,  
   [in] ULONG32 contextSize,   [in, size_is(contextSize)] const BYTE * pContext);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="f21c5-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="f21c5-105">Parameters</span></span>  
 `dwThreadID`  
 <span data-ttu-id="f21c5-106">[in] Der vom Betriebssystem definierte Threadbezeichner.</span><span class="sxs-lookup"><span data-stu-id="f21c5-106">[in] The operating system-defined thread identifier.</span></span>  
  
 `contextSize`  
 <span data-ttu-id="f21c5-107">[in] Die Größe des zu schreibenden `pContext`-Puffers.</span><span class="sxs-lookup"><span data-stu-id="f21c5-107">[in] The size of the `pContext` buffer to be written.</span></span>  
  
 `pContext`  
 <span data-ttu-id="f21c5-108">[in] Ein Zeiger auf die zu schreibenden Bytes.</span><span class="sxs-lookup"><span data-stu-id="f21c5-108">[in] A pointer to the bytes to be written.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="f21c5-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="f21c5-109">Remarks</span></span>  
 <span data-ttu-id="f21c5-110">Die `SetThreadContext`-Methode aktualisiert den aktuellen Kontext für den Thread, der durch das vom Betriebssystem definierte `dwThreadID`-Argument angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="f21c5-110">The `SetThreadContext` method updates the current context for the thread specified by the operating system-defined `dwThreadID` argument.</span></span> <span data-ttu-id="f21c5-111">Das Format des Kontextdatensatzes wird von der Plattform erkennbar bestimmt die [ICorDebugDataTarget:: GetPlatform](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="f21c5-111">The format of the context record is determined by the platform indicated by the [ICorDebugDataTarget::GetPlatform](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget-getplatform-method.md) method.</span></span> <span data-ttu-id="f21c5-112">Unter Windows ist dies ein [Kontext](http://msdn.microsoft.com/library/windows/desktop/ms679284.aspx) Struktur.</span><span class="sxs-lookup"><span data-stu-id="f21c5-112">On Windows, this is a [CONTEXT](http://msdn.microsoft.com/library/windows/desktop/ms679284.aspx) structure.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f21c5-113">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="f21c5-113">Requirements</span></span>  
 <span data-ttu-id="f21c5-114">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f21c5-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f21c5-115">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f21c5-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f21c5-116">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f21c5-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f21c5-117">**.NET Framework-Versionen:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f21c5-117">**.NET Framework Versions:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f21c5-118">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f21c5-118">See Also</span></span>  
 [<span data-ttu-id="f21c5-119">ICorDebugMutableDataTarget-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="f21c5-119">ICorDebugMutableDataTarget Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmutabledatatarget-interface.md)  
 [<span data-ttu-id="f21c5-120">Debugschnittstellen</span><span class="sxs-lookup"><span data-stu-id="f21c5-120">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)