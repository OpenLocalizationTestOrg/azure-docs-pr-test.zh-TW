---
title: "與 Azure 網路監看員安全性群組檢視 REST API aaaAnalyze 網路安全性 |Microsoft 文件"
description: "本文將說明如何 toouse PowerShell tooanalyze 的虛擬機器安全性與安全性的群組檢視。"
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
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="5a4db-103">使用 REST API，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="5a4db-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5a4db-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a4db-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="5a4db-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5a4db-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="5a4db-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5a4db-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="5a4db-107">REST API</span><span class="sxs-lookup"><span data-stu-id="5a4db-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="5a4db-108">安全性的群組檢視會傳回已設定且有效的網路安全性規則所套用的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a4db-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="5a4db-109">這項功能會很有用的 tooaudit 及診斷網路安全性群組和 VM tooensure 流量所設定的規則已正確地允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="5a4db-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="5a4db-110">在本文中，我們會示範 tooretrieve hello 有效且套用安全性規則使用 REST API tooa 虛擬機器的方式</span><span class="sxs-lookup"><span data-stu-id="5a4db-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5a4db-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="5a4db-111">Before you begin</span></span>

<span data-ttu-id="5a4db-112">在此案例中，您可以呼叫 hello 網路監看員 Rest API tooget hello 安全性的群組檢視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a4db-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="5a4db-113">ARMclient 是使用 PowerShell 的使用的 toocall hello REST API。</span><span class="sxs-lookup"><span data-stu-id="5a4db-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="5a4db-114">您可以在 chocolatey 的 [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient) 上找到 ARMClient</span><span class="sxs-lookup"><span data-stu-id="5a4db-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="5a4db-115">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="5a4db-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="5a4db-116">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="5a4db-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="5a4db-117">案例</span><span class="sxs-lookup"><span data-stu-id="5a4db-117">Scenario</span></span>

<span data-ttu-id="5a4db-118">hello 案例涵蓋在本文中擷取指定的虛擬機器的 hello 有效且套用安全性規則。</span><span class="sxs-lookup"><span data-stu-id="5a4db-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="5a4db-119">使用 ARMClient 登入</span><span class="sxs-lookup"><span data-stu-id="5a4db-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="5a4db-120">擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5a4db-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="5a4db-121">執行下列指令碼 tooreturn 虛擬 machineThe hello，下列程式碼需要變數：</span><span class="sxs-lookup"><span data-stu-id="5a4db-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="5a4db-122">**subscriptionId** -hello 訂用帳戶 id 也可以擷取與 hello **Get AzureRMSubscription** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5a4db-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="5a4db-123">**resourceGroupName** -hello 包含虛擬機器的資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="5a4db-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="5a4db-124">hello 所需的資訊為 hello**識別碼**hello 類型之下`Microsoft.Compute/virtualMachines`回應 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5a4db-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

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

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="5a4db-125">取得虛擬機器的安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="5a4db-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="5a4db-126">下列範例中的 hello 要求目標的虛擬機器的 hello 安全性的群組檢視。</span><span class="sxs-lookup"><span data-stu-id="5a4db-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="5a4db-127">這個範例中的 hello 結果可能是使用的 toocompare toohello 規則與安全性設定漂移 hello 原始 toolook 所定義。</span><span class="sxs-lookup"><span data-stu-id="5a4db-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

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

## <a name="view-hello-response"></a><span data-ttu-id="5a4db-128">檢視 hello 回應</span><span class="sxs-lookup"><span data-stu-id="5a4db-128">View hello response</span></span>

<span data-ttu-id="5a4db-129">下列範例中的 hello 是 hello 回應 hello 先前命令所傳回。</span><span class="sxs-lookup"><span data-stu-id="5a4db-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="5a4db-130">hello 結果會顯示所有 hello 有效且套用安全性規則 hello 細分的群組中的虛擬機器上**NetworkInterfaceSecurityRules**， **DefaultSecurityRules**，和**EffectiveSecurityRules**。</span><span class="sxs-lookup"><span data-stu-id="5a4db-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5a4db-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a4db-131">Next steps</span></span>

<span data-ttu-id="5a4db-132">請瀏覽[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-security-group-view-powershell.md)toolearn 如何 tooautomate 驗證的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5a4db-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


