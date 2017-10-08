---
title: "儲存體帳戶的 aaaAzure 資源原則 |Microsoft 文件"
description: "描述 Azure 資源管理員管理的儲存體帳戶的 hello 部署原則。"
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>適用於資源原則 toostorage 帳戶
本主題說明數個[資源原則](resource-manager-policy.md)可以套用 tooAzure 儲存體帳戶。 這些原則，確保您組織中部署的 hello 儲存體帳戶的一致性。 

## <a name="define-permitted-storage-account-types"></a>定義允許的儲存體帳戶類型

hello 下列原則會限制其[儲存體帳戶類型](../storage/common/storage-redundancy.md)可以部署：

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

類似的原則規則的參數，以便接受 hello 允許的 Sku 為可用的內建的原則定義。 hello 內建原則都有的資源識別碼 hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`。 

## <a name="define-permitted-access-tier"></a>定義允許的存取層

hello 下列原則指定 hello 類型[存取層](../storage/blobs/storage-blob-storage-tiers.md)可指定儲存體帳戶：

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a>請確定已啟用加密

hello 下列原則要求所有的儲存體帳戶 tooenable[儲存體服務加密](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

此原則規則，也可以為內建的原則定義與資源識別碼 hello `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`。

## <a name="next-steps"></a>後續步驟
* 定義原則規則 （如 hello 前面範例所示） 之後, 您會需要 toocreate hello 原則定義，並將它指派 tooa 範圍。 hello 領域可以訂用帳戶、 資源群組或資源。 tooassign 原則透過 hello 入口網站，請參閱[使用 Azure 入口網站 tooassign 和管理資源原則](resource-manager-policy-portal.md)。 tooassign 原則透過 REST API、 PowerShell 或 Azure CLI，請參閱[指派及管理透過指令碼的原則](resource-manager-policy-create-assign.md)。 
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

