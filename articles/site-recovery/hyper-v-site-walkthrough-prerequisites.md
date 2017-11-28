---
title: "HYPER-V tooAzure 複寫 （不含 System Center VMM) 使用 Azure Site Recovery 的 aaaReview hello 必要條件 |Microsoft 文件"
description: "說明用於設定複寫、 容錯移轉和復原的內部部署 HYPER-V Vm tooAzure 與 Azure Site Recovery 的 hello 必要條件"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="ebbe2-103">步驟 2： 檢閱 HYPER-V （無 VMM) tooAzure 複寫 hello 必要條件</span><span class="sxs-lookup"><span data-stu-id="ebbe2-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="ebbe2-104">hello 表中摘要說明 hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="ebbe2-105">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="ebbe2-105">**Prerequisite**</span></span> | <span data-ttu-id="ebbe2-106">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="ebbe2-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="ebbe2-107">**Azure**</span><span class="sxs-lookup"><span data-stu-id="ebbe2-107">**Azure**</span></span> | <span data-ttu-id="ebbe2-108">了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="ebbe2-109">**內部部署伺服器**</span><span class="sxs-lookup"><span data-stu-id="ebbe2-109">**On-premises servers**</span></span> | <span data-ttu-id="ebbe2-110">[進一步了解](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm)關於 hello 在內部部署 HYPER-V 主機的需求。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="ebbe2-111">**內部部署 Hyper-V VM**</span><span class="sxs-lookup"><span data-stu-id="ebbe2-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="ebbe2-112">您想要 tooreplicate 應執行的 Vm[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，而且必須符合與[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="ebbe2-113">**Azure URL**</span><span class="sxs-lookup"><span data-stu-id="ebbe2-113">**Azure URLs**</span></span> | <span data-ttu-id="ebbe2-114">HYPER-V 主機需要存取 toothese Url:</span><span class="sxs-lookup"><span data-stu-id="ebbe2-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="ebbe2-115">如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="ebbe2-116">允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)，和 hello HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="ebbe2-117">允許的 IP 位址範圍 hello Azure 區域，您的訂用帳戶，以及美國西部 （用於存取控制與身分識別管理）。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="ebbe2-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebbe2-118">Next steps</span></span>

- <span data-ttu-id="ebbe2-119">如果您進行完整部署，請移至太[步驟 3： 規劃容量](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="ebbe2-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="ebbe2-120">如果您所做的簡單測試部署，請移至太[步驟 4： 規劃網路](hyper-v-site-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="ebbe2-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
