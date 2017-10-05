---
title: "針對邏輯組織標記 Azure 資源 | Microsoft Docs"
description: "示範如何套用標籤以針對計費及管理來組織 Azure 資源。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a><span data-ttu-id="85f44-103">使用標記來組織 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="85f44-103">Use tags to organize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="85f44-104">您只能將標籤套用到支援 Azure Resource Manager 作業的資源。</span><span class="sxs-lookup"><span data-stu-id="85f44-104">You can apply tags only to resources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="85f44-105">如果您透過傳統部署模型 (例如透過 Azure 傳統入口網站) 建立虛擬機器、虛擬網路或儲存體帳戶，就無法將標籤套用至該資源。</span><span class="sxs-lookup"><span data-stu-id="85f44-105">If you created a virtual machine, virtual network, or storage account through the classic deployment model (such as through the Azure classic portal), you cannot apply a tag to that resource.</span></span> <span data-ttu-id="85f44-106">若要支援標記，請透過資源管理員重新部署這些資源。</span><span class="sxs-lookup"><span data-stu-id="85f44-106">To support tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="85f44-107">所有其他資源皆支援標記。</span><span class="sxs-lookup"><span data-stu-id="85f44-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="85f44-108">標籤一致性原則</span><span class="sxs-lookup"><span data-stu-id="85f44-108">Policies for tag consistency</span></span>

