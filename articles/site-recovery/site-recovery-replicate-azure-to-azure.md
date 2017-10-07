---
title: "aaaReplicate 應用程式 (Azure tooAzure) |Microsoft 文件"
description: "本文說明如何 tooset 複寫的虛擬機器執行在一個 Azure 區域中太另一個在 Azure 中的區域。"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="0bd78-103">將 Azure 虛擬機器 tooanother Azure 地區複寫</span><span class="sxs-lookup"><span data-stu-id="0bd78-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="0bd78-104">Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="0bd78-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="0bd78-105">本文說明如何 tooset 複寫的虛擬機器正在執行一個 Azure 區域 tooanother Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="0bd78-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bd78-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="0bd78-106">Prerequisites</span></span>

* <span data-ttu-id="0bd78-107">hello 文章假設您已經知道有關站台復原和復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="0bd78-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="0bd78-108">您需要 toohave '復原服務保存庫' 預先建立。</span><span class="sxs-lookup"><span data-stu-id="0bd78-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="0bd78-109">建議您建立 hello 「 復原服務保存庫 」 中您想要 Vm tooreplicate hello 位置。</span><span class="sxs-lookup"><span data-stu-id="0bd78-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="0bd78-110">例如，如果您的目標位置是「美國中部」，請在「美國中部」建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="0bd78-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="0bd78-111">如果您正在 hello Azure Vm 上使用網路安全性群組群組 (NSG) 規則或防火牆 proxy toocontrol 存取 toooutbound 網際網路連線，請確定該您白名單 hello 所需的 Url 或 Ip。</span><span class="sxs-lookup"><span data-stu-id="0bd78-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="0bd78-112">請參閱太[網路功能指南 」 文件](./site-recovery-azure-to-azure-networking-guidance.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0bd78-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="0bd78-113">如果您有 ExpressRoute 或 VPN 連線在內部部署與 hello 之間來源在 Azure 中的位置，請遵循[站台復原考量 Azure tooon 內部 expressroute / VPN 組態](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration)文件。</span><span class="sxs-lookup"><span data-stu-id="0bd78-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="0bd78-114">您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooenable 的 Azure 虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="0bd78-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="0bd78-115">您的 Azure 訂用帳戶應啟用的 toocreate Vm hello 目標位置中您想 toouse 為 DR 區域。</span><span class="sxs-lookup"><span data-stu-id="0bd78-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="0bd78-116">您可以連絡支援 tooenable hello 必要的配額。</span><span class="sxs-lookup"><span data-stu-id="0bd78-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="0bd78-117">啟用從 Azure Site Recovery 保存庫進行複寫</span><span class="sxs-lookup"><span data-stu-id="0bd78-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="0bd78-118">此圖中，我們將會複寫在 hello '東亞' Azure 位置 toohello '東南亞' 位置中執行的 Vm。</span><span class="sxs-lookup"><span data-stu-id="0bd78-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="0bd78-119">hello 步驟如下所示：</span><span class="sxs-lookup"><span data-stu-id="0bd78-119">hello steps are as follows:</span></span>

 <span data-ttu-id="0bd78-120">按一下**+ 複寫**hello hello 虛擬機器的保存庫 tooenable 複寫中。</span><span class="sxs-lookup"><span data-stu-id="0bd78-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="0bd78-121">**來源：**它所參考的 hello 機器，即在此情況下的原始 toohello 起點**Azure**。</span><span class="sxs-lookup"><span data-stu-id="0bd78-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="0bd78-122">**來源位置：**是 hello 您想 tooprotect 虛擬機器的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="0bd78-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="0bd78-123">此圖中，對於 hello 來源位置將會是 ' 東亞 '</span><span class="sxs-lookup"><span data-stu-id="0bd78-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="0bd78-124">**部署模型：**它所參考的 hello 來源機器 toohello Azure 部署模型。</span><span class="sxs-lookup"><span data-stu-id="0bd78-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="0bd78-125">您可以選取其中一個傳統或資源管理員和機器屬於 toohello 特定模型會列在 hello 下一個步驟中的保護。</span><span class="sxs-lookup"><span data-stu-id="0bd78-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="0bd78-126">您只能複寫傳統的虛擬機器，並將它復原為傳統的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0bd78-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="0bd78-127">您無法將它復原為資源管理員虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0bd78-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="0bd78-128">**資源群組：**它的來源虛擬機器隸屬的 hello 資源群組 toowhich。</span><span class="sxs-lookup"><span data-stu-id="0bd78-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="0bd78-129">Hello 選取的資源群組下的所有 hello Vm 將會都列出在 hello 下一個步驟中的保護。</span><span class="sxs-lookup"><span data-stu-id="0bd78-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="0bd78-131">在**虛擬機器 > 選取的虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。</span><span class="sxs-lookup"><span data-stu-id="0bd78-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="0bd78-132">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="0bd78-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="0bd78-133">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0bd78-133">Then click OK.</span></span>
    <span data-ttu-id="0bd78-134">![啟用複寫](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="0bd78-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="0bd78-135">在 [設定] 區段下，您可以設定目標網站內容</span><span class="sxs-lookup"><span data-stu-id="0bd78-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="0bd78-136">**目標位置：**就 hello 位置，才能複寫虛擬機器資料來源。</span><span class="sxs-lookup"><span data-stu-id="0bd78-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="0bd78-137">視您選取的機器的位置，站台復原會提供 hello 的適當目標區域清單。</span><span class="sxs-lookup"><span data-stu-id="0bd78-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="0bd78-138">建議 tookeep 目標位置相同為準，您的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="0bd78-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="0bd78-139">**目標資源群組：**是 hello 您複寫的虛擬機器所屬的資源群組 toowhich。根據預設 ASR 會 hello 目標地區建立新的資源群組名稱有"asr"後置詞使用。</span><span class="sxs-lookup"><span data-stu-id="0bd78-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="0bd78-140">如果已經 ASR 所建立的資源群組存在，就會重複使用。您也可以選擇 toocustomize hello 一節所示。</span><span class="sxs-lookup"><span data-stu-id="0bd78-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="0bd78-141">**目標虛擬網路：**根據預設，ASR 將會建立新的虛擬網路中 hello 目標區域名稱具有"asr"後置詞。</span><span class="sxs-lookup"><span data-stu-id="0bd78-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="0bd78-142">這會對應的 tooyour 來源網路，並將用於所有未來的保護。</span><span class="sxs-lookup"><span data-stu-id="0bd78-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0bd78-143">[檢查網路的詳細資料](site-recovery-network-mapping-azure-to-azure.md)tooknow 深入了解網路對應。</span><span class="sxs-lookup"><span data-stu-id="0bd78-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="0bd78-144">**目標儲存體帳戶：** ASR 將會根據預設，建立 hello 新目標儲存體帳戶模擬來源 VM 存放裝置設定。</span><span class="sxs-lookup"><span data-stu-id="0bd78-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="0bd78-145">如果 ASR 建立的儲存體帳戶已經存在，就會重複使用。</span><span class="sxs-lookup"><span data-stu-id="0bd78-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="0bd78-146">**快取儲存體帳戶：** ASR 需要額外的儲存體帳戶稱為 hello 來源範圍中的快取儲存體。</span><span class="sxs-lookup"><span data-stu-id="0bd78-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="0bd78-147">所有 hello 智慧 hello 來源 Vm，會追蹤並傳送 toocache 儲存體帳戶之前複寫這些 toohello 目標位置的變更。</span><span class="sxs-lookup"><span data-stu-id="0bd78-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="0bd78-148">**可用性設定組：** ASR 會根據預設，建立新的可用性設定組 hello 目標區域中，具有"asr"後置字元的名稱。</span><span class="sxs-lookup"><span data-stu-id="0bd78-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="0bd78-149">如果 ASR 建立的可用性設定組已經存在，就會重複使用。</span><span class="sxs-lookup"><span data-stu-id="0bd78-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="0bd78-150">**複寫原則：**它會定義復原點保留歷程記錄和應用程式一致快照頻率的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="0bd78-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="0bd78-151">根據預設，ASR 將對於復原點保留使用「24 小時」預設設定建立新的複寫原則，並對於應用程式一致快照集頻率使用「60 分鐘」。</span><span class="sxs-lookup"><span data-stu-id="0bd78-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="0bd78-153">自訂目標資源</span><span class="sxs-lookup"><span data-stu-id="0bd78-153">Customize target resources</span></span>

<span data-ttu-id="0bd78-154">如果您想使用 ASR toochange hello 預設值，您可以變更您的需求為基礎的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="0bd78-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="0bd78-155">**自訂：**按一下 toochange hello ASR 所使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="0bd78-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="0bd78-156">**目標資源群組：**您可以從現有的 hello hello 訂用帳戶內的目標位置中的所有 hello 資源群組的 hello 清單中選取 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="0bd78-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="0bd78-157">**目標虛擬網路：**您可以在 hello 目標位置找到的所有 hello 虛擬網路的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="0bd78-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="0bd78-158">**可用性設定組：**您只能新增可用性集合設定 toohello 虛擬機器屬於來源範圍中的可用性。</span><span class="sxs-lookup"><span data-stu-id="0bd78-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="0bd78-159">**目標儲存體帳戶：**</span><span class="sxs-lookup"><span data-stu-id="0bd78-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="0bd78-160">![啟用複寫](./media/site-recovery-replicate-azure-to-azure/customize.PNG)按一下**建立目標資源**及 [啟用複寫]</span><span class="sxs-lookup"><span data-stu-id="0bd78-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="0bd78-161">虛擬機器受到保護之後，您就可以檢查 hello Vm 底下的健全狀況狀態**複寫項目**</span><span class="sxs-lookup"><span data-stu-id="0bd78-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="0bd78-162">Hello 期間發生初始複寫的時間無法可能狀態會時間 toorefresh，和您沒有看到段時間的進度。</span><span class="sxs-lookup"><span data-stu-id="0bd78-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="0bd78-163">您可以按一下 hello 重新整理 按鈕上 hello 頂端 hello 刀鋒視窗 tooget hello 最新狀態。</span><span class="sxs-lookup"><span data-stu-id="0bd78-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![啟用複寫](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="0bd78-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bd78-165">Next steps</span></span>
- <span data-ttu-id="0bd78-166">[深入了解](site-recovery-test-failover-to-azure.md)執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="0bd78-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="0bd78-167">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="0bd78-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="0bd78-168">深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)tooreduce RTO。</span><span class="sxs-lookup"><span data-stu-id="0bd78-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="0bd78-169">深入了解容錯移轉之後[重新保護 Azure VM](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="0bd78-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
