---
title: IMetaDataEmit::DefineTypeRefByName-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataEmit.DefineTypeRefByName
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataEmit::DefineTypeRefByName
helpviewer_keywords:
- DefineTypeRefByName method [.NET Framework metadata]
- IMetaDataEmit::DefineTypeRefByName method [.NET Framework metadata]
ms.assetid: c30a4ce3-2d3e-411a-98df-e62ac4a5dd50
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 9ce04733fa9f149f155d850c53b65b263943cf8b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="imetadataemitdefinetyperefbyname-method"></a><span data-ttu-id="f71bb-102">IMetaDataEmit::DefineTypeRefByName-Methode</span><span class="sxs-lookup"><span data-stu-id="f71bb-102">IMetaDataEmit::DefineTypeRefByName Method</span></span>
<span data-ttu-id="f71bb-103">Ruft ein Metadatentoken für einen Typ, der im angegebenen Bereich außerhalb des aktuellen Bereichs ist definiert.</span><span class="sxs-lookup"><span data-stu-id="f71bb-103">Gets a metadata token for a type that is defined in the specified scope, which is outside the current scope.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f71bb-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="f71bb-104">Syntax</span></span>  
  
```  
HRESULT DefineTypeRefByName (   
    [in]  mdToken     tkResolutionScope,   
    [in]  LPCWSTR     szName,   
    [out] mdTypeRef   *ptr   
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="f71bb-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="f71bb-105">Parameters</span></span>  
 `tkResolutionScope`  
 <span data-ttu-id="f71bb-106">[in] Das Token der Auflösungsbereich angeben.</span><span class="sxs-lookup"><span data-stu-id="f71bb-106">[in] The token specifying the resolution scope.</span></span> <span data-ttu-id="f71bb-107">Die folgenden Tokentypen sind gültig:</span><span class="sxs-lookup"><span data-stu-id="f71bb-107">The following token types are valid:</span></span>  
  
-   <span data-ttu-id="f71bb-108">`mdModuleRef`, wenn der Typ in der gleichen Assembly definiert ist, in dem der Aufrufer definiert wird.</span><span class="sxs-lookup"><span data-stu-id="f71bb-108">`mdModuleRef`, if the type is defined in the same assembly in which the caller is defined.</span></span>  
  
-   <span data-ttu-id="f71bb-109">`mdAssemblyRef`, wenn der Typ in einer anderen als der Assembly definiert ist, in dem der Aufrufer definiert wird.</span><span class="sxs-lookup"><span data-stu-id="f71bb-109">`mdAssemblyRef`, if the type is defined in an assembly other than the one in which the caller is defined.</span></span>  
  
-   <span data-ttu-id="f71bb-110">`mdTypeRef`, wenn der Typ ein geschachtelter Typ ist.</span><span class="sxs-lookup"><span data-stu-id="f71bb-110">`mdTypeRef`, if the type is a nested type.</span></span>  
  
-   <span data-ttu-id="f71bb-111">`mdModule`, wenn der Typ im selben Modul definiert ist, in dem der Aufrufer definiert wird.</span><span class="sxs-lookup"><span data-stu-id="f71bb-111">`mdModule`, if the type is defined in the same module in which the caller is defined.</span></span>  
  
-   <span data-ttu-id="f71bb-112">NULL, wenn der Typ global definiert ist.</span><span class="sxs-lookup"><span data-stu-id="f71bb-112">Null, if the type is defined globally.</span></span>  
  
 `szName`  
 <span data-ttu-id="f71bb-113">[in] Der Name des Zieltyps im Unicode-Format.</span><span class="sxs-lookup"><span data-stu-id="f71bb-113">[in] The name of the target type in Unicode.</span></span>  
  
 `ptr`  
 <span data-ttu-id="f71bb-114">[out] Ein Zeiger auf die `mdTypeRef` Token, das den Typ zugewiesen ist.</span><span class="sxs-lookup"><span data-stu-id="f71bb-114">[out] A pointer to the `mdTypeRef` token that is assigned to the type.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f71bb-115">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="f71bb-115">Requirements</span></span>  
 <span data-ttu-id="f71bb-116">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f71bb-116">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f71bb-117">**Header:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="f71bb-117">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="f71bb-118">**Bibliothek:** als Ressource in MSCorEE.dll verwendet</span><span class="sxs-lookup"><span data-stu-id="f71bb-118">**Library:** Used as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="f71bb-119">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f71bb-119">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f71bb-120">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f71bb-120">See Also</span></span>  
 [<span data-ttu-id="f71bb-121">IMetaDataEmit-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="f71bb-121">IMetaDataEmit Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)  
 [<span data-ttu-id="f71bb-122">IMetaDataEmit2-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="f71bb-122">IMetaDataEmit2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)