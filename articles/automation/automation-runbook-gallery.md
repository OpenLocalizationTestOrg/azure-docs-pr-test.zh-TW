---
title: "Azure 自動化的 Runbook 和模組資源庫 | Microsoft Docs"
description: "來自 Microsoft 和社群的 Runbook 和模組可供您在 Azure 自動化環境中安裝及使用。  本文說明如何存取這些資源以及將您的 Runbook 貢獻至資源庫。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 04cfafc9e7a037d915f63723fd0b67a07954460b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a><span data-ttu-id="64efb-104">Azure 自動化的 Runbook 和模組資源庫</span><span class="sxs-lookup"><span data-stu-id="64efb-104">Runbook and module galleries for Azure Automation</span></span>
<span data-ttu-id="64efb-105">您可以存取各種已由 Microsoft 和社群建置的案例，而不是在 Azure 自動化中建立您自己的 Runbook 和模組。</span><span class="sxs-lookup"><span data-stu-id="64efb-105">Rather than creating your own runbooks and modules in Azure Automation, you can access a variety of scenarios that have already been built by Microsoft and the community.</span></span>  <span data-ttu-id="64efb-106">您可以不加修改地使用這些案例，或者使用它們做為起點並針對您的特定需求進行編輯。</span><span class="sxs-lookup"><span data-stu-id="64efb-106">You can either use these scenarios without modification or you can use them as a starting point and edit them for your specific requirements.</span></span>

