---
title: "aaaJust 時間虛擬機器中的存取 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件逐步解說如何在 Azure 資訊安全中心可以協助您控制 VM 存取存取 tooyour Azure 虛擬機器。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a><span data-ttu-id="3cb20-103">使用 Just-In-Time 管理虛擬機器存取</span><span class="sxs-lookup"><span data-stu-id="3cb20-103">Manage virtual machine access using just in time</span></span>

<span data-ttu-id="3cb20-104">時間虛擬機器 (VM) 中只可以存取使用的 toolock 輸入的流量 tooyour Azure Vm，降低暴露 tooattacks 同時提供讓您輕鬆存取 tooconnect tooVMs 需要時關閉。</span><span class="sxs-lookup"><span data-stu-id="3cb20-104">Just in time virtual machine (VM) access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks while providing easy access tooconnect tooVMs when needed.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb20-105">在時間 」 功能中的 hello 已預覽並可使用 hello 標準層的資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="3cb20-105">hello just in time feature is in preview and available on hello Standard tier of Security Center.</span></span>  <span data-ttu-id="3cb20-106">請參閱[定價](security-center-pricing.md)toolearn 詳細的資訊安全中心的定價層。</span><span class="sxs-lookup"><span data-stu-id="3cb20-106">See [Pricing](security-center-pricing.md) toolearn more about Security Center's pricing tiers.</span></span>
>
>

## <a name="attack-scenario"></a><span data-ttu-id="3cb20-107">攻擊案例</span><span class="sxs-lookup"><span data-stu-id="3cb20-107">Attack scenario</span></span>

<span data-ttu-id="3cb20-108">暴力攻擊的常見目標管理連接埠為表示 toogain 存取 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-108">Brute force attacks commonly target management ports as a means toogain access tooa VM.</span></span> <span data-ttu-id="3cb20-109">如果成功的話，攻擊者可以使用控制 hello VM，並建立據點至您的環境。</span><span class="sxs-lookup"><span data-stu-id="3cb20-109">If successful, an attacker can take control over hello VM and establish a foothold into your environment.</span></span>

<span data-ttu-id="3cb20-110">其中一種方式 tooreduce 曝光 tooa 暴力攻擊是時間的 toolimit hello 數量的連接埠已開啟。</span><span class="sxs-lookup"><span data-stu-id="3cb20-110">One way tooreduce exposure tooa brute force attack is toolimit hello amount of time that a port is open.</span></span> <span data-ttu-id="3cb20-111">管理連接埠隨時都能執行需要 toobe 開啟。</span><span class="sxs-lookup"><span data-stu-id="3cb20-111">Management ports do not need toobe open at all times.</span></span> <span data-ttu-id="3cb20-112">他們只需要 toobe 開啟時您所連接的 toohello VM，例如 tooperform 管理或維護工作。</span><span class="sxs-lookup"><span data-stu-id="3cb20-112">They only need toobe open while you are connected toohello VM, for example tooperform management or maintenance tasks.</span></span> <span data-ttu-id="3cb20-113">在啟用時，會使用資訊安全中心[網路安全性群組](../virtual-network/virtual-networks-nsg.md)(NSG) 規則，限制存取 toomanagement 連接埠，因此無法由攻擊者為目標。</span><span class="sxs-lookup"><span data-stu-id="3cb20-113">When just in time is enabled, Security Center uses [Network Security Group](../virtual-network/virtual-networks-nsg.md) (NSG) rules, which restrict access toomanagement ports so they cannot be targeted by attackers.</span></span>

![Just-In-Time 案例][1]

## <a name="how-does-just-in-time-access-work"></a><span data-ttu-id="3cb20-115">Just-In-Time 存取如何運作？</span><span class="sxs-lookup"><span data-stu-id="3cb20-115">How does just in time access work?</span></span>

<span data-ttu-id="3cb20-116">在啟用時，資訊安全中心鎖定輸入的流量 tooyour Azure Vm 建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="3cb20-116">When just in time is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="3cb20-117">您選取 hello 連接埠上 hello VM toowhich 輸入的流量會鎖定。</span><span class="sxs-lookup"><span data-stu-id="3cb20-117">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="3cb20-118">這些連接埠是由在時間方案中的 hello 控制。</span><span class="sxs-lookup"><span data-stu-id="3cb20-118">These ports are controlled by hello just in time solution.</span></span>

