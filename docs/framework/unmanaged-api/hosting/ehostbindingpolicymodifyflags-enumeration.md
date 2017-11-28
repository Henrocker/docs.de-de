---
title: EHostBindingPolicyModifyFlags-Enumeration
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: EHostBindingPolicyModifyFlags
api_location: mscoree.dll
api_type: COM
f1_keywords: EHostBindingPolicyModifyFlags
helpviewer_keywords: EHostBindingPolicyModifyFlags enumeration [.NET Framework hosting]
ms.assetid: 0339af16-ee1d-48ec-837d-a79d9a9c89f8
topic_type: apiref
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 42ff7ec7487be649e353b48e537cf1d8d45f6962
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="ehostbindingpolicymodifyflags-enumeration"></a><span data-ttu-id="eb8b5-102">EHostBindingPolicyModifyFlags-Enumeration</span><span class="sxs-lookup"><span data-stu-id="eb8b5-102">EHostBindingPolicyModifyFlags Enumeration</span></span>
<span data-ttu-id="eb8b5-103">Ermöglicht es dem Host um den Typ der Umleitung anzugeben, die die common Language Runtime (CLR) beim Anwenden der Richtlinie Änderungen aus einer Assembly der Ereignisquelle an eine Zielassembly durchführen sollten.</span><span class="sxs-lookup"><span data-stu-id="eb8b5-103">Allows the host to specify the type of redirection the common language runtime (CLR) should perform when applying policy modifications from a source assembly to a target assembly.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="eb8b5-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="eb8b5-104">Syntax</span></span>  
  
```  
typedef enum _hostBindingPolicyModifyFlags {  
    HOST_BINDING_POLICY_MODIFY_DEFAULT  = 0,  
    HOST_BINDING_POLICY_MODIFY_CHAIN    = 1,  
    HOST_BINDING_POLICY_MODIFY_REMOVE   = 2,  
    HOST_BINDING_POLICY_MODIFY_MAX      = 3  
} EHostBindingPolicyModifyFlags;  
```  
  
## <a name="members"></a><span data-ttu-id="eb8b5-105">Member</span><span class="sxs-lookup"><span data-stu-id="eb8b5-105">Members</span></span>  
  
|<span data-ttu-id="eb8b5-106">Member</span><span class="sxs-lookup"><span data-stu-id="eb8b5-106">Member</span></span>|<span data-ttu-id="eb8b5-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="eb8b5-107">Description</span></span>|  
|------------|-----------------|  
|`HOST_BINDING_POLICY_MODIFY_CHAIN`|<span data-ttu-id="eb8b5-108">Gibt an, dass die CLR Richtlinienwerte der Quellassembly mit denen der Zielassembly verkettet wird.</span><span class="sxs-lookup"><span data-stu-id="eb8b5-108">Specifies that the CLR will chain policy values of the source assembly onto those of the target assembly.</span></span>|  
|`HOST_BINDING_POLICY_MODIFY_DEFAULT`|<span data-ttu-id="eb8b5-109">Gibt an, dass die CLR die Standardaktion ausführt.</span><span class="sxs-lookup"><span data-stu-id="eb8b5-109">Specifies that the CLR will perform the default action.</span></span>|  
|`HOST_BINDING_POLICY_MODIFY_MAX`|<span data-ttu-id="eb8b5-110">Gibt an, dass die CLR die Richtlinienwerte der Zielassembly auf die maximalen Werte festgelegt werden.</span><span class="sxs-lookup"><span data-stu-id="eb8b5-110">Specifies that the CLR will set the policy values of the target assembly to the maximum values.</span></span>|  
|`HOST_BINDING_POLICY_MODIFY_REMOVE`|<span data-ttu-id="eb8b5-111">Gibt an, dass die CLR Richtlinienwerte der Zielassembly mit denen die Assembly der Ereignisquelle ersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="eb8b5-111">Specifies that the CLR will replace policy values of the target assembly with those of the source assembly.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="eb8b5-112">Hinweise</span><span class="sxs-lookup"><span data-stu-id="eb8b5-112">Remarks</span></span>  
 <span data-ttu-id="eb8b5-113">Die [ICLRHostBindingPolicyManager:: ModifyApplicationPolicy](../../../../docs/framework/unmanaged-api/hosting/iclrhostbindingpolicymanager-modifyapplicationpolicy-method.md) Methode nimmt einen Parameter vom Typ `EHostBindingPolicyModifyFlags`.</span><span class="sxs-lookup"><span data-stu-id="eb8b5-113">The [ICLRHostBindingPolicyManager::ModifyApplicationPolicy](../../../../docs/framework/unmanaged-api/hosting/iclrhostbindingpolicymanager-modifyapplicationpolicy-method.md) method takes a parameter of type `EHostBindingPolicyModifyFlags`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="eb8b5-114">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="eb8b5-114">Requirements</span></span>  
 <span data-ttu-id="eb8b5-115">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="eb8b5-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="eb8b5-116">**Header:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="eb8b5-116">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="eb8b5-117">**Bibliothek:** "Mscoree.dll"</span><span class="sxs-lookup"><span data-stu-id="eb8b5-117">**Library:** MSCorEE.dll</span></span>  
  
 <span data-ttu-id="eb8b5-118">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="eb8b5-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="eb8b5-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="eb8b5-119">See Also</span></span>  
 [<span data-ttu-id="eb8b5-120">ICLRHostBindingPolicyManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="eb8b5-120">ICLRHostBindingPolicyManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrhostbindingpolicymanager-interface.md)  
 [<span data-ttu-id="eb8b5-121">Hosten von Enumerationen</span><span class="sxs-lookup"><span data-stu-id="eb8b5-121">Hosting Enumerations</span></span>](../../../../docs/framework/unmanaged-api/hosting/hosting-enumerations.md)