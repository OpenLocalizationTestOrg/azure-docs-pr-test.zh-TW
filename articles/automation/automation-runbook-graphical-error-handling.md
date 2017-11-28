---
title: "Azure 自動化之圖形化 Runbook 中的錯誤處理 | Microsoft Docs"
description: "本文說明如何在 Azure 自動化的圖形化 Runbook 中實作錯誤處理邏輯。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: 12313f7f245d32c33882f1036f7d4b48bfb3ddc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a><span data-ttu-id="f8b55-103">Azure 自動化之圖形化 Runbook 中的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="f8b55-103">Error handling in Azure Automation graphical runbooks</span></span>

<span data-ttu-id="f8b55-104">所要考量的主要 Runbook 設計主體是找出 Runbook 可能遇到的不同問題。</span><span class="sxs-lookup"><span data-stu-id="f8b55-104">A key runbook design principal to consider is identifying different issues that a runbook might experience.</span></span> <span data-ttu-id="f8b55-105">這些問題包括成功、預期的錯誤狀態，以及非預期的錯誤情況。</span><span class="sxs-lookup"><span data-stu-id="f8b55-105">These issues can include success, expected error states, and unexpected error conditions.</span></span>

<span data-ttu-id="f8b55-106">Runbook 應該包含錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="f8b55-106">Runbooks should include error handling.</span></span> <span data-ttu-id="f8b55-107">若要驗證活動的輸出，或以圖形化 Runbook 處理錯誤，您可以使用 Windows PowerShell 程式碼活動、定義活動輸出連結的條件式邏輯，或套用其他方法。</span><span class="sxs-lookup"><span data-stu-id="f8b55-107">To validate the output of an activity or handle an error with graphical runbooks, you could use a Windows PowerShell code activity, define conditional logic on the output link of the activity, or apply another method.</span></span>          

<span data-ttu-id="f8b55-108">如果 Runbook 活動發生非終止錯誤，其後的任何活動往往不管此錯誤仍會進行處理。</span><span class="sxs-lookup"><span data-stu-id="f8b55-108">Often, if there is a non-terminating error that occurs with a runbook activity, any activity that follows is processed regardless of the error.</span></span> <span data-ttu-id="f8b55-109">此錯誤可能會產生例外狀況，但仍允許執行下一個活動。</span><span class="sxs-lookup"><span data-stu-id="f8b55-109">The error is likely to generate an exception, but the next activity is still allowed to run.</span></span> <span data-ttu-id="f8b55-110">這是 PowerShell 設計用來處理錯誤的方式。</span><span class="sxs-lookup"><span data-stu-id="f8b55-110">This is the way that PowerShell is designed to handle errors.</span></span>    

<span data-ttu-id="f8b55-111">執行期間可能發生的 PowerShell 錯誤類型為終止或非終止。</span><span class="sxs-lookup"><span data-stu-id="f8b55-111">The types of PowerShell errors that can occur during execution are terminating or non-terminating.</span></span> <span data-ttu-id="f8b55-112">終止和非終止錯誤之間的差異如下︰</span><span class="sxs-lookup"><span data-stu-id="f8b55-112">The differences between terminating and non-terminating errors are as follows:</span></span>

* <span data-ttu-id="f8b55-113">**終止錯誤**︰執行期間所發生的嚴重錯誤，此錯誤會完全終止命令 (或指令碼執行)。</span><span class="sxs-lookup"><span data-stu-id="f8b55-113">**Terminating error**: A serious error during execution that halts the command (or script execution) completely.</span></span> <span data-ttu-id="f8b55-114">範例包括不存在的 Cmdlet、防止 Cmdlet 執行的語法錯誤，或其他嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8b55-114">Examples include non-existent cmdlets, syntax errors that prevent a cmdlet from running, or other fatal errors.</span></span>

* <span data-ttu-id="f8b55-115">**非終止錯誤**︰非嚴重錯誤，會允許繼續執行，而不理會失敗。</span><span class="sxs-lookup"><span data-stu-id="f8b55-115">**Non-terminating error**: A non-serious error that allows execution to continue despite the failure.</span></span> <span data-ttu-id="f8b55-116">範例包括操作錯誤，例如找不到檔案錯誤和權限問題。</span><span class="sxs-lookup"><span data-stu-id="f8b55-116">Examples include operational errors such as file not found errors and permissions problems.</span></span>

<span data-ttu-id="f8b55-117">Azure 自動化的圖形化 Runbook 已納入錯誤處理功能。</span><span class="sxs-lookup"><span data-stu-id="f8b55-117">Azure Automation graphical runbooks have been improved with the capability to include error handling.</span></span> <span data-ttu-id="f8b55-118">您現在可以將例外狀況變成非終止錯誤，並建立活動之間的錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="f8b55-118">You can now turn exceptions into non-terminating errors and create error links between activities.</span></span> <span data-ttu-id="f8b55-119">此處理可讓 Runbook 作者捕捉到錯誤，以及管理已實現或非預期的狀況。</span><span class="sxs-lookup"><span data-stu-id="f8b55-119">This process allows a runbook author to catch errors and manage realized or unexpected conditions.</span></span>  