<span data-ttu-id="3cb20-119">當使用者要求存取 tooa VM 時，資訊安全中心會檢查該 hello 使用者擁有[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md) hello Azure 資源提供寫入存取權的權限。</span><span class="sxs-lookup"><span data-stu-id="3cb20-119">When a user requests access tooa VM, Security Center checks that hello user has [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) permissions that provide write access for hello Azure resource.</span></span> <span data-ttu-id="3cb20-120">如果他們擁有寫入權限、 hello 會核准要求並且資訊安全中心會自動設定的網路安全性群組 (Nsg) tooallow hello 傳入流量 toohello 管理連接埠 hello 您指定的時間量。</span><span class="sxs-lookup"><span data-stu-id="3cb20-120">If they have write permissions, hello request is approved and Security Center automatically configures hello Network Security Groups (NSGs) tooallow inbound traffic toohello management ports for hello amount of time you specified.</span></span> <span data-ttu-id="3cb20-121">Hello 時間到期之後，資訊安全中心還原 hello Nsg tootheir 先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="3cb20-121">After hello time has expired, Security Center restores hello NSGs tootheir previous states.</span></span>

> [!NOTE]
> <span data-ttu-id="3cb20-122">資訊安全中心 Just-In-Time VM 存取目前僅支援透過 Azure Resource Manager 部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-122">Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="3cb20-123">傳統的 hello 與資源管理員部署模型的詳細資訊請參閱的 toolearn [Azure Resource Manager vs 傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3cb20-123">toolearn more about hello classic and Resource Manager deployment models see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
>
>

## <a name="using-just-in-time-access"></a><span data-ttu-id="3cb20-124">使用 Just-In-Time 存取</span><span class="sxs-lookup"><span data-stu-id="3cb20-124">Using just in time access</span></span>

<span data-ttu-id="3cb20-125">hello**階段 VM 存取中的恰好**磚 hello**資訊安全中心**刀鋒視窗中顯示的 Vm 設定為在時間的存取權與 hello 核准的存取提出的要求數目 hello 在過去一週中的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="3cb20-125">hello **Just in time VM access** tile on hello **Security Center** blade shows hello number of VMs configured for just in time access and hello number of approved access requests made in hello last week.</span></span>

<span data-ttu-id="3cb20-126">選取 hello**階段 VM 存取中的恰好**磚與 hello**恰好在時間 VM 存取**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="3cb20-126">Select hello **Just in time VM access** tile and hello **Just in time VM access** blade opens.</span></span>

![[Just-In-Time VM 存取] 圖格][2]

<span data-ttu-id="3cb20-128">hello**階段 VM 存取中的恰好**刀鋒視窗中提供您 Vm hello 狀態的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="3cb20-128">hello **Just in time VM access** blade provides information on hello state of your VMs:</span></span>

- <span data-ttu-id="3cb20-129">**設定**-已設定的 toosupport 只在時間 VM 存取的 Vm。</span><span class="sxs-lookup"><span data-stu-id="3cb20-129">**Configured** - VMs that have been configured toosupport just in time VM access.</span></span> <span data-ttu-id="3cb20-130">顯示 hello 資料 hello 過去一週，而且包含的每個 VM hello 數目核准的要求、 上次存取日期和時間和最後一位使用者。</span><span class="sxs-lookup"><span data-stu-id="3cb20-130">hello data presented is for hello last week and includes for each VM hello number of approved requests, last access date and time, and last user.</span></span>
- <span data-ttu-id="3cb20-131">[建議] - 可支援但未設定 Just-In-Time VM 存取的 VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-131">**Recommended** - VMs that can support just in time VM access but have not been configured to.</span></span> <span data-ttu-id="3cb20-132">建議您啟用這些 VM 的 Just-In-Time VM 存取控制。</span><span class="sxs-lookup"><span data-stu-id="3cb20-132">We recommend that you enable just in time VM access control for these VMs.</span></span> <span data-ttu-id="3cb20-133">請參閱[啟用 Just-In-Time VM 存取](#enable-just-in-time-vm-access)。</span><span class="sxs-lookup"><span data-stu-id="3cb20-133">See [Enable just in time VM access](#enable-just-in-time-vm-access).</span></span>
- <span data-ttu-id="3cb20-134">**不推薦**-可能會導致 VM toobe 建議的原因如下：</span><span class="sxs-lookup"><span data-stu-id="3cb20-134">**No recommendation** - Reasons that can cause a VM not toobe recommended are:</span></span>
  - <span data-ttu-id="3cb20-135">遺漏 NSG-hello 時間解決方案中只需要就地 NSG toobe。</span><span class="sxs-lookup"><span data-stu-id="3cb20-135">Missing NSG - hello just in time solution requires an NSG toobe in place.</span></span>
  - <span data-ttu-id="3cb20-136">傳統 VM - 資訊安全中心 Just-In-Time VM 存取目前僅支援透過 Azure Resource Manager 部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-136">Classic VM - Security Center just in time VM access currently supports only VMs deployed through Azure Resource Manager.</span></span> <span data-ttu-id="3cb20-137">在時間方案中的 hello 不支援傳統的部署。</span><span class="sxs-lookup"><span data-stu-id="3cb20-137">A classic deployment is not supported by hello just in time solution.</span></span>
  - <span data-ttu-id="3cb20-138">其他-VM 如果是在此類別在解決方案已關閉 hello 訂用帳戶或 hello 資源群組、 hello 安全性原則中的 hello 或該 VM 的 hello 遺漏公用 IP，因此未就地擁有 NSG。</span><span class="sxs-lookup"><span data-stu-id="3cb20-138">Other - A VM is in this category if hello just in time solution is turned off in hello security policy of hello subscription or hello resource group, or that hello VM is missing a public IP and doesn't have an NSG in place.</span></span>

