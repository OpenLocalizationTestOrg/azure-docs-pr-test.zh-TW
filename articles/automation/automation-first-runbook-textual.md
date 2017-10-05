---
title: "我在 Azure 自動化中的第一個 PowerShell 工作流程 Runbook | Microsoft Docs"
description: "本教學課程逐步引導您使用 PowerShell 工作流程建立、測試和發佈簡單的文字 Runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "powershell 工作流程, powershell 工作流程範例, 工作流程 powershell"
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 739f7c0fe0cca03d80fa8b4bdadbf93b5da72a73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="my-first-powershell-workflow-runbook"></a><span data-ttu-id="45b4d-104">我的第一個 PowerShell 工作流程 Runbook</span><span class="sxs-lookup"><span data-stu-id="45b4d-104">My first PowerShell Workflow runbook</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="45b4d-105">圖形化</span><span class="sxs-lookup"><span data-stu-id="45b4d-105">Graphical</span></span>](automation-first-runbook-graphical.md)
> * [<span data-ttu-id="45b4d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45b4d-106">PowerShell</span></span>](automation-first-runbook-textual-powershell.md)
> * [<span data-ttu-id="45b4d-107">PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="45b4d-107">PowerShell Workflow</span></span>](automation-first-runbook-textual.md)
> 
> 

<span data-ttu-id="45b4d-108">本教學課程將逐步引導您在 Azure 自動化中建立 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="45b4d-108">This tutorial walks you through the creation of a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks) in Azure Automation.</span></span> <span data-ttu-id="45b4d-109">我們先從測試和發佈的簡單 Runbook 開始，同時說明如何追蹤 Runbook 作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="45b4d-109">We start with a simple runbook that we test and publish while explaining how to track the status of the runbook job.</span></span> <span data-ttu-id="45b4d-110">接著我們會修改 Runbook 以實際管理 Azure 資源，在此情況下會啟動 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45b4d-110">Then we modify the runbook to actually manage Azure resources, in this case starting an Azure virtual machine.</span></span> <span data-ttu-id="45b4d-111">最後我們會藉由新增 Runbook 參數，讓 Runbook 更穩固。</span><span class="sxs-lookup"><span data-stu-id="45b4d-111">Lastly we make the runbook more robust by adding runbook parameters.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45b4d-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="45b4d-112">Prerequisites</span></span>
<span data-ttu-id="45b4d-113">若要完成本教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="45b4d-113">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="45b4d-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="45b4d-114">Azure subscription.</span></span> <span data-ttu-id="45b4d-115">如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="45b4d-115">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="45b4d-116">[自動化帳戶](automation-sec-configure-azure-runas-account.md) ，用來保存 Runbook 以及向 Azure 資源驗證。</span><span class="sxs-lookup"><span data-stu-id="45b4d-116">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="45b4d-117">此帳戶必須擁有啟動和停止虛擬機器的權限。</span><span class="sxs-lookup"><span data-stu-id="45b4d-117">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="45b4d-118">Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45b4d-118">An Azure virtual machine.</span></span> <span data-ttu-id="45b4d-119">我們會停止並啟動這部電腦，因此它不該是生產 VM。</span><span class="sxs-lookup"><span data-stu-id="45b4d-119">We stop and start this machine so it should not be a production VM.</span></span>

## <a name="step-1---create-new-runbook"></a><span data-ttu-id="45b4d-120">步驟 1 - 建立新的 Runbook</span><span class="sxs-lookup"><span data-stu-id="45b4d-120">Step 1 - Create new runbook</span></span>
<span data-ttu-id="45b4d-121">我們將藉由建立一個輸出文字「Hello World」 的簡單 Runbook 開始。</span><span class="sxs-lookup"><span data-stu-id="45b4d-121">We'll start by creating a simple runbook that outputs the text *Hello World*.</span></span>

