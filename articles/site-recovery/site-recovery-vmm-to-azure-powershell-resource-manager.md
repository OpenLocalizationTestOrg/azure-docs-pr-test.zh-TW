---
title: "使用 Azure Site Recovery 及 PowerShell (Resource Manager) 複寫 VMM 雲端中的 HYPER-V 虛擬機器 | Microsoft Docs"
description: "使用 Azure Site Recovery 及 PowerShell 複寫 VMM 雲端中的 HYPER-V 虛擬機器"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: 34086044db752f09f1282517b59856091e85c2fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="dcfe6-103">使用 PowerShell 和 Azure Resource Manager 將 Hyper-V 虛擬機器 (位於 VMM 雲端中) 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="dcfe6-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dcfe6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dcfe6-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="dcfe6-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="dcfe6-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="dcfe6-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="dcfe6-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="dcfe6-107">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="dcfe6-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="dcfe6-108">Overview</span><span class="sxs-lookup"><span data-stu-id="dcfe6-108">Overview</span></span>
<span data-ttu-id="dcfe6-109">Azure Site Recovery 可在一些部署案例中協調虛擬機器的複寫、容錯移轉及復原，為您的商務持續性與災害復原 (BCDR) 做出貢獻。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="dcfe6-110">如需完整的部署案例清單，請參閱 [Azure Site Recovery 概觀](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="dcfe6-111">本文說明如何使用 PowerShell 自動化您在設定 Azure Site Recovery 將 System Center VMM 雲端中的 HYPER-V 虛擬機器，複寫到 Azure 儲存體時常需要執行的工作。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="dcfe6-112">本文包含案例的必要條件，並對您示範</span><span class="sxs-lookup"><span data-stu-id="dcfe6-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="dcfe6-113">如何設定復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="dcfe6-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="dcfe6-114">您會在來源 VMM 伺服器上安裝 Azure Site Recovery 提供者。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="dcfe6-115">在保存庫中註冊伺服器、新增 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="dcfe6-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="dcfe6-116">在 Hyper-V 主機伺服器上安裝 Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="dcfe6-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="dcfe6-117">設定將套用到所有受保護虛擬機器之 VMM 雲端的保護設定</span><span class="sxs-lookup"><span data-stu-id="dcfe6-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="dcfe6-118">為那些虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="dcfe6-119">測試容錯移轉，確認一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="dcfe6-120">您在設定此案例如有任何問題，可將問題張貼到 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="dcfe6-121">Azure 建立和處理資源的部署模型有二種： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dcfe6-122">本文涵蓋內容包括如何使用 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-122">This article covers using the Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="dcfe6-123">開始之前</span><span class="sxs-lookup"><span data-stu-id="dcfe6-123">Before you start</span></span>
<span data-ttu-id="dcfe6-124">確認您已備妥這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="dcfe6-125">Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="dcfe6-125">Azure prerequisites</span></span>
* <span data-ttu-id="dcfe6-126">您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="dcfe6-127">如果您沒有此帳戶，請先前往 [免費帳戶](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="dcfe6-128">此外，您可以參閱 [Azure Site Recovery 管理員價格](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="dcfe6-129">如果您正在嘗試複寫至 CSP 訂用帳戶的案例，您將需要 CSP 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="dcfe6-130">若要深入了解 CSP 程式，請參閱 [如何註冊 CSP 程式](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="dcfe6-131">您將需要 Azure v2 儲存體 (Resource Manager) 帳戶，才能將複寫的資料儲存至 Azure。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="dcfe6-132">此帳戶必須啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="dcfe6-133">它應該與 Azure Site Recovery 服務位於相同的區或，且與相同的訂用帳戶或 CSP 訂用帳戶關聯。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="dcfe6-134">若要深入了解設定 Azure 儲存體，請參閱 [Microsoft Azure 儲存體簡介](../storage/common/storage-introduction.md) 。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="dcfe6-135">您必須確定您要保護的虛擬機器符合 [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="dcfe6-136">目前，只有 VM 層級作業可以通過 Powershell。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="dcfe6-137">即將推出對復原計劃層級作業的支援。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="dcfe6-138">現在，您僅限在「受保護 VM」資料粒度才能執行容錯移轉，而不能在復原計劃層級。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-138">For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="dcfe6-139">VMM 必要條件</span><span class="sxs-lookup"><span data-stu-id="dcfe6-139">VMM prerequisites</span></span>
* <span data-ttu-id="dcfe6-140">您將需要在在 System Center 2012 R2 上執行的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="dcfe6-141">任何包含您想要保護之虛擬機器的 VMM 伺服器都必須執行 Azure Site Recovery 提供者。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="dcfe6-142">它會在部署 Azure Site Recovery 期間安裝。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="dcfe6-143">在您想要保護的 VMM 伺服器上，您至少需要一個雲端。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="dcfe6-144">這個雲端應該包含：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-144">The cloud should contain:</span></span>
  * <span data-ttu-id="dcfe6-145">一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="dcfe6-146">每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="dcfe6-147">來源 Hyper-V 伺服器上的一或多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="dcfe6-148">深入了解設定 VMM 雲端：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="dcfe6-149">如需深入了解私人 VMM 雲端，請參閱 [System Center 2012 R2 VMM 的私人雲端新功能](http://go.microsoft.com/fwlink/?LinkId=324952)及 [VMM 2012 和雲端](http://go.microsoft.com/fwlink/?LinkId=324956)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="dcfe6-150">深入了解 [設定 VMM 雲端網狀架構](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="dcfe6-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="dcfe6-151">在您備妥雲端網狀架構元素之後，如需了解如何建立私人雲端，請參閱[在 VMM 中建立私人雲端](http://go.microsoft.com/fwlink/p/?LinkId=324953)及[逐步解說：使用 System Center 2012 SP1 VMM 建立私人雲端](http://go.microsoft.com/fwlink/p/?LinkId=324954)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="dcfe6-152">Hyper-V 的必要條件</span><span class="sxs-lookup"><span data-stu-id="dcfe6-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="dcfe6-153">Hyper-V 主機伺服器必須至少執行具備 Hyper-V 角色的 **Windows Server 2012** 或 **Microsoft Hyper-V Server 2012** 並已安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="dcfe6-154">如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="dcfe6-155">您必須手動設定叢集代理。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="dcfe6-156">如需</span><span class="sxs-lookup"><span data-stu-id="dcfe6-156">For</span></span>
* <span data-ttu-id="dcfe6-157">如需指示，請參閱 [如何設定 Hyper-V 複本代理人](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="dcfe6-158">您想要管理保護的任何 Hyper-V 主機伺服計或叢集都必須包含在 VMM 雲端中。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="dcfe6-159">網路對應的必要條件</span><span class="sxs-lookup"><span data-stu-id="dcfe6-159">Network mapping prerequisites</span></span>
<span data-ttu-id="dcfe6-160">當您在 Azure 中保護虛擬機器時，網路對應會對應來源 VMM 伺服器上的虛擬機器網路和目標 Azure 網路，以啟用下列功能：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="dcfe6-161">在相同網路上容錯移轉的所有機器都可以彼此連接，無論它們隸屬於哪個復原計畫都一樣。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="dcfe6-162">如果目標 Azure 網路上已設定網路閘道，則虛擬機器可以連接到其他內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="dcfe6-163">如果您未設定網路對應，則只有在相同復原計畫中容錯移轉的虛擬機器才能在容錯移轉到 Azure 之後彼此連接。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="dcfe6-164">如果您想要部署網路對應，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="dcfe6-165">您想要在來源 VMM 伺服器上保護的虛擬機器應該連線到 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="dcfe6-166">該網路應該連結到與雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="dcfe6-167">複寫的虛擬機器可在容錯移轉之後連線的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="dcfe6-168">您將在容錯移轉時選取此網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="dcfe6-169">此網路應該和您的 Azure Site Recovery 訂用帳戶在相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="dcfe6-170">在下列內容中深入了解網路對應</span><span class="sxs-lookup"><span data-stu-id="dcfe6-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="dcfe6-171">如何在 VMM 中設定邏輯網路</span><span class="sxs-lookup"><span data-stu-id="dcfe6-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="dcfe6-172">如何在 VMM 中設定 VM 網路和閘道</span><span class="sxs-lookup"><span data-stu-id="dcfe6-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="dcfe6-173">如何在 Azure 中設定和監視虛擬網路</span><span class="sxs-lookup"><span data-stu-id="dcfe6-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="dcfe6-174">PowerShell 必要條件</span><span class="sxs-lookup"><span data-stu-id="dcfe6-174">PowerShell prerequisites</span></span>
<span data-ttu-id="dcfe6-175">確定 Azure PowerShell 已經準備就緒。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="dcfe6-176">如果您已經使用 PowerShell，您必須升級至 0.8.10 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="dcfe6-177">如需設定 PowerShell 的資訊，請參閱 [安裝和設定 Azure PowerShell 指南](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="dcfe6-178">一旦已安裝並設定 PowerShell，您可以檢視 [這裡](/powershell/azure/overview)之服務的所有可用的 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="dcfe6-179">如需了解可協助您使用這些 Cmdlet 的提示 (例如參數值、輸入及輸出在 Azure PowerShell 中的處理方式)，請參閱 [Azure Cmdlet 使用者入門](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="dcfe6-180">步驟 1：設定訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dcfe6-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="dcfe6-181">從 Azure powershell，登入您的 Azure 帳戶︰使用下列 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="dcfe6-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="dcfe6-182">取得您的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="dcfe6-183">這樣也會列出每個訂用帳戶的 subscriptionID。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="dcfe6-184">記下您要建立復原服務保存庫之訂用帳戶的 subscriptionID</span><span class="sxs-lookup"><span data-stu-id="dcfe6-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="dcfe6-185">設定藉由提及訂用帳戶識別碼在其中建立復原服務保存庫的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dcfe6-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="dcfe6-186">步驟 2：建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="dcfe6-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="dcfe6-187">在 Azure Resource Manager 中建立一個資源群組 (如果您還沒有資源群組)</span><span class="sxs-lookup"><span data-stu-id="dcfe6-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="dcfe6-188">建立新的復原服務保存庫，並儲存在變數 (稍後使用) 中建立的 ASR 保存庫物件。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="dcfe6-189">您也可以使用 Get-AzureRMRecoveryServicesVault Cmdlet 擷取建立後的 ASR 保存庫物件：-</span><span class="sxs-lookup"><span data-stu-id="dcfe6-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="dcfe6-190">步驟 3：設定復原服務保存庫內容</span><span class="sxs-lookup"><span data-stu-id="dcfe6-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="dcfe6-191">執行下面的命令來設定保存庫內容。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="dcfe6-192">步驟 4：安裝 Azure Site Recovery 提供者</span><span class="sxs-lookup"><span data-stu-id="dcfe6-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="dcfe6-193">在 VMM 機器上，執行下列命令來建立目錄：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="dcfe6-194">執行下列命令，使用已下載的提供者將檔案解壓縮</span><span class="sxs-lookup"><span data-stu-id="dcfe6-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="dcfe6-195">使用下列命令安裝提供者：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-195">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="dcfe6-196">等待安裝完成。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="dcfe6-197">使用下列命令在保存庫中註冊伺服器：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="dcfe6-198">步驟 5：建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="dcfe6-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="dcfe6-199">如果您沒有 Azure 儲存體帳戶，請執行下列命令，在相同地區建立啟用帳戶的異地複寫：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="dcfe6-200">請注意，儲存體帳戶必須與 Azure Site Recovery 服務位於相同的區或，且與相同的訂用帳戶關聯。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="dcfe6-201">步驟 6：安裝 Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="dcfe6-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="dcfe6-202">在 [http:/aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) 下載 Azure 復原服務代理程式，並在 VMM 雲端中您要保護的每一個 Hyper-V 主機伺服器上將其安裝。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="dcfe6-203">在所有 VMM 主機上執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="dcfe6-204">步驟 7：設定雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="dcfe6-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="dcfe6-205">執行下列命令來建立 Azure 的複寫原則：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="dcfe6-206">執行下列命令以取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="dcfe6-207">取得原則詳細資料給使用已建立作業並且提及易記原則名稱的變數︰</span><span class="sxs-lookup"><span data-stu-id="dcfe6-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="dcfe6-208">啟動保護容器與複寫原則的關聯：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="dcfe6-209">完成工作之後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="dcfe6-210">完成工作處理之後，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="dcfe6-211">若要檢查作業是否完成，請執行 [監視活動](#monitor)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="dcfe6-212">步驟 8：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="dcfe6-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="dcfe6-213">開始網路對應之前，請確認來源 VMM 伺服器上的虛擬機器已連線到 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="dcfe6-214">此外，請建立一或多個 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="dcfe6-215">在 [使用 Azure Resource Manager 和 PowerShell 建立具有站對站 VPN 連線的虛擬網路](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="dcfe6-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="dcfe6-216">請注意，多個虛擬機器網路可對應至單一 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="dcfe6-217">如果目標網路具有多個子網路，且其中一個子網路的名稱和來源虛擬機器所在之子網路名稱相同，複本虛擬機器將會在容錯移轉之後連線到該目標子網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="dcfe6-218">如果沒有目標子網路具有相符的名稱，虛擬機器將會連線到網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="dcfe6-219">第一個命令會取得目前的 Azure Site Recovery 保存庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="dcfe6-220">命令會將 Microsoft Azure Site Recovery 伺服器儲存在 $Servers 陣列變數。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="dcfe6-221">第二個命令會取得 $Servers 陣列中第一部伺服器的站台復原網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="dcfe6-222">此命令會在 $Networks 變數中儲存網路。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="dcfe6-223">第三個命令會取得 Azure 虛擬網路，然後取得 $AzureVmNetworks 變數中的該值。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="dcfe6-224">最終的 Cmdlet 會在主要網路與 Azure 虛擬機器網路之間建立對應。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="dcfe6-225">Cmdlet 會將主要網路指定為 $Networks 的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="dcfe6-226">Cmdlet 會將虛擬機器網路指定為 $AzureVmNetworks 的第一個元素。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="dcfe6-227">步驟 9：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="dcfe6-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="dcfe6-228">正確設定伺服器、雲端和網路後，您就可以對雲端中的虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="dcfe6-229">請注意：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-229">Note the following:</span></span>

* <span data-ttu-id="dcfe6-230">虛擬機器必須符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="dcfe6-231">請在《規劃指南》的 [必要條件和支援](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 中查看這些需求。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="dcfe6-232">若要啟用保護功能，您必須為虛擬機器設定作業系統和作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="dcfe6-233">當您使用虛擬機器範本在 VMM 中建立虛擬機器時，您可以設定屬性。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="dcfe6-234">您也可以在虛擬機器屬性的 [一般] 及 [硬體設定] 索引標籤上，為現有的虛擬機器設定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="dcfe6-235">若未在 VMM 中設定這些屬性，您將可在 Azure 站台復原入口網站中加以設定。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="dcfe6-236">若要啟用保護，請執行下列命令以取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="dcfe6-237">執行下列命令以取得保護實體 (VM)：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="dcfe6-238">執行下列命令以啟用 VM 的 DR：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="dcfe6-239">測試您的部署</span><span class="sxs-lookup"><span data-stu-id="dcfe6-239">Test your deployment</span></span>
<span data-ttu-id="dcfe6-240">若要測試部署，您可以對單一虛擬機器執行測試容錯移轉，或者建立包含多部虛擬機器的復原方案，再對這個方案執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="dcfe6-241">測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="dcfe6-242">請注意：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-242">Note that:</span></span>

* <span data-ttu-id="dcfe6-243">如果您在容錯移轉之後要使用遠端桌面連接到 Azure 中的虛擬機器，請先在虛擬機器上啟用遠端桌面連線，再執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="dcfe6-244">容錯移轉之後，您將透過遠端桌面使用公用 IP 位址連接到 Azure 中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="dcfe6-245">如果想要這樣做，請確定沒有任何網域原則禁止您使用公用位址連接到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="dcfe6-246">若要檢查作業是否完成，請執行 [監視活動](#monitor)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="dcfe6-247">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="dcfe6-247">Run a test failover</span></span>
- <span data-ttu-id="dcfe6-248">執行下列命令來啟動測試容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="dcfe6-249">執行計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="dcfe6-249">Run a planned failover</span></span>
- <span data-ttu-id="dcfe6-250">執行下列命令來啟動計劃性容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="dcfe6-251">執行非計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="dcfe6-251">Run an unplanned failover</span></span>
- <span data-ttu-id="dcfe6-252">執行下列命令來啟動非計劃性容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="dcfe6-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="dcfe6-253"><a name=monitor></a> 監視活動</span><span class="sxs-lookup"><span data-stu-id="dcfe6-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="dcfe6-254">使用下列命令來監視活動。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="dcfe6-255">請注意，您必須在工作之間等候處理程序完成。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="dcfe6-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dcfe6-256">Next steps</span></span>
<span data-ttu-id="dcfe6-257">[閱讀更多](/powershell/module/azurerm.recoveryservices.backup/#recovery) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="dcfe6-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
