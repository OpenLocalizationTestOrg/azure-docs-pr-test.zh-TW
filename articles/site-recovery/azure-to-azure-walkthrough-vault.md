---
title: "註冊 Azure Site recovery 的區域之間保存庫以 Azure VM repliction aaaSet |Microsoft 文件"
description: "摘要說明您需要保存庫註冊 tooset Azure 之間的複寫使用 Azure Site Recovery 的 Azure 區域的 hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="749a1-103">步驟 4： 設定 Azure tooAzure 複寫保存庫</span><span class="sxs-lookup"><span data-stu-id="749a1-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="749a1-104">之後[規劃網路](azure-to-azure-walkthrough-network.md)，使用 Azure 虛擬機器 (Vm) 的保存庫註冊此發行項 tooset 複寫 tooanother Azure 區域，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="749a1-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="749a1-105">當您完成 hello 發行項時，您應該設定復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="749a1-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="749a1-106">張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="749a1-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="749a1-107">Azure VM 複寫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="749a1-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="749a1-108">建立保存庫</span><span class="sxs-lookup"><span data-stu-id="749a1-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="749a1-109">我們建議您在您想要 Vm tooreplicate hello 位置建立 hello 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="749a1-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="749a1-110">例如，如果您的目標位置是 hello 中央而我們，建立 hello 保存庫中的**美國中部**。</span><span class="sxs-lookup"><span data-stu-id="749a1-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="749a1-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="749a1-111">Next steps</span></span>

<span data-ttu-id="749a1-112">跳過[步驟 5： 啟用複寫](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="749a1-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
