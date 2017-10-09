---
title: "aaaReplicate 實體伺服器 tooAzure |Microsoft 文件"
description: "描述如何 toodeploy Azure Site Recovery tooorchestrate 複寫、 容錯移轉和復原的內部部署 Windows/Linux 實體伺服器 tooAzure 使用 hello Azure 入口網站"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: physical-walkthrough-overview
ms.openlocfilehash: cf5928fb631f6858d57b27f6f21babc312714e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
---
# <a name="replicate-physical-machines-tooazure-by-using-site-recovery"></a><span data-ttu-id="15f2d-103">將實體機器 tooAzure 複寫使用站台復原</span><span class="sxs-lookup"><span data-stu-id="15f2d-103">Replicate physical machines tooAzure by using Site Recovery</span></span>


<span data-ttu-id="15f2d-104">本文說明如何 tooreplicate 內部部署實體機器 tooAzure hello Azure 入口網站中使用 hello Azure Site Recovery 服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-104">This article describes how tooreplicate on-premises physical machines tooAzure by using hello Azure Site Recovery service in hello Azure portal.</span></span>

<span data-ttu-id="15f2d-105">如果您想 toomigrate 實體機器 tooAzure （僅限容錯移轉），讀取[移轉與 Site Recovery tooAzure](site-recovery-migrate-to-azure.md) toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="15f2d-105">If you want toomigrate physical machines tooAzure (failover only), read [Migrate tooAzure with Site Recovery](site-recovery-migrate-to-azure.md) toolearn more.</span></span>

<span data-ttu-id="15f2d-106">在這份文件或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="15f2d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="15f2d-107">Prerequisites</span></span>

