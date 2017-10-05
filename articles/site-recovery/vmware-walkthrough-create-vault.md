---
title: "使用 Azure Site Recovery 針對 VMware 到 Azure 的複寫設定保存庫 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 針對 VMware 到 Azure 的複寫設定保存庫時所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dca95ad46b8de587140c3573ba6ed5702a122032
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-to-azure"></a><span data-ttu-id="74c6b-103">步驟 7：針對 VMware 到 Azure 的複寫設定保存庫</span><span class="sxs-lookup"><span data-stu-id="74c6b-103">Step 7: Set up a vault for VMware replication to Azure</span></span>


<span data-ttu-id="74c6b-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務來設定保存庫，並指定要將哪些項目從內部部署位置複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="74c6b-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="74c6b-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="74c6b-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="74c6b-106">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="74c6b-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="74c6b-107">選取保護目標</span><span class="sxs-lookup"><span data-stu-id="74c6b-107">Select a protection goal</span></span>

<span data-ttu-id="74c6b-108">選取您要複寫的項目以及您要複寫到的位置。</span><span class="sxs-lookup"><span data-stu-id="74c6b-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="74c6b-109">按一下 [復原服務保存庫] > 保存庫。</span><span class="sxs-lookup"><span data-stu-id="74c6b-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="74c6b-110">在 [資源] 功能表中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="74c6b-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="74c6b-111">在 [保護目標] 中選取 [至 Azure] > [是，使用 VMware vSphere Hypervisor]。</span><span class="sxs-lookup"><span data-stu-id="74c6b-111">In **Protection goal**, select **To Azure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="74c6b-112">後續步驟</span><span class="sxs-lookup"><span data-stu-id="74c6b-112">Next steps</span></span>

<span data-ttu-id="74c6b-113">移至[步驟 8：設定來源和目標](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="74c6b-113">Go to [Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
