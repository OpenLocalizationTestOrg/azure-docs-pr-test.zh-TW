---
title: "為網路安全性群組疑難排解 - 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站對 Azure Resource Manager 部署模型中的網路安全性群組進行疑難排解。"
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: f01d3b43a7953697a6b03e176dace33448d95cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="242a9-103">使用 Azure 入口網站為網路安全性群組疑難排解</span><span class="sxs-lookup"><span data-stu-id="242a9-103">Troubleshoot Network Security Groups using the Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="242a9-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="242a9-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="242a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="242a9-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="242a9-106">如果您在虛擬機器 (VM) 上設定網路安全性群組 (NSG) 卻遇到 VM 連線問題，本文提供診斷 NSG 功能的概觀以協助進一步進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="242a9-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs to help troubleshoot further.</span></span>

<span data-ttu-id="242a9-107">NSG 可讓您控制流入和流出虛擬機器 (VM) 的流量類型。</span><span class="sxs-lookup"><span data-stu-id="242a9-107">NSGs enable you to control the types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="242a9-108">您可對 Azure 虛擬網路 (VNet) 中的子網路、網路介面 (NIC) 或兩者套用 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-108">NSGs can be applied to subnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="242a9-109">對 NIC 套用的有效規則是對 NIC 套用的 NSG，以及對 NIC 所連線到的子網路套用的 NSG 兩者中的規則彙總的結果。</span><span class="sxs-lookup"><span data-stu-id="242a9-109">The effective rules applied to a NIC are an aggregation of the rules that exist in the NSGs applied to a NIC and the subnet it is connected to.</span></span> <span data-ttu-id="242a9-110">這些 NSG 的規則有時候會互相衝突，影響 VM 的網路連線。</span><span class="sxs-lookup"><span data-stu-id="242a9-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="242a9-111">您可以檢視 NSG 中對 VM NIC 套用的所有有效安全性規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-111">You can view all the effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="242a9-112">本文說明如何在 Azure Resource Manager 部署模型中使用這些規則對 VM 連線問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="242a9-112">This article shows how to troubleshoot VM connectivity issues using these rules in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="242a9-113">如果您不熟悉 VNet 與 NSG 的概念，請參閱[虛擬網路](virtual-networks-overview.md)和[網路安全性群組](virtual-networks-nsg.md)概觀文章。</span><span class="sxs-lookup"><span data-stu-id="242a9-113">If you're not familiar with VNet and NSG concepts, read the [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-to-troubleshoot-vm-traffic-flow"></a><span data-ttu-id="242a9-114">使用有效安全性規則對 VM 流量流程進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="242a9-114">Using Effective Security Rules to troubleshoot VM traffic flow</span></span>
<span data-ttu-id="242a9-115">下面的案例是常見的連線問題範例︰</span><span class="sxs-lookup"><span data-stu-id="242a9-115">The scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="242a9-116">一個名為 *VM1* 的 VM 位於 *WestUS-VNet1* VNet 內的 *Subnet1* 子網路。</span><span class="sxs-lookup"><span data-stu-id="242a9-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="242a9-117">嘗試使用 RDP over TCP 連接埠 3389 連線到 VM 時失敗。</span><span class="sxs-lookup"><span data-stu-id="242a9-117">An attempt to connect to the VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="242a9-118">在 NIC *VM1-NIC1* 和子網路 *Subnet1* 同時套用了 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-118">NSGs are applied at both the NIC *VM1-NIC1* and the subnet *Subnet1*.</span></span> <span data-ttu-id="242a9-119">與網路介面 *VM1-NIC1*相關聯的 NSG 中允許 TCP 連接埠 3389 的流量，不過 TCP Ping VM1 的連接埠 3389 失敗。</span><span class="sxs-lookup"><span data-stu-id="242a9-119">Traffic to TCP port 3389 is allowed in the NSG associated with the network interface *VM1-NIC1*, however TCP ping to VM1's port 3389 fails.</span></span>

