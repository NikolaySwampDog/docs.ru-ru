---
description: Дополнительные сведения о функции FunctionLeave3WithInfo
title: Функция FunctionLeave3WithInfo
ms.date: 03/30/2017
api_name:
- FunctionLeave3WithInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave3WithInfo
helpviewer_keywords:
- FunctionLeave3WithInfo function [.NET Framework profiling]
ms.assetid: 5fa68a67-ced6-41c6-a2c0-467060fd0692
topic_type:
- apiref
ms.openlocfilehash: 617ca023f58a180c198751fea9752fe737249331
ms.sourcegitcommit: 20b4565974d185c7716656a6c63e3cfdbdf4bf41
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104760084"
---
# <a name="functionleave3withinfo-function"></a><span data-ttu-id="14d03-103">Функция FunctionLeave3WithInfo</span><span class="sxs-lookup"><span data-stu-id="14d03-103">FunctionLeave3WithInfo Function</span></span>

<span data-ttu-id="14d03-104">Уведомляет профилировщик о том, что управление возвращается из функции, и предоставляет маркер, который может быть передан [методу ICorProfilerInfo3:: GetFunctionLeave3Info](icorprofilerinfo3-getfunctionleave3info-method.md) для получения кадра стека и возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="14d03-104">Notifies the profiler that control is being returned from a function, and provides a handle that can be passed to the [ICorProfilerInfo3::GetFunctionLeave3Info method](icorprofilerinfo3-getfunctionleave3info-method.md) to retrieve the stack frame and the return value.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="14d03-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="14d03-105">Syntax</span></span>  
  
```cpp  
void __stdcall FunctionLeave3WithInfo(  
               [in] FunctionIDOrClientID functionIDOrClientID,  
               [in] COR_PRF_ELT_INFO eltInfo);  
```  
  
## <a name="parameters"></a><span data-ttu-id="14d03-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="14d03-106">Parameters</span></span>

<span data-ttu-id="14d03-107">`functionIDOrClientID` окне Идентификатор функции, из которой возвращается элемент управления.</span><span class="sxs-lookup"><span data-stu-id="14d03-107">`functionIDOrClientID` [in] The identifier of the function from which control is returned.</span></span>

<span data-ttu-id="14d03-108">`eltInfo` окне Непрозрачный маркер, представляющий сведения об заданном кадре стека.</span><span class="sxs-lookup"><span data-stu-id="14d03-108">`eltInfo` [in] An opaque handle that represents information about a given stack frame.</span></span> <span data-ttu-id="14d03-109">Этот маркер действителен только во время обратного вызова, к которому он передается.</span><span class="sxs-lookup"><span data-stu-id="14d03-109">This handle is valid only during the callback to which it is passed.</span></span>

## <a name="remarks"></a><span data-ttu-id="14d03-110">Remarks</span><span class="sxs-lookup"><span data-stu-id="14d03-110">Remarks</span></span>  

 <span data-ttu-id="14d03-111">`FunctionLeave3WithInfo`Метод обратного вызова уведомляет профилировщик о вызове функций и позволяет профилировщику использовать [метод ICorProfilerInfo3:: GetFunctionLeave3Info](icorprofilerinfo3-getfunctionleave3info-method.md) для проверки возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="14d03-111">The `FunctionLeave3WithInfo` callback method notifies the profiler as functions are called, and allows the profiler to use the [ICorProfilerInfo3::GetFunctionLeave3Info method](icorprofilerinfo3-getfunctionleave3info-method.md) to inspect the return value.</span></span> <span data-ttu-id="14d03-112">Чтобы получить доступ к сведениям о возвращаемом значении, необходимо `COR_PRF_ENABLE_FUNCTION_RETVAL` установить флаг.</span><span class="sxs-lookup"><span data-stu-id="14d03-112">To access return value information, the `COR_PRF_ENABLE_FUNCTION_RETVAL` flag has to be set.</span></span> <span data-ttu-id="14d03-113">Профилировщик может использовать [метод ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md) для установки флагов событий, а затем использовать [метод ICorProfilerInfo3:: SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) для регистрации реализации этой функции.</span><span class="sxs-lookup"><span data-stu-id="14d03-113">The profiler can use the [ICorProfilerInfo::SetEventMask method](icorprofilerinfo-seteventmask-method.md) to set the event flags, and then use the [ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo method](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md) to register your implementation of this function.</span></span>  
  
 <span data-ttu-id="14d03-114">`FunctionLeave3WithInfo`Функция является обратным вызовом. ее необходимо реализовать.</span><span class="sxs-lookup"><span data-stu-id="14d03-114">The `FunctionLeave3WithInfo` function is a callback; you must implement it.</span></span> <span data-ttu-id="14d03-115">Реализация должна использовать `__declspec(naked)` атрибут класса хранения.</span><span class="sxs-lookup"><span data-stu-id="14d03-115">The implementation must use the `__declspec(naked)` storage-class attribute.</span></span>  
  
 <span data-ttu-id="14d03-116">Подсистема выполнения не сохраняет никакие регистры перед вызовом этой функции.</span><span class="sxs-lookup"><span data-stu-id="14d03-116">The execution engine does not save any registers before calling this function.</span></span>  
  
