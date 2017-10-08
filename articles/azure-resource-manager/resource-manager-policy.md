---
title: "aaaAzure 資源原則 |Microsoft 文件"
description: "描述如何在部署期間設定 toouse Azure 資源管理員原則 tooensure 一致的資源內容。 原則可以套用在 hello 訂用帳戶或資源群組。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>資源原則概觀
資源原則可讓您在組織中的資源 tooestablish 慣例。 藉由定義慣例，您可以控制成本以及更輕鬆地管理您的資源。 例如，您可以指定僅允許特定類型的虛擬機器。 或者，您可以要求所有資源都有特定標籤。 原則會由所有子資源繼承。 因此，如果原則已套用的 tooa 資源群組，則該資源群組中的適用 tooall hello 資源。

有兩個概念 toounderstand 有關原則：

* 原則定義-您說明 hello 原則會強制執行以及何種動作 tootake
* 原則指派-套用 hello 原則定義 tooa 範圍 （訂用帳戶或資源群組）

本主題著重於原則定義。 原則指派的詳細資訊，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)或[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。

建立和更新資源 (PUT 和 PATCH 作業) 時，會評估原則。

> [!NOTE]
> 目前，原則不會評估標記、 種類和位置，例如 hello Microsoft.Resources/deployments 資源類型不支援的資源類型。 未來將加入此支援。 tooavoid 回溯相容性問題，您應該明確地指定類型撰寫原則時。 例如，會對所有類型套用未指定類型的標記原則。 在此情況下，如果沒有不支援標記的巢狀的資源，範本部署可能會失敗，且已新增 hello 部署資源類型 toopolicy 評估。 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>它和 RBAC 有什麼不同？
原則和角色型存取控制 (RBAC) 之間有幾個主要差異。 RBAC 著重於不同範圍的**使用者**動作。 比方說，您會加入資源群組的 toohello 參與者角色在 hello 預期範圍，因此您可以變更 toothat 資源群組。 原則在部署期間著重於**資源**屬性。 例如，透過原則，您可以控制 hello 類型可以佈建的資源。 或者，您可以限制 hello hello 資源可以佈建所在的位置。 不同於 RBAC，原則是個預設允許和明確拒絕的系統。 

toouse 原則，您必須透過 RBAC 進行驗證。 具體來說，您的帳戶需要：

* `Microsoft.Authorization/policydefinitions/write`權限 toodefine 原則
* `Microsoft.Authorization/policyassignments/write`權限 tooassign 原則 

這些權限不包含在 hello**參與者**角色。

## <a name="built-in-policies"></a>內建原則

Azure 提供 hello 數目可能會降低某些內建的原則定義的原則，您有 toodefine。 原則定義之前，您應該考慮的內建原則是否已提供您需要的 hello 定義。 hello 內建的原則定義如下：

* 允許的位置
* 允許的資源類型
* 允許的儲存體帳戶 SKU
* 允許的虛擬機器 SKU
* 套用標籤和預設值
* 強制執行標籤和值
* 不允許的資源類型
* 需要 SQL Server 12.0 版
* 需要儲存體帳戶加密

您可以指定任何這些原則透過 hello[入口網站](resource-manager-policy-portal.md)， [PowerShell](resource-manager-policy-create-assign.md#powershell)，或[Azure CLI](resource-manager-policy-create-assign.md#azure-cli)。

## <a name="policy-definition-structure"></a>原則定義結構
您使用 JSON toocreate 原則定義。 hello 原則定義中包含項的目：

* 參數
* 顯示名稱
* 說明
* 原則規則
  * 邏輯評估
  * 效果

下列範例中的 hello 顯示限制在部署資源的原則：

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>參數
使用參數，可協助減少 hello 原則定義的數量，以簡化原則管理。 定義的原則，資源內容 （例如限制可部署資源的 hello 位置），並在 hello 定義中包含參數。 然後，您重複使用該原則的定義不同的案例藉由傳遞不同的值 （例如，指定一組訂用帳戶的位置） 時指派 hello 原則。

當您建立原則定義時，宣告參數。

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

hello 參數型別可以是字串或陣列。 hello 中繼資料屬性用於 Azure 入口網站 toodisplay 人性化的資訊等工具。 

Hello 原則規則中，您可以參考參數以 hello，請使用下列語法： 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>顯示名稱和描述

使用 hello **displayName**和**描述**tooidentify hello 原則定義和使用時才提供的內容。

## <a name="policy-rule"></a>原則規則

hello 原則規則包含**如果**和**然後**區塊。 在 hello**如果**區塊中，您定義一個或多個條件，指定 hello 原則會強制執行。 您可以套用邏輯運算子 toothese 條件 tooprecisely 定義 hello 案例的原則。 在 hello**然後**區塊中，定義當 hello hello 效果**如果**符合條件。

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>邏輯運算子
是支援的 hello 邏輯運算子：

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

hello**不**語法反轉 hello 條件的 hello 結果。 hello **allOf**語法 (類似 toohello 邏輯**和**作業) 需要所有的條件 toobe true。 hello **anyOf**語法 (類似 toohello 邏輯**或**作業) 需要一或多個條件 toobe true。

您可以巢狀邏輯運算子。 下列範例所示的 hello**不**內變成巢狀的作業**allOf**作業。 

```json
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
```

### <a name="conditions"></a>條件
hello 條件評估是否**欄位**是否符合特定準則。 支援的 hello 條件如下：

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

當使用 hello**像**條件，您可以提供萬用字元 （*） 在 hello 值。

當使用 hello**符合**條件，請提供`#`toorepresent 數字，`?`的字母，而且其他所有字元 toorepresent 的實際字元。 例如，請參閱[為名稱和文字套用資源原則](resource-manager-policy-naming-convention.md)。

### <a name="fields"></a>欄位
條件是透過欄位所形成。 欄位代表 hello 資源要求裝載中的內容也就是使用的 toodescribe hello hello 資源狀態。  

支援下列欄位的 hello:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* 屬性別名 - 如需清單，請參閱[別名](#aliases)。

### <a name="effect"></a>效果
原則支援三種效果類型 - `deny`、`audit` 和 `append`。 

* **拒絕**hello 稽核記錄檔中產生事件，就會失敗 hello 要求
* **稽核**稽核記錄檔中就會產生警告事件，但不會失敗 hello 要求
* **附加**新增 hello 定義欄位 toohello 要求組 

如**附加**，您必須提供下列詳細資料的 hello:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

hello 值可以是字串或物件的 JSON 格式。 

## <a name="aliases"></a>別名

您可以使用屬性別名 tooaccess 特定屬性資源類型。 別名可讓您 toorestrict 哪些值或條件允許資源上的屬性。 每個別名將對應 toopaths 中指定的資源類型的不同應用程式開發介面版本。 原則評估期間 hello 原則引擎會取得該應用程式開發介面版本 hello 屬性路徑。

**Microsoft.Cache/Redis**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | 設定 hello 非 ssl 的 Redis 伺服器連接埠 (6379) 是否已啟用。 |
| Microsoft.Cache/Redis/shardCount | 設定進階叢集快取上建立的分區 toobe hello 號碼。  |
| Microsoft.Cache/Redis/sku.capacity | 設定 hello Redis 快取 toodeploy hello 大小。  |
| Microsoft.Cache/Redis/sku.family | 設定 hello SKU 系列 toouse。 |
| Microsoft.Cache/Redis/sku.name | 設定 Redis 快取 toodeploy hello 類型。 |

**Microsoft.Cdn/profiles**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Hello 名稱 hello 定價層設定。 |

**Microsoft.Compute/disks**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/imagePublisher | Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。 |
| Microsoft.Compute/imageSku | 設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/imageVersion | 設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。 |


**Microsoft.Compute/virtualMachines**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Compute/imageId | 設定 hello hello 用映像 toocreate hello 虛擬機器的識別項。 |
| Microsoft.Compute/imageOffer | Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/imagePublisher | Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。 |
| Microsoft.Compute/imageSku | 設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/imageVersion | 設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。 |
| Microsoft.Compute/licenseType | 設定 hello 映像或磁碟為內部授權。 這個值只用於包含 hello Windows 伺服器作業系統映像。  |
| Microsoft.Compute/virtualMachines/imageOffer | Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/virtualMachines/imagePublisher | Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。 |
| Microsoft.Compute/virtualMachines/imageSku | 設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/virtualMachines/imageVersion | 設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。 |
| Microsoft.Compute/virtualMachines/osDisk.Uri | 設定 hello vhd URI。 |
| Microsoft.Compute/virtualMachines/sku.name | 設定 hello hello 虛擬機器大小。 |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | 設定 hello hello 擴充功能的發行者名稱。 |
| Microsoft.Compute/virtualMachines/extensions/type | 設定延伸 hello 型別。 |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | 設定 hello hello 擴充功能版本。 |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Compute/imageId | 設定 hello hello 用映像 toocreate hello 虛擬機器的識別項。 |
| Microsoft.Compute/imageOffer | Hello 平台映像或 marketplace 映像組 hello 優惠 toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/imagePublisher | Hello 平台映像或 marketplace 映像組 hello 發行者使用 toocreate hello 虛擬機器。 |
| Microsoft.Compute/imageSku | 設定 hello hello 平台映像或 marketplace 映像的 SKU toocreate hello 虛擬機器的使用。 |
| Microsoft.Compute/imageVersion | 設定 hello hello 平台映像或 marketplace 映像使用新版 toocreate hello 虛擬機器。 |
| Microsoft.Compute/licenseType | 設定 hello 映像或磁碟為內部授權。 這個值只用於包含 hello Windows 伺服器作業系統映像。 |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Hello 規模集中設定 hello hello 的所有虛擬機器的電腦名稱前置詞。 |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | 設定使用者映像的 hello blob URI。 |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | 設定使用的 toostore hello 擴展集的作業系統磁碟的 hello 容器 Url。 |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | 設定 hello 大小的虛擬機器規模集中的。 |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | 設定虛擬機器規模集中的 hello 層。 |
  
**Microsoft.Network/applicationGateways**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | 設定的 hello 閘道的 hello 大小。 |

**Microsoft.Network/virtualNetworkGateways**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | 將此虛擬網路閘道 hello 類型的設定。 |
| Microsoft.Network/virtualNetworkGateways/sku.name | 設定 hello 閘道 SKU 的名稱。 |

**Microsoft.Sql/servers**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Sql/servers/version | 設定 hello hello 伺服器版本。 |

**Microsoft.Sql/databases**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | 設定 hello hello 資料庫版本。 |
| Microsoft.Sql/servers/databases/elasticPoolName | 」 組 hello hello 彈性集區 hello 資料庫名稱。 |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | 設定 hello 設定層級的服務目標識別碼 hello 資料庫。 |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Hello hello 設定 hello 資料庫的服務等級目標名稱設定。  |

**Microsoft.Sql/elasticpools**

| Alias | 說明 |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | 設定 hello 總計共用 hello 資料庫彈性集區 DTU。 |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | 將 hello edition hello 彈性集區的設定。 |

**Microsoft.Storage/storageAccounts**

| Alias | 說明 |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | 設定用於計費 hello 存取層。 |
| Microsoft.Storage/storageAccounts/accountType | 設定 hello SKU 的名稱。 |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | 設定是否 hello 服務加密 hello 資料會儲存在 hello blob 儲存體服務。 |
| Microsoft.Storage/storageAccounts/enableFileEncryption | 設定是否 hello 服務加密 hello 資料儲存在 hello 檔案儲存體服務。 |
| Microsoft.Storage/storageAccounts/sku.name | 設定 hello SKU 的名稱。 |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | 設定 tooallow 只有 https 流量 toostorage 服務。 |


## <a name="policy-examples"></a>原則範例

下列主題中的 hello 包含原則範例：

* 如需標籤原則的範例，請參閱[套用標籤的資源原則](resource-manager-policy-tags.md)。
* 如需命名和文字模式的範例，請參閱[為名稱和文字套用資源原則](resource-manager-policy-naming-convention.md)。
* 儲存原則的範例，請參閱[套用資源原則 toostorage 帳戶](resource-manager-policy-storage.md)。
* 虛擬機器原則的範例，請參閱[套用資源原則 tooLinux Vm](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)和[套用資源原則 tooWindows Vm](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>後續步驟
* 定義原則規則之後, 將它指派 tooa 範圍。 tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。 tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。
* 發行位置 hello 原則結構描述是在[http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)。 

