---
title: "aaaPrepare Azure 資源 tooreplicate 內部部署 VMware Vm tooAzure 使用 Azure Site Recovery |Microsoft 文件"
description: "說明您需要在 Azure 中的位置開始複寫在內部部署 VMware Vm tooAzure 使用 Azure Site Recovery 之前"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ac72fff0593783add789408ecfeb1812d70108b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-tooazure"></a><span data-ttu-id="d03e4-103">步驟 5： 準備 VMWare 複寫 tooAzure Azure 資源</span><span class="sxs-lookup"><span data-stu-id="d03e4-103">Step 5: Prepare Azure resources for VMWare replication tooAzure</span></span>


<span data-ttu-id="d03e4-104">使用此發行項 tooprepare Azure hello 指示資源，以便您可以將複寫在內部部署機器 tooAzure 使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="d03e4-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises machines tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="d03e4-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d03e4-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="d03e4-106">Before you start</span></span>

<span data-ttu-id="d03e4-107">請確定您已閱讀 hello[必要條件](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="d03e4-107">Make sure you've read hello [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="d03e4-108">設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="d03e4-108">Set up an Azure account</span></span>

- <span data-ttu-id="d03e4-109">取得 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="d03e4-110">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="d03e4-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="d03e4-111">檢查網站復原，在各地區上市中支援的 hello 區域[Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="d03e4-112">深入了解[站台復原定價](site-recovery-faq.md#pricing)，並取得 hello[定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="d03e4-113">設定 Azure 網路</span><span class="sxs-lookup"><span data-stu-id="d03e4-113">Set up an Azure network</span></span>

- <span data-ttu-id="d03e4-114">設定 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="d03e4-114">Set up an Azure network.</span></span> <span data-ttu-id="d03e4-115">在容錯移轉之後建立的 Azure VM 會置於這個網路。</span><span class="sxs-lookup"><span data-stu-id="d03e4-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="d03e4-116">站台復原 hello Azure 入口網站中的可以使用在中設定網路[資源管理員](../resource-manager-deployment-model.md)，或以傳統模式。</span><span class="sxs-lookup"><span data-stu-id="d03e4-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="d03e4-117">hello 網路應位於 hello hello 與相同的區域復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="d03e4-117">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="d03e4-118">深入了解[虛擬網路定價](https://azure.microsoft.com/pricing/details/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="d03e4-119">深入了解容錯移轉後的 [Azure VM 連線](site-recovery-network-design.md)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="d03e4-120">設定 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d03e4-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="d03e4-121">Site Recovery 會複寫在內部部署機器 tooAzure 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="d03e4-121">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="d03e4-122">容錯移轉發生後，會建立 hello 儲存體從 azure Vm。</span><span class="sxs-lookup"><span data-stu-id="d03e4-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="d03e4-123">為複寫的資料設定 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="d03e4-124">站台復原 hello Azure 入口網站中的可以使用資源管理員 中，或在傳統模式中設定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d03e4-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="d03e4-125">hello 儲存體帳戶可以是標準或[premium](../storage/common/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="d03e4-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="d03e4-126">如果您設定的是進階帳戶，則也需要一個額外的標準帳戶來記錄資料。</span><span class="sxs-lookup"><span data-stu-id="d03e4-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d03e4-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d03e4-127">Next steps</span></span>

<span data-ttu-id="d03e4-128">跳過[步驟 6： 準備 VMware 資源](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="d03e4-128">Go too[Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
