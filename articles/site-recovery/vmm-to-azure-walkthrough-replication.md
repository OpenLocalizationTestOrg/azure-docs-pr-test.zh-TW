---
title: "（使用 VMM) 的 HYPER-V 虛擬機器複寫 tooAzure 與 Azure Site Recovery 的複寫原則 aaaSet |Microsoft 文件"
description: "描述如何 tooset （使用 VMM) 的 HYPER-V 虛擬機器複寫 tooAzure 與 Azure Site Recovery 的複寫原則"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="1d7de-103">步驟 10： 設定 HYPER-V 虛擬機器的複寫 （VMM) tooAzure 的複寫原則</span><span class="sxs-lookup"><span data-stu-id="1d7de-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="1d7de-104">設定好後[網路對應](vmm-to-azure-walkthrough-network-mapping.md)，使用此發行項 tooconfigure 的複寫原則 T\tooreplicate 內部部署 System Center Virtual Machine Manager (VMM) 雲端 tooAzure 中受管理的 HYPER-V 虛擬機器使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="1d7de-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="1d7de-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="1d7de-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="1d7de-106">建立原則</span><span class="sxs-lookup"><span data-stu-id="1d7de-106">Create a policy</span></span>

1. <span data-ttu-id="1d7de-107">toocreate 新的複寫原則，請按一下**準備基礎結構** > **複寫設定** > **+ 建立及關聯**。</span><span class="sxs-lookup"><span data-stu-id="1d7de-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![網路](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="1d7de-109">在 [建立及關聯原則] 中指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="1d7de-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="1d7de-110">在**複製頻率**，指定您在 hello 初始複寫 （每隔 30 秒、 5 或 15 分鐘） 之後要 tooreplicate 差異資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="1d7de-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="1d7de-111">複寫 toopremium 存放裝置時，不支援第二個頻率為 30。</span><span class="sxs-lookup"><span data-stu-id="1d7de-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="1d7de-112">hello 限制取決於 hello 高階儲存體所支援的每個 blob (100) 的快照集數目。</span><span class="sxs-lookup"><span data-stu-id="1d7de-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="1d7de-113">深入了解</span><span class="sxs-lookup"><span data-stu-id="1d7de-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="1d7de-114">在**復原點保留**，以小時為單位指定多久 hello 保留時間將會針對每個復原點。</span><span class="sxs-lookup"><span data-stu-id="1d7de-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="1d7de-115">受保護的電腦可以是復原 tooany 視窗內的點。</span><span class="sxs-lookup"><span data-stu-id="1d7de-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="1d7de-116">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。</span><span class="sxs-lookup"><span data-stu-id="1d7de-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="1d7de-117">HYPER-V 使用兩種類型的快照集，提供 hello 整部虛擬機器的累加快照集的標準快照集和 hello hello 虛擬機器內的應用程式資料的時間點快照的應用程式一致快照集。</span><span class="sxs-lookup"><span data-stu-id="1d7de-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="1d7de-118">應用程式一致快照集會使用應用程式處於一致的狀態時 hello 快照時的磁碟區陰影複製服務 (VSS) tooensure。</span><span class="sxs-lookup"><span data-stu-id="1d7de-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="1d7de-119">請注意，是否您啟用應用程式一致快照集時，它會影響來源虛擬機器上執行的應用程式的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="1d7de-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="1d7de-120">確定您設定的 hello 值小於 hello 您設定其他復原點數目。</span><span class="sxs-lookup"><span data-stu-id="1d7de-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="1d7de-121">在**初始複寫開始時間**，指出當 toostart hello 初始複寫。</span><span class="sxs-lookup"><span data-stu-id="1d7de-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="1d7de-122">hello 發生複寫的網際網路頻寬，您可能會想 tooschedule 它忙碌的時間之外。</span><span class="sxs-lookup"><span data-stu-id="1d7de-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="1d7de-123">在**加密資料儲存在 Azure 上**，指定是否在 Azure 儲存體中的其餘資料 tooencrypt。</span><span class="sxs-lookup"><span data-stu-id="1d7de-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="1d7de-124">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1d7de-124">Then click **OK**.</span></span>

    ![複寫原則](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="1d7de-126">當您建立新的原則會自動對 hello VMM 雲端與其相關。</span><span class="sxs-lookup"><span data-stu-id="1d7de-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="1d7de-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="1d7de-127">Click **OK**.</span></span> <span data-ttu-id="1d7de-128">您可以將其他 VMM 雲端 （和它們的 hello Vm），與在此複寫原則**複寫**> 原則名稱 >**關聯 VMM 雲端**。</span><span class="sxs-lookup"><span data-stu-id="1d7de-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![複寫原則](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="1d7de-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d7de-130">Next steps</span></span>

<span data-ttu-id="1d7de-131">跳過[步驟 11： 啟用複寫](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="1d7de-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
