---
title: "使用 Azure 網路監看員安全性群組檢視分析網路安全性 - REST API | Microsoft Docs"
description: "本文會說明如何使用 PowerShell，利用安全性群組檢視分析虛擬機器的安全性。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="9dfc8-103">使用 REST API，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="9dfc8-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9dfc8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dfc8-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="9dfc8-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9dfc8-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="9dfc8-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9dfc8-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="9dfc8-107">REST API</span><span class="sxs-lookup"><span data-stu-id="9dfc8-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="9dfc8-108">安全性群組檢視會傳回套用至虛擬機器之已設定且有效的網路安全性規則。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="9dfc8-109">這項功能可用來稽核及診斷 VM 所設定的網路安全性群組和規則，以確保會正確允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="9dfc8-110">在本文中，我們會說明如何使用 REST API 來擷取有效且已套用至虛擬機器的安全性規則</span><span class="sxs-lookup"><span data-stu-id="9dfc8-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9dfc8-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="9dfc8-111">Before you begin</span></span>

<span data-ttu-id="9dfc8-112">在此案例中，您可以呼叫網路監看員 REST API 來取得的虛擬機器安全性群組檢視。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="9dfc8-113">使用 ARMclient 透過 PowerShell 呼叫 REST API。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="9dfc8-114">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="9dfc8-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="9dfc8-115">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="9dfc8-116">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="9dfc8-117">案例</span><span class="sxs-lookup"><span data-stu-id="9dfc8-117">Scenario</span></span>

<span data-ttu-id="9dfc8-118">本文涵蓋的案例會擷取有效且已套用指定虛擬機器的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="9dfc8-119">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="9dfc8-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="9dfc8-120">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9dfc8-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="9dfc8-121">執行下列程式碼以傳回虛擬機器。下列程式碼需要變數︰</span><span class="sxs-lookup"><span data-stu-id="9dfc8-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="9dfc8-122">**subscriptionId** - 也可使用 **Get-AzureRMSubscription** Cmdlet 來擷取訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="9dfc8-123">**resourceGroupName** - 包含虛擬機器的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="9dfc8-124">所需的資訊是回應中 `Microsoft.Compute/virtualMachines`類型下方的**識別碼**，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="9dfc8-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="9dfc8-125">取得虛擬機器的安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="9dfc8-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="9dfc8-126">下列範例會要求目標虛擬機器的安全性群組檢視。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="9dfc8-127">本範例的結果可用於比較依原始所定義的規則及安全性來尋找設定漂移。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a><span data-ttu-id="9dfc8-128">檢視回應</span><span class="sxs-lookup"><span data-stu-id="9dfc8-128">View the response</span></span>

<span data-ttu-id="9dfc8-129">下列範例是前述命令中所傳回的回應。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="9dfc8-130">結果顯示虛擬機器上所有有效且套用的安全性規則，並細分為 **NetworkInterfaceSecurityRules**、**DefaultSecurityRules**和 **EffectiveSecurityRules** 群組。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="9dfc8-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9dfc8-131">Next steps</span></span>

<span data-ttu-id="9dfc8-132">請瀏覽[使用網路監看員稽核網路安全性群組 (NSG)](network-watcher-security-group-view-powershell.md) 以了解如何自動驗證網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9dfc8-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


