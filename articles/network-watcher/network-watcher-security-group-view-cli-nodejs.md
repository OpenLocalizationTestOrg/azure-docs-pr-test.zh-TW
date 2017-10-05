---
title: "使用 Azure 網路監看員安全性群組檢視分析網路安全性 - Azure CLI 1.0 | Microsoft Docs"
description: "本文會描述如何使用 Azure CLI 1.0，利用安全性群組檢視分析虛擬機器的安全性。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="38cf7-103">使用 Azure CLI 1.0，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="38cf7-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="38cf7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38cf7-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="38cf7-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="38cf7-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="38cf7-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="38cf7-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="38cf7-107">REST API</span><span class="sxs-lookup"><span data-stu-id="38cf7-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="38cf7-108">安全性群組檢視會傳回套用至虛擬機器之已設定且有效的網路安全性規則。</span><span class="sxs-lookup"><span data-stu-id="38cf7-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="38cf7-109">這項功能可用來稽核及診斷 VM 所設定的網路安全性群組和規則，以確保會正確允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="38cf7-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="38cf7-110">在本文中，我們會說明如何使用 Azure CLI 來擷取虛擬機器所設定且有效的安全性規則</span><span class="sxs-lookup"><span data-stu-id="38cf7-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="38cf7-111">本文使用跨平台 Azure CLI 1.0，這適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="38cf7-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="38cf7-112">網路監看員目前使用 Azure CLI 1.0 提供 CLI 支援。</span><span class="sxs-lookup"><span data-stu-id="38cf7-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="38cf7-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="38cf7-113">Before you begin</span></span>

<span data-ttu-id="38cf7-114">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="38cf7-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="38cf7-115">案例</span><span class="sxs-lookup"><span data-stu-id="38cf7-115">Scenario</span></span>

<span data-ttu-id="38cf7-116">本文涵蓋的案例會擷取指定虛擬機器之已設定且有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="38cf7-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="38cf7-117">取得 VM</span><span class="sxs-lookup"><span data-stu-id="38cf7-117">Get a VM</span></span>

<span data-ttu-id="38cf7-118">必須有虛擬機器才能執行 `vm list` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="38cf7-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="38cf7-119">下列命令會列出資源群組中的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="38cf7-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="38cf7-120">在知道虛擬機器後，您可以使用 `vm show` Cmdlet 來取得其資源識別碼︰</span><span class="sxs-lookup"><span data-stu-id="38cf7-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="38cf7-121">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="38cf7-121">Retrieve security group view</span></span>

<span data-ttu-id="38cf7-122">下一步是擷取安全性群組檢視的結果。</span><span class="sxs-lookup"><span data-stu-id="38cf7-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="38cf7-123">新增 "--json" 旗標會將結果設為 json 格式。</span><span class="sxs-lookup"><span data-stu-id="38cf7-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="38cf7-124">檢視結果</span><span class="sxs-lookup"><span data-stu-id="38cf7-124">Viewing the results</span></span>

<span data-ttu-id="38cf7-125">下列範例是所傳回結果的縮短回應。</span><span class="sxs-lookup"><span data-stu-id="38cf7-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="38cf7-126">結果顯示虛擬機器上所有有效且套用的安全性規則，並細分為 **NetworkInterfaceSecurityRules**、**DefaultSecurityRules**和 **EffectiveSecurityRules** 群組。</span><span class="sxs-lookup"><span data-stu-id="38cf7-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="38cf7-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="38cf7-127">Next steps</span></span>

<span data-ttu-id="38cf7-128">請瀏覽[使用網路監看員稽核網路安全性群組 (NSG)](network-watcher-nsg-auditing-powershell.md) 以了解如何自動驗證網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="38cf7-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="38cf7-129">請瀏覽[安全性群組檢視概觀](network-watcher-security-group-view-overview.md)以深入了解套用到網路資源的安全性規則</span><span class="sxs-lookup"><span data-stu-id="38cf7-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
