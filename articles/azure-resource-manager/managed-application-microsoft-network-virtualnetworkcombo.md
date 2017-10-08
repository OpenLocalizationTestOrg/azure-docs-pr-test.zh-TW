---
title: "aaaAzure 受管理的應用程式 VirtualNetworkCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Network.VirtualNetworkCombo UI 項目"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Microsoft.Network.VirtualNetworkCombo UI 元素
選取新的或現有虛擬網路的控制項群組。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- 在 hello 上框線，hello 使用者已挑選新的虛擬網路，因此 hello 使用者可以自訂每個子網路的名稱和位址前置詞。 在此情況下，設定子網路為選擇性的。
- 在 hello 底部框線，hello 使用者已挑選現有的虛擬網路，因此 hello 使用者必須對應每一個子網路 hello 部署範本需要 tooan 現有的子網路。 在此情況下，設定子網路為必要的。

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>備註
- 如果指定，hello 第一個非重疊位址首碼的大小`defaultValue.addressPrefixSize`根據 hello 使用者訂用帳戶中的現有虛擬網路，自動決定。
- 預設值的 hello`defaultValue.name`和`defaultValue.addressPrefixSize`是**null**。
- 必須指定 `constraints.minAddressPrefixSize`。 任何現有的虛擬網路與小於 hello 指定的值都將無法使用選取的位址空間。
- 必須指定 `subnets`，且必須指定每個子網路的 `constraints.minAddressPrefixSize`。
- 在建立新的虛擬網路時，每個子網路位址首碼會自動根據計算 hello 虛擬網路的位址前置詞和個別`addressPrefixSize`。
- 在使用現有的虛擬網路時，無法選取任何小於個別 `constraints.minAddressPrefixSize` 的子網路。 此外，如果指定，就無法選取未至少包含 `minAddressCount` 的子網路。
hello 預設值是**0**。 hello 可用位址的 tooensure 是連續的請指定**true**如`requireContiguousAddresses`。 hello 預設值是**true**。
- 不支援在現有的虛擬網路中建立子網路。
- 如果`options.hideExisting`是**true**，hello 使用者無法選擇現有的虛擬網路。 hello 預設值是**false**。

## <a name="sample-output"></a>範例輸出
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
