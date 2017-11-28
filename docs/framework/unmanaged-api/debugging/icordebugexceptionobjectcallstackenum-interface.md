---
title: ICorDebugExceptionObjectCallStackEnum-Schnittstelle
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugExceptionObjectCallStackEnum
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugExceptionObjectCallStackEnum
helpviewer_keywords: ICorDebugExceptionObjectCallStackEnum interface [.NET Framework debugging]
ms.assetid: 39dffa18-c71b-48c4-b11d-e814631ab1e9
topic_type: apiref
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 4814de2de71ba0fa4d1400f0be27fa4942febf54
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugexceptionobjectcallstackenum-interface"></a><span data-ttu-id="27cf9-102">ICorDebugExceptionObjectCallStackEnum-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="27cf9-102">ICorDebugExceptionObjectCallStackEnum Interface</span></span>
<span data-ttu-id="27cf9-103">Stellt einen Enumerator für Aufruflisteninformationen bereit, die in einem Ausnahmeobjekt eingebettet sind.</span><span class="sxs-lookup"><span data-stu-id="27cf9-103">Provides an enumerator for call stack information that is embedded in an exception object.</span></span> <span data-ttu-id="27cf9-104">Diese Schnittstelle ist eine Unterklasse von ICorDebugEnum-Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="27cf9-104">This interface is a subclass of the ICorDebugEnum interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="27cf9-105">Methoden</span><span class="sxs-lookup"><span data-stu-id="27cf9-105">Methods</span></span>  
  
|<span data-ttu-id="27cf9-106">Methode</span><span class="sxs-lookup"><span data-stu-id="27cf9-106">Method</span></span>|<span data-ttu-id="27cf9-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="27cf9-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="27cf9-108">Icordebugexceptionobjectcallstackenum:: Next</span><span class="sxs-lookup"><span data-stu-id="27cf9-108">ICorDebugExceptionObjectCallStackEnum::Next</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptionobjectcallstackenum-next-method.md)|<span data-ttu-id="27cf9-109">Ruft eine angegebene Anzahl von [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) Objekte, die Informationen zur Aufrufliste des Ausnahmeobjekts enthalten.</span><span class="sxs-lookup"><span data-stu-id="27cf9-109">Gets a specified number of [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) objects that contain information about an exception object's call stack.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="27cf9-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="27cf9-110">Remarks</span></span>  
 <span data-ttu-id="27cf9-111">Die `ICorDebugExceptionObjectCallStackEnum` Schnittstelle implementiert ICorDebugEnum-Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="27cf9-111">The `ICorDebugExceptionObjectCallStackEnum` interface implements the ICorDebugEnum interface.</span></span>  
  
 <span data-ttu-id="27cf9-112">Ein `ICorDebugExceptionObjectCallStackEnum` Instanz wird mit aufgefüllt [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) -Objektpaaren durch Aufrufen der [icordebugexceptionobjectvalue:: Enumerateexceptioncallstack](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptionobjectvalue-enumerateexceptioncallstack-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="27cf9-112">An `ICorDebugExceptionObjectCallStackEnum` instance is populated with [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) objects by calling the [ICorDebugExceptionObjectValue::EnumerateExceptionCallStack](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptionobjectvalue-enumerateexceptioncallstack-method.md) method.</span></span> <span data-ttu-id="27cf9-113">Der Aufruf Stapel Elemente in der Auflistung aufgelistet werden können, durch Aufrufen der [icordebugexceptionobjectcallstackenum:: Next](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptionobjectcallstackenum-next-method.md) Methode</span><span class="sxs-lookup"><span data-stu-id="27cf9-113">The call stack items in the collection can be enumerated by calling the [ICorDebugExceptionObjectCallStackEnum::Next](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptionobjectcallstackenum-next-method.md) method</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="27cf9-114">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="27cf9-114">Requirements</span></span>  
 <span data-ttu-id="27cf9-115">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="27cf9-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="27cf9-116">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="27cf9-116">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="27cf9-117">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="27cf9-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="27cf9-118">**.NET Framework-Versionen:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="27cf9-118">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="27cf9-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="27cf9-119">See Also</span></span>  
 [<span data-ttu-id="27cf9-120">Debugschnittstellen</span><span class="sxs-lookup"><span data-stu-id="27cf9-120">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="27cf9-121">Debuggen</span><span class="sxs-lookup"><span data-stu-id="27cf9-121">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)