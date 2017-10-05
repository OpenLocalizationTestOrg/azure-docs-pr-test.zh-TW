---
title: "在 Azure 自動化中建立或匯入 Runbook"
description: "本文說明如何在 Azure 自動化中建立新的 Runbook，或從檔案匯入新的 Runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 0264de12caaf62e976673a423df731ad27ab01e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a><span data-ttu-id="32b97-103">在 Azure 自動化中建立或匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-103">Creating or importing a runbook in Azure Automation</span></span>
<span data-ttu-id="32b97-104">您可以將 Runbook 新增至 Azure 自動化，方法是[建立新的](#creating-a-new-runbook)，或是從檔案或 [Runbook 資源庫](automation-runbook-gallery.md)匯入現有 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-104">You can add a runbook to Azure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from the [Runbook Gallery](automation-runbook-gallery.md).</span></span> <span data-ttu-id="32b97-105">本文提供從檔案建立和匯入 Runbook 的資訊。</span><span class="sxs-lookup"><span data-stu-id="32b97-105">This article provides information on creating and importing runbooks from a file.</span></span>  <span data-ttu-id="32b97-106">您可以在 [Azure 自動化的 Runbook 和模組資源庫](automation-runbook-gallery.md)中取得有關存取社群 Runbook 和模組的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32b97-106">You can get all of the details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>

## <a name="creating-a-new-runbook"></a><span data-ttu-id="32b97-107">建立新的 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-107">Creating a new runbook</span></span>
<span data-ttu-id="32b97-108">您可以使用其中一個 Azure 入口網站或 Windows PowerShell，在 Azure 自動化中建立新的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-108">You can create a new runbook in Azure Automation using one of the Azure portals or Windows PowerShell.</span></span> <span data-ttu-id="32b97-109">一旦建立 Runbook 之後，您就能使用[了解 PowerShell 工作流程](automation-powershell-workflow.md)和 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)中的資訊來編輯它。</span><span class="sxs-lookup"><span data-stu-id="32b97-109">Once the runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md) and [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="32b97-110">使用 Azure 傳統入口網站建立新的 Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-110">To create a new Azure Automation runbook with the Azure Classic portal</span></span>
<span data-ttu-id="32b97-111">您只能在 Azure 入口網站中使用 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 。</span><span class="sxs-lookup"><span data-stu-id="32b97-111">You can only work with [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks) in the Azure portal.</span></span>

1. <span data-ttu-id="32b97-112">在 Azure 傳統入口網站中，按一下 [新增]、[應用程式服務]、[自動化]、[Runbook]、[快速建立]。</span><span class="sxs-lookup"><span data-stu-id="32b97-112">In the Azure Classic portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.</span></span>
2. <span data-ttu-id="32b97-113">輸入必要資訊，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="32b97-113">Enter the required information, and then click **Create**.</span></span> <span data-ttu-id="32b97-114">Runbook 名稱必須以字母開頭，可以具有字母、數字、底線和連字號。</span><span class="sxs-lookup"><span data-stu-id="32b97-114">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
3. <span data-ttu-id="32b97-115">如果您想要立即編輯 Runbook，則按一下 [編輯 Runbook] 。</span><span class="sxs-lookup"><span data-stu-id="32b97-115">If you want to edit the runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="32b97-116">否則，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="32b97-116">Otherwise, click **OK**.</span></span>
4. <span data-ttu-id="32b97-117">新的 Runbook 會出現在 [Runbook]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="32b97-117">Your new runbook will appear on the **Runbooks** tab.</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-the-azure-portal"></a><span data-ttu-id="32b97-118">使用 Azure 入口網站建立新的 Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-118">To create a new Azure Automation runbook with the Azure portal</span></span>
1. <span data-ttu-id="32b97-119">在 Azure 入口網站中，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="32b97-119">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="32b97-120">從 [中樞] 選取 [Runbook] 以開啟 Runbook 清單。</span><span class="sxs-lookup"><span data-stu-id="32b97-120">From the Hub, select **Runbooks** to open the list of runbooks.</span></span>
3. <span data-ttu-id="32b97-121">按一下 [加入 Runbook] 按鈕，然後按一下 [建立新的 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="32b97-121">Click on the **Add a runbook** button and then **Create a new runbook**.</span></span>
4. <span data-ttu-id="32b97-122">輸入 Runbook 的 [名稱]  ，然後選取其 [類型](automation-runbook-types.md)。</span><span class="sxs-lookup"><span data-stu-id="32b97-122">Type a **Name** for the runbook and select its [Type](automation-runbook-types.md).</span></span> <span data-ttu-id="32b97-123">Runbook 名稱必須以字母開頭，可以具有字母、數字、底線和連字號。</span><span class="sxs-lookup"><span data-stu-id="32b97-123">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
5. <span data-ttu-id="32b97-124">按一下 [建立]  來建立 Runbook 並開啟編輯器。</span><span class="sxs-lookup"><span data-stu-id="32b97-124">Click **Create** to create the runbook and open the editor.</span></span>

### <a name="to-create-a-new-azure-automation-runbook-with-windows-powershell"></a><span data-ttu-id="32b97-125">使用 Windows PowerShell 建立新的 Azure 自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-125">To create a new Azure Automation runbook with Windows PowerShell</span></span>
<span data-ttu-id="32b97-126">您可以使用 [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) Cmdlet，建立空的 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="32b97-126">You can use the [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet to create an empty [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="32b97-127">您可以指定 **Name** 參數來建立空白 Runbook，您稍後可加以編輯，或者您可以指定 **Path** 參數以匯入 Runbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="32b97-127">You can either specify the **Name** parameter to create an empty runbook that you can later edit, or you can specify the **Path** parameter to import a runbook file.</span></span> <span data-ttu-id="32b97-128">您也應該包含 **Type** 參數來指定這四個 Runbook 類型其中之一。</span><span class="sxs-lookup"><span data-stu-id="32b97-128">The **Type** parameter should also be included to specify one of the four runbook types.</span></span>

<span data-ttu-id="32b97-129">下列範例命令顯示如何建立新的空白 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-129">The following sample commands show how to create a new empty runbook.</span></span>

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a><span data-ttu-id="32b97-130">將 Runbook 從檔案匯入 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="32b97-130">Importing a runbook from a file into Azure Automation</span></span>
<span data-ttu-id="32b97-131">您可以在 Azure 自動化中建立新的 Runbook，方法是匯入 PowerShell 指令碼或 PowerShell 工作流程 (.ps1 延伸模組)，或匯入已匯出的圖形化 Runbook (.graphrunbook)。</span><span class="sxs-lookup"><span data-stu-id="32b97-131">You can create a new runbook in Azure Automation by importing a PowerShell script or PowerShell Workflow (.ps1 extension) or an exported graphical runbook (.graphrunbook).</span></span>  <span data-ttu-id="32b97-132">您必須指定從匯入建立的 [Runbook 的類型](automation-runbook-types.md) ，以將下列事項列入考量。</span><span class="sxs-lookup"><span data-stu-id="32b97-132">You must specify the [type of runbook](automation-runbook-types.md) that will be created from the import taking into account the following considerations.</span></span>

* <span data-ttu-id="32b97-133">.graphrunbook 檔案只能匯入至新的 [圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)，圖形化 Runbook 只能從 .graphrunbook 檔案建立。</span><span class="sxs-lookup"><span data-stu-id="32b97-133">A .graphrunbook file may only be imported into a new [graphical runbook](automation-runbook-types.md#graphical-runbooks), and graphical runbooks can only be created from a .graphrunbook file.</span></span>
* <span data-ttu-id="32b97-134">包含 PowerShell 工作流程的 .ps1 檔案只能匯入至 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="32b97-134">A .ps1 file containing a PowerShell Workflow can only be imported into a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="32b97-135">如果檔案包含多個 PowerShell 工作流程，則匯入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="32b97-135">If the file contains multiple PowerShell Workflows, then the import will fail.</span></span> <span data-ttu-id="32b97-136">您必須將每個工作流程儲存到它們各自的檔案，並且個別匯入。</span><span class="sxs-lookup"><span data-stu-id="32b97-136">You must save each workflow to its own file and import each separately.</span></span>
* <span data-ttu-id="32b97-137">未包含工作流程的 .ps1 檔案可以匯入至 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 或 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="32b97-137">A .ps1 file that does not contain a workflow can be imported into either a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="32b97-138">如果它匯入 PowerShell 工作流程 Runbook，則它會轉換為工作流程，註解會包含在 Runbook 中，指定所做的變更。</span><span class="sxs-lookup"><span data-stu-id="32b97-138">If it is imported into a PowerShell Workflow runbook, then it will be converted to a workflow, and comments will be included in the runbook specifying the changes that were made.</span></span>

### <a name="to-import-a-runbook-from-a-file-with-the-azure-classic-portal"></a><span data-ttu-id="32b97-139">使用 Azure 傳統入口網站從檔案匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-139">To import a runbook from a file with the Azure Classic portal</span></span>
<span data-ttu-id="32b97-140">您可以使用下列程序，將指令碼檔案匯入到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="32b97-140">You can use the following procedure to import a script file into Azure Automation.</span></span>  <span data-ttu-id="32b97-141">請注意，您只能使用此入口網站將 .ps1 檔案匯入 PowerShell 工作流程 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-141">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using this portal.</span></span>  <span data-ttu-id="32b97-142">對於其他類型，您必須使用 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="32b97-142">You must use the Azure portal for other types.</span></span>

1. <span data-ttu-id="32b97-143">在 Azure 管理入口網站中，選取 [自動化]  ，然後選取自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="32b97-143">In the Azure Management portal, select **Automation** and then select an Automation Account.</span></span>
2. <span data-ttu-id="32b97-144">按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="32b97-144">Click **Import**.</span></span>
3. <span data-ttu-id="32b97-145">按一下 [瀏覽檔案]  並找出要匯入的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="32b97-145">Click **Browse for File** and locate the script file to import.</span></span>
4. <span data-ttu-id="32b97-146">如果您想要立即編輯 Runbook，則按一下 [編輯 Runbook] 。</span><span class="sxs-lookup"><span data-stu-id="32b97-146">If you want to edit the runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="32b97-147">否則，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="32b97-147">Otherwise, click OK.</span></span>
5. <span data-ttu-id="32b97-148">新的 Runbook 會出現在 [自動化帳戶] 的 [Runbook]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="32b97-148">The new runbook will appear on the **Runbooks** tab for the Automation Account.</span></span>
6. <span data-ttu-id="32b97-149">您必須 [發佈 Runbook](#publishing-a-runbook) ，才能執行。</span><span class="sxs-lookup"><span data-stu-id="32b97-149">You must [publish the runbook](#publishing-a-runbook) before you can run it.</span></span>

### <a name="to-import-a-runbook-from-a-file-with-the-azure-portal"></a><span data-ttu-id="32b97-150">使用 Azure 入口網站從檔案匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-150">To import a runbook from a file with the Azure portal</span></span>
<span data-ttu-id="32b97-151">您可以使用下列程序，將指令碼檔案匯入到 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="32b97-151">You can use the following procedure to import a script file into Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="32b97-152">請注意，您只能使用入口網站，將 .ps1 檔案匯入 PowerShell 工作流程 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-152">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using the portal.</span></span>
> 
> 

1. <span data-ttu-id="32b97-153">在 Azure 入口網站中，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="32b97-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="32b97-154">從 [中樞] 選取 [Runbook] 以開啟 Runbook 清單。</span><span class="sxs-lookup"><span data-stu-id="32b97-154">From the Hub, select **Runbooks** to open the list of runbooks.</span></span>
3. <span data-ttu-id="32b97-155">按一下 [加入 Runbook] 按鈕，然後按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="32b97-155">Click on the **Add a runbook** button and then **Import**.</span></span>
4. <span data-ttu-id="32b97-156">按一下 [Runbook 檔案]  以選取要匯入的檔案</span><span class="sxs-lookup"><span data-stu-id="32b97-156">Click **Runbook file** to select the file to import</span></span>
5. <span data-ttu-id="32b97-157">如果 [名稱]  欄位已啟用，則您可以選擇變更它。</span><span class="sxs-lookup"><span data-stu-id="32b97-157">If the **Name** field is enabled, then you have the option to change it.</span></span>  <span data-ttu-id="32b97-158">Runbook 名稱必須以字母開頭，可以具有字母、數字、底線和連字號。</span><span class="sxs-lookup"><span data-stu-id="32b97-158">The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
6. <span data-ttu-id="32b97-159">[Runbook 類型](automation-runbook-types.md) 將會自動選取，但您可以在將適用限制納入考量之後變更此類型。</span><span class="sxs-lookup"><span data-stu-id="32b97-159">The [runbook type](automation-runbook-types.md) will be automatically selected, but you can change the type after taking the applicable restrictions into account.</span></span> 
7. <span data-ttu-id="32b97-160">新的 Runbook 會出現在 [自動化帳戶] 的 Runbook 清單中。</span><span class="sxs-lookup"><span data-stu-id="32b97-160">The new runbook will appear in the list of runbooks for the Automation Account.</span></span>
8. <span data-ttu-id="32b97-161">您必須 [發佈 Runbook](#publishing-a-runbook) ，才能執行。</span><span class="sxs-lookup"><span data-stu-id="32b97-161">You must [publish the runbook](#publishing-a-runbook) before you can run it.</span></span>

> [!NOTE]
> <span data-ttu-id="32b97-162">當您匯入圖形化 Runbook 或圖形化 PowerShell 工作流程 Runbook 之後，您可以視需要選擇轉換成另一種類型。</span><span class="sxs-lookup"><span data-stu-id="32b97-162">After you import a graphical runbook or a graphical PowerShell workflow runbook, you have the option to convert to the other type if wanted.</span></span> <span data-ttu-id="32b97-163">您無法轉換為文字。</span><span class="sxs-lookup"><span data-stu-id="32b97-163">You can’t convert to textual.</span></span>
> 
> 

### <a name="to-import-a-runbook-from-a-script-file-with-windows-powershell"></a><span data-ttu-id="32b97-164">使用 Windows PowerShell 從指令碼檔案匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-164">To import a runbook from a script file with Windows PowerShell</span></span>
<span data-ttu-id="32b97-165">您可以使用 [Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) Cmdlet，來匯入為指令碼檔案以做為草稿 PowerShell 工作流程 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-165">You can use the [Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet to import a script file as a draft PowerShell Workflow runbook.</span></span> <span data-ttu-id="32b97-166">如果 Runbook 已經存在，除非您使用 *-Force* 參數，否則匯入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="32b97-166">If the runbook already exists, the import will fail unless you use the *-Force* parameter.</span></span> 

<span data-ttu-id="32b97-167">以下範例命令示範如何將指令碼檔案匯入 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-167">The following sample commands show how to import a script file into a runbook.</span></span>

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a><span data-ttu-id="32b97-168">發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-168">Publishing a runbook</span></span>
<span data-ttu-id="32b97-169">當您建立或匯入新的 Runbook 時，您必須發佈才能執行它。</span><span class="sxs-lookup"><span data-stu-id="32b97-169">When you create or import a new runbook, you must publish it before you can run it.</span></span>  <span data-ttu-id="32b97-170">自動化中的每個 Runbook 都有草稿和已發行的版本。</span><span class="sxs-lookup"><span data-stu-id="32b97-170">Each runbook in Automation has a Draft and a Published version.</span></span> <span data-ttu-id="32b97-171">只可執行已發行版本，而且只可編輯草稿版本。</span><span class="sxs-lookup"><span data-stu-id="32b97-171">Only the Published version is available to be run, and only the Draft version can be edited.</span></span> <span data-ttu-id="32b97-172">已發行版本不會受到草稿版本的任何變更影響。</span><span class="sxs-lookup"><span data-stu-id="32b97-172">The Published version is unaffected by any changes to the Draft version.</span></span> <span data-ttu-id="32b97-173">草稿版本應該已可供使用時，您會將它發佈，以草稿版本覆寫已發佈版本。</span><span class="sxs-lookup"><span data-stu-id="32b97-173">When the Draft version should be made available, then you publish it which overwrites the Published version with the Draft version.</span></span>

## <a name="to-publish-a-runbook-using-the-azure-classic-portal"></a><span data-ttu-id="32b97-174">使用 Azure 傳統入口網站發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-174">To publish a runbook using the Azure Classic portal</span></span>
1. <span data-ttu-id="32b97-175">在 Azure 傳統入口網站中開啟 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-175">Open the runbook in the Azure Classic portal.</span></span>
2. <span data-ttu-id="32b97-176">在畫面頂端按一下 [撰寫] 。</span><span class="sxs-lookup"><span data-stu-id="32b97-176">At the top of the screen, click **Author**.</span></span>
3. <span data-ttu-id="32b97-177">在畫面底部按一下 [發佈]，然後對驗證訊息按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="32b97-177">At the bottom of the screen, click **Publish** and then **Yes** to the verification message.</span></span>

## <a name="to-publish-a-runbook-using-the-azure-portal"></a><span data-ttu-id="32b97-178">使用 Azure 入口網站發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-178">To publish a runbook using the Azure portal</span></span>
1. <span data-ttu-id="32b97-179">在 Azure 入口網站中開啟 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-179">Open the runbook in the Azure portal.</span></span>
2. <span data-ttu-id="32b97-180">按一下 [ **編輯** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="32b97-180">Click the **Edit** button.</span></span>
3. <span data-ttu-id="32b97-181">按一下 [發佈] 按鈕，然後對驗證訊息按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="32b97-181">Click the **Publish** button and then **Yes** to the verification message.</span></span>

## <a name="to-publish-a-runbook-using-windows-powershell"></a><span data-ttu-id="32b97-182">使用 Windows PowerShell 發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="32b97-182">To publish a runbook using Windows PowerShell</span></span>
<span data-ttu-id="32b97-183">您可以使用 [Publish-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) Cmdlet，利用 Windows PowerShell 發佈 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-183">You can use the [Publish-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet to publish a runbook with Windows PowerShell.</span></span> <span data-ttu-id="32b97-184">下列範例命令顯示如何發佈範例 Runbook。</span><span class="sxs-lookup"><span data-stu-id="32b97-184">The following sample commands show how to publish a sample runbook.</span></span>

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a><span data-ttu-id="32b97-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32b97-185">Next Steps</span></span>
* <span data-ttu-id="32b97-186">若要了解如何從 Runbook 和 PowerShell 模組資源庫中受益，請參閱 [Azure 自動化的 Runbook 和模組資源庫](automation-runbook-gallery.md)</span><span class="sxs-lookup"><span data-stu-id="32b97-186">To learn about how you can benefit from the Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)</span></span>
* <span data-ttu-id="32b97-187">若要深入了解使用文字編輯器編輯 PowerShell 和 PowerShell 工作流程 Runbook，請參閱 [在 Azure 自動化中編輯文字式 Runbook](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="32b97-187">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span>
* <span data-ttu-id="32b97-188">若要深入了解如何編寫圖形化 Runbook，請參閱 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="32b97-188">To learn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>

