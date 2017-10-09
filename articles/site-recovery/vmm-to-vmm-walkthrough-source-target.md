---
title: "aaaSet hello 來源和目標 HYPER-V 複寫 tooa 次要站台與 Azure Site Recovery |Microsoft 文件"
description: "描述如何 tooset hello 來源及目標時複寫 HYPER-V Vm toosecondary VMM 站台與 Azure Site Recovery。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="2e0cb-103">步驟 6： 設定 hello 複寫來源和目標</span><span class="sxs-lookup"><span data-stu-id="2e0cb-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="2e0cb-104">之後建立復原服務保存庫的 HYPER-V 複寫 tooa 次要 VMM 站台使用[Azure Site Recovery](site-recovery-overview.md)、 使用此發行項 tooset hello 來源和目標位置複寫。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="2e0cb-105">閱讀這篇文章之後, 張貼的任何註解底部 hello 或 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="2e0cb-106">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="2e0cb-106">Set up hello source environment</span></span>

<span data-ttu-id="2e0cb-107">Hello Azure Site Recovery Provider 安裝 VMM 伺服器上探索和 hello 保存庫中註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="2e0cb-108">按一下 [步驟 1：準備基礎結構]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![設定來源](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="2e0cb-110">在**準備來源**，按一下  **+ VMM** tooadd VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![設定來源](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="2e0cb-112">在**新增伺服器**，請檢查**System Center VMM 伺服器**會出現在**伺服器類型**和該 hello VMM 伺服器符合 hello[必要條件](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="2e0cb-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="2e0cb-113">下載 hello Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="2e0cb-114">下載 hello 登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-114">Download hello registration key.</span></span> <span data-ttu-id="2e0cb-115">您會在執行安裝程式時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-115">You need this when you run setup.</span></span> <span data-ttu-id="2e0cb-116">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-116">hello key is valid for five days after you generate it.</span></span>

    ![設定來源](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="2e0cb-118">Hello VMM 伺服器上安裝 hello Azure Site Recovery Provider。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="2e0cb-119">您不需要 tooexplicitly 則會在 HYPER-V 主機伺服器上安裝任何項目。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="2e0cb-120">安裝 Azure Site Recovery Provider hello</span><span class="sxs-lookup"><span data-stu-id="2e0cb-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="2e0cb-121">執行每一部 VMM 伺服器上的 hello 提供者安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="2e0cb-122">如果 VMM 部署在叢集中，請勿遵循您所安裝的第一次 hello hello:</span><span class="sxs-lookup"><span data-stu-id="2e0cb-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="2e0cb-123">Hello 提供者上安裝的作用中的節點，並完成 hello 安裝 tooregister hello VMM 伺服器 hello 保存庫中。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="2e0cb-124">然後，hello 提供者上安裝 hello 其他節點。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="2e0cb-125">叢集節點應該執行所有 hello 相同版本的 hello 提供者。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="2e0cb-126">安裝程式會執行幾個必要條件檢查，並要求權限 toostop hello VMM 服務。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="2e0cb-127">hello VMM 服務將會自動重新啟動安裝程式完成時。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="2e0cb-128">如果您安裝在 VMM 叢集上，您提示的 toostop hello 叢集角色。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="2e0cb-129">在**Microsoft Update**，您也可以選擇 toospecify，根據 Microsoft Update 原則安裝 provider 更新。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="2e0cb-130">在**安裝**接受或修改 hello 預設安裝位置，然後按**安裝**。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![安裝位置](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="2e0cb-132">安裝已完成之後，請按一下**註冊**tooregister hello 伺服器 hello 保存庫中的。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![安裝位置](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="2e0cb-134">在**保存庫名稱**，確認 hello hello 保存庫中的 hello 註冊伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="2e0cb-135">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-135">Click *Next*.</span></span>

    ![伺服器註冊](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="2e0cb-137">在**網際網路連線**，指定 hello hello VMM 伺服器上執行的提供者如何連接 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![網際網路設定](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="2e0cb-139">您可以指定該 hello 提供者應該連接直接 toohello 網際網路，或透過 proxy。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="2e0cb-140">指定 proxy 設定 (如有需要)。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="2e0cb-141">VMM RunAs 帳戶 (DRAProxyAccount) 如果您使用 proxy，使用指定的 hello 自動會建立 proxy 認證。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="2e0cb-142">設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="2e0cb-143">hello RunAs 帳戶的設定可以修改 hello VMM 主控台中 >**設定** > **安全性** > **執行身分帳戶**。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="2e0cb-144">重新啟動 hello VMM 服務 tooupdate 變更。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="2e0cb-145">在**登錄機碼**，選取您從 Azure Site Recovery 下載並複製 toohello VMM 伺服器的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="2e0cb-146">只有在您要在 VMM 雲端 tooAzure 複寫 HYPER-V Vm 時，才會使用 hello 加密設定。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="2e0cb-147">如果您要複寫 tooa 次要站台不使用它。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="2e0cb-148">在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="2e0cb-149">在叢集組態中指定 hello VMM 叢集角色名稱。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="2e0cb-150">在**同步處理雲端中繼資料**，選取是否要在 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端的 toosynchronize 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="2e0cb-151">這個動作只需要 toohappen 每部伺服器上一次。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="2e0cb-152">如果您不想 toosynchronize 所有雲端，您可以不勾選，此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="2e0cb-153">按一下**下一步**toocomplete hello 程序。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="2e0cb-154">註冊後，Azure Site Recovery 會擷取從 hello VMM 伺服器的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="2e0cb-155">hello 伺服器顯示在 [hello **VMM 伺服器**] 索引標籤上 hello**伺服器**hello 保存庫中的頁面。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![伺服器](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="2e0cb-157">Hello 伺服器可以使用在 hello 站台復原主控台中之後, 在**來源** > **準備來源**hello VMM 伺服器，並選取 hello 雲端中的 hello HYPER-V 主機所在的選取。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="2e0cb-158">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-158">Then click **OK**.</span></span>

<span data-ttu-id="2e0cb-159">您也可以從 hello 命令列安裝 hello 提供者：</span><span class="sxs-lookup"><span data-stu-id="2e0cb-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="2e0cb-160">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="2e0cb-160">Set up hello target environment</span></span>

<span data-ttu-id="2e0cb-161">選取 hello 目標 VMM 伺服器和雲端：</span><span class="sxs-lookup"><span data-stu-id="2e0cb-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="2e0cb-162">按一下**準備基礎結構** > **目標**，和您想要 toouse hello 選取目標 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="2e0cb-163">將會顯示 hello 伺服器上會同步處理與 Site Recovery 的雲端。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="2e0cb-164">選取 hello 目標雲端。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-164">Select hello target cloud.</span></span>

   ![目標](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="2e0cb-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e0cb-166">Next steps</span></span>

<span data-ttu-id="2e0cb-167">跳過[步驟 7： 設定網路對應](vmm-to-vmm-walkthrough-network-mapping.md)。</span><span class="sxs-lookup"><span data-stu-id="2e0cb-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