<span data-ttu-id="64efb-107">您可以從 [Runbook 資源庫](#runbooks-in-runbook-gallery)取得 Runbook，從 [PowerShell 資源庫](#modules-in-powerShell-gallery)取得模組。</span><span class="sxs-lookup"><span data-stu-id="64efb-107">You can get runbooks from the [Runbook Gallery](#runbooks-in-runbook-gallery) and modules from the [PowerShell Gallery](#modules-in-powerShell-gallery).</span></span>  <span data-ttu-id="64efb-108">您也可以藉由共用您開發的案例來參與社群。</span><span class="sxs-lookup"><span data-stu-id="64efb-108">You can also contribute to the community by sharing scenarios that you develop.</span></span>

## <a name="runbooks-in-runbook-gallery"></a><span data-ttu-id="64efb-109">Runbook 資源庫中的 Runbook</span><span class="sxs-lookup"><span data-stu-id="64efb-109">Runbooks in Runbook Gallery</span></span>
<span data-ttu-id="64efb-110">[Runbook 資源庫](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation)提供各種來自 Microsoft 和社群的 Runbook，您可以匯入至 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="64efb-110">The [Runbook Gallery](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) provides a variety of runbooks from Microsoft and the community that you can import into Azure Automation.</span></span> <span data-ttu-id="64efb-111">您可以從 [TechNet 指令碼中心](https://gallery.technet.microsoft.com/scriptcenter/site/upload)託管的資源庫下載 Runbook，或者您可以直接從 Azure 傳統入口網站或 Azure 入口網站的資源庫匯入 Runbook。</span><span class="sxs-lookup"><span data-stu-id="64efb-111">You can either download a runbook from the gallery which is hosted in the [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), or you can directly import runbooks from the gallery from either the Azure classic portal or Azure portal.</span></span>

<span data-ttu-id="64efb-112">若要直接從 Runbook 資源庫匯入，您只能使用 Azure 傳統入口網站或 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="64efb-112">You can only import directly from the Runbook Gallery using the Azure classic portal or Azure portal.</span></span> <span data-ttu-id="64efb-113">您無法使用 Windows PowerShell 執行此函式。</span><span class="sxs-lookup"><span data-stu-id="64efb-113">You cannot perform this function using Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="64efb-114">您應該驗證您從 Runbook 資源庫取得的任何 Runbook 的內容，並且在生產環境中安裝和執行它們時小心謹慎。</span><span class="sxs-lookup"><span data-stu-id="64efb-114">You should validate the contents of any runbooks that you get from the Runbook Gallery and use extreme caution in installing and running them in a production environment.|</span></span>
> 
> 

### <a name="to-import-a-runbook-from-the-runbook-gallery-with-the-azure-classic-portal"></a><span data-ttu-id="64efb-115">透過 Azure 傳統入口網站從 Runbook 資源庫匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="64efb-115">To import a runbook from the Runbook Gallery with the Azure classic portal</span></span>
1. <span data-ttu-id="64efb-116">在 Azure 入口網站中，按一下 [新增] > [應用程式服務] > [自動化] > [Runbook] > [從資源庫]。</span><span class="sxs-lookup"><span data-stu-id="64efb-116">In the Azure Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **From Gallery**.</span></span>
2. <span data-ttu-id="64efb-117">選取類別以檢視相關的 Runbook，然後選取 Runbook 以檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="64efb-117">Select a category to view related runbooks, and select a runbook to view its details.</span></span> <span data-ttu-id="64efb-118">當您選取您想要的 Runbook 時，按一下向右箭頭按鈕。</span><span class="sxs-lookup"><span data-stu-id="64efb-118">When you select the runbook you want, click the right arrow button.</span></span>
   
    ![Runbook 資源庫](media/automation-runbook-gallery/runbook-gallery.png)
3. <span data-ttu-id="64efb-120">檢閱 Runbook 的內容並記下說明中的任何需求。</span><span class="sxs-lookup"><span data-stu-id="64efb-120">Review the contents of the runbook and note any requirements in the description.</span></span> <span data-ttu-id="64efb-121">當您完成時按一下向右箭頭按鈕。</span><span class="sxs-lookup"><span data-stu-id="64efb-121">Click the right arrow button when you’re done.</span></span>
4. <span data-ttu-id="64efb-122">輸入 Runbook 詳細資料，然後按一下勾選記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="64efb-122">Enter the runbook details and then click the checkmark button.</span></span> <span data-ttu-id="64efb-123">Runbook 名稱已填入。</span><span class="sxs-lookup"><span data-stu-id="64efb-123">The runbook name will already be filled in.</span></span>
5. <span data-ttu-id="64efb-124">Runbook 會出現在 [自動化帳戶] 的 [Runbook]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="64efb-124">The runbook will appear on the **Runbooks** tab for the Automation Account.</span></span>

### <a name="to-import-a-runbook-from-the-runbook-gallery-with-the-azure-portal"></a><span data-ttu-id="64efb-125">使用 Azure 入口網站從 Runbook 資源庫匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="64efb-125">To import a runbook from the Runbook Gallery with the Azure portal</span></span>
1. <span data-ttu-id="64efb-126">在 Azure 入口網站中，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="64efb-126">In the Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="64efb-127">按一下 [Runbook]  磚以開啟 Runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="64efb-127">Click on the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="64efb-128">按一下 [瀏覽資源庫]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="64efb-128">Click **Browse gallery** button.</span></span>
   
    ![瀏覽資源庫按鈕](media/automation-runbook-gallery/browse-gallery-button.png)
4. <span data-ttu-id="64efb-130">找出您想要的資源庫項目，並且選取以檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="64efb-130">Locate the gallery item you want and select it to view its details.</span></span>
   
    ![瀏覽資源庫](media/automation-runbook-gallery/browse-gallery.png)
5. <span data-ttu-id="64efb-132">按一下 [檢視來源專案]  以檢視 [TechNet 指令碼中心](http://gallery.technet.microsoft.com/)中的項目。</span><span class="sxs-lookup"><span data-stu-id="64efb-132">Click on **View source project** to view the item in the [TechNet Script Center](http://gallery.technet.microsoft.com/).</span></span>
6. <span data-ttu-id="64efb-133">若要匯入項目，請按一下以檢視其詳細資料，然後按一下 [匯入]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="64efb-133">To import an item, click on it to view its details and then click the **Import** button.</span></span>
   
    ![匯入按鈕](media/automation-runbook-gallery/gallery-item-detail.png)
7. <span data-ttu-id="64efb-135">選擇性變更 Runbook 的名稱，然後按一下 [確定]  以匯入 Runbook。</span><span class="sxs-lookup"><span data-stu-id="64efb-135">Optionally, change the name of the runbook and then click **OK** to import the runbook.</span></span>
8. <span data-ttu-id="64efb-136">Runbook 會出現在 [自動化帳戶] 的 [Runbook]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="64efb-136">The runbook will appear on the **Runbooks** tab for the Automation Account.</span></span>

### <a name="adding-a-runbook-to-the-runbook-gallery"></a><span data-ttu-id="64efb-137">將 Runbook 新增至 Runbook 資源庫</span><span class="sxs-lookup"><span data-stu-id="64efb-137">Adding a runbook to the runbook gallery</span></span>
<span data-ttu-id="64efb-138">Microsoft 鼓勵您將您認為可能有助於其他客戶的 Runbook 新增至 Runbook 資源庫。</span><span class="sxs-lookup"><span data-stu-id="64efb-138">Microsoft encourages you to add runbooks to the Runbook Gallery that you think would be useful to other customers.</span></span>  <span data-ttu-id="64efb-139">您可以藉由 [將其上傳到指令碼中心](http://gallery.technet.microsoft.com/site/upload) 來新增 Runbook，並且將下列詳細資料納入考量。</span><span class="sxs-lookup"><span data-stu-id="64efb-139">You can add a runbook by [uploading it to the Script Center](http://gallery.technet.microsoft.com/site/upload) taking into account the following details.</span></span>

* <span data-ttu-id="64efb-140">您必須針對 [類別] 指定 [Windows Azure]，針對 [子類別] 指定[自動化]，讓 Runbook 顯示在精靈中。</span><span class="sxs-lookup"><span data-stu-id="64efb-140">You must specify *Windows Azure* for the **Category** and *Automation* for the **Subcategory** for the runbook to be displayed in the wizard.</span></span>  
* <span data-ttu-id="64efb-141">上傳必須是單一 .ps1 或 .graphrunbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="64efb-141">The upload must be a single .ps1 or .graphrunbook file.</span></span>  <span data-ttu-id="64efb-142">如果 Runbook 需要任何模組、子 Runbook 或資產，則您應該在提交的說明中和 Runbook 的註解區段中列出。</span><span class="sxs-lookup"><span data-stu-id="64efb-142">If the runbook requires any modules, child runbooks, or assets, then you should list those in the description of the submission and in the comments section of the runbook.</span></span>  <span data-ttu-id="64efb-143">如果您有需要多個 Runbook 的案例，則分別將每個上傳並且在各自的說明中列出相關 Runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="64efb-143">If you have a scenario requiring multiple runbooks, then upload each separately and list the names of the related runbooks in each of their descriptions.</span></span> <span data-ttu-id="64efb-144">請確定您使用相同的標記，這樣它們就會在相同的類別中顯示。</span><span class="sxs-lookup"><span data-stu-id="64efb-144">Make sure that you use the same tags so that they will show up in the same category.</span></span> <span data-ttu-id="64efb-145">使用者必須閱讀說明，以得知案例需要其他 Runbook 才能運作。</span><span class="sxs-lookup"><span data-stu-id="64efb-145">A user will have to read the description to know that other runbooks are required the scenario to work.</span></span>
* <span data-ttu-id="64efb-146">如果您要發佈 [圖形化 Runbook]  \(而非圖形化工作流程)，請新增 "GraphicalPS" 標籤。</span><span class="sxs-lookup"><span data-stu-id="64efb-146">Add the tag "GraphicalPS" if you are publishing a **Graphical runbook** (not a Graphical Workflow).</span></span> 
* <span data-ttu-id="64efb-147">使用 [ **插入程式碼區段** ] 圖示將 PowerShell 或 PowerShell 工作流程程式碼片段插入說明中。</span><span class="sxs-lookup"><span data-stu-id="64efb-147">Insert either a PowerShell or PowerShell Workflow code snippet into the description using **Insert code section** icon.</span></span>
* <span data-ttu-id="64efb-148">上傳的摘要會顯示在 Runbook 資源庫結果，因此您應該提供詳細資訊，幫助使用者識別 Runbook 的功能。</span><span class="sxs-lookup"><span data-stu-id="64efb-148">The Summary for the upload will be displayed in the Runbook Gallery results so you should provide detailed information that will help a user identify the functionality of the runbook.</span></span>
* <span data-ttu-id="64efb-149">您應該對上傳項目指派 1 到 3 個下列標記。</span><span class="sxs-lookup"><span data-stu-id="64efb-149">You should assign one to three of the following Tags to the upload.</span></span>  <span data-ttu-id="64efb-150">Runbook 會列在精靈中符合其標記的類別底下。</span><span class="sxs-lookup"><span data-stu-id="64efb-150">The runbook will be listed in the wizard under the categories that match its tags.</span></span>  <span data-ttu-id="64efb-151">精靈會略過不在此清單上的任何標記。</span><span class="sxs-lookup"><span data-stu-id="64efb-151">Any tags not on this list will be ignored by the wizard.</span></span> <span data-ttu-id="64efb-152">如果您未指定任何相符的標記，Runbook 會列在 [其他] 類別底下。</span><span class="sxs-lookup"><span data-stu-id="64efb-152">If you don’t specify any matching tags, the runbook will be listed under the Other category.</span></span>
  
  * <span data-ttu-id="64efb-153">備份</span><span class="sxs-lookup"><span data-stu-id="64efb-153">Backup</span></span>
  * <span data-ttu-id="64efb-154">產能管理</span><span class="sxs-lookup"><span data-stu-id="64efb-154">Capacity Management</span></span>
  * <span data-ttu-id="64efb-155">變更控制</span><span class="sxs-lookup"><span data-stu-id="64efb-155">Change Control</span></span>
  * <span data-ttu-id="64efb-156">法規遵循</span><span class="sxs-lookup"><span data-stu-id="64efb-156">Compliance</span></span>
  * <span data-ttu-id="64efb-157">開發/測試環境</span><span class="sxs-lookup"><span data-stu-id="64efb-157">Dev / Test Environments</span></span>
  * <span data-ttu-id="64efb-158">災害復原</span><span class="sxs-lookup"><span data-stu-id="64efb-158">Disaster Recovery</span></span>
  * <span data-ttu-id="64efb-159">監視</span><span class="sxs-lookup"><span data-stu-id="64efb-159">Monitoring</span></span>
  * <span data-ttu-id="64efb-160">修補</span><span class="sxs-lookup"><span data-stu-id="64efb-160">Patching</span></span>
  * <span data-ttu-id="64efb-161">佈建</span><span class="sxs-lookup"><span data-stu-id="64efb-161">Provisioning</span></span>
  * <span data-ttu-id="64efb-162">補救</span><span class="sxs-lookup"><span data-stu-id="64efb-162">Remediation</span></span>
  * <span data-ttu-id="64efb-163">VM 生命週期管理</span><span class="sxs-lookup"><span data-stu-id="64efb-163">VM Lifecycle Management</span></span>
* <span data-ttu-id="64efb-164">一小時更新自動化資源庫一次，因此您不會立即看到您的貢獻。</span><span class="sxs-lookup"><span data-stu-id="64efb-164">Automation updates the Gallery once an hour, so you won’t see your contributions immediately.</span></span>

## <a name="modules-in-powershell-gallery"></a><span data-ttu-id="64efb-165">PowerShell 資源庫中的模組</span><span class="sxs-lookup"><span data-stu-id="64efb-165">Modules in PowerShell Gallery</span></span>
<span data-ttu-id="64efb-166">PowerShell 模組包含您可以在 Runbook 中使用的 Cmdlet，您可以安裝在 Azure 自動化中的現有模組可於 [PowerShell 資源庫](http://www.powershellgallery.com)取得。</span><span class="sxs-lookup"><span data-stu-id="64efb-166">PowerShell modules contain cmdlets that you can use in your runbooks, and existing modules that you can install in Azure Automation are available in the [PowerShell Gallery](http://www.powershellgallery.com).</span></span>  <span data-ttu-id="64efb-167">您可以從 Azure 入口網站啟動此資源庫，然後直接安裝至 Azure 自動化，也可以手動下載及安裝。</span><span class="sxs-lookup"><span data-stu-id="64efb-167">You can launch this gallery from the Azure portal and install them directly into Azure Automation or you can download them and install them manually.</span></span>  <span data-ttu-id="64efb-168">您無法直接從 Azure 傳統入口網站安裝模組，但是您可以使用一般方式，下載及安裝這些模組。</span><span class="sxs-lookup"><span data-stu-id="64efb-168">You cannot install the modules directly from the Azure classic portal, but you can download them install them as you would any other module.</span></span>

### <a name="to-import-a-module-from-the-automation-module-gallery-with-the-azure-portal"></a><span data-ttu-id="64efb-169">透過 Azure 入口網站從自動化模組資源庫匯入模組</span><span class="sxs-lookup"><span data-stu-id="64efb-169">To import a module from the Automation Module Gallery with the Azure portal</span></span>
1. <span data-ttu-id="64efb-170">在 Azure 入口網站中，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="64efb-170">In the Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="64efb-171">按一下 [ **資產** ] 磚以開啟資產的清單。</span><span class="sxs-lookup"><span data-stu-id="64efb-171">Click on the **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="64efb-172">按一下 [ **模組** ] 磚以開啟模組的清單。</span><span class="sxs-lookup"><span data-stu-id="64efb-172">Click on the **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="64efb-173">按一下 [瀏覽資源庫]  按鈕，即可啟動 [瀏覽資源庫] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64efb-173">Click on the **Browse gallery** button and the Browse gallery blade is launched.</span></span>
   
    ![模組資源庫](media/automation-runbook-gallery/modules-blade.png) <br>
5. <span data-ttu-id="64efb-175">啟動 [瀏覽資源庫] 刀鋒視窗後，您就可以搜尋下列欄位：</span><span class="sxs-lookup"><span data-stu-id="64efb-175">After you have launched the Browse gallery blade, you can search by the following fields:</span></span>
   
   * <span data-ttu-id="64efb-176">模組名稱</span><span class="sxs-lookup"><span data-stu-id="64efb-176">Module Name</span></span>
   * <span data-ttu-id="64efb-177">標記</span><span class="sxs-lookup"><span data-stu-id="64efb-177">Tags</span></span>
   * <span data-ttu-id="64efb-178">作者</span><span class="sxs-lookup"><span data-stu-id="64efb-178">Author</span></span>
   * <span data-ttu-id="64efb-179">Cmdlet/DSC 資源名稱</span><span class="sxs-lookup"><span data-stu-id="64efb-179">Cmdlet/DSC resource name</span></span>
6. <span data-ttu-id="64efb-180">尋找您感興趣的模組，並選取以檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="64efb-180">Locate a module that you're interested in and select it to view its details.</span></span>  
   <span data-ttu-id="64efb-181">當您向下切入到特定的模組時，您可以檢視有關該模組的詳細資訊，包括返回 PowerShell 資源庫的連結、任何必要的相依性，以及該模組包含的所有 cmdlet 和 (或) DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="64efb-181">When you drill into a specific module, you can view more information about the module, including a link back to the PowerShell Gallery, any required dependencies, and all of the cmdlets and/or DSC resources that the module contains.</span></span>
   
    ![PowerShell 模組的詳細資料](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. <span data-ttu-id="64efb-183">若要將該模組直接安裝至 Azure 自動化，請按一下 [匯入]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="64efb-183">To install the module directly into Azure Automation, click the **Import** button.</span></span>
   
    ![[匯入模組] 按鈕](media/automation-runbook-gallery/module-import-button.png)
8. <span data-ttu-id="64efb-185">按一下 [匯入] 按鈕時，會看到要匯入的模組名稱。</span><span class="sxs-lookup"><span data-stu-id="64efb-185">When you click the Import button, you will see the module name that you are about to import.</span></span> <span data-ttu-id="64efb-186">如果已安裝所有相依性，便可使用 [確定]  。</span><span class="sxs-lookup"><span data-stu-id="64efb-186">If all the dependencies are installed, the **OK** button will be active.</span></span> <span data-ttu-id="64efb-187">如果缺少相依性，需先加以匯入後才能匯入該模組。</span><span class="sxs-lookup"><span data-stu-id="64efb-187">If you are missing dependencies, you need to import those before you can import this module.</span></span>
9. <span data-ttu-id="64efb-188">按一下 [確定]  匯入模組，即可啟動 [模組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64efb-188">Click **OK** to import the module, and the module blade will launch.</span></span> <span data-ttu-id="64efb-189">當 Azure 自動化模組匯入到您的帳戶時，會擷取有關模組和 cmdlet 的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="64efb-189">When Azure Automation imports a module to your account, it extracts metadata about the module and the cmdlets.</span></span>
   
    ![[匯入模組] 刀鋒視窗](media/automation-runbook-gallery/module-import-blade.png)
   
    <span data-ttu-id="64efb-191">因為必須解壓縮每個活動，此步驟可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="64efb-191">This may take a couple of minutes since each activity needs to be extracted.</span></span>
10. <span data-ttu-id="64efb-192">您會在模組已部署以及模組完成時收到通知。</span><span class="sxs-lookup"><span data-stu-id="64efb-192">You will receive a notification that the module is being deployed and a notification when it has completed.</span></span>
11. <span data-ttu-id="64efb-193">在匯入模組之後，會看到可用的活動。您可以將其資源用於您的 Runbook 和預期狀態設定中。</span><span class="sxs-lookup"><span data-stu-id="64efb-193">After the module is imported, you will see the available activities, and you can use its resources in your runbooks and Desired State Configuration.</span></span>

## <a name="requesting-a-runbook-or-module"></a><span data-ttu-id="64efb-194">要求 Runbook 或模組</span><span class="sxs-lookup"><span data-stu-id="64efb-194">Requesting a runbook or module</span></span>
<span data-ttu-id="64efb-195">您可以將要求傳送至 [使用者心聲](https://feedback.azure.com/forums/246290-azure-automation/)。</span><span class="sxs-lookup"><span data-stu-id="64efb-195">You can send requests to [User Voice](https://feedback.azure.com/forums/246290-azure-automation/).</span></span>  <span data-ttu-id="64efb-196">如果您需要協助撰寫 Runbook 或有關於 PowerShell 的問題，請將問題張貼至我們的 [論壇](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc)。</span><span class="sxs-lookup"><span data-stu-id="64efb-196">If you need help writing a runbook or have a question about PowerShell, post a question to our [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).</span></span>

## <a name="next-steps"></a><span data-ttu-id="64efb-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64efb-197">Next Steps</span></span>
* <span data-ttu-id="64efb-198">若要開始使用 Runbook，請參閱 [在 Azure 自動化中建立或匯入 Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="64efb-198">To get started with runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="64efb-199">若要了解含有 Runbook 的 PowerShell 和 PowerShell 工作流程之間的差異，請參閱 [了解 PowerShell 工作流程](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="64efb-199">To understand the differences between PowerShell and PowerShell Workflow with runbooks, see [Learning PowerShell workflow](automation-powershell-workflow.md)</span></span>

