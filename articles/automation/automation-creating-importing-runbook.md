---
title: "aaaCreating 或匯入在 Azure 自動化 runbook"
description: "本文說明如何 toocreate Azure 自動化中的檔案從一個匯入新的 runbook。"
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
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a><span data-ttu-id="92d63-103">在 Azure 自動化中建立或匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-103">Creating or importing a runbook in Azure Automation</span></span>
<span data-ttu-id="92d63-104">您可以加入由 runbook tooAzure 自動化[建立一個新](#creating-a-new-runbook)或匯入現有的 runbook，從檔案或從 hello [Runbook 庫](automation-runbook-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="92d63-104">You can add a runbook tooAzure Automation by either [creating a new one](#creating-a-new-runbook) or by importing an existing runbook from a file or from hello [Runbook Gallery](automation-runbook-gallery.md).</span></span> <span data-ttu-id="92d63-105">本文提供從檔案建立和匯入 Runbook 的資訊。</span><span class="sxs-lookup"><span data-stu-id="92d63-105">This article provides information on creating and importing runbooks from a file.</span></span>  <span data-ttu-id="92d63-106">您可以取得所有上存取社群的 runbook 和模組中的 hello 詳細[Azure 自動化 Runbook 和模組組件庫](automation-runbook-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="92d63-106">You can get all of hello details on accessing community runbooks and modules in [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>

## <a name="creating-a-new-runbook"></a><span data-ttu-id="92d63-107">建立新的 Runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-107">Creating a new runbook</span></span>
<span data-ttu-id="92d63-108">您可以建立新的 runbook 在 Azure 自動化中使用其中一種 hello Azure 入口網站或 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="92d63-108">You can create a new runbook in Azure Automation using one of hello Azure portals or Windows PowerShell.</span></span> <span data-ttu-id="92d63-109">一旦建立 hello runbook 之後，您可以使用編輯中的資訊[學習 PowerShell 工作流程](automation-powershell-workflow.md)和[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="92d63-109">Once hello runbook has been created, you can edit it using information in [Learning PowerShell Workflow](automation-powershell-workflow.md) and [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a><span data-ttu-id="92d63-110">toocreate hello Azure 傳統入口網站使用新的 Azure 自動化 runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-110">toocreate a new Azure Automation runbook with hello Azure Classic portal</span></span>
<span data-ttu-id="92d63-111">您只能搭配[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="92d63-111">You can only work with [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks) in hello Azure portal.</span></span>

1. <span data-ttu-id="92d63-112">Hello Azure 傳統入口網站中按一下，**新增**，**應用程式服務**，**自動化**， **Runbook**，**快速建立**.</span><span class="sxs-lookup"><span data-stu-id="92d63-112">In hello Azure Classic portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.</span></span>
2. <span data-ttu-id="92d63-113">輸入所需的 hello 的詳細資訊，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="92d63-113">Enter hello required information, and then click **Create**.</span></span> <span data-ttu-id="92d63-114">hello runbook 名稱必須以字母開頭，而且可以有字母、 數字、 底線和連字號。</span><span class="sxs-lookup"><span data-stu-id="92d63-114">hello runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
3. <span data-ttu-id="92d63-115">如果您現在想 tooedit hello runbook，然後按一下**編輯 Runbook**。</span><span class="sxs-lookup"><span data-stu-id="92d63-115">If you want tooedit hello runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="92d63-116">否則，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="92d63-116">Otherwise, click **OK**.</span></span>
4. <span data-ttu-id="92d63-117">新的 runbook 會出現在 hello **Runbook**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="92d63-117">Your new runbook will appear on hello **Runbooks** tab.</span></span>

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a><span data-ttu-id="92d63-118">toocreate hello Azure 入口網站使用新的 Azure 自動化 runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-118">toocreate a new Azure Automation runbook with hello Azure portal</span></span>
1. <span data-ttu-id="92d63-119">在 hello Azure 入口網站，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="92d63-119">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="92d63-120">從 hello 中樞，選取**Runbook** tooopen hello 的 runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="92d63-120">From hello Hub, select **Runbooks** tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="92d63-121">按一下 hello**新增 runbook**  按鈕，然後**建立新的 runbook**。</span><span class="sxs-lookup"><span data-stu-id="92d63-121">Click on hello **Add a runbook** button and then **Create a new runbook**.</span></span>
4. <span data-ttu-id="92d63-122">輸入**名稱**hello runbook 並選取其[類型](automation-runbook-types.md)。</span><span class="sxs-lookup"><span data-stu-id="92d63-122">Type a **Name** for hello runbook and select its [Type](automation-runbook-types.md).</span></span> <span data-ttu-id="92d63-123">hello runbook 名稱必須以字母開頭，而且可以有字母、 數字、 底線和連字號。</span><span class="sxs-lookup"><span data-stu-id="92d63-123">hello runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
5. <span data-ttu-id="92d63-124">按一下**建立**toocreate hello runbook 和開啟 hello 編輯器。</span><span class="sxs-lookup"><span data-stu-id="92d63-124">Click **Create** toocreate hello runbook and open hello editor.</span></span>

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a><span data-ttu-id="92d63-125">toocreate 使用 Windows PowerShell 新的 Azure 自動化 runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-125">toocreate a new Azure Automation runbook with Windows PowerShell</span></span>
<span data-ttu-id="92d63-126">您可以使用 hello[新增 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate 空[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="92d63-126">You can use hello [New-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate an empty [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="92d63-127">您可以指定 hello**名稱**參數 toocreate 空的 runbook，您可以稍後編輯，或者您可以指定 hello**路徑**參數 tooimport runbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="92d63-127">You can either specify hello **Name** parameter toocreate an empty runbook that you can later edit, or you can specify hello **Path** parameter tooimport a runbook file.</span></span> <span data-ttu-id="92d63-128">hello**類型**參數也應該包含的 toospecify hello 四個 runbook 類型之一。</span><span class="sxs-lookup"><span data-stu-id="92d63-128">hello **Type** parameter should also be included toospecify one of hello four runbook types.</span></span>

<span data-ttu-id="92d63-129">hello 下列範例命令顯示如何 toocreate 新的空白 rubbook。</span><span class="sxs-lookup"><span data-stu-id="92d63-129">hello following sample commands show how toocreate a new empty runbook.</span></span>

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a><span data-ttu-id="92d63-130">將 Runbook 從檔案匯入 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="92d63-130">Importing a runbook from a file into Azure Automation</span></span>
<span data-ttu-id="92d63-131">您可以在 Azure 自動化中建立新的 Runbook，方法是匯入 PowerShell 指令碼或 PowerShell 工作流程 (.ps1 延伸模組)，或匯入已匯出的圖形化 Runbook (.graphrunbook)。</span><span class="sxs-lookup"><span data-stu-id="92d63-131">You can create a new runbook in Azure Automation by importing a PowerShell script or PowerShell Workflow (.ps1 extension) or an exported graphical runbook (.graphrunbook).</span></span>  <span data-ttu-id="92d63-132">您必須指定 hello[的 runbook 類型](automation-runbook-types.md)，會建立下列帳戶 hello 下列考量因素納入 hello 匯入。</span><span class="sxs-lookup"><span data-stu-id="92d63-132">You must specify hello [type of runbook](automation-runbook-types.md) that will be created from hello import taking into account hello following considerations.</span></span>

* <span data-ttu-id="92d63-133">.graphrunbook 檔案只能匯入至新的 [圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)，圖形化 Runbook 只能從 .graphrunbook 檔案建立。</span><span class="sxs-lookup"><span data-stu-id="92d63-133">A .graphrunbook file may only be imported into a new [graphical runbook](automation-runbook-types.md#graphical-runbooks), and graphical runbooks can only be created from a .graphrunbook file.</span></span>
* <span data-ttu-id="92d63-134">包含 PowerShell 工作流程的 .ps1 檔案只能匯入至 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="92d63-134">A .ps1 file containing a PowerShell Workflow can only be imported into a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="92d63-135">如果 hello 檔案包含多個 PowerShell 工作流程，hello 匯入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="92d63-135">If hello file contains multiple PowerShell Workflows, then hello import will fail.</span></span> <span data-ttu-id="92d63-136">您必須儲存每個工作流程 tooits 自己的檔案，並分別匯入每個。</span><span class="sxs-lookup"><span data-stu-id="92d63-136">You must save each workflow tooits own file and import each separately.</span></span>
* <span data-ttu-id="92d63-137">未包含工作流程的 .ps1 檔案可以匯入至 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 或 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="92d63-137">A .ps1 file that does not contain a workflow can be imported into either a [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) or a [PowerShell Workflow runbook](automation-runbook-types.md#powershell-workflow-runbooks).</span></span>  <span data-ttu-id="92d63-138">如果匯入到 PowerShell 工作流程 runbook，然後它會轉換的 tooa 工作流程，並註解將會包含在 hello runbook 指定 hello 所做的變更。</span><span class="sxs-lookup"><span data-stu-id="92d63-138">If it is imported into a PowerShell Workflow runbook, then it will be converted tooa workflow, and comments will be included in hello runbook specifying hello changes that were made.</span></span>

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a><span data-ttu-id="92d63-139">tooimport hello Azure 傳統入口網站的檔案從 runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-139">tooimport a runbook from a file with hello Azure Classic portal</span></span>
<span data-ttu-id="92d63-140">您可以使用下列程序 tooimport 指令碼檔案到 Azure 自動化的 hello。</span><span class="sxs-lookup"><span data-stu-id="92d63-140">You can use hello following procedure tooimport a script file into Azure Automation.</span></span>  <span data-ttu-id="92d63-141">請注意，您只能使用此入口網站將 .ps1 檔案匯入 PowerShell 工作流程 Runbook。</span><span class="sxs-lookup"><span data-stu-id="92d63-141">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using this portal.</span></span>  <span data-ttu-id="92d63-142">您必須使用其他類型 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="92d63-142">You must use hello Azure portal for other types.</span></span>

1. <span data-ttu-id="92d63-143">在 hello Azure 管理入口網站中，選取 **自動化**，然後選取 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="92d63-143">In hello Azure Management portal, select **Automation** and then select an Automation Account.</span></span>
2. <span data-ttu-id="92d63-144">按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="92d63-144">Click **Import**.</span></span>
3. <span data-ttu-id="92d63-145">按一下**瀏覽檔案**並找出 hello 指令碼檔案 tooimport。</span><span class="sxs-lookup"><span data-stu-id="92d63-145">Click **Browse for File** and locate hello script file tooimport.</span></span>
4. <span data-ttu-id="92d63-146">如果您現在想 tooedit hello runbook，然後按一下**編輯 Runbook**。</span><span class="sxs-lookup"><span data-stu-id="92d63-146">If you want tooedit hello runbook now, then click **Edit Runbook**.</span></span> <span data-ttu-id="92d63-147">否則，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="92d63-147">Otherwise, click OK.</span></span>
5. <span data-ttu-id="92d63-148">hello 新 runbook 會出現在 hello **Runbook** hello 自動化帳戶 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="92d63-148">hello new runbook will appear on hello **Runbooks** tab for hello Automation Account.</span></span>
6. <span data-ttu-id="92d63-149">您必須[發行 hello runbook](#publishing-a-runbook)才能執行它。</span><span class="sxs-lookup"><span data-stu-id="92d63-149">You must [publish hello runbook](#publishing-a-runbook) before you can run it.</span></span>

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a><span data-ttu-id="92d63-150">tooimport hello Azure 入口網站的檔案從 runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-150">tooimport a runbook from a file with hello Azure portal</span></span>
<span data-ttu-id="92d63-151">您可以使用下列程序 tooimport 指令碼檔案到 Azure 自動化的 hello。</span><span class="sxs-lookup"><span data-stu-id="92d63-151">You can use hello following procedure tooimport a script file into Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="92d63-152">請注意，您可以只匯入.ps1 檔案至 PowerShell 工作流程 runbook 使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="92d63-152">Note that you can only import a .ps1 file into a PowerShell Workflow runbook using hello portal.</span></span>
> 
> 

1. <span data-ttu-id="92d63-153">在 hello Azure 入口網站，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="92d63-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="92d63-154">從 hello 中樞，選取**Runbook** tooopen hello 的 runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="92d63-154">From hello Hub, select **Runbooks** tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="92d63-155">按一下 hello**新增 runbook**  按鈕，然後**匯入**。</span><span class="sxs-lookup"><span data-stu-id="92d63-155">Click on hello **Add a runbook** button and then **Import**.</span></span>
4. <span data-ttu-id="92d63-156">按一下**Runbook 檔案**tooselect hello 檔案 tooimport</span><span class="sxs-lookup"><span data-stu-id="92d63-156">Click **Runbook file** tooselect hello file tooimport</span></span>
5. <span data-ttu-id="92d63-157">如果 hello**名稱**欄位才會啟用，則您擁有 hello 選項 toochange 它。</span><span class="sxs-lookup"><span data-stu-id="92d63-157">If hello **Name** field is enabled, then you have hello option toochange it.</span></span>  <span data-ttu-id="92d63-158">hello runbook 名稱必須以字母開頭，而且可以有字母、 數字、 底線和連字號。</span><span class="sxs-lookup"><span data-stu-id="92d63-158">hello runbook name must start with a letter and can have letters, numbers, underscores, and dashes.</span></span>
6. <span data-ttu-id="92d63-159">hello [runbook 類型](automation-runbook-types.md)會自動選取，但您可以變更 hello 類型後 hello 適用限制納入考量。</span><span class="sxs-lookup"><span data-stu-id="92d63-159">hello [runbook type](automation-runbook-types.md) will be automatically selected, but you can change hello type after taking hello applicable restrictions into account.</span></span> 
7. <span data-ttu-id="92d63-160">hello 新的 runbook 會出現在 hello hello 自動化帳戶的 runbook 清單。</span><span class="sxs-lookup"><span data-stu-id="92d63-160">hello new runbook will appear in hello list of runbooks for hello Automation Account.</span></span>
8. <span data-ttu-id="92d63-161">您必須[發行 hello runbook](#publishing-a-runbook)才能執行它。</span><span class="sxs-lookup"><span data-stu-id="92d63-161">You must [publish hello runbook](#publishing-a-runbook) before you can run it.</span></span>

> [!NOTE]
> <span data-ttu-id="92d63-162">您匯入圖形化 runbook 或圖形化的 PowerShell 工作流程 runbook 之後，您必須 hello 選項 tooconvert toohello 其他型別如果想。</span><span class="sxs-lookup"><span data-stu-id="92d63-162">After you import a graphical runbook or a graphical PowerShell workflow runbook, you have hello option tooconvert toohello other type if wanted.</span></span> <span data-ttu-id="92d63-163">您無法轉換 tootextual。</span><span class="sxs-lookup"><span data-stu-id="92d63-163">You can’t convert tootextual.</span></span>
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a><span data-ttu-id="92d63-164">tooimport runbook 從使用 Windows PowerShell 指令碼檔案</span><span class="sxs-lookup"><span data-stu-id="92d63-164">tooimport a runbook from a script file with Windows PowerShell</span></span>
<span data-ttu-id="92d63-165">您可以使用 hello[匯入 AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport 為草稿 PowerShell 工作流程 runbook 的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="92d63-165">You can use hello [Import-AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport a script file as a draft PowerShell Workflow runbook.</span></span> <span data-ttu-id="92d63-166">如果已經存在 hello runbook，hello 匯入將會失敗，除非您使用 hello *-Force*參數。</span><span class="sxs-lookup"><span data-stu-id="92d63-166">If hello runbook already exists, hello import will fail unless you use hello *-Force* parameter.</span></span> 

<span data-ttu-id="92d63-167">hello，下列命令範例顯示如何 tooimport 指令碼檔案至 runbook。</span><span class="sxs-lookup"><span data-stu-id="92d63-167">hello following sample commands show how tooimport a script file into a runbook.</span></span>

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a><span data-ttu-id="92d63-168">發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="92d63-168">Publishing a runbook</span></span>
<span data-ttu-id="92d63-169">當您建立或匯入新的 Runbook 時，您必須發佈才能執行它。</span><span class="sxs-lookup"><span data-stu-id="92d63-169">When you create or import a new runbook, you must publish it before you can run it.</span></span>  <span data-ttu-id="92d63-170">自動化中的每個 Runbook 都有草稿和已發行的版本。</span><span class="sxs-lookup"><span data-stu-id="92d63-170">Each runbook in Automation has a Draft and a Published version.</span></span> <span data-ttu-id="92d63-171">只有 hello 已發佈版本可用 toobe 執行，且 hello 草稿版本可供編輯。</span><span class="sxs-lookup"><span data-stu-id="92d63-171">Only hello Published version is available toobe run, and only hello Draft version can be edited.</span></span> <span data-ttu-id="92d63-172">hello 已發佈 」 版本不會受到任何變更 toohello 草稿版本。</span><span class="sxs-lookup"><span data-stu-id="92d63-172">hello Published version is unaffected by any changes toohello Draft version.</span></span> <span data-ttu-id="92d63-173">當 hello 草稿版本應該成為可用時，您應發佈該 hello 草稿版本覆寫 hello 已發佈版本。</span><span class="sxs-lookup"><span data-stu-id="92d63-173">When hello Draft version should be made available, then you publish it which overwrites hello Published version with hello Draft version.</span></span>

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a><span data-ttu-id="92d63-174">toopublish 的 runbook 使用 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="92d63-174">toopublish a runbook using hello Azure Classic portal</span></span>
1. <span data-ttu-id="92d63-175">Hello Azure 傳統入口網站中開啟 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="92d63-175">Open hello runbook in hello Azure Classic portal.</span></span>
2. <span data-ttu-id="92d63-176">在 hello 囉 」 畫面頂端，按一下**作者**。</span><span class="sxs-lookup"><span data-stu-id="92d63-176">At hello top of hello screen, click **Author**.</span></span>
3. <span data-ttu-id="92d63-177">在 hello 囉 」 畫面底部，按一下 **發行**然後**是**toohello 驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="92d63-177">At hello bottom of hello screen, click **Publish** and then **Yes** toohello verification message.</span></span>

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a><span data-ttu-id="92d63-178">toopublish 的 runbook 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="92d63-178">toopublish a runbook using hello Azure portal</span></span>
1. <span data-ttu-id="92d63-179">開啟 hello runbook 中的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="92d63-179">Open hello runbook in hello Azure portal.</span></span>
2. <span data-ttu-id="92d63-180">按一下 hello**編輯** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92d63-180">Click hello **Edit** button.</span></span>
3. <span data-ttu-id="92d63-181">按一下 hello**發行** 按鈕，然後**是**toohello 驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="92d63-181">Click hello **Publish** button and then **Yes** toohello verification message.</span></span>

## <a name="toopublish-a-runbook-using-windows-powershell"></a><span data-ttu-id="92d63-182">使用 Windows PowerShell runbook toopublish</span><span class="sxs-lookup"><span data-stu-id="92d63-182">toopublish a runbook using Windows PowerShell</span></span>
<span data-ttu-id="92d63-183">您可以使用 hello[發行 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish 使用 Windows PowerShell runbook。</span><span class="sxs-lookup"><span data-stu-id="92d63-183">You can use hello [Publish-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish a runbook with Windows PowerShell.</span></span> <span data-ttu-id="92d63-184">hello 下列範例命令顯示如何 toopublish 範例 runbook。</span><span class="sxs-lookup"><span data-stu-id="92d63-184">hello following sample commands show how toopublish a sample runbook.</span></span>

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a><span data-ttu-id="92d63-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92d63-185">Next Steps</span></span>
* <span data-ttu-id="92d63-186">請參閱有關如何享有 hello Runbook 和 PowerShell 模組資源庫，toolearn [Azure 自動化 Runbook 和模組組件庫](automation-runbook-gallery.md)</span><span class="sxs-lookup"><span data-stu-id="92d63-186">toolearn about how you can benefit from hello Runbook and PowerShell Module Gallery, see  [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md)</span></span>
* <span data-ttu-id="92d63-187">進一步了解使用文字編輯器，編輯 PowerShell 和 PowerShell 工作流程 runbook toolearn 看到[編輯 Azure 自動化中的文字 runbook](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="92d63-187">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span>
* <span data-ttu-id="92d63-188">toolearn 進一步了解撰寫圖形化 runbook，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="92d63-188">toolearn more about Graphical runbook authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>

