---
title: "使用 Site Recovery 移轉至 Azure | Microsoft Docs"
description: "本文概述如何使用 Azure Site Recovery 將 VM 與實體伺服器移轉至 Azure"
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
ms.openlocfilehash: f4dfe430fba51bd009431ca72279a21be55e3a40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-to-azure-with-site-recovery"></a><span data-ttu-id="ad48e-103">使用 Site Recovery 移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="ad48e-103">Migrate to Azure with Site Recovery</span></span>

<span data-ttu-id="ad48e-104">請閱讀本文，以概略了解如何使用 Azure Site Recovery 服務來移轉虛擬機器和實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="ad48e-104">Read this article for an overview of using the Azure Site Recovery service for migration of virtual machines and physical servers.</span></span>

<span data-ttu-id="ad48e-105">Site Recovery 是一項 Azure 服務，可藉由將內部部署實體伺服器和虛擬機器的複寫協調至雲端 (Azure) 或次要資料中心，協助您的 BCDR 策略。</span><span class="sxs-lookup"><span data-stu-id="ad48e-105">Site Recovery is an Azure service that contributes to your BCDR strategy, by orchestrating replication of on-premises physical servers and virtual machines to the cloud (Azure), or to a secondary datacenter.</span></span> <span data-ttu-id="ad48e-106">當您的主要位置發生故障時，您容錯移轉至次要位置，讓應用程式和工作負載保持可用。</span><span class="sxs-lookup"><span data-stu-id="ad48e-106">When outages occur in your primary location, you fail over to the secondary location to keep apps and workloads available.</span></span> <span data-ttu-id="ad48e-107">當它恢復正常作業時，容錯回復至您的主要位置。</span><span class="sxs-lookup"><span data-stu-id="ad48e-107">You fail back to your primary location when it returns to normal operations.</span></span> <span data-ttu-id="ad48e-108">深入了解 [什麼是 Site Recovery？](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="ad48e-108">Learn more in [What is Site Recovery?](site-recovery-overview.md)</span></span> <span data-ttu-id="ad48e-109">您也可以使用 Site Recovery，將現有的內部部署工作負載移轉至 Azure，以加速您的雲端旅程，並使用 Azure 提供的功能陣列。</span><span class="sxs-lookup"><span data-stu-id="ad48e-109">You can also use Site Recovery to migrate your existing on-premises workloads to Azure to expedite your cloud journey and avail the array of features that Azure offers.</span></span>

<span data-ttu-id="ad48e-110">如需如何執行移轉的快速概觀，請觀看這段影片。</span><span class="sxs-lookup"><span data-stu-id="ad48e-110">For a quick overview of how to perform migration, please refer to this video.</span></span>
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

<span data-ttu-id="ad48e-111">本文說明 [Azure 入口網站](https://portal.azure.com)中的部署作業。</span><span class="sxs-lookup"><span data-stu-id="ad48e-111">This article describes deployment in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad48e-112">[Azure 傳統入口網站](https://manage.windowsazure.com/)可用來維護現有的 Site Recovery 保存庫，但無法建立新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="ad48e-112">The [Azure classic portal](https://manage.windowsazure.com/) can be used to maintain existing Site Recovery vaults, but you can't create new vaults.</span></span>

<span data-ttu-id="ad48e-113">若有任何意見，請張貼於文末。</span><span class="sxs-lookup"><span data-stu-id="ad48e-113">Post any comments at the bottom of this article.</span></span> <span data-ttu-id="ad48e-114">請在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="ad48e-114">Ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="what-do-we-mean-by-migration"></a><span data-ttu-id="ad48e-115">移轉的意思為何？</span><span class="sxs-lookup"><span data-stu-id="ad48e-115">What do we mean by migration?</span></span>

<span data-ttu-id="ad48e-116">您可以將用來複寫內部部署 VM 和實體伺服器的 Site Recovery 部署至 Azure 或次要站台。</span><span class="sxs-lookup"><span data-stu-id="ad48e-116">You can deploy Site Recovery for replication of on-premises VMs and physical servers, to Azure or to a secondary site.</span></span> <span data-ttu-id="ad48e-117">您會複寫機器、發生中斷時從主要站台容錯移轉它們，然後在主要站台復原時將它們容錯移轉回到該站台。</span><span class="sxs-lookup"><span data-stu-id="ad48e-117">You replicate machines, fail them over from the primary site when outages occur, and fail them back to the primary site when it recovers.</span></span> <span data-ttu-id="ad48e-118">除此之外，您還可以使用 Site Recovery 將 VM 和實體伺服器移轉到 Azure，讓使用者可以存取它們做為 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="ad48e-118">In addition to this, you can use Site Recovery to migrate VMs and physical servers to Azure, so that users can access them as Azure VMs.</span></span> <span data-ttu-id="ad48e-119">移轉作業需要進行複寫、從主要站台容錯移轉至 Azure，以及完整的移轉軌跡。</span><span class="sxs-lookup"><span data-stu-id="ad48e-119">Migration entails replication, and failover from the primary site to Azure, and a complete migration gesture.</span></span>

## <a name="what-can-site-recovery-migrate"></a><span data-ttu-id="ad48e-120">Site Recovery 可以移轉什麼項目？</span><span class="sxs-lookup"><span data-stu-id="ad48e-120">What can Site Recovery migrate?</span></span>

<span data-ttu-id="ad48e-121">您可以：</span><span class="sxs-lookup"><span data-stu-id="ad48e-121">You can:</span></span>

- <span data-ttu-id="ad48e-122">將在內部部署 Hyper-V VM、VMware VM 和實體伺服器上執行的工作負載，移轉到 Azure VM 上來執行。</span><span class="sxs-lookup"><span data-stu-id="ad48e-122">Migrate workloads running on on-premises Hyper-V VMs, VMware VMs, and physical servers, to run on Azure VMs.</span></span> <span data-ttu-id="ad48e-123">在此案例中，您也可以執行完整的複寫和容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ad48e-123">You can also do full replication and failback in this scenario.</span></span>
- <span data-ttu-id="ad48e-124">在 Azure 區域之間移轉 [Azure IaaS VM](site-recovery-migrate-azure-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="ad48e-124">Migrate [Azure IaaS VMs](site-recovery-migrate-azure-to-azure.md) between Azure regions.</span></span> <span data-ttu-id="ad48e-125">此案例目前只支援移轉，亦即不支援容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ad48e-125">Currently only migration is supported in this scenario, which means failback isn't supported.</span></span>
- <span data-ttu-id="ad48e-126">將 [AWS Windows 執行個體](site-recovery-migrate-aws-to-azure.md)移轉到 Azure IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="ad48e-126">Migrate [AWS Windows instances](site-recovery-migrate-aws-to-azure.md) to Azure IaaS VMs.</span></span> <span data-ttu-id="ad48e-127">此案例目前只支援移轉，亦即不支援容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ad48e-127">Currently only migration is supported in this scenario, which means failback isn't supported.</span></span>

## <a name="migrate-on-premises-vms-and-physical-servers"></a><span data-ttu-id="ad48e-128">移轉內部部署 VM 和實體伺服器</span><span class="sxs-lookup"><span data-stu-id="ad48e-128">Migrate on-premises VMs and physical servers</span></span>

<span data-ttu-id="ad48e-129">若要移轉內部部署 Hyper-V VM、VMware VM 和實體伺服器，您所需遵循的步驟幾乎和一般複寫時所使用的步驟相同。</span><span class="sxs-lookup"><span data-stu-id="ad48e-129">To migrate on-premises Hyper-V VMs, VMware VMs, and physical servers, you follow almost the same steps as those used for regular replication.</span></span>

1. <span data-ttu-id="ad48e-130">設定復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="ad48e-130">Set up a Recovery Services vault</span></span>
2. <span data-ttu-id="ad48e-131">設定所需的管理伺服器 (VMware、VMM、Hyper-V - 視您要移轉的項目而定)、將它們新增至保存庫，並指定複寫設定。</span><span class="sxs-lookup"><span data-stu-id="ad48e-131">Configure the required management servers (VMware, VMM, Hyper-V - depending on what you want to migrate), add them to the vault, and specify replication settings.</span></span>
3. <span data-ttu-id="ad48e-132">針對您想要移轉的電腦啟用複寫</span><span class="sxs-lookup"><span data-stu-id="ad48e-132">Enable replication for the machines you want to migrate</span></span>
4. <span data-ttu-id="ad48e-133">在初始移轉之後，執行快速的測試容錯移轉，以確保一切運作正常。</span><span class="sxs-lookup"><span data-stu-id="ad48e-133">After the initial migration, run a quick test failover to ensure that everything's working as it should.</span></span>
5. <span data-ttu-id="ad48e-134">確認複寫環境有用之後，您需要根據您的案例[所支援的項目](site-recovery-failover.md)使用計劃性或非計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-134">After you verify that your replication environment is working, you use a planned or unplanned failover depending on [what's supported](site-recovery-failover.md) for your scenario.</span></span> <span data-ttu-id="ad48e-135">我們建議您儘可能使用規劃的容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-135">We recommend you use a planned failover when possible.</span></span>
6. <span data-ttu-id="ad48e-136">若要進行移轉，您不需要認可容錯移轉或刪除它。</span><span class="sxs-lookup"><span data-stu-id="ad48e-136">For migration, you don't need to commit a failover, or delete it.</span></span> <span data-ttu-id="ad48e-137">相反地，您要為所要移轉的每一部機器選取**完成移轉**選項。</span><span class="sxs-lookup"><span data-stu-id="ad48e-137">Instead, you select the **Complete Migration** option for each machine you want to migrate.</span></span>
     - <span data-ttu-id="ad48e-138">在 [複寫的項目] 中，以滑鼠右鍵按一下 VM，然後按一下 [完成移轉]。</span><span class="sxs-lookup"><span data-stu-id="ad48e-138">In **Replicated Items**, right-click the VM, and click **Complete Migration**.</span></span> <span data-ttu-id="ad48e-139">按一下 [確定] 以完成。</span><span class="sxs-lookup"><span data-stu-id="ad48e-139">Click **OK** to complete.</span></span> <span data-ttu-id="ad48e-140">您可以在 [Site Recovery 作業] 中監視 [完成移轉] 作業，以在 VM 屬性中追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="ad48e-140">You can track progress in the VM properties, in by monitoring the Complete Migration job in **Site Recovery jobs**.</span></span>
     - <span data-ttu-id="ad48e-141">**完成移轉**動作會完成移轉程序、移除機器的複寫，並停止該機器的 Site Recovery 計費。</span><span class="sxs-lookup"><span data-stu-id="ad48e-141">The **Complete Migration** action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

![完成移轉](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a><span data-ttu-id="ad48e-143">在不同的 Azure 地區之間移轉</span><span class="sxs-lookup"><span data-stu-id="ad48e-143">Migrate between Azure regions</span></span>

<span data-ttu-id="ad48e-144">您可以使用 Site Recovery 在區域之間移轉 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="ad48e-144">You can migrate Azure VMs between regions using Site Recovery.</span></span> <span data-ttu-id="ad48e-145">此案例只支援移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-145">In this scenario only migration is supported.</span></span> <span data-ttu-id="ad48e-146">換句話說，您可以複寫 Azure VM，並將它們容錯移轉至另一個區域，但您無法容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ad48e-146">In other words, you can replicate the Azure VMs and fail them over to another region, but you can't fail back.</span></span> <span data-ttu-id="ad48e-147">在此案例中，您要設定復原服務保存庫、部署用來管理複寫的內部部署組態伺服器、將它新增至保存庫，以及指定複寫設定。</span><span class="sxs-lookup"><span data-stu-id="ad48e-147">In this scenario you set up a Recovery Services vault, deploy an on-premises configuration server to manage replication, add it to the vault, and specify replication settings.</span></span> <span data-ttu-id="ad48e-148">為您想要移轉的機器啟用複寫，並執行快速的測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-148">You enable replication for the machines you want to migrate, and run a quick test failover.</span></span> <span data-ttu-id="ad48e-149">然後使用**完成移轉**選項執行非計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-149">Then you run an unplanned failover with the **Complete Migration** option.</span></span>

## <a name="migrate-aws-to-azure"></a><span data-ttu-id="ad48e-150">將 AWS 移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="ad48e-150">Migrate AWS to Azure</span></span>

<span data-ttu-id="ad48e-151">您可以將 AWS 執行個體移轉至 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="ad48e-151">You can migrate AWS instances to Azure VMs.</span></span> <span data-ttu-id="ad48e-152">此案例只支援移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-152">In this scenario only migration is supported.</span></span> <span data-ttu-id="ad48e-153">換句話說，您可以複寫 AWS 執行個體，並將它們容錯移轉至 Azure，但您無法容錯回復。</span><span class="sxs-lookup"><span data-stu-id="ad48e-153">In other words, you can replicate the AWS instances and fail them over to Azure, but you can't fail back.</span></span> <span data-ttu-id="ad48e-154">在進行移轉時，AWS 執行個體的處理方式和實體伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="ad48e-154">AWS instances are handled in the same way as physical servers for migration purposes.</span></span> <span data-ttu-id="ad48e-155">您要設定復原服務保存庫、部署用來管理複寫的內部部署組態伺服器、將它新增至保存庫，以及指定複寫設定。</span><span class="sxs-lookup"><span data-stu-id="ad48e-155">You set up a Recovery Services vault, deploy an on-premises configuration server to manage replication, add it to the vault, and specify replication settings.</span></span> <span data-ttu-id="ad48e-156">為您想要移轉的機器啟用複寫，並執行快速的測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-156">You enable replication for the machines you want to migrate, and run a quick test failover.</span></span> <span data-ttu-id="ad48e-157">然後使用**完成移轉**選項執行非計劃性容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="ad48e-157">Then you run an unplanned failover with the **Complete Migration** option.</span></span>




## <a name="next-steps"></a><span data-ttu-id="ad48e-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ad48e-158">Next steps</span></span>

- [<span data-ttu-id="ad48e-159">將 VMware VM 移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="ad48e-159">Migrate VMware VMs to Azure</span></span>](site-recovery-vmware-to-azure.md)
- [<span data-ttu-id="ad48e-160">將 VMM 雲端中的 Hyper-V VM 移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="ad48e-160">Migrate Hyper-V VMs in VMM clouds to Azure</span></span>](site-recovery-vmm-to-azure.md)
- [<span data-ttu-id="ad48e-161">將沒有 VMM 的 Hyper-V VM 移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="ad48e-161">Migrate Hyper-V VMs without VMM to Azure</span></span>](site-recovery-hyper-v-site-to-azure.md)
- [<span data-ttu-id="ad48e-162">在 Azure 區域之間移轉 Azure VM</span><span class="sxs-lookup"><span data-stu-id="ad48e-162">Migrate Azure VMs between Azure regions</span></span>](site-recovery-migrate-azure-to-azure.md)
- [<span data-ttu-id="ad48e-163">將 AWS 執行個體移轉至 Azure</span><span class="sxs-lookup"><span data-stu-id="ad48e-163">Migrate AWS instances to Azure</span></span>](site-recovery-migrate-aws-to-azure.md)
- <span data-ttu-id="ad48e-164">[準備已移轉的機器，以便複寫](site-recovery-azure-to-azure-after-migration.md)至其他區域以因應災害復原的需要。</span><span class="sxs-lookup"><span data-stu-id="ad48e-164">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="ad48e-165">[複寫 Azure 虛擬機器](site-recovery-azure-to-azure.md)來開始保護您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="ad48e-165">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
