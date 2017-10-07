---
title: "實體伺服器複寫 tooAzure 與 Azure Site Recovery 的複寫原則 aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟時複寫在內部部署實體伺服器 tooAzure 儲存體使用 hello Azure Site Recovery 服務，您會需要 tooset 複寫原則"
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="60b14-103">步驟 8： 設定實體伺服器複寫 tooAzure 的複寫原則</span><span class="sxs-lookup"><span data-stu-id="60b14-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="60b14-104">本文說明如何建立複寫原則，當您要複寫 Windows/Linux 實體伺服器 tooAzure 使用 hello tooset [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="60b14-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="60b14-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="60b14-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="60b14-106">設定原則</span><span class="sxs-lookup"><span data-stu-id="60b14-106">Configure a policy</span></span>

1. <span data-ttu-id="60b14-107">按一下 [Site Recovery 基礎結構] > [複寫原則] > [+複寫原則]。</span><span class="sxs-lookup"><span data-stu-id="60b14-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="60b14-108">在 [建立複寫原則]中，指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="60b14-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="60b14-109">在**RPO 臨界值**，指定 hello RPO 上限。</span><span class="sxs-lookup"><span data-stu-id="60b14-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="60b14-110">這個值表示資料復原點的建立頻率。</span><span class="sxs-lookup"><span data-stu-id="60b14-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="60b14-111">連續複寫超過此限制時會產生警示。</span><span class="sxs-lookup"><span data-stu-id="60b14-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="60b14-112">在**復原點保留**，指定時間長度 （以小時為單位） hello 保留週期是每個復原點。</span><span class="sxs-lookup"><span data-stu-id="60b14-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="60b14-113">複寫的 Vm 就能復原 tooany 點視窗中的。</span><span class="sxs-lookup"><span data-stu-id="60b14-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="60b14-114">向上 too24 小時保留支援機器複寫 toopremium 儲存體和標準儲存體 72 小時的時間。</span><span class="sxs-lookup"><span data-stu-id="60b14-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="60b14-115">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="60b14-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="60b14-116">按一下**確定**toocreate hello 原則。</span><span class="sxs-lookup"><span data-stu-id="60b14-116">Click **OK** toocreate hello policy.</span></span>

    ![複寫原則](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="60b14-118">當您建立新的原則會自動對 hello 組態伺服器與其相關。</span><span class="sxs-lookup"><span data-stu-id="60b14-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="60b14-119">依預設會自動建立容錯回復的比對原則。</span><span class="sxs-lookup"><span data-stu-id="60b14-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="60b14-120">例如，如果 hello 複寫原則是**rep 原則**hello 容錯回復原則將會**容錯原則 rep 回復**。</span><span class="sxs-lookup"><span data-stu-id="60b14-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="60b14-121">從 Azure 起始容錯回復時才會使用此原則。</span><span class="sxs-lookup"><span data-stu-id="60b14-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60b14-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="60b14-122">Next steps</span></span>

<span data-ttu-id="60b14-123">跳過[步驟 9： 安裝 hello 行動服務](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="60b14-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
