---
title: "移除伺服器與停用保護 | Microsoft Docs"
description: "本文說明如何取消註冊 Site Recovery 保存庫中的伺服器，並停用虛擬機器和實體伺服器的保護。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="c7ead-103">移除伺服器並停用保護</span><span class="sxs-lookup"><span data-stu-id="c7ead-103">Remove servers and disable protection</span></span>

<span data-ttu-id="c7ead-104">Azure Site Recovery 是一項有助於建立商務持續性和災害復原 (BCDR) 策略的服務。</span><span class="sxs-lookup"><span data-stu-id="c7ead-104">The Azure Site Recovery service contributes to your business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="c7ead-105">該服務可協調虛擬機器和實體伺服器的複寫、容錯移轉和復原。</span><span class="sxs-lookup"><span data-stu-id="c7ead-105">The service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="c7ead-106">機器可以複寫至 Azure，或次要的內部部署資料中心。</span><span class="sxs-lookup"><span data-stu-id="c7ead-106">Machines can be replicated to Azure, or to a secondary on-premises data center.</span></span> <span data-ttu-id="c7ead-107">如需快速概觀，請參閱 [什麼是 Azure Site Recovery？](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c7ead-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="c7ead-108">本文說明如何在 Azure 入口網站中，將「復原服務」保存庫中的伺服器取消註冊，以及如何針對由 Site Recovery 保護的機器停用保護。</span><span class="sxs-lookup"><span data-stu-id="c7ead-108">This article describes how to unregister servers from a Recovery Services vault in the Azure portal, and how to disable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="c7ead-109">在這篇文章下方或 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="c7ead-109">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="c7ead-110">將已連線的組態伺服器取消註冊</span><span class="sxs-lookup"><span data-stu-id="c7ead-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="c7ead-111">如果您將 VMware VM 或 Windows/Linux 實體伺服器複寫到 Azure，您可以將已連線的組態伺服器從保存庫取消註冊，方法如下：</span><span class="sxs-lookup"><span data-stu-id="c7ead-111">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="c7ead-112">停用機器保護。</span><span class="sxs-lookup"><span data-stu-id="c7ead-112">Disable machine protection.</span></span> <span data-ttu-id="c7ead-113">在 [受保護的項目] > [已複寫的項目] 中，以滑鼠右鍵按一下機器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-113">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="c7ead-114">取消關聯任何原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-114">Disassociate any policies.</span></span> <span data-ttu-id="c7ead-115">在 [Site Recovery 基礎結構] > [適用於 VMWare 與實體機器] > [複寫原則] 中，按兩下相關聯的原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="c7ead-116">以滑鼠右鍵按一下組態伺服器 > [取消關聯]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-116">Right-click the configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="c7ead-117">移除任何額外的內部部署處理伺服器或主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="c7ead-118">在 [Site Recovery 基礎結構] > [適用於 VMWare 與 Physical 機器] > [組態伺服器] 中，以滑鼠右鍵按一下伺服器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="c7ead-119">刪除組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-119">Delete the configuration server.</span></span>
5. <span data-ttu-id="c7ead-120">將在主要目標伺服器 (個別的伺服器，或在組態伺服器上執行的伺服器) 上執行的行動服務手動解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-120">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
6. <span data-ttu-id="c7ead-121">將任何額外的處理伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="c7ead-122">將組態伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-122">Uninstall the configuration server.</span></span>
8. <span data-ttu-id="c7ead-123">在組態伺服器上，將 Site Recovery 安裝的 MySQL 執行個體解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-123">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="c7ead-124">在組態伺服器的登錄中，刪除金鑰 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``。</span><span class="sxs-lookup"><span data-stu-id="c7ead-124">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="c7ead-125">將未連線的組態伺服器取消註冊</span><span class="sxs-lookup"><span data-stu-id="c7ead-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="c7ead-126">如果您將 VMware VM 或 Windows/Linux 實體伺服器複寫到 Azure，您可以將未連線的組態伺服器從保存庫取消註冊，方法如下：</span><span class="sxs-lookup"><span data-stu-id="c7ead-126">If you replicate VMware VMs or Windows/Linux physical servers to Azure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="c7ead-127">停用機器保護。</span><span class="sxs-lookup"><span data-stu-id="c7ead-127">Disable machine protection.</span></span> <span data-ttu-id="c7ead-128">在 [受保護的項目] > [已複寫的項目] 中，以滑鼠右鍵按一下機器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-128">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span> <span data-ttu-id="c7ead-129">選取 [停止管理機器]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-129">Select **Stop managing the machine**.</span></span>
2. <span data-ttu-id="c7ead-130">移除任何額外的內部部署處理伺服器或主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="c7ead-131">在 [Site Recovery 基礎結構] > [適用於 VMWare 與 Physical 機器] > [組態伺服器] 中，以滑鼠右鍵按一下伺服器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click the server > **Delete**.</span></span>
3. <span data-ttu-id="c7ead-132">刪除組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-132">Delete the configuration server.</span></span>
4. <span data-ttu-id="c7ead-133">將在主要目標伺服器 (個別的伺服器，或在組態伺服器上執行的伺服器) 上執行的行動服務手動解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-133">Manually uninstall the Mobility service running on the master target server (this will be either a separate server, or running on the configuration server).</span></span>
5. <span data-ttu-id="c7ead-134">將任何額外的處理伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="c7ead-135">將組態伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-135">Uninstall the configuration server.</span></span>
7. <span data-ttu-id="c7ead-136">在組態伺服器上，將 Site Recovery 安裝的 MySQL 執行個體解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-136">On the configuration server, uninstall the instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="c7ead-137">在組態伺服器的登錄中，刪除金鑰 ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``。</span><span class="sxs-lookup"><span data-stu-id="c7ead-137">In the registry of the configuration server delete the key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="c7ead-138">取消註冊已連線的 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="c7ead-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="c7ead-139">根據最佳做法，建議您在連線到 Azure 時，取消註冊 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-139">As a best practice, we recommend that you unregister the VMM server when it's connected to Azure.</span></span> <span data-ttu-id="c7ead-140">這麼做可以確保適當地清除 VMM 伺服器 (以及其他已和雲端配對的 VMM 伺服器) 上的設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-140">This ensures that settings on the VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="c7ead-141">您只應在連線發生永久性問題時，才移除未連線的伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="c7ead-142">如果 VMM 伺服器未連線，您將需要手動執行指令碼來清除設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-142">If the VMM server isn’t connected, you will need to manually run a script to clean up settings.</span></span>

1. <span data-ttu-id="c7ead-143">在您想要移除的 VMM 伺服器上，停止在雲端複寫 VM。</span><span class="sxs-lookup"><span data-stu-id="c7ead-143">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="c7ead-144">在您想要刪除的 VMM 伺服器上，刪除任何由雲端使用的網路對應。</span><span class="sxs-lookup"><span data-stu-id="c7ead-144">Delete any network mappings used by clouds on the VMM server you want to delete.</span></span> <span data-ttu-id="c7ead-145">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] > [網路對應] 中，以滑鼠右鍵按一下網路對應 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="c7ead-146">將您想要移除的 VMM 伺服器上取消雲端和複寫原則的關聯。</span><span class="sxs-lookup"><span data-stu-id="c7ead-146">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="c7ead-147">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] >  [複寫原則] 中，按兩下相關聯的原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="c7ead-148">以滑鼠右鍵按一下雲端 > [取消關聯]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-148">Right-click the cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="c7ead-149">刪除 VMM 伺服器或作用中的 VMM 節點。</span><span class="sxs-lookup"><span data-stu-id="c7ead-149">Delete the VMM server or active VMM node.</span></span> <span data-ttu-id="c7ead-150">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] > [VMM 伺服器] 中，以滑鼠右鍵按一下伺服器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
5. <span data-ttu-id="c7ead-151">在 VMM 伺服器上手動將提供者解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-151">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="c7ead-152">如果您有叢集，請將它從所有節點中移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="c7ead-153">如果您是複寫到 Azure，請將 Microsoft 復原服務代理程式從已刪除之雲端中的 Hyper-V 主機上手動移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-153">If you're replicating to Azure, manually remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="c7ead-154">取消註冊未連線的 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="c7ead-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="c7ead-155">在您想要移除的 VMM 伺服器上，停止在雲端複寫 VM。</span><span class="sxs-lookup"><span data-stu-id="c7ead-155">Stop replicating VMs in clouds on the VMM server you want to remove.</span></span>
2. <span data-ttu-id="c7ead-156">在您想要刪除的 VMM 伺服器上，刪除任何由雲端使用的網路對應。</span><span class="sxs-lookup"><span data-stu-id="c7ead-156">Delete any network mappings used by clouds on the VMM server that you want to delete.</span></span> <span data-ttu-id="c7ead-157">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] > [網路對應] 中，以滑鼠右鍵按一下網路對應 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click the network mapping > **Delete**.</span></span>
3. <span data-ttu-id="c7ead-158">記下 VMM 伺服器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-158">Note the ID of the VMM server.</span></span>
4. <span data-ttu-id="c7ead-159">將您想要移除的 VMM 伺服器上取消雲端和複寫原則的關聯。</span><span class="sxs-lookup"><span data-stu-id="c7ead-159">Disassociate replication policies from clouds on the VMM server you want to remove.</span></span>  <span data-ttu-id="c7ead-160">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] >  [複寫原則] 中，按兩下相關聯的原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="c7ead-161">以滑鼠右鍵按一下雲端 > [取消關聯]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-161">Right-click the cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="c7ead-162">刪除 VMM 伺服器或作用中的節點。</span><span class="sxs-lookup"><span data-stu-id="c7ead-162">Delete the VMM server or active node.</span></span> <span data-ttu-id="c7ead-163">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] > [VMM 伺服器] 中，以滑鼠右鍵按一下伺服器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click the server > **Delete**.</span></span>
6. <span data-ttu-id="c7ead-164">在 VMM 伺服器上下載並執行[清除指令碼](http://aka.ms/asr-cleanup-script-vmm)。</span><span class="sxs-lookup"><span data-stu-id="c7ead-164">Download and run the [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on the VMM server.</span></span> <span data-ttu-id="c7ead-165">使用 [以系統管理員身分執行] 選項開啟 PowerShell，以變更預設 (LocalMachine) 範圍的執行原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-165">Open PowerShell with the **Run as Administrator** option, to change the execution policy for the default (LocalMachine) scope.</span></span> <span data-ttu-id="c7ead-166">在指令碼中，指定您想要移除的 VMM 伺服器的識別碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-166">In the script, specify the ID of the VMM server you want to remove.</span></span> <span data-ttu-id="c7ead-167">該指令碼會從伺服器移除註冊及雲端配對資訊。</span><span class="sxs-lookup"><span data-stu-id="c7ead-167">The script removes registration and cloud pairing information from the server.</span></span>
5. <span data-ttu-id="c7ead-168">在包含已和您想要刪除之 VMM 伺服器上的雲端配對之雲端的任何其他 VMM 伺服器上執行清除指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-168">Run the cleanup script on any other VMM servers that contain clouds that are paired with clouds on the VMM server you want to remove.</span></span>
6. <span data-ttu-id="c7ead-169">在已安裝提供者的任何其他被動 VMM 叢集節點上執行清除指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-169">Run the  cleanup script on any other passive VMM cluster nodes that have the Provider installed.</span></span>
7. <span data-ttu-id="c7ead-170">在 VMM 伺服器上手動將提供者解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c7ead-170">Uninstall the Provider manually on the VMM server.</span></span> <span data-ttu-id="c7ead-171">如果您有叢集，請將它從所有節點中移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="c7ead-172">如果您是複寫到 Azure，您可以將 Microsoft 復原服務代理程式從已刪除之雲端中的 Hyper-V 主機上移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-172">If you replicating to Azure, you can remove the Microsoft Recovery Services agent from Hyper-V hosts in the deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="c7ead-173">取消註冊 Hyper-V 站台中的 Hyper-V 主機</span><span class="sxs-lookup"><span data-stu-id="c7ead-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="c7ead-174">未受 VMM 管理的 Hyper-V 主機會集合成 Hyper-V 站台。</span><span class="sxs-lookup"><span data-stu-id="c7ead-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="c7ead-175">移除 Hyper-V 站台中的主機，方法如下：</span><span class="sxs-lookup"><span data-stu-id="c7ead-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="c7ead-176">針對主機上的 Hyper-V VM 停用複寫。</span><span class="sxs-lookup"><span data-stu-id="c7ead-176">Disable replication for Hyper-V VMs located on the host.</span></span>
2. <span data-ttu-id="c7ead-177">取消關聯 Hyper-V 站台的原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-177">Disassociate policies for the Hyper-V site.</span></span> <span data-ttu-id="c7ead-178">在 [Site Recovery 基礎結構] > [適用於 Hyper-V 站台] >  [複寫原則] 中，按兩下相關聯的原則。</span><span class="sxs-lookup"><span data-stu-id="c7ead-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click the associated policy.</span></span> <span data-ttu-id="c7ead-179">以滑鼠右鍵按一下站台 > [取消關聯]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-179">Right-click the site > **Disassociate**.</span></span>
3. <span data-ttu-id="c7ead-180">刪除 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="c7ead-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="c7ead-181">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] > [Hyper-V 主機] 中，以滑鼠右鍵按一下伺服器 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click the server > **Delete**.</span></span>
4. <span data-ttu-id="c7ead-182">從 Hyper-V 站台移除所有主機之後，將 Hyper-V 站台刪除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-182">Delete the Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="c7ead-183">在 [Site Recovery 基礎結構] > [適用於 System Center VMM] > [Hyper-V 站台] 中，以滑鼠右鍵按一下站台 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click the site > **Delete**.</span></span>
5. <span data-ttu-id="c7ead-184">在每個移除的 Hyper-V 主機上執行下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-184">Run the following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="c7ead-185">該指令碼會清除伺服器上的設定，並從保存庫取消註冊該伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-185">The script cleans up settings on the server, and unregisters it from the vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping the Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="c7ead-186">停用 VMware VM 或實體伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="c7ead-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="c7ead-187">在 [受保護的項目] > [已複寫的項目] 中，以滑鼠右鍵按一下機器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-187">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="c7ead-188">在 [移除機器] 中，選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="c7ead-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="c7ead-189">**停用對機器的保護 (建議)**。</span><span class="sxs-lookup"><span data-stu-id="c7ead-189">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="c7ead-190">使用此選項以停止複寫機器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-190">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="c7ead-191">系統會自動清除 Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="c7ead-192">您只會在以下情況看到此選項：</span><span class="sxs-lookup"><span data-stu-id="c7ead-192">You will only see this option in the following circumstances:</span></span>
        - <span data-ttu-id="c7ead-193">**您已調整虛擬機器磁碟區的大小**—當您調整磁碟區大小時，虛擬機器會進入重大狀態。</span><span class="sxs-lookup"><span data-stu-id="c7ead-193">**You've resized the VM volume**—When you resize a volume the virtual machine goes into a critical state.</span></span> <span data-ttu-id="c7ead-194">選取此選項以停用保護，同時保留在 Azure 中的復原點。</span><span class="sxs-lookup"><span data-stu-id="c7ead-194">Select this option to disables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="c7ead-195">當您再次啟用機器的保護時，調整過大小的磁碟區資料會傳輸至 Azure。</span><span class="sxs-lookup"><span data-stu-id="c7ead-195">When you enable protection for the machine again, the data for the resized volume will be transferred to Azure.</span></span>
        - <span data-ttu-id="c7ead-196">**您最近已執行容錯移轉**—在您執行容錯移轉進行環境測試之後，請選取此選項以再次開始保護內部部署機器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-196">**You've recently run a failover**—After you've run a failover to test your environment, select this option to start protecting on-premises machines again.</span></span> <span data-ttu-id="c7ead-197">它會停用每個虛擬機器，您接著必須再次啟用對它們的保護。</span><span class="sxs-lookup"><span data-stu-id="c7ead-197">It disables each virtual machine, and then you need to enable protection for them again.</span></span> <span data-ttu-id="c7ead-198">使用這項設定停用機器，不會影響 Azure 中的複本虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-198">Disabling the machine with this setting doesn't affect the replica virtual machine in Azure.</span></span> <span data-ttu-id="c7ead-199">請勿從機器解除安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="c7ead-199">Don't uninstall the Mobility service from the machine.</span></span>
    - <span data-ttu-id="c7ead-200">[停止管理機器]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-200">**Stop managing the machine**.</span></span> <span data-ttu-id="c7ead-201">如果選取此選項，則只會將機器從保存庫移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-201">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="c7ead-202">機器的內部部署保護設定不受影響。</span><span class="sxs-lookup"><span data-stu-id="c7ead-202">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="c7ead-203">若要移除機器上的設定並從 Azure 訂用帳戶移除機器，您需要將行動服務解除安裝以清除設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-203">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings by uninstalling the Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="c7ead-204">停用 VMM 雲端中 Hyper-V VM 的保護</span><span class="sxs-lookup"><span data-stu-id="c7ead-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="c7ead-205">在 [受保護的項目] > [已複寫的項目] 中，以滑鼠右鍵按一下機器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-205">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="c7ead-206">在 [移除機器] 中，選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="c7ead-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="c7ead-207">**停用對機器的保護 (建議)**。</span><span class="sxs-lookup"><span data-stu-id="c7ead-207">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="c7ead-208">使用此選項以停止複寫機器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-208">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="c7ead-209">系統會自動清除 Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="c7ead-210">[停止管理機器]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-210">**Stop managing the machine**.</span></span> <span data-ttu-id="c7ead-211">如果選取此選項，則只會將機器從保存庫移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-211">If you select this option, the machine will only be removed from the vault.</span></span> <span data-ttu-id="c7ead-212">機器的內部部署保護設定不受影響。</span><span class="sxs-lookup"><span data-stu-id="c7ead-212">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="c7ead-213">若要移除機器上的設定並從 Azure 訂用帳戶移除機器，您需要按照以下指示手動清除設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-213">To remove settings on the machine, and to remove the machine from the Azure subscription, you need to clean the settings up manually, using the instructions below.</span></span> <span data-ttu-id="c7ead-214">請注意，如果您選擇刪除虛擬機器及其硬碟，將會從目標位置移除它們。</span><span class="sxs-lookup"><span data-stu-id="c7ead-214">Note that if you select to delete the virtual machine and its hard disks, they'll be removed from the target location.</span></span>

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a><span data-ttu-id="c7ead-215">清除保護設定 - 複寫至次要 VMM 站台</span><span class="sxs-lookup"><span data-stu-id="c7ead-215">Clean up protection settings - replication to a secondary VMM site</span></span>

<span data-ttu-id="c7ead-216">如果您選取 [停止管理機器] 且複寫至次要站台，請在主要伺服器上執行此指令碼，以清除主要虛擬機器的設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-216">If you selected **Stop managing the machine** and you replicating to a secondary site, run this script on the primary server to clean up the settings for the primary virtual machine.</span></span> <span data-ttu-id="c7ead-217">在 VMM 主控台中，按一下 [PowerShell] 按鈕來開啟 VMM PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="c7ead-217">In the VMM console click the PowerShell button to open the VMM PowerShell console.</span></span> <span data-ttu-id="c7ead-218">將 SQLVM1 取代成您的虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7ead-218">Replace SQLVM1 with the name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="c7ead-219">在次要 VMM 伺服器上，執行此指令碼來清除次要虛擬機器的設定：</span><span class="sxs-lookup"><span data-stu-id="c7ead-219">On the secondary VMM server run this script to clean up the settings for the secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="c7ead-220">在次要 VMM 伺服器上，重新整理 Hyper-V 主機伺服器上的虛擬機器，以便再次於 VMM 主控台中偵測次要 VM。</span><span class="sxs-lookup"><span data-stu-id="c7ead-220">On the secondary VMM server, refresh the virtual machines on the Hyper-V host server, so that the secondary VM gets detected again in the VMM console.</span></span>
4. <span data-ttu-id="c7ead-221">上述步驟會清除 VMM 伺服器上的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-221">The above steps clear up the replication settings on the VMM server.</span></span> <span data-ttu-id="c7ead-222">如果您想要停止複寫虛擬機器，請在主要和次要 VM 上執行以下指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-222">If you want to stop replication for the virtual machine, run the following script oh the primary and secondary VMs.</span></span> <span data-ttu-id="c7ead-223">將 SQLVM1 取代成您的虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7ead-223">Replace SQLVM1 with the name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a><span data-ttu-id="c7ead-224">清除保護設定 - 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="c7ead-224">Clean up protection settings - replication to Azure</span></span>

1. <span data-ttu-id="c7ead-225">如果您選取 [停止管理機器] 且複寫到 Azure，請從 VMM 主控台使用 PowerShell，在來源 VMM 伺服器上執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-225">If you selected **Stop managing the machine** and you replicate to Azure, run this script on the source VMM server, using PowerShell from the VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="c7ead-226">上述步驟會清除 VMM 伺服器上的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-226">The above steps clear the replication settings on the VMM server.</span></span> <span data-ttu-id="c7ead-227">若要停止複寫在 Hyper-V 主機伺服器上執行的虛擬機器，請執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="c7ead-227">To stop replication for the virtual machine running on the Hyper-V host server, run this script.</span></span> <span data-ttu-id="c7ead-228">將 SQLVM1 取代成您的虛擬機器的名稱，並將 host01.contoso.com 取代成 Hyper-V 主機伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7ead-228">Replace SQLVM1 with the name of your virtual machine, and host01.contoso.com with the name of the Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="c7ead-229">停用對 Hyper-V 站台中 Hyper-V VM 的保護</span><span class="sxs-lookup"><span data-stu-id="c7ead-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="c7ead-230">如果您是在沒有 VMM 伺服器的情況下將 Hyper-V VM 複寫到 Azure，請使用此程序。</span><span class="sxs-lookup"><span data-stu-id="c7ead-230">Use this procedure if you're replicating Hyper-V VMs to Azure without a VMM server.</span></span>

1. <span data-ttu-id="c7ead-231">在 [受保護的項目] > [已複寫的項目] 中，以滑鼠右鍵按一下機器 > [刪除]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-231">In **Protected Items** > **Replicated Items**, right-click the machine > **Delete**.</span></span>
2. <span data-ttu-id="c7ead-232">在 [移除機器] 中，您可以選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="c7ead-232">In **Remove Machine**, you can select the following options:</span></span>

   - <span data-ttu-id="c7ead-233">**停用對機器的保護 (建議)**。</span><span class="sxs-lookup"><span data-stu-id="c7ead-233">**Disable protection for the machine (recommended)**.</span></span> <span data-ttu-id="c7ead-234">使用此選項以停止複寫機器。</span><span class="sxs-lookup"><span data-stu-id="c7ead-234">Use this option to stop replicating the machine.</span></span> <span data-ttu-id="c7ead-235">系統會自動清除 Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="c7ead-236">[停止管理機器]。</span><span class="sxs-lookup"><span data-stu-id="c7ead-236">**Stop managing the machine**.</span></span> <span data-ttu-id="c7ead-237">如果選取此選項，則只會將機器從保存庫移除。</span><span class="sxs-lookup"><span data-stu-id="c7ead-237">If you select this option the machine will only be removed from the vault.</span></span> <span data-ttu-id="c7ead-238">機器的內部部署保護設定不受影響。</span><span class="sxs-lookup"><span data-stu-id="c7ead-238">On-premises protection settings for the machine won’t be affected.</span></span> <span data-ttu-id="c7ead-239">若要移除機器上的設定並從 Azure 訂用帳戶移除虛擬機器，您需要手動清除設定。</span><span class="sxs-lookup"><span data-stu-id="c7ead-239">To remove settings on the machine, and to remove the virtual machine from the Azure subscription, you need to clean the settings up manually.</span></span> <span data-ttu-id="c7ead-240">如果您選擇刪除虛擬機器及其硬碟，將會從目標位置移除它們。</span><span class="sxs-lookup"><span data-stu-id="c7ead-240">If you select to delete the virtual machine and its hard disks they will be removed from the target location.</span></span>
3. <span data-ttu-id="c7ead-241">如果您選取 [停止管理機器]，請在來源 Hyper-V 主機伺服器上執行此指令碼，以移除虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="c7ead-241">If you selected **Stop managing the machine**, run this script on the source Hyper-V host server, to remove replication for the virtual machine.</span></span> <span data-ttu-id="c7ead-242">將 SQLVM1 取代成您的虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7ead-242">Replace SQLVM1 with the name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
