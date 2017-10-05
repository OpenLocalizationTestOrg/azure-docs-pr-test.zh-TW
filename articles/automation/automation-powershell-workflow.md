---
title: "了解適用於 Azure 自動化的 PowerShell 工作流程 | Microsoft Docs"
description: "本文旨在做為熟悉 PowerShell 的作者的快速課程，以了解 PowerShell 和 PowerShell 工作流程的特定差異，以及適用於自動化 Runbook 的概念。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 4de812c7f863e42a6ed10c2312d61b8377e06431
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="d9d00-103">了解適用於自動化 Runbook 的重要 Windows PowerShell 工作流程概念</span><span class="sxs-lookup"><span data-stu-id="d9d00-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="d9d00-104">Azure 自動化中的 Runbook 會實作為 Windows PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="d9d00-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="d9d00-105">Windows PowerShell 工作流程類似於 Windows PowerShell 指令碼，但有一些顯著的差異可能會對新使用者造成混淆。</span><span class="sxs-lookup"><span data-stu-id="d9d00-105">A Windows PowerShell Workflow is similar to a Windows PowerShell script but has some significant differences that can be confusing to a new user.</span></span>  <span data-ttu-id="d9d00-106">雖然本文旨在協助您使用 PowerShell 工作流程撰寫 Runbook，但是除非您需要檢查點，否則建議您使用 PowerShell 來撰寫 Runbook。</span><span class="sxs-lookup"><span data-stu-id="d9d00-106">While this article is intended to help you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="d9d00-107">在撰寫 PowerShell 工作流程 Runbook 時有許多語法差異，而這些差異需要更多的工作來撰寫有效的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d9d00-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work to write effective workflows.</span></span>  

