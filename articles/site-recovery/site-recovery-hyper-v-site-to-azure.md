---
title: "將 Hyper-V VM 複寫至 Azure | Microsoft Docs"
description: "說明如何將內部部署 Hyper-V VM 針對 Azure 進行協調複寫、容錯移轉及復原"
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
ms.openlocfilehash: 8a2ea92759a777b1178fbfe8084a97eec931f709
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure-using-azure-site-recovery-with-the-azure-portal"></a><span data-ttu-id="81f47-103">使用 Azure Site Recovery 搭配 Azure 入口網站將 Hyper-V 虛擬機器 (不使用 VMM) 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="81f47-103">Replicate Hyper-V virtual machines (without VMM) to Azure using Azure Site Recovery with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="81f47-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="81f47-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="81f47-105">Azure 傳統型</span><span class="sxs-lookup"><span data-stu-id="81f47-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="81f47-106">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="81f47-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="81f47-107">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md)，將內部部署 Hyper-V 虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="81f47-107">This article describes how to replicate on-premises Hyper-V virtual machines to Azure, using [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="81f47-108">在此部署中，Hyper-V VM 並非由 System Center Virtual Machine Manager (VMM) 所管理。</span><span class="sxs-lookup"><span data-stu-id="81f47-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>

<span data-ttu-id="81f47-109">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="81f47-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

<span data-ttu-id="81f47-110">如果您想要將電腦移轉至 Azure (不含容錯回復)，請在[這篇文章](site-recovery-migrate-to-azure.md)中深入了解。</span><span class="sxs-lookup"><span data-stu-id="81f47-110">If you want to migrate machines to Azure (without failback), learn more in [this article](site-recovery-migrate-to-azure.md).</span></span>



## <a name="deployment-steps"></a><span data-ttu-id="81f47-111">部署步驟</span><span class="sxs-lookup"><span data-stu-id="81f47-111">Deployment steps</span></span>

<span data-ttu-id="81f47-112">請依照下列文件完成這些部署步驟︰</span><span class="sxs-lookup"><span data-stu-id="81f47-112">Follow the article to complete these deployment steps:</span></span>