## <a name="when-to-use-error-handling"></a><span data-ttu-id="f8b55-120">何時使用錯誤處理</span><span class="sxs-lookup"><span data-stu-id="f8b55-120">When to use error handling</span></span>

<span data-ttu-id="f8b55-121">每當有重要活動擲回錯誤或例外狀況時，務必要避免繼續處理 Runbook 中的下一個活動，並適當地處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8b55-121">Whenever there is a critical activity that throws an error or exception, it's important to prevent the next activity in your runbook from processing and to handle the error appropriately.</span></span> <span data-ttu-id="f8b55-122">當 Runbook 支援商務或服務營運流程時，這點格外重要。</span><span class="sxs-lookup"><span data-stu-id="f8b55-122">This is especially critical when your runbooks are supporting a business or service operations process.</span></span>

<span data-ttu-id="f8b55-123">對於每個可產生錯誤的活動，Runbook 作者均可新增指向任何其他活動的錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="f8b55-123">For each activity that can produce an error, the runbook author can add an error link pointing to any other activity.</span></span>  <span data-ttu-id="f8b55-124">目的地活動可以是任何類型，包括程式碼活動、叫用 Cmdlet、叫用另一個 Runbook 等等。</span><span class="sxs-lookup"><span data-stu-id="f8b55-124">The destination activity can be of any type, including code activities, invoking a cmdlet, invoking another runbook, and so on.</span></span>

<span data-ttu-id="f8b55-125">此外，目的地活動也可以有連出連結。</span><span class="sxs-lookup"><span data-stu-id="f8b55-125">In addition, the destination activity can also have outgoing links.</span></span> <span data-ttu-id="f8b55-126">這些連結可以是一般連結或錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="f8b55-126">These links can be regular links or error links.</span></span> <span data-ttu-id="f8b55-127">這表示 Runbook 作者可以實作複雜的錯誤處理邏輯，而不需向程式碼活動報告。</span><span class="sxs-lookup"><span data-stu-id="f8b55-127">This means the runbook author can implement complex error-handling logic without resorting to a code activity.</span></span> <span data-ttu-id="f8b55-128">建議作法是建立具有常用功能的專用錯誤處理 Runbook，但您不一定要照做。</span><span class="sxs-lookup"><span data-stu-id="f8b55-128">The recommended practice is to create a dedicated error-handling runbook with common functionality, but it's not mandatory.</span></span> <span data-ttu-id="f8b55-129">將錯誤處理邏輯放在 PowerShell 程式碼活動中也並非是唯一的選項。</span><span class="sxs-lookup"><span data-stu-id="f8b55-129">Error-handling logic in a PowerShell code activity it isn't the only option.</span></span>  

<span data-ttu-id="f8b55-130">例如，請考慮嘗試啟動 VM 的 Runbook 並在其上安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="f8b55-130">For example, consider a runbook that tries to start a VM and install an application on it.</span></span> <span data-ttu-id="f8b55-131">如果 VM 未正確啟動，它會執行兩個動作︰</span><span class="sxs-lookup"><span data-stu-id="f8b55-131">If the VM doesn't start correctly, it performs two actions:</span></span>

1. <span data-ttu-id="f8b55-132">傳送關於這個問題的通知。</span><span class="sxs-lookup"><span data-stu-id="f8b55-132">It sends a notification about this problem.</span></span>
2. <span data-ttu-id="f8b55-133">改為啟動另一個會自動佈建新 VM 的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f8b55-133">It starts another runbook that automatically provisions a new VM instead.</span></span>

<span data-ttu-id="f8b55-134">解決方案之一是擁有錯誤連結，以指向可處理步驟 1 的活動。</span><span class="sxs-lookup"><span data-stu-id="f8b55-134">One solution is to have an error link pointing to an activity that handles step one.</span></span> <span data-ttu-id="f8b55-135">例如，您可以將 **Write-Warning** Cmdlet 連接至步驟 2 的活動，例如 **Start-AzureRmAutomationRunbook** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f8b55-135">For example, you could connect the **Write-Warning** cmdlet to an activity for step two, such as the **Start-AzureRmAutomationRunbook** cmdlet.</span></span>

<span data-ttu-id="f8b55-136">將這兩個活動放在不同的錯誤處理 Runbook 中，並遵循稍早建議的指導方針，也可以讓此行為廣泛用於許多 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f8b55-136">You could also generalize this behavior for use in many runbooks by putting these two activities in a separate error handling runbook and following the guidance suggested earlier.</span></span> <span data-ttu-id="f8b55-137">在呼叫此錯誤處理 Runbook 之前，您可以從原始 Runbook 中的資料建構自訂訊息，然後將此訊息做為參數傳遞至錯誤處理 Runbook。</span><span class="sxs-lookup"><span data-stu-id="f8b55-137">Before calling this error-handling runbook, you could construct a custom message from the data in the original runbook, and then pass it as a parameter to the error-handling runbook.</span></span>

