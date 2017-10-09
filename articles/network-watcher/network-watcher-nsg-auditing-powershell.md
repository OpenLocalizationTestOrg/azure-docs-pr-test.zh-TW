---
title: "使用 Azure 網路監看員安全性的群組檢視稽核的 aaaAutomate NSG |Microsoft 文件"
description: "此頁面提供有關指示 tooconfigure 稽核的網路安全性群組"
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
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="17501-103">使用 Azure 網路監看員安全性群組檢視自動化 NSG 稽核</span><span class="sxs-lookup"><span data-stu-id="17501-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="17501-104">客戶通常會面對 hello 挑戰的驗證基礎結構的 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="17501-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="17501-105">這項挑戰在其 Azure 中的 VM 沒有不同。</span><span class="sxs-lookup"><span data-stu-id="17501-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="17501-106">很重要的 toohave 類似的安全性設定檔為基礎套用 hello 網路安全性群組 (NSG) 規則。</span><span class="sxs-lookup"><span data-stu-id="17501-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="17501-107">使用 hello 安全性的群組檢視，您現在可以取得 hello 套用規則 tooa NSG 中的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="17501-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="17501-108">您可以定義標準的 NSG 安全性設定檔並起始以每週的步調安全性的群組檢視和比較 hello 輸出 toohello 標準設定檔和建立報表。</span><span class="sxs-lookup"><span data-stu-id="17501-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="17501-109">如此一來您可以識別就能輕鬆所有不符合規定的安全性設定檔的 toohello hello Vm。</span><span class="sxs-lookup"><span data-stu-id="17501-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="17501-110">如果您不熟悉網路安全性群組，請造訪[網路安全性概觀](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="17501-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17501-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="17501-111">Before you begin</span></span>

<span data-ttu-id="17501-112">在此案例中，您可以比較已知的理想基準 toohello 安全性群組檢視虛擬機器所傳回的結果。</span><span class="sxs-lookup"><span data-stu-id="17501-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="17501-113">此案例假設您已依照中的 hello 步驟[建立網路監看員](network-watcher-create.md)toocreate 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="17501-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="17501-114">hello 案例也會假設具有有效的虛擬機器的資源群組存在 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="17501-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="17501-115">案例</span><span class="sxs-lookup"><span data-stu-id="17501-115">Scenario</span></span>

<span data-ttu-id="17501-116">本文涵蓋的 hello 案例取得 hello 安全性的群組檢視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="17501-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="17501-117">在此案例中，您將會：</span><span class="sxs-lookup"><span data-stu-id="17501-117">In this scenario, you will:</span></span>

- <span data-ttu-id="17501-118">擷取已知的良好規則集</span><span class="sxs-lookup"><span data-stu-id="17501-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="17501-119">使用 REST API 擷取虛擬機器</span><span class="sxs-lookup"><span data-stu-id="17501-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="17501-120">取得虛擬機器的安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="17501-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="17501-121">評估回應</span><span class="sxs-lookup"><span data-stu-id="17501-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="17501-122">擷取規則集</span><span class="sxs-lookup"><span data-stu-id="17501-122">Retrieve rule set</span></span>

<span data-ttu-id="17501-123">在此範例中的 hello 第一個步驟是 toowork 與現有的基準。</span><span class="sxs-lookup"><span data-stu-id="17501-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="17501-124">hello 下列範例是擷取自現有網路安全性群組使用 hello 某些 json `Get-AzureRmNetworkSecurityGroup` hello 基準為用於此範例中的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17501-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

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

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="17501-125">轉換規則集 tooPowerShell 物件</span><span class="sxs-lookup"><span data-stu-id="17501-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="17501-126">在此步驟中，我們正在閱讀的 hello 規則，會在此範例中的 hello 網路安全性群組的預期的 toobe 稍早建立的 json 檔案。</span><span class="sxs-lookup"><span data-stu-id="17501-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="17501-127">擷取網路監看員</span><span class="sxs-lookup"><span data-stu-id="17501-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="17501-128">hello 下一個步驟是 tooretrieve hello 網路監看員執行個體。</span><span class="sxs-lookup"><span data-stu-id="17501-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="17501-129">hello`$networkWatcher`變數傳遞 toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17501-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="17501-130">取得 VM</span><span class="sxs-lookup"><span data-stu-id="17501-130">Get a VM</span></span>

<span data-ttu-id="17501-131">虛擬機器為必要的 toorun hello`Get-AzureRmNetworkWatcherSecurityGroupView`針對 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17501-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="17501-132">下列範例中的 hello 取得 VM 物件。</span><span class="sxs-lookup"><span data-stu-id="17501-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="17501-133">擷取安全性群組檢視</span><span class="sxs-lookup"><span data-stu-id="17501-133">Retrieve security group view</span></span>

<span data-ttu-id="17501-134">hello 下一個步驟是 tooretrieve hello 安全性的群組檢視結果。</span><span class="sxs-lookup"><span data-stu-id="17501-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="17501-135">這個結果會是比較的 toohello 稍早顯示的 「 數基準 」 json。</span><span class="sxs-lookup"><span data-stu-id="17501-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="17501-136">分析 hello 結果</span><span class="sxs-lookup"><span data-stu-id="17501-136">Analyzing hello results</span></span>

<span data-ttu-id="17501-137">hello 回應分組依據的網路介面。</span><span class="sxs-lookup"><span data-stu-id="17501-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="17501-138">hello 不同類型傳回的規則會生效，且預設安全性規則。</span><span class="sxs-lookup"><span data-stu-id="17501-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="17501-139">hello 結果進一步細分由及其套用方式，在子網路或虛擬 nic。</span><span class="sxs-lookup"><span data-stu-id="17501-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="17501-140">hello 下列 PowerShell 指令碼比較 hello hello NSG 的安全性的群組檢視 tooan 現有輸出結果。</span><span class="sxs-lookup"><span data-stu-id="17501-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="17501-141">hello 下列範例是簡單的範例的方式比較 hello 結果與`Compare-Object`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="17501-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="17501-142">下列範例中的 hello 是 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="17501-142">hello following example is hello result.</span></span> <span data-ttu-id="17501-143">您可以看到兩個已 hello 第一個規則集合中的 hello 規則沒有出現在 hello 比較。</span><span class="sxs-lookup"><span data-stu-id="17501-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="17501-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17501-144">Next steps</span></span>

<span data-ttu-id="17501-145">如果設定已變更，請參閱[管理網路安全性群組](../virtual-network/virtual-network-manage-nsg-arm-portal.md)tootrack 向 hello 網路安全性群組和安全性規則，會有問題。</span><span class="sxs-lookup"><span data-stu-id="17501-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













