---
title: "複寫應用程式 (Azure 至 Azure) | Microsoft Docs"
description: "本文說明如何設定將一個 Azure 區域中執行的虛擬機器複寫至 Azure 的另一個區域。"
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
ms.openlocfilehash: f9f97cf840b722c8cfee169dd1640e0682f287ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-virtual-machines-to-another-azure-region"></a><span data-ttu-id="b769f-103">將 Azure 虛擬機器複寫到另一個 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="b769f-103">Replicate Azure virtual machines to another Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="b769f-104">Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="b769f-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="b769f-105">本文說明如何設定將一個 Azure 區域中執行的虛擬機器複寫至另一個 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b769f-105">This article describes how to set up replication of virtual machines running in one Azure region to another Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b769f-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="b769f-106">Prerequisites</span></span>

* <span data-ttu-id="b769f-107">本文假設您已經知道 Site Recovery 和復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="b769f-107">The article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="b769f-108">您必須先建立「復原服務保存庫」。</span><span class="sxs-lookup"><span data-stu-id="b769f-108">You need to have a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="b769f-109">建議您在要 VM 複寫的位置中建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="b769f-109">It is recommended that you create the 'Recovery services vault' in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="b769f-110">例如，如果您的目標位置是「美國中部」，請在「美國中部」建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="b769f-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="b769f-111">如果您使用網路安全性群組 (NSG) 規則或防火牆 Proxy 對於 Azure VM 上的連出網際網路連線能力控制其存取權，請確定您已將所需的 URL 或 IP 列入白名單中。</span><span class="sxs-lookup"><span data-stu-id="b769f-111">If you are using Network Security Groups (NSG) rules or firewall proxy to control access to outbound internet connectivity on the Azure VMs, ensure that you whitelist the required URLs or IPs.</span></span> <span data-ttu-id="b769f-112">如需詳細資料，請參閱[網路指引文件](./site-recovery-azure-to-azure-networking-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="b769f-112">Refer to [Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="b769f-113">如果 Azure 中的內部部署與來源位置之間有 ExpressRoute 或 VPN 連線，請遵循 [Azure 至內部部署 ExpressRoute / VPN 組態的 Site Recovery 考量](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration)文件。</span><span class="sxs-lookup"><span data-stu-id="b769f-113">If you have an ExpressRoute or a VPN connection between on-premises and the source location in Azure, follow [Site Recovery Considerations for Azure to on-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="b769f-114">您的 Azure 使用者帳戶必須具有特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，才能啟用 Azure 虛擬機器的複寫功能。</span><span class="sxs-lookup"><span data-stu-id="b769f-114">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="b769f-115">必須啟用您的 Azure 訂用帳戶，才能在要做為 DR 區域的目標位置中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="b769f-115">Your Azure subscription should be enabled to create VMs in the target location you want to use as DR region.</span></span> <span data-ttu-id="b769f-116">您可以連絡支援人員啟用所需的配額。</span><span class="sxs-lookup"><span data-stu-id="b769f-116">You can contact support to enable the required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="b769f-117">啟用從 Azure Site Recovery 保存庫進行複寫</span><span class="sxs-lookup"><span data-stu-id="b769f-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="b769f-118">為了說明這一點，我們將「東亞」Azure 位置中執行的 VM 複寫到「東南亞」位置。</span><span class="sxs-lookup"><span data-stu-id="b769f-118">For this illustration, we will replicate VMs running  in the ‘East Asia’ Azure location to the ‘South East Asia’ location.</span></span> <span data-ttu-id="b769f-119">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="b769f-119">The steps are as follows:</span></span>

 <span data-ttu-id="b769f-120">按一下保存庫中的 **+ 複寫**，啟用虛擬機器的複寫功能。</span><span class="sxs-lookup"><span data-stu-id="b769f-120">Click **+Replicate** in the vault to enable replication for the virtual machines.</span></span>

1. <span data-ttu-id="b769f-121">**來源：**這是指機器的源點，在此案例中為 **Azure**。</span><span class="sxs-lookup"><span data-stu-id="b769f-121">**Source:** It refers to the point of origin of the machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="b769f-122">**來源位置：**這是您想要保護虛擬機器的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b769f-122">**Source location:** It is the Azure region from where you want to protect your virtual machines.</span></span> <span data-ttu-id="b769f-123">為了說明這一點，來源位置將是「東亞」</span><span class="sxs-lookup"><span data-stu-id="b769f-123">For this illustration, the source location will be 'East Asia'</span></span>