<span data-ttu-id="d9d00-108">工作流程是一連串的程式化、連接步驟，執行長時間執行的工作，或是需要跨多個裝置或受管理節點協調多個步驟。</span><span class="sxs-lookup"><span data-stu-id="d9d00-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="d9d00-109">透過標準的指令碼工作流程的好處包括能夠同時對多個裝置執行動作，以及可自動從失敗復原的能力。</span><span class="sxs-lookup"><span data-stu-id="d9d00-109">The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures.</span></span> <span data-ttu-id="d9d00-110">Windows PowerShell 工作流程是使用 Windows Workflow Foundation 的 Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d9d00-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="d9d00-111">雖然工作流程是使用 Windows PowerShell 語法編寫，並由 Windows PowerShell 啟動，它是由 Windows Workflow Foundation 來處理。</span><span class="sxs-lookup"><span data-stu-id="d9d00-111">While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="d9d00-112">如需這篇文章中的主題的完整詳細資訊，請參閱 [開始使用 Windows PowerShell 工作流程](http://technet.microsoft.com/library/jj134242.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-112">For complete details on the topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="d9d00-113">工作流程的基本結構</span><span class="sxs-lookup"><span data-stu-id="d9d00-113">Basic structure of a workflow</span></span>
<span data-ttu-id="d9d00-114">將 PowerShell 指令碼轉換成 PowerShell 工作流程的第一個步驟是將它使用 **Workflow** 關鍵字含括。</span><span class="sxs-lookup"><span data-stu-id="d9d00-114">The first step to converting a PowerShell script to a PowerShell workflow is enclosing it with the **Workflow** keyword.</span></span>  <span data-ttu-id="d9d00-115">一種工作流程，以 **Workflow** 關鍵字為開頭，後面接著括在大括弧中的指令碼主體。</span><span class="sxs-lookup"><span data-stu-id="d9d00-115">A workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces.</span></span> <span data-ttu-id="d9d00-116">工作流程的名稱會遵循 **Workflow** 關鍵字，如下列語法所示：</span><span class="sxs-lookup"><span data-stu-id="d9d00-116">The name of the workflow follows the **Workflow** keyword as shown in the following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="d9d00-117">工作流程的名稱必須符合自動化 Runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d00-117">The name of the workflow must match the name of the Automation runbook.</span></span> <span data-ttu-id="d9d00-118">如果正在匯入 Runbook，檔案名稱必須符合工作流程名稱，並必須以 .ps1 結尾。</span><span class="sxs-lookup"><span data-stu-id="d9d00-118">If the runbook is being imported, then the filename must match the workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="d9d00-119">若要將參數加入至工作流程，請使用 **Param** 關鍵字，如同您會對指令碼執行的動作。</span><span class="sxs-lookup"><span data-stu-id="d9d00-119">To add parameters to the workflow, use the **Param** keyword just as you would to a script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="d9d00-120">程式碼變更</span><span class="sxs-lookup"><span data-stu-id="d9d00-120">Code changes</span></span>
<span data-ttu-id="d9d00-121">PowerShell 工作流程程式碼看起來幾乎類似於 PowerShell 指令碼，除了少數幾個重大變更。</span><span class="sxs-lookup"><span data-stu-id="d9d00-121">PowerShell workflow code looks almost identical to PowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="d9d00-122">下列各節說明您必須對 PowerShell 指令碼進行的變更，以讓它在工作流程中執行。</span><span class="sxs-lookup"><span data-stu-id="d9d00-122">The following sections describe changes that you need to make to a PowerShell script for it to run in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="d9d00-123">活動</span><span class="sxs-lookup"><span data-stu-id="d9d00-123">Activities</span></span>
<span data-ttu-id="d9d00-124">活動是工作流程中的特定工作。</span><span class="sxs-lookup"><span data-stu-id="d9d00-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="d9d00-125">就像指令碼是由一或多個命令所組成，工作流程是由序列中執行的一或多個活動所組成。</span><span class="sxs-lookup"><span data-stu-id="d9d00-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="d9d00-126">執行工作流程時，Windows PowerShell 工作流程會自動將許多 Windows PowerShell Cmdlet 轉換為活動。</span><span class="sxs-lookup"><span data-stu-id="d9d00-126">Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow.</span></span> <span data-ttu-id="d9d00-127">在 Runbook 中指定其中一個 Cmdlet 時，對應的活動是由 Windows Workflow Foundation 執行。</span><span class="sxs-lookup"><span data-stu-id="d9d00-127">When you specify one of these cmdlets in your runbook, the corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="d9d00-128">針對沒有對應活動的 Cmdlet，Windows PowerShell 工作流程會自動在 [InlineScript](#inlinescript) 活動內執行 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d9d00-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="d9d00-129">有一組 Cmdlet 被排除，除非您明確在 InlineScript 區塊中將其納入，否則無法用在工作流程中。</span><span class="sxs-lookup"><span data-stu-id="d9d00-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="d9d00-130">如需這些概念的詳細資訊，請參閱 [在指令碼工作流程中使用活動](http://technet.microsoft.com/library/jj574194.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="d9d00-131">工作流程活動共用一組通用參數來設定其作業。</span><span class="sxs-lookup"><span data-stu-id="d9d00-131">Workflow activities share a set of common parameters to configure their operation.</span></span> <span data-ttu-id="d9d00-132">如需有關工作流程通用參數的詳細資訊，請參閱 [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-132">For details about the workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="d9d00-133">位置參數</span><span class="sxs-lookup"><span data-stu-id="d9d00-133">Positional parameters</span></span>
<span data-ttu-id="d9d00-134">您無法對活動和工作流程中的 Cmdlet 使用位置參數。</span><span class="sxs-lookup"><span data-stu-id="d9d00-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="d9d00-135">這都表示您必須使用參數名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d00-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="d9d00-136">例如，請考慮會取得所有執行中服務的下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d9d00-136">For example, consider the following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="d9d00-137">如果您嘗試在工作流程中執行這個相同的程式碼，您會接收到像「無法使用指定的具名參數解析參數集」的訊息。</span><span class="sxs-lookup"><span data-stu-id="d9d00-137">If you try to run this same code in a workflow, you receive a message like "Parameter set cannot be resolved using the specified named parameters."</span></span>  <span data-ttu-id="d9d00-138">若要修正這個問題，請提供參數名稱，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d9d00-138">To correct this, provide the parameter name as in the following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="d9d00-139">已還原序列化的物件</span><span class="sxs-lookup"><span data-stu-id="d9d00-139">Deserialized objects</span></span>
<span data-ttu-id="d9d00-140">工作流程中的物件會還原序列化。</span><span class="sxs-lookup"><span data-stu-id="d9d00-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="d9d00-141">這表示其屬性都仍然可用，而不是它們的方法。</span><span class="sxs-lookup"><span data-stu-id="d9d00-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="d9d00-142">例如，請考慮下列 PowerShell 程式碼，它會使用 Service 物件的 Stop 方法來停止服務。</span><span class="sxs-lookup"><span data-stu-id="d9d00-142">For example, consider the following PowerShell code that stops a service using the Stop method of the Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="d9d00-143">如果您嘗試執行此工作流程，您會接收到錯誤，指出「Windows PowerShell 工作流程不支援方法引動過程」。</span><span class="sxs-lookup"><span data-stu-id="d9d00-143">If you try to run this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="d9d00-144">其中一個選項是將這兩行程式碼中包裝在 [InlineScript](#inlinescript) 區塊中，在此情況下 $Service 會是區塊內的服務物件。</span><span class="sxs-lookup"><span data-stu-id="d9d00-144">One option is to wrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within the block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="d9d00-145">另一個選項是使用會與方法執行相同功能的另一個 Cmdlet，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="d9d00-145">Another option is to use another cmdlet that performs the same functionality as the method, if one is available.</span></span>  <span data-ttu-id="d9d00-146">在我們的範例中，Stop-Service Cmdlet 會提供與 Stop 方法相同的功能，並且您可以使用下面工作流程。</span><span class="sxs-lookup"><span data-stu-id="d9d00-146">In our sample, the Stop-Service cmdlet provides the same functionality as the Stop method, and you could use the following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="d9d00-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="d9d00-147">InlineScript</span></span>
<span data-ttu-id="d9d00-148">當您需要執行一或多個命令做為傳統的 PowerShell 指令碼 (而不是 PowerShell 工作流程) 時， **InlineScript** 活動很實用。</span><span class="sxs-lookup"><span data-stu-id="d9d00-148">The **InlineScript** activity is useful when you need to run one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="d9d00-149">在工作流程中的命令會傳送至 Windows Workflow Foundation 進行處理，而 Windows PowerShell 會處理 InlineScript 區塊中的命令。</span><span class="sxs-lookup"><span data-stu-id="d9d00-149">While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="d9d00-150">InlineScript 使用如下所示的語法。</span><span class="sxs-lookup"><span data-stu-id="d9d00-150">InlineScript uses the following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="d9d00-151">透過將輸出指派給變數，您可以從 InlineScript 傳回輸出。</span><span class="sxs-lookup"><span data-stu-id="d9d00-151">You can return output from an InlineScript by assigning the output to a variable.</span></span> <span data-ttu-id="d9d00-152">下列範例會停止服務，然後輸出服務名稱。</span><span class="sxs-lookup"><span data-stu-id="d9d00-152">The following example stops a service and then outputs the service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="d9d00-153">您可以將值傳入 InlineScript 區塊，但必須使用 **$Using** 範圍修飾詞。</span><span class="sxs-lookup"><span data-stu-id="d9d00-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="d9d00-154">下列範例與前一個範例相同，不同之處在於服務名稱是由變數所提供。</span><span class="sxs-lookup"><span data-stu-id="d9d00-154">The following example is identical to the previous example except that the service name is provided by a variable.</span></span>

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="d9d00-155">雖然 InlineScript 活動在特定工作流程中可能是關鍵，它們不支援工作流程建構，而且應該基於以下原因時使用：</span><span class="sxs-lookup"><span data-stu-id="d9d00-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for the following reasons:</span></span>

* <span data-ttu-id="d9d00-156">您不能在 InlineScript 區塊內使用[檢查點](#checkpoints)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="d9d00-157">如果失敗發生在區塊內，它必須從區塊的開頭繼續。</span><span class="sxs-lookup"><span data-stu-id="d9d00-157">If a failure occurs within the block, it must be resumed from the beginning of the block.</span></span>
* <span data-ttu-id="d9d00-158">您不能在 InlineScriptBlock 內使用[平行執行](#parallel-processing)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="d9d00-159">InlineScript 會影響工作流程的延展性，因為它會保留 InlineScript 區塊的整個長度的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d9d00-159">InlineScript affects scalability of the workflow since it holds the Windows PowerShell session for the entire length of the InlineScript block.</span></span>

<span data-ttu-id="d9d00-160">如需使用 InlineScript 的詳細資訊，請參閱[在工作流程中執行 Windows PowerShell 命令](http://technet.microsoft.com/library/jj574197.aspx)和 [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="d9d00-161">平行處理</span><span class="sxs-lookup"><span data-stu-id="d9d00-161">Parallel processing</span></span>
<span data-ttu-id="d9d00-162">Windows PowerShell 工作流程的優點之一是可平行執行一組命令，而不是如同一般的指令碼以循序方式執行。</span><span class="sxs-lookup"><span data-stu-id="d9d00-162">One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="d9d00-163">您可以使用 **Parallel** 關鍵字來建立具有多個同時執行的命令的指令碼區塊。</span><span class="sxs-lookup"><span data-stu-id="d9d00-163">You can use the **Parallel** keyword to create a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="d9d00-164">這會使用如下所示的語法。</span><span class="sxs-lookup"><span data-stu-id="d9d00-164">This uses the following syntax shown below.</span></span> <span data-ttu-id="d9d00-165">在此情況下，Activity1 和 Activity2 將同時開始。</span><span class="sxs-lookup"><span data-stu-id="d9d00-165">In this case, Activity1 and Activity2 starts at the same time.</span></span> <span data-ttu-id="d9d00-166">只有在 Activity1 和 Activity2 都已完成之後，Activity3 才會開始。</span><span class="sxs-lookup"><span data-stu-id="d9d00-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="d9d00-167">例如，考慮下列 PowerShell 命令，它會將多個檔案複製到網路目的地。</span><span class="sxs-lookup"><span data-stu-id="d9d00-167">For example, consider the following PowerShell commands that copy multiple files to a network destination.</span></span>  <span data-ttu-id="d9d00-168">這些命令會循序執行，因此一個檔案必須完成複製才能開始複製下一個。</span><span class="sxs-lookup"><span data-stu-id="d9d00-168">These commands are run sequentially so that one file must finish copying before the next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="d9d00-169">下列工作流程會平行執行這些相同的命令，讓它們在相同的時間全部開始複製。</span><span class="sxs-lookup"><span data-stu-id="d9d00-169">The following workflow runs these same commands in parallel so that they all start copying at the same time.</span></span>  <span data-ttu-id="d9d00-170">只有在全部複製之後，才會顯示完成訊息。</span><span class="sxs-lookup"><span data-stu-id="d9d00-170">Only after they are all copied is the completion message displayed.</span></span>

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


<span data-ttu-id="d9d00-171">您可以使用 **ForEach-Parallel** 建構來並行處理集合中每個項目的命令。</span><span class="sxs-lookup"><span data-stu-id="d9d00-171">You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently.</span></span> <span data-ttu-id="d9d00-172">會以平行方式處理集合中的項目，而循序執行指令碼區塊中的命令。</span><span class="sxs-lookup"><span data-stu-id="d9d00-172">The items in the collection are processed in parallel while the commands in the script block run sequentially.</span></span> <span data-ttu-id="d9d00-173">這會使用如下所示的語法。</span><span class="sxs-lookup"><span data-stu-id="d9d00-173">This uses the following syntax shown below.</span></span> <span data-ttu-id="d9d00-174">在此情況下，Activity1 將與集合中的所有項目同時開始。</span><span class="sxs-lookup"><span data-stu-id="d9d00-174">In this case, Activity1 starts at the same time for all items in the collection.</span></span> <span data-ttu-id="d9d00-175">針對每個項目，Activity2 會在 Activity1 完成之後開始。</span><span class="sxs-lookup"><span data-stu-id="d9d00-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="d9d00-176">只有在 Activity1 和 Activity2 已完成所有項目之後，Activity3 才會開始。</span><span class="sxs-lookup"><span data-stu-id="d9d00-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="d9d00-177">下列範例類似於先前的平行複製檔案範例。</span><span class="sxs-lookup"><span data-stu-id="d9d00-177">The following example is similar to the previous example copying files in parallel.</span></span>  <span data-ttu-id="d9d00-178">在此情況下，複製之後會對每個檔案顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="d9d00-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="d9d00-179">只有在全部完成複製之後，才會顯示最終完成訊息。</span><span class="sxs-lookup"><span data-stu-id="d9d00-179">Only after they are all completely copied is the final completion message displayed.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> <span data-ttu-id="d9d00-180">我們不建議並行執行子 Runbook，因為這可能會提供不可靠的結果。</span><span class="sxs-lookup"><span data-stu-id="d9d00-180">We do not recommend running child runbooks in parallel since this has been shown to give unreliable results.</span></span>  <span data-ttu-id="d9d00-181">有時候子 Runbook 的輸出不會出現，並且一個子 Runbook 中的設定會影響其他平行子 Runbook</span><span class="sxs-lookup"><span data-stu-id="d9d00-181">The output from the child runbook sometimes does not show up, and settings in one child runbook can affect the other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="d9d00-182">檢查點</span><span class="sxs-lookup"><span data-stu-id="d9d00-182">Checkpoints</span></span>
<span data-ttu-id="d9d00-183">*檢查點* 是包含變數的目前值和在該點產生的任何輸出的工作流程的目前狀態的快照。</span><span class="sxs-lookup"><span data-stu-id="d9d00-183">A *checkpoint* is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point.</span></span> <span data-ttu-id="d9d00-184">如果工作流程結束時發生錯誤或是擱置，則下次執行時就會從其最後一個檢查點開始，而不是工作流程的開頭開始。</span><span class="sxs-lookup"><span data-stu-id="d9d00-184">If a workflow ends in error or is suspended, then the next time it is run it will start from its last checkpoint instead of the start of the worfklow.</span></span>  <span data-ttu-id="d9d00-185">您可以使用 **Checkpoint-Workflow** 活動來設定工作流程中的檢查點。</span><span class="sxs-lookup"><span data-stu-id="d9d00-185">You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="d9d00-186">在下列範例程式碼中，Activity2 之後發生的例外狀況造成工作流程結束。</span><span class="sxs-lookup"><span data-stu-id="d9d00-186">In the following sample code, an exception occurs after Activity2 causing the workflow to end.</span></span> <span data-ttu-id="d9d00-187">工作流程再次執行時，它會先執行 Activity2，因為這是緊接在設定的最後一個檢查點之後。</span><span class="sxs-lookup"><span data-stu-id="d9d00-187">When the workflow is run again, it starts by running Activity2 since this was just after the last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="d9d00-188">在活動可能容易發生例外狀況，且不應在工作流程繼續執行之後重複執行時，您應該在工作流程中設定檢查點。</span><span class="sxs-lookup"><span data-stu-id="d9d00-188">You should set checkpoints in a workflow after activities that may be prone to exception and should not be repeated if the workflow is resumed.</span></span> <span data-ttu-id="d9d00-189">例如，您的工作流程可能會建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d9d00-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="d9d00-190">您可以在建立虛擬機器命令的前面和後面設定檢查點。</span><span class="sxs-lookup"><span data-stu-id="d9d00-190">You could set a checkpoint both before and after the commands to create the virtual machine.</span></span> <span data-ttu-id="d9d00-191">如果建立失敗，若再次開始工作流程，命令可能會重複。</span><span class="sxs-lookup"><span data-stu-id="d9d00-191">If the creation fails, then the commands would be repeated if the workflow is started again.</span></span> <span data-ttu-id="d9d00-192">如果建立成功之後工作流程失敗，當工作流程繼續時，將不會再次建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d9d00-192">If the worfklow fails after the creation succeeds, then the virtual machine will not be created again when the workflow is resumed.</span></span>

<span data-ttu-id="d9d00-193">下列範例會將多個檔案複製到網路位置，並在每個檔案後設定檢查點。</span><span class="sxs-lookup"><span data-stu-id="d9d00-193">The following example copies multiple files to a network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="d9d00-194">如果遺失網路位置，工作流程結束時會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="d9d00-194">If the network location is lost, then the workflow ends in error.</span></span>  <span data-ttu-id="d9d00-195">當重新啟動時，它會從最後一個檢查點繼續，表示只會略過已複製的檔案。</span><span class="sxs-lookup"><span data-stu-id="d9d00-195">When it is started again, it will resume at the last checkpoint meaning that only the files that have already been copied are skipped.</span></span>

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

<span data-ttu-id="d9d00-196">在您呼叫 [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) 活動或最後一個檢查點之後，使用者名稱認證就不會保存下來，因此您必須將認證設定為 null，然後在呼叫 **Suspend-Workflow** 或檢查點後，再次從資產存放區擷取認證。</span><span class="sxs-lookup"><span data-stu-id="d9d00-196">Because username credentials are not persisted after you call the [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after the last checkpoint, you need to set the credentials to null and then retrieve them again from the asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="d9d00-197">否則，您可能會收到下列錯誤訊息︰工作流程作業無法繼續，原因是無法完整儲存持續性資料或儲存的持續性資料已損毀。您必須重新啟動工作流程。</span><span class="sxs-lookup"><span data-stu-id="d9d00-197">Otherwise, you may receive the following error message: *The workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart the workflow.*</span></span>

<span data-ttu-id="d9d00-198">下列同一個程式碼會示範如何在 PowerShell 工作流程 Runbook 中處理此問題。</span><span class="sxs-lookup"><span data-stu-id="d9d00-198">The following same code demonstrates how to handle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first to create the VM (code not shown)

          # Now add the VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="d9d00-199">如果您使用以服務主體設定的執行身分帳戶進行驗證，則不必這麼做。</span><span class="sxs-lookup"><span data-stu-id="d9d00-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="d9d00-200">如需有關檢查點的詳細資訊，請參閱 [加入檢查點至指令碼工作流程](http://technet.microsoft.com/library/jj574114.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d9d00-200">For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d00-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9d00-201">Next steps</span></span>
* <span data-ttu-id="d9d00-202">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="d9d00-202">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
