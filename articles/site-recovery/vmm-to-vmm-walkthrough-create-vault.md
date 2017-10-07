---
title: "aaaCreate HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery 保存庫 |Microsoft 文件"
description: "描述如何 toocreate 保存庫時複寫 HYPER-V Vm tooa 次要 System Center VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="47c22-103">步驟 5： 建立 HYPER-V 複寫 tooa 次要站台的保存庫</span><span class="sxs-lookup"><span data-stu-id="47c22-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="47c22-104">準備內部部署之後[System Center Virtual Machine Manager (VMM) 伺服器和 HYPER-V 主機叢集](vmm-to-vmm-walkthrough-vmm-hyper-v.md)HYPER-V 複寫 tooa 次要站台使用[Azure Site Recovery](site-recovery-overview.md)，您可以建立復原服務保存庫，並選取 hello 複寫案例。</span><span class="sxs-lookup"><span data-stu-id="47c22-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="47c22-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="47c22-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="47c22-106">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="47c22-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="47c22-107">選擇保護目標</span><span class="sxs-lookup"><span data-stu-id="47c22-107">Choose a protection goal</span></span>

<span data-ttu-id="47c22-108">選取您想要 tooreplicate 和您想要 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="47c22-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="47c22-109">按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="47c22-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="47c22-110">選取**toorecovery 網站**，然後選取**是的含 HYPER-V**。</span><span class="sxs-lookup"><span data-stu-id="47c22-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="47c22-111">選取**是**tooindicate 您使用 VMM toomanage hello HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="47c22-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="47c22-112">如果您有次要 VMM 伺服器，請選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="47c22-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="47c22-113">如果您要在單一 VMM 伺服器上的雲端之間部署複寫，請按一下 [否] 。</span><span class="sxs-lookup"><span data-stu-id="47c22-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="47c22-114">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="47c22-114">Then click **OK**.</span></span>

    ![選擇目標](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="47c22-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47c22-116">Next steps</span></span>

<span data-ttu-id="47c22-117">跳過[步驟 6： 設定 hello 複寫來源和目標](vmm-to-vmm-walkthrough-source-target.md)。</span><span class="sxs-lookup"><span data-stu-id="47c22-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
