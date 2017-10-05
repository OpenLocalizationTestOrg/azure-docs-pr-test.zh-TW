---
title: "使用 Azure 資源群組專案在 Visual Studio Team Services中進行連續整合 | Microsoft Docs"
description: "使用 Azure 資源群組部署專案在 Visual Studio Team Services 中進行連續整合"
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: e7d98ca3fa281a136595c37ed9b7e71de0cf7bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a><span data-ttu-id="cc4f2-103">使用 Azure 資源群組部署專案在 Visual Studio Team Services 中進行連續整合</span><span class="sxs-lookup"><span data-stu-id="cc4f2-103">Continuous integration in Visual Studio Team Services using Azure Resource Group deployment projects</span></span>
<span data-ttu-id="cc4f2-104">若要部署 Azure 範本，您需要執行各種階段的工作：組建、測試、複製到 Azure (也稱為「暫存」) 及部署範本。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-104">To deploy an Azure template, you perform tasks in various stages: Build, Test, Copy to Azure (also called "Staging"), and Deploy Template.</span></span> <span data-ttu-id="cc4f2-105">有兩種不同的方式可將範本部署至 Visual Studio Team Services (VS Team Services)。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-105">There are two different ways to deploy templates to Visual Studio Team Services (VS Team Services).</span></span> <span data-ttu-id="cc4f2-106">兩種方法所產生的結果都相同，因此請選擇最符合您工作流程的方法。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-106">Both methods provide the same results, so choose the one that best fits your workflow.</span></span>

1. <span data-ttu-id="cc4f2-107">在執行 PowerShell 指令碼的組建定義 (包含在 Azure 資源群組部署專案，Deploy-AzureResourceGroup.ps1) 中新增一個步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-107">Add a single step to your build definition that runs the PowerShell script that’s included in the Azure Resource Group deployment project (Deploy-AzureResourceGroup.ps1).</span></span> <span data-ttu-id="cc4f2-108">指令碼會複製構件，接著部署範本。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-108">The script copies artifacts and then deploys the template.</span></span>
2. <span data-ttu-id="cc4f2-109">新增多個 VS Team Services 建置步驟，每個都執行一個階段工作。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-109">Add multiple VS Team Services build steps, each one performing a stage task.</span></span>

<span data-ttu-id="cc4f2-110">本文將示範兩個選項。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-110">This article demonstrates both options.</span></span> <span data-ttu-id="cc4f2-111">第一個選項的優點是能夠使用開發人員在 Visual Studio 中所使用的相同指令碼，並在整個生命週期中提供一致性。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-111">The first option has the advantage of using the same script used by developers in Visual Studio and providing consistency throughout the lifecycle.</span></span> <span data-ttu-id="cc4f2-112">第二個選項可提供內建指令碼的方便替代選項。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-112">The second option offers a convenient alternative to the built-in script.</span></span> <span data-ttu-id="cc4f2-113">這兩個程序假設您已經在 VS Team Services 中簽入 Visual Studio 部署專案。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-113">Both procedures assume you already have a Visual Studio deployment project checked into VS Team Services.</span></span>

## <a name="copy-artifacts-to-azure"></a><span data-ttu-id="cc4f2-114">將構件複製到 Azure</span><span class="sxs-lookup"><span data-stu-id="cc4f2-114">Copy artifacts to Azure</span></span>
<span data-ttu-id="cc4f2-115">無論何種情況，如果您有範本部署所需的任何構件，則必須提供存取權給 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-115">Regardless of the scenario, if you have any artifacts that are needed for template deployment, you must give Azure Resource Manager access to them.</span></span> <span data-ttu-id="cc4f2-116">這些構件包括下列檔案：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-116">These artifacts can include files such as:</span></span>

