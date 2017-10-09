---
title: "在 Azure 自動化的圖形化 runbook 中處理 aaaError |Microsoft 文件"
description: "本文說明如何 tooimplement 錯誤處理邏輯，在 Azure 自動化的圖形化 runbook。"
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
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a><span data-ttu-id="58a85-103">Azure 自動化之圖形化 Runbook 中的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="58a85-103">Error handling in Azure Automation graphical runbooks</span></span>

<span data-ttu-id="58a85-104">索引鍵的 runbook 設計主體 tooconsider 發現不同 runbook 可能會遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="58a85-104">A key runbook design principal tooconsider is identifying different issues that a runbook might experience.</span></span> <span data-ttu-id="58a85-105">這些問題包括成功、預期的錯誤狀態，以及非預期的錯誤情況。</span><span class="sxs-lookup"><span data-stu-id="58a85-105">These issues can include success, expected error states, and unexpected error conditions.</span></span>

<span data-ttu-id="58a85-106">Runbook 應該包含錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="58a85-106">Runbooks should include error handling.</span></span> <span data-ttu-id="58a85-107">toovalidate hello 活動的輸出，或處理的錯誤與圖形化 runbook，您可以使用 Windows PowerShell 程式碼活動、 hello 輸出連結的 hello 活動上定義的條件式邏輯或套用另一種方法。</span><span class="sxs-lookup"><span data-stu-id="58a85-107">toovalidate hello output of an activity or handle an error with graphical runbooks, you could use a Windows PowerShell code activity, define conditional logic on hello output link of hello activity, or apply another method.</span></span>          

<span data-ttu-id="58a85-108">通常，如果沒有與 runbook 活動，就會發生非終止錯誤，遵循任何活動處理不論 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="58a85-108">Often, if there is a non-terminating error that occurs with a runbook activity, any activity that follows is processed regardless of hello error.</span></span> <span data-ttu-id="58a85-109">hello 錯誤可能 toogenerate 例外狀況，但 hello 下一個活動仍允許 toorun。</span><span class="sxs-lookup"><span data-stu-id="58a85-109">hello error is likely toogenerate an exception, but hello next activity is still allowed toorun.</span></span> <span data-ttu-id="58a85-110">這是 PowerShell 是設計的 toohandle 錯誤 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="58a85-110">This is hello way that PowerShell is designed toohandle errors.</span></span>    

<span data-ttu-id="58a85-111">終止或非終止 hello PowerShell 發生的錯誤可以在執行期間的類型。</span><span class="sxs-lookup"><span data-stu-id="58a85-111">hello types of PowerShell errors that can occur during execution are terminating or non-terminating.</span></span> <span data-ttu-id="58a85-112">hello 終止和非終止錯誤之間的差異如下所示：</span><span class="sxs-lookup"><span data-stu-id="58a85-112">hello differences between terminating and non-terminating errors are as follows:</span></span>

* <span data-ttu-id="58a85-113">**終止錯誤**： 完全中止 hello 命令 （或執行指令碼） 的執行期間發生嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="58a85-113">**Terminating error**: A serious error during execution that halts hello command (or script execution) completely.</span></span> <span data-ttu-id="58a85-114">範例包括不存在的 Cmdlet、防止 Cmdlet 執行的語法錯誤，或其他嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="58a85-114">Examples include non-existent cmdlets, syntax errors that prevent a cmdlet from running, or other fatal errors.</span></span>

* <span data-ttu-id="58a85-115">**非終止錯誤**： 可讓執行 toocontinue 儘管 hello 失敗的非嚴重錯誤。</span><span class="sxs-lookup"><span data-stu-id="58a85-115">**Non-terminating error**: A non-serious error that allows execution toocontinue despite hello failure.</span></span> <span data-ttu-id="58a85-116">範例包括操作錯誤，例如找不到檔案錯誤和權限問題。</span><span class="sxs-lookup"><span data-stu-id="58a85-116">Examples include operational errors such as file not found errors and permissions problems.</span></span>

<span data-ttu-id="58a85-117">Azure 自動化的圖形化 runbook 已改善了 hello 功能 tooinclude 錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="58a85-117">Azure Automation graphical runbooks have been improved with hello capability tooinclude error handling.</span></span> <span data-ttu-id="58a85-118">您現在可以將例外狀況變成非終止錯誤，並建立活動之間的錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="58a85-118">You can now turn exceptions into non-terminating errors and create error links between activities.</span></span> <span data-ttu-id="58a85-119">此程序可讓 runbook 作者 toocatch 錯誤，並管理實現或非預期的條件。</span><span class="sxs-lookup"><span data-stu-id="58a85-119">This process allows a runbook author toocatch errors and manage realized or unexpected conditions.</span></span>  

## <a name="when-toouse-error-handling"></a><span data-ttu-id="58a85-120">當 toouse 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="58a85-120">When toouse error handling</span></span>

