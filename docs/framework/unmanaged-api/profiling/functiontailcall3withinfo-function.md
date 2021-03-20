---
description: Дополнительные сведения о функции FunctionTailcall3WithInfo
title: Функция FunctionTailcall3WithInfo
ms.date: 03/30/2017
api_name:
- FunctionTailcall3WithInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionTailcall3WithInfo
helpviewer_keywords:
- FunctionTailcall3WithInfo function [.NET Framework profiling]
ms.assetid: 46380fcc-0198-43ae-a1f5-2d4939425886
topic_type:
- apiref
ms.openlocfilehash: d84cac19acb8a1d696030fe372d29c655c5f97a6
ms.sourcegitcommit: 20b4565974d185c7716656a6c63e3cfdbdf4bf41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104760799"
---
# <a name="functiontailcall3withinfo-function"></a><span data-ttu-id="c615d-103">Функция FunctionTailcall3WithInfo</span><span class="sxs-lookup"><span data-stu-id="c615d-103">FunctionTailcall3WithInfo Function</span></span>

<span data-ttu-id="c615d-104">Уведомляет профилировщик о том, что выполняемая в данный момент функция собирается выполнить вызов другой функции с префиксом tail, и предоставляет маркер, который может быть передан [методу ICorProfilerInfo3:: GetFunctionTailcall3Info](icorprofilerinfo3-getfunctiontailcall3info-method.md) для получения кадра стека.</span><span class="sxs-lookup"><span data-stu-id="c615d-104">Notifies the profiler that the currently executing function is about to perform a tail call to another function, and provides a handle that can be passed to the [ICorProfilerInfo3::GetFunctionTailcall3Info method](icorprofilerinfo3-getfunctiontailcall3info-method.md) to retrieve the stack frame.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c615d-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="c615d-105">Syntax</span></span>  
  
```cpp  
void __stdcall FunctionTailcall3WithInfo(  
               [in] FunctionIDOrClientID functionIDOrClientID,  
               [in] COR_PRF_ELT_INFO eltInfo);  
```  
  
## <a name="parameters"></a><span data-ttu-id="c615d-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="c615d-106">Parameters</span></span>  

<span data-ttu-id="c615d-107">`functionIDOrClientID` окне Идентификатор выполняемой в данный момент функции, которая собирается выполнить вызов с префиксом tail.</span><span class="sxs-lookup"><span data-stu-id="c615d-107">`functionIDOrClientID` [in] The identifier of the currently executing function that is about to make a tail call.</span></span>

<span data-ttu-id="c615d-108">`eltInfo` окне Непрозрачный маркер, представляющий сведения об заданном кадре стека.</span><span class="sxs-lookup"><span data-stu-id="c615d-108">`eltInfo` [in] An opaque handle that represents information about a given stack frame.</span></span> <span data-ttu-id="c615d-109">Этот маркер действителен только во время обратного вызова, к которому он передается.</span><span class="sxs-lookup"><span data-stu-id="c615d-109">This handle is valid only during the callback to which it is passed.</span></span>

## <a name="remarks"></a><span data-ttu-id="c615d-110">Remarks</span><span class="sxs-lookup"><span data-stu-id="c615d-110">Remarks</span></span>  

 <span data-ttu-id="c615d-111">`FunctionTailcall3WithInfo`Метод обратного вызова уведомляет профилировщик о вызове функций и позволяет профилировщику использовать [метод ICorProfilerInfo3:: GetFunctionTailcall3Info](icorprofilerinfo3-getfunctiontailcall3info-method.md) для проверки кадра стека.</span><span class="sxs-lookup"><span data-stu-id="c615d-111">The `FunctionTailcall3WithInfo` callback method notifies the profiler as functions are called, and allows the profiler to use the [ICorProfilerInfo3::GetFunctionTailcall3Info method](icorprofilerinfo3-getfunctiontailcall3info-method.md) to inspect the stack frame.</span></span> <span data-ttu-id="c615d-112">Чтобы получить доступ к сведениям о кадрах стека, необходимо `COR_PRF_ENABLE_FRAME_INFO` установить флаг.</span><span class="sxs-lookup"><span data-stu-id="c615d-112">To access stack frame information, the `COR_PRF_ENABLE_FRAME_INFO` flag has to be set.</span></span> <span data-ttu-id="c615d-113">Профилировщик может использовать [метод ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md) для установки флагов событий, а затем использовать [метод ICorProfilerInfo3:: SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) для регистрации реализации этой функции.</span><span class="sxs-lookup"><span data-stu-id="c615d-113">The profiler can use the [ICorProfilerInfo::SetEventMask method](icorprofilerinfo-seteventmask-method.md) to set the event flags, and then use the [ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo method](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) to register your implementation of this function.</span></span>  
  
 <span data-ttu-id="c615d-114">`FunctionTailcall3WithInfo`Функция является обратным вызовом. ее необходимо реализовать.</span><span class="sxs-lookup"><span data-stu-id="c615d-114">The `FunctionTailcall3WithInfo` function is a callback; you must implement it.</span></span> <span data-ttu-id="c615d-115">Реализация должна использовать `__declspec(naked)` атрибут класса хранения.</span><span class="sxs-lookup"><span data-stu-id="c615d-115">The implementation must use the `__declspec(naked)` storage-class attribute.</span></span>  
  
 <span data-ttu-id="c615d-116">Подсистема выполнения не сохраняет никакие регистры перед вызовом этой функции.</span><span class="sxs-lookup"><span data-stu-id="c615d-116">The execution engine does not save any registers before calling this function.</span></span>  
  
