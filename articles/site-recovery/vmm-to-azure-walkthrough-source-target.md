---
title: "hello 來源和目標 （使用 System Center VMM) 」 與 Azure Site Recovery 中的 HYPER-V 複寫 tooAzure aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset 與 Azure Site Recovery 的 VMM 雲端 tooAzure 儲存體中的 HYPER-V Vm 複寫的來源和目標設定"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a><span data-ttu-id="02749-103">步驟 8: Hello 來源和目標 （使用 VMM) 的 HYPER-V 複寫 tooAzure 設定</span><span class="sxs-lookup"><span data-stu-id="02749-103">Step 8: Set up hello source and target for Hyper-V (with VMM) replication tooAzure</span></span>

<span data-ttu-id="02749-104">之後[建立保存庫](vmm-to-azure-walkthrough-create-vault.md)並指定您想 tooreplicate、 使用此發行項 tooconfigure 來源和目標設定，當複寫在內部部署 HYPER-V 虛擬機器在 System Center Virtual Machine Manager (VMM)雲端 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="02749-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want tooreplicate, use this article tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="02749-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="02749-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="02749-106">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="02749-106">Set up hello source environment</span></span>

<span data-ttu-id="02749-107">S1.</span><span class="sxs-lookup"><span data-stu-id="02749-107">S1.</span></span> <span data-ttu-id="02749-108">按一下 [準備基礎結構]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="02749-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="02749-109">在**準備來源**，按一下  **+ VMM** tooadd VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="02749-109">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![設定來源](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="02749-111">在**新增伺服器**，請檢查**System Center VMM 伺服器**會出現在**伺服器類型**和該 hello VMM 伺服器符合 hello[必要條件和 URL需求](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="02749-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="02749-112">下載 hello Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="02749-112">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="02749-113">下載 hello 登錄機碼。</span><span class="sxs-lookup"><span data-stu-id="02749-113">Download hello registration key.</span></span> <span data-ttu-id="02749-114">您會在執行安裝程式時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="02749-114">You need this when you run setup.</span></span> <span data-ttu-id="02749-115">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="02749-115">hello key is valid for five days after you generate it.</span></span>

    ![設定來源](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a><span data-ttu-id="02749-117">Hello VMM 伺服器上安裝提供者 hello</span><span class="sxs-lookup"><span data-stu-id="02749-117">Install hello Provider on hello VMM server</span></span>

1. <span data-ttu-id="02749-118">執行 hello VMM 伺服器上的 hello 提供者設定檔。</span><span class="sxs-lookup"><span data-stu-id="02749-118">Run hello Provider setup file on hello VMM server.</span></span>
2. <span data-ttu-id="02749-119">在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。</span><span class="sxs-lookup"><span data-stu-id="02749-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="02749-120">在**安裝**、 接受或修改 hello 預設提供者安裝位置並按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="02749-120">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>

    ![安裝位置](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="02749-122">安裝完成後，按一下**註冊**tooregister hello VMM 伺服器 hello 保存庫中的。</span><span class="sxs-lookup"><span data-stu-id="02749-122">When installation finishes, click **Register** tooregister hello VMM server in hello vault.</span></span>
5. <span data-ttu-id="02749-123">在 hello**保存庫設定**頁面上，按一下**瀏覽**tooselect hello 保存庫金鑰檔。</span><span class="sxs-lookup"><span data-stu-id="02749-123">In hello **Vault Settings** page, click **Browse** tooselect hello vault key file.</span></span> <span data-ttu-id="02749-124">指定 hello Azure Site Recovery 訂用帳戶和 hello 保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="02749-124">Specify hello Azure Site Recovery subscription and hello vault name.</span></span>

    ![伺服器註冊](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="02749-126">在**網際網路連線**，指定如何 hello hello VMM 伺服器上執行的提供者會透過連線 tooSite 復原 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="02749-126">In **Internet Connection**, specify how hello Provider running on hello VMM server will connect tooSite Recovery over hello internet.</span></span>

   * <span data-ttu-id="02749-127">若要直接 hello 提供者 tooconnect，選取**直接連接不使用 proxy 的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="02749-127">If you want hello Provider tooconnect directly, select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="02749-128">如果您現有的 proxy 需要驗證，或您想要 toouse 自訂 proxy，選取**連線使用 proxy 伺服器的站台復原 tooAzure**。</span><span class="sxs-lookup"><span data-stu-id="02749-128">If your existing proxy requires authentication, or you want toouse a custom proxy, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="02749-129">如果您使用自訂 proxy，請指定 hello 位址、 連接埠，以及認證。</span><span class="sxs-lookup"><span data-stu-id="02749-129">If you use a custom proxy, specify hello address, port, and credentials.</span></span>
   * <span data-ttu-id="02749-130">如果您使用 proxy，您應該已經允許 hello Url 中所述[必要條件](#on-premises-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="02749-130">If you're using a proxy, you should have already allowed hello URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="02749-131">如果您使用自訂 proxy，將會使用指定的 hello，自動建立 VMM RunAs 帳戶 (DRAProxyAccount) proxy 認證。</span><span class="sxs-lookup"><span data-stu-id="02749-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="02749-132">設定 hello proxy 伺服器，讓此帳戶可成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="02749-132">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="02749-133">hello VMM 主控台中，可以修改 hello VMM RunAs 帳戶的設定。</span><span class="sxs-lookup"><span data-stu-id="02749-133">hello VMM RunAs account settings can be modified in hello VMM console.</span></span> <span data-ttu-id="02749-134">在**設定**，依序展開**安全性** > **執行身分帳戶**，然後修改 draproxyaccount 的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="02749-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify hello password for DRAProxyAccount.</span></span> <span data-ttu-id="02749-135">您將需要 toorestart hello VMM 服務，讓這項設定會生效。</span><span class="sxs-lookup"><span data-stu-id="02749-135">You’ll need toorestart hello VMM service so that this setting takes effect.</span></span>

     ![網際網路](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="02749-137">接受或修改 hello 位置之資料加密時，會自動產生 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="02749-137">Accept or modify hello location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="02749-138">如果您啟用資料加密受 Azure 保護的 hello Azure Site Recovery 入口網站雲端，則會使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="02749-138">This certificate is used if you enable data encryption for a cloud protected by Azure in hello Azure Site Recovery portal.</span></span> <span data-ttu-id="02749-139">請保護此憑證的安全。</span><span class="sxs-lookup"><span data-stu-id="02749-139">Keep this certificate safe.</span></span> <span data-ttu-id="02749-140">當您執行容錯移轉 tooAzure 您將需要它 toodecrypt，如果已啟用資料加密。</span><span class="sxs-lookup"><span data-stu-id="02749-140">When you run a failover tooAzure you’ll need it toodecrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="02749-141">在**伺服器名稱**，指定在 hello 保存庫中的易記名稱 tooidentify hello 的 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="02749-141">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="02749-142">在叢集組態中，指定 hello VMM 叢集角色名稱。</span><span class="sxs-lookup"><span data-stu-id="02749-142">In a cluster configuration, specify hello VMM cluster role name.</span></span>
9. <span data-ttu-id="02749-143">啟用**同步處理雲端中繼資料**，如果您想 toosynchronize 中繼資料的 hello 與 hello 保存庫的 VMM 伺服器上的所有雲端。</span><span class="sxs-lookup"><span data-stu-id="02749-143">Enable **Sync cloud metadata**, if you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="02749-144">這個動作只需要 toohappen 每部伺服器上一次。</span><span class="sxs-lookup"><span data-stu-id="02749-144">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="02749-145">如果您不想 toosynchronize 所有雲端，您可以不勾選此設定，並個別同步處理每個雲端 hello VMM 主控台中的 hello 雲端內容。</span><span class="sxs-lookup"><span data-stu-id="02749-145">If you don't want toosynchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span> <span data-ttu-id="02749-146">按一下**註冊**toocomplete hello 程序。</span><span class="sxs-lookup"><span data-stu-id="02749-146">Click **Register** toocomplete hello process.</span></span>

    ![伺服器註冊](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="02749-148">註冊作業隨即開始。</span><span class="sxs-lookup"><span data-stu-id="02749-148">Registration starts.</span></span> <span data-ttu-id="02749-149">註冊完成之後，在中，會顯示 hello 伺服器**Site Recovery 基礎結構** > **VMM 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="02749-149">After registration finishes, hello server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="02749-150">HYPER-V 主機上安裝 hello Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="02749-150">Install hello Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="02749-151">當您設定 hello 提供者之後，您需要 toodownload hello 安裝檔案 hello Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="02749-151">After you've set up hello Provider, you need toodownload hello installation file for hello Azure Recovery Services agent.</span></span> <span data-ttu-id="02749-152">Hello VMM 雲端中的每個 HYPER-V 伺服器上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="02749-152">Run setup on each Hyper-V server in hello VMM cloud.</span></span>

    ![Hyper-V 網站](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="02749-154">在 [檢查先決條件] 中，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="02749-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="02749-155">將自動安裝任何缺少的必要元件。</span><span class="sxs-lookup"><span data-stu-id="02749-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Prerequisites Recovery Services Agent](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="02749-157">在**安裝設定**，接受或修改 hello 安裝位置，與 hello 快取位置。</span><span class="sxs-lookup"><span data-stu-id="02749-157">In **Installation Settings**, accept or modify hello installation location, and hello cache location.</span></span> <span data-ttu-id="02749-158">您可以設定 hello 快取有至少 5 GB 的可用儲存體的磁碟機上，但我們建議 600 GB 或更多的可用空間的快取磁碟機。</span><span class="sxs-lookup"><span data-stu-id="02749-158">You can configure hello cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="02749-159">然後按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="02749-159">Then click **Install**.</span></span>
4. <span data-ttu-id="02749-160">安裝已完成之後，請按一下**關閉**toofinish。</span><span class="sxs-lookup"><span data-stu-id="02749-160">After installation is complete, click **Close** toofinish.</span></span>

    ![註冊 MARS 代理程式](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="02749-162">命令列安裝</span><span class="sxs-lookup"><span data-stu-id="02749-162">Command line installation</span></span>
<span data-ttu-id="02749-163">您可以從命令列使用下列命令的 hello 安裝 Microsoft Azure Recovery Services Agent hello:</span><span class="sxs-lookup"><span data-stu-id="02749-163">You can install hello Microsoft Azure Recovery Services Agent from command line using hello following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a><span data-ttu-id="02749-164">設定網際網路的 proxy 存取 tooSite 復原，從 HYPER-V 主機</span><span class="sxs-lookup"><span data-stu-id="02749-164">Set up internet proxy access tooSite Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="02749-165">HYPER-V 主機上執行的 hello 復原服務代理程式需要網際網路存取 tooAzure VM 複寫。</span><span class="sxs-lookup"><span data-stu-id="02749-165">hello Recovery Services agent running on Hyper-V hosts needs internet access tooAzure for VM replication.</span></span> <span data-ttu-id="02749-166">如果您正在存取 hello 網際網路透過 proxy、 設定它，如下所示：</span><span class="sxs-lookup"><span data-stu-id="02749-166">If you're accessing hello internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="02749-167">開啟 hello Microsoft Azure 備份 MMC 嵌入式管理單元 hello HYPER-V 主機上。</span><span class="sxs-lookup"><span data-stu-id="02749-167">Open hello Microsoft Azure Backup MMC snap-in on hello Hyper-V host.</span></span> <span data-ttu-id="02749-168">根據預設，Microsoft Azure 備份的捷徑使用。 在 hello 桌面上或 C:\Program Files\Microsoft Azure 復原服務 Agent\bin\wabadmin</span><span class="sxs-lookup"><span data-stu-id="02749-168">By default, a shortcut for Microsoft Azure Backup is available on hello desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="02749-169">在 hello 嵌入式管理單元，按一下 **變更屬性**。</span><span class="sxs-lookup"><span data-stu-id="02749-169">In hello snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="02749-170">在 hello **Proxy 組態**索引標籤上，指定 proxy 伺服器資訊。</span><span class="sxs-lookup"><span data-stu-id="02749-170">On hello **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![註冊 MARS 代理程式](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="02749-172">檢查該 hello 代理程式是否可送達 hello 中所述的 hello Url[必要條件](#on-premises-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="02749-172">Check that hello agent can reach hello URLs described in hello [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-hello-target-environment"></a><span data-ttu-id="02749-173">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="02749-173">Set up hello target environment</span></span>
<span data-ttu-id="02749-174">指定用於複寫，hello Azure 儲存體帳戶 toobe 和容錯移轉後連線 hello Azure 網路 toowhich Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="02749-174">Specify hello Azure storage account toobe used for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="02749-175">按一下**準備基礎結構** > **目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="02749-175">Click **Prepare infrastructure** > **Target**, select hello subscription and hello resource group where you want toocreate hello failed over virtual machines.</span></span> <span data-ttu-id="02749-176">選擇要容錯移轉虛擬機器的 hello toouse Azure （classic 或資源管理） 中的 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="02749-176">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello failed over virtual machines.</span></span>

    ![儲存體](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="02749-178">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="02749-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![儲存體](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="02749-180">如果您尚未建立儲存體帳戶，而且您想 toocreate 其中一個使用資源管理員，按一下**+ 儲存體帳戶**toodo 該內嵌。</span><span class="sxs-lookup"><span data-stu-id="02749-180">If you haven't created a storage account, and you want toocreate one using Resource Manager, click **+Storage account** toodo that inline.</span></span>  <span data-ttu-id="02749-181">在 hello**建立儲存體帳戶**刀鋒視窗中指定帳戶名稱、 類型、 訂閱與位置。</span><span class="sxs-lookup"><span data-stu-id="02749-181">On hello **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="02749-182">hello 帳戶應該位於 hello hello 與相同的位置復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="02749-182">hello account should be in hello same location as hello Recovery Services vault.</span></span>

   ![儲存體](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="02749-184">如果您想 toocreate 使用 hello 傳統模型的儲存體帳戶，請在 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="02749-184">If you want toocreate a storage account using hello classic model, do that in hello Azure portal.</span></span> [<span data-ttu-id="02749-185">深入了解</span><span class="sxs-lookup"><span data-stu-id="02749-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="02749-186">如果您使用進階儲存體帳戶複寫資料，設定額外標準儲存體帳戶，擷取進行中的變更 tooon 內部部署資料的 toostore 複寫記錄檔。</span><span class="sxs-lookup"><span data-stu-id="02749-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
5. <span data-ttu-id="02749-187">如果您尚未建立 Azure 網路，而且您想 toocreate 其中一個使用資源管理員，按一下**+ 網路**toodo 該內嵌。</span><span class="sxs-lookup"><span data-stu-id="02749-187">If you haven't created an Azure network, and you want toocreate one using Resource Manager, click **+Network** toodo that inline.</span></span> <span data-ttu-id="02749-188">在 hello**建立虛擬網路**刀鋒視窗中指定的網路名稱、 位址範圍、 子網路詳細資料、 訂閱與位置。</span><span class="sxs-lookup"><span data-stu-id="02749-188">On hello **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="02749-189">hello 網路應位於 hello hello 與相同的位置復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="02749-189">hello network should be in hello same location as hello Recovery Services vault.</span></span>

   ![網路](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="02749-191">如果您想 toocreate 網路使用 hello 傳統模式，請 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="02749-191">If you want toocreate a network using hello classic model, do that in hello Azure portal.</span></span> <span data-ttu-id="02749-192">[深入了解](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="02749-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="02749-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02749-193">Next steps</span></span>

<span data-ttu-id="02749-194">跳過[步驟 9： 設定網路對應](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="02749-194">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