1. <span data-ttu-id="81f47-113">[深入了解](site-recovery-components.md#hyper-v-to-azure)此部署的架構。</span><span class="sxs-lookup"><span data-stu-id="81f47-113">[Learn more](site-recovery-components.md#hyper-v-to-azure) about the architecture for this deployment.</span></span> <span data-ttu-id="81f47-114">此外，[深入了解](site-recovery-hyper-v-azure-architecture.md) Site Recovery 中 Hyper-V 複寫的運作方式。</span><span class="sxs-lookup"><span data-stu-id="81f47-114">In addition, [learn about](site-recovery-hyper-v-azure-architecture.md) how Hyper-V replication works in Site Recovery.</span></span>
2. <span data-ttu-id="81f47-115">確認必要條件和限制。</span><span class="sxs-lookup"><span data-stu-id="81f47-115">Verify prerequisites and limitations.</span></span>
3. <span data-ttu-id="81f47-116">設定 Azure 網路和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-116">Set up Azure network and storage accounts.</span></span>
4. <span data-ttu-id="81f47-117">準備 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="81f47-117">Prepare Hyper-V hosts.</span></span>
5. <span data-ttu-id="81f47-118">建立復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="81f47-118">Create a Recovery Services vault.</span></span> <span data-ttu-id="81f47-119">保存庫包含組態設定，並協調複寫。</span><span class="sxs-lookup"><span data-stu-id="81f47-119">The vault contains configuration settings, and orchestrates replication.</span></span>
6. <span data-ttu-id="81f47-120">指定來源設定。</span><span class="sxs-lookup"><span data-stu-id="81f47-120">Specify source settings.</span></span> <span data-ttu-id="81f47-121">建立包含 Hyper-V 主機的 Hyper-V 網站，並在保存庫註冊網站。</span><span class="sxs-lookup"><span data-stu-id="81f47-121">Create a Hyper-V site that contains the Hyper-V hosts, and register the site in the vault.</span></span> <span data-ttu-id="81f47-122">安裝 Azure Site Recovery Provider，然後在 Hyper-V 主機上安裝 Microsoft 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="81f47-122">Install the Azure Site Recovery Provider, and the Microsoft Recovery Services agent, on the Hyper-V hosts.</span></span>
7. <span data-ttu-id="81f47-123">設定目標和複寫設定。</span><span class="sxs-lookup"><span data-stu-id="81f47-123">Set up target and replication settings.</span></span>
8. <span data-ttu-id="81f47-124">啟用 VM 複寫。</span><span class="sxs-lookup"><span data-stu-id="81f47-124">Enable replication for the VMs.</span></span>
9. <span data-ttu-id="81f47-125">執行測試容錯移轉，確定一切都沒問題。</span><span class="sxs-lookup"><span data-stu-id="81f47-125">Run a test failover to make sure everything's working as expected.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="81f47-126">必要條件</span><span class="sxs-lookup"><span data-stu-id="81f47-126">Prerequisites</span></span>


<span data-ttu-id="81f47-127">**需求**</span><span class="sxs-lookup"><span data-stu-id="81f47-127">**Requirement**</span></span> | <span data-ttu-id="81f47-128">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="81f47-128">**Details**</span></span> |
--- | --- |
<span data-ttu-id="81f47-129">**Azure**</span><span class="sxs-lookup"><span data-stu-id="81f47-129">**Azure**</span></span> | <span data-ttu-id="81f47-130">了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="81f47-130">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="81f47-131">**內部部署伺服器**</span><span class="sxs-lookup"><span data-stu-id="81f47-131">**On-premises servers**</span></span> | <span data-ttu-id="81f47-132">[深入了解](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)內部部署 Hyper-V 主機的需求。</span><span class="sxs-lookup"><span data-stu-id="81f47-132">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="81f47-133">**內部部署 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="81f47-133">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="81f47-134">您想要複寫的 VM 應該執行[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，也要符合 [Azure 必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="81f47-134">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="81f47-135">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="81f47-135">**Azure URLs**</span></span> | <span data-ttu-id="81f47-136">Hyper-V 主機需要存取這些 URL：</span><span class="sxs-lookup"><span data-stu-id="81f47-136">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="81f47-137">如果您有以 IP 位址為基礎的防火牆規則，請確定這些規則允許對 Azure 的通訊。</span><span class="sxs-lookup"><span data-stu-id="81f47-137">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="81f47-138">允許 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="81f47-138">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="81f47-139">允許訂用帳戶的 Azure 區域和美國西部使用 IP 位址範圍 (用於存取控制和身分識別管理)。</span><span class="sxs-lookup"><span data-stu-id="81f47-139">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="prepare-for-deployment"></a><span data-ttu-id="81f47-140">準備部署</span><span class="sxs-lookup"><span data-stu-id="81f47-140">Prepare for deployment</span></span>

<span data-ttu-id="81f47-141">若要準備進行部署，您必須︰</span><span class="sxs-lookup"><span data-stu-id="81f47-141">To prepare for deployment you need to:</span></span>

1. <span data-ttu-id="81f47-142">[設定 Azure 網路](#set-up-an-azure-network) ，這是 Azure VM 於容錯移轉後建立時將所在的網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-142">[Set up an Azure network](#set-up-an-azure-network) in which Azure VMs will be located when they're created after failover.</span></span>
2. <span data-ttu-id="81f47-143">[設定 Azure 儲存體帳戶](#set-up-an-azure-storage-account) 。</span><span class="sxs-lookup"><span data-stu-id="81f47-143">[Set up an Azure storage account](#set-up-an-azure-storage-account) for replicated data.</span></span>
3. <span data-ttu-id="81f47-144">[準備 Hyper-V 主機](#prepare-the-hyper-v-hosts) 以確保它們可以存取所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="81f47-144">[Prepare the Hyper-V hosts](#prepare-the-hyper-v-hosts) to ensure they can access the required URLs.</span></span>

### <a name="set-up-an-azure-network"></a><span data-ttu-id="81f47-145">設定 Azure 網路</span><span class="sxs-lookup"><span data-stu-id="81f47-145">Set up an Azure network</span></span>

<span data-ttu-id="81f47-146">設定 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-146">Set up an Azure network.</span></span> <span data-ttu-id="81f47-147">您將需要 Azure 網路，以便在容錯移轉後建立的 Azure VM 連接網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-147">You’ll need this so that the Azure VMs created after failover are connected to a network.</span></span>

* <span data-ttu-id="81f47-148">此網路應位於與復原服務保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="81f47-148">The network should be in the same region as the Recovery Services vault.</span></span>
* <span data-ttu-id="81f47-149">視您想要針對已容錯移轉的 Azure VM 使用的資源模型而定，您會以 [Resource Manager 模式](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)，或[傳統模式](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)設定 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-149">Depending on the resource model you want to use for failed over Azure VMs, you set up the Azure network in [Resource Manager mode](../virtual-network/virtual-networks-create-vnet-arm-pportal.md), or [classic mode](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>
* <span data-ttu-id="81f47-150">建議您在開始之前先設定網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-150">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="81f47-151">若非如此，則必須在 Site Recovery 部署期間這麼做。</span><span class="sxs-lookup"><span data-stu-id="81f47-151">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="81f47-152">Site Recovery 所使用的儲存體帳戶不能在相同訂用帳戶內或跨越不同的訂用帳戶[移動](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="81f47-152">Storage accounts used by Site Recovery can't be [moved](../azure-resource-manager/resource-group-move-resources.md) within the same, or across different, subscriptions.</span></span>


### <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="81f47-153">設定 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="81f47-153">Set up an Azure storage account</span></span>

- <span data-ttu-id="81f47-154">您需要標準/進階 Azure 儲存體帳戶才可將複寫到 Azure 的資料進行保存。[進階儲存體](../storage/storage-premium-storage.md)通常是用於需要持續高 IO 效能和低延遲性以裝載 IO 密集型工作負載的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-154">You need a standard/premium Azure storage account to hold data replicated to Azure.[Premium storage](../storage/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="81f47-155">如果您想要使用進階帳戶來儲存複寫的資料，就也需要標準儲存體帳戶來儲存複寫記錄檔，這些記錄檔會擷取內部部署資料的進行中變更。</span><span class="sxs-lookup"><span data-stu-id="81f47-155">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="81f47-156">視您想要針對已容錯移轉的 Azure VM 使用的資源模型而定，您會以 [Resource Manager 模式](../storage/storage-create-storage-account.md)，或[傳統模式](../storage/storage-create-storage-account-classic-portal.md)設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-156">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/storage-create-storage-account.md), or [classic mode](../storage/storage-create-storage-account-classic-portal.md).</span></span>
- <span data-ttu-id="81f47-157">建議您在開始之前先設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-157">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="81f47-158">若非如此，則必須在 Site Recovery 部署期間這麼做。</span><span class="sxs-lookup"><span data-stu-id="81f47-158">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="81f47-159">帳戶必須位於與復原服務保存庫相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="81f47-159">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="81f47-160">您無法跨相同訂用帳戶內的資源群組，或跨越不同訂用帳戶移動 Site Recovery 所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-160">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


### <a name="prepare-the-hyper-v-hosts"></a><span data-ttu-id="81f47-161">準備 Hyper-V 主機</span><span class="sxs-lookup"><span data-stu-id="81f47-161">Prepare the Hyper-V hosts</span></span>

* <span data-ttu-id="81f47-162">確定 Hyper-V 主機符合[必要條件](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager)。</span><span class="sxs-lookup"><span data-stu-id="81f47-162">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-virtual-machines-to-azure-no-virtual-machine-manager).</span></span>
- <span data-ttu-id="81f47-163">請確定主機可以存取必要的 URL。</span><span class="sxs-lookup"><span data-stu-id="81f47-163">Make sure that the hosts can access the required URLs.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="81f47-164">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="81f47-164">Create a Recovery Services vault</span></span>
1. <span data-ttu-id="81f47-165">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="81f47-165">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="81f47-166">按一下 [新增] > [監視 + 管理] > [備份和 Site Recovery (OMS)]。</span><span class="sxs-lookup"><span data-stu-id="81f47-166">Click **New** > **Monitoring + Management** > **Backup and Site Recovery (OMS)**.</span></span>  

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure/new-vault.png)

3. <span data-ttu-id="81f47-168">在 [名稱] 中，指定保存庫的易記識別名稱。</span><span class="sxs-lookup"><span data-stu-id="81f47-168">In **Name**, specify a friendly name to identify the vault.</span></span> <span data-ttu-id="81f47-169">如果您有多個訂用帳戶，請選取其中一個。</span><span class="sxs-lookup"><span data-stu-id="81f47-169">If you have more than one subscription, select one of them.</span></span>

4. <span data-ttu-id="81f47-170">[建立新的資源群組](../azure-resource-manager/resource-group-template-deploy-portal.md) 或選取現有的資源群組，並指定 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="81f47-170">[Create a new resource group](../azure-resource-manager/resource-group-template-deploy-portal.md) or select an existing one, and specify an Azure region.</span></span> <span data-ttu-id="81f47-171">機器將會複寫到此區域。</span><span class="sxs-lookup"><span data-stu-id="81f47-171">Machines will be replicated to this region.</span></span> <span data-ttu-id="81f47-172">若要查看支援的區域，請參閱 [Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)中的＜各地區上市情況＞。</span><span class="sxs-lookup"><span data-stu-id="81f47-172">To check supported regions, see Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>

5. <span data-ttu-id="81f47-173">如果您想要從「儀表板」快速存取保存庫，請按一下 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="81f47-173">If you want to quickly access the vault from the Dashboard, click **Pin to dashboard**, and then click **Create**.</span></span>

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure/new-vault-settings.png)

<span data-ttu-id="81f47-175">新的保存庫會出現在 [儀表板] > [所有資源] 清單中，以及主要 [復原服務保存庫] 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="81f47-175">The new vault appears in the **Dashboard** > **All resources** list, and on the main **Recovery Services vaults** blade.</span></span>



## <a name="select-the-protection-goal"></a><span data-ttu-id="81f47-176">選取保護目標</span><span class="sxs-lookup"><span data-stu-id="81f47-176">Select the protection goal</span></span>

<span data-ttu-id="81f47-177">選取您要複寫的項目以及您要複寫到的位置。</span><span class="sxs-lookup"><span data-stu-id="81f47-177">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="81f47-178">在 [復原服務保存庫] 中選取保存庫。</span><span class="sxs-lookup"><span data-stu-id="81f47-178">In the **Recovery Services vaults**, select the vault.</span></span>
2. <span data-ttu-id="81f47-179">在 [快速入門] 中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="81f47-179">In **Getting Started**, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-hyper-v-site-to-azure/choose-goals.png)
3. <span data-ttu-id="81f47-181">在 [保護目標] 中，選取 [至 Azure]，然後選取 [是，利用 Hyper-V]。</span><span class="sxs-lookup"><span data-stu-id="81f47-181">In **Protection goal**, select **To Azure**, and select **Yes, with Hyper-V**.</span></span> <span data-ttu-id="81f47-182">選取 [否]  以確認您未使用 VMM。</span><span class="sxs-lookup"><span data-stu-id="81f47-182">Select **No** to confirm you're not using VMM.</span></span> <span data-ttu-id="81f47-183">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-183">Then click **OK**.</span></span>

    ![選擇目標](./media/site-recovery-hyper-v-site-to-azure/choose-goals2.png)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="81f47-185">設定來源環境</span><span class="sxs-lookup"><span data-stu-id="81f47-185">Set up the source environment</span></span>

<span data-ttu-id="81f47-186">設定 Hyper-V 網站、在 Hyper-V 主機上安裝 Azure Site Recovery Provider 和 Azure 復原服務代理程式，並在保存庫註冊網站。</span><span class="sxs-lookup"><span data-stu-id="81f47-186">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="81f47-187">在 [準備基礎結構] 中，按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="81f47-187">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="81f47-188">若要加入新的 Hyper-V 網站作為 Hyper-V 主機或叢集的容器，請按一下 [+Hyper-V 網站] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-188">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source1.png)
2. <span data-ttu-id="81f47-190">在 [建立 Hyper-V 網站] 中，指定網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="81f47-190">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="81f47-191">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-191">Then click **OK**.</span></span> <span data-ttu-id="81f47-192">現在，選取您建立的網站，然後按一下 [+Hyper-V Server]，將伺服器新增至網站。</span><span class="sxs-lookup"><span data-stu-id="81f47-192">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source2.png)

3. <span data-ttu-id="81f47-194">在 [新增伺服器] > [伺服器類型] 中，檢查是否已顯示 [Hyper-V 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="81f47-194">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="81f47-195">確定您想要新增的 Hyper-V 伺服器符合[必要條件](#on-premises-prerequisites)，而且能夠存取指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="81f47-195">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="81f47-196">下載 Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="81f47-196">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="81f47-197">您將執行這個檔案，在每個 Hyper-V 主機上安裝 Provider 和復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="81f47-197">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![設定來源](./media/site-recovery-hyper-v-site-to-azure/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="81f47-199">安裝 Provider 和代理程式</span><span class="sxs-lookup"><span data-stu-id="81f47-199">Install the Provider and agent</span></span>

1. <span data-ttu-id="81f47-200">在您已加入 Hyper-V 網站中的每個主機上執行 Provider 安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="81f47-200">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="81f47-201">如果您安裝在 Hyper-V 叢集上，請在每個叢集節點上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="81f47-201">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="81f47-202">安裝和註冊每個 Hyper-V 叢集節點，可確保 VM 即使跨節點移轉，都還是會受保護。</span><span class="sxs-lookup"><span data-stu-id="81f47-202">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="81f47-203">在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。</span><span class="sxs-lookup"><span data-stu-id="81f47-203">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="81f47-204">在 [安裝] 中接受或修改預設 Provider 安裝位置，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="81f47-204">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="81f47-205">在 [保存庫設定] 中，按一下 [瀏覽] 來選取您已下載的保存庫金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="81f47-205">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="81f47-206">指定 Azure Site Recovery 訂用帳戶、保存庫名稱，以及 Hyper-V 伺服器所屬的 Hyper-V 網站。</span><span class="sxs-lookup"><span data-stu-id="81f47-206">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure/provider3.png)

5. <span data-ttu-id="81f47-208">在 [Proxy 設定] 中，指定在 Hyper-V 主機上執行的 Provider 要如何透過網際網路連線到 Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="81f47-208">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="81f47-209">如果您想要讓 Provider 直接連線，請選取 [不使用 Proxy 直接連接至 Azure Site Recovery] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-209">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="81f47-210">如果您現有的 Proxy 需要驗證，或您想要使用自訂 Proxy 進行 Provider 連線，請選取 [使用 Proxy 伺服器連線至 Azure Site Recovery]。</span><span class="sxs-lookup"><span data-stu-id="81f47-210">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="81f47-211">如果您使用 Proxy：</span><span class="sxs-lookup"><span data-stu-id="81f47-211">If you use a proxy:</span></span>
        - <span data-ttu-id="81f47-212">請指定位址、連接埠以及認證</span><span class="sxs-lookup"><span data-stu-id="81f47-212">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="81f47-213">請確定已允許[必要條件](#prerequisites)中所述的 URL 通過 Proxy。</span><span class="sxs-lookup"><span data-stu-id="81f47-213">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![網際網路](./media/site-recovery-hyper-v-site-to-azure/provider7.PNG)

6. <span data-ttu-id="81f47-215">安裝完成之後，按一下 [註冊] 以在保存庫中註冊該伺服器。</span><span class="sxs-lookup"><span data-stu-id="81f47-215">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![安裝位置](./media/site-recovery-hyper-v-site-to-azure/provider2.png)

7. <span data-ttu-id="81f47-217">註冊完成之後，Azure Site Recovery 便會抓取來自 Hyper-V 伺服器的中繼資料，而該伺服器會顯示在 [站台復原基礎結構] > [Hyper-V 主機] 中。</span><span class="sxs-lookup"><span data-stu-id="81f47-217">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="81f47-218">設定目標環境</span><span class="sxs-lookup"><span data-stu-id="81f47-218">Set up the target environment</span></span>

<span data-ttu-id="81f47-219">指定要用於複寫的 Azure 儲存體帳戶，以及 Azure VM 在容錯移轉後會連線的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-219">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="81f47-220">按一下 [準備基礎結構] > [目標]。</span><span class="sxs-lookup"><span data-stu-id="81f47-220">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="81f47-221">選取您想要在容錯移轉後，在其中建立 Azure VM 的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="81f47-221">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="81f47-222">選擇您想要在 Azure (傳統或資源管理) 中，針對 VM 使用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="81f47-222">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="81f47-223">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-223">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="81f47-224">如果您沒有儲存體帳戶，請按一下 [+儲存體]，建立以 Resource Manager 為基礎的內嵌帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-224">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> <span data-ttu-id="81f47-225">深入了解[儲存體需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="81f47-225">Read about [storage requirements](site-recovery-prereq.md#azure-requirements).</span></span>
    - <span data-ttu-id="81f47-226">如果您沒有 Azure 網路，請按一下 [+網路]，建立以 Resource Manager 為基礎的內嵌網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-226">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>

    ![儲存體](./media/site-recovery-vmware-to-azure/enable-rep3.png)




## <a name="configure-replication-settings"></a><span data-ttu-id="81f47-228">設定複寫設定</span><span class="sxs-lookup"><span data-stu-id="81f47-228">Configure replication settings</span></span>

1. <span data-ttu-id="81f47-229">若要建立新的複寫原則，請按一下 [準備基礎結構] > [複寫設定] > [+建立及關聯]。</span><span class="sxs-lookup"><span data-stu-id="81f47-229">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![網路](./media/site-recovery-hyper-v-site-to-azure/gs-replication.png)
2. <span data-ttu-id="81f47-231">在 [建立及關聯原則] 中指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="81f47-231">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="81f47-232">在 [複製頻率] 中，指定您要在初始複寫後複寫差異資料的頻率 (每隔 30 秒、5 或 15 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="81f47-232">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="81f47-233">複寫到進階儲存體時，不支援 30 秒的頻率。</span><span class="sxs-lookup"><span data-stu-id="81f47-233">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="81f47-234">限制取決於進階儲存體所支援之每 blob (100) 的快照集數目。</span><span class="sxs-lookup"><span data-stu-id="81f47-234">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="81f47-235">[深入了解](../storage/storage-premium-storage.md#snapshots-and-copy-blob)。</span><span class="sxs-lookup"><span data-stu-id="81f47-235">[Learn more](../storage/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="81f47-236">在 [復原點保留] 中，指定每個復原點的保留週期長度 (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="81f47-236">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="81f47-237">VM 可以復原到週期內的任意點。</span><span class="sxs-lookup"><span data-stu-id="81f47-237">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="81f47-238">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。</span><span class="sxs-lookup"><span data-stu-id="81f47-238">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>

    - <span data-ttu-id="81f47-239">Hyper-V 使用兩種類型的快照，一個是標準快照，提供整個虛擬機器的增量快照，另一個是應用程式一致快照，會建立虛擬機器內應用程式資料的時間點快照。</span><span class="sxs-lookup"><span data-stu-id="81f47-239">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="81f47-240">應用程式一致快照會使用「磁碟區陰影複製服務」(VSS) 來確保建立快照時，應用程式是處於一致狀態。</span><span class="sxs-lookup"><span data-stu-id="81f47-240">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="81f47-241">如果您啟用應用程式一致快照，它會影響在來源虛擬機器上執行的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="81f47-241">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="81f47-242">確認您設定的值低於您設定的其他復原點數目。</span><span class="sxs-lookup"><span data-stu-id="81f47-242">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

6. <span data-ttu-id="81f47-243">在 [初始複寫開始時間]  中，指定開始初始複寫的時間。</span><span class="sxs-lookup"><span data-stu-id="81f47-243">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="81f47-244">複寫會透過您的網際網路頻寬發生，所以您可能想將它排程在忙碌時間之外。</span><span class="sxs-lookup"><span data-stu-id="81f47-244">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="81f47-245">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-245">Then click **OK**.</span></span>

    ![複寫原則](./media/site-recovery-hyper-v-site-to-azure/gs-replication2.png)

<span data-ttu-id="81f47-247">當您建立新的原則時，該原則會自動與 Hyper-V 網站產生關聯。</span><span class="sxs-lookup"><span data-stu-id="81f47-247">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="81f47-248">您可以在 [複寫] > 原則名稱 > [關聯 Hyper-V 網站] 中，將 Hyper-V 網站 (及其中的 VM) 與多個複寫原則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="81f47-248">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>

## <a name="capacity-planning"></a><span data-ttu-id="81f47-249">容量規劃</span><span class="sxs-lookup"><span data-stu-id="81f47-249">Capacity planning</span></span>

<span data-ttu-id="81f47-250">您現已設定您的基本基礎結構，您可以思考容量規劃並找出您是否需要額外的資源。</span><span class="sxs-lookup"><span data-stu-id="81f47-250">Now that you have your basic infrastructure set up, you can think about capacity planning, and figure out whether you need additional resources.</span></span>

<span data-ttu-id="81f47-251">Site Recovery 會提供 Capacity Planner 以協助您為計算、網路及儲存體配置適當的資源。</span><span class="sxs-lookup"><span data-stu-id="81f47-251">Site Recovery provides a capacity planner to help you allocate the right resources for compute, networking, and storage.</span></span> <span data-ttu-id="81f47-252">您可以在快速模式中執行規劃工具，以便根據 VM、磁碟和儲存體的平均數量進行估計，或在詳細模式中執行規劃工具，以包含工作負載層級的自訂數字。</span><span class="sxs-lookup"><span data-stu-id="81f47-252">You can run the planner in quick mode for estimations based on an average number of VMs, disks, and storage, or in detailed mode with customized numbers at the workload level.</span></span> <span data-ttu-id="81f47-253">開始之前，您必須︰</span><span class="sxs-lookup"><span data-stu-id="81f47-253">Before you start you need to:</span></span>

* <span data-ttu-id="81f47-254">收集有關複寫環境的資訊，包括 VM、每個 VM 的磁碟和每個磁碟的儲存體。</span><span class="sxs-lookup"><span data-stu-id="81f47-254">Gather information about your replication environment, including VMs, disks per VMs, and storage per disk.</span></span>
* <span data-ttu-id="81f47-255">估計複寫資料的每日變更 (流失) 率。</span><span class="sxs-lookup"><span data-stu-id="81f47-255">Estimate the daily change (churn) rate for your replicated data.</span></span> <span data-ttu-id="81f47-256">您可以使用 [Capacity Planner for Hyper-V Replica (適用於 Hyper-V 複本的 Capacity Planner)](https://www.microsoft.com/download/details.aspx?id=39057) 來協助您執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="81f47-256">You can use the [Capacity Planner for Hyper-V Replica](https://www.microsoft.com/download/details.aspx?id=39057) to help you do this.</span></span>

1. <span data-ttu-id="81f47-257">按一下 [下載] 來下載此工具並加以執行。</span><span class="sxs-lookup"><span data-stu-id="81f47-257">Click **Download** to download the tool, and then run it.</span></span> <span data-ttu-id="81f47-258">[文章](site-recovery-capacity-planner.md) 。</span><span class="sxs-lookup"><span data-stu-id="81f47-258">[Read the article](site-recovery-capacity-planner.md) that accompanies the tool.</span></span>
2. <span data-ttu-id="81f47-259">當您完成時，請在 [是否已執行 Capacity Planner?]中選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="81f47-259">When you’re done, select **Yes** in **Have you run the Capacity Planner**?</span></span>

   ![容量規劃](./media/site-recovery-hyper-v-site-to-azure/gs-capacity-planning.png)

<span data-ttu-id="81f47-261">深入了解[控制網路頻寬](#network-bandwidth-considerations)</span><span class="sxs-lookup"><span data-stu-id="81f47-261">Learn more about [controlling network bandwidth](#network-bandwidth-considerations)</span></span>



## <a name="enable-replication"></a><span data-ttu-id="81f47-262">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="81f47-262">Enable replication</span></span>

<span data-ttu-id="81f47-263">在開始之前，請確定您的 Azure 使用者帳戶具有必要的[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，才能將新的虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="81f47-263">Before you start, ensure that your Azure user account has the required  [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

<span data-ttu-id="81f47-264">啟用 VM 複寫，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="81f47-264">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="81f47-265">按一下 [複寫應用程式] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="81f47-265">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="81f47-266">第一次設定複寫之後，您可以按一下 [+複寫]，以對其他電腦啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="81f47-266">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication.png)
2. <span data-ttu-id="81f47-268">在 [來源] 中，選取 Hyper-V 網站。</span><span class="sxs-lookup"><span data-stu-id="81f47-268">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="81f47-269">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-269">Then click **OK**.</span></span>
3. <span data-ttu-id="81f47-270">在 [目標] 中，選取保存庫訂用帳戶，以及您想要在容錯移轉後於 Azure 中使用的容錯移轉模型 (傳統或資源管理)。</span><span class="sxs-lookup"><span data-stu-id="81f47-270">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="81f47-271">選取您要使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-271">Select the storage account you want to use.</span></span> <span data-ttu-id="81f47-272">如果您沒有想要使用的帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="81f47-272">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="81f47-273">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-273">Then click **OK**.</span></span>
5. <span data-ttu-id="81f47-274">選取 Azure VM 在容錯移轉後啟動時所要連線的 Azure 網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-274">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="81f47-275">若要將網路設定套用至您啟用要進行複寫的所有電腦，請選取 [立即設定選取的機器]。</span><span class="sxs-lookup"><span data-stu-id="81f47-275">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="81f47-276">選取 [稍後設定] 以選取每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-276">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="81f47-277">如果您沒有想要使用的網路，您可以[建立一個](#set-up-an-azure-network)。</span><span class="sxs-lookup"><span data-stu-id="81f47-277">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="81f47-278">選取適用的子網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-278">Select a subnet if applicable.</span></span> <span data-ttu-id="81f47-279">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-279">Then click **OK**.</span></span>

   ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication11.png)

6. <span data-ttu-id="81f47-281">在 [虛擬機器] > [選取虛擬機器] 中，按一下並選取您要複寫的每部機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-281">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="81f47-282">您只能選取可以啟用複寫的機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-282">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="81f47-283">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-283">Then click **OK**.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="81f47-285">在 [名稱]  > 中，為選取的 VM 選取作業系統，以及 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-285">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="81f47-286">確認 Azure VM 名稱 (目標名稱) 符合 [Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="81f47-286">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="81f47-287">依預設會選取 VM 的所有磁碟以進行複寫，但您可以將磁碟清除以排除它們。</span><span class="sxs-lookup"><span data-stu-id="81f47-287">By default all the disks of the VM are selected for replication, but you can clear disks to exclude them.</span></span>
    - <span data-ttu-id="81f47-288">您可能想要排除磁碟來減少複寫頻寬。</span><span class="sxs-lookup"><span data-stu-id="81f47-288">You might want to exclude disks to reduce replication bandwidth.</span></span> <span data-ttu-id="81f47-289">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次電腦或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 Microsoft SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="81f47-289">For example, you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or apps restarts (such as pagefile.sys or Microsoft SQL Server tempdb).</span></span> <span data-ttu-id="81f47-290">您可以取消選取磁碟以將磁碟排除複寫。</span><span class="sxs-lookup"><span data-stu-id="81f47-290">You can exclude the disk from replication by unselecting the disk.</span></span>
    - <span data-ttu-id="81f47-291">只有基本磁碟可以排除。</span><span class="sxs-lookup"><span data-stu-id="81f47-291">Only basic disks can be exclude.</span></span> <span data-ttu-id="81f47-292">您無法排除作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-292">You can't exclude OS disks.</span></span>
    - <span data-ttu-id="81f47-293">我們建議不要排除動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-293">We recommend that you don't exclude dynamic disks.</span></span> <span data-ttu-id="81f47-294">Site Recovery 無法識別客體 VM 內的虛擬硬碟為基本還是動態磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-294">Site Recovery can't identify whether a virtual hard disk inside a guest VM is basic or dynamic.</span></span> <span data-ttu-id="81f47-295">如果未排除所有的相依動態磁碟區磁碟，受保護的動態磁碟會在 VM 容錯移轉時顯示為失敗的磁碟，且該磁碟上的資料無法存取。</span><span class="sxs-lookup"><span data-stu-id="81f47-295">If all dependent dynamic volume disks aren't excluded, the protected dynamic disk will show as a failed disk when the VM fails over, and the data on that disk won't be accessible.</span></span>
        - <span data-ttu-id="81f47-296">啟用複寫後，您無法加入或移除複寫的磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-296">After replication is enabled, you can't add or remove disks for replication.</span></span> <span data-ttu-id="81f47-297">如果您想要新增或排除磁碟，必須停用 VM 的保護，然後重新啟用它。</span><span class="sxs-lookup"><span data-stu-id="81f47-297">If you want to add or exclude a disk, you need to disable protection for the VM, and then re-enable it.</span></span>
        - <span data-ttu-id="81f47-298">您以手動方式在 Azure 中建立的磁碟將不會容錯回復。</span><span class="sxs-lookup"><span data-stu-id="81f47-298">Disks you create manually in Azure aren't failed back.</span></span> <span data-ttu-id="81f47-299">例如，如果您容錯移轉三個磁碟，並直接在 Azure VM 中建立兩個磁碟，則只有那三個容錯移轉的磁碟會從 Azure 容錯回復至 Hyper-V。</span><span class="sxs-lookup"><span data-stu-id="81f47-299">For example, if you fail over three disks, and create two directly in Azure VM, only the three disks which were failed over will be failed back from Azure to Hyper-V.</span></span> <span data-ttu-id="81f47-300">您無法在容錯回復，或是從 Hyper-V 至 Azure 的反向複寫中包含手動建立的磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-300">You can't include disks created manually in failback, or in reverse replication from Hyper-V to Azure.</span></span>
        - <span data-ttu-id="81f47-301">如果您排除應用程式運作所需的磁碟，在容錯移轉至 Azure 之後，您必須在 Azure 中手動建立它，複寫的應用程式才能執行。</span><span class="sxs-lookup"><span data-stu-id="81f47-301">If you exclude a disk that's needed for an application to operate, after failover to Azure you need to create it manually in Azure, so that the replicated application can run.</span></span> <span data-ttu-id="81f47-302">或者，您可以將 Azure 自動化整合至復原計畫，在電腦容錯移轉期間建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-302">Alternatively, you could integrate Azure automation into a recovery plan, to create the disk during failover of the machine.</span></span>

10. <span data-ttu-id="81f47-303">按一下 [確定] 儲存變更。</span><span class="sxs-lookup"><span data-stu-id="81f47-303">Click **OK** to save changes.</span></span> <span data-ttu-id="81f47-304">您可以稍後再設定其他屬性。</span><span class="sxs-lookup"><span data-stu-id="81f47-304">You can set additional properties later.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="81f47-306">在 [複寫設定]  >  [進行複寫設定] 中，選取您要套用於受保護 VM 的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="81f47-306">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="81f47-307">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-307">Then click **OK**.</span></span> <span data-ttu-id="81f47-308">您可以在 [複寫原則] > 原則名稱 > [編輯設定] 中，修改複寫原則。</span><span class="sxs-lookup"><span data-stu-id="81f47-308">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="81f47-309">您套用的變更將用於已在複寫的機器和新的機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-309">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/enable-replication7.png)

<span data-ttu-id="81f47-311">您可以在 [作業] >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="81f47-311">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="81f47-312">執行 [完成保護]  作業之後，機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="81f47-312">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

### <a name="view-and-manage-vm-properties"></a><span data-ttu-id="81f47-313">檢視及管理 VM 屬性</span><span class="sxs-lookup"><span data-stu-id="81f47-313">View and manage VM properties</span></span>

<span data-ttu-id="81f47-314">建議您確認來源機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="81f47-314">We recommend that you verify the properties of the source machine.</span></span>

1. <span data-ttu-id="81f47-315">在 [受保護的項目]中，按一下 [複寫的項目]，然後選取機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-315">In **Protected Items**, click **Replicated Items**, and select the machine.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover1.png)
2. <span data-ttu-id="81f47-317">在 [屬性] 中，您可以檢視 VM 的複寫和容錯移轉資訊。</span><span class="sxs-lookup"><span data-stu-id="81f47-317">In **Properties**, you can view replication and failover information for the VM.</span></span>

    ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover2.png)
3. <span data-ttu-id="81f47-319">在 [計算和網路] > [計算屬性] 中，您可以指定 Azure VM 名稱和目標大小。</span><span class="sxs-lookup"><span data-stu-id="81f47-319">In **Compute and Network** > **Compute properties**, you can specify the Azure VM name and target size.</span></span> <span data-ttu-id="81f47-320">視需要修改名稱以符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="81f47-320">Modify the name to comply with Azure requirements if you need to.</span></span> <span data-ttu-id="81f47-321">您也可以檢視和修改目標網路、子網路的相關資訊，以及將指派給 Azure VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="81f47-321">You can also view and modify information about the target network, subnet, and IP address that will be assigned to the Azure VM.</span></span> <span data-ttu-id="81f47-322">請注意：</span><span class="sxs-lookup"><span data-stu-id="81f47-322">Note the following:</span></span>

   * <span data-ttu-id="81f47-323">您可以設定目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="81f47-323">You can set the target IP address.</span></span> <span data-ttu-id="81f47-324">如果您未提供地址，則容錯移轉的機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="81f47-324">If you don't provide an address, the failed over machine will use DHCP.</span></span> <span data-ttu-id="81f47-325">如果您設定無法用於容錯移轉的位址，則容錯移轉會失敗。</span><span class="sxs-lookup"><span data-stu-id="81f47-325">If you set an address that isn't available at failover, the failover will fail.</span></span> <span data-ttu-id="81f47-326">如果位址可用於測試容錯移轉網路，則相同的目標 IP 位址可用於測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="81f47-326">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>
   * <span data-ttu-id="81f47-327">網路介面卡的數目會視您指定給目標虛擬機器的大小而有所不同，如下所示：</span><span class="sxs-lookup"><span data-stu-id="81f47-327">The number of network adapters is dictated by the size you specify for the target virtual machine, as follows:</span></span>

     * <span data-ttu-id="81f47-328">如果來源電腦上的網路介面卡數目小於或等於針對目標機器大小所允許的介面卡數目，則目標將具備與來源相同的介面卡數目。</span><span class="sxs-lookup"><span data-stu-id="81f47-328">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
     * <span data-ttu-id="81f47-329">如果來源虛擬機器的介面卡數目超過針對目標大小所允許的數目，則將使用目標大小的最大值。</span><span class="sxs-lookup"><span data-stu-id="81f47-329">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
     * <span data-ttu-id="81f47-330">例如，如果來源機器具有兩張網路介面卡，而目標機器大小支援四張，則目標機器將會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="81f47-330">For example if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="81f47-331">如果來源機器具有兩張介面卡，但支援的目標大小僅支援一張，則目標機器將只會有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="81f47-331">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>     
     * <span data-ttu-id="81f47-332">如果 VM 有多張網路介面卡，則全部會連接至相同的網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-332">If the VM has multiple network adapters they will all connect to the same network.</span></span>
     * <span data-ttu-id="81f47-333">如果虛擬機器具有多個網路介面卡，則清單中顯示的第一個會變成 Azure 虛擬機器中的*預設*網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="81f47-333">If the virtual machine has multiple network adapters then the first one shown in the list becomes the *Default* network adapter in the Azure virtual machine.</span></span>

     ![啟用複寫](./media/site-recovery-hyper-v-site-to-azure/test-failover4.png)

4. <span data-ttu-id="81f47-335">在 [磁碟] 中，您可以看見 VM 上將要複寫的作業系統和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-335">In **Disks**, you can see the operating system and data disks on the VM that will be replicated.</span></span>

#### <a name="managed-disks"></a><span data-ttu-id="81f47-336">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="81f47-336">Managed disks</span></span>

<span data-ttu-id="81f47-337">在 [計算和網路] > [計算屬性] 中，如果您想要將受控磁碟連結至您要移轉至 Azure 的電腦上，可以將 VM 的 [使用受控磁碟] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="81f47-337">In **Compute and Network** > **Compute properties**, you can set "Use managed disks" setting to "Yes" for the VM if you want to attach managed disks to your machine on migration to Azure.</span></span> <span data-ttu-id="81f47-338">受控磁碟會管理與 VM 磁碟相關的儲存體帳戶，從而簡化 Azure IaaS VM 的磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="81f47-338">Managed disks simplifies disk management for Azure IaaS VMs by managing the storage accounts associated with the VM disks.</span></span> <span data-ttu-id="81f47-339">[深入了解受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview)。</span><span class="sxs-lookup"><span data-stu-id="81f47-339">[Learn More about managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).</span></span>

   - <span data-ttu-id="81f47-340">只有容錯移轉至 Azure 的受控磁碟會加以建立並連結至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-340">Managed disks are created and attached to the virtual machine only on a failover to Azure.</span></span> <span data-ttu-id="81f47-341">啟用保護時，內部部署電腦的資料會繼續複寫至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="81f47-341">On enabling protection, data from on-premises machines will continue to replicate to storage accounts.</span></span>
   <span data-ttu-id="81f47-342">只有使用 Resource Manager 部署模型部署的虛擬機器才能建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="81f47-342">Managed disks can be created only for virtual machines deployed using the Resource manager deployment model.</span></span>

  > [!NOTE]
  > <span data-ttu-id="81f47-343">具有受控磁碟的電腦目前不支援從 Azure 容錯回復到內部部署 Hyper-V 環境。</span><span class="sxs-lookup"><span data-stu-id="81f47-343">Failback from Azure to on-premises Hyper-V environment is not currently supported for machines with managed disks.</span></span> <span data-ttu-id="81f47-344">只在您想要將這台電腦移轉至 Azure 時，才將 [使用受控磁碟] 設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="81f47-344">Set "Use managed disks" to "Yes" only if you intend to migrate this machine to Azure.</span></span>

   - <span data-ttu-id="81f47-345">當您將 [使用受控磁碟] 設定為 [是] 時，只能選取資源群組中 [使用受控磁碟] 設定為 [是] 的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="81f47-345">When you set "Use managed disks" to "Yes", only availability sets in the resource group with "Use managed disks" set to "Yes" would be available for selection.</span></span> <span data-ttu-id="81f47-346">這是因為只有當 [使用受控磁碟] 屬性設定為 [是] 時，具有受控磁碟的虛擬機器才能成為可用性設定組的一部分。</span><span class="sxs-lookup"><span data-stu-id="81f47-346">This is because virtual machines with managed disks can only be part of availability sets with "Use managed disks" property set to "Yes".</span></span> <span data-ttu-id="81f47-347">請確定您建立的可用性設定組，是以容錯移轉時使用受控磁碟的意圖作為基礎設定 [使用受控磁碟] 屬性。</span><span class="sxs-lookup"><span data-stu-id="81f47-347">Make sure that you create availability sets with "Use managed disks" property set based on your intent to use managed disks on failover.</span></span> <span data-ttu-id="81f47-348">同樣地，當您將 [使用受控磁碟] 設定為 [否] 時，只能選取資源群組中 [使用受控磁碟] 屬性設定為 [否] 的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="81f47-348">Likewise, when you set "Use managed disks" to "No", only availability sets in the resource group with "Use managed disks" property set to "No" would be available for selection.</span></span> <span data-ttu-id="81f47-349">[深入了解受控磁碟和可用性設定組](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set)。</span><span class="sxs-lookup"><span data-stu-id="81f47-349">[Learn more about managed disks and availability sets](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).</span></span>

  > [!NOTE]
  > <span data-ttu-id="81f47-350">如果用於複寫的儲存體帳戶在任何時間點透過儲存體服務加密進行加密，在容錯移轉期間建立受控磁碟就會失敗。</span><span class="sxs-lookup"><span data-stu-id="81f47-350">If the storage account used for replication was encrypted with Storage Service Encryption at any point in time, creation of managed disks during failover will fail.</span></span> <span data-ttu-id="81f47-351">您可以將 [使用受控磁碟] 設定為 [否] 並重試容錯移轉，或將虛擬機器保護停用，並在未於任何時間點啟用儲存體服務加密的儲存體帳戶中加以保護。</span><span class="sxs-lookup"><span data-stu-id="81f47-351">You can either set "Use managed disks" to "No" and retry failover or disable protection for the virtual machine and protect it to a storage account which did not have Storage service encryption enabled at any point in time.</span></span>
  > <span data-ttu-id="81f47-352">[深入了解儲存體服務加密及受控磁碟](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption)。</span><span class="sxs-lookup"><span data-stu-id="81f47-352">[Learn more about Storage service encryption and managed disks](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).</span></span>


## <a name="test-the-deployment"></a><span data-ttu-id="81f47-353">測試部署</span><span class="sxs-lookup"><span data-stu-id="81f47-353">Test the deployment</span></span>

<span data-ttu-id="81f47-354">若要測試部署，您可以針對單一虛擬機器執行測試容錯移轉，或執行包含一或多部虛擬機器的復原方案。</span><span class="sxs-lookup"><span data-stu-id="81f47-354">To test the deployment you can run a test failover for a single virtual machine or a recovery plan that contains one or more virtual machines.</span></span>

### <a name="before-you-start"></a><span data-ttu-id="81f47-355">開始之前</span><span class="sxs-lookup"><span data-stu-id="81f47-355">Before you start</span></span>

 - <span data-ttu-id="81f47-356">如果您想要在容錯移轉後使用 RDP 連線到 Azure VM，請了解[準備連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)。</span><span class="sxs-lookup"><span data-stu-id="81f47-356">If you want to connect to Azure VMs using RDP after failover, learn about [preparing to connect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).</span></span>
 - <span data-ttu-id="81f47-357">若要完整測試，您需要在測試環境中將 Active Directory 和 DNS 進行複製。</span><span class="sxs-lookup"><span data-stu-id="81f47-357">To fully test you need to copy of Active Directory and DNS in your test environment.</span></span> <span data-ttu-id="81f47-358">[深入了解](site-recovery-active-directory.md#test-failover-considerations)。</span><span class="sxs-lookup"><span data-stu-id="81f47-358">[Learn more](site-recovery-active-directory.md#test-failover-considerations).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="81f47-359">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="81f47-359">Run a test failover</span></span>

1. <span data-ttu-id="81f47-360">若要容錯移轉單一機器，請在 [複寫的項目] 中，按一下 VM > [+測試容錯移轉] 圖示。</span><span class="sxs-lookup"><span data-stu-id="81f47-360">To fail over a single machine, in **Replicated Items**, click the VM > **+Test Failover** icon.</span></span>
2. <span data-ttu-id="81f47-361">若要容錯移轉復原方案，請在 [復原方案] 中，以滑鼠右鍵按一下方案 > [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="81f47-361">To fail over a recovery plan, in **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="81f47-362">若要建立復原方案，請[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="81f47-362">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>
3. <span data-ttu-id="81f47-363">在 [測試容錯移轉] 中，選取 Azure VM 在容錯移轉之後要連接的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="81f47-363">In **Test Failover**, select the Azure network to which Azure VMs will be connected after failover occurs.</span></span>
4. <span data-ttu-id="81f47-364">按一下 [確定]  即可開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="81f47-364">Click **OK** to begin the failover.</span></span> <span data-ttu-id="81f47-365">您可以按一下 VM 以開啟其屬性，或在保存庫名稱 > [作業]  > [Site Recovery 作業] 中的 [測試容錯移轉] 作業上按一下，來追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="81f47-365">You can track progress by clicking on the VM to open its properties, or on the **Test Failover** job in vault name > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="81f47-366">容錯移轉完成之後，您應該也會看到複本 Azure 機器出現在 Azure 入口網站 > [虛擬機器]中。</span><span class="sxs-lookup"><span data-stu-id="81f47-366">After the failover completes, you should also be able to see the replica Azure machine appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="81f47-367">您應該確定 VM 為適當的大小、已連接到適當的網路，而且正在執行中。</span><span class="sxs-lookup"><span data-stu-id="81f47-367">You should make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="81f47-368">如果您已準備好在容錯移轉後進行連線，應該能夠連線到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="81f47-368">If you prepared for connections after failover, you should be able to connect to the Azure VM.</span></span>
7. <span data-ttu-id="81f47-369">完成後，在復原方案上按一下 [清除測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="81f47-369">Once you're done, click on **Cleanup test failover** on the recovery plan.</span></span> <span data-ttu-id="81f47-370">在 [記事]  中，記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="81f47-370">In **Notes** record and save any observations associated with the test failover.</span></span> <span data-ttu-id="81f47-371">這將刪除在測試容錯移轉期間所建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81f47-371">This will delete the virtual machines that were created during test failover.</span></span>

<span data-ttu-id="81f47-372">如需詳細資訊，請參閱[測試容錯移轉至 Azure](site-recovery-test-failover-to-azure.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="81f47-372">For more details, read the [Test failover to Azure](site-recovery-test-failover-to-azure.md) article.</span></span>



## <a name="monitor-the-deployment"></a><span data-ttu-id="81f47-373">監視部署</span><span class="sxs-lookup"><span data-stu-id="81f47-373">Monitor the deployment</span></span>

<span data-ttu-id="81f47-374">監視 Site Recovery 部署的組態設定、狀態和健康情況︰</span><span class="sxs-lookup"><span data-stu-id="81f47-374">Monitor the configuration settings, status, and health for your Site Recovery deployment:</span></span>

1. <span data-ttu-id="81f47-375">按一下保存庫名稱來存取 [基本資訊]  儀表板。</span><span class="sxs-lookup"><span data-stu-id="81f47-375">Click on the vault name to access the **Essentials** dashboard.</span></span> <span data-ttu-id="81f47-376">在此儀表板中，您可以追蹤 Site Recovery 作業、複寫狀態、復原方案、伺服器健康情況和事件。</span><span class="sxs-lookup"><span data-stu-id="81f47-376">In this dashboard you can track Site Recovery jobs, replication status, recovery plans, server health, and events.</span></span>  

    ![基本資訊](./media/site-recovery-hyper-v-site-to-azure/essentials.png)
2. <span data-ttu-id="81f47-378">在 [健康情況]  圖格中，您可以監視在過去 24 小時內發生問題的站台伺服器，以及 Site Recovery 引發的事件。</span><span class="sxs-lookup"><span data-stu-id="81f47-378">In the **Health** tile you can monitor site servers that are experiencing issue, and the events raised by Site Recovery in the last 24 hours.</span></span> <span data-ttu-id="81f47-379">您可以自訂 [基本資訊] 以顯示最適合您的圖格和配置，包括其他 Site Recovery 和備份保存庫的狀態。</span><span class="sxs-lookup"><span data-stu-id="81f47-379">You can customize Essentials to show the tiles and layouts that are most useful to you, including the status of other Site Recovery and Backup vaults.</span></span>
3. <span data-ttu-id="81f47-380">您可以在 [複寫的項目]、[復原方案] 和 [Site Recovery 作業] 圖格中管理和監視複寫。</span><span class="sxs-lookup"><span data-stu-id="81f47-380">You can manage and monitor replication in the **Replicated Items**, **Recovery Plans**, and **Site Recovery Jobs** tiles.</span></span> <span data-ttu-id="81f47-381">您可以在 [作業]  >  [Site Recovery 作業] 中鑽研作業以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="81f47-381">You can drill into jobs for more details in **Jobs** > **Site Recovery Jobs**.</span></span>

## <a name="command-line-provider-and-agent-installation"></a><span data-ttu-id="81f47-382">命令列 Provider 和代理程式安裝</span><span class="sxs-lookup"><span data-stu-id="81f47-382">Command-line Provider and agent installation</span></span>

<span data-ttu-id="81f47-383">您也可以使用下列命令列來安裝 Azure Site Recovery Provider 和代理程式。</span><span class="sxs-lookup"><span data-stu-id="81f47-383">The Azure Site Recovery Provider and agent can also be installed using the following command line.</span></span> <span data-ttu-id="81f47-384">這個方法可以用來在適用於 Windows Server 2012 R2 的伺服器核心上安裝提供者。</span><span class="sxs-lookup"><span data-stu-id="81f47-384">This method can be used to install the provider on a Server Core for Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="81f47-385">將提供者安裝檔案和註冊金鑰下載至資料夾。</span><span class="sxs-lookup"><span data-stu-id="81f47-385">Download the Provider installation file and registration key to a folder.</span></span> <span data-ttu-id="81f47-386">例如 C:\ASR。</span><span class="sxs-lookup"><span data-stu-id="81f47-386">For example C:\ASR.</span></span>
2. <span data-ttu-id="81f47-387">在提高權限的命令提示字元中，執行下列命令來擷取 Provider 安裝程式：</span><span class="sxs-lookup"><span data-stu-id="81f47-387">From an elevated command prompt, run these commands to extract the Provider installer:</span></span>

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="81f47-388">執行這個命令來安裝元件︰</span><span class="sxs-lookup"><span data-stu-id="81f47-388">Run this command to install the components:</span></span>

            C:\ASR> setupdr.exe /i
4. <span data-ttu-id="81f47-389">然後執行下列命令以在保存庫中註冊伺服器：</span><span class="sxs-lookup"><span data-stu-id="81f47-389">Then run these commands to register the server in the vault:</span></span>

            CD C:\Program Files\Microsoft Azure Site Recovery Provider\
            C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file>

<br/>
<span data-ttu-id="81f47-390">其中：</span><span class="sxs-lookup"><span data-stu-id="81f47-390">Where:</span></span>

* <span data-ttu-id="81f47-391">**/Credentials**：必要參數，用來指定註冊金鑰檔案所在的位置</span><span class="sxs-lookup"><span data-stu-id="81f47-391">**/Credentials**: Mandatory parameter that specifies the location in which the registration key file is located</span></span>  
* <span data-ttu-id="81f47-392">**/FriendlyName**：對於 Hyper-V 主機伺服器名稱的必要參數，該伺服器會出現在 Azure Site Recovery 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="81f47-392">**/FriendlyName**: Mandatory parameter for the name of the Hyper-V host server that appears in the Azure Site Recovery portal.</span></span>
* <span data-ttu-id="81f47-393">**/proxyAddress**：指定 Proxy 伺服器位址的選用參數。</span><span class="sxs-lookup"><span data-stu-id="81f47-393">**/proxyAddress**: Optional parameter that specifies the address of the proxy server.</span></span>
* <span data-ttu-id="81f47-394">**/proxyport** ：指定 Proxy 伺服器連接埠的選用參數。</span><span class="sxs-lookup"><span data-stu-id="81f47-394">**/proxyport** : Optional parameter that specifies the port of the proxy server.</span></span>
* <span data-ttu-id="81f47-395">**/proxyUsername**：指定 Proxy 使用者名稱 (如果 Proxy 需要驗證) 的選用參數。</span><span class="sxs-lookup"><span data-stu-id="81f47-395">**/proxyUsername**: Optional parameter that specifies the Proxy user name (if proxy requires authentication).</span></span>
* <span data-ttu-id="81f47-396">**/proxyPassword**：指定用於驗證 Proxy 伺服器的密碼 (如果 Proxy 需要驗證) 的選用參數。</span><span class="sxs-lookup"><span data-stu-id="81f47-396">**/proxyPassword**: Optional parameter that specifies the Password for authenticating with the proxy server (if proxy requires authentication).</span></span>


## <a name="network-bandwidth-considerations"></a><span data-ttu-id="81f47-397">網路頻寬考量</span><span class="sxs-lookup"><span data-stu-id="81f47-397">Network bandwidth considerations</span></span>
<span data-ttu-id="81f47-398">您可以使用 [Hyper-V 容量規劃工具](site-recovery-capacity-planner.md)來計算複寫 (初始複寫，而後是差異複寫) 所需的頻寬。</span><span class="sxs-lookup"><span data-stu-id="81f47-398">You can use the [Hyper-V capacity planner tool](site-recovery-capacity-planner.md) to calculate the bandwidth you need for replication (initial replication and then delta).</span></span> <span data-ttu-id="81f47-399">若要控制複寫所用的頻寬數量，您有幾個選項可用︰</span><span class="sxs-lookup"><span data-stu-id="81f47-399">To control the amount of bandwidth use for replication you have a few options:</span></span>

* <span data-ttu-id="81f47-400">**節流頻寬**︰複寫至 Azure 的 Hyper-V 流量會經過特定的 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="81f47-400">**Throttle bandwidth**: Hyper-V traffic that replicates to Azure goes through a specific Hyper-V host.</span></span> <span data-ttu-id="81f47-401">您可以在主機伺服器上進行頻寬節流。</span><span class="sxs-lookup"><span data-stu-id="81f47-401">You can throttle bandwidth on the host server.</span></span>
* <span data-ttu-id="81f47-402">**調整頻寬**︰您可以使用幾個登錄機碼來影響用於複寫的頻寬。</span><span class="sxs-lookup"><span data-stu-id="81f47-402">**Tweak bandwidth**: You can influence the bandwidth used for replication using a couple of registry keys.</span></span>

### <a name="throttle-bandwidth"></a><span data-ttu-id="81f47-403">節流頻寬</span><span class="sxs-lookup"><span data-stu-id="81f47-403">Throttle bandwidth</span></span>
1. <span data-ttu-id="81f47-404">在 Hyper-V 主機伺服器上開啟 Microsoft Azure 備份 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="81f47-404">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host server.</span></span> <span data-ttu-id="81f47-405">根據預設，Microsoft Azure 備份的捷徑位於桌面上或在 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin 中。</span><span class="sxs-lookup"><span data-stu-id="81f47-405">By default a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="81f47-406">在嵌入式管理單元中，按一下 [變更屬性] 。</span><span class="sxs-lookup"><span data-stu-id="81f47-406">In the snap-in click **Change Properties**.</span></span>
3. <span data-ttu-id="81f47-407">在 [節流] 索引標籤上，選取 [啟用備份操作的網際網路頻寬使用節流設定]，然後設定工作和非工作時數的限制。</span><span class="sxs-lookup"><span data-stu-id="81f47-407">On the **Throttling** tab select **Enable internet bandwidth usage throttling for backup operations**, and set the limits for work and non-work hours.</span></span> <span data-ttu-id="81f47-408">有效範圍是每秒 512 Kbps 到 102 Mbps。</span><span class="sxs-lookup"><span data-stu-id="81f47-408">Valid ranges are from 512 Kbps to 102 Mbps per second.</span></span>

    ![節流頻寬](./media/site-recovery-hyper-v-site-to-azure/throttle2.png)

<span data-ttu-id="81f47-410">您也可以使用 [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) Cmdlet 來設定節流。</span><span class="sxs-lookup"><span data-stu-id="81f47-410">You can also use the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet to set throttling.</span></span> <span data-ttu-id="81f47-411">以下是一個範例：</span><span class="sxs-lookup"><span data-stu-id="81f47-411">Here's a sample:</span></span>

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

<span data-ttu-id="81f47-412">**Set-OBMachineSetting -NoThrottle** 表示不需要節流。</span><span class="sxs-lookup"><span data-stu-id="81f47-412">**Set-OBMachineSetting -NoThrottle** indicates that no throttling is required.</span></span>

### <a name="influence-network-bandwidth"></a><span data-ttu-id="81f47-413">影響網路頻寬</span><span class="sxs-lookup"><span data-stu-id="81f47-413">Influence network bandwidth</span></span>
1. <span data-ttu-id="81f47-414">在登錄中瀏覽至 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**。</span><span class="sxs-lookup"><span data-stu-id="81f47-414">In the registry navigate to **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.</span></span>
   * <span data-ttu-id="81f47-415">若要影響複製磁碟上的頻寬流量，請修改 **UploadThreadsPerVM**的值，如果不存在則請建立機碼。</span><span class="sxs-lookup"><span data-stu-id="81f47-415">To influence the bandwidth traffic on a replicating disk, modify the value the **UploadThreadsPerVM**, or create the key if it doesn't exist.</span></span>
   * <span data-ttu-id="81f47-416">若要影響從 Azure 容錯回復流量的頻寬，請修改 **DownloadThreadsPerVM**的值。</span><span class="sxs-lookup"><span data-stu-id="81f47-416">To influence the bandwidth for failback traffic from Azure, modify the value **DownloadThreadsPerVM**.</span></span>
2. <span data-ttu-id="81f47-417">預設值為 4。</span><span class="sxs-lookup"><span data-stu-id="81f47-417">The default value is 4.</span></span> <span data-ttu-id="81f47-418">在 “overprovisioned” 網路中，這些登錄機碼必須變更自其預設值。</span><span class="sxs-lookup"><span data-stu-id="81f47-418">In an “overprovisioned” network, these registry keys should be changed from the default values.</span></span> <span data-ttu-id="81f47-419">最大值為 32。</span><span class="sxs-lookup"><span data-stu-id="81f47-419">The maximum is 32.</span></span> <span data-ttu-id="81f47-420">監視流量，將此值最佳化。</span><span class="sxs-lookup"><span data-stu-id="81f47-420">Monitor traffic to optimize the value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81f47-421">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81f47-421">Next steps</span></span>

<span data-ttu-id="81f47-422">在初始複寫完成，且您已測試部署之後，便可以視需要叫用容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="81f47-422">After initial replication is complete, and you've tested the deployment, you can invoke failovers as the need arises.</span></span> <span data-ttu-id="81f47-423">[深入了解](site-recovery-failover.md)不同類型的容錯移轉及執行方法。</span><span class="sxs-lookup"><span data-stu-id="81f47-423">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
