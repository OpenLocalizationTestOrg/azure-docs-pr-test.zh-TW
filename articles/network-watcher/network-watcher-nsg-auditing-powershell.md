---
title: "使用 Azure 網路監看員安全性群組檢視自動化 NSG 稽核 | Microsoft Docs"
description: "此頁面說明如何設定網路安全性群組的稽核"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="3d979-103">使用 Azure 網路監看員安全性群組檢視自動化 NSG 稽核</span><span class="sxs-lookup"><span data-stu-id="3d979-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="3d979-104">客戶通常面臨難以驗證其基礎結構的安全性狀態之挑戰。</span><span class="sxs-lookup"><span data-stu-id="3d979-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="3d979-105">這項挑戰在其 Azure 中的 VM 沒有不同。</span><span class="sxs-lookup"><span data-stu-id="3d979-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="3d979-106">請務必根據套用的網路安全性群組 (NSG) 規則，具有類似的安全性設定檔。</span><span class="sxs-lookup"><span data-stu-id="3d979-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="3d979-107">您現在可以使用安全性群組檢視，取得套用到 NSG 中 VM 的規則清單。</span><span class="sxs-lookup"><span data-stu-id="3d979-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="3d979-108">您可以每週頻率定義黃金 NSG 安全性設定檔並起始安全性群組檢視，並比較輸出與標準設定檔且建立報告。</span><span class="sxs-lookup"><span data-stu-id="3d979-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="3d979-109">如此一來，您可以輕鬆識別不符合指定安全性設定檔規定的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="3d979-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="3d979-110">如果您不熟悉網路安全性群組，請造訪[網路安全性概觀](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="3d979-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3d979-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="3d979-111">Before you begin</span></span>

<span data-ttu-id="3d979-112">在此案例中，您可以比較已知的良好基準與針對虛擬機器傳回的安全性群組檢視結果。</span><span class="sxs-lookup"><span data-stu-id="3d979-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="3d979-113">此案例假設您已依照[建立網路監看員](network-watcher-create.md)中的步驟建立網路監看員。</span><span class="sxs-lookup"><span data-stu-id="3d979-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="3d979-114">此案例也假設已有具有有效虛擬機器的資源群組可供使用。</span><span class="sxs-lookup"><span data-stu-id="3d979-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="3d979-115">案例</span><span class="sxs-lookup"><span data-stu-id="3d979-115">Scenario</span></span>

<span data-ttu-id="3d979-116">本文章涵蓋的案例會取得虛擬機器的安全性群組檢視。</span><span class="sxs-lookup"><span data-stu-id="3d979-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="3d979-117">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="3d979-117">In this scenario, you will:</span></span>

- <span data-ttu-id="3d979-118">擷取已知的良好規則集</span><span class="sxs-lookup"><span data-stu-id="3d979-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="3d979-119">使用 REST API 擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="3d979-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="3d979-120">取得虛擬機器的安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="3d979-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="3d979-121">評估回應</span><span class="sxs-lookup"><span data-stu-id="3d979-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="3d979-122">擷取規則集</span><span class="sxs-lookup"><span data-stu-id="3d979-122">Retrieve rule set</span></span>

<span data-ttu-id="3d979-123">此範例中的第一個步驟是使用現有的基準。</span><span class="sxs-lookup"><span data-stu-id="3d979-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="3d979-124">下列範例是使用此範例中用作為基準的 `Get-AzureRmNetworkSecurityGroup` cmdlet，擷取自現有網路安全性小組的某些 JSON。</span><span class="sxs-lookup"><span data-stu-id="3d979-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="3d979-125">將規則集轉換成 PowerShell 物件</span><span class="sxs-lookup"><span data-stu-id="3d979-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="3d979-126">在此步驟中，我們會讀取稍早使用預期要在此範例的網路安全性群組上之規則建立的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="3d979-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="3d979-127">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="3d979-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="3d979-128">下一步是擷取網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="3d979-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="3d979-129">`$networkWatcher` 變數會傳遞至 `AzureRmNetworkWatcherSecurityGroupView` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3d979-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="3d979-130">取得 VM</span><span class="sxs-lookup"><span data-stu-id="3d979-130">Get a VM</span></span>

<span data-ttu-id="3d979-131">必須有虛擬機器才能執行 `Get-AzureRmNetworkWatcherSecurityGroupView` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3d979-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="3d979-132">下列範例會取得 VM 物件。</span><span class="sxs-lookup"><span data-stu-id="3d979-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="3d979-133">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="3d979-133">Retrieve security group view</span></span>

<span data-ttu-id="3d979-134">下一步是擷取安全性群組檢視的結果。</span><span class="sxs-lookup"><span data-stu-id="3d979-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="3d979-135">此結果會與稍早顯示的「基準」JSON 相比較。</span><span class="sxs-lookup"><span data-stu-id="3d979-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="3d979-136">分析結果</span><span class="sxs-lookup"><span data-stu-id="3d979-136">Analyzing the results</span></span>

<span data-ttu-id="3d979-137">回應會依網路介面群組。</span><span class="sxs-lookup"><span data-stu-id="3d979-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="3d979-138">所傳回的不同類型規則為有效及預設的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="3d979-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="3d979-139">結果會依子網路或虛擬 NIC 上的套用方式進一步細分。</span><span class="sxs-lookup"><span data-stu-id="3d979-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="3d979-140">下列 PowerShell 指令碼會比較安全性群組檢視與 NSG 現有輸出的結果。</span><span class="sxs-lookup"><span data-stu-id="3d979-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="3d979-141">下列範例是結果與 `Compare-Object` cmdlet 比較方式的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="3d979-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="3d979-142">以下是結果範例。</span><span class="sxs-lookup"><span data-stu-id="3d979-142">The following example is the result.</span></span> <span data-ttu-id="3d979-143">您可以看到第一個規則集中的兩個規則未出現在比較中。</span><span class="sxs-lookup"><span data-stu-id="3d979-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a><span data-ttu-id="3d979-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d979-144">Next steps</span></span>

<span data-ttu-id="3d979-145">如果設定已變更，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)以追蹤有問題的網路安全性群組和安全性規則。</span><span class="sxs-lookup"><span data-stu-id="3d979-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