## <a name="configuring-a-just-in-time-access-policy"></a><span data-ttu-id="3cb20-139">設定 Just-In-Time 存取原則</span><span class="sxs-lookup"><span data-stu-id="3cb20-139">Configuring a just in time access policy</span></span>

<span data-ttu-id="3cb20-140">tooselect hello 想 tooenable Vm:</span><span class="sxs-lookup"><span data-stu-id="3cb20-140">tooselect hello VMs that you want tooenable:</span></span>

1. <span data-ttu-id="3cb20-141">在 hello**階段 VM 存取中的恰好**刀鋒視窗中，選取 hello**建議** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3cb20-141">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![啟用 Just-In-Time 存取][3]

2. <span data-ttu-id="3cb20-143">在下**Vm**，選取您想 tooenable hello Vm。</span><span class="sxs-lookup"><span data-stu-id="3cb20-143">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="3cb20-144">這會使核取記號下一步 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-144">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="3cb20-145">選取 [在 VM 上啟用 JIT]。</span><span class="sxs-lookup"><span data-stu-id="3cb20-145">Select **Enable JIT on VMs**.</span></span>
4. <span data-ttu-id="3cb20-146">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="3cb20-146">Select **Save**.</span></span>

### <a name="default-ports"></a><span data-ttu-id="3cb20-147">預設連接埠</span><span class="sxs-lookup"><span data-stu-id="3cb20-147">Default ports</span></span>

<span data-ttu-id="3cb20-148">您可以看到的資訊安全中心建議啟用 just-in-time hello 預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="3cb20-148">You can see hello default ports that Security Center recommends enabling just in time.</span></span>

1. <span data-ttu-id="3cb20-149">在 hello**階段 VM 存取中的恰好**刀鋒視窗中，選取 hello**建議** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3cb20-149">On hello **Just in time VM access** blade, select hello **Recommended** tab.</span></span>

  ![顯示預設連接埠][6]

2. <span data-ttu-id="3cb20-151">在 [VM] 下方，選取 VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-151">Under **VMs**, select a VM.</span></span> <span data-ttu-id="3cb20-152">這會使核取記號下一步 toohello VM，並開啟 hello **JIT VM 存取組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3cb20-152">This puts a checkmark next toohello VM and opens hello **JIT VM access configuration** blade.</span></span> <span data-ttu-id="3cb20-153">此刀鋒視窗會顯示 hello 預設連接埠。</span><span class="sxs-lookup"><span data-stu-id="3cb20-153">This blade displays hello default ports.</span></span>

### <a name="add-ports"></a><span data-ttu-id="3cb20-154">新增連接埠</span><span class="sxs-lookup"><span data-stu-id="3cb20-154">Add ports</span></span>

<span data-ttu-id="3cb20-155">從 hello **JIT VM 存取組態**刀鋒視窗中，您可以同時新增並設定新的連接埠，您想要只在時間方案 tooenable hello。</span><span class="sxs-lookup"><span data-stu-id="3cb20-155">From hello **JIT VM access configuration** blade, you can also add and configure a new port on which you want tooenable hello just in time solution.</span></span>