1. <span data-ttu-id="45b4d-122">在 Azure 入口網站中，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="45b4d-122">In the Azure portal, open your Automation account.</span></span>  
   <span data-ttu-id="45b4d-123">[自動化帳戶] 頁面提供這個帳戶中資源的快速檢視。</span><span class="sxs-lookup"><span data-stu-id="45b4d-123">The Automation account page gives you a quick view of the resources in this account.</span></span> <span data-ttu-id="45b4d-124">您應該已經有一些資產。</span><span class="sxs-lookup"><span data-stu-id="45b4d-124">You should already have some assets.</span></span> <span data-ttu-id="45b4d-125">其中大部分是會自動包含在新自動化帳戶的模組。</span><span class="sxs-lookup"><span data-stu-id="45b4d-125">Most of those are the modules that are automatically included in a new Automation account.</span></span> <span data-ttu-id="45b4d-126">您應該也擁有 [必要條件](#prerequisites)中所述的認證資產。</span><span class="sxs-lookup"><span data-stu-id="45b4d-126">You should also have the Credential asset that's mentioned in the [prerequisites](#prerequisites).</span></span>
2. <span data-ttu-id="45b4d-127">按一下 [Runbook]  磚以開啟 Runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="45b4d-127">Click on the **Runbooks** tile to open the list of runbooks.</span></span><br><br> <span data-ttu-id="45b4d-128">![Runbook 控制項](media/automation-first-runbook-textual/runbooks-control-tiles.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-128">![Runbooks control](media/automation-first-runbook-textual/runbooks-control-tiles.png)</span></span>
3. <span data-ttu-id="45b4d-129">按一下 [新增 Runbook] 按鈕，然後按一下 [建立新的 Runbook] 來建立新的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-129">Create a new runbook by clicking on the **Add a runbook** button and then **Create a new runbook**.</span></span>
4. <span data-ttu-id="45b4d-130">將 Runbook 命名為「MyFirstRunbook-Workflow」 。</span><span class="sxs-lookup"><span data-stu-id="45b4d-130">Give the runbook the name *MyFirstRunbook-Workflow*.</span></span>
5. <span data-ttu-id="45b4d-131">在此情況下，我們要建立 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)，因此請選取 [PowerShell 工作流程] 作為 [Runbook 類型]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-131">In this case, we're going to create a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks) so select **Powershell Workflow** for **Runbook type**.</span></span><br><br> <span data-ttu-id="45b4d-132">![新的 Runbook](media/automation-first-runbook-textual/new-runbook-properties.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-132">![New runbook](media/automation-first-runbook-textual/new-runbook-properties.png)</span></span>
6. <span data-ttu-id="45b4d-133">按一下 [建立]  來建立 Runbook 並開啟文字式編輯器。</span><span class="sxs-lookup"><span data-stu-id="45b4d-133">Click **Create** to create the runbook and open the textual editor.</span></span>

## <a name="step-2---add-code-to-the-runbook"></a><span data-ttu-id="45b4d-134">步驟 2 - 將程式碼加入至 runbook</span><span class="sxs-lookup"><span data-stu-id="45b4d-134">Step 2 - Add code to the runbook</span></span>
<span data-ttu-id="45b4d-135">您可以直接將程式碼輸入到 runbook 中，或從程式庫控制項選取 cmdlet、runbook 和資產，並利用任何相關的參數將它們加入至 runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-135">You can either type code directly into the runbook, or you can select cmdlets, runbooks, and assets from the Library control and have them added to the runbook with any related parameters.</span></span> <span data-ttu-id="45b4d-136">在此逐步解說中，我們將直接輸入至 runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-136">For this walkthrough, we'll type directly into the runbook.</span></span>

1. <span data-ttu-id="45b4d-137">我們的 runbook 目前是空白的，只有必要的「工作流程」  關鍵字、runbook 名稱以及將括住整個工作流程的大括弧。</span><span class="sxs-lookup"><span data-stu-id="45b4d-137">Our runbook is currently empty with only the required *workflow* keyword, the name of our runbook, and the braces that will encase the entire workflow.</span></span>

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. <span data-ttu-id="45b4d-138">在括號之間輸入「」 </span><span class="sxs-lookup"><span data-stu-id="45b4d-138">Type *Write-Output "Hello World."*</span></span> <span data-ttu-id="45b4d-139">。</span><span class="sxs-lookup"><span data-stu-id="45b4d-139">between the braces.</span></span>

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. <span data-ttu-id="45b4d-140">按一下 [儲存] 來儲存 Runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-140">Save the runbook by clicking **Save**.</span></span><br><br> <span data-ttu-id="45b4d-141">![儲存 Runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-141">![Save runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)</span></span>

## <a name="step-3---test-the-runbook"></a><span data-ttu-id="45b4d-142">步驟 3 - 測試 Runbook</span><span class="sxs-lookup"><span data-stu-id="45b4d-142">Step 3 - Test the runbook</span></span>
<span data-ttu-id="45b4d-143">在我們發佈 Runbook 之前，為了使其可用於生產環境，我們想要測試以確定它可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="45b4d-143">Before we publish the runbook to make it available in production, we want to test it to make sure that it works properly.</span></span> <span data-ttu-id="45b4d-144">測試 Runbook 時，您會執行其 **草稿** 版本，並以互動方式檢視其輸出。</span><span class="sxs-lookup"><span data-stu-id="45b4d-144">When you test a runbook, you run its **Draft** version and view its output interactively.</span></span>

1. <span data-ttu-id="45b4d-145">按一下 [測試窗格]  來開啟 [測試] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-145">Click **Test pane** to open the Test pane.</span></span><br><br> <span data-ttu-id="45b4d-146">![](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-146">![Test pane](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)</span></span>
2. <span data-ttu-id="45b4d-147">按一下 [開始]  以開始測試。</span><span class="sxs-lookup"><span data-stu-id="45b4d-147">Click **Start** to start the test.</span></span> <span data-ttu-id="45b4d-148">這應該是唯一啟用的選項。</span><span class="sxs-lookup"><span data-stu-id="45b4d-148">This should be the only enabled option.</span></span>
3. <span data-ttu-id="45b4d-149">隨即會建立 [Runbook 工作](automation-runbook-execution.md) ，並顯示其狀態。</span><span class="sxs-lookup"><span data-stu-id="45b4d-149">A [runbook job](automation-runbook-execution.md) is created and its status displayed.</span></span>  
   <span data-ttu-id="45b4d-150">工作狀態會從「已排入佇列」  開始，表示等候雲端中的 Runbook 背景工作可供使用。</span><span class="sxs-lookup"><span data-stu-id="45b4d-150">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to come available.</span></span> <span data-ttu-id="45b4d-151">然後當背景工作宣告該工作時，狀態將變更為 [正在開始]，然後 Runbook 實際開始執行時再變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-151">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  
4. <span data-ttu-id="45b4d-152">Runbook 工作完成時，會顯示其輸出。</span><span class="sxs-lookup"><span data-stu-id="45b4d-152">When the runbook job completes, its output is displayed.</span></span> <span data-ttu-id="45b4d-153">在我們的情況中，我們應該會看到 Hello World。</span><span class="sxs-lookup"><span data-stu-id="45b4d-153">In our case, we should see *Hello World*.</span></span><br><br> <span data-ttu-id="45b4d-154">![](media/automation-first-runbook-textual/test-output-hello-world.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-154">![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)</span></span>
5. <span data-ttu-id="45b4d-155">關閉 [測試] 窗格以返回畫布。</span><span class="sxs-lookup"><span data-stu-id="45b4d-155">Close the Test pane to return to the canvas.</span></span>

## <a name="step-4---publish-and-start-the-runbook"></a><span data-ttu-id="45b4d-156">步驟 4 - 發佈和啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="45b4d-156">Step 4 - Publish and start the runbook</span></span>
<span data-ttu-id="45b4d-157">我們剛剛建立的 Runbook 仍處於草稿模式。</span><span class="sxs-lookup"><span data-stu-id="45b4d-157">The runbook that we just created is still in Draft mode.</span></span> <span data-ttu-id="45b4d-158">我們需要將它發佈，才能在生產環境中執行它。</span><span class="sxs-lookup"><span data-stu-id="45b4d-158">We need to publish it before we can run it in production.</span></span> <span data-ttu-id="45b4d-159">當您發佈 Runbook 時，您會使用草稿版本覆寫現有的已發佈版本。</span><span class="sxs-lookup"><span data-stu-id="45b4d-159">When you publish a runbook, you overwrite the existing Published version with the Draft version.</span></span> <span data-ttu-id="45b4d-160">在我們的情況中，因為我們剛剛建立 Runbook，因此還沒有已發佈版本。</span><span class="sxs-lookup"><span data-stu-id="45b4d-160">In our case, we don't have a Published version yet because we just created the runbook.</span></span>

1. <span data-ttu-id="45b4d-161">按一下 [發佈] 來發佈 Runbook，然後出現提示時按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-161">Click **Publish** to publish the runbook and then **Yes** when prompted.</span></span><br><br> <span data-ttu-id="45b4d-162">![](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-162">![Publish](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)</span></span>
2. <span data-ttu-id="45b4d-163">如果您現在向左捲動以檢視 [Runbook] 窗格中的 Runbook，它會顯示 [已發佈] 的 [撰寫狀態]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-163">If you scroll left to view the runbook in the **Runbooks** pane now, it will show an **Authoring Status** of **Published**.</span></span>
3. <span data-ttu-id="45b4d-164">捲動回到右側，檢視 **MyFirstRunbook-Workflow**的窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-164">Scroll back to the right to view the pane for **MyFirstRunbook-Workflow**.</span></span>  
   <span data-ttu-id="45b4d-165">在頂端的選項可讓我們啟動 Runbook、排程它在未來的某個時間點啟動，或建立 [webhook](automation-webhooks.md) ，使得可以透過 HTTP 呼叫啟動它。</span><span class="sxs-lookup"><span data-stu-id="45b4d-165">The options across the top allow us to start the runbook, schedule it to start at some time in the future, or create a [webhook](automation-webhooks.md) so it can be started through an HTTP call.</span></span>
4. <span data-ttu-id="45b4d-166">我們只想要啟動 Runbook，因此按一下 [開始]，然後在提示出現時按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-166">We just want to start the runbook so click **Start** and then **Yes** when prompted.</span></span><br><br> <span data-ttu-id="45b4d-167">![啟動 Runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-167">![Start runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)</span></span>
5. <span data-ttu-id="45b4d-168">工作窗格會開啟我們剛剛建立的 Runbook 工作。</span><span class="sxs-lookup"><span data-stu-id="45b4d-168">A job pane is opened for the runbook job that we just created.</span></span> <span data-ttu-id="45b4d-169">我們可以關閉此窗格，但在此情況下，我們要將它開啟，使得我們可以觀看工作的進度。</span><span class="sxs-lookup"><span data-stu-id="45b4d-169">We can close this pane, but in this case we'll leave it open so we can watch the job's progress.</span></span>
6. <span data-ttu-id="45b4d-170">[作業摘要]  中會顯示作業狀態，且符合當我們測試 Runbook 時看到的狀態。</span><span class="sxs-lookup"><span data-stu-id="45b4d-170">The job status is shown in **Job Summary** and matches the statuses that we saw when we tested the runbook.</span></span><br><br> <span data-ttu-id="45b4d-171">![工作摘要](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-171">![Job Summary](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)</span></span>
7. <span data-ttu-id="45b4d-172">一旦 Runbook 狀態顯示 [已完成]，請按一下 [輸出]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-172">Once the runbook status shows *Completed*, click **Output**.</span></span> <span data-ttu-id="45b4d-173">[輸出] 窗格會開啟，而且可以看到我們的「Hello World」 。</span><span class="sxs-lookup"><span data-stu-id="45b4d-173">The Output pane is opened, and we can see our *Hello World*.</span></span><br><br> <span data-ttu-id="45b4d-174">![工作摘要](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-174">![Job Summary](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)</span></span>  
8. <span data-ttu-id="45b4d-175">關閉 [輸出] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-175">Close the Output pane.</span></span>
9. <span data-ttu-id="45b4d-176">按一下 [所有記錄檔]  以開啟 Runbook 作業的 [資料流] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-176">Click **All Logs** to open the Streams pane for the runbook job.</span></span> <span data-ttu-id="45b4d-177">我們應該只會在輸出資料流中看到「Hello World」  ，但可能也會顯示 Runbook 作業的其他資料流，例如 Runbook 寫入時發生的詳細資訊和錯誤。</span><span class="sxs-lookup"><span data-stu-id="45b4d-177">We should only see *Hello World* in the output stream, but this can show other streams for a runbook job such as Verbose and Error if the runbook writes to them.</span></span><br><br> <span data-ttu-id="45b4d-178">![工作摘要](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-178">![Job Summary](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)</span></span>
10. <span data-ttu-id="45b4d-179">關閉 [資料流] 窗格和 [工作] 窗格，以返回 MyFirstRunbook 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-179">Close the Streams pane and the Job pane to return to the MyFirstRunbook pane.</span></span>
11. <span data-ttu-id="45b4d-180">按一下 [作業]  以開啟此 Runbook 的 [工作] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-180">Click **Jobs** to open the Jobs pane for this runbook.</span></span> <span data-ttu-id="45b4d-181">這樣會列出此 Runbook 所建立的所有工作。</span><span class="sxs-lookup"><span data-stu-id="45b4d-181">This lists all of the jobs created by this runbook.</span></span> <span data-ttu-id="45b4d-182">由於我們只執行一次作業，因此應該只會看到列出一項作業。</span><span class="sxs-lookup"><span data-stu-id="45b4d-182">We should only see one job listed since we only ran the job once.</span></span><br><br> <span data-ttu-id="45b4d-183">![作業](media/automation-first-runbook-textual/runbook-control-job-tile.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-183">![Jobs](media/automation-first-runbook-textual/runbook-control-job-tile.png)</span></span>
12. <span data-ttu-id="45b4d-184">您可以按一下此工作以開啟我們啟動 Runbook 時所檢視的相同 [工作] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-184">You can click on this job to open the same Job pane that we viewed when we started the runbook.</span></span> <span data-ttu-id="45b4d-185">這可讓您回到過去的時間並檢視針對特定 Runbook 所建立的任何工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="45b4d-185">This allows you to go back in time and view the details of any job that was created for a particular runbook.</span></span>

## <a name="step-5---add-authentication-to-manage-azure-resources"></a><span data-ttu-id="45b4d-186">步驟 5 - 加入驗證來管理 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="45b4d-186">Step 5 - Add authentication to manage Azure resources</span></span>
<span data-ttu-id="45b4d-187">我們已經測試並發行我們 Runbook，但是到目前為止，它似乎並不實用。</span><span class="sxs-lookup"><span data-stu-id="45b4d-187">We've tested and published our runbook, but so far it doesn't do anything useful.</span></span> <span data-ttu-id="45b4d-188">我們想要讓它管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="45b4d-188">We want to have it manage Azure resources.</span></span> <span data-ttu-id="45b4d-189">不過它無法辦到這點，除非我們使用在 [必要條件](#prerequisites)中提及的認證對其進行驗證。</span><span class="sxs-lookup"><span data-stu-id="45b4d-189">It won't be able to do that though unless we have it authenticate using the credentials that are referred to in the [prerequisites](#prerequisites).</span></span> <span data-ttu-id="45b4d-190">我們會利用 **Add-AzureRMAccount** Cmdlet 來執行。</span><span class="sxs-lookup"><span data-stu-id="45b4d-190">We do that with the **Add-AzureRMAccount** cmdlet.</span></span>

1. <span data-ttu-id="45b4d-191">按一下 MyFirstRunbook-Workflow 窗格上的 [編輯] 以開啟文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="45b4d-191">Open the textual editor by clicking **Edit** on the MyFirstRunbook-Workflow pane.</span></span><br><br> <span data-ttu-id="45b4d-192">![編輯 Runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-192">![Edit runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)</span></span>
2. <span data-ttu-id="45b4d-193">我們不再需要 **Write-Output** 行，因此可以放心刪除。</span><span class="sxs-lookup"><span data-stu-id="45b4d-193">We don't need the **Write-Output** line anymore, so go ahead and delete it.</span></span>
3. <span data-ttu-id="45b4d-194">將游標放在大括弧之間的空白行。</span><span class="sxs-lookup"><span data-stu-id="45b4d-194">Position the cursor on a blank line between the braces.</span></span>
4. <span data-ttu-id="45b4d-195">輸入或是複製並貼上下列程式碼，此程式碼會處理您的自動化執行身分帳戶的驗證︰</span><span class="sxs-lookup"><span data-stu-id="45b4d-195">Type or copy and paste the following code that will handle the authentication with your Automation Run As account:</span></span>

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. <span data-ttu-id="45b4d-196">按一下 [測試]  窗格，我們便可以測試 Runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-196">Click **Test pane** so that we can test the runbook.</span></span>
6. <span data-ttu-id="45b4d-197">按一下 [開始]  以開始測試。</span><span class="sxs-lookup"><span data-stu-id="45b4d-197">Click **Start** to start the test.</span></span> <span data-ttu-id="45b4d-198">測試完成時，您應該會從帳戶收到如同以下顯示基本資訊的輸出。</span><span class="sxs-lookup"><span data-stu-id="45b4d-198">Once it completes, you should receive output similar to the following, displaying basic information from your account.</span></span> <span data-ttu-id="45b4d-199">這可確認認證有效。</span><span class="sxs-lookup"><span data-stu-id="45b4d-199">This confirms that the credential is valid.</span></span><br><br> <span data-ttu-id="45b4d-200">![驗證](media/automation-first-runbook-textual/runbook-auth-output.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-200">![Authenticate](media/automation-first-runbook-textual/runbook-auth-output.png)</span></span>

## <a name="step-6---add-code-to-start-a-virtual-machine"></a><span data-ttu-id="45b4d-201">步驟 6 - 加入程式碼以啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="45b4d-201">Step 6 - Add code to start a virtual machine</span></span>
<span data-ttu-id="45b4d-202">由於我們的 runbook 正在驗證我們的 Azure 訂用帳戶，所以我們可以管理資源。</span><span class="sxs-lookup"><span data-stu-id="45b4d-202">Now that our runbook is authenticating to our Azure subscription, we can manage resources.</span></span> <span data-ttu-id="45b4d-203">我們會新增一個命令以啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45b4d-203">We add a command to start a virtual machine.</span></span> <span data-ttu-id="45b4d-204">您可以在您的 Azure 訂用帳戶中挑選任何虛擬機器，而現在我們會在 Runbook 中將該名稱硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="45b4d-204">You can pick any virtual machine in your Azure subscription, and for now we will be hardcoding that name in the runbook.</span></span>

1. <span data-ttu-id="45b4d-205">在 Add-AzureRmAccount 後面輸入 Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'NameofResourceGroup'，提供要啟動之虛擬機器的名稱和資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="45b4d-205">After *Add-AzureRmAccount*, type *Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'NameofResourceGroup'* providing the name and Resource Group name of the virtual machine to start.</span></span>  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. <span data-ttu-id="45b4d-206">儲存 Runbook，然後按一下 [測試]  窗格，我們便能加以測試。</span><span class="sxs-lookup"><span data-stu-id="45b4d-206">Save the runbook and then click **Test pane** so that we can test it.</span></span>
3. <span data-ttu-id="45b4d-207">按一下 [開始]  以開始測試。</span><span class="sxs-lookup"><span data-stu-id="45b4d-207">Click **Start** to start the test.</span></span> <span data-ttu-id="45b4d-208">當它完成時，請檢查虛擬機器已啟動。</span><span class="sxs-lookup"><span data-stu-id="45b4d-208">Once it completes, check that the virtual machine was started.</span></span>

## <a name="step-7---add-an-input-parameter-to-the-runbook"></a><span data-ttu-id="45b4d-209">步驟 7 - 將輸入參數加入至 Runbook</span><span class="sxs-lookup"><span data-stu-id="45b4d-209">Step 7 - Add an input parameter to the runbook</span></span>
<span data-ttu-id="45b4d-210">我們的 Runbook 目前會啟動我們在 runbook 中硬式編碼的虛擬機器，但如果可以在啟動 runbook 時指定虛擬機器，它會更有用。</span><span class="sxs-lookup"><span data-stu-id="45b4d-210">Our runbook currently starts the virtual machine that we hardcoded in the runbook, but it would be more useful if we could specify the virtual machine when the runbook is started.</span></span> <span data-ttu-id="45b4d-211">我們現在會將輸入參數加入 Runbook，以提供該功能。</span><span class="sxs-lookup"><span data-stu-id="45b4d-211">We will now add input parameters to the runbook to provide that functionality.</span></span>

1. <span data-ttu-id="45b4d-212">如下列範例所示，將 [VMName] 和 [ResourceGroupName] 的參數新增至 Runbook，並搭配使用這些變數與 **Start-AzureRmVM** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="45b4d-212">Add parameters for *VMName* and *ResourceGroupName* to the runbook and use these variables with the **Start-AzureRmVM** cmdlet as in the example below.</span></span>

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. <span data-ttu-id="45b4d-213">儲存 Runbook 並開啟 [測試] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-213">Save the runbook and open the Test pane.</span></span> <span data-ttu-id="45b4d-214">請注意，您現在可以提供測試中將使用的兩個輸入變數的值。</span><span class="sxs-lookup"><span data-stu-id="45b4d-214">Note that you can now provide values for the two input variables that will be used in the test.</span></span>
3. <span data-ttu-id="45b4d-215">關閉 [測試] 窗格。</span><span class="sxs-lookup"><span data-stu-id="45b4d-215">Close the Test pane.</span></span>
4. <span data-ttu-id="45b4d-216">按一下 [發佈]  來發行新版本的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-216">Click **Publish** to publish the new version of the runbook.</span></span>
5. <span data-ttu-id="45b4d-217">停止您在上一個步驟中啟動的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45b4d-217">Stop the virtual machine that you started in the previous step.</span></span>
6. <span data-ttu-id="45b4d-218">按一下 [開始]  以啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="45b4d-218">Click **Start** to start the runbook.</span></span> <span data-ttu-id="45b4d-219">輸入您要啟動之虛擬機器的 [VMName] 和 [ResourceGroupName]。</span><span class="sxs-lookup"><span data-stu-id="45b4d-219">Type in the **VMName** and **ResourceGroupName** for the virtual machine that you're going to start.</span></span><br><br> <span data-ttu-id="45b4d-220">![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)</span><span class="sxs-lookup"><span data-stu-id="45b4d-220">![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)</span></span><br>  
7. <span data-ttu-id="45b4d-221">Runbook 完成時，請檢查虛擬機器已啟動。</span><span class="sxs-lookup"><span data-stu-id="45b4d-221">When the runbook completes, check that the virtual machine was started.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="45b4d-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45b4d-222">Next steps</span></span>
* <span data-ttu-id="45b4d-223">若要開始使用圖形化 Runbook，請參閱 [我的第一個圖形化 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="45b4d-223">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="45b4d-224">若要開始使用 PowerShell Runbook，請參閱 [我的第一個 PowerShell Runbook](automation-first-runbook-textual-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="45b4d-224">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md)</span></span>
* <span data-ttu-id="45b4d-225">若要深入了解 Runbook 類型、其優點和限制，請參閱 [Azure 自動化 Runbook 類型](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="45b4d-225">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
* <span data-ttu-id="45b4d-226">如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span><span class="sxs-lookup"><span data-stu-id="45b4d-226">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span></span>
