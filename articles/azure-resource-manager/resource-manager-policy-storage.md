---
title: "儲存體帳戶的 Azure 資源原則 | Microsoft Docs"
description: "描述 Azure Resource Manager 管理儲存體帳戶部署的的原則。"
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
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="38b9d-103">將資源原則套用至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="38b9d-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="38b9d-104">本主題將示範數個您可以套用到 Azure 儲存體帳戶的[資源原則](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="38b9d-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="38b9d-105">這些原則可確保您組織中所部署之儲存體帳戶的一致性。</span><span class="sxs-lookup"><span data-stu-id="38b9d-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="38b9d-106">定義允許的儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="38b9d-106">Define permitted storage account types</span></span>

<span data-ttu-id="38b9d-107">下列原則會限制可部署的[儲存體帳戶類型](../storage/common/storage-redundancy.md)︰</span><span class="sxs-lookup"><span data-stu-id="38b9d-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="38b9d-108">包含接受允許 SKU 參數的類似原則規則可做為內建的原則定義。</span><span class="sxs-lookup"><span data-stu-id="38b9d-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="38b9d-109">內建的原則具有 `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1` 的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="38b9d-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="38b9d-110">定義允許的存取層</span><span class="sxs-lookup"><span data-stu-id="38b9d-110">Define permitted access tier</span></span>

<span data-ttu-id="38b9d-111">下列原則指定可針對儲存體帳戶指定的[存取層](../storage/blobs/storage-blob-storage-tiers.md)類型︰</span><span class="sxs-lookup"><span data-stu-id="38b9d-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="38b9d-112">請確定已啟用加密</span><span class="sxs-lookup"><span data-stu-id="38b9d-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="38b9d-113">下列原則要求所有儲存體帳戶啟用[儲存體服務加密](../storage/common/storage-service-encryption.md)：</span><span class="sxs-lookup"><span data-stu-id="38b9d-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="38b9d-114">此原則規則也可做為具有資源識別碼 `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f` 的內建原則定義。</span><span class="sxs-lookup"><span data-stu-id="38b9d-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38b9d-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38b9d-115">Next steps</span></span>
* <span data-ttu-id="38b9d-116">定義原則規則 (如上述範例所示) 之後，您必須建立原則定義，並將它指派到某個範圍。</span><span class="sxs-lookup"><span data-stu-id="38b9d-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="38b9d-117">範圍可以是訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="38b9d-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="38b9d-118">若要透過入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="38b9d-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="38b9d-119">若要透過 REST API、PowerShell 或 Azure CLI 來指派原則，請參閱[透過指令碼來指派和管理原則](resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="38b9d-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="38b9d-120">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="38b9d-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

