---
title: "使用 Azure Site Recovery aaaPrepare Azure 資源 tooreplicate （使用 System Center VMM) 的 HYPER-V Vm tooAzure |Microsoft 文件"
description: "說明您需要在 Azure 中的位置開始之前複寫 （使用 VMM) 的 HYPER-V Vm tooAzure 使用 Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1568bdc3-e767-477b-b040-f13699ab5644
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 86bfbab7722fe5bd5b93b92e398d1d441505d3b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="af3d6-103">步驟 5： 準備 HYPER-V 複寫 （VMM) tooAzure Azure 資源</span><span class="sxs-lookup"><span data-stu-id="af3d6-103">Step 5: Prepare Azure resources for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="af3d6-104">在確認之後[網路需求](vmm-to-azure-walkthrough-network.md)，使用此發行項 tooprepare Azure hello 指示資源，以便您可以將複寫在內部部署 HYPER-V Vm 中 System Center Virtual Machine Manager (VMM) 雲端 tooAzure，使用hello [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="af3d6-104">After verifying [network requirements](vmm-to-azure-walkthrough-network.md), use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="af3d6-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或詢問技術問題上 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-an-azure-account"></a><span data-ttu-id="af3d6-106">設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="af3d6-106">Set up an Azure account</span></span>

- <span data-ttu-id="af3d6-107">取得 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-107">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="af3d6-108">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="af3d6-108">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="af3d6-109">檢查網站復原，在各地區上市中支援的 hello 區域[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-109">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="af3d6-110">深入了解[站台復原定價](site-recovery-faq.md#pricing)，並取得 hello[定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-110">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="af3d6-111">請確定您的 Azure 帳戶具有正確的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="af3d6-111">Make sure your Azure account has hello correct [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure VMs.</span></span> <span data-ttu-id="af3d6-112">[深入了解](../active-directory/role-based-access-built-in-roles.md) Azure 角色型存取控制。</span><span class="sxs-lookup"><span data-stu-id="af3d6-112">[Learn more](../active-directory/role-based-access-built-in-roles.md) about Azure role-based access control.</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="af3d6-113">設定 Azure 網路</span><span class="sxs-lookup"><span data-stu-id="af3d6-113">Set up an Azure network</span></span>

- <span data-ttu-id="af3d6-114">設定 [Azure 網路](../virtual-network/virtual-network-get-started-vnet-subnet.md)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-114">Set up an [Azure network](../virtual-network/virtual-network-get-started-vnet-subnet.md).</span></span> <span data-ttu-id="af3d6-115">在容錯移轉之後建立的 Azure VM 會置於這個網路。</span><span class="sxs-lookup"><span data-stu-id="af3d6-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="af3d6-116">hello 網路應位於 hello hello 與相同的區域復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="af3d6-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="af3d6-117">站台復原 hello Azure 入口網站中的可以使用在中設定網路[資源管理員](../resource-manager-deployment-model.md)，或以傳統模式。</span><span class="sxs-lookup"><span data-stu-id="af3d6-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="af3d6-118">建議您在開始之前先設定網路。</span><span class="sxs-lookup"><span data-stu-id="af3d6-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="af3d6-119">如果沒有，您需要 toodo Site Recovery 部署期間它。</span><span class="sxs-lookup"><span data-stu-id="af3d6-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="af3d6-120">深入了解[虛擬網路定價](https://azure.microsoft.com/pricing/details/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="af3d6-121">設定 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="af3d6-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="af3d6-122">Site Recovery 會複寫在內部部署機器 tooAzure 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="af3d6-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="af3d6-123">容錯移轉發生後，會建立 hello 儲存體從 azure Vm。</span><span class="sxs-lookup"><span data-stu-id="af3d6-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="af3d6-124">設定標準/優質[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)toohold 資料複寫 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="af3d6-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="af3d6-125">[高階儲存體](../storage/common/storage-premium-storage.md)通常用於需要一直居高 IO 效能和低度延遲 toohost IO 密集工作負載的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="af3d6-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="af3d6-126">如果您想要 toouse premium 帳戶 toostore 複寫的資料，您也需要標準儲存體帳戶 toostore 複寫記錄檔擷取進行中變更 tooon 內部部署資料。</span><span class="sxs-lookup"><span data-stu-id="af3d6-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="af3d6-127">Hello 資源模型，根據您想 toouse 容錯移轉 Azure Vm，您在設定帳戶[Resource Manager 模式](../storage/common/storage-create-storage-account.md)，或[傳統模式](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="af3d6-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="af3d6-128">建議您在開始之前先設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="af3d6-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="af3d6-129">如果您需要 toodo Site Recovery 部署期間它。</span><span class="sxs-lookup"><span data-stu-id="af3d6-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="af3d6-130">hello 帳戶必須在 hello 與 hello 相同區域復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="af3d6-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="af3d6-131">儲存體帳戶之間所使用的站台復原 hello 內的資源群組相同，則無法移動訂用帳戶，或跨不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="af3d6-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="af3d6-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af3d6-132">Next steps</span></span>

<span data-ttu-id="af3d6-133">跳過[步驟 6： 準備 VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="af3d6-133">Go too[Step 6: Prepare VMM](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>
