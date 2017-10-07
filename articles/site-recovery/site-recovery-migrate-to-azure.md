---
title: "使用站台復原 aaaMigrate tooAzure |Microsoft 文件"
description: "本文提供移轉的 Vm 和 Azure Site recovery 的實體伺服器 tooAzure 的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a><span data-ttu-id="c638c-103">移轉與 Site Recovery tooAzure</span><span class="sxs-lookup"><span data-stu-id="c638c-103">Migrate tooAzure with Site Recovery</span></span>

<span data-ttu-id="c638c-104">閱讀本文如需使用 移轉虛擬機器和實體伺服器 hello Azure Site Recovery 服務。</span><span class="sxs-lookup"><span data-stu-id="c638c-104">Read this article for an overview of using hello Azure Site Recovery service for migration of virtual machines and physical servers.</span></span>

<span data-ttu-id="c638c-105">站台復原是達成 tooyour BCDR 策略，來協調複寫在內部部署實體伺服器和虛擬機器 toohello 雲端 (Azure)，或 tooa 次要資料中心的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="c638c-105">Site Recovery is an Azure service that contributes tooyour BCDR strategy, by orchestrating replication of on-premises physical servers and virtual machines toohello cloud (Azure), or tooa secondary datacenter.</span></span> <span data-ttu-id="c638c-106">當您的主要位置發生中斷時，您容錯移轉 toohello 次要位置 tookeep 應用程式和可用的工作負載。</span><span class="sxs-lookup"><span data-stu-id="c638c-106">When outages occur in your primary location, you fail over toohello secondary location tookeep apps and workloads available.</span></span> <span data-ttu-id="c638c-107">當它傳回 toonormal 作業，您就會容錯回復 tooyour 主要位置。</span><span class="sxs-lookup"><span data-stu-id="c638c-107">You fail back tooyour primary location when it returns toonormal operations.</span></span> <span data-ttu-id="c638c-108">深入了解 [什麼是 Site Recovery？](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c638c-108">Learn more in [What is Site Recovery?](site-recovery-overview.md)</span></span> <span data-ttu-id="c638c-109">您也可以使用站台復原 toomigrate 您現有的內部工作負載 tooAzure tooexpedite 您的雲端之旅和可用性 hello Azure 提供的功能的陣列。</span><span class="sxs-lookup"><span data-stu-id="c638c-109">You can also use Site Recovery toomigrate your existing on-premises workloads tooAzure tooexpedite your cloud journey and avail hello array of features that Azure offers.</span></span>

<span data-ttu-id="c638c-110">如需快速概觀 tooperform 移轉 toothis 視訊，請參閱。</span><span class="sxs-lookup"><span data-stu-id="c638c-110">For a quick overview of how tooperform migration, please refer toothis video.</span></span>
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

<span data-ttu-id="c638c-111">本文說明部署中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c638c-111">This article describes deployment in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c638c-112">hello [Azure 傳統入口網站](https://manage.windowsazure.com/)可以使用的 toomaintain 現有站台復原保存庫，但您無法建立新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="c638c-112">hello [Azure classic portal](https://manage.windowsazure.com/) can be used toomaintain existing Site Recovery vaults, but you can't create new vaults.</span></span>

<span data-ttu-id="c638c-113">張貼在 hello 這篇文章底部的任何註解。</span><span class="sxs-lookup"><span data-stu-id="c638c-113">Post any comments at hello bottom of this article.</span></span> <span data-ttu-id="c638c-114">在 hello 詢問技術問題[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="c638c-114">Ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="what-do-we-mean-by-migration"></a><span data-ttu-id="c638c-115">移轉的意思為何？</span><span class="sxs-lookup"><span data-stu-id="c638c-115">What do we mean by migration?</span></span>

<span data-ttu-id="c638c-116">您可以部署站台復原的複寫在內部部署 Vm 和實體伺服器、 tooAzure 或 tooa 次要站台。</span><span class="sxs-lookup"><span data-stu-id="c638c-116">You can deploy Site Recovery for replication of on-premises VMs and physical servers, tooAzure or tooa secondary site.</span></span> <span data-ttu-id="c638c-117">複寫機器，它們從容錯移轉 hello 主要站台的中斷發生的而且它會復原完成時將它們容錯回復 toohello 主要站台。</span><span class="sxs-lookup"><span data-stu-id="c638c-117">You replicate machines, fail them over from hello primary site when outages occur, and fail them back toohello primary site when it recovers.</span></span> <span data-ttu-id="c638c-118">在加法 toothis，您可以使用站台復原 toomigrate Vm 和實體伺服器 tooAzure，讓使用者可以存取它們做為 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="c638c-118">In addition toothis, you can use Site Recovery toomigrate VMs and physical servers tooAzure, so that users can access them as Azure VMs.</span></span> <span data-ttu-id="c638c-119">移轉需要複寫和容錯移轉從 hello 主要站台 tooAzure 和完成移轉筆勢。</span><span class="sxs-lookup"><span data-stu-id="c638c-119">Migration entails replication, and failover from hello primary site tooAzure, and a complete migration gesture.</span></span>

## <a name="what-can-site-recovery-migrate"></a><span data-ttu-id="c638c-120">Site Recovery 可以移轉什麼項目？</span><span class="sxs-lookup"><span data-stu-id="c638c-120">What can Site Recovery migrate?</span></span>

<span data-ttu-id="c638c-121">您可以：</span><span class="sxs-lookup"><span data-stu-id="c638c-121">You can:</span></span>

- <span data-ttu-id="c638c-122">將 Azure Vm 上的內部部署 HYPER-V Vm、 VMware Vm 與實體伺服器、 toorun 上執行的工作負載的移轉。</span><span class="sxs-lookup"><span data-stu-id="c638c-122">Migrate workloads running on on-premises Hyper-V VMs, VMware VMs, and physical servers, toorun on Azure VMs.</span></span> <span data-ttu-id="c638c-123">在此案例中，您也可以執行完整的複寫和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="c638c-123">You can also do full replication and failback in this scenario.</span></span>
- <span data-ttu-id="c638c-124">在 Azure 區域之間移轉 [Azure IaaS VM](site-recovery-migrate-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="c638c-124">Migrate [Azure IaaS VMs](site-recovery-migrate-azure-to-azure.md) between Azure regions.</span></span> <span data-ttu-id="c638c-125">此案例目前只支援移轉，亦即不支援容錯回復。</span><span class="sxs-lookup"><span data-stu-id="c638c-125">Currently only migration is supported in this scenario, which means failback isn't supported.</span></span>
- <span data-ttu-id="c638c-126">移轉[AWS Windows 執行個體](site-recovery-migrate-aws-to-azure.md)tooAzure IaaS Vm。</span><span class="sxs-lookup"><span data-stu-id="c638c-126">Migrate [AWS Windows instances](site-recovery-migrate-aws-to-azure.md) tooAzure IaaS VMs.</span></span> <span data-ttu-id="c638c-127">此案例目前只支援移轉，亦即不支援容錯回復。</span><span class="sxs-lookup"><span data-stu-id="c638c-127">Currently only migration is supported in this scenario, which means failback isn't supported.</span></span>

## <a name="migrate-on-premises-vms-and-physical-servers"></a><span data-ttu-id="c638c-128">移轉內部部署 VM 和實體伺服器</span><span class="sxs-lookup"><span data-stu-id="c638c-128">Migrate on-premises VMs and physical servers</span></span>

<span data-ttu-id="c638c-129">toomigrate 內部部署 HYPER-V Vm、 VMware Vm 和實體伺服器，您可以遵循幾乎相同步驟所使用的一般複寫的 hello。</span><span class="sxs-lookup"><span data-stu-id="c638c-129">toomigrate on-premises Hyper-V VMs, VMware VMs, and physical servers, you follow almost hello same steps as those used for regular replication.</span></span>

1. <span data-ttu-id="c638c-130">設定復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="c638c-130">Set up a Recovery Services vault</span></span>
2. <span data-ttu-id="c638c-131">設定所需的 hello 管理伺服器 (VMware，VMM 中，HYPER-V-取決於您想要 toomigrate)、 將它們加入 toohello 保存庫，並指定複寫設定。</span><span class="sxs-lookup"><span data-stu-id="c638c-131">Configure hello required management servers (VMware, VMM, Hyper-V - depending on what you want toomigrate), add them toohello vault, and specify replication settings.</span></span>
3. <span data-ttu-id="c638c-132">啟用複寫，對 hello 機器想 toomigrate</span><span class="sxs-lookup"><span data-stu-id="c638c-132">Enable replication for hello machines you want toomigrate</span></span>
4. <span data-ttu-id="c638c-133">Hello 初始移轉之後，執行一切正常地快速測試容錯移轉 tooensure。</span><span class="sxs-lookup"><span data-stu-id="c638c-133">After hello initial migration, run a quick test failover tooensure that everything's working as it should.</span></span>
5. <span data-ttu-id="c638c-134">確認複寫環境有用之後，您需要根據您的案例[所支援的項目](site-recovery-failover.md)使用計劃性或非計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c638c-134">After you verify that your replication environment is working, you use a planned or unplanned failover depending on [what's supported](site-recovery-failover.md) for your scenario.</span></span> <span data-ttu-id="c638c-135">我們建議您儘可能使用規劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c638c-135">We recommend you use a planned failover when possible.</span></span>
6. <span data-ttu-id="c638c-136">如需移轉，您不需要 toocommit 容錯移轉時，或刪除它。</span><span class="sxs-lookup"><span data-stu-id="c638c-136">For migration, you don't need toocommit a failover, or delete it.</span></span> <span data-ttu-id="c638c-137">相反地，您可以選取 hello**完成移轉**選項要為每一部機器 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="c638c-137">Instead, you select hello **Complete Migration** option for each machine you want toomigrate.</span></span>
     - <span data-ttu-id="c638c-138">在**複寫的項目**，以滑鼠右鍵按一下 hello VM，然後按一下**完成移轉**。</span><span class="sxs-lookup"><span data-stu-id="c638c-138">In **Replicated Items**, right-click hello VM, and click **Complete Migration**.</span></span> <span data-ttu-id="c638c-139">按一下**確定**toocomplete。</span><span class="sxs-lookup"><span data-stu-id="c638c-139">Click **OK** toocomplete.</span></span> <span data-ttu-id="c638c-140">您也可以監視中的 hello 完成移轉作業中追蹤在 hello VM 屬性中，進度**站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="c638c-140">You can track progress in hello VM properties, in by monitoring hello Complete Migration job in **Site Recovery jobs**.</span></span>
     - <span data-ttu-id="c638c-141">hello**完成移轉**動作完成 hello 移轉程序、 移除 hello 機器的複寫和停止 hello 機器的 Site Recovery 計費。</span><span class="sxs-lookup"><span data-stu-id="c638c-141">hello **Complete Migration** action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

![完成移轉](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a><span data-ttu-id="c638c-143">在不同的 Azure 地區之間移轉</span><span class="sxs-lookup"><span data-stu-id="c638c-143">Migrate between Azure regions</span></span>

<span data-ttu-id="c638c-144">您可以使用 Site Recovery 在區域之間移轉 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c638c-144">You can migrate Azure VMs between regions using Site Recovery.</span></span> <span data-ttu-id="c638c-145">此案例只支援移轉。</span><span class="sxs-lookup"><span data-stu-id="c638c-145">In this scenario only migration is supported.</span></span> <span data-ttu-id="c638c-146">換句話說，您可以複寫 hello Azure Vm，並容錯 tooanother 區域，但您無法進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="c638c-146">In other words, you can replicate hello Azure VMs and fail them over tooanother region, but you can't fail back.</span></span> <span data-ttu-id="c638c-147">在此案例中，您將設定復原服務保存庫，部署在內部部署組態伺服器 toomanage 複寫，將它加入 toohello 保存庫，並指定複寫設定。</span><span class="sxs-lookup"><span data-stu-id="c638c-147">In this scenario you set up a Recovery Services vault, deploy an on-premises configuration server toomanage replication, add it toohello vault, and specify replication settings.</span></span> <span data-ttu-id="c638c-148">針對您想 toomigrate，而且執行快速的 hello 機器測試容錯移轉，您可以啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="c638c-148">You enable replication for hello machines you want toomigrate, and run a quick test failover.</span></span> <span data-ttu-id="c638c-149">然後您可以執行規劃的容錯移轉以 hello**完成移轉**選項。</span><span class="sxs-lookup"><span data-stu-id="c638c-149">Then you run an unplanned failover with hello **Complete Migration** option.</span></span>

## <a name="migrate-aws-tooazure"></a><span data-ttu-id="c638c-150">移轉 AWS tooAzure</span><span class="sxs-lookup"><span data-stu-id="c638c-150">Migrate AWS tooAzure</span></span>

<span data-ttu-id="c638c-151">您可以移轉 AWS 執行個體 tooAzure Vm。</span><span class="sxs-lookup"><span data-stu-id="c638c-151">You can migrate AWS instances tooAzure VMs.</span></span> <span data-ttu-id="c638c-152">此案例只支援移轉。</span><span class="sxs-lookup"><span data-stu-id="c638c-152">In this scenario only migration is supported.</span></span> <span data-ttu-id="c638c-153">換句話說，您可以將複寫 hello AWS 執行個體，並容錯 tooAzure，但您無法進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="c638c-153">In other words, you can replicate hello AWS instances and fail them over tooAzure, but you can't fail back.</span></span> <span data-ttu-id="c638c-154">AWS 執行個體以處理 hello 相同實體伺服器進行移轉的方式。</span><span class="sxs-lookup"><span data-stu-id="c638c-154">AWS instances are handled in hello same way as physical servers for migration purposes.</span></span> <span data-ttu-id="c638c-155">您設定 復原服務保存庫、 部署在內部部署組態伺服器 toomanage 複寫、 將它加入 toohello 保存庫，和指定的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="c638c-155">You set up a Recovery Services vault, deploy an on-premises configuration server toomanage replication, add it toohello vault, and specify replication settings.</span></span> <span data-ttu-id="c638c-156">針對您想 toomigrate，而且執行快速的 hello 機器測試容錯移轉，您可以啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="c638c-156">You enable replication for hello machines you want toomigrate, and run a quick test failover.</span></span> <span data-ttu-id="c638c-157">然後您可以執行規劃的容錯移轉以 hello**完成移轉**選項。</span><span class="sxs-lookup"><span data-stu-id="c638c-157">Then you run an unplanned failover with hello **Complete Migration** option.</span></span>




## <a name="next-steps"></a><span data-ttu-id="c638c-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c638c-158">Next steps</span></span>

- [<span data-ttu-id="c638c-159">移轉 VMware Vm tooAzure</span><span class="sxs-lookup"><span data-stu-id="c638c-159">Migrate VMware VMs tooAzure</span></span>](site-recovery-vmware-to-azure.md)
- [<span data-ttu-id="c638c-160">在 VMM 雲端 tooAzure 移轉 HYPER-V Vm</span><span class="sxs-lookup"><span data-stu-id="c638c-160">Migrate Hyper-V VMs in VMM clouds tooAzure</span></span>](site-recovery-vmm-to-azure.md)
- [<span data-ttu-id="c638c-161">移轉 HYPER-V Vm 沒有 VMM tooAzure</span><span class="sxs-lookup"><span data-stu-id="c638c-161">Migrate Hyper-V VMs without VMM tooAzure</span></span>](site-recovery-hyper-v-site-to-azure.md)
- [<span data-ttu-id="c638c-162">在 Azure 區域之間移轉 Azure VM</span><span class="sxs-lookup"><span data-stu-id="c638c-162">Migrate Azure VMs between Azure regions</span></span>](site-recovery-migrate-azure-to-azure.md)
- [<span data-ttu-id="c638c-163">移轉 AWS 執行個體 tooAzure</span><span class="sxs-lookup"><span data-stu-id="c638c-163">Migrate AWS instances tooAzure</span></span>](site-recovery-migrate-aws-to-azure.md)
- <span data-ttu-id="c638c-164">[準備移轉的機器 tooenable 複寫](site-recovery-azure-to-azure-after-migration.md)tooanother 嚴重損壞修復所需的區域。</span><span class="sxs-lookup"><span data-stu-id="c638c-164">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="c638c-165">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="c638c-165">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
