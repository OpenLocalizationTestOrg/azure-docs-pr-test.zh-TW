---
title: "aaaTroubleshoot 網路安全性群組-入口網站 |Microsoft 文件"
description: "了解如何在 hello Azure Resource Manager 部署 tootroubleshoot 網路安全性群組的相關模型使用 hello Azure 入口網站。"
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
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="216b3-103">疑難排解使用 hello Azure 入口網站的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="216b3-103">Troubleshoot Network Security Groups using hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="216b3-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="216b3-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="216b3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="216b3-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="216b3-106">如果您在虛擬機器 (VM) 上設定網路安全性群組 (Nsg)，而遭遇 VM 連線問題，這篇文章會提供的 Nsg toohelp 進一步的疑難排解診斷功能的概觀。</span><span class="sxs-lookup"><span data-stu-id="216b3-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="216b3-107">Nsg 可讓您 toocontrol hello 類型的流量進出虛擬機器 (Vm) 的流程。</span><span class="sxs-lookup"><span data-stu-id="216b3-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="216b3-108">Nsg 可以套用的 toosubnets Azure 虛擬網路 (VNet)、 網路介面 (NIC)，或兩者。</span><span class="sxs-lookup"><span data-stu-id="216b3-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="216b3-109">hello 套用有效的規則 tooa NIC 是存在於 hello Nsg 套用 tooa NIC 和 hello 它連接至子網路中的 hello 規則的彙總。</span><span class="sxs-lookup"><span data-stu-id="216b3-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="216b3-110">這些 NSG 的規則有時候會互相衝突，影響 VM 的網路連線。</span><span class="sxs-lookup"><span data-stu-id="216b3-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="216b3-111">套用您的 VM Nic 上，您可以檢視 Nsg，從所有 hello 有效的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="216b3-112">本文示範如何使用這些規則在 tootroubleshoot VM 連線問題 hello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="216b3-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="216b3-113">如果您不熟悉 VNet 和 NSG 的概念，請參閱 hello[虛擬網路](virtual-networks-overview.md)和[網路安全性群組](virtual-networks-nsg.md)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="216b3-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="216b3-114">使用有效的安全性規則 tootroubleshoot VM 流量</span><span class="sxs-lookup"><span data-stu-id="216b3-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="216b3-115">常見的連接問題的範例，則 hello 案例所示：</span><span class="sxs-lookup"><span data-stu-id="216b3-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="216b3-116">一個名為 *VM1* 的 VM 位於 *WestUS-VNet1* VNet 內的 *Subnet1* 子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="216b3-117">嘗試 tooconnect toohello 透過 TCP 連接埠 3389 使用 RDP 的 VM 會失敗。</span><span class="sxs-lookup"><span data-stu-id="216b3-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="216b3-118">在這兩個 hello NIC 套用 Nsg *VM1 NIC1* hello 子網路和*Subnet1*。</span><span class="sxs-lookup"><span data-stu-id="216b3-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="216b3-119">Hello hello 網路介面相關聯的 NSG 中允許流量 tooTCP 連接埠 3389 *VM1 NIC1*，不過 TCP ping tooVM1 的連接埠 3389 失敗。</span><span class="sxs-lookup"><span data-stu-id="216b3-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="216b3-120">雖然這個範例會使用 TCP 連接埠 3389，hello 下列步驟可以使用的 toodetermine 透過任何連接埠是傳入和傳出的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="216b3-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

### <span data-ttu-id="216b3-121"><a name="vm"></a>檢視虛擬機器的有效安全性規則</span><span class="sxs-lookup"><span data-stu-id="216b3-121"><a name="vm"></a>View effective security rules for a virtual machine</span></span>
<span data-ttu-id="216b3-122">完成下列步驟 tootroubleshoot Nsg vm 的 hello:</span><span class="sxs-lookup"><span data-stu-id="216b3-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

