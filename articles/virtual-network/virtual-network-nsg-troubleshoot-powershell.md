---
title: "aaaTroubleshoot 網路安全性群組-PowerShell |Microsoft 文件"
description: "了解如何在 hello Azure Resource Manager 部署 tootroubleshoot 網路安全性群組的相關模型使用 Azure PowerShell。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="865d6-103">使用 Azure PowerShell 為網路安全性群組疑難排解</span><span class="sxs-lookup"><span data-stu-id="865d6-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="865d6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="865d6-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="865d6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="865d6-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="865d6-106">如果您在虛擬機器 (VM) 上設定網路安全性群組 (Nsg)，而遭遇 VM 連線問題，這篇文章會提供的 Nsg toohelp 進一步的疑難排解診斷功能的概觀。</span><span class="sxs-lookup"><span data-stu-id="865d6-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="865d6-107">Nsg 可讓您 toocontrol hello 類型的流量進出虛擬機器 (Vm) 的流程。</span><span class="sxs-lookup"><span data-stu-id="865d6-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="865d6-108">Nsg 可以套用的 toosubnets Azure 虛擬網路 (VNet)、 網路介面 (NIC)，或兩者。</span><span class="sxs-lookup"><span data-stu-id="865d6-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="865d6-109">hello 套用有效的規則 tooa NIC 是存在於 hello Nsg 套用 tooa NIC 和 hello 它連接至子網路中的 hello 規則的彙總。</span><span class="sxs-lookup"><span data-stu-id="865d6-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="865d6-110">這些 NSG 的規則有時候會互相衝突，影響 VM 的網路連線。</span><span class="sxs-lookup"><span data-stu-id="865d6-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="865d6-111">套用您的 VM Nic 上，您可以檢視 Nsg，從所有 hello 有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="865d6-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="865d6-112">本文示範如何使用這些規則在 tootroubleshoot VM 連線問題 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="865d6-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="865d6-113">如果您不熟悉 VNet 和 NSG 的概念，請參閱 hello[虛擬網路](virtual-networks-overview.md)和[網路安全性群組](virtual-networks-nsg.md)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="865d6-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="865d6-114">使用有效的安全性規則 tootroubleshoot VM 流量</span><span class="sxs-lookup"><span data-stu-id="865d6-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="865d6-115">常見的連接問題的範例，則 hello 案例所示：</span><span class="sxs-lookup"><span data-stu-id="865d6-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="865d6-116">一個名為 *VM1* 的 VM 位於 *WestUS-VNet1* VNet 內的 *Subnet1* 子網路。</span><span class="sxs-lookup"><span data-stu-id="865d6-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="865d6-117">嘗試 tooconnect toohello 透過 TCP 連接埠 3389 使用 RDP 的 VM 會失敗。</span><span class="sxs-lookup"><span data-stu-id="865d6-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="865d6-118">在這兩個 hello NIC 套用 Nsg *VM1 NIC1* hello 子網路和*Subnet1*。</span><span class="sxs-lookup"><span data-stu-id="865d6-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="865d6-119">Hello hello 網路介面相關聯的 NSG 中允許流量 tooTCP 連接埠 3389 *VM1 NIC1*，不過 TCP ping tooVM1 的連接埠 3389 失敗。</span><span class="sxs-lookup"><span data-stu-id="865d6-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="865d6-120">雖然這個範例會使用 TCP 連接埠 3389，hello 下列步驟可以使用的 toodetermine 透過任何連接埠是傳入和傳出的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="865d6-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="865d6-121">詳細的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="865d6-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="865d6-122">完成下列步驟 tootroubleshoot Nsg vm 的 hello:</span><span class="sxs-lookup"><span data-stu-id="865d6-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="865d6-123">啟動 Azure PowerShell 工作階段與登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="865d6-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="865d6-124">如果您不熟悉使用 Azure PowerShell，請參閱 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="865d6-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="865d6-125">輸入下列命令 tooreturn 所有 NSG 規則都套用 tooa NIC 名為 hello *VM1 NIC1* hello 資源群組中*RG1*:</span><span class="sxs-lookup"><span data-stu-id="865d6-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="865d6-126">如果您不知道 NIC hello 名稱，請輸入下列命令 tooretrieve hello 名稱的資源群組中的所有 Nic 的 hello:</span><span class="sxs-lookup"><span data-stu-id="865d6-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="865d6-127">hello 下列文字是針對 hello 傳回 hello 有效的規則輸出的範例*VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="865d6-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="865d6-128">請注意下列資訊 hello 輸出中的 hello:</span><span class="sxs-lookup"><span data-stu-id="865d6-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="865d6-129">有兩個 **NetworkSecurityGroup** 區段︰一個與子網路 (*Subnet1*) 相關聯，一個與 NIC (*VM1-NIC1*) 相關聯。</span><span class="sxs-lookup"><span data-stu-id="865d6-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="865d6-130">在此範例中，NSG 已套用的 tooeach。</span><span class="sxs-lookup"><span data-stu-id="865d6-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="865d6-131">**關聯**顯示 hello 資源 （子網路或 NIC） 指定的 NSG 與相關聯。</span><span class="sxs-lookup"><span data-stu-id="865d6-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="865d6-132">如果 hello NSG 資源移動/解除關聯執行此命令之前，您可能需要 toowait 幾秒鐘的時間以 hello 變更 tooreflect hello 命令輸出中。</span><span class="sxs-lookup"><span data-stu-id="865d6-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="865d6-133">hello 做為開頭的規則名稱*defaultSecurityRules*： 當 NSG 會建立，在其中建立數個預設安全性規則。</span><span class="sxs-lookup"><span data-stu-id="865d6-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="865d6-134">預設規則無法移除，但是可以較高優先順序的規則覆寫。</span><span class="sxs-lookup"><span data-stu-id="865d6-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="865d6-135">讀取 hello [NSG 概觀](virtual-networks-nsg.md#default-rules)深入了解 NSG 文章 toolearn 預設安全性規則。</span><span class="sxs-lookup"><span data-stu-id="865d6-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="865d6-136">**ExpandedAddressPrefix**展開 NSG 預設標記的 hello 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="865d6-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="865d6-137">標籤代表多個位址首碼。</span><span class="sxs-lookup"><span data-stu-id="865d6-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="865d6-138">從特定位址前置詞的 VM 連線進行疑難排解時，擴充的 hello 標記很有用。</span><span class="sxs-lookup"><span data-stu-id="865d6-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="865d6-139">例如，具有對等互連的 VNET，VIRTUAL_NETWORK 標記會展開 tooshow 所以 VNet hello 上述輸出中的前置詞。</span><span class="sxs-lookup"><span data-stu-id="865d6-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="865d6-140">NSG 相關聯的子網路、 NIC，或兩者是否 hello 命令只會顯示有效的規則。</span><span class="sxs-lookup"><span data-stu-id="865d6-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="865d6-141">一個 VM 可能有多個 NIC 分別套用不同的 NSG。</span><span class="sxs-lookup"><span data-stu-id="865d6-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="865d6-142">進行疑難排解時，執行每個 NIC hello 命令</span><span class="sxs-lookup"><span data-stu-id="865d6-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="865d6-143">tooease 覆寫較大的數字的 NSG 規則篩選輸入下列命令 tootroubleshoot 進一步 hello:</span><span class="sxs-lookup"><span data-stu-id="865d6-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="865d6-144">RDP 流量 （TCP 連接埠 3389），篩選條件是套用 toohello 方格檢視中，hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="865d6-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![規則清單](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="865d6-146">您可以看到 hello 方格檢視中，有同時允許與拒絕 rdp 的規則。</span><span class="sxs-lookup"><span data-stu-id="865d6-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="865d6-147">hello 步驟 2 中的輸出會顯示該 hello *DenyRDP*規則是在 hello NSG 套用 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="865d6-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="865d6-148">對於輸入規則，會先處理 Nsg 套用 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="865d6-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="865d6-149">如果找到相符項目，不會處理 hello NSG 套用 toohello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="865d6-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="865d6-150">在此情況下，hello *DenyRDP*從 hello 子網路的規則會封鎖 RDP toohello VM (**VM1**)。</span><span class="sxs-lookup"><span data-stu-id="865d6-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="865d6-151">VM 可能會有多個 Nic 附加的 tooit。</span><span class="sxs-lookup"><span data-stu-id="865d6-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="865d6-152">每個可能是連線的 tooa 不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="865d6-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="865d6-153">因為在 hello 先前步驟中的 hello 命令會針對 NIC 執行，很重要您指定的 tooensure hello 的 NIC 遇到 hello 連線失敗。</span><span class="sxs-lookup"><span data-stu-id="865d6-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="865d6-154">如果您不確定，您就可以針對每個連結 NIC toohello VM，一律執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="865d6-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="865d6-155">到 VM1，變更 hello tooRDP*拒絕 RDP (為 3389)*太規則*允許 RDP(3389)*在 hello **Subnet1 NSG** NSG。</span><span class="sxs-lookup"><span data-stu-id="865d6-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="865d6-156">確認開啟 RDP 連線 toohello VM，或使用 hello PsPing 工具開啟 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="865d6-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="865d6-157">您可以進一步了解 PsPing 讀取 hello [PsPing 下載頁面](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="865d6-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="865d6-158">您可以使用或移除規則從 NSG hello 資訊在 hello 輸出 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="865d6-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="865d6-159">考量</span><span class="sxs-lookup"><span data-stu-id="865d6-159">Considerations</span></span>
<span data-ttu-id="865d6-160">請考慮 hello 疑難排解連線問題時，下列點：</span><span class="sxs-lookup"><span data-stu-id="865d6-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="865d6-161">預設 NSG 規則將會封鎖從 hello 對內的存取網際網路和允許 VNet 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="865d6-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="865d6-162">規則應該明確加入 tooallow 輸入視需要從網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="865d6-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="865d6-163">如果沒有造成 VM 的網路連線 toofail NSG 安全性規則，hello 問題可能是因為：</span><span class="sxs-lookup"><span data-stu-id="865d6-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="865d6-164">Hello VM 作業系統內執行的防火牆軟體</span><span class="sxs-lookup"><span data-stu-id="865d6-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="865d6-165">為虛擬設備或內部部署流量設定的路由。</span><span class="sxs-lookup"><span data-stu-id="865d6-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="865d6-166">網際網路流量可以透過強制通道的重新導向的 tooon 單位。</span><span class="sxs-lookup"><span data-stu-id="865d6-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="865d6-167">RDP/SSH 連線從 hello 網際網路 tooyour VM 可能不適用於此設定，根據 hello 在內部部署網路硬體如何處理這個流量。</span><span class="sxs-lookup"><span data-stu-id="865d6-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="865d6-168">讀取 hello[疑難排解路由](virtual-network-routes-troubleshoot-powershell.md)文章 toolearn 如何 toodiagnose 路由問題，可能索性 hello 和出的流量傳送 hello VM。</span><span class="sxs-lookup"><span data-stu-id="865d6-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="865d6-169">如果您有所以 Vnet，根據預設，hello VIRTUAL_NETWORK 標記會自動擴展 tooinclude 前置詞所以 vnet。</span><span class="sxs-lookup"><span data-stu-id="865d6-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="865d6-170">您可以檢視這些前置詞中 hello **ExpandedAddressPrefix**清單，tootroubleshoot 對等互連連線問題相關 tooVNet。</span><span class="sxs-lookup"><span data-stu-id="865d6-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="865d6-171">有效的安全性規則只會顯示於是否有與 hello VM NIC 和或子網路的 NSG 相關聯。</span><span class="sxs-lookup"><span data-stu-id="865d6-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="865d6-172">如果沒有相關聯 hello NIC 的 Nsg 或子網路，而且您有指派 tooyour VM 的公用 IP 位址，所有連接埠將會開啟以供對內及對外存取。</span><span class="sxs-lookup"><span data-stu-id="865d6-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="865d6-173">如果 hello VM 的公用 IP 位址，強烈建議套用 Nsg toohello NIC 或子網路。</span><span class="sxs-lookup"><span data-stu-id="865d6-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

