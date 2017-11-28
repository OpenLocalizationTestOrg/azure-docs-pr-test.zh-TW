---
title: "Azure 自動化 aaaRunbook 和模組組件庫 |Microsoft 文件"
description: "Runbook 與模組的 Microsoft 和 hello 社群成員可供您 tooinstall，而且您的 Azure 自動化環境中使用。  本文說明如何存取這些資源和 toocontribute runbook toohello 圖庫。"
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
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a><span data-ttu-id="015c5-104">Azure 自動化的 Runbook 和模組資源庫</span><span class="sxs-lookup"><span data-stu-id="015c5-104">Runbook and module galleries for Azure Automation</span></span>
<span data-ttu-id="015c5-105">而不是在 Azure 自動化中建立您自己的 runbook 與模組，您可以存取的各種已經建置由 Microsoft 和 hello 社群的案例。</span><span class="sxs-lookup"><span data-stu-id="015c5-105">Rather than creating your own runbooks and modules in Azure Automation, you can access a variety of scenarios that have already been built by Microsoft and hello community.</span></span>  <span data-ttu-id="015c5-106">您可以不加修改地使用這些案例，或者使用它們做為起點並針對您的特定需求進行編輯。</span><span class="sxs-lookup"><span data-stu-id="015c5-106">You can either use these scenarios without modification or you can use them as a starting point and edit them for your specific requirements.</span></span>

