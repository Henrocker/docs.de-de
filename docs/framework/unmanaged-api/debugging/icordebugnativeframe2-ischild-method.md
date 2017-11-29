---
title: ICorDebugNativeFrame2::IsChild-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugNativeFrame2.IsChild Method
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugNativeFrame2::IsChild
helpviewer_keywords:
- IsChild method [.NET Framework debugging]
- ICorDebugNativeFrame2::IsChild method [.NET Framework debugging]
ms.assetid: 9e2aae09-49cb-4fbd-81e5-e29cd864a88b
topic_type: apiref
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 006543e473ca3b7cc1818b2b4641567ce37f6f0e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugnativeframe2ischild-method"></a><span data-ttu-id="70261-102">ICorDebugNativeFrame2::IsChild-Methode</span><span class="sxs-lookup"><span data-stu-id="70261-102">ICorDebugNativeFrame2::IsChild Method</span></span>
<span data-ttu-id="70261-103">Bestimmt, ob der aktuelle Rahmen ist ein untergeordneter Frame ist.</span><span class="sxs-lookup"><span data-stu-id="70261-103">Determines whether the current frame is a child frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="70261-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="70261-104">Syntax</span></span>  
  
```  
HRESULT IsChild([out] BOOL * pIsChild);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="70261-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="70261-105">Parameters</span></span>  
 `pIsChild`  
 <span data-ttu-id="70261-106">[out] Ein boolescher Wert, der angibt, ob der aktuelle Rahmen ist ein untergeordneter Frame ist.</span><span class="sxs-lookup"><span data-stu-id="70261-106">[out] A Boolean value that specifies whether the current frame is a child frame.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="70261-107">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="70261-107">Return Value</span></span>  
 <span data-ttu-id="70261-108">Diese Methode gibt die folgenden spezifischen HRESULTs sowie HRESULT-Fehler zurück, die Methodenfehler anzeigen.</span><span class="sxs-lookup"><span data-stu-id="70261-108">This method returns the following specific HRESULTs as well as HRESULT errors that indicate method failure.</span></span>  
  
|<span data-ttu-id="70261-109">HRESULT</span><span class="sxs-lookup"><span data-stu-id="70261-109">HRESULT</span></span>|<span data-ttu-id="70261-110">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="70261-110">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="70261-111">S_OK</span><span class="sxs-lookup"><span data-stu-id="70261-111">S_OK</span></span>|<span data-ttu-id="70261-112">Der untergeordnete Status wurde erfolgreich zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="70261-112">The child status was successfully returned.</span></span>|  
|<span data-ttu-id="70261-113">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="70261-113">E_FAIL</span></span>|<span data-ttu-id="70261-114">Der untergeordnete Status konnte nicht zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="70261-114">The child status could not be returned.</span></span>|  
|<span data-ttu-id="70261-115">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="70261-115">E_INVALIDARG</span></span>|<span data-ttu-id="70261-116">`pIsChild` ist NULL.</span><span class="sxs-lookup"><span data-stu-id="70261-116">`pIsChild` is null.</span></span>|  
  
## <a name="exceptions"></a><span data-ttu-id="70261-117">Ausnahmen</span><span class="sxs-lookup"><span data-stu-id="70261-117">Exceptions</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="70261-118">Hinweise</span><span class="sxs-lookup"><span data-stu-id="70261-118">Remarks</span></span>  
 <span data-ttu-id="70261-119">Die `IsChild` -Methode zurückkehrt `true` die Frame-Objekt, das auf dem Sie die Methode aufrufen, ist ein untergeordnetes Element von einem anderen Frame.</span><span class="sxs-lookup"><span data-stu-id="70261-119">The `IsChild` method returns `true` if the frame object on which you call the method is a child of another frame.</span></span> <span data-ttu-id="70261-120">Wenn dies der Fall ist, verwenden Sie die [IsMatchingParentFrame](../../../../docs/framework/unmanaged-api/debugging/icordebugnativeframe2-ismatchingparentframe-method.md) -Methode überprüft, ob ein Frame mit seinem übergeordneten Element ist.</span><span class="sxs-lookup"><span data-stu-id="70261-120">If this is the case, use the [IsMatchingParentFrame](../../../../docs/framework/unmanaged-api/debugging/icordebugnativeframe2-ismatchingparentframe-method.md) method to check whether a frame is its parent.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="70261-121">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="70261-121">Requirements</span></span>  
 <span data-ttu-id="70261-122">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="70261-122">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="70261-123">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="70261-123">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="70261-124">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="70261-124">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="70261-125">**.NET Framework-Versionen:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="70261-125">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="70261-126">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="70261-126">See Also</span></span>  
 [<span data-ttu-id="70261-127">ICorDebugNativeFrame2-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="70261-127">ICorDebugNativeFrame2 Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugnativeframe2-interface.md)  
 [<span data-ttu-id="70261-128">Debugschnittstellen</span><span class="sxs-lookup"><span data-stu-id="70261-128">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="70261-129">Debuggen</span><span class="sxs-lookup"><span data-stu-id="70261-129">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)