---
title: "使用 Azure Site Recovery 準備 Azure 資源將 Hyper-V VM (不含 System Center VMM) 複寫至 Azure | Microsoft Docs"
description: "說明您在使用 Azure Site Recovery 開始將 Hyper-V VM (不含 VMM) 複寫至 Azure 之前，在 Azure 中需要的項目"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="06db5-103">步驟 5：準備要將 Hyper-V 複寫至 Azure 的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="06db5-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="06db5-104">使用本文章中的指示來準備 Azure 資源，讓您可以使用 [Azure Site Recovery](site-recovery-overview.md) 服務，將內部部署 Hyper-V VM (不含 System Center VMM) 複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="06db5-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="06db5-105">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="06db5-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="06db5-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="06db5-106">Before you start</span></span>

<span data-ttu-id="06db5-107">確認您已閱讀[必要條件](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="06db5-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="06db5-108">設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="06db5-108">Set up an Azure account</span></span>

- <span data-ttu-id="06db5-109">取得 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="06db5-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="06db5-110">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="06db5-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="06db5-111">在 [Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)的＜各地區上市情況＞底下，查看 Site Recovery 的支援地區。</span><span class="sxs-lookup"><span data-stu-id="06db5-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="06db5-112">了解 [Site Recovery 定價](site-recovery-faq.md#pricing)，並取得[定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="06db5-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="06db5-113">設定 Azure 網路</span><span class="sxs-lookup"><span data-stu-id="06db5-113">Set up an Azure network</span></span>

- <span data-ttu-id="06db5-114">設定 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="06db5-114">Set up an Azure network.</span></span> <span data-ttu-id="06db5-115">在容錯移轉之後建立的 Azure VM 會置於這個網路。</span><span class="sxs-lookup"><span data-stu-id="06db5-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="06db5-116">此網路應位於與復原服務保存庫相同的區域</span><span class="sxs-lookup"><span data-stu-id="06db5-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="06db5-117">Azure 入口網站的 Site Recovery 可以在 [Resource Manager](../resource-manager-deployment-model.md) 中，或以傳統模式使用網路設定。</span><span class="sxs-lookup"><span data-stu-id="06db5-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="06db5-118">建議您在開始之前先設定網路。</span><span class="sxs-lookup"><span data-stu-id="06db5-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="06db5-119">若非如此，則必須在 Site Recovery 部署期間這麼做。</span><span class="sxs-lookup"><span data-stu-id="06db5-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="06db5-120">深入了解[虛擬網路定價](https://azure.microsoft.com/pricing/details/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="06db5-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="06db5-121">設定 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="06db5-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="06db5-122">Site Recovery 會將內部部署機器複寫至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="06db5-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="06db5-123">容錯移轉發生後，會從儲存體建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="06db5-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="06db5-124">設定標準/進階 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)來保存複寫到 Azure 的資料。</span><span class="sxs-lookup"><span data-stu-id="06db5-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="06db5-125">[進階儲存體](../storage/common/storage-premium-storage.md)通常是用於需要持續高 IO 效能和低延遲性以裝載 IO 密集型工作負載的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="06db5-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="06db5-126">如果您想要使用進階帳戶來儲存複寫的資料，就也需要標準儲存體帳戶來儲存複寫記錄檔，這些記錄檔會擷取內部部署資料的進行中變更。</span><span class="sxs-lookup"><span data-stu-id="06db5-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="06db5-127">視您想要針對已容錯移轉的 Azure VM 使用的資源模型而定，您會以 [Resource Manager 模式](../storage/common/storage-create-storage-account.md)，或[傳統模式](../storage/common/storage-create-storage-account.md)設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="06db5-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="06db5-128">建議您在開始之前先設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="06db5-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="06db5-129">若非如此，則必須在 Site Recovery 部署期間這麼做。</span><span class="sxs-lookup"><span data-stu-id="06db5-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="06db5-130">帳戶必須位於與復原服務保存庫相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="06db5-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="06db5-131">您無法跨相同訂用帳戶內的資源群組，或跨越不同訂用帳戶移動 Site Recovery 所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="06db5-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="06db5-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06db5-132">Next steps</span></span>

<span data-ttu-id="06db5-133">移至[步驟 6：準備 Hyper-V 資源](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="06db5-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
