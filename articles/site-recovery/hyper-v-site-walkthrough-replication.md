---
title: "使用 Azure Site Recovery 設定將 Hyper-V VM (不含 System Center VMM) 複寫至 Azure 的複寫原則 | Microsoft Docs"
description: "摘要說明您在將 Hyper-V VM 複寫至 Azure 儲存體時，設定複寫原則所需的步驟"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: ca5bec5cf1152e6259b9fe7a869edd2d62b88e1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-to-azure"></a><span data-ttu-id="84381-103">步驟 9：設定 Hyper-V VM 複寫至 Azure 的複寫原則</span><span class="sxs-lookup"><span data-stu-id="84381-103">Step 9: Set up a replication policy for Hyper-V VM replication to Azure</span></span>

<span data-ttu-id="84381-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，在您要將 Hyper-V VM 複寫至 Azure (不含 System Center VMM) 時設定複寫原則。</span><span class="sxs-lookup"><span data-stu-id="84381-104">This article describes how to set up a replication policy when you're replicating Hyper-V VMs to Azure (without System Center VMM) using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="84381-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="84381-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="84381-106">關於快照集</span><span class="sxs-lookup"><span data-stu-id="84381-106">About snapshots</span></span>

<span data-ttu-id="84381-107">Hyper-V 使用兩種類型的快照，一個是標準快照，提供整個虛擬機器的增量快照，另一個是應用程式一致快照，會建立虛擬機器內應用程式資料的時間點快照。</span><span class="sxs-lookup"><span data-stu-id="84381-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span>
    - <span data-ttu-id="84381-108">應用程式一致快照會使用「磁碟區陰影複製服務」(VSS) 來確保建立快照時，應用程式是處於一致狀態。</span><span class="sxs-lookup"><span data-stu-id="84381-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span>
    - <span data-ttu-id="84381-109">如果您啟用應用程式一致快照，它會影響在來源虛擬機器上執行的應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="84381-109">If you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="84381-110">確認您設定的值低於您設定的其他復原點數目。</span><span class="sxs-lookup"><span data-stu-id="84381-110">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="84381-111">設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="84381-111">Set up a replication policy</span></span>

1. <span data-ttu-id="84381-112">若要建立新的複寫原則，請按一下 [準備基礎結構] > [複寫設定] > [+建立及關聯]。</span><span class="sxs-lookup"><span data-stu-id="84381-112">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![網路](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="84381-114">在 [建立及關聯原則] 中指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="84381-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="84381-115">在 [複製頻率] 中，指定您要在初始複寫後複寫差異資料的頻率 (每隔 30 秒、5 或 15 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="84381-115">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="84381-116">複寫到進階儲存體時，不支援 30 秒的頻率。</span><span class="sxs-lookup"><span data-stu-id="84381-116">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="84381-117">限制取決於進階儲存體所支援之每 blob (100) 的快照集數目。</span><span class="sxs-lookup"><span data-stu-id="84381-117">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="84381-118">[深入了解](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)。</span><span class="sxs-lookup"><span data-stu-id="84381-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="84381-119">在 [復原點保留] 中，指定每個復原點的保留週期長度 (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="84381-119">In **Recovery point retention**, specify in hours how long the retention window is for each recovery point.</span></span> <span data-ttu-id="84381-120">VM 可以復原到週期內的任意點。</span><span class="sxs-lookup"><span data-stu-id="84381-120">VMs can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="84381-121">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (1-12 小時)。</span><span class="sxs-lookup"><span data-stu-id="84381-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="84381-122">在 [初始複寫開始時間]  中，指定開始初始複寫的時間。</span><span class="sxs-lookup"><span data-stu-id="84381-122">In **Initial replication start time**, specify when to start the initial replication.</span></span> <span data-ttu-id="84381-123">複寫會透過您的網際網路頻寬發生，所以您可能想將它排程在忙碌時間之外。</span><span class="sxs-lookup"><span data-stu-id="84381-123">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span> <span data-ttu-id="84381-124">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="84381-124">Then click **OK**.</span></span>

    ![複寫原則](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="84381-126">當您建立新的原則時，該原則會自動與 Hyper-V 網站產生關聯。</span><span class="sxs-lookup"><span data-stu-id="84381-126">When you create a new policy, it's automatically associated with the Hyper-V site.</span></span> <span data-ttu-id="84381-127">您可以在 [複寫] > 原則名稱 > [關聯 Hyper-V 網站] 中，將 Hyper-V 網站 (及其中的 VM) 與多個複寫原則建立關聯。</span><span class="sxs-lookup"><span data-stu-id="84381-127">You can associate a Hyper-V site (and the VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="84381-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84381-128">Next steps</span></span>

<span data-ttu-id="84381-129">移至[步驟 10：啟用複寫](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="84381-129">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
