---
title: "將實體伺服器複寫至 Azure | Microsoft Docs"
description: "說明如何使用 Azure 入口網站部署 Azure Site Recovery，以協調內部部署 Windows/Linux 實體伺服器至 Azure 的複寫、容錯移轉和復原"
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
ms.openlocfilehash: a9655ce1540c788d02d178eb619d2051cddda1c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
---
# <a name="replicate-physical-machines-to-azure-by-using-site-recovery"></a><span data-ttu-id="c93c8-103">使用 Site Recovery 將實體機器複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="c93c8-103">Replicate physical machines to Azure by using Site Recovery</span></span>


<span data-ttu-id="c93c8-104">本文說明如何在 Azure 入口網站中使用 Azure Site Recovery 服務，將內部部署實體機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="c93c8-104">This article describes how to replicate on-premises physical machines to Azure by using the Azure Site Recovery service in the Azure portal.</span></span>

<span data-ttu-id="c93c8-105">如果您要將實體機器移轉至 Azure (僅容錯移轉)，請參閱[使用 Site Recovery 移轉至 Azure](site-recovery-migrate-to-azure.md)以深入了解。</span><span class="sxs-lookup"><span data-stu-id="c93c8-105">If you want to migrate physical machines to Azure (failover only), read [Migrate to Azure with Site Recovery](site-recovery-migrate-to-azure.md) to learn more.</span></span>

<span data-ttu-id="c93c8-106">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="c93c8-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c93c8-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="c93c8-107">Prerequisites</span></span>

