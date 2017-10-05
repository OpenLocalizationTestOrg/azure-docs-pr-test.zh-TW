---
title: "設定使用 Azure Site Recovery 將 Hyper-V (含 System Center VMM) 複寫至 Azure 時的來源和目標 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 將 VMM 雲端中的 Hyper-V VM 複寫至 Azure 儲存體時，設定來源和目標設定時所需的步驟"
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
ms.openlocfilehash: c72f839d0a1288dccb7deb3e44fc2b20d64818f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-with-vmm-replication-to-azure"></a><span data-ttu-id="d9e23-103">步驟 8：設定將 Hyper-V (含 VMM) 複寫至 Azure 時的來源與目標</span><span class="sxs-lookup"><span data-stu-id="d9e23-103">Step 8: Set up the source and target for Hyper-V (with VMM) replication to Azure</span></span>

<span data-ttu-id="d9e23-104">[建立保存庫](vmm-to-azure-walkthrough-create-vault.md)和指定複寫的目標後，請使用本文來設定來源和目標設定，以在使用 Azure 入口網站中的 [Azure Site Recovery](site-recovery-overview.md) 服務將 System Center Virtual Machine Manager (VMM) 雲端中的內部部署 Hyper-V 虛擬機器複寫至 Azure 時套用。</span><span class="sxs-lookup"><span data-stu-id="d9e23-104">After [creating a vault](vmm-to-azure-walkthrough-create-vault.md) and specifying what you want to replicate, use this article to configure source and target settings when replicating on-premises Hyper-V virtual machines in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="d9e23-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="d9e23-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="d9e23-106">設定來源環境</span><span class="sxs-lookup"><span data-stu-id="d9e23-106">Set up the source environment</span></span>

