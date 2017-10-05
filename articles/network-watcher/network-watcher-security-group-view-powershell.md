---
title: "使用 Azure 網路監看員安全性群組檢視分析網路安全性 - PowerShell | Microsoft Docs"
description: "本文會說明如何使用 PowerShell，利用安全性群組檢視分析虛擬機器的安全性。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 363fdd9f1de933bb4050f91e1e111aaf3e419058
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="e8236-103">使用 PowerShell，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="e8236-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e8236-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8236-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="e8236-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e8236-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="e8236-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e8236-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="e8236-107">REST API</span><span class="sxs-lookup"><span data-stu-id="e8236-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="e8236-108">安全性群組檢視會傳回套用至虛擬機器之已設定且有效的網路安全性規則。</span><span class="sxs-lookup"><span data-stu-id="e8236-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="e8236-109">這項功能可用來稽核及診斷 VM 所設定的網路安全性群組和規則，以確保會正確允許或拒絕流量。</span><span class="sxs-lookup"><span data-stu-id="e8236-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="e8236-110">在本文中，我們會說明如何使用 PowerShell 來擷取虛擬機器所設定且有效的安全性規則</span><span class="sxs-lookup"><span data-stu-id="e8236-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e8236-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="e8236-111">Before you begin</span></span>

<span data-ttu-id="e8236-112">在此案例中，您會執行 `Get-AzureRmNetworkWatcherSecurityGroupView` Cmdlet 來擷取安全性規則資訊。</span><span class="sxs-lookup"><span data-stu-id="e8236-112">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="e8236-113">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="e8236-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="e8236-114">案例</span><span class="sxs-lookup"><span data-stu-id="e8236-114">Scenario</span></span>

<span data-ttu-id="e8236-115">本文涵蓋的案例會擷取指定虛擬機器之已設定且有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="e8236-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="e8236-116">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="e8236-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="e8236-117">第一步是擷取網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="e8236-117">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="e8236-118">此變數會傳遞至 `Get-AzureRmNetworkWatcherSecurityGroupView` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e8236-118">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="e8236-119">取得 VM</span><span class="sxs-lookup"><span data-stu-id="e8236-119">Get a VM</span></span>

<span data-ttu-id="e8236-120">必須有虛擬機器才能執行 `Get-AzureRmNetworkWatcherSecurityGroupView` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e8236-120">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="e8236-121">下列範例會取得 VM 物件。</span><span class="sxs-lookup"><span data-stu-id="e8236-121">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="e8236-122">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="e8236-122">Retrieve security group view</span></span>

<span data-ttu-id="e8236-123">下一步是擷取安全性群組檢視的結果。</span><span class="sxs-lookup"><span data-stu-id="e8236-123">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="e8236-124">檢視結果</span><span class="sxs-lookup"><span data-stu-id="e8236-124">Viewing the results</span></span>

<span data-ttu-id="e8236-125">下列範例是所傳回結果的縮短回應。</span><span class="sxs-lookup"><span data-stu-id="e8236-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="e8236-126">結果顯示虛擬機器上所有有效且套用的安全性規則，並細分為 **NetworkInterfaceSecurityRules**、**DefaultSecurityRules**和 **EffectiveSecurityRules** 群組。</span><span class="sxs-lookup"><span data-stu-id="e8236-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="e8236-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8236-127">Next steps</span></span>

<span data-ttu-id="e8236-128">請瀏覽[使用網路監看員稽核網路安全性群組 (NSG)](network-watcher-nsg-auditing-powershell.md) 以了解如何自動驗證網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e8236-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