- <span data-ttu-id="c615d-117">Во время записи необходимо сохранить все используемые регистры, включая те, которые находятся в блоке с плавающей запятой (FPU).</span><span class="sxs-lookup"><span data-stu-id="c615d-117">On entry, you must save all registers that you use, including those in the floating-point unit (FPU).</span></span>  
  
- <span data-ttu-id="c615d-118">При выходе необходимо восстановить стек, выключив все параметры, которые были переданы его вызывающим.</span><span class="sxs-lookup"><span data-stu-id="c615d-118">On exit, you must restore the stack by popping off all the parameters that were pushed by its caller.</span></span>  
  
 <span data-ttu-id="c615d-119">Реализация `FunctionTailcall3WithInfo` не должна блокироваться, так как она приведет к задержке сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="c615d-119">The implementation of `FunctionTailcall3WithInfo` should not block, because it will delay garbage collection.</span></span> <span data-ttu-id="c615d-120">Реализация не должна пытаться выполнить сборку мусора, так как стек может не находиться в состоянии, удобном для сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="c615d-120">The implementation should not attempt a garbage collection, because the stack may not be in a garbage collection-friendly state.</span></span> <span data-ttu-id="c615d-121">Если выполняется сборка мусора, среда выполнения будет блокироваться до тех пор, пока не `FunctionTailcall3WithInfo` вернет.</span><span class="sxs-lookup"><span data-stu-id="c615d-121">If a garbage collection is attempted, the runtime will block until `FunctionTailcall3WithInfo` returns.</span></span>  
  
 <span data-ttu-id="c615d-122">Кроме того, функция FunctionTailcall3WithInfo не должна вызывать управляемый код или каким-либо образом вызывать управляемое выделение памяти.</span><span class="sxs-lookup"><span data-stu-id="c615d-122">Also, the FunctionTailcall3WithInfo function must not call into managed code or cause a managed memory allocation in any way.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c615d-123">Требования</span><span class="sxs-lookup"><span data-stu-id="c615d-123">Requirements</span></span>  

 <span data-ttu-id="c615d-124">**Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c615d-124">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c615d-125">**Заголовок:** CorProf. idl</span><span class="sxs-lookup"><span data-stu-id="c615d-125">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="c615d-126">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c615d-126">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c615d-127">**Платформа .NET Framework версии:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c615d-127">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c615d-128">См. также раздел</span><span class="sxs-lookup"><span data-stu-id="c615d-128">See also</span></span>

- [<span data-ttu-id="c615d-129">FunctionEnter3</span><span class="sxs-lookup"><span data-stu-id="c615d-129">FunctionEnter3</span></span>](functionenter3-function.md)
- [<span data-ttu-id="c615d-130">FunctionLeave3</span><span class="sxs-lookup"><span data-stu-id="c615d-130">FunctionLeave3</span></span>](functionleave3-function.md)
- [<span data-ttu-id="c615d-131">FunctionTailcall3</span><span class="sxs-lookup"><span data-stu-id="c615d-131">FunctionTailcall3</span></span>](functiontailcall3-function.md)
- [<span data-ttu-id="c615d-132">FunctionEnter3WithInfo</span><span class="sxs-lookup"><span data-stu-id="c615d-132">FunctionEnter3WithInfo</span></span>](functiontailcall3-function.md)
- [<span data-ttu-id="c615d-133">FunctionLeave3WithInfo</span><span class="sxs-lookup"><span data-stu-id="c615d-133">FunctionLeave3WithInfo</span></span>](functionleave3withinfo-function.md)
- [<span data-ttu-id="c615d-134">SetEnterLeaveFunctionHooks3</span><span class="sxs-lookup"><span data-stu-id="c615d-134">SetEnterLeaveFunctionHooks3</span></span>](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [<span data-ttu-id="c615d-135">SetEnterLeaveFunctionHooks3WithInfo</span><span class="sxs-lookup"><span data-stu-id="c615d-135">SetEnterLeaveFunctionHooks3WithInfo</span></span>](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [<span data-ttu-id="c615d-136">SetFunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="c615d-136">SetFunctionIDMapper</span></span>](icorprofilerinfo-setfunctionidmapper-method.md)
- [<span data-ttu-id="c615d-137">SetFunctionIDMapper2</span><span class="sxs-lookup"><span data-stu-id="c615d-137">SetFunctionIDMapper2</span></span>](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [<span data-ttu-id="c615d-138">Глобальные статические функции профилирования</span><span class="sxs-lookup"><span data-stu-id="c615d-138">Profiling Global Static Functions</span></span>](profiling-global-static-functions.md)