<span data-ttu-id="242a9-120">雖然此範例使用 TCP 連接埠 3389，但是可以使用下列的步驟判斷任何連接埠的輸入和輸出連線失敗。</span><span class="sxs-lookup"><span data-stu-id="242a9-120">While this example uses TCP port 3389, the following steps can be used to determine inbound and outbound connection failures over any port.</span></span>

### <span data-ttu-id="242a9-121"><a name="vm"></a>檢視虛擬機器的有效安全性規則</span><span class="sxs-lookup"><span data-stu-id="242a9-121"><a name="vm"></a>View effective security rules for a virtual machine</span></span>
<span data-ttu-id="242a9-122">完成下列步驟對 VM 的 NSG 進行疑難排解：</span><span class="sxs-lookup"><span data-stu-id="242a9-122">Complete the following steps to troubleshoot NSGs for a VM:</span></span>

<span data-ttu-id="242a9-123">您可以從 VM 本身檢視 NIC 上完整的有效安全性規則清單。</span><span class="sxs-lookup"><span data-stu-id="242a9-123">You can view full list of the effective security rules on a NIC, from the VM itself.</span></span> <span data-ttu-id="242a9-124">如果您有權限，也可以從有效規則的刀鋒視窗新增、修改和刪除 NIC 和子網路的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-124">You can also add, modify, and delete both NIC and subnet NSG rules from the effective rules blade, if you have permissions to perform these operations.</span></span>

