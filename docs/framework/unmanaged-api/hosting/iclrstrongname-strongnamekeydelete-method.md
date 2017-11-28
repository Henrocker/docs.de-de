---
title: ICLRStrongName::StrongNameKeyDelete-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRStrongName.StrongNameKeyDelete
api_location: mscoree.dll
api_type: COM
f1_keywords: ICLRStrongName::StrongNameKeyDelete
helpviewer_keywords:
- StrongNameKeyDelete method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameKeyDelete method [.NET Framework hosting]
ms.assetid: 0163412f-f617-4428-89e0-03992fec31e8
topic_type: apiref
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 8fbb6af492007eb0dc2a9ea83c53e3559225428d
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="iclrstrongnamestrongnamekeydelete-method"></a><span data-ttu-id="6f8f7-102">ICLRStrongName::StrongNameKeyDelete-Methode</span><span class="sxs-lookup"><span data-stu-id="6f8f7-102">ICLRStrongName::StrongNameKeyDelete Method</span></span>
<span data-ttu-id="6f8f7-103">Löscht den angegebenen Schlüsselcontainer.</span><span class="sxs-lookup"><span data-stu-id="6f8f7-103">Deletes the specified key container.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6f8f7-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="6f8f7-104">Syntax</span></span>  
  
```  
HRESULT StrongNameKeyDelete (  
    [in]  LPCWSTR   wszKeyContainer  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="6f8f7-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="6f8f7-105">Parameters</span></span>  
 `wszKeyContainer`  
 <span data-ttu-id="6f8f7-106">[in] Der Name des Schlüsselcontainers zu löschen.</span><span class="sxs-lookup"><span data-stu-id="6f8f7-106">[in] The name of the key container to delete.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="6f8f7-107">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="6f8f7-107">Return Value</span></span>  
 <span data-ttu-id="6f8f7-108">`S_OK`Wenn die Methode erfolgreich abgeschlossen. andernfalls ein HRESULT-Wert, der Fehler weist darauf hin (finden Sie unter [häufig auftretende HRESULT-Werte](http://go.microsoft.com/fwlink/?LinkId=213878) eine Liste).</span><span class="sxs-lookup"><span data-stu-id="6f8f7-108">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](http://go.microsoft.com/fwlink/?LinkId=213878) for a list).</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="6f8f7-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="6f8f7-109">Remarks</span></span>  
 <span data-ttu-id="6f8f7-110">Verwenden der [ICLRStrongName:: StrongNameKeyInstall](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeyinstall-method.md) Methode, um ein öffentliches/privates Schlüsselpaar in einen Container zu importieren.</span><span class="sxs-lookup"><span data-stu-id="6f8f7-110">Use the [ICLRStrongName::StrongNameKeyInstall](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeyinstall-method.md) method to import a public/private key pair into a container.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6f8f7-111">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="6f8f7-111">Requirements</span></span>  
 <span data-ttu-id="6f8f7-112">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6f8f7-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6f8f7-113">**Header:** MetaHost.h</span><span class="sxs-lookup"><span data-stu-id="6f8f7-113">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="6f8f7-114">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="6f8f7-114">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="6f8f7-115">**.NET Framework-Versionen:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6f8f7-115">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6f8f7-116">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="6f8f7-116">See Also</span></span>  
 [<span data-ttu-id="6f8f7-117">StrongNameKeyInstall-Methode</span><span class="sxs-lookup"><span data-stu-id="6f8f7-117">StrongNameKeyInstall Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamekeyinstall-method.md)  
 [<span data-ttu-id="6f8f7-118">ICLRStrongName-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="6f8f7-118">ICLRStrongName Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)