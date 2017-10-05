---
title: "使用 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源 | Microsoft Docs"
description: "了解如何從 Azure Resource Manager 範本在 Azure DevTest Labs 中建立多個 VM 環境和 PaaS 資源"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: 4e1aae6c041e4572e7e2281203f969e7649e1480
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a><span data-ttu-id="9fbb2-103">使用 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源</span><span class="sxs-lookup"><span data-stu-id="9fbb2-103">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>

<span data-ttu-id="9fbb2-104">[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)可讓您輕鬆地[建立，並將 VM 新增至實驗室](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm)。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-104">The [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) enables you to easily [create and add a VM to a lab](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm).</span></span> <span data-ttu-id="9fbb2-105">這適用於一次建立一個 VM。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-105">This works well for creating one VM at a time.</span></span> <span data-ttu-id="9fbb2-106">不過，如果環境包含多個 VM，則每個 VM 都必須分別建立。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-106">However, if the environment contains multiple VMs, each VM has to be individually created.</span></span> <span data-ttu-id="9fbb2-107">針對多層式 Web 應用程式或 SharePoint 伺服器陣列的情況，需要有機制以允許在單一步驟中建立多個 VM。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-107">For scenarios such as a multi-tier Web app or a SharePoint farm, a mechanism is needed to allow for the creation of multiple VMs in a single step.</span></span> <span data-ttu-id="9fbb2-108">使用 Azure Resource Manager 範本，您現在可以定義 Azure 方案的基礎結構和組態，並在一致的狀態中重複部署多個 VM。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-108">By using Azure Resource Manager templates, you can now define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span></span> <span data-ttu-id="9fbb2-109">此功能可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="9fbb2-109">This feature provides the following benefits:</span></span>

- <span data-ttu-id="9fbb2-110">Azure Resource Manager 範本會直接從您的原始檔控制儲存機制 (GitHub 或 Team Services Git) 載入。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-110">Azure Resource Manager templates are loaded directly from your source control repository (GitHub or Team Services Git).</span></span>
- <span data-ttu-id="9fbb2-111">一旦設定後，您的使用者可以建立環境，方法為從 Azure 入口網站選取 Azure Resource Manager 範本，做為它們可以使用其他類型的 [VM 基底](./devtest-lab-comparing-vm-base-image-types.md)進行的動作。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-111">Once configured, your users can create an environment by picking an Azure Resource Manager template from the Azure portal as what they can do with other types of [VM bases](./devtest-lab-comparing-vm-base-image-types.md).</span></span>
- <span data-ttu-id="9fbb2-112">Azure PaaS 資源除了 IaaS VM 之外，可以從 Azure Resource Manager 範本的環境中佈建。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-112">Azure PaaS resources can be provisioned in an environment from an Azure Resource Manager template in addition to IaaS VMs.</span></span>
- <span data-ttu-id="9fbb2-113">除了其他類型基底所建立的個別 VM 之外，可在實驗室中追蹤環境的成本。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-113">The cost of environments can be tracked in the lab in addition to individual VMs created by other types of bases.</span></span>
- <span data-ttu-id="9fbb2-114">PaaS 資源會建立並出現在成本追蹤中；不過，VM 自動關機不適用於 PaaS 資源。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-114">PaaS resources are created and will appear in cost tracking; however, VM auto shutdown does not apply to PaaS resources.</span></span>
- <span data-ttu-id="9fbb2-115">使用者具有的環境 VM 原則控制與單一實驗室 VM 所具有的相同。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-115">Users have the same VM policy control for environments as they have for single-lab VMs.</span></span>

<span data-ttu-id="9fbb2-116">深入了解許多[使用 Resource Manager 範本的優點](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager)，以透過單一作業部署、更新或刪除所有實驗室資源。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-116">Learn more about the many [benefits of using Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) to deploy, update, or delete all of your lab resources in a single operation.</span></span>

> [!NOTE]
> <span data-ttu-id="9fbb2-117">當您使用 Resource Manager 範本作為建立其他實驗室 VM 的基礎時，不論是建立多重 VM 還是單一 VM，都請記住一些差異。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-117">When you use a Resource Manager template as a basis to create more lab VMs, there are some differences to keep in mind whether you are creating Multi-VMs or single-VMs.</span></span> <span data-ttu-id="9fbb2-118">使用虛擬機器的 Azure Resource Manager 範本會更詳細地說明這些差異。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-118">Use a virtual machine's Azure Resource Manager template explains these differences in greater detail.</span></span>
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a><span data-ttu-id="9fbb2-119">設定 Azure Resource Manager 範本儲存機制</span><span class="sxs-lookup"><span data-stu-id="9fbb2-119">Configure Azure Resource Manager template repositories</span></span>

