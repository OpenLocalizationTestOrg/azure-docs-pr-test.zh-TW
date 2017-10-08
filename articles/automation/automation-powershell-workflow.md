---
title: "Azure 自動化的 PowerShell 工作流程 aaaLearning |Microsoft 文件"
description: "本文旨在作為快速課程的作者熟悉 PowerShell 和 PowerShell 工作流程與概念適用 tooAutomation runbook 之間的 PowerShell toounderstand hello 特定差異。"
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
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a><span data-ttu-id="6d48e-103">了解適用於自動化 Runbook 的重要 Windows PowerShell 工作流程概念</span><span class="sxs-lookup"><span data-stu-id="6d48e-103">Learning key Windows PowerShell Workflow concepts for Automation runbooks</span></span> 
<span data-ttu-id="6d48e-104">Azure 自動化中的 Runbook 會實作為 Windows PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="6d48e-104">Runbooks in Azure Automation are implemented as Windows PowerShell Workflows.</span></span>  <span data-ttu-id="6d48e-105">Windows PowerShell 工作流程為類似 tooa Windows PowerShell 指令碼，但有一些顯著的差異可能會造成混淆的 tooa 新的使用者。</span><span class="sxs-lookup"><span data-stu-id="6d48e-105">A Windows PowerShell Workflow is similar tooa Windows PowerShell script but has some significant differences that can be confusing tooa new user.</span></span>  <span data-ttu-id="6d48e-106">您撰寫使用 PowerShell 工作流程 runbook 的預期的 toohelp 本文時，我們建議您撰寫使用 PowerShell，除非您需要檢查點的 runbook。</span><span class="sxs-lookup"><span data-stu-id="6d48e-106">While this article is intended toohelp you write runbooks using PowerShell workflow, we recommend you write runbooks using PowerShell unless you need checkpoints.</span></span>  <span data-ttu-id="6d48e-107">有幾個語法差異撰寫 PowerShell 工作流程 runbook 時，這些差異需要更多工作 toowrite 有效工作流程。</span><span class="sxs-lookup"><span data-stu-id="6d48e-107">There are several syntax differences when authoring PowerShell Workflow runbooks and these differences require a bit more work toowrite effective workflows.</span></span>  

<span data-ttu-id="6d48e-108">工作流程是一系列經過程式設計、 相互連結的步驟執行長時間執行工作，或需要多個裝置或受管理的節點上的 hello 協調多個步驟。</span><span class="sxs-lookup"><span data-stu-id="6d48e-108">A workflow is a sequence of programmed, connected steps that perform long-running tasks or require hello coordination of multiple steps across multiple devices or managed nodes.</span></span> <span data-ttu-id="6d48e-109">hello 一般指令碼工作流程的好處包括 hello 能力 toosimultaneously 執行多個裝置的動作和 hello 能力 tooautomatically 從失敗中復原。</span><span class="sxs-lookup"><span data-stu-id="6d48e-109">hello benefits of a workflow over a normal script include hello ability toosimultaneously perform an action against multiple devices and hello ability tooautomatically recover from failures.</span></span> <span data-ttu-id="6d48e-110">Windows PowerShell 工作流程是使用 Windows Workflow Foundation 的 Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6d48e-110">A Windows PowerShell Workflow is a Windows PowerShell script that uses Windows Workflow Foundation.</span></span> <span data-ttu-id="6d48e-111">雖然 hello 工作流程是使用 Windows PowerShell 語法撰寫，並由 Windows PowerShell 啟動，它會由 Windows Workflow Foundation 進行處理。</span><span class="sxs-lookup"><span data-stu-id="6d48e-111">While hello workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.</span></span>

