---
title: "使用 Azure Site Recovery 設定將 Hyper-V (不含 System Center VMM) 複寫至 Azure 的保存庫 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 設定將 Hyper-V 複寫至 Azure 的保存庫所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 8212ff011633c3a89d3310e828b6d5f1cda6ce3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="942f7-103">步驟 7：設定 Hyper-V 複寫的保存庫</span><span class="sxs-lookup"><span data-stu-id="942f7-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="942f7-104">本文說明如何使用 Azure 入口網站中的 [Azure Site Recovery](site-recovery-overview.md) 服務來設定保存庫，並指定要從內部部署位置複寫到 Azure 的項目。</span><span class="sxs-lookup"><span data-stu-id="942f7-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="942f7-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="942f7-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="942f7-106">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="942f7-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="942f7-107">選取保護目標</span><span class="sxs-lookup"><span data-stu-id="942f7-107">Select a protection goal</span></span>

<span data-ttu-id="942f7-108">選取您要複寫的項目以及您要複寫到的位置。</span><span class="sxs-lookup"><span data-stu-id="942f7-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="942f7-109">按一下 [復原服務保存庫] > 保存庫。</span><span class="sxs-lookup"><span data-stu-id="942f7-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="942f7-110">在 [資源功能表] 中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="942f7-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="942f7-111">在 [保護目標] 中，選取 [至 Azure] > [是，利用 Hyper-V]。</span><span class="sxs-lookup"><span data-stu-id="942f7-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="942f7-112">選取 [否]  以確認您未使用 VMM。</span><span class="sxs-lookup"><span data-stu-id="942f7-112">Select **No** to confirm you're not using VMM.</span></span> 

    ![選擇目標](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="942f7-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="942f7-114">Next steps</span></span>

<span data-ttu-id="942f7-115">移至[步驟 8：設定來源和目標](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="942f7-115">Go to [Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
