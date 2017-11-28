---
title: "設定使用 Azure Site Recovery 將 Hyper-V 複寫至次要站台的複寫原則 | Microsoft Docs"
description: "說明如何設定使用 Azure Site Recovery 將 Hyper-V VM 複寫至次要 VMM 站台的原則。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a3ecc555e049914d7bffdddce7b0522f09362d24
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="22fde-103">步驟 8：設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="22fde-103">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="22fde-104">設定[網路對應](vmm-to-vmm-walkthrough-network-mapping.md)後，請使用本文設定複寫原則，以使用 [Azure Site Recovery](site-recovery-overview.md) 將 Hyper-V 虛擬機器 (VM) 複寫至次要站台。</span><span class="sxs-lookup"><span data-stu-id="22fde-104">After configuring [network mapping](vmm-to-vmm-walkthrough-network-mapping.md), use this article to set up a replication policy for Hyper-V virtual machine (VM) replication to a secondary site, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="22fde-105">在閱讀本文之後，請在下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)中張貼任何意見。</span><span class="sxs-lookup"><span data-stu-id="22fde-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="22fde-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="22fde-106">Before you start</span></span>

- <span data-ttu-id="22fde-107">當您建立複寫原則時，所有使用該原則的主機都必須有相同的作業系統。</span><span class="sxs-lookup"><span data-stu-id="22fde-107">When you create a replication policy, all hosts using the policy must have the same operating system.</span></span> <span data-ttu-id="22fde-108">VMM 雲端中可以包含執行不同 Windows Server 版本的 Hyper-V 主機，但在此情況下，您需要多個複寫原則。</span><span class="sxs-lookup"><span data-stu-id="22fde-108">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server, but in this case, you need multiple replication policies.</span></span>
- <span data-ttu-id="22fde-109">您可以離線執行初始複寫。</span><span class="sxs-lookup"><span data-stu-id="22fde-109">You can perform the initial replication offline.</span></span>

## <a name="configure-replication-settings"></a><span data-ttu-id="22fde-110">設定複寫設定</span><span class="sxs-lookup"><span data-stu-id="22fde-110">Configure replication settings</span></span>

