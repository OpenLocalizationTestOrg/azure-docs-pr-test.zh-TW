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
# <a name="use-tags-tooorganize-your-azure-resources"></a>使用標記 tooorganize 您的 Azure 資源
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> 您可以套用標籤只有 tooresources 支援 Azure 資源管理員作業。 如果您建立虛擬機器、 虛擬網路或透過 hello 傳統部署模型 (例如透過 hello Azure 傳統入口網站) 的儲存體帳戶，則無法套用標籤 toothat 資源。 toosupport 標記，重新部署這些資源透過資源管理員。 所有其他資源皆支援標記。
> 
> 

## <a name="policies-for-tag-consistency"></a>標籤一致性原則

您可以為您的組織使用資源原則 toocreate 標準規則。 您可以建立原則，確保資源都會加上 hello 適當的值。 如需詳細資訊，請參閱[套用標籤的資源原則](resource-manager-policy-tags.md)。

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Azure CLI

toosee hello 的現有標籤*資源群組*，使用：

```azurecli
az group show -n examplegroup --query tags
```

該指令碼會傳回下列格式的 hello:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee hello 的現有標籤*資源具有指定的資源識別碼*，使用：

```azurecli
az resource show --id {resource-id} --query tags
```

或 toosee hello 的現有標籤*具有指定的名稱、 類型和資源群組的資源*，使用：

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

具有特定標記的 tooget 資源群組使用`az group list`:

```azurecli
az group list --tag Dept=IT
```

tooget hello 具有所有資源，特定的標記和值，都使用`az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

每次您套用標籤 tooa 資源或資源群組，您就會覆寫 hello 現有資源或資源群組上的標記。 因此，您必須使用不同的方式根據 hello 資源或資源群組是否擁有現有的標記。 

tooadd 標記 tooa*沒有現有的標記的資源群組*，使用：

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd 標記 tooa*沒有現有的標記資源*，使用：

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd 標記 tooa 資源已有標籤，擷取 hello 現有的標記、 重新格式化該值，然後重新套用 hello 現有和新標籤： 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

資源群組 tooits，從資源標記的所有 tooapply 和*不會保留現有的都標記 hello 資源*，使用下列指令碼的 hello:

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

資源群組 tooits，從資源標記的所有 tooapply 和*保留資源上的現有都標籤*，使用下列指令碼的 hello:

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


## <a name="templates"></a>範本

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>入口網站
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>REST API
hello Azure 入口網站和 PowerShell 使用 hello[資源管理員 REST API](https://docs.microsoft.com/rest/api/resources/)幕後 hello。 如果您需要 toointegrate 標記成另一個環境，您可以使用來取得標記**取得**hello 資源識別碼和更新 hello 組上所使用的標記**修補**呼叫。

## <a name="tags-and-billing"></a>標記與計費
您可以使用標記 toogroup 計費資料。 比方說，如果您執行於不同的組織多個 Vm，請依成本中心使用 hello 標記 toogroup 使用量。 您也可以使用標記 toocategorize 成本的執行階段環境，例如 hello 計費使用量 hello 實際執行環境中執行的 vm。


您可以擷取有關透過 hello 標記資訊[Azure 資源使用量和 RateCard Api](../billing/billing-usage-rate-card-overview.md)或 hello 使用量逗點分隔值 (CSV) 檔案。 您可以下載 hello 使用量檔案從 hello [Azure 帳戶入口網站](https://account.windowsazure.com/)或[EA 入口網站](https://ea.azure.com)。 如需有關以程式設計方式存取 toobilling 資訊的詳細資訊，請參閱[深入了解您的 Microsoft Azure 資源耗用量](../billing/billing-usage-rate-card-overview.md)。 若為 REST API 作業，請參閱 [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)。


當您下載之服務的支援和計費標籤 hello 使用 CSV 時，hello 標籤會顯示在 hello**標記**資料行。 如需詳細資訊，請參閱[了解 Microsoft Azure 帳單](../billing/billing-understand-your-bill.md)。

![查看計費中的標記](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>後續步驟
* 您可以使用自訂原則，在訂用帳戶內套用限制和慣例。 您所定義的原則可能需要所有資源都具有特定標籤的值。 如需詳細資訊，請參閱[原則 toomanage 資源及控制存取](resource-manager-policy.md)。
* 如簡介 toousing Azure PowerShell 時您要部署資源，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](powershell-azure-resource-manager.md)。
* 如簡介 toousing hello Azure CLI 時您要部署資源，請參閱[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](xplat-cli-azure-resource-manager.md)。
* 如簡介 toousing hello 入口網站中，請參閱[使用 hello Azure 入口網站 toomanage 您的 Azure 資源](resource-group-portal.md)。  
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

