---
title: "aaaReplicate HYPER-V Vm tooAzure |Microsoft 文件"
description: "描述如何 tooorchestrate 複寫、 容錯移轉和復原的內部部署 Hyper-v-V Vm tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 04/05/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: hyper-v-site-walkthrough-overview
ms.openlocfilehash: 6fba41e43823fc57511d51ea2e09691159693982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure-using-azure-site-recovery-with-hello-azure-portal"></a><span data-ttu-id="8fb07-103">複寫 HYPER-V 虛擬機器 （無 VMM) tooAzure hello Azure 入口網站中使用 Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8fb07-103">Replicate Hyper-V virtual machines (without VMM) tooAzure using Azure Site Recovery with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fb07-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8fb07-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="8fb07-105">Azure 傳統型</span><span class="sxs-lookup"><span data-stu-id="8fb07-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="8fb07-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="8fb07-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="8fb07-107">本文說明如何 tooreplicate 內部部署 HYPER-V 虛擬機器 tooAzure，使用[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="8fb07-107">This article describes how tooreplicate on-premises Hyper-V virtual machines tooAzure, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="8fb07-108">在此部署中，Hyper-V VM 並非由 System Center Virtual Machine Manager (VMM) 所管理。</span><span class="sxs-lookup"><span data-stu-id="8fb07-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>

<span data-ttu-id="8fb07-109">閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