1. <span data-ttu-id="3cb20-156">在 hello **JIT VM 存取組態**刀鋒視窗中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="3cb20-156">On hello **JIT VM access configuration** blade, select **Add**.</span></span> <span data-ttu-id="3cb20-157">這會開啟 hello**新增連接埠組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3cb20-157">This opens hello **Add port configuration** blade.</span></span>

  ![連接埠組態][7]

2. <span data-ttu-id="3cb20-159">在**新增連接埠組態**刀鋒視窗中，識別 hello 允許通訊埠，通訊協定類型的來源 Ip 和最大要求的時間。</span><span class="sxs-lookup"><span data-stu-id="3cb20-159">On **Add port configuration** blade, you identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>

  <span data-ttu-id="3cb20-160">允許的來源 Ip 是 hello IP 範圍 tooget 允許的存取已核准的要求。</span><span class="sxs-lookup"><span data-stu-id="3cb20-160">Allowed source IPs are hello IP ranges allowed tooget access upon an approved request.</span></span>

  <span data-ttu-id="3cb20-161">最大要求時間是特定的連接埠，可以開啟 hello 大的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="3cb20-161">Maximum request time is hello maximum time window that a specific port can be opened.</span></span>

3. <span data-ttu-id="3cb20-162">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3cb20-162">Select **OK**.</span></span>

## <a name="requesting-access-tooa-vm"></a><span data-ttu-id="3cb20-163">要求存取 tooa VM</span><span class="sxs-lookup"><span data-stu-id="3cb20-163">Requesting access tooa VM</span></span>

<span data-ttu-id="3cb20-164">toorequest 存取 tooa VM:</span><span class="sxs-lookup"><span data-stu-id="3cb20-164">toorequest access tooa VM:</span></span>

1. <span data-ttu-id="3cb20-165">在 hello**恰好在時間 VM 存取**刀鋒視窗中，選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3cb20-165">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="3cb20-166">在下**Vm**，選取您想要 tooenable 存取 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="3cb20-166">Under **VMs**, select hello VMs that you want tooenable access.</span></span> <span data-ttu-id="3cb20-167">這會使核取記號下一步 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="3cb20-167">This puts a checkmark next tooa VM.</span></span>
3. <span data-ttu-id="3cb20-168">選取 [要求存取]。</span><span class="sxs-lookup"><span data-stu-id="3cb20-168">Select **Request access**.</span></span> <span data-ttu-id="3cb20-169">這會開啟 hello**要求存取**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3cb20-169">This opens hello **Request access** blade.</span></span>

  ![要求存取 tooa VM][4]

4. <span data-ttu-id="3cb20-171">在 hello**要求存取**刀鋒視窗中，您設定 hello 來源 IP hello 連接埠，以及每個 VM hello 連接埠 tooopen 開啟 tooand hello 時段的 hello 通訊埠已開啟的。</span><span class="sxs-lookup"><span data-stu-id="3cb20-171">On hello **Request access** blade, you configure for each VM hello ports tooopen along with hello source IP that hello port is opened tooand hello time window for which hello port is opened.</span></span> <span data-ttu-id="3cb20-172">您可以要求存取只有 toohello 連接埠 hello 只在時間原則中所設定。</span><span class="sxs-lookup"><span data-stu-id="3cb20-172">You can request access only toohello ports that are configured in hello just in time policy.</span></span> <span data-ttu-id="3cb20-173">每個連接埠有衍生自 hello 只在時間原則的最大允許的時間。</span><span class="sxs-lookup"><span data-stu-id="3cb20-173">Each port has a maximum allowed time derived from hello just in time policy.</span></span>
5. <span data-ttu-id="3cb20-174">選取 [開啟連接埠]。</span><span class="sxs-lookup"><span data-stu-id="3cb20-174">Select **Open ports**.</span></span>

## <a name="editing-a-just-in-time-access-policy"></a><span data-ttu-id="3cb20-175">編輯 Just-In-Time 存取原則</span><span class="sxs-lookup"><span data-stu-id="3cb20-175">Editing a just in time access policy</span></span>

<span data-ttu-id="3cb20-176">您可以變更 VM 的現有時間原則中，只將新增並設定新的連接埠 tooopen 該 vm，或變更任何其他參數相關的 tooan 已受保護的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="3cb20-176">You can change a VM's existing just in time policy by adding and configuring a new port tooopen for that VM, or by changing any other parameter related tooan already protected port.</span></span>

<span data-ttu-id="3cb20-177">在順序 tooedit 現有的 VM，時間原則在 hello**設定**索引標籤可用：</span><span class="sxs-lookup"><span data-stu-id="3cb20-177">In order tooedit an existing just in time policy of a VM, hello **Configured** tab is used:</span></span>

