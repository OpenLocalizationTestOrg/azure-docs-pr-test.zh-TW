---
title: "aaaCreate 環境多部 VM 和 PaaS 具有 Azure 資源管理員範本 |Microsoft 文件"
description: "深入了解如何 toocreate 多部 VM 的環境和 Azure Resource Manager 範本從 Azure DevTest Labs PaaS 資源"
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
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a><span data-ttu-id="4c75c-103">使用 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源</span><span class="sxs-lookup"><span data-stu-id="4c75c-103">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>

<span data-ttu-id="4c75c-104">hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)可讓您 tooeasily[建立並加入 VM tooa 實驗室](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm)。</span><span class="sxs-lookup"><span data-stu-id="4c75c-104">hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) enables you tooeasily [create and add a VM tooa lab](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm).</span></span> <span data-ttu-id="4c75c-105">這適用於一次建立一個 VM。</span><span class="sxs-lookup"><span data-stu-id="4c75c-105">This works well for creating one VM at a time.</span></span> <span data-ttu-id="4c75c-106">不過，如果 hello 環境包含多個 Vm，每個 VM 有 toobe 分別建立。</span><span class="sxs-lookup"><span data-stu-id="4c75c-106">However, if hello environment contains multiple VMs, each VM has toobe individually created.</span></span> <span data-ttu-id="4c75c-107">例如多層式 Web 應用程式或 SharePoint 伺服器陣列的情況下，一種機制是需要的 tooallow hello 建立在單一步驟中的多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="4c75c-107">For scenarios such as a multi-tier Web app or a SharePoint farm, a mechanism is needed tooallow for hello creation of multiple VMs in a single step.</span></span> <span data-ttu-id="4c75c-108">藉由使用 Azure 資源管理員範本，您可以現在定義 hello 基礎結構和 Azure 方案的組態，並重複地部署多個 Vm 一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="4c75c-108">By using Azure Resource Manager templates, you can now define hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple VMs in a consistent state.</span></span> <span data-ttu-id="4c75c-109">這項功能提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="4c75c-109">This feature provides hello following benefits:</span></span>

- <span data-ttu-id="4c75c-110">Azure Resource Manager 範本會直接從您的原始檔控制儲存機制 (GitHub 或 Team Services Git) 載入。</span><span class="sxs-lookup"><span data-stu-id="4c75c-110">Azure Resource Manager templates are loaded directly from your source control repository (GitHub or Team Services Git).</span></span>
- <span data-ttu-id="4c75c-111">您的使用者設定之後，才能挑選從 hello 做為其功能與其他類型的 Azure 入口網站的 Azure Resource Manager 範本來建立環境[VM 基底](./devtest-lab-comparing-vm-base-image-types.md)。</span><span class="sxs-lookup"><span data-stu-id="4c75c-111">Once configured, your users can create an environment by picking an Azure Resource Manager template from hello Azure portal as what they can do with other types of [VM bases](./devtest-lab-comparing-vm-base-image-types.md).</span></span>
- <span data-ttu-id="4c75c-112">可以從 Azure Resource Manager 範本加法 tooIaaS Vm 中的環境中佈建 azure PaaS 資源。</span><span class="sxs-lookup"><span data-stu-id="4c75c-112">Azure PaaS resources can be provisioned in an environment from an Azure Resource Manager template in addition tooIaaS VMs.</span></span>
- <span data-ttu-id="4c75c-113">加法 tooindividual Vm 建立其他類型的基底中的 hello 實驗室中可追蹤環境的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="4c75c-113">hello cost of environments can be tracked in hello lab in addition tooindividual VMs created by other types of bases.</span></span>
- <span data-ttu-id="4c75c-114">PaaS 資源所建立，而且會出現在成本追蹤。不過，VM 自動關機不適用 tooPaaS 資源。</span><span class="sxs-lookup"><span data-stu-id="4c75c-114">PaaS resources are created and will appear in cost tracking; however, VM auto shutdown does not apply tooPaaS resources.</span></span>
- <span data-ttu-id="4c75c-115">使用者擁有 hello 相同 VM 原則控制的環境，因為它們已用於單一實驗室 Vm。</span><span class="sxs-lookup"><span data-stu-id="4c75c-115">Users have hello same VM policy control for environments as they have for single-lab VMs.</span></span>

