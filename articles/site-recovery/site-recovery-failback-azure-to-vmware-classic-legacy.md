---
title: "在舊版傳統入口網站中從 Azure 容錯回復 VMware VM | Microsoft Docs"
description: "這篇文章說明如何利用 Azure Site Recovery 容錯回復已複寫至 Azure 的 VMware 虛擬機器。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: a63524bf-990c-42ee-8554-e017e6e67e68
ms.service: site-recovery
ms.devlang: na
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 3053fc622c6343898e2007b8aaafbe1fa8e6934e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-to-vmware-with-azure-site-recovery-legacy"></a><span data-ttu-id="b8ce2-103">利用 Azure Site Recovery 將 VMware 虛擬機器和實體伺服器從 Azure 容錯回復到 VMware (舊版)</span><span class="sxs-lookup"><span data-stu-id="b8ce2-103">Fail back VMware virtual machines and physical servers from Azure to VMware with Azure Site Recovery (legacy)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8ce2-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b8ce2-104">Azure Portal</span></span>](site-recovery-failback-azure-to-vmware.md)
> * [<span data-ttu-id="b8ce2-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="b8ce2-105">Azure Classic Portal</span></span>](site-recovery-failback-azure-to-vmware-classic.md)
> * [<span data-ttu-id="b8ce2-106">Azure 傳統入口網站 (舊版)</span><span class="sxs-lookup"><span data-stu-id="b8ce2-106">Azure Classic Portal (Legacy)</span></span>](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

<span data-ttu-id="b8ce2-107">本文件說明如何在您使用[什麼是 Azure Site Recovery？](site-recovery-overview.md)從內部部署網站複寫到 Azure 之後，將 VMware 虛擬機器和 Windows/Linux 實體伺服器從 Azure 容錯回復到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-107">This article describes how to fail back VMware virtual machines and Windows/Linux physical servers from Azure to your on-premises site after you've replicated from your on-premises site to Azure using [Azure Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="b8ce2-108">本文說明的是舊版設定，不應用於新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-108">This article describes an old configuration and shouldn't be used for new vaults.</span></span>

## <a name="architecture"></a><span data-ttu-id="b8ce2-109">架構</span><span class="sxs-lookup"><span data-stu-id="b8ce2-109">Architecture</span></span>
<span data-ttu-id="b8ce2-110">這個圖代表容錯移轉和容錯回復案例。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-110">This diagram represents the failover and failback scenario.</span></span> <span data-ttu-id="b8ce2-111">藍線是在容錯移轉期間使用的連線。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-111">The blue lines are the connections used during failover.</span></span> <span data-ttu-id="b8ce2-112">紅線是在容錯回復期間使用的連線。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-112">The red lines are the connections used during failback.</span></span> <span data-ttu-id="b8ce2-113">帶有箭號的線條表示會透過網際網路。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-113">The lines with arrows go over the internet.</span></span>

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a><span data-ttu-id="b8ce2-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="b8ce2-114">Before you start</span></span>
* <span data-ttu-id="b8ce2-115">您應該已容錯移轉您的 VMware VM 或實體伺服器，且它們應該在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-115">You should have failed over your VMware VMs or physical servers and they should be running in Azure.</span></span>
* <span data-ttu-id="b8ce2-116">您應該注意，只能將 VMware 虛擬機器和 Windows/Linux 實體伺服器從 Azure 容錯移轉到內部部署主要網站中的 VMware 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-116">You should note that you can only fail back VMware virtual machines and Windows/Linux physical servers from Azure to VMware virtual machines in the on-premises primary site.</span></span>  <span data-ttu-id="b8ce2-117">如果您正在容錯回復實體機器，容錯移轉至 Azure 會將它轉換至 Azure VM，容錯回復到 VMware 會將它轉換至 VMware VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-117">If you're failing back a physical machine, failover to Azure will convert it to an Azure VM, and failback to VMware will convert it to a VMware VM.</span></span>

<span data-ttu-id="b8ce2-118">設定容錯回復的方式如下︰</span><span class="sxs-lookup"><span data-stu-id="b8ce2-118">Here's how you set up failback:</span></span>

1. <span data-ttu-id="b8ce2-119">**設定容錯回復元件**：您必須在內部部署設定 vContinuum 伺服器，並將它指向 Azure 中的組態伺服器 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-119">**Set up failback components**: You'll need to set up a vContinuum server on-premises, and point it to the configuration server VM in Azure.</span></span> <span data-ttu-id="b8ce2-120">您也會將處理序伺服器設定為 Azure VM，以將資料傳送回內部部署主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-120">You'll also set up a process server as an Azure VM to send data back to the on-premises master target server.</span></span> <span data-ttu-id="b8ce2-121">您向處理容錯移轉的組態伺服器註冊處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-121">You register the process server with the configuration server that  handled the failover.</span></span> <span data-ttu-id="b8ce2-122">您安裝內部部署主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-122">You install an on-premises master target server.</span></span> <span data-ttu-id="b8ce2-123">如果您需要 Windows 主要目標伺服器，它會在您安裝 vContinuum 時自動設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-123">If you need a Windows master target server it's set up automatically when you install vContinuum.</span></span> <span data-ttu-id="b8ce2-124">如果您需要 Linux，您必須在不同的伺服器上手動設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-124">If you need Linux you'll need to set it up manually on a separate server.</span></span>
2. <span data-ttu-id="b8ce2-125">**啟用保護和容錯回復**︰您已經設定好元件之後，在 vContinuum 中您將需要為已容錯移轉的 Azure VM 啟用保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-125">**Enable protection and failback**: After you've set up the components, in vContinuum you'll need to enable protection for failed over Azure VMs.</span></span> <span data-ttu-id="b8ce2-126">您將執行 VM 整備檢查，並從 Azure 執行容錯移轉至您的內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-126">You'll run a readiness check on the VMs and run a failover from Azure to your on-premises site.</span></span> <span data-ttu-id="b8ce2-127">完成容錯回復之後，您重新保護內部部署機器，讓它們開始複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-127">After failback finishes you reprotect on-premises machines so that they start replicating to Azure.</span></span>

## <a name="step-1-install-vcontinuum-on-premises"></a><span data-ttu-id="b8ce2-128">步驟 1：安裝 vContinuum 內部部署</span><span class="sxs-lookup"><span data-stu-id="b8ce2-128">Step 1: Install vContinuum on-premises</span></span>
<span data-ttu-id="b8ce2-129">您必須在內部部署安裝 vContinuum 伺服器並將它指向組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-129">You'll need to install a vContinuum server on premises and point it to the configuration server.</span></span>

1. <span data-ttu-id="b8ce2-130">[下載 vContinuum](http://go.microsoft.com/fwlink/?linkid=526305)。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-130">[Download vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).</span></span>
2. <span data-ttu-id="b8ce2-131">然後下載 [vContinuum 更新](http://go.microsoft.com/fwlink/?LinkID=533813) 版本。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-131">Then download the [vContinuum update](http://go.microsoft.com/fwlink/?LinkID=533813) version.</span></span>
3. <span data-ttu-id="b8ce2-132">安裝最新版本的 vContinuum。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-132">Install the latest version of vContinuum.</span></span> <span data-ttu-id="b8ce2-133">在 [歡迎] 頁面中按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-133">On the **Welcome** page click **Next**.</span></span>
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. <span data-ttu-id="b8ce2-134">在精靈的第一個頁面上，指定 CX 伺服器 IP 位址和 CX 伺服器連接埠。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-134">On the first page of the wizard specify the CX server IP address and the CX server port.</span></span> <span data-ttu-id="b8ce2-135">選取 [使用 HTTPS] 。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-135">Select **Use HTTPS**.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. <span data-ttu-id="b8ce2-136">在 Azure 中組態伺服器 VM 的 [儀表板]  索引標籤上尋找組態伺服器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-136">Find the configuration server IP address on the **Dashboard** tab of the configuration server VM in Azure.</span></span>
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. <span data-ttu-id="b8ce2-137">在 Azure 中組態伺服器 VM 的 [端點]  索引標籤上尋找組態伺服器 HTTPS 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-137">Find the configuration server HTTPS public port on the **Endpoints** tab of the configuration server VM in Azure.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. <span data-ttu-id="b8ce2-138">在 [CS 複雜密碼詳細資料] 頁面上，指定您在註冊組態伺服器時記下的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-138">On the **CS Passphrase Details** page specify the passphrase that you noted down when you registered the configuration server.</span></span> <span data-ttu-id="b8ce2-139">如果您不記得，請在組態伺服器 VM 上的 **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase** 中查看。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-139">If you don't remember it check it in **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase** on the configuration server VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. <span data-ttu-id="b8ce2-140">在 [選取目的地位置] 頁面上，指定您要安裝 vContinuum 伺服器的地方，並按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-140">In the **Select Destination Location** page specify where you want to install the vContinuum server and click **Install**.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. <span data-ttu-id="b8ce2-141">安裝完成後，您可以啟動 vContinuum。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-141">After installation completes, you can launch vContinuum.</span></span>
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a><span data-ttu-id="b8ce2-142">步驟 2：在 Azure 中安裝處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-142">Step 2: Install a process server in Azure</span></span>
<span data-ttu-id="b8ce2-143">您必須在 Azure 上安裝處理序伺服器，讓 Azure 中的 VM 可以將資料傳回內部部署的主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-143">You need to install a process server in Azure so that the VMs in Azure can send the data back to an on-premises master target server.</span></span>

1. <span data-ttu-id="b8ce2-144">在 Azure 的 [組態伺服器]  頁面中，選取要加入新的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-144">On the **Configuration Servers** page in Azure, select to add a new process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. <span data-ttu-id="b8ce2-145">指定處程序伺服器名稱，以及要以系統管理員身分連接到虛擬機器的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-145">Specify a process server name, and a name and password to connect to the virtual machine as an administrator.</span></span> <span data-ttu-id="b8ce2-146">選取您要向其註冊處理序伺服器的組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-146">Select the configuration server to which you want to register the process server.</span></span> <span data-ttu-id="b8ce2-147">這應該是您用來保護並容錯移轉虛擬機器的同一部相伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-147">This should be the same server you're using to protect and fail over your virtual machines.</span></span>
3. <span data-ttu-id="b8ce2-148">指定應在其中部署處理序伺服器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-148">Specify the Azure network in which the process server should be deployed.</span></span> <span data-ttu-id="b8ce2-149">它應該是與組態伺服器相同的網路。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-149">It should be the same network as the configuration server.</span></span> <span data-ttu-id="b8ce2-150">指定唯一的 IP 位址選取的子網路並開始部署。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-150">Specify a unique IP address selected subnet and begin deployment.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. <span data-ttu-id="b8ce2-151">已觸發作業部署處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-151">A job is triggered to deploy the process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. <span data-ttu-id="b8ce2-152">在 Azure 中部署處理序伺服器之後，您就能使用指定的認證來登入該伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-152">After the process server is deployed in Azure you can log into the server using the credentials you specified.</span></span> <span data-ttu-id="b8ce2-153">以您註冊內部部署處理序伺服器的相同方式註冊此處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-153">Register the process server in the same way you registered the on-premises process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> <span data-ttu-id="b8ce2-154">在容錯回復期間註冊的伺服器將不會顯示於 Site Recovery 中的 VM 屬性下方。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-154">The servers registered during failback won't be visible under VM properties in Site Recovery.</span></span> <span data-ttu-id="b8ce2-155">它們將會只顯示於它們已註冊之組態伺服器的 [伺服器]  索引標籤下方。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-155">They are only visible under the **Servers** tab of the configuration server to which they're registered.</span></span> <span data-ttu-id="b8ce2-156">可能需要大約 10-15 分鐘，直到處理序伺服器出現在索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-156">It can take about 10-15 minutes until they the process server appears on the tab.</span></span>
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a><span data-ttu-id="b8ce2-157">步驟 3：安裝主要目標伺服器內部部署</span><span class="sxs-lookup"><span data-stu-id="b8ce2-157">Step 3: Install a master target server on-premises</span></span>
<span data-ttu-id="b8ce2-158">根據您的來源虛擬機器作業系統而定，您可能需要安裝 Linux 或 Windows 主要目標伺服器內部部署。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-158">Depending on your source virtual machines operating system, you need to install a Linux or a Windows master target server on-premises.</span></span>

### <a name="deploy-a-windows-master-target-server"></a><span data-ttu-id="b8ce2-159">部署 Windows 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-159">Deploy a Windows master target server</span></span>
<span data-ttu-id="b8ce2-160">Windows 主要目標已經隨附於 vContinuum 安裝程式中。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-160">A Windows master target is already bundled with vContinuum setup.</span></span> <span data-ttu-id="b8ce2-161">當您安裝 vContinuum 時，主要伺服器也會部署於同一部機器上，並向組態伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-161">When you install the vContinuum, a master server is also deployed on the same machine and registered to the configuration server.</span></span>

1. <span data-ttu-id="b8ce2-162">若要開始部署，請在 ESX 主機上建立空的機器內部部署，該主機是您想要從 Auzre 將 VM 復原到其中的主機。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-162">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span></span>
2. <span data-ttu-id="b8ce2-163">確定至少已將兩個磁碟連接到 VM - 一個用於作業系統，另一個則用於保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-163">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span></span>
3. <span data-ttu-id="b8ce2-164">安裝作業系統。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-164">Install the operating system.</span></span>
4. <span data-ttu-id="b8ce2-165">在伺服器上安裝 vContinuum。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-165">Install the vContinuum on the server.</span></span> <span data-ttu-id="b8ce2-166">這也會完成主要目標伺服器的安裝。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-166">This also completes installation of the master target server.</span></span>

### <a name="deploy-a-linux-master-target-server"></a><span data-ttu-id="b8ce2-167">部署 Linux 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-167">Deploy a Linux master target server</span></span>
1. <span data-ttu-id="b8ce2-168">若要開始部署，請在 ESX 主機上建立空的機器內部部署，該主機是您想要從 Auzre 將 VM 復原到其中的主機。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-168">To begin deployment, create an empty machine on-premises on the ESX host onto which you want to recover the VMs from Azure.</span></span>
2. <span data-ttu-id="b8ce2-169">確定至少已將兩個磁碟連接到 VM - 一個用於作業系統，另一個則用於保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-169">Ensure that there are at least two disks attached to the VM – one is used for the operating system and the other is used for the retention drive.</span></span>
3. <span data-ttu-id="b8ce2-170">安裝 Linux 作業系統。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-170">Install the Linux operating system.</span></span> <span data-ttu-id="b8ce2-171">Linux 主要目標系統不應針對根或保留儲存空間使用 LVM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-171">The Linux master target system should not use LVM for root or retention storage spaces.</span></span> <span data-ttu-id="b8ce2-172">預設會設定 Linux 主要伺服器，以避免 LVM 磁碟分割/磁碟探索。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-172">A Linux master target server is configured to avoid LVM partitions/disks discovery by default.</span></span>
4. <span data-ttu-id="b8ce2-173">您可以建立的磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="b8ce2-173">Partitions that you can create:</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. <span data-ttu-id="b8ce2-174">開始安裝主要伺服器之前，請執行下列的安裝前步驟。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-174">Carry out the below post installation steps before beginning the master target installation.</span></span>

#### <a name="post-os-installation-steps"></a><span data-ttu-id="b8ce2-175">作業系統的安裝前步驟</span><span class="sxs-lookup"><span data-stu-id="b8ce2-175">Post OS Installation Steps</span></span>
<span data-ttu-id="b8ce2-176">若要取得 Linux 虛擬機器中每個 SCSI 硬碟的 SCSI 識別碼，請啟用參數 “disk.EnableUUID = TRUE”，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b8ce2-176">To get the SCSI ID’s for each of SCSI hard disk in a Linux virtual machine, enable the parameter “disk.EnableUUID = TRUE” as follows:</span></span>

1. <span data-ttu-id="b8ce2-177">關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-177">Shut down your virtual machine.</span></span>
2. <span data-ttu-id="b8ce2-178">以滑鼠右鍵按一下左面板中的 VM 項目 > [編輯設定]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-178">Right-click the VM entry in the left-hand panel > **Edit Settings**.</span></span>
3. <span data-ttu-id="b8ce2-179">按一下 [選項]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-179">Click the **Options** tab.</span></span> <span data-ttu-id="b8ce2-180">選取 [進階]\> [一般項目]  >  [組態參數]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-180">Select **Advanced\>General item** > **Configuration Parameters**.</span></span> <span data-ttu-id="b8ce2-181">[組態參數]  選項只有在機器關機時才可以使用。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-181">The **Configuration Parameters** option is only available when the machine is shut down.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. <span data-ttu-id="b8ce2-182">查看含有 **disk.EnableUUID** 的資料列是否已經存在？</span><span class="sxs-lookup"><span data-stu-id="b8ce2-182">Checks whether a row with **disk.EnableUUID** exists.</span></span> <span data-ttu-id="b8ce2-183">如果存在且已設定為 **False**，請將它設定為 **True** (不區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-183">If it does and is set to **False** then set it to **True** (not case sensitive).</span></span> <span data-ttu-id="b8ce2-184">如果存在且已設為 True，可按一下 [取消]  ，然後在其開機之後，於客體作業系統內部測試 SCSI 命令。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-184">If exists and is set to true, click **Cancel** and test the SCSI command inside the guest operating system after it's booted up.</span></span> <span data-ttu-id="b8ce2-185">如果不存在，請按一下 [加入資料列] 。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-185">If doesn't exist click **Add Row**.</span></span>
5. <span data-ttu-id="b8ce2-186">在 [名稱]  欄中加入 disk.EnableUUID。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-186">Add disk.EnableUUID in the **Name** column.</span></span> <span data-ttu-id="b8ce2-187">將其值儲存為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-187">Set its value as TRUE.</span></span> <span data-ttu-id="b8ce2-188">請勿為上述值加上雙引號。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-188">Don't add the above values along with double-quotes.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-the-additional-packages"></a><span data-ttu-id="b8ce2-189">下載並安裝其他封裝</span><span class="sxs-lookup"><span data-stu-id="b8ce2-189">Download and install the additional packages</span></span>
<span data-ttu-id="b8ce2-190">注意：請先確定系統具有網際網路連線，然後再下載並安裝其他封裝。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-190">NOTE: Make sure the system has internet connectivity before downloading and installing the additional packages.</span></span>

<span data-ttu-id="b8ce2-191">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span><span class="sxs-lookup"><span data-stu-id="b8ce2-191">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span></span>

<span data-ttu-id="b8ce2-192">此命令會從 CentOS 6.6 儲存機制下載這 15 個封裝，並加以安裝：</span><span class="sxs-lookup"><span data-stu-id="b8ce2-192">This command downloads these 15 packages from CentOS 6.6 repository and installs them:</span></span>

<span data-ttu-id="b8ce2-193">bc-1.06.95-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-193">bc-1.06.95-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-194">busybox-1.15.1-20.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-194">busybox-1.15.1-20.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-195">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-195">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-196">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-196">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-197">lsscsi-0.23-2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-197">lsscsi-0.23-2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-198">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-198">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-199">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-199">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-200">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-200">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-201">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-201">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-202">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-202">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-203">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-203">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-204">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-204">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-205">rsync-3.0.6-12.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-205">rsync-3.0.6-12.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-206">snappy-1.1.0-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-206">snappy-1.1.0-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-207">wget-1.12-5.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-207">wget-1.12-5.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-208">如果來源機器會針對根目錄或開機裝置使用 Reiser 或 XFS 檔案系統，則應該下載並安裝下列套件於 Linux 主要目標上，才能提供保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-208">If the source machine uses Reiser or XFS filesystem for the root or boot device, then following packages should be downloaded and installed on Linux master target prior to protection.</span></span>

<span data-ttu-id="b8ce2-209">\# cd /usr/local</span><span class="sxs-lookup"><span data-stu-id="b8ce2-209">\# cd /usr/local</span></span>

<span data-ttu-id="b8ce2-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="b8ce2-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="b8ce2-211">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="b8ce2-211">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="b8ce2-212">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-212">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span></span>

<span data-ttu-id="b8ce2-213">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="b8ce2-213">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span></span>

<span data-ttu-id="b8ce2-214">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="b8ce2-214">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span></span>

#### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="b8ce2-215">套用自訂組態變更</span><span class="sxs-lookup"><span data-stu-id="b8ce2-215">Apply custom configuration changes</span></span>
<span data-ttu-id="b8ce2-216">套用這些變更之前，請確定您已完成上一節，然後請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b8ce2-216">Before applying these changes make sure you've completed the previous section, then follow these steps:</span></span>

1. <span data-ttu-id="b8ce2-217">將 RHEL 6-64 整合代理程式二進位檔複製到新建立的作業系統。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-217">Copy the RHEL 6-64 Unified Agent binary to the newly created OS.</span></span>
2. <span data-ttu-id="b8ce2-218">執行此命令來將二進位檔解壓縮：**tar -zxvf \<檔案名稱\>**</span><span class="sxs-lookup"><span data-stu-id="b8ce2-218">Run this command to untar the binary: **tar -zxvf \<File name\>**</span></span>
3. <span data-ttu-id="b8ce2-219">執行此命令來授與權限：\# **chmod 755 ./ApplyCustomChanges.sh**</span><span class="sxs-lookup"><span data-stu-id="b8ce2-219">Run this command to give permissions: \# **chmod 755 ./ApplyCustomChanges.sh**</span></span>
4. <span data-ttu-id="b8ce2-220">執行指令碼：**\# ./ApplyCustomChanges.sh**。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-220">Run the script: **\# ./ApplyCustomChanges.sh**.</span></span> <span data-ttu-id="b8ce2-221">只需在伺服器上執行指令碼一次。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-221">Run the script only once on the server.</span></span> <span data-ttu-id="b8ce2-222">指令碼執行後，請重新啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-222">Restart the server after the script runs.</span></span>

### <a name="install-the-linux-server"></a><span data-ttu-id="b8ce2-223">安裝 Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-223">Install the Linux server</span></span>
1. <span data-ttu-id="b8ce2-224">[下載](http://go.microsoft.com/fwlink/?LinkID=529757) 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-224">[Download](http://go.microsoft.com/fwlink/?LinkID=529757) the installation file.</span></span>
2. <span data-ttu-id="b8ce2-225">使用您選擇的 sftp 用戶端公用程式，將檔案複製到 Linux 主要目標虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-225">Copy the file to the Linux Master Target virtual machine using an sftp client utility of your choice.</span></span> <span data-ttu-id="b8ce2-226">或者，您可以登入 Linux 主要目標虛擬機器，並使用 wget 從提供的連結下載安裝套件</span><span class="sxs-lookup"><span data-stu-id="b8ce2-226">Alternately you can log onto the Linux master target virtual machine and use wget to download the installation package from the provided link</span></span>
3. <span data-ttu-id="b8ce2-227">使用您選擇的 ssh 用戶端，登入 Linux 主要目標伺服器虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-227">Log onto the Linux master target server virtual machine using an ssh client of your choice</span></span>
4. <span data-ttu-id="b8ce2-228">如果您已連接到 Azure 網路 (您已在其上透過 VPN 連線部署 Linux 主要目標伺服器)，則可使用您在虛擬機器 [儀表板]  索引標籤中發現之伺服器的內部 IP 位址，以及使用連接埠 22 來連接到使用安全殼層的 Linux 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-228">If you're connected to the Azure network on which you deployed your Linux master target server through a VPN connection then use the internal IP address for the server that you can find in the virtual machine **Dashboard** tab, and port 22 to connect to the Linux master target Server using Secure Shell.</span></span>
5. <span data-ttu-id="b8ce2-229">如果您透過公用網際網路連線連接到 Linux 主要目標伺服器，則可使用 Linux 主要目標伺服器的公用虛擬 IP 位址 (從虛擬機器 [儀表板]  索引標籤)，以及針對 ssh 建立的公用端點來登入 Linux 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-229">If you're connecting to the Linux master target server over a public internet connection use the Linux master target server’s public virtual IP address (from the virtual machines **Dashboard** tab) and the public endpoint created for ssh to login to the Linux servder.</span></span>
6. <span data-ttu-id="b8ce2-230">藉由從包含安裝程式檔案的目錄執行：*“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”*，來從 gzipped Linux 主要目標伺服器安裝程式 tar 封存檔解壓縮檔案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-230">Extract the files from the gzipped Linux master target Server installer tar archive by running: *“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”* from the directory that contains the installer file.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. <span data-ttu-id="b8ce2-231">如果您將安裝程式檔案解壓縮到不同的目錄，請變更為要解壓縮 tar 封存內容的目錄。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-231">If you extracted the installer files to a different directory change to the directory to which the contents of the tar archive were extracted.</span></span> <span data-ttu-id="b8ce2-232">從這個目錄路徑執行 “sudo ./install.sh”。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-232">From this directory path run “sudo ./install.sh”.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. <span data-ttu-id="b8ce2-233">當系統提示您選擇主要角色時，選取 [2 (主要目標)] 。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-233">When prompted to choose a primary role select **2 (Master Target)**.</span></span> <span data-ttu-id="b8ce2-234">保留其他互動式安裝選項的預設值。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-234">Leave the other interactive install options at their default values.</span></span>
9. <span data-ttu-id="b8ce2-235">請等待安裝繼續進行以及主機組態介面出現。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-235">Wait for installation to continue and the Host Config Interface to appear.</span></span> <span data-ttu-id="b8ce2-236">適用於 Linux 主要目標伺服器的主機組態公用程式是一個命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-236">The Host Configuration utility for the Linux master sarget Server is a command line utility.</span></span> <span data-ttu-id="b8ce2-237">請勿調整 ssh 用戶端公用程式視窗的大小。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-237">Don’t resize the ssh client utility window.</span></span> <span data-ttu-id="b8ce2-238">使用方向鍵來選取 [全域]  選項，然後按鍵盤上的 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-238">Use the arrow keys to select the **Global** option and press ENTER on your keyboard.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. <span data-ttu-id="b8ce2-239">在 [IP] 欄位中，輸入組態伺服器的內部 IP 位址 (您可以在組態伺服器 VM 的 [儀表板] 索引標籤中找到它) 然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-239">In the field **IP** enter the Internal IP address of the configuration server (you can find it in the **Dashboard** tab of the configuration server VM) and press ENTER.</span></span> <span data-ttu-id="b8ce2-240">在 [連接埠] 中，輸入 **22**，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-240">In **Port** enter **22** and press ENTER.</span></span>
11. <span data-ttu-id="b8ce2-241">保留 [使用 HTTPS] 為 [是]，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-241">Leave **Use HTTPS** as **Yes**, and press ENTER.</span></span>
12. <span data-ttu-id="b8ce2-242">輸入組態伺服器上產生的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-242">Enter the Passphrase that was generated on the configuration server.</span></span> <span data-ttu-id="b8ce2-243">如果您從 Windows 機器使用 PUTTY 用戶端 ssh 到 Linux 虛擬機器，您可以使用 Shift+Insert 鍵來貼上剪貼簿的內容。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-243">If you're using a PUTTY client from a Windows machine to ssh to the Linux virtual machine you can use Shift+Insert to paste the contents of the clipboard.</span></span> <span data-ttu-id="b8ce2-244">使用 Ctrl+C 鍵，將複雜密碼複製到本機剪貼簿，然後使用 Shift+Insert 鍵來貼上它。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-244">Copy the Passphrase to the local clipboard using Ctrl-C and use Shift+Insert to paste it.</span></span> <span data-ttu-id="b8ce2-245">按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-245">Press ENTER.</span></span>
13. <span data-ttu-id="b8ce2-246">使用向右鍵瀏覽到結束並按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-246">Use the right arrow key to navigate to quit and press ENTER.</span></span> <span data-ttu-id="b8ce2-247">等待安裝完成。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-247">Wait for installation to complete.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

<span data-ttu-id="b8ce2-248">如果您基於某些原因而無法向 Linux 主要目標伺服器註冊您的組態伺服器，則您應該從 /usr/local/ASR/Vx/bin/hostconfigcli 執行主機組態公用程式，再次執行這個動作 (您必須先以進階使用者身分執行 chmod，來設定此目錄的存取權限)。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-248">If for some reason you failed to register your Linux master target server to the configuration server you can do so again by running the host configuration utility from /usr/local/ASR/Vx/bin/hostconfigcli (you'll first need to set access permissions to this directory by running chmod as a super user).</span></span>

#### <a name="validate-master-target-registration"></a><span data-ttu-id="b8ce2-249">驗證主要目標註冊</span><span class="sxs-lookup"><span data-stu-id="b8ce2-249">Validate master target registration</span></span>
<span data-ttu-id="b8ce2-250">您可以驗證主要目標伺服器已成功向 Azure Site Recovery 保存庫 > [組態伺服器]  >  [伺服器詳細資料] 中的組態伺服器註冊。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-250">You can validate that the master target server was registered successfully to the configuration server in Azure Site Recovery vault > **Configuration Server** > **Server Details**.</span></span>

> [!NOTE]
> <span data-ttu-id="b8ce2-251">在註冊主要目標伺服器之後，如果您收到虛擬機器可能已從 Azure 刪除，或未正確設定端點等錯誤，這是因為在 Azure 中部署主要目標時，雖然 Azure 端點偵測到主要目標組態，但是內部部署主要目標伺服器內部部署卻不是這個情形。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-251">After registering the master target server, if you receive configuration errors that the virtual machine might have been deleted from Azure or that endpoints are not properly configured, this is because although the master target configuration is detected by the Azure dndpoints when the master target is deployed in Azure, this isn't true for an on-premises master target server on-premises.</span></span> <span data-ttu-id="b8ce2-252">這並不會影響容錯回復，您可以忽略這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-252">This won't affect failback and you can ignore these errors.</span></span>
>
>

## <a name="step-4-protect-the-virtual-machines-to-the-on-premises-site"></a><span data-ttu-id="b8ce2-253">步驟 4：保護虛擬機器至內部部署網站</span><span class="sxs-lookup"><span data-stu-id="b8ce2-253">Step 4: Protect the virtual machines to the on-premises site</span></span>
<span data-ttu-id="b8ce2-254">您要保護 VM 至內部部署網站，然後再容錯回復。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-254">You need to protect VMs to the on-premises site before you fail back.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="b8ce2-255">開始之前</span><span class="sxs-lookup"><span data-stu-id="b8ce2-255">Before you begin</span></span>
<span data-ttu-id="b8ce2-256">將 VM 容錯移轉到 Azure 時，它會新增額外的暫存磁碟機以供分頁檔使用。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-256">When a VM is failed over to Azure, it adds an extra temp drive for page file.</span></span> <span data-ttu-id="b8ce2-257">這通常是您已容錯移轉的 VM 不需要的額外磁碟機，因為它可能已經有分頁檔專用的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-257">This is an extra drive that is typically not required by your failed over VM since it might already have a drive dedicated for the page file.</span></span> <span data-ttu-id="b8ce2-258">在開始反向保護虛擬機器之前，您需要確定磁碟機已離線，使它不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-258">Before you begin reverse protection of the virtual machines, you need to ensure that this drive is taken offline so that it does not get protected.</span></span> <span data-ttu-id="b8ce2-259">以下列方式來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="b8ce2-259">Do this as follows:</span></span>

1. <span data-ttu-id="b8ce2-260">開啟 [電腦管理] 並選取 [儲存管理]，即會列出磁碟已上線且已連接到機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-260">Open Computer Management and select Storage Management so that it lists the disks online and attached to the machine.</span></span>
2. <span data-ttu-id="b8ce2-261">選取連接到機器的暫存磁碟，並選擇使其離線。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-261">Select the temporary disk attached to the machine and choose to bring it offline.</span></span>

### <a name="protect-the-vms"></a><span data-ttu-id="b8ce2-262">保護 VM</span><span class="sxs-lookup"><span data-stu-id="b8ce2-262">Protect the VMs</span></span>
1. <span data-ttu-id="b8ce2-263">在 Azure 入口網站中，查看虛擬機器的狀態，並確定它們已容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-263">In the Azure portal, check the states of the virtual machine to ensure that they're failed over.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. <span data-ttu-id="b8ce2-264">啟動機器上的 vContinuum。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-264">Launch vContinuum on your machine.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. <span data-ttu-id="b8ce2-265">按一下 [新增保護]  並選取作業系統類型，這個</span><span class="sxs-lookup"><span data-stu-id="b8ce2-265">Click **New Protection** and select the operation system type, the</span></span>
4. <span data-ttu-id="b8ce2-266">在開啟的新視窗中，選取 [OS 類型]  >  [取得詳細資料] 以取得您想要容錯回復的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-266">In the new window that open select the **OS type** > **Get Details** for the VMs you want to fail back.</span></span> <span data-ttu-id="b8ce2-267">在 [主要伺服器詳細資料] 中，識別並選取您想要保護的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-267">In **Primary server details**, identify and select the virtual machines that you want to protect.</span></span> <span data-ttu-id="b8ce2-268">在容錯移轉之前，VM 會列在其隸屬的主機名稱之下。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-268">VMs are listed under the vCenter host name that they were on before failover.</span></span>
5. <span data-ttu-id="b8ce2-269">當您選取要保護的虛擬機器 (而且已經將它容錯移轉到 Azure) 時，快顯視窗會提供兩個適用於虛擬機器的項目。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-269">When you select a virtual machine to protect (and it has already failed over to Azure) a pop-up window provides two entries for the virtual machine.</span></span> <span data-ttu-id="b8ce2-270">這是因為組態伺服器偵測到兩個已向其註冊的虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-270">This is because the configuration server detects two instances of the virtual machines registered to it.</span></span> <span data-ttu-id="b8ce2-271">您需要移除內部部署 VM 的項目，如此就能保護正確的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-271">You need to remove the entry for the on-premises VM so that you can protect the correct VM.</span></span> <span data-ttu-id="b8ce2-272">若要在此處識別正確的 Azure VM 項目，您可以登入 Azure VM，然後移至 C:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc。在 drscout.conf 檔案中，識別主機識別碼。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-272">To identify the correct Azure VM entry here, you can log into the Azure VM and go to C:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc. In the file drscout.conf , identify the host ID.</span></span> <span data-ttu-id="b8ce2-273">在 vContinuum 對話方塊中，保留可在 VM 上找到主機識別碼的項目。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-273">In the vContinuum dialog, keep the entry for which you found the host ID on  the VM.</span></span> <span data-ttu-id="b8ce2-274">刪除所有其他項目。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-274">Delete all other entries.</span></span> <span data-ttu-id="b8ce2-275">若要選取正確的 VM，您可以參考其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-275">To select the correct VM you can refer to its IP address.</span></span> <span data-ttu-id="b8ce2-276">IP 位址範圍內部部署將會在內部部署 VM 上。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-276">The IP address range on-premises will be the on-premises VM.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. <span data-ttu-id="b8ce2-277">在 vCenter 伺服器上，停止虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-277">On the vCenter server stop the virtual machine.</span></span> <span data-ttu-id="b8ce2-278">您也可以刪除 VM 內部部署。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-278">You can also delete the VMs on-premises.</span></span>
7. <span data-ttu-id="b8ce2-279">接下來，指定您要保護 VM 的內部部署 MT 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-279">Then specify the on-premises MT server to which you want to protect the VMs.</span></span> <span data-ttu-id="b8ce2-280">若要這樣做，請連接到您想要容錯回復的目標 vCenter 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-280">To do this, connect to the vCenter server to which you want to fail back.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. <span data-ttu-id="b8ce2-281">根據您要復原 VM 的目標主機來選取主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-281">Select the master target server based on the host to which you want to recover the VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. <span data-ttu-id="b8ce2-282">提供每個虛擬機器的複寫選項。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-282">Provide the replication option for each of the virtual machines.</span></span> <span data-ttu-id="b8ce2-283">若要這樣做，您需要選取要將 VM 還原到其中的復原端資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-283">To do this you need to select the recovery side datastore to which the VMs will be recovered.</span></span> <span data-ttu-id="b8ce2-284">下表摘要說明您必須提供給每個 VM 的不同選項。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-284">The table summarizes the different options you need to provide for each VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | <span data-ttu-id="b8ce2-285">**選項**</span><span class="sxs-lookup"><span data-stu-id="b8ce2-285">**Option**</span></span> | <span data-ttu-id="b8ce2-286">**選項建議值**</span><span class="sxs-lookup"><span data-stu-id="b8ce2-286">**Option recommended value**</span></span> |
   | --- | --- |
   |  <span data-ttu-id="b8ce2-287">處理序伺服器 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b8ce2-287">Process server IP address</span></span> |<span data-ttu-id="b8ce2-288">選取部署在 Azure 中的處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-288">Select the process server deployed in Azure</span></span> |
   |  <span data-ttu-id="b8ce2-289">保留大小 (以 MB 為單位)</span><span class="sxs-lookup"><span data-stu-id="b8ce2-289">Retention size in MB</span></span> | |
   |  <span data-ttu-id="b8ce2-290">保留值</span><span class="sxs-lookup"><span data-stu-id="b8ce2-290">Retention value</span></span> |<span data-ttu-id="b8ce2-291">1</span><span class="sxs-lookup"><span data-stu-id="b8ce2-291">1</span></span> |
   |  <span data-ttu-id="b8ce2-292">天/小時</span><span class="sxs-lookup"><span data-stu-id="b8ce2-292">Days/Hours</span></span> |<span data-ttu-id="b8ce2-293">星期幾</span><span class="sxs-lookup"><span data-stu-id="b8ce2-293">Days</span></span> |
   |  <span data-ttu-id="b8ce2-294">一致性間隔</span><span class="sxs-lookup"><span data-stu-id="b8ce2-294">Consistency interval</span></span> |<span data-ttu-id="b8ce2-295">1</span><span class="sxs-lookup"><span data-stu-id="b8ce2-295">1</span></span> |
   |  <span data-ttu-id="b8ce2-296">選取目標資料存放區</span><span class="sxs-lookup"><span data-stu-id="b8ce2-296">Select target datastore</span></span> |<span data-ttu-id="b8ce2-297">可在復原端使用的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-297">The datastore available on the recovery site.</span></span> <span data-ttu-id="b8ce2-298">這個資料存放區應具備足夠空間，而且可供您要在其上還原虛擬機器的 ESX 主機使用。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-298">The data store should have enough space, and be available to the ESX host on which you want to restore the virtual machine.</span></span> |
10. <span data-ttu-id="b8ce2-299">設定虛擬機器將在容錯移轉到內部部署站台之後取得的屬性。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-299">Configure the properties that the virtual machine will acquire after failover to on-premises site.</span></span> <span data-ttu-id="b8ce2-300">下表中會摘要說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-300">The properties are summarized in the following table.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | <span data-ttu-id="b8ce2-301">**屬性**</span><span class="sxs-lookup"><span data-stu-id="b8ce2-301">**Property**</span></span> | <span data-ttu-id="b8ce2-302">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="b8ce2-302">**Details**</span></span> |
    | --- | --- |
    | <span data-ttu-id="b8ce2-303">網路組態</span><span class="sxs-lookup"><span data-stu-id="b8ce2-303">Network configuration</span></span> |<span data-ttu-id="b8ce2-304">針對偵測到的每個網路介面卡，請選取它，然後按一下 [變更]  來設定虛擬機器的容錯回復 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-304">For each network adapter detected, select it and click **Change** to configure the failback IP address for the virtual machine.</span></span> |
    | <span data-ttu-id="b8ce2-305">硬體組態</span><span class="sxs-lookup"><span data-stu-id="b8ce2-305">Hardware Configuration</span></span> |<span data-ttu-id="b8ce2-306">指定 VM 的 CPU 和記憶體。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-306">Specify the CPU and the memory for the VM.</span></span> <span data-ttu-id="b8ce2-307">這些設定可套用到您嘗試保護的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-307">Settings can be applied to all the VMs you are trying to protect.</span></span> <span data-ttu-id="b8ce2-308">若要識別 CPU 和記憶體的正確值，您可以參考 IAAS VM 角色大小，並查看核心數及指派的記憶體。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-308">To identify the correct values for the CPU and memory, you can refer to the IAAS VMs role size and see the number of cores and memory assigned.</span></span> |
    | <span data-ttu-id="b8ce2-309">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="b8ce2-309">Display name</span></span> |<span data-ttu-id="b8ce2-310">容錯回復到內部部署之後，您可以在虛擬機器出現在 vCenter 詳細目錄中時將其重新命名。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-310">After failback to on-premises, you can rename the virtual machines as they'll appear in the vCenter inventory.</span></span> <span data-ttu-id="b8ce2-311">預設名稱是虛擬機器的電腦主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-311">The default name is the virtual machine computer host name.</span></span> <span data-ttu-id="b8ce2-312">若要識別 VM 名稱，您可以參考保護群組中的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-312">To identify the VM name, you can refer to the VM list in the Protection group.</span></span> |
    | <span data-ttu-id="b8ce2-313">NAT 組態</span><span class="sxs-lookup"><span data-stu-id="b8ce2-313">NAT Configuration</span></span> |<span data-ttu-id="b8ce2-314">以下將詳細討論</span><span class="sxs-lookup"><span data-stu-id="b8ce2-314">Discussed in detail below</span></span> |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a><span data-ttu-id="b8ce2-315">設定 NAT 原則</span><span class="sxs-lookup"><span data-stu-id="b8ce2-315">Configure NAT settings</span></span>
1. <span data-ttu-id="b8ce2-316">若要啟用虛擬機器的保護，需要建立兩個通訊通道。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-316">To enable protection of the virtual machines, two communication channels need to be established.</span></span> <span data-ttu-id="b8ce2-317">第一個通道位於虛擬機器和處理序伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-317">The first channel is between the virtual machine and the process server.</span></span> <span data-ttu-id="b8ce2-318">此通道會從 VM 收集資料，並將其傳送至處理序伺服器，該伺服器會再將資料傳送給主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-318">This channel collects the data from the VM and sends it to the process server which then sends the data to the master target server.</span></span> <span data-ttu-id="b8ce2-319">如果處理序伺服器和受保護的虛擬機器位於相同的 Azure 虛擬網路上，則您不需使用 NAT 設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-319">If the process server and the virtual machine to be protected are on the same Azure virtual network then you don't need to use NAT settings.</span></span> <span data-ttu-id="b8ce2-320">否則，請指定 NAT 設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-320">Otherwise specify NAT settings.</span></span> <span data-ttu-id="b8ce2-321">在 Azure 中檢視處理序伺服器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-321">View the public IP address of the process server in Azure.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. <span data-ttu-id="b8ce2-322">第二個通道介於處理序伺服器和主要目標伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-322">The second channel is between the process server and the master target server.</span></span> <span data-ttu-id="b8ce2-323">是否使用 NAT 的選項取決於您是使用以連線為基礎的 VPN，還是透過網際網路通訊。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-323">The option to use NAT or not depends on whether you are using a VPN based connection or communicating over the internet.</span></span> <span data-ttu-id="b8ce2-324">如果您使用 VPN，請不要選取 NAt，只有當您使用網際網路連線時才選取。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-324">Don't select NAt if you're using VPN, but only if you're using an internet connection.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. <span data-ttu-id="b8ce2-325">如果您尚未刪除指定的內部部署虛擬機器，而且如果您要容錯回復的目標資料存放區仍包含舊的 VMDK，則您必須確定容錯回復的 VM 會建立於新的位置上。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-325">If you haven't deleted the on-premises virtual machines as specified and if the datastore you are failing back to still contains the old VMDK’s then you will need to ensure that the failback VM gets created in a new place.</span></span> <span data-ttu-id="b8ce2-326">若要這樣做，請選取 [進階] 設定，並且在 [資料夾名稱設定] 中指定要還原到其中的替代資料夾。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-326">To do this select the **Advanced** settings and specify an alternate Folder to restore to in **Folder Name Settings**.</span></span> <span data-ttu-id="b8ce2-327">保留其他選項的預設設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-327">Leave the other options with their default settings.</span></span> <span data-ttu-id="b8ce2-328">將資料夾名稱設定套用到所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-328">Apply the folder name settings to all the servers.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. <span data-ttu-id="b8ce2-329">執行整備檢查，以確保虛擬機器已準備好回復到內部部署接受保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-329">Run a Readiness Check to ensure that the virtual machines are ready to be protected back to on-premises.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. <span data-ttu-id="b8ce2-330">等候它完成。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-330">Wait for it to complete.</span></span> <span data-ttu-id="b8ce2-331">如果已順利位於所有 VM 上，您可以指定保護方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-331">If it's successfully on all VMs you can specify a name for the protection plan.</span></span> <span data-ttu-id="b8ce2-332">然後按一下 [保護]  以開始進行。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-332">Then click **Protect** to begin.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. <span data-ttu-id="b8ce2-333">您可以在 vContinuum 中監視進度。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-333">You can monitor progress in vContinuum.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. <span data-ttu-id="b8ce2-334">在 [啟用保護計劃]  步驟完成之後，您可以監視 Site Recovery 入口網站中的 VM 保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-334">After the step **Activating Protection Plan** finishes you can monitor VM protection in the Site Recovery portal.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. <span data-ttu-id="b8ce2-335">您可以按一下 VM 並監視其進度以查看確切狀態。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-335">You can see the exact status clicking on the VM and monitoring its progress.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-the-failback-plan"></a><span data-ttu-id="b8ce2-336">準備容錯回復方案</span><span class="sxs-lookup"><span data-stu-id="b8ce2-336">Prepare the failback plan</span></span>
<span data-ttu-id="b8ce2-337">您可以使用 vContinuum 來準備容錯回復方案，讓應用程式隨時都能容錯回復到內部部署網站。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-337">You can prepare a failback plan using vContinuum so that the application can be failed back to the on-premises site at any time.</span></span> <span data-ttu-id="b8ce2-338">這些復原方案非常類似 Site Recovery 中的復原方案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-338">These recovery plans are very similar to the recovery plans in Site Recovery.</span></span>

1. <span data-ttu-id="b8ce2-339">啟動 vContinuum，然後選取 [管理方案]  >  [復原]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-339">Launch vContinuum and select **Manage plans** > **Recover.**</span></span> <span data-ttu-id="b8ce2-340">您可以看到所有已用來容錯移轉 VM 的方案清單。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-340">You can see of list of all the plans that have been used to fail over VMs.</span></span> <span data-ttu-id="b8ce2-341">您可以使用相同的方案來復原。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-341">You can use the same plans to recover.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. <span data-ttu-id="b8ce2-342">選取保護方案，以及您想要在其中復原的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-342">Select the protection plan and all of the VMs you want to recover in it.</span></span> <span data-ttu-id="b8ce2-343">當您選取每個 VM 時，您可以看到更多詳細資料，包括目標 ESX 伺服器與來源 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-343">When you select each VM you can see more details including the target ESX server and the source VM disk.</span></span> <span data-ttu-id="b8ce2-344">按 [下一步]  以開始 [復原精靈]，然後選取您想要復原的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-344">Click **Next** to begin the Recover Wizard and select the VMs you want to recover.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. <span data-ttu-id="b8ce2-345">您可以根據多個選項進行復原，但建議您使用「最新的標記」，然後選取 [套用所有 VM] 以確保使用虛擬機器的最新資料。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-345">You can recover based on multiple options but we recommend you use **Latest Tag** and select **Apply for All VMs** to ensure that the latest data from the virtual machine will be used.</span></span>
4. <span data-ttu-id="b8ce2-346">執行 [整備檢查]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-346">Run the **Readiness Check.**</span></span> <span data-ttu-id="b8ce2-347">這會檢查是否設為啟用 VM 復原的正確參數。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-347">This will check if the right parameters are configured to enable VM recovery.</span></span> <span data-ttu-id="b8ce2-348">如果所有檢查都成功，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-348">Click **Next** if all the checks are successful.</span></span> <span data-ttu-id="b8ce2-349">如果未成功，請檢查記錄檔並解決錯誤。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-349">If not check the log and resolve the errors.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. <span data-ttu-id="b8ce2-350">在 [VM 組態]  中，確定已正確設定復原設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-350">In **VM Configuration** ensure that the recovery settings are correctly set.</span></span> <span data-ttu-id="b8ce2-351">您可以在必要時變更 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-351">You can change the VM settings if you need to.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. <span data-ttu-id="b8ce2-352">檢閱將復原的虛擬機器清單並指定復原順序。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-352">Review the list of virtual machines that will be recovered and specify a recovery order.</span></span> <span data-ttu-id="b8ce2-353">請注意，VM 會使用電腦主機名稱列出。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-353">Note that VMs are listed using the computer host name.</span></span> <span data-ttu-id="b8ce2-354">可能很難將電腦主機名稱對應到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-354">It might be difficult to map the computer host name to the virtual machine.</span></span>
   <span data-ttu-id="b8ce2-355">若要對應名稱，請移至 Azure 中的虛擬機器 [儀表板]  並檢查 VM 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-355">To map the names, go to the virtual machines **Dashboard** in Azure and check the VM host name.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. <span data-ttu-id="b8ce2-356">指定方案名稱，然後選取 [稍後復原] 。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-356">Specify a plan name and select **Recover later**.</span></span> <span data-ttu-id="b8ce2-357">建議稍後復原，因為初始保護可能不完整。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-357">We recommend to recover later since the initial protection might not be complete.</span></span>
8. <span data-ttu-id="b8ce2-358">如果您選取立即復原而不是稍後復原，請按一下 [復原]  來儲存方案或觸發復原。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-358">Click on **Recover** to save the plan or trigger the recovery if you've selected to recover now and not later.</span></span> <span data-ttu-id="b8ce2-359">您可以檢查復原狀態以查看是否已儲存方案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-359">You can check the recovery status to see if the plan's been saved.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a><span data-ttu-id="b8ce2-360">復原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-360">Recover virtual machines</span></span>
<span data-ttu-id="b8ce2-361">建立方案之後，您可以復原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-361">After the plan's been created, you can recover the virtual machines.</span></span> <span data-ttu-id="b8ce2-362">在您復原之前，請檢查虛擬機器是否已完成同步處理。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-362">Before you do check that the virtual machines have completed synchronization.</span></span> <span data-ttu-id="b8ce2-363">如果複寫狀態顯示正常，則表示保護已完成且已符合 RPO 閾值。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-363">If replication status shows OK then the protection is completed and the RPO threshold has been met.</span></span> <span data-ttu-id="b8ce2-364">您可以確認 VM 屬性中的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-364">You can verify health in the VM properties.</span></span>

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

<span data-ttu-id="b8ce2-365">起始復原之前，請關閉 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-365">Turn off the Azure virtual machines before you initiate the recovery.</span></span> <span data-ttu-id="b8ce2-366">這可確保不會產生核心分裂，而且使用者將只能存取應用程式的複本。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-366">This ensures there's no split brain and that users will only access one copy of the application.</span></span>

1. <span data-ttu-id="b8ce2-367">啟動儲存的方案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-367">Start the saved plan.</span></span> <span data-ttu-id="b8ce2-368">在 vContinuum 中，選取 [監視]  方案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-368">In vContinuum select **Monitor** the plans.</span></span> <span data-ttu-id="b8ce2-369">這樣會列出所有已執行的方案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-369">This lists all the plans that have been run.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. <span data-ttu-id="b8ce2-370">在 [復原] 中選取方案並按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-370">Select the plan in **Recovery** and click **Start**.</span></span> <span data-ttu-id="b8ce2-371">您可以監視復原。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-371">You can monitor recovery.</span></span> <span data-ttu-id="b8ce2-372">開啟 VM 之後，您可以在 vCenter 中與它們連接。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-372">After VMs have been turned on you can connect to them in vCenter.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-to-azure-again-after-failback"></a><span data-ttu-id="b8ce2-373">在容錯回復後重新保護至 Azure</span><span class="sxs-lookup"><span data-stu-id="b8ce2-373">Protect to Azure again after failback</span></span>
<span data-ttu-id="b8ce2-374">完成容錯回復之後，您可能會想要再次保護虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-374">After failback has been completed you'll probably want to protect the virtual machines again.</span></span> <span data-ttu-id="b8ce2-375">以下列方式來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="b8ce2-375">Do this as follows:</span></span>

1. <span data-ttu-id="b8ce2-376">檢查虛擬機器內部部署正在運作，而且應用程式能夠聯繫。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-376">Check that the virtual machines on-premises are working and that applications are reachable.</span></span>
2. <span data-ttu-id="b8ce2-377">在 Azure Site Recovery 入口網站中，選取虛擬機器，並將它們刪除。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-377">In the Azure Site Recovery portal, select the virtual machines and delete them.</span></span> <span data-ttu-id="b8ce2-378">選取停用虛擬機器的保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-378">Select to disable the protection of the virtual machines.</span></span> <span data-ttu-id="b8ce2-379">如此可確保 VM 沒有其他保護。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-379">This ensures that the VMs are no more protected.</span></span>
3. <span data-ttu-id="b8ce2-380">在 Azure 中，刪除已容錯移轉的 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b8ce2-380">In Azure delete the failed over Azure virtual machines</span></span>
4. <span data-ttu-id="b8ce2-381">刪除 vSpehere 上的舊虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-381">Delete the old virtual machine on vSpehere.</span></span> <span data-ttu-id="b8ce2-382">這些是您先前容錯移轉到 Azure 的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-382">These are the VMs that you previously failed over to Azure.</span></span>
5. <span data-ttu-id="b8ce2-383">在 Site Recovery 入口網站中，保護最近容錯移轉的 VM。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-383">In the Site Recovery portal protect the VMs that recently failed over.</span></span> <span data-ttu-id="b8ce2-384">在它們受保護之後，您可以將它們加入復原方案。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-384">After they're protected  you can add them to a recovery plan.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8ce2-385">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8ce2-385">Next steps</span></span>
* <span data-ttu-id="b8ce2-386">[深入了解](site-recovery-vmware-to-azure-classic.md) 使用增強部署，將 VMware 虛擬機器和實體伺服器複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b8ce2-386">[Read about](site-recovery-vmware-to-azure-classic.md) replicating VMware virtual machines and physical servers to Azure using the enhanced deployment.</span></span>