<span data-ttu-id="8fb07-110">如果您想 toomigrate 機器 tooAzure （不含錯誤後回復），進一步了解[本文](site-recovery-migrate-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-110">If you want toomigrate machines tooAzure (without failback), learn more in [this article](site-recovery-migrate-to-azure.md).</span></span>



## <a name="deployment-steps"></a><span data-ttu-id="8fb07-111">部署步驟</span><span class="sxs-lookup"><span data-stu-id="8fb07-111">Deployment steps</span></span>

<span data-ttu-id="8fb07-112">請依照下列 hello 文章 toocomplete 部署步驟執行：</span><span class="sxs-lookup"><span data-stu-id="8fb07-112">Follow hello article toocomplete these deployment steps:</span></span>

1. <span data-ttu-id="8fb07-113">[進一步了解](site-recovery-components.md#hyper-v-to-azure)有關此部署的 hello 架構。</span><span class="sxs-lookup"><span data-stu-id="8fb07-113">[Learn more](site-recovery-components.md#hyper-v-to-azure) about hello architecture for this deployment.</span></span> <span data-ttu-id="8fb07-114">此外，[深入了解](site-recovery-hyper-v-azure-architecture.md) Site Recovery 中 Hyper-V 複寫的運作方式。</span><span class="sxs-lookup"><span data-stu-id="8fb07-114">In addition, [learn about](site-recovery-hyper-v-azure-architecture.md) how Hyper-V replication works in Site Recovery.</span></span>
2. <span data-ttu-id="8fb07-115">確認必要條件和限制。</span><span class="sxs-lookup"><span data-stu-id="8fb07-115">Verify prerequisites and limitations.</span></span>
3. <span data-ttu-id="8fb07-116">設定 Azure 網路和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fb07-116">Set up Azure network and storage accounts.</span></span>
4. <span data-ttu-id="8fb07-117">準備 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="8fb07-117">Prepare Hyper-V hosts.</span></span>
5. <span data-ttu-id="8fb07-118">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-118">Create a Recovery Services vault.</span></span> <span data-ttu-id="8fb07-119">hello 保存庫包含組態設定，並且會協調複寫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-119">hello vault contains configuration settings, and orchestrates replication.</span></span>
6. <span data-ttu-id="8fb07-120">指定來源設定。</span><span class="sxs-lookup"><span data-stu-id="8fb07-120">Specify source settings.</span></span> <span data-ttu-id="8fb07-121">建立 HYPER-V 站台包含 hello 與 HYPER-V 主機，並在 hello 保存庫中註冊 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="8fb07-121">Create a Hyper-V site that contains hello Hyper-V hosts, and register hello site in hello vault.</span></span> <span data-ttu-id="8fb07-122">安裝 Azure Site Recovery Provider，hello 和 hello Microsoft 復原服務代理程式，hello HYPER-V 主機上。</span><span class="sxs-lookup"><span data-stu-id="8fb07-122">Install hello Azure Site Recovery Provider, and hello Microsoft Recovery Services agent, on hello Hyper-V hosts.</span></span>
7. <span data-ttu-id="8fb07-123">設定目標和複寫設定。</span><span class="sxs-lookup"><span data-stu-id="8fb07-123">Set up target and replication settings.</span></span>
8. <span data-ttu-id="8fb07-124">啟用複寫 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="8fb07-124">Enable replication for hello VMs.</span></span>
9. <span data-ttu-id="8fb07-125">執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="8fb07-125">Run a test failover toomake sure everything's working as expected.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="8fb07-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="8fb07-126">Prerequisites</span></span>


<span data-ttu-id="8fb07-127">**需求**</span><span class="sxs-lookup"><span data-stu-id="8fb07-127">**Requirement**</span></span> | <span data-ttu-id="8fb07-128">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="8fb07-128">**Details**</span></span> |
--- | --- |
<span data-ttu-id="8fb07-129">**Azure**</span><span class="sxs-lookup"><span data-stu-id="8fb07-129">**Azure**</span></span> | <span data-ttu-id="8fb07-130">了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-130">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="8fb07-131">**內部部署伺服器**</span><span class="sxs-lookup"><span data-stu-id="8fb07-131">**On-premises servers**</span></span> | <span data-ttu-id="8fb07-132">[進一步了解](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)關於 hello 在內部部署 HYPER-V 主機的需求。</span><span class="sxs-lookup"><span data-stu-id="8fb07-132">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="8fb07-133">**內部部署 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="8fb07-133">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="8fb07-134">您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-134">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="8fb07-135">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="8fb07-135">**Azure URLs**</span></span> | <span data-ttu-id="8fb07-136">HYPER-V 主機需要存取 toothese Url:</span><span class="sxs-lookup"><span data-stu-id="8fb07-136">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="8fb07-137">如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="8fb07-137">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="8fb07-138">允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="8fb07-138">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="8fb07-139">允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。</span><span class="sxs-lookup"><span data-stu-id="8fb07-139">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="prepare-for-deployment"></a><span data-ttu-id="8fb07-140">準備部署</span><span class="sxs-lookup"><span data-stu-id="8fb07-140">Prepare for deployment</span></span>

<span data-ttu-id="8fb07-141">您需要部署 tooprepare:</span><span class="sxs-lookup"><span data-stu-id="8fb07-141">tooprepare for deployment you need to:</span></span>

1. <span data-ttu-id="8fb07-142">[設定 Azure 網路](#set-up-an-azure-network) ，這是 Azure VM 於容錯移轉後建立時將所在的網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-142">[Set up an Azure network](#set-up-an-azure-network) in which Azure VMs will be located when they're created after failover.</span></span>
2. <span data-ttu-id="8fb07-143">[設定 Azure 儲存體帳戶](#set-up-an-azure-storage-account) 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-143">[Set up an Azure storage account](#set-up-an-azure-storage-account) for replicated data.</span></span>
3. <span data-ttu-id="8fb07-144">[準備 hello HYPER-V 主機](#prepare-the-hyper-v-hosts)tooensure 他們可以存取 hello 所需的 Url。</span><span class="sxs-lookup"><span data-stu-id="8fb07-144">[Prepare hello Hyper-V hosts](#prepare-the-hyper-v-hosts) tooensure they can access hello required URLs.</span></span>

### <a name="set-up-an-azure-network"></a><span data-ttu-id="8fb07-145">設定 Azure 網路</span><span class="sxs-lookup"><span data-stu-id="8fb07-145">Set up an Azure network</span></span>

<span data-ttu-id="8fb07-146">設定 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-146">Set up an Azure network.</span></span> <span data-ttu-id="8fb07-147">您將需要此以便 hello Azure Vm 建立容錯移轉之後連接的 tooa 網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-147">You’ll need this so that hello Azure VMs created after failover are connected tooa network.</span></span>

* <span data-ttu-id="8fb07-148">hello 網路應位於 hello hello 與相同的區域復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-148">hello network should be in hello same region as hello Recovery Services vault.</span></span>
* <span data-ttu-id="8fb07-149">根據 hello 資源模型，您會想 toouse 容錯移轉 Azure Vm、 hello Azure 網路中設定[Resource Manager 模式](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)，或[傳統模式](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-149">Depending on hello resource model you want toouse for failed over Azure VMs, you set up hello Azure network in [Resource Manager mode](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), or [classic mode](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>
* <span data-ttu-id="8fb07-150">建議您在開始之前先設定網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-150">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="8fb07-151">如果沒有，您需要 toodo Site Recovery 部署期間它。</span><span class="sxs-lookup"><span data-stu-id="8fb07-151">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="8fb07-152">Site Recovery 所使用的儲存體帳戶不能是[移動](../azure-resource-manager/resource-group-move-resources.md)hello 相同，或跨不同，訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="8fb07-152">Storage accounts used by Site Recovery can't be [moved](../azure-resource-manager/resource-group-move-resources.md) within hello same, or across different, subscriptions.</span></span>


### <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="8fb07-153">設定 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8fb07-153">Set up an Azure storage account</span></span>

- <span data-ttu-id="8fb07-154">您需要標準/優質 toohold 資料複寫 tooAzure 的 Azure 儲存體帳戶。[高階儲存體](../storage/storage-premium-storage.md)通常用於需要一直居高 IO 效能和低度延遲 toohost IO 密集工作負載的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-154">You need a standard/premium Azure storage account toohold data replicated tooAzure.[Premium storage](../storage/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="8fb07-155">如果您想要 toouse premium 帳戶 toostore 複寫的資料，您也需要標準儲存體帳戶 toostore 複寫記錄檔擷取進行中變更 tooon 內部部署資料。</span><span class="sxs-lookup"><span data-stu-id="8fb07-155">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="8fb07-156">Hello 資源模型，根據您想 toouse 容錯移轉 Azure Vm，您在設定帳戶[Resource Manager 模式](../storage/storage-create-storage-account.md)，或[傳統模式](../storage/storage-create-storage-account-classic-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-156">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/storage-create-storage-account.md), or [classic mode](../storage/storage-create-storage-account-classic-portal.md).</span></span>
- <span data-ttu-id="8fb07-157">建議您在開始之前先設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fb07-157">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="8fb07-158">如果您需要 toodo Site Recovery 部署期間它。</span><span class="sxs-lookup"><span data-stu-id="8fb07-158">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="8fb07-159">hello 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-159">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="8fb07-160">儲存體帳戶之間所使用的站台復原 hello 內的資源群組相同，則無法移動訂用帳戶，或跨不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fb07-160">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


### <a name="prepare-hello-hyper-v-hosts"></a><span data-ttu-id="8fb07-161">準備 hello 與 HYPER-V 主機</span><span class="sxs-lookup"><span data-stu-id="8fb07-161">Prepare hello Hyper-V hosts</span></span>

* <span data-ttu-id="8fb07-162">請確定 hello HYPER-V 主機符合 hello[必要條件](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-162">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).</span></span>
- <span data-ttu-id="8fb07-163">請確定 hello 主機可存取所需的 hello Url。</span><span class="sxs-lookup"><span data-stu-id="8fb07-163">Make sure that hello hosts can access hello required URLs.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="8fb07-164">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="8fb07-164">Create a Recovery Services vault</span></span>
1. <span data-ttu-id="8fb07-165">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-165">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8fb07-166">按一下 [新增] > [監視 + 管理] > [備份和 Site Recovery (OMS)]。</span><span class="sxs-lookup"><span data-stu-id="8fb07-166">Click **New** > **Monitoring + Management** > **Backup and Site Recovery (OMS)**.</span></span>  

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. <span data-ttu-id="8fb07-168">在**名稱**，指定易記名稱 tooidentify hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-168">In **Name**, specify a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="8fb07-169">如果您有多個訂用帳戶，請選取其中一個。</span><span class="sxs-lookup"><span data-stu-id="8fb07-169">If you have more than one subscription, select one of them.</span></span>

4. <span data-ttu-id="8fb07-170">[建立新的資源群組](../azure-resource-manager/resource-group-template-deploy-portal.md) 或選取現有的資源群組，並指定 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="8fb07-170">[Create a new resource group](../azure-resource-manager/resource-group-template-deploy-portal.md) or select an existing one, and specify an Azure region.</span></span> <span data-ttu-id="8fb07-171">機器必須複寫的 toothis 區域。</span><span class="sxs-lookup"><span data-stu-id="8fb07-171">Machines will be replicated toothis region.</span></span> <span data-ttu-id="8fb07-172">支援 toocheck 區域，請參閱中的各地區上市[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-172">toocheck supported regions, see Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>

5. <span data-ttu-id="8fb07-173">如果您想從儀表板 hello tooquickly 存取 hello 保存庫，請按一下**Pin toodashboard**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-173">If you want tooquickly access hello vault from hello Dashboard, click **Pin toodashboard**, and then click **Create**.</span></span>

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

<span data-ttu-id="8fb07-175">hello 新的保存庫會出現在 hello**儀表板** > **所有資源**清單，並在 hello 主要**復原服務保存庫**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8fb07-175">hello new vault appears in hello **Dashboard** > **All resources** list, and on hello main **Recovery Services vaults** blade.</span></span>



## <a name="select-hello-protection-goal"></a><span data-ttu-id="8fb07-176">選取 hello 保護目標</span><span class="sxs-lookup"><span data-stu-id="8fb07-176">Select hello protection goal</span></span>

<span data-ttu-id="8fb07-177">選取您想 tooreplicate，而且想要 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="8fb07-177">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="8fb07-178">在 hello**復原服務保存庫**，選取 hello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-178">In hello **Recovery Services vaults**, select hello vault.</span></span>
2. <span data-ttu-id="8fb07-179">在 [快速入門] 中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="8fb07-179">In **Getting Started**, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. <span data-ttu-id="8fb07-181">在**保護目標**，選取**tooAzure**，然後選取**是的含 HYPER-V**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-181">In **Protection goal**, select **tooAzure**, and select **Yes, with Hyper-V**.</span></span> <span data-ttu-id="8fb07-182">選取**否**tooconfirm 您未使用 VMM。</span><span class="sxs-lookup"><span data-stu-id="8fb07-182">Select **No** tooconfirm you're not using VMM.</span></span> <span data-ttu-id="8fb07-183">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-183">Then click **OK**.</span></span>

    ![選擇目標](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="8fb07-185">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="8fb07-185">Set up hello source environment</span></span>

<span data-ttu-id="8fb07-186">設定 hello HYPER-V 站台、 HYPER-V 主機上安裝 Azure Site Recovery Provider hello 和 hello Azure 復原服務代理程式和 hello 保存庫中註冊 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="8fb07-186">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="8fb07-187">在 [準備基礎結構] 中，按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="8fb07-187">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="8fb07-188">按一下 新的 HYPER-V 站台做為您的 HYPER-V 主機或叢集的容器 tooadd **+ HYPER-V 站台**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-188">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. <span data-ttu-id="8fb07-190">在**建立 HYPER-V 站台**，指定 hello 網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="8fb07-190">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="8fb07-191">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-191">Then click **OK**.</span></span> <span data-ttu-id="8fb07-192">現在，選取您建立，然後按一下 「 hello 」 站台**+ HYPER-V Server** tooadd 伺服器 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="8fb07-192">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. <span data-ttu-id="8fb07-194">在 [新增伺服器] > [伺服器類型] 中，檢查是否已顯示 [Hyper-V 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="8fb07-194">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="8fb07-195">請確定您想要 hello tooadd 符合該 hello HYPER-V 伺服器[必要條件](#on-premises-prerequisites)，和是無法 tooaccess hello 指定的 Url。</span><span class="sxs-lookup"><span data-stu-id="8fb07-195">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="8fb07-196">下載 hello Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="8fb07-196">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="8fb07-197">執行此檔案 tooinstall hello 提供者並 hello 每個 HYPER-V 主機上的復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="8fb07-197">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="8fb07-199">安裝 hello 提供者和代理程式</span><span class="sxs-lookup"><span data-stu-id="8fb07-199">Install hello Provider and agent</span></span>

1. <span data-ttu-id="8fb07-200">您已新增 toohello HYPER-V 站台執行每個主機上的 hello 提供者安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="8fb07-200">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="8fb07-201">如果您安裝在 Hyper-V 叢集上，請在每個叢集節點上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="8fb07-201">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="8fb07-202">安裝和註冊每個 Hyper-V 叢集節點，可確保 VM 即使跨節點移轉，都還是會受保護。</span><span class="sxs-lookup"><span data-stu-id="8fb07-202">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="8fb07-203">在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。</span><span class="sxs-lookup"><span data-stu-id="8fb07-203">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="8fb07-204">在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-204">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="8fb07-205">在**保存庫設定**，按一下 **瀏覽**tooselect hello 保存庫金鑰檔下載。</span><span class="sxs-lookup"><span data-stu-id="8fb07-205">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="8fb07-206">指定 hello Azure Site Recovery 訂用帳戶，hello 保存庫名稱，並所屬 hello HYPER-V 站台 toowhich hello HYPER-V 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-206">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. <span data-ttu-id="8fb07-208">在**Proxy 設定**，指定 HYPER-V 主機上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路的方式。</span><span class="sxs-lookup"><span data-stu-id="8fb07-208">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="8fb07-209">如果您想 hello 提供者 tooconnect 直接選取**直接連接不使用 proxy 的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-209">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="8fb07-210">如果您現有的 proxy 需要驗證，或者您想 toouse 自訂 proxy hello 提供者連接，請選取**連線使用 proxy 伺服器的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-210">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="8fb07-211">如果您使用 Proxy：</span><span class="sxs-lookup"><span data-stu-id="8fb07-211">If you use a proxy:</span></span>
        - <span data-ttu-id="8fb07-212">指定 hello 位址、 連接埠和認證</span><span class="sxs-lookup"><span data-stu-id="8fb07-212">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="8fb07-213">請確定 hello 中所述的 hello Url[必要條件](#prerequisites)允許透過 hello proxy。</span><span class="sxs-lookup"><span data-stu-id="8fb07-213">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![網際網路](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. <span data-ttu-id="8fb07-215">安裝完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。</span><span class="sxs-lookup"><span data-stu-id="8fb07-215">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![安裝位置](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. <span data-ttu-id="8fb07-217">註冊完成之後，Azure Site Recovery 中，擷取中繼資料從 hello HYPER-V 伺服器和中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **HYPER-V 主機**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-217">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="8fb07-218">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="8fb07-218">Set up hello target environment</span></span>

<span data-ttu-id="8fb07-219">指定 hello Azure 儲存體帳戶來進行複寫，並容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="8fb07-219">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="8fb07-220">按一下 [準備基礎結構] > [目標]。</span><span class="sxs-lookup"><span data-stu-id="8fb07-220">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="8fb07-221">選取 hello 訂用帳戶與您想 toocreate hello Azure Vm 容錯移轉之後的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8fb07-221">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="8fb07-222">選擇 hello 部署模型的 toouse Azure （classic 或資源管理） 中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="8fb07-222">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="8fb07-223">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-223">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="8fb07-224">如果您沒有儲存體帳戶，按一下**+ 儲存體**toocreate 資源管理員帳戶內嵌。</span><span class="sxs-lookup"><span data-stu-id="8fb07-224">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> <span data-ttu-id="8fb07-225">深入了解[儲存體需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-225">Read about [storage requirements](site-recovery-prereq.md#azure-requirements).</span></span>
    - <span data-ttu-id="8fb07-226">如果您沒有 Azure 網路，按一下**+ 網路**toocreate 資源管理員為基礎的網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="8fb07-226">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>

    ![儲存體](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a><span data-ttu-id="8fb07-228">設定複寫設定</span><span class="sxs-lookup"><span data-stu-id="8fb07-228">Configure replication settings</span></span>

1. <span data-ttu-id="8fb07-229">toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-229">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![網路](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. <span data-ttu-id="8fb07-231">在 [建立及關聯原則] 中指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="8fb07-231">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="8fb07-232">在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="8fb07-232">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="8fb07-233">複寫 toopremium 存放裝置時，不支援第二個頻率為 30。</span><span class="sxs-lookup"><span data-stu-id="8fb07-233">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="8fb07-234">hello 限制取決於 hello 高階儲存體所支援的每個 blob (100) 的快照集數目。</span><span class="sxs-lookup"><span data-stu-id="8fb07-234">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="8fb07-235">[深入了解](../storage/storage-premium-storage.md#snapshots-and-copy-blob)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-235">[Learn more](../storage/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="8fb07-236">在**復原點保留**，指定以小時多久 hello 保留週期是每個復原點。</span><span class="sxs-lookup"><span data-stu-id="8fb07-236">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="8fb07-237">Vm 就能復原 tooany 視窗內的點。</span><span class="sxs-lookup"><span data-stu-id="8fb07-237">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="8fb07-238">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-238">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>

    - <span data-ttu-id="8fb07-239">HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。</span><span class="sxs-lookup"><span data-stu-id="8fb07-239">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="8fb07-240">應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。</span><span class="sxs-lookup"><span data-stu-id="8fb07-240">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="8fb07-241">如果您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="8fb07-241">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="8fb07-242">確定您設定的 hello 值小於 hello 您設定其他復原點數目。</span><span class="sxs-lookup"><span data-stu-id="8fb07-242">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

6. <span data-ttu-id="8fb07-243">在**初始複寫開始時間**，指定當 toostart hello 初始複寫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-243">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="8fb07-244">hello 發生複寫的網際網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。</span><span class="sxs-lookup"><span data-stu-id="8fb07-244">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="8fb07-245">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-245">Then click **OK**.</span></span>

    ![複寫原則](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

<span data-ttu-id="8fb07-247">當您建立新的原則時，它會自動與相關聯 hello HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="8fb07-247">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="8fb07-248">您可以將 HYPER-V 站台 （和中的 hello Vm） 中的多個複寫原則與**複寫**> 原則名稱 >**關聯 HYPER-V 站台**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-248">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>

## <a name="capacity-planning"></a><span data-ttu-id="8fb07-249">容量規劃</span><span class="sxs-lookup"><span data-stu-id="8fb07-249">Capacity planning</span></span>

<span data-ttu-id="8fb07-250">您現已設定您的基本基礎結構，您可以思考容量規劃並找出您是否需要額外的資源。</span><span class="sxs-lookup"><span data-stu-id="8fb07-250">Now that you have your basic infrastructure set up, you can think about capacity planning, and figure out whether you need additional resources.</span></span>

<span data-ttu-id="8fb07-251">站台復原提供容量規劃 toohelp 讓您針對計算、 網路及存放裝置配置 hello 正確的資源。</span><span class="sxs-lookup"><span data-stu-id="8fb07-251">Site Recovery provides a capacity planner toohelp you allocate hello right resources for compute, networking, and storage.</span></span> <span data-ttu-id="8fb07-252">您可以執行 hello 規劃 detailed 模式或快速模式的 Vm、 磁碟和儲存體的平均數目為基礎的估計中使用自訂的數字在 hello 工作負載層級。</span><span class="sxs-lookup"><span data-stu-id="8fb07-252">You can run hello planner in quick mode for estimations based on an average number of VMs, disks, and storage, or in detailed mode with customized numbers at hello workload level.</span></span> <span data-ttu-id="8fb07-253">開始之前，您必須︰</span><span class="sxs-lookup"><span data-stu-id="8fb07-253">Before you start you need to:</span></span>

* <span data-ttu-id="8fb07-254">收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。</span><span class="sxs-lookup"><span data-stu-id="8fb07-254">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
* <span data-ttu-id="8fb07-255">評估 hello 每日變更 （變換） 速率複寫的資料。</span><span class="sxs-lookup"><span data-stu-id="8fb07-255">Estimate hello daily change (churn) rate for your replicated data.</span></span> <span data-ttu-id="8fb07-256">您可以使用 hello [HYPER-V 複本的容量規劃](https://www.microsoft.com/download/details.aspx?id=39057)toohelp 執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="8fb07-256">You can use hello [Capacity Planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) toohelp you do this.</span></span>

1. <span data-ttu-id="8fb07-257">按一下**下載**toodownload hello 工具，並加以執行。</span><span class="sxs-lookup"><span data-stu-id="8fb07-257">Click **Download** toodownload hello tool, and then run it.</span></span> <span data-ttu-id="8fb07-258">[閱讀文章 hello](site-recovery-capacity-planner.md) ，伴隨著 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="8fb07-258">[Read hello article](site-recovery-capacity-planner.md) that accompanies hello tool.</span></span>
2. <span data-ttu-id="8fb07-259">當您完成時，選取**是**中**已執行 hello 容量規劃**嗎？</span><span class="sxs-lookup"><span data-stu-id="8fb07-259">When you’re done, select **Yes** in **Have you run hello Capacity Planner**?</span></span>

   ![容量規劃](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

<span data-ttu-id="8fb07-261">深入了解[控制網路頻寬](#network-bandwidth-considerations)</span><span class="sxs-lookup"><span data-stu-id="8fb07-261">Learn more about [controlling network bandwidth](#network-bandwidth-considerations)</span></span>



## <a name="enable-replication"></a><span data-ttu-id="8fb07-262">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="8fb07-262">Enable replication</span></span>

<span data-ttu-id="8fb07-263">在開始之前，請確定您的 Azure 使用者帳戶具有所需的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-263">Before you start, ensure that your Azure user account has hello required  [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

<span data-ttu-id="8fb07-264">啟用 VM 複寫，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8fb07-264">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="8fb07-265">按一下 [複寫應用程式] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="8fb07-265">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="8fb07-266">您已設定第一次的 hello 複寫之後，您可以按一下**+ 複寫**tooenable 其他機器複寫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-266">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. <span data-ttu-id="8fb07-268">在**來源**，選取 hello HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="8fb07-268">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="8fb07-269">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-269">Then click **OK**.</span></span>
3. <span data-ttu-id="8fb07-270">在**目標**選取 hello 保存庫訂用帳戶，hello 想在容錯移轉之後 toouse Azure （classic 或資源管理） 中的容錯移轉模式。</span><span class="sxs-lookup"><span data-stu-id="8fb07-270">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="8fb07-271">選取您想 toouse hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fb07-271">Select hello storage account you want toouse.</span></span> <span data-ttu-id="8fb07-272">如果您沒有您想要讓 toouse 帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-272">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="8fb07-273">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-273">Then click **OK**.</span></span>
5. <span data-ttu-id="8fb07-274">正在建立容錯移轉時，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="8fb07-274">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="8fb07-275">選取 tooapply hello 網路設定 tooall 機器啟用複寫，**現在選取的機器設定**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-275">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="8fb07-276">選取**稍後設定**tooselect hello 每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-276">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="8fb07-277">如果您沒有您想 toouse 網路，您可以[建立一個](#set-up-an-azure-network)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-277">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="8fb07-278">選取適用的子網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-278">Select a subnet if applicable.</span></span> <span data-ttu-id="8fb07-279">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-279">Then click **OK**.</span></span>

   ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. <span data-ttu-id="8fb07-281">在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-281">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="8fb07-282">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-282">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="8fb07-283">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-283">Then click **OK**.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="8fb07-285">在**屬性** > **設定屬性**hello 作業系統選取的 hello 選取 Vm，hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-285">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="8fb07-286">確認該 hello Azure VM 名稱 （目標） 符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-286">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="8fb07-287">根據預設，所有 hello 磁碟的 hello VM 都選取複寫，但是您可以清除磁碟 tooexclude 它們。</span><span class="sxs-lookup"><span data-stu-id="8fb07-287">By default all hello disks of hello VM are selected for replication, but you can clear disks tooexclude them.</span></span>
    - <span data-ttu-id="8fb07-288">您可能想 tooexclude 磁碟 tooreduce 複寫的頻寬。</span><span class="sxs-lookup"><span data-stu-id="8fb07-288">You might want tooexclude disks tooreduce replication bandwidth.</span></span> <span data-ttu-id="8fb07-289">例如，您可能不想 tooreplicate 磁碟取代為暫存資料，或重新整理每次在電腦或應用程式的資料會重新啟動 （例如 pagefile.sys 或 Microsoft SQL Server tempdb）。</span><span class="sxs-lookup"><span data-stu-id="8fb07-289">For example, you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or apps restarts (such as pagefile.sys or Microsoft SQL Server tempdb).</span></span> <span data-ttu-id="8fb07-290">您可以取消選取 hello 磁碟從複寫排除 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-290">You can exclude hello disk from replication by unselecting hello disk.</span></span>
    - <span data-ttu-id="8fb07-291">只有基本磁碟可以排除。</span><span class="sxs-lookup"><span data-stu-id="8fb07-291">Only basic disks can be exclude.</span></span> <span data-ttu-id="8fb07-292">您無法排除作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-292">You can't exclude OS disks.</span></span>
    - <span data-ttu-id="8fb07-293">我們建議不要排除動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-293">We recommend that you don't exclude dynamic disks.</span></span> <span data-ttu-id="8fb07-294">Site Recovery 無法識別客體 VM 內的虛擬硬碟為基本還是動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-294">Site Recovery can't identify whether a virtual hard disk inside a guest VM is basic or dynamic.</span></span> <span data-ttu-id="8fb07-295">如果所有相依的動態磁碟區磁碟不排除，hello 受保護的動態磁碟會顯示失敗的磁碟時 hello VM 容錯移轉，而且您無法存取該磁碟上的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="8fb07-295">If all dependent dynamic volume disks aren't excluded, hello protected dynamic disk will show as a failed disk when hello VM fails over, and hello data on that disk won't be accessible.</span></span>
        - <span data-ttu-id="8fb07-296">啟用複寫後，您無法加入或移除複寫的磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-296">After replication is enabled, you can't add or remove disks for replication.</span></span> <span data-ttu-id="8fb07-297">如果您想 tooadd 或排除磁碟，您需要 toodisable 保護 hello VM，並重新啟用它。</span><span class="sxs-lookup"><span data-stu-id="8fb07-297">If you want tooadd or exclude a disk, you need toodisable protection for hello VM, and then re-enable it.</span></span>
        - <span data-ttu-id="8fb07-298">您以手動方式在 Azure 中建立的磁碟將不會容錯回復。</span><span class="sxs-lookup"><span data-stu-id="8fb07-298">Disks you create manually in Azure aren't failed back.</span></span> <span data-ttu-id="8fb07-299">比方說，如果您無法超過三個磁碟，並建立兩個直接在 Azure VM 中，只有 hello 三個磁碟已容錯移轉將無法從 Azure tooHyper-V。</span><span class="sxs-lookup"><span data-stu-id="8fb07-299">For example, if you fail over three disks, and create two directly in Azure VM, only hello three disks which were failed over will be failed back from Azure tooHyper-V.</span></span> <span data-ttu-id="8fb07-300">您不能包含在容錯回復，或從 HYPER-V tooAzure 的反向複寫以手動方式建立的磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-300">You can't include disks created manually in failback, or in reverse replication from Hyper-V tooAzure.</span></span>
        - <span data-ttu-id="8fb07-301">如果您排除的應用程式 toooperate 所需的磁碟，在容錯移轉 tooAzure 之後您需要的 toocreate 它以手動方式在 Azure 中，因此該 hello 複寫應用程式可以執行。</span><span class="sxs-lookup"><span data-stu-id="8fb07-301">If you exclude a disk that's needed for an application toooperate, after failover tooAzure you need toocreate it manually in Azure, so that hello replicated application can run.</span></span> <span data-ttu-id="8fb07-302">或者，您無法將 Azure 自動化整合至復原計劃，hello 機器容錯移轉期間 toocreate hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="8fb07-302">Alternatively, you could integrate Azure automation into a recovery plan, toocreate hello disk during failover of hello machine.</span></span>

10. <span data-ttu-id="8fb07-303">按一下**確定**toosave 變更。</span><span class="sxs-lookup"><span data-stu-id="8fb07-303">Click **OK** toosave changes.</span></span> <span data-ttu-id="8fb07-304">您可以稍後再設定其他屬性。</span><span class="sxs-lookup"><span data-stu-id="8fb07-304">You can set additional properties later.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="8fb07-306">在**複寫設定** > **設定複寫設定**，選取您想 tooapply hello 受保護 Vm 的 hello 複寫原則。</span><span class="sxs-lookup"><span data-stu-id="8fb07-306">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="8fb07-307">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8fb07-307">Then click **OK**.</span></span> <span data-ttu-id="8fb07-308">您可以修改中的 hello 複寫原則**複寫原則**> 原則名稱 >**編輯設定**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-308">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="8fb07-309">您套用的變更將用於已在複寫的機器和新的機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-309">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

<span data-ttu-id="8fb07-311">您可以追蹤進度的 hello**啟用保護**作業中**作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-311">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="8fb07-312">之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="8fb07-312">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>

### <a name="view-and-manage-vm-properties"></a><span data-ttu-id="8fb07-313">檢視及管理 VM 屬性</span><span class="sxs-lookup"><span data-stu-id="8fb07-313">View and manage VM properties</span></span>

<span data-ttu-id="8fb07-314">我們建議您確認 hello hello 來源機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="8fb07-314">We recommend that you verify hello properties of hello source machine.</span></span>

1. <span data-ttu-id="8fb07-315">在**受保護項目**，按一下 **複寫的項目**，並選取 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-315">In **Protected Items**, click **Replicated Items**, and select hello machine.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. <span data-ttu-id="8fb07-317">在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。</span><span class="sxs-lookup"><span data-stu-id="8fb07-317">In **Properties**, you can view replication and failover information for hello VM.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. <span data-ttu-id="8fb07-319">在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。</span><span class="sxs-lookup"><span data-stu-id="8fb07-319">In **Compute and Network** > **Compute properties**, you can specify hello Azure VM name and target size.</span></span> <span data-ttu-id="8fb07-320">如果您需要，修改 hello 名稱 toocomply Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="8fb07-320">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="8fb07-321">您也可以檢視和修改 hello 目標網路、 子網路及指派 toohello Azure VM 的 IP 位址資訊。</span><span class="sxs-lookup"><span data-stu-id="8fb07-321">You can also view and modify information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span> <span data-ttu-id="8fb07-322">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="8fb07-322">Note hello following:</span></span>

   * <span data-ttu-id="8fb07-323">您可以設定 hello 目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8fb07-323">You can set hello target IP address.</span></span> <span data-ttu-id="8fb07-324">如果您沒有提供的地址，hello 無法容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="8fb07-324">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="8fb07-325">如果您將無法使用在容錯移轉的位址，hello 容錯移轉將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8fb07-325">If you set an address that isn't available at failover, hello failover will fail.</span></span> <span data-ttu-id="8fb07-326">相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。</span><span class="sxs-lookup"><span data-stu-id="8fb07-326">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>
   * <span data-ttu-id="8fb07-327">hello 大小，如下所示為 hello 目標虛擬機器，指定的網路介面卡的 hello 數目會取決於：</span><span class="sxs-lookup"><span data-stu-id="8fb07-327">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

     * <span data-ttu-id="8fb07-328">如果 hello hello 來源電腦上的網路介面卡數目小於或等於 toohello 數目的介面卡允許 hello 目標機器的大小，則會有 hello 目標 hello 做 hello 來源的相同數目的介面卡。</span><span class="sxs-lookup"><span data-stu-id="8fb07-328">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
     * <span data-ttu-id="8fb07-329">如果 hello hello 來源虛擬機器介面卡的數目超過允許將使用 hello 目標大小則 hello 目標大小上限的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8fb07-329">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
     * <span data-ttu-id="8fb07-330">例如，如果來源機器有兩個網路介面卡，而且 hello 目標機器大小支援四個，hello 目標電腦會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="8fb07-330">For example if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="8fb07-331">如果 hello 來源機器有兩張介面卡，但 hello 支援的目標大小只支援一個 hello 目標電腦會有一個配接器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-331">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>     
     * <span data-ttu-id="8fb07-332">如果 hello VM 有多張網路介面卡將所有連線 toohello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="8fb07-332">If hello VM has multiple network adapters they will all connect toohello same network.</span></span>
     * <span data-ttu-id="8fb07-333">如果 hello 虛擬機器有多個網路介面卡則 hello 先 hello 清單所示的其中一個會變成 hello*預設*hello Azure 虛擬機器中的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="8fb07-333">If hello virtual machine has multiple network adapters then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure virtual machine.</span></span>

     ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. <span data-ttu-id="8fb07-335">在**磁碟**、 您所見 hello 作業系統和資料磁碟上的 hello 將複寫的 VM。</span><span class="sxs-lookup"><span data-stu-id="8fb07-335">In **Disks**, you can see hello operating system and data disks on hello VM that will be replicated.</span></span>

#### <a name="managed-disks"></a><span data-ttu-id="8fb07-336">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="8fb07-336">Managed disks</span></span>

<span data-ttu-id="8fb07-337">在**計算與網路** > **計算屬性**，如果您想要在移轉 tooAzure tooattach 受管理的磁碟 tooyour 機器，您可以設定 「 使用受管理磁碟 」 設定太"Yes"hello VM。</span><span class="sxs-lookup"><span data-stu-id="8fb07-337">In **Compute and Network** > **Compute properties**, you can set "Use managed disks" setting too"Yes" for hello VM if you want tooattach managed disks tooyour machine on migration tooAzure.</span></span> <span data-ttu-id="8fb07-338">受管理的磁碟，藉以管理 hello 與 hello VM 磁碟相關聯的儲存體帳戶，簡化 Azure IaaS Vm 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="8fb07-338">Managed disks simplifies disk management for Azure IaaS VMs by managing hello storage accounts associated with hello VM disks.</span></span> <span data-ttu-id="8fb07-339">[深入了解受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-339">[Learn More about managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).</span></span>

   - <span data-ttu-id="8fb07-340">受管理的磁碟是已建立並附加 toohello 只能在容錯移轉 tooAzure 上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-340">Managed disks are created and attached toohello virtual machine only on a failover tooAzure.</span></span> <span data-ttu-id="8fb07-341">啟用保護之後，在內部部署機器的資料會繼續 tooreplicate toostorage 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fb07-341">On enabling protection, data from on-premises machines will continue tooreplicate toostorage accounts.</span></span>
   <span data-ttu-id="8fb07-342">受管理的磁碟只可以建立使用 hello 資源管理員部署模型部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-342">Managed disks can be created only for virtual machines deployed using hello Resource manager deployment model.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8fb07-343">從 Azure tooon 部署的 HYPER-V 環境中的容錯回復目前不支援受管理的磁碟使用的機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-343">Failback from Azure tooon-premises Hyper-V environment is not currently supported for machines with managed disks.</span></span> <span data-ttu-id="8fb07-344">「 使用受管理磁碟 」 太"Yes"時才設定此機器 tooAzure 想 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="8fb07-344">Set "Use managed disks" too"Yes" only if you intend toomigrate this machine tooAzure.</span></span>

   - <span data-ttu-id="8fb07-345">當您設定 「 使用受管理磁碟 」 太"Yes"時，只可用性設定組 hello 資源群組中的使用 「 使用受管理磁碟 」 組太"Yes"時將可讓您選取。</span><span class="sxs-lookup"><span data-stu-id="8fb07-345">When you set "Use managed disks" too"Yes", only availability sets in hello resource group with "Use managed disks" set too"Yes" would be available for selection.</span></span> <span data-ttu-id="8fb07-346">這是因為受管理的磁碟與虛擬機器只能太 「 是 」 是 「 受管理的使用磁碟 」 屬性設定的可用性設定組的一部分。</span><span class="sxs-lookup"><span data-stu-id="8fb07-346">This is because virtual machines with managed disks can only be part of availability sets with "Use managed disks" property set too"Yes".</span></span> <span data-ttu-id="8fb07-347">請確定您使用 「 使用受管理磁碟 」 屬性集，根據您在容錯移轉的受管理的意圖 toouse 磁碟建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8fb07-347">Make sure that you create availability sets with "Use managed disks" property set based on your intent toouse managed disks on failover.</span></span> <span data-ttu-id="8fb07-348">同樣地，當您設定 「 使用受管理磁碟 」 太"No"時，只有與 「 使用受管理磁碟 」 的屬性設定太"No"hello 資源群組中的可用性設定組將可讓您選取。</span><span class="sxs-lookup"><span data-stu-id="8fb07-348">Likewise, when you set "Use managed disks" too"No", only availability sets in hello resource group with "Use managed disks" property set too"No" would be available for selection.</span></span> <span data-ttu-id="8fb07-349">[深入了解受控磁碟和可用性設定組](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-349">[Learn more about managed disks and availability sets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span></span>

  > [!NOTE]
  > <span data-ttu-id="8fb07-350">如果 hello 儲存體帳戶用於複寫加密所使用的儲存體服務加密的任何一點的時間，在容錯移轉期間建立受管理的磁碟將會失敗。</span><span class="sxs-lookup"><span data-stu-id="8fb07-350">If hello storage account used for replication was encrypted with Storage Service Encryption at any point in time, creation of managed disks during failover will fail.</span></span> <span data-ttu-id="8fb07-351">您可以設定 「 使用受管理磁碟 」 太"No"時和重試容錯移轉或停用 hello 虛擬機器的保護和 tooa 儲存體帳戶沒有時間啟用在任何時間點的儲存體服務加密可保護它。</span><span class="sxs-lookup"><span data-stu-id="8fb07-351">You can either set "Use managed disks" too"No" and retry failover or disable protection for hello virtual machine and protect it tooa storage account which did not have Storage service encryption enabled at any point in time.</span></span>
  > <span data-ttu-id="8fb07-352">[深入了解儲存體服務加密及受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-352">[Learn more about Storage service encryption and managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="test-hello-deployment"></a><span data-ttu-id="8fb07-353">測試 hello 部署</span><span class="sxs-lookup"><span data-stu-id="8fb07-353">Test hello deployment</span></span>

<span data-ttu-id="8fb07-354">您可以執行單一的虛擬機器或包含一或多個虛擬機器的復原計劃的測試容錯移轉 tootest hello 部署。</span><span class="sxs-lookup"><span data-stu-id="8fb07-354">tootest hello deployment you can run a test failover for a single virtual machine or a recovery plan that contains one or more virtual machines.</span></span>

### <a name="before-you-start"></a><span data-ttu-id="8fb07-355">開始之前</span><span class="sxs-lookup"><span data-stu-id="8fb07-355">Before you start</span></span>

 - <span data-ttu-id="8fb07-356">如果您想 tooconnect tooAzure Vm 容錯移轉之後，使用 RDP 深入了解[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-356">If you want tooconnect tooAzure VMs using RDP after failover, learn about [preparing tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="8fb07-357">您在測試環境中需要 Active Directory 和 DNS 的 toocopy toofully 測試。</span><span class="sxs-lookup"><span data-stu-id="8fb07-357">toofully test you need toocopy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="8fb07-358">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-358">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="8fb07-359">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="8fb07-359">Run a test failover</span></span>

1. <span data-ttu-id="8fb07-360">透過單一電腦、 toofail 中**複寫的項目**，按一下 hello VM > **+ 測試容錯移轉**圖示。</span><span class="sxs-lookup"><span data-stu-id="8fb07-360">toofail over a single machine, in **Replicated Items**, click hello VM > **+Test Failover** icon.</span></span>
2. <span data-ttu-id="8fb07-361">toofail 透過復原計劃，在**復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-361">toofail over a recovery plan, in **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="8fb07-362">復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="8fb07-362">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>
3. <span data-ttu-id="8fb07-363">在**測試容錯移轉**，選取容錯移轉發生後，將會連接 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="8fb07-363">In **Test Failover**, select hello Azure network toowhich Azure VMs will be connected after failover occurs.</span></span>
4. <span data-ttu-id="8fb07-364">按一下**確定**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="8fb07-364">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="8fb07-365">您可以追蹤進度，藉由按 hello VM tooopen 其屬性，或是在 hello**測試容錯移轉**作業在保存庫名稱 >**作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-365">You can track progress by clicking on hello VM tooopen its properties, or on hello **Test Failover** job in vault name > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="8fb07-366">Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-366">After hello failover completes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="8fb07-367">您應該確定該 hello VM 是 hello 適當大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="8fb07-367">You should make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="8fb07-368">如果您在容錯移轉之後連接備妥，您應該能夠 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="8fb07-368">If you prepared for connections after failover, you should be able tooconnect toohello Azure VM.</span></span>
7. <span data-ttu-id="8fb07-369">一旦您完成時，按一下**清除測試容錯移轉**hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="8fb07-369">Once you're done, click on **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="8fb07-370">在**備忘稿**記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="8fb07-370">In **Notes** record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="8fb07-371">這將刪除 hello 測試容錯移轉期間所建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-371">This will delete hello virtual machines that were created during test failover.</span></span>

<span data-ttu-id="8fb07-372">如需詳細資訊，請閱讀 hello[測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8fb07-372">For more details, read hello [Test failover tooAzure](site-recovery-test-failover-to-azure.md) article.</span></span>



## <a name="monitor-hello-deployment"></a><span data-ttu-id="8fb07-373">監視 hello 部署</span><span class="sxs-lookup"><span data-stu-id="8fb07-373">Monitor hello deployment</span></span>

<span data-ttu-id="8fb07-374">Hello 組態設定、 狀態和站台復原部署的健全狀況監視：</span><span class="sxs-lookup"><span data-stu-id="8fb07-374">Monitor hello configuration settings, status, and health for your Site Recovery deployment:</span></span>

1. <span data-ttu-id="8fb07-375">按一下 hello 保存庫名稱 tooaccess hello **Essentials**儀表板。</span><span class="sxs-lookup"><span data-stu-id="8fb07-375">Click on hello vault name tooaccess hello **Essentials** dashboard.</span></span> <span data-ttu-id="8fb07-376">在此儀表板中，您可以追蹤 Site Recovery 作業、複寫狀態、復原方案、伺服器健康情況和事件。</span><span class="sxs-lookup"><span data-stu-id="8fb07-376">In this dashboard you can track Site Recovery jobs, replication status, recovery plans, server health, and events.</span></span>  

    ![基本資訊](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. <span data-ttu-id="8fb07-378">在 hello**健全狀況**磚，您可以監視發生問題，並 hello 引發的事件 Site recovery hello 過去 24 小時內的站台伺服器。</span><span class="sxs-lookup"><span data-stu-id="8fb07-378">In hello **Health** tile you can monitor site servers that are experiencing issue, and hello events raised by Site Recovery in hello last 24 hours.</span></span> <span data-ttu-id="8fb07-379">您可以自訂 Essentials tooshow hello 磚和配置的是最有用的 tooyou，包括 hello 狀態的其他站台復原和備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="8fb07-379">You can customize Essentials tooshow hello tiles and layouts that are most useful tooyou, including hello status of other Site Recovery and Backup vaults.</span></span>
3. <span data-ttu-id="8fb07-380">您可以管理和監視複寫的 hello**複寫的項目**，**復原計劃**，和**站台復原作業**磚。</span><span class="sxs-lookup"><span data-stu-id="8fb07-380">You can manage and monitor replication in hello **Replicated Items**, **Recovery Plans**, and **Site Recovery Jobs** tiles.</span></span> <span data-ttu-id="8fb07-381">您可以在 [作業]  >  [Site Recovery 作業] 中鑽研作業以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8fb07-381">You can drill into jobs for more details in **Jobs** > **Site Recovery Jobs**.</span></span>

## <a name="command-line-provider-and-agent-installation"></a><span data-ttu-id="8fb07-382">命令列 Provider 和代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="8fb07-382">Command-line Provider and agent installation</span></span>

<span data-ttu-id="8fb07-383">hello Azure Site Recovery Provider 代理程式也可以被安裝和使用下列命令列的 hello。</span><span class="sxs-lookup"><span data-stu-id="8fb07-383">hello Azure Site Recovery Provider and agent can also be installed using hello following command line.</span></span> <span data-ttu-id="8fb07-384">這個方法可以是使用的 tooinstall hello 的提供者的 Windows Server 2012 R2 的 Server Core 上。</span><span class="sxs-lookup"><span data-stu-id="8fb07-384">This method can be used tooinstall hello provider on a Server Core for Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="8fb07-385">下載 hello 提供者安裝檔案和註冊金鑰 tooa 資料夾。</span><span class="sxs-lookup"><span data-stu-id="8fb07-385">Download hello Provider installation file and registration key tooa folder.</span></span> <span data-ttu-id="8fb07-386">例如 C:\ASR。</span><span class="sxs-lookup"><span data-stu-id="8fb07-386">For example C:\ASR.</span></span>
2. <span data-ttu-id="8fb07-387">從提升權限的命令提示字元中執行這些命令 tooextract hello 提供者安裝程式：</span><span class="sxs-lookup"><span data-stu-id="8fb07-387">From an elevated command prompt, run these commands tooextract hello Provider installer:</span></span>

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="8fb07-388">執行這個命令 tooinstall hello 元件：</span><span class="sxs-lookup"><span data-stu-id="8fb07-388">Run this command tooinstall hello components:</span></span>

            C:\ASR> setupdr.exe /i
4. <span data-ttu-id="8fb07-389">然後伺服器上執行這些命令 tooregister hello hello 保存庫中：</span><span class="sxs-lookup"><span data-stu-id="8fb07-389">Then run these commands tooregister hello server in hello vault:</span></span>

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file>

<br/>
<span data-ttu-id="8fb07-390">其中：</span><span class="sxs-lookup"><span data-stu-id="8fb07-390">Where:</span></span>

* <span data-ttu-id="8fb07-391">**/ 認證**： 指定 hello 位置中的 hello 註冊金鑰檔所在的必要參數</span><span class="sxs-lookup"><span data-stu-id="8fb07-391">**/Credentials**: Mandatory parameter that specifies hello location in which hello registration key file is located</span></span>  
* <span data-ttu-id="8fb07-392">**/Friendlyname**: hello 名稱出現在 hello Azure Site Recovery 入口網站中的 hello HYPER-V 主機伺服器的必要參數。</span><span class="sxs-lookup"><span data-stu-id="8fb07-392">**/FriendlyName**: Mandatory parameter for hello name of hello Hyper-V host server that appears in hello Azure Site Recovery portal.</span></span>
* <span data-ttu-id="8fb07-393">**/proxyAddress**： 指定 hello hello proxy 伺服器位址的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="8fb07-393">**/proxyAddress**: Optional parameter that specifies hello address of hello proxy server.</span></span>
* <span data-ttu-id="8fb07-394">**/proxyport** ： 指定 hello hello proxy 伺服器的連接埠的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="8fb07-394">**/proxyport** : Optional parameter that specifies hello port of hello proxy server.</span></span>
* <span data-ttu-id="8fb07-395">**/proxyUsername**： 指定 hello Proxy 使用者名稱 （如果 proxy 需要驗證） 的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="8fb07-395">**/proxyUsername**: Optional parameter that specifies hello Proxy user name (if proxy requires authentication).</span></span>
* <span data-ttu-id="8fb07-396">**/proxyPassword**： 指定的選擇性參數 hello 密碼進行驗證的 hello proxy 伺服器 （proxy 需要驗證）。</span><span class="sxs-lookup"><span data-stu-id="8fb07-396">**/proxyPassword**: Optional parameter that specifies hello Password for authenticating with hello proxy server (if proxy requires authentication).</span></span>


## <a name="network-bandwidth-considerations"></a><span data-ttu-id="8fb07-397">網路頻寬考量</span><span class="sxs-lookup"><span data-stu-id="8fb07-397">Network bandwidth considerations</span></span>
<span data-ttu-id="8fb07-398">您可以使用 hello [HYPER-V 產能規劃工具](site-recovery-capacity-planner.md)toocalculate hello 頻寬，您需要複寫 （初始複寫，然後差異處）。</span><span class="sxs-lookup"><span data-stu-id="8fb07-398">You can use hello [Hyper-V capacity planner tool](site-recovery-capacity-planner.md) toocalculate hello bandwidth you need for replication (initial replication and then delta).</span></span> <span data-ttu-id="8fb07-399">toocontrol hello 數量的複寫的頻寬使用量，您有幾個選項：</span><span class="sxs-lookup"><span data-stu-id="8fb07-399">toocontrol hello amount of bandwidth use for replication you have a few options:</span></span>

* <span data-ttu-id="8fb07-400">**節流的頻寬**: HYPER-V 複寫 tooAzure 流量透過特定的 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="8fb07-400">**Throttle bandwidth**: Hyper-V traffic that replicates tooAzure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="8fb07-401">您可以節流處理 hello 主機伺服器上的頻寬。</span><span class="sxs-lookup"><span data-stu-id="8fb07-401">You can throttle bandwidth on hello host server.</span></span>
* <span data-ttu-id="8fb07-402">**調整頻寬**： 您可能會影響用來複寫使用數個登錄機碼的 hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="8fb07-402">**Tweak bandwidth**: You can influence hello bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="8fb07-403">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="8fb07-403">Throttle bandwidth</span></span>
1. <span data-ttu-id="8fb07-404">開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機伺服器上。</span><span class="sxs-lookup"><span data-stu-id="8fb07-404">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host server.</span></span> <span data-ttu-id="8fb07-405">依預設 Microsoft Azure 備份的捷徑。 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin</span><span class="sxs-lookup"><span data-stu-id="8fb07-405">By default a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="8fb07-406">在 [hello] 嵌入式管理單元中按一下**變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-406">In hello snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="8fb07-407">在 hello**節流**索引標籤上選取**啟用網際網路頻寬使用節流設定的備份操作**，並設定工作的 hello 限制和非工作小時。</span><span class="sxs-lookup"><span data-stu-id="8fb07-407">On hello **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set hello limits for work and non-work hours.</span></span> <span data-ttu-id="8fb07-408">有效範圍是從每秒 512 Kbps too102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="8fb07-408">Valid ranges are from 512 Kbps too102 Mbps per second.</span></span>

    ![節流頻寬](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

<span data-ttu-id="8fb07-410">您也可以使用 hello [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 節流。</span><span class="sxs-lookup"><span data-stu-id="8fb07-410">You can also use hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset throttling.</span></span> <span data-ttu-id="8fb07-411">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="8fb07-411">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="8fb07-412">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="8fb07-412">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="8fb07-413">影響網路頻寬</span><span class="sxs-lookup"><span data-stu-id="8fb07-413">Influence network bandwidth</span></span>
1. <span data-ttu-id="8fb07-414">Hello 登錄中瀏覽過**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-414">In hello registry navigate too**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="8fb07-415">tooinfluence hello 頻寬流量複寫在磁碟上，修改 hello 值 hello **UploadThreadsPerVM**，或建立 hello 索引鍵，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="8fb07-415">tooinfluence hello bandwidth traffic on a replicating disk, modify hello value hello **UploadThreadsPerVM**, or create hello key if it doesn't exist.</span></span>
   * <span data-ttu-id="8fb07-416">從 Azure 容錯回復流量 tooinfluence hello 頻寬修改 hello 值**DownloadThreadsPerVM**。</span><span class="sxs-lookup"><span data-stu-id="8fb07-416">tooinfluence hello bandwidth for failback traffic from Azure, modify hello value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="8fb07-417">hello 預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="8fb07-417">hello default value is 4.</span></span> <span data-ttu-id="8fb07-418">在 「 超量佈建 」 的網路中，應該從 hello 預設值變更這些登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="8fb07-418">In an “overprovisioned” network, these registry keys should be changed from hello default values.</span></span> <span data-ttu-id="8fb07-419">hello 上限為 32。</span><span class="sxs-lookup"><span data-stu-id="8fb07-419">hello maximum is 32.</span></span> <span data-ttu-id="8fb07-420">監視流量 toooptimize hello 值。</span><span class="sxs-lookup"><span data-stu-id="8fb07-420">Monitor traffic toooptimize hello value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fb07-421">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fb07-421">Next steps</span></span>

<span data-ttu-id="8fb07-422">初始複寫完成，並測試過 hello 部署之後，您可以在 hello 需要時叫用容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="8fb07-422">After initial replication is complete, and you've tested hello deployment, you can invoke failovers as hello need arises.</span></span> <span data-ttu-id="8fb07-423">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="8fb07-423">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
