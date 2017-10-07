---
title: "以 hello Azure CLI aaaManage 資源 |Microsoft 文件"
description: "使用 hello Azure 命令列介面 (CLI) toomanage Azure 資源和群組"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="3a92e-103">使用 hello Azure CLI toomanage Azure 資源與資源群組</span><span class="sxs-lookup"><span data-stu-id="3a92e-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a92e-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="3a92e-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="3a92e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3a92e-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="3a92e-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a92e-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="3a92e-107">REST API</span><span class="sxs-lookup"><span data-stu-id="3a92e-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="3a92e-108">hello Azure 命令列介面 (Azure CLI) 是其中一個的數個工具，您可以使用 toodeploy 和管理資源與資源管理員。</span><span class="sxs-lookup"><span data-stu-id="3a92e-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="3a92e-109">本文介紹常見方式 toomanage Azure 資源與資源群組使用 hello Azure CLI Resource Manager 模式中。</span><span class="sxs-lookup"><span data-stu-id="3a92e-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="3a92e-110">如需使用 hello CLI toodeploy 資源資訊，請參閱[部署資源，資源管理員範本與 Azure CLI](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="3a92e-111">如需 Azure 資源與資源管理員的背景，請瀏覽 hello [Azure 資源管理員概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3a92e-112">toomanage Azure hello Azure CLI 資源，您需要太[安裝 hello Azure CLI](../cli-install-nodejs.md)，和[登入 tooAzure](../xplat-cli-connect.md)使用 hello`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="3a92e-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="3a92e-113">請確定 hello CLI 處於 Resource Manager 模式 (執行`azure config mode arm`)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="3a92e-114">如果您已經完成這些工作，您已準備好 toogo。</span><span class="sxs-lookup"><span data-stu-id="3a92e-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="3a92e-115">取得資源群組和資源</span><span class="sxs-lookup"><span data-stu-id="3a92e-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="3a92e-116">資源群組</span><span class="sxs-lookup"><span data-stu-id="3a92e-116">Resource groups</span></span>
<span data-ttu-id="3a92e-117">tooget 一份您訂用帳戶和它們的位置中的所有資源群組執行此命令。</span><span class="sxs-lookup"><span data-stu-id="3a92e-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="3a92e-118">資源</span><span class="sxs-lookup"><span data-stu-id="3a92e-118">Resources</span></span>
 <span data-ttu-id="3a92e-119">toolist 群組，例如使用中的所有資源都名稱*testRG*，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3a92e-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="3a92e-120">tooview hello 群組，例如，名為的 VM 內的個別資源*MyUbuntuVM*，使用類似 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="3a92e-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="3a92e-121">請注意 hello **Microsoft.Compute/virtualMachines**參數。</span><span class="sxs-lookup"><span data-stu-id="3a92e-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="3a92e-122">這個參數會指出 hello hello 資源要求的資訊類型。</span><span class="sxs-lookup"><span data-stu-id="3a92e-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="3a92e-123">當使用 hello **azure 資源**hello 以外的命令**清單**命令時，您必須指定 hello 資源 hello API 版本以 hello **-o**參數。</span><span class="sxs-lookup"><span data-stu-id="3a92e-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="3a92e-124">如果您懷疑 hello API 版本，請參閱 hello 範本檔案，並找出 hello 資源的 hello api 版本欄位。</span><span class="sxs-lookup"><span data-stu-id="3a92e-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="3a92e-125">如需 Resource Manager 中的 API 版本詳細資訊，請參閱[資源提供者和類型](resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="3a92e-126">當資源上檢視詳細資料，通常會很有用的 toouse hello`--json`參數。</span><span class="sxs-lookup"><span data-stu-id="3a92e-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="3a92e-127">這個參數可讓 hello 輸出更容易閱讀，因為有些值會巢狀的結構或集合。</span><span class="sxs-lookup"><span data-stu-id="3a92e-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="3a92e-128">hello 下列範例示範傳回的 hello 結果的 hello**顯示**命令做為 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="3a92e-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="3a92e-129">如果您想要儲存使用 hello hello JSON 資料 toofile&gt;字元 toodirect hello 輸出 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="3a92e-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="3a92e-130">例如：</span><span class="sxs-lookup"><span data-stu-id="3a92e-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="3a92e-131">標記</span><span class="sxs-lookup"><span data-stu-id="3a92e-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="3a92e-132">管理資源</span><span class="sxs-lookup"><span data-stu-id="3a92e-132">Manage resources</span></span>
<span data-ttu-id="3a92e-133">tooadd 資源，例如儲存體帳戶 tooa 資源群組，執行如下命令：</span><span class="sxs-lookup"><span data-stu-id="3a92e-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="3a92e-134">此外 toospecifying hello API 版的 hello 資源以 hello **-o**參數、 使用 hello **-p**參數 toopass JSON 格式化字串的任何必要或其他屬性。</span><span class="sxs-lookup"><span data-stu-id="3a92e-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="3a92e-135">toodelete 現有的資源，例如虛擬機器資源使用 hello 下列類似的命令：</span><span class="sxs-lookup"><span data-stu-id="3a92e-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="3a92e-136">toomove 現有資源 tooanother 資源群組或訂用帳戶，使用 hello **azure 資源移動**命令。</span><span class="sxs-lookup"><span data-stu-id="3a92e-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="3a92e-137">下列範例會示範如何 hello toomove Redis 快取 tooa 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3a92e-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="3a92e-138">在 hello **-i**參數，提供以逗號分隔的 toomove hello 資源識別碼的清單。</span><span class="sxs-lookup"><span data-stu-id="3a92e-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="3a92e-139">控制存取 tooresources</span><span class="sxs-lookup"><span data-stu-id="3a92e-139">Control access tooresources</span></span>
<span data-ttu-id="3a92e-140">您可以使用 hello Azure CLI toocreate 和管理原則 toocontrol 存取 tooAzure 資源。</span><span class="sxs-lookup"><span data-stu-id="3a92e-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="3a92e-141">如需原則定義和指派原則 tooresources 背景，請參閱[原則 toomanage 資源及控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="3a92e-142">例如，定義下列原則 toodeny hello 其中位置不是美國西部或美國中北部，所有要求，並將它儲存 toohello 原則定義檔案 policy.json:</span><span class="sxs-lookup"><span data-stu-id="3a92e-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="3a92e-143">然後執行 hello**原則定義建立**命令：</span><span class="sxs-lookup"><span data-stu-id="3a92e-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="3a92e-144">此命令會顯示類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3a92e-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="3a92e-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="3a92e-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="3a92e-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="3a92e-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="3a92e-147">tooassign hello 範圍要請使用 hello 原則**PolicyDefinitionId** hello 前一個命令所傳回。</span><span class="sxs-lookup"><span data-stu-id="3a92e-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="3a92e-148">在下列範例的 hello，此範圍是 hello 訂閱，但您可以為範圍 tooresource 群組或個別的資源：</span><span class="sxs-lookup"><span data-stu-id="3a92e-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="3a92e-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="3a92e-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="3a92e-150">您可以取得、 變更或移除原則定義使用 hello**原則定義顯示**，**原則定義集中**，和**原則定義刪除**命令。</span><span class="sxs-lookup"><span data-stu-id="3a92e-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="3a92e-151">同樣地，您可以取得、 變更或移除原則指派使用 hello**原則指派顯示**，**原則指派集中**，和**原則指派刪除**命令.</span><span class="sxs-lookup"><span data-stu-id="3a92e-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="3a92e-152">匯出資源群組作為範本</span><span class="sxs-lookup"><span data-stu-id="3a92e-152">Export a resource group as a template</span></span>
<span data-ttu-id="3a92e-153">為現有的資源群組，您可以檢視 hello 資源群組的 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="3a92e-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="3a92e-154">匯出的 hello 範本提供兩個優點：</span><span class="sxs-lookup"><span data-stu-id="3a92e-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="3a92e-155">您可以輕鬆地自動化未來 hello 方案的部署，因為 hello 範本中定義所有 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3a92e-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="3a92e-156">您先熟悉樣板語法藉由查看 hello JSON 表示您的方案。</span><span class="sxs-lookup"><span data-stu-id="3a92e-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="3a92e-157">使用 Azure CLI hello，您可以匯出範本代表 hello 的目前狀態的資源群組，或下載用於特定部署的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3a92e-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="3a92e-158">**匯出的資源群組的 hello 範本**-當您所做的變更 tooa 資源群組，而需要 tooretrieve hello JSON 字串表示的目前狀態，這會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="3a92e-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="3a92e-159">不過，hello 產生的範本包含最少的參數和任何變數。</span><span class="sxs-lookup"><span data-stu-id="3a92e-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="3a92e-160">大多數 hello 範本中的 hello 值是硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="3a92e-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="3a92e-161">在部署之前產生的 hello 範本，您可能希望 tooconvert hello 值的多個參數中，因此您可以自訂的不同環境的 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="3a92e-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="3a92e-162">資源群組 tooa 本機目錄，執行 hello tooexport hello 範本`azure group export`命令 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="3a92e-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="3a92e-163">(取代適用於您作業系統環境的本機目錄。)</span><span class="sxs-lookup"><span data-stu-id="3a92e-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="3a92e-164">**下載特定部署的 hello 範本**-當您需要 tooview hello 實際範本已使用的 toodeploy 資源時，這是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="3a92e-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="3a92e-165">hello 範本包含所有參數和 hello 原始部署中所定義的變數。</span><span class="sxs-lookup"><span data-stu-id="3a92e-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="3a92e-166">不過，如果您組織中有人 hello 範本中進行變更 toohello 資源群組 hello 定義之外，此範本不代表 hello hello 資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="3a92e-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="3a92e-167">使用特定部署 tooa 本機目錄中，執行 hello toodownload hello 樣板`azure group deployment template download`命令。</span><span class="sxs-lookup"><span data-stu-id="3a92e-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="3a92e-168">例如：</span><span class="sxs-lookup"><span data-stu-id="3a92e-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="3a92e-169">範本匯出處於預覽狀態，並非所有的資源類型目前都支援匯出範本。</span><span class="sxs-lookup"><span data-stu-id="3a92e-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="3a92e-170">當嘗試 tooexport 範本，可能會看到錯誤指出未匯出一些資源。</span><span class="sxs-lookup"><span data-stu-id="3a92e-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="3a92e-171">如有需要，下載範本之後，在範本中手動定義這些資源。</span><span class="sxs-lookup"><span data-stu-id="3a92e-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3a92e-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a92e-172">Next steps</span></span>
* <span data-ttu-id="3a92e-173">部署作業的 tooget 詳細資料和疑難排解部署錯誤，以 hello Azure CLI，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="3a92e-174">如果您想 toouse hello CLI tooset 應用程式或指令碼 tooaccess 資源，請參閱[使用 Azure CLI toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="3a92e-175">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="3a92e-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