- <span data-ttu-id="14d03-117">Во время записи необходимо сохранить все используемые регистры, включая те, которые находятся в блоке с плавающей запятой (FPU).</span><span class="sxs-lookup"><span data-stu-id="14d03-117">On entry, you must save all registers that you use, including those in the floating-point unit (FPU).</span></span>  
  
- <span data-ttu-id="14d03-118">При выходе необходимо восстановить стек, выключив все параметры, которые были переданы его вызывающим.</span><span class="sxs-lookup"><span data-stu-id="14d03-118">On exit, you must restore the stack by popping off all the parameters that were pushed by its caller.</span></span>  
  
 <span data-ttu-id="14d03-119">Реализация `FunctionLeave3WithInfo` не должна блокироваться, так как она приведет к задержке сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="14d03-119">The implementation of `FunctionLeave3WithInfo` should not block, because it will delay garbage collection.</span></span> <span data-ttu-id="14d03-120">Реализация не должна пытаться выполнить сборку мусора, так как стек может не находиться в состоянии, удобном для сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="14d03-120">The implementation should not attempt a garbage collection, because the stack may not be in a garbage collection-friendly state.</span></span> <span data-ttu-id="14d03-121">Если выполняется сборка мусора, среда выполнения будет блокироваться до тех пор, пока не `FunctionLeave3WithInfo` вернет.</span><span class="sxs-lookup"><span data-stu-id="14d03-121">If a garbage collection is attempted, the runtime will block until `FunctionLeave3WithInfo` returns.</span></span>  
  
 <span data-ttu-id="14d03-122">`FunctionLeave3WithInfo`Функция не должна вызывать управляемый код или вызывать управляемое выделение памяти каким-либо образом.</span><span class="sxs-lookup"><span data-stu-id="14d03-122">The `FunctionLeave3WithInfo` function must not call into managed code or cause a managed memory allocation in any way.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="14d03-123">Требования</span><span class="sxs-lookup"><span data-stu-id="14d03-123">Requirements</span></span>  

 <span data-ttu-id="14d03-124">**Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="14d03-124">**Platforms:** See [System Requirements](../../get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="14d03-125">**Заголовок:** CorProf. idl</span><span class="sxs-lookup"><span data-stu-id="14d03-125">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="14d03-126">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="14d03-126">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="14d03-127">**Платформа .NET Framework версии:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="14d03-127">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="14d03-128">См. также раздел</span><span class="sxs-lookup"><span data-stu-id="14d03-128">See also</span></span>

- [<span data-ttu-id="14d03-129">GetFunctionLeave3Info</span><span class="sxs-lookup"><span data-stu-id="14d03-129">GetFunctionLeave3Info</span></span>](icorprofilerinfo3-getfunctionleave3info-method.md)
- [<span data-ttu-id="14d03-130">FunctionEnter3</span><span class="sxs-lookup"><span data-stu-id="14d03-130">FunctionEnter3</span></span>](functionenter3-function.md)
- [<span data-ttu-id="14d03-131">FunctionLeave3</span><span class="sxs-lookup"><span data-stu-id="14d03-131">FunctionLeave3</span></span>](functionleave3-function.md)
- [<span data-ttu-id="14d03-132">FunctionTailcall3</span><span class="sxs-lookup"><span data-stu-id="14d03-132">FunctionTailcall3</span></span>](functiontailcall3-function.md)
- [<span data-ttu-id="14d03-133">FunctionEnter3WithInfo</span><span class="sxs-lookup"><span data-stu-id="14d03-133">FunctionEnter3WithInfo</span></span>](functionenter3withinfo-function.md)
- [<span data-ttu-id="14d03-134">FunctionTailcall3WithInfo</span><span class="sxs-lookup"><span data-stu-id="14d03-134">FunctionTailcall3WithInfo</span></span>](functiontailcall3withinfo-function.md)
- [<span data-ttu-id="14d03-135">SetEnterLeaveFunctionHooks3</span><span class="sxs-lookup"><span data-stu-id="14d03-135">SetEnterLeaveFunctionHooks3</span></span>](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [<span data-ttu-id="14d03-136">SetEnterLeaveFunctionHooks3WithInfo</span><span class="sxs-lookup"><span data-stu-id="14d03-136">SetEnterLeaveFunctionHooks3WithInfo</span></span>](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [<span data-ttu-id="14d03-137">SetFunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="14d03-137">SetFunctionIDMapper</span></span>](icorprofilerinfo-setfunctionidmapper-method.md)
- [<span data-ttu-id="14d03-138">SetFunctionIDMapper2</span><span class="sxs-lookup"><span data-stu-id="14d03-138">SetFunctionIDMapper2</span></span>](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [<span data-ttu-id="14d03-139">Глобальные статические функции профилирования</span><span class="sxs-lookup"><span data-stu-id="14d03-139">Profiling Global Static Functions</span></span>](profiling-global-static-functions.md)
