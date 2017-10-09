---
title: "VMware VM 複寫 tooAzure 與 Azure Site Recovery 的複寫原則 aaaSet |Microsoft 文件"
description: "摘要說明複寫 VMware Vm tooAzure 儲存體時，需要建立複寫原則 tooset hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="bfc19-103">步驟 9： 設定 VMware VM 複寫 tooAzure 的複寫原則</span><span class="sxs-lookup"><span data-stu-id="bfc19-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="bfc19-104">本文說明如何建立複寫原則，當您要複寫使用 hello 的 VMware Vm tooAzure tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="bfc19-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="bfc19-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="bfc19-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="bfc19-106">設定原則</span><span class="sxs-lookup"><span data-stu-id="bfc19-106">Configure a policy</span></span>

<span data-ttu-id="bfc19-107">在開始之前，請透過影片快速建立概念︰</span><span class="sxs-lookup"><span data-stu-id="bfc19-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="bfc19-108">toocreate 新的複寫原則，請按一下**Site Recovery 基礎結構** > **複寫原則** > **+ 複寫原則**。</span><span class="sxs-lookup"><span data-stu-id="bfc19-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="bfc19-109">在 [建立複寫原則]中，指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="bfc19-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="bfc19-110">在**RPO 臨界值**，指定 hello RPO 上限。</span><span class="sxs-lookup"><span data-stu-id="bfc19-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="bfc19-111">這個值指定資料復原點的建立頻率。</span><span class="sxs-lookup"><span data-stu-id="bfc19-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="bfc19-112">連續複寫超過此限制時會產生警示。</span><span class="sxs-lookup"><span data-stu-id="bfc19-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="bfc19-113">在**復原點保留**，指定時間長度 （以小時為單位） hello 保留週期是每個復原點。</span><span class="sxs-lookup"><span data-stu-id="bfc19-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="bfc19-114">複寫的 Vm 就能復原 tooany 點視窗中的。</span><span class="sxs-lookup"><span data-stu-id="bfc19-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="bfc19-115">向上 too24 小時保留支援機器複寫 toopremium 儲存體和標準儲存體 72 小時的時間。</span><span class="sxs-lookup"><span data-stu-id="bfc19-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="bfc19-116">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="bfc19-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="bfc19-117">按一下**確定**toocreate hello 原則。</span><span class="sxs-lookup"><span data-stu-id="bfc19-117">Click **OK** toocreate hello policy.</span></span>

    ![複寫原則](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="bfc19-119">當您建立新的原則會自動對 hello 組態伺服器與其相關。</span><span class="sxs-lookup"><span data-stu-id="bfc19-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="bfc19-120">依預設會自動建立容錯回復的比對原則。</span><span class="sxs-lookup"><span data-stu-id="bfc19-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="bfc19-121">例如，如果 hello 複寫原則是**rep 原則**hello 容錯回復原則將會**容錯原則 rep 回復**。</span><span class="sxs-lookup"><span data-stu-id="bfc19-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="bfc19-122">從 Azure 起始容錯回復時才會使用此原則。</span><span class="sxs-lookup"><span data-stu-id="bfc19-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfc19-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bfc19-123">Next steps</span></span>

<span data-ttu-id="bfc19-124">跳過[步驟 10： 安裝 hello 行動服務](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="bfc19-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
