---
title: "HYPER-V 複寫 （搭配 System Center VMM) tooAzure 使用 Azure Site Recovery 保存庫註冊 aaaSet |Microsoft 文件"
description: "摘要說明您需要 HYPER-V 複寫 （VMM) tooAzure 使用 Azure Site Recovery 保存庫註冊 tooset hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="a7c96-103">步驟 7：設定 Hyper-V 複寫的保存庫</span><span class="sxs-lookup"><span data-stu-id="a7c96-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="a7c96-104">本文說明如何 tooset 保存庫，並指定您想要從您的內部部署位置，使用 hello tooAzure tooreplicate [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="a7c96-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="a7c96-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="a7c96-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a7c96-106">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="a7c96-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="a7c96-107">選取保護目標</span><span class="sxs-lookup"><span data-stu-id="a7c96-107">Select a protection goal</span></span>

<span data-ttu-id="a7c96-108">選取您想 tooreplicate，而且想要 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="a7c96-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="a7c96-109">按一下 [復原服務保存庫] > 保存庫。</span><span class="sxs-lookup"><span data-stu-id="a7c96-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="a7c96-110">在 hello 資源功能表上，按一下  **Site Recovery** > **準備基礎結構** > **保護目標**。</span><span class="sxs-lookup"><span data-stu-id="a7c96-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="a7c96-111">在**保護目標**，選取**tooAzure** > **是的含 HYPER-V**。</span><span class="sxs-lookup"><span data-stu-id="a7c96-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="a7c96-112">選取**是**tooconfirm 您 nusing VMM。</span><span class="sxs-lookup"><span data-stu-id="a7c96-112">Select **Yes** tooconfirm you're nusing VMM.</span></span> 

     ![選擇目標](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="a7c96-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7c96-114">Next steps</span></span>

<span data-ttu-id="a7c96-115">跳過[步驟 8： 設定來源和目標](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="a7c96-115">Go too[Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