1. <span data-ttu-id="242a9-125">登入 Azure 入口網站，位址是 https://portal.azure.com。</span><span class="sxs-lookup"><span data-stu-id="242a9-125">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="242a9-126">按一下 [更多服務]，然後在出現的清單中按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="242a9-126">Click **More services**, then click **Virtual machines** in the list that appears.</span></span>
3. <span data-ttu-id="242a9-127">從出現的清單中選取要進行疑難排解的 VM，此時會出現一個有選項的 VM 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="242a9-127">Select a VM to troubleshoot from the list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="242a9-128">按一下 [診斷並解決問題]，然後選取常見的問題。</span><span class="sxs-lookup"><span data-stu-id="242a9-128">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="242a9-129">例如選取了 [我無法連接到我的 Windows VM]  。</span><span class="sxs-lookup"><span data-stu-id="242a9-129">For this example, **I can’t connect to my Windows VM** is selected.</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. <span data-ttu-id="242a9-130">在問題下方會出現步驟，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="242a9-130">Steps appear under the problem, as shown in the following picture:</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    <span data-ttu-id="242a9-131">按一下建議步驟清單中的 [有效安全性群組規則]  。</span><span class="sxs-lookup"><span data-stu-id="242a9-131">Click *effective security group rules* in the list of recommended steps.</span></span>
6. <span data-ttu-id="242a9-132">[取得有效的安全性規則]  刀鋒視窗隨即會出現，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="242a9-132">The **Get effective security rules** blade appears, as shown in the following picture:</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    <span data-ttu-id="242a9-133">請注意圖片的下列各區段︰</span><span class="sxs-lookup"><span data-stu-id="242a9-133">Notice the following sections of the picture:</span></span>
   
   * <span data-ttu-id="242a9-134">**範圍︰** 設定為在步驟 3 選取的 VM *VM1*。</span><span class="sxs-lookup"><span data-stu-id="242a9-134">**Scope:** Set to *VM1*, the VM selected in step 3.</span></span>
   * <span data-ttu-id="242a9-135">**網路介面︰** *VM1-NIC1* 。</span><span class="sxs-lookup"><span data-stu-id="242a9-135">**Network interface:** *VM1-NIC1* is selected.</span></span> <span data-ttu-id="242a9-136">一個 VM 可以有多個網路介面 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="242a9-136">A VM can have multiple network interfaces (NIC).</span></span> <span data-ttu-id="242a9-137">每個 NIC 只能有唯一的有效安全性規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-137">Each NIC can have unique effective security rules.</span></span> <span data-ttu-id="242a9-138">進行疑難排解時，您可能需要檢視每個 NIC 的有效安全性規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-138">When troubleshooting, you may need to view the effective security rules for each NIC.</span></span>
   * <span data-ttu-id="242a9-139">**相關聯的 NSG：** 可以對 NIC 和 NIC 所連線到的子網路兩者套用 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-139">**Associated NSGs:** NSGs can be applied to both the NIC and the subnet the NIC is connected to.</span></span> <span data-ttu-id="242a9-140">在圖片中，已經對 NIC 和所連線的子網路兩者套用 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-140">In the picture, an NSG has been applied to both the NIC and the subnet it's connected to.</span></span> <span data-ttu-id="242a9-141">您可以按一下 NSG 名稱來直接修改 NSG 中的規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-141">You can click on the NSG names to directly modify rules in the NSGs.</span></span>
   * <span data-ttu-id="242a9-142">**VM1-nsg 索引標籤︰** 圖片中顯示的規則清單是對 NIC 套用的 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-142">**VM1-nsg tab:** The list of rules displayed in the picture is for the NSG applied to the NIC.</span></span> <span data-ttu-id="242a9-143">每當建立一個 NSG 時，Azure 就會建立幾個預設的規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-143">Several default rules are created by Azure whenever an NSG is created.</span></span> <span data-ttu-id="242a9-144">您無法移除預設規則，但是可以使用較高優先順序的規則覆寫。</span><span class="sxs-lookup"><span data-stu-id="242a9-144">You can't remove the default rules, but you can override them with rules of higher priority.</span></span> <span data-ttu-id="242a9-145">若要深入了解預設規則，請閱讀 [NSG 概觀](virtual-networks-nsg.md#default-rules) 文章。</span><span class="sxs-lookup"><span data-stu-id="242a9-145">To learn more about default rules, read the [NSG overview](virtual-networks-nsg.md#default-rules) article.</span></span>
   * <span data-ttu-id="242a9-146">**DESTINATION 欄︰** 欄中某些規則有文字，而有些規則有位址首碼。</span><span class="sxs-lookup"><span data-stu-id="242a9-146">**DESTINATION column:** Some of the rules have text in the column, while others have address prefixes.</span></span> <span data-ttu-id="242a9-147">文字是在安全性規則建立時套用的預設標籤名稱。</span><span class="sxs-lookup"><span data-stu-id="242a9-147">The text is the name of default tags applied to the security rule when it was created.</span></span> <span data-ttu-id="242a9-148">標籤是系統提供的識別項，代表多個首碼。</span><span class="sxs-lookup"><span data-stu-id="242a9-148">The tags are system-provided identifiers that represent multiple prefixes.</span></span> <span data-ttu-id="242a9-149">選取有標籤的規則，例如 *AllowInternetOutBound* 會在 [位址首碼] 刀鋒視窗中列出首碼。</span><span class="sxs-lookup"><span data-stu-id="242a9-149">Selecting a rule with a tag, such as *AllowInternetOutBound*, lists the prefixes in the **Address prefixes** blade.</span></span>
   * <span data-ttu-id="242a9-150">**下載︰** 規則的清單可能很長。</span><span class="sxs-lookup"><span data-stu-id="242a9-150">**Download:** The list of rules can be long.</span></span> <span data-ttu-id="242a9-151">您可以按一下 [下載]  並儲存檔案，下載規則的 .csv 檔案供離線分析。</span><span class="sxs-lookup"><span data-stu-id="242a9-151">You can download a .csv file of the rules for offline analysis by clicking **Download** and saving the file.</span></span>
   * <span data-ttu-id="242a9-152">**AllowRDP** 輸入規則︰此規則允許透過 RDP 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="242a9-152">**AllowRDP** Inbound rule: This rule allows RDP connections to the VM.</span></span>
