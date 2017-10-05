---
title: "使用 Azure CLI 管理資源 | Microsoft Docs"
description: "使用 Azure 命令列介面 (CLI) 來管理 Azure 資源和群組"
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
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="c3721-103">使用 Azure CLI 管理 Azure 資源和資源群組</span><span class="sxs-lookup"><span data-stu-id="c3721-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3721-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="c3721-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="c3721-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c3721-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="c3721-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3721-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="c3721-107">REST API</span><span class="sxs-lookup"><span data-stu-id="c3721-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="c3721-108">Azure 命令列介面 (Azure CLI) 是您可以使用 Resource Manager 來部署和管理資源的其中一個工具。</span><span class="sxs-lookup"><span data-stu-id="c3721-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="c3721-109">本文將介紹以 Resource Manager 模式使用 Azure CLI 來管理 Azure 資源和資源群組的常見方式。</span><span class="sxs-lookup"><span data-stu-id="c3721-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="c3721-110">如需使用 CLI 來部署資源的相關資訊，請參閱[使用 Resource Manager 範本與 Azure CLI 部署資源](resource-group-template-deploy-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="c3721-111">如需 Azure 資源和 Resource Manager 的背景，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c3721-112">若要以 Azure CLI 管理 Azure 資源，您需要[安裝 Azure CLI](../cli-install-nodejs.md) 並使用 `azure login` 命令[登入 Azure](../xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="c3721-113">請確定 CLI 是處於 Resource Manager 模式 (執行 `azure config mode arm`)。</span><span class="sxs-lookup"><span data-stu-id="c3721-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="c3721-114">如果上述事項都已完成，您就能開始進行了。</span><span class="sxs-lookup"><span data-stu-id="c3721-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="c3721-115">取得資源群組和資源</span><span class="sxs-lookup"><span data-stu-id="c3721-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="c3721-116">資源群組</span><span class="sxs-lookup"><span data-stu-id="c3721-116">Resource groups</span></span>
<span data-ttu-id="c3721-117">若要取得您的訂用帳戶中所有資源群組及其位置的清單，請執行此命令。</span><span class="sxs-lookup"><span data-stu-id="c3721-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="c3721-118">資源</span><span class="sxs-lookup"><span data-stu-id="c3721-118">Resources</span></span>
 <span data-ttu-id="c3721-119">若要列出群組中的所有資源 (例如具有名稱 *testRG* 的資源)，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="c3721-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="c3721-120">若要檢視群組內的個別資源 (例如名為 *MyUbuntuVM* 的 VM)，請使用如下所示的命令：</span><span class="sxs-lookup"><span data-stu-id="c3721-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="c3721-121">請注意 **Microsoft.Compute/virtualMachines** 參數。</span><span class="sxs-lookup"><span data-stu-id="c3721-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="c3721-122">此參數表示您正在要求哪類資源的資訊。</span><span class="sxs-lookup"><span data-stu-id="c3721-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="c3721-123">使用 **list** 命令以外的 **azure resource** 命令時，必須以**-o** 參數指定資源的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="c3721-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="c3721-124">如果不確定要使用的 API 版本，請咨詢範本檔案並尋找資源的 apiVersion 欄位。</span><span class="sxs-lookup"><span data-stu-id="c3721-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="c3721-125">如需 Resource Manager 中的 API 版本詳細資訊，請參閱[資源提供者和類型](resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="c3721-126">檢視資源的詳細資料時，建議使用 `--json` 參數，更加實用。</span><span class="sxs-lookup"><span data-stu-id="c3721-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="c3721-127">這個參數可讓輸出更容易閱讀，因為部分值是巢狀的結構或集合。</span><span class="sxs-lookup"><span data-stu-id="c3721-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="c3721-128">下列範例示範如何以 JSON 文件傳回 **show** 命令的結果。</span><span class="sxs-lookup"><span data-stu-id="c3721-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="c3721-129">若您希望，可以使用 &gt; 字元將輸出導向檔案，藉此將 JSON 資料儲存至檔案。</span><span class="sxs-lookup"><span data-stu-id="c3721-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="c3721-130">例如：</span><span class="sxs-lookup"><span data-stu-id="c3721-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="c3721-131">標記</span><span class="sxs-lookup"><span data-stu-id="c3721-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="c3721-132">管理資源</span><span class="sxs-lookup"><span data-stu-id="c3721-132">Manage resources</span></span>
<span data-ttu-id="c3721-133">若要將例如儲存體帳戶的資源新增至資源群組，請執行類似下列的命令︰</span><span class="sxs-lookup"><span data-stu-id="c3721-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="c3721-134">除了以 **-o** 參數指定資源的 API 版本，請使用 **-p** 參數來傳遞任何具有必要或其他屬性的 JSON 格式字串。</span><span class="sxs-lookup"><span data-stu-id="c3721-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="c3721-135">若要刪除現有的資源 (例如虛擬機器資源)，請使用如下所示的命令：</span><span class="sxs-lookup"><span data-stu-id="c3721-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="c3721-136">若要將現有的資源移動到另一個資源群組或訂用帳戶，請使用 **azure resource move** 命令。</span><span class="sxs-lookup"><span data-stu-id="c3721-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="c3721-137">下列範例說明如何將 Redis 快取移動到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c3721-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="c3721-138">請在 **-i** 參數中，為要移動的資源識別碼提供以逗號分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="c3721-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="c3721-139">控制資源的存取</span><span class="sxs-lookup"><span data-stu-id="c3721-139">Control access to resources</span></span>
<span data-ttu-id="c3721-140">您可以使用 Azure CLI 來建立和管理原則，以控制 Azure 資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="c3721-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="c3721-141">如需原則定義和將原則指派給資源的背景，請參閱[使用原則來管理資源並控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="c3721-142">例如，定義下列的原則，以拒絕所有位置不在美國西部或美國中北部的要求，並將其儲存到原則定義檔案 policy.json：</span><span class="sxs-lookup"><span data-stu-id="c3721-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

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

<span data-ttu-id="c3721-143">然後執行 **policy definition create** 命令：</span><span class="sxs-lookup"><span data-stu-id="c3721-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="c3721-144">此命令會顯示如下輸出：</span><span class="sxs-lookup"><span data-stu-id="c3721-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="c3721-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="c3721-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="c3721-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="c3721-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="c3721-147">若要在您想要的範圍內指派原則，請使用從前一個命令傳回的 **PolicyDefinitionId**。</span><span class="sxs-lookup"><span data-stu-id="c3721-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="c3721-148">在下列範例中，此範圍是訂用帳戶，但您可以將範圍設為資源群組或個別資源︰</span><span class="sxs-lookup"><span data-stu-id="c3721-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="c3721-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="c3721-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="c3721-150">您可以使用 **policy definition show**、**policy definition set** 和 **policy definition delete** 命令來取得、變更或移除原則定義。</span><span class="sxs-lookup"><span data-stu-id="c3721-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="c3721-151">同樣地，您可以使用 **policy assignment show**、**policy assignment set** 和 **policy assignment delete** 命令來取得、變更或移除原則指派。</span><span class="sxs-lookup"><span data-stu-id="c3721-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="c3721-152">匯出資源群組作為範本</span><span class="sxs-lookup"><span data-stu-id="c3721-152">Export a resource group as a template</span></span>
<span data-ttu-id="c3721-153">針對現有的資源群組，您可以檢視此資源群組的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="c3721-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="c3721-154">匯出此範本有兩個優點︰</span><span class="sxs-lookup"><span data-stu-id="c3721-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="c3721-155">因為所有基礎結構都已定義於範本中，所以您可以輕鬆地自動進行解決方案的未來部署。</span><span class="sxs-lookup"><span data-stu-id="c3721-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="c3721-156">您可以查看代表您的解決方案的 JSON，藉此熟悉範本語法。</span><span class="sxs-lookup"><span data-stu-id="c3721-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="c3721-157">使用 Azure CLI，您可以匯出代表資源群組目前狀態的範本，或下載特定部署所用的範本。</span><span class="sxs-lookup"><span data-stu-id="c3721-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="c3721-158">**匯出資源群組的範本** - 這在您已變更資源群組，而且需要擷取其目前狀態的 JSON 表示法時很有用。</span><span class="sxs-lookup"><span data-stu-id="c3721-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="c3721-159">不過，產生的範本只包含最少的參數數目，但不包含任何變數。</span><span class="sxs-lookup"><span data-stu-id="c3721-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="c3721-160">範本中大部分的值為硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="c3721-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="c3721-161">在部署所產生的範本之前，您可能想要將更多的值轉換成參數，以便針對不同的環境自訂部署。</span><span class="sxs-lookup"><span data-stu-id="c3721-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="c3721-162">若要將資源群組範本匯出至本機目錄中，請執行 `azure group export` 命令，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="c3721-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="c3721-163">(取代適用於您作業系統環境的本機目錄。)</span><span class="sxs-lookup"><span data-stu-id="c3721-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="c3721-164">**下載特定部署的範本** - 這在您需要檢視用來部署資源的實際範本時很有用。</span><span class="sxs-lookup"><span data-stu-id="c3721-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="c3721-165">範本會包含針對原始部署定義的所有參數和變數。</span><span class="sxs-lookup"><span data-stu-id="c3721-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="c3721-166">不過，如果您組織中有人已變更非此範本中定義的資源群組，此範本並不會代表資源群組的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="c3721-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="c3721-167">若要將用於特定部署的範本下載至本機目錄，請執行 `azure group deployment template download` 命令。</span><span class="sxs-lookup"><span data-stu-id="c3721-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="c3721-168">例如：</span><span class="sxs-lookup"><span data-stu-id="c3721-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="c3721-169">範本匯出處於預覽狀態，並非所有的資源類型目前都支援匯出範本。</span><span class="sxs-lookup"><span data-stu-id="c3721-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="c3721-170">嘗試匯出範本時，您可能會看到一個錯誤，表示未匯出某些資源。</span><span class="sxs-lookup"><span data-stu-id="c3721-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="c3721-171">如有需要，下載範本之後，在範本中手動定義這些資源。</span><span class="sxs-lookup"><span data-stu-id="c3721-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c3721-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3721-172">Next steps</span></span>
* <span data-ttu-id="c3721-173">若要取得部署作業的詳細資料，並使用 Azure CLI 進行部署錯誤疑難排解，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="c3721-174">如果您想要使用 CLI 來設定應用程式或指令碼以存取資源，請參閱[使用 Azure CLI 來建立服務主體以存取資源](resource-group-authenticate-service-principal-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="c3721-175">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="c3721-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

