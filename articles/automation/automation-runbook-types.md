---
title: "自動化 Runbook 類型 aaaAzure |Microsoft 文件"
description: "描述 hello 不同類型的 runbook，您可以使用 Azure 自動化，您應該考慮判斷哪些類型 toouse 時的考量中。 "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a><span data-ttu-id="fd270-103">Azure 自動化 Runbook 類型</span><span class="sxs-lookup"><span data-stu-id="fd270-103">Azure Automation runbook types</span></span>
<span data-ttu-id="fd270-104">Azure 自動化 hello 下表中支援四種類型的簡短描述的 runbook。</span><span class="sxs-lookup"><span data-stu-id="fd270-104">Azure Automation supports four types of runbooks that are  briefly described in hello following table.</span></span>  <span data-ttu-id="fd270-105">hello 以下各節提供每個型別，包括時的考量的進一步資訊每個 toouse。</span><span class="sxs-lookup"><span data-stu-id="fd270-105">hello sections below provide further information about each type including considerations on when toouse each.</span></span>

| <span data-ttu-id="fd270-106">類型</span><span class="sxs-lookup"><span data-stu-id="fd270-106">Type</span></span> | <span data-ttu-id="fd270-107">說明</span><span class="sxs-lookup"><span data-stu-id="fd270-107">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="fd270-108">圖形化</span><span class="sxs-lookup"><span data-stu-id="fd270-108">Graphical</span></span>](#graphical-runbooks) |<span data-ttu-id="fd270-109">以 Windows PowerShell 為基礎，而且完全在 Azure 入口網站的圖形化編輯器中建立和編輯。</span><span class="sxs-lookup"><span data-stu-id="fd270-109">Based on Windows PowerShell and created and edited completely in graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="fd270-110">圖形化 PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="fd270-110">Graphical PowerShell Workflow</span></span>](#graphical-runbooks) |<span data-ttu-id="fd270-111">根據 Windows PowerShell 工作流程和 Azure 入口網站中的建立及編輯完全在 hello 圖形化編輯器。</span><span class="sxs-lookup"><span data-stu-id="fd270-111">Based on Windows PowerShell Workflow and created and edited completely in hello graphical editor in Azure portal.</span></span> |
| [<span data-ttu-id="fd270-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd270-112">PowerShell</span></span>](#powershell-runbooks) |<span data-ttu-id="fd270-113">以 Windows PowerShell 指令碼為基礎的文字 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fd270-113">Text runbook based on Windows PowerShell script.</span></span> |
| [<span data-ttu-id="fd270-114">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="fd270-114">PowerShell Workflow</span></span>](#powershell-workflow-runbooks) |<span data-ttu-id="fd270-115">以 Windows PowerShell 工作流程為基礎的文字 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fd270-115">Text runbook based on Windows PowerShell Workflow.</span></span> |

## <a name="graphical-runbooks"></a><span data-ttu-id="fd270-116">圖形化 Runbook</span><span class="sxs-lookup"><span data-stu-id="fd270-116">Graphical runbooks</span></span>
<span data-ttu-id="fd270-117">[圖形化](automation-runbook-types.md#graphical-runbooks)及圖形化 PowerShell 工作流程 runbook 建立和編輯與 hello hello Azure 入口網站中的圖形化編輯器。</span><span class="sxs-lookup"><span data-stu-id="fd270-117">[Graphical](automation-runbook-types.md#graphical-runbooks) and Graphical PowerShell Workflow runbooks are created and edited with hello graphical editor in hello Azure portal.</span></span>  <span data-ttu-id="fd270-118">您可以將它們匯出 tooa 檔案，然後匯入另一個自動化帳戶，但您無法建立或編輯這些其他工具。</span><span class="sxs-lookup"><span data-stu-id="fd270-118">You can export them tooa file and then import them into another automation account, but you cannot create or edit them with another tool.</span></span>  <span data-ttu-id="fd270-119">圖形化 runbook 產生 PowerShell 程式碼，但您無法直接檢視或修改 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd270-119">Graphical runbooks generate PowerShell code, but you can't directly view or modify hello code.</span></span> <span data-ttu-id="fd270-120">圖形化 runbook 不能轉換的 hello tooone[文字格式](automation-runbook-types.md)，也不可以是轉換的 toographical 格式文字 runbook。</span><span class="sxs-lookup"><span data-stu-id="fd270-120">Graphical runbooks cannot be converted tooone of hello [text formats](automation-runbook-types.md), nor can a text runbook be converted toographical format.</span></span> <span data-ttu-id="fd270-121">圖形化 runbook 可以轉換的 tooGraphical PowerShell 工作流程 runbook 在匯入，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="fd270-121">Graphical runbooks can be converted tooGraphical PowerShell Workflow runbooks during import and vice-versa.</span></span>

### <a name="advantages"></a><span data-ttu-id="fd270-122">優點</span><span class="sxs-lookup"><span data-stu-id="fd270-122">Advantages</span></span>
* <span data-ttu-id="fd270-123">虛擬插入連結設定撰寫模型</span><span class="sxs-lookup"><span data-stu-id="fd270-123">Visual insert-link-configure authoring model</span></span>  
* <span data-ttu-id="fd270-124">專注於資料如何流經 hello 程序</span><span class="sxs-lookup"><span data-stu-id="fd270-124">Focus on how data flows through hello process</span></span>  
* <span data-ttu-id="fd270-125">以視覺方式呈現管理程序</span><span class="sxs-lookup"><span data-stu-id="fd270-125">Visually represent management processes</span></span>  
* <span data-ttu-id="fd270-126">子 runbook toocreate 高等級的工作流程中包含其他 runbook</span><span class="sxs-lookup"><span data-stu-id="fd270-126">Include other runbooks as child runbooks toocreate high level workflows</span></span>  
* <span data-ttu-id="fd270-127">建議您採用模組化的程式設計</span><span class="sxs-lookup"><span data-stu-id="fd270-127">Encourages modular programming</span></span>  


### <a name="limitations"></a><span data-ttu-id="fd270-128">限制</span><span class="sxs-lookup"><span data-stu-id="fd270-128">Limitations</span></span>
* <span data-ttu-id="fd270-129">無法在 Azure 入口網站之外編輯 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fd270-129">Can't edit runbook outside of Azure portal.</span></span>
* <span data-ttu-id="fd270-130">可能需要包含 PowerShell 程式碼 tooperform 複雜邏輯的程式碼活動。</span><span class="sxs-lookup"><span data-stu-id="fd270-130">May require a Code activity containing PowerShell code tooperform complex logic.</span></span>
* <span data-ttu-id="fd270-131">無法檢視或直接編輯 hello PowerShell 程式碼所建立的 hello 圖形化工作流程。</span><span class="sxs-lookup"><span data-stu-id="fd270-131">Can't view or directly edit hello PowerShell code that is created by hello graphical workflow.</span></span> <span data-ttu-id="fd270-132">請注意，您可以檢視您在任何程式碼活動中建立的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd270-132">Note that you can view hello code you create in any Code activities.</span></span>

## <a name="powershell-runbooks"></a><span data-ttu-id="fd270-133">PowerShell Runbook</span><span class="sxs-lookup"><span data-stu-id="fd270-133">PowerShell runbooks</span></span>
<span data-ttu-id="fd270-134">PowerShell Runbook 以 Windows PowerShell 為基礎。</span><span class="sxs-lookup"><span data-stu-id="fd270-134">PowerShell runbooks are based on Windows PowerShell.</span></span>  <span data-ttu-id="fd270-135">您直接編輯 hello 的 hello runbook 使用 hello Azure 入口網站中的 hello 文字編輯器的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd270-135">You directly edit hello code of hello runbook using hello text editor in hello Azure portal.</span></span>  <span data-ttu-id="fd270-136">您也可以使用任何離線的文字編輯器和[匯入 hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx)至 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="fd270-136">You can also use any offline text editor and [import hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="fd270-137">優點</span><span class="sxs-lookup"><span data-stu-id="fd270-137">Advantages</span></span>
* <span data-ttu-id="fd270-138">實作所有的複雜邏輯與 hello 額外複雜的 PowerShell 工作流程沒有 PowerShell 程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd270-138">Implement all complex logic with PowerShell code without hello additional complexities of PowerShell Workflow.</span></span> 
* <span data-ttu-id="fd270-139">Runbook 便會啟動 PowerShell 工作流程 runbook 速度，因為它不需要再執行編譯 toobe。</span><span class="sxs-lookup"><span data-stu-id="fd270-139">Runbook starts faster than PowerShell Workflow runbooks since it doesn't need toobe compiled before running.</span></span>

### <a name="limitations"></a><span data-ttu-id="fd270-140">限制</span><span class="sxs-lookup"><span data-stu-id="fd270-140">Limitations</span></span>
* <span data-ttu-id="fd270-141">必須熟悉 PowerShell 指令碼處理。</span><span class="sxs-lookup"><span data-stu-id="fd270-141">Must be familiar with PowerShell scripting.</span></span>
* <span data-ttu-id="fd270-142">無法使用[平行處理](automation-powershell-workflow.md#parallel-processing)tooperform 多個平行的動作。</span><span class="sxs-lookup"><span data-stu-id="fd270-142">Can't use [parallel processing](automation-powershell-workflow.md#parallel-processing) tooperform multiple actions in parallel.</span></span>
* <span data-ttu-id="fd270-143">無法使用[檢查點](automation-powershell-workflow.md#checkpoints)tooresume runbook，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd270-143">Can't use [checkpoints](automation-powershell-workflow.md#checkpoints) tooresume runbook in case of error.</span></span>
* <span data-ttu-id="fd270-144">PowerShell 工作流程 runbook 和圖形化 runbook 只能包含以子 runbook 使用 hello Start-azureautomationrunbook cmdlet，此 cmdlet 會建立新的工作。</span><span class="sxs-lookup"><span data-stu-id="fd270-144">PowerShell Workflow runbooks and Graphical runbooks can only be included as child runbooks by using hello Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

### <a name="known-issues"></a><span data-ttu-id="fd270-145">已知問題</span><span class="sxs-lookup"><span data-stu-id="fd270-145">Known Issues</span></span>
<span data-ttu-id="fd270-146">以下是 PowerShell Runbook 目前已知的問題。</span><span class="sxs-lookup"><span data-stu-id="fd270-146">Following are current known issues with PowerShell runbooks.</span></span>

* <span data-ttu-id="fd270-147">PowerShell Runbook 無法擷取具有 Null 值的未加密 [變數資產](automation-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="fd270-147">PowerShell runbooks cannot cannot retrieve an unencrypted [variable asset](automation-variables.md) with a null value.</span></span>
* <span data-ttu-id="fd270-148">無法擷取 PowerShell runbook[變數資產](automation-variables.md)與 *~*  hello 名稱中。</span><span class="sxs-lookup"><span data-stu-id="fd270-148">PowerShell runbooks cannot retrieve a [variable asset](automation-variables.md) with *~* in hello name.</span></span>
* <span data-ttu-id="fd270-149">PowerShell Runbook 中落入迴圈的 Get-Process 大約在 80 次反覆運算之後就會損毀。</span><span class="sxs-lookup"><span data-stu-id="fd270-149">Get-Process in a loop in a PowerShell runbook may crash after about 80 iterations.</span></span> 
* <span data-ttu-id="fd270-150">如果它一次嘗試 toowrite 資料 toohello 輸出資料流的數量極大，PowerShell runbook 可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="fd270-150">A PowerShell runbook may fail if it attempts toowrite a very large amount of data toohello output stream at once.</span></span>   <span data-ttu-id="fd270-151">您通常可以解決這個問題，藉由輸出只會 hello 使用大型物件時所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="fd270-151">You can typically work around this issue by outputting just hello information you need when working with large objects.</span></span>  <span data-ttu-id="fd270-152">例如，而不是輸出類似*Get-process*，您可以將輸出只具有所需的 hello 欄位*Get-process |選取 ProcessName，CPU*。</span><span class="sxs-lookup"><span data-stu-id="fd270-152">For example, instead of outputting something like *Get-Process*, you can output just hello required fields with *Get-Process | Select ProcessName, CPU*.</span></span>

## <a name="powershell-workflow-runbooks"></a><span data-ttu-id="fd270-153">PowerShell 工作流程 Runbook</span><span class="sxs-lookup"><span data-stu-id="fd270-153">PowerShell Workflow runbooks</span></span>
<span data-ttu-id="fd270-154">PowerShell Workflow Runbook 是以 [Windows PowerShell 工作流程](automation-powershell-workflow.md)為基礎的文字 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fd270-154">PowerShell Workflow runbooks are text runbooks based on [Windows PowerShell Workflow](automation-powershell-workflow.md).</span></span>  <span data-ttu-id="fd270-155">您直接編輯 hello 的 hello runbook 使用 hello Azure 入口網站中的 hello 文字編輯器的程式碼。</span><span class="sxs-lookup"><span data-stu-id="fd270-155">You directly edit hello code of hello runbook using hello text editor in hello Azure portal.</span></span>  <span data-ttu-id="fd270-156">您也可以使用任何離線的文字編輯器和[匯入 hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx)至 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="fd270-156">You can also use any offline text editor and [import hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx) into Azure Automation.</span></span>

### <a name="advantages"></a><span data-ttu-id="fd270-157">優點</span><span class="sxs-lookup"><span data-stu-id="fd270-157">Advantages</span></span>
* <span data-ttu-id="fd270-158">使用 PowerShell 工作流程程式碼實作所有複雜的邏輯。</span><span class="sxs-lookup"><span data-stu-id="fd270-158">Implement all complex logic with PowerShell Workflow code.</span></span>
* <span data-ttu-id="fd270-159">使用[檢查點](automation-powershell-workflow.md#checkpoints)tooresume runbook，如果發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fd270-159">Use [checkpoints](automation-powershell-workflow.md#checkpoints) tooresume runbook in case of error.</span></span>
* <span data-ttu-id="fd270-160">使用[平行處理](automation-powershell-workflow.md#parallel-processing)tooperform 多個平行的動作。</span><span class="sxs-lookup"><span data-stu-id="fd270-160">Use [parallel processing](automation-powershell-workflow.md#parallel-processing) tooperform multiple actions in parallel.</span></span>
* <span data-ttu-id="fd270-161">可以包含其他圖形化 runbook 和 PowerShell 工作流程 runbook 做為子 runbook toocreate 高等級的工作流程。</span><span class="sxs-lookup"><span data-stu-id="fd270-161">Can include other Graphical runbooks and PowerShell Workflow runbooks as child runbooks toocreate high level workflows.</span></span>

### <a name="limitations"></a><span data-ttu-id="fd270-162">限制</span><span class="sxs-lookup"><span data-stu-id="fd270-162">Limitations</span></span>
* <span data-ttu-id="fd270-163">作者必須熟悉 PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="fd270-163">Author must be familiar with PowerShell Workflow.</span></span>
* <span data-ttu-id="fd270-164">Runbook 必須這類處理 hello 的 PowerShell 工作流程的其他複雜度[還原序列化物件](automation-powershell-workflow.md#code-changes)。</span><span class="sxs-lookup"><span data-stu-id="fd270-164">Runbook must deal with hello additional complexity of PowerShell Workflow such as [deserialized objects](automation-powershell-workflow.md#code-changes).</span></span>
* <span data-ttu-id="fd270-165">Runbook 採取長 toostart 比 PowerShell runbook，因為它需要 toobe 才執行編譯。</span><span class="sxs-lookup"><span data-stu-id="fd270-165">Runbook takes longer toostart than PowerShell runbooks since it needs toobe compiled before running.</span></span>
* <span data-ttu-id="fd270-166">PowerShell runbook 只能包含以子 runbook 使用 hello Start-azureautomationrunbook cmdlet，此 cmdlet 會建立新的工作。</span><span class="sxs-lookup"><span data-stu-id="fd270-166">PowerShell runbooks can only be included as child runbooks by using hello Start-AzureAutomationRunbook cmdlet which creates a new job.</span></span>

## <a name="considerations"></a><span data-ttu-id="fd270-167">考量</span><span class="sxs-lookup"><span data-stu-id="fd270-167">Considerations</span></span>
<span data-ttu-id="fd270-168">您應該考慮到帳戶 hello 時判斷特定 runbook 的型別 toouse 下列其他考量。</span><span class="sxs-lookup"><span data-stu-id="fd270-168">You should take into account hello following additional considerations when determining which type toouse for a particular runbook.</span></span>

* <span data-ttu-id="fd270-169">您無法將 runbook 轉換從圖形化 tootextual 型別，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="fd270-169">You can't convert runbooks from graphical tootextual type or vice-versa.</span></span>
* <span data-ttu-id="fd270-170">使用不同類型的 Runbook 作為子 Runbook 時有所限制。</span><span class="sxs-lookup"><span data-stu-id="fd270-170">There are limitations using runbooks of different types as a child runbook.</span></span>  <span data-ttu-id="fd270-171">如需詳細資訊，請參閱 [Azure 自動化中的子 Runbook](automation-child-runbooks.md) 。</span><span class="sxs-lookup"><span data-stu-id="fd270-171">See [Child runbooks in Azure Automation](automation-child-runbooks.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd270-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd270-172">Next steps</span></span>
* <span data-ttu-id="fd270-173">toolearn 進一步了解撰寫圖形化 runbook，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="fd270-173">toolearn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="fd270-174">toounderstand hello PowerShell 和 PowerShell 之間的差異工作流程中的 runbook，請參閱[學習 Windows PowerShell 工作流程](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="fd270-174">toounderstand hello differences between PowerShell and PowerShell workflows for runbooks, see [Learning Windows PowerShell Workflow](automation-powershell-workflow.md)</span></span>
* <span data-ttu-id="fd270-175">如需有關如何 toocreate 或匯入 Runbook，請參閱[建立或匯入 Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="fd270-175">For more information on how toocreate or import a Runbook, see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span>