7. <span data-ttu-id="242a9-153">按一下 [Subnet1-NSG]  索引標籤可檢視對子網路套用的 NSG 有效規則，如下圖所示︰</span><span class="sxs-lookup"><span data-stu-id="242a9-153">Click the **Subnet1-NSG** tab to view the effective rules from the NSG applied to the subnet, as shown in the following picture:</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="242a9-154">請注意 *denyRDP* **輸入** 規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-154">Notice the *denyRDP* **Inbound** rule.</span></span> <span data-ttu-id="242a9-155">在網路介面套用規則之前，會先評估在子網路套用的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-155">Inbound rules applied at the subnet are evaluated before rules applied at the network interface.</span></span> <span data-ttu-id="242a9-156">由於在子網路套用了拒絕規則，而不會評估在 NIC 的允許規則，連線到 TCP 3389 的要求失敗。</span><span class="sxs-lookup"><span data-stu-id="242a9-156">Since the deny rule is applied at the subnet, the request to connect to TCP 3389 fails, because the allow rule at the NIC is never evaluated.</span></span> 
   
    <span data-ttu-id="242a9-157">*denyRDP* 規則是 RDP 連線失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="242a9-157">The *denyRDP* rule is the reason why the RDP connection is failing.</span></span> <span data-ttu-id="242a9-158">移除此規則應該可以解決問題。</span><span class="sxs-lookup"><span data-stu-id="242a9-158">Removing it should resolve the problem.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="242a9-159">如果與 NIC 相關聯的 VM 不在執行中，或者尚未對 NIC 或子網路套用 NSG，則不會顯示任何規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-159">If the VM associated with the NIC is not in a running state, or NSGs haven't been applied to the NIC or subnet, no rules are shown.</span></span>
   > 
   > 
8. <span data-ttu-id="242a9-160">若要編輯 NSG 規則，請在 [相關聯的 NSG] 區段中按一下 [Subnet1-NSG]。</span><span class="sxs-lookup"><span data-stu-id="242a9-160">To edit NSG rules, click *Subnet1-NSG* in the **Associated NSGs** section.</span></span>
   <span data-ttu-id="242a9-161">這會開啟 [Subnet1-NSG]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="242a9-161">This opens the **Subnet1-NSG** blade.</span></span> <span data-ttu-id="242a9-162">您可以按一下 [輸入安全性規則] ，直接編輯規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-162">You can directly edit the rules by clicking on **Inbound security rules**.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. <span data-ttu-id="242a9-163">在 [Subnet1-NSG] 中移除 *denyRDP* 輸入規則並加入 *allowRDP* 規則之後，有效規則清單看起來會類似下圖︰</span><span class="sxs-lookup"><span data-stu-id="242a9-163">After removing the *denyRDP* inbound rule in the **Subnet1-NSG** and adding an *allowRDP* rule, the effective rules list looks like the following picture:</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    <span data-ttu-id="242a9-164">開啟 VM 的 RDP 連線或使用 PsPing 工具，確認 TCP 連接埠 3389 已開啟。</span><span class="sxs-lookup"><span data-stu-id="242a9-164">Confirm that TCP port 3389 is open by opening an RDP connection to the VM or using the PsPing tool.</span></span> <span data-ttu-id="242a9-165">您可以閱讀 [PsPing 下載頁面](https://technet.microsoft.com/sysinternals/psping.aspx)進一步了解 PsPing。</span><span class="sxs-lookup"><span data-stu-id="242a9-165">You can learn more about PsPing by reading the [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx).</span></span>

### <span data-ttu-id="242a9-166"><a name="nic"></a>檢視網路介面的有效安全性規則</span><span class="sxs-lookup"><span data-stu-id="242a9-166"><a name="nic"></a>View effective security rules for a network interface</span></span>
<span data-ttu-id="242a9-167">如果您 VM 的流量流程因特定 NIC 而受到影響，可以完成下列步驟從網路介面內容檢視 NIC 的有效規則完整清單︰</span><span class="sxs-lookup"><span data-stu-id="242a9-167">If your VM traffic flow is impacted for a specific NIC, you can view a full list of the effective rules for the NIC from the network interfaces context by completing the following steps:</span></span>

