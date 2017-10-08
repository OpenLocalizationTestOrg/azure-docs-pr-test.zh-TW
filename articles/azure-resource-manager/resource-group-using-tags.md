---
title: "aaaTag Azure 邏輯組織的資源 |Microsoft 文件"
description: "示範如何 tooapply 標記 tooorganize Azure 帳單及管理資源。"
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
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a><span data-ttu-id="3c264-103">使用標記 tooorganize 您的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="3c264-103">Use tags tooorganize your Azure resources</span></span>
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> <span data-ttu-id="3c264-104">您可以套用標籤只有 tooresources 支援 Azure 資源管理員作業。</span><span class="sxs-lookup"><span data-stu-id="3c264-104">You can apply tags only tooresources that support Azure Resource Manager operations.</span></span> <span data-ttu-id="3c264-105">如果您建立虛擬機器、 虛擬網路或透過 hello 傳統部署模型 (例如透過 hello Azure 傳統入口網站) 的儲存體帳戶，則無法套用標籤 toothat 資源。</span><span class="sxs-lookup"><span data-stu-id="3c264-105">If you created a virtual machine, virtual network, or storage account through hello classic deployment model (such as through hello Azure classic portal), you cannot apply a tag toothat resource.</span></span> <span data-ttu-id="3c264-106">toosupport 標記，重新部署這些資源透過資源管理員。</span><span class="sxs-lookup"><span data-stu-id="3c264-106">toosupport tagging, redeploy these resources through Resource Manager.</span></span> <span data-ttu-id="3c264-107">所有其他資源皆支援標記。</span><span class="sxs-lookup"><span data-stu-id="3c264-107">All other resources support tagging.</span></span>
> 
> 

## <a name="policies-for-tag-consistency"></a><span data-ttu-id="3c264-108">標籤一致性原則</span><span class="sxs-lookup"><span data-stu-id="3c264-108">Policies for tag consistency</span></span>

<span data-ttu-id="3c264-109">您可以為您的組織使用資源原則 toocreate 標準規則。</span><span class="sxs-lookup"><span data-stu-id="3c264-109">You can use resource policies toocreate standard rules for your organization.</span></span> <span data-ttu-id="3c264-110">您可以建立原則，確保資源都會加上 hello 適當的值。</span><span class="sxs-lookup"><span data-stu-id="3c264-110">You can create policies that ensure resources are tagged with hello appropriate values.</span></span> <span data-ttu-id="3c264-111">如需詳細資訊，請參閱[套用標籤的資源原則](resource-manager-policy-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-111">For more information, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>

## <a name="powershell"></a><span data-ttu-id="3c264-112">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c264-112">PowerShell</span></span>
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a><span data-ttu-id="3c264-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c264-113">Azure CLI</span></span>

<span data-ttu-id="3c264-114">toosee hello 的現有標籤*資源群組*，使用：</span><span class="sxs-lookup"><span data-stu-id="3c264-114">toosee hello existing tags for a *resource group*, use:</span></span>

```azurecli
az group show -n examplegroup --query tags
```

<span data-ttu-id="3c264-115">該指令碼會傳回下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c264-115">That script returns hello following format:</span></span>

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

<span data-ttu-id="3c264-116">toosee hello 的現有標籤*資源具有指定的資源識別碼*，使用：</span><span class="sxs-lookup"><span data-stu-id="3c264-116">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```azurecli
az resource show --id {resource-id} --query tags
```

<span data-ttu-id="3c264-117">或 toosee hello 的現有標籤*具有指定的名稱、 類型和資源群組的資源*，使用：</span><span class="sxs-lookup"><span data-stu-id="3c264-117">Or, toosee hello existing tags for a *resource that has a specified name, type, and resource group*, use:</span></span>

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

<span data-ttu-id="3c264-118">具有特定標記的 tooget 資源群組使用`az group list`:</span><span class="sxs-lookup"><span data-stu-id="3c264-118">tooget resource groups that have a specific tag, use `az group list`:</span></span>

```azurecli
az group list --tag Dept=IT
```

<span data-ttu-id="3c264-119">tooget hello 具有所有資源，特定的標記和值，都使用`az resource list`:</span><span class="sxs-lookup"><span data-stu-id="3c264-119">tooget all hello resources that have a particular tag and value, use `az resource list`:</span></span>

```azurecli
az resource list --tag Dept=Finance
```

<span data-ttu-id="3c264-120">每次您套用標籤 tooa 資源或資源群組，您就會覆寫 hello 現有資源或資源群組上的標記。</span><span class="sxs-lookup"><span data-stu-id="3c264-120">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="3c264-121">因此，您必須使用不同的方式根據 hello 資源或資源群組是否擁有現有的標記。</span><span class="sxs-lookup"><span data-stu-id="3c264-121">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="3c264-122">tooadd 標記 tooa*沒有現有的標記的資源群組*，使用：</span><span class="sxs-lookup"><span data-stu-id="3c264-122">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

<span data-ttu-id="3c264-123">tooadd 標記 tooa*沒有現有的標記資源*，使用：</span><span class="sxs-lookup"><span data-stu-id="3c264-123">tooadd tags tooa *resource without existing tags*, use:</span></span>

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

<span data-ttu-id="3c264-124">tooadd 標記 tooa 資源已有標籤，擷取 hello 現有的標記、 重新格式化該值，然後重新套用 hello 現有和新標籤：</span><span class="sxs-lookup"><span data-stu-id="3c264-124">tooadd tags tooa resource that already has tags, retrieve hello existing tags, reformat that value, and reapply hello existing and new tags:</span></span> 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

<span data-ttu-id="3c264-125">資源群組 tooits，從資源標記的所有 tooapply 和*不會保留現有的都標記 hello 資源*，使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c264-125">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

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

<span data-ttu-id="3c264-126">資源群組 tooits，從資源標記的所有 tooapply 和*保留資源上的現有都標籤*，使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c264-126">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources*, use hello following script:</span></span>

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


## <a name="templates"></a><span data-ttu-id="3c264-127">範本</span><span class="sxs-lookup"><span data-stu-id="3c264-127">Templates</span></span>

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a><span data-ttu-id="3c264-128">入口網站</span><span class="sxs-lookup"><span data-stu-id="3c264-128">Portal</span></span>
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a><span data-ttu-id="3c264-129">REST API</span><span class="sxs-lookup"><span data-stu-id="3c264-129">REST API</span></span>
<span data-ttu-id="3c264-130">hello Azure 入口網站和 PowerShell 使用 hello[資源管理員 REST API](https://docs.microsoft.com/rest/api/resources/)幕後 hello。</span><span class="sxs-lookup"><span data-stu-id="3c264-130">hello Azure portal and PowerShell both use hello [Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/) behind hello scenes.</span></span> <span data-ttu-id="3c264-131">如果您需要 toointegrate 標記成另一個環境，您可以使用來取得標記**取得**hello 資源識別碼和更新 hello 組上所使用的標記**修補**呼叫。</span><span class="sxs-lookup"><span data-stu-id="3c264-131">If you need toointegrate tagging into another environment, you can get tags by using **GET** on hello resource ID and update hello set of tags by using a **PATCH** call.</span></span>

## <a name="tags-and-billing"></a><span data-ttu-id="3c264-132">標記與計費</span><span class="sxs-lookup"><span data-stu-id="3c264-132">Tags and billing</span></span>
<span data-ttu-id="3c264-133">您可以使用標記 toogroup 計費資料。</span><span class="sxs-lookup"><span data-stu-id="3c264-133">You can use tags toogroup your billing data.</span></span> <span data-ttu-id="3c264-134">比方說，如果您執行於不同的組織多個 Vm，請依成本中心使用 hello 標記 toogroup 使用量。</span><span class="sxs-lookup"><span data-stu-id="3c264-134">For example, if you are running multiple VMs for different organizations, use hello tags toogroup usage by cost center.</span></span> <span data-ttu-id="3c264-135">您也可以使用標記 toocategorize 成本的執行階段環境，例如 hello 計費使用量 hello 實際執行環境中執行的 vm。</span><span class="sxs-lookup"><span data-stu-id="3c264-135">You can also use tags toocategorize costs by runtime environment, such as hello billing usage for VMs running in hello production environment.</span></span>


<span data-ttu-id="3c264-136">您可以擷取有關透過 hello 標記資訊[Azure 資源使用量和 RateCard Api](../billing/billing-usage-rate-card-overview.md)或 hello 使用量逗點分隔值 (CSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="3c264-136">You can retrieve information about tags through hello [Azure Resource Usage and RateCard APIs](../billing/billing-usage-rate-card-overview.md) or hello usage comma-separated values (CSV) file.</span></span> <span data-ttu-id="3c264-137">您可以下載 hello 使用量檔案從 hello [Azure 帳戶入口網站](https://account.windowsazure.com/)或[EA 入口網站](https://ea.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3c264-137">You download hello usage file from hello [Azure account portal](https://account.windowsazure.com/) or [EA portal](https://ea.azure.com).</span></span> <span data-ttu-id="3c264-138">如需有關以程式設計方式存取 toobilling 資訊的詳細資訊，請參閱[深入了解您的 Microsoft Azure 資源耗用量](../billing/billing-usage-rate-card-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-138">For more information about programmatic access toobilling information, see [Gain insights into your Microsoft Azure resource consumption](../billing/billing-usage-rate-card-overview.md).</span></span> <span data-ttu-id="3c264-139">若為 REST API 作業，請參閱 [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)。</span><span class="sxs-lookup"><span data-stu-id="3c264-139">For REST API operations, see [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).</span></span>


<span data-ttu-id="3c264-140">當您下載之服務的支援和計費標籤 hello 使用 CSV 時，hello 標籤會顯示在 hello**標記**資料行。</span><span class="sxs-lookup"><span data-stu-id="3c264-140">When you download hello usage CSV for services that support tags with billing, hello tags appear in hello **Tags** column.</span></span> <span data-ttu-id="3c264-141">如需詳細資訊，請參閱[了解 Microsoft Azure 帳單](../billing/billing-understand-your-bill.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-141">For more information, see [Understand your bill for Microsoft Azure](../billing/billing-understand-your-bill.md).</span></span>

![查看計費中的標記](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a><span data-ttu-id="3c264-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c264-143">Next steps</span></span>
* <span data-ttu-id="3c264-144">您可以使用自訂原則，在訂用帳戶內套用限制和慣例。</span><span class="sxs-lookup"><span data-stu-id="3c264-144">You can apply restrictions and conventions across your subscription by using customized policies.</span></span> <span data-ttu-id="3c264-145">您所定義的原則可能需要所有資源都具有特定標籤的值。</span><span class="sxs-lookup"><span data-stu-id="3c264-145">A policy that you define might require that all resources have a value for a particular tag.</span></span> <span data-ttu-id="3c264-146">如需詳細資訊，請參閱[原則 toomanage 資源及控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-146">For more information, see [Use policies toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="3c264-147">如簡介 toousing Azure PowerShell 時您要部署資源，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-147">For an introduction toousing Azure PowerShell when you're deploying resources, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="3c264-148">如簡介 toousing hello Azure CLI 時您要部署資源，請參閱[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-148">For an introduction toousing hello Azure CLI when you're deploying resources, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="3c264-149">如簡介 toousing hello 入口網站中，請參閱[使用 hello Azure 入口網站 toomanage 您的 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-149">For an introduction toousing hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>  
* <span data-ttu-id="3c264-150">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="3c264-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

