---
title: IHostManualEvent::Set-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostManualEvent.Set
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostManualEvent::Set
helpviewer_keywords:
- Set method, IHostManualEvent interface [.NET Framework hosting]
- IHostManualEvent::Set method [.NET Framework hosting]
ms.assetid: e930c174-f71d-4faa-bb59-f0fb3df4d77b
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7f093e1278e74553ed78445e0cb83127a219e622
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="ihostmanualeventset-method"></a><span data-ttu-id="a3615-102">IHostManualEvent::Set-Methode</span><span class="sxs-lookup"><span data-stu-id="a3615-102">IHostManualEvent::Set Method</span></span>
<span data-ttu-id="a3615-103">Legt die aktuelle [IHostManualEvent](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-interface.md) Instanz zum Zustand "signalisiert".</span><span class="sxs-lookup"><span data-stu-id="a3615-103">Sets the current [IHostManualEvent](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-interface.md) instance to a signaled state.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="a3615-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="a3615-104">Syntax</span></span>  
  
```  
HRESULT Set ();  
```  
  
## <a name="return-value"></a><span data-ttu-id="a3615-105">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="a3615-105">Return Value</span></span>  
  
|<span data-ttu-id="a3615-106">HRESULT</span><span class="sxs-lookup"><span data-stu-id="a3615-106">HRESULT</span></span>|<span data-ttu-id="a3615-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a3615-107">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="a3615-108">S_OK</span><span class="sxs-lookup"><span data-stu-id="a3615-108">S_OK</span></span>|<span data-ttu-id="a3615-109">`Set`wurde erfolgreich zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="a3615-109">`Set` returned successfully.</span></span>|  
|<span data-ttu-id="a3615-110">HOST_E_CLRNOTAVAILABLE ZURÜCK</span><span class="sxs-lookup"><span data-stu-id="a3615-110">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="a3615-111">Die common Language Runtime (CLR) wurde nicht in einen Prozess geladen, oder die CLR wird in einem Zustand, in dem er nicht verwalteten Code ausführen oder den Aufruf erfolgreich verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="a3615-111">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="a3615-112">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="a3615-112">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="a3615-113">Der Aufruf ist ein Timeout aufgetreten.</span><span class="sxs-lookup"><span data-stu-id="a3615-113">The call timed out.</span></span>|  
|<span data-ttu-id="a3615-114">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="a3615-114">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="a3615-115">Der Aufrufer ist nicht Besitzer der Sperre.</span><span class="sxs-lookup"><span data-stu-id="a3615-115">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="a3615-116">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="a3615-116">HOST_E_ABANDONED</span></span>|<span data-ttu-id="a3615-117">Ein Ereignis wurde abgebrochen, während ein blockierten Thread oder eine Fiber darauf gewartet.</span><span class="sxs-lookup"><span data-stu-id="a3615-117">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="a3615-118">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="a3615-118">E_FAIL</span></span>|<span data-ttu-id="a3615-119">Ein Unbekannter Schwerwiegender Fehler aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="a3615-119">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="a3615-120">Wenn eine Methode E_FAIL zurückgibt, ist die CLR nicht mehr verwendbar innerhalb des Prozesses.</span><span class="sxs-lookup"><span data-stu-id="a3615-120">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="a3615-121">Nachfolgende Aufrufe zum Hosten der Methoden HOST_E_CLRNOTAVAILABLE zurück.</span><span class="sxs-lookup"><span data-stu-id="a3615-121">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="a3615-122">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="a3615-122">Requirements</span></span>  
 <span data-ttu-id="a3615-123">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="a3615-123">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="a3615-124">**Header:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="a3615-124">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="a3615-125">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="a3615-125">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="a3615-126">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a3615-126">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a3615-127">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a3615-127">See Also</span></span>  
 [<span data-ttu-id="a3615-128">ICLRSyncManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="a3615-128">ICLRSyncManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrsyncmanager-interface.md)  
 [<span data-ttu-id="a3615-129">IHostAutoEvent-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="a3615-129">IHostAutoEvent Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostautoevent-interface.md)  
 [<span data-ttu-id="a3615-130">IHostManualEvent-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="a3615-130">IHostManualEvent Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostmanualevent-interface.md)  
 [<span data-ttu-id="a3615-131">IHostSemaphore-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="a3615-131">IHostSemaphore Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsemaphore-interface.md)  
 [<span data-ttu-id="a3615-132">IHostSyncManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="a3615-132">IHostSyncManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsyncmanager-interface.md)