1. <span data-ttu-id="242a9-168">登入 Azure 入口網站，位址是 https://portal.azure.com。</span><span class="sxs-lookup"><span data-stu-id="242a9-168">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="242a9-169">按一下 [更多服務]，然後在出現的清單中按一下 [網路介面]。</span><span class="sxs-lookup"><span data-stu-id="242a9-169">Click **More services**, then click **Network interfaces** in the list that appears.</span></span>
3. <span data-ttu-id="242a9-170">選取某個網路介面。</span><span class="sxs-lookup"><span data-stu-id="242a9-170">Select a network interface.</span></span> <span data-ttu-id="242a9-171">在下圖中選取了名為 *VM1-NIC1* 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="242a9-171">In the following picture, a NIC named *VM1-NIC1* is selected.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    <span data-ttu-id="242a9-172">請注意 [範圍]  已設為選取的網路介面。</span><span class="sxs-lookup"><span data-stu-id="242a9-172">Notice that the **Scope** is set to the network interface selected.</span></span> <span data-ttu-id="242a9-173">若要深入了解所顯示的其他資訊，請閱讀本文＜對 VM 的 NSG 進行疑難排解＞  一節的步驟 6。</span><span class="sxs-lookup"><span data-stu-id="242a9-173">To learn more about the additional information shown, read step 6 of the **Troubleshoot NSGs for a VM** section of this article.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="242a9-174">如果從網路介面移除 NSG，子網路 NSG 仍然會對指定的 NIC 有效。</span><span class="sxs-lookup"><span data-stu-id="242a9-174">If an NSG is removed from a network interface, the subnet NSG is still effective on the given NIC.</span></span> <span data-ttu-id="242a9-175">此時，輸出只會顯示子網路 NSG 的規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-175">In this case, the output would only show rules from the subnet NSG.</span></span> <span data-ttu-id="242a9-176">只有當 NIC 附加至 VM 時，規則才會出現。</span><span class="sxs-lookup"><span data-stu-id="242a9-176">Rules only appear if the NIC is attached to a VM.</span></span>
   > 
   > 
4. <span data-ttu-id="242a9-177">您可以直接編輯與 NIC 和子網路相關聯之 NSG 的規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-177">You can directly edit rules for NSGs associated with a NIC and a subnet.</span></span> <span data-ttu-id="242a9-178">若要了解如何進行，請閱讀＜檢視虛擬機器的有效安全性規則＞  一節的步驟 8。</span><span class="sxs-lookup"><span data-stu-id="242a9-178">To learn how, read step 8 of the **View effective security rules for a virtual machine** section of this article.</span></span>

## <span data-ttu-id="242a9-179"><a name="nsg"></a>檢視網路安全性群組 (NSG) 的有效安全性規則</span><span class="sxs-lookup"><span data-stu-id="242a9-179"><a name="nsg"></a>View effective security rules for a network security group (NSG)</span></span>
<span data-ttu-id="242a9-180">修改 NSG 規則時，可以檢閱特定 VM 上新增規則的影響。</span><span class="sxs-lookup"><span data-stu-id="242a9-180">When modifying NSG rules, you may want to review the impact of the rules being added on a particular VM.</span></span> <span data-ttu-id="242a9-181">您可以檢視套用指定 NSG 之所有 NIC 的完整有效安全性規則清單，而不必從指定的 NSG 刀鋒視窗切換內容。</span><span class="sxs-lookup"><span data-stu-id="242a9-181">You can view a full list of the effective security rules for all the NICs that a given NSG is applied to, without having to switch context from the given NSG blade.</span></span> <span data-ttu-id="242a9-182">若要對 NSG 中的有效規則進行疑難排解，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="242a9-182">To troubleshoot effective rules within an NSG, complete the following steps:</span></span>