1. <span data-ttu-id="3cb20-178">在下**Vm**，選取 VM tooadd 連接埠 tooby hello 三個點 hello 資料列中按一下該 vm。</span><span class="sxs-lookup"><span data-stu-id="3cb20-178">Under **VMs**, select a VM tooadd a port tooby clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="3cb20-179">這會開啟功能表。</span><span class="sxs-lookup"><span data-stu-id="3cb20-179">This opens a menu.</span></span>
2. <span data-ttu-id="3cb20-180">選取**編輯**hello 功能表中。</span><span class="sxs-lookup"><span data-stu-id="3cb20-180">Select **Edit** in hello menu.</span></span> <span data-ttu-id="3cb20-181">這會開啟 hello **JIT VM 存取組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3cb20-181">This opens hello **JIT VM access configuration** blade.</span></span>

  ![編輯原則][8]

3. <span data-ttu-id="3cb20-183">在 hello **JIT VM 存取組態**刀鋒視窗中，您可以在其連接埠，按一下編輯 hello 已受保護的通訊埠現有的設定，或者您可以選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="3cb20-183">On hello **JIT VM access configuration** blade, you can either edit hello existing settings of an already protected port by clicking on its port, or you can select **Add**.</span></span> <span data-ttu-id="3cb20-184">這會開啟 hello**新增連接埠組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3cb20-184">This opens hello **Add port configuration** blade.</span></span>

  ![新增連接埠][7]

4. <span data-ttu-id="3cb20-186">在**新增連接埠組態**刀鋒視窗中識別 hello 連接埠、 通訊協定類型，允許的來源 Ip 時，以及最大要求時間。</span><span class="sxs-lookup"><span data-stu-id="3cb20-186">On **Add port configuration** blade identify hello port, protocol type, allowed source IPs, and maximum request time.</span></span>
5. <span data-ttu-id="3cb20-187">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3cb20-187">Select **OK**.</span></span>
6. <span data-ttu-id="3cb20-188">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="3cb20-188">Select **Save**.</span></span>

## <a name="auditing-just-in-time-access-activity"></a><span data-ttu-id="3cb20-189">稽核 Just-In-Time 存取活動</span><span class="sxs-lookup"><span data-stu-id="3cb20-189">Auditing just in time access activity</span></span>

<span data-ttu-id="3cb20-190">您可以使用記錄搜尋來深入了解 VM 活動。</span><span class="sxs-lookup"><span data-stu-id="3cb20-190">You can gain insights into VM activities using log search.</span></span> <span data-ttu-id="3cb20-191">tooview 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="3cb20-191">tooview logs:</span></span>

1. <span data-ttu-id="3cb20-192">在 hello**恰好在時間 VM 存取**刀鋒視窗中，選取 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3cb20-192">On hello **Just in time VM access** blade, select hello **Configured** tab.</span></span>
2. <span data-ttu-id="3cb20-193">在下**Vm**，選取 關於 VM tooview 資訊 hello 三個點 hello 資料列中按一下該 vm。</span><span class="sxs-lookup"><span data-stu-id="3cb20-193">Under **VMs**, select a VM tooview information about by clicking on hello three dots within hello row for that VM.</span></span> <span data-ttu-id="3cb20-194">這會開啟功能表。</span><span class="sxs-lookup"><span data-stu-id="3cb20-194">This opens a menu.</span></span>
3. <span data-ttu-id="3cb20-195">選取**活動記錄檔**hello 功能表中。</span><span class="sxs-lookup"><span data-stu-id="3cb20-195">Select **Activity Log** in hello menu.</span></span> <span data-ttu-id="3cb20-196">這會開啟 hello**活動記錄檔**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3cb20-196">This opens hello **Activity log** blade.</span></span>

![選取活動記錄][9]

<span data-ttu-id="3cb20-198">hello**活動記錄檔**刀鋒視窗中提供的時間、 日期和訂用帳戶以及該 vm 的先前作業篩選的檢視。</span><span class="sxs-lookup"><span data-stu-id="3cb20-198">hello **Activity log** blade provides a filtered view of previous operations for that VM along with time, date, and subscription.</span></span>

![檢視活動記錄][5]

<span data-ttu-id="3cb20-200">您可以藉由選取下載 hello 記錄資訊**按一下這裡 toodownload hello 的所有項目做為 CSV**。</span><span class="sxs-lookup"><span data-stu-id="3cb20-200">You can download hello log information by selecting **Click here toodownload all hello items as CSV**.</span></span>

