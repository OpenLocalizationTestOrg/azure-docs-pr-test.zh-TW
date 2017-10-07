---
title: "aaaRemove 伺服器並停用保護 |Microsoft 文件"
description: "本文說明如何 toounregister 伺服器從站台復原保存庫，和 toodisable 保護的虛擬機器和實體伺服器。"
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
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a><span data-ttu-id="b8aba-103">移除伺服器並停用保護</span><span class="sxs-lookup"><span data-stu-id="b8aba-103">Remove servers and disable protection</span></span>

<span data-ttu-id="b8aba-104">hello Azure Site Recovery 服務佔 tooyour 業務續航力和災害復原 (BCDR) 策略。</span><span class="sxs-lookup"><span data-stu-id="b8aba-104">hello Azure Site Recovery service contributes tooyour business continuity and disaster recovery (BCDR) strategy.</span></span> <span data-ttu-id="b8aba-105">hello 服務會協調複寫、 容錯移轉和復原的虛擬機器和實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-105">hello service orchestrates replication, failover and recovery of virtual machines and physical servers.</span></span> <span data-ttu-id="b8aba-106">電腦可以是複寫的 tooAzure 或 tooa 次要內部部署資料中心。</span><span class="sxs-lookup"><span data-stu-id="b8aba-106">Machines can be replicated tooAzure, or tooa secondary on-premises data center.</span></span> <span data-ttu-id="b8aba-107">如需快速概觀，請參閱 [什麼是 Azure Site Recovery？](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b8aba-107">For a quick overview read [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>

<span data-ttu-id="b8aba-108">本文說明如何 toounregister 伺服器，從 復原服務保存庫中 hello Azure 入口網站和 toodisable 保護機器的保護站台復原的方式。</span><span class="sxs-lookup"><span data-stu-id="b8aba-108">This article describes how toounregister servers from a Recovery Services vault in hello Azure portal, and how toodisable protection for machines protected by Site Recovery.</span></span>

<span data-ttu-id="b8aba-109">將任何註解或問題張貼在本文中，或在 hello hello 下方[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="b8aba-109">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="unregister-a-connected-configuration-server"></a><span data-ttu-id="b8aba-110">將已連線的組態伺服器取消註冊</span><span class="sxs-lookup"><span data-stu-id="b8aba-110">Unregister a connected configuration server</span></span>

<span data-ttu-id="b8aba-111">如果您要複寫的 VMware Vm 或 Windows/Linux 實體伺服器 tooAzure，您可以伺服器取消登錄已連線的設定從保存庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8aba-111">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister a connected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="b8aba-112">停用機器保護。</span><span class="sxs-lookup"><span data-stu-id="b8aba-112">Disable machine protection.</span></span> <span data-ttu-id="b8aba-113">在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-113">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b8aba-114">取消關聯任何原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-114">Disassociate any policies.</span></span> <span data-ttu-id="b8aba-115">在**Site Recovery 基礎結構** > **的 VMWare 及實體機器** > **複寫原則**，按兩下 hello相關聯的原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-115">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b8aba-116">以滑鼠右鍵按一下 hello 組態伺服器 > **Disassociate**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-116">Right-click hello configuration server > **Disassociate**.</span></span>
3. <span data-ttu-id="b8aba-117">移除任何額外的內部部署處理伺服器或主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-117">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="b8aba-118">在**Site Recovery 基礎結構** > **的 VMWare 及實體機器** > **設定伺服器**，以滑鼠右鍵按一下 hello 伺服器>**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-118">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="b8aba-119">刪除 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-119">Delete hello configuration server.</span></span>
5. <span data-ttu-id="b8aba-120">手動解除安裝 hello hello 主要目標伺服器上執行的行動服務 (這會是另一個伺服器或 hello 組態伺服器上執行)。</span><span class="sxs-lookup"><span data-stu-id="b8aba-120">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
6. <span data-ttu-id="b8aba-121">將任何額外的處理伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="b8aba-121">Uninstall any additional process servers.</span></span>
7. <span data-ttu-id="b8aba-122">Hello 組態伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="b8aba-122">Uninstall hello configuration server.</span></span>
8. <span data-ttu-id="b8aba-123">在 hello 組態伺服器上解除安裝 hello 所安裝的站台復原的 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b8aba-123">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
9. <span data-ttu-id="b8aba-124">Hello 登錄 hello 組態伺服器中刪除 hello 金鑰``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``。</span><span class="sxs-lookup"><span data-stu-id="b8aba-124">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-unconnected-configuration-server"></a><span data-ttu-id="b8aba-125">將未連線的組態伺服器取消註冊</span><span class="sxs-lookup"><span data-stu-id="b8aba-125">Unregister a unconnected configuration server</span></span>

<span data-ttu-id="b8aba-126">如果您要複寫的 VMware Vm 或 Windows/Linux 實體伺服器 tooAzure，可取消從保存庫未連接的組態伺服器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8aba-126">If you replicate VMware VMs or Windows/Linux physical servers tooAzure, you can unregister an unconnected configuration server from a vault as follows:</span></span>

1. <span data-ttu-id="b8aba-127">停用機器保護。</span><span class="sxs-lookup"><span data-stu-id="b8aba-127">Disable machine protection.</span></span> <span data-ttu-id="b8aba-128">在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-128">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span> <span data-ttu-id="b8aba-129">選取**停止管理 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-129">Select **Stop managing hello machine**.</span></span>
2. <span data-ttu-id="b8aba-130">移除任何額外的內部部署處理伺服器或主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-130">Remove any additional on-premises process or master target servers.</span></span> <span data-ttu-id="b8aba-131">在**Site Recovery 基礎結構** > **的 VMWare 及實體機器** > **設定伺服器**，以滑鼠右鍵按一下 hello 伺服器>**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-131">In **Site Recovery Infrastructure** > **For VMWare & Physical Machines** > **Configuration Servers**, right-click hello server > **Delete**.</span></span>
3. <span data-ttu-id="b8aba-132">刪除 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-132">Delete hello configuration server.</span></span>
4. <span data-ttu-id="b8aba-133">手動解除安裝 hello hello 主要目標伺服器上執行的行動服務 (這會是另一個伺服器或 hello 組態伺服器上執行)。</span><span class="sxs-lookup"><span data-stu-id="b8aba-133">Manually uninstall hello Mobility service running on hello master target server (this will be either a separate server, or running on hello configuration server).</span></span>
5. <span data-ttu-id="b8aba-134">將任何額外的處理伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="b8aba-134">Uninstall any additional process servers.</span></span>
6. <span data-ttu-id="b8aba-135">Hello 組態伺服器解除安裝。</span><span class="sxs-lookup"><span data-stu-id="b8aba-135">Uninstall hello configuration server.</span></span>
7. <span data-ttu-id="b8aba-136">在 hello 組態伺服器上解除安裝 hello 所安裝的站台復原的 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b8aba-136">On hello configuration server, uninstall hello instance of MySQL that was installed by Site Recovery.</span></span>
8. <span data-ttu-id="b8aba-137">Hello 登錄 hello 組態伺服器中刪除 hello 金鑰``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``。</span><span class="sxs-lookup"><span data-stu-id="b8aba-137">In hello registry of hello configuration server delete hello key ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.</span></span>

## <a name="unregister-a-connected-vmm-server"></a><span data-ttu-id="b8aba-138">取消註冊已連線的 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="b8aba-138">Unregister a connected VMM server</span></span>

<span data-ttu-id="b8aba-139">最佳做法，建議您已連接 tooAzure 時，取消登錄 hello VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-139">As a best practice, we recommend that you unregister hello VMM server when it's connected tooAzure.</span></span> <span data-ttu-id="b8aba-140">這可確保設定 hello VMM 伺服器上 （和其他與配對雲端的 VMM 伺服器上） 會正確清除。</span><span class="sxs-lookup"><span data-stu-id="b8aba-140">This ensures that settings on hello VMM servers (and on other VMM servers with paired clouds) are cleaned up properly.</span></span> <span data-ttu-id="b8aba-141">您只應在連線發生永久性問題時，才移除未連線的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-141">You should only remove an unconnected server if there's a permanent issue with connectivity.</span></span> <span data-ttu-id="b8aba-142">如果 hello VMM 伺服器未連接，您將需要 toomanually 執行指令碼 tooclean 的設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-142">If hello VMM server isn’t connected, you will need toomanually run a script tooclean up settings.</span></span>

1. <span data-ttu-id="b8aba-143">停止複寫 hello 想 tooremove VMM 伺服器上雲端中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="b8aba-143">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="b8aba-144">刪除任何 hello 想 toodelete VMM 伺服器上雲端所使用的網路對應。</span><span class="sxs-lookup"><span data-stu-id="b8aba-144">Delete any network mappings used by clouds on hello VMM server you want toodelete.</span></span> <span data-ttu-id="b8aba-145">在**Site Recovery 基礎結構** > **System Center VMM** > **網路對應**，以滑鼠右鍵按一下 hello 網路對應 > **刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-145">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="b8aba-146">取消關聯 hello 想 tooremove VMM 伺服器上雲端的複寫的原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-146">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="b8aba-147">在**Site Recovery 基礎結構** > **System Center VMM** >  **複寫原則**，連按兩下 相關聯的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-147">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b8aba-148">以滑鼠右鍵按一下 hello 雲端 > **Disassociate**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-148">Right-click hello cloud > **Disassociate**.</span></span>
4. <span data-ttu-id="b8aba-149">刪除 hello VMM 伺服器或作用中 VMM 的節點。</span><span class="sxs-lookup"><span data-stu-id="b8aba-149">Delete hello VMM server or active VMM node.</span></span> <span data-ttu-id="b8aba-150">在**Site Recovery 基礎結構** > **System Center VMM** > **VMM 伺服器**，以滑鼠右鍵按一下 hello 伺服器 > **刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-150">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
5. <span data-ttu-id="b8aba-151">解除安裝 hello VMM 伺服器上手動 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="b8aba-151">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="b8aba-152">如果您有叢集，請將它從所有節點中移除。</span><span class="sxs-lookup"><span data-stu-id="b8aba-152">If you have a cluster, remove from all nodes.</span></span>
6. <span data-ttu-id="b8aba-153">如果您要複寫 tooAzure，手動移除 hello Microsoft 復原服務代理程式從 hello 刪除雲端中的 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="b8aba-153">If you're replicating tooAzure, manually remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>



### <a name="unregister-an-unconnected-vmm-server"></a><span data-ttu-id="b8aba-154">取消註冊未連線的 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="b8aba-154">Unregister an unconnected VMM server</span></span>

1. <span data-ttu-id="b8aba-155">停止複寫 hello 想 tooremove VMM 伺服器上雲端中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="b8aba-155">Stop replicating VMs in clouds on hello VMM server you want tooremove.</span></span>
2. <span data-ttu-id="b8aba-156">刪除任何您想 toodelete hello VMM 伺服器上雲端所使用的網路對應。</span><span class="sxs-lookup"><span data-stu-id="b8aba-156">Delete any network mappings used by clouds on hello VMM server that you want toodelete.</span></span> <span data-ttu-id="b8aba-157">在**Site Recovery 基礎結構** > **System Center VMM** > **網路對應**，以滑鼠右鍵按一下 hello 網路對應 > **刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-157">In **Site Recovery Infrastructure** > **For System Center VMM** > **Network Mapping**, right-click hello network mapping > **Delete**.</span></span>
3. <span data-ttu-id="b8aba-158">請注意 hello 識別碼 hello VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-158">Note hello ID of hello VMM server.</span></span>
4. <span data-ttu-id="b8aba-159">取消關聯 hello 想 tooremove VMM 伺服器上雲端的複寫的原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-159">Disassociate replication policies from clouds on hello VMM server you want tooremove.</span></span>  <span data-ttu-id="b8aba-160">在**Site Recovery 基礎結構** > **System Center VMM** >  **複寫原則**，連按兩下 相關聯的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-160">In **Site Recovery Infrastructure** > **For System Center VMM** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b8aba-161">以滑鼠右鍵按一下 hello 雲端 > **Disassociate**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-161">Right-click hello cloud > **Disassociate**.</span></span>
5. <span data-ttu-id="b8aba-162">刪除 hello VMM 伺服器或作用中節點。</span><span class="sxs-lookup"><span data-stu-id="b8aba-162">Delete hello VMM server or active node.</span></span> <span data-ttu-id="b8aba-163">在**Site Recovery 基礎結構** > **System Center VMM** > **VMM 伺服器**，以滑鼠右鍵按一下 hello 伺服器 > **刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-163">In **Site Recovery Infrastructure** > **For System Center VMM** > **VMM Servers**, right-click hello server > **Delete**.</span></span>
6. <span data-ttu-id="b8aba-164">下載並執行 hello[清除指令碼](http://aka.ms/asr-cleanup-script-vmm)hello VMM 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b8aba-164">Download and run hello [cleanup script](http://aka.ms/asr-cleanup-script-vmm) on hello VMM server.</span></span> <span data-ttu-id="b8aba-165">開啟 PowerShell 以 hello**系統管理員身分執行**選項，hello 預設 (LocalMachine) 範圍 toochange hello 執行原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-165">Open PowerShell with hello **Run as Administrator** option, toochange hello execution policy for hello default (LocalMachine) scope.</span></span> <span data-ttu-id="b8aba-166">在 hello 指令碼指定 hello 識別碼 hello 想 tooremove VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-166">In hello script, specify hello ID of hello VMM server you want tooremove.</span></span> <span data-ttu-id="b8aba-167">hello 指令碼會移除登錄與雲端配對 hello 伺服器的資訊。</span><span class="sxs-lookup"><span data-stu-id="b8aba-167">hello script removes registration and cloud pairing information from hello server.</span></span>
5. <span data-ttu-id="b8aba-168">包含會與 hello 想 tooremove VMM 伺服器上的雲端配對的雲端的其他任何 VMM 伺服器上執行 hello 清除指令碼。</span><span class="sxs-lookup"><span data-stu-id="b8aba-168">Run hello cleanup script on any other VMM servers that contain clouds that are paired with clouds on hello VMM server you want tooremove.</span></span>
6. <span data-ttu-id="b8aba-169">任何其他被動 VMM 叢集節點上已安裝提供者的 hello 執行 hello 清除指令碼。</span><span class="sxs-lookup"><span data-stu-id="b8aba-169">Run hello  cleanup script on any other passive VMM cluster nodes that have hello Provider installed.</span></span>
7. <span data-ttu-id="b8aba-170">解除安裝 hello VMM 伺服器上手動 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="b8aba-170">Uninstall hello Provider manually on hello VMM server.</span></span> <span data-ttu-id="b8aba-171">如果您有叢集，請將它從所有節點中移除。</span><span class="sxs-lookup"><span data-stu-id="b8aba-171">If you have a cluster, remove from all nodes.</span></span>
8. <span data-ttu-id="b8aba-172">如果您複寫 tooAzure，您可以移除 hello Microsoft 復原服務代理程式在 hello 刪除雲端中的 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="b8aba-172">If you replicating tooAzure, you can remove hello Microsoft Recovery Services agent from Hyper-V hosts in hello deleted clouds.</span></span>

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a><span data-ttu-id="b8aba-173">取消註冊 Hyper-V 站台中的 Hyper-V 主機</span><span class="sxs-lookup"><span data-stu-id="b8aba-173">Unregister a Hyper-V host in a Hyper-V Site</span></span>

<span data-ttu-id="b8aba-174">未受 VMM 管理的 Hyper-V 主機會集合成 Hyper-V 站台。</span><span class="sxs-lookup"><span data-stu-id="b8aba-174">Hyper-V hosts that aren't managed by VMM are gathered into a Hyper-V site.</span></span> <span data-ttu-id="b8aba-175">移除 Hyper-V 站台中的主機，方法如下：</span><span class="sxs-lookup"><span data-stu-id="b8aba-175">Remove a host in a Hyper-V site as follows:</span></span>

1. <span data-ttu-id="b8aba-176">停用 HYPER-V Vm 位於 hello 主機上的複寫。</span><span class="sxs-lookup"><span data-stu-id="b8aba-176">Disable replication for Hyper-V VMs located on hello host.</span></span>
2. <span data-ttu-id="b8aba-177">取消關聯 hello HYPER-V 站台的原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-177">Disassociate policies for hello Hyper-V site.</span></span> <span data-ttu-id="b8aba-178">在**Site Recovery 基礎結構** > **HYPER-V 站台的** >  **複寫原則**，連按兩下 相關聯的 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="b8aba-178">In **Site Recovery Infrastructure** > **For Hyper-V Sites** >  **Replication Policies**, double-click hello associated policy.</span></span> <span data-ttu-id="b8aba-179">以滑鼠右鍵按一下 hello 網站 > **Disassociate**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-179">Right-click hello site > **Disassociate**.</span></span>
3. <span data-ttu-id="b8aba-180">刪除 Hyper-V 主機。</span><span class="sxs-lookup"><span data-stu-id="b8aba-180">Delete Hyper-V hosts.</span></span> <span data-ttu-id="b8aba-181">在**Site Recovery 基礎結構** > **System Center VMM** > **HYPER-V 主機**，以滑鼠右鍵按一下 hello 伺服器 > **刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-181">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Hosts**, right-click hello server > **Delete**.</span></span>
4. <span data-ttu-id="b8aba-182">從中移除所有主機之後，請刪除 hello HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="b8aba-182">Delete hello Hyper-V site after all hosts have been removed from it.</span></span> <span data-ttu-id="b8aba-183">在**Site Recovery 基礎結構** > **System Center VMM** > **HYPER-V 站台**，以滑鼠右鍵按一下 hello 網站 > **刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-183">In **Site Recovery Infrastructure** > **For System Center VMM** > **Hyper-V Sites**, right-click hello site > **Delete**.</span></span>
5. <span data-ttu-id="b8aba-184">執行下列指令碼，移除每個 HYPER-V 主機上的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8aba-184">Run hello following script on each Hyper-V host that you removed.</span></span> <span data-ttu-id="b8aba-185">hello 指令碼清除 hello 伺服器上的設定，並從 hello 保存庫取消註冊。</span><span class="sxs-lookup"><span data-stu-id="b8aba-185">hello script cleans up settings on hello server, and unregisters it from hello vault.</span></span>


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
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
                "Stopping hello Azure Site Recovery service..."
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

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
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



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a><span data-ttu-id="b8aba-186">停用 VMware VM 或實體伺服器的保護</span><span class="sxs-lookup"><span data-stu-id="b8aba-186">Disable protection for a VMware VM or physical server</span></span>

1. <span data-ttu-id="b8aba-187">在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-187">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b8aba-188">在 [移除機器] 中，選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="b8aba-188">In **Remove Machine**, select one of these options:</span></span>
    - <span data-ttu-id="b8aba-189">**停用保護 （建議選項） 的 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-189">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="b8aba-190">使用此選項 toostop，將 hello 機器複寫。</span><span class="sxs-lookup"><span data-stu-id="b8aba-190">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="b8aba-191">系統會自動清除 Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-191">Site Recovery settings will be cleaned up automatically.</span></span> <span data-ttu-id="b8aba-192">您只會看到此選項，在下列情況下的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8aba-192">You will only see this option in hello following circumstances:</span></span>
        - <span data-ttu-id="b8aba-193">**調整 hello VM 磁碟區**— 當您調整磁碟區 hello 虛擬機器便會進入 「 重大 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="b8aba-193">**You've resized hello VM volume**—When you resize a volume hello virtual machine goes into a critical state.</span></span> <span data-ttu-id="b8aba-194">選取此選項 toodisables 保護，同時保留在 Azure 中的復原點。</span><span class="sxs-lookup"><span data-stu-id="b8aba-194">Select this option toodisables protection while retaining recovery points in Azure.</span></span> <span data-ttu-id="b8aba-195">當您啟用 hello 機器的保護功能時，hello hello 調整磁碟區的資料會傳送的 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="b8aba-195">When you enable protection for hello machine again, hello data for hello resized volume will be transferred tooAzure.</span></span>
        - <span data-ttu-id="b8aba-196">**您最近已執行容錯移轉**— 您已執行容錯移轉 tootest 您的環境之後，請選取此選項 toostart，一次保護內部部署機器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-196">**You've recently run a failover**—After you've run a failover tootest your environment, select this option toostart protecting on-premises machines again.</span></span> <span data-ttu-id="b8aba-197">它會停用每個虛擬機器，然後再 tooenable 保護它們一次。</span><span class="sxs-lookup"><span data-stu-id="b8aba-197">It disables each virtual machine, and then you need tooenable protection for them again.</span></span> <span data-ttu-id="b8aba-198">停用這項設定的 hello 機器不會影響在 Azure 中的 hello 複本虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-198">Disabling hello machine with this setting doesn't affect hello replica virtual machine in Azure.</span></span> <span data-ttu-id="b8aba-199">不要解除安裝 hello 機器 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="b8aba-199">Don't uninstall hello Mobility service from hello machine.</span></span>
    - <span data-ttu-id="b8aba-200">**停止管理 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-200">**Stop managing hello machine**.</span></span> <span data-ttu-id="b8aba-201">如果您選取此選項時，只會移除 hello 機器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="b8aba-201">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="b8aba-202">Hello 機器的內部部署保護設定不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="b8aba-202">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="b8aba-203">tooremove hello 電腦及從 hello Azure 訂用帳戶的 tooremove hello 電腦上，您需要設定 tooclean hello 設定解除安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="b8aba-203">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings by uninstalling hello Mobility service.</span></span>

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a><span data-ttu-id="b8aba-204">停用 VMM 雲端中 Hyper-V VM 的保護</span><span class="sxs-lookup"><span data-stu-id="b8aba-204">Disable protection for a Hyper-V VM in a VMM cloud</span></span>

1. <span data-ttu-id="b8aba-205">在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-205">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b8aba-206">在 [移除機器] 中，選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="b8aba-206">In **Remove Machine**, select one of these options:</span></span>

    - <span data-ttu-id="b8aba-207">**停用保護 （建議選項） 的 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-207">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="b8aba-208">使用此選項 toostop，將 hello 機器複寫。</span><span class="sxs-lookup"><span data-stu-id="b8aba-208">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="b8aba-209">系統會自動清除 Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-209">Site Recovery settings will be cleaned up automatically.</span></span>
    - <span data-ttu-id="b8aba-210">**停止管理 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-210">**Stop managing hello machine**.</span></span> <span data-ttu-id="b8aba-211">如果您選取此選項時，只會移除 hello 機器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="b8aba-211">If you select this option, hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="b8aba-212">Hello 機器的內部部署保護設定不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="b8aba-212">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="b8aba-213">tooremove hello 電腦及從 hello Azure 訂用帳戶的 tooremove hello 電腦上的設定，您需要 tooclean hello 設定向上以手動方式，使用下列的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="b8aba-213">tooremove settings on hello machine, and tooremove hello machine from hello Azure subscription, you need tooclean hello settings up manually, using hello instructions below.</span></span> <span data-ttu-id="b8aba-214">請注意，是否您選取 toodelete hello 虛擬機器和其硬碟，將會移除這些 hello 目標位置。</span><span class="sxs-lookup"><span data-stu-id="b8aba-214">Note that if you select toodelete hello virtual machine and its hard disks, they'll be removed from hello target location.</span></span>

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a><span data-ttu-id="b8aba-215">清理保護設定-複寫 tooa 次要 VMM 站台</span><span class="sxs-lookup"><span data-stu-id="b8aba-215">Clean up protection settings - replication tooa secondary VMM site</span></span>

<span data-ttu-id="b8aba-216">如果您選取**停止管理 hello 機器**和複寫 tooa 次要站台，您可以執行這個指令碼在 hello 主要伺服器 tooclean hello hello 主要虛擬機器的設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-216">If you selected **Stop managing hello machine** and you replicating tooa secondary site, run this script on hello primary server tooclean up hello settings for hello primary virtual machine.</span></span> <span data-ttu-id="b8aba-217">Hello VMM 主控台中按一下 hello PowerShell 按鈕 tooopen hello VMM PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="b8aba-217">In hello VMM console click hello PowerShell button tooopen hello VMM PowerShell console.</span></span> <span data-ttu-id="b8aba-218">SQLVM1 取代 hello 您的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="b8aba-218">Replace SQLVM1 with hello name of your virtual machine.</span></span>

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="b8aba-219">Hello 次要 VMM 伺服器上執行此指令碼 tooclean，hello 次要虛擬機器的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="b8aba-219">On hello secondary VMM server run this script tooclean up hello settings for hello secondary virtual machine:</span></span>

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. <span data-ttu-id="b8aba-220">Hello 次要 VMM 伺服器上，重新整理 hello hello HYPER-V 主機伺服器上的虛擬機器，如此 hello 第二個 VM 取得偵測再次 hello VMM 主控台中。</span><span class="sxs-lookup"><span data-stu-id="b8aba-220">On hello secondary VMM server, refresh hello virtual machines on hello Hyper-V host server, so that hello secondary VM gets detected again in hello VMM console.</span></span>
4. <span data-ttu-id="b8aba-221">上述步驟 hello 清除 hello hello VMM 伺服器上的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-221">hello above steps clear up hello replication settings on hello VMM server.</span></span> <span data-ttu-id="b8aba-222">如果您想 hello 虛擬機器，執行下列指令碼喔 hello toostop 複寫 hello 主要和次要的 Vm。</span><span class="sxs-lookup"><span data-stu-id="b8aba-222">If you want toostop replication for hello virtual machine, run hello following script oh hello primary and secondary VMs.</span></span> <span data-ttu-id="b8aba-223">SQLVM1 取代 hello 您的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="b8aba-223">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a><span data-ttu-id="b8aba-224">清理保護設定-複寫 tooAzure</span><span class="sxs-lookup"><span data-stu-id="b8aba-224">Clean up protection settings - replication tooAzure</span></span>

1. <span data-ttu-id="b8aba-225">如果您選取**停止管理 hello 機器**和您複寫 tooAzure、 hello 來源 VMM 伺服器上，從 hello VMM 主控台中使用 PowerShell 執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="b8aba-225">If you selected **Stop managing hello machine** and you replicate tooAzure, run this script on hello source VMM server, using PowerShell from hello VMM console.</span></span>
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. <span data-ttu-id="b8aba-226">hello 上述步驟，請清除 hello hello VMM 伺服器上的複寫設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-226">hello above steps clear hello replication settings on hello VMM server.</span></span> <span data-ttu-id="b8aba-227">toostop hello hello HYPER-V 主機伺服器上所執行的虛擬機器的複寫執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="b8aba-227">toostop replication for hello virtual machine running on hello Hyper-V host server, run this script.</span></span> <span data-ttu-id="b8aba-228">SQLVM1 hello 名稱取代您的虛擬機器和 host01.contoso.com hello hello HYPER-V 主機伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="b8aba-228">Replace SQLVM1 with hello name of your virtual machine, and host01.contoso.com with hello name of hello Hyper-V host server.</span></span>

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a><span data-ttu-id="b8aba-229">停用對 Hyper-V 站台中 Hyper-V VM 的保護</span><span class="sxs-lookup"><span data-stu-id="b8aba-229">Disable protection for a Hyper-V VM in a Hyper-V Site</span></span>

<span data-ttu-id="b8aba-230">如果您要複寫 HYPER-V Vm tooAzure 沒有 VMM 伺服器，請使用此程序。</span><span class="sxs-lookup"><span data-stu-id="b8aba-230">Use this procedure if you're replicating Hyper-V VMs tooAzure without a VMM server.</span></span>

1. <span data-ttu-id="b8aba-231">在**受保護項目** > **複寫的項目**，以滑鼠右鍵按一下 hello 機器 >**刪除**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-231">In **Protected Items** > **Replicated Items**, right-click hello machine > **Delete**.</span></span>
2. <span data-ttu-id="b8aba-232">在**移除機器**，您可以選取下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8aba-232">In **Remove Machine**, you can select hello following options:</span></span>

   - <span data-ttu-id="b8aba-233">**停用保護 （建議選項） 的 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-233">**Disable protection for hello machine (recommended)**.</span></span> <span data-ttu-id="b8aba-234">使用此選項 toostop，將 hello 機器複寫。</span><span class="sxs-lookup"><span data-stu-id="b8aba-234">Use this option toostop replicating hello machine.</span></span> <span data-ttu-id="b8aba-235">系統會自動清除 Site Recovery 設定。</span><span class="sxs-lookup"><span data-stu-id="b8aba-235">Site Recovery settings will be cleaned up automatically.</span></span>
   - <span data-ttu-id="b8aba-236">**停止管理 hello 機器**。</span><span class="sxs-lookup"><span data-stu-id="b8aba-236">**Stop managing hello machine**.</span></span> <span data-ttu-id="b8aba-237">如果您選取此選項將只會從 hello 保存庫移除 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="b8aba-237">If you select this option hello machine will only be removed from hello vault.</span></span> <span data-ttu-id="b8aba-238">Hello 機器的內部部署保護設定不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="b8aba-238">On-premises protection settings for hello machine won’t be affected.</span></span> <span data-ttu-id="b8aba-239">tooremove hello 機器和從 hello Azure 訂用帳戶的 tooremove hello 虛擬機器上，您需要設定 tooclean hello 設定總手動。</span><span class="sxs-lookup"><span data-stu-id="b8aba-239">tooremove settings on hello machine, and tooremove hello virtual machine from hello Azure subscription, you need tooclean hello settings up manually.</span></span> <span data-ttu-id="b8aba-240">如果您選取 toodelete hello 虛擬機器和其會移除 hello 目標位置的硬碟。</span><span class="sxs-lookup"><span data-stu-id="b8aba-240">If you select toodelete hello virtual machine and its hard disks they will be removed from hello target location.</span></span>
3. <span data-ttu-id="b8aba-241">如果您選取**停止管理 hello 機器**，執行這個 hello 來源 HYPER-V 主機伺服器上的指令碼、 tooremove hello 虛擬機器的複寫。</span><span class="sxs-lookup"><span data-stu-id="b8aba-241">If you selected **Stop managing hello machine**, run this script on hello source Hyper-V host server, tooremove replication for hello virtual machine.</span></span> <span data-ttu-id="b8aba-242">SQLVM1 取代 hello 您的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="b8aba-242">Replace SQLVM1 with hello name of your virtual machine.</span></span>

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
