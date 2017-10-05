---
title: "使用 Azure Site Recovery 針對實體伺服器到 Azure 的複寫設定保存庫 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 來設定保存庫以將實體伺服器複寫至 Azure 時所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="7869a-103">步驟 6：針對實體伺服器到 Azure 的複寫設定保存庫</span><span class="sxs-lookup"><span data-stu-id="7869a-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="7869a-104">本文說明如何設定保存庫。</span><span class="sxs-lookup"><span data-stu-id="7869a-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="7869a-105">您將在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務來建立保存庫，並指定要將哪些項目從內部部署位置複寫到 Azure。</span><span class="sxs-lookup"><span data-stu-id="7869a-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="7869a-106">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="7869a-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7869a-107">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="7869a-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="7869a-108">選取保護目標</span><span class="sxs-lookup"><span data-stu-id="7869a-108">Select a protection goal</span></span>

<span data-ttu-id="7869a-109">選取您要複寫的項目以及您要複寫到的位置。</span><span class="sxs-lookup"><span data-stu-id="7869a-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="7869a-110">按一下 [復原服務保存庫] > 保存庫。</span><span class="sxs-lookup"><span data-stu-id="7869a-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="7869a-111">在 [資源] 功能表中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="7869a-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="7869a-112">在 [保護目標] 中，選取 [至 Azure] > [未虛擬化/其他]。</span><span class="sxs-lookup"><span data-stu-id="7869a-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7869a-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7869a-113">Next steps</span></span>

<span data-ttu-id="7869a-114">移至[步驟 7：設定來源和目標](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="7869a-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
