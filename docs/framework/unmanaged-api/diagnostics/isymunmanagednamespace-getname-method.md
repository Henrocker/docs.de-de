---
title: ISymUnmanagedNamespace::GetName-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedNamespace.GetName
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedNamespace::GetName
helpviewer_keywords:
- ISymUnmanagedNamespace::GetName method [.NET Framework debugging]
- GetName method, ISymUnmanagedNamespace interface [.NET Framework debugging]
ms.assetid: 657bf91d-005a-4ea4-9298-04d1291c0bc3
topic_type: apiref
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: abb21c7d5f239b19396d3182b97d9502cfa3da15
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanagednamespacegetname-method"></a><span data-ttu-id="4046b-102">ISymUnmanagedNamespace::GetName-Methode</span><span class="sxs-lookup"><span data-stu-id="4046b-102">ISymUnmanagedNamespace::GetName Method</span></span>
<span data-ttu-id="4046b-103">Ruft den Namen dieses Namespaces ab.</span><span class="sxs-lookup"><span data-stu-id="4046b-103">Gets the name of this namespace.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4046b-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="4046b-104">Syntax</span></span>  
  
```  
HRESULT GetName(  
    [in]  ULONG32  cchName,  
    [out] ULONG32  *pcchName,  
    [out, size_is(cchName),  
        length_is(*pcchName)] WCHAR szName[]);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="4046b-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="4046b-105">Parameters</span></span>  
 `cchName`  
 <span data-ttu-id="4046b-106">[in] Ein `ULONG32` , der angibt, dass der Größe des der `szName` Puffer.</span><span class="sxs-lookup"><span data-stu-id="4046b-106">[in] A `ULONG32` that indicates the size of the `szName` buffer.</span></span>  
  
 `pcchName`  
 <span data-ttu-id="4046b-107">[out] Ein Zeiger auf eine `ULONG32` , empfängt die Größe des für den Namespacenamen, einschließlich der null-Terminierung enthalten die erforderlichen Puffers in Zeichen.</span><span class="sxs-lookup"><span data-stu-id="4046b-107">[out] A pointer to a `ULONG32` that receives the size, in characters, of the buffer required to contain the namespace name, including the null termination.</span></span>  
  
 `szName`  
 <span data-ttu-id="4046b-108">[out] Ein Zeiger auf einen Puffer, der Name des Namespaces enthält.</span><span class="sxs-lookup"><span data-stu-id="4046b-108">[out] A pointer to a buffer that contains the namespace name.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="4046b-109">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="4046b-109">Return Value</span></span>  
 <span data-ttu-id="4046b-110">S_OK, wenn die Methode erfolgreich ist; andernfalls E_FAIL oder einen anderen Fehlercode.</span><span class="sxs-lookup"><span data-stu-id="4046b-110">S_OK if the method succeeds; otherwise, E_FAIL or some other error code.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4046b-111">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="4046b-111">Requirements</span></span>  
 <span data-ttu-id="4046b-112">**Header:** CorSym.idl, CorSym.h</span><span class="sxs-lookup"><span data-stu-id="4046b-112">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4046b-113">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="4046b-113">See Also</span></span>  
 [<span data-ttu-id="4046b-114">ISymUnmanagedNamespace-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="4046b-114">ISymUnmanagedNamespace Interface</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagednamespace-interface.md)