<span data-ttu-id="3cb20-201">修改 hello 篩選，然後選取**套用**toocreate 搜尋和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3cb20-201">Modify hello filters and select **Apply** toocreate a search and log.</span></span>

## <a name="using-just-in-time-vm-access-via-powershell"></a><span data-ttu-id="3cb20-202">透過 PowerShell 使用 Just-In-Time VM 存取</span><span class="sxs-lookup"><span data-stu-id="3cb20-202">Using just in time VM access via PowerShell</span></span>

<span data-ttu-id="3cb20-203">在訂單 toouse hello 只在透過 PowerShell 時間方案，請確定您擁有 hello[最新](/powershell/azure/install-azurerm-ps)Azure PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="3cb20-203">In order toouse hello just in time solution via PowerShell, make sure you have hello [latest](/powershell/azure/install-azurerm-ps) Azure PowerShell version.</span></span>
<span data-ttu-id="3cb20-204">一旦您這樣做，您需要 tooinstall hello[最新](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12)hello PowerShell 資源庫從 Azure 資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="3cb20-204">Once you do, you need tooinstall hello [latest](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center from hello PowerShell gallery.</span></span>

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a><span data-ttu-id="3cb20-205">為 VM 設定 Just-In-Time 原則</span><span class="sxs-lookup"><span data-stu-id="3cb20-205">Configuring a just in time policy for a VM</span></span>

<span data-ttu-id="3cb20-206">tooconfigure 只在特定 VM 上的時間原則，您需要 toorun 此命令在您的 PowerShell 工作階段中： 組 ASCJITAccessPolicy。</span><span class="sxs-lookup"><span data-stu-id="3cb20-206">tooconfigure a just in time policy on a specific VM, you need toorun this command in your PowerShell session: Set-ASCJITAccessPolicy.</span></span>
<span data-ttu-id="3cb20-207">請遵循詳細的 hello cmdlet 文件 toolearn。</span><span class="sxs-lookup"><span data-stu-id="3cb20-207">Follow hello cmdlet documentation toolearn more.</span></span>

### <a name="requesting-access-tooa-vm"></a><span data-ttu-id="3cb20-208">要求存取 tooa VM</span><span class="sxs-lookup"><span data-stu-id="3cb20-208">Requesting access tooa VM</span></span>

<span data-ttu-id="3cb20-209">只在時間方案 hello tooaccess 受到將特定 VM，您需要 toorun 此命令中您的 PowerShell 工作階段： ASCJITAccess 叫用。</span><span class="sxs-lookup"><span data-stu-id="3cb20-209">tooaccess a specific VM that is protected with hello just in time solution, you need toorun this command in your PowerShell session: Invoke-ASCJITAccess.</span></span>
<span data-ttu-id="3cb20-210">請遵循詳細的 hello cmdlet 文件 toolearn。</span><span class="sxs-lookup"><span data-stu-id="3cb20-210">Follow hello cmdlet documentation toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cb20-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3cb20-211">Next steps</span></span>
<span data-ttu-id="3cb20-212">在本文中，您學到如何在 VM 存取在資訊安全中心可協助您控制存取 tooyour Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3cb20-212">In this article, you learned how just in time VM access in Security Center helps you control access tooyour Azure virtual machines.</span></span>

<span data-ttu-id="3cb20-213">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3cb20-213">toolearn more about Security Center, see hello following:</span></span>

- <span data-ttu-id="3cb20-214">[設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="3cb20-214">[Setting security policies](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
- <span data-ttu-id="3cb20-215">[管理安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="3cb20-215">[Managing security recommendations](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
- <span data-ttu-id="3cb20-216">[安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="3cb20-216">[Security health monitoring](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
- <span data-ttu-id="3cb20-217">[管理及回應 toosecurity 警示](security-center-managing-and-responding-alerts.md)— 了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="3cb20-217">[Managing and responding toosecurity alerts](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
- <span data-ttu-id="3cb20-218">[監視協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="3cb20-218">[Monitoring partner solutions](security-center-partner-solutions.md) — Learn how toomonitor hello health status of your partner solutions.</span></span>
- <span data-ttu-id="3cb20-219">[資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="3cb20-219">[Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
- <span data-ttu-id="3cb20-220">[Azure 安全性部落格](https://blogs.msdn.microsoft.com/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="3cb20-220">[Azure Security blog](https://blogs.msdn.microsoft.com/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
