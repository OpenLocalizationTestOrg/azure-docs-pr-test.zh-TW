---
title: "匯出 Azure Resource Manager 範本 | Microsoft Docs"
description: "使用 Azure Resource Manager 從現有資源群組匯出範本。"
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
ms.openlocfilehash: 1801ef47e5b182e0bcd5b23970a2999633b4a852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="0c14a-103">從現有資源匯出 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="0c14a-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="0c14a-104">在本文中，您將了解如何從您訂用帳戶中的現有資源匯出 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-104">In this article, you learn how to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="0c14a-105">您可以使用這個產生的範本，來深入了解範本語法。</span><span class="sxs-lookup"><span data-stu-id="0c14a-105">You can use that generated template to gain a better understanding of template syntax.</span></span>

<span data-ttu-id="0c14a-106">有兩種方式可以匯出範本：</span><span class="sxs-lookup"><span data-stu-id="0c14a-106">There are two ways to export a template:</span></span>

* <span data-ttu-id="0c14a-107">您可以匯出**用於部署的實際範本**。</span><span class="sxs-lookup"><span data-stu-id="0c14a-107">You can export the **actual template used for deployment**.</span></span> <span data-ttu-id="0c14a-108">匯出的範本包含與原始範本完全相同的所有參數和變數。</span><span class="sxs-lookup"><span data-stu-id="0c14a-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="0c14a-109">如果您透過入口網站部署資源，而且想要知道範本如何建立這些資源，則這種方法十分有用。</span><span class="sxs-lookup"><span data-stu-id="0c14a-109">This approach is helpful when you deployed resources through the portal, and want to see the template to create those resources.</span></span> <span data-ttu-id="0c14a-110">此範本立即可用。</span><span class="sxs-lookup"><span data-stu-id="0c14a-110">This template is readily usable.</span></span> 
* <span data-ttu-id="0c14a-111">您可以匯出**代表資源群組目前狀態的已產生範本**。</span><span class="sxs-lookup"><span data-stu-id="0c14a-111">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="0c14a-112">匯出的範本不是以任何用於部署的範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="0c14a-112">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="0c14a-113">反而，它所建立的範本是資源群組的快照。</span><span class="sxs-lookup"><span data-stu-id="0c14a-113">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="0c14a-114">匯出的範本會有許多硬式編碼值，但數量可能不如您通常會定義的參數數量。</span><span class="sxs-lookup"><span data-stu-id="0c14a-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="0c14a-115">當您在部署之後修改資源群組時，這種方法十分有用。</span><span class="sxs-lookup"><span data-stu-id="0c14a-115">This approach is useful when you have modified the resource group after deployment.</span></span> <span data-ttu-id="0c14a-116">此範本通常需要修改才能使用。</span><span class="sxs-lookup"><span data-stu-id="0c14a-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="0c14a-117">本主題說明透過入口網站的兩種方法。</span><span class="sxs-lookup"><span data-stu-id="0c14a-117">This topic shows both approaches through the portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="0c14a-118">部署資源</span><span class="sxs-lookup"><span data-stu-id="0c14a-118">Deploy resources</span></span>
<span data-ttu-id="0c14a-119">請開始將可用於匯出為範本的資源部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="0c14a-119">Let's start by deploying resources to Azure that you can use for exporting as a template.</span></span> <span data-ttu-id="0c14a-120">如果您的訂用帳戶中已有想要匯出至範本的資源群組，就可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="0c14a-120">If you already have a resource group in your subscription that you want to export to a template, you can skip this section.</span></span> <span data-ttu-id="0c14a-121">本文的其餘部分假設您已部署本節中所顯示的 Web 應用程式和 SQL 資料庫解決方案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-121">The remainder of this article assumes you have deployed the web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="0c14a-122">如果您使用不同的解決方案，則體驗可能會稍有不同，但匯出範本的步驟相同。</span><span class="sxs-lookup"><span data-stu-id="0c14a-122">If you use a different solution, your experience might be a little different, but the steps to export a template are the same.</span></span> 

