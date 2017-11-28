---
title: "與 Azure 網路監看員安全性群組檢視 PowerShell aaaAnalyze 網路安全性 |Microsoft 文件"
description: "本文將說明如何 toouse PowerShell tooanalyze 的虛擬機器安全性與安全性的群組檢視。"
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
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="a8485-103">使用 PowerShell，利用安全性群組檢視分析虛擬機器的安全性</span><span class="sxs-lookup"><span data-stu-id="a8485-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a8485-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8485-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="a8485-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a8485-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="a8485-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a8485-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="a8485-107">REST API</span><span class="sxs-lookup"><span data-stu-id="a8485-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="a8485-108">安全性的群組檢視會傳回已設定且有效的網路安全性規則所套用的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a8485-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="a8485-109">這項功能會很有用的 tooaudit 及診斷網路安全性群組和 VM tooensure 流量所設定的規則已正確地允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="a8485-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="a8485-110">在本文中，我們會示範如何設定 tooretrieve hello 和有效的安全性規則 tooa 虛擬機器使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8485-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a8485-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="a8485-111">Before you begin</span></span>

<span data-ttu-id="a8485-112">在此案例中，您會執行 hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello 安全性規則資訊。</span><span class="sxs-lookup"><span data-stu-id="a8485-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="a8485-113">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="a8485-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="a8485-114">案例</span><span class="sxs-lookup"><span data-stu-id="a8485-114">Scenario</span></span>

<span data-ttu-id="a8485-115">hello 案例涵蓋在本文中擷取設定的 hello 和指定的虛擬機器的有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="a8485-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="a8485-116">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="a8485-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="a8485-117">hello 第一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="a8485-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="a8485-118">這個變數會傳遞 toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a8485-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="a8485-119">取得 VM</span><span class="sxs-lookup"><span data-stu-id="a8485-119">Get a VM</span></span>

<span data-ttu-id="a8485-120">虛擬機器為必要的 toorun hello`Get-AzureRmNetworkWatcherSecurityGroupView`針對 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a8485-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="a8485-121">下列範例中的 hello 取得 VM 物件。</span><span class="sxs-lookup"><span data-stu-id="a8485-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="a8485-122">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="a8485-122">Retrieve security group view</span></span>

<span data-ttu-id="a8485-123">hello 下一個步驟是 tooretrieve hello 安全性的群組檢視結果。</span><span class="sxs-lookup"><span data-stu-id="a8485-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="a8485-124">檢視 hello 結果</span><span class="sxs-lookup"><span data-stu-id="a8485-124">Viewing hello results</span></span>

<span data-ttu-id="a8485-125">hello 下列範例是縮短的回應 hello 傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="a8485-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="a8485-126">hello 結果會顯示所有 hello 有效且套用安全性規則 hello 細分的群組中的虛擬機器上**NetworkInterfaceSecurityRules**， **DefaultSecurityRules**，和**EffectiveSecurityRules**。</span><span class="sxs-lookup"><span data-stu-id="a8485-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a8485-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8485-127">Next steps</span></span>

<span data-ttu-id="a8485-128">請瀏覽[稽核網路安全性群組群組 (NSG) 與網路監看員](network-watcher-nsg-auditing-powershell.md)toolearn 如何 tooautomate 驗證的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="a8485-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


