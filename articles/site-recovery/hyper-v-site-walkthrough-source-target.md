---
title: "aaaSet hello 來源和目標 HYPER-V 複寫 tooAzure （不含 System Center VMM) 與 Azure Site Recovery |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset HYPER-V Vm tooAzure 儲存體與 Azure Site Recovery 的複寫的來源和目標設定"
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
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="13571-103">步驟 8: Hello 來源和目標 HYPER-V 複寫 tooAzure 設定</span><span class="sxs-lookup"><span data-stu-id="13571-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="13571-104">本文說明如何 tooconfigure 來源和目標設定複寫時內部部署 HYPER-V 虛擬機器 （不含 System Center VMM) tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="13571-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="13571-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="13571-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="13571-106">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="13571-106">Set up hello source environment</span></span>

<span data-ttu-id="13571-107">設定 hello HYPER-V 站台、 HYPER-V 主機上安裝 Azure Site Recovery Provider hello 和 hello Azure 復原服務代理程式和 hello 保存庫中註冊 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="13571-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="13571-108">在 [準備基礎結構] 中，按一下 [來源]。</span><span class="sxs-lookup"><span data-stu-id="13571-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="13571-109">按一下 新的 HYPER-V 站台做為您的 HYPER-V 主機或叢集的容器 tooadd **+ HYPER-V 站台**。</span><span class="sxs-lookup"><span data-stu-id="13571-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="13571-111">在**建立 HYPER-V 站台**，指定 hello 網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="13571-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="13571-112">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="13571-112">Then click **OK**.</span></span> <span data-ttu-id="13571-113">現在，選取您建立，然後按一下 「 hello 」 站台**+ HYPER-V Server** tooadd 伺服器 toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="13571-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="13571-115">在 [新增伺服器] > [伺服器類型] 中，檢查是否已顯示 [Hyper-V 伺服器]。</span><span class="sxs-lookup"><span data-stu-id="13571-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="13571-116">請確定您想要 hello tooadd 符合該 hello HYPER-V 伺服器[必要條件](#on-premises-prerequisites)，和是無法 tooaccess hello 指定的 Url。</span><span class="sxs-lookup"><span data-stu-id="13571-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="13571-117">下載 hello Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="13571-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="13571-118">執行此檔案 tooinstall hello 提供者並 hello 每個 HYPER-V 主機上的復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="13571-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![設定來源](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="13571-120">安裝 hello 提供者和代理程式</span><span class="sxs-lookup"><span data-stu-id="13571-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="13571-121">您已新增 toohello HYPER-V 站台執行每個主機上的 hello 提供者安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="13571-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="13571-122">如果您安裝在 Hyper-V 叢集上，請在每個叢集節點上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="13571-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="13571-123">安裝和註冊每個 Hyper-V 叢集節點，可確保 VM 即使跨節點移轉，都還是會受保護。</span><span class="sxs-lookup"><span data-stu-id="13571-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="13571-124">在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。</span><span class="sxs-lookup"><span data-stu-id="13571-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="13571-125">在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="13571-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="13571-126">在**保存庫設定**，按一下 **瀏覽**tooselect hello 保存庫金鑰檔下載。</span><span class="sxs-lookup"><span data-stu-id="13571-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="13571-127">指定 hello Azure Site Recovery 訂用帳戶，hello 保存庫名稱，並所屬 hello HYPER-V 站台 toowhich hello HYPER-V 伺服器。</span><span class="sxs-lookup"><span data-stu-id="13571-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![伺服器註冊](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="13571-129">在**Proxy 設定**，指定 HYPER-V 主機上執行的提供者透過連接 tooAzure Site Recovery 的 hello hello 網際網路的方式。</span><span class="sxs-lookup"><span data-stu-id="13571-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="13571-130">如果您想 hello 提供者 tooconnect 直接選取**直接連接不使用 proxy 的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="13571-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="13571-131">如果您現有的 proxy 需要驗證，或者您想 toouse 自訂 proxy hello 提供者連接，請選取**連線使用 proxy 伺服器的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="13571-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="13571-132">如果您使用 Proxy：</span><span class="sxs-lookup"><span data-stu-id="13571-132">If you use a proxy:</span></span>
        - <span data-ttu-id="13571-133">指定 hello 位址、 連接埠和認證</span><span class="sxs-lookup"><span data-stu-id="13571-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="13571-134">請確定 hello 中所述的 hello Url[必要條件](#prerequisites)允許透過 hello proxy。</span><span class="sxs-lookup"><span data-stu-id="13571-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![網際網路](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="13571-136">安裝完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。</span><span class="sxs-lookup"><span data-stu-id="13571-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![安裝位置](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="13571-138">註冊完成之後，Azure Site Recovery 中，擷取中繼資料從 hello HYPER-V 伺服器和中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **HYPER-V 主機**。</span><span class="sxs-lookup"><span data-stu-id="13571-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="13571-139">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="13571-139">Set up hello target environment</span></span>

<span data-ttu-id="13571-140">指定 hello Azure 儲存體帳戶來進行複寫，並容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="13571-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="13571-141">按一下 [準備基礎結構] > [目標]。</span><span class="sxs-lookup"><span data-stu-id="13571-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="13571-142">選取 hello 訂用帳戶與您想 toocreate hello Azure Vm 容錯移轉之後的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="13571-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="13571-143">選擇 hello 部署模型的 toouse Azure （classic 或資源管理） 中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="13571-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="13571-144">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="13571-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="13571-145">如果您沒有儲存體帳戶，按一下**+ 儲存體**toocreate 資源管理員帳戶內嵌。</span><span class="sxs-lookup"><span data-stu-id="13571-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="13571-146">如果您沒有 Azure 網路，按一下**+ 網路**toocreate 資源管理員為基礎的網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="13571-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="13571-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13571-147">Next steps</span></span>

<span data-ttu-id="13571-148">跳過[步驟 9： 設定複寫原則](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="13571-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
