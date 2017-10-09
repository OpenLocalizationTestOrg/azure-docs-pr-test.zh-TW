---
title: "aaaAzure 受管理應用程式文字方塊中的 UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.TextBox UI 項目"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI 元素
可以是使用的 tooedit 控制項未格式化的文字。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a>備註
- 如果`constraints.required`設定得**true**，則 hello 文字方塊必須包含值 toovalidate 成功。 hello 預設值是**false**。
- `constraints.regex` 是 JavaScript 規則運算式模式。 如果指定，然後 hello 文字方塊的值必須符合 hello 模式 toovalidate 成功。 預設值為 **null**。
- `constraints.validationMessage`時，字串 toodisplay hello 文字方塊的值無法通過驗證。 如果未指定，則 hello 訊息在使用文字方塊中內建的驗證。 hello 預設值是**null**。
- 它的可能 toospecify 值`constraints.regex`時`constraints.required`設定得**false**。 在此案例中，不需要值的 hello 文字方塊 toovalidate 成功。 如果有指定，它必須符合 hello 規則運算式模式。

## <a name="sample-output"></a>範例輸出

```json
"foobar"
```

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