<span data-ttu-id="d9e23-107">S1.</span><span class="sxs-lookup"><span data-stu-id="d9e23-107">S1.</span></span> <span data-ttu-id="d9e23-108">按一下 [準備基礎結構]  >  [來源]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-108">Click **Prepare Infrastructure** > **Source**.</span></span>

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. <span data-ttu-id="d9e23-109">在 [準備來源] 中，按一下 [+ VMM] 以新增 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9e23-109">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![設定來源](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="d9e23-111">在 [新增伺服器] 中，檢查 [System Center VMM 伺服器] 是否出現在 [伺服器類型] 中，以及 VMM 伺服器是否符合[必要條件和 URL 需求](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="d9e23-111">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites and URL requirements](#prerequisites).</span></span>
4. <span data-ttu-id="d9e23-112">下載 Azure Site Recovery Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="d9e23-112">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="d9e23-113">下載註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="d9e23-113">Download the registration key.</span></span> <span data-ttu-id="d9e23-114">您會在執行安裝程式時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="d9e23-114">You need this when you run setup.</span></span> <span data-ttu-id="d9e23-115">該金鑰在產生後會維持 5 天有效。</span><span class="sxs-lookup"><span data-stu-id="d9e23-115">The key is valid for five days after you generate it.</span></span>

    ![設定來源](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-the-provider-on-the-vmm-server"></a><span data-ttu-id="d9e23-117">在 VMM 伺服器上將提供者解除安裝</span><span class="sxs-lookup"><span data-stu-id="d9e23-117">Install the Provider on the VMM server</span></span>

1. <span data-ttu-id="d9e23-118">在 VMM 伺服器上執行 Provider 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="d9e23-118">Run the Provider setup file on the VMM server.</span></span>
2. <span data-ttu-id="d9e23-119">在 [Microsoft Update] 中，您可以選擇進行更新，以便根據您的 Microsoft Update 原則安裝 Provider 更新。</span><span class="sxs-lookup"><span data-stu-id="d9e23-119">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="d9e23-120">在 [安裝] 中接受或修改預設 Provider 安裝位置，然後按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-120">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>

    ![安裝位置](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. <span data-ttu-id="d9e23-122">安裝完成時，請按一下 [註冊] 以在保存庫中註冊 VMM 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9e23-122">When installation finishes, click **Register** to register the VMM server in the vault.</span></span>
5. <span data-ttu-id="d9e23-123">在 [保存庫設定] 頁面中，按一下 [瀏覽] 來選取保存庫金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="d9e23-123">In the **Vault Settings** page, click **Browse** to select the vault key file.</span></span> <span data-ttu-id="d9e23-124">指定 Azure Site Recovery 訂用帳戶和保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="d9e23-124">Specify the Azure Site Recovery subscription and the vault name.</span></span>

    ![伺服器註冊](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. <span data-ttu-id="d9e23-126">在 [網際網路連線] 中，指定在 VMM 伺服器上執行的 Provider 透過網際網路連接到 Site Recovery 的方式。</span><span class="sxs-lookup"><span data-stu-id="d9e23-126">In **Internet Connection**, specify how the Provider running on the VMM server will connect to Site Recovery over the internet.</span></span>

   * <span data-ttu-id="d9e23-127">如果您想要讓 Provider 直接連線，請選取 [不使用 Proxy 直接連接至 Azure Site Recovery]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-127">If you want the Provider to connect directly, select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
   * <span data-ttu-id="d9e23-128">如果您現有的 Proxy 需要驗證，或您想要使用自訂 Proxy，請選取 [使用 Proxy 伺服器連接至 Azure Site Recovery]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-128">If your existing proxy requires authentication, or you want to use a custom proxy, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
   * <span data-ttu-id="d9e23-129">如果您使用自訂 proxy，請指定位址、連接埠以及認證</span><span class="sxs-lookup"><span data-stu-id="d9e23-129">If you use a custom proxy, specify the address, port, and credentials.</span></span>
   * <span data-ttu-id="d9e23-130">如果您使用 Proxy，您應該已經允許[必要條件](#on-premises-prerequisites)中所述的 URL。</span><span class="sxs-lookup"><span data-stu-id="d9e23-130">If you're using a proxy, you should have already allowed the URLs described in [prerequisites](#on-premises-prerequisites).</span></span>
   * <span data-ttu-id="d9e23-131">如果您使用的是自訂 proxy，則會使用指定的 proxy 認證自動建立 VMM RunAs 帳戶 (DRAProxyAccount)。</span><span class="sxs-lookup"><span data-stu-id="d9e23-131">If you use a custom proxy, a VMM RunAs account (DRAProxyAccount) will be created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="d9e23-132">設定 proxy 伺服器，讓此帳戶可以成功進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d9e23-132">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="d9e23-133">在 VMM 主控台中，可以修改 VMM RunAs 帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="d9e23-133">The VMM RunAs account settings can be modified in the VMM console.</span></span> <span data-ttu-id="d9e23-134">在 [設定] 中，展開 [安全性] > [執行身分帳戶]，然後修改 DRAProxyAccount 的密碼。</span><span class="sxs-lookup"><span data-stu-id="d9e23-134">In **Settings**, expand **Security** > **Run As Accounts**, and then modify the password for DRAProxyAccount.</span></span> <span data-ttu-id="d9e23-135">您必須重新啟動 VMM 服務，這項設定才會生效。</span><span class="sxs-lookup"><span data-stu-id="d9e23-135">You’ll need to restart the VMM service so that this setting takes effect.</span></span>

     ![網際網路](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. <span data-ttu-id="d9e23-137">接受或修改自動為資料加密產生的 SSL 憑證位置。</span><span class="sxs-lookup"><span data-stu-id="d9e23-137">Accept or modify the location of an SSL certificate that’s automatically generated for data encryption.</span></span> <span data-ttu-id="d9e23-138">如果您在 Azure 站台復原入口網站中為 Azure 所保護的雲端啟用資料加密，則會使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="d9e23-138">This certificate is used if you enable data encryption for a cloud protected by Azure in the Azure Site Recovery portal.</span></span> <span data-ttu-id="d9e23-139">請保護此憑證的安全。</span><span class="sxs-lookup"><span data-stu-id="d9e23-139">Keep this certificate safe.</span></span> <span data-ttu-id="d9e23-140">當您執行容錯移轉至 Azure 時，如果已啟用資料加密，您需要使用它來解密。</span><span class="sxs-lookup"><span data-stu-id="d9e23-140">When you run a failover to Azure you’ll need it to decrypt, if data encryption is enabled.</span></span>
8. <span data-ttu-id="d9e23-141">在 [伺服器名稱] 中，指定保存庫中 VMM 伺服器的易記識別名稱。</span><span class="sxs-lookup"><span data-stu-id="d9e23-141">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="d9e23-142">在叢集設定中，指定 VMM 叢集角色名稱。</span><span class="sxs-lookup"><span data-stu-id="d9e23-142">In a cluster configuration, specify the VMM cluster role name.</span></span>
9. <span data-ttu-id="d9e23-143">如果您想要將 VMM 伺服器上所有雲端的中繼資料與保存庫進行同步，請啟用 [同步處理雲端中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-143">Enable **Sync cloud metadata**, if you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="d9e23-144">這個動作只需要在每個伺服器上進行一次。</span><span class="sxs-lookup"><span data-stu-id="d9e23-144">This action only needs to happen once on each server.</span></span> <span data-ttu-id="d9e23-145">如果不要同步所有雲端，您可以取消核取這項設定，再於 VMM 主控台的雲端屬性中個別同步每個雲端。</span><span class="sxs-lookup"><span data-stu-id="d9e23-145">If you don't want to synchronize all clouds, you can leave this setting unchecked and synchronize each cloud individually in the cloud properties in the VMM console.</span></span> <span data-ttu-id="d9e23-146">按一下 [註冊]  完成此程序。</span><span class="sxs-lookup"><span data-stu-id="d9e23-146">Click **Register** to complete the process.</span></span>

    ![伺服器註冊](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. <span data-ttu-id="d9e23-148">註冊作業隨即開始。</span><span class="sxs-lookup"><span data-stu-id="d9e23-148">Registration starts.</span></span> <span data-ttu-id="d9e23-149">註冊完成後，伺服器會顯示在 [Site Recovery 基礎結構]  >  [VMM 伺服器] 中。</span><span class="sxs-lookup"><span data-stu-id="d9e23-149">After registration finishes, the server is displayed in **Site Recovery Infrastructure** > **VMM Servers**.</span></span>


## <a name="install-the-azure-recovery-services-agent-on-hyper-v-hosts"></a><span data-ttu-id="d9e23-150">在 Hyper-V 主機上安裝 Azure 復原服務代理程式</span><span class="sxs-lookup"><span data-stu-id="d9e23-150">Install the Azure Recovery Services agent on Hyper-V hosts</span></span>

1. <span data-ttu-id="d9e23-151">設定 Provider 之後，您需要下載 Azure 復原服務代理程式的安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="d9e23-151">After you've set up the Provider, you need to download the installation file for the Azure Recovery Services agent.</span></span> <span data-ttu-id="d9e23-152">在 VMM 雲端中的每部 Hyper-V 伺服器上執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="d9e23-152">Run setup on each Hyper-V server in the VMM cloud.</span></span>

    ![Hyper-V 網站](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. <span data-ttu-id="d9e23-154">在 [檢查先決條件] 中，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-154">In **Prerequisites Check**, click **Next**.</span></span> <span data-ttu-id="d9e23-155">將自動安裝任何缺少的必要元件。</span><span class="sxs-lookup"><span data-stu-id="d9e23-155">Any missing prerequisites will be automatically installed.</span></span>

    ![Prerequisites Recovery Services Agent](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. <span data-ttu-id="d9e23-157">在 [安裝設定] 中，接受或修改安裝位置和快取位置。</span><span class="sxs-lookup"><span data-stu-id="d9e23-157">In **Installation Settings**, accept or modify the installation location, and the cache location.</span></span> <span data-ttu-id="d9e23-158">您可以在至少有 5 GB 可用儲存體的磁碟機上設定快取，但我們建議快取磁碟機有 600 GB 或更多可用空間。</span><span class="sxs-lookup"><span data-stu-id="d9e23-158">You can configure the cache on a drive that has at least 5 GB of storage available but we recommend a cache drive with 600 GB or more of free space.</span></span> <span data-ttu-id="d9e23-159">然後按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="d9e23-159">Then click **Install**.</span></span>
4. <span data-ttu-id="d9e23-160">安裝完成後，按一下 [關閉]  即可完成。</span><span class="sxs-lookup"><span data-stu-id="d9e23-160">After installation is complete, click **Close** to finish.</span></span>

    ![註冊 MARS 代理程式](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a><span data-ttu-id="d9e23-162">命令列安裝</span><span class="sxs-lookup"><span data-stu-id="d9e23-162">Command line installation</span></span>
<span data-ttu-id="d9e23-163">您可以使用下列命令，從命令列安裝 Microsoft Azure 復原服務代理程式：</span><span class="sxs-lookup"><span data-stu-id="d9e23-163">You can install the Microsoft Azure Recovery Services Agent from command line using the following command:</span></span>

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-to-site-recovery-from-hyper-v-hosts"></a><span data-ttu-id="d9e23-164">設定從 Hyper-V 主機對 Site Recovery 的網際網路 Proxy 存取</span><span class="sxs-lookup"><span data-stu-id="d9e23-164">Set up internet proxy access to Site Recovery from Hyper-V hosts</span></span>

<span data-ttu-id="d9e23-165">在 Hyper-V 主機上執行的復原服務代理程式需要 Azure 的網際網路存取權才能進行 VM 複寫。</span><span class="sxs-lookup"><span data-stu-id="d9e23-165">The Recovery Services agent running on Hyper-V hosts needs internet access to Azure for VM replication.</span></span> <span data-ttu-id="d9e23-166">如果您透過 Proxy 存取網際網路，請如下所示設定它︰</span><span class="sxs-lookup"><span data-stu-id="d9e23-166">If you're accessing the internet through a proxy, set it up as follows:</span></span>

1. <span data-ttu-id="d9e23-167">在 Hyper-V 主機上開啟 Microsoft Azure 備份 MMC 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="d9e23-167">Open the Microsoft Azure Backup MMC snap-in on the Hyper-V host.</span></span> <span data-ttu-id="d9e23-168">根據預設，Microsoft Azure 備份的捷徑位於桌面上或在 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin 中。</span><span class="sxs-lookup"><span data-stu-id="d9e23-168">By default, a shortcut for Microsoft Azure Backup is available on the desktop or in C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.</span></span>
2. <span data-ttu-id="d9e23-169">在嵌入式管理單元中，按一下 [變更屬性]。</span><span class="sxs-lookup"><span data-stu-id="d9e23-169">In the snap-in, click **Change Properties**.</span></span>
3. <span data-ttu-id="d9e23-170">在 [Proxy 設定]  索引標籤上指定 Proxy 伺服器資訊。</span><span class="sxs-lookup"><span data-stu-id="d9e23-170">On the **Proxy Configuration** tab, specify proxy server information.</span></span>

    ![註冊 MARS 代理程式](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. <span data-ttu-id="d9e23-172">確定代理程式可以連到[必要條件](#on-premises-prerequisites)中所述的 URL。</span><span class="sxs-lookup"><span data-stu-id="d9e23-172">Check that the agent can reach the URLs described in the [prerequisites](#on-premises-prerequisites).</span></span>

## <a name="set-up-the-target-environment"></a><span data-ttu-id="d9e23-173">設定目標環境</span><span class="sxs-lookup"><span data-stu-id="d9e23-173">Set up the target environment</span></span>
<span data-ttu-id="d9e23-174">指定要用於複寫的 Azure 儲存體帳戶，以及 Azure VM 在容錯移轉後會連接的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="d9e23-174">Specify the Azure storage account to be used for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="d9e23-175">按一下 [準備基礎結構] > [目標]，選取您想要在其中建立容錯移轉虛擬機器的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="d9e23-175">Click **Prepare infrastructure** > **Target**, select the subscription and the resource group where you want to create the failed over virtual machines.</span></span> <span data-ttu-id="d9e23-176">選擇您想要在 Azure (傳統或資源管理) 中，針對容錯移轉虛擬機器使用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="d9e23-176">Choose the deployment model that you want to use in Azure (classic or resource management) for the failed over virtual machines.</span></span>

    ![儲存體](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. <span data-ttu-id="d9e23-178">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="d9e23-178">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    ![儲存體](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. <span data-ttu-id="d9e23-180">如果您尚未建立儲存體帳戶而想要使用 Resource Manager 建立一個帳戶，請按一下 [+儲存體帳戶] 以內嵌方式執行該作業。</span><span class="sxs-lookup"><span data-stu-id="d9e23-180">If you haven't created a storage account, and you want to create one using Resource Manager, click **+Storage account** to do that inline.</span></span>  <span data-ttu-id="d9e23-181">在 [建立儲存體帳戶]  刀鋒視窗中，指定帳戶名稱、類型、訂用帳戶和位置。</span><span class="sxs-lookup"><span data-stu-id="d9e23-181">On the **Create storage account** blade specify an account name, type, subscription, and location.</span></span> <span data-ttu-id="d9e23-182">此帳戶應位於與復原服務保存庫相同的位置。</span><span class="sxs-lookup"><span data-stu-id="d9e23-182">The account should be in the same location as the Recovery Services vault.</span></span>

   ![儲存體](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * <span data-ttu-id="d9e23-184">如果您想要使用傳統模型建立儲存體帳戶，請在 Azure 入口網站中執行該作業。</span><span class="sxs-lookup"><span data-stu-id="d9e23-184">If you want to create a storage account using the classic model, do that in the Azure portal.</span></span> [<span data-ttu-id="d9e23-185">深入了解</span><span class="sxs-lookup"><span data-stu-id="d9e23-185">Learn more</span></span>](../storage/common/storage-create-storage-account.md)
   * <span data-ttu-id="d9e23-186">如果您將進階儲存體帳戶使用於複寫的資料，則須設定其他標準儲存體帳戶來儲存複寫記錄檔，而這類記錄檔會擷取內部部署資料的進行中變更。</span><span class="sxs-lookup"><span data-stu-id="d9e23-186">If you’re using a premium storage account for replicated data, set up an additional standard storage account, to store replication logs that capture ongoing changes to on-premises data.</span></span>
5. <span data-ttu-id="d9e23-187">如果您尚未建立 Azure 網路，而且想要使用 Resource Manager 建立一個，請按一下 [+網路] 以內嵌方式執行該作業。</span><span class="sxs-lookup"><span data-stu-id="d9e23-187">If you haven't created an Azure network, and you want to create one using Resource Manager, click **+Network** to do that inline.</span></span> <span data-ttu-id="d9e23-188">在 [建立虛擬網路]  刀鋒視窗上，指定網路名稱、位址範圍、子網路詳細資料、訂用帳戶和位置。</span><span class="sxs-lookup"><span data-stu-id="d9e23-188">On the **Create virtual network** blade specify a network name, address range, subnet details, subscription, and location.</span></span> <span data-ttu-id="d9e23-189">此網路應位於與復原服務保存庫相同的位置。</span><span class="sxs-lookup"><span data-stu-id="d9e23-189">The network should be in the same location as the Recovery Services vault.</span></span>

   ![網路](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   <span data-ttu-id="d9e23-191">如果您想要使用傳統模型建立網路，請在 Azure 入口網站中執行該作業。</span><span class="sxs-lookup"><span data-stu-id="d9e23-191">If you want to create a network using the classic model, do that in the Azure portal.</span></span> <span data-ttu-id="d9e23-192">[深入了解](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="d9e23-192">[Learn more](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span>





## <a name="next-steps"></a><span data-ttu-id="d9e23-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9e23-193">Next steps</span></span>

<span data-ttu-id="d9e23-194">移至[步驟 9：設定網路對應](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="d9e23-194">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>
