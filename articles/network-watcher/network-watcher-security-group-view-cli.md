---
title: "使用 Azure 網路監看員安全性群組檢視分析網路安全性 - Azure CLI 2.0 | Microsoft Docs"
description: "本文會描述如何使用 Azure CLI 2.0，利用安全性群組檢視分析虛擬機器的安全性。"
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
ms.openlocfilehash: 1756e14819e3b7c79361c193413a1fcd7f24a4e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="757bf-103">使用 Azure CLI 2.0，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="757bf-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="757bf-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="757bf-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="757bf-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="757bf-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="757bf-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="757bf-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="757bf-107">REST API</span><span class="sxs-lookup"><span data-stu-id="757bf-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="757bf-108">安全性群組檢視會傳回套用至虛擬機器之已設定且有效的網路安全性規則。</span><span class="sxs-lookup"><span data-stu-id="757bf-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="757bf-109">這項功能可用來稽核及診斷 VM 所設定的網路安全性群組和規則，以確保會正確允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="757bf-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="757bf-110">在本文中，我們會說明如何使用 Azure CLI 來擷取虛擬機器所設定且有效的安全性規則</span><span class="sxs-lookup"><span data-stu-id="757bf-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>


<span data-ttu-id="757bf-111">本文使用資源管理部署模型的新一代 CLI：Azure CLI 2.0，它適用於 Windows、Mac 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="757bf-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="757bf-112">若要執行本文的步驟，您需要[安裝適用於 Mac、Linux 和 Windows 的 Azure 命令列介面 (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="757bf-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="757bf-113">開始之前</span><span class="sxs-lookup"><span data-stu-id="757bf-113">Before you begin</span></span>

<span data-ttu-id="757bf-114">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="757bf-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="757bf-115">案例</span><span class="sxs-lookup"><span data-stu-id="757bf-115">Scenario</span></span>

<span data-ttu-id="757bf-116">本文涵蓋的案例會擷取指定虛擬機器之已設定且有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="757bf-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="757bf-117">取得 VM</span><span class="sxs-lookup"><span data-stu-id="757bf-117">Get a VM</span></span>

<span data-ttu-id="757bf-118">必須有虛擬機器才能執行 `vm list` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="757bf-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="757bf-119">下列命令會列出資源群組中的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="757bf-119">The following command lists the virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="757bf-120">在知道虛擬機器後，您可以使用 `vm show` Cmdlet 來取得其資源識別碼︰</span><span class="sxs-lookup"><span data-stu-id="757bf-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="757bf-121">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="757bf-121">Retrieve security group view</span></span>

<span data-ttu-id="757bf-122">下一步是擷取安全性群組檢視的結果。</span><span class="sxs-lookup"><span data-stu-id="757bf-122">The next step is to retrieve the security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-the-results"></a><span data-ttu-id="757bf-123">檢視結果</span><span class="sxs-lookup"><span data-stu-id="757bf-123">Viewing the results</span></span>

<span data-ttu-id="757bf-124">下列範例是所傳回結果的縮短回應。</span><span class="sxs-lookup"><span data-stu-id="757bf-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="757bf-125">結果顯示虛擬機器上所有有效且套用的安全性規則，並細分為 **NetworkInterfaceSecurityRules**、**DefaultSecurityRules**和 **EffectiveSecurityRules** 群組。</span><span class="sxs-lookup"><span data-stu-id="757bf-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="757bf-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="757bf-126">Next steps</span></span>

<span data-ttu-id="757bf-127">請瀏覽[使用網路監看員稽核網路安全性群組 (NSG)](network-watcher-nsg-auditing-powershell.md) 以了解如何自動驗證網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="757bf-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="757bf-128">請瀏覽[安全性群組檢視概觀](network-watcher-security-group-view-overview.md)以深入了解套用到網路資源的安全性規則</span><span class="sxs-lookup"><span data-stu-id="757bf-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