3. <span data-ttu-id="b769f-124">**部署模型：**這是指來源機器的 Azure 部署模型。</span><span class="sxs-lookup"><span data-stu-id="b769f-124">**Deployment model:** It refers to the Azure deployment model of the source machines.</span></span> <span data-ttu-id="b769f-125">您可選擇使用傳統管理員或資源管理員，且屬於特定模型的機器將在下一個步驟中列出，以提供保護。</span><span class="sxs-lookup"><span data-stu-id="b769f-125">You can select either classic or resource manager and machines belonging to the specific model will be listed for protection in the next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="b769f-126">您只能複寫傳統的虛擬機器，並將它復原為傳統的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b769f-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="b769f-127">您無法將它復原為資源管理員虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b769f-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="b769f-128">**資源群組：**這是來源虛擬機器所屬的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b769f-128">**Resource Group:** It’s the resource group to which your source virtual machines belong.</span></span> <span data-ttu-id="b769f-129">選取的資源群組下的所有 VM 會都在下一個步驟中列出，以供保護。</span><span class="sxs-lookup"><span data-stu-id="b769f-129">All the VMs under the selected resource group will be listed for protection in the next step.</span></span>

    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="b769f-131">在 [虛擬機器] > [選取虛擬機器] 中，按一下並選取您要複寫的每部機器。</span><span class="sxs-lookup"><span data-stu-id="b769f-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="b769f-132">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="b769f-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="b769f-133">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b769f-133">Then click OK.</span></span>
    <span data-ttu-id="b769f-134">![啟用複寫](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="b769f-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="b769f-135">在 [設定] 區段下，您可以設定目標網站內容</span><span class="sxs-lookup"><span data-stu-id="b769f-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="b769f-136">**目標位置**：這是將複寫來源虛擬機器資料的位置。</span><span class="sxs-lookup"><span data-stu-id="b769f-136">**Target Location:**  This is the location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="b769f-137">端視您選取的機器位置而定，Site Recovery 將提供適當目標區域的清單。</span><span class="sxs-lookup"><span data-stu-id="b769f-137">Depending upon your selected machines location, Site Recovery will provide you the list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="b769f-138">建議您保留與復原服務保存庫相同的目標位置。</span><span class="sxs-lookup"><span data-stu-id="b769f-138">It is recommended to keep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="b769f-139">**目標資源群組**：這是所有複寫的虛擬機器所屬的資源群組。根據預設，ASR 將在目標區域中建立新的資源群組，其名稱會有「asr」尾碼。</span><span class="sxs-lookup"><span data-stu-id="b769f-139">**Target resource group :** It is the resource group to which all your replicated virtual machines will belong.By default ASR will create a new resource group in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="b769f-140">如果 ASR 建立的資源群組已經存在，就會重複使用。您也可以選擇自訂該群組，如下一節所示。</span><span class="sxs-lookup"><span data-stu-id="b769f-140">In case resource group created by ASR already exist, it will be reused.You can also choose to customize it as shown in the section below.</span></span>    
3. <span data-ttu-id="b769f-141">**目標虛擬網路：**根據預設，ASR 將在目標區域中建立新的虛擬網路，其名稱會有「asr」尾碼。</span><span class="sxs-lookup"><span data-stu-id="b769f-141">**Target Virtual Network:** By default, ASR will create a new virtual network in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="b769f-142">這將對應於來源網路，並且將用於任何未來的保護。</span><span class="sxs-lookup"><span data-stu-id="b769f-142">This will be mapped to your source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b769f-143">[檢查網路服務詳細資料](site-recovery-network-mapping-azure-to-azure.md)，深入了解網路對應。</span><span class="sxs-lookup"><span data-stu-id="b769f-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) to know more about network mapping.</span></span>

4. <span data-ttu-id="b769f-144">**目標儲存體帳戶：**根據預設，ASR 將建立新目標儲存體帳戶，模擬來源 VM 儲存體組態。</span><span class="sxs-lookup"><span data-stu-id="b769f-144">**Target Storage accounts:** By default, ASR will create the new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="b769f-145">如果 ASR 建立的儲存體帳戶已經存在，就會重複使用。</span><span class="sxs-lookup"><span data-stu-id="b769f-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="b769f-146">**快取儲存體帳戶：**ASR 需要在來源地區中有額外的儲存體帳戶 (稱為快取儲存體)。</span><span class="sxs-lookup"><span data-stu-id="b769f-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in the source region.</span></span> <span data-ttu-id="b769f-147">在來源 VM 上發生的所有變更都會受到追蹤，並傳送到快取儲存體帳戶，然後複寫到目標位置。</span><span class="sxs-lookup"><span data-stu-id="b769f-147">All the changes happening on the source VMs are tracked and sent to cache storage account before replicating those to the target location.</span></span>