<span data-ttu-id="9fbb2-120">做為基礎結構即程式碼與組態即程式碼的其中一個最佳作法，應在原始檔控制中管理環境範本。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-120">As one of the best practices with infrastructure-as-code and configuration-as-code, environment templates should be managed in source control.</span></span> <span data-ttu-id="9fbb2-121">Azure DevTest Labs 採用這種作法，並直接從您的 GitHub 或 VSTS Git 儲存機制載入所有 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-121">Azure DevTest Labs follows this practice and loads all Azure Resource Manager templates directly from your GitHub or VSTS Git repositories.</span></span> <span data-ttu-id="9fbb2-122">因此，可以在測試環境到生產環境的整個發行週期使用 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-122">As a result, Resource Manager templates can be used across the entire release cycle, from the test environment to the production environment.</span></span>

<span data-ttu-id="9fbb2-123">您可以遵循幾個規則，以在存放庫中組織 Azure Resource Manager 範本︰</span><span class="sxs-lookup"><span data-stu-id="9fbb2-123">There are a couple of rules to follow to organize your Azure Resource Manager templates in a repository:</span></span>

- <span data-ttu-id="9fbb2-124">主要的範本檔案必須命名為 `azuredeploy.json`。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-124">The master template file must be named `azuredeploy.json`.</span></span> 

    ![金鑰 Azure Resource Manager 範本檔案](./media/devtest-lab-create-environment-from-arm/master-template.png)

