---
title: ICorDebugStaticFieldSymbol::GetAddress-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 5a6c9a5a-ec72-4c40-a9c3-cee7baa63687
caps.latest.revision: "4"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 20c0c934772625d27057957d00e53fb4b485c4fd
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugstaticfieldsymbolgetaddress-method"></a><span data-ttu-id="e528c-102">ICorDebugStaticFieldSymbol::GetAddress-Methode</span><span class="sxs-lookup"><span data-stu-id="e528c-102">ICorDebugStaticFieldSymbol::GetAddress Method</span></span>
<span data-ttu-id="e528c-103">Ruft die Adresse eines statischen Felds ab.</span><span class="sxs-lookup"><span data-stu-id="e528c-103">Gets the address of a static field.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e528c-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="e528c-104">Syntax</span></span>  
  
```  
HRESULT GetAddress(  
   [out] CORDB_ADDRESS *pRVA  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="e528c-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="e528c-105">Parameters</span></span>  
 <span data-ttu-id="e528c-106">pRVA</span><span class="sxs-lookup"><span data-stu-id="e528c-106">pRVA</span></span>  
 <span data-ttu-id="e528c-107">[out] Ein Zeiger auf die relative virtuelle Adresse (RVA) des statischen Felds.</span><span class="sxs-lookup"><span data-stu-id="e528c-107">[out] A pointer to the relative virtual address (RVA) of the static field.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="e528c-108">Hinweise</span><span class="sxs-lookup"><span data-stu-id="e528c-108">Remarks</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e528c-109">Diese Methode ist nur in Verbindung mit .NET Native verfügbar.</span><span class="sxs-lookup"><span data-stu-id="e528c-109">This method is available with .NET Native only.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e528c-110">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="e528c-110">Requirements</span></span>  
 <span data-ttu-id="e528c-111">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e528c-111">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e528c-112">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e528c-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e528c-113">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e528c-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e528c-114">**.NET Framework-Versionen:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e528c-114">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e528c-115">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e528c-115">See Also</span></span>  
 [<span data-ttu-id="e528c-116">ICorDebugStaticFieldSymbol-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="e528c-116">ICorDebugStaticFieldSymbol Interface</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugstaticfieldsymbol-interface.md)  
 [<span data-ttu-id="e528c-117">Debugschnittstellen</span><span class="sxs-lookup"><span data-stu-id="e528c-117">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)