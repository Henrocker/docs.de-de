---
title: ICorProfilerInfo2::GetFunctionInfo2-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo2.GetFunctionInfo2
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo2::GetFunctionInfo2
helpviewer_keywords:
- GetFunctionInfo2 method [.NET Framework profiling]
- ICorProfilerInfo2::GetFunctionInfo2 method [.NET Framework profiling]
ms.assetid: 0aa60f24-8bbd-4c83-83c5-86ad191b1d82
topic_type: apiref
caps.latest.revision: "18"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 8b0c288b88c868bc6e324ec57b3956344f03f34e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfo2getfunctioninfo2-method"></a><span data-ttu-id="2827d-102">ICorProfilerInfo2::GetFunctionInfo2-Methode</span><span class="sxs-lookup"><span data-stu-id="2827d-102">ICorProfilerInfo2::GetFunctionInfo2 Method</span></span>
<span data-ttu-id="2827d-103">Ruft die übergeordnete Klasse, das Metadatentoken und die `ClassID` jedes Typarguments einer Funktion ab, falls vorhanden.</span><span class="sxs-lookup"><span data-stu-id="2827d-103">Gets the parent class, the metadata token, and the `ClassID` of each type argument, if present, of a function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="2827d-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="2827d-104">Syntax</span></span>  
  
```  
HRESULT GetFunctionInfo2(  
    [in]  FunctionID funcId,  
    [in]  COR_PRF_FRAME_INFO frameInfo,  
    [out] ClassID *pClassId,  
    [out] ModuleID *pModuleId,  
    [out] mdToken *pToken,  
    [in]  ULONG32 cTypeArgs,  
    [out] ULONG32 *pcTypeArgs,  
    [out] ClassID typeArgs[]);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="2827d-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="2827d-105">Parameters</span></span>  
 `funcId`  
 <span data-ttu-id="2827d-106">[in] Die ID der Funktion, für die die übergeordnete Klasse und andere Informationen abgerufen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="2827d-106">[in] The ID of the function for which to get the parent class and other information.</span></span>  
  
 `frameInfo`  
 <span data-ttu-id="2827d-107">[in] Ein `COR_PRF_FRAME_INFO`-Wert, der auf Informationen zu einem Stapelrahmen verweist.</span><span class="sxs-lookup"><span data-stu-id="2827d-107">[in] A `COR_PRF_FRAME_INFO` value that points to information about a stack frame.</span></span>  
  
 `pClassId`  
 <span data-ttu-id="2827d-108">[out] Ein Zeiger auf die übergeordnete Klasse der Funktion.</span><span class="sxs-lookup"><span data-stu-id="2827d-108">[out] A pointer to the parent class of the function.</span></span>  
  
 `pModuleId`  
 <span data-ttu-id="2827d-109">[out] Ein Zeiger auf das Modul, in dem die übergeordnete Klasse der Funktion definiert ist.</span><span class="sxs-lookup"><span data-stu-id="2827d-109">[out] A pointer to the module in which the function's parent class is defined.</span></span>  
  
 `pToken`  
 <span data-ttu-id="2827d-110">[out] Ein Zeiger auf das Metadatentoken für die Funktion.</span><span class="sxs-lookup"><span data-stu-id="2827d-110">[out] A pointer to the metadata token for the function.</span></span>  
  
 `cTypeArgs`  
 <span data-ttu-id="2827d-111">[in] Die Größe des `typeArgs`-Arrays.</span><span class="sxs-lookup"><span data-stu-id="2827d-111">[in] The size of the `typeArgs` array.</span></span>  
  
 `pcTypeArgs`  
 <span data-ttu-id="2827d-112">[out] Ein Zeiger auf die Gesamtzahl der `ClassID`-Werte.</span><span class="sxs-lookup"><span data-stu-id="2827d-112">[out] A pointer to the total number of `ClassID` values.</span></span>  
  
 `typeArgs`  
 <span data-ttu-id="2827d-113">[out] Ein Array von `ClassID`-Werten, von denen jedes die ID eines Typarguments der Funktion darstellt.</span><span class="sxs-lookup"><span data-stu-id="2827d-113">[out] An array of `ClassID` values, each of which is the ID of a type argument of the function.</span></span> <span data-ttu-id="2827d-114">Nach Rückgabe der Methode enthält `typeArgs` einige oder alle der `ClassID`-Werte.</span><span class="sxs-lookup"><span data-stu-id="2827d-114">When the method returns, `typeArgs` will contain some or all of the `ClassID` values.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="2827d-115">Hinweise</span><span class="sxs-lookup"><span data-stu-id="2827d-115">Remarks</span></span>  
 <span data-ttu-id="2827d-116">Der Profilercode kann Aufrufen [ICorProfilerInfo:: GetModuleMetaData](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md) zum Abrufen einer [Metadaten](../../../../docs/framework/unmanaged-api/metadata/index.md) Schnittstelle für ein bestimmtes Modul.</span><span class="sxs-lookup"><span data-stu-id="2827d-116">The profiler code can call [ICorProfilerInfo::GetModuleMetaData](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md) to obtain a [metadata](../../../../docs/framework/unmanaged-api/metadata/index.md) interface for a given module.</span></span> <span data-ttu-id="2827d-117">Das Metadatentoken, das an den Speicherort zurückgegeben wird, auf den durch `pToken` verwiesen wird, kann anschließend für den Zugriff auf die Metadaten für die Funktion verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="2827d-117">The metadata token that is returned to the location referenced by `pToken` can then be used to access the metadata for the function.</span></span>  
  
 <span data-ttu-id="2827d-118">Die Klassen-ID und die Typargumente, die über die Parameter `pClassId` und `typeArgs` zurückgegeben werden, hängen vom im Parameter `frameInfo` übergebenen Wert ab (wie in der folgenden Tabelle gezeigt).</span><span class="sxs-lookup"><span data-stu-id="2827d-118">The class ID and type arguments that are returned through the `pClassId` and `typeArgs` parameters depend on the value that is passed in the `frameInfo` parameter, as shown in the following table.</span></span>  
  
|<span data-ttu-id="2827d-119">Der Wert des Parameters `frameInfo`.</span><span class="sxs-lookup"><span data-stu-id="2827d-119">Value of the `frameInfo` parameter</span></span>|<span data-ttu-id="2827d-120">Ergebnis</span><span class="sxs-lookup"><span data-stu-id="2827d-120">Result</span></span>|  
|----------------------------------------|------------|  
|<span data-ttu-id="2827d-121">Ein `COR_PRF_FRAME_INFO`-Wert, der von einem `FunctionEnter2`-Rückruf abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="2827d-121">A `COR_PRF_FRAME_INFO` value that was obtained from a `FunctionEnter2` callback</span></span>|<span data-ttu-id="2827d-122">Die `ClassID`, die an den Speicherort zurückgegeben wird, auf den `pClassId` verweist, sowie alle Typargumente, die im Array `typeArgs` zurückgegeben werden, sind genau.</span><span class="sxs-lookup"><span data-stu-id="2827d-122">The `ClassID`, returned in the location referenced by `pClassId`, and all type arguments, returned in the `typeArgs` array, will be exact.</span></span>|  
|<span data-ttu-id="2827d-123">Ein `COR_PRF_FRAME_INFO`-Objekt, das aus einer anderen Quelle als einem `FunctionEnter2`-Rückruf abgerufen wurde.</span><span class="sxs-lookup"><span data-stu-id="2827d-123">A `COR_PRF_FRAME_INFO` that was obtained from a source other than a `FunctionEnter2` callback</span></span>|<span data-ttu-id="2827d-124">Die genaue `ClassID` und Typargumente können nicht bestimmt werden.</span><span class="sxs-lookup"><span data-stu-id="2827d-124">The exact `ClassID` and type arguments cannot be determined.</span></span> <span data-ttu-id="2827d-125">Dies bedeutet ggf., dass `ClassID` NULL ist und einige Typargumente als <xref:System.Object> zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2827d-125">That is, the `ClassID` might be null and some type arguments might come back as <xref:System.Object>.</span></span>|  
|<span data-ttu-id="2827d-126">Zero</span><span class="sxs-lookup"><span data-stu-id="2827d-126">Zero</span></span>|<span data-ttu-id="2827d-127">Die genaue `ClassID` und Typargumente können nicht bestimmt werden.</span><span class="sxs-lookup"><span data-stu-id="2827d-127">The exact `ClassID` and type arguments cannot be determined.</span></span> <span data-ttu-id="2827d-128">Dies bedeutet ggf., dass `ClassID` NULL ist und einige Typargumente als <xref:System.Object> zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="2827d-128">That is, the `ClassID` might be null and some type arguments might come back as <xref:System.Object>.</span></span>|  
  
 <span data-ttu-id="2827d-129">Nachdem `GetFunctionInfo2` zurückgegeben wurde, müssen Sie sicherstellen, dass der `typeArgs`-Puffer groß genug war, um alle `ClassID`-Werte aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="2827d-129">After `GetFunctionInfo2` returns, you must verify that the `typeArgs` buffer was large enough to contain all the `ClassID` values.</span></span> <span data-ttu-id="2827d-130">Vergleichen Sie zu diesem Zweck den Wert, auf den `pcTypeArgs` verweist, mit dem Wert des Parameters `cTypeArgs`.</span><span class="sxs-lookup"><span data-stu-id="2827d-130">To do this, compare the value that `pcTypeArgs` points to with the value of the `cTypeArgs` parameter.</span></span> <span data-ttu-id="2827d-131">Wenn `pcTypeArgs` auf einen Wert verweist, der größer als `cTypeArgs` geteilt durch die Größe eines `ClassID`-Werts ist, weisen Sie einen größeren `pcTypeArgs`-Puffer zu, aktualisieren Sie `cTypeArgs` mit der neuen Größe, und rufen Sie dann `GetFunctionInfo2` erneut auf.</span><span class="sxs-lookup"><span data-stu-id="2827d-131">If `pcTypeArgs` points to a value that is larger than `cTypeArgs` divided by the size of a `ClassID` value, allocate a larger `pcTypeArgs` buffer, update `cTypeArgs` with the new, larger size, and call `GetFunctionInfo2` again.</span></span>  
  
 <span data-ttu-id="2827d-132">Alternativ können Sie zuerst `GetFunctionInfo2` mit einem `pcTypeArgs`-Puffer der Länge 0 (NULL) aufrufen, um die richtige Puffergröße zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="2827d-132">Alternatively, you can first call `GetFunctionInfo2` with a zero-length `pcTypeArgs` buffer to obtain the correct buffer size.</span></span> <span data-ttu-id="2827d-133">Sie können dann die Größe des Puffers auf den in `pcTypeArgs` zurückgegebenen Wert dividiert durch die Größe eines `ClassID`-Werts festlegen und `GetFunctionInfo2` erneut aufrufen.</span><span class="sxs-lookup"><span data-stu-id="2827d-133">You can then set the buffer size to the value returned in `pcTypeArgs` divided by the size of a `ClassID` value, and call `GetFunctionInfo2` again.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2827d-134">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="2827d-134">Requirements</span></span>  
 <span data-ttu-id="2827d-135">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2827d-135">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2827d-136">**Header:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="2827d-136">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="2827d-137">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="2827d-137">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="2827d-138">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2827d-138">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2827d-139">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2827d-139">See Also</span></span>  
 [<span data-ttu-id="2827d-140">ICorProfilerInfo-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="2827d-140">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [<span data-ttu-id="2827d-141">ICorProfilerInfo2-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="2827d-141">ICorProfilerInfo2 Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)  
 [<span data-ttu-id="2827d-142">Profilerstellungsschnittstellen</span><span class="sxs-lookup"><span data-stu-id="2827d-142">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [<span data-ttu-id="2827d-143">Profilerstellung</span><span class="sxs-lookup"><span data-stu-id="2827d-143">Profiling</span></span>](../../../../docs/framework/unmanaged-api/profiling/index.md)