- <span data-ttu-id="9fbb2-126">如果您想要使用參數檔案中定義的參數值，參數檔案必須命名為 `azuredeploy.parameters.json`。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-126">If you want to use parameter values defined in a parameter file, the parameter file must be named `azuredeploy.parameters.json`.</span></span>
- <span data-ttu-id="9fbb2-127">您可以使用 `_artifactsLocation` 和 `_artifactsLocationSasToken` 參數來建構 parametersLink URI 值，讓 DevTest Labs 自動管理巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-127">You can use the parameters `_artifactsLocation` and `_artifactsLocationSasToken` to construct the parametersLink URI value, allowing DevTest Labs to automatically manage nested templates.</span></span> <span data-ttu-id="9fbb2-128">如需詳細資訊，請參閱 [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) (Azure DevTest Labs 如何簡化測試環境的巢狀 Resource Manager 範本部署)。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-128">See [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) for more information.</span></span>
- <span data-ttu-id="9fbb2-129">可以定義中繼資料來指定範本顯示名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-129">Metadata can be defined to specify the template display name and description.</span></span> <span data-ttu-id="9fbb2-130">此中繼資料必須在名為 `metadata.json` 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-130">This metadata must be in a file named `metadata.json`.</span></span> <span data-ttu-id="9fbb2-131">下列範例中繼資料檔案說明如何指定顯示名稱和描述︰</span><span class="sxs-lookup"><span data-stu-id="9fbb2-131">The following example metadata file illustrates how to specify the display name and description:</span></span> 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of the template>"
 
}
```

<span data-ttu-id="9fbb2-132">下列步驟將引導您使用 Azure 入口網站將儲存機制新增至您的實驗室。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-132">The following steps guide you through adding a repository to your lab using the Azure portal.</span></span> 

1. <span data-ttu-id="9fbb2-133">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-133">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="9fbb2-134">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-134">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="9fbb2-135">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-135">From the list of labs, select the desired lab.</span></span>   
1. <span data-ttu-id="9fbb2-136">在實驗室的刀鋒視窗上，選取 [組態和原則]。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-136">On the lab's blade, select **Configuration and Policies**.</span></span>

    ![組態和原則](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. <span data-ttu-id="9fbb2-138">從 [組態和原則] 設定清單中，選取 [儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-138">From the **Configuration and Policies** settings list, select **Repositories**.</span></span> <span data-ttu-id="9fbb2-139">[儲存機制] 刀鋒視窗會列出已新增至實驗室的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-139">The **Repositories** blade lists the repositories that have been added to the lab.</span></span> <span data-ttu-id="9fbb2-140">會為所有實驗室自動產生名為 `Public Repo` 的儲存機制，並連接到 [DevTest Labs GitHub 儲存機制](https://github.com/Azure/azure-devtestlab)，其中包含數個 VM 構件供您使用。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-140">A repository named `Public Repo` is automatically generated for all labs, and connects to the [DevTest Labs GitHub repo](https://github.com/Azure/azure-devtestlab) that contains several VM artifacts for your use.</span></span>

    ![公用儲存機制](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. <span data-ttu-id="9fbb2-142">選取 [新增 +] 以新增您的 Azure Resource Manager 範本儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-142">Select **Add+** to add your Azure Resource Manager template repository.</span></span>
1. <span data-ttu-id="9fbb2-143">當第二個 [儲存機制] 刀鋒視窗開啟時，輸入必要資訊，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9fbb2-143">When the second **Repositories** blade opens, enter the necessary information as follows:</span></span>
    - <span data-ttu-id="9fbb2-144">**名稱** - 輸入在實驗室中使用的儲存機制名稱。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-144">**Name** - Enter the repository name that is used in the lab.</span></span>
    - <span data-ttu-id="9fbb2-145">**Git 複製 URL** - 輸入來自 GitHub 或 Visual Studio Team Services 的 Git HTTPS 複製 URL。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-145">**Git clone URL** - Enter the GIT HTTPS clone URL from GitHub or Visual Studio Team Services.</span></span>  
    - <span data-ttu-id="9fbb2-146">**分支** - 輸入分支的名稱，以存取您的 Azure Resource Manager 範本定義。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-146">**Branch** - Enter the branch name to access your Azure Resource Manager template definitions.</span></span> 
    - <span data-ttu-id="9fbb2-147">**個人的存取權杖** - 個人的存取權杖用來安全地存取您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-147">**Personal access token** - The personal access token is used to securely access your repository.</span></span> <span data-ttu-id="9fbb2-148">若要從 Visual Studio Team Services 取得您的權杖，請選取 [YourName > > 我的設定檔 > 安全性 > 公用存取權杖]**&lt;**。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-148">To get your token from Visual Studio Team Services, select **&lt;YourName> > My profile > Security > Public access token**.</span></span> <span data-ttu-id="9fbb2-149">若要從 GitHub 取得權杖，請選取 avatar 然後選取 [設定 > 公用存取權杖]。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-149">To get your token from GitHub, select your avatar followed by selecting **Settings > Public access token**.</span></span> 
    - <span data-ttu-id="9fbb2-150">**資料夾路徑** - 使用兩個輸入欄位其中之一、輸入資料夾路徑，其開頭為正斜線 - / - 且與 Git 複製 URI 相關，至構件定義 (第一個輸入欄位) 或您的 Azure Resource Manager 範本定義。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-150">**Folder paths** - Using one of the two input fields, enter the folder path that starts with a forward slash - / - and is relative to your Git clone URI to either your artifact definitions (first input field) or your Azure Resource Manager template definitions.</span></span>   
    
        ![公用儲存機制](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. <span data-ttu-id="9fbb2-152">一旦輸入所有必要的欄位並通過驗證後，請選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-152">Once all the required fields are entered and pass the validation, select **Save**.</span></span>

<span data-ttu-id="9fbb2-153">下一節將引導您從 Azure Resource Manager 範本建立環境。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-153">The next section will walk you through creating environments from an Azure Resource Manager template.</span></span>

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a><span data-ttu-id="9fbb2-154">從 Azure Resource Manager 範本建立環境</span><span class="sxs-lookup"><span data-stu-id="9fbb2-154">Create an environment from an Azure Resource Manager template</span></span>

<span data-ttu-id="9fbb2-155">一旦在實驗室中設定 Azure Resource Manager 範本儲存機制之後，您實驗室的使用者可以使用 Azure 入口網站以下列步驟建立環境︰</span><span class="sxs-lookup"><span data-stu-id="9fbb2-155">Once an Azure Resource Manager template repository has been configured in the lab, your lab users can create an environment using Azure portal with the following steps:</span></span>

1. <span data-ttu-id="9fbb2-156">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-156">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="9fbb2-157">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-157">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="9fbb2-158">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-158">From the list of labs, select the desired lab.</span></span>   
1. <span data-ttu-id="9fbb2-159">在實驗室的刀鋒視窗上，選取 [新增+]**Add+**。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-159">On the lab's blade, select **Add+**.</span></span>
1. <span data-ttu-id="9fbb2-160">[選擇基底] 刀鋒視窗會顯示您可以與先列出的 Azure Resource Manager 範本搭配使用的基本映像。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-160">The **Choose a base** blade displays the base images you can use with the Azure Resource Manager templates listed first.</span></span> <span data-ttu-id="9fbb2-161">選取所需的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-161">Select the desired Azure Resource Manager template.</span></span>

    ![選擇基底](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. <span data-ttu-id="9fbb2-163">在 [新增] 刀鋒視窗中，輸入**環境名稱**值。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-163">On the **Add** blade, enter the **Environment name** value.</span></span> <span data-ttu-id="9fbb2-164">環境名稱是實驗室中向您使用者顯示的內容。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-164">The environment name is what is displayed to your users in the lab.</span></span> <span data-ttu-id="9fbb2-165">會在 Azure Resource Manager 範本中定義其餘的輸入欄位。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-165">The remaining input fields are defined in the Azure Resource Manager template.</span></span> <span data-ttu-id="9fbb2-166">如果在範本中定義預設值或 `azuredeploy.parameter.json` 檔案存在，則預設值會顯示在這些輸入欄位中。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-166">If default values are defined in the template or the `azuredeploy.parameter.json` file is present, default values are displayed in those input fields.</span></span> <span data-ttu-id="9fbb2-167">針對安全字串類型的參數，您可以使用儲存在實驗室中的[個人密碼存放區](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)的密碼。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-167">For parameters of type *secure string*, you can use the secrets stored in the lab’s [personal secret store](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).</span></span>

    ![新增刀鋒視窗](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > <span data-ttu-id="9fbb2-169">有幾個參數值 (即使指定) 會顯示為空值。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-169">There are several parameter values that - even if specified - are displayed as empty values.</span></span> <span data-ttu-id="9fbb2-170">因此，如果使用者將這些值指派給 Azure Resource Manager 範本中的參數，DevTest Labs 不會顯示值；而是顯示空白的輸入欄位，當中實驗室使用者需在建立環境時輸入值。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-170">Therefore, if users assign those values to parameters in an Azure Resource Manager template, DevTest Labs does not display the values; instead showing blank input fields where the lab users need to enter a value when creating the environment.</span></span>
    > 
    > - <span data-ttu-id="9fbb2-171">GEN-UNIQUE</span><span class="sxs-lookup"><span data-stu-id="9fbb2-171">GEN-UNIQUE</span></span>
    > - <span data-ttu-id="9fbb2-172">GEN-UNIQUE-[N]</span><span class="sxs-lookup"><span data-stu-id="9fbb2-172">GEN-UNIQUE-[N]</span></span>
    > - <span data-ttu-id="9fbb2-173">GEN-SSH-PUB-KEY</span><span class="sxs-lookup"><span data-stu-id="9fbb2-173">GEN-SSH-PUB-KEY</span></span>
    > - <span data-ttu-id="9fbb2-174">GEN-PASSWORD</span><span class="sxs-lookup"><span data-stu-id="9fbb2-174">GEN-PASSWORD</span></span> 
 
1. <span data-ttu-id="9fbb2-175">選取 [新增] 以建立環境。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-175">Select **Add** to create the environment.</span></span> <span data-ttu-id="9fbb2-176">環境會立即啟動佈建，並在**我的虛擬機器**清單中有狀態顯示。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-176">The environment starts provisioning immediately with the status displaying in the **My virtual machines** list.</span></span> <span data-ttu-id="9fbb2-177">實驗室會自動建立新的資源群組，以佈建 Azure Resource Manager 範本中定義的所有資源。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-177">A new resource group is automatically created by the lab to provision all the resources defined in the Azure Resource Manager template.</span></span>
1. <span data-ttu-id="9fbb2-178">建立環境之後，請在 [我的虛擬機器] 清單中選取環境，以開啟資源群組刀鋒視窗並瀏覽環境中佈建的所有資源。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-178">Once the environment is created, select the environment in the **My virtual machines** list to open the resource group blade and browse all of the resources provisioned in the environment.</span></span>
    
    ![我的虛擬機器清單](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   <span data-ttu-id="9fbb2-180">您也可以展開環境，只檢視環境中所佈建的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-180">You can also expand the environment to view just the list of VMs that are provisioned in the environment.</span></span>
    
    ![我的虛擬機器清單](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. <span data-ttu-id="9fbb2-182">按一下任何環境，以檢視可用的動作 - 例如套用構件、加入資料磁碟、變更自動關機時間等等。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-182">Click any of the environments to view the available actions - such as applying artifacts, attaching data disks, changing auto-shutdown time, and more.</span></span>

    ![環境動作](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a><span data-ttu-id="9fbb2-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9fbb2-184">Next steps</span></span>
* <span data-ttu-id="9fbb2-185">一旦建立 VM 之後，您可以選取 VM 刀鋒視窗上的 [連接] 來連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-185">Once a VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="9fbb2-186">在實驗室的 [我的虛擬機器] 清單中選取環境，以檢視和管理環境中的資源。</span><span class="sxs-lookup"><span data-stu-id="9fbb2-186">View and manage resources in an environment by selecting the environment in the **My virtual machines** list in your lab.</span></span> 
* <span data-ttu-id="9fbb2-187">瀏覽 [Azure 快速入門範本庫中的 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates)</span><span class="sxs-lookup"><span data-stu-id="9fbb2-187">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates)</span></span>
