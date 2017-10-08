---
title: "aaaAzure 受管理的應用程式 SizeSelector UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Compute.SizeSelector UI 項目"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Microsoft.Compute.SizeSelector UI 元素
選取一個或多個虛擬機器執行個體之大小的控制項。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>備註
- `recommendedSizes` 須包含至少一個大小。 hello 先建議 hello 預設會使用大小。
- 如果在選取的 hello 位置無法使用建議的大小，會自動略過 hello 大小。 相反地，hello 下一步建議使用大小。
- Hello 中未指定任何大小`constraints.allowedSizes`隱藏的並在未指定任何大小`constraints.excludedSizes`顯示。
`constraints.allowedSizes` 和 `constraints.excludedSizes` 都是選擇性的，但不能同時使用。 hello 清單中的可用大小由呼叫[清單的訂用帳戶可用的虛擬機器大小](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)。
- 必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。 它已用 toodetermine hello 硬體成本的 hello 虛擬機器。
- 第一方映像的 `imageReference` 會加以省略，但會提供給第三方映像。 它已用 hello 虛擬機器的 toodetermine hello 軟體成本。
- `count`是使用的 tooset hello 適當的乘數 hello 項目。 它支援靜態值 (例如 **2**)，或者另一個元素的動態值 (例如 `[steps('step1').vmCount]`)。 hello 預設值是**1**。

## <a name="sample-output"></a>範例輸出
```json
"Standard_D1"
```

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