<span data-ttu-id="58a85-121">重要的活動會擲回錯誤或例外狀況時，它是重要 tooprevent hello 下一個活動處理和 toohandle hello 錯誤從 runbook 中的適當地。</span><span class="sxs-lookup"><span data-stu-id="58a85-121">Whenever there is a critical activity that throws an error or exception, it's important tooprevent hello next activity in your runbook from processing and toohandle hello error appropriately.</span></span> <span data-ttu-id="58a85-122">當 Runbook 支援商務或服務營運流程時，這點格外重要。</span><span class="sxs-lookup"><span data-stu-id="58a85-122">This is especially critical when your runbooks are supporting a business or service operations process.</span></span>

<span data-ttu-id="58a85-123">每個活動可能會產生錯誤，hello runbook 作者可以加入錯誤連結指向 tooany 其他活動。</span><span class="sxs-lookup"><span data-stu-id="58a85-123">For each activity that can produce an error, hello runbook author can add an error link pointing tooany other activity.</span></span>  <span data-ttu-id="58a85-124">hello 目的地活動可以是任何類型，包括程式碼活動叫用 cmdlet 中叫用另一個 runbook，並以此類推。</span><span class="sxs-lookup"><span data-stu-id="58a85-124">hello destination activity can be of any type, including code activities, invoking a cmdlet, invoking another runbook, and so on.</span></span>

<span data-ttu-id="58a85-125">此外，hello 目的地活動也可以連出連結。</span><span class="sxs-lookup"><span data-stu-id="58a85-125">In addition, hello destination activity can also have outgoing links.</span></span> <span data-ttu-id="58a85-126">這些連結可以是一般連結或錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="58a85-126">These links can be regular links or error links.</span></span> <span data-ttu-id="58a85-127">這表示 hello runbook 作者可以實作複雜的錯誤處理邏輯，就可以做到 tooa 沒有程式碼活動。</span><span class="sxs-lookup"><span data-stu-id="58a85-127">This means hello runbook author can implement complex error-handling logic without resorting tooa code activity.</span></span> <span data-ttu-id="58a85-128">hello 建議的作法是 toocreate 專用的錯誤處理 runbook 一般功能，但不是強制性。</span><span class="sxs-lookup"><span data-stu-id="58a85-128">hello recommended practice is toocreate a dedicated error-handling runbook with common functionality, but it's not mandatory.</span></span> <span data-ttu-id="58a85-129">不是 PowerShell 程式碼活動中的錯誤處理邏輯 hello 僅 選項。</span><span class="sxs-lookup"><span data-stu-id="58a85-129">Error-handling logic in a PowerShell code activity it isn't hello only option.</span></span>  

<span data-ttu-id="58a85-130">比方說，請思考嘗試 toostart runbook 的 VM，並在其上安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="58a85-130">For example, consider a runbook that tries toostart a VM and install an application on it.</span></span> <span data-ttu-id="58a85-131">如果 hello VM 並未正確啟動，它會執行兩個動作：</span><span class="sxs-lookup"><span data-stu-id="58a85-131">If hello VM doesn't start correctly, it performs two actions:</span></span>

1. <span data-ttu-id="58a85-132">傳送關於這個問題的通知。</span><span class="sxs-lookup"><span data-stu-id="58a85-132">It sends a notification about this problem.</span></span>
2. <span data-ttu-id="58a85-133">改為啟動另一個會自動佈建新 VM 的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="58a85-133">It starts another runbook that automatically provisions a new VM instead.</span></span>

<span data-ttu-id="58a85-134">其中一種解決方案是 toohave 指向 tooan 活動處理步驟一錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="58a85-134">One solution is toohave an error link pointing tooan activity that handles step one.</span></span> <span data-ttu-id="58a85-135">例如，您就可以連接 hello **Write-warning** cmdlet tooan 活動的第二個，步驟，例如 hello**開始 AzureRmAutomationRunbook** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="58a85-135">For example, you could connect hello **Write-Warning** cmdlet tooan activity for step two, such as hello **Start-AzureRmAutomationRunbook** cmdlet.</span></span>

<span data-ttu-id="58a85-136">您也無法將這兩種活動放在個別錯誤處理 runbook 和先前建議下列 hello 指引來一般化許多 runbook 中使用這個的行為。</span><span class="sxs-lookup"><span data-stu-id="58a85-136">You could also generalize this behavior for use in many runbooks by putting these two activities in a separate error handling runbook and following hello guidance suggested earlier.</span></span> <span data-ttu-id="58a85-137">然後再呼叫此錯誤處理 runbook，可以建構自訂訊息 hello 原始 runbook、 hello 資料，然後將它傳遞為參數 toohello 錯誤處理 runbook。</span><span class="sxs-lookup"><span data-stu-id="58a85-137">Before calling this error-handling runbook, you could construct a custom message from hello data in hello original runbook, and then pass it as a parameter toohello error-handling runbook.</span></span>

## <a name="how-toouse-error-handling"></a><span data-ttu-id="58a85-138">如何 toouse 錯誤處理</span><span class="sxs-lookup"><span data-stu-id="58a85-138">How toouse error handling</span></span>

