---
title: "使用 Azure Site Recovery 設定將 Hyper-V VM 複寫至 Azure (不含 System Center VMM) 時的來源和目標 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 針對將 Hyper-V VM 複寫至 Azure 儲存體設定來源和目標設定時所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="194aa-103">步驟 8：針對將 Hyper-V 複寫至 Azure 設定來源與目標</span><span class="sxs-lookup"><span data-stu-id="194aa-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="194aa-104">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，設定將內部部署 Hyper-V 虛擬機器 (不含 System Center VMM) 複寫至 Azure 時的來源和目標設定。</span><span class="sxs-lookup"><span data-stu-id="194aa-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="194aa-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="194aa-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="194aa-106">設定來源環境</span><span class="sxs-lookup"><span data-stu-id="194aa-106">Set up the source environment</span></span>

<span data-ttu-id="194aa-107">設定 Hyper-V 網站、在 Hyper-V 主機上安裝 Azure Site Recovery Provider 和 Azure 復原服務代理程式，並在保存庫註冊網站。</span><span class="sxs-lookup"><span data-stu-id="194aa-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="194aa-108">在 [準備基礎結構] 中，按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="194aa-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="194aa-109">若要加入新的 Hyper-V 網站作為 Hyper-V 主機或叢集的容器，請按一下 [+Hyper-V 網站] 。</span><span class="sxs-lookup"><span data-stu-id="194aa-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="194aa-111">在 [建立 Hyper-V 網站] 中，指定網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="194aa-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="194aa-112">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="194aa-112">Then click **OK**.</span></span> <span data-ttu-id="194aa-113">現在，選取您建立的網站，然後按一下 [+Hyper-V Server]，將伺服器新增至網站。</span><span class="sxs-lookup"><span data-stu-id="194aa-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="194aa-115">在 [新增伺服器] > [伺服器類型] 中，檢查是否已顯示 [Hyper-V 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="194aa-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="194aa-116">確定您想要新增的 Hyper-V 伺服器符合[必要條件](#on-premises-prerequisites)，而且能夠存取指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="194aa-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="194aa-117">下載 Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="194aa-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="194aa-118">您將執行這個檔案，在每個 Hyper-V 主機上安裝 Provider 和復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="194aa-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="194aa-120">安裝 Provider 和代理程式</span><span class="sxs-lookup"><span data-stu-id="194aa-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="194aa-121">在您已加入 Hyper-V 網站中的每個主機上執行 Provider 安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="194aa-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="194aa-122">如果您安裝在 Hyper-V 叢集上，請在每個叢集節點上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="194aa-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="194aa-123">安裝和註冊每個 Hyper-V 叢集節點，可確保 VM 即使跨節點移轉，都還是會受保護。</span><span class="sxs-lookup"><span data-stu-id="194aa-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="194aa-124">在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。</span><span class="sxs-lookup"><span data-stu-id="194aa-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="194aa-125">在 [安裝] 中接受或修改預設 Provider 安裝位置，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="194aa-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="194aa-126">在 [保存庫設定] 中，按一下 [瀏覽] 來選取您已下載的保存庫金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="194aa-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="194aa-127">指定 Azure Site Recovery 訂用帳戶、保存庫名稱，以及 Hyper-V 伺服器所屬的 Hyper-V 網站。</span><span class="sxs-lookup"><span data-stu-id="194aa-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![伺服器註冊](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="194aa-129">在 [Proxy 設定] 中，指定在 Hyper-V 主機上執行的 Provider 要如何透過網際網路連線到 Azure Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="194aa-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="194aa-130">如果您想要讓 Provider 直接連線，請選取 [不使用 Proxy 直接連接至 Azure Site Recovery] 。</span><span class="sxs-lookup"><span data-stu-id="194aa-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="194aa-131">如果您現有的 Proxy 需要驗證，或您想要使用自訂 Proxy 進行 Provider 連線，請選取 [使用 Proxy 伺服器連線至 Azure Site Recovery]。</span><span class="sxs-lookup"><span data-stu-id="194aa-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="194aa-132">如果您使用 Proxy：</span><span class="sxs-lookup"><span data-stu-id="194aa-132">If you use a proxy:</span></span>
        - <span data-ttu-id="194aa-133">請指定位址、連接埠以及認證</span><span class="sxs-lookup"><span data-stu-id="194aa-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="194aa-134">請確定已允許[必要條件](#prerequisites)中所述的 URL 通過 Proxy。</span><span class="sxs-lookup"><span data-stu-id="194aa-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![網際網路](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="194aa-136">安裝完成之後，按一下 [註冊] 以在保存庫中註冊該伺服器。</span><span class="sxs-lookup"><span data-stu-id="194aa-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![安裝位置](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="194aa-138">註冊完成之後，Azure Site Recovery 便會抓取來自 Hyper-V 伺服器的中繼資料，而該伺服器會顯示在 [站台復原基礎結構] > [Hyper-V 主機] 中。</span><span class="sxs-lookup"><span data-stu-id="194aa-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="194aa-139">設定目標環境</span><span class="sxs-lookup"><span data-stu-id="194aa-139">Set up the target environment</span></span>

<span data-ttu-id="194aa-140">指定要用於複寫的 Azure 儲存體帳戶，以及 Azure VM 在容錯移轉後會連線的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="194aa-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="194aa-141">按一下 [準備基礎結構] > [目標]。</span><span class="sxs-lookup"><span data-stu-id="194aa-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="194aa-142">選取您想要在容錯移轉後，在其中建立 Azure VM 的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="194aa-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="194aa-143">選擇您想要在 Azure (傳統或資源管理) 中，針對 VM 使用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="194aa-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="194aa-144">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="194aa-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="194aa-145">如果您沒有儲存體帳戶，請按一下 [+儲存體]，建立以 Resource Manager 為基礎的內嵌帳戶。</span><span class="sxs-lookup"><span data-stu-id="194aa-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="194aa-146">如果您沒有 Azure 網路，請按一下 [+網路]，建立以 Resource Manager 為基礎的內嵌網路。</span><span class="sxs-lookup"><span data-stu-id="194aa-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="194aa-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="194aa-147">Next steps</span></span>

<span data-ttu-id="194aa-148">移至[步驟 9：設定複寫原則](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="194aa-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