1. <span data-ttu-id="22fde-111">若要建立新的複寫原則，請按一下 [準備基礎結構] > [複寫設定] > [+建立及關聯]。</span><span class="sxs-lookup"><span data-stu-id="22fde-111">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![網路](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="22fde-113">在 [建立及關聯原則] 中指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="22fde-113">In **Create and associate policy**, specify a policy name.</span></span> <span data-ttu-id="22fde-114">來源和目標類型應該是 **Hyper-V**。</span><span class="sxs-lookup"><span data-stu-id="22fde-114">The source and target type should be **Hyper-V**.</span></span>
3. <span data-ttu-id="22fde-115">在 [Hyper-V 主機版本] 中，選取在主機上執行的作業系統。</span><span class="sxs-lookup"><span data-stu-id="22fde-115">In **Hyper-V host version**, select which operating system is running on the host.</span></span>
4. <span data-ttu-id="22fde-116">在 [驗證類型] 和 [驗證連接埠] 中，指定主要與復原 Hyper-V 主機伺服器之間流量的驗證方式。</span><span class="sxs-lookup"><span data-stu-id="22fde-116">In **Authentication type** and **Authentication port**, specify how traffic is authenticated between the primary and recovery Hyper-V host servers.</span></span> <span data-ttu-id="22fde-117">除非您有有效的 Kerberos 環境，否則請選取 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="22fde-117">Select **Certificate** unless you have a working Kerberos environment.</span></span> <span data-ttu-id="22fde-118">Azure Site Recovery 會自動設定用於 HTTPS 驗證的憑證。</span><span class="sxs-lookup"><span data-stu-id="22fde-118">Azure Site Recovery will automatically configure certificates for HTTPS authentication.</span></span> <span data-ttu-id="22fde-119">您不需要手動執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="22fde-119">You don't need to do anything manually.</span></span> <span data-ttu-id="22fde-120">根據預設，連接埠 8083 和 8084 (用於憑證) 將在 Hyper-V 主機伺服器上的 Windows 防火牆中開啟。</span><span class="sxs-lookup"><span data-stu-id="22fde-120">By default, port 8083 and 8084 (for certificates) will be opened in the Windows Firewall on the Hyper-V host servers.</span></span> <span data-ttu-id="22fde-121">如果您確實選取 [Kerberos]，Kerberos 票證將會用於主機伺服器的相互驗證。</span><span class="sxs-lookup"><span data-stu-id="22fde-121">If you do select **Kerberos**, a Kerberos ticket will be used for mutual authentication of the host servers.</span></span> <span data-ttu-id="22fde-122">請注意，這項設定只有在 Hyper-V 主機伺服器是執行於 Windows Server 2012 R2 時才有重要性。</span><span class="sxs-lookup"><span data-stu-id="22fde-122">Note that this setting is only relevant for Hyper-V host servers running on Windows Server 2012 R2.</span></span>
5. <span data-ttu-id="22fde-123">在 [複製頻率] 中，指定您要在初始複寫後複寫差異資料的頻率 (每隔 30 秒、5 或 15 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="22fde-123">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>
6. <span data-ttu-id="22fde-124">在 [復原點保留] 中，針對每個復原點指定保留週期的長度 (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="22fde-124">In **Recovery point retention**, specify in hours how long the retention window will be for each recovery point.</span></span> <span data-ttu-id="22fde-125">受保護的機器可以復原到週期內的任意點。</span><span class="sxs-lookup"><span data-stu-id="22fde-125">Protected machines can be recovered to any point within a window.</span></span>
7. <span data-ttu-id="22fde-126">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。</span><span class="sxs-lookup"><span data-stu-id="22fde-126">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span> <span data-ttu-id="22fde-127">Hyper-V 使用兩種類型的快照，一個是標準快照，提供整個虛擬機器的增量快照，另一個是應用程式一致快照，會建立虛擬機器內應用程式資料的時間點快照。</span><span class="sxs-lookup"><span data-stu-id="22fde-127">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span> <span data-ttu-id="22fde-128">應用程式一致快照會使用「磁碟區陰影複製服務」(VSS) 來確保建立快照時，應用程式是處於一致狀態。</span><span class="sxs-lookup"><span data-stu-id="22fde-128">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="22fde-129">如果您啟用應用程式一致快照，它會影響在來源虛擬機器上執行的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="22fde-129">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="22fde-130">確認您設定的值低於您設定的其他復原點數目。</span><span class="sxs-lookup"><span data-stu-id="22fde-130">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>
8. <span data-ttu-id="22fde-131">在 [資料傳輸壓縮] 中，指定是否應該將傳輸的已複寫資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="22fde-131">In **Data transfer compression**, specify whether replicated data that is transferred should be compressed.</span></span>
9. <span data-ttu-id="22fde-132">選取 [刪除複本 VM]，以指定如果您停用對來源 VM 的保護，則應刪除複本虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="22fde-132">Select **Delete replica VM**, to specify that the replica virtual machine should be deleted if you disable protection for the source VM.</span></span> <span data-ttu-id="22fde-133">如果啟用此設定，當您停用對來源 VM 的保護時，便會從 Site Recovery 主控台中加以移除、在 VMM 主控台中移除 VMM 的 Site Recovery 設定，並刪除複本。</span><span class="sxs-lookup"><span data-stu-id="22fde-133">If you enable this setting, when you disable protection for the source VM it's removed from the Site Recovery console, Site Recovery settings for the VMM are removed from the VMM console, and the replica is deleted.</span></span>
10. <span data-ttu-id="22fde-134">在 [初始複寫方法] 中，如果您要透過網路進行複寫，請指定是否要啟動初始複寫，或將它排程。</span><span class="sxs-lookup"><span data-stu-id="22fde-134">In **Initial replication method**, if you're replicating over the network, specify whether to start the initial replication or schedule it.</span></span> <span data-ttu-id="22fde-135">若要節省網路頻寬，您可能要將它排程在離峰時間執行。</span><span class="sxs-lookup"><span data-stu-id="22fde-135">To save network bandwidth, you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="22fde-136">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="22fde-136">Then click **OK**.</span></span>

     ![複寫原則](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. <span data-ttu-id="22fde-138">當您建立新的原則時，該原則會自動與 VMM 雲端產生關聯。</span><span class="sxs-lookup"><span data-stu-id="22fde-138">When you create a new policy it's automatically associated with the VMM cloud.</span></span> <span data-ttu-id="22fde-139">在 [複寫原則] 中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="22fde-139">In **Replication policy**, click **OK**.</span></span> <span data-ttu-id="22fde-140">您可以在 [複寫] > 原則名稱 > [關聯 VMM 雲端] 中，將其他 VMM 雲端 (及其中的 VM) 與此複寫原則產生關聯。</span><span class="sxs-lookup"><span data-stu-id="22fde-140">You can associate additional VMM Clouds (and the VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

     ![複寫原則](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a><span data-ttu-id="22fde-142">準備進行離線初始複寫</span><span class="sxs-lookup"><span data-stu-id="22fde-142">Prepare for offline initial replication</span></span>

<span data-ttu-id="22fde-143">您可以針對初始資料複本進行離線複寫。</span><span class="sxs-lookup"><span data-stu-id="22fde-143">You can do offline replication for the initial data copy.</span></span> <span data-ttu-id="22fde-144">您可以如下所示方式進行準備︰</span><span class="sxs-lookup"><span data-stu-id="22fde-144">You can prepare this as follows:</span></span>

* <span data-ttu-id="22fde-145">在來源伺服器上，您會指定要從中匯出資料的路徑位置。</span><span class="sxs-lookup"><span data-stu-id="22fde-145">On the source server, you specify a path location from which the data export will take place.</span></span> <span data-ttu-id="22fde-146">在匯出路徑上指派 NTFS 和共用權限的完整控制權給 VMM 服務。</span><span class="sxs-lookup"><span data-stu-id="22fde-146">Assign Full Control for NTFS and, Share permissions to the VMM service on the export path.</span></span> <span data-ttu-id="22fde-147">在目標伺服器上，您會指定要從中匯入資料的路徑位置。</span><span class="sxs-lookup"><span data-stu-id="22fde-147">On the target server, you specify a path location from which the data import will occur.</span></span> <span data-ttu-id="22fde-148">在這個匯入路徑上指派相同的權限。</span><span class="sxs-lookup"><span data-stu-id="22fde-148">Assign the same permissions on this import path.</span></span>
* <span data-ttu-id="22fde-149">如果共用匯入或匯出路徑，請在共用所在的遠端桌面上，指派系統管理員、進階使用者、列印操作員或伺服器操作員群組成員資格給 VMM 伺服器帳戶。</span><span class="sxs-lookup"><span data-stu-id="22fde-149">If the import or export path is shared, assign Administrator, Power User, Print Operator, or Server Operator group membership for the VMM service account on the remote computer on which the shared is located.</span></span>
* <span data-ttu-id="22fde-150">如果您使用任何執行身分帳戶加入主機，請在匯入和匯出路徑上指派讀取和寫入權限給 VMM 中的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="22fde-150">If you're using any Run As accounts to add hosts, on the import and export paths, assign read and write permissions to the Run As accounts in VMM.</span></span>
* <span data-ttu-id="22fde-151">匯入和匯出共用不得位於任何做為 Hyper-V 主機伺服器的電腦，因為 Hyper-V 不支援回送設定。</span><span class="sxs-lookup"><span data-stu-id="22fde-151">The import and export shares should not be located on any computer used as a Hyper-V host server, because loopback configuration is not supported by Hyper-V.</span></span>
* <span data-ttu-id="22fde-152">在 Active Directory 的每部包含您想要保護之虛擬機器的 Hyper-V 主機伺服器上，啟用與設定限制委派，以信任匯入與匯出路徑所在的遠端電腦，如下所示：</span><span class="sxs-lookup"><span data-stu-id="22fde-152">In Active Directory, on each Hyper-V host server that contains virtual machines you want to protect, enable and configure constrained delegation to trust the remote computers on which the import and export paths are located, as follows:</span></span>
  1. <span data-ttu-id="22fde-153">在網域控制站上，開啟 [Active Directory 使用者和電腦] 。</span><span class="sxs-lookup"><span data-stu-id="22fde-153">On the domain controller, open **Active Directory Users and Computers**.</span></span>
  2. <span data-ttu-id="22fde-154">在主控台樹狀目錄中，按一下 [DomainName] > [電腦]。</span><span class="sxs-lookup"><span data-stu-id="22fde-154">In the console tree, click **DomainName** > **Computers**.</span></span>
  3. <span data-ttu-id="22fde-155">在 Hyper-V 主機伺服器名稱上按一下滑鼠右鍵 > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="22fde-155">Right-click the Hyper-V host server name > **Properties**.</span></span>
  4. <span data-ttu-id="22fde-156">在 [委派] 索引標籤上，按一下 [信任這台電腦，但只委派指定的服務]。</span><span class="sxs-lookup"><span data-stu-id="22fde-156">On the **Delegation** tab, click **Trust this computer for delegation to specified services only**.</span></span>
  5. <span data-ttu-id="22fde-157">按一下 [使用任何驗證通訊協定] 。</span><span class="sxs-lookup"><span data-stu-id="22fde-157">Click **Use any authentication protocol**.</span></span>
  6. <span data-ttu-id="22fde-158">按一下 [新增]  > 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="22fde-158">Click **Add** > **Users and Computers**.</span></span>
  7. <span data-ttu-id="22fde-159">輸入裝載匯出路徑之電腦的名稱 > [確定]。</span><span class="sxs-lookup"><span data-stu-id="22fde-159">Type the name of the computer that hosts the export path > **OK**.</span></span> <span data-ttu-id="22fde-160">從可用服務清單，按住 CTRL 鍵，然後按一下 [cifs] > [確定]。</span><span class="sxs-lookup"><span data-stu-id="22fde-160">From the list of available services, hold down the CTRL key and click **cifs** > **OK**.</span></span> <span data-ttu-id="22fde-161">為裝載匯入路徑的電腦名稱重複動作。</span><span class="sxs-lookup"><span data-stu-id="22fde-161">Repeat for the name of the computer that hosts the import path.</span></span> <span data-ttu-id="22fde-162">視需要為其他 Hyper-V 主機伺服器重複動作。</span><span class="sxs-lookup"><span data-stu-id="22fde-162">Repeat as necessary for additional Hyper-V host servers.</span></span>



## <a name="next-steps"></a><span data-ttu-id="22fde-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22fde-163">Next steps</span></span>

<span data-ttu-id="22fde-164">移至[步驟 9：啟用複寫](vmm-to-vmm-walkthrough-enable-replication.md)。</span><span class="sxs-lookup"><span data-stu-id="22fde-164">Go to [Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>
