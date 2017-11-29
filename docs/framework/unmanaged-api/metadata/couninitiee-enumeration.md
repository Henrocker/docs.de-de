---
title: COUNINITIEE-Enumeration
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COUNINITIEE
api_location: mscoree.dll
api_type: COM
f1_keywords: COUNINITIEE
helpviewer_keywords: COUNINITIEE enumeration [.NET Framework metadata]
ms.assetid: c42baa79-f469-4330-95a2-baf7f021c2fc
topic_type: apiref
caps.latest.revision: "10"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: c849a32850b5fc9aaca7ea75fdfb30db3de5d8c9
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="couninitiee-enumeration"></a><span data-ttu-id="f1b57-102">COUNINITIEE-Enumeration</span><span class="sxs-lookup"><span data-stu-id="f1b57-102">COUNINITIEE Enumeration</span></span>
<span data-ttu-id="f1b57-103">Gibt Konstanten verwendet [CoUninitializeEE](../../../../docs/framework/unmanaged-api/hosting/couninitializeee-function.md) beim Initialisieren der common Language Runtime.</span><span class="sxs-lookup"><span data-stu-id="f1b57-103">Specifies constants used by [CoUninitializeEE](../../../../docs/framework/unmanaged-api/hosting/couninitializeee-function.md) when initializing the common language runtime.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f1b57-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="f1b57-104">Syntax</span></span>  
  
```  
typedef enum tagCOUNINITEE  
{  
    COUNINITEE_DEFAULT  = 0x0,   
    COUNINITEE_DLL      = 0x1  
} COUNINITIEE;  
```  
  
## <a name="members"></a><span data-ttu-id="f1b57-105">Member</span><span class="sxs-lookup"><span data-stu-id="f1b57-105">Members</span></span>  
  
|<span data-ttu-id="f1b57-106">Member</span><span class="sxs-lookup"><span data-stu-id="f1b57-106">Member</span></span>|<span data-ttu-id="f1b57-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="f1b57-107">Description</span></span>|  
|------------|-----------------|  
|`COUNINITEE_DEFAULT`|<span data-ttu-id="f1b57-108">Gibt an, zur Aufhebung der Standardmodus.</span><span class="sxs-lookup"><span data-stu-id="f1b57-108">Indicates default uninitialization mode.</span></span>|  
|`COUNINITEE_DLL`|<span data-ttu-id="f1b57-109">Gibt die zur Aufhebung der Modus zum Entladen einer Assemblys an.</span><span class="sxs-lookup"><span data-stu-id="f1b57-109">Indicates uninitialization mode for unloading an assembly.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="f1b57-110">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="f1b57-110">Requirements</span></span>  
 <span data-ttu-id="f1b57-111">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f1b57-111">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f1b57-112">**Header:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="f1b57-112">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="f1b57-113">**Bibliothek:** als Ressource in MsCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="f1b57-113">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="f1b57-114">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f1b57-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f1b57-115">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f1b57-115">See Also</span></span>  
 [<span data-ttu-id="f1b57-116">Metadatenenumerationen</span><span class="sxs-lookup"><span data-stu-id="f1b57-116">Metadata Enumerations</span></span>](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)