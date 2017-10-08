---
title: "標記的 aaaAzure 資源原則 |Microsoft 文件"
description: "提供在資源上管理標籤之資源原則的範例"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>套用標籤的資源原則

本主題提供常見的原則，規則可套用 tooensure 使用一致的標記上的資源。

套用標籤原則 tooa 資源群組或與現有資源的訂用帳戶、 追溯性不適 hello 原則 toothose 資源。 tooenforce hello 原則對這些資源，會觸發更新 toohello，現有的資源。 本文包含觸發更新的 PowerShell 範例。

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>請確定資源群組中的所有資源都有標籤/值

常見的需求是資源群組中的所有資源都有特定的標籤和值。 這項需求通常會依部門所需的 tootrack 成本。 必須符合下列條件的 hello:

* hello 需要標記和值附加的 toonew 並已更新沒有 hello 標記的資源。
* hello 所需的標記和值無法從任何現有的資源移除。

您可以套用兩個內建原則 tooa 資源群組，以完成這項需求。

| ID | 說明 |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Hello 使用者未指定時，適用於要求的標記和其預設值。 |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | 強制必要的標籤和其值。 |

### <a name="powershell"></a>PowerShell

下列 PowerShell 指令碼的 hello 指派 hello 兩個內建原則定義 tooa 資源群組。 在執行之前 hello 指令碼，將指派所有必要的標記 toohello 資源群組。 需要 hello 群組中的 hello 資源 hello 資源群組上的每個標記。 在您的訂閱，tooassign tooall 資源群組不提供 hello`-Name`參數取得 hello 資源群組時。

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

指派之後 hello 原則，您可以觸發現有資源 tooenforce hello 標記原則有新增更新 tooall。 hello 下列指令碼會保留任何存在於 hello 資源的標記：

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>需要資源類型的標籤
hello 下列範例顯示如何 toonest 邏輯運算子 toorequire 應用程式標記只有指定的資源類型 （在此案例中的儲存體帳戶）。

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>需要標籤
hello 下列原則會拒絕要求沒有包含"costCenter"索引鍵 （可以套用任何值） 的標記：

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>後續步驟
* 定義原則規則 （如 hello 前面範例所示） 之後, 您會需要 toocreate hello 原則定義，並將它指派 tooa 範圍。 hello 領域可以訂用帳戶、 資源群組或資源。 tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。 tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。
* 如簡介 tooresource 原則，請參閱[資源原則概觀](resource-manager-policy.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

