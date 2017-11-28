---
title: ICorDebugEnum::Skip-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugEnum.Skip
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugEnum::Skip
helpviewer_keywords:
- ICorDebugEnum::Skip method [.NET Framework debugging]
- Skip method, ICorDebugEnum interface [.NET Framework debugging]
ms.assetid: e925d88a-67a5-4f76-88b8-09cedeed0232
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: d109d8e28f94edc3eeceeb22d2d0639d010b532e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugenumskip-method"></a><span data-ttu-id="8c2fb-102">ICorDebugEnum::Skip-Methode</span><span class="sxs-lookup"><span data-stu-id="8c2fb-102">ICorDebugEnum::Skip Method</span></span>
<span data-ttu-id="8c2fb-103">Verschiebt den Cursor in der Enumeration, um die angegebene Anzahl von Elementen.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-103">Moves the cursor forward in the enumeration by the specified number of items.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="8c2fb-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="8c2fb-104">Syntax</span></span>  
  
```  
HRESULT Skip (  
    [in] ULONG celt  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="8c2fb-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="8c2fb-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="8c2fb-106">[in] Die Anzahl von Elementen, die den Cursor vorwärts zu bewegen.</span><span class="sxs-lookup"><span data-stu-id="8c2fb-106">[in] The number of items by which to move the cursor forward.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="8c2fb-107">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="8c2fb-107">Requirements</span></span>  
 <span data-ttu-id="8c2fb-108">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8c2fb-108">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="8c2fb-109">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="8c2fb-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="8c2fb-110">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="8c2fb-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="8c2fb-111">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="8c2fb-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="8c2fb-112">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="8c2fb-112">See Also</span></span>  
 [<span data-ttu-id="8c2fb-113">ICorDebugEnum Schnittstelle1</span><span class="sxs-lookup"><span data-stu-id="8c2fb-113">ICorDebugEnum Interface1</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugenum-interface1.md)