---
title: "在 Azure 中的 Linux VM 上使用原則強制執行安全性 | Microsoft Docs"
description: "如何將原則套用至 Azure Resource Manager Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 58eaab4fa03afc1e6a5e38bef691cce62a921ea9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="apply-policies-to-linux-vms-with-azure-resource-manager"></a><span data-ttu-id="449f5-103">使用 Azure Resource Manager 將原則套用至 Linux VM</span><span class="sxs-lookup"><span data-stu-id="449f5-103">Apply policies to Linux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="449f5-104">藉由使用原則，組織可以強制執行整個企業的各種慣例和規則。</span><span class="sxs-lookup"><span data-stu-id="449f5-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="449f5-105">強制執行所要的行為有助於降低風險，同時促進組織的成功。</span><span class="sxs-lookup"><span data-stu-id="449f5-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="449f5-106">我們會在本文中說明如何使用 Azure Resource Manager 原則來為您組織的虛擬機器定義所要的行為。</span><span class="sxs-lookup"><span data-stu-id="449f5-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="449f5-107">如需原則的簡介，請參閱 [使用原則來管理資源和控制存取](../../azure-resource-manager/resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="449f5-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="449f5-108">允許的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="449f5-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="449f5-109">若要確保您組織的虛擬機器與應用程式相容，您可以針對允許使用哪些作業系統設下限制。</span><span class="sxs-lookup"><span data-stu-id="449f5-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="449f5-110">您可以透過以下原則範例，允許只能建立 Ubuntu 14.04.2-LTS 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="449f5-110">In the following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines to be created.</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

<span data-ttu-id="449f5-111">使用萬用字元修改上述原則，來允許任何 Ubuntu LTS 映像：</span><span class="sxs-lookup"><span data-stu-id="449f5-111">Use a wild card to modify the preceding policy to allow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="449f5-112">如需原則欄位的相關資訊，請參閱[原則別名](../../azure-resource-manager/resource-manager-policy.md#aliases)。</span><span class="sxs-lookup"><span data-stu-id="449f5-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="449f5-113">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="449f5-113">Managed disks</span></span>

<span data-ttu-id="449f5-114">若要要求使用受控磁碟，請使用以下原則：</span><span class="sxs-lookup"><span data-stu-id="449f5-114">To require the use of managed disks, use the following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="449f5-115">虛擬機器的映像</span><span class="sxs-lookup"><span data-stu-id="449f5-115">Images for Virtual Machines</span></span>

<span data-ttu-id="449f5-116">基於安全性理由，您可以要求只在環境中部署已核准的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="449f5-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="449f5-117">您可以指定含有已核准映像的資源群組，或已核准的特定映像。</span><span class="sxs-lookup"><span data-stu-id="449f5-117">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="449f5-118">下列範例會從已核准的資源群組要求映像：</span><span class="sxs-lookup"><span data-stu-id="449f5-118">The following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="449f5-119">下列範例會指定已核准的映像識別碼：</span><span class="sxs-lookup"><span data-stu-id="449f5-119">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="449f5-120">虛擬機器延伸模組</span><span class="sxs-lookup"><span data-stu-id="449f5-120">Virtual Machine extensions</span></span>

<span data-ttu-id="449f5-121">您可能想要禁止使用某些類型的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="449f5-121">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="449f5-122">例如，一個延伸模組可能與某些自訂虛擬機器映像不相容。</span><span class="sxs-lookup"><span data-stu-id="449f5-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="449f5-123">下列範例示範如何封鎖特定延伸模組。</span><span class="sxs-lookup"><span data-stu-id="449f5-123">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="449f5-124">它利用發行者和類型來判斷要封鎖哪個延伸模組。</span><span class="sxs-lookup"><span data-stu-id="449f5-124">It uses publisher and type to determine which extension to block.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="449f5-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="449f5-125">Next steps</span></span>
* <span data-ttu-id="449f5-126">定義原則規則 (如上述範例所示) 之後，您必須建立原則定義，並將它指派到某個範圍。</span><span class="sxs-lookup"><span data-stu-id="449f5-126">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="449f5-127">範圍可以是訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="449f5-127">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="449f5-128">若要透過入口網站來指派原則，請參閱[使用 Azure 入口網站來指派和管理資源原則](../../azure-resource-manager/resource-manager-policy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="449f5-128">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="449f5-129">若要透過 REST API、PowerShell 或 Azure CLI 來指派原則，請參閱[透過指令碼來指派和管理原則](../../azure-resource-manager/resource-manager-policy-create-assign.md)。</span><span class="sxs-lookup"><span data-stu-id="449f5-129">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="449f5-130">如需資源原則的簡介，請參閱[資源原則概觀](../../azure-resource-manager/resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="449f5-130">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="449f5-131">如需關於企業如何使用 Resource Manager 有效地管理訂閱的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](../../azure-resource-manager/resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="449f5-131">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
