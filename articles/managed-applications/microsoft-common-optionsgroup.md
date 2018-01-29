---
title: "Azure 受管理的應用程式 OptionsGroup UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Common.OptionsGroup UI 元素"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 0ba820176e0231437e878922cb508cd3b97d46c3
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a>Microsoft.Common.OptionsGroup UI 元素
包含可用選項資料列的選取控制項。 您可以在[建立 Azure 受管理應用程式](publish-service-catalog-app.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a>備註
- `constraints.allowedValues` 的標籤是項目的顯示文字，其值為選取時的元素輸出值。
- 如果指定，預設值必須是 `constraints.allowedValues` 中存在的標籤。 如果未指定，依預設會選取 `constraints.allowedValues` 中的第一個項目。 預設值為 **null**。
- `constraints.allowedValues` 必須包含至少一個項目。
- 這個元素不支援 `constraints.required` 屬性；必須選取項目，才能順利通過驗證。

## <a name="sample-output"></a>範例輸出
```json
"Bar"
```

## <a name="next-steps"></a>後續步驟
* 如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](overview.md)。
* 如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](create-uidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](create-uidefinition-elements.md)。
