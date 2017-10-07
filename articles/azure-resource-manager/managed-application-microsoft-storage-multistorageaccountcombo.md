---
title: "aaaAzure 受管理的應用程式 MultiStorageAccountCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Storage.MultiStorageAccountCombo UI 項目"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Microsoft.Storage.MultiStorageAccountCombo UI 元素
用來建立名稱以通用前置詞作為開頭的多個儲存體帳戶之控制項群組。 您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。

## <a name="ui-sample"></a>UI 範例
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>結構描述
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>備註
- hello 值`defaultValue.prefix`串連一或多個整數 toogenerate hello 序列的儲存體帳戶名稱。 例如，如果 `defaultValue.prefix` 為 **foobar** 且 `count` 為 **2**，就會產生 **foobar1** 和 **foobar2** 儲存體帳戶名稱。 會自動驗證所產生儲存體帳戶名稱的唯一性。
- hello 儲存體帳戶名稱產生辭典編纂順序根據`count`。 例如，如果`count`為 10、 則 hello 儲存體帳戶名稱的結尾 2 位數的整數 (01、 02、 03 中，等。)。
- hello 預設值為`defaultValue.prefix`是**null**，以及`defaultValue.type`是**Premium_LRS**。
- `constraints.allowedTypes` 中未指定的任何類型都會加以隱藏，`constraints.excludedTypes` 中未指定的任何類型都會加以顯示。
`constraints.allowedTypes` 和 `constraints.excludedTypes` 都是選擇性的，但不能同時使用。
- 在加法 toogenerating 儲存體帳戶名稱，`count`是使用的 tooset hello 項目的適當的乘數。 它支援靜態值 (例如 **2**)，或者另一個元素的動態值 (例如 `[steps('step1').storageAccountCount]`)。 hello 預設值是**1**。

## <a name="sample-output"></a>範例輸出
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>後續步驟
* 對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。
* 如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。
* 如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。