* <span data-ttu-id="cc4f2-117">巢狀範本</span><span class="sxs-lookup"><span data-stu-id="cc4f2-117">Nested templates</span></span>
* <span data-ttu-id="cc4f2-118">組態指令碼及 DSC 指令碼</span><span class="sxs-lookup"><span data-stu-id="cc4f2-118">Configuration scripts and DSC scripts</span></span>
* <span data-ttu-id="cc4f2-119">應用程式二進位檔</span><span class="sxs-lookup"><span data-stu-id="cc4f2-119">Application binaries</span></span>

### <a name="nested-templates-and-configuration-scripts"></a><span data-ttu-id="cc4f2-120">巢狀範本和組態指令碼</span><span class="sxs-lookup"><span data-stu-id="cc4f2-120">Nested Templates and Configuration Scripts</span></span>
<span data-ttu-id="cc4f2-121">當您使用 Visual Studio (或以 Visual Studio 程式碼片段建置的) 提供的範本時，PowerShell 指令碼不但會暫存構件，也會參數化資源 URI 以進行不同的部署。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-121">When you use the templates provided by Visual Studio (or built with Visual Studio snippets), the PowerShell script not only stages the artifacts, it also parameterizes the URI for the resources for different deployments.</span></span> <span data-ttu-id="cc4f2-122">接著，指令碼會將構件複製到 Azure 中的安全容器，並為該容器建立 SaS 權杖，再將該資訊傳遞至範本部署。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-122">The script then copies the artifacts to a secure container in Azure, creates a SaS token for that container, and then passes that information on to the template deployment.</span></span> <span data-ttu-id="cc4f2-123">請參閱 [建立範本部署](https://msdn.microsoft.com/library/azure/dn790564.aspx) 以深入了解巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-123">See [Create a template deployment](https://msdn.microsoft.com/library/azure/dn790564.aspx) to learn more about nested templates.</span></span>  <span data-ttu-id="cc4f2-124">在 VS Team Services 中使用工作時，您必須針對範本部署選取適當的工作，且如果必要，必須從預備步驟將參數值傳遞至範本部署。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-124">When using tasks in VS Team Services, you must select the appropriate tasks for your template deployment and if necessary, pass parameter values from the staging step to the template deployment.</span></span>

## <a name="set-up-continuous-deployment-in-vs-team-services"></a><span data-ttu-id="cc4f2-125">在 VS Team Services 中設定連續部署</span><span class="sxs-lookup"><span data-stu-id="cc4f2-125">Set up continuous deployment in VS Team Services</span></span>
<span data-ttu-id="cc4f2-126">要在 VS Team Services 中呼叫 PowerShell 指令碼，請更新您的組建定義。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-126">To call the PowerShell script in VS Team Services, you need to update your build definition.</span></span> <span data-ttu-id="cc4f2-127">簡單來說，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-127">In brief, the steps are:</span></span> 

1. <span data-ttu-id="cc4f2-128">編輯組建定義。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-128">Edit the build definition.</span></span>
2. <span data-ttu-id="cc4f2-129">在 VS Team Services 中設定 Azure 授權。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-129">Set up Azure authorization in VS Team Services.</span></span>
3. <span data-ttu-id="cc4f2-130">新增參考 Azure 資源群組部署專案中 PowerShell 指令碼的 Azure PowerShell 組建步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-130">Add an Azure PowerShell build step that references the PowerShell script in the Azure Resource Group deployment project.</span></span>
4. <span data-ttu-id="cc4f2-131">設定 *-ArtifactsStagingDirectory* 參數值，以與 VS Team Services 中建置的專案搭配使用。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-131">Set the value of the *-ArtifactsStagingDirectory* parameter to work with a project built in VS Team Services.</span></span>

### <a name="detailed-walkthrough-for-option-1"></a><span data-ttu-id="cc4f2-132">選項 1 的詳細逐步解說</span><span class="sxs-lookup"><span data-stu-id="cc4f2-132">Detailed walkthrough for Option 1</span></span>
<span data-ttu-id="cc4f2-133">下列程序會使用單一工作在您的專案中執行 PowerShell 指令碼，逐步引導您進行在 VS Team Services 中設定持續部署所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-133">The following procedures walk you through the steps necessary to configure continuous deployment in VS Team Services using a single task that runs the PowerShell script in your project.</span></span> 

1. <span data-ttu-id="cc4f2-134">編輯您的 VS Team Services 組建定義並新增 Azure PowerShell 建置步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-134">Edit your VS Team Services build definition and add an Azure PowerShell build step.</span></span> <span data-ttu-id="cc4f2-135">在 [組建定義] 類別下選擇組建定義，再選擇 [編輯] 連結。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-135">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span></span>
   
   ![編輯組建定義][0]
2. <span data-ttu-id="cc4f2-137">在組建定義中新增 [Azure PowerShell] 組建步驟，再選擇 [新增組建步驟...]</span><span class="sxs-lookup"><span data-stu-id="cc4f2-137">Add a new **Azure PowerShell** build step to the build definition and then choose the **Add build step…**</span></span> <span data-ttu-id="cc4f2-138">按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-138">button.</span></span>
   
   ![新增組建步驟][1]
3. <span data-ttu-id="cc4f2-140">選擇 [部署工作] 類別，選取 [Azure PowerShell] 工作，再選擇其 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-140">Choose the **Deploy task** category, select the **Azure PowerShell** task, and then choose its **Add** button.</span></span>
   
   ![新增工作][2]
4. <span data-ttu-id="cc4f2-142">選擇 [Azure PowerShell]  組建步驟，再填上其值。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-142">Choose the **Azure PowerShell** build step and then fill in its values.</span></span>
   
   1. <span data-ttu-id="cc4f2-143">如果您已將 Azure 服務端點新增至 VS Team Services，請在 [Azure 訂用帳戶] 下拉式清單方塊中選擇訂用帳戶，並跳至下一節。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-143">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop-down list box and then skip to the next section.</span></span> 
      
      <span data-ttu-id="cc4f2-144">如果您的 VS Team Services 中沒有 Azure 服務端點，請新增一個。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-144">If you don’t have an Azure service endpoint in VS Team Services, you need to add one.</span></span> <span data-ttu-id="cc4f2-145">此訂用帳戶會帶您完成此程序。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-145">This subsection takes you through the process.</span></span> <span data-ttu-id="cc4f2-146">如果您的 Azure 帳戶使用 Microsoft 帳戶 (例如 Hotmail)，您必須進行下列步驟以取得服務主體驗證。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-146">If your Azure account uses a Microsoft account (such as Hotmail), you must take the following steps to get a Service Principal authentication.</span></span>
   2. <span data-ttu-id="cc4f2-147">選擇 [Azure 訂用帳戶] 下拉式清單方塊旁的 [管理] 連結。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-147">Choose the **Manage** link next to the **Azure Subscription** drop-down list box.</span></span>
      
      ![管理 Azure 訂用帳戶][3]
   3. <span data-ttu-id="cc4f2-149">在 [新服務端點] 下拉式清單方塊中選擇 [Azure]。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-149">Choose **Azure** in the **New Service Endpoint** drop-down list box.</span></span>
      
      ![新增服務端點][4]
   4. <span data-ttu-id="cc4f2-151">在 [新增 Azure 訂用帳戶] 對話方塊中，選取 [服務主體] 選項。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-151">In the **Add Azure Subscription** dialog box, select the **Service Principal** option.</span></span>
      
      ![服務主體選項][5]
   5. <span data-ttu-id="cc4f2-153">在 [新增 Azure 訂用帳戶]  對話方塊中新增 Azure 訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-153">Add your Azure subscription information to the **Add Azure Subscription** dialog box.</span></span> <span data-ttu-id="cc4f2-154">您必須先提供下列項目：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-154">You need to provide the following items:</span></span>
      
      * <span data-ttu-id="cc4f2-155">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="cc4f2-155">Subscription Id</span></span>
      * <span data-ttu-id="cc4f2-156">訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="cc4f2-156">Subscription Name</span></span>
      * <span data-ttu-id="cc4f2-157">服務主體識別碼</span><span class="sxs-lookup"><span data-stu-id="cc4f2-157">Service Principal Id</span></span>
      * <span data-ttu-id="cc4f2-158">服務主體金鑰</span><span class="sxs-lookup"><span data-stu-id="cc4f2-158">Service Principal Key</span></span>
      * <span data-ttu-id="cc4f2-159">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="cc4f2-159">Tenant Id</span></span>
   6. <span data-ttu-id="cc4f2-160">在 [訂用帳戶]  名稱方塊中新增您選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-160">Add a name of your choice to the **Subscription** name box.</span></span> <span data-ttu-id="cc4f2-161">此值稍後會出現在 VS Team Services 的 [Azure 訂用帳戶] 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-161">This value appears later in the **Azure Subscription** drop-down list in VS Team Services.</span></span> 
   7. <span data-ttu-id="cc4f2-162">如果您不知道 Azure 訂用帳戶識別碼，可以使用以下其中一個命令擷取。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-162">If you don’t know your Azure subscription ID, you can use one of the following commands to retrieve it.</span></span>
      
      <span data-ttu-id="cc4f2-163">對於 Azure PowerShell 指令碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-163">For PowerShell scripts, use:</span></span>
      
      `Get-AzureRmSubscription`
      
      <span data-ttu-id="cc4f2-164">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-164">For Azure CLI, use:</span></span>
      
      `azure account show`
   8. <span data-ttu-id="cc4f2-165">若要取得服務主體識別碼、服務主體金鑰及租用戶識別碼，請依照[使用入口網站建立 Active Directory 應用程式和服務主體](resource-group-create-service-principal-portal.md)或[以 Azure 資源管理員驗證服務主體](resource-group-authenticate-service-principal.md)中的程序。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-165">To get a Service Principal ID, Service Principal Key, and Tenant ID, follow the procedure in [Create Active Directory application and service principal using portal](resource-group-create-service-principal-portal.md) or [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal.md).</span></span>
   9. <span data-ttu-id="cc4f2-166">將服務主體識別碼、服務主體金鑰，以及租用戶識別碼值新增至 [新增 Azure 訂用帳戶] 對話方塊，然後選擇 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-166">Add the Service Principal ID, Service Principal Key, and Tenant ID values to the **Add Azure Subscription** dialog box and then choose the **OK** button.</span></span>
      
      <span data-ttu-id="cc4f2-167">現在，您擁有可執行 Azure PowerShell 指令碼的有效服務主體。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-167">You now have a valid Service Principal to use to run the Azure PowerShell script.</span></span>
5. <span data-ttu-id="cc4f2-168">編輯組建定義並選擇 **Azure PowerShell** 建置步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-168">Edit the build definition and choose the **Azure PowerShell** build step.</span></span> <span data-ttu-id="cc4f2-169">在 [Azure 訂用帳戶] 下拉式清單方塊中選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-169">Select the subscription in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="cc4f2-170">(如果訂用帳戶未出現，請選擇 [管理] 連結旁的 [重新整理]按鈕。)</span><span class="sxs-lookup"><span data-stu-id="cc4f2-170">(If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.)</span></span> 
   
   ![安裝並設定 Azure PowerShell 建置工作][8]
6. <span data-ttu-id="cc4f2-172">提供 Deploy-AzureResourceGroup.ps1 PowerShell 指令碼的路徑。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-172">Provide a path to the Deploy-AzureResourceGroup.ps1 PowerShell script.</span></span> <span data-ttu-id="cc4f2-173">若要這樣做，請選擇 [指令碼路徑] 方塊旁的省略符號 (…) 按鈕，瀏覽到您專案的 [指令碼] 資料夾中的 Deploy-AzureResourceGroup.ps1 PowerShell 指令碼，選取並選擇 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-173">To do this, choose the ellipsis (…) button next to the **Script Path** box, navigate to the Deploy-AzureResourceGroup.ps1 PowerShell script in the **Scripts** folder of your project, select it, and then choose the **OK** button.</span></span>    
   
   ![選取要編寫指令碼的路徑][9]
7. <span data-ttu-id="cc4f2-175">選取指令碼之後，將路徑更新到該指令碼，以便從 Build.StagingDirectory 執行 (與 *ArtifactsLocation* 設定的目錄相同)。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-175">After you select the script, update the path to the script so that it’s run from the Build.StagingDirectory (the same directory that *ArtifactsLocation* is set to).</span></span> <span data-ttu-id="cc4f2-176">您可以在指令碼路徑的開頭加入 “$(Build.StagingDirectory)/” 以執行此項作業。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-176">You can do this by adding “$(Build.StagingDirectory)/” to the beginning of the script path.</span></span>
   
    ![選取要編寫指令碼的路徑][10]
8. <span data-ttu-id="cc4f2-178">在 [指令碼引數]  方塊中，輸入下列參數 (請輸入在同一行)。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-178">In the **Script Arguments** box, enter the following parameters (in a single line).</span></span> <span data-ttu-id="cc4f2-179">當您在 Visual Studio 中執行指令碼時，可以在 [輸出]  視窗中看到 VS 如何使用參數。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-179">When you run the script in Visual Studio, you can see how VS uses the parameters in the **Output** window.</span></span> <span data-ttu-id="cc4f2-180">您可以從這裡開始，在建置步驟中設定參數值。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-180">You can use this as a starting point for setting the parameter values in your build step.</span></span>
   
   | <span data-ttu-id="cc4f2-181">參數</span><span class="sxs-lookup"><span data-stu-id="cc4f2-181">Parameter</span></span> | <span data-ttu-id="cc4f2-182">說明</span><span class="sxs-lookup"><span data-stu-id="cc4f2-182">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="cc4f2-183">-ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="cc4f2-183">-ResourceGroupLocation</span></span> |<span data-ttu-id="cc4f2-184">資源群組所在的地理位置，例如 **eastus** 或**美國東部**。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-184">The geo-location value where the resource group is located, such as **eastus** or **'East US'**.</span></span> <span data-ttu-id="cc4f2-185">(如果名稱中有空間，請加入單引號。)如需詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/en-us/regions/)。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-185">(Add single quotes if there's a space in the name.) See [Azure Regions](https://azure.microsoft.com/en-us/regions/) for more information.</span></span> |
   | <span data-ttu-id="cc4f2-186">-ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cc4f2-186">-ResourceGroupName</span></span> |<span data-ttu-id="cc4f2-187">此部署使用的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-187">The name of the resource group used for this deployment.</span></span> |
   | <span data-ttu-id="cc4f2-188">-UploadArtifacts</span><span class="sxs-lookup"><span data-stu-id="cc4f2-188">-UploadArtifacts</span></span> |<span data-ttu-id="cc4f2-189">此參數出現時，可指定需要從本機系統上傳到 Azure 的構件。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-189">This parameter, when present, specifies that artifacts that need to be uploaded to Azure from the local system.</span></span> <span data-ttu-id="cc4f2-190">您只需要在範本部署需要您希望暫存的其他構件時，使用 PowerShell 指令碼設定此轉換 (例如組態指令碼或巢狀範本) 即可。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-190">You only need to set this switch if your template deployment requires extra artifacts that you want to stage using the PowerShell script (such as configuration scripts or nested templates).</span></span> |
   | <span data-ttu-id="cc4f2-191">-StorageAccountName</span><span class="sxs-lookup"><span data-stu-id="cc4f2-191">-StorageAccountName</span></span> |<span data-ttu-id="cc4f2-192">用來暫存此部署之構件的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-192">The name of the storage account used to stage artifacts for this deployment.</span></span> <span data-ttu-id="cc4f2-193">僅在您執行部署的成品時才會使用這個參數。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-193">This parameter is only used if you are staging artifacts for deployment.</span></span> <span data-ttu-id="cc4f2-194">如果提供這個參數，則如果指令碼在先前部署期間尚未建立儲存體帳戶，便會建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-194">If this parameter is supplied, a new storage account is created if the script has not created one during a previous deployment.</span></span> <span data-ttu-id="cc4f2-195">如果指定參數，則儲存體帳戶必須已經存在。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-195">If the parameter is specified, the storage account must already exist.</span></span> |
   | <span data-ttu-id="cc4f2-196">-StorageAccountResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cc4f2-196">-StorageAccountResourceGroupName</span></span> |<span data-ttu-id="cc4f2-197">與儲存體帳戶相關聯的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-197">The name of the resource group associated with the storage account.</span></span> <span data-ttu-id="cc4f2-198">僅在您提供 StorageAccountName 參數的值時，才需要此參數。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-198">This parameter is required only if you provide a value for the StorageAccountName parameter.</span></span> |
   | <span data-ttu-id="cc4f2-199">-TemplateFile</span><span class="sxs-lookup"><span data-stu-id="cc4f2-199">-TemplateFile</span></span> |<span data-ttu-id="cc4f2-200">Azure 資源群組部署專案中的範本檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-200">The path to the template file in the Azure Resource Group deployment project.</span></span> <span data-ttu-id="cc4f2-201">為了提高彈性，請使用與 PowerShell 指令碼相關的參數路徑，不要使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-201">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="cc4f2-202">-TemplateParametersFile</span><span class="sxs-lookup"><span data-stu-id="cc4f2-202">-TemplateParametersFile</span></span> |<span data-ttu-id="cc4f2-203">Azure 資源群組部署專案中的參數檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-203">The path to the parameters file in the Azure Resource Group deployment project.</span></span> <span data-ttu-id="cc4f2-204">為了提高彈性，請使用與 PowerShell 指令碼相關的參數路徑，不要使用絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-204">To enhance flexibility, use a path for this parameter that is relative to the location of the PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="cc4f2-205">-ArtifactStagingDirectory</span><span class="sxs-lookup"><span data-stu-id="cc4f2-205">-ArtifactStagingDirectory</span></span> |<span data-ttu-id="cc4f2-206">此參數可讓 PowerShell 指令碼從應該複製專案二進位檔的位置取得資料夾。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-206">This parameter lets the PowerShell script know the folder from where the project’s binary files should be copied.</span></span> <span data-ttu-id="cc4f2-207">這個值會覆寫 PowerShell 指令碼使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-207">This value overrides the default value used by the PowerShell script.</span></span> <span data-ttu-id="cc4f2-208">若要供 VS Team Services 使用，請將值設為：-ArtifactStagingDirectory $(Build.StagingDirectory)</span><span class="sxs-lookup"><span data-stu-id="cc4f2-208">For VS Team Services use, set the value to: -ArtifactStagingDirectory $(Build.StagingDirectory)</span></span> |
   
   <span data-ttu-id="cc4f2-209">以下是指令碼引數的範例 (斷行以方便閱讀)：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-209">Here’s a script arguments example (line broken for readability):</span></span>
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   <span data-ttu-id="cc4f2-210">完成之後，[指令碼引數] 方塊應該如下清單所示：</span><span class="sxs-lookup"><span data-stu-id="cc4f2-210">When you’re finished, the **Script Arguments** box should resemble the following list:</span></span>
   
   ![指令碼引數][11]
9. <span data-ttu-id="cc4f2-212">將所有必要的項目都加入 Azure PowerShell 建置步驟之後，請選擇 [佇列]  建置按鈕以建置專案。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-212">After you’ve added all the required items to the Azure PowerShell build step, choose the **Queue** build button to build the project.</span></span> <span data-ttu-id="cc4f2-213">[建置]  畫面會顯示 PowerShell 指令碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-213">The **Build** screen shows the output from the PowerShell script.</span></span>

### <a name="detailed-walkthrough-for-option-2"></a><span data-ttu-id="cc4f2-214">選項 2 的詳細逐步解說</span><span class="sxs-lookup"><span data-stu-id="cc4f2-214">Detailed walkthrough for Option 2</span></span>
<span data-ttu-id="cc4f2-215">下列程序會使用內建工作，逐步引導您進行在 VS Team Services 中設定持續部署所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-215">The following procedures walk you through the steps necessary to configure continuous deployment in VS Team Services using the built-in tasks.</span></span>

1. <span data-ttu-id="cc4f2-216">編輯您的 VS Team Services 組建定義來新增兩個新的建置步驟。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-216">Edit your VS Team Services build definition to add two new build steps.</span></span> <span data-ttu-id="cc4f2-217">在 [組建定義] 類別下選擇組建定義，再選擇 [編輯] 連結。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-217">Choose the build definition under the **Build definitions** category and then choose the **Edit** link.</span></span>
   
   ![編輯組建定義][12]
2. <span data-ttu-id="cc4f2-219">將新的建置步驟新增至組建定義，方法為使用 [新增建置步驟...]</span><span class="sxs-lookup"><span data-stu-id="cc4f2-219">Add the new build steps to the build definition using the **Add build step…**</span></span> <span data-ttu-id="cc4f2-220">按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-220">button.</span></span>
   
   ![新增組建步驟][13]
3. <span data-ttu-id="cc4f2-222">選擇 [部署工作] 類別，選取 [Azure 檔案複製] 工作，再選擇其 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-222">Choose the **Deploy** task category, select the **Azure File Copy** task, and then choose its **Add** button.</span></span>
   
   ![新增 Azure 檔案複製工作][14]
4. <span data-ttu-id="cc4f2-224">選擇 [Azure 資源群組部署] 工作，然後選擇其 [新增] 按鈕，然後 [關閉] [工作目錄]。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-224">Choose the **Azure Resource Group Deployment** task, then choose its **Add** button and then **Close** the **Task Catalog**.</span></span>
   
   ![新增 [Azure 資源群組部署] 工作][15]
5. <span data-ttu-id="cc4f2-226">選擇 **Azure 檔案複製**工作並填入其值。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-226">Choose the **Azure File Copy** task and fill in its values.</span></span>
   
   <span data-ttu-id="cc4f2-227">如果您已將 Azure 服務端點新增至 VS Team Services，請在 [Azure 訂用帳戶] 下拉式清單方塊中選擇訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-227">If you already have an Azure service endpoint added to VS Team Services, choose the subscription in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="cc4f2-228">如果您沒有訂用帳戶，請參閱[選項 1](#detailed-walkthrough-for-option-1)，以查看在 VS Team Services 中設定訂用帳戶的指示。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-228">If you do not have a subscription, see [Option 1](#detailed-walkthrough-for-option-1) for instructions on setting one up in VS Team Services.</span></span>
   
   * <span data-ttu-id="cc4f2-229">來源 - 輸入 **$(Build.StagingDirectory)**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-229">Source - enter **$(Build.StagingDirectory)**</span></span>
   * <span data-ttu-id="cc4f2-230">Azure 連線類型 - 選取 **Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-230">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="cc4f2-231">Azure RM 訂用帳戶 - 在 [Azure 訂用帳戶] 下拉式清單方塊中，選取您想要使用之儲存體帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-231">Azure RM Subscription - select the subscription for the storage account you want to use in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="cc4f2-232">如果訂用帳戶未出現，請選擇 [管理] 連結旁的 [重新整理]按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-232">If the subscription doesn't appear, choose the **Refresh** button next the **Manage** link.</span></span>
   * <span data-ttu-id="cc4f2-233">目的地類型 - 選取 **Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-233">Destination Type - select **Azure Blob**</span></span>
   * <span data-ttu-id="cc4f2-234">RM 儲存體帳戶 - 選取您想要針對預備構件使用的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cc4f2-234">RM Storage Account - select the storage account you would like to use for staging artifacts</span></span>
   * <span data-ttu-id="cc4f2-235">容器名稱 - 輸入您想要用於暫存的容器名稱，可以是任何有效的容器名稱，但請使用專用於此組建定義的名稱</span><span class="sxs-lookup"><span data-stu-id="cc4f2-235">Container Name - enter the name of the container you would like to use for staging; it can be any valid container name, but use one dedicated to this build definition</span></span>
   
   <span data-ttu-id="cc4f2-236">輸出值︰</span><span class="sxs-lookup"><span data-stu-id="cc4f2-236">For the output values:</span></span>
   
   * <span data-ttu-id="cc4f2-237">儲存體容器 URI - 輸入 **artifactsLocation**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-237">Storage Container URI - enter **artifactsLocation**</span></span>
   * <span data-ttu-id="cc4f2-238">儲存體容器 SAS - 輸入 **artifactsLocationSasToken**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-238">Storage Container SAS Token - enter **artifactsLocationSasToken**</span></span>
   
   ![設定 Azure 檔案複製工作][16]
6. <span data-ttu-id="cc4f2-240">選擇 [Azure 資源群組部署]  組建步驟，再填上其值。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-240">Choose the **Azure Resource Group Deployment** build step and then fill in its values.</span></span>
   
   * <span data-ttu-id="cc4f2-241">Azure 連線類型 - 選取 **Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-241">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="cc4f2-242">Azure RM 訂用帳戶 - 在 [Azure 訂用帳戶] 下拉式清單方塊中選取部署的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-242">Azure RM Subscription - select the subscription for deployment in the **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="cc4f2-243">這通常與上一個步驟中使用的訂用帳戶相同</span><span class="sxs-lookup"><span data-stu-id="cc4f2-243">This will usually be the same subscription used in the previous step</span></span>
   * <span data-ttu-id="cc4f2-244">動作 - 選取 **建立或更新資源群組**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-244">Action - select **Create or Update Resource Group**</span></span>
   * <span data-ttu-id="cc4f2-245">資源群組 - 選取資源群組或輸入部署的新資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="cc4f2-245">Resource Group - select a resource group or enter the name of a new resource group for the deployment</span></span>
   * <span data-ttu-id="cc4f2-246">位置 - 選取資源群組的位置</span><span class="sxs-lookup"><span data-stu-id="cc4f2-246">Location - select the location for the resource group</span></span>
   * <span data-ttu-id="cc4f2-247">範本 - 輸入要部署之範本的名稱與路徑前面加上 **$(Build.StagingDirectory)**，例如︰**$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-247">Template - enter the path and name of the template to be deployed prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span></span>
   * <span data-ttu-id="cc4f2-248">範本參數 - 輸入要使用之參數的名稱與路徑，前面加上 **$(Build.StagingDirectory)**，例如︰**$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span><span class="sxs-lookup"><span data-stu-id="cc4f2-248">Template Parameters - enter the path and name of the parameters to be used, prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span></span>
   * <span data-ttu-id="cc4f2-249">覆寫範本參數 - 輸入或複製並貼上下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="cc4f2-249">Override Template Parameters - enter or copy and paste the following code:</span></span>
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![設定 [Azure 資源群組部署] 工作][17]
7. <span data-ttu-id="cc4f2-251">在新增所有必要的項目之後，儲存組建定義然後在頂端選擇 [將新組建排入佇列]。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-251">After you’ve added all the required items, save the build definition and choose **Queue new build** at the top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc4f2-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc4f2-252">Next steps</span></span>
<span data-ttu-id="cc4f2-253">如需 Azure Resource Manager 和 Azure 資源群組的詳細資訊的詳細資訊，請參閱 [Azure Resource Manager 概觀](azure-resource-manager/resource-group-overview.md) 。</span><span class="sxs-lookup"><span data-stu-id="cc4f2-253">Read [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md) to learn more about Azure Resource Manager and Azure resource groups.</span></span>

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
