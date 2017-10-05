---
title: "準備 Azure 資源以使用 Azure Site Recovery 將內部部署實體伺服器複寫至 Azure | Microsoft Docs"
description: "說明在使用 Azure Site Recovery 服務開始將內部部署伺服器複寫至 Azure 之前，需要在 Azure 中備妥的項目"
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
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b7411fa6aba04ffd34f3f4bd03e706ca75afc9c8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-to-azure"></a><span data-ttu-id="55e9e-103">步驟 5：準備將實體伺服器複寫至 Azure 的 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="55e9e-103">Step 5: Prepare Azure resources for physical server replication to Azure</span></span>


<span data-ttu-id="55e9e-104">使用本文中的指示來準備 Azure 資源，以便使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署伺服器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="55e9e-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="55e9e-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="55e9e-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="55e9e-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="55e9e-106">Before you start</span></span>

<span data-ttu-id="55e9e-107">確認您已閱讀[必要條件](physical-walkthrough-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="55e9e-107">Make sure you've read the [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="55e9e-108">設定 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="55e9e-108">Set up an Azure account</span></span>

- <span data-ttu-id="55e9e-109">取得 [Microsoft Azure 帳戶](http://azure.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="55e9e-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="55e9e-110">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="55e9e-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="55e9e-111">在 [Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)的＜各地區上市情況＞底下，查看 Site Recovery 的支援地區。</span><span class="sxs-lookup"><span data-stu-id="55e9e-111">Check the supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="55e9e-112">了解 [Site Recovery 定價](site-recovery-faq.md#pricing)，並取得[定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="55e9e-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="55e9e-113">設定 Azure 網路</span><span class="sxs-lookup"><span data-stu-id="55e9e-113">Set up an Azure network</span></span>

- <span data-ttu-id="55e9e-114">設定 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="55e9e-114">Set up an Azure network.</span></span> <span data-ttu-id="55e9e-115">在容錯移轉之後建立的 Azure VM 會置於這個網路。</span><span class="sxs-lookup"><span data-stu-id="55e9e-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="55e9e-116">Azure 入口網站中的 Site Recovery 可以使用在 [Resource Manager](../resource-manager-deployment-model.md) 中或傳統模式中設定的網路。</span><span class="sxs-lookup"><span data-stu-id="55e9e-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="55e9e-117">此網路應位於與復原服務保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="55e9e-117">The network should be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="55e9e-118">了解[虛擬網路定價](https://azure.microsoft.com/pricing/details/virtual-network/)。</span><span class="sxs-lookup"><span data-stu-id="55e9e-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="55e9e-119">深入了解容錯移轉後的 [Azure VM 連線](physical-walkthrough-network.md)。</span><span class="sxs-lookup"><span data-stu-id="55e9e-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="55e9e-120">設定 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="55e9e-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="55e9e-121">Site Recovery 會將內部部署伺服器複寫至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="55e9e-121">Site Recovery replicates on-premises servers to Azure storage.</span></span> <span data-ttu-id="55e9e-122">在容錯移轉發生後，會從該儲存體建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="55e9e-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="55e9e-123">為複寫的資料設定 [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="55e9e-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="55e9e-124">Azure 入口網站中的 Site Recovery 可以使用在 Resource Manager 中或傳統模式中設定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55e9e-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="55e9e-125">此儲存體帳戶可以是標準或[進階](../storage/common/storage-premium-storage.md)帳戶。</span><span class="sxs-lookup"><span data-stu-id="55e9e-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="55e9e-126">如果您設定的是進階帳戶，則也需要一個額外的標準帳戶來記錄資料。</span><span class="sxs-lookup"><span data-stu-id="55e9e-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="55e9e-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55e9e-127">Next steps</span></span>

<span data-ttu-id="55e9e-128">移至[步驟 6：設定保存庫](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="55e9e-128">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>