## <a name="how-to-use-error-handling"></a><span data-ttu-id="f8b55-138">如何使用錯誤處理</span><span class="sxs-lookup"><span data-stu-id="f8b55-138">How to use error handling</span></span>

<span data-ttu-id="f8b55-139">每個活動均有組態設定可將例外狀況變成非終止錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8b55-139">Each activity has a configuration setting that turns exceptions into non-terminating errors.</span></span> <span data-ttu-id="f8b55-140">此設定預設為停用狀態。</span><span class="sxs-lookup"><span data-stu-id="f8b55-140">By default, this setting is disabled.</span></span> <span data-ttu-id="f8b55-141">建議您在想要用來處理錯誤的任何活動上啟用此設定。</span><span class="sxs-lookup"><span data-stu-id="f8b55-141">We recommend that you enable this setting on any activity where you want to handle errors.</span></span>  

<span data-ttu-id="f8b55-142">藉由啟用此組態，您可以確保活動中的終止和非終止錯誤都會被當作非終止錯誤處理，並且可透過錯誤連結進行處理。</span><span class="sxs-lookup"><span data-stu-id="f8b55-142">By enabling this configuration, you are assuring that both terminating and non-terminating errors in the activity are handled as non-terminating errors, and can be handled with an error link.</span></span>  

<span data-ttu-id="f8b55-143">進行此設定之後，您就可以建立可處理錯誤的活動。</span><span class="sxs-lookup"><span data-stu-id="f8b55-143">After configuring this setting, you create an activity that handles the error.</span></span> <span data-ttu-id="f8b55-144">如果活動產生任何錯誤，則會出現連出的錯誤連結，而不會出現一般連結，即使活動也產生一般輸出。</span><span class="sxs-lookup"><span data-stu-id="f8b55-144">If an activity produces any error, then the outgoing error links are followed, and the regular links are not, even if the activity produces regular output as well.</span></span><br><br> ![自動化 Runbook 的錯誤連結範例](media/automation-runbook-graphical-error-handling/error-link-example.png)

<span data-ttu-id="f8b55-146">在下列範例中，Runbook 會擷取一個變數，其中包含虛擬機器的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="f8b55-146">In the following example, a runbook retrieves a variable that contains the computer name of a virtual machine.</span></span> <span data-ttu-id="f8b55-147">它會嘗試使用下一個活動啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8b55-147">It then attempts to start the virtual machine with the next activity.</span></span><br><br> ![自動化 Runbook 的錯誤處理範例](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

<span data-ttu-id="f8b55-149">依設定，**Get-AutomationVariable** 活動和 **Start-AzureRmVm** 會將例外狀況轉換為錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8b55-149">The **Get-AutomationVariable** activity and **Start-AzureRmVm** are configured to convert exceptions to errors.</span></span>  <span data-ttu-id="f8b55-150">如果無法取得變數或啟動 VM，就會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="f8b55-150">If there are problems getting the variable or starting the VM, then errors are generated.</span></span><br><br> <span data-ttu-id="f8b55-151">![自動化 Runbook 的錯誤處理活動設定](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)</span><span class="sxs-lookup"><span data-stu-id="f8b55-151">![Automation runbook error-handling activity settings](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)</span></span>

<span data-ttu-id="f8b55-152">錯誤連結會從這些活動流向單一**錯誤管理**活動 (程式碼活動)。</span><span class="sxs-lookup"><span data-stu-id="f8b55-152">Error links flow from these activities to a single **error management** activity (a code activity).</span></span> <span data-ttu-id="f8b55-153">此活動已設定了簡單的 PowerShell 運算式，其使用 Throw 關鍵字來停止處理，以及使用 $Error.Exception.Message 來取得說明目前例外狀況的訊息。</span><span class="sxs-lookup"><span data-stu-id="f8b55-153">This activity is configured with a simple PowerShell expression that uses the *Throw* keyword to stop processing, along with *$Error.Exception.Message* to get the message that describes the current exception.</span></span><br><br> <span data-ttu-id="f8b55-154">![自動化 Runbook 的錯誤處理程式碼範例](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)</span><span class="sxs-lookup"><span data-stu-id="f8b55-154">![Automation runbook error-handling code example](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="f8b55-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8b55-155">Next steps</span></span>

* <span data-ttu-id="f8b55-156">若要深入了解圖形化 Runbook 中的連結和連結類型，請參閱 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md#links-and-workflow)。</span><span class="sxs-lookup"><span data-stu-id="f8b55-156">To learn more about links and link types in graphical runbooks, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md#links-and-workflow).</span></span>

* <span data-ttu-id="f8b55-157">若要深入了解 Runbook 執行方式、如何監視 Runbook 作業，以及其他技術性詳細資料，請參閱[追蹤 Runbook 作業](automation-runbook-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="f8b55-157">To learn more about runbook execution, how to monitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md).</span></span>