<span data-ttu-id="015c5-107">您可以從 hello 取得 runbook [Runbook 庫](#runbooks-in-runbook-gallery)和模組從 hello [PowerShell 資源庫](#modules-in-powerShell-gallery)。</span><span class="sxs-lookup"><span data-stu-id="015c5-107">You can get runbooks from hello [Runbook Gallery](#runbooks-in-runbook-gallery) and modules from hello [PowerShell Gallery](#modules-in-powerShell-gallery).</span></span>  <span data-ttu-id="015c5-108">您也可以透過分享您所開發的案例會導致 toohello 社群。</span><span class="sxs-lookup"><span data-stu-id="015c5-108">You can also contribute toohello community by sharing scenarios that you develop.</span></span>

## <a name="runbooks-in-runbook-gallery"></a><span data-ttu-id="015c5-109">Runbook 資源庫中的 Runbook</span><span class="sxs-lookup"><span data-stu-id="015c5-109">Runbooks in Runbook Gallery</span></span>
<span data-ttu-id="015c5-110">hello [Runbook 庫](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation)從 Microsoft 和 hello 社群，您可以匯入至 Azure 自動化中提供各種不同的 runbook。</span><span class="sxs-lookup"><span data-stu-id="015c5-110">hello [Runbook Gallery](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) provides a variety of runbooks from Microsoft and hello community that you can import into Azure Automation.</span></span> <span data-ttu-id="015c5-111">您可以從裝載於 hello hello 組件庫下載 runbook [TechNet 指令碼中心](https://gallery.technet.microsoft.com/scriptcenter/site/upload)，或您可以從 hello 庫 hello Azure 傳統入口網站或 Azure 入口網站直接匯入 runbook。</span><span class="sxs-lookup"><span data-stu-id="015c5-111">You can either download a runbook from hello gallery which is hosted in hello [TechNet Script Center](https://gallery.technet.microsoft.com/scriptcenter/site/upload), or you can directly import runbooks from hello gallery from either hello Azure classic portal or Azure portal.</span></span>

<span data-ttu-id="015c5-112">您可以只匯入直接從 hello Runbook 庫使用 hello Azure 傳統入口網站或 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="015c5-112">You can only import directly from hello Runbook Gallery using hello Azure classic portal or Azure portal.</span></span> <span data-ttu-id="015c5-113">您無法使用 Windows PowerShell 執行此函式。</span><span class="sxs-lookup"><span data-stu-id="015c5-113">You cannot perform this function using Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="015c5-114">您應該驗證 hello 內容從 hello Runbook 庫取得，且小心中安裝及執行它們在生產環境中的任何 runbook。 |</span><span class="sxs-lookup"><span data-stu-id="015c5-114">You should validate hello contents of any runbooks that you get from hello Runbook Gallery and use extreme caution in installing and running them in a production environment.|</span></span>
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a><span data-ttu-id="015c5-115">tooimport hello Runbook 資源庫以 hello Azure 傳統入口網站的 runbook</span><span class="sxs-lookup"><span data-stu-id="015c5-115">tooimport a runbook from hello Runbook Gallery with hello Azure classic portal</span></span>
1. <span data-ttu-id="015c5-116">在 hello Azure 入口網站中，按一下，**新增**，**應用程式服務**，**自動化**， **Runbook**，**從組件庫**.</span><span class="sxs-lookup"><span data-stu-id="015c5-116">In hello Azure Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **From Gallery**.</span></span>
2. <span data-ttu-id="015c5-117">選取類別目錄 tooview 相關 runbook，然後選取 runbook tooview 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="015c5-117">Select a category tooview related runbooks, and select a runbook tooview its details.</span></span> <span data-ttu-id="015c5-118">當您選取您想要的 hello runbook 時，請按一下 hello 向右箭號按鈕。</span><span class="sxs-lookup"><span data-stu-id="015c5-118">When you select hello runbook you want, click hello right arrow button.</span></span>
   
    ![Runbook 資源庫](media/automation-runbook-gallery/runbook-gallery.png)
3. <span data-ttu-id="015c5-120">檢閱 hello hello runbook 內容，並記下 hello 描述中的任何需求。</span><span class="sxs-lookup"><span data-stu-id="015c5-120">Review hello contents of hello runbook and note any requirements in hello description.</span></span> <span data-ttu-id="015c5-121">當您完成時，請按一下 hello 向右箭號按鈕。</span><span class="sxs-lookup"><span data-stu-id="015c5-121">Click hello right arrow button when you’re done.</span></span>
4. <span data-ttu-id="015c5-122">輸入 hello runbook 詳細資料，然後按一下hello 核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="015c5-122">Enter hello runbook details and then click hello checkmark button.</span></span> <span data-ttu-id="015c5-123">將已填入 hello runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="015c5-123">hello runbook name will already be filled in.</span></span>
5. <span data-ttu-id="015c5-124">hello runbook 會出現在 hello **Runbook** hello 自動化帳戶 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="015c5-124">hello runbook will appear on hello **Runbooks** tab for hello Automation Account.</span></span>

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a><span data-ttu-id="015c5-125">tooimport hello Runbook 資源庫以 hello Azure 入口網站的 runbook</span><span class="sxs-lookup"><span data-stu-id="015c5-125">tooimport a runbook from hello Runbook Gallery with hello Azure portal</span></span>
1. <span data-ttu-id="015c5-126">在 hello Azure 入口網站，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="015c5-126">In hello Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="015c5-127">按一下 hello **Runbook**磚 tooopen hello runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="015c5-127">Click on hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="015c5-128">按一下 [瀏覽資源庫]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="015c5-128">Click **Browse gallery** button.</span></span>
   
    ![瀏覽資源庫按鈕](media/automation-runbook-gallery/browse-gallery-button.png)
4. <span data-ttu-id="015c5-130">找出 hello 主機庫項目，然後選取它 tooview 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="015c5-130">Locate hello gallery item you want and select it tooview its details.</span></span>
   
    ![瀏覽資源庫](media/automation-runbook-gallery/browse-gallery.png)
5. <span data-ttu-id="015c5-132">按一下**檢視原始碼專案**tooview hello 項目在 hello [TechNet 指令碼中心](http://gallery.technet.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="015c5-132">Click on **View source project** tooview hello item in hello [TechNet Script Center](http://gallery.technet.microsoft.com/).</span></span>
6. <span data-ttu-id="015c5-133">tooimport 項目，按一下 tooview 其詳細資料，然後按一下hello**匯入** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="015c5-133">tooimport an item, click on it tooview its details and then click hello **Import** button.</span></span>
   
    ![匯入按鈕](media/automation-runbook-gallery/gallery-item-detail.png)
7. <span data-ttu-id="015c5-135">（選擇性） 變更 hello hello runbook 名稱，然後按一下**確定**tooimport hello runbook。</span><span class="sxs-lookup"><span data-stu-id="015c5-135">Optionally, change hello name of hello runbook and then click **OK** tooimport hello runbook.</span></span>
8. <span data-ttu-id="015c5-136">hello runbook 會出現在 hello **Runbook** hello 自動化帳戶 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="015c5-136">hello runbook will appear on hello **Runbooks** tab for hello Automation Account.</span></span>

### <a name="adding-a-runbook-toohello-runbook-gallery"></a><span data-ttu-id="015c5-137">新增 runbook toohello runbook 資源庫</span><span class="sxs-lookup"><span data-stu-id="015c5-137">Adding a runbook toohello runbook gallery</span></span>
<span data-ttu-id="015c5-138">Microsoft 會鼓勵 tooadd runbook toohello 您認為有用 tooother 客戶的 Runbook 資源庫。</span><span class="sxs-lookup"><span data-stu-id="015c5-138">Microsoft encourages you tooadd runbooks toohello Runbook Gallery that you think would be useful tooother customers.</span></span>  <span data-ttu-id="015c5-139">您可以新增 runbook[將資料上傳 toohello 指令碼中心](http://gallery.technet.microsoft.com/site/upload)納入帳戶 hello 下列詳細資料。</span><span class="sxs-lookup"><span data-stu-id="015c5-139">You can add a runbook by [uploading it toohello Script Center](http://gallery.technet.microsoft.com/site/upload) taking into account hello following details.</span></span>

* <span data-ttu-id="015c5-140">您必須指定*Windows Azure* hello**類別**和*自動化*hello **Subcategory**的 hello runbook toobe 顯示在 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="015c5-140">You must specify *Windows Azure* for hello **Category** and *Automation* for hello **Subcategory** for hello runbook toobe displayed in hello wizard.</span></span>  
* <span data-ttu-id="015c5-141">hello 上載必須是單一.ps1 或.graphrunbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="015c5-141">hello upload must be a single .ps1 or .graphrunbook file.</span></span>  <span data-ttu-id="015c5-142">如果 hello runbook 需要任何模組、 子系 runbook 或資產，則您應該列出 hello 送出 hello 描述中，並且在 hello runbook hello 註解區段。</span><span class="sxs-lookup"><span data-stu-id="015c5-142">If hello runbook requires any modules, child runbooks, or assets, then you should list those in hello description of hello submission and in hello comments section of hello runbook.</span></span>  <span data-ttu-id="015c5-143">如果您需要多個 runbook 的案例，然後才能上傳每個個別，以及列出 hello 名稱的 hello 相關各項描述中的 runbook。</span><span class="sxs-lookup"><span data-stu-id="015c5-143">If you have a scenario requiring multiple runbooks, then upload each separately and list hello names of hello related runbooks in each of their descriptions.</span></span> <span data-ttu-id="015c5-144">請確定您使用的相同標記，因此它們會顯示在 hello hello 相同類別目錄。</span><span class="sxs-lookup"><span data-stu-id="015c5-144">Make sure that you use hello same tags so that they will show up in hello same category.</span></span> <span data-ttu-id="015c5-145">使用者會有其他 runbook 所需要的 hello 案例 toowork tooread hello 描述 tooknow。</span><span class="sxs-lookup"><span data-stu-id="015c5-145">A user will have tooread hello description tooknow that other runbooks are required hello scenario toowork.</span></span>
* <span data-ttu-id="015c5-146">如果您要發行，加入 hello 標記"GraphicalPS"**圖形化 runbook** （沒有圖形化工作流程）。</span><span class="sxs-lookup"><span data-stu-id="015c5-146">Add hello tag "GraphicalPS" if you are publishing a **Graphical runbook** (not a Graphical Workflow).</span></span> 
* <span data-ttu-id="015c5-147">插入 hello 說明使用 PowerShell 或 PowerShell 工作流程的程式碼片段**插入程式碼區段**圖示。</span><span class="sxs-lookup"><span data-stu-id="015c5-147">Insert either a PowerShell or PowerShell Workflow code snippet into hello description using **Insert code section** icon.</span></span>
* <span data-ttu-id="015c5-148">hello hello 上傳摘要會顯示在 Runbook 庫結果，因此您應該提供詳細的資訊可協助使用者識別的 hello runbook 的 hello 功能 hello。</span><span class="sxs-lookup"><span data-stu-id="015c5-148">hello Summary for hello upload will be displayed in hello Runbook Gallery results so you should provide detailed information that will help a user identify hello functionality of hello runbook.</span></span>
* <span data-ttu-id="015c5-149">您應指派一個 toothree 的 hello 下列標記 toohello 上傳。</span><span class="sxs-lookup"><span data-stu-id="015c5-149">You should assign one toothree of hello following Tags toohello upload.</span></span>  <span data-ttu-id="015c5-150">hello runbook 會列出在 hello 精靈中符合 runbook 標記的 hello 類別之下。</span><span class="sxs-lookup"><span data-stu-id="015c5-150">hello runbook will be listed in hello wizard under hello categories that match its tags.</span></span>  <span data-ttu-id="015c5-151">Hello 精靈會略過此清單上沒有任何標記。</span><span class="sxs-lookup"><span data-stu-id="015c5-151">Any tags not on this list will be ignored by hello wizard.</span></span> <span data-ttu-id="015c5-152">如果您未指定任何相符的標記，hello runbook 將會列在 hello 其他類別。</span><span class="sxs-lookup"><span data-stu-id="015c5-152">If you don’t specify any matching tags, hello runbook will be listed under hello Other category.</span></span>
  
  * <span data-ttu-id="015c5-153">備份</span><span class="sxs-lookup"><span data-stu-id="015c5-153">Backup</span></span>
  * <span data-ttu-id="015c5-154">產能管理</span><span class="sxs-lookup"><span data-stu-id="015c5-154">Capacity Management</span></span>
  * <span data-ttu-id="015c5-155">變更控制</span><span class="sxs-lookup"><span data-stu-id="015c5-155">Change Control</span></span>
  * <span data-ttu-id="015c5-156">法規遵循</span><span class="sxs-lookup"><span data-stu-id="015c5-156">Compliance</span></span>
  * <span data-ttu-id="015c5-157">開發/測試環境</span><span class="sxs-lookup"><span data-stu-id="015c5-157">Dev / Test Environments</span></span>
  * <span data-ttu-id="015c5-158">災害復原</span><span class="sxs-lookup"><span data-stu-id="015c5-158">Disaster Recovery</span></span>
  * <span data-ttu-id="015c5-159">監視</span><span class="sxs-lookup"><span data-stu-id="015c5-159">Monitoring</span></span>
  * <span data-ttu-id="015c5-160">修補</span><span class="sxs-lookup"><span data-stu-id="015c5-160">Patching</span></span>
  * <span data-ttu-id="015c5-161">佈建</span><span class="sxs-lookup"><span data-stu-id="015c5-161">Provisioning</span></span>
  * <span data-ttu-id="015c5-162">補救</span><span class="sxs-lookup"><span data-stu-id="015c5-162">Remediation</span></span>
  * <span data-ttu-id="015c5-163">VM 生命週期管理</span><span class="sxs-lookup"><span data-stu-id="015c5-163">VM Lifecycle Management</span></span>
* <span data-ttu-id="015c5-164">自動化更新 hello 圖庫小時一次，所以不會立即看到您的貢獻。</span><span class="sxs-lookup"><span data-stu-id="015c5-164">Automation updates hello Gallery once an hour, so you won’t see your contributions immediately.</span></span>

## <a name="modules-in-powershell-gallery"></a><span data-ttu-id="015c5-165">PowerShell 資源庫中的模組</span><span class="sxs-lookup"><span data-stu-id="015c5-165">Modules in PowerShell Gallery</span></span>
<span data-ttu-id="015c5-166">PowerShell 模組包含 cmdlet，您可以使用您的 runbook 中，您可以安裝在 Azure 自動化中的現有模組在 hello [PowerShell 資源庫](http://www.powershellgallery.com)。</span><span class="sxs-lookup"><span data-stu-id="015c5-166">PowerShell modules contain cmdlets that you can use in your runbooks, and existing modules that you can install in Azure Automation are available in hello [PowerShell Gallery](http://www.powershellgallery.com).</span></span>  <span data-ttu-id="015c5-167">您可以啟動這個組件庫，從 hello Azure 入口網站，並直接在 Azure 自動化安裝，或您可以下載它們並手動進行安裝。</span><span class="sxs-lookup"><span data-stu-id="015c5-167">You can launch this gallery from hello Azure portal and install them directly into Azure Automation or you can download them and install them manually.</span></span>  <span data-ttu-id="015c5-168">您無法直接從 hello Azure 傳統入口網站安裝 hello 模組，但您也可以將其下載安裝它們，如同任何其他模組。</span><span class="sxs-lookup"><span data-stu-id="015c5-168">You cannot install hello modules directly from hello Azure classic portal, but you can download them install them as you would any other module.</span></span>

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a><span data-ttu-id="015c5-169">tooimport hello 自動化模組資源庫以 hello Azure 入口網站的模組</span><span class="sxs-lookup"><span data-stu-id="015c5-169">tooimport a module from hello Automation Module Gallery with hello Azure portal</span></span>
1. <span data-ttu-id="015c5-170">在 hello Azure 入口網站，開啟您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="015c5-170">In hello Azure Portal, open your Automation account.</span></span>
2. <span data-ttu-id="015c5-171">按一下 hello**資產**磚 tooopen hello 列出的資產清單。</span><span class="sxs-lookup"><span data-stu-id="015c5-171">Click on hello **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="015c5-172">按一下 hello**模組**磚 tooopen hello 模組的清單。</span><span class="sxs-lookup"><span data-stu-id="015c5-172">Click on hello **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="015c5-173">按一下 hello**瀏覽圖庫**啟動按鈕和 hello 瀏覽圖庫刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="015c5-173">Click on hello **Browse gallery** button and hello Browse gallery blade is launched.</span></span>
   
    ![模組資源庫](media/automation-runbook-gallery/modules-blade.png) <br>
5. <span data-ttu-id="015c5-175">您啟動 hello 瀏覽圖庫刀鋒視窗之後，您可以搜尋下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="015c5-175">After you have launched hello Browse gallery blade, you can search by hello following fields:</span></span>
   
   * <span data-ttu-id="015c5-176">模組名稱</span><span class="sxs-lookup"><span data-stu-id="015c5-176">Module Name</span></span>
   * <span data-ttu-id="015c5-177">標記</span><span class="sxs-lookup"><span data-stu-id="015c5-177">Tags</span></span>
   * <span data-ttu-id="015c5-178">作者</span><span class="sxs-lookup"><span data-stu-id="015c5-178">Author</span></span>
   * <span data-ttu-id="015c5-179">Cmdlet/DSC 資源名稱</span><span class="sxs-lookup"><span data-stu-id="015c5-179">Cmdlet/DSC resource name</span></span>
6. <span data-ttu-id="015c5-180">找出您感興趣，並選取該 tooview 模組其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="015c5-180">Locate a module that you're interested in and select it tooview its details.</span></span>  
   <span data-ttu-id="015c5-181">當您向下鑽研至特定模組時，您可以檢視需 hello 模組，包括連結後 toohello PowerShell 資源庫中，任何必要的相依性，而且所有 hello cmdlet 及/或 hello 模組的 DSC 資源的包含。</span><span class="sxs-lookup"><span data-stu-id="015c5-181">When you drill into a specific module, you can view more information about hello module, including a link back toohello PowerShell Gallery, any required dependencies, and all of hello cmdlets and/or DSC resources that hello module contains.</span></span>
   
    ![PowerShell 模組的詳細資料](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. <span data-ttu-id="015c5-183">tooinstall hello 模組，直接在 Azure 自動化中，按一下 [hello**匯入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="015c5-183">tooinstall hello module directly into Azure Automation, click hello **Import** button.</span></span>
   
    ![[匯入模組] 按鈕](media/automation-runbook-gallery/module-import-button.png)
8. <span data-ttu-id="015c5-185">當您按一下 hello 匯入 按鈕時，您會看到您所需 tooimport hello 模組名稱。</span><span class="sxs-lookup"><span data-stu-id="015c5-185">When you click hello Import button, you will see hello module name that you are about tooimport.</span></span> <span data-ttu-id="015c5-186">如果已安裝所有的 hello 相依性，hello**確定**按鈕將處於使用中。</span><span class="sxs-lookup"><span data-stu-id="015c5-186">If all hello dependencies are installed, hello **OK** button will be active.</span></span> <span data-ttu-id="015c5-187">如果您遺漏相依性，您需要 tooimport 這些之前您可以匯入此模組。</span><span class="sxs-lookup"><span data-stu-id="015c5-187">If you are missing dependencies, you need tooimport those before you can import this module.</span></span>
9. <span data-ttu-id="015c5-188">按一下**確定**tooimport hello 模組和 hello 模組刀鋒視窗，將會啟動。</span><span class="sxs-lookup"><span data-stu-id="015c5-188">Click **OK** tooimport hello module, and hello module blade will launch.</span></span> <span data-ttu-id="015c5-189">當 Azure 自動化匯入模組 tooyour 帳戶時，它會擷取 hello 模組和 hello 指令程式的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="015c5-189">When Azure Automation imports a module tooyour account, it extracts metadata about hello module and hello cmdlets.</span></span>
   
    ![[匯入模組] 刀鋒視窗](media/automation-runbook-gallery/module-import-blade.png)
   
    <span data-ttu-id="015c5-191">因為每個活動需要 toobe 擷取，這可能需要數分鐘。</span><span class="sxs-lookup"><span data-stu-id="015c5-191">This may take a couple of minutes since each activity needs toobe extracted.</span></span>
10. <span data-ttu-id="015c5-192">您會收到通知正在部署該 hello 模組的通知完成時。</span><span class="sxs-lookup"><span data-stu-id="015c5-192">You will receive a notification that hello module is being deployed and a notification when it has completed.</span></span>
11. <span data-ttu-id="015c5-193">Hello 模組匯入之後，您會看到 hello 可用的活動，而且您可以使用其在您的 runbook 和預期狀態設定資源。</span><span class="sxs-lookup"><span data-stu-id="015c5-193">After hello module is imported, you will see hello available activities, and you can use its resources in your runbooks and Desired State Configuration.</span></span>

## <a name="requesting-a-runbook-or-module"></a><span data-ttu-id="015c5-194">要求 Runbook 或模組</span><span class="sxs-lookup"><span data-stu-id="015c5-194">Requesting a runbook or module</span></span>
<span data-ttu-id="015c5-195">您可以將要求傳送太[User Voice](https://feedback.azure.com/forums/246290-azure-automation/)。</span><span class="sxs-lookup"><span data-stu-id="015c5-195">You can send requests too[User Voice](https://feedback.azure.com/forums/246290-azure-automation/).</span></span>  <span data-ttu-id="015c5-196">如果您需要協助撰寫 runbook，或有 PowerShell 疑問，張貼問題 tooour[論壇](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc)。</span><span class="sxs-lookup"><span data-stu-id="015c5-196">If you need help writing a runbook or have a question about PowerShell, post a question tooour [forum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).</span></span>

## <a name="next-steps"></a><span data-ttu-id="015c5-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="015c5-197">Next Steps</span></span>
* <span data-ttu-id="015c5-198">tooget 啟動 runbook，請參閱[建立或匯入在 Azure 自動化 runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="015c5-198">tooget started with runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="015c5-199">toounderstand hello 差異 PowerShell 和 PowerShell 工作流程與 runbook，請參閱[學習 PowerShell 工作流程](automation-powershell-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="015c5-199">toounderstand hello differences between PowerShell and PowerShell Workflow with runbooks, see [Learning PowerShell workflow](automation-powershell-workflow.md)</span></span>

