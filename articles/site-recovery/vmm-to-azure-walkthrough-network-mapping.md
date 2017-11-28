---
title: "使用 Azure Site Recovery 將 VMM 雲端中的 Hyper-V VM 複寫至 Azure 時設定網路對應 | Microsoft Docs"
description: "說明使用 Azure Site Recovery 將 VMM 雲端中的 Hyper-V VM 複寫至 Azure 時，如何設定網路對應"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ed6f73d8baea5af0d2aa5f0ae885f305911ccc82
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-to-azure"></a><span data-ttu-id="8418a-103">步驟 9：針對複寫至 Azure 的 Hyper-V 複寫作業 (含 VMM) 設定網路對應</span><span class="sxs-lookup"><span data-stu-id="8418a-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) to Azure</span></span>

<span data-ttu-id="8418a-104">設定[來源和目標的複寫設定](vmm-to-azure-walkthrough-source-target.md)後，使用本文來設定網路對應，以對應內部部署 VMM VM 網路和 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-104">After you set up the [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article to configure network mapping to map between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="8418a-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="8418a-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8418a-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="8418a-106">Before you start</span></span>

- <span data-ttu-id="8418a-107">深入了解[網路對應](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)。</span><span class="sxs-lookup"><span data-stu-id="8418a-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="8418a-108">[準備 VMM 以進行網路對應](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping)。</span><span class="sxs-lookup"><span data-stu-id="8418a-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="8418a-109">確認 VMM 伺服器上的虛擬機器已連接到 VM 網路，以及您已建立至少一個 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-109">Verify that virtual machines on the VMM server are connected to a VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="8418a-110">多個 VM 網路可對應至單一 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-110">Multiple VM networks can be mapped to a single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="8418a-111">設定對應</span><span class="sxs-lookup"><span data-stu-id="8418a-111">Configure mapping</span></span>

<span data-ttu-id="8418a-112">設定對應，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8418a-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="8418a-113">在 [Site Recovery 基礎結構]  >  [網路對應]  >  [網路對應]中，按一下 [+網路對應] 圖示。</span><span class="sxs-lookup"><span data-stu-id="8418a-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click the **+Network Mapping** icon.</span></span>

    ![網路對應](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="8418a-115">在 [新增網路對應] 上選取來源 VMM 伺服器，並選 [Azure] 做為目標。</span><span class="sxs-lookup"><span data-stu-id="8418a-115">In **Add network mapping**, select the source VMM server, and **Azure** as the target.</span></span>
3. <span data-ttu-id="8418a-116">在容錯移轉後確認訂用帳戶和部署模型。</span><span class="sxs-lookup"><span data-stu-id="8418a-116">Verify the subscription and the deployment model after failover.</span></span>
4. <span data-ttu-id="8418a-117">在 [來源網路] 中，從與 VMM 伺服器相關聯的清單中，選取您要對應的來源內部部署 VM 網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-117">In **Source network**, select the source on-premises VM network you want to map from the list associated with the VMM server.</span></span>
5. <span data-ttu-id="8418a-118">在 [目標網路] 中，選取複本 Azure VM 建立後所在的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-118">In **Target network**, select the Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="8418a-119">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8418a-119">Then click **OK**.</span></span>

    ![網路對應](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="8418a-121">以下是網路對應開始時發生的事情︰</span><span class="sxs-lookup"><span data-stu-id="8418a-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="8418a-122">開始對應時，來源 VM 網路上的現有 VM 會連接到目標網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-122">Existing VMs on the source VM network are connected to the target network when mapping begins.</span></span> <span data-ttu-id="8418a-123">連接到來源 VM 網路的新 VM 會在發生複寫時連接到對應的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-123">New VMs connected to the source VM network are connected to the mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="8418a-124">如果您修改現有的網路對應，則複本虛擬機器會使用新設定進行連線。</span><span class="sxs-lookup"><span data-stu-id="8418a-124">If you modify an existing network mapping, replica virtual machines connect using the new settings.</span></span>
* <span data-ttu-id="8418a-125">如果目標網路具有多個子網路，且其中一個子網路的名稱和來源虛擬機器所在之子網路名稱相同，複本虛擬機器會在容錯移轉之後連線到該目標子網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-125">If the target network has multiple subnets, and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine connects to that target subnet after failover.</span></span>
* <span data-ttu-id="8418a-126">如果沒有目標子網路具有相符的名稱，虛擬機器會連線到網路中的第一個子網路。</span><span class="sxs-lookup"><span data-stu-id="8418a-126">If there’s no target subnet with a matching name, the virtual machine connects to the first subnet in the network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8418a-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8418a-127">Next steps</span></span>

<span data-ttu-id="8418a-128">移至[步驟 10：建立複寫原則](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="8418a-128">Go to [Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