<span data-ttu-id="6d48e-112">如這篇文章中的 hello 主題的詳細資訊，請參閱[開始使用 Windows PowerShell 工作流程](http://technet.microsoft.com/library/jj134242.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-112">For complete details on hello topics in this article, see [Getting Started with Windows PowerShell Workflow](http://technet.microsoft.com/library/jj134242.aspx).</span></span>

## <a name="basic-structure-of-a-workflow"></a><span data-ttu-id="6d48e-113">工作流程的基本結構</span><span class="sxs-lookup"><span data-stu-id="6d48e-113">Basic structure of a workflow</span></span>
<span data-ttu-id="6d48e-114">hello 第一個步驟 tooconverting PowerShell 指令碼 tooa PowerShell 工作流程括以 hello**工作流程**關鍵字。</span><span class="sxs-lookup"><span data-stu-id="6d48e-114">hello first step tooconverting a PowerShell script tooa PowerShell workflow is enclosing it with hello **Workflow** keyword.</span></span>  <span data-ttu-id="6d48e-115">工作流程啟動以 hello**工作流程**關鍵字後面接著括在大括弧的 hello 指令碼的 hello 主體。</span><span class="sxs-lookup"><span data-stu-id="6d48e-115">A workflow starts with hello **Workflow** keyword followed by hello body of hello script enclosed in braces.</span></span> <span data-ttu-id="6d48e-116">hello hello 工作流程名稱遵循 hello**工作流程**關鍵字 hello 語法如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d48e-116">hello name of hello workflow follows hello **Workflow** keyword as shown in hello following syntax:</span></span>

    Workflow Test-Workflow
    {
       <Commands>
    }

<span data-ttu-id="6d48e-117">hello hello 工作流程名稱必須符合 hello hello 自動化 runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="6d48e-117">hello name of hello workflow must match hello name of hello Automation runbook.</span></span> <span data-ttu-id="6d48e-118">如果正在匯入 hello runbook，則 hello 檔案名稱必須符合 hello 工作流程名稱，而且必須以結尾*.ps1*。</span><span class="sxs-lookup"><span data-stu-id="6d48e-118">If hello runbook is being imported, then hello filename must match hello workflow name and must end in *.ps1*.</span></span>

<span data-ttu-id="6d48e-119">tooadd 參數 toohello 工作流程，使用 hello **Param**關鍵字就像 tooa 指令碼一樣。</span><span class="sxs-lookup"><span data-stu-id="6d48e-119">tooadd parameters toohello workflow, use hello **Param** keyword just as you would tooa script.</span></span>

## <a name="code-changes"></a><span data-ttu-id="6d48e-120">程式碼變更</span><span class="sxs-lookup"><span data-stu-id="6d48e-120">Code changes</span></span>
<span data-ttu-id="6d48e-121">PowerShell 工作流程程式碼看起來幾乎完全相同的 tooPowerShell 指令碼，除了少數的重大變更。</span><span class="sxs-lookup"><span data-stu-id="6d48e-121">PowerShell workflow code looks almost identical tooPowerShell script code except for a few significant changes.</span></span>  <span data-ttu-id="6d48e-122">hello 下列各節描述您需要 toomake tooa PowerShell 指令碼為其 toorun 工作流程中的變更。</span><span class="sxs-lookup"><span data-stu-id="6d48e-122">hello following sections describe changes that you need toomake tooa PowerShell script for it toorun in a workflow.</span></span>

### <a name="activities"></a><span data-ttu-id="6d48e-123">活動</span><span class="sxs-lookup"><span data-stu-id="6d48e-123">Activities</span></span>
<span data-ttu-id="6d48e-124">活動是工作流程中的特定工作。</span><span class="sxs-lookup"><span data-stu-id="6d48e-124">An activity is a specific task in a workflow.</span></span> <span data-ttu-id="6d48e-125">就像指令碼是由一或多個命令所組成，工作流程是由序列中執行的一或多個活動所組成。</span><span class="sxs-lookup"><span data-stu-id="6d48e-125">Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence.</span></span> <span data-ttu-id="6d48e-126">Windows PowerShell 工作流程，自動轉換許多 Windows PowerShell cmdlet tooactivities hello 執行工作流程時。</span><span class="sxs-lookup"><span data-stu-id="6d48e-126">Windows PowerShell Workflow automatically converts many of hello Windows PowerShell cmdlets tooactivities when it runs a workflow.</span></span> <span data-ttu-id="6d48e-127">當您在 runbook 中指定其中一個指令程式時，hello 對應的活動是由 Windows Workflow Foundation 中執行。</span><span class="sxs-lookup"><span data-stu-id="6d48e-127">When you specify one of these cmdlets in your runbook, hello corresponding activity is run by Windows Workflow Foundation.</span></span> <span data-ttu-id="6d48e-128">針對沒有相應動作這些 cmdlet，Windows PowerShell 工作流程會自動執行中的 hello cmdlet [InlineScript](#inlinescript)活動。</span><span class="sxs-lookup"><span data-stu-id="6d48e-128">For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs hello cmdlet within an [InlineScript](#inlinescript) activity.</span></span> <span data-ttu-id="6d48e-129">有一組 Cmdlet 被排除，除非您明確在 InlineScript 區塊中將其納入，否則無法用在工作流程中。</span><span class="sxs-lookup"><span data-stu-id="6d48e-129">There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an InlineScript block.</span></span> <span data-ttu-id="6d48e-130">如需這些概念的詳細資訊，請參閱 [在指令碼工作流程中使用活動](http://technet.microsoft.com/library/jj574194.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-130">For further details on these concepts, see [Using Activities in Script Workflows](http://technet.microsoft.com/library/jj574194.aspx).</span></span>

<span data-ttu-id="6d48e-131">工作流程活動共用一組通用參數 tooconfigure 其作業。</span><span class="sxs-lookup"><span data-stu-id="6d48e-131">Workflow activities share a set of common parameters tooconfigure their operation.</span></span> <span data-ttu-id="6d48e-132">如需 hello 工作流程一般參數的詳細資訊，請參閱[about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-132">For details about hello workflow common parameters, see [about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx).</span></span>

### <a name="positional-parameters"></a><span data-ttu-id="6d48e-133">位置參數</span><span class="sxs-lookup"><span data-stu-id="6d48e-133">Positional parameters</span></span>
<span data-ttu-id="6d48e-134">您無法對活動和工作流程中的 Cmdlet 使用位置參數。</span><span class="sxs-lookup"><span data-stu-id="6d48e-134">You can't use positional parameters with activities and cmdlets in a workflow.</span></span>  <span data-ttu-id="6d48e-135">這都表示您必須使用參數名稱。</span><span class="sxs-lookup"><span data-stu-id="6d48e-135">All this means is that you must use parameter names.</span></span>

<span data-ttu-id="6d48e-136">例如，請考慮下列程式碼可取得所有執行中服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d48e-136">For example, consider hello following code that gets all running services.</span></span>

     Get-Service | Where-Object {$_.Status -eq "Running"}

<span data-ttu-id="6d48e-137">如果您嘗試 toorun 這個相同的程式碼工作流程中，您收到訊息像 「 無法使用指定的 hello 解析集參數具名參數 」。</span><span class="sxs-lookup"><span data-stu-id="6d48e-137">If you try toorun this same code in a workflow, you receive a message like "Parameter set cannot be resolved using hello specified named parameters."</span></span>  <span data-ttu-id="6d48e-138">toocorrect，提供 hello 參數名稱，如 hello 下列所示。</span><span class="sxs-lookup"><span data-stu-id="6d48e-138">toocorrect this, provide hello parameter name as in hello following.</span></span>

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a><span data-ttu-id="6d48e-139">已還原序列化的物件</span><span class="sxs-lookup"><span data-stu-id="6d48e-139">Deserialized objects</span></span>
<span data-ttu-id="6d48e-140">工作流程中的物件會還原序列化。</span><span class="sxs-lookup"><span data-stu-id="6d48e-140">Objects in workflows are deserialized.</span></span>  <span data-ttu-id="6d48e-141">這表示其屬性都仍然可用，而不是它們的方法。</span><span class="sxs-lookup"><span data-stu-id="6d48e-141">This means that their properties are still available, but not their methods.</span></span>  <span data-ttu-id="6d48e-142">例如，請考慮 hello 下列 PowerShell 程式碼會停止服務，使用 hello 停止方法的 hello 服務物件。</span><span class="sxs-lookup"><span data-stu-id="6d48e-142">For example, consider hello following PowerShell code that stops a service using hello Stop method of hello Service object.</span></span>

    $Service = Get-Service -Name MyService
    $Service.Stop()

<span data-ttu-id="6d48e-143">如果您嘗試 toorun 此工作流程中，您會收到的錯誤訊息 「 方法引動過程不支援在 Windows PowerShell 工作流程 」。</span><span class="sxs-lookup"><span data-stu-id="6d48e-143">If you try toorun this in a workflow, you receive an error saying "Method invocation is not supported in a Windows PowerShell Workflow."</span></span>  

<span data-ttu-id="6d48e-144">其中一個選項是 toowrap 這兩行程式中的程式碼[InlineScript](#inlinescript)封鎖在這種情況下 $Service 會 hello 區塊內的服務物件。</span><span class="sxs-lookup"><span data-stu-id="6d48e-144">One option is toowrap these two lines of code in an [InlineScript](#inlinescript) block in which case $Service would be a service object within hello block.</span></span>

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

<span data-ttu-id="6d48e-145">另一個選項是 toouse 執行的另一個 cmdlet hello 與 hello 方法相同的功能，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="6d48e-145">Another option is toouse another cmdlet that performs hello same functionality as hello method, if one is available.</span></span>  <span data-ttu-id="6d48e-146">在我們的範例，hello Stop-service cmdlet 提供 hello 與 hello 停止方法之外，相同的功能無法使用 hello 下列工作流程。</span><span class="sxs-lookup"><span data-stu-id="6d48e-146">In our sample, hello Stop-Service cmdlet provides hello same functionality as hello Stop method, and you could use hello following for a workflow.</span></span>

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a><span data-ttu-id="6d48e-147">InlineScript</span><span class="sxs-lookup"><span data-stu-id="6d48e-147">InlineScript</span></span>
<span data-ttu-id="6d48e-148">hello **InlineScript**活動時，您需要 toorun 一或多個命令做為傳統的 PowerShell 指令碼，而不是 PowerShell 工作流程。</span><span class="sxs-lookup"><span data-stu-id="6d48e-148">hello **InlineScript** activity is useful when you need toorun one or more commands as traditional PowerShell script instead of PowerShell workflow.</span></span>  <span data-ttu-id="6d48e-149">工作流程中的命令會傳送 tooWindows Workflow Foundation 進行處理，而 Windows PowerShell 會處理 InlineScript 區塊中的命令。</span><span class="sxs-lookup"><span data-stu-id="6d48e-149">While commands in a workflow are sent tooWindows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell.</span></span>

<span data-ttu-id="6d48e-150">InlineScript 會使用下列語法如下所示的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d48e-150">InlineScript uses hello following syntax shown below.</span></span>

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

<span data-ttu-id="6d48e-151">您可以從 InlineScript 傳回輸出，透過將 hello 輸出 tooa 變數指派。</span><span class="sxs-lookup"><span data-stu-id="6d48e-151">You can return output from an InlineScript by assigning hello output tooa variable.</span></span> <span data-ttu-id="6d48e-152">hello 下列範例會停止服務，並再將輸出 hello 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="6d48e-152">hello following example stops a service and then outputs hello service name.</span></span>

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


<span data-ttu-id="6d48e-153">您可以將值傳入 InlineScript 區塊，但必須使用 **$Using** 範圍修飾詞。</span><span class="sxs-lookup"><span data-stu-id="6d48e-153">You can pass values into an InlineScript block, but you must use **$Using** scope modifier.</span></span>  <span data-ttu-id="6d48e-154">hello 下列範例是相同的 toohello 前一個範例不同之處在於 hello 服務提供名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="6d48e-154">hello following example is identical toohello previous example except that hello service name is provided by a variable.</span></span>

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


<span data-ttu-id="6d48e-155">雖然 InlineScript 活動可以在特定工作流程中重要，它們不支援工作流程建構，並應該只用於時所需的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="6d48e-155">While InlineScript activities may be critical in certain workflows, they do not support workflow constructs and should only be used when necessary for hello following reasons:</span></span>

* <span data-ttu-id="6d48e-156">您不能在 InlineScript 區塊內使用[檢查點](#checkpoints)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-156">You cannot use [checkpoints](#checkpoints) inside an InlineScript block.</span></span> <span data-ttu-id="6d48e-157">如果 hello 區塊內發生失敗，它必須從 hello 區塊的 hello 開頭繼續。</span><span class="sxs-lookup"><span data-stu-id="6d48e-157">If a failure occurs within hello block, it must be resumed from hello beginning of hello block.</span></span>
* <span data-ttu-id="6d48e-158">您不能在 InlineScriptBlock 內使用[平行執行](#parallel-processing)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-158">You cannot use [parallel execution](#parallel-processing) inside an InlineScriptBlock.</span></span>
* <span data-ttu-id="6d48e-159">InlineScript 會影響 hello 工作流程的延展性，因為它會保留 hello hello hello InlineScript 區塊完整長度的 Windows PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6d48e-159">InlineScript affects scalability of hello workflow since it holds hello Windows PowerShell session for hello entire length of hello InlineScript block.</span></span>

<span data-ttu-id="6d48e-160">如需使用 InlineScript 的詳細資訊，請參閱[在工作流程中執行 Windows PowerShell 命令](http://technet.microsoft.com/library/jj574197.aspx)和 [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-160">For more information on using InlineScript, see [Running Windows PowerShell Commands in a Workflow](http://technet.microsoft.com/library/jj574197.aspx) and [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx).</span></span>

## <a name="parallel-processing"></a><span data-ttu-id="6d48e-161">平行處理</span><span class="sxs-lookup"><span data-stu-id="6d48e-161">Parallel processing</span></span>
<span data-ttu-id="6d48e-162">Windows PowerShell 工作流程的其中一個優點是 hello 能力 tooperform 一組命令，以平行方式，而不是以循序方式就如同一般的指令碼。</span><span class="sxs-lookup"><span data-stu-id="6d48e-162">One advantage of Windows PowerShell Workflows is hello ability tooperform a set of commands in parallel instead of sequentially as with a typical script.</span></span>

<span data-ttu-id="6d48e-163">您可以使用 hello**平行**關鍵字 toocreate 同時執行的多個命令與指令碼區塊。</span><span class="sxs-lookup"><span data-stu-id="6d48e-163">You can use hello **Parallel** keyword toocreate a script block with multiple commands that run concurrently.</span></span> <span data-ttu-id="6d48e-164">這會使用下列語法如下所示的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d48e-164">This uses hello following syntax shown below.</span></span> <span data-ttu-id="6d48e-165">在此情況下，Activity1 和 Activity2 開始 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="6d48e-165">In this case, Activity1 and Activity2 starts at hello same time.</span></span> <span data-ttu-id="6d48e-166">只有在 Activity1 和 Activity2 都已完成之後，Activity3 才會開始。</span><span class="sxs-lookup"><span data-stu-id="6d48e-166">Activity3 starts only after both Activity1 and Activity2 have completed.</span></span>

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


<span data-ttu-id="6d48e-167">例如，請考慮下列 PowerShell 命令，複製多個檔案 tooa 網路目的地的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d48e-167">For example, consider hello following PowerShell commands that copy multiple files tooa network destination.</span></span>  <span data-ttu-id="6d48e-168">這些命令會以循序方式執行，因此該檔案必須完成複製之前 hello 接下來會啟動。</span><span class="sxs-lookup"><span data-stu-id="6d48e-168">These commands are run sequentially so that one file must finish copying before hello next is started.</span></span>     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

<span data-ttu-id="6d48e-169">hello 下列工作流程來執行這些相同命令以平行方式，讓他們所有啟動複製 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="6d48e-169">hello following workflow runs these same commands in parallel so that they all start copying at hello same time.</span></span>  <span data-ttu-id="6d48e-170">它們只是所有之後複製 hello 完成訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6d48e-170">Only after they are all copied is hello completion message displayed.</span></span>

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


<span data-ttu-id="6d48e-171">您可以使用 hello **ForEach-Parallel**同時建構 tooprocess 命令，每個項目集合中。</span><span class="sxs-lookup"><span data-stu-id="6d48e-171">You can use hello **ForEach -Parallel** construct tooprocess commands for each item in a collection concurrently.</span></span> <span data-ttu-id="6d48e-172">hello hello 集合中的項目會處理以平行方式，而 hello 指令碼區塊中的 hello 命令以循序方式執行。</span><span class="sxs-lookup"><span data-stu-id="6d48e-172">hello items in hello collection are processed in parallel while hello commands in hello script block run sequentially.</span></span> <span data-ttu-id="6d48e-173">這會使用下列語法如下所示的 hello。</span><span class="sxs-lookup"><span data-stu-id="6d48e-173">This uses hello following syntax shown below.</span></span> <span data-ttu-id="6d48e-174">在此情況下，Activity1 啟動 hello 相同時間 hello 集合中的所有項目。</span><span class="sxs-lookup"><span data-stu-id="6d48e-174">In this case, Activity1 starts at hello same time for all items in hello collection.</span></span> <span data-ttu-id="6d48e-175">針對每個項目，Activity2 會在 Activity1 完成之後開始。</span><span class="sxs-lookup"><span data-stu-id="6d48e-175">For each item, Activity2 starts after Activity1 is complete.</span></span> <span data-ttu-id="6d48e-176">只有在 Activity1 和 Activity2 已完成所有項目之後，Activity3 才會開始。</span><span class="sxs-lookup"><span data-stu-id="6d48e-176">Activity3 starts only after both Activity1 and Activity2 have completed for all items.</span></span>

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

<span data-ttu-id="6d48e-177">下列範例中的 hello 是類似 toohello 上例平行複製檔案。</span><span class="sxs-lookup"><span data-stu-id="6d48e-177">hello following example is similar toohello previous example copying files in parallel.</span></span>  <span data-ttu-id="6d48e-178">在此情況下，複製之後會對每個檔案顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="6d48e-178">In this case, a message is displayed for each file after it copies.</span></span>  <span data-ttu-id="6d48e-179">它們只是所有之後完全複製 hello 最後完成的訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="6d48e-179">Only after they are all completely copied is hello final completion message displayed.</span></span>

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
> <span data-ttu-id="6d48e-180">我們不建議以平行方式執行子系 runbook，因為這已顯示 toogive 不可靠的結果。</span><span class="sxs-lookup"><span data-stu-id="6d48e-180">We do not recommend running child runbooks in parallel since this has been shown toogive unreliable results.</span></span>  <span data-ttu-id="6d48e-181">hello 有時 hello 子系 runbook 的輸出不會顯示，並設定一個子系 runbook 中的可能會影響 hello 其他平行子 runbook</span><span class="sxs-lookup"><span data-stu-id="6d48e-181">hello output from hello child runbook sometimes does not show up, and settings in one child runbook can affect hello other parallel child runbooks</span></span>
>

## <a name="checkpoints"></a><span data-ttu-id="6d48e-182">檢查點</span><span class="sxs-lookup"><span data-stu-id="6d48e-182">Checkpoints</span></span>
<span data-ttu-id="6d48e-183">A*檢查點*是 hello hello 工作流程包含 hello 目前變數值的目前狀態的快照集並將任何輸出產生的 toothat 點。</span><span class="sxs-lookup"><span data-stu-id="6d48e-183">A *checkpoint* is a snapshot of hello current state of hello workflow that includes hello current value for variables and any output generated toothat point.</span></span> <span data-ttu-id="6d48e-184">如果工作流程以錯誤結束，或已暫停，然後 hello 下一次執行它將會開始從其最後一個檢查點，而不是 hello 開頭 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="6d48e-184">If a workflow ends in error or is suspended, then hello next time it is run it will start from its last checkpoint instead of hello start of hello worfklow.</span></span>  <span data-ttu-id="6d48e-185">您可以在 hello 的工作流程中設定檢查點**Checkpoint-workflow**活動。</span><span class="sxs-lookup"><span data-stu-id="6d48e-185">You can set a checkpoint in a workflow with hello **Checkpoint-Workflow** activity.</span></span>

<span data-ttu-id="6d48e-186">在下列範例程式碼的 hello，Activity2 造成 hello tooend 工作流程之後，就會發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6d48e-186">In hello following sample code, an exception occurs after Activity2 causing hello workflow tooend.</span></span> <span data-ttu-id="6d48e-187">再次執行 hello 工作流程時，會從執行 Activity2 因為這是之後在 hello 最後一個檢查點設定。</span><span class="sxs-lookup"><span data-stu-id="6d48e-187">When hello workflow is run again, it starts by running Activity2 since this was just after hello last checkpoint set.</span></span>

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

<span data-ttu-id="6d48e-188">活動可能容易出錯的 tooexception 且不應重複如果繼續 hello 工作流程之後，您應該在工作流程中設定檢查點。</span><span class="sxs-lookup"><span data-stu-id="6d48e-188">You should set checkpoints in a workflow after activities that may be prone tooexception and should not be repeated if hello workflow is resumed.</span></span> <span data-ttu-id="6d48e-189">例如，您的工作流程可能會建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6d48e-189">For example, your workflow may create a virtual machine.</span></span> <span data-ttu-id="6d48e-190">您可以設定檢查點之前和之後 hello 命令 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6d48e-190">You could set a checkpoint both before and after hello commands toocreate hello virtual machine.</span></span> <span data-ttu-id="6d48e-191">如果 hello 建立失敗，然後 hello 命令可能會重複一次啟動 hello 工作流程時。</span><span class="sxs-lookup"><span data-stu-id="6d48e-191">If hello creation fails, then hello commands would be repeated if hello workflow is started again.</span></span> <span data-ttu-id="6d48e-192">如果 hello 工作失敗之後 hello 建立成功，然後 hello 虛擬機器將不會建立一次時繼續 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="6d48e-192">If hello worfklow fails after hello creation succeeds, then hello virtual machine will not be created again when hello workflow is resumed.</span></span>

<span data-ttu-id="6d48e-193">下列範例中的 hello 複製多個檔案 tooa 網路位置，並設定檢查點之後的每個檔案。</span><span class="sxs-lookup"><span data-stu-id="6d48e-193">hello following example copies multiple files tooa network location and sets a checkpoint after each file.</span></span>  <span data-ttu-id="6d48e-194">如果失去 hello 網路位置，則 hello 工作流程結束錯誤。</span><span class="sxs-lookup"><span data-stu-id="6d48e-194">If hello network location is lost, then hello workflow ends in error.</span></span>  <span data-ttu-id="6d48e-195">當重新啟動時，它將會繼續在 hello 最後一個檢查點，這表示只有 hello 已複製的檔案會略過。</span><span class="sxs-lookup"><span data-stu-id="6d48e-195">When it is started again, it will resume at hello last checkpoint meaning that only hello files that have already been copied are skipped.</span></span>

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

<span data-ttu-id="6d48e-196">因為使用者名稱認證不永久變更之後呼叫 hello [Suspend-workflow](https://technet.microsoft.com/library/jj733586.aspx)活動或 hello 最後一個檢查點之後, 您需要 tooset hello 認證 toonull，然後再擷取一次從 hello 資產存放區之後**暫停工作流程**或稱為檢查點。</span><span class="sxs-lookup"><span data-stu-id="6d48e-196">Because username credentials are not persisted after you call hello [Suspend-Workflow](https://technet.microsoft.com/library/jj733586.aspx) activity or after hello last checkpoint, you need tooset hello credentials toonull and then retrieve them again from hello asset store after **Suspend-Workflow** or checkpoint is called.</span></span>  <span data-ttu-id="6d48e-197">否則，您可能會收到下列錯誤訊息的 hello: *hello 工作流程工作無法繼續執行，可能是因為持續性資料無法完整地儲存或儲存持續性資料已損毀。您必須重新啟動 hello 工作流程。*</span><span class="sxs-lookup"><span data-stu-id="6d48e-197">Otherwise, you may receive hello following error message: *hello workflow job cannot be resumed, either because persistence data could not be saved completely, or saved persistence data has been corrupted. You must restart hello workflow.*</span></span>

<span data-ttu-id="6d48e-198">hello 遵循相同的程式碼示範如何 toohandle 這在您的 PowerShell 工作流程 runbook。</span><span class="sxs-lookup"><span data-stu-id="6d48e-198">hello following same code demonstrates how toohandle this in your PowerShell Workflow runbooks.</span></span>

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


<span data-ttu-id="6d48e-199">如果您使用以服務主體設定的執行身分帳戶進行驗證，則不必這麼做。</span><span class="sxs-lookup"><span data-stu-id="6d48e-199">This is not required if you are authenticating using a Run As account configured with a service principal.</span></span>  

<span data-ttu-id="6d48e-200">如需有關檢查點的詳細資訊，請參閱[新增檢查點 tooa 指令碼工作流程](http://technet.microsoft.com/library/jj574114.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d48e-200">For more information about checkpoints, see [Adding Checkpoints tooa Script Workflow](http://technet.microsoft.com/library/jj574114.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d48e-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d48e-201">Next steps</span></span>
* <span data-ttu-id="6d48e-202">tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="6d48e-202">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