<span data-ttu-id="c93c8-108">**支援需求**</span><span class="sxs-lookup"><span data-stu-id="c93c8-108">**Support requirement**</span></span> | <span data-ttu-id="c93c8-109">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="c93c8-109">**Details**</span></span>
--- | ---
<span data-ttu-id="c93c8-110">**Azure**</span><span class="sxs-lookup"><span data-stu-id="c93c8-110">**Azure**</span></span> | <span data-ttu-id="c93c8-111">了解 [Azure 需求](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-111">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="c93c8-112">**內部部署組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="c93c8-112">**On-premises configuration server**</span></span> | <span data-ttu-id="c93c8-113">執行 Windows Server 2012 R2 或更新版本的內部部署機器 (實體或 VMware VM)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-113">On-premises machine (physical or VMware VM) running Windows Server 2012 R2 or later.</span></span> <span data-ttu-id="c93c8-114">您在 Site Recovery 部署期間設定組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="c93c8-114">You set up the configuration server during Site Recovery deployment.</span></span><br/><br/> <span data-ttu-id="c93c8-115">根據預設，處理序伺服器與主要目標伺服器也會安裝在此電腦上。</span><span class="sxs-lookup"><span data-stu-id="c93c8-115">By default, the process server and master target server are also installed on this machine.</span></span> <span data-ttu-id="c93c8-116">當您相應增加時，可能需要不同的處理序伺服器，它的需求與組態伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="c93c8-116">When you scale up, you might need a separate process server, and it has the same requirements as the configuration server.</span></span><br/><br/> <span data-ttu-id="c93c8-117">在[設定來源環境](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements)中深入了解這些元件。</span><span class="sxs-lookup"><span data-stu-id="c93c8-117">Learn more about these components in [Set up the source environment](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).</span></span>
<span data-ttu-id="c93c8-118">**內部部署 VM**</span><span class="sxs-lookup"><span data-stu-id="c93c8-118">**On-premises VMs**</span></span> | <span data-ttu-id="c93c8-119">您想要複寫的電腦需執行[支援的作業系統](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)，並且要符合 [Azure 必要條件](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-119">Machines you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="c93c8-120">**URL**</span><span class="sxs-lookup"><span data-stu-id="c93c8-120">**URLs**</span></span> | <span data-ttu-id="c93c8-121">設定伺服器需要存取這些 URL：</span><span class="sxs-lookup"><span data-stu-id="c93c8-121">The configuration server needs access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="c93c8-122">如果您有以 IP 位址為基礎的防火牆規則，請確定這些規則允許對 Azure 的通訊。</span><span class="sxs-lookup"><span data-stu-id="c93c8-122">If you have IP address-based firewall rules, ensure that they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="c93c8-123">允許 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="c93c8-123">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="c93c8-124">允許訂用帳戶的 Azure 區域和美國西部使用 IP 位址範圍 (用於存取控制和身分識別管理)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-124">Allow IP address ranges for the Azure region of your subscription and for West US (used for access control and identity management).</span></span><br/><br/> <span data-ttu-id="c93c8-125">允許使用此 URL 下載 MySQL：http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi</span><span class="sxs-lookup"><span data-stu-id="c93c8-125">Allow this URL for the MySQL download: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.</span></span>
<span data-ttu-id="c93c8-126">**行動服務**</span><span class="sxs-lookup"><span data-stu-id="c93c8-126">**Mobility service**</span></span> | <span data-ttu-id="c93c8-127">此服務必須安裝於您要複寫的每部電腦上。</span><span class="sxs-lookup"><span data-stu-id="c93c8-127">This service is installed on each machine you want to replicate.</span></span>

## <a name="limitations"></a><span data-ttu-id="c93c8-128">限制</span><span class="sxs-lookup"><span data-stu-id="c93c8-128">Limitations</span></span>

<span data-ttu-id="c93c8-129">**限制**</span><span class="sxs-lookup"><span data-stu-id="c93c8-129">**Limitation**</span></span> | <span data-ttu-id="c93c8-130">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="c93c8-130">**Details**</span></span>
--- | ---
<span data-ttu-id="c93c8-131">**Azure**</span><span class="sxs-lookup"><span data-stu-id="c93c8-131">**Azure**</span></span> | <span data-ttu-id="c93c8-132">儲存體和網路帳戶必須位於與保存庫相同的區域。</span><span class="sxs-lookup"><span data-stu-id="c93c8-132">Storage and network accounts must be in the same region as the vault.</span></span><br/><br/> <span data-ttu-id="c93c8-133">如果您使用進階儲存體帳戶，則也需要有標準儲存體帳戶來儲存複寫記錄。</span><span class="sxs-lookup"><span data-stu-id="c93c8-133">If you use a premium storage account, you also need a standard store account to store replication logs.</span></span><br/><br/> <span data-ttu-id="c93c8-134">您無法複寫到印度中部和南部的進階帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-134">You can't replicate to premium accounts in Central and South India.</span></span>
<span data-ttu-id="c93c8-135">**內部部署組態伺服器**</span><span class="sxs-lookup"><span data-stu-id="c93c8-135">**On-premises configuration server**</span></span> | <span data-ttu-id="c93c8-136">如果您在 VMware VM 上安裝組態伺服器，VM 配接器類型應該是 VMXNET3。</span><span class="sxs-lookup"><span data-stu-id="c93c8-136">If you install the configuration server on a VMware VM, the VM adapter type should be VMXNET3.</span></span> <span data-ttu-id="c93c8-137">如果不是，請[安裝此更新](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-137">If it isn't, [install this update](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).</span></span><br/><br/> <span data-ttu-id="c93c8-138">如果您使用 VMware VM，則應該在其上安裝 vSphere PowerCLI 6.0。</span><span class="sxs-lookup"><span data-stu-id="c93c8-138">If you're using a VMware VM, vSphere PowerCLI 6.0 should be installed on it.</span></span><br/><br> <span data-ttu-id="c93c8-139">電腦不應該是網域控制站。</span><span class="sxs-lookup"><span data-stu-id="c93c8-139">The machine shouldn't be a domain controller.</span></span><br/><br/> <span data-ttu-id="c93c8-140">電腦應有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c93c8-140">The machine should have a static IP address.</span></span><br/><br/> <span data-ttu-id="c93c8-141">主機名稱應該是 15 個字元以下，而且作業系統應該是英文版。</span><span class="sxs-lookup"><span data-stu-id="c93c8-141">The host name should be 15 characters or less, and the operating system should be in English.</span></span>
<span data-ttu-id="c93c8-142">**複寫的機器**</span><span class="sxs-lookup"><span data-stu-id="c93c8-142">**Replicated machines**</span></span> | <span data-ttu-id="c93c8-143">確認 [Azure VM 限制](site-recovery-prereq.md#azure-requirements)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-143">Verify [Azure VM limitations](site-recovery-prereq.md#azure-requirements).</span></span><br/><br/> <span data-ttu-id="c93c8-144">如果您想要啟用多部 VM 一致性 (這可讓執行相同工作負載的機器一起復原到一致的資料點)，請開啟機器上的連接埠 20004。</span><span class="sxs-lookup"><span data-stu-id="c93c8-144">If you want to enable multi-VM consistency, which enables machines running the same workload to be recovered together to a consistent data point, open port 20004 on the machine.</span></span><br/><br/> <span data-ttu-id="c93c8-145">支援特定類型的 [Linux 儲存體](site-recovery-support-matrix-to-azure.md#support-for-storage)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-145">Specific types of [Linux storage](site-recovery-support-matrix-to-azure.md#support-for-storage) are supported.</span></span>
<span data-ttu-id="c93c8-146">**容錯回復**</span><span class="sxs-lookup"><span data-stu-id="c93c8-146">**Failback**</span></span> | <span data-ttu-id="c93c8-147">您無法從 Azure 容錯回復到實體機器。</span><span class="sxs-lookup"><span data-stu-id="c93c8-147">You can't fail back from Azure to a physical machine.</span></span> <span data-ttu-id="c93c8-148">如果您想要能夠在容錯移轉之後容錯回復到內部部署，則需要 VMware 環境，讓您可以容錯回復到 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="c93c8-148">If you want to be able to fail back to on-premises after failover, you need a VMware environment so that you can fail back to a VMware VM.</span></span>


## <a name="set-up-azure"></a><span data-ttu-id="c93c8-149">設定 Azure</span><span class="sxs-lookup"><span data-stu-id="c93c8-149">Set up Azure</span></span>

1. <span data-ttu-id="c93c8-150">[設定 Azure 網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-150">[Set up an Azure network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

      <span data-ttu-id="c93c8-151">a.</span><span class="sxs-lookup"><span data-stu-id="c93c8-151">a.</span></span> <span data-ttu-id="c93c8-152">在容錯移轉之後建立的 Azure VM 會置於這個網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-152">Azure VMs are placed in this network when they're created after failover.</span></span>

      <span data-ttu-id="c93c8-153">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c93c8-153">b.</span></span> <span data-ttu-id="c93c8-154">您可以在 Azure [Resource Manager](../resource-manager-deployment-model.md) 或傳統模式中設定網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-154">You can set up a network in Azure [Resource Manager](../resource-manager-deployment-model.md) or in classic mode.</span></span>

2. <span data-ttu-id="c93c8-155">為複寫的資料設定 [Azure 儲存體帳戶](../storage/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-155">Set up an [Azure storage account](../storage/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>

    <span data-ttu-id="c93c8-156">a.</span><span class="sxs-lookup"><span data-stu-id="c93c8-156">a.</span></span> <span data-ttu-id="c93c8-157">此帳戶可以是標準或[進階](../storage/storage-premium-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-157">The account can be standard or [premium](../storage/storage-premium-storage.md).</span></span>

    <span data-ttu-id="c93c8-158">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c93c8-158">b.</span></span> <span data-ttu-id="c93c8-159">您可以在 Resource Manager 或傳統模式中設定帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-159">You can set up an account in Resource Manager or in classic mode.</span></span>

## <a name="prepare-the-configuration-server"></a><span data-ttu-id="c93c8-160">準備組態伺服器</span><span class="sxs-lookup"><span data-stu-id="c93c8-160">Prepare the configuration server</span></span>

1. <span data-ttu-id="c93c8-161">在內部部署實體伺服器或 VMware VM 上，安裝 Windows Server 2012 R2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="c93c8-161">Install Windows Server 2012 R2 or later on an on-premises physical server or a VMware VM.</span></span>

2. <span data-ttu-id="c93c8-162">確定電腦可存取[必要條件](#prerequisites)中列出的 URL。</span><span class="sxs-lookup"><span data-stu-id="c93c8-162">Make sure the machine has access to the URLs listed in [Prerequisites](#prerequisites).</span></span>

## <a name="prepare-for-mobility-service-installation"></a><span data-ttu-id="c93c8-163">準備行動服務安裝</span><span class="sxs-lookup"><span data-stu-id="c93c8-163">Prepare for Mobility service installation</span></span>

<span data-ttu-id="c93c8-164">如果您要將行動服務推送至實體機器，需要有一個可讓處理序伺服器存取該機器的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-164">If you want to push the Mobility service to a physical machine, you need an account that can be used by the process server to access the machines.</span></span> <span data-ttu-id="c93c8-165">此帳戶僅用於推送安裝。</span><span class="sxs-lookup"><span data-stu-id="c93c8-165">The account is used only for the push installation.</span></span> <span data-ttu-id="c93c8-166">您可以使用網域或本機帳戶：</span><span class="sxs-lookup"><span data-stu-id="c93c8-166">You can use a domain or local account:</span></span>

  - <span data-ttu-id="c93c8-167">在 Windows 上，如果您不使用網域帳戶，則必須停用本機電腦上的遠端使用者存取控制。</span><span class="sxs-lookup"><span data-stu-id="c93c8-167">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="c93c8-168">若要執行此動作，請在登錄的 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System** 下，新增 DWORD 登錄 **LocalAccountTokenFilterPolicy**，其值為 1。</span><span class="sxs-lookup"><span data-stu-id="c93c8-168">To do this, in the registry under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span> <span data-ttu-id="c93c8-169">如果您想要從命令列介面新增適用於 Windows 的登錄項目，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="c93c8-169">If you want to add the registry entry for Windows from a command-line interface, type:</span></span>

        ``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
  - <span data-ttu-id="c93c8-170">在 Linux 上，帳戶應該是來源 Linux 伺服器上的根使用者。</span><span class="sxs-lookup"><span data-stu-id="c93c8-170">For Linux, the account should be a root user on the source Linux server.</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="c93c8-171">建立復原服務保存庫</span><span class="sxs-lookup"><span data-stu-id="c93c8-171">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="select-the-protection-goal"></a><span data-ttu-id="c93c8-172">選取保護目標</span><span class="sxs-lookup"><span data-stu-id="c93c8-172">Select the protection goal</span></span>

<span data-ttu-id="c93c8-173">選取您要複寫的項目以及您要複寫到的位置。</span><span class="sxs-lookup"><span data-stu-id="c93c8-173">Select what you want to replicate and where you want to replicate to.</span></span>

1. <span data-ttu-id="c93c8-174">按一下 [復原服務保存庫] > [保存庫]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-174">Click **Recovery Services vaults** > **vault**.</span></span>
2. <span data-ttu-id="c93c8-175">在 [資源] 功能表中，按一下 [Site Recovery] > [準備基礎結構] > [保護目標]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-175">On the **Resource** menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-vmware-to-azure/choose-goal-physical.PNG)

3. <span data-ttu-id="c93c8-177">在 [保護目標] 中選取 [至 Azure] > [未虛擬化/其他]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-177">In **Protection goal**, select **To Azure** > **Not virtualized / Other**.</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="c93c8-178">設定來源環境</span><span class="sxs-lookup"><span data-stu-id="c93c8-178">Set up the source environment</span></span>

<span data-ttu-id="c93c8-179">安裝設定伺服器、註冊在保存庫及探索 VM。</span><span class="sxs-lookup"><span data-stu-id="c93c8-179">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="c93c8-180">按一下 [Site Recovery] > [準備基礎結構] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-180">Click **Site Recovery** > **Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="c93c8-181">如果您沒有設定伺服器，請按一下 [+設定伺服器]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-181">If you don’t have a configuration server, click **+Configuration Server**.</span></span>

    ![設定來源](./media/site-recovery-vmware-to-azure/set-source1.png)

3. <span data-ttu-id="c93c8-183">在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。</span><span class="sxs-lookup"><span data-stu-id="c93c8-183">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="c93c8-184">下載 **Site Recovery 統一安裝的**安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="c93c8-184">Download the **Site Recovery Unified Setup** installation file.</span></span>
5. <span data-ttu-id="c93c8-185">下載**保存庫註冊金鑰**。</span><span class="sxs-lookup"><span data-stu-id="c93c8-185">Download the **vault registration key**.</span></span> <span data-ttu-id="c93c8-186">您會在執行統一安裝時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="c93c8-186">You need this key when you run Unified Setup.</span></span> <span data-ttu-id="c93c8-187">該金鑰在產生後會維持 5 天有效。</span><span class="sxs-lookup"><span data-stu-id="c93c8-187">The key is valid for five days after you generate it.</span></span>

   ![設定來源](./media/site-recovery-vmware-to-azure/set-source2.png)


## <a name="run-site-recovery-unified-setup"></a><span data-ttu-id="c93c8-189">執行 Site Recovery 統一安裝</span><span class="sxs-lookup"><span data-stu-id="c93c8-189">Run Site Recovery Unified Setup</span></span>

<span data-ttu-id="c93c8-190">開始之前，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="c93c8-190">Before you start, do the following:</span></span>

- <span data-ttu-id="c93c8-191">透過影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="c93c8-191">Get a quick video overview.</span></span> <span data-ttu-id="c93c8-192">(該影片說明如何複寫 VMware VM，但程序類似實體機器複寫。)</span><span class="sxs-lookup"><span data-stu-id="c93c8-192">(The video describes how to replicate VMware VMs, but the process is similar for physical machine replication.)</span></span>

    > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

- <span data-ttu-id="c93c8-193">在設定伺服器電腦上，確定系統時鐘會與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)進行同步。</span><span class="sxs-lookup"><span data-stu-id="c93c8-193">On the configuration server machine, make sure that the system clock is synchronized with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="c93c8-194">如果快慢誤差 15 分鐘，安裝就可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="c93c8-194">If it's 15 minutes in front or behind, Setup might fail.</span></span>
- <span data-ttu-id="c93c8-195">在設定伺服器電腦上，以本機系統管理員身分執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c93c8-195">Run Setup as a local administrator on the configuration server machine.</span></span>
- <span data-ttu-id="c93c8-196">確定已在機器上啟用 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="c93c8-196">Make sure TLS 1.0 is enabled on the machine.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="c93c8-197">您也可以[從命令列](http://aka.ms/installconfigsrv)安裝組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="c93c8-197">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="c93c8-198">設定目標環境</span><span class="sxs-lookup"><span data-stu-id="c93c8-198">Set up the target environment</span></span>

<span data-ttu-id="c93c8-199">設定目標環境之前，請檢查以確定您有 [Azure 儲存體帳戶和網路](#set-up-azure)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-199">Before you set up the target environment, check to make sure that you have an [Azure storage account and network](#set-up-azure).</span></span>

1. <span data-ttu-id="c93c8-200">按一下 [準備基礎結構] > [目標]，然後選取您要使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-200">Click **Prepare Infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="c93c8-201">指定目標部署模型為 Resource Manager 還是傳統的。</span><span class="sxs-lookup"><span data-stu-id="c93c8-201">Specify whether your target deployment model is Resource Manager or classic.</span></span>
3. <span data-ttu-id="c93c8-202">Site Recovery 會檢查以確定您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-202">Site Recovery checks to make sure that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![目標](./media/site-recovery-vmware-to-azure/gs-target.png)

4. <span data-ttu-id="c93c8-204">如果您尚未建立儲存體帳戶或網路，請按一下 [+儲存體帳戶] 或 [+網路]，以建立 Resource Manager 帳戶或網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="c93c8-204">If you haven't created a storage account or network, click **+Storage account** or **+Network** to create a Resource Manager account or network inline.</span></span>

## <a name="set-up-replication-settings"></a><span data-ttu-id="c93c8-205">設定複寫設定</span><span class="sxs-lookup"><span data-stu-id="c93c8-205">Set up replication settings</span></span>

<span data-ttu-id="c93c8-206">在開始之前，請透過影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="c93c8-206">Before you start, get a quick video overview.</span></span> <span data-ttu-id="c93c8-207">(該影片說明如何複寫 VMware VM，但程序類似實體機器複寫。)</span><span class="sxs-lookup"><span data-stu-id="c93c8-207">(The video describes how to replicate VMware VMs, but the process is similar for physical machine replication.)</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="c93c8-208">若要建立新的複寫原則，請按一下 [Site Recovery 基礎結構] > [複寫原則] > [+複寫原則]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-208">To create a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="c93c8-209">在 [建立複寫原則]中，指定原則名稱。</span><span class="sxs-lookup"><span data-stu-id="c93c8-209">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="c93c8-210">在 [RPO 臨界值] 中，指定 RPO 限制。</span><span class="sxs-lookup"><span data-stu-id="c93c8-210">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="c93c8-211">這個值指定資料復原點的建立頻率。</span><span class="sxs-lookup"><span data-stu-id="c93c8-211">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="c93c8-212">連續複寫超過此限制時會產生警示。</span><span class="sxs-lookup"><span data-stu-id="c93c8-212">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="c93c8-213">在 [復原點保留] 中，指定每個復原點的保留週期長度 (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-213">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="c93c8-214">複寫的 VM 可以還原至一個週期內的任何時間點。</span><span class="sxs-lookup"><span data-stu-id="c93c8-214">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="c93c8-215">針對複寫到進階儲存體的電腦，支援保留期最長為 24 小時。</span><span class="sxs-lookup"><span data-stu-id="c93c8-215">Up to 24 hours' retention is supported for machines replicated to premium storage.</span></span> <span data-ttu-id="c93c8-216">針對複寫到標準儲存體的電腦，支援保留期最長為 72 小時。</span><span class="sxs-lookup"><span data-stu-id="c93c8-216">Up to 72 hours' retention is supported for machines replicated to standard storage.</span></span>
5. <span data-ttu-id="c93c8-217">在 [應用程式一致快照集頻率] 中，指定建立包含應用程式一致快照集之復原點的頻率 (以分鐘為單位)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-217">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots are created.</span></span> <span data-ttu-id="c93c8-218">按一下 [確定]  以建立原則。</span><span class="sxs-lookup"><span data-stu-id="c93c8-218">Click **OK** to create the policy.</span></span>

    ![複寫原則](./media/site-recovery-vmware-to-azure/gs-replication2.png)

6. <span data-ttu-id="c93c8-220">當您建立新的原則時，該原則會自動與設定伺服器產生關聯。</span><span class="sxs-lookup"><span data-stu-id="c93c8-220">When you create a new policy, it's automatically associated with the configuration server.</span></span> <span data-ttu-id="c93c8-221">依預設會自動建立容錯回復的比對原則。</span><span class="sxs-lookup"><span data-stu-id="c93c8-221">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="c93c8-222">例如，如果複寫原則是 **rep-policy**，容錯回復原則就會是 **rep-policy-failback**。</span><span class="sxs-lookup"><span data-stu-id="c93c8-222">For example, if the replication policy is **rep-policy**, then the failback policy is **rep-policy-failback**.</span></span> <span data-ttu-id="c93c8-223">從 Azure 起始容錯回復時才會使用此原則。</span><span class="sxs-lookup"><span data-stu-id="c93c8-223">This policy isn't used until you initiate a failback from Azure.</span></span>  


## <a name="plan-capacity"></a><span data-ttu-id="c93c8-224">規劃容量</span><span class="sxs-lookup"><span data-stu-id="c93c8-224">Plan capacity</span></span>

1. <span data-ttu-id="c93c8-225">現在您已設定基本基礎結構，可以思考容量規劃，並找出您是否需要額外的資源。</span><span class="sxs-lookup"><span data-stu-id="c93c8-225">Now that you have your basic infrastructure set up, you can think about capacity planning and figure out whether you need additional resources.</span></span> <span data-ttu-id="c93c8-226">[深入了解](site-recovery-plan-capacity-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-226">[Learn more](site-recovery-plan-capacity-vmware.md).</span></span>
2. <span data-ttu-id="c93c8-227">當您完成容量規劃時，請在 [已完成容量計劃了嗎?] 中選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-227">When you’re done with capacity planning, select **Yes** in **Have you completed capacity planning?**</span></span>

   ![容量規劃](./media/site-recovery-vmware-to-azure/gs-capacity-planning.png)


## <a name="prepare-vms-for-replication"></a><span data-ttu-id="c93c8-229">準備 VM 進行複寫</span><span class="sxs-lookup"><span data-stu-id="c93c8-229">Prepare VMs for replication</span></span>

<span data-ttu-id="c93c8-230">您想要複寫的所有電腦都必須安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="c93c8-230">All machines that you want to replicate must have the Mobility service installed.</span></span> <span data-ttu-id="c93c8-231">安裝行動服務有許多方式︰</span><span class="sxs-lookup"><span data-stu-id="c93c8-231">You can install the Mobility service in a number of ways:</span></span>

- <span data-ttu-id="c93c8-232">從處理伺服器使用推送安裝來安裝服務。</span><span class="sxs-lookup"><span data-stu-id="c93c8-232">Install the service with a push installation from the process server.</span></span> <span data-ttu-id="c93c8-233">您需要預先準備機器，才能使用這個方法。</span><span class="sxs-lookup"><span data-stu-id="c93c8-233">You need to prepare machines in advance to use this method.</span></span>
- <span data-ttu-id="c93c8-234">使用諸如 System Center Configuration Manager 或 Azure 自動化 Desired State Configuration 等部署工具來安裝服務。</span><span class="sxs-lookup"><span data-stu-id="c93c8-234">Install the service by using deployment tools such as System Center Configuration Manager or Azure Automation Desired State Configuration.</span></span>
- <span data-ttu-id="c93c8-235">手動安裝服務。</span><span class="sxs-lookup"><span data-stu-id="c93c8-235">Install the service manually.</span></span>

<span data-ttu-id="c93c8-236">[深入了解](site-recovery-vmware-to-azure-install-mob-svc.md)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-236">[Learn more](site-recovery-vmware-to-azure-install-mob-svc.md).</span></span>


## <a name="enable-replication"></a><span data-ttu-id="c93c8-237">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="c93c8-237">Enable replication</span></span>

<span data-ttu-id="c93c8-238">開始之前：</span><span class="sxs-lookup"><span data-stu-id="c93c8-238">Before you start:</span></span>

- <span data-ttu-id="c93c8-239">您的 Azure 使用者帳戶必須具有特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)，才能將新的虛擬機器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="c93c8-239">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>
- <span data-ttu-id="c93c8-240">當您新增或修改 VM 時，可能需要 15 分鐘或更久，變更才會生效，也才會出現在入口網站中。</span><span class="sxs-lookup"><span data-stu-id="c93c8-240">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect and for them to appear in the portal.</span></span>
- <span data-ttu-id="c93c8-241">您可以在 [設定伺服器] > [上次連絡時間] 中，查看上次探索 VM 的時間。</span><span class="sxs-lookup"><span data-stu-id="c93c8-241">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="c93c8-242">若要新增 VM 而不等候已排定的探索，請醒目提示設定伺服器 (不要按一下)，然後按一下 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-242">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>
- <span data-ttu-id="c93c8-243">如果已準備好 VM 進行推入安裝，當您啟用複寫時，處理序伺服器會自動安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="c93c8-243">If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="c93c8-244">透過影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="c93c8-244">Get a quick video overview.</span></span> <span data-ttu-id="c93c8-245">(該影片說明如何複寫 VMware VM，但程序類似實體機器複寫。)</span><span class="sxs-lookup"><span data-stu-id="c93c8-245">(The video describes how to replicate VMware VMs, but the process is similar for physical machine replication.)</span></span>

    >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]


### <a name="exclude-disks-from-replication"></a><span data-ttu-id="c93c8-246">從複寫排除磁碟</span><span class="sxs-lookup"><span data-stu-id="c93c8-246">Exclude disks from replication</span></span>

<span data-ttu-id="c93c8-247">依預設會複寫機器上的所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="c93c8-247">By default, all disks on a machine are replicated.</span></span> <span data-ttu-id="c93c8-248">您可以從複寫排除磁碟。</span><span class="sxs-lookup"><span data-stu-id="c93c8-248">You can exclude disks from replication.</span></span> <span data-ttu-id="c93c8-249">例如，您可能不想要複寫具有暫存資料的磁碟，或是每次電腦或應用程式重新啟動時便重新整理的資料 (例如 pagefile.sys 或 SQL Server tempdb)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-249">For example, you might not want to replicate disks with temporary data or data that's refreshed each time a machine or application restarts (for example, pagefile.sys or SQL Server tempdb).</span></span>

### <a name="replicate-vms"></a><span data-ttu-id="c93c8-250">複寫 VM</span><span class="sxs-lookup"><span data-stu-id="c93c8-250">Replicate VMs</span></span>

1. <span data-ttu-id="c93c8-251">按一下 [複寫應用程式] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-251">Click **Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="c93c8-252">在 [來源] 中，選取 [內部部署]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-252">In **Source**, select **On-premises**.</span></span>
3. <span data-ttu-id="c93c8-253">在 [來源位置] 中，選取設定伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c93c8-253">In **Source location**, select the configuration server name.</span></span>
4. <span data-ttu-id="c93c8-254">在 [機器類型] 中，選取 [實體機器]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-254">In **Machine type**, select **Physical Machines**.</span></span>
5. <span data-ttu-id="c93c8-255">在 [處理序伺服器] 中，選擇處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="c93c8-255">In **Process server**, choose the process server.</span></span> <span data-ttu-id="c93c8-256">如果您尚未建立任何額外的處理序伺服器，這個伺服器就會成為設定伺服器。</span><span class="sxs-lookup"><span data-stu-id="c93c8-256">If you haven't created any additional process servers, this server is the configuration server.</span></span> <span data-ttu-id="c93c8-257">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c93c8-257">Then click **OK**.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/chooseVM.png)

6. <span data-ttu-id="c93c8-259">在 [目標] 中，選取您想要在容錯移轉後，在其中建立 Azure VM 的**訂用帳戶**和**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="c93c8-259">In **Target**, select the **Subscription** and the **Resource group** in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="c93c8-260">選擇您想要在 Azure (傳統或 Resource Manager) 中，針對容錯移轉 VM 使用的部署模型。</span><span class="sxs-lookup"><span data-stu-id="c93c8-260">Choose the deployment model that you want to use in Azure (classic or Resource Manager) for the failed-over VMs.</span></span>

7. <span data-ttu-id="c93c8-261">選取您要用來複寫資料的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-261">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="c93c8-262">如果您不想要使用已設定的帳戶，您可以建立新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-262">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="c93c8-263">選取 Azure VM 在容錯移轉後所要連線的 **Azure 網路**和**子網路**。</span><span class="sxs-lookup"><span data-stu-id="c93c8-263">Select the **Azure network** and **Subnet** to which Azure VMs connect after failover.</span></span> <span data-ttu-id="c93c8-264">選取 [立即設定選取的機器]，將網路設定套用至您選取要進行保護的所有機器。</span><span class="sxs-lookup"><span data-stu-id="c93c8-264">Select **Configure now for selected machines** to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="c93c8-265">選取 [稍後設定] 以選取每部機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-265">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="c93c8-266">如果您不想使用現有的網路，您可以建立網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-266">If you don't want to use an existing network, you can create one.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/targetsettings.png)

9. <span data-ttu-id="c93c8-268">在**實體機器**中，按一下 [+實體機器]，然後輸入**名稱**和 **IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="c93c8-268">In **Physical machines**, click **+Physical machine** and enter the **Name** and **IP address**.</span></span> <span data-ttu-id="c93c8-269">選擇您想要複寫之電腦的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c93c8-269">Choose the operating system of the machine you want to replicate.</span></span> <span data-ttu-id="c93c8-270">需要花費數分鐘的時間，才能探索到電腦並加以顯示於清單中。</span><span class="sxs-lookup"><span data-stu-id="c93c8-270">It takes a few minutes until machines are discovered and shown in the list.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/machineselect.png)

10. <span data-ttu-id="c93c8-272">在 [屬性] > [設定屬性] 中，選取處理序伺服器要用來在電腦上自動安裝行動服務的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93c8-272">In **Properties** > **Configure properties**, select the account to be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="c93c8-273">依預設會複寫所有磁碟。</span><span class="sxs-lookup"><span data-stu-id="c93c8-273">By default, all disks are replicated.</span></span> <span data-ttu-id="c93c8-274">按一下 [所有磁碟]，然後將任何您不想要複寫的磁碟清除。</span><span class="sxs-lookup"><span data-stu-id="c93c8-274">Click **All Disks**, and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="c93c8-275">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c93c8-275">Then click **OK**.</span></span> <span data-ttu-id="c93c8-276">您可以稍後再設定其他 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="c93c8-276">You can set additional VM properties later.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/configprop.png)

12. <span data-ttu-id="c93c8-278">在 [複寫設定] > [設定複寫設定] 中，確認已選取正確的複寫原則。</span><span class="sxs-lookup"><span data-stu-id="c93c8-278">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="c93c8-279">如果您修改原則，變更就會套用至複寫電腦及新的電腦。</span><span class="sxs-lookup"><span data-stu-id="c93c8-279">If you modify a policy, changes are applied to the replicating machine and to new machines.</span></span>
13. <span data-ttu-id="c93c8-280">如果您想要將機器聚集成一個複寫群組，請啟用 [多部 VM 一致性]  ，並指定群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="c93c8-280">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="c93c8-281">然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c93c8-281">Then click **OK**.</span></span> <span data-ttu-id="c93c8-282">請注意：</span><span class="sxs-lookup"><span data-stu-id="c93c8-282">Note that:</span></span>

    <span data-ttu-id="c93c8-283">a.</span><span class="sxs-lookup"><span data-stu-id="c93c8-283">a.</span></span> <span data-ttu-id="c93c8-284">複寫群組中的電腦會一起複寫，且在容錯移轉時，會有共用的損毀一致和應用程式一致的復原點。</span><span class="sxs-lookup"><span data-stu-id="c93c8-284">Machines in replication groups replicate together and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>

    <span data-ttu-id="c93c8-285">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c93c8-285">b.</span></span> <span data-ttu-id="c93c8-286">我們建議您將 VM 與實體伺服器一起收集，讓它們鏡像您的工作負載。</span><span class="sxs-lookup"><span data-stu-id="c93c8-286">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="c93c8-287">啟用多 VM 一致性可能會影響工作負載的效能。</span><span class="sxs-lookup"><span data-stu-id="c93c8-287">Enabling multi-VM consistency can affect workload performance.</span></span> <span data-ttu-id="c93c8-288">僅在電腦執行相同的工作負載且需要一致性時，您才應該使用它。</span><span class="sxs-lookup"><span data-stu-id="c93c8-288">It should be used only if machines are running the same workload and you need consistency.</span></span>

    ![啟用複寫](./media/site-recovery-physical-to-azure/policy.png)

14. <span data-ttu-id="c93c8-290">按一下 [啟用複寫] 。</span><span class="sxs-lookup"><span data-stu-id="c93c8-290">Click **Enable Replication**.</span></span> <span data-ttu-id="c93c8-291">您可以在 [設定]  >  [作業]  >  [Site Recovery 作業] 中，追蹤 [啟用保護] 作業的進度。</span><span class="sxs-lookup"><span data-stu-id="c93c8-291">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="c93c8-292">執行 [完成保護] 作業之後，機器即準備好進行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c93c8-292">After the **Finalize Protection** job runs, the machine is ready for failover.</span></span>

<span data-ttu-id="c93c8-293">啟用複寫後，如果您設定推送安裝，就會安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="c93c8-293">After you enable replication, the Mobility service is installed if you set up push installation.</span></span> <span data-ttu-id="c93c8-294">在電腦上將行動服務推送安裝之後，保護作業就會啟動且失敗。</span><span class="sxs-lookup"><span data-stu-id="c93c8-294">After the Mobility service is push installed on a machine, a protection job starts and fails.</span></span> <span data-ttu-id="c93c8-295">在失敗之後，您需要手動將每一部電腦重新啟動。</span><span class="sxs-lookup"><span data-stu-id="c93c8-295">After the failure, you need to manually restart each machine.</span></span> <span data-ttu-id="c93c8-296">然後，保護作業會再次啟動，並進行初始複寫。</span><span class="sxs-lookup"><span data-stu-id="c93c8-296">Then the protection job begins again, and initial replication occurs.</span></span>


### <a name="view-and-manage-azure-vm-properties"></a><span data-ttu-id="c93c8-297">檢視及管理 Azure VM 屬性</span><span class="sxs-lookup"><span data-stu-id="c93c8-297">View and manage Azure VM properties</span></span>

<span data-ttu-id="c93c8-298">我們建議您確認 VM 屬性，並進行任何需要的變更。</span><span class="sxs-lookup"><span data-stu-id="c93c8-298">We recommend that you verify the VM properties and make any changes you need.</span></span>

1. <span data-ttu-id="c93c8-299">按一下 [複寫的項目]，然後選取電腦。</span><span class="sxs-lookup"><span data-stu-id="c93c8-299">Click **Replicated items**, and select the machine.</span></span> <span data-ttu-id="c93c8-300">[程式集]  刀鋒視窗會顯示機器設定與狀態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c93c8-300">The **Essentials** blade shows information about machines settings and status.</span></span>
2. <span data-ttu-id="c93c8-301">在 [屬性] 中，您可以檢視 VM 的複寫和容錯移轉資訊。</span><span class="sxs-lookup"><span data-stu-id="c93c8-301">In **Properties**, you can view replication and failover information for the VM.</span></span>
3. <span data-ttu-id="c93c8-302">在 [計算和網路] > [計算屬性] 中，您可以指定 Azure VM 名稱和目標大小。</span><span class="sxs-lookup"><span data-stu-id="c93c8-302">In **Compute and Network** > **Compute properties**, you can specify the Azure VM name and target size.</span></span> <span data-ttu-id="c93c8-303">視需要修改名稱以符合 [Azure 需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) 。</span><span class="sxs-lookup"><span data-stu-id="c93c8-303">Modify the name to comply with [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) if you need to.</span></span>
4. <span data-ttu-id="c93c8-304">修改目標網路、子網路以及將指派給 Azure VM 的 IP 位址等設定：</span><span class="sxs-lookup"><span data-stu-id="c93c8-304">Modify settings for the target network, subnet, and IP address that are assigned to the Azure VM:</span></span>

    <span data-ttu-id="c93c8-305">a.</span><span class="sxs-lookup"><span data-stu-id="c93c8-305">a.</span></span> <span data-ttu-id="c93c8-306">您可以設定目標 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c93c8-306">You can set the target IP address.</span></span>

    <span data-ttu-id="c93c8-307">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c93c8-307">b.</span></span>  <span data-ttu-id="c93c8-308">如果您未提供地址，容錯移轉的電腦就會使用 DHCP。</span><span class="sxs-lookup"><span data-stu-id="c93c8-308">If you don't provide an address, the failed-over machine uses DHCP.</span></span>

    <span data-ttu-id="c93c8-309">c.</span><span class="sxs-lookup"><span data-stu-id="c93c8-309">c.</span></span> <span data-ttu-id="c93c8-310">如果您設定的位址在容錯移轉時無法使用，容錯移轉就無法運作。</span><span class="sxs-lookup"><span data-stu-id="c93c8-310">If you set an address that isn't available at failover, failover doesn't work.</span></span>

    <span data-ttu-id="c93c8-311">d.</span><span class="sxs-lookup"><span data-stu-id="c93c8-311">d.</span></span> <span data-ttu-id="c93c8-312">如果位址可用於測試容錯移轉網路，則相同的目標 IP 位址可用於測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c93c8-312">The same target IP address can be used for test failover if the address is available in the test failover network.</span></span>

    <span data-ttu-id="c93c8-313">e.</span><span class="sxs-lookup"><span data-stu-id="c93c8-313">e.</span></span> <span data-ttu-id="c93c8-314">網路介面卡的數目會視您指定給目標虛擬機器的大小而有所不同：</span><span class="sxs-lookup"><span data-stu-id="c93c8-314">The number of network adapters is dictated by the size you specify for the target virtual machine:</span></span>

     - <span data-ttu-id="c93c8-315">如果來源電腦上的網路介面卡數目等於或小於針對目標電腦大小所允許的介面卡數目，目標就會具備與來源相同的介面卡數目。</span><span class="sxs-lookup"><span data-stu-id="c93c8-315">If the number of network adapters on the source machine is the same as, or less than, the number of adapters allowed for the target machine size, then the target has the same number of adapters as the source.</span></span>
     - <span data-ttu-id="c93c8-316">如果來源虛擬機器的介面卡數目超過針對目標大小所允許的數目，則使用目標大小的最大值。</span><span class="sxs-lookup"><span data-stu-id="c93c8-316">If the number of adapters for the source virtual machine exceeds the number allowed for the target size, then the target size maximum is used.</span></span>
     - <span data-ttu-id="c93c8-317">例如，如果來源電腦具有兩張網路介面卡，而目標電腦大小支援四張，目標電腦就會有兩張介面卡。</span><span class="sxs-lookup"><span data-stu-id="c93c8-317">For example, if a source machine has two network adapters and the target machine size supports four, the target machine has two adapters.</span></span> <span data-ttu-id="c93c8-318">如果來源電腦具有兩張介面卡，但支援的目標大小僅支援一張介面卡，目標電腦就只會有一張介面卡。</span><span class="sxs-lookup"><span data-stu-id="c93c8-318">If the source machine has two adapters but the supported target size supports only one, then the target machine has only one adapter.</span></span>     
   - <span data-ttu-id="c93c8-319">如果虛擬機器有多張網路介面卡，就會全部連線至相同的網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-319">If the virtual machine has multiple network adapters, they all connect to the same network.</span></span>
   - <span data-ttu-id="c93c8-320">如果虛擬機器具有多張網路介面卡，清單中顯示的第一項就會變成 Azure VM 中的預設網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="c93c8-320">If the virtual machine has multiple network adapters, then the first one shown in the list becomes the *Default* network adapter in the Azure VM.</span></span>
5. <span data-ttu-id="c93c8-321">在 [磁碟] 中，您可以看見 VM 作業系統和將要複寫的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c93c8-321">In **Disks**, you can see the VM operating system and the data disks that are replicated.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="c93c8-322">執行測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="c93c8-322">Run a test failover</span></span>

<span data-ttu-id="c93c8-323">一切就緒後，執行測試容錯移轉，確定一切如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="c93c8-323">After you've set up everything, run a test failover to make sure everything's working as expected.</span></span> <span data-ttu-id="c93c8-324">開始之前，請觀看影片快速建立概念。</span><span class="sxs-lookup"><span data-stu-id="c93c8-324">Watch a quick video overview before you start.</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


1. <span data-ttu-id="c93c8-325">若要將單一電腦容錯移轉，請在 [設定] > [複寫的項目] 中，按一下 [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-325">To fail over a single machine, in **Settings** > **Replicated Items**, click **Test failover**.</span></span>

    ![測試容錯移轉](./media/site-recovery-vmware-to-azure/TestFailover.png)

2. <span data-ttu-id="c93c8-327">若要容錯移轉復原方案，請在 [設定]  >  [復原方案] 中，以滑鼠右鍵按一下方案 > [測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-327">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan > **Test Failover**.</span></span> <span data-ttu-id="c93c8-328">若要建立復原方案，請[遵循這些指示](site-recovery-create-recovery-plans.md)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-328">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span>  
3. <span data-ttu-id="c93c8-329">在 [測試容錯移轉] 中，選取 Azure VM 在容錯移轉之後所要連線的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="c93c8-329">In **Test Failover**, select the Azure network to which Azure VMs are connected after failover occurs.</span></span>
4. <span data-ttu-id="c93c8-330">按一下 [確定]  即可開始容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="c93c8-330">Click **OK** to begin the failover.</span></span> <span data-ttu-id="c93c8-331">您可以按一下 VM 以開啟其屬性，或在保存庫名稱 > [設定] > [作業] > [Site Recovery 作業] 中的 [測試容錯移轉] 作業上按一下，從而追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="c93c8-331">You can track progress by clicking the VM to open its properties or by clicking the **Test Failover** job in vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>
5. <span data-ttu-id="c93c8-332">容錯移轉完成之後，您應該也會看到複本 Azure 電腦出現在 Azure 入口網站> [虛擬機器] 中。</span><span class="sxs-lookup"><span data-stu-id="c93c8-332">After the failover finishes, you should also be able to see the replica Azure machine appear in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="c93c8-333">請確定 VM 為適當的大小、已連線到適當的網路，而且正在執行中。</span><span class="sxs-lookup"><span data-stu-id="c93c8-333">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>
6. <span data-ttu-id="c93c8-334">如果您[已準備好容錯移轉後的連線](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)，您應該能夠連接到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c93c8-334">If you [prepared for connections after failover](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover), you should be able to connect to the Azure VM.</span></span>
7. <span data-ttu-id="c93c8-335">完成後，在復原方案上按一下 [清除測試容錯移轉]。</span><span class="sxs-lookup"><span data-stu-id="c93c8-335">After you're done, click **Cleanup test failover** on the recovery plan.</span></span> <span data-ttu-id="c93c8-336">在 [記事] 中，記錄並儲存關於測試容錯移轉的任何觀察。</span><span class="sxs-lookup"><span data-stu-id="c93c8-336">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="c93c8-337">此步驟會將測試容錯移轉期間所建立的虛擬機器刪除。</span><span class="sxs-lookup"><span data-stu-id="c93c8-337">This step deletes the virtual machines that were created during test failover.</span></span>

<span data-ttu-id="c93c8-338">如需詳細資訊，請參閱[測試容錯移轉至 Azure](site-recovery-test-failover-to-azure.md)文件。</span><span class="sxs-lookup"><span data-stu-id="c93c8-338">For more information, see the [Test failover to Azure](site-recovery-test-failover-to-azure.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c93c8-339">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c93c8-339">Next steps</span></span>

<span data-ttu-id="c93c8-340">複寫開始正常執行之後，運作中斷時就會容錯移轉至 Azure，而且會從複寫的資料建立 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c93c8-340">After you get replication up and running, when an outage occurs you fail over to Azure, and Azure VMs are created from the replicated data.</span></span> <span data-ttu-id="c93c8-341">然後，您可以在 Azure 中存取工作負載和應用程式，直到恢復正常運作時容錯回復至主要位置。</span><span class="sxs-lookup"><span data-stu-id="c93c8-341">You can then access workloads and apps in Azure, until you fail back to your primary location when it returns to normal operations.</span></span>

- <span data-ttu-id="c93c8-342">[深入了解](site-recovery-failover.md)不同類型的容錯移轉及執行方法。</span><span class="sxs-lookup"><span data-stu-id="c93c8-342">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="c93c8-343">如果您要移轉電腦而不是複寫和容錯回復，請[深入了解](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-343">If you're migrating machines rather than replicating and failing back, [read more](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).</span></span>
- <span data-ttu-id="c93c8-344">當複寫實體機器，您可以只容錯回復到 VMware 環境。</span><span class="sxs-lookup"><span data-stu-id="c93c8-344">When replicating physical machines, you can only failback to a VMware environment.</span></span> <span data-ttu-id="c93c8-345">[了解容錯回復](site-recovery-failback-azure-to-vmware.md)。</span><span class="sxs-lookup"><span data-stu-id="c93c8-345">[Read about failback](site-recovery-failback-azure-to-vmware.md).</span></span>

## <a name="third-party-software-notices-and-information"></a><span data-ttu-id="c93c8-346">第三方廠商軟體注意事項和資訊</span><span class="sxs-lookup"><span data-stu-id="c93c8-346">Third-party software notices and information</span></span>
<span data-ttu-id="c93c8-347">Do Not Translate or Localize</span><span class="sxs-lookup"><span data-stu-id="c93c8-347">Do Not Translate or Localize</span></span>

<span data-ttu-id="c93c8-348">The software and firmware running in the Microsoft product or service is based on or incorporates material from the projects listed below (collectively, “Third-Party Code”).</span><span class="sxs-lookup"><span data-stu-id="c93c8-348">The software and firmware running in the Microsoft product or service is based on or incorporates material from the projects listed below (collectively, “Third-Party Code”).</span></span> <span data-ttu-id="c93c8-349">Microsoft is not the original author of the Third-Party Code.</span><span class="sxs-lookup"><span data-stu-id="c93c8-349">Microsoft is not the original author of the Third-Party Code.</span></span> <span data-ttu-id="c93c8-350">The original copyright notice and license, under which Microsoft received such Third-Party Code, are set forth below.</span><span class="sxs-lookup"><span data-stu-id="c93c8-350">The original copyright notice and license, under which Microsoft received such Third-Party Code, are set forth below.</span></span>

<span data-ttu-id="c93c8-351">The information in Section A is regarding Third-Party Code components from the projects listed below.</span><span class="sxs-lookup"><span data-stu-id="c93c8-351">The information in Section A is regarding Third-Party Code components from the projects listed below.</span></span> <span data-ttu-id="c93c8-352">Such licenses and information are provided for informational purposes only.</span><span class="sxs-lookup"><span data-stu-id="c93c8-352">Such licenses and information are provided for informational purposes only.</span></span> <span data-ttu-id="c93c8-353">This Third-Party Code is being relicensed to you by Microsoft under Microsoft's software licensing terms for the Microsoft product or service.</span><span class="sxs-lookup"><span data-stu-id="c93c8-353">This Third-Party Code is being relicensed to you by Microsoft under Microsoft's software licensing terms for the Microsoft product or service.</span></span>  

<span data-ttu-id="c93c8-354">The information in Section B is regarding Third Party Code components that are being made available to you by Microsoft under the original licensing terms.</span><span class="sxs-lookup"><span data-stu-id="c93c8-354">The information in Section B is regarding Third Party Code components that are being made available to you by Microsoft under the original licensing terms.</span></span>

<span data-ttu-id="c93c8-355">The complete file can be found on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428).</span><span class="sxs-lookup"><span data-stu-id="c93c8-355">The complete file can be found on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428).</span></span> <span data-ttu-id="c93c8-356">Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.</span><span class="sxs-lookup"><span data-stu-id="c93c8-356">Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel, or otherwise.</span></span>
