---
title: "aaaPrepare HYPER-V 裝載 （不含 System Center VMM) 複寫 tooAzure |Microsoft 文件"
description: "描述如何 tooprepare HYPER-V 裝載的複寫 tooAzure 使用 Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="7016d-103">步驟 6： 準備 HYPER-V 主機複寫 tooAzure</span><span class="sxs-lookup"><span data-stu-id="7016d-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="7016d-104">使用此發行項 tooprepare 在內部部署 HYPER-V 主機 toointeract 與 Azure Site Recovery hello 指示。</span><span class="sxs-lookup"><span data-stu-id="7016d-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="7016d-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="7016d-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="7016d-106">準備主機</span><span class="sxs-lookup"><span data-stu-id="7016d-106">Prepare hosts</span></span>

- <span data-ttu-id="7016d-107">請確定 hello HYPER-V 主機符合 hello[必要條件](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm)。</span><span class="sxs-lookup"><span data-stu-id="7016d-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="7016d-108">請確定 hello 主機可存取所需的 hello Url:</span><span class="sxs-lookup"><span data-stu-id="7016d-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="7016d-109">如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="7016d-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="7016d-110">允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="7016d-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="7016d-111">允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。</span><span class="sxs-lookup"><span data-stu-id="7016d-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="7016d-112">Site Recovery 部署期間，您可以加入包含您想要 tooreplicate tooa HYPER-V 站台 Vm 的 HYPER-V 主機。</span><span class="sxs-lookup"><span data-stu-id="7016d-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="7016d-113">hello 站台復原提供者，以及復原服務代理程式會安裝在每部主機上。</span><span class="sxs-lookup"><span data-stu-id="7016d-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="7016d-114">在 hello 復原服務保存庫中註冊 hello HYPER-V 站台。</span><span class="sxs-lookup"><span data-stu-id="7016d-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7016d-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7016d-115">Next steps</span></span>

<span data-ttu-id="7016d-116">跳過[步驟 7： 建立保存庫](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="7016d-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