1. <span data-ttu-id="0c14a-123">在 [Azure 入口網站](https://portal.azure.com)中，選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-123">In the [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![選取 [新增]](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="0c14a-125">搜尋 **Web 應用程式 + SQL**，並從可用的選項加以選取。</span><span class="sxs-lookup"><span data-stu-id="0c14a-125">Search for **web app + SQL** and select it from the available options.</span></span>
   
      ![搜尋 Web 應用程式和 SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="0c14a-127">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-127">Select **Create**.</span></span>

      ![選取 [建立]](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="0c14a-129">提供 Web 應用程式和 SQL 資料庫的必要值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-129">Provide the required values for the web app and SQL database.</span></span> <span data-ttu-id="0c14a-130">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-130">Select **Create**.</span></span>

      ![提供 Web 和 SQL 值](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="0c14a-132">部署可能需要一會兒的時間。</span><span class="sxs-lookup"><span data-stu-id="0c14a-132">The deployment may take a minute.</span></span> <span data-ttu-id="0c14a-133">部署完成後，您的訂用帳戶就會包含解決方案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-133">After the deployment finishes, your subscription contains the solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="0c14a-134">從部署記錄中檢視範本</span><span class="sxs-lookup"><span data-stu-id="0c14a-134">View template from deployment history</span></span>
1. <span data-ttu-id="0c14a-135">移至您的新資源群組的 [資源群組] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0c14a-135">Go to the resource group blade for your new resource group.</span></span> <span data-ttu-id="0c14a-136">請注意，刀鋒視窗會顯示最後部署的結果。</span><span class="sxs-lookup"><span data-stu-id="0c14a-136">Notice that the blade shows the result of the last deployment.</span></span> <span data-ttu-id="0c14a-137">選取此連結。</span><span class="sxs-lookup"><span data-stu-id="0c14a-137">Select this link.</span></span>
   
      ![資源群組刀鋒視窗](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="0c14a-139">您會看到群組的部署歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0c14a-139">You see a history of deployments for the group.</span></span> <span data-ttu-id="0c14a-140">在您的案例中，刀鋒視窗可能只列出一個部署。</span><span class="sxs-lookup"><span data-stu-id="0c14a-140">In your case, the blade probably lists only one deployment.</span></span> <span data-ttu-id="0c14a-141">選取此部署。</span><span class="sxs-lookup"><span data-stu-id="0c14a-141">Select this deployment.</span></span>
   
     ![上次部署](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="0c14a-143">刀鋒視窗會顯示部署的摘要。</span><span class="sxs-lookup"><span data-stu-id="0c14a-143">The blade displays a summary of the deployment.</span></span> <span data-ttu-id="0c14a-144">摘要包含部署和其作業的狀態，與您為參數所提供的值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-144">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span></span> <span data-ttu-id="0c14a-145">若要查看用於部署的範本，請選取 [檢視範本] 。</span><span class="sxs-lookup"><span data-stu-id="0c14a-145">To see the template that you used for the deployment, select **View template**.</span></span>
   
     ![檢視部署摘要](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="0c14a-147">Resource Manager 會為您擷取下列七個檔案：</span><span class="sxs-lookup"><span data-stu-id="0c14a-147">Resource Manager retrieves the following seven files for you:</span></span>
   
   1. <span data-ttu-id="0c14a-148">**範本** - 用於定義解決方案之基礎結構的範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-148">**Template** - The template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="0c14a-149">當您透過入口網站建立儲存體帳戶時，Resource Manager 會使用範本來部署它，並且儲存該範本供日後參考。</span><span class="sxs-lookup"><span data-stu-id="0c14a-149">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="0c14a-150">**參數** - 您可以在部署期間用來傳入值的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-150">**Parameters** - A parameter file that you can use to pass in values during deployment.</span></span> <span data-ttu-id="0c14a-151">它會包含您在第一次部署期間所提供的值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-151">It contains the values that you provided during the first deployment.</span></span> <span data-ttu-id="0c14a-152">當您重新部署範本時，即可變更所有這些值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-152">You can change any of these values when you redeploy the template.</span></span>
   3. <span data-ttu-id="0c14a-153">**CLI** - 您可以為了部署範本而使用的 Azure 令列介面 (CLI) 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   3. <span data-ttu-id="0c14a-154">**CLI 2.0** - 您可以為了部署範本而使用的 Azure 令列介面 (CLI) 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   4. <span data-ttu-id="0c14a-155">**PowerShell** - 您可以為了部署範本而使用的 Azure PowerShell 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-155">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span></span>
   5. <span data-ttu-id="0c14a-156">**.NET** - 您可以為了部署範本而使用的 .NET 類別。</span><span class="sxs-lookup"><span data-stu-id="0c14a-156">**.NET** - A .NET class that you can use to deploy the template.</span></span>
   6. <span data-ttu-id="0c14a-157">**Ruby** - 您可以為了部署範本而使用的 Ruby 類別。</span><span class="sxs-lookup"><span data-stu-id="0c14a-157">**Ruby** - A Ruby class that you can use to deploy the template.</span></span>
      
      <span data-ttu-id="0c14a-158">這些檔案可以透過刀鋒視窗的連結取得。</span><span class="sxs-lookup"><span data-stu-id="0c14a-158">The files are available through links across the blade.</span></span> <span data-ttu-id="0c14a-159">根據預設，刀鋒視窗會顯示範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-159">By default, the blade displays the template.</span></span>
      
       ![檢視範本](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="0c14a-161">此範本是用來建立 Web 應用程式和 SQL 資料庫的實際範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-161">This template is the actual template used to create your web app and SQL database.</span></span> <span data-ttu-id="0c14a-162">請注意，其中包含的參數可讓您在部署期間提供不同的值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-162">Notice it contains parameters that enable you to provide different values during deployment.</span></span> <span data-ttu-id="0c14a-163">若要深入了解範本的結構，請參閱 [編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="0c14a-163">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-the-template-from-resource-group"></a><span data-ttu-id="0c14a-164">從資源群組匯出範本</span><span class="sxs-lookup"><span data-stu-id="0c14a-164">Export the template from resource group</span></span>
<span data-ttu-id="0c14a-165">如果您已手動變更資源或在多個部署中新增資源，則從部署記錄中擷取範本並不會反映資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="0c14a-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from the deployment history does not reflect the current state of the resource group.</span></span> <span data-ttu-id="0c14a-166">本節說明您如何匯出反映資源群組目前狀態的範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-166">This section shows you how to export a template that reflects the current state of the resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="0c14a-167">您無法針對具有超過 200 個資源的資源群組匯出範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="0c14a-168">若要檢視資源群組的範本，請選取 [自動化指令碼] 。</span><span class="sxs-lookup"><span data-stu-id="0c14a-168">To view the template for a resource group, select **Automation script**.</span></span>
   
      ![匯出資源群組](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="0c14a-170">Resource Manager 會評估資源群組中的資源，並產生這些資源的範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-170">Resource Manager evaluates the resources in the resource group, and generates a template for those resources.</span></span> <span data-ttu-id="0c14a-171">並非所有的資源類型都支援匯出範本功能。</span><span class="sxs-lookup"><span data-stu-id="0c14a-171">Not all resource types support the export template function.</span></span> <span data-ttu-id="0c14a-172">您可能會看到一則錯誤，指出匯出發生問題。</span><span class="sxs-lookup"><span data-stu-id="0c14a-172">You may see an error stating that there is a problem with the export.</span></span> <span data-ttu-id="0c14a-173">您會在 [修正匯出問題](#fix-export-issues) 一節中了解如何處理這些問題。</span><span class="sxs-lookup"><span data-stu-id="0c14a-173">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="0c14a-174">同樣地，您會看到可用來重新部署解決方案的六個檔案。</span><span class="sxs-lookup"><span data-stu-id="0c14a-174">You again see the six files that you can use to redeploy the solution.</span></span> <span data-ttu-id="0c14a-175">不過，此範本目前會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="0c14a-175">However, this time the template is a little different.</span></span> <span data-ttu-id="0c14a-176">請注意，已產生的範本所包含的參數，會比上一節中範本所包含的參數更少。</span><span class="sxs-lookup"><span data-stu-id="0c14a-176">Notice that the generated template contains fewer parameters than the template in previous section.</span></span> <span data-ttu-id="0c14a-177">此外，許多值 (如位置和 SKU 值) 都是硬式編碼在這個範本中，而不接受參數值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-177">Also, many of the values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="0c14a-178">重複使用此範本之前，您可能會想要編輯範本，以善用參數。</span><span class="sxs-lookup"><span data-stu-id="0c14a-178">Before reusing this template, you might want to edit the template to make better use of parameters.</span></span> 
   
3. <span data-ttu-id="0c14a-179">有幾個選項可供您繼續使用此範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-179">You have a couple of options for continuing to work with this template.</span></span> <span data-ttu-id="0c14a-180">您可以下載範本，並在本機使用 JSON 編輯器來處理範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-180">You can either download the template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="0c14a-181">或者，您可以將範本儲存至程式庫，並透過入口網站處理範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-181">Or, you can save the template to your library and work on it through the portal.</span></span>
   
     <span data-ttu-id="0c14a-182">如果您熟悉如何使用 JSON 編輯器，例如 [VS Code](https://code.visualstudio.com/) 或 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)，您可能會偏好將範本下載到本機並使用該編輯器。</span><span class="sxs-lookup"><span data-stu-id="0c14a-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span></span> <span data-ttu-id="0c14a-183">若要在本機上工作，請選取 [下載]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-183">To work locally, select **Download**.</span></span>
   
      ![下載範本](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="0c14a-185">如果您未設定 JSON 編輯器，則可能會偏好透過入口網站來編輯範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-185">If you are not set up with a JSON editor, you might prefer editing the template through the portal.</span></span> <span data-ttu-id="0c14a-186">本主題的其餘部分假設您已將範本儲存至入口網站中的程式庫。</span><span class="sxs-lookup"><span data-stu-id="0c14a-186">The remainder of this topic assumes you have saved the template to your library in the portal.</span></span> <span data-ttu-id="0c14a-187">不過，不論是在本機使用 JSON 編輯器進行工作或透過入口網站來進行，您都要對範本進行相同的語法變更。</span><span class="sxs-lookup"><span data-stu-id="0c14a-187">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span></span> <span data-ttu-id="0c14a-188">若要透過入口網站工作，請選取 [新增至程式庫]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-188">To work through the portal, select **Add to library**.</span></span>
   
      ![新增至程式庫](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="0c14a-190">在程式庫中新增範本時，請為範本提供名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="0c14a-190">When adding a template to the library, give the template a name and description.</span></span> <span data-ttu-id="0c14a-191">然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-191">Then, select **Save**.</span></span>
   
     ![設定範本值](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="0c14a-193">若要檢視程式庫中儲存的範本，請選取 [更多服務]，輸入**範本**來篩選結果，然後選取 [範本]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-193">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span></span>
   
      ![尋找範本](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="0c14a-195">選取具有您所儲存之名稱的範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-195">Select the template with the name you saved.</span></span>
   
      ![選取範本](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-the-template"></a><span data-ttu-id="0c14a-197">自訂範本</span><span class="sxs-lookup"><span data-stu-id="0c14a-197">Customize the template</span></span>
<span data-ttu-id="0c14a-198">如果您想要為每個部署建立相同的 Web 應用程式和 SQL 資料庫，匯出的範本就夠用。</span><span class="sxs-lookup"><span data-stu-id="0c14a-198">The exported template works fine if you want to create the same web app and SQL database for every deployment.</span></span> <span data-ttu-id="0c14a-199">但 Resource Manager 提供了一些選項，以便您可以更有彈性地部署範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="0c14a-200">本文說明如何新增資料庫管理員名稱和密碼的參數。</span><span class="sxs-lookup"><span data-stu-id="0c14a-200">This article shows you how to add parameters for the database administrator name and password.</span></span> <span data-ttu-id="0c14a-201">您可以使用這種相同的方法，為範本中的其他值新增更多彈性。</span><span class="sxs-lookup"><span data-stu-id="0c14a-201">You can use this same approach to add more flexibility for other values in the template.</span></span>

1. <span data-ttu-id="0c14a-202">若要自訂範本，請選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-202">To customize the template, select **Edit**.</span></span>
   
     ![顯示範本](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="0c14a-204">選取範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-204">Select the template.</span></span>
   
     ![編輯範本](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="0c14a-206">為了能夠傳遞您可能想要在部署期間指定的值，請將下列兩個參數新增至範本中的 **parameters** 區段：</span><span class="sxs-lookup"><span data-stu-id="0c14a-206">To be able to pass the values that you might want to specify during deployment, add the following two parameters to the **parameters** section in the template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="0c14a-207">若要使用新的參數，請取代 **resources** 區段中的 SQL Server 定義。</span><span class="sxs-lookup"><span data-stu-id="0c14a-207">To use the new parameters, replace the SQL server definition in the **resources** section.</span></span> <span data-ttu-id="0c14a-208">請注意，**administratorLogin** 和 **administratorLoginPassword** 現在使用參數值。</span><span class="sxs-lookup"><span data-stu-id="0c14a-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

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

6. <span data-ttu-id="0c14a-209">當您編輯好範本時，選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-209">Select **OK** when you are done editing the template.</span></span>
7. <span data-ttu-id="0c14a-210">選取 [儲存] 以儲存對範本所做的變更。</span><span class="sxs-lookup"><span data-stu-id="0c14a-210">Select **Save** to save the changes to the template.</span></span>
   
     ![儲存範本](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="0c14a-212">若要重新部署更新過的範本，請選取 [部署]。</span><span class="sxs-lookup"><span data-stu-id="0c14a-212">To redeploy the updated template, select **Deploy**.</span></span>
   
     ![部署範本](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="0c14a-214">提供參數值，並選取要在其中部署資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0c14a-214">Provide parameter values, and select a resource group to deploy the resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="0c14a-215">修正匯出問題</span><span class="sxs-lookup"><span data-stu-id="0c14a-215">Fix export issues</span></span>
<span data-ttu-id="0c14a-216">並非所有的資源類型都支援匯出範本功能。</span><span class="sxs-lookup"><span data-stu-id="0c14a-216">Not all resource types support the export template function.</span></span> <span data-ttu-id="0c14a-217">若要解決此問題，請手動將遺漏的資源新增回您的範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-217">To resolve this issue, manually add the missing resources back into your template.</span></span> <span data-ttu-id="0c14a-218">此錯誤訊息包含無法匯出的資源類型。</span><span class="sxs-lookup"><span data-stu-id="0c14a-218">The error message includes the resource types that cannot be exported.</span></span> <span data-ttu-id="0c14a-219">在[範本參考](/azure/templates/)中尋找該資源類型。</span><span class="sxs-lookup"><span data-stu-id="0c14a-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="0c14a-220">例如，若要手動新增虛擬網路閘道，請參閱 [Microsoft.Network/virtualNetworkGateways 範本參考](/azure/templates/microsoft.network/virtualnetworkgateways)。</span><span class="sxs-lookup"><span data-stu-id="0c14a-220">For example, to manually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="0c14a-221">從資源群組 (而非部署歷程記錄) 匯出時，您只會遇到匯出問題。</span><span class="sxs-lookup"><span data-stu-id="0c14a-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="0c14a-222">如果上一次部署精確地表示資源群組的目前狀態，您應該從部署歷程記錄 (而非資源群組) 匯出範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-222">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span></span> <span data-ttu-id="0c14a-223">只有在變更未定義於單一範本中的資源群組時，才能從資源群組匯出。</span><span class="sxs-lookup"><span data-stu-id="0c14a-223">Only export from a resource group when you have made changes to the resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0c14a-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c14a-224">Next steps</span></span>
<span data-ttu-id="0c14a-225">您已經了解如何從您在入口網站中建立的資源匯出範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-225">You have learned how to export a template from resources that you created in the portal.</span></span>

* <span data-ttu-id="0c14a-226">您可以透過 [PowerShell](resource-group-template-deploy.md)、[Azure CLI](resource-group-template-deploy-cli.md) 或 [REST API](resource-group-template-deploy-rest.md) 部署範本。</span><span class="sxs-lookup"><span data-stu-id="0c14a-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="0c14a-227">若要查看如何透過 PowerShell 匯出範本，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0c14a-227">To see how to export a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="0c14a-228">若要查看如何透過 Azure CLI 匯出範本，請參閱 [搭配使用 Mac、Linux 和 Windows 適用的 Azure CLI 與 Azure Resource Manager](xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0c14a-228">To see how to export a template through Azure CLI, see [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

