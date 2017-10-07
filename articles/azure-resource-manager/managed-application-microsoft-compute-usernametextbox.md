---
title: "aaaAzure 受管理的應用程式 UserNameTextBox UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Compute.UserNameTextBox UI 項目"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Microsoft.Compute.UserNameTextBox UI 元素
使用 Windows 和 Linux 使用者名稱內建驗證的文字方塊控制項。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a>備註
- 如果`constraints.required`設定得**true**，則 hello 文字方塊必須包含值 toovalidate 成功。 hello 預設值是**true**。
- 必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。
- `constraints.regex` 是 JavaScript 規則運算式模式。 如果指定，然後 hello 文字方塊的值必須符合 hello 模式 toovalidate 成功。 預設值為 **null**。
- `constraints.validationMessage`hello 文字方塊的值所指定的 hello 驗證失敗時，是字串 toodisplay `constraints.regex`。 如果未指定，則 hello 訊息在使用文字方塊中內建的驗證。 hello 預設值是**null**。
- 這個項目具有內建 hello 值指定為基礎的驗證`osPlatform`。 hello 內建的驗證可以搭配自訂的規則運算式。
值如果`constraints.regex`指定，則兩者 hello 內建和自訂驗證所觸發。

## <a name="sample-output"></a>範例輸出
```json
"tabrezm"
```

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
