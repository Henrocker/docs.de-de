---
title: ICorDebugArrayValue::GetRank-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugArrayValue.GetRank
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugArrayValue::GetRank
helpviewer_keywords:
- ICorDebugArrayValue::GetRank method [.NET Framework debugging]
- GetRank method, ICorDebugArrayValue interface [.NET Framework debugging]
ms.assetid: 5e83c82c-593d-4691-90b0-383d218b415e
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: a7e92a0edfe220bda820550cc385bf2eb3846b08
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugarrayvaluegetrank-method"></a><span data-ttu-id="7c5ca-102">ICorDebugArrayValue::GetRank-Methode</span><span class="sxs-lookup"><span data-stu-id="7c5ca-102">ICorDebugArrayValue::GetRank Method</span></span>
<span data-ttu-id="7c5ca-103">Ruft die Anzahl der Dimensionen im Array ab.</span><span class="sxs-lookup"><span data-stu-id="7c5ca-103">Gets the number of dimensions in the array.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7c5ca-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="7c5ca-104">Syntax</span></span>  
  
```  
HRESULT GetRank (  
    [out] ULONG32   *pnRank  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7c5ca-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="7c5ca-105">Parameters</span></span>  
 `pnRank`  
 <span data-ttu-id="7c5ca-106">[out] Ein Zeiger auf die Anzahl der Dimensionen in diesem `ICorDebugArrayValue` Objekt.</span><span class="sxs-lookup"><span data-stu-id="7c5ca-106">[out] A pointer to the number of dimensions in this `ICorDebugArrayValue` object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7c5ca-107">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="7c5ca-107">Requirements</span></span>  
 <span data-ttu-id="7c5ca-108">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7c5ca-108">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7c5ca-109">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="7c5ca-109">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="7c5ca-110">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7c5ca-110">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7c5ca-111">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7c5ca-111">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>