<span data-ttu-id="216b3-123">您可以從 hello VM 本身的 NIC 上檢視 hello 有效的安全性規則的完整的清單。</span><span class="sxs-lookup"><span data-stu-id="216b3-123">You can view full list of hello effective security rules on a NIC, from hello VM itself.</span></span> <span data-ttu-id="216b3-124">您也可以新增、 修改及刪除 hello 有效的規則刀鋒視窗中，從子網路和 NIC 的 NSG 規則，如果您有權限 tooperform 這些作業。</span><span class="sxs-lookup"><span data-stu-id="216b3-124">You can also add, modify, and delete both NIC and subnet NSG rules from hello effective rules blade, if you have permissions tooperform these operations.</span></span>

1. <span data-ttu-id="216b3-125">登入 toohello https://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="216b3-125">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="216b3-126">按一下**更多服務**，然後按一下 **虛擬機器**hello 的清單中，會出現。</span><span class="sxs-lookup"><span data-stu-id="216b3-126">Click **More services**, then click **Virtual machines** in hello list that appears.</span></span>
3. <span data-ttu-id="216b3-127">從出現的 hello 清單中選取 VM tootroubleshoot 和選項的 VM 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="216b3-127">Select a VM tootroubleshoot from hello list that appears and a VM blade with options appears.</span></span>
4. <span data-ttu-id="216b3-128">按一下 [診斷並解決問題]，然後選取常見的問題。</span><span class="sxs-lookup"><span data-stu-id="216b3-128">Click **Diagnose & solve problems** and then select a common problem.</span></span> <span data-ttu-id="216b3-129">例如，**我無法連線 toomy Windows VM**已選取。</span><span class="sxs-lookup"><span data-stu-id="216b3-129">For this example, **I can’t connect toomy Windows VM** is selected.</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. <span data-ttu-id="216b3-130">Hello 下列圖片所示步驟就會出現在 hello 問題：</span><span class="sxs-lookup"><span data-stu-id="216b3-130">Steps appear under hello problem, as shown in hello following picture:</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    <span data-ttu-id="216b3-131">按一下*有效安全性群組規則*在 hello 清單中的建議步驟。</span><span class="sxs-lookup"><span data-stu-id="216b3-131">Click *effective security group rules* in hello list of recommended steps.</span></span>
6. <span data-ttu-id="216b3-132">hello**取得有效的安全性規則**刀鋒視窗隨即出現，如 hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="216b3-132">hello **Get effective security rules** blade appears, as shown in hello following picture:</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    <span data-ttu-id="216b3-133">請注意下列各節 hello 圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="216b3-133">Notice hello following sections of hello picture:</span></span>
   
   * <span data-ttu-id="216b3-134">**範圍：**設定得*VM1*，hello 在步驟 3 中選取的 VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-134">**Scope:** Set too*VM1*, hello VM selected in step 3.</span></span>
   * <span data-ttu-id="216b3-135">**網路介面︰** *VM1-NIC1* 。</span><span class="sxs-lookup"><span data-stu-id="216b3-135">**Network interface:** *VM1-NIC1* is selected.</span></span> <span data-ttu-id="216b3-136">一個 VM 可以有多個網路介面 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="216b3-136">A VM can have multiple network interfaces (NIC).</span></span> <span data-ttu-id="216b3-137">每個 NIC 只能有唯一的有效安全性規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-137">Each NIC can have unique effective security rules.</span></span> <span data-ttu-id="216b3-138">進行疑難排解時，您可能需要 tooview hello 有效的安全性規則的每個 nic。</span><span class="sxs-lookup"><span data-stu-id="216b3-138">When troubleshooting, you may need tooview hello effective security rules for each NIC.</span></span>
   * <span data-ttu-id="216b3-139">**關聯 Nsg:** Nsg 可以套用的 tooboth hello NIC 和 hello 子網路 hello NIC 連線到。</span><span class="sxs-lookup"><span data-stu-id="216b3-139">**Associated NSGs:** NSGs can be applied tooboth hello NIC and hello subnet hello NIC is connected to.</span></span> <span data-ttu-id="216b3-140">Hello 圖片中 NSG 已套用的 tooboth hello NIC 和 hello 它連接至子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-140">In hello picture, an NSG has been applied tooboth hello NIC and hello subnet it's connected to.</span></span> <span data-ttu-id="216b3-141">您可以按一下 hello NSG 名稱 toodirectly 修改 hello Nsg 中的規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-141">You can click on hello NSG names toodirectly modify rules in hello NSGs.</span></span>
   * <span data-ttu-id="216b3-142">**VM1 nsg 索引標籤：** hello hello 圖片中顯示的規則清單是 hello NSG 套用 toohello nic。</span><span class="sxs-lookup"><span data-stu-id="216b3-142">**VM1-nsg tab:** hello list of rules displayed in hello picture is for hello NSG applied toohello NIC.</span></span> <span data-ttu-id="216b3-143">每當建立一個 NSG 時，Azure 就會建立幾個預設的規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-143">Several default rules are created by Azure whenever an NSG is created.</span></span> <span data-ttu-id="216b3-144">您無法移除 hello 預設規則，但您可以使用較高優先順序的規則覆寫它們。</span><span class="sxs-lookup"><span data-stu-id="216b3-144">You can't remove hello default rules, but you can override them with rules of higher priority.</span></span> <span data-ttu-id="216b3-145">深入了解預設規則，讀取 hello toolearn [NSG 概觀](virtual-networks-nsg.md#default-rules)發行項。</span><span class="sxs-lookup"><span data-stu-id="216b3-145">toolearn more about default rules, read hello [NSG overview](virtual-networks-nsg.md#default-rules) article.</span></span>
   * <span data-ttu-id="216b3-146">**目的地資料行：**一些 hello 規則有文字 hello 資料行中，而有些則擁有位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="216b3-146">**DESTINATION column:** Some of hello rules have text in hello column, while others have address prefixes.</span></span> <span data-ttu-id="216b3-147">hello 文字時建立 hello 預設標籤套用 toohello 安全性規則名稱。</span><span class="sxs-lookup"><span data-stu-id="216b3-147">hello text is hello name of default tags applied toohello security rule when it was created.</span></span> <span data-ttu-id="216b3-148">hello 標記是系統提供的識別碼，代表多個前置詞。</span><span class="sxs-lookup"><span data-stu-id="216b3-148">hello tags are system-provided identifiers that represent multiple prefixes.</span></span> <span data-ttu-id="216b3-149">選取的規則與標記，例如*AllowInternetOutBound*，列出在 hello hello 前置詞**位址首碼**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="216b3-149">Selecting a rule with a tag, such as *AllowInternetOutBound*, lists hello prefixes in hello **Address prefixes** blade.</span></span>
   * <span data-ttu-id="216b3-150">**下載：** hello 的規則清單中可能會很長。</span><span class="sxs-lookup"><span data-stu-id="216b3-150">**Download:** hello list of rules can be long.</span></span> <span data-ttu-id="216b3-151">您可以按一下來下載.csv 檔案的 hello 規則進行離線分析**下載**和儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="216b3-151">You can download a .csv file of hello rules for offline analysis by clicking **Download** and saving hello file.</span></span>
   * <span data-ttu-id="216b3-152">**AllowRDP**輸入的規則： 這個規則允許 RDP 連線 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-152">**AllowRDP** Inbound rule: This rule allows RDP connections toohello VM.</span></span>
7. <span data-ttu-id="216b3-153">按一下 hello **Subnet1 NSG** hello NSG 中的索引標籤 tooview hello 有效規則套用 toohello 子網路，hello 下列圖片所示：</span><span class="sxs-lookup"><span data-stu-id="216b3-153">Click hello **Subnet1-NSG** tab tooview hello effective rules from hello NSG applied toohello subnet, as shown in hello following picture:</span></span> 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="216b3-154">請注意 hello *denyRDP* **輸入**規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-154">Notice hello *denyRDP* **Inbound** rule.</span></span> <span data-ttu-id="216b3-155">在 hello 網路介面套用的規則之前，會評估輸入的規則套用於 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-155">Inbound rules applied at hello subnet are evaluated before rules applied at hello network interface.</span></span> <span data-ttu-id="216b3-156">Hello 拒絕規則套 hello 子網路，因為 hello 要求 tooconnect tooTCP 3389 會失敗，因為 hello 允許規則在 hello NIC 不會加以評估。</span><span class="sxs-lookup"><span data-stu-id="216b3-156">Since hello deny rule is applied at hello subnet, hello request tooconnect tooTCP 3389 fails, because hello allow rule at hello NIC is never evaluated.</span></span> 
   
    <span data-ttu-id="216b3-157">hello *denyRDP*規則是 hello 原因 hello RDP 連線失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="216b3-157">hello *denyRDP* rule is hello reason why hello RDP connection is failing.</span></span> <span data-ttu-id="216b3-158">將它移除，應該解決 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="216b3-158">Removing it should resolve hello problem.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="216b3-159">如果關聯的 hello VM hello 與 NIC 不是處於執行中狀態，或 Nsg 未套用的 toohello NIC 或子網路，會顯示任何規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-159">If hello VM associated with hello NIC is not in a running state, or NSGs haven't been applied toohello NIC or subnet, no rules are shown.</span></span>
   > 
   > 
8. <span data-ttu-id="216b3-160">tooedit NSG 規則中，按一下  *Subnet1 NSG*在 hello**關聯 Nsg** > 一節。</span><span class="sxs-lookup"><span data-stu-id="216b3-160">tooedit NSG rules, click *Subnet1-NSG* in hello **Associated NSGs** section.</span></span>
   <span data-ttu-id="216b3-161">這會開啟 hello **Subnet1 NSG**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="216b3-161">This opens hello **Subnet1-NSG** blade.</span></span> <span data-ttu-id="216b3-162">您可以直接編輯 hello 規則上的 **輸入安全性規則**。</span><span class="sxs-lookup"><span data-stu-id="216b3-162">You can directly edit hello rules by clicking on **Inbound security rules**.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. <span data-ttu-id="216b3-163">移除 hello 之後*denyRDP* hello 中的輸入的規則**Subnet1 NSG**並加入*allowRDP*規則 hello 有效的規則清單看起來像下列圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="216b3-163">After removing hello *denyRDP* inbound rule in hello **Subnet1-NSG** and adding an *allowRDP* rule, hello effective rules list looks like hello following picture:</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    <span data-ttu-id="216b3-164">確認開啟 RDP 連線 toohello VM，或使用 hello PsPing 工具開啟 TCP 連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="216b3-164">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="216b3-165">您可以進一步了解 PsPing 讀取 hello [PsPing 下載頁面](https://technet.microsoft.com/sysinternals/psping.aspx)。</span><span class="sxs-lookup"><span data-stu-id="216b3-165">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx).</span></span>

### <span data-ttu-id="216b3-166"><a name="nic"></a>檢視網路介面的有效安全性規則</span><span class="sxs-lookup"><span data-stu-id="216b3-166"><a name="nic"></a>View effective security rules for a network interface</span></span>
<span data-ttu-id="216b3-167">如果您 VM 的流量會影響特定 nic，您可以藉由完成下列步驟的 hello 檢視 hello 從 hello 網路介面內容 hello NIC 的有效規則的完整清單：</span><span class="sxs-lookup"><span data-stu-id="216b3-167">If your VM traffic flow is impacted for a specific NIC, you can view a full list of hello effective rules for hello NIC from hello network interfaces context by completing hello following steps:</span></span>

1. <span data-ttu-id="216b3-168">登入 toohello https://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="216b3-168">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="216b3-169">按一下**更多服務**，然後按一下 **網路介面**hello 的清單中，會出現。</span><span class="sxs-lookup"><span data-stu-id="216b3-169">Click **More services**, then click **Network interfaces** in hello list that appears.</span></span>
3. <span data-ttu-id="216b3-170">選取某個網路介面。</span><span class="sxs-lookup"><span data-stu-id="216b3-170">Select a network interface.</span></span> <span data-ttu-id="216b3-171">在下列圖片 hello，NIC 命名為*VM1 NIC1*已選取。</span><span class="sxs-lookup"><span data-stu-id="216b3-171">In hello following picture, a NIC named *VM1-NIC1* is selected.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    <span data-ttu-id="216b3-172">請注意該 hello**範圍**toohello 選取的網路介面設定。</span><span class="sxs-lookup"><span data-stu-id="216b3-172">Notice that hello **Scope** is set toohello network interface selected.</span></span> <span data-ttu-id="216b3-173">深入了解 toolearn hello 額外的資訊顯示，讀取 hello 的步驟 6**疑難排解 Nsg vm**本文一節。</span><span class="sxs-lookup"><span data-stu-id="216b3-173">toolearn more about hello additional information shown, read step 6 of hello **Troubleshoot NSGs for a VM** section of this article.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="216b3-174">從網路介面移除 NSG，hello 子網路的 nsg 關聯仍然有效上指定 NIC 的 hello</span><span class="sxs-lookup"><span data-stu-id="216b3-174">If an NSG is removed from a network interface, hello subnet NSG is still effective on hello given NIC.</span></span> <span data-ttu-id="216b3-175">在此情況下，hello 輸出只會顯示 hello 子網路 NSG 的規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-175">In this case, hello output would only show rules from hello subnet NSG.</span></span> <span data-ttu-id="216b3-176">規則只會顯示 hello NIC 是否附加的 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-176">Rules only appear if hello NIC is attached tooa VM.</span></span>
   > 
   > 
4. <span data-ttu-id="216b3-177">您可以直接編輯與 NIC 和子網路相關聯之 NSG 的規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-177">You can directly edit rules for NSGs associated with a NIC and a subnet.</span></span> <span data-ttu-id="216b3-178">toolearn 作法，請閱讀步驟 8 的 hello**檢視虛擬機器的有效的安全性規則**本文一節。</span><span class="sxs-lookup"><span data-stu-id="216b3-178">toolearn how, read step 8 of hello **View effective security rules for a virtual machine** section of this article.</span></span>

## <span data-ttu-id="216b3-179"><a name="nsg"></a>檢視網路安全性群組 (NSG) 的有效安全性規則</span><span class="sxs-lookup"><span data-stu-id="216b3-179"><a name="nsg"></a>View effective security rules for a network security group (NSG)</span></span>
<span data-ttu-id="216b3-180">當修改 NSG 規則，您可能想 tooreview hello 影響的特定 VM 上的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-180">When modifying NSG rules, you may want tooreview hello impact of hello rules being added on a particular VM.</span></span> <span data-ttu-id="216b3-181">您可以檢視所有 hello Nic 給定的 NSG 套用 hello 有效的安全性規則的完整清單而不需要從給定 NSG 刀鋒視窗中的 hello tooswitch 內容。</span><span class="sxs-lookup"><span data-stu-id="216b3-181">You can view a full list of hello effective security rules for all hello NICs that a given NSG is applied to, without having tooswitch context from hello given NSG blade.</span></span> <span data-ttu-id="216b3-182">tootroubleshoot NSG，完成下列步驟的 hello 內的有效規則：</span><span class="sxs-lookup"><span data-stu-id="216b3-182">tootroubleshoot effective rules within an NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="216b3-183">登入 toohello https://portal.azure.com 在 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="216b3-183">Login toohello Azure portal at https://portal.azure.com.</span></span>
2. <span data-ttu-id="216b3-184">按一下**更多服務**，然後按一下 **網路安全性群組**hello 的清單中，會出現。</span><span class="sxs-lookup"><span data-stu-id="216b3-184">Click **More services**, then click **Network security groups** in hello list that appears.</span></span>
3. <span data-ttu-id="216b3-185">選取某個 NSG。</span><span class="sxs-lookup"><span data-stu-id="216b3-185">Select an NSG.</span></span> <span data-ttu-id="216b3-186">在下列圖片 hello，選取名為 VM1 nsg NSG。</span><span class="sxs-lookup"><span data-stu-id="216b3-186">In hello following picture, an NSG named VM1-nsg was selected.</span></span>
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    <span data-ttu-id="216b3-187">請注意下列各節的 hello 上一張圖片的 hello:</span><span class="sxs-lookup"><span data-stu-id="216b3-187">Notice hello following sections of hello previous picture:</span></span>
   
   * <span data-ttu-id="216b3-188">**範圍：**設定 toohello 選取 NSG。</span><span class="sxs-lookup"><span data-stu-id="216b3-188">**Scope:** Set toohello NSG selected.</span></span>
   * <span data-ttu-id="216b3-189">**虛擬機器：**當 NSG 是套用的 tooa 子網路，而是套用的 tooall 介面附加的 tooall Vm 連接的 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-189">**Virtual machine:** When an NSG is applied tooa subnet, it's applied tooall network interfaces attached tooall VMs connected toohello subnet.</span></span> <span data-ttu-id="216b3-190">此清單顯示套用此 NSG 的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-190">This list shows all VMs this NSG is applied to.</span></span> <span data-ttu-id="216b3-191">您可以從 hello 清單中選取任何 VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-191">You can select any VM from hello list.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="216b3-192">如果 NSG 套用的 tooonly 空白的子網路，不會列 Vm。</span><span class="sxs-lookup"><span data-stu-id="216b3-192">If an NSG is applied tooonly an empty subnet, VMs will not be listed.</span></span> <span data-ttu-id="216b3-193">如果 NSG 套用的 tooa NIC 不是與 VM 相關聯，這些 Nic 也不會列。</span><span class="sxs-lookup"><span data-stu-id="216b3-193">If an NSG is applied tooa NIC which is not associated with a VM, those NICs will also not be listed.</span></span> 
     > 
     > 
   * <span data-ttu-id="216b3-194">**網路介面：**一個 VM 可以有多個網路介面。</span><span class="sxs-lookup"><span data-stu-id="216b3-194">**Network Interface:** A VM can have multiple network interfaces.</span></span> <span data-ttu-id="216b3-195">您可以選取網路介面附加的 toohello 選取 VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-195">You can select a network interface attached toohello selected VM.</span></span>
   * <span data-ttu-id="216b3-196">**AssociatedNSGs:**最 tootwo 多處理能力的 NIC 可以有任何時候，有效 Nsg，一個套用 toohello NIC，hello 其他 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-196">**AssociatedNSGs:** At any time, a NIC can have up tootwo effective NSGs, one applied toohello NIC and hello other toohello subnet.</span></span> <span data-ttu-id="216b3-197">雖然 hello 範圍當做 VM1 nsg，如果 hello NIC 具有有效的子網路 NSG，hello 輸出會顯示這兩個 Nsg。</span><span class="sxs-lookup"><span data-stu-id="216b3-197">Although hello scope is selected as VM1-nsg, if hello NIC has an effective subnet NSG, hello output will show both NSGs.</span></span>
4. <span data-ttu-id="216b3-198">您可以直接編輯與 NIC 或子網路相關聯之 NSG 的規則。</span><span class="sxs-lookup"><span data-stu-id="216b3-198">You can directly edit rules for NSGs associated with a NIC or subnet.</span></span> <span data-ttu-id="216b3-199">toolearn 作法，請閱讀步驟 8 的 hello**檢視虛擬機器的有效的安全性規則**本文一節。</span><span class="sxs-lookup"><span data-stu-id="216b3-199">toolearn how, read step 8 of hello **View effective security rules for a virtual machine** section of this article.</span></span>

<span data-ttu-id="216b3-200">深入了解 toolearn hello 額外的資訊顯示，讀取 hello 的步驟 6**檢視虛擬機器的有效的安全性規則**本文一節。</span><span class="sxs-lookup"><span data-stu-id="216b3-200">toolearn more about hello additional information shown, read step 6 of hello **View effective security rules for a virtual machine** section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="216b3-201">雖然子網路和 NIC 各有一個 NSG 套用 toothem，NSG 可以關聯的 toomultiple Nic 和多重子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-201">Though a subnet and NIC can each have only one NSG applied toothem, an NSG can be associated toomultiple NICs and multiple subnets.</span></span>
> 
> 

## <a name="considerations"></a><span data-ttu-id="216b3-202">考量</span><span class="sxs-lookup"><span data-stu-id="216b3-202">Considerations</span></span>
<span data-ttu-id="216b3-203">請考慮 hello 疑難排解連線問題時，下列點：</span><span class="sxs-lookup"><span data-stu-id="216b3-203">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="216b3-204">預設 NSG 規則將會封鎖從 hello 對內的存取網際網路和允許 VNet 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="216b3-204">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="216b3-205">規則應該明確加入 tooallow 輸入視需要從網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="216b3-205">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="216b3-206">如果沒有造成 VM 的網路連線 toofail NSG 安全性規則，hello 問題可能是因為：</span><span class="sxs-lookup"><span data-stu-id="216b3-206">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="216b3-207">Hello VM 作業系統內執行的防火牆軟體</span><span class="sxs-lookup"><span data-stu-id="216b3-207">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="216b3-208">為虛擬設備或內部部署流量設定的路由。</span><span class="sxs-lookup"><span data-stu-id="216b3-208">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="216b3-209">網際網路流量可以透過強制通道的重新導向的 tooon 單位。</span><span class="sxs-lookup"><span data-stu-id="216b3-209">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="216b3-210">RDP/SSH 連線從 hello 網際網路 tooyour VM 可能不適用於此設定，根據 hello 在內部部署網路硬體如何處理這個流量。</span><span class="sxs-lookup"><span data-stu-id="216b3-210">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="216b3-211">讀取 hello[疑難排解路由](virtual-network-routes-troubleshoot-powershell.md)文章 toolearn 如何 toodiagnose 路由問題，可能索性 hello 和出的流量傳送 hello VM。</span><span class="sxs-lookup"><span data-stu-id="216b3-211">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="216b3-212">如果您有所以 Vnet，根據預設，hello VIRTUAL_NETWORK 標記會自動擴展 tooinclude 前置詞所以 vnet。</span><span class="sxs-lookup"><span data-stu-id="216b3-212">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="216b3-213">您可以檢視這些前置詞中 hello **ExpandedAddressPrefix**清單，tootroubleshoot 對等互連連線問題相關 tooVNet。</span><span class="sxs-lookup"><span data-stu-id="216b3-213">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="216b3-214">有效的安全性規則只會顯示於是否有與 hello VM NIC 和或子網路的 NSG 相關聯。</span><span class="sxs-lookup"><span data-stu-id="216b3-214">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="216b3-215">如果沒有相關聯 hello NIC 的 Nsg 或子網路，而且您有指派 tooyour VM 的公用 IP 位址，所有連接埠將會開啟以供對內及對外存取。</span><span class="sxs-lookup"><span data-stu-id="216b3-215">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="216b3-216">如果 hello VM 的公用 IP 位址，強烈建議套用 Nsg toohello NIC 或子網路。</span><span class="sxs-lookup"><span data-stu-id="216b3-216">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>

