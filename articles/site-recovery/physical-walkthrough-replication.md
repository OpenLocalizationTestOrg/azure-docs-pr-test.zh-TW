---
title: "使用 Azure Site Recovery 針對實體伺服器到 Azure 的複寫設定複寫原則 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務將內部部署實體伺服器複寫至 Azure 儲存體時設定複寫原則所需的步驟"
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
ms.openlocfilehash: 9ce23382001b54e7b9b7a58b8dd9aa61b400826d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-to-azure"></a><span data-ttu-id="30cc7-103">步驟 8：針對實體伺服器到 Azure 的複寫設定複寫原則</span><span class="sxs-lookup"><span data-stu-id="30cc7-103">Step 8: Set up a replication policy for physical server replication to Azure</span></span>


<span data-ttu-id="30cc7-104">本文說明在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務將 Windows/Linux 實體伺服器複寫至 Azure 時，如何設定複寫原則。</span><span class="sxs-lookup"><span data-stu-id="30cc7-104">This article describes how to set up a replication policy when you're replicating Windows/Linux physical servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="30cc7-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="30cc7-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="30cc7-106">設定原則</span><span class="sxs-lookup"><span data-stu-id="30cc7-106">Configure a policy</span></span>

1. <span data-ttu-id="30cc7-107">按一下 [Site Recovery 基礎結構] > [複寫原則] > [+複寫原則]。</span><span class="sxs-lookup"><span data-stu-id="30cc7-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="30cc7-108">在 [建立複寫原則]中，指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="30cc7-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="30cc7-109">在 [RPO 臨界值] 中，指定 RPO 限制。</span><span class="sxs-lookup"><span data-stu-id="30cc7-109">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="30cc7-110">這個值表示資料復原點的建立頻率。</span><span class="sxs-lookup"><span data-stu-id="30cc7-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="30cc7-111">連續複寫超過此限制時會產生警示。</span><span class="sxs-lookup"><span data-stu-id="30cc7-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="30cc7-112">在 [復原點保留] 中，指定每個復原點的保留週期長度 (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="30cc7-112">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="30cc7-113">複寫的 VM 可以還原至一個週期內的任何時間點。</span><span class="sxs-lookup"><span data-stu-id="30cc7-113">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="30cc7-114">複寫至進階儲存體的電腦支援最長保留 24 小時，標準儲存體則是 72 小時。</span><span class="sxs-lookup"><span data-stu-id="30cc7-114">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="30cc7-115">在 [應用程式一致快照頻率] 中，指定建立包含應用程式一致快照之復原點的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="30cc7-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="30cc7-116">按一下 [確定]  以建立原則。</span><span class="sxs-lookup"><span data-stu-id="30cc7-116">Click **OK** to create the policy.</span></span>

    ![複寫原則](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="30cc7-118">當您建立新的原則時，該原則會自動與組態伺服器產生關聯。</span><span class="sxs-lookup"><span data-stu-id="30cc7-118">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="30cc7-119">依預設會自動建立容錯回復的比對原則。</span><span class="sxs-lookup"><span data-stu-id="30cc7-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="30cc7-120">例如，如果複寫原則是 **rep-policy**，容錯回復原則便會是 **rep-policy-failback**。</span><span class="sxs-lookup"><span data-stu-id="30cc7-120">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="30cc7-121">從 Azure 起始容錯回復時才會使用此原則。</span><span class="sxs-lookup"><span data-stu-id="30cc7-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30cc7-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30cc7-122">Next steps</span></span>

<span data-ttu-id="30cc7-123">移至[步驟 9：安裝行動服務](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="30cc7-123">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>