<span data-ttu-id="85f44-109">您可以使用資源原則來建立組織適用的標準規則。</span><span class="sxs-lookup"><span data-stu-id="85f44-109">You can use resource policies to create standard rules for your organization.</span></span> <span data-ttu-id="85f44-110">您可以建立原則，以確保會為資源標記適當的值。</span><span class="sxs-lookup"><span data-stu-id="85f44-110">You can create policies that ensure resources are tagged with the appropriate values.</span></span> <span data-ttu-id="85f44-111">如需詳細資訊，請參閱[套用標籤的資源原則](resource-manager-policy-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="85f44-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85f44-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="85f44-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="85f44-113">Azure CLI</span></span>

<span data-ttu-id="85f44-114">若要查看*資源群組*的現有標籤，請使用：</span><span class="sxs-lookup"><span data-stu-id="85f44-114">To see the existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="85f44-115">該指令碼會傳回下列格式︰</span><span class="sxs-lookup"><span data-stu-id="85f44-115">That script returns the following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="85f44-116">若要查看「具有指定之資源識別碼的資源」的現有標記，請使用：</span><span class="sxs-lookup"><span data-stu-id="85f44-116">To see the existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="85f44-117">或者，若要查看「具有指定之名稱、類型和資源群組的資源」的現有標籤，請使用：</span><span class="sxs-lookup"><span data-stu-id="85f44-117">Or, to see the existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="85f44-118">若要取得「具有特定標籤的資源群組」，請使用 `az group list`：</span><span class="sxs-lookup"><span data-stu-id="85f44-118">To get resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="85f44-119">若要取得「具有特定標籤和值的所有資源」，請使用 `az resource list`：</span><span class="sxs-lookup"><span data-stu-id="85f44-119">To get all the resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="85f44-120">每當您將標記套用到資源或資源群組時，即會覆寫該資源或資源群組上現有的標記。</span><span class="sxs-lookup"><span data-stu-id="85f44-120">Every time you apply tags to a resource or a resource group, you overwrite the existing tags on that resource or resource group.</span></span> <span data-ttu-id="85f44-121">因此，您必須視該資源或資源群組是否具備現有標籤來使用不同的方法。</span><span class="sxs-lookup"><span data-stu-id="85f44-121">Therefore, you must use a different approach based on whether the resource or resource group has existing tags.</span></span> 

<span data-ttu-id="85f44-122">若要將標籤新增至*不具現有標籤的資源群組*，請使用：</span><span class="sxs-lookup"><span data-stu-id="85f44-122">To add tags to a *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="85f44-123">若要將標籤新增至*沒有現有標籤的資源*，請使用：</span><span class="sxs-lookup"><span data-stu-id="85f44-123">To add tags to a *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="85f44-124">若要將標籤新增至已經具有標籤的資源，請擷取現有的標籤、將該值重新格式化，然後重新套用現有和新的標籤：</span><span class="sxs-lookup"><span data-stu-id="85f44-124">To add tags to a resource that already has tags, retrieve the existing tags, reformat that value, and reapply the existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="85f44-125">若要將所有標籤從資源群組套用至其資源，而*不在資源上保留現有的標籤*，請使用下列指令碼︰</span><span class="sxs-lookup"><span data-stu-id="85f44-125">To apply all tags from a resource group to its resources, and *not retain existing tags on the resources*, use the following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

<span data-ttu-id="85f44-126">若要將所有標籤從資源群組套用至其資源，並*在資源上保留現有的標籤*，請使用下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="85f44-126">To apply all tags from a resource group to its resources, and *retain existing tags on resources*, use the following script:</span></span>

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a><span data-ttu-id="85f44-127">範本</span><span class="sxs-lookup"><span data-stu-id="85f44-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="85f44-128">入口網站</span><span class="sxs-lookup"><span data-stu-id="85f44-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="85f44-129">REST API</span><span class="sxs-lookup"><span data-stu-id="85f44-129">REST API</span></span>
<span data-ttu-id="85f44-130">Azure 入口網站和 PowerShell 在幕後都使用 [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) 。</span><span class="sxs-lookup"><span data-stu-id="85f44-130">The Azure portal and PowerShell both use the [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind the scenes.</span></span> <span data-ttu-id="85f44-131">如果您需要將標籤整合到另一個環境中，則可以在資源識別碼上利用 **GET** 來取得標籤，並使用 **PATCH** 呼叫來更新一組標籤。</span><span class="sxs-lookup"><span data-stu-id="85f44-131">If you need to integrate tagging into another environment, you can get tags by using **GET** on the resource ID and update the set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="85f44-132">標記與計費</span><span class="sxs-lookup"><span data-stu-id="85f44-132">Tags and billing</span></span>
<span data-ttu-id="85f44-133">您可以使用標籤將您的計費資料分組。</span><span class="sxs-lookup"><span data-stu-id="85f44-133">You can use tags to group your billing data.</span></span> <span data-ttu-id="85f44-134">例如，如果您執行不同組織的多個 VM，您可以使用標籤根據成本中心將使用情況分組。</span><span class="sxs-lookup"><span data-stu-id="85f44-134">For example, if you are running multiple VMs for different organizations, use the tags to group usage by cost center.</span></span> <span data-ttu-id="85f44-135">您也可以使用標籤來根據執行階段環境將成本分類。例如，在生產環境中執行之 VM 的計費使用量。</span><span class="sxs-lookup"><span data-stu-id="85f44-135">You can also use tags to categorize costs by runtime environment, such as the billing usage for VMs running in the production environment.</span></span>


<span data-ttu-id="85f44-136">您可以透過 [Azure 資源使用狀況和 RateCard API](../billing/billing-usage-rate-card-overview.md) 或使用狀況逗號分隔值 (CSV) 檔案，擷取關於標記的資訊。</span><span class="sxs-lookup"><span data-stu-id="85f44-136">You can retrieve information about tags through the [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or the usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="85f44-137">您可以從 [Azure 帳戶入口網站](https://account.windowsazure.com/)或 [EA 入口網站](https://ea.azure.com)下載使用量檔案。</span><span class="sxs-lookup"><span data-stu-id="85f44-137">You download the usage file from the [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="85f44-138">如需以程式設計方式存取帳單資訊的詳細資訊，請參閱 [深入了解 Microsoft Azure 資源耗用量](../billing/billing-usage-rate-card-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-138">For more information about programmatic access to billing information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="85f44-139">若為 REST API 作業，請參閱 [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)。</span><span class="sxs-lookup"><span data-stu-id="85f44-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="85f44-140">當您下載服務 (支援附計費的標記) 的使用狀況 CSV 時，標記會出現在 [標記]  資料行。</span><span class="sxs-lookup"><span data-stu-id="85f44-140">When you download the usage CSV for services that support tags with billing, the tags appear in the **Tags** column.</span></span> <span data-ttu-id="85f44-141">如需詳細資訊，請參閱[了解 Microsoft Azure 帳單](../billing/billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![查看計費中的標記](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="85f44-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85f44-143">Next steps</span></span>
* <span data-ttu-id="85f44-144">您可以使用自訂原則，在訂用帳戶內套用限制和慣例。</span><span class="sxs-lookup"><span data-stu-id="85f44-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="85f44-145">您所定義的原則可能需要所有資源都具有特定標籤的值。</span><span class="sxs-lookup"><span data-stu-id="85f44-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="85f44-146">如需詳細資訊，請參閱 [使用原則來管理資源和控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-146">For more information, see [Use policies to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="85f44-147">如需在部署資源時使用 Azure PowerShell 的簡介，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-147">For an introduction to using Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="85f44-148">如需在部署資源時使用 Azure CLI 的簡介，請參閱[使用適用於 Mac、Linux 和 Windows 的 Azure CLI 搭配 Azure Resource Manager](xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-148">For an introduction to using the Azure CLI when you're deploying resources, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="85f44-149">如需使用入口網站的簡介，請參閱[使用 Azure 入口網站來管理您的 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-149">For an introduction to using the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="85f44-150">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="85f44-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

