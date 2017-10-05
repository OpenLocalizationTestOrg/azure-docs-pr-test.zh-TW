---
title: "在傳統入口網站中將 Hyper-V VM 複寫至 Azure | Microsoft Docs"
description: "本文說明如何將不在 VMM 雲端中管理的 Hyper-V 虛擬機器複寫至 Azure。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 438f32ee3605e2dd0c46de7993a359cc269262fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a><span data-ttu-id="b3d2c-103">使用 Azure Site Recovery 在內部部署 Hyper-V 虛擬機器與 Azure (沒有 VMM) 之間複寫</span><span class="sxs-lookup"><span data-stu-id="b3d2c-103">Replicate between on-premises Hyper-V virtual machines and Azure (without VMM) with Azure Site Recovery</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3d2c-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b3d2c-104">Azure Portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="b3d2c-105">PowerShell - 資源管理員</span><span class="sxs-lookup"><span data-stu-id="b3d2c-105">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
> * [<span data-ttu-id="b3d2c-106">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b3d2c-106">Classic Portal</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

<span data-ttu-id="b3d2c-107">本文說明如何在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務，將內部部署 Hyper-V 虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-107">This article describes how to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service, in the Azure portal.</span></span> <span data-ttu-id="b3d2c-108">在此案例中，不是在 VMM 雲端中管理 Hyper-V 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-108">In this scenario, Hyper-V servers are not managed in VMM clouds.</span></span>

<span data-ttu-id="b3d2c-109">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="site-recovery-in-the-azure-portal"></a><span data-ttu-id="b3d2c-110">Azure 入口網站中的 Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b3d2c-110">Site Recovery in the Azure portal</span></span>

<span data-ttu-id="b3d2c-111">Azure 用來建立和處理資源的[部署模型](../resource-manager-deployment-model.md)有二種 - Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-111">Azure has two different [deployment models](../resource-manager-deployment-model.md) for creating and working with resources – Azure Resource Manager and classic.</span></span> <span data-ttu-id="b3d2c-112">Azure 也有兩個入口網站 – Azure 傳統入口網站和 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-112">Azure also has two portals – the Azure classic portal, and the Azure portal.</span></span>

<span data-ttu-id="b3d2c-113">本文說明如何在傳統入口網站中進行部署。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-113">This article describes how to deploy in the classic portal.</span></span> <span data-ttu-id="b3d2c-114">傳統入口網站可用於維護現有的保存庫。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-114">The classic portal can be used to maintain existing vaults.</span></span> <span data-ttu-id="b3d2c-115">您無法使用傳統入口網站建立新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-115">You can't create new vaults using the classic portal.</span></span>

## <a name="site-recovery-in-your-business"></a><span data-ttu-id="b3d2c-116">您企業中的 Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b3d2c-116">Site Recovery in your business</span></span>

<span data-ttu-id="b3d2c-117">組織需要 BCDR 策略，以決定應用程式和資料如何在規劃與未規劃停機期間維持運作，並儘速復原到正常運作的情況。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-117">Organizations need a BCDR strategy that determines how apps and data stay running and available during planned and unplanned downtime, and recover to normal working conditions as soon as possible.</span></span> <span data-ttu-id="b3d2c-118">以下是 Site Recovery 可以提供的協助︰</span><span class="sxs-lookup"><span data-stu-id="b3d2c-118">Here's what Site Recovery can do:</span></span>

* <span data-ttu-id="b3d2c-119">在 Hyper-V VM 上執行之企業應用程式的異地保護。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-119">Offsite protection for business apps running on Hyper-V VMs.</span></span>
* <span data-ttu-id="b3d2c-120">單一位置以設定、管理和監視複寫、容錯移轉及復原。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-120">A single location to set up, manage, and monitor replication, failover, and recovery.</span></span>
* <span data-ttu-id="b3d2c-121">簡易容錯移轉至 Azure，以及從 Azure 容錯回復 (還原) 至內部部署網站中的 Hyper-V 主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-121">Simple failover to Azure, and failback (restore) from Azure to Hyper-V host servers in your on-premises site.</span></span>
* <span data-ttu-id="b3d2c-122">包含多部 VM 的復原方案，以便階層式應用程式工作負載一起容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-122">Recovery plans that include multiple VMs, so that tiered application workloads fail over together.</span></span>

## <a name="azure-prerequisites"></a><span data-ttu-id="b3d2c-123">Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="b3d2c-123">Azure prerequisites</span></span>
* <span data-ttu-id="b3d2c-124">您需要 [Microsoft Azure](https://azure.microsoft.com/) 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-124">You need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="b3d2c-125">您可以從 [免費試用](https://azure.microsoft.com/pricing/free-trial/)開始。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-125">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b3d2c-126">您需要 Azure 儲存體帳戶來儲存複寫的資料。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-126">You need an Azure storage account to store replicated data.</span></span> <span data-ttu-id="b3d2c-127">此帳戶必須啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-127">The account needs geo-replication enabled.</span></span> <span data-ttu-id="b3d2c-128">它應該與 Azure Site Recovery 保存庫位於相同的區域，且和同一個訂用帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-128">It should be in the same region as the Azure Site Recovery vault and be associated with the same subscription.</span></span> <span data-ttu-id="b3d2c-129">[深入了解 Azure 儲存體](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-129">[Learn more about Azure storage](../storage/common/storage-introduction.md).</span></span> <span data-ttu-id="b3d2c-130">請注意，我們不支援使用 [新的 Azure 入口網站](../storage/common/storage-create-storage-account.md) 來跨資源群組移動所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-130">Note that we don't support moving storage accounts created using the [new Azure portal](../storage/common/storage-create-storage-account.md) across resource groups.</span></span>
* <span data-ttu-id="b3d2c-131">您將需要 Azure 虛擬網路，如此一來，當您從主要網站容錯移轉時，Azure 虛擬機器就會連接至網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-131">You'll need an Azure virtual network so that Azure virtual machines will be connected to a network when you fail over from your primary site.</span></span>

## <a name="hyper-v-prerequisites"></a><span data-ttu-id="b3d2c-132">Hyper-V 的必要條件</span><span class="sxs-lookup"><span data-stu-id="b3d2c-132">Hyper-V prerequisites</span></span>
* <span data-ttu-id="b3d2c-133">在來源內部部署站台中，您將需要一或多部執行已安裝 Hyper-V 角色之 **Windows Server 2012 R2** 或 **Microsoft Hyper-V Server 2012 R2** 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-133">In the source on-premises site you'll need one or more servers running **Windows Server 2012 R2** with the Hyper-V role installed or **Microsoft Hyper-V Server 2012 R2**.</span></span> <span data-ttu-id="b3d2c-134">此伺服器應該：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-134">This server should:</span></span>
* <span data-ttu-id="b3d2c-135">包含一或多部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-135">Contain one or more virtual machines.</span></span>
* <span data-ttu-id="b3d2c-136">直接或透過 Proxy 連接到網際網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-136">Be connected to the Internet, either directly or via a proxy.</span></span>
* <span data-ttu-id="b3d2c-137">執行 KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977") 中所述的修正。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-137">Be running the fixes described in KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").</span></span>

## <a name="virtual-machine-prerequisites"></a><span data-ttu-id="b3d2c-138">虛擬機器先決條件</span><span class="sxs-lookup"><span data-stu-id="b3d2c-138">Virtual machine prerequisites</span></span>
<span data-ttu-id="b3d2c-139">您想要保護的虛擬機器必須符合 [Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-139">Virtual machines you want to protect should conform with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

## <a name="provider-and-agent-prerequisites"></a><span data-ttu-id="b3d2c-140">提供者和代理程式的必要條件</span><span class="sxs-lookup"><span data-stu-id="b3d2c-140">Provider and agent prerequisites</span></span>
<span data-ttu-id="b3d2c-141">在 Azure Site Recovery 部署期間，您將在每部 Hyper-V 伺服器上，安裝 Azure Site Recovery Provider 和 Azure 復原服務代理程式。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-141">As part of Azure Site Recovery deployment you’ll install the Azure Site Recovery Provider and the Azure Recovery Services Agent on each Hyper-V server.</span></span> <span data-ttu-id="b3d2c-142">請注意：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-142">Note that:</span></span>

* <span data-ttu-id="b3d2c-143">建議您一律執行最新版本的提供者和代理程式。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-143">We recommend you always run the latest versions of the Provider and agent.</span></span> <span data-ttu-id="b3d2c-144">這些程式可以在 Site Recovery 入口網站中取得。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-144">These are available in the Site Recovery portal.</span></span>
* <span data-ttu-id="b3d2c-145">保存庫中的所有 Hyper-V 伺服器應該有相同版本的提供者和代理程式。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-145">All Hyper-V servers in a vault should have the same versions of the Provider and agent.</span></span>
* <span data-ttu-id="b3d2c-146">伺服器上執行的提供者會透過網際網路連接到 Site Recovery。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-146">The Provider running on the server connects to Site Recovery over the internet.</span></span> <span data-ttu-id="b3d2c-147">您不需要使用 Poxy 就能選擇執行這個動作，方法是使用目前設定於 Hyper-V 伺服器上的 Poxy 設定，或使用您在提供者安裝期間所設定的自訂 Poxy 設定。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-147">You can do this without a proxy, with the proxy settings currently configured on the Hyper-V server, or with custom proxy settings that you configure during Provider installation.</span></span> <span data-ttu-id="b3d2c-148">您必須確定您想要使用的 Proxy 伺服器可以存取這些 URL 以連接到 Azure：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-148">You'll need to make sure that the proxy server you want to use can access these the URLs for connecting to Azure:</span></span>

  * <span data-ttu-id="b3d2c-149">*.accesscontrol.windows.net</span><span class="sxs-lookup"><span data-stu-id="b3d2c-149">*.accesscontrol.windows.net</span></span>
  * <span data-ttu-id="b3d2c-150">*.backup.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="b3d2c-150">*.backup.windowsazure.com</span></span>
  * <span data-ttu-id="b3d2c-151">*.hypervrecoverymanager.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="b3d2c-151">*.hypervrecoverymanager.windowsazure.com</span></span>
  * <span data-ttu-id="b3d2c-152">*.store.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b3d2c-152">*.store.core.windows.net</span></span>      
  * <span data-ttu-id="b3d2c-153">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="b3d2c-153">*.blob.core.windows.net</span></span>
  - <span data-ttu-id="b3d2c-154">https://www.msftncsi.com/ncsi.txt</span><span class="sxs-lookup"><span data-stu-id="b3d2c-154">https://www.msftncsi.com/ncsi.txt</span></span>
  - <span data-ttu-id="b3d2c-155">time.windows.com</span><span class="sxs-lookup"><span data-stu-id="b3d2c-155">time.windows.com</span></span>
  - <span data-ttu-id="b3d2c-156">time.nist.gov</span><span class="sxs-lookup"><span data-stu-id="b3d2c-156">time.nist.gov</span></span>
* <span data-ttu-id="b3d2c-157">此外，允許 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653) 中所述的 IP 位址和 HTTPS (443) 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-157">In addition allow the IP addresses described in [Azure Datacenter IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) and HTTPS (443) protocol.</span></span> <span data-ttu-id="b3d2c-158">您必須具有打算使用以及美國西部之 Azure 區域的 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-158">You have to allow the IP ranges of the Azure region that you plan to use and that of West US.</span></span>

<span data-ttu-id="b3d2c-159">下圖顯示 Site Recovery 為協調流程與複寫所使用的不同通訊通道與連接埠</span><span class="sxs-lookup"><span data-stu-id="b3d2c-159">This graphic shows the different communication channels and ports used by Site Recovery for orchestration and replication</span></span>

![B2A 拓樸](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a><span data-ttu-id="b3d2c-161">步驟 1：建立保存庫</span><span class="sxs-lookup"><span data-stu-id="b3d2c-161">Step 1: Create a vault</span></span>
1. <span data-ttu-id="b3d2c-162">登入 [管理入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-162">Sign in to the [Management Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3d2c-163">展開 [資料服務]  >  [復原服務]，然後按一下 [Site Recovery 保存庫]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-163">Expand **Data Services** > **Recovery Services** and click **Site Recovery Vault**.</span></span>
3. <span data-ttu-id="b3d2c-164">按一下 [新建]  >  [快速建立]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-164">Click **Create New** > **Quick Create**.</span></span>
4. <span data-ttu-id="b3d2c-165">在 [ **名稱**] 中，輸入保存庫的易記識別名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-165">In **Name**, enter a friendly name to identify the vault.</span></span>
5. <span data-ttu-id="b3d2c-166">在 [地區] 中，選取保存庫的地理區域。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-166">In **Region**, select the geographic region for the vault.</span></span> <span data-ttu-id="b3d2c-167">若要查看支援的區域，請參閱 [Azure Site Recovery 定價詳細資料](https://azure.microsoft.com/pricing/details/site-recovery/)中的＜各地區上市情況＞。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-167">To check supported regions see Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
6. <span data-ttu-id="b3d2c-168">按一下 [建立保存庫] 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-168">Click **Create vault**.</span></span>

    ![新增保存庫](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

<span data-ttu-id="b3d2c-170">檢查狀態列，以確認是否順利建立保存庫。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-170">Check the status bar to confirm that the vault was successfully created.</span></span> <span data-ttu-id="b3d2c-171">保存庫在主要復原服務頁面上會列為 [使用中]  。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-171">The vault will be listed as **Active** on the main Recovery Services page.</span></span>

## <a name="step-2-create-a-hyper-v-site"></a><span data-ttu-id="b3d2c-172">步驟 2：建立 Hyper-V 站台</span><span class="sxs-lookup"><span data-stu-id="b3d2c-172">Step 2: Create a Hyper-V site</span></span>
1. <span data-ttu-id="b3d2c-173">在 [復原服務] 頁面中，按一下保存庫以開啟 [快速入門] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-173">In the Recovery Services page, click the vault to open the Quick Start page.</span></span> <span data-ttu-id="b3d2c-174">您也可以使用圖示隨時開啟 [快速啟動]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-174">Quick Start can also be opened at any time using the icon.</span></span>

    ![快速啟動](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. <span data-ttu-id="b3d2c-176">在下拉式清單中，選取 [在內部部署 Hyper-V 站台與 Azure 之間] 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-176">In the dropdown list, select **Between an on-premises Hyper-V site and Azure**.</span></span>

    ![Hyper-V 站台案例](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. <span data-ttu-id="b3d2c-178">在 [建立 Hyper-V 站台] 中，按一下 [建立 Hyper-V 站台]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-178">In **Create a Hyper-V Site** click **Create Hyper-V site**.</span></span> <span data-ttu-id="b3d2c-179">指定站台名稱並儲存。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-179">Specify a site name and save.</span></span>

    ![Hyper-V 站台](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-the-provider-and-agent"></a><span data-ttu-id="b3d2c-181">步驟 3：安裝提供者和代理程式</span><span class="sxs-lookup"><span data-stu-id="b3d2c-181">Step 3: Install the Provider and agent</span></span>
<span data-ttu-id="b3d2c-182">在具有您想要保護的 VM 的每部 Hyper-V 伺服器上，安裝提供者和代理程式。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-182">Install the Provider and agent on each Hyper-V server that has VMs you want to protect.</span></span>

<span data-ttu-id="b3d2c-183">如果您正在 Hyper-V 叢集上進行安裝，請在容錯移轉叢集中的每個節點上執行步驟 5-11 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-183">If you're installing on a Hyper-V cluster, performs steps 5-11 on each node in the failover cluster.</span></span> <span data-ttu-id="b3d2c-184">在註冊所有節點並啟用保護之後，虛擬機器將會受到保護，即使它們在叢集中的節點間進行移轉也一樣。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-184">After all nodes are registered and protection is enabled, virtual machines will be protected even if they migrate across nodes in the cluster.</span></span>

1. <span data-ttu-id="b3d2c-185">在 [準備 Hyper-V 伺服器] 中，按一下 [下載註冊金鑰] 檔案。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-185">In **Prepare Hyper-V servers**, click **Download a registration key** file.</span></span>
2. <span data-ttu-id="b3d2c-186">在 [下載註冊金鑰] 頁面上，按一下站台旁邊的 [下載]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-186">On the **Download Registration Key** page, click **Download** next to the site.</span></span> <span data-ttu-id="b3d2c-187">將金鑰下載到 Hyper-V 伺服器容易存取的安全位置。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-187">Download the key to a safe location that can be easily accessed by the Hyper-V server.</span></span> <span data-ttu-id="b3d2c-188">該金鑰在產生後會維持 5 天有效。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-188">The key is valid for 5 days after it's generated.</span></span>

    ![註冊金鑰](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. <span data-ttu-id="b3d2c-190">按一下 [下載提供者]  來取得最新版本。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-190">Click **Download the Provider** to obtain the latest version.</span></span>
4. <span data-ttu-id="b3d2c-191">在您想要於保存庫中註冊的每一部 Hyper-V 伺服器上執行該檔案。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-191">Run the file on each Hyper-V server you want to register in the vault.</span></span> <span data-ttu-id="b3d2c-192">該檔案會安裝兩個元件：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-192">The file installs two components:</span></span>
   * <span data-ttu-id="b3d2c-193">**Azure Site Recovery Provider**- 處理 Hyper-V 伺服器與 Azure Site Recovery 入口網站之間的通訊和協調流程。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-193">**Azure Site Recovery Provider**—Handles communication and orchestration between the Hyper-V server and the Azure Site Recovery portal.</span></span>
   * <span data-ttu-id="b3d2c-194">**Azure 復原服務代理程式**- 處理在來源 Hyper-V 伺服器上執行之虛擬機器與 Azure 儲存體之間的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-194">**Azure Recovery Services Agent**—Handles data transport between virtual machines running on the source Hyper-V server and Azure storage.</span></span>
5. <span data-ttu-id="b3d2c-195">在 [Microsoft Update]  中，您可以選擇加入以取得更新。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-195">In **Microsoft Update** you can opt in for updates.</span></span> <span data-ttu-id="b3d2c-196">啟用這項設定時，會根據您的 Microsoft Update 原則來安裝提供者和代理程式更新。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-196">With this setting enabled, Provider and Agent updates will be installed according to your Microsoft Update policy.</span></span>

    ![Microsoft Update](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. <span data-ttu-id="b3d2c-198">在 [安裝]  中，指定要將提供者和代理程式安裝到 Hyper-V 伺服器上的哪個位置。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-198">In **Installation** specify where you want to install the Provider and Agent on the Hyper-V server.</span></span>

    ![安裝位置](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. <span data-ttu-id="b3d2c-200">安裝完成之後，請繼續設定以在保存庫中註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-200">After installation is complete continue setup to register the server in the vault.</span></span>
8. <span data-ttu-id="b3d2c-201">在 [保存庫設定] 頁面上，按一下 [瀏覽] 來選取金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-201">On the **Vault Settings** page, click **Browse** to select the key file.</span></span> <span data-ttu-id="b3d2c-202">指定 Azure Site Recovery 訂用帳戶、保存庫名稱，以及 Hyper-V 伺服器所屬的 Hyper-V 網站。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-202">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. <span data-ttu-id="b3d2c-204">在 [網際網路連線]  頁面上，您將指定提供者連接到 Azure Site Recovery 的方式。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-204">On the **Internet Connection** page you specify how the Provider connects to Azure Site Recovery.</span></span> <span data-ttu-id="b3d2c-205">選取 [Use default system proxy settings]  ，以使用在伺服器上設定的預設網際網路連線設定。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-205">Select **Use default system proxy settings** to use the default Internet connection settings configured on the server.</span></span> <span data-ttu-id="b3d2c-206">如果未指定值，將使用預設設定。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-206">If you don't specify a value the default settings will be used.</span></span>

   ![網際網路設定](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. <span data-ttu-id="b3d2c-208">註冊作業會開始在保存庫中註冊伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-208">Registration starts to register the server in the vault.</span></span>

    ![伺服器註冊](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. <span data-ttu-id="b3d2c-210">註冊完成之後，Azure Site Recovery 便會擷取來自 Hyper-V 伺服器的中繼資料，而該伺服器會顯示在保存庫中 [伺服器] 頁面的 [Hyper-V 站台] 索引標籤上 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-210">After registration finishes metadata from the Hyper-V server is retrieved by Azure Site Recovery and the server is displayed on the **Hyper-V Sites** tab on the **Servers** page in the vault.</span></span>

### <a name="install-the-provider-from-the-command-line"></a><span data-ttu-id="b3d2c-211">從命令列安裝提供者</span><span class="sxs-lookup"><span data-stu-id="b3d2c-211">Install the Provider from the command line</span></span>
<span data-ttu-id="b3d2c-212">或者，您可以從命令列安裝 Azure Site Recovery 提供者。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-212">As an alternative you can install the Azure Site Recovery Provider from the command line.</span></span> <span data-ttu-id="b3d2c-213">如果您想要在執行 Windows Server Core 2012 R2 的電腦上安裝提供者，您應該使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-213">You should use this method if you want to install the Provider on a computer running Windows Server Core 2012 R2.</span></span> <span data-ttu-id="b3d2c-214">從命令列執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-214">Run from the command line as follows:</span></span>

1. <span data-ttu-id="b3d2c-215">將提供者安裝檔案和註冊金鑰下載至資料夾。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-215">Download the Provider installation file and registration key to a folder.</span></span> <span data-ttu-id="b3d2c-216">例如 C:\ASR。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-216">For example C:\ASR.</span></span>
2. <span data-ttu-id="b3d2c-217">以系統管理員身分開啟 [命令提示字元] 並輸入：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-217">Run a command prompt as an Administrator and type:</span></span>

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="b3d2c-218">然後執行下列命令以安裝提供者：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-218">Then install the Provider by running:</span></span>

        C:\ASR> setupdr.exe /i
4. <span data-ttu-id="b3d2c-219">執行下列命令以完成註冊：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-219">Run the following to complete registration:</span></span>

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of the server> /Credentials <path of the credentials file> /EncryptionEnabled <full file name to save the encryption certificate>         

<span data-ttu-id="b3d2c-220">參數包括：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-220">Where parameters include:</span></span>

* <span data-ttu-id="b3d2c-221">**/Credentials**：指定您下載的註冊金鑰的位置。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-221">**/Credentials**: Specify the location of the registration key you downloaded.</span></span>
* <span data-ttu-id="b3d2c-222">**/FriendlyName**：指定名稱以識別 Hyper-V 主機伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-222">**/FriendlyName**: Specify a name to identify the Hyper-V host server.</span></span> <span data-ttu-id="b3d2c-223">這個名稱會出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-223">This name will appear in the portal</span></span>
* <span data-ttu-id="b3d2c-224">**/EncryptionEnabled**：選擇性。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-224">**/EncryptionEnabled**: Optional.</span></span> <span data-ttu-id="b3d2c-225">指定是否要在 Azure 中加密複本虛擬機器 (靜態加密)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-225">Specify whether you want to encrypt replica virtual machines in Azure (at rest encryption).</span></span>
* <span data-ttu-id="b3d2c-226">**/proxyAddress**；**/proxyport**；**/proxyUsername**；**/proxyPassword**：選擇性。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-226">**/proxyAddress**; **/proxyport**; **/proxyUsername**; **/proxyPassword**: Optional.</span></span> <span data-ttu-id="b3d2c-227">如果您想要使用自訂 proxy，或您現有的 proxy 需要驗證，請指定 proxy 參數。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-227">Specify proxy parameters if you want to use a custom proxy, or your existing proxy requires authentication.</span></span>

## <a name="step-4-create-an-azure-storage-account"></a><span data-ttu-id="b3d2c-228">步驟 4：建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b3d2c-228">Step 4: Create an Azure storage account</span></span>
* <span data-ttu-id="b3d2c-229">在 [準備資源] 中選取 [建立儲存體帳戶]，以建立 Azure 儲存體帳戶 (如果您沒有儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-229">In **Prepare resources** select **Create Storage Account**  to create an Azure storage account if you don't have one.</span></span> <span data-ttu-id="b3d2c-230">此帳戶應啟用異地複寫。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-230">The account should have geo-replication enabled.</span></span> <span data-ttu-id="b3d2c-231">它應該與 Azure Site Recovery 保存庫位於相同的區域，並與同一個訂用帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-231">It should be in the same region as the Azure Site Recovery vault, and be associated with the same subscription.</span></span>

    ![建立儲存體帳戶](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. <span data-ttu-id="b3d2c-233">我們不支援使用 [新的 Azure 入口網站](../storage/common/storage-create-storage-account.md) 來跨資源群組移動所建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-233">We do not support the move of Storage accounts created using the [new Azure portal](../storage/common/storage-create-storage-account.md) across resource groups.</span></span>
> 2. <span data-ttu-id="b3d2c-234">對於用於部署 Site Recovery 的儲存體帳戶，不支援跨相同訂用帳戶內的資源群組或跨訂用帳戶[移轉儲存體帳戶](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-234">[Migration of storage accounts](../azure-resource-manager/resource-group-move-resources.md) across resource groups within the same subscription or across subscriptions is not supported for storage accounts used for deploying Site Recovery.</span></span>
>

## <a name="step-5-create-and-configure-protection-groups"></a><span data-ttu-id="b3d2c-235">步驟 5：建立和設定保護群組</span><span class="sxs-lookup"><span data-stu-id="b3d2c-235">Step 5: Create and configure protection groups</span></span>
<span data-ttu-id="b3d2c-236">保護群組是虛擬機器的邏輯群組，您想要使用相同的保護設定來保護這類群組。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-236">Protection groups are logical groupings of virtual machines that you want to protect using the same protection settings.</span></span> <span data-ttu-id="b3d2c-237">您只要將保護設定套用至保護群組，這些設定就會套用至您新增至該群組中的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-237">You apply protection settings to a protection group, and those settings are applied to all virtual machines that you add to the group.</span></span>

1. <span data-ttu-id="b3d2c-238">在 [建立和設定保護群組] 中，按一下 [建立保護群組]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-238">In **Create and configure protection groups** click **Create a protection group**.</span></span> <span data-ttu-id="b3d2c-239">如果有任何必要條件不符，系統就會發出訊息，您可以按一下 [檢視詳細資料]  來取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-239">If any prerequisites aren't in place a message is issued and you can click **View details** for more information.</span></span>
2. <span data-ttu-id="b3d2c-240">在 [保護群組] 索引標籤中，新增保護群組。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-240">In the **Protection Groups** tab, add a protection group.</span></span> <span data-ttu-id="b3d2c-241">指定名稱、來源 Hyper-V 網站、目標 **Azure**、您的 Azure Site Recovery 訂用帳戶名稱，以及 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-241">Specify a name, the source Hyper-V site, the target **Azure**, your Azure Site Recovery subscription name, and the Azure storage account.</span></span>

    ![保護群組](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. <span data-ttu-id="b3d2c-243">在 [複寫設定] 中，設定 [複製頻率]，來指定應在來源和目標之間同步處理資料差異的頻率。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-243">In **Replication settings** set the **Copy frequency** to specify how often the data delta should be synchronized between the source and target.</span></span> <span data-ttu-id="b3d2c-244">您可以設定為 30 秒、5 分鐘或 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-244">You can set to 30 seconds, 5 minutes, or 15 minutes.</span></span>
4. <span data-ttu-id="b3d2c-245">在 [保留復原點]  中，指定復原歷程記錄應該儲存多少個小時。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-245">In **Retain recovery points** specify how many hours of recovery history should be stored.</span></span>
5. <span data-ttu-id="b3d2c-246">在 [應用程式一致快照的頻率]  中，您可以指定是否要建立快照，使用「磁碟區陰影複製服務」(VSS) 來確保建立快照時，應用程式是處於一致狀態。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-246">In **Frequency of application-consistent snapshots** you can specify whether to take snapshots that use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="b3d2c-247">預設不會建立這些快照。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-247">By default these aren't taken.</span></span> <span data-ttu-id="b3d2c-248">請確定已將此值設定為小於您設定的其他復原點數目。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-248">Make sure this value is set to less than the number of additional recovery points you configure.</span></span> <span data-ttu-id="b3d2c-249">只有當虛擬機器正在執行 Windows 作業系統時，才支援此功能。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-249">This is only supported if the virtual machine is running a Windows operating system.</span></span>
6. <span data-ttu-id="b3d2c-250">在 [初始複寫開始時間]  中，指定何時應將保護群組中虛擬機器的初始複寫傳送到 Azure。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-250">In **Initial replication start time** specify when initial replication of virtual machines in the protection group should be sent to Azure.</span></span>

    ![保護群組](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a><span data-ttu-id="b3d2c-252">步驟 6：啟用虛擬機器保護</span><span class="sxs-lookup"><span data-stu-id="b3d2c-252">Step 6: Enable virtual machine protection</span></span>
<span data-ttu-id="b3d2c-253">將虛擬機器新增到保護群組，為其啟用保護。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-253">Add virtual machines to a protection group to enable protection for them.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d2c-254">不支援保護使用靜態 IP 位址執行 Linux 的 VM。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-254">Protecting VMs running Linux with a static IP address isn't supported.</span></span>
>
>

1. <span data-ttu-id="b3d2c-255">在保護群組的 [機器] 索引標籤上，按一下 [將虛擬機器加入保護群組以啟用保護]****。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-255">On the **Machines** tab for the protection group, click** Add virtual machines to protection groups to enable protection**.</span></span>
2. <span data-ttu-id="b3d2c-256">在 [啟用虛擬機器保護]  頁面上，選取要保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-256">On the **Enable Virtual Machine Protection** page select the virtual machines you want to protect.</span></span>

    ![啟用虛擬機器保護](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    <span data-ttu-id="b3d2c-258">「啟用保護」工作隨即開始。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-258">The Enable Protection jobs begins.</span></span> <span data-ttu-id="b3d2c-259">您可以在 [工作]  索引標籤上追蹤進度。執行「完成保護」工作之後，虛擬機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-259">You can track progress on the **Jobs** tab. After the Finalize Protection job runs the virtual machine is ready for failover.</span></span>
3. <span data-ttu-id="b3d2c-260">設定保護之後，您可以：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-260">After protection is set up you can:</span></span>

   * <span data-ttu-id="b3d2c-261">在 [受保護的項目]  >  [保護群組]  >  *rotectiongroup_name*  >  [虛擬機器] 中檢視虛擬機器。您可以在 [屬性] 索引標籤中向下切入到機器詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-261">View virtual machines in **Protected Items** > **Protection Groups** > *protectiongroup_name* > **Virtual Machines** You can drill down to machine details in the **Properties** tab..</span></span>
   * <span data-ttu-id="b3d2c-262">在 [受保護的項目]  >  [保護群組]  >  *protectiongroup_name*  >  [虛擬機器] *virtual_machine_name*  >  [設定] 中，設定虛擬機器的容錯移轉屬性。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-262">Configure the failover properties for a virtual machines in **Protected Items** > **Protection Groups** > *protectiongroup_name* > **Virtual Machines** *virtual_machine_name* > **Configure**.</span></span> <span data-ttu-id="b3d2c-263">您可以設定：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-263">You can configure:</span></span>

     * <span data-ttu-id="b3d2c-264">**名稱**：Azure 中的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-264">**Name**: The name of the virtual machine in Azure.</span></span>
     * <span data-ttu-id="b3d2c-265">**大小**：要容錯移轉之虛擬機器的目標大小。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-265">**Size**: The target size of the virtual machine that fails over.</span></span>

       ![設定虛擬機器屬性](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * <span data-ttu-id="b3d2c-267">在 [受保護的項目]* > [保護群組] > *protectiongroup_name* > [虛擬機器] *virtual_machine_name* > [設定] 中，設定其他虛擬機器設定，包括：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-267">Configure additional virtual machine settings in *Protected Items** > **Protection Groups** > *protectiongroup_name* > **Virtual Machines** *virtual_machine_name* > **Configure**, including:</span></span>

     * <span data-ttu-id="b3d2c-268">**網路介面卡**：網路介面卡的數目取決於您針對目標虛擬機器所指定的大小。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-268">**Network adapters**: The number of network adapters is dictated by the size you specify for the target virtual machine.</span></span> <span data-ttu-id="b3d2c-269">查看 [虛擬機器大小規格](../virtual-machines/linux/sizes.md) ，了解虛擬機器大小所支援的 NIC 數目。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-269">Check [virtual machine size specs](../virtual-machines/linux/sizes.md) for the number of nics supported by the virtual machine size.</span></span>

       <span data-ttu-id="b3d2c-270">在修改虛擬機器的大小並儲存設定之後，當您下次開啟 [設定]  頁面時，網路介面卡的數量將會改變。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-270">When you modify the size for a virtual machine and save the settings, the number of network adapter will change when you open **Configure** page the next time.</span></span> <span data-ttu-id="b3d2c-271">目標虛擬機器的網路介面卡數目，是來源虛擬機器上的網路介面卡數目下限，以及所選虛擬機器大小支援的網路介面卡數目上限。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-271">The number of network adapters of target virtual machines is minimum of the number of network adapters on source virtual machine and maximum number of network adapters supported by the size of the virtual machine chosen.</span></span> <span data-ttu-id="b3d2c-272">其說明如下：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-272">It is explained below:</span></span>

       * <span data-ttu-id="b3d2c-273">如果來源電腦上的網路介面卡數目小於或等於針對目標機器大小所允許的介面卡數目，則目標將具備與來源相同的介面卡數目。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-273">If the number of network adapters on the source machine is less than or equal to the number of adapters allowed for the target machine size, then the target will have the same number of adapters as the source.</span></span>
       * <span data-ttu-id="b3d2c-274">如果來源虛擬機器的介面卡數目超過針對目標大小所允許的數目，則將使用目標大小的最大值。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-274">If the number of adapters for the source virtual machine exceeds the number allowed for the target size then the target size maximum will be used.</span></span>
       * <span data-ttu-id="b3d2c-275">例如，如果來源機器具有兩張網路介面卡，而目標機器大小支援四張，則目標機器將會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-275">For example if a source machine has two network adapters and the target machine size supports four, the target machine will have two adapters.</span></span> <span data-ttu-id="b3d2c-276">如果來源機器具有兩張介面卡，但支援的目標大小僅支援一張，則目標機器將只會有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-276">If the source machine has two adapters but the supported target size only supports one then the target machine will have only one adapter.</span></span>

     * <span data-ttu-id="b3d2c-277">**Azure 網路**：指定應將虛擬機器容錯移轉到其中的目標網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-277">**Azure network**: Specify the network to which the virtual machine should fail over.</span></span> <span data-ttu-id="b3d2c-278">如果虛擬機器具有多張網路介面卡，則所有的介面卡都應該連接到同一個 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-278">If the virtual machine has multiple network adapters all adapters should connected to the same Azure network.</span></span>
     * <span data-ttu-id="b3d2c-279">**子網路** ：針對虛擬機器上的每張網路介面卡，請選取 Azure 網路中的子網路，機器在容錯移轉之後應會連接到該子網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-279">**Subnet** For each network adapter on the virtual machine, select the subnet in the Azure network to which the machine should connect after failover.</span></span>
     * <span data-ttu-id="b3d2c-280">**目標 IP 位址**：如果來源虛擬機器的網路介面卡已設定為使用靜態 IP 位址，則您可以指定目標虛擬機器的 IP 位址，以確保機器在容錯移轉後會有相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-280">**Target IP address**: If the network adapter of source virtual machine is configured to use static a IP address then you can specify the IP address for the target virtual machine to ensure that the machine has the same IP address after failover.</span></span>  <span data-ttu-id="b3d2c-281">如果您未指定 IP 位址，則系統將在容錯移轉期間指派任何可用的位址。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-281">If you don't specify an IP address then any available address will be assigned at the time of failover.</span></span> <span data-ttu-id="b3d2c-282">如果您指定了使用中的位址，則容錯移轉將會失敗。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-282">If you specify an address that's in use then failover will fail.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b3d2c-283">對於用於部署 Site Recovery 的網路，不支援跨相同訂用帳戶內的資源群組或跨訂用帳戶[移轉網路](../azure-resource-manager/resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-283">[Migration of networks](../azure-resource-manager/resource-group-move-resources.md) across resource groups within the same subscription or across subscriptions is not supported for networks used for deploying Site Recovery.</span></span>
     >

     ![設定虛擬機器屬性](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a><span data-ttu-id="b3d2c-285">步驟 7：建立復原計畫</span><span class="sxs-lookup"><span data-stu-id="b3d2c-285">Step 7: Create a recovery plan</span></span>
<span data-ttu-id="b3d2c-286">為測試部署，您可以針對單一虛擬機器執行測試容錯移轉，或執行包含一或多部虛擬機器的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-286">In order to test the deployment you can run a test failover for a single virtual machine or a recovery plan that contains one or more virtual machines.</span></span> <span data-ttu-id="b3d2c-287">[深入了解](site-recovery-create-recovery-plans.md) 如何建立復原計劃。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-287">[Learn more](site-recovery-create-recovery-plans.md) about creating a recovery plan.</span></span>

## <a name="step-8-test-the-deployment"></a><span data-ttu-id="b3d2c-288">步驟 8：測試部署</span><span class="sxs-lookup"><span data-stu-id="b3d2c-288">Step 8: Test the deployment</span></span>
<span data-ttu-id="b3d2c-289">有兩種方式可以測試容錯移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-289">There are two ways to run a test failover to Azure.</span></span>

* <span data-ttu-id="b3d2c-290">**在沒有 Azure 網路的情況下測試容錯移轉**—這種測試容錯移轉可以檢查虛擬機器是否正確地出現在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-290">**Test failover without an Azure network**—This type of test failover checks that the virtual machine comes up correctly in Azure.</span></span> <span data-ttu-id="b3d2c-291">在容錯移轉之後，虛擬機器不會連線到任何 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-291">The virtual machine won’t be connected to any Azure network after failover.</span></span>
* <span data-ttu-id="b3d2c-292">**利用 Azure 網路測試容錯移轉**—這種測試容錯移轉可以檢查整個復寫環境是否如預期般出現並進行容錯移轉，虛擬機器會連線到只訂的目標 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-292">**Test failover with an Azure network**—This type of failover checks that the entire replication environment comes up as expected and that failed over the virtual machines connects to the specified target Azure network.</span></span> <span data-ttu-id="b3d2c-293">請注意，針對測試容錯移轉，可根據複本虛擬機器的子網路得知測試虛擬機器的子網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-293">Note that for test failover the subnet of the test virtual machine will be figured out based on the subnet of the replica virtual machine.</span></span> <span data-ttu-id="b3d2c-294">這和一般的複寫不同，一般複寫的複本虛擬機器子網路是根據來源虛擬機器的子網路得知。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-294">This is different to regular replication when the subnet of a replica virtual machine is based on the subnet of the source virtual machine.</span></span>

<span data-ttu-id="b3d2c-295">如果您想要執行測試容錯轉移，卻不想指定 Azure 網路，您不需要作任何準備。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-295">If you want to run a test failover without specifying an Azure network you don’t need to prepare anything.</span></span>

<span data-ttu-id="b3d2c-296">若要以目標 Azure 網路執行測試容錯移轉，您必須建立與您的 Azure 正式作業網路 (當您在 Azure 中建立新網路時的預設行為) 分隔的新的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-296">To run a test failover with a target Azure network you’ll need to create a new Azure network that’s isolated from your Azure production network (default behavior when you create a new network in Azure).</span></span> <span data-ttu-id="b3d2c-297">如需詳細資訊，請參閱 [執行測試容錯移轉](site-recovery-failover.md) 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-297">Read [run a test failover](site-recovery-failover.md) for more details.</span></span>

<span data-ttu-id="b3d2c-298">若要完整測試您的複寫和網路部署，您必須針對複寫虛擬機器設定基礎結構，以如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-298">To fully test your replication and network deployment you'll need to set up the infrastructure so that the replicated virtual machine to work as expected.</span></span> <span data-ttu-id="b3d2c-299">其中一個方式是將虛擬機器設定為具有 DNS 的網域控制站，並且使用 Site Recovery 將其複寫至 Azure，以藉由執行測試容錯移轉在測試網路中建立它。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-299">One way of doing this to to set up a virtual machine as a domain controller with DNS and replicate it to Azure using Site Recovery to create it in the test network by running a test failover.</span></span>  <span data-ttu-id="b3d2c-300">[深入了解](site-recovery-active-directory.md#test-failover-considerations) Active Directory 的測試容錯移轉考量。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-300">[Read more](site-recovery-active-directory.md#test-failover-considerations) about test failover considerations for Active Directory.</span></span>

<span data-ttu-id="b3d2c-301">執行測試容錯移轉，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-301">Run the test failover as follows:</span></span>

> [!NOTE]
> <span data-ttu-id="b3d2c-302">若要在執行容錯移轉至 Azure 時獲得最佳效能，請確保您已經在受保護的機器上安裝 Azure 代理程式。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-302">To get the best performance when you do a failover to Azure, ensure that you have installed the Azure Agent in the protected machine.</span></span> <span data-ttu-id="b3d2c-303">這有助於更快速開機，也有助於診斷發生的問題。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-303">This helps in booting faster and also helps in diagnosis in case of issues.</span></span> <span data-ttu-id="b3d2c-304">您可以在[這裡](https://github.com/Azure/WALinuxAgent)找到 Linux 代理程式，而 Windows 代理程式則可在[這裡](http://go.microsoft.com/fwlink/?LinkID=394789)找到</span><span class="sxs-lookup"><span data-stu-id="b3d2c-304">Linux agent can be found [here](https://github.com/Azure/WALinuxAgent) - and Windows agent can be found [here](http://go.microsoft.com/fwlink/?LinkID=394789)</span></span>
>
>

1. <span data-ttu-id="b3d2c-305">在 [復原計畫] 索引標籤上，選取計畫，然後按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-305">On the **Recovery Plans** tab, select the plan and click **Test Failover**.</span></span>
2. <span data-ttu-id="b3d2c-306">在 [確認測試容錯移轉] 頁面上，選取 [無] 或特定的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-306">On the **Confirm Test Failover** page select **None** or a specific Azure network.</span></span>  <span data-ttu-id="b3d2c-307">請注意，如果選取 [無]  ，測試容錯移轉將會檢查虛擬機器是否會正確複寫到 Azure，但並不會檢查您的複寫網路組態。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-307">Note that if you select **None** the test failover will check that the virtual machine replicated correctly to Azure but doesn't check your replication network configuration.</span></span>

    ![測試容錯移轉](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. <span data-ttu-id="b3d2c-309">在 [工作]  索引標籤上，您可以追蹤容錯移轉進度。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-309">On the **Jobs** tab you can track failover progress.</span></span> <span data-ttu-id="b3d2c-310">您應該可以在 Azure 入口網站中看到該虛擬機器測試複本。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-310">You should also be able to see the virtual machine test replica in the Azure portal.</span></span> <span data-ttu-id="b3d2c-311">如果您設定從內部部署網路存取虛擬機器，您可以初始化虛擬機器的「遠端桌面」連線。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-311">If you’re set up to access virtual machines from your on-premises network you can initiate a Remote Desktop connection to the virtual machine.</span></span>
4. <span data-ttu-id="b3d2c-312">當容錯移轉到達 [完成測試] 階段時，請按一下 [完成測試] 以完成測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-312">When the failover reaches the **Complete testing** phase , click **Complete Test** to finish up the test failover.</span></span> <span data-ttu-id="b3d2c-313">您可以向下切入到 [工作]  索引標籤，來追蹤容錯移轉進度和狀態，並執行任何所需的動作。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-313">You can drill down to the **Job** tab to track failover progress and status, and to perform any actions that are needed.</span></span>
5. <span data-ttu-id="b3d2c-314">在容錯移轉之後，您將可以在 Azure 入口網站中看到該虛擬機器測試複本。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-314">After  failover you'll be able to see the virtual machine test replica in the Azure portal.</span></span> <span data-ttu-id="b3d2c-315">如果您設定從內部部署網路存取虛擬機器，您可以初始化虛擬機器的「遠端桌面」連線。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-315">If you’re set up to access virtual machines from your on-premises network you can initiate a Remote Desktop connection to the virtual machine.</span></span>

   1. <span data-ttu-id="b3d2c-316">確認虛擬機器成功啟動。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-316">Verify that the virtual machines start successfully.</span></span>
   2. <span data-ttu-id="b3d2c-317">如果您在容錯移轉之後要使用遠端桌面連接到 Azure 中的虛擬機器，請先在虛擬機器上啟用遠端桌面連線，再執行測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-317">If you want to connect to the virtual machine in Azure using Remote Desktop after the failover, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span> <span data-ttu-id="b3d2c-318">您也必須在虛擬機器上新增 RDP 端點。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-318">You will also need to add an RDP endpoint on the virtual machine.</span></span> <span data-ttu-id="b3d2c-319">您可以利用 [Azure 自動化 Runbook](site-recovery-runbook-automation.md) 來執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-319">You can leverage an [Azure automation runbook](site-recovery-runbook-automation.md) to do that.</span></span>
   3. <span data-ttu-id="b3d2c-320">容錯移轉之後，如果您使用公用 IP 位址，利用 [遠端桌面] 連接到 Azure 中的虛擬機器，請確定您沒有任何網域原則會阻止您使用公用位址連接到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-320">After failover if you use a public IP address to connect to the virtual machine in Azure using Remote Desktop, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>
6. <span data-ttu-id="b3d2c-321">測試完成之後，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-321">After the testing is complete do the following:</span></span>

   * <span data-ttu-id="b3d2c-322">按一下 [測試容錯移轉完成] 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-322">Click **The test failover is complete**.</span></span> <span data-ttu-id="b3d2c-323">清除測試環境，以自動關閉電源及刪除測試虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-323">Clean up the test environment to automatically power off and delete the test virtual machines.</span></span>
   * <span data-ttu-id="b3d2c-324">按一下 [記事]  記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-324">Click **Notes** to record and save any observations associated with the test failover.</span></span>
7. <span data-ttu-id="b3d2c-325">當容錯移轉到達 [完成測試]  階段時，請依下列方式完成驗證：</span><span class="sxs-lookup"><span data-stu-id="b3d2c-325">When the failover reaches the **Complete testing** phase finish the verification as follows:</span></span>
   1. <span data-ttu-id="b3d2c-326">在 Azure 入口網站中檢視複本虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-326">View the replica virtual machine in the Azure portal.</span></span> <span data-ttu-id="b3d2c-327">確認虛擬機器成功啟動。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-327">Verify that the virtual machine starts successfully.</span></span>
   2. <span data-ttu-id="b3d2c-328">如果您設定從內部部署網路存取虛擬機器，您可以初始化虛擬機器的「遠端桌面」連線。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-328">If you’re set up to access virtual machines from your on-premises network you can initiate a Remote Desktop connection to the virtual machine.</span></span>
   3. <span data-ttu-id="b3d2c-329">按一下 [完成測試]  來完成它。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-329">Click **Complete the test** to finish it.</span></span>
   4. <span data-ttu-id="b3d2c-330">按一下 [記事]  記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-330">Click **Notes** to record and save any observations associated with the test failover.</span></span>
   5. <span data-ttu-id="b3d2c-331">按一下 [測試容錯移轉完成] 。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-331">Click **The test failover is complete**.</span></span> <span data-ttu-id="b3d2c-332">清除測試環境，以自動關閉電源及刪除測試虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-332">Clean up the test environment to automatically power off and delete the test virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3d2c-333">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3d2c-333">Next steps</span></span>
<span data-ttu-id="b3d2c-334">在您的部署設定完成並開始執行之後， [深入了解](site-recovery-failover.md) 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b3d2c-334">After your deployment is set up and running, [learn more](site-recovery-failover.md) about failover.</span></span>
