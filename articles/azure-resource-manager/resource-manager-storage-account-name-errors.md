---
title: "Azure 儲存體帳戶名稱錯誤 | Microsoft Docs"
description: "描述當指定儲存體帳戶名稱時，可能會遇到的錯誤。"
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: support-article
ms.date: 09/13/2017
ms.author: tomfitz
ms.openlocfilehash: dc045827fbd38054a334ff22eb30e0db6a31bac8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="resolve-errors-for-storage-account-names"></a>解決儲存體帳戶名稱的錯誤

本文描述當部署儲存體帳戶時，可能會遇到的命名錯誤。

## <a name="symptom"></a>徵狀

如果您的儲存體帳戶名稱包含禁止的字元，您會收到如下的錯誤：

```
Code=AccountNameInvalid
Message=S!torageckrexph7isnoc is not a valid storage account name. Storage account name must be 
between 3 and 24 characters in length and use numbers and lower-case letters only.
```

對於儲存體帳戶，您必須提供在 Azure 中是唯一的資源名稱。 如果您未提供唯一的名稱，您會收到類似下列的錯誤：

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

如果您以與您的訂用帳戶中現有的儲存體帳戶相同的名稱部署儲存體帳戶，但提供不同的位置，您會遇到錯誤，指出儲存體帳戶已存在於不同的位置。 刪除現有的儲存體帳戶，或提供與現有儲存體帳戶相同的位置。

## <a name="cause"></a>原因

儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能使用數字和小寫字母。 名稱必須是唯一的。

## <a name="solution"></a>方案

### <a name="solution-1"></a>解決方案 1

請確定儲存體帳戶名稱是唯一的。 您可以將您的命名慣例與 [uniqueString](resource-group-template-functions-string.md#uniquestring) 函式的結果串連，以建立一個唯一名稱。

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

### <a name="solution-2"></a>解決方案 2

請確定您的儲存體帳戶名稱不超過 24 個字元。 [uniqueString](resource-group-template-functions-string.md#uniquestring) 函式會傳回 13 個字元。 如果您要對 **uniqueString** 結果串連前置詞或後置詞，請提供 11 個字元以下的值。

```json
"parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name."
      }
    }
}
```

### <a name="solution-3"></a>解決方案 3

請確定您的儲存體帳戶名稱不包含任何大寫字母或特殊字元。