6. <span data-ttu-id="b769f-148">**可用性設定組：**根據預設，ASR 將在目標區域中建立新的可用性設定組，其名稱會有「asr」尾碼。</span><span class="sxs-lookup"><span data-stu-id="b769f-148">**Availability set :** By default, ASR will create a new availability set in the target region with name having "asr" suffix.</span></span> <span data-ttu-id="b769f-149">如果 ASR 建立的可用性設定組已經存在，就會重複使用。</span><span class="sxs-lookup"><span data-stu-id="b769f-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="b769f-150">**複寫原則：**這會定義復原點保留歷程記錄和應用程式一致快照集頻率的設定。</span><span class="sxs-lookup"><span data-stu-id="b769f-150">**Replication Policy:** It defines the settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="b769f-151">根據預設，ASR 將對於復原點保留使用「24 小時」預設設定建立新的複寫原則，並對於應用程式一致快照集頻率使用「60 分鐘」。</span><span class="sxs-lookup"><span data-stu-id="b769f-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![啟用複寫](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="b769f-153">自訂目標資源</span><span class="sxs-lookup"><span data-stu-id="b769f-153">Customize target resources</span></span>

<span data-ttu-id="b769f-154">如果您想要變更 ASR 使用的預設值，可以按照您的需求變更設定。</span><span class="sxs-lookup"><span data-stu-id="b769f-154">In case you want to change the defaults used by ASR, you can change the settings based on your needs.</span></span>

1. <span data-ttu-id="b769f-155">**自訂：**按一下將變更 ASR 使用的預設值。</span><span class="sxs-lookup"><span data-stu-id="b769f-155">**Customize:** Click it to change the defaults used by ASR.</span></span>

2. <span data-ttu-id="b769f-156">**目標資源群組：**您可以從訂用帳戶內的目標位置中現有的所有資源群組清單選取資源群組。</span><span class="sxs-lookup"><span data-stu-id="b769f-156">**Target resource group :**  You can select the resource group from the list of all the resource groups existing in the target location within the subscription.</span></span>

3. <span data-ttu-id="b769f-157">**目標虛擬網路：**您可以找到目標位置中所有虛擬網路的清單。</span><span class="sxs-lookup"><span data-stu-id="b769f-157">**Target Virtual Network:** You can find the list of all the virtual network in the target location.</span></span>

4. <span data-ttu-id="b769f-158">**可用性設定組：**您只能將可用性集合設定新增到來源範圍中的可用性所屬的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b769f-158">**Availability set :** You can only add availability sets settings to the virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="b769f-159">**目標儲存體帳戶：**</span><span class="sxs-lookup"><span data-stu-id="b769f-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="b769f-160">![啟用複寫](./media/site-recovery-replicate-azure-to-azure/customize.PNG)按一下**建立目標資源**及 [啟用複寫]</span><span class="sxs-lookup"><span data-stu-id="b769f-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="b769f-161">虛擬機器受到保護之後，您就可以在**複寫項目**下檢查 VM 健全狀況的狀態</span><span class="sxs-lookup"><span data-stu-id="b769f-161">Once virtual machines are protected you can check the status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="b769f-162">在初始複寫期間，狀態可能需要一些時間才能重新整理，因此您有一段時間不會看見進度。</span><span class="sxs-lookup"><span data-stu-id="b769f-162">During the time of initial replication there could a possibility that status takes time to refresh and you don't see progress for some time.</span></span> <span data-ttu-id="b769f-163">您可以按一下刀鋒視窗頂端的 [重新整理] 按鈕，以取得最新狀態。</span><span class="sxs-lookup"><span data-stu-id="b769f-163">You can click the Refresh button on the top of the blade to get the latest status.</span></span>
>

![啟用複寫](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="b769f-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b769f-165">Next steps</span></span>
- <span data-ttu-id="b769f-166">[深入了解](site-recovery-test-failover-to-azure.md)執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b769f-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="b769f-167">[深入了解](site-recovery-failover.md)不同類型的容錯移轉及如何執行。</span><span class="sxs-lookup"><span data-stu-id="b769f-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how to run them.</span></span>
- <span data-ttu-id="b769f-168">深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)降低 RTO。</span><span class="sxs-lookup"><span data-stu-id="b769f-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
- <span data-ttu-id="b769f-169">深入了解容錯移轉之後[重新保護 Azure VM](site-recovery-how-to-reprotect.md)。</span><span class="sxs-lookup"><span data-stu-id="b769f-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