1. <span data-ttu-id="242a9-183">登入 Azure 入口網站，位址是 https://portal.azure.com。</span><span class="sxs-lookup"><span data-stu-id="242a9-183">Login to the Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="242a9-184">按一下 [更多服務]，然後在出現的清單中按一下 [網路安全性群組]。</span><span class="sxs-lookup"><span data-stu-id="242a9-184">Click **More services**, then click **Network security groups** in the list that appears.</span></span>
3. <span data-ttu-id="242a9-185">選取某個 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-185">Select an NSG.</span></span> <span data-ttu-id="242a9-186">在下圖中選取了名為 VM1-nsg 的 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-186">In the following picture, an NSG named VM1-nsg was selected.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    <span data-ttu-id="242a9-187">請注意上圖的下列各區段︰</span><span class="sxs-lookup"><span data-stu-id="242a9-187">Notice the following sections of the previous picture:</span></span>
   
   * <span data-ttu-id="242a9-188">**範圍︰** 設定為選取的 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-188">**Scope:** Set to the NSG selected.</span></span>
   * <span data-ttu-id="242a9-189">**虛擬機器︰** 對子網路套用 NSG 時，會對連線到子網路的所有 VM 的所有網路介面套用。</span><span class="sxs-lookup"><span data-stu-id="242a9-189">**Virtual machine:** When an NSG is applied to a subnet, it's applied to all network interfaces attached to all VMs connected to the subnet.</span></span> <span data-ttu-id="242a9-190">此清單顯示套用此 NSG 的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="242a9-190">This list shows all VMs this NSG is applied to.</span></span> <span data-ttu-id="242a9-191">您可以從清單中選取任何 VM。</span><span class="sxs-lookup"><span data-stu-id="242a9-191">You can select any VM from the list.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="242a9-192">如果只對空白子網路套用 NSG，則不會列出 VM。</span><span class="sxs-lookup"><span data-stu-id="242a9-192">If an NSG is applied to only an empty subnet, VMs will not be listed.</span></span> <span data-ttu-id="242a9-193">如果對與 VM 無關的 NIC 套用 NSG，也不會列出這些 NIC。</span><span class="sxs-lookup"><span data-stu-id="242a9-193">If an NSG is applied to a NIC which is not associated with a VM, those NICs will also not be listed.</span></span> 
     > 
     > 
   * <span data-ttu-id="242a9-194">**網路介面：**一個 VM 可以有多個網路介面。</span><span class="sxs-lookup"><span data-stu-id="242a9-194">**Network Interface:** A VM can have multiple network interfaces.</span></span> <span data-ttu-id="242a9-195">您可以選取附加至所選 VM 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="242a9-195">You can select a network interface attached to the selected VM.</span></span>
   * <span data-ttu-id="242a9-196">**AssociatedNSGs：**一個 NIC 在任何時候最多可以有兩個有效的 NSG，一個套用到 NIC，一個套用到子網路。</span><span class="sxs-lookup"><span data-stu-id="242a9-196">**AssociatedNSGs:** At any time, a NIC can have up to two effective NSGs, one applied to the NIC and the other to the subnet.</span></span> <span data-ttu-id="242a9-197">雖然範圍選取了 VM1-nsg，但如果 NIC 有有效的子網路 NSG，輸出會顯示兩個 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-197">Although the scope is selected as VM1-nsg, if the NIC has an effective subnet NSG, the output will show both NSGs.</span></span>
4. <span data-ttu-id="242a9-198">您可以直接編輯與 NIC 或子網路相關聯之 NSG 的規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-198">You can directly edit rules for NSGs associated with a NIC or subnet.</span></span> <span data-ttu-id="242a9-199">若要了解如何進行，請閱讀＜檢視虛擬機器的有效安全性規則＞  一節的步驟 8。</span><span class="sxs-lookup"><span data-stu-id="242a9-199">To learn how, read step 8 of the **View effective security rules for a virtual machine** section of this article.</span></span>

<span data-ttu-id="242a9-200">若要深入了解所顯示的其他資訊，請閱讀本文＜檢視虛擬機器的有效安全性規則＞  一節的步驟 6。</span><span class="sxs-lookup"><span data-stu-id="242a9-200">To learn more about the additional information shown, read step 6 of the **View effective security rules for a virtual machine** section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="242a9-201">雖然子網路和 NIC 各只能套用一個 NSG，但是 NSG 可以與多個 NIC 和多個子網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="242a9-201">Though a subnet and NIC can each have only one NSG applied to them, an NSG can be associated to multiple NICs and multiple subnets.</span></span>
> 
> 

## <a name="considerations"></a><span data-ttu-id="242a9-202">考量</span><span class="sxs-lookup"><span data-stu-id="242a9-202">Considerations</span></span>
<span data-ttu-id="242a9-203">對連線問題進行疑難排解時，請考量下列幾點︰</span><span class="sxs-lookup"><span data-stu-id="242a9-203">Consider the following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="242a9-204">預設的 NSG 規則會封鎖來自網際網路的輸入存取，並只允許 VNet 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="242a9-204">Default NSG rules will block inbound access from the internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="242a9-205">必須視需要明確地新增規則，才能允許來自網際網路的輸入存取。</span><span class="sxs-lookup"><span data-stu-id="242a9-205">Rules should be explicitly added to allow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="242a9-206">如果沒有 NSG 安全性規則導致 VM 的網路連線失敗，則問題可能是來自於︰</span><span class="sxs-lookup"><span data-stu-id="242a9-206">If there are no NSG security rules causing a VM’s network connectivity to fail, the problem may be due to:</span></span>
  * <span data-ttu-id="242a9-207">VM 作業系統內執行的防火牆軟體</span><span class="sxs-lookup"><span data-stu-id="242a9-207">Firewall software running within the VM's operating system</span></span>
  * <span data-ttu-id="242a9-208">為虛擬設備或內部部署流量設定的路由。</span><span class="sxs-lookup"><span data-stu-id="242a9-208">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="242a9-209">網際網路流量可以透過強制通道重新導向至內部部署。</span><span class="sxs-lookup"><span data-stu-id="242a9-209">Internet traffic can be redirected to on-premises via forced-tunneling.</span></span> <span data-ttu-id="242a9-210">使用此設定時，根據內部部署網路硬體處理此流量的方式，從網際網路可能無法 RDP/SSH 連線到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="242a9-210">An RDP/SSH connection from the Internet to your VM may not work with this setting, depending on how the on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="242a9-211">閱讀 [對路由進行疑難排解](virtual-network-routes-troubleshoot-powershell.md) 文章，以了解如何診斷可能會妨礙流量進出 VM 的路由問題。</span><span class="sxs-lookup"><span data-stu-id="242a9-211">Read the [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article to learn how to diagnose route problems that may be impeding the flow of traffic in and out of the VM.</span></span> 
* <span data-ttu-id="242a9-212">如果您有對等互連的 VNet，VIRTUAL_NETWORK 標籤預設會自動展開以包含對等互連的 VNet 的首碼。</span><span class="sxs-lookup"><span data-stu-id="242a9-212">If you have peered VNets, by default, the VIRTUAL_NETWORK tag will automatically expand to include prefixes for peered VNets.</span></span> <span data-ttu-id="242a9-213">您可以在 **ExpandedAddressPrefix** 清單中檢視這些首碼，對任何與 VNet 對等互連連線相關的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="242a9-213">You can view these prefixes in the **ExpandedAddressPrefix** list, to troubleshoot any issues related to VNet peering connectivity.</span></span> 
* <span data-ttu-id="242a9-214">只有在有 NSG 與 VM 的 NIC 和/或子網路關聯時，才會顯示有效安全性規則。</span><span class="sxs-lookup"><span data-stu-id="242a9-214">Effective security rules are only shown if there is an NSG associated with the VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="242a9-215">如果沒有 NSG 與 NIC 或子網路相關聯，且您已對 VM 指派公用 IP 位址，則會開啟所有連接埠供輸入和輸出存取。</span><span class="sxs-lookup"><span data-stu-id="242a9-215">If there are no NSGs associated with the NIC or subnet and you have a public IP address assigned to your VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="242a9-216">如果 VM 有公用 IP 位址，強烈建議對 NIC 或子網路套用 NSG。</span><span class="sxs-lookup"><span data-stu-id="242a9-216">If the VM has a public IP address, applying NSGs to the NIC or subnet is strongly recommended.</span></span>