<span data-ttu-id="4c75c-116">深入了解 hello 許多[使用資源管理員範本的優點](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager)toodeploy、 更新或刪除所有實驗室資源在單一作業中。</span><span class="sxs-lookup"><span data-stu-id="4c75c-116">Learn more about hello many [benefits of using Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, update, or delete all of your lab resources in a single operation.</span></span>

> [!NOTE]
> <span data-ttu-id="4c75c-117">當您使用資源管理員範本為基礎 toocreate 多個實驗室 Vm 時，有一些差異 tookeep 記住是否建立多個 Vm 或單一 Vm。</span><span class="sxs-lookup"><span data-stu-id="4c75c-117">When you use a Resource Manager template as a basis toocreate more lab VMs, there are some differences tookeep in mind whether you are creating Multi-VMs or single-VMs.</span></span> <span data-ttu-id="4c75c-118">使用虛擬機器的 Azure Resource Manager 範本會更詳細地說明這些差異。</span><span class="sxs-lookup"><span data-stu-id="4c75c-118">Use a virtual machine's Azure Resource Manager template explains these differences in greater detail.</span></span>
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a><span data-ttu-id="4c75c-119">設定 Azure Resource Manager 範本儲存機制</span><span class="sxs-lookup"><span data-stu-id="4c75c-119">Configure Azure Resource Manager template repositories</span></span>

<span data-ttu-id="4c75c-120">做為其中一個 hello 有基礎結構做為程式碼和組態與程式碼，環境範本的最佳作法應管理原始檔控制中。</span><span class="sxs-lookup"><span data-stu-id="4c75c-120">As one of hello best practices with infrastructure-as-code and configuration-as-code, environment templates should be managed in source control.</span></span> <span data-ttu-id="4c75c-121">Azure DevTest Labs 採用這種作法，並直接從您的 GitHub 或 VSTS Git 儲存機制載入所有 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c75c-121">Azure DevTest Labs follows this practice and loads all Azure Resource Manager templates directly from your GitHub or VSTS Git repositories.</span></span> <span data-ttu-id="4c75c-122">如此一來，資源管理員範本可跨 hello 整個發行週期，從 hello 測試 toohello 生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c75c-122">As a result, Resource Manager templates can be used across hello entire release cycle, from hello test environment toohello production environment.</span></span>

<span data-ttu-id="4c75c-123">有幾個規則 toofollow tooorganize Azure 資源管理員範本放在儲存機制：</span><span class="sxs-lookup"><span data-stu-id="4c75c-123">There are a couple of rules toofollow tooorganize your Azure Resource Manager templates in a repository:</span></span>

- <span data-ttu-id="4c75c-124">hello 主要範本檔案必須命名為`azuredeploy.json`。</span><span class="sxs-lookup"><span data-stu-id="4c75c-124">hello master template file must be named `azuredeploy.json`.</span></span> 

    ![金鑰 Azure Resource Manager 範本檔案](./media/devtest-lab-create-environment-from-arm/master-template.png)

- <span data-ttu-id="4c75c-126">如果您想 toouse 參數檔案中定義的參數值時，必須為 hello 參數檔案`azuredeploy.parameters.json`。</span><span class="sxs-lookup"><span data-stu-id="4c75c-126">If you want toouse parameter values defined in a parameter file, hello parameter file must be named `azuredeploy.parameters.json`.</span></span>
- <span data-ttu-id="4c75c-127">您可以使用 hello 參數`_artifactsLocation`和`_artifactsLocationSasToken`tooconstruct hello parametersLink URI 值，允許 DevTest Labs tooautomatically 管理巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="4c75c-127">You can use hello parameters `_artifactsLocation` and `_artifactsLocationSasToken` tooconstruct hello parametersLink URI value, allowing DevTest Labs tooautomatically manage nested templates.</span></span> <span data-ttu-id="4c75c-128">如需詳細資訊，請參閱 [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) (Azure DevTest Labs 如何簡化測試環境的巢狀 Resource Manager 範本部署)。</span><span class="sxs-lookup"><span data-stu-id="4c75c-128">See [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) for more information.</span></span>
- <span data-ttu-id="4c75c-129">中繼資料可以是定義的 toospecify hello 範本顯示名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="4c75c-129">Metadata can be defined toospecify hello template display name and description.</span></span> <span data-ttu-id="4c75c-130">此中繼資料必須在名為 `metadata.json` 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="4c75c-130">This metadata must be in a file named `metadata.json`.</span></span> <span data-ttu-id="4c75c-131">hello 下列中繼資料檔範例將示範如何 toospecify hello 顯示名稱和描述：</span><span class="sxs-lookup"><span data-stu-id="4c75c-131">hello following example metadata file illustrates how toospecify hello display name and description:</span></span> 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

<span data-ttu-id="4c75c-132">hello 下列步驟將引導您透過加入使用 hello Azure 入口網站的儲存機制 tooyour 實驗室。</span><span class="sxs-lookup"><span data-stu-id="4c75c-132">hello following steps guide you through adding a repository tooyour lab using hello Azure portal.</span></span> 

1. <span data-ttu-id="4c75c-133">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="4c75c-133">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4c75c-134">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="4c75c-134">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="4c75c-135">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="4c75c-135">From hello list of labs, select hello desired lab.</span></span>   
1. <span data-ttu-id="4c75c-136">在 hello 實驗室刀鋒視窗中，選取 **組態和原則**。</span><span class="sxs-lookup"><span data-stu-id="4c75c-136">On hello lab's blade, select **Configuration and Policies**.</span></span>

    ![組態和原則](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. <span data-ttu-id="4c75c-138">從 hello**組態和原則**設定清單中，選取**儲存機制**。</span><span class="sxs-lookup"><span data-stu-id="4c75c-138">From hello **Configuration and Policies** settings list, select **Repositories**.</span></span> <span data-ttu-id="4c75c-139">hello**儲存機制**刀鋒視窗會列出已加入 toohello 實驗室 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4c75c-139">hello **Repositories** blade lists hello repositories that have been added toohello lab.</span></span> <span data-ttu-id="4c75c-140">名為儲存機制`Public Repo`會自動產生的所有實驗室，並連接 toohello [DevTest Labs GitHub 儲存機制](https://github.com/Azure/azure-devtestlab)，其中包含您可以使用數個 VM 成品。</span><span class="sxs-lookup"><span data-stu-id="4c75c-140">A repository named `Public Repo` is automatically generated for all labs, and connects toohello [DevTest Labs GitHub repo](https://github.com/Azure/azure-devtestlab) that contains several VM artifacts for your use.</span></span>

    ![公用儲存機制](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. <span data-ttu-id="4c75c-142">選取**新增 +** tooadd 您的 Azure Resource Manager 範本儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4c75c-142">Select **Add+** tooadd your Azure Resource Manager template repository.</span></span>
1. <span data-ttu-id="4c75c-143">當第二個 hello**儲存機制**刀鋒視窗隨即開啟，輸入 hello 的必要資訊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4c75c-143">When hello second **Repositories** blade opens, enter hello necessary information as follows:</span></span>
    - <span data-ttu-id="4c75c-144">**名稱**-輸入 hello 實驗室中的 hello 用的儲存機制名稱。</span><span class="sxs-lookup"><span data-stu-id="4c75c-144">**Name** - Enter hello repository name that is used in hello lab.</span></span>
    - <span data-ttu-id="4c75c-145">**Git 複製 URL** -從 GitHub 或 Visual Studio Team Services 輸入 hello GIT HTTPS 複製 URL。</span><span class="sxs-lookup"><span data-stu-id="4c75c-145">**Git clone URL** - Enter hello GIT HTTPS clone URL from GitHub or Visual Studio Team Services.</span></span>  
    - <span data-ttu-id="4c75c-146">**分支**-輸入 hello 分支名稱 tooaccess 您的 Azure Resource Manager 範本定義。</span><span class="sxs-lookup"><span data-stu-id="4c75c-146">**Branch** - Enter hello branch name tooaccess your Azure Resource Manager template definitions.</span></span> 
    - <span data-ttu-id="4c75c-147">**個人存取權杖**-hello 個人存取權杖用 toosecurely 存取您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4c75c-147">**Personal access token** - hello personal access token is used toosecurely access your repository.</span></span> <span data-ttu-id="4c75c-148">您的權杖，從 Visual Studio Team Services 中，選取 tooget  **&lt;YourName >> 我的設定檔 > 安全性 > 公用存取語彙基元**。</span><span class="sxs-lookup"><span data-stu-id="4c75c-148">tooget your token from Visual Studio Team Services, select **&lt;YourName> > My profile > Security > Public access token**.</span></span> <span data-ttu-id="4c75c-149">tooget 您的權杖從 GitHub，選取您的顯示圖片後面接著選取**設定 > 公用存取語彙基元**。</span><span class="sxs-lookup"><span data-stu-id="4c75c-149">tooget your token from GitHub, select your avatar followed by selecting **Settings > Public access token**.</span></span> 
    - <span data-ttu-id="4c75c-150">**資料夾路徑**-使用其中一種 hello 兩個輸入欄位，輸入 hello 的資料夾路徑開頭是正斜線-/-且相對 tooyour Git 複製 URI tooeither 成品定義 （第一個輸入的欄位） 或您的 Azure Resource Manager 範本定義。</span><span class="sxs-lookup"><span data-stu-id="4c75c-150">**Folder paths** - Using one of hello two input fields, enter hello folder path that starts with a forward slash - / - and is relative tooyour Git clone URI tooeither your artifact definitions (first input field) or your Azure Resource Manager template definitions.</span></span>   
    
        ![公用儲存機制](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. <span data-ttu-id="4c75c-152">Hello 所需的所有欄位輸入，並傳遞 hello 驗證，請選取**儲存**。</span><span class="sxs-lookup"><span data-stu-id="4c75c-152">Once all hello required fields are entered and pass hello validation, select **Save**.</span></span>

<span data-ttu-id="4c75c-153">hello 下一節將引導您完成從 Azure Resource Manager 範本建立環境。</span><span class="sxs-lookup"><span data-stu-id="4c75c-153">hello next section will walk you through creating environments from an Azure Resource Manager template.</span></span>

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a><span data-ttu-id="4c75c-154">從 Azure Resource Manager 範本建立環境</span><span class="sxs-lookup"><span data-stu-id="4c75c-154">Create an environment from an Azure Resource Manager template</span></span>

<span data-ttu-id="4c75c-155">Hello 實驗室中設定的 Azure Resource Manager 範本存放庫之後, 您的實驗室使用者可以建立 hello 步驟搭配使用 Azure 入口網站的環境：</span><span class="sxs-lookup"><span data-stu-id="4c75c-155">Once an Azure Resource Manager template repository has been configured in hello lab, your lab users can create an environment using Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="4c75c-156">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="4c75c-156">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="4c75c-157">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="4c75c-157">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="4c75c-158">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="4c75c-158">From hello list of labs, select hello desired lab.</span></span>   
1. <span data-ttu-id="4c75c-159">在 hello 實驗室刀鋒視窗中，選取 **新增 +**。</span><span class="sxs-lookup"><span data-stu-id="4c75c-159">On hello lab's blade, select **Add+**.</span></span>
1. <span data-ttu-id="4c75c-160">hello**選擇基底**刀鋒視窗會顯示 hello 基底映像，您可以使用列於首位的 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c75c-160">hello **Choose a base** blade displays hello base images you can use with hello Azure Resource Manager templates listed first.</span></span> <span data-ttu-id="4c75c-161">選取 hello 所需的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c75c-161">Select hello desired Azure Resource Manager template.</span></span>

    ![選擇基底](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. <span data-ttu-id="4c75c-163">在 hello**新增**刀鋒視窗中，輸入 hello**環境名稱**值。</span><span class="sxs-lookup"><span data-stu-id="4c75c-163">On hello **Add** blade, enter hello **Environment name** value.</span></span> <span data-ttu-id="4c75c-164">hello 環境名稱是會顯示的 tooyour hello 實驗室中的使用者。</span><span class="sxs-lookup"><span data-stu-id="4c75c-164">hello environment name is what is displayed tooyour users in hello lab.</span></span> <span data-ttu-id="4c75c-165">hello 其餘的輸入的欄位會定義在 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="4c75c-165">hello remaining input fields are defined in hello Azure Resource Manager template.</span></span> <span data-ttu-id="4c75c-166">如果預設值會定義在 hello 範本或 hello`azuredeploy.parameter.json`檔案是否存在，預設值都會顯示在這些輸入欄位中。</span><span class="sxs-lookup"><span data-stu-id="4c75c-166">If default values are defined in hello template or hello `azuredeploy.parameter.json` file is present, default values are displayed in those input fields.</span></span> <span data-ttu-id="4c75c-167">類型參數*安全字串*，您可以使用儲存在 hello 實驗室中的 hello 密碼[個人密碼存放區](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)。</span><span class="sxs-lookup"><span data-stu-id="4c75c-167">For parameters of type *secure string*, you can use hello secrets stored in hello lab’s [personal secret store](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).</span></span>

    ![新增刀鋒視窗](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > <span data-ttu-id="4c75c-169">有幾個參數值 (即使指定) 會顯示為空值。</span><span class="sxs-lookup"><span data-stu-id="4c75c-169">There are several parameter values that - even if specified - are displayed as empty values.</span></span> <span data-ttu-id="4c75c-170">因此，如果使用者指派 Azure Resource Manager 範本中的這些值 tooparameters，DevTest Labs 不會顯示 hello 值;改為顯示 hello 實驗室使用者必須 tooenter 空白輸入的欄位的值建立 hello 環境。</span><span class="sxs-lookup"><span data-stu-id="4c75c-170">Therefore, if users assign those values tooparameters in an Azure Resource Manager template, DevTest Labs does not display hello values; instead showing blank input fields where hello lab users need tooenter a value when creating hello environment.</span></span>
    > 
    > - <span data-ttu-id="4c75c-171">GEN-UNIQUE</span><span class="sxs-lookup"><span data-stu-id="4c75c-171">GEN-UNIQUE</span></span>
    > - <span data-ttu-id="4c75c-172">GEN-UNIQUE-[N]</span><span class="sxs-lookup"><span data-stu-id="4c75c-172">GEN-UNIQUE-[N]</span></span>
    > - <span data-ttu-id="4c75c-173">GEN-SSH-PUB-KEY</span><span class="sxs-lookup"><span data-stu-id="4c75c-173">GEN-SSH-PUB-KEY</span></span>
    > - <span data-ttu-id="4c75c-174">GEN-PASSWORD</span><span class="sxs-lookup"><span data-stu-id="4c75c-174">GEN-PASSWORD</span></span> 
 
1. <span data-ttu-id="4c75c-175">選取**新增**toocreate hello 環境。</span><span class="sxs-lookup"><span data-stu-id="4c75c-175">Select **Add** toocreate hello environment.</span></span> <span data-ttu-id="4c75c-176">hello 環境啟動佈建立即 hello 狀態顯示在 hello**我的虛擬機器**清單。</span><span class="sxs-lookup"><span data-stu-id="4c75c-176">hello environment starts provisioning immediately with hello status displaying in hello **My virtual machines** list.</span></span> <span data-ttu-id="4c75c-177">新的資源群組會自動建立 hello 實驗室 tooprovision hello Azure Resource Manager 範本中定義的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="4c75c-177">A new resource group is automatically created by hello lab tooprovision all hello resources defined in hello Azure Resource Manager template.</span></span>
1. <span data-ttu-id="4c75c-178">一旦建立 hello 環境時，選取 hello 環境中 hello**我的虛擬機器**清單 tooopen hello 資源群組 刀鋒視窗並瀏覽所有 hello hello 環境中，佈建的資源。</span><span class="sxs-lookup"><span data-stu-id="4c75c-178">Once hello environment is created, select hello environment in hello **My virtual machines** list tooopen hello resource group blade and browse all of hello resources provisioned in hello environment.</span></span>
    
    ![我的虛擬機器清單](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   <span data-ttu-id="4c75c-180">您也可以展開 Vm 佈建 hello 環境中的 hello 環境 tooview 只 hello 的清單。</span><span class="sxs-lookup"><span data-stu-id="4c75c-180">You can also expand hello environment tooview just hello list of VMs that are provisioned in hello environment.</span></span>
    
    ![我的虛擬機器清單](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. <span data-ttu-id="4c75c-182">按一下任何 hello 環境 tooview hello 可用的動作-例如套用成品，附加資料磁碟、 變更自動關機時間等等。</span><span class="sxs-lookup"><span data-stu-id="4c75c-182">Click any of hello environments tooview hello available actions - such as applying artifacts, attaching data disks, changing auto-shutdown time, and more.</span></span>

    ![環境動作](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a><span data-ttu-id="4c75c-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c75c-184">Next steps</span></span>
* <span data-ttu-id="4c75c-185">一旦建立 VM 之後，您可以藉由選取連接 toohello VM**連接**hello VM 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="4c75c-185">Once a VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="4c75c-186">檢視和管理的環境中的資源中 hello 選取 hello 環境**我的虛擬機器**實驗室中的清單。</span><span class="sxs-lookup"><span data-stu-id="4c75c-186">View and manage resources in an environment by selecting hello environment in hello **My virtual machines** list in your lab.</span></span> 
* <span data-ttu-id="4c75c-187">瀏覽 hello [Azure 資源管理員範本，從 Azure 快速入門範本庫](https://github.com/Azure/azure-quickstart-templates)</span><span class="sxs-lookup"><span data-stu-id="4c75c-187">Explore hello [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates)</span></span>