<span data-ttu-id="58a85-139">每個活動均有組態設定可將例外狀況變成非終止錯誤。</span><span class="sxs-lookup"><span data-stu-id="58a85-139">Each activity has a configuration setting that turns exceptions into non-terminating errors.</span></span> <span data-ttu-id="58a85-140">此設定預設為停用狀態。</span><span class="sxs-lookup"><span data-stu-id="58a85-140">By default, this setting is disabled.</span></span> <span data-ttu-id="58a85-141">我們建議您啟用這項設定在您想要 toohandle 錯誤的任何活動。</span><span class="sxs-lookup"><span data-stu-id="58a85-141">We recommend that you enable this setting on any activity where you want toohandle errors.</span></span>  

<span data-ttu-id="58a85-142">您會藉由啟用這項設定，以確保在 hello 活動的終止和非終止錯誤會當做非終止錯誤，處理，而且可以處理與錯誤連結。</span><span class="sxs-lookup"><span data-stu-id="58a85-142">By enabling this configuration, you are assuring that both terminating and non-terminating errors in hello activity are handled as non-terminating errors, and can be handled with an error link.</span></span>  

<span data-ttu-id="58a85-143">設定此設定之後, 您可以建立處理 hello 錯誤的活動。</span><span class="sxs-lookup"><span data-stu-id="58a85-143">After configuring this setting, you create an activity that handles hello error.</span></span> <span data-ttu-id="58a85-144">活動就會產生任何錯誤，然後 hello 傳出錯誤連結會遵循，和 hello 標準連結則不會，即使 hello 活動都會產生以及規則的輸出。</span><span class="sxs-lookup"><span data-stu-id="58a85-144">If an activity produces any error, then hello outgoing error links are followed, and hello regular links are not, even if hello activity produces regular output as well.</span></span><br><br> ![自動化 Runbook 的錯誤連結範例](media/automation-runbook-graphical-error-handling/error-link-example.png)

<span data-ttu-id="58a85-146">在下列範例的 hello，runbook 會擷取包含 hello 的虛擬機器的電腦名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="58a85-146">In hello following example, a runbook retrieves a variable that contains hello computer name of a virtual machine.</span></span> <span data-ttu-id="58a85-147">接著，它會嘗試 toostart hello 虛擬機器與 hello 下一個活動。</span><span class="sxs-lookup"><span data-stu-id="58a85-147">It then attempts toostart hello virtual machine with hello next activity.</span></span><br><br> ![自動化 Runbook 的錯誤處理範例](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

<span data-ttu-id="58a85-149">hello **Get-automationvariable**活動和**開始 AzureRmVm**會設定的 tooconvert 例外狀況 tooerrors。</span><span class="sxs-lookup"><span data-stu-id="58a85-149">hello **Get-AutomationVariable** activity and **Start-AzureRmVm** are configured tooconvert exceptions tooerrors.</span></span>  <span data-ttu-id="58a85-150">如果有問題 hello 變數或起始 hello VM，則會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="58a85-150">If there are problems getting hello variable or starting hello VM, then errors are generated.</span></span><br><br> <span data-ttu-id="58a85-151">![自動化 Runbook 的錯誤處理活動設定](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)</span><span class="sxs-lookup"><span data-stu-id="58a85-151">![Automation runbook error-handling activity settings](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)</span></span>

<span data-ttu-id="58a85-152">錯誤連結會從單一這些活動 tooa 流向**錯誤管理**活動 （程式碼活動）。</span><span class="sxs-lookup"><span data-stu-id="58a85-152">Error links flow from these activities tooa single **error management** activity (a code activity).</span></span> <span data-ttu-id="58a85-153">此活動設定簡單的 PowerShell 運算式使用 hello*擲回*處理，以及與關鍵字 toostop *$Error.Exception.Message* tooget hello 訊息，描述 hello目前的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="58a85-153">This activity is configured with a simple PowerShell expression that uses hello *Throw* keyword toostop processing, along with *$Error.Exception.Message* tooget hello message that describes hello current exception.</span></span><br><br> <span data-ttu-id="58a85-154">![自動化 Runbook 的錯誤處理程式碼範例](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)</span><span class="sxs-lookup"><span data-stu-id="58a85-154">![Automation runbook error-handling code example](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)</span></span>


## <a name="next-steps"></a><span data-ttu-id="58a85-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58a85-155">Next steps</span></span>

* <span data-ttu-id="58a85-156">toolearn 深入了解連結和連結類型，在圖形化 runbook，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md#links-and-workflow)。</span><span class="sxs-lookup"><span data-stu-id="58a85-156">toolearn more about links and link types in graphical runbooks, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md#links-and-workflow).</span></span>

* <span data-ttu-id="58a85-157">深入了解 runbook 執行時，如何 toomonitor runbook 作業和其他技術的詳細資訊，請參閱 toolearn[追蹤 runbook 工作](automation-runbook-execution.md)。</span><span class="sxs-lookup"><span data-stu-id="58a85-157">toolearn more about runbook execution, how toomonitor runbook jobs, and other technical details, see [Track a runbook job](automation-runbook-execution.md).</span></span>
