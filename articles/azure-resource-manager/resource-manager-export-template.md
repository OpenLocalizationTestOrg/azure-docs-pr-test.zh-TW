---
title: "aaaExport Azure Resource Manager 範本 |Microsoft 文件"
description: "使用 Azure 資源管理 tooexport 現有的資源群組中的範本。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="82651-103">從現有資源匯出 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="82651-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="82651-104">在本文中，您將學習如何 tooexport Resource Manager 範本使用從您的訂用帳戶中現有的資源。</span><span class="sxs-lookup"><span data-stu-id="82651-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="82651-105">您可以使用該產生的範本 toogain 進一步了解樣板語法。</span><span class="sxs-lookup"><span data-stu-id="82651-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="82651-106">有兩種方式 tooexport 範本：</span><span class="sxs-lookup"><span data-stu-id="82651-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="82651-107">您可以匯出 hello**用於部署的實際範本**。</span><span class="sxs-lookup"><span data-stu-id="82651-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="82651-108">hello 匯出的範本包含所有 hello 參數和變數，如同它們是出現在 hello 原始範本。</span><span class="sxs-lookup"><span data-stu-id="82651-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="82651-109">此方法時，很有幫助您部署的 hello 入口網站，透過資源，並想 toosee hello 範本 toocreate 那些資源。</span><span class="sxs-lookup"><span data-stu-id="82651-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="82651-110">此範本立即可用。</span><span class="sxs-lookup"><span data-stu-id="82651-110">This template is readily usable.</span></span> 
* <span data-ttu-id="82651-111">您可以匯出**產生代表 hello hello 資源群組的目前狀態的範本**。</span><span class="sxs-lookup"><span data-stu-id="82651-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="82651-112">hello 匯出的範本不根據您用於部署的任何範本。</span><span class="sxs-lookup"><span data-stu-id="82651-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="82651-113">相反地，它會建立 hello 資源群組的快照集的範本。</span><span class="sxs-lookup"><span data-stu-id="82651-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="82651-114">hello 匯出的範本有許多的硬式編碼值，可能不一樣多的參數，因為您通常會定義。</span><span class="sxs-lookup"><span data-stu-id="82651-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="82651-115">當您在部署後修改了 hello 資源群組，則這個方法會很有用。</span><span class="sxs-lookup"><span data-stu-id="82651-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="82651-116">此範本通常需要修改才能使用。</span><span class="sxs-lookup"><span data-stu-id="82651-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="82651-117">本主題說明這兩種方法，透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="82651-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="82651-118">部署資源</span><span class="sxs-lookup"><span data-stu-id="82651-118">Deploy resources</span></span>
<span data-ttu-id="82651-119">讓我們開始部署，您可以使用匯出為範本的資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="82651-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="82651-120">如果您已經有資源群組訂閱您想要 tooexport tooa 範本中，您可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="82651-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="82651-121">hello 本文其餘部分會假設您已部署 hello web 應用程式和本節中所顯示的 SQL 資料庫解決方案。</span><span class="sxs-lookup"><span data-stu-id="82651-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="82651-122">如果您使用不同的解決方案，您的體驗可能會稍有不同，但 hello 步驟 tooexport 範本是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="82651-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="82651-123">在 hello [Azure 入口網站](https://portal.azure.com)，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="82651-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![選取 [新增]](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="82651-125">搜尋**web 應用程式 + SQL**和選取從 hello 可用的選項。</span><span class="sxs-lookup"><span data-stu-id="82651-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![搜尋 Web 應用程式和 SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="82651-127">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="82651-127">Select **Create**.</span></span>

      ![選取 [建立]](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="82651-129">提供所需的 hello 值 hello web 應用程式和 SQL database。</span><span class="sxs-lookup"><span data-stu-id="82651-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="82651-130">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="82651-130">Select **Create**.</span></span>

      ![提供 Web 和 SQL 值](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="82651-132">hello 部署可能會花一分鐘。</span><span class="sxs-lookup"><span data-stu-id="82651-132">hello deployment may take a minute.</span></span> <span data-ttu-id="82651-133">Hello 部署完成之後，您的訂用帳戶包含 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="82651-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="82651-134">從部署記錄中檢視範本</span><span class="sxs-lookup"><span data-stu-id="82651-134">View template from deployment history</span></span>
1. <span data-ttu-id="82651-135">移 toohello 資源群組刀鋒視窗，新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="82651-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="82651-136">請注意該 hello 刀鋒視窗會顯示 hello 最後一個部署的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="82651-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="82651-137">選取此連結。</span><span class="sxs-lookup"><span data-stu-id="82651-137">Select this link.</span></span>
   
      ![資源群組刀鋒視窗](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="82651-139">您會看到 hello 群組部署的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="82651-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="82651-140">在您的情況下，hello 刀鋒視窗可能會列出只能有一個部署。</span><span class="sxs-lookup"><span data-stu-id="82651-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="82651-141">選取此部署。</span><span class="sxs-lookup"><span data-stu-id="82651-141">Select this deployment.</span></span>
   
     ![上次部署](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="82651-143">hello 刀鋒視窗會顯示 hello 部署的摘要。</span><span class="sxs-lookup"><span data-stu-id="82651-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="82651-144">hello 摘要包含 hello 部署的 hello 狀態及作業以及您為參數提供的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="82651-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="82651-145">您用於 hello 部署中，選取 toosee hello 範本**檢視範本**。</span><span class="sxs-lookup"><span data-stu-id="82651-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![檢視部署摘要](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="82651-147">下列為您的七個檔案的資源管理員擷取 hello:</span><span class="sxs-lookup"><span data-stu-id="82651-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="82651-148">**範本**-hello 範本可定義您方案的 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="82651-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="82651-149">當您建立 hello 透過 hello 入口網站的儲存體帳戶時，資源管理員會使用範本 toodeploy 它並儲存供日後參考該範本。</span><span class="sxs-lookup"><span data-stu-id="82651-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="82651-150">**參數**-參數檔案，您可以在部署期間在值中使用 toopass。</span><span class="sxs-lookup"><span data-stu-id="82651-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="82651-151">它包含您在第一次部署的 hello 期間提供的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="82651-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="82651-152">當您重新部署的 hello 範本時，您可以變更這些值。</span><span class="sxs-lookup"><span data-stu-id="82651-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="82651-153">**CLI** -Azure 命令列介面 (CLI) 指令碼檔案，您可以使用 toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="82651-154">**CLI 2.0** -Azure 命令列介面 (CLI) 指令碼檔案，您可以使用 toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="82651-155">**PowerShell** -您可以使用 toodeploy hello 範本的 Azure PowerShell 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="82651-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="82651-156">**.NET** -您可以使用 toodeploy hello 範本的.NET 類別。</span><span class="sxs-lookup"><span data-stu-id="82651-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="82651-157">**Ruby** -A Ruby 類別，您可以使用 toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="82651-158">hello 檔可透過連結跨 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="82651-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="82651-159">根據預設，hello 刀鋒視窗會顯示 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-159">By default, hello blade displays hello template.</span></span>
      
       ![檢視範本](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="82651-161">此範本是使用 toocreate hello 實際範本您 web 應用程式和 SQL database。</span><span class="sxs-lookup"><span data-stu-id="82651-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="82651-162">請注意它包含可讓您 tooprovide 不同的值在部署期間的參數。</span><span class="sxs-lookup"><span data-stu-id="82651-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="82651-163">toolearn 進一步了解 hello 結構的範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="82651-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="82651-164">從資源群組匯出 hello 範本</span><span class="sxs-lookup"><span data-stu-id="82651-164">Export hello template from resource group</span></span>
<span data-ttu-id="82651-165">如果您手動變更您的資源或將資源加入多個部署中，從 hello 部署歷程記錄中擷取範本並不會反映 hello hello 資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="82651-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="82651-166">本節說明如何 tooexport 範本，以反映 hello hello 資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="82651-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="82651-167">您無法針對具有超過 200 個資源的資源群組匯出範本。</span><span class="sxs-lookup"><span data-stu-id="82651-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="82651-168">資源群組中，選取 tooview hello 範本**自動化指令碼**。</span><span class="sxs-lookup"><span data-stu-id="82651-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![匯出資源群組](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="82651-170">資源管理員會評估 hello hello 資源群組中的資源，並產生這些資源的範本。</span><span class="sxs-lookup"><span data-stu-id="82651-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="82651-171">並非所有的資源類型都支援 hello 匯出樣板函式。</span><span class="sxs-lookup"><span data-stu-id="82651-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="82651-172">您可能會看到錯誤指出 hello 匯出問題。</span><span class="sxs-lookup"><span data-stu-id="82651-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="82651-173">您了解如何 toohandle 那些問題 hello[修正匯出問題](#fix-export-issues)> 一節。</span><span class="sxs-lookup"><span data-stu-id="82651-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="82651-174">同樣地，您會看到 hello 六個檔案中，您可以使用 tooredeploy hello 方案。</span><span class="sxs-lookup"><span data-stu-id="82651-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="82651-175">不過，此時間 hello 範本是稍有不同。</span><span class="sxs-lookup"><span data-stu-id="82651-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="82651-176">請注意，hello 產生的範本包含比上一節中的 hello 範本較少的參數。</span><span class="sxs-lookup"><span data-stu-id="82651-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="82651-177">此外，許多 hello 值 （如位置和 SKU 值） 是硬式編碼這個範本，而不會接受參數值。</span><span class="sxs-lookup"><span data-stu-id="82651-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="82651-178">重複使用此範本之前, 您可能想 tooedit hello 範本 toomake 更妥善運用參數。</span><span class="sxs-lookup"><span data-stu-id="82651-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="82651-179">您有幾個選項用於接續 toowork 與此範本。</span><span class="sxs-lookup"><span data-stu-id="82651-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="82651-180">您可以下載 hello 範本，並使用它在本機 JSON 編輯器。</span><span class="sxs-lookup"><span data-stu-id="82651-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="82651-181">或者，您可以儲存 hello 範本庫 tooyour 並處理它，透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="82651-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="82651-182">如果您想要使用 JSON 編輯器，例如[VS Code](https://code.visualstudio.com/)或[Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)，您可能會偏好下載本機 hello 範本並使用該編輯器。</span><span class="sxs-lookup"><span data-stu-id="82651-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="82651-183">toowork 的在本機上，選取**下載**。</span><span class="sxs-lookup"><span data-stu-id="82651-183">toowork locally, select **Download**.</span></span>
   
      ![下載範本](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="82651-185">如果您未設定使用 JSON 編輯器，您可能會偏好編輯 hello 透過 hello 入口網站的範本。</span><span class="sxs-lookup"><span data-stu-id="82651-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="82651-186">hello 本主題其餘部分會假設您已儲存 hello 範本庫 tooyour hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="82651-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="82651-187">不過，您可以建立 hello 相同語法變更 toohello 範本是否在本機使用 JSON 編輯器，或透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="82651-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="82651-188">toowork 透過 hello 入口網站中，選取**新增 toolibrary**。</span><span class="sxs-lookup"><span data-stu-id="82651-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![新增 toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="82651-190">加入時範本庫 toohello，讓 hello 範本的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="82651-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="82651-191">然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="82651-191">Then, select **Save**.</span></span>
   
     ![設定範本值](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="82651-193">tooview 範本儲存在您的程式庫中，選取**更多服務**，型別**範本**toofilter 結果中，選取**範本**。</span><span class="sxs-lookup"><span data-stu-id="82651-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![尋找範本](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="82651-195">選取具有您所儲存的 hello 名稱 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-195">Select hello template with hello name you saved.</span></span>
   
      ![選取範本](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="82651-197">自訂 hello 範本</span><span class="sxs-lookup"><span data-stu-id="82651-197">Customize hello template</span></span>
<span data-ttu-id="82651-198">匯出的 hello 範本運作良好，如果您想 toocreate hello 相同 web 應用程式和每個部署的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="82651-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="82651-199">但 Resource Manager 提供了一些選項，以便您可以更有彈性地部署範本。</span><span class="sxs-lookup"><span data-stu-id="82651-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="82651-200">本文章將示範如何 hello tooadd 參數資料庫管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="82651-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="82651-201">您可以使用這個相同的方法 tooadd 更大的彈性，其他 hello 範本中的值。</span><span class="sxs-lookup"><span data-stu-id="82651-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="82651-202">toocustomize hello 範本中，選取**編輯**。</span><span class="sxs-lookup"><span data-stu-id="82651-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![顯示範本](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="82651-204">選取 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-204">Select hello template.</span></span>
   
     ![編輯範本](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="82651-206">toobe 無法 toopass hello 值，您可能會想 toospecify 在部署期間，加入下列兩個參數 toohello hello**參數**hello 範本中的區段：</span><span class="sxs-lookup"><span data-stu-id="82651-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="82651-207">toouse hello 新參數取代 hello 中的 hello SQL 伺服器定義**資源**> 一節。</span><span class="sxs-lookup"><span data-stu-id="82651-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="82651-208">請注意，**administratorLogin** 和 **administratorLoginPassword** 現在使用參數值。</span><span class="sxs-lookup"><span data-stu-id="82651-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="82651-209">選取**確定**當您完成編輯 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="82651-210">選取**儲存**toosave hello 變更 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="82651-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![儲存範本](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="82651-212">tooredeploy hello 更新範本中，選取**部署**。</span><span class="sxs-lookup"><span data-stu-id="82651-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![部署範本](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="82651-214">提供參數值，並選取資源群組 toodeploy hello 資源。</span><span class="sxs-lookup"><span data-stu-id="82651-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="82651-215">修正匯出問題</span><span class="sxs-lookup"><span data-stu-id="82651-215">Fix export issues</span></span>
<span data-ttu-id="82651-216">並非所有的資源類型都支援 hello 匯出樣板函式。</span><span class="sxs-lookup"><span data-stu-id="82651-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="82651-217">這個問題，請以手動方式 tooresolve hello 遺失資源，將重新加入至您的範本。</span><span class="sxs-lookup"><span data-stu-id="82651-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="82651-218">hello 錯誤訊息包含無法匯出的 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="82651-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="82651-219">在[範本參考](/azure/templates/)中尋找該資源類型。</span><span class="sxs-lookup"><span data-stu-id="82651-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="82651-220">例如，toomanually 加入虛擬網路閘道，請參閱[Microsoft.Network/virtualNetworkGateways 範本參考](/azure/templates/microsoft.network/virtualnetworkgateways)。</span><span class="sxs-lookup"><span data-stu-id="82651-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="82651-221">從資源群組 (而非部署歷程記錄) 匯出時，您只會遇到匯出問題。</span><span class="sxs-lookup"><span data-stu-id="82651-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="82651-222">如果您的最後一個部署準確地呈現 hello hello 資源群組的目前狀態，您應該將 hello 範本匯出從 hello 部署歷程記錄，而不是從 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="82651-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="82651-223">您所做的變更 toohello 資源群組的單一範本中未定義時，只能匯出從資源群組。</span><span class="sxs-lookup"><span data-stu-id="82651-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="82651-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82651-224">Next steps</span></span>
<span data-ttu-id="82651-225">您已經學會如何 tooexport 範本，以從您在 hello 入口網站中建立的資源。</span><span class="sxs-lookup"><span data-stu-id="82651-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="82651-226">您可以透過 [PowerShell](resource-group-template-deploy.md)、[Azure CLI](resource-group-template-deploy-cli.md) 或 [REST API](resource-group-template-deploy-rest.md) 部署範本。</span><span class="sxs-lookup"><span data-stu-id="82651-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="82651-227">如何 tooexport 範本，以透過 PowerShell，請參閱的 toosee[使用 Azure PowerShell 的 Azure Resource Manager](powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="82651-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="82651-228">如何 tooexport 範本，以透過 Azure CLI，請參閱的 toosee[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="82651-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