<span data-ttu-id="15f2d-108">**支援需求**</span><span class="sxs-lookup"><span data-stu-id="15f2d-108">**Support requirement**</span></span> | <span data-ttu-id="15f2d-109">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="15f2d-109">**Details**</span></span>
--- | ---
<span data-ttu-id="15f2d-110">**Azure**</span><span class="sxs-lookup"><span data-stu-id="15f2d-110">**Azure**</span></span> | <span data-ttu-id="15f2d-111">了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-111">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="15f2d-112">**內部部署組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="15f2d-112">**On-premises configuration server**</span></span> | <span data-ttu-id="15f2d-113">執行 Windows Server 2012 R2 或更新版本的內部部署機器 (實體或 VMware VM)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-113">On-premises machine (physical or VMware VM) running Windows Server 2012 R2 or later.</span></span> <span data-ttu-id="15f2d-114">在站台復原 」 部署期間設定 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-114">You set up hello configuration server during Site Recovery deployment.</span></span><br/><br/> <span data-ttu-id="15f2d-115">根據預設，hello 處理序伺服器與主要目標伺服器也安裝在這部電腦上。</span><span class="sxs-lookup"><span data-stu-id="15f2d-115">By default, hello process server and master target server are also installed on this machine.</span></span> <span data-ttu-id="15f2d-116">當您向上延展，您可能需要不同的處理序伺服器，並且具有 hello 與 hello 組態伺服器相同的需求。</span><span class="sxs-lookup"><span data-stu-id="15f2d-116">When you scale up, you might need a separate process server, and it has hello same requirements as hello configuration server.</span></span><br/><br/> <span data-ttu-id="15f2d-117">深入了解這些元件在[設定 hello 來源環境](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-117">Learn more about these components in [Set up hello source environment](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).</span></span>
<span data-ttu-id="15f2d-118">**內部部署 VM**</span><span class="sxs-lookup"><span data-stu-id="15f2d-118">**On-premises VMs**</span></span> | <span data-ttu-id="15f2d-119">您想應該執行 tooreplicate 機器[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)和符合[Azure 的必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-119">Machines you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="15f2d-120">**URL**</span><span class="sxs-lookup"><span data-stu-id="15f2d-120">**URLs**</span></span> | <span data-ttu-id="15f2d-121">hello 組態伺服器需要存取 toothese Url:</span><span class="sxs-lookup"><span data-stu-id="15f2d-121">hello configuration server needs access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="15f2d-122">如果您有 IP 位址為基礎的防火牆規則，確保它們允許通訊 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="15f2d-122">If you have IP address-based firewall rules, ensure that they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="15f2d-123">允許 hello [Azure Datacenter IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 hello HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="15f2d-123">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="15f2d-124">允許的 IP 位址範圍 hello Azure 地區的訂用帳戶和西部 （用於存取控制和身分識別管理）。</span><span class="sxs-lookup"><span data-stu-id="15f2d-124">Allow IP address ranges for hello Azure region of your subscription and for West US (used for access control and identity management).</span></span><br/><br/> <span data-ttu-id="15f2d-125">允許 hello MySQL 下載此 URL: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi。</span><span class="sxs-lookup"><span data-stu-id="15f2d-125">Allow this URL for hello MySQL download: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.</span></span>
<span data-ttu-id="15f2d-126">**行動服務**</span><span class="sxs-lookup"><span data-stu-id="15f2d-126">**Mobility service**</span></span> | <span data-ttu-id="15f2d-127">這項服務安裝在每部電腦上您想 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="15f2d-127">This service is installed on each machine you want tooreplicate.</span></span>

## <a name="limitations"></a><span data-ttu-id="15f2d-128">限制</span><span class="sxs-lookup"><span data-stu-id="15f2d-128">Limitations</span></span>

<span data-ttu-id="15f2d-129">**限制**</span><span class="sxs-lookup"><span data-stu-id="15f2d-129">**Limitation**</span></span> | <span data-ttu-id="15f2d-130">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="15f2d-130">**Details**</span></span>
--- | ---
<span data-ttu-id="15f2d-131">**Azure**</span><span class="sxs-lookup"><span data-stu-id="15f2d-131">**Azure**</span></span> | <span data-ttu-id="15f2d-132">儲存體和網路的帳戶必須在 hello 與 hello 保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="15f2d-132">Storage and network accounts must be in hello same region as hello vault.</span></span><br/><br/> <span data-ttu-id="15f2d-133">如果您使用進階儲存體帳戶，您也需要標準儲存帳戶 toostore 複寫記錄檔。</span><span class="sxs-lookup"><span data-stu-id="15f2d-133">If you use a premium storage account, you also need a standard store account toostore replication logs.</span></span><br/><br/> <span data-ttu-id="15f2d-134">您無法複寫在中部和印度南部及印度 toopremium 帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f2d-134">You can't replicate toopremium accounts in Central and South India.</span></span>
<span data-ttu-id="15f2d-135">**內部部署組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="15f2d-135">**On-premises configuration server**</span></span> | <span data-ttu-id="15f2d-136">如果您在 VMware VM 上安裝 hello 組態伺服器，hello VM 配接器類型應該是 VMXNET3。</span><span class="sxs-lookup"><span data-stu-id="15f2d-136">If you install hello configuration server on a VMware VM, hello VM adapter type should be VMXNET3.</span></span> <span data-ttu-id="15f2d-137">如果不是，請[安裝此更新](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-137">If it isn't, [install this update](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).</span></span><br/><br/> <span data-ttu-id="15f2d-138">如果您使用 VMware VM，則應該在其上安裝 vSphere PowerCLI 6.0。</span><span class="sxs-lookup"><span data-stu-id="15f2d-138">If you're using a VMware VM, vSphere PowerCLI 6.0 should be installed on it.</span></span><br/><br> <span data-ttu-id="15f2d-139">hello 機器不應該是網域控制站。</span><span class="sxs-lookup"><span data-stu-id="15f2d-139">hello machine shouldn't be a domain controller.</span></span><br/><br/> <span data-ttu-id="15f2d-140">hello 電腦應該具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15f2d-140">hello machine should have a static IP address.</span></span><br/><br/> <span data-ttu-id="15f2d-141">hello 主機名稱必須是 15 個字元或更少，而且 hello 作業系統應該是英文。</span><span class="sxs-lookup"><span data-stu-id="15f2d-141">hello host name should be 15 characters or less, and hello operating system should be in English.</span></span>
<span data-ttu-id="15f2d-142">**複寫的機器**</span><span class="sxs-lookup"><span data-stu-id="15f2d-142">**Replicated machines**</span></span> | <span data-ttu-id="15f2d-143">確認 [Azure VM 限制](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-143">Verify [Azure VM limitations](site-recovery-prereq.md#azure-requirements).</span></span><br/><br/> <span data-ttu-id="15f2d-144">如果您 tooenable 多重 VM 一致性，可讓執行相同工作負載 toobe 復原的 hello 機器一起 tooa 一致的資料點，請開啟連接埠 20004 hello 機器上。</span><span class="sxs-lookup"><span data-stu-id="15f2d-144">If you want tooenable multi-VM consistency, which enables machines running hello same workload toobe recovered together tooa consistent data point, open port 20004 on hello machine.</span></span><br/><br/> <span data-ttu-id="15f2d-145">支援特定類型的 [Linux 儲存體](site-recovery-support-matrix-to-azure.md#support-for-storage)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-145">Specific types of [Linux storage](site-recovery-support-matrix-to-azure.md#support-for-storage) are supported.</span></span>
<span data-ttu-id="15f2d-146">**容錯回復**</span><span class="sxs-lookup"><span data-stu-id="15f2d-146">**Failback**</span></span> | <span data-ttu-id="15f2d-147">您無法從 Azure tooa 實體機器失敗。</span><span class="sxs-lookup"><span data-stu-id="15f2d-147">You can't fail back from Azure tooa physical machine.</span></span> <span data-ttu-id="15f2d-148">如果您想 toobe 無法 toofail 後 tooon 內部部署容錯移轉之後，您需要的 VMware 環境，讓您可以容錯回復 tooa VMware VM。</span><span class="sxs-lookup"><span data-stu-id="15f2d-148">If you want toobe able toofail back tooon-premises after failover, you need a VMware environment so that you can fail back tooa VMware VM.</span></span>


## <a name="set-up-azure"></a><span data-ttu-id="15f2d-149">設定 Azure</span><span class="sxs-lookup"><span data-stu-id="15f2d-149">Set up Azure</span></span>

1. <span data-ttu-id="15f2d-150">[設定 Azure 網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-150">[Set up an Azure network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

      <span data-ttu-id="15f2d-151">a.</span><span class="sxs-lookup"><span data-stu-id="15f2d-151">a.</span></span> <span data-ttu-id="15f2d-152">在容錯移轉之後建立的 Azure VM 會置於這個網路。</span><span class="sxs-lookup"><span data-stu-id="15f2d-152">Azure VMs are placed in this network when they're created after failover.</span></span>

      <span data-ttu-id="15f2d-153">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="15f2d-153">b.</span></span> <span data-ttu-id="15f2d-154">您可以在 Azure [Resource Manager](../resource-manager-deployment-model.md) 或傳統模式中設定網路。</span><span class="sxs-lookup"><span data-stu-id="15f2d-154">You can set up a network in Azure [Resource Manager](../resource-manager-deployment-model.md) or in classic mode.</span></span>

2. <span data-ttu-id="15f2d-155">為複寫的資料設定 [Azure 儲存體帳戶](../storage/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-155">Set up an [Azure storage account](../storage/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>

    <span data-ttu-id="15f2d-156">a.</span><span class="sxs-lookup"><span data-stu-id="15f2d-156">a.</span></span> <span data-ttu-id="15f2d-157">hello 帳戶可以是標準或[premium](../storage/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-157">hello account can be standard or [premium](../storage/storage-premium-storage.md).</span></span>

    <span data-ttu-id="15f2d-158">b.</span><span class="sxs-lookup"><span data-stu-id="15f2d-158">b.</span></span> <span data-ttu-id="15f2d-159">您可以在 Resource Manager 或傳統模式中設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f2d-159">You can set up an account in Resource Manager or in classic mode.</span></span>

## <a name="prepare-hello-configuration-server"></a><span data-ttu-id="15f2d-160">準備 hello 組態伺服器</span><span class="sxs-lookup"><span data-stu-id="15f2d-160">Prepare hello configuration server</span></span>

1. <span data-ttu-id="15f2d-161">在內部部署實體伺服器或 VMware VM 上，安裝 Windows Server 2012 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="15f2d-161">Install Windows Server 2012 R2 or later on an on-premises physical server or a VMware VM.</span></span>

2. <span data-ttu-id="15f2d-162">請確定 hello 電腦具有存取 toohello Url 中所列[必要條件](#prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-162">Make sure hello machine has access toohello URLs listed in [Prerequisites](#prerequisites).</span></span>

## <a name="prepare-for-mobility-service-installation"></a><span data-ttu-id="15f2d-163">準備行動服務安裝</span><span class="sxs-lookup"><span data-stu-id="15f2d-163">Prepare for Mobility service installation</span></span>

<span data-ttu-id="15f2d-164">如果您想 toopush hello 行動服務 tooa 實體機器，您必須可供 hello 處理序伺服器 tooaccess hello 機器帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f2d-164">If you want toopush hello Mobility service tooa physical machine, you need an account that can be used by hello process server tooaccess hello machines.</span></span> <span data-ttu-id="15f2d-165">hello 帳戶只能用於 hello 推入安裝。</span><span class="sxs-lookup"><span data-stu-id="15f2d-165">hello account is used only for hello push installation.</span></span> <span data-ttu-id="15f2d-166">您可以使用網域或本機帳戶：</span><span class="sxs-lookup"><span data-stu-id="15f2d-166">You can use a domain or local account:</span></span>

  - <span data-ttu-id="15f2d-167">對於 Windows，如果您不使用網域帳戶，您需要 toodisable hello 本機電腦上的遠端使用者存取控制。</span><span class="sxs-lookup"><span data-stu-id="15f2d-167">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="15f2d-168">toodo hello 下的登錄中的這**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**，新增 hello DWORD 項目**LocalAccountTokenFilterPolicy**，值為 1。</span><span class="sxs-lookup"><span data-stu-id="15f2d-168">toodo this, in hello registry under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span> <span data-ttu-id="15f2d-169">如果您想用於 Windows 的 tooadd hello 登錄項目從命令列介面上，輸入：</span><span class="sxs-lookup"><span data-stu-id="15f2d-169">If you want tooadd hello registry entry for Windows from a command-line interface, type:</span></span>

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - <span data-ttu-id="15f2d-170">適用於 Linux，hello 帳戶應該是 hello 來源 Linux 伺服器上的根使用者。</span><span class="sxs-lookup"><span data-stu-id="15f2d-170">For Linux, hello account should be a root user on hello source Linux server.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="15f2d-171">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="15f2d-171">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-hello-protection-goal"></a><span data-ttu-id="15f2d-172">選取 hello 保護目標</span><span class="sxs-lookup"><span data-stu-id="15f2d-172">Select hello protection goal</span></span>

<span data-ttu-id="15f2d-173">選取您想要 tooreplicate 和您想要 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="15f2d-173">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="15f2d-174">按一下 [復原服務保存庫] > [保存庫]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-174">Click **Recovery Services vaults** > **vault**.</span></span>
2. <span data-ttu-id="15f2d-175">在 hello**資源**功能表上，按一下  **Site Recovery** > **準備基礎結構** > **保護目標**.</span><span class="sxs-lookup"><span data-stu-id="15f2d-175">On hello **Resource** menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. <span data-ttu-id="15f2d-177">在**保護目標**，選取**tooAzure** > **未虛擬化 / 其他**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-177">In **Protection goal**, select **tooAzure** > **Not virtualized / Other**.</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="15f2d-178">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="15f2d-178">Set up hello source environment</span></span>

<span data-ttu-id="15f2d-179">設定 hello 組態伺服器、 其註冊 hello 保存庫，以及探索 Vm。</span><span class="sxs-lookup"><span data-stu-id="15f2d-179">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="15f2d-180">按一下 [Site Recovery] > [準備基礎結構] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-180">Click **Site Recovery** > **Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="15f2d-181">如果您沒有設定伺服器，請按一下 [+設定伺服器]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-181">If you don’t have a configuration server, click **+Configuration Server**.</span></span>

    ![設定來源](./media/site-recovery-vmware-to-azure/set-source1.png)

3. <span data-ttu-id="15f2d-183">在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。</span><span class="sxs-lookup"><span data-stu-id="15f2d-183">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="15f2d-184">下載 hello **Site Recovery 整合安裝程式**安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="15f2d-184">Download hello **Site Recovery Unified Setup** installation file.</span></span>
5. <span data-ttu-id="15f2d-185">下載 hello**保存庫註冊金鑰**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-185">Download hello **vault registration key**.</span></span> <span data-ttu-id="15f2d-186">您會在執行統一安裝時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="15f2d-186">You need this key when you run Unified Setup.</span></span> <span data-ttu-id="15f2d-187">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="15f2d-187">hello key is valid for five days after you generate it.</span></span>

   ![設定來源](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a><span data-ttu-id="15f2d-189">執行 Site Recovery 統一安裝</span><span class="sxs-lookup"><span data-stu-id="15f2d-189">Run Site Recovery Unified Setup</span></span>

<span data-ttu-id="15f2d-190">開始之前，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="15f2d-190">Before you start, do hello following:</span></span>

- <span data-ttu-id="15f2d-191">透過影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="15f2d-191">Get a quick video overview.</span></span> <span data-ttu-id="15f2d-192">(hello 視訊描述 tooreplicate VMware Vm，但 hello 如何處理實體機器複寫的類似。)</span><span class="sxs-lookup"><span data-stu-id="15f2d-192">(hello video describes how tooreplicate VMware VMs, but hello process is similar for physical machine replication.)</span></span>

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- <span data-ttu-id="15f2d-193">在 hello 組態伺服器的電腦，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-193">On hello configuration server machine, make sure that hello system clock is synchronized with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="15f2d-194">如果快慢誤差 15 分鐘，安裝就可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="15f2d-194">If it's 15 minutes in front or behind, Setup might fail.</span></span>
- <span data-ttu-id="15f2d-195">Hello 組態伺服器電腦上，本機系統管理員身分執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="15f2d-195">Run Setup as a local administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="15f2d-196">請確定 hello 機器上已啟用 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="15f2d-196">Make sure TLS 1.0 is enabled on hello machine.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="15f2d-197">也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-197">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="15f2d-198">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="15f2d-198">Set up hello target environment</span></span>

<span data-ttu-id="15f2d-199">設定 hello 目標環境之前，請確定您有 toomake [Azure 儲存體帳戶和網路](#set-up-azure)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-199">Before you set up hello target environment, check toomake sure that you have an [Azure storage account and network](#set-up-azure).</span></span>

1. <span data-ttu-id="15f2d-200">按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f2d-200">Click **Prepare Infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="15f2d-201">指定目標部署模型為 Resource Manager 還是傳統的。</span><span class="sxs-lookup"><span data-stu-id="15f2d-201">Specify whether your target deployment model is Resource Manager or classic.</span></span>
3. <span data-ttu-id="15f2d-202">Site Recovery 會檢查 toomake 確定您有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="15f2d-202">Site Recovery checks toomake sure that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![目標](./media/site-recovery-vmware-to-azure/gs-target.png)

4. <span data-ttu-id="15f2d-204">如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**toocreate 資源管理員帳戶或網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="15f2d-204">If you haven't created a storage account or network, click **+Storage account** or **+Network** toocreate a Resource Manager account or network inline.</span></span>

## <a name="set-up-replication-settings"></a><span data-ttu-id="15f2d-205">設定複寫設定</span><span class="sxs-lookup"><span data-stu-id="15f2d-205">Set up replication settings</span></span>

<span data-ttu-id="15f2d-206">在開始之前，請透過影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="15f2d-206">Before you start, get a quick video overview.</span></span> <span data-ttu-id="15f2d-207">(hello 視訊描述 tooreplicate VMware Vm，但 hello 如何處理實體機器複寫的類似。)</span><span class="sxs-lookup"><span data-stu-id="15f2d-207">(hello video describes how tooreplicate VMware VMs, but hello process is similar for physical machine replication.)</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="15f2d-208">toocreate 新的複寫原則，請按一下**Site Recovery 基礎結構** > **複寫原則** > **+ 複寫原則**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-208">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="15f2d-209">在 [建立複寫原則]中，指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="15f2d-209">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="15f2d-210">在**RPO 臨界值**，指定 hello RPO 上限。</span><span class="sxs-lookup"><span data-stu-id="15f2d-210">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="15f2d-211">這個值指定資料復原點的建立頻率。</span><span class="sxs-lookup"><span data-stu-id="15f2d-211">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="15f2d-212">連續複寫超過此限制時會產生警示。</span><span class="sxs-lookup"><span data-stu-id="15f2d-212">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="15f2d-213">在**復原點保留**，指定時間長度 （以小時為單位） hello 保留週期是每個復原點。</span><span class="sxs-lookup"><span data-stu-id="15f2d-213">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="15f2d-214">複寫的 Vm 就能復原 tooany 點視窗中的。</span><span class="sxs-lookup"><span data-stu-id="15f2d-214">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="15f2d-215">向上 too24 機器複寫的 toopremium 存放裝置支援小時的保留。</span><span class="sxs-lookup"><span data-stu-id="15f2d-215">Up too24 hours' retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="15f2d-216">向上 too72 機器複寫的 toostandard 存放裝置支援小時的保留。</span><span class="sxs-lookup"><span data-stu-id="15f2d-216">Up too72 hours' retention is supported for machines replicated toostandard storage.</span></span>
5. <span data-ttu-id="15f2d-217">在 [應用程式一致快照集頻率] 中，指定建立包含應用程式一致快照集之復原點的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-217">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots are created.</span></span> <span data-ttu-id="15f2d-218">按一下**確定**toocreate hello 原則。</span><span class="sxs-lookup"><span data-stu-id="15f2d-218">Click **OK** toocreate hello policy.</span></span>

    ![複寫原則](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. <span data-ttu-id="15f2d-220">當您建立新的原則時，它會自動與相關聯 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-220">When you create a new policy, it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="15f2d-221">依預設會自動建立容錯回復的比對原則。</span><span class="sxs-lookup"><span data-stu-id="15f2d-221">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="15f2d-222">例如，如果 hello 複寫原則是**rep 原則**，那麼 hello 容錯回復原則是**容錯原則 rep 回復**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-222">For example, if hello replication policy is **rep-policy**, then hello failback policy is **rep-policy-failback**.</span></span> <span data-ttu-id="15f2d-223">從 Azure 起始容錯回復時才會使用此原則。</span><span class="sxs-lookup"><span data-stu-id="15f2d-223">This policy isn't used until you initiate a failback from Azure.</span></span>  


## <a name="plan-capacity"></a><span data-ttu-id="15f2d-224">規劃容量</span><span class="sxs-lookup"><span data-stu-id="15f2d-224">Plan capacity</span></span>

1. <span data-ttu-id="15f2d-225">現在您已設定基本基礎結構，可以思考容量規劃，並找出您是否需要額外的資源。</span><span class="sxs-lookup"><span data-stu-id="15f2d-225">Now that you have your basic infrastructure set up, you can think about capacity planning and figure out whether you need additional resources.</span></span> <span data-ttu-id="15f2d-226">[深入了解](site-recovery-plan-capacity-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-226">[Learn more](site-recovery-plan-capacity-vmware.md).</span></span>
2. <span data-ttu-id="15f2d-227">當您完成容量規劃時，請在 [已完成容量計劃了嗎?] 中選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-227">When you’re done with capacity planning, select **Yes** in **Have you completed capacity planning?**</span></span>

   ![容量規劃](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a><span data-ttu-id="15f2d-229">準備 VM 進行複寫</span><span class="sxs-lookup"><span data-stu-id="15f2d-229">Prepare VMs for replication</span></span>

<span data-ttu-id="15f2d-230">您要讓 tooreplicate 必須已安裝的 hello 行動服務的所有機器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-230">All machines that you want tooreplicate must have hello Mobility service installed.</span></span> <span data-ttu-id="15f2d-231">您可以在數種方式安裝 hello 行動服務：</span><span class="sxs-lookup"><span data-stu-id="15f2d-231">You can install hello Mobility service in a number of ways:</span></span>

- <span data-ttu-id="15f2d-232">以從 hello 處理序伺服器推入安裝來安裝 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-232">Install hello service with a push installation from hello process server.</span></span> <span data-ttu-id="15f2d-233">這個方法需要進階 toouse tooprepare 機器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-233">You need tooprepare machines in advance toouse this method.</span></span>
- <span data-ttu-id="15f2d-234">使用 System Center Configuration Manager 或 Azure 自動化 Desired State Configuration 之類的部署工具安裝 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-234">Install hello service by using deployment tools such as System Center Configuration Manager or Azure Automation Desired State Configuration.</span></span>
- <span data-ttu-id="15f2d-235">手動安裝 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-235">Install hello service manually.</span></span>

<span data-ttu-id="15f2d-236">[深入了解](site-recovery-vmware-to-azure-install-mob-svc.md)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-236">[Learn more](site-recovery-vmware-to-azure-install-mob-svc.md).</span></span>


## <a name="enable-replication"></a><span data-ttu-id="15f2d-237">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="15f2d-237">Enable replication</span></span>

<span data-ttu-id="15f2d-238">開始之前：</span><span class="sxs-lookup"><span data-stu-id="15f2d-238">Before you start:</span></span>

- <span data-ttu-id="15f2d-239">您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。</span><span class="sxs-lookup"><span data-stu-id="15f2d-239">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>
- <span data-ttu-id="15f2d-240">當您加入或修改 Vm 時，可能需要向上 too15 分鐘或更久變更 tootake 效果，並為其 tooappear hello 入口網站中的。</span><span class="sxs-lookup"><span data-stu-id="15f2d-240">When you add or modify VMs, it can take up too15 minutes or longer for changes tootake effect and for them tooappear in hello portal.</span></span>
- <span data-ttu-id="15f2d-241">您可以檢查 hello 上次探索的時間中的 Vm**設定伺服器** > **上次連絡時間**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-241">You can check hello last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="15f2d-242">不需等到 hello 已排程的探索，反白顯示 hello 組態伺服器 tooadd Vm （但不要按），然後按一下**重新整理**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-242">tooadd VMs without waiting for hello scheduled discovery, highlight hello configuration server (don’t click it), and click **Refresh**.</span></span>
- <span data-ttu-id="15f2d-243">如果 VM 備妥推入安裝，hello 處理序伺服器在啟用複寫時自動安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-243">If a VM is prepared for push installation, hello process server automatically installs hello Mobility service when you enable replication.</span></span>
- <span data-ttu-id="15f2d-244">透過影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="15f2d-244">Get a quick video overview.</span></span> <span data-ttu-id="15f2d-245">(hello 視訊描述 tooreplicate VMware Vm，但 hello 如何處理實體機器複寫的類似。)</span><span class="sxs-lookup"><span data-stu-id="15f2d-245">(hello video describes how tooreplicate VMware VMs, but hello process is similar for physical machine replication.)</span></span>

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a><span data-ttu-id="15f2d-246">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="15f2d-246">Exclude disks from replication</span></span>

<span data-ttu-id="15f2d-247">依預設會複寫機器上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="15f2d-247">By default, all disks on a machine are replicated.</span></span> <span data-ttu-id="15f2d-248">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="15f2d-248">You can exclude disks from replication.</span></span> <span data-ttu-id="15f2d-249">比方說，您可能不想使用暫存資料 tooreplicate 磁碟或資料重新整理每一次電腦或應用程式重新啟動 （例如，pagefile.sys 或 SQL Server tempdb）。</span><span class="sxs-lookup"><span data-stu-id="15f2d-249">For example, you might not want tooreplicate disks with temporary data or data that's refreshed each time a machine or application restarts (for example, pagefile.sys or SQL Server tempdb).</span></span>

### <a name="replicate-vms"></a><span data-ttu-id="15f2d-250">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="15f2d-250">Replicate VMs</span></span>

1. <span data-ttu-id="15f2d-251">按一下 [複寫應用程式] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-251">Click **Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="15f2d-252">在 [來源] 中，選取 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-252">In **Source**, select **On-premises**.</span></span>
3. <span data-ttu-id="15f2d-253">在**來源位置**，選取 hello 組態伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="15f2d-253">In **Source location**, select hello configuration server name.</span></span>
4. <span data-ttu-id="15f2d-254">在 [機器類型] 中，選取 [實體機器]。</span><span class="sxs-lookup"><span data-stu-id="15f2d-254">In **Machine type**, select **Physical Machines**.</span></span>
5. <span data-ttu-id="15f2d-255">在**處理序伺服器**，選擇 hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-255">In **Process server**, choose hello process server.</span></span> <span data-ttu-id="15f2d-256">如果您尚未建立任何額外的處理序伺服器，此伺服器是 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-256">If you haven't created any additional process servers, this server is hello configuration server.</span></span> <span data-ttu-id="15f2d-257">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="15f2d-257">Then click **OK**.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/chooseVM.png)

6. <span data-ttu-id="15f2d-259">在**目標**，選取 hello**訂用帳戶**和 hello**資源群組**您想 toocreate hello Azure Vm 容錯移轉之後。</span><span class="sxs-lookup"><span data-stu-id="15f2d-259">In **Target**, select hello **Subscription** and hello **Resource group** in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="15f2d-260">選擇 hello 部署模型，您想要在 Azure 中的 toouse (傳統或資源管理員) 的 hello 容錯移轉 Vm。</span><span class="sxs-lookup"><span data-stu-id="15f2d-260">Choose hello deployment model that you want toouse in Azure (classic or Resource Manager) for hello failed-over VMs.</span></span>

7. <span data-ttu-id="15f2d-261">選取要用於複寫資料 toouse hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f2d-261">Select hello Azure storage account you want toouse for replicating data.</span></span> <span data-ttu-id="15f2d-262">如果您不想 toouse 您已經設定的帳戶，您可以建立一個新。</span><span class="sxs-lookup"><span data-stu-id="15f2d-262">If you don't want toouse an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="15f2d-263">選取 hello **Azure 網路**和**子網路**toowhich Azure Vm 容錯移轉之後連接。</span><span class="sxs-lookup"><span data-stu-id="15f2d-263">Select hello **Azure network** and **Subnet** toowhich Azure VMs connect after failover.</span></span> <span data-ttu-id="15f2d-264">選取**現在選取的機器設定**tooapply hello 網路設定 tooall 您選取的機器進行保護。</span><span class="sxs-lookup"><span data-stu-id="15f2d-264">Select **Configure now for selected machines** tooapply hello network setting tooall machines you select for protection.</span></span> <span data-ttu-id="15f2d-265">選取**稍後設定**tooselect hello 每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="15f2d-265">Select **Configure later** tooselect hello Azure network per machine.</span></span> <span data-ttu-id="15f2d-266">如果您不想 toouse 現有網路，您可以建立一個。</span><span class="sxs-lookup"><span data-stu-id="15f2d-266">If you don't want toouse an existing network, you can create one.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/targetsettings.png)

9. <span data-ttu-id="15f2d-268">在**實體機器**，按一下  **+ 實體機器**，然後輸入 hello**名稱**和**IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-268">In **Physical machines**, click **+Physical machine** and enter hello **Name** and **IP address**.</span></span> <span data-ttu-id="15f2d-269">選擇 hello 作業系統要 tooreplicate 的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-269">Choose hello operating system of hello machine you want tooreplicate.</span></span> <span data-ttu-id="15f2d-270">花幾分鐘的時間之前的電腦系統會探索並 hello 清單所示。</span><span class="sxs-lookup"><span data-stu-id="15f2d-270">It takes a few minutes until machines are discovered and shown in hello list.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/machineselect.png)

10. <span data-ttu-id="15f2d-272">在**屬性** > **設定屬性**，選取 hello toobe 供 hello 處理序伺服器 tooautomatically hello 機器上安裝 hello 行動服務的帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f2d-272">In **Properties** > **Configure properties**, select hello account toobe used by hello process server tooautomatically install hello Mobility service on hello machine.</span></span>
11. <span data-ttu-id="15f2d-273">依預設會複寫所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="15f2d-273">By default, all disks are replicated.</span></span> <span data-ttu-id="15f2d-274">按一下**所有磁碟**，並清除您不想 tooreplicate 任何磁碟。</span><span class="sxs-lookup"><span data-stu-id="15f2d-274">Click **All Disks**, and clear any disks you don't want tooreplicate.</span></span> <span data-ttu-id="15f2d-275">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="15f2d-275">Then click **OK**.</span></span> <span data-ttu-id="15f2d-276">您可以稍後再設定其他 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="15f2d-276">You can set additional VM properties later.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/configprop.png)

12. <span data-ttu-id="15f2d-278">在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。</span><span class="sxs-lookup"><span data-stu-id="15f2d-278">In **Replication settings** > **Configure replication settings**, verify that hello correct replication policy is selected.</span></span> <span data-ttu-id="15f2d-279">如果您修改原則時，變更將會套用的 toohello 機器和 toonew 機器複寫。</span><span class="sxs-lookup"><span data-stu-id="15f2d-279">If you modify a policy, changes are applied toohello replicating machine and toonew machines.</span></span>
13. <span data-ttu-id="15f2d-280">啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="15f2d-280">Enable **Multi-VM consistency** if you want toogather machines into a replication group, and specify a name for hello group.</span></span> <span data-ttu-id="15f2d-281">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="15f2d-281">Then click **OK**.</span></span> <span data-ttu-id="15f2d-282">請注意：</span><span class="sxs-lookup"><span data-stu-id="15f2d-282">Note that:</span></span>

    <span data-ttu-id="15f2d-283">a.</span><span class="sxs-lookup"><span data-stu-id="15f2d-283">a.</span></span> <span data-ttu-id="15f2d-284">複寫群組中的電腦會一起複寫，且在容錯移轉時，會有共用的損毀一致和應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="15f2d-284">Machines in replication groups replicate together and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>

    <span data-ttu-id="15f2d-285">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="15f2d-285">b.</span></span> <span data-ttu-id="15f2d-286">我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="15f2d-286">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="15f2d-287">啟用多 VM 一致性可能會影響工作負載的效能。</span><span class="sxs-lookup"><span data-stu-id="15f2d-287">Enabling multi-VM consistency can affect workload performance.</span></span> <span data-ttu-id="15f2d-288">如果電腦執行 hello 相同的工作負載，且您需要一致性應該使用它。</span><span class="sxs-lookup"><span data-stu-id="15f2d-288">It should be used only if machines are running hello same workload and you need consistency.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/policy.png)

14. <span data-ttu-id="15f2d-290">按一下 [啟用複寫] 。</span><span class="sxs-lookup"><span data-stu-id="15f2d-290">Click **Enable Replication**.</span></span> <span data-ttu-id="15f2d-291">您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.</span><span class="sxs-lookup"><span data-stu-id="15f2d-291">You can track progress of hello **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="15f2d-292">之後 hello**完成保護**作業會執行，hello 機器是否已做好容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="15f2d-292">After hello **Finalize Protection** job runs, hello machine is ready for failover.</span></span>

<span data-ttu-id="15f2d-293">啟用複寫後，如果您設定推入安裝安裝 hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-293">After you enable replication, hello Mobility service is installed if you set up push installation.</span></span> <span data-ttu-id="15f2d-294">Hello 行動服務推入安裝在電腦上後，保護工作會啟動，並會失敗。</span><span class="sxs-lookup"><span data-stu-id="15f2d-294">After hello Mobility service is push installed on a machine, a protection job starts and fails.</span></span> <span data-ttu-id="15f2d-295">Hello 失敗之後，您需要 toomanually 重新啟動每一部機器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-295">After hello failure, you need toomanually restart each machine.</span></span> <span data-ttu-id="15f2d-296">Hello 保護作業，然後再次，開始，就會發生初始複寫。</span><span class="sxs-lookup"><span data-stu-id="15f2d-296">Then hello protection job begins again, and initial replication occurs.</span></span>


### <a name="view-and-manage-azure-vm-properties"></a><span data-ttu-id="15f2d-297">檢視及管理 Azure VM 屬性</span><span class="sxs-lookup"><span data-stu-id="15f2d-297">View and manage Azure VM properties</span></span>

<span data-ttu-id="15f2d-298">我們建議您確認 hello VM 屬性，然後進行您需要的任何變更。</span><span class="sxs-lookup"><span data-stu-id="15f2d-298">We recommend that you verify hello VM properties and make any changes you need.</span></span>

1. <span data-ttu-id="15f2d-299">按一下**複寫項目**，並選取 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-299">Click **Replicated items**, and select hello machine.</span></span> <span data-ttu-id="15f2d-300">hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。</span><span class="sxs-lookup"><span data-stu-id="15f2d-300">hello **Essentials** blade shows information about machines settings and status.</span></span>
2. <span data-ttu-id="15f2d-301">在**屬性**，您可以檢視複寫和容錯移轉資訊 hello VM。</span><span class="sxs-lookup"><span data-stu-id="15f2d-301">In **Properties**, you can view replication and failover information for hello VM.</span></span>
3. <span data-ttu-id="15f2d-302">在**計算與網路** > **計算屬性**，您可以指定 hello Azure VM 的名稱和目標大小。</span><span class="sxs-lookup"><span data-stu-id="15f2d-302">In **Compute and Network** > **Compute properties**, you can specify hello Azure VM name and target size.</span></span> <span data-ttu-id="15f2d-303">修改與 hello 名稱 toocomply [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)如果您需要。</span><span class="sxs-lookup"><span data-stu-id="15f2d-303">Modify hello name toocomply with [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) if you need to.</span></span>
4. <span data-ttu-id="15f2d-304">修改設定 hello 目標網路、 子網路和 IP 位址指派 toohello Azure VM:</span><span class="sxs-lookup"><span data-stu-id="15f2d-304">Modify settings for hello target network, subnet, and IP address that are assigned toohello Azure VM:</span></span>

    <span data-ttu-id="15f2d-305">a.</span><span class="sxs-lookup"><span data-stu-id="15f2d-305">a.</span></span> <span data-ttu-id="15f2d-306">您可以設定 hello 目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="15f2d-306">You can set hello target IP address.</span></span>

    <span data-ttu-id="15f2d-307">b.</span><span class="sxs-lookup"><span data-stu-id="15f2d-307">b.</span></span>  <span data-ttu-id="15f2d-308">如果您沒有提供的地址，hello 容錯機器會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="15f2d-308">If you don't provide an address, hello failed-over machine uses DHCP.</span></span>

    <span data-ttu-id="15f2d-309">c.</span><span class="sxs-lookup"><span data-stu-id="15f2d-309">c.</span></span> <span data-ttu-id="15f2d-310">如果您設定的位址在容錯移轉時無法使用，容錯移轉就無法運作。</span><span class="sxs-lookup"><span data-stu-id="15f2d-310">If you set an address that isn't available at failover, failover doesn't work.</span></span>

    <span data-ttu-id="15f2d-311">d.</span><span class="sxs-lookup"><span data-stu-id="15f2d-311">d.</span></span> <span data-ttu-id="15f2d-312">相同的目標 IP 位址可用於測試容錯移轉 hello 位址是否可用 hello 測試容錯移轉網路中的 hello。</span><span class="sxs-lookup"><span data-stu-id="15f2d-312">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

    <span data-ttu-id="15f2d-313">e.</span><span class="sxs-lookup"><span data-stu-id="15f2d-313">e.</span></span> <span data-ttu-id="15f2d-314">網路介面卡的 hello 數目取決於您指定 hello 目標虛擬機器的 hello 大小：</span><span class="sxs-lookup"><span data-stu-id="15f2d-314">hello number of network adapters is dictated by hello size you specify for hello target virtual machine:</span></span>

     - <span data-ttu-id="15f2d-315">如果 hello hello 來源電腦上的網路介面卡的數目相同，或允許 hello 目標機器的大小，介面卡的 hello 數目大於或等於 hello 則 hello 目標有 hello 做 hello 來源的相同數目的介面卡。</span><span class="sxs-lookup"><span data-stu-id="15f2d-315">If hello number of network adapters on hello source machine is hello same as, or less than, hello number of adapters allowed for hello target machine size, then hello target has hello same number of adapters as hello source.</span></span>
     - <span data-ttu-id="15f2d-316">如果 hello hello 來源虛擬機器介面卡的數目超過 hello 目標大小，允許 hello 數目，則使用 hello 目標大小最大值。</span><span class="sxs-lookup"><span data-stu-id="15f2d-316">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size, then hello target size maximum is used.</span></span>
     - <span data-ttu-id="15f2d-317">例如，如果來源機器有兩個網路介面卡，hello 目標機器大小支援四個 hello 目標電腦有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="15f2d-317">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine has two adapters.</span></span> <span data-ttu-id="15f2d-318">如果 hello 來源機器有兩張介面卡，但支援 hello 目標大小僅支援一個，hello 目標電腦有只有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="15f2d-318">If hello source machine has two adapters but hello supported target size supports only one, then hello target machine has only one adapter.</span></span>     
   - <span data-ttu-id="15f2d-319">如果 hello 虛擬機器有多張網路介面卡，它們全部連接 toohello 相同的網路。</span><span class="sxs-lookup"><span data-stu-id="15f2d-319">If hello virtual machine has multiple network adapters, they all connect toohello same network.</span></span>
   - <span data-ttu-id="15f2d-320">如果 hello 虛擬機器有多張網路介面卡，則 hello hello 清單中所顯示的最早 hello*預設*hello Azure VM 中的網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="15f2d-320">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello *Default* network adapter in hello Azure VM.</span></span>
5. <span data-ttu-id="15f2d-321">在**磁碟**，您可以看到 hello VM 作業系統以及 hello 複寫的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="15f2d-321">In **Disks**, you can see hello VM operating system and hello data disks that are replicated.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="15f2d-322">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="15f2d-322">Run a test failover</span></span>

<span data-ttu-id="15f2d-323">您已設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="15f2d-323">After you've set up everything, run a test failover toomake sure everything's working as expected.</span></span> <span data-ttu-id="15f2d-324">開始之前，請觀看影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="15f2d-324">Watch a quick video overview before you start.</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. <span data-ttu-id="15f2d-325">透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 **測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-325">toofail over a single machine, in **Settings** > **Replicated Items**, click **Test failover**.</span></span>

    ![測試容錯移轉](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. <span data-ttu-id="15f2d-327">toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃 >**測試容錯移轉**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-327">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan > **Test Failover**.</span></span> <span data-ttu-id="15f2d-328">復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-328">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  
3. <span data-ttu-id="15f2d-329">在**測試容錯移轉**，選取 hello Azure 網路 toowhich Azure Vm 容錯移轉發生後的連線。</span><span class="sxs-lookup"><span data-stu-id="15f2d-329">In **Test Failover**, select hello Azure network toowhich Azure VMs are connected after failover occurs.</span></span>
4. <span data-ttu-id="15f2d-330">按一下**確定**toobegin hello 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="15f2d-330">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="15f2d-331">您可以追蹤進度，方法是按一下 hello VM tooopen 其屬性，或按一下 hello**測試容錯移轉**作業在保存庫名稱 >**設定** > **作業** > **站台復原工作**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-331">You can track progress by clicking hello VM tooopen its properties or by clicking hello **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="15f2d-332">Hello 容錯移轉完成之後，您也應該可以 toosee hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="15f2d-332">After hello failover finishes, you should also be able toosee hello replica Azure machine appear in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="15f2d-333">請確定該 hello VM hello 適當的大小，它已連接 toohello 適當的網路，而且它正在執行。</span><span class="sxs-lookup"><span data-stu-id="15f2d-333">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="15f2d-334">如果您[做好容錯移轉之後的連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)，您應該能夠 tooconnect toohello Azure VM。</span><span class="sxs-lookup"><span data-stu-id="15f2d-334">If you [prepared for connections after failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), you should be able tooconnect toohello Azure VM.</span></span>
7. <span data-ttu-id="15f2d-335">瀏覽完畢之後，請按一下**清除測試容錯移轉**hello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="15f2d-335">After you're done, click **Cleanup test failover** on hello recovery plan.</span></span> <span data-ttu-id="15f2d-336">在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="15f2d-336">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="15f2d-337">此步驟會刪除 hello 測試容錯移轉期間所建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="15f2d-337">This step deletes hello virtual machines that were created during test failover.</span></span>

<span data-ttu-id="15f2d-338">如需詳細資訊，請參閱 hello[測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)文件。</span><span class="sxs-lookup"><span data-stu-id="15f2d-338">For more information, see hello [Test failover tooAzure](site-recovery-test-failover-to-azure.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15f2d-339">後續步驟</span><span class="sxs-lookup"><span data-stu-id="15f2d-339">Next steps</span></span>

<span data-ttu-id="15f2d-340">之後看到 複寫和執行、 發生中斷時，您容錯移轉 tooAzure，和從 hello 複寫資料建立 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="15f2d-340">After you get replication up and running, when an outage occurs you fail over tooAzure, and Azure VMs are created from hello replicated data.</span></span> <span data-ttu-id="15f2d-341">然後您可以存取工作負載和應用程式在 Azure 中，直到它傳回 toonormal 作業時，無法回復 tooyour 主要位置。</span><span class="sxs-lookup"><span data-stu-id="15f2d-341">You can then access workloads and apps in Azure, until you fail back tooyour primary location when it returns toonormal operations.</span></span>

- <span data-ttu-id="15f2d-342">[進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。</span><span class="sxs-lookup"><span data-stu-id="15f2d-342">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="15f2d-343">如果您要移轉電腦而不是複寫和容錯回復，請[深入了解](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-343">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="15f2d-344">當複寫實體機器，您可以只容錯回復 tooa VMware 環境。</span><span class="sxs-lookup"><span data-stu-id="15f2d-344">When replicating physical machines, you can only failback tooa VMware environment.</span></span> <span data-ttu-id="15f2d-345">[了解容錯回復](site-recovery-failback-azure-to-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-345">[Read about failback](site-recovery-failback-azure-to-vmware.md).</span></span>

## <a name="third-party-software-notices-and-information"></a><span data-ttu-id="15f2d-346">第三方廠商軟體注意事項和資訊</span><span class="sxs-lookup"><span data-stu-id="15f2d-346">Third-party software notices and information</span></span>
<span data-ttu-id="15f2d-347">Do Not Translate or Localize</span><span class="sxs-lookup"><span data-stu-id="15f2d-347">Do Not Translate or Localize</span></span>

<span data-ttu-id="15f2d-348">hello 軟體和韌體中執行 hello Microsoft 產品或服務為基礎，或納入 hello 從資料列下方 （以下合稱 「 第三方程式碼 」） 的專案。</span><span class="sxs-lookup"><span data-stu-id="15f2d-348">hello software and firmware running in hello Microsoft product or service is based on or incorporates material from hello projects listed below (collectively, “Third-Party Code”).</span></span> <span data-ttu-id="15f2d-349">Microsoft 不 hello 的 hello 協力廠商程式碼的原始作者。</span><span class="sxs-lookup"><span data-stu-id="15f2d-349">Microsoft is not hello original author of hello Third-Party Code.</span></span> <span data-ttu-id="15f2d-350">hello 原始著作權聲明與授權，在其下 Microsoft 接收這類協力廠商程式碼中，會設定制定下方。</span><span class="sxs-lookup"><span data-stu-id="15f2d-350">hello original copyright notice and license, under which Microsoft received such Third-Party Code, are set forth below.</span></span>

<span data-ttu-id="15f2d-351">區段 A 中的 hello 資訊關於從 hello 專案元件下面所列的第三方程式碼。</span><span class="sxs-lookup"><span data-stu-id="15f2d-351">hello information in Section A is regarding Third-Party Code components from hello projects listed below.</span></span> <span data-ttu-id="15f2d-352">Such licenses and information are provided for informational purposes only.</span><span class="sxs-lookup"><span data-stu-id="15f2d-352">Such licenses and information are provided for informational purposes only.</span></span> <span data-ttu-id="15f2d-353">此協力廠商程式碼正在 relicensed 的 tooyou microsoft 在 Microsoft 軟體授權條款的 hello Microsoft 產品或服務。</span><span class="sxs-lookup"><span data-stu-id="15f2d-353">This Third-Party Code is being relicensed tooyou by Microsoft under Microsoft's software licensing terms for hello Microsoft product or service.</span></span>  

<span data-ttu-id="15f2d-354">節 B 中的 hello 資訊有關第三方廠商程式碼元件所進行可用 tooyou microsoft hello 原始授權條款。</span><span class="sxs-lookup"><span data-stu-id="15f2d-354">hello information in Section B is regarding Third Party Code components that are being made available tooyou by Microsoft under hello original licensing terms.</span></span>

<span data-ttu-id="15f2d-355">hello 完整的檔案可以位於 hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428)。</span><span class="sxs-lookup"><span data-stu-id="15f2d-355">hello complete file can be found on hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428).</span></span> <span data-ttu-id="15f2d-356">Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.</span><span class="sxs-lookup"><span data-stu-id="15f2d-356">Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.</span></span>
