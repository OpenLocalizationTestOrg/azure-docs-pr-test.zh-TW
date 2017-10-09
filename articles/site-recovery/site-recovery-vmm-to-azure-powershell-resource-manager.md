---
title: "使用 Azure Site Recovery 和 PowerShell （資源管理員） 的 VMM 雲端中的 aaaReplicate HYPER-V 虛擬機器 |Microsoft 文件"
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
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="08866-103">使用 PowerShell 和 Azure 資源管理員的 VMM 雲端 tooAzure 中的 HYPER-V 虛擬機器，複寫</span><span class="sxs-lookup"><span data-stu-id="08866-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08866-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="08866-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="08866-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="08866-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="08866-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="08866-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="08866-107">PowerShell - 傳統</span><span class="sxs-lookup"><span data-stu-id="08866-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="08866-108">概觀</span><span class="sxs-lookup"><span data-stu-id="08866-108">Overview</span></span>
<span data-ttu-id="08866-109">Azure Site Recovery 提供 tooyour 業務續航力和災害復原 (BCDR) 策略可藉由協調複寫、 容錯移轉和復原的虛擬機器中部署案例的數目。</span><span class="sxs-lookup"><span data-stu-id="08866-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="08866-110">如需完整的部署案例請參閱 hello [Azure 站台復原概觀](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="08866-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="08866-111">本文章將示範如何 toouse PowerShell tooautomate 一般工作時，您需要 tooperform 您設定 Azure Site Recovery tooreplicate HYPER-V 虛擬機器在 System Center VMM 雲端 tooAzure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="08866-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="08866-112">hello 發行項包含 hello 案例的先決條件，並示範您</span><span class="sxs-lookup"><span data-stu-id="08866-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="08866-113">如何復原服務保存庫註冊 tooset</span><span class="sxs-lookup"><span data-stu-id="08866-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="08866-114">Hello 來源 VMM 伺服器上安裝 Azure Site Recovery Provider hello</span><span class="sxs-lookup"><span data-stu-id="08866-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="08866-115">Hello 保存庫中註冊伺服器 hello、 新增 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="08866-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="08866-116">HYPER-V 主機伺服器上安裝 hello Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="08866-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="08866-117">設定會套用的 tooall 受保護的虛擬機器的 VMM 雲端的保護設定</span><span class="sxs-lookup"><span data-stu-id="08866-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="08866-118">為那些虛擬機器啟用保護。</span><span class="sxs-lookup"><span data-stu-id="08866-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="08866-119">測試容錯移轉 hello toomake，確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="08866-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="08866-120">如果您遇到此案例中所設定的問題時，請張貼您的問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="08866-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="08866-121">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="08866-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="08866-122">本文說明如何使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="08866-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="08866-123">開始之前</span><span class="sxs-lookup"><span data-stu-id="08866-123">Before you start</span></span>
<span data-ttu-id="08866-124">確認您已備妥這些必要條件：</span><span class="sxs-lookup"><span data-stu-id="08866-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="08866-125">Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="08866-125">Azure prerequisites</span></span>
* <span data-ttu-id="08866-126">您將需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="08866-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="08866-127">如果您沒有此帳戶，請先前往 [免費帳戶](https://azure.microsoft.com/free)。</span><span class="sxs-lookup"><span data-stu-id="08866-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="08866-128">此外，您可以閱讀 hello [Azure Site Recovery Manager 定價](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="08866-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="08866-129">如果您嘗試出 hello 複寫 tooa CSP 訂閱案例，您將需要 CSP 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08866-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="08866-130">深入了解中的 hello CSP 程式[如何在 hello CSP 程式 tooenroll](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx)。</span><span class="sxs-lookup"><span data-stu-id="08866-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="08866-131">您將需要 Azure v2 存放裝置 （資源管理員） 帳戶 toostore 複寫資料 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="08866-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="08866-132">hello 帳戶必須啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="08866-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="08866-133">在 hello 與 hello Azure Site Recovery 服務相同的區域和 hello 與相關聯，它應該是相同的訂用帳戶或 hello CSP 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08866-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="08866-134">toolearn 進一步了解設定 Azure 儲存體，請參閱 hello[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)供參考。</span><span class="sxs-lookup"><span data-stu-id="08866-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="08866-135">您必須確定您想 tooprotect 虛擬機器符合 hello toomake [Azure 虛擬機器必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="08866-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="08866-136">目前，只有 VM 層級作業可以通過 Powershell。</span><span class="sxs-lookup"><span data-stu-id="08866-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="08866-137">即將推出對復原計劃層級作業的支援。</span><span class="sxs-lookup"><span data-stu-id="08866-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="08866-138">現在，您必須是有限的 tooperforming 容錯移轉只能在 'protected VM' 資料粒度，而不是在復原方案層級。</span><span class="sxs-lookup"><span data-stu-id="08866-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="08866-139">VMM 必要條件</span><span class="sxs-lookup"><span data-stu-id="08866-139">VMM prerequisites</span></span>
* <span data-ttu-id="08866-140">您將需要在在 System Center 2012 R2 上執行的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="08866-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="08866-141">您所要的任何包含虛擬機器的 VMM 伺服器 tooprotect 必須執行 hello Azure Site Recovery Provider。</span><span class="sxs-lookup"><span data-stu-id="08866-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="08866-142">這會在 hello Azure Site Recovery 部署期間安裝。</span><span class="sxs-lookup"><span data-stu-id="08866-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="08866-143">您必須在 hello 想 tooprotect VMM 伺服器上的至少一個雲端。</span><span class="sxs-lookup"><span data-stu-id="08866-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="08866-144">hello 雲端應包含：</span><span class="sxs-lookup"><span data-stu-id="08866-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="08866-145">一或多個 VMM 主機群組。</span><span class="sxs-lookup"><span data-stu-id="08866-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="08866-146">每個主機群組中的一或多個 Hyper-V 主機伺服器或叢集。</span><span class="sxs-lookup"><span data-stu-id="08866-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="08866-147">一或多個虛擬機器 hello 來源 HYPER-V 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="08866-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="08866-148">深入了解設定 VMM 雲端：</span><span class="sxs-lookup"><span data-stu-id="08866-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="08866-149">深入了解私人 VMM 雲端中[What's New in 搭配 System Center 2012 R2 VMM 的私人雲端](http://go.microsoft.com/fwlink/?LinkId=324952)和[VMM 2012 和 hello 雲端](http://go.microsoft.com/fwlink/?LinkId=324956)。</span><span class="sxs-lookup"><span data-stu-id="08866-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="08866-150">深入了解[設定 hello VMM 雲端網狀架構](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="08866-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="08866-151">在您備妥雲端網狀架構元素之後，如需了解如何建立私人雲端，請參閱[在 VMM 中建立私人雲端](http://go.microsoft.com/fwlink/p/?LinkId=324953)及[逐步解說：使用 System Center 2012 SP1 VMM 建立私人雲端](http://go.microsoft.com/fwlink/p/?LinkId=324954)。</span><span class="sxs-lookup"><span data-stu-id="08866-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="08866-152">Hyper-V 的必要條件</span><span class="sxs-lookup"><span data-stu-id="08866-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="08866-153">hello HYPER-V 主機伺服器必須執行至少**Windows Server 2012**與 HYPER-V 角色或**Microsoft HYPER-V Server 2012**和擁有 hello 安裝最新的更新。</span><span class="sxs-lookup"><span data-stu-id="08866-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="08866-154">如果您在叢集中執行 Hyper-V，請注意，如果您具有靜態 IP 位址叢集，並不會自動建立叢集代理。</span><span class="sxs-lookup"><span data-stu-id="08866-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="08866-155">您以手動方式將需要 tooconfigure hello 叢集代理人。</span><span class="sxs-lookup"><span data-stu-id="08866-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="08866-156">如需</span><span class="sxs-lookup"><span data-stu-id="08866-156">For</span></span>
* <span data-ttu-id="08866-157">如需指示，請參閱[如何 tooConfigure HYPER-V 複本代理人](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)。</span><span class="sxs-lookup"><span data-stu-id="08866-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="08866-158">必須包含任何 HYPER-V 主機伺服器或叢集，您會想 toomanage 保護 VMM 雲端中。</span><span class="sxs-lookup"><span data-stu-id="08866-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="08866-159">網路對應的必要條件</span><span class="sxs-lookup"><span data-stu-id="08866-159">Network mapping prerequisites</span></span>
<span data-ttu-id="08866-160">當您保護 Azure 中虛擬機器時，hello 進行網路對應 hello hello 來源 VMM 伺服器與目標 Azure 網路 tooenable hello 下列上的虛擬機器網路：</span><span class="sxs-lookup"><span data-stu-id="08866-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="08866-161">容錯移轉 hello 相同的所有機器網路可以連接 tooeach 其他，無論它們是在復原計劃。</span><span class="sxs-lookup"><span data-stu-id="08866-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="08866-162">如果網路閘道 hello 目標 Azure 網路上的安裝程式，虛擬機器可以連接 tooother 在內部部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="08866-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="08866-163">如果您未設定網路對應，僅 hello 容錯移轉 hello 中相同的虛擬機器容錯移轉 tooAzure 後，即可能 tooconnect tooeach 其他復原方案。</span><span class="sxs-lookup"><span data-stu-id="08866-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="08866-164">如果您想 toodeploy 網路對應，您將需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="08866-165">hello 想 tooprotect hello 來源 VMM 伺服器上的虛擬機器應連接的 tooa VM 網路。</span><span class="sxs-lookup"><span data-stu-id="08866-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="08866-166">該網路應連結的 tooa hello 雲端相關聯的邏輯網路。</span><span class="sxs-lookup"><span data-stu-id="08866-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="08866-167">Azure 網路 toowhich 複寫虛擬機器可以容錯移轉之後連接。</span><span class="sxs-lookup"><span data-stu-id="08866-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="08866-168">您將在容錯移轉的 hello 階段選取此網路。</span><span class="sxs-lookup"><span data-stu-id="08866-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="08866-169">hello 網路應位於 hello 與 Azure Site Recovery 訂用帳戶相同的區域。</span><span class="sxs-lookup"><span data-stu-id="08866-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="08866-170">在下列內容中深入了解網路對應</span><span class="sxs-lookup"><span data-stu-id="08866-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="08866-171">如何在 VMM 中的 tooconfigure 邏輯網路</span><span class="sxs-lookup"><span data-stu-id="08866-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="08866-172">如何 tooconfigure VM 網路和閘道在 VMM 中</span><span class="sxs-lookup"><span data-stu-id="08866-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="08866-173">如何 tooconfigure 和監視 Azure 中的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="08866-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="08866-174">PowerShell 必要條件</span><span class="sxs-lookup"><span data-stu-id="08866-174">PowerShell prerequisites</span></span>
<span data-ttu-id="08866-175">請確定您具有 Azure PowerShell 準備 toogo。</span><span class="sxs-lookup"><span data-stu-id="08866-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="08866-176">如果您已經使用 PowerShell，您將需要 tooupgrade tooversion 0.8.10 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="08866-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="08866-177">PowerShell 設定的詳細資訊，請參閱 hello[引導 tooinstall 和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="08866-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="08866-178">一旦您已安裝並設定 PowerShell，您可以檢視所有 hello 可用的 hello 服務 cmdlet[這裡](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="08866-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="08866-179">toolearn 的相關技巧，可協助您使用 hello cmdlet，例如如何參數值、 輸入和輸出通常處理 Azure PowerShell，請參閱 hello[引導 tooget 開始使用 Azure Cmdlet](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="08866-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="08866-180">步驟 1： 設定 hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="08866-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="08866-181">從 Azure powershell、 Azure 帳戶的登入 tooyour： 使用下列 cmdlet 的 hello</span><span class="sxs-lookup"><span data-stu-id="08866-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="08866-182">取得您的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="08866-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="08866-183">這也會列出 hello 訂用帳戶每一個 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08866-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="08866-184">記下您想在其中 toocreate hello 復原服務保存庫的 hello 訂用帳戶的 hello subscriptionID</span><span class="sxs-lookup"><span data-stu-id="08866-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="08866-185">設定中的 hello 復原服務保存庫是由一提 hello 訂用帳戶 ID 的 toobe hello 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="08866-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="08866-186">步驟 2：建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="08866-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="08866-187">在 Azure Resource Manager 中建立一個資源群組 (如果您還沒有資源群組)</span><span class="sxs-lookup"><span data-stu-id="08866-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="08866-188">建立新的復原服務保存庫並儲存在變數 （會使用更新版本） 中建立 ASR 保存庫物件的 hello。</span><span class="sxs-lookup"><span data-stu-id="08866-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="08866-189">您也可以擷取 hello ASR 保存庫後建立物件使用 hello Get AzureRMRecoveryServicesVault 指令程式:-</span><span class="sxs-lookup"><span data-stu-id="08866-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="08866-190">步驟 3： 設定 hello 復原服務保存庫內容</span><span class="sxs-lookup"><span data-stu-id="08866-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="08866-191">藉由執行下列命令 hello 設定 hello 保存庫的內容。</span><span class="sxs-lookup"><span data-stu-id="08866-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="08866-192">步驟 4： 安裝 hello Azure Site Recovery Provider</span><span class="sxs-lookup"><span data-stu-id="08866-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="08866-193">Hello VMM 在電腦上，執行下列命令的 hello 建立目錄：</span><span class="sxs-lookup"><span data-stu-id="08866-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="08866-194">擷取使用 hello 下載提供者藉由執行下列命令的 hello hello 檔案</span><span class="sxs-lookup"><span data-stu-id="08866-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="08866-195">安裝 hello 提供者使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="08866-195">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="08866-196">等候 hello 安裝 toofinish。</span><span class="sxs-lookup"><span data-stu-id="08866-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="08866-197">使用下列命令的 hello hello 保存庫中註冊伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="08866-198">步驟 5：建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="08866-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="08866-199">如果您沒有 Azure 儲存體帳戶，建立 啟用地理複寫帳戶在 hello 同一地區 hello 保存庫執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="08866-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="08866-200">請注意，hello 儲存體帳戶必須在 hello 與 hello Azure Site Recovery 服務相同的區域和與其相關聯 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08866-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="08866-201">步驟 6： 安裝 Azure Recovery Services Agent hello</span><span class="sxs-lookup"><span data-stu-id="08866-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="08866-202">下載 hello Azure 復原服務代理程式在[http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) ，而且它位於 hello VMM 每部 HYPER-V 主機伺服器上雲端您安裝想 tooprotect。</span><span class="sxs-lookup"><span data-stu-id="08866-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="08866-203">執行下列命令，在所有 VMM 主機上的 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="08866-204">步驟 7：設定雲端保護設定</span><span class="sxs-lookup"><span data-stu-id="08866-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="08866-205">建立複寫原則 tooAzure 藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="08866-206">藉由執行下列命令的 hello 取得保護容器：</span><span class="sxs-lookup"><span data-stu-id="08866-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="08866-207">收到 hello 原則詳細資料 tooa 變數使用 hello 作業所建立然後提及 hello 原則的易記名稱：</span><span class="sxs-lookup"><span data-stu-id="08866-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="08866-208">開始 hello 複寫原則中的 hello hello 保護容器的關聯：</span><span class="sxs-lookup"><span data-stu-id="08866-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="08866-209">Hello 工作已完成之後，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="08866-210">Hello 作業已完成處理之後，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="08866-211">toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。</span><span class="sxs-lookup"><span data-stu-id="08866-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="08866-212">步驟 8：設定網路對應</span><span class="sxs-lookup"><span data-stu-id="08866-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="08866-213">開始之前請確認網路對應 hello 來源 VMM 伺服器上的虛擬機器會連接的 tooa VM 網路。</span><span class="sxs-lookup"><span data-stu-id="08866-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="08866-214">此外，請建立一或多個 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="08866-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="08866-215">深入了解如何 toocreate 的虛擬網路中，使用 Azure 資源管理員和 PowerShell，[使用站對站 VPN 連線使用 Azure 資源管理員和 PowerShell 建立虛擬網路](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="08866-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="08866-216">請注意，多個虛擬機器網路可以是對應的 tooa 單一 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="08866-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="08866-217">如果 hello 目標網路有多個子網路，而且其中一個子網路具有 hello 相同的 hello 來源虛擬機器上的子網路的名稱，則 hello 複本虛擬機器將會連接的 toothat 目標子網路容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="08866-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="08866-218">如果不沒有具有相符名稱的任何目標子網路，hello 虛擬機器會連接的 toohello hello 網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="08866-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="08866-219">hello 第一個命令會取得 hello 目前 Azure Site Recovery 保存庫中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="08866-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="08866-220">hello 命令儲存 hello Microsoft Azure Site Recovery 伺服器 hello $Servers 陣列變數中。</span><span class="sxs-lookup"><span data-stu-id="08866-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="08866-221">hello 第二個命令會取得 hello hello 第一部伺服器的站台復原網路 hello $Servers 陣列中。</span><span class="sxs-lookup"><span data-stu-id="08866-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="08866-222">hello 命令儲存 hello 網路 hello $Networks 變數中。</span><span class="sxs-lookup"><span data-stu-id="08866-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="08866-223">hello 第三個命令會取得 Azure 的虛擬網路，然後該值 hello $AzureVmNetworks 變數中。</span><span class="sxs-lookup"><span data-stu-id="08866-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="08866-224">hello 最終 cmdlet 會建立 hello 主要網路與 hello Azure 虛擬機器網路之間的對應。</span><span class="sxs-lookup"><span data-stu-id="08866-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="08866-225">hello 指令程式會指定 hello 主要網路作為 $Networks hello 第一個項目。</span><span class="sxs-lookup"><span data-stu-id="08866-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="08866-226">hello cmdlet 會指定虛擬機器網路為 $AzureVmNetworks hello 第一個項目。</span><span class="sxs-lookup"><span data-stu-id="08866-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="08866-227">步驟 9：對虛擬機器啟用保護</span><span class="sxs-lookup"><span data-stu-id="08866-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="08866-228">Hello 伺服器、 雲端和網路已正確設定之後，您可以啟用 hello 雲端中的虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="08866-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="08866-229">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="08866-229">Note hello following:</span></span>

* <span data-ttu-id="08866-230">虛擬機器必須符合 Azure 需求。</span><span class="sxs-lookup"><span data-stu-id="08866-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="08866-231">這些簽入[必要條件和支援](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)hello 規劃指南中。</span><span class="sxs-lookup"><span data-stu-id="08866-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="08866-232">tooenable 保護、 hello 作業系統以及作業系統磁碟屬性必須設定為 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="08866-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="08866-233">當您在 VMM 使用虛擬機器範本中建立虛擬機器時，您可以設定 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="08866-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="08866-234">您也可以設定這些屬性的現有虛擬機器上 hello**一般**和**硬體組態**hello 虛擬機器內容 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="08866-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="08866-235">如果您不需要在 VMM 中設定這些屬性，您將必須能夠 tooconfigure hello Azure Site Recovery 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="08866-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="08866-236">tooenable 保護，執行下列命令 tooget hello 保護容器 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="08866-237">取得 hello 保護實體 (VM) 執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="08866-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="08866-238">執行下列命令的 hello 啟用 hello DR hello VM:</span><span class="sxs-lookup"><span data-stu-id="08866-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="08866-239">測試您的部署</span><span class="sxs-lookup"><span data-stu-id="08866-239">Test your deployment</span></span>
<span data-ttu-id="08866-240">tootest 部署可以在執行測試容錯移轉單一的虛擬機器，或建立包含多個虛擬機器的復原計劃和執行測試容錯移轉 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="08866-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="08866-241">測試容錯移轉會在隔離的網路中模擬您的容錯移轉與復原機制。</span><span class="sxs-lookup"><span data-stu-id="08866-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="08866-242">請注意：</span><span class="sxs-lookup"><span data-stu-id="08866-242">Note that:</span></span>

* <span data-ttu-id="08866-243">如果您想 tooconnect toohello Azure 虛擬機器中使用遠端桌面 hello 容錯移轉之後，請啟用遠端桌面連線 hello 虛擬機器上執行 hello 測試容錯移轉之前。</span><span class="sxs-lookup"><span data-stu-id="08866-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="08866-244">在容錯移轉之後您將使用遠端桌面在 Azure 中使用公用 IP 位址 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="08866-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="08866-245">如果您希望 toodo 如此，請確定您沒有任何網域原則，讓您無法使用的公用位址的連接 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="08866-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="08866-246">toocheck hello 完成 hello 作業時，請依照下列中的 hello 步驟[監視活動](#monitor)。</span><span class="sxs-lookup"><span data-stu-id="08866-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="08866-247">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="08866-247">Run a test failover</span></span>
- <span data-ttu-id="08866-248">執行下列命令的 hello 啟動 hello 測試容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="08866-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="08866-249">執行計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="08866-249">Run a planned failover</span></span>
- <span data-ttu-id="08866-250">執行下列命令的 hello 啟動 hello 計劃的容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="08866-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="08866-251">執行非計劃性容錯移轉</span><span class="sxs-lookup"><span data-stu-id="08866-251">Run an unplanned failover</span></span>
- <span data-ttu-id="08866-252">開始執行下列命令的 hello hello 規劃的容錯移轉：</span><span class="sxs-lookup"><span data-stu-id="08866-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="08866-253"><a name=monitor></a>監視活動</span><span class="sxs-lookup"><span data-stu-id="08866-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="08866-254">使用下列命令 toomonitor hello 活動 hello。</span><span class="sxs-lookup"><span data-stu-id="08866-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="08866-255">請注意，您 toowait 之間 hello 處理 toofinish 的作業。</span><span class="sxs-lookup"><span data-stu-id="08866-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="08866-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08866-256">Next steps</span></span>
<span data-ttu-id="08866-257">[閱讀更多](/powershell/module/azurerm.recoveryservices.backup/#recovery) 使用 Azure Resource Manager PowerShell Cmdlet 進行 Azure Site Recovery 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="08866-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
