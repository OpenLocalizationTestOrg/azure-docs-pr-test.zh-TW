---
title: "使用 Azure 資源群組專案的 VS Team Services 中的 aaaContinuous 整合 |Microsoft 文件"
description: "描述在 Visual Studio Team Services 中使用 Azure 資源群組部署的連續整合 tooset Visual Studio 中的專案。"
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
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a><span data-ttu-id="1d16e-103">使用 Azure 資源群組部署專案在 Visual Studio Team Services 中進行連續整合</span><span class="sxs-lookup"><span data-stu-id="1d16e-103">Continuous integration in Visual Studio Team Services using Azure Resource Group deployment projects</span></span>
<span data-ttu-id="1d16e-104">toodeploy Azure 的範本，您在執行工作各個階段： 建置時，測試中，複製 tooAzure （也稱為 「 預備 」），並部署範本。</span><span class="sxs-lookup"><span data-stu-id="1d16e-104">toodeploy an Azure template, you perform tasks in various stages: Build, Test, Copy tooAzure (also called "Staging"), and Deploy Template.</span></span> <span data-ttu-id="1d16e-105">有兩個不同的方式 toodeploy 範本 tooVisual Studio Team Services (VS Team Services)。</span><span class="sxs-lookup"><span data-stu-id="1d16e-105">There are two different ways toodeploy templates tooVisual Studio Team Services (VS Team Services).</span></span> <span data-ttu-id="1d16e-106">這兩種方法提供 hello 相同的結果，因此請選擇最適合您的工作流程的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="1d16e-106">Both methods provide hello same results, so choose hello one that best fits your workflow.</span></span>

1. <span data-ttu-id="1d16e-107">加入執行包含 hello Azure 資源群組部署專案 (Deploy-azureresourcegroup.ps1) 中的 hello PowerShell 指令碼的單一步驟 tooyour 組建定義。</span><span class="sxs-lookup"><span data-stu-id="1d16e-107">Add a single step tooyour build definition that runs hello PowerShell script that’s included in hello Azure Resource Group deployment project (Deploy-AzureResourceGroup.ps1).</span></span> <span data-ttu-id="1d16e-108">hello 指令碼複製成品，並將部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1d16e-108">hello script copies artifacts and then deploys hello template.</span></span>
2. <span data-ttu-id="1d16e-109">新增多個 VS Team Services 建置步驟，每個都執行一個階段工作。</span><span class="sxs-lookup"><span data-stu-id="1d16e-109">Add multiple VS Team Services build steps, each one performing a stage task.</span></span>

<span data-ttu-id="1d16e-110">本文將示範兩個選項。</span><span class="sxs-lookup"><span data-stu-id="1d16e-110">This article demonstrates both options.</span></span> <span data-ttu-id="1d16e-111">hello 第一個選項優點 hello hello 使用相同的指令碼開發人員使用 Visual Studio 中，並提供整個 hello 生命週期的一致性。</span><span class="sxs-lookup"><span data-stu-id="1d16e-111">hello first option has hello advantage of using hello same script used by developers in Visual Studio and providing consistency throughout hello lifecycle.</span></span> <span data-ttu-id="1d16e-112">hello 第二個選項可提供方便的替代 toohello 內建指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d16e-112">hello second option offers a convenient alternative toohello built-in script.</span></span> <span data-ttu-id="1d16e-113">這兩個程序假設您已經在 VS Team Services 中簽入 Visual Studio 部署專案。</span><span class="sxs-lookup"><span data-stu-id="1d16e-113">Both procedures assume you already have a Visual Studio deployment project checked into VS Team Services.</span></span>

## <a name="copy-artifacts-tooazure"></a><span data-ttu-id="1d16e-114">複製成品 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d16e-114">Copy artifacts tooAzure</span></span>
<span data-ttu-id="1d16e-115">不論 hello 案例中，如果您有任何所需的範本部署的成品必須提供 Azure Resource Manager 存取 toothem。</span><span class="sxs-lookup"><span data-stu-id="1d16e-115">Regardless of hello scenario, if you have any artifacts that are needed for template deployment, you must give Azure Resource Manager access toothem.</span></span> <span data-ttu-id="1d16e-116">這些構件包括下列檔案：</span><span class="sxs-lookup"><span data-stu-id="1d16e-116">These artifacts can include files such as:</span></span>

* <span data-ttu-id="1d16e-117">巢狀範本</span><span class="sxs-lookup"><span data-stu-id="1d16e-117">Nested templates</span></span>
* <span data-ttu-id="1d16e-118">組態指令碼及 DSC 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d16e-118">Configuration scripts and DSC scripts</span></span>
* <span data-ttu-id="1d16e-119">應用程式二進位檔</span><span class="sxs-lookup"><span data-stu-id="1d16e-119">Application binaries</span></span>

### <a name="nested-templates-and-configuration-scripts"></a><span data-ttu-id="1d16e-120">巢狀範本和組態指令碼</span><span class="sxs-lookup"><span data-stu-id="1d16e-120">Nested Templates and Configuration Scripts</span></span>
<span data-ttu-id="1d16e-121">當您使用 Visual Studio 所提供的 hello 範本 （或使用 Visual Studio 程式碼片段建置），hello PowerShell 指令碼不僅會設置 hello 成品，如需不同部署的 hello 資源 hello URI 也會參數化。</span><span class="sxs-lookup"><span data-stu-id="1d16e-121">When you use hello templates provided by Visual Studio (or built with Visual Studio snippets), hello PowerShell script not only stages hello artifacts, it also parameterizes hello URI for hello resources for different deployments.</span></span> <span data-ttu-id="1d16e-122">hello 指令碼，然後複製在 Azure 中的 hello 成品 tooa 安全容器、 建立 SaS 權杖，該容器，並接著會將 toohello 範本部署上的該資訊傳遞。</span><span class="sxs-lookup"><span data-stu-id="1d16e-122">hello script then copies hello artifacts tooa secure container in Azure, creates a SaS token for that container, and then passes that information on toohello template deployment.</span></span> <span data-ttu-id="1d16e-123">請參閱[建立範本部署](https://msdn.microsoft.com/library/azure/dn790564.aspx)toolearn 深入了解巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="1d16e-123">See [Create a template deployment](https://msdn.microsoft.com/library/azure/dn790564.aspx) toolearn more about nested templates.</span></span>  <span data-ttu-id="1d16e-124">當 VS Team Services 中使用的工作，您必須選取針對範本部署的 hello 適當工作，並如有必要，請從預備環境步驟 toohello 範本部署的 hello 傳遞參數值。</span><span class="sxs-lookup"><span data-stu-id="1d16e-124">When using tasks in VS Team Services, you must select hello appropriate tasks for your template deployment and if necessary, pass parameter values from hello staging step toohello template deployment.</span></span>

## <a name="set-up-continuous-deployment-in-vs-team-services"></a><span data-ttu-id="1d16e-125">在 VS Team Services 中設定連續部署</span><span class="sxs-lookup"><span data-stu-id="1d16e-125">Set up continuous deployment in VS Team Services</span></span>
<span data-ttu-id="1d16e-126">您需要 tooupdate toocall VS Team Services 中的 hello PowerShell 指令碼，您的組建定義。</span><span class="sxs-lookup"><span data-stu-id="1d16e-126">toocall hello PowerShell script in VS Team Services, you need tooupdate your build definition.</span></span> <span data-ttu-id="1d16e-127">簡單地說，hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="1d16e-127">In brief, hello steps are:</span></span> 

1. <span data-ttu-id="1d16e-128">編輯 hello 組建定義。</span><span class="sxs-lookup"><span data-stu-id="1d16e-128">Edit hello build definition.</span></span>
2. <span data-ttu-id="1d16e-129">在 VS Team Services 中設定 Azure 授權。</span><span class="sxs-lookup"><span data-stu-id="1d16e-129">Set up Azure authorization in VS Team Services.</span></span>
3. <span data-ttu-id="1d16e-130">新增參考 hello hello Azure 資源群組部署專案中的 PowerShell 指令碼的 Azure PowerShell 建置步驟。</span><span class="sxs-lookup"><span data-stu-id="1d16e-130">Add an Azure PowerShell build step that references hello PowerShell script in hello Azure Resource Group deployment project.</span></span>
4. <span data-ttu-id="1d16e-131">設定 hello hello 值*-ArtifactsStagingDirectory*參數 toowork 與 VS Team Services 中所建置的專案。</span><span class="sxs-lookup"><span data-stu-id="1d16e-131">Set hello value of hello *-ArtifactsStagingDirectory* parameter toowork with a project built in VS Team Services.</span></span>

### <a name="detailed-walkthrough-for-option-1"></a><span data-ttu-id="1d16e-132">選項 1 的詳細逐步解說</span><span class="sxs-lookup"><span data-stu-id="1d16e-132">Detailed walkthrough for Option 1</span></span>
<span data-ttu-id="1d16e-133">hello 下列程序引導您完成使用單一工作執行 hello PowerShell 指令碼專案中的 VS Team Services 中的 hello 步驟需要 tooconfigure 連續部署。</span><span class="sxs-lookup"><span data-stu-id="1d16e-133">hello following procedures walk you through hello steps necessary tooconfigure continuous deployment in VS Team Services using a single task that runs hello PowerShell script in your project.</span></span> 

1. <span data-ttu-id="1d16e-134">編輯您的 VS Team Services 組建定義並新增 Azure PowerShell 建置步驟。</span><span class="sxs-lookup"><span data-stu-id="1d16e-134">Edit your VS Team Services build definition and add an Azure PowerShell build step.</span></span> <span data-ttu-id="1d16e-135">選擇在 hello hello 組建定義**組建定義**類別目錄，然後選擇 hello**編輯**連結。</span><span class="sxs-lookup"><span data-stu-id="1d16e-135">Choose hello build definition under hello **Build definitions** category and then choose hello **Edit** link.</span></span>
   
   ![編輯組建定義][0]
2. <span data-ttu-id="1d16e-137">加入新**Azure PowerShell**建置步驟 toohello 組建定義，然後選擇 hello**加入建置步驟...**</span><span class="sxs-lookup"><span data-stu-id="1d16e-137">Add a new **Azure PowerShell** build step toohello build definition and then choose hello **Add build step…**</span></span> <span data-ttu-id="1d16e-138">按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d16e-138">button.</span></span>
   
   ![新增組建步驟][1]
3. <span data-ttu-id="1d16e-140">選擇 hello**部署工作**類別目錄中，選取 hello **Azure PowerShell**工作，並再選擇其**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d16e-140">Choose hello **Deploy task** category, select hello **Azure PowerShell** task, and then choose its **Add** button.</span></span>
   
   ![新增工作][2]
4. <span data-ttu-id="1d16e-142">選擇 hello **Azure PowerShell**建置步驟，然後填入其值。</span><span class="sxs-lookup"><span data-stu-id="1d16e-142">Choose hello **Azure PowerShell** build step and then fill in its values.</span></span>
   
   1. <span data-ttu-id="1d16e-143">如果您已經有 Azure 服務端點加入 tooVS Team Services 中，選擇 hello 訂閱 hello **Azure 訂用帳戶**下拉式清單方塊，然後略過 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="1d16e-143">If you already have an Azure service endpoint added tooVS Team Services, choose hello subscription in hello **Azure Subscription** drop-down list box and then skip toohello next section.</span></span> 
      
      <span data-ttu-id="1d16e-144">如果您還沒有 Azure 服務端點在 VS Team Services 中，您會需要 tooadd 其中一個。</span><span class="sxs-lookup"><span data-stu-id="1d16e-144">If you don’t have an Azure service endpoint in VS Team Services, you need tooadd one.</span></span> <span data-ttu-id="1d16e-145">本小節會帶領您完成 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="1d16e-145">This subsection takes you through hello process.</span></span> <span data-ttu-id="1d16e-146">如果您的 Azure 帳戶使用 Microsoft 帳戶 （例如 Hotmail)，您必須採取下列步驟 tooget hello 服務主體驗證。</span><span class="sxs-lookup"><span data-stu-id="1d16e-146">If your Azure account uses a Microsoft account (such as Hotmail), you must take hello following steps tooget a Service Principal authentication.</span></span>
   2. <span data-ttu-id="1d16e-147">選擇 hello**管理**連結下一步 toohello **Azure 訂用帳戶**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-147">Choose hello **Manage** link next toohello **Azure Subscription** drop-down list box.</span></span>
      
      ![管理 Azure 訂用帳戶][3]
   3. <span data-ttu-id="1d16e-149">選擇**Azure**在 hello**新的服務端點**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-149">Choose **Azure** in hello **New Service Endpoint** drop-down list box.</span></span>
      
      ![新增服務端點][4]
   4. <span data-ttu-id="1d16e-151">在 hello**新增 Azure 訂用帳戶**對話方塊中，選取 hello**服務主體**選項。</span><span class="sxs-lookup"><span data-stu-id="1d16e-151">In hello **Add Azure Subscription** dialog box, select hello **Service Principal** option.</span></span>
      
      ![服務主體選項][5]
   5. <span data-ttu-id="1d16e-153">加入您的 Azure 訂用帳戶資訊 toohello**新增 Azure 訂用帳戶** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-153">Add your Azure subscription information toohello **Add Azure Subscription** dialog box.</span></span> <span data-ttu-id="1d16e-154">您需要下列項目 tooprovide hello:</span><span class="sxs-lookup"><span data-stu-id="1d16e-154">You need tooprovide hello following items:</span></span>
      
      * <span data-ttu-id="1d16e-155">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="1d16e-155">Subscription Id</span></span>
      * <span data-ttu-id="1d16e-156">訂用帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="1d16e-156">Subscription Name</span></span>
      * <span data-ttu-id="1d16e-157">服務主體識別碼</span><span class="sxs-lookup"><span data-stu-id="1d16e-157">Service Principal Id</span></span>
      * <span data-ttu-id="1d16e-158">服務主體金鑰</span><span class="sxs-lookup"><span data-stu-id="1d16e-158">Service Principal Key</span></span>
      * <span data-ttu-id="1d16e-159">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="1d16e-159">Tenant Id</span></span>
   6. <span data-ttu-id="1d16e-160">新增您選擇 toohello 名稱**訂用帳戶**名稱 方塊中。</span><span class="sxs-lookup"><span data-stu-id="1d16e-160">Add a name of your choice toohello **Subscription** name box.</span></span> <span data-ttu-id="1d16e-161">這個值會出現在 hello 稍後**Azure 訂用帳戶**VS Team Services 中的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="1d16e-161">This value appears later in hello **Azure Subscription** drop-down list in VS Team Services.</span></span> 
   7. <span data-ttu-id="1d16e-162">如果您不知道您的 Azure 訂用帳戶 ID，您可以使用下列命令 tooretrieve hello 的其中一個它。</span><span class="sxs-lookup"><span data-stu-id="1d16e-162">If you don’t know your Azure subscription ID, you can use one of hello following commands tooretrieve it.</span></span>
      
      <span data-ttu-id="1d16e-163">對於 Azure PowerShell 指令碼，請使用：</span><span class="sxs-lookup"><span data-stu-id="1d16e-163">For PowerShell scripts, use:</span></span>
      
      `Get-AzureRmSubscription`
      
      <span data-ttu-id="1d16e-164">對於 Azure CLI，請使用：</span><span class="sxs-lookup"><span data-stu-id="1d16e-164">For Azure CLI, use:</span></span>
      
      `azure account show`
   8. <span data-ttu-id="1d16e-165">tooget 服務主體識別碼、 服務主要金鑰和租用戶識別碼，請依照下列中的 hello 程序[建立 Active Directory 應用程式和服務主體使用入口網站](resource-group-create-service-principal-portal.md)或[驗證的服務主體Azure 資源管理員](resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="1d16e-165">tooget a Service Principal ID, Service Principal Key, and Tenant ID, follow hello procedure in [Create Active Directory application and service principal using portal](resource-group-create-service-principal-portal.md) or [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal.md).</span></span>
   9. <span data-ttu-id="1d16e-166">新增 hello 服務主體識別碼、 服務主要金鑰，以及租用戶識別碼值 toohello**新增 Azure 訂用帳戶**對話方塊方塊，然後選擇 [hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d16e-166">Add hello Service Principal ID, Service Principal Key, and Tenant ID values toohello **Add Azure Subscription** dialog box and then choose hello **OK** button.</span></span>
      
      <span data-ttu-id="1d16e-167">您現在有有效的服務主體 toouse toorun hello Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d16e-167">You now have a valid Service Principal toouse toorun hello Azure PowerShell script.</span></span>
5. <span data-ttu-id="1d16e-168">編輯 hello 組建定義，並選擇 hello **Azure PowerShell**建置步驟。</span><span class="sxs-lookup"><span data-stu-id="1d16e-168">Edit hello build definition and choose hello **Azure PowerShell** build step.</span></span> <span data-ttu-id="1d16e-169">選取 hello 訂用帳戶中 hello **Azure 訂用帳戶**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-169">Select hello subscription in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="1d16e-170">(如果 hello 訂用帳戶未出現，請選擇 hello**重新整理**按鈕的下一個 hello**管理**連結。)</span><span class="sxs-lookup"><span data-stu-id="1d16e-170">(If hello subscription doesn't appear, choose hello **Refresh** button next hello **Manage** link.)</span></span> 
   
   ![安裝並設定 Azure PowerShell 建置工作][8]
6. <span data-ttu-id="1d16e-172">提供路徑 toohello Deploy-azureresourcegroup.ps1 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d16e-172">Provide a path toohello Deploy-AzureResourceGroup.ps1 PowerShell script.</span></span> <span data-ttu-id="1d16e-173">toodo，選擇 hello 省略符號 （...） 按鈕的下一個 toohello**指令碼路徑**方塊中，瀏覽 toohello Deploy-azureresourcegroup.ps1 PowerShell 指令碼，在 hello**指令碼**您的專案的資料夾，選取它，然後選擇 [hello**確定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d16e-173">toodo this, choose hello ellipsis (…) button next toohello **Script Path** box, navigate toohello Deploy-AzureResourceGroup.ps1 PowerShell script in hello **Scripts** folder of your project, select it, and then choose hello **OK** button.</span></span>    
   
   ![選取路徑 tooscript][9]
7. <span data-ttu-id="1d16e-175">您選取 hello 指令碼之後，更新 hello 路徑 toohello 指令碼，讓它會執行從 hello Build.StagingDirectory (hello 相同的目錄， *ArtifactsLocation*設)。</span><span class="sxs-lookup"><span data-stu-id="1d16e-175">After you select hello script, update hello path toohello script so that it’s run from hello Build.StagingDirectory (hello same directory that *ArtifactsLocation* is set to).</span></span> <span data-ttu-id="1d16e-176">您可以藉由新增"$（Build.StagingDirectory)/"toohello 開頭 hello 指令碼路徑。</span><span class="sxs-lookup"><span data-stu-id="1d16e-176">You can do this by adding “$(Build.StagingDirectory)/” toohello beginning of hello script path.</span></span>
   
    ![編輯路徑 tooscript][10]
8. <span data-ttu-id="1d16e-178">在 hello**指令碼引數**方塊中，輸入下列參數 （在單一行） 中的 hello。</span><span class="sxs-lookup"><span data-stu-id="1d16e-178">In hello **Script Arguments** box, enter hello following parameters (in a single line).</span></span> <span data-ttu-id="1d16e-179">當您執行 Visual Studio 中的 hello 指令碼時，您可以查看如何與使用 hello 參數在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="1d16e-179">When you run hello script in Visual Studio, you can see how VS uses hello parameters in hello **Output** window.</span></span> <span data-ttu-id="1d16e-180">您可以使用它做為起點建置步驟中設定 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="1d16e-180">You can use this as a starting point for setting hello parameter values in your build step.</span></span>
   
   | <span data-ttu-id="1d16e-181">參數</span><span class="sxs-lookup"><span data-stu-id="1d16e-181">Parameter</span></span> | <span data-ttu-id="1d16e-182">說明</span><span class="sxs-lookup"><span data-stu-id="1d16e-182">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1d16e-183">-ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="1d16e-183">-ResourceGroupLocation</span></span> |<span data-ttu-id="1d16e-184">hello hello 資源群組的位置，例如地理位置值**eastus**或**'美國東部'**。</span><span class="sxs-lookup"><span data-stu-id="1d16e-184">hello geo-location value where hello resource group is located, such as **eastus** or **'East US'**.</span></span> <span data-ttu-id="1d16e-185">（新增方以單引號包住如果 hello 名稱中有空格。）如需詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/en-us/regions/)。</span><span class="sxs-lookup"><span data-stu-id="1d16e-185">(Add single quotes if there's a space in hello name.) See [Azure Regions](https://azure.microsoft.com/en-us/regions/) for more information.</span></span> |
   | <span data-ttu-id="1d16e-186">-ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1d16e-186">-ResourceGroupName</span></span> |<span data-ttu-id="1d16e-187">hello 用於這個部署的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1d16e-187">hello name of hello resource group used for this deployment.</span></span> |
   | <span data-ttu-id="1d16e-188">-UploadArtifacts</span><span class="sxs-lookup"><span data-stu-id="1d16e-188">-UploadArtifacts</span></span> |<span data-ttu-id="1d16e-189">此參數存在時，會指定需要 toobe 的成品上傳 tooAzure 從 hello 本機系統。</span><span class="sxs-lookup"><span data-stu-id="1d16e-189">This parameter, when present, specifies that artifacts that need toobe uploaded tooAzure from hello local system.</span></span> <span data-ttu-id="1d16e-190">您只需要 tooset 此交換器如果範本部署需要額外的 toostage 使用 hello PowerShell 指令碼 （例如設定指令碼或巢狀的範本） 的成品。</span><span class="sxs-lookup"><span data-stu-id="1d16e-190">You only need tooset this switch if your template deployment requires extra artifacts that you want toostage using hello PowerShell script (such as configuration scripts or nested templates).</span></span> |
   | <span data-ttu-id="1d16e-191">-StorageAccountName</span><span class="sxs-lookup"><span data-stu-id="1d16e-191">-StorageAccountName</span></span> |<span data-ttu-id="1d16e-192">hello hello 儲存體帳戶名稱會用於此部署 toostage 成品。</span><span class="sxs-lookup"><span data-stu-id="1d16e-192">hello name of hello storage account used toostage artifacts for this deployment.</span></span> <span data-ttu-id="1d16e-193">僅在您執行部署的成品時才會使用這個參數。</span><span class="sxs-lookup"><span data-stu-id="1d16e-193">This parameter is only used if you are staging artifacts for deployment.</span></span> <span data-ttu-id="1d16e-194">如果沒有提供這個參數，如果 hello 指令碼已不會建立在先前的部署期間建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d16e-194">If this parameter is supplied, a new storage account is created if hello script has not created one during a previous deployment.</span></span> <span data-ttu-id="1d16e-195">如果指定了 hello 參數，hello 儲存體帳戶必須已經存在。</span><span class="sxs-lookup"><span data-stu-id="1d16e-195">If hello parameter is specified, hello storage account must already exist.</span></span> |
   | <span data-ttu-id="1d16e-196">-StorageAccountResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1d16e-196">-StorageAccountResourceGroupName</span></span> |<span data-ttu-id="1d16e-197">hello hello hello 儲存體帳戶相關聯的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1d16e-197">hello name of hello resource group associated with hello storage account.</span></span> <span data-ttu-id="1d16e-198">Hello StorageAccountName 參數中提供的值時，才需要此參數。</span><span class="sxs-lookup"><span data-stu-id="1d16e-198">This parameter is required only if you provide a value for hello StorageAccountName parameter.</span></span> |
   | <span data-ttu-id="1d16e-199">-TemplateFile</span><span class="sxs-lookup"><span data-stu-id="1d16e-199">-TemplateFile</span></span> |<span data-ttu-id="1d16e-200">hello 路徑 toohello 範本檔案 hello Azure 資源群組部署專案中。</span><span class="sxs-lookup"><span data-stu-id="1d16e-200">hello path toohello template file in hello Azure Resource Group deployment project.</span></span> <span data-ttu-id="1d16e-201">使用這個參數，這是 hello PowerShell 指令碼，而不是絕對路徑的相對 toohello 位置路徑 tooenhance 彈性。</span><span class="sxs-lookup"><span data-stu-id="1d16e-201">tooenhance flexibility, use a path for this parameter that is relative toohello location of hello PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="1d16e-202">-TemplateParametersFile</span><span class="sxs-lookup"><span data-stu-id="1d16e-202">-TemplateParametersFile</span></span> |<span data-ttu-id="1d16e-203">hello 路徑 toohello 參數檔案 hello Azure 資源群組部署專案中。</span><span class="sxs-lookup"><span data-stu-id="1d16e-203">hello path toohello parameters file in hello Azure Resource Group deployment project.</span></span> <span data-ttu-id="1d16e-204">使用這個參數，這是 hello PowerShell 指令碼，而不是絕對路徑的相對 toohello 位置路徑 tooenhance 彈性。</span><span class="sxs-lookup"><span data-stu-id="1d16e-204">tooenhance flexibility, use a path for this parameter that is relative toohello location of hello PowerShell script instead of an absolute path.</span></span> |
   | <span data-ttu-id="1d16e-205">-ArtifactStagingDirectory</span><span class="sxs-lookup"><span data-stu-id="1d16e-205">-ArtifactStagingDirectory</span></span> |<span data-ttu-id="1d16e-206">這個參數可讓您知道 hello 資料夾從 hello 專案的二進位檔案應該複製其中的 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d16e-206">This parameter lets hello PowerShell script know hello folder from where hello project’s binary files should be copied.</span></span> <span data-ttu-id="1d16e-207">這個值會覆寫 hello hello PowerShell 指令碼所使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="1d16e-207">This value overrides hello default value used by hello PowerShell script.</span></span> <span data-ttu-id="1d16e-208">如需使用 VS Team Services，則將 hello 值設定為:-ArtifactStagingDirectory $(Build.StagingDirectory)</span><span class="sxs-lookup"><span data-stu-id="1d16e-208">For VS Team Services use, set hello value to: -ArtifactStagingDirectory $(Build.StagingDirectory)</span></span> |
   
   <span data-ttu-id="1d16e-209">以下是指令碼引數的範例 (斷行以方便閱讀)：</span><span class="sxs-lookup"><span data-stu-id="1d16e-209">Here’s a script arguments example (line broken for readability):</span></span>
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   <span data-ttu-id="1d16e-210">當您完成時，hello**指令碼引數**方塊應該類似下列清單中的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d16e-210">When you’re finished, hello **Script Arguments** box should resemble hello following list:</span></span>
   
   ![指令碼引數][11]
9. <span data-ttu-id="1d16e-212">您已新增所有 hello Azure PowerShell 建置步驟的必要項目 toohello 之後，請選擇 hello**佇列**建置按鈕 toobuild hello 專案。</span><span class="sxs-lookup"><span data-stu-id="1d16e-212">After you’ve added all hello required items toohello Azure PowerShell build step, choose hello **Queue** build button toobuild hello project.</span></span> <span data-ttu-id="1d16e-213">hello**建置**螢幕會顯示 hello hello PowerShell 指令碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="1d16e-213">hello **Build** screen shows hello output from hello PowerShell script.</span></span>

### <a name="detailed-walkthrough-for-option-2"></a><span data-ttu-id="1d16e-214">選項 2 的詳細逐步解說</span><span class="sxs-lookup"><span data-stu-id="1d16e-214">Detailed walkthrough for Option 2</span></span>
<span data-ttu-id="1d16e-215">hello 下列程序引導您完成使用 hello 內建工作 VS Team Services 中的 hello 步驟需要 tooconfigure 連續部署。</span><span class="sxs-lookup"><span data-stu-id="1d16e-215">hello following procedures walk you through hello steps necessary tooconfigure continuous deployment in VS Team Services using hello built-in tasks.</span></span>

1. <span data-ttu-id="1d16e-216">編輯您 VS Team Services 組建定義 tooadd 兩個新組建的步驟。</span><span class="sxs-lookup"><span data-stu-id="1d16e-216">Edit your VS Team Services build definition tooadd two new build steps.</span></span> <span data-ttu-id="1d16e-217">選擇在 hello hello 組建定義**組建定義**類別目錄，然後選擇 hello**編輯**連結。</span><span class="sxs-lookup"><span data-stu-id="1d16e-217">Choose hello build definition under hello **Build definitions** category and then choose hello **Edit** link.</span></span>
   
   ![編輯組建定義][12]
2. <span data-ttu-id="1d16e-219">加入新的 hello 建置步驟 toohello 組建定義使用 hello**加入建置步驟...**</span><span class="sxs-lookup"><span data-stu-id="1d16e-219">Add hello new build steps toohello build definition using hello **Add build step…**</span></span> <span data-ttu-id="1d16e-220">按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d16e-220">button.</span></span>
   
   ![新增組建步驟][13]
3. <span data-ttu-id="1d16e-222">選擇 hello**部署**工作分類中，選取 hello **Azure File Copy**工作，並再選擇其**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d16e-222">Choose hello **Deploy** task category, select hello **Azure File Copy** task, and then choose its **Add** button.</span></span>
   
   ![新增 Azure 檔案複製工作][14]
4. <span data-ttu-id="1d16e-224">選擇 hello **Azure 資源群組部署**工作，然後選擇其**新增** 按鈕，然後**關閉**hello**工作目錄**。</span><span class="sxs-lookup"><span data-stu-id="1d16e-224">Choose hello **Azure Resource Group Deployment** task, then choose its **Add** button and then **Close** hello **Task Catalog**.</span></span>
   
   ![新增 [Azure 資源群組部署] 工作][15]
5. <span data-ttu-id="1d16e-226">選擇 hello **Azure File Copy**工作，並填入其值。</span><span class="sxs-lookup"><span data-stu-id="1d16e-226">Choose hello **Azure File Copy** task and fill in its values.</span></span>
   
   <span data-ttu-id="1d16e-227">如果您已經有 Azure 服務端點加入 tooVS Team Services 中，選擇 hello 訂閱 hello **Azure 訂用帳戶**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-227">If you already have an Azure service endpoint added tooVS Team Services, choose hello subscription in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="1d16e-228">如果您沒有訂用帳戶，請參閱[選項 1](#detailed-walkthrough-for-option-1)，以查看在 VS Team Services 中設定訂用帳戶的指示。</span><span class="sxs-lookup"><span data-stu-id="1d16e-228">If you do not have a subscription, see [Option 1](#detailed-walkthrough-for-option-1) for instructions on setting one up in VS Team Services.</span></span>
   
   * <span data-ttu-id="1d16e-229">來源 - 輸入 **$(Build.StagingDirectory)**</span><span class="sxs-lookup"><span data-stu-id="1d16e-229">Source - enter **$(Build.StagingDirectory)**</span></span>
   * <span data-ttu-id="1d16e-230">Azure 連線類型 - 選取 **Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="1d16e-230">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="1d16e-231">Azure RM 訂用帳戶-您想要在 hello toouse hello 儲存體帳戶的訂用帳戶選取 hello **Azure 訂用帳戶**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-231">Azure RM Subscription - select hello subscription for hello storage account you want toouse in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="1d16e-232">如果 hello 訂用帳戶未出現，請選擇 hello**重新整理**按鈕的下一個 hello**管理**連結。</span><span class="sxs-lookup"><span data-stu-id="1d16e-232">If hello subscription doesn't appear, choose hello **Refresh** button next hello **Manage** link.</span></span>
   * <span data-ttu-id="1d16e-233">目的地類型 - 選取 **Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="1d16e-233">Destination Type - select **Azure Blob**</span></span>
   * <span data-ttu-id="1d16e-234">希望臨時成品 toouse RM 儲存體帳戶-選取您 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d16e-234">RM Storage Account - select hello storage account you would like toouse for staging artifacts</span></span>
   * <span data-ttu-id="1d16e-235">容器名稱-輸入 hello 名稱的 hello 容器中，您想要 toouse 供暫存。它可以是任何有效的容器名稱，但使用一個專用的 toothis 組建定義</span><span class="sxs-lookup"><span data-stu-id="1d16e-235">Container Name - enter hello name of hello container you would like toouse for staging; it can be any valid container name, but use one dedicated toothis build definition</span></span>
   
   <span data-ttu-id="1d16e-236">Hello 輸出值：</span><span class="sxs-lookup"><span data-stu-id="1d16e-236">For hello output values:</span></span>
   
   * <span data-ttu-id="1d16e-237">儲存體容器 URI - 輸入 **artifactsLocation**</span><span class="sxs-lookup"><span data-stu-id="1d16e-237">Storage Container URI - enter **artifactsLocation**</span></span>
   * <span data-ttu-id="1d16e-238">儲存體容器 SAS - 輸入 **artifactsLocationSasToken**</span><span class="sxs-lookup"><span data-stu-id="1d16e-238">Storage Container SAS Token - enter **artifactsLocationSasToken**</span></span>
   
   ![設定 Azure 檔案複製工作][16]
6. <span data-ttu-id="1d16e-240">選擇 hello **Azure 資源群組部署**建置步驟，然後填入其值。</span><span class="sxs-lookup"><span data-stu-id="1d16e-240">Choose hello **Azure Resource Group Deployment** build step and then fill in its values.</span></span>
   
   * <span data-ttu-id="1d16e-241">Azure 連線類型 - 選取 **Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="1d16e-241">Azure Connection Type - select **Azure Resource Manager**</span></span>
   * <span data-ttu-id="1d16e-242">Azure RM 訂閱 hello 中部署的訂用帳戶選取 hello **Azure 訂用帳戶**下拉式清單方塊。</span><span class="sxs-lookup"><span data-stu-id="1d16e-242">Azure RM Subscription - select hello subscription for deployment in hello **Azure Subscription** drop-down list box.</span></span> <span data-ttu-id="1d16e-243">這通常會是相同的訂用帳戶使用的 hello hello 上一個步驟中</span><span class="sxs-lookup"><span data-stu-id="1d16e-243">This will usually be hello same subscription used in hello previous step</span></span>
   * <span data-ttu-id="1d16e-244">動作 - 選取 **建立或更新資源群組**</span><span class="sxs-lookup"><span data-stu-id="1d16e-244">Action - select **Create or Update Resource Group**</span></span>
   * <span data-ttu-id="1d16e-245">資源群組-選取的資源群組，或輸入 hello 部署新的資源群組的 hello 名稱</span><span class="sxs-lookup"><span data-stu-id="1d16e-245">Resource Group - select a resource group or enter hello name of a new resource group for hello deployment</span></span>
   * <span data-ttu-id="1d16e-246">位置-選取 hello hello 資源群組位置</span><span class="sxs-lookup"><span data-stu-id="1d16e-246">Location - select hello location for hello resource group</span></span>
   * <span data-ttu-id="1d16e-247">範本-輸入 hello 路徑和名稱 hello 範本部署 toobe 前面加上的**$(Build.StagingDirectory)**，例如： **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span><span class="sxs-lookup"><span data-stu-id="1d16e-247">Template - enter hello path and name of hello template toobe deployed prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**</span></span>
   * <span data-ttu-id="1d16e-248">範本參數的輸入 hello 路徑和名稱使用，hello 參數 toobe 前面加上**$(Build.StagingDirectory)**，例如： **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span><span class="sxs-lookup"><span data-stu-id="1d16e-248">Template Parameters - enter hello path and name of hello parameters toobe used, prepending **$(Build.StagingDirectory)**, for example: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**</span></span>
   * <span data-ttu-id="1d16e-249">覆寫範本參數-輸入或複製並貼上下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d16e-249">Override Template Parameters - enter or copy and paste hello following code:</span></span>
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![設定 [Azure 資源群組部署] 工作][17]
7. <span data-ttu-id="1d16e-251">您已新增 hello 所需的所有項目之後，儲存 hello 組建定義，然後選擇**新組建排入佇列**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="1d16e-251">After you’ve added all hello required items, save hello build definition and choose **Queue new build** at hello top.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d16e-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d16e-252">Next steps</span></span>
<span data-ttu-id="1d16e-253">讀取[Azure 資源管理員概觀](azure-resource-manager/resource-group-overview.md)toolearn 深入了解 Azure 資源管理員和 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="1d16e-253">Read [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md) toolearn more about Azure Resource Manager and Azure resource groups.</span></span>

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
