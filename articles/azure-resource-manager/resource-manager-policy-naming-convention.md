---
title: "如需命名慣例 aaaAzure 資源原則 |Microsoft 文件"
description: "描述資源命名慣例的 Azure Resource Manager 原則。"
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>為名稱和文字套用資源原則
本主題說明數個[資源原則](resource-manager-policy.md)可以套用 tooestablish 命名和文字的慣例。 這些原則可確保資源名稱和標籤值的一致性。 

## <a name="set-naming-convention-with-wildcard"></a>使用萬用字元設定命名慣例
hello 下列範例顯示 hello 的使用萬用字元，這會受到 hello**像**條件。 hello 條件狀態，是否 hello 名稱相符 hello 提及的模式 (namePrefix\*nameSuffix) 然後拒絕 hello 要求：

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>使用模式設定命名慣例

資源名稱比對模式中，使用 hello toospecify 符合條件。 hello 下列範例要求與名稱 toostart`contoso`而且包含六個其他字母：

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>設定標籤值的日期模式

toorequire 日期圖樣的兩個數字字元、 虛線、 三個字母、 虛線和四位數，使用：

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>後續步驟
* 定義原則規則 （如 hello 前面範例所示） 之後, 您會需要 toocreate hello 原則定義，並將它指派 tooa 範圍。 hello 領域可以訂用帳戶、 資源群組或資源。 tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。 tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。 
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

