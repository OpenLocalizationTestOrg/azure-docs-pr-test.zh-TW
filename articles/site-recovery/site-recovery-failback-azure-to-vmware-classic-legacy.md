---
title: "aaaFail hello 傳統舊版入口網站中從 Azure 備份 VMware Vm |Microsoft 文件"
description: "本文說明 toofail 後將 VMware 虛擬機器已複寫 tooAzure 與 Azure Site Recovery 的方式。"
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
ms.openlocfilehash: 5ef66b366dcdc43f3bc171e0ed1532216cc2ab89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fail-back-vmware-virtual-machines-and-physical-servers-from-azure-toovmware-with-azure-site-recovery-legacy"></a><span data-ttu-id="a86bc-103">失敗後的 VMware 虛擬機器和實體伺服器從 Azure tooVMware 與 Azure Site Recovery （舊版）</span><span class="sxs-lookup"><span data-stu-id="a86bc-103">Fail back VMware virtual machines and physical servers from Azure tooVMware with Azure Site Recovery (legacy)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a86bc-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a86bc-104">Azure Portal</span></span>](site-recovery-failback-azure-to-vmware.md)
> * [<span data-ttu-id="a86bc-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a86bc-105">Azure Classic Portal</span></span>](site-recovery-failback-azure-to-vmware-classic.md)
> * [<span data-ttu-id="a86bc-106">Azure 傳統入口網站 (舊版)</span><span class="sxs-lookup"><span data-stu-id="a86bc-106">Azure Classic Portal (Legacy)</span></span>](site-recovery-failback-azure-to-vmware-classic-legacy.md)
>
>

<span data-ttu-id="a86bc-107">本文說明如何 toofail 後 VMware 虛擬機器和 Windows/Linux 實體伺服器，從 Azure tooyour 在內部部署站台之後，您已從您內部部署複寫站台使用 tooAzure [Azure Site Recovery？](site-recovery-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a86bc-107">This article describes how toofail back VMware virtual machines and Windows/Linux physical servers from Azure tooyour on-premises site after you've replicated from your on-premises site tooAzure using [Azure Site Recovery?](site-recovery-overview.md).</span></span>

<span data-ttu-id="a86bc-108">本文說明的是舊版設定，不應用於新的保存庫。</span><span class="sxs-lookup"><span data-stu-id="a86bc-108">This article describes an old configuration and shouldn't be used for new vaults.</span></span>

## <a name="architecture"></a><span data-ttu-id="a86bc-109">架構</span><span class="sxs-lookup"><span data-stu-id="a86bc-109">Architecture</span></span>
<span data-ttu-id="a86bc-110">此圖表顯示 hello 容錯移轉和容錯回復案例。</span><span class="sxs-lookup"><span data-stu-id="a86bc-110">This diagram represents hello failover and failback scenario.</span></span> <span data-ttu-id="a86bc-111">hello 藍色行會 hello 容錯移轉期間使用的連接。</span><span class="sxs-lookup"><span data-stu-id="a86bc-111">hello blue lines are hello connections used during failover.</span></span> <span data-ttu-id="a86bc-112">hello 紅線是 hello 容錯回復期間使用的連接。</span><span class="sxs-lookup"><span data-stu-id="a86bc-112">hello red lines are hello connections used during failback.</span></span> <span data-ttu-id="a86bc-113">有箭頭的 hello 線經過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="a86bc-113">hello lines with arrows go over hello internet.</span></span>

![](./media/site-recovery-failback-azure-to-vmware/vconports.png)

## <a name="before-you-start"></a><span data-ttu-id="a86bc-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="a86bc-114">Before you start</span></span>
* <span data-ttu-id="a86bc-115">您應該已容錯移轉您的 VMware VM 或實體伺服器，且它們應該在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="a86bc-115">You should have failed over your VMware VMs or physical servers and they should be running in Azure.</span></span>
* <span data-ttu-id="a86bc-116">您應該注意，您可以只失敗後的 VMware 虛擬機器和 Azure tooVMware hello 在內部部署主要站台中的虛擬機器從 Windows/Linux 實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-116">You should note that you can only fail back VMware virtual machines and Windows/Linux physical servers from Azure tooVMware virtual machines in hello on-premises primary site.</span></span>  <span data-ttu-id="a86bc-117">如果您正在失敗實體機器，容錯移轉 tooAzure 會將它轉換 tooan Azure VM，並容錯回復 tooVMware 會將它轉換 tooa VMware VM。</span><span class="sxs-lookup"><span data-stu-id="a86bc-117">If you're failing back a physical machine, failover tooAzure will convert it tooan Azure VM, and failback tooVMware will convert it tooa VMware VM.</span></span>

<span data-ttu-id="a86bc-118">設定容錯回復的方式如下︰</span><span class="sxs-lookup"><span data-stu-id="a86bc-118">Here's how you set up failback:</span></span>

1. <span data-ttu-id="a86bc-119">**設定容錯回復元件**： 您將需要 tooset vContinuum 伺服器內部部署，並使之指向 toohello 組態伺服器 VM 在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a86bc-119">**Set up failback components**: You'll need tooset up a vContinuum server on-premises, and point it toohello configuration server VM in Azure.</span></span> <span data-ttu-id="a86bc-120">您也會設定處理序伺服器，為 Azure VM toosend 資料回復 toohello 在內部部署主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-120">You'll also set up a process server as an Azure VM toosend data back toohello on-premises master target server.</span></span> <span data-ttu-id="a86bc-121">透過處理 hello 容錯移轉的 hello 組態伺服器註冊 hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-121">You register hello process server with hello configuration server that  handled hello failover.</span></span> <span data-ttu-id="a86bc-122">您安裝內部部署主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-122">You install an on-premises master target server.</span></span> <span data-ttu-id="a86bc-123">如果您需要 Windows 主要目標伺服器，它會在您安裝 vContinuum 時自動設定。</span><span class="sxs-lookup"><span data-stu-id="a86bc-123">If you need a Windows master target server it's set up automatically when you install vContinuum.</span></span> <span data-ttu-id="a86bc-124">如果您需要 Linux 需要 tooset 它以手動方式在不同的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-124">If you need Linux you'll need tooset it up manually on a separate server.</span></span>
2. <span data-ttu-id="a86bc-125">**啟用保護和容錯回復**： 當您設定 hello 元件之後，在 vContinuum 您將需要 tooenable 保護容錯移轉 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="a86bc-125">**Enable protection and failback**: After you've set up hello components, in vContinuum you'll need tooenable protection for failed over Azure VMs.</span></span> <span data-ttu-id="a86bc-126">將執行整備檢查 hello Vm 上的，並從 Azure tooyour 在內部部署站台執行容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a86bc-126">You'll run a readiness check on hello VMs and run a failover from Azure tooyour on-premises site.</span></span> <span data-ttu-id="a86bc-127">容錯回復完成後您重新保護內部部署機器，讓他們可以啟動複寫 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a86bc-127">After failback finishes you reprotect on-premises machines so that they start replicating tooAzure.</span></span>

## <a name="step-1-install-vcontinuum-on-premises"></a><span data-ttu-id="a86bc-128">步驟 1：安裝 vContinuum 內部部署</span><span class="sxs-lookup"><span data-stu-id="a86bc-128">Step 1: Install vContinuum on-premises</span></span>
<span data-ttu-id="a86bc-129">您將需要 tooinstall vContinuum 伺服器在內部部署，而且它指向 toohello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-129">You'll need tooinstall a vContinuum server on premises and point it toohello configuration server.</span></span>

1. <span data-ttu-id="a86bc-130">[下載 vContinuum](http://go.microsoft.com/fwlink/?linkid=526305)。</span><span class="sxs-lookup"><span data-stu-id="a86bc-130">[Download vContinuum](http://go.microsoft.com/fwlink/?linkid=526305).</span></span>
2. <span data-ttu-id="a86bc-131">然後下載 hello [vContinuum 更新](http://go.microsoft.com/fwlink/?LinkID=533813)版本。</span><span class="sxs-lookup"><span data-stu-id="a86bc-131">Then download hello [vContinuum update](http://go.microsoft.com/fwlink/?LinkID=533813) version.</span></span>
3. <span data-ttu-id="a86bc-132">安裝 vContinuum hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="a86bc-132">Install hello latest version of vContinuum.</span></span> <span data-ttu-id="a86bc-133">在 hello ** 褖畫惎**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-133">On hello **Welcome** page click **Next**.</span></span>
    ![](./media/site-recovery-failback-azure-to-vmware/image2.png)
4. <span data-ttu-id="a86bc-134">在 hello hello 精靈第一頁指定 hello CX 伺服器 IP 位址和 hello CX 伺服器連接埠。</span><span class="sxs-lookup"><span data-stu-id="a86bc-134">On hello first page of hello wizard specify hello CX server IP address and hello CX server port.</span></span> <span data-ttu-id="a86bc-135">選取 [使用 HTTPS] 。</span><span class="sxs-lookup"><span data-stu-id="a86bc-135">Select **Use HTTPS**.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image3.png)
5. <span data-ttu-id="a86bc-136">尋找 hello 組態伺服器 IP 位址上 hello**儀表板**hello 組態伺服器中 Azure VM 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a86bc-136">Find hello configuration server IP address on hello **Dashboard** tab of hello configuration server VM in Azure.</span></span>
   ![](./media/site-recovery-failback-azure-to-vmware/image4.png)
6. <span data-ttu-id="a86bc-137">尋找 hello 組態伺服器 HTTPS 公用連接埠上 hello**端點**hello 組態伺服器中 Azure VM 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a86bc-137">Find hello configuration server HTTPS public port on hello **Endpoints** tab of hello configuration server VM in Azure.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image5.png)
7. <span data-ttu-id="a86bc-138">在 hello **CS 複雜密碼詳細資料**頁面上，指定您記下下註冊 hello 組態伺服器時的 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a86bc-138">On hello **CS Passphrase Details** page specify hello passphrase that you noted down when you registered hello configuration server.</span></span> <span data-ttu-id="a86bc-139">如果您不記得它簽入**c:\\Program Files (x86)\\InMage 系統\\私人\\connection.passphrase** hello 組態伺服器 VM 上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-139">If you don't remember it check it in **C:\\Program Files (x86)\\InMage Systems\\private\\connection.passphrase** on hello configuration server VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image6.png)
8. <span data-ttu-id="a86bc-140">在 hello**選取目的地位置**頁面上，指定您希望 tooinstall hello vContinuum 伺服器並按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-140">In hello **Select Destination Location** page specify where you want tooinstall hello vContinuum server and click **Install**.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image7.png)
9. <span data-ttu-id="a86bc-141">安裝完成後，您可以啟動 vContinuum。</span><span class="sxs-lookup"><span data-stu-id="a86bc-141">After installation completes, you can launch vContinuum.</span></span>
    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)

## <a name="step-2-install-a-process-server-in-azure"></a><span data-ttu-id="a86bc-142">步驟 2：在 Azure 中安裝處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="a86bc-142">Step 2: Install a process server in Azure</span></span>
<span data-ttu-id="a86bc-143">您需要 tooinstall 在 Azure 中的處理序伺服器，以便在 Azure 中的 hello Vm 可以傳送 hello 資料回復 tooan 在內部部署主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-143">You need tooinstall a process server in Azure so that hello VMs in Azure can send hello data back tooan on-premises master target server.</span></span>

1. <span data-ttu-id="a86bc-144">在 hello**設定伺服器**頁面在 Azure 中，選取 tooadd 新的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-144">On hello **Configuration Servers** page in Azure, select tooadd a new process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image9.png)
2. <span data-ttu-id="a86bc-145">指定處理序伺服器名稱，以及名稱和密碼 tooconnect toohello 虛擬機器系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="a86bc-145">Specify a process server name, and a name and password tooconnect toohello virtual machine as an administrator.</span></span> <span data-ttu-id="a86bc-146">選取您想 tooregister hello 處理序伺服器 hello 組態伺服器 toowhich。</span><span class="sxs-lookup"><span data-stu-id="a86bc-146">Select hello configuration server toowhich you want tooregister hello process server.</span></span> <span data-ttu-id="a86bc-147">這應該是 hello 相同的伺服器，您使用 tooprotect，並將虛擬機器容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a86bc-147">This should be hello same server you're using tooprotect and fail over your virtual machines.</span></span>
3. <span data-ttu-id="a86bc-148">指定 hello Azure 網路中的 hello 應該部署處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-148">Specify hello Azure network in which hello process server should be deployed.</span></span> <span data-ttu-id="a86bc-149">它應該是相同的 hello hello 組態伺服器的網路。</span><span class="sxs-lookup"><span data-stu-id="a86bc-149">It should be hello same network as hello configuration server.</span></span> <span data-ttu-id="a86bc-150">指定唯一的 IP 位址選取的子網路並開始部署。</span><span class="sxs-lookup"><span data-stu-id="a86bc-150">Specify a unique IP address selected subnet and begin deployment.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image10.png)
4. <span data-ttu-id="a86bc-151">作業是觸發的 toodeploy hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-151">A job is triggered toodeploy hello process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image11.png)
5. <span data-ttu-id="a86bc-152">Hello 處理序伺服器部署在 Azure 中之後，您可以使用登入 hello server hello 您指定的認證。</span><span class="sxs-lookup"><span data-stu-id="a86bc-152">After hello process server is deployed in Azure you can log into hello server using hello credentials you specified.</span></span> <span data-ttu-id="a86bc-153">註冊 hello 處理序伺服器在 hello 註冊 hello 的相同方式在內部處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-153">Register hello process server in hello same way you registered hello on-premises process server.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image12.png)

> [!NOTE]
> <span data-ttu-id="a86bc-154">hello 容錯回復期間已註冊的伺服器將不會顯示在 Site Recovery 中的 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="a86bc-154">hello servers registered during failback won't be visible under VM properties in Site Recovery.</span></span> <span data-ttu-id="a86bc-155">它們才會顯示在 [hello**伺服器**hello 組態伺服器 toowhich 進行登錄] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a86bc-155">They are only visible under hello **Servers** tab of hello configuration server toowhich they're registered.</span></span> <span data-ttu-id="a86bc-156">可能需要大約 10-15 分鐘直到它們 hello 處理序伺服器已出現在 [hello] 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-156">It can take about 10-15 minutes until they hello process server appears on hello tab.</span></span>
>
>

## <a name="step-3-install-a-master-target-server-on-premises"></a><span data-ttu-id="a86bc-157">步驟 3：安裝主要目標伺服器內部部署</span><span class="sxs-lookup"><span data-stu-id="a86bc-157">Step 3: Install a master target server on-premises</span></span>
<span data-ttu-id="a86bc-158">根據您來源虛擬機器的作業系統，您需要 tooinstall Linux 或 Windows 主要目標伺服器在內部。</span><span class="sxs-lookup"><span data-stu-id="a86bc-158">Depending on your source virtual machines operating system, you need tooinstall a Linux or a Windows master target server on-premises.</span></span>

### <a name="deploy-a-windows-master-target-server"></a><span data-ttu-id="a86bc-159">部署 Windows 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="a86bc-159">Deploy a Windows master target server</span></span>
<span data-ttu-id="a86bc-160">Windows 主要目標已經隨附於 vContinuum 安裝程式中。</span><span class="sxs-lookup"><span data-stu-id="a86bc-160">A Windows master target is already bundled with vContinuum setup.</span></span> <span data-ttu-id="a86bc-161">當您安裝 hello vContinuum 時，主要伺服器也部署在 hello 上相同的電腦和已註冊的 toohello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-161">When you install hello vContinuum, a master server is also deployed on hello same machine and registered toohello configuration server.</span></span>

1. <span data-ttu-id="a86bc-162">toobegin 部署中，建立空白電腦在內部想 toorecover hello 從 Azure Vm 的 hello ESX 主機上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-162">toobegin deployment, create an empty machine on-premises on hello ESX host onto which you want toorecover hello VMs from Azure.</span></span>
2. <span data-ttu-id="a86bc-163">請確定有兩個以上的磁碟附加 toohello VM – hello 作業系統使用的其中一種，而且其他 hello 用於 hello 保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a86bc-163">Ensure that there are at least two disks attached toohello VM – one is used for hello operating system and hello other is used for hello retention drive.</span></span>
3. <span data-ttu-id="a86bc-164">Hello 作業系統安裝。</span><span class="sxs-lookup"><span data-stu-id="a86bc-164">Install hello operating system.</span></span>
4. <span data-ttu-id="a86bc-165">Hello 伺服器上安裝 hello vContinuum。</span><span class="sxs-lookup"><span data-stu-id="a86bc-165">Install hello vContinuum on hello server.</span></span> <span data-ttu-id="a86bc-166">這也會完成 hello 主要目標伺服器的安裝。</span><span class="sxs-lookup"><span data-stu-id="a86bc-166">This also completes installation of hello master target server.</span></span>

### <a name="deploy-a-linux-master-target-server"></a><span data-ttu-id="a86bc-167">部署 Linux 主要目標伺服器</span><span class="sxs-lookup"><span data-stu-id="a86bc-167">Deploy a Linux master target server</span></span>
1. <span data-ttu-id="a86bc-168">toobegin 部署中，建立空白電腦在內部想 toorecover hello 從 Azure Vm 的 hello ESX 主機上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-168">toobegin deployment, create an empty machine on-premises on hello ESX host onto which you want toorecover hello VMs from Azure.</span></span>
2. <span data-ttu-id="a86bc-169">請確定有兩個以上的磁碟附加 toohello VM – hello 作業系統使用的其中一種，而且其他 hello 用於 hello 保留磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a86bc-169">Ensure that there are at least two disks attached toohello VM – one is used for hello operating system and hello other is used for hello retention drive.</span></span>
3. <span data-ttu-id="a86bc-170">安裝 hello Linux 作業系統。</span><span class="sxs-lookup"><span data-stu-id="a86bc-170">Install hello Linux operating system.</span></span> <span data-ttu-id="a86bc-171">hello Linux 主要目標系統不應該使用 LVM 根或保留儲存空間。</span><span class="sxs-lookup"><span data-stu-id="a86bc-171">hello Linux master target system should not use LVM for root or retention storage spaces.</span></span> <span data-ttu-id="a86bc-172">依預設，的 Linux 主要目標伺服器已設定 tooavoid LVM 分割區/磁碟探索。</span><span class="sxs-lookup"><span data-stu-id="a86bc-172">A Linux master target server is configured tooavoid LVM partitions/disks discovery by default.</span></span>
4. <span data-ttu-id="a86bc-173">您可以建立的磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="a86bc-173">Partitions that you can create:</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image13.png)
5. <span data-ttu-id="a86bc-174">開始 hello 主要目標安裝之前執行下列後續安裝步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="a86bc-174">Carry out hello below post installation steps before beginning hello master target installation.</span></span>

#### <a name="post-os-installation-steps"></a><span data-ttu-id="a86bc-175">作業系統的安裝前步驟</span><span class="sxs-lookup"><span data-stu-id="a86bc-175">Post OS Installation Steps</span></span>
<span data-ttu-id="a86bc-176">tooget hello SCSI 識別碼傳回的每個 SCSI 硬碟，在 Linux 虛擬機器，啟用 hello 參數 「 磁碟。EnableUUID = TRUE"，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a86bc-176">tooget hello SCSI ID’s for each of SCSI hard disk in a Linux virtual machine, enable hello parameter “disk.EnableUUID = TRUE” as follows:</span></span>

1. <span data-ttu-id="a86bc-177">關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-177">Shut down your virtual machine.</span></span>
2. <span data-ttu-id="a86bc-178">以滑鼠右鍵按一下 hello 左側面板中的 hello VM 項目 >**編輯設定**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-178">Right-click hello VM entry in hello left-hand panel > **Edit Settings**.</span></span>
3. <span data-ttu-id="a86bc-179">按一下 hello**選項** 索引標籤。選取 進階\> 一般項目  >  組態參數。</span><span class="sxs-lookup"><span data-stu-id="a86bc-179">Click hello **Options** tab. Select **Advanced\>General item** > **Configuration Parameters**.</span></span> <span data-ttu-id="a86bc-180">hello**組態參數**hello 機器關機時，才可用選項。</span><span class="sxs-lookup"><span data-stu-id="a86bc-180">hello **Configuration Parameters** option is only available when hello machine is shut down.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image14.png)
4. <span data-ttu-id="a86bc-181">查看含有 **disk.EnableUUID** 的資料列是否已經存在？</span><span class="sxs-lookup"><span data-stu-id="a86bc-181">Checks whether a row with **disk.EnableUUID** exists.</span></span> <span data-ttu-id="a86bc-182">如果它設定得**False**然後將它設定太**True** （不區分大小寫）。</span><span class="sxs-lookup"><span data-stu-id="a86bc-182">If it does and is set too**False** then set it too**True** (not case sensitive).</span></span> <span data-ttu-id="a86bc-183">如果存在，而且是設定 tootrue，請按一下**取消**和開機設定之後，測試 hello hello 客體作業系統內的 SCSI 命令。</span><span class="sxs-lookup"><span data-stu-id="a86bc-183">If exists and is set tootrue, click **Cancel** and test hello SCSI command inside hello guest operating system after it's booted up.</span></span> <span data-ttu-id="a86bc-184">如果不存在，請按一下 [加入資料列] 。</span><span class="sxs-lookup"><span data-stu-id="a86bc-184">If doesn't exist click **Add Row**.</span></span>
5. <span data-ttu-id="a86bc-185">新增磁碟。在 hello EnableUUID**名稱**資料行。</span><span class="sxs-lookup"><span data-stu-id="a86bc-185">Add disk.EnableUUID in hello **Name** column.</span></span> <span data-ttu-id="a86bc-186">將其值儲存為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="a86bc-186">Set its value as TRUE.</span></span> <span data-ttu-id="a86bc-187">請勿將加入 hello 高於以及雙引號的值。</span><span class="sxs-lookup"><span data-stu-id="a86bc-187">Don't add hello above values along with double-quotes.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image15.png)

#### <a name="download-and-install-hello-additional-packages"></a><span data-ttu-id="a86bc-188">下載並安裝 hello 其他封裝</span><span class="sxs-lookup"><span data-stu-id="a86bc-188">Download and install hello additional packages</span></span>
<span data-ttu-id="a86bc-189">注意： 請確定 hello 系統具有網際網路連線才能下載和安裝 hello 其他封裝。</span><span class="sxs-lookup"><span data-stu-id="a86bc-189">NOTE: Make sure hello system has internet connectivity before downloading and installing hello additional packages.</span></span>

<span data-ttu-id="a86bc-190">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span><span class="sxs-lookup"><span data-stu-id="a86bc-190">\# yum install -y xfsprogs perl lsscsi rsync wget kexec-tools</span></span>

<span data-ttu-id="a86bc-191">此命令會從 CentOS 6.6 儲存機制下載這 15 個封裝，並加以安裝：</span><span class="sxs-lookup"><span data-stu-id="a86bc-191">This command downloads these 15 packages from CentOS 6.6 repository and installs them:</span></span>

<span data-ttu-id="a86bc-192">bc-1.06.95-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-192">bc-1.06.95-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-193">busybox-1.15.1-20.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-193">busybox-1.15.1-20.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-194">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-194">elfutils-libs-0.158-3.2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-195">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-195">kexec-tools-2.0.0-280.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-196">lsscsi-0.23-2.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-196">lsscsi-0.23-2.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-197">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-197">lzo-2.03-3.1.el6\_5.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-198">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-198">perl-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-199">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-199">perl-Module-Pluggable-3.90-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-200">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-200">perl-Pod-Escapes-1.04-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-201">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-201">perl-Pod-Simple-3.13-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-202">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-202">perl-libs-5.10.1-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-203">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-203">perl-version-0.77-136.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-204">rsync-3.0.6-12.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-204">rsync-3.0.6-12.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-205">snappy-1.1.0-1.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-205">snappy-1.1.0-1.el6.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-206">wget-1.12-5.el6\_6.1.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-206">wget-1.12-5.el6\_6.1.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-207">如果 hello 來源電腦會使用 Reiser 或 XFS filesystem hello 根或開機裝置，然後下列套件必須下載並安裝 tooprotection 先前的 Linux 主要目標上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-207">If hello source machine uses Reiser or XFS filesystem for hello root or boot device, then following packages should be downloaded and installed on Linux master target prior tooprotection.</span></span>

<span data-ttu-id="a86bc-208">\# cd /usr/local</span><span class="sxs-lookup"><span data-stu-id="a86bc-208">\# cd /usr/local</span></span>

<span data-ttu-id="a86bc-209">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="a86bc-209">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/kmod-reiserfs-0.0-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="a86bc-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="a86bc-210">\# wget <http://elrepo.org/linux/elrepo/el6/x86_64/RPMS/reiserfs-utils-3.6.21-1.el6.elrepo.x86_64.rpm></span></span>

<span data-ttu-id="a86bc-211">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-211">\# rpm -ivh kmod-reiserfs-0.0-1.el6.elrepo.x86\_64.rpm reiserfs-utils-3.6.21-1.el6.elrepo.x86\_64.rpm</span></span>

<span data-ttu-id="a86bc-212">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span><span class="sxs-lookup"><span data-stu-id="a86bc-212">\# wget <http://mirror.centos.org/centos/6.6/os/x86_64/Packages/xfsprogs-3.1.1-16.el6.x86_64.rpm></span></span>

<span data-ttu-id="a86bc-213">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span><span class="sxs-lookup"><span data-stu-id="a86bc-213">\# rpm -ivh xfsprogs-3.1.1-16.el6.x86\_64.rpm</span></span>

#### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="a86bc-214">套用自訂組態變更</span><span class="sxs-lookup"><span data-stu-id="a86bc-214">Apply custom configuration changes</span></span>
<span data-ttu-id="a86bc-215">套用這些變更之前請先確定您已完成 hello 上一節，則請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a86bc-215">Before applying these changes make sure you've completed hello previous section, then follow these steps:</span></span>

1. <span data-ttu-id="a86bc-216">將複製 hello RHEL 6 64 整合代理程式二進位 toohello 新建立的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a86bc-216">Copy hello RHEL 6-64 Unified Agent binary toohello newly created OS.</span></span>
2. <span data-ttu-id="a86bc-217">執行這個命令 toountar hello 二進位： **tar-zxvf\<檔案名稱\>**</span><span class="sxs-lookup"><span data-stu-id="a86bc-217">Run this command toountar hello binary: **tar -zxvf \<File name\>**</span></span>
3. <span data-ttu-id="a86bc-218">執行這個命令 toogive 權限： \# **chmod 755./ApplyCustomChanges.sh**</span><span class="sxs-lookup"><span data-stu-id="a86bc-218">Run this command toogive permissions: \# **chmod 755 ./ApplyCustomChanges.sh**</span></span>
4. <span data-ttu-id="a86bc-219">執行 hello 指令碼：  **\# ./ApplyCustomChanges.sh**。Hello 伺服器上執行一次 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a86bc-219">Run hello script: **\# ./ApplyCustomChanges.sh**. Run hello script only once on hello server.</span></span> <span data-ttu-id="a86bc-220">Hello 指令碼執行後，請重新啟動 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-220">Restart hello server after hello script runs.</span></span>

### <a name="install-hello-linux-server"></a><span data-ttu-id="a86bc-221">安裝 hello Linux 伺服器</span><span class="sxs-lookup"><span data-stu-id="a86bc-221">Install hello Linux server</span></span>
1. <span data-ttu-id="a86bc-222">[下載](http://go.microsoft.com/fwlink/?LinkID=529757)hello 安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="a86bc-222">[Download](http://go.microsoft.com/fwlink/?LinkID=529757) hello installation file.</span></span>
2. <span data-ttu-id="a86bc-223">將複製 hello 檔案 toohello Linux 主要目標虛擬機器使用您選擇的 sftp 用戶端公用程式。</span><span class="sxs-lookup"><span data-stu-id="a86bc-223">Copy hello file toohello Linux Master Target virtual machine using an sftp client utility of your choice.</span></span> <span data-ttu-id="a86bc-224">或者，您便可以登入 hello Linux 主要目標虛擬機器上，並使用 wget toodownload hello 安裝套件從提供的連結</span><span class="sxs-lookup"><span data-stu-id="a86bc-224">Alternately you can log onto hello Linux master target virtual machine and use wget toodownload hello installation package from the provided link</span></span>
3. <span data-ttu-id="a86bc-225">登入 hello Linux 主要目標伺服器的虛擬機器使用 ssh 您選擇的用戶端</span><span class="sxs-lookup"><span data-stu-id="a86bc-225">Log onto hello Linux master target server virtual machine using an ssh client of your choice</span></span>
4. <span data-ttu-id="a86bc-226">如果您已經連接 toohello Azure 網路的方法，您可以部署 Linux 主要目標伺服器透過 VPN 連線，然後 hello server 發現虛擬機器中使用的內部 IP 位址**儀表板** 索引標籤和連接埠22 tooconnect toohello Linux 主要目標伺服器使用 Secure Shell。</span><span class="sxs-lookup"><span data-stu-id="a86bc-226">If you're connected toohello Azure network on which you deployed your Linux master target server through a VPN connection then use the internal IP address for hello server that you can find in the virtual machine **Dashboard** tab, and port 22 tooconnect toohello Linux master target Server using Secure Shell.</span></span>
5. <span data-ttu-id="a86bc-227">如果您正在連接 toohello Linux 主要目標伺服器，透過公用網際網路連線使用 hello Linux 主要目標伺服器的公用虛擬 IP 位址 (hello 虛擬機器從**儀表板** 索引標籤) 和 hello 公用端點針對建立 ssh toologin toohello Linux servder。</span><span class="sxs-lookup"><span data-stu-id="a86bc-227">If you're connecting toohello Linux master target server over a public internet connection use hello Linux master target server’s public virtual IP address (from hello virtual machines **Dashboard** tab) and hello public endpoint created for ssh toologin toohello Linux servder.</span></span>
6. <span data-ttu-id="a86bc-228">執行從 hello gzipped Linux 主要目標伺服器安裝程式的 tar 檔案解壓縮封存擷取 hello 檔案： *"tar – xvzf Microsoft ASR\_UA\_8.2.0.0\_RHEL6 64"* hello 目錄中，包含 hello 安裝程式檔案。</span><span class="sxs-lookup"><span data-stu-id="a86bc-228">Extract hello files from hello gzipped Linux master target Server installer tar archive by running: *“tar –xvzf Microsoft-ASR\_UA\_8.2.0.0\_RHEL6-64\”* from hello directory that contains hello installer file.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image16.png)
7. <span data-ttu-id="a86bc-229">如果您擷取的 hello 安裝程式檔案 tooa 不同的目錄變更 toohello 目錄 toowhich hello hello tar 檔案解壓縮封存內容解壓縮。</span><span class="sxs-lookup"><span data-stu-id="a86bc-229">If you extracted hello installer files tooa different directory change toohello directory toowhich hello contents of hello tar archive were extracted.</span></span> <span data-ttu-id="a86bc-230">從這個目錄路徑執行 “sudo ./install.sh”。</span><span class="sxs-lookup"><span data-stu-id="a86bc-230">From this directory path run “sudo ./install.sh”.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image17.png)
8. <span data-ttu-id="a86bc-231">當提示的 toochoose 主要角色選取**2 （主要目標）**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-231">When prompted toochoose a primary role select **2 (Master Target)**.</span></span> <span data-ttu-id="a86bc-232">Hello 其他互動式安裝選項保留其預設值。</span><span class="sxs-lookup"><span data-stu-id="a86bc-232">Leave hello other interactive install options at their default values.</span></span>
9. <span data-ttu-id="a86bc-233">等候安裝 toocontinue 和 hello 主機組態介面 tooappear。</span><span class="sxs-lookup"><span data-stu-id="a86bc-233">Wait for installation toocontinue and hello Host Config Interface tooappear.</span></span> <span data-ttu-id="a86bc-234">hello hello Linux 主要目標伺服器的主機組態公用程式是命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="a86bc-234">hello Host Configuration utility for hello Linux master sarget Server is a command line utility.</span></span> <span data-ttu-id="a86bc-235">不要 hello ssh 用戶端公用程式調整視窗的大小。</span><span class="sxs-lookup"><span data-stu-id="a86bc-235">Don’t resize hello ssh client utility window.</span></span> <span data-ttu-id="a86bc-236">使用 hello 箭號鍵 tooselect hello **Global**選項並按下鍵盤上的輸入。</span><span class="sxs-lookup"><span data-stu-id="a86bc-236">Use hello arrow keys tooselect hello **Global** option and press ENTER on your keyboard.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image18.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image19.png)
10. <span data-ttu-id="a86bc-237">在 hello 欄位中**IP**輸入 hello hello 組態伺服器的內部 IP 位址 (在 hello**儀表板**hello 組態伺服器 VM 索引標籤) 按下 ENTER。</span><span class="sxs-lookup"><span data-stu-id="a86bc-237">In hello field **IP** enter hello Internal IP address of hello configuration server (you can find it in hello **Dashboard** tab of hello configuration server VM) and press ENTER.</span></span> <span data-ttu-id="a86bc-238">在 [連接埠] 中，輸入 **22**，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="a86bc-238">In **Port** enter **22** and press ENTER.</span></span>
11. <span data-ttu-id="a86bc-239">保留 [使用 HTTPS] 為 [是]，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="a86bc-239">Leave **Use HTTPS** as **Yes**, and press ENTER.</span></span>
12. <span data-ttu-id="a86bc-240">輸入 hello hello 組態伺服器所產生的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a86bc-240">Enter hello Passphrase that was generated on hello configuration server.</span></span> <span data-ttu-id="a86bc-241">如果您使用 PUTTY 的用戶端從 Windows 電腦 toossh toohello Linux 虛擬機器，您可以使用 Shift + Insert toopaste hello 內容 hello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="a86bc-241">If you're using a PUTTY client from a Windows machine toossh toohello Linux virtual machine you can use Shift+Insert toopaste hello contents of hello clipboard.</span></span> <span data-ttu-id="a86bc-242">複製 hello 複雜密碼 toohello 本機剪貼簿使用 Ctrl + C，並使用 Shift + Insert toopaste 它。</span><span class="sxs-lookup"><span data-stu-id="a86bc-242">Copy hello Passphrase toohello local clipboard using Ctrl-C and use Shift+Insert toopaste it.</span></span> <span data-ttu-id="a86bc-243">按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="a86bc-243">Press ENTER.</span></span>
13. <span data-ttu-id="a86bc-244">使用 hello 向右箭號鍵 toonavigate tooquit，然後按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="a86bc-244">Use hello right arrow key toonavigate tooquit and press ENTER.</span></span> <span data-ttu-id="a86bc-245">等候安裝 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="a86bc-245">Wait for installation toocomplete.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image20.png)

<span data-ttu-id="a86bc-246">如果基於某些原因您無法 tooregister Linux 主要目標伺服器 toohello 組態伺服器您可以再次從 /usr/local/ASR/Vx/bin/hostconfigcli （您必須先 tooset 存取權限 toothis 執行主機組態公用程式目錄執行 chmod 做為進階使用者）。</span><span class="sxs-lookup"><span data-stu-id="a86bc-246">If for some reason you failed tooregister your Linux master target server toohello configuration server you can do so again by running the host configuration utility from /usr/local/ASR/Vx/bin/hostconfigcli (you'll first need tooset access permissions toothis directory by running chmod as a super user).</span></span>

#### <a name="validate-master-target-registration"></a><span data-ttu-id="a86bc-247">驗證主要目標註冊</span><span class="sxs-lookup"><span data-stu-id="a86bc-247">Validate master target registration</span></span>
<span data-ttu-id="a86bc-248">您可以驗證該 hello 主要目標伺服器已成功註冊 Azure Site Recovery 保存庫中的 toohello 組態伺服器 >**組態伺服器** > **伺服器詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-248">You can validate that hello master target server was registered successfully toohello configuration server in Azure Site Recovery vault > **Configuration Server** > **Server Details**.</span></span>

> [!NOTE]
> <span data-ttu-id="a86bc-249">如果您收到 hello 虛擬機器的組態錯誤註冊 hello 主要目標伺服器，可能已經刪除從 Azure 或端點設定不正確之後，這是因為雖然 hello 偵測到主要目標設定由 hello Azure dndpoints hello 主要目標是部署在 Azure 中，這不是在內部部署主要目標伺服器內部部署，則為 true。</span><span class="sxs-lookup"><span data-stu-id="a86bc-249">After registering hello master target server, if you receive configuration errors that hello virtual machine might have been deleted from Azure or that endpoints are not properly configured, this is because although hello master target configuration is detected by hello Azure dndpoints when hello master target is deployed in Azure, this isn't true for an on-premises master target server on-premises.</span></span> <span data-ttu-id="a86bc-250">這並不會影響容錯回復，您可以忽略這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="a86bc-250">This won't affect failback and you can ignore these errors.</span></span>
>
>

## <a name="step-4-protect-hello-virtual-machines-toohello-on-premises-site"></a><span data-ttu-id="a86bc-251">步驟 4： 保護虛擬機器 toohello 在內部部署站台 hello</span><span class="sxs-lookup"><span data-stu-id="a86bc-251">Step 4: Protect hello virtual machines toohello on-premises site</span></span>
<span data-ttu-id="a86bc-252">您的容錯回復之前，您會需要 tooprotect Vm toohello 在內部部署站台。</span><span class="sxs-lookup"><span data-stu-id="a86bc-252">You need tooprotect VMs toohello on-premises site before you fail back.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="a86bc-253">開始之前</span><span class="sxs-lookup"><span data-stu-id="a86bc-253">Before you begin</span></span>
<span data-ttu-id="a86bc-254">VM 容錯移轉 tooAzure，它會新增網頁檔案的額外暫存磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a86bc-254">When a VM is failed over tooAzure, it adds an extra temp drive for page file.</span></span> <span data-ttu-id="a86bc-255">這通常是您已容錯移轉的 VM 不需要的額外磁碟機，因為它可能已經有分頁檔專用的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a86bc-255">This is an extra drive that is typically not required by your failed over VM since it might already have a drive dedicated for the page file.</span></span> <span data-ttu-id="a86bc-256">在開始反向 hello 虛擬機器的保護之前，您需要請確定此磁碟機已離線，因此它並不會受到保護。</span><span class="sxs-lookup"><span data-stu-id="a86bc-256">Before you begin reverse protection of hello virtual machines, you need to ensure that this drive is taken offline so that it does not get protected.</span></span> <span data-ttu-id="a86bc-257">以下列方式來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="a86bc-257">Do this as follows:</span></span>

1. <span data-ttu-id="a86bc-258">開啟 電腦管理，然後選取存放裝置管理，因此，它會列出 hello 磁碟線上和附加 toohello 機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-258">Open Computer Management and select Storage Management so that it lists hello disks online and attached toohello machine.</span></span>
2. <span data-ttu-id="a86bc-259">選取 hello 暫存磁碟附加的 toohello 機器，然後選擇 toobring 離線。</span><span class="sxs-lookup"><span data-stu-id="a86bc-259">Select hello temporary disk attached toohello machine and choose toobring it offline.</span></span>

### <a name="protect-hello-vms"></a><span data-ttu-id="a86bc-260">保護 hello Vm</span><span class="sxs-lookup"><span data-stu-id="a86bc-260">Protect hello VMs</span></span>
1. <span data-ttu-id="a86bc-261">在 hello Azure 入口網站，檢查 hello 它們正在容錯移轉的虛擬機器 tooensure hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="a86bc-261">In hello Azure portal, check hello states of hello virtual machine tooensure that they're failed over.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image21.png)
2. <span data-ttu-id="a86bc-262">啟動機器上的 vContinuum。</span><span class="sxs-lookup"><span data-stu-id="a86bc-262">Launch vContinuum on your machine.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image8.png)
3. <span data-ttu-id="a86bc-263">按一下**新的保護**選取 hello 作業系統類型，</span><span class="sxs-lookup"><span data-stu-id="a86bc-263">Click **New Protection** and select hello operation system type, the</span></span>
4. <span data-ttu-id="a86bc-264">在 hello 新視窗中開啟選取的 hello **OS 類型** > **取得詳細資料**想 hello Vm toofail 回。</span><span class="sxs-lookup"><span data-stu-id="a86bc-264">In hello new window that open select hello **OS type** > **Get Details** for hello VMs you want toofail back.</span></span> <span data-ttu-id="a86bc-265">在**主要伺服器的詳細資料**、 識別及選取 hello 您想 tooprotect 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-265">In **Primary server details**, identify and select hello virtual machines that you want tooprotect.</span></span> <span data-ttu-id="a86bc-266">Vm 列在進行容錯移轉前的 hello vCenter 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a86bc-266">VMs are listed under hello vCenter host name that they were on before failover.</span></span>
5. <span data-ttu-id="a86bc-267">當您選取虛擬機器 tooprotect （它已經有容錯 tooAzure） 快顯視窗會提供兩個項目 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-267">When you select a virtual machine tooprotect (and it has already failed over tooAzure) a pop-up window provides two entries for hello virtual machine.</span></span> <span data-ttu-id="a86bc-268">這是因為 hello 組態伺服器偵測到的 hello 註冊的虛擬機器 tooit 的兩個執行個體。</span><span class="sxs-lookup"><span data-stu-id="a86bc-268">This is because hello configuration server detects two instances of hello virtual machines registered tooit.</span></span> <span data-ttu-id="a86bc-269">Hello 在內部部署 VM，讓您可以保護 hello 正確的 VM，您會需要 tooremove hello 項目。</span><span class="sxs-lookup"><span data-stu-id="a86bc-269">You need tooremove hello entry for hello on-premises VM so that you can protect hello correct VM.</span></span> <span data-ttu-id="a86bc-270">tooidentify hello 正確 Azure VM 的項目這裡，您可以登入 hello Azure VM 和移 tooC:\Program 檔案 (x86) \Microsoft Azure Site Recovery\Application Data\etc。在 hello 檔案 drscout.conf，找出 hello 主機識別碼。</span><span class="sxs-lookup"><span data-stu-id="a86bc-270">tooidentify hello correct Azure VM entry here, you can log into hello Azure VM and go tooC:\Program Files (x86)\Microsoft Azure Site Recovery\Application Data\etc. In hello file drscout.conf , identify hello host ID.</span></span> <span data-ttu-id="a86bc-271">在 [hello vContinuum] 對話方塊保持 hello 項目，您必須找到 hello 主機識別碼 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a86bc-271">In hello vContinuum dialog, keep hello entry for which you found hello host ID on  hello VM.</span></span> <span data-ttu-id="a86bc-272">刪除所有其他項目。</span><span class="sxs-lookup"><span data-stu-id="a86bc-272">Delete all other entries.</span></span> <span data-ttu-id="a86bc-273">tooselect hello 更正 VM，您可以使用參照 tooits IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a86bc-273">tooselect hello correct VM you can refer tooits IP address.</span></span> <span data-ttu-id="a86bc-274">hello IP 位址範圍在內部將 hello 在內部部署 VM。</span><span class="sxs-lookup"><span data-stu-id="a86bc-274">hello IP address range on-premises will be hello on-premises VM.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image22.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image23.png)
6. <span data-ttu-id="a86bc-275">Hello vCenter server 上停止 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-275">On hello vCenter server stop hello virtual machine.</span></span> <span data-ttu-id="a86bc-276">您也可以刪除 hello Vm 內部部署。</span><span class="sxs-lookup"><span data-stu-id="a86bc-276">You can also delete hello VMs on-premises.</span></span>
7. <span data-ttu-id="a86bc-277">然後指定您想要 tooprotect hello Vm hello 內部 MT 伺服器 toowhich。</span><span class="sxs-lookup"><span data-stu-id="a86bc-277">Then specify hello on-premises MT server toowhich you want tooprotect hello VMs.</span></span> <span data-ttu-id="a86bc-278">toodo，連接您想要回到 toofail toohello vCenter server toowhich。</span><span class="sxs-lookup"><span data-stu-id="a86bc-278">toodo this, connect toohello vCenter server toowhich you want toofail back.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
8. <span data-ttu-id="a86bc-279">選取 hello 主要目標伺服器根據 hello 主機 toowhich 想 toorecover hello VM。</span><span class="sxs-lookup"><span data-stu-id="a86bc-279">Select hello master target server based on hello host toowhich you want toorecover hello VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image24.png)
9. <span data-ttu-id="a86bc-280">提供每個 hello 虛擬機器的 hello replication 選項。</span><span class="sxs-lookup"><span data-stu-id="a86bc-280">Provide hello replication option for each of hello virtual machines.</span></span> <span data-ttu-id="a86bc-281">toodo 這您需要 tooselect hello 復原端資料存放區 toowhich hello Vm 將會復原。</span><span class="sxs-lookup"><span data-stu-id="a86bc-281">toodo this you need tooselect hello recovery side datastore toowhich hello VMs will be recovered.</span></span> <span data-ttu-id="a86bc-282">hello 表格摘要說明您需要為每個 VM 的 tooprovide hello 不同的選項。</span><span class="sxs-lookup"><span data-stu-id="a86bc-282">hello table summarizes hello different options you need tooprovide for each VM.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image25.png)

   | <span data-ttu-id="a86bc-283">**選項**</span><span class="sxs-lookup"><span data-stu-id="a86bc-283">**Option**</span></span> | <span data-ttu-id="a86bc-284">**選項建議值**</span><span class="sxs-lookup"><span data-stu-id="a86bc-284">**Option recommended value**</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a86bc-285">處理序伺服器 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a86bc-285">Process server IP address</span></span> |<span data-ttu-id="a86bc-286">選取 Azure 中部署的 hello 處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="a86bc-286">Select hello process server deployed in Azure</span></span> |
   |  <span data-ttu-id="a86bc-287">保留大小 (以 MB 為單位)</span><span class="sxs-lookup"><span data-stu-id="a86bc-287">Retention size in MB</span></span> | |
   |  <span data-ttu-id="a86bc-288">保留值</span><span class="sxs-lookup"><span data-stu-id="a86bc-288">Retention value</span></span> |<span data-ttu-id="a86bc-289">1</span><span class="sxs-lookup"><span data-stu-id="a86bc-289">1</span></span> |
   |  <span data-ttu-id="a86bc-290">天/小時</span><span class="sxs-lookup"><span data-stu-id="a86bc-290">Days/Hours</span></span> |<span data-ttu-id="a86bc-291">星期幾</span><span class="sxs-lookup"><span data-stu-id="a86bc-291">Days</span></span> |
   |  <span data-ttu-id="a86bc-292">一致性間隔</span><span class="sxs-lookup"><span data-stu-id="a86bc-292">Consistency interval</span></span> |<span data-ttu-id="a86bc-293">1</span><span class="sxs-lookup"><span data-stu-id="a86bc-293">1</span></span> |
   |  <span data-ttu-id="a86bc-294">選取目標資料存放區</span><span class="sxs-lookup"><span data-stu-id="a86bc-294">Select target datastore</span></span> |<span data-ttu-id="a86bc-295">hello 資料存放區可用 hello 復原站台上。</span><span class="sxs-lookup"><span data-stu-id="a86bc-295">hello datastore available on hello recovery site.</span></span> <span data-ttu-id="a86bc-296">hello 資料存放區應該有足夠空間，並且想 toorestore hello 虛擬機器的可用 toohello ESX 主機。</span><span class="sxs-lookup"><span data-stu-id="a86bc-296">hello data store should have enough space, and be available toohello ESX host on which you want toorestore hello virtual machine.</span></span> |
10. <span data-ttu-id="a86bc-297">設定的 hello hello 虛擬機器的屬性會取得容錯移轉 tooon 內部部署站台之後。</span><span class="sxs-lookup"><span data-stu-id="a86bc-297">Configure hello properties that hello virtual machine will acquire after failover tooon-premises site.</span></span> <span data-ttu-id="a86bc-298">hello 屬性都摘要在下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a86bc-298">hello properties are summarized in hello following table.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image26.png)

    | <span data-ttu-id="a86bc-299">**屬性**</span><span class="sxs-lookup"><span data-stu-id="a86bc-299">**Property**</span></span> | <span data-ttu-id="a86bc-300">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="a86bc-300">**Details**</span></span> |
    | --- | --- |
    | <span data-ttu-id="a86bc-301">網路組態</span><span class="sxs-lookup"><span data-stu-id="a86bc-301">Network configuration</span></span> |<span data-ttu-id="a86bc-302">偵測到每個網路介面卡，請選取它，然後按一下 **變更**tooconfigure hello 容錯回復 hello 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a86bc-302">For each network adapter detected, select it and click **Change** tooconfigure hello failback IP address for hello virtual machine.</span></span> |
    | <span data-ttu-id="a86bc-303">硬體組態</span><span class="sxs-lookup"><span data-stu-id="a86bc-303">Hardware Configuration</span></span> |<span data-ttu-id="a86bc-304">指定 hello CPU 和 hello 記憶體 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a86bc-304">Specify hello CPU and hello memory for hello VM.</span></span> <span data-ttu-id="a86bc-305">設定可以套用的 tooall hello 想 tooprotect 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a86bc-305">Settings can be applied tooall hello VMs you are trying tooprotect.</span></span> <span data-ttu-id="a86bc-306">tooidentify hello hello CPU 和記憶體的正確值，您可以參考 toohello IAAS Vm 角色大小，請參閱 hello 的核心數及指派的記憶體。</span><span class="sxs-lookup"><span data-stu-id="a86bc-306">tooidentify hello correct values for hello CPU and memory, you can refer toohello IAAS VMs role size and see hello number of cores and memory assigned.</span></span> |
    | <span data-ttu-id="a86bc-307">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="a86bc-307">Display name</span></span> |<span data-ttu-id="a86bc-308">容錯回復 tooon 內部部署之後, 您可以重新命名 hello 虛擬機器會出現在 hello vCenter 清查。</span><span class="sxs-lookup"><span data-stu-id="a86bc-308">After failback tooon-premises, you can rename hello virtual machines as they'll appear in hello vCenter inventory.</span></span> <span data-ttu-id="a86bc-309">hello 預設名稱是 hello 虛擬機器的電腦主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a86bc-309">hello default name is hello virtual machine computer host name.</span></span> <span data-ttu-id="a86bc-310">tooidentify hello VM 名稱，您可以參考 toohello hello 保護群組中的 VM 清單。</span><span class="sxs-lookup"><span data-stu-id="a86bc-310">tooidentify hello VM name, you can refer toohello VM list in hello Protection group.</span></span> |
    | <span data-ttu-id="a86bc-311">NAT 組態</span><span class="sxs-lookup"><span data-stu-id="a86bc-311">NAT Configuration</span></span> |<span data-ttu-id="a86bc-312">以下將詳細討論</span><span class="sxs-lookup"><span data-stu-id="a86bc-312">Discussed in detail below</span></span> |

    ![](./media/site-recovery-failback-azure-to-vmware/image27.png)

#### <a name="configure-nat-settings"></a><span data-ttu-id="a86bc-313">設定 NAT 原則</span><span class="sxs-lookup"><span data-stu-id="a86bc-313">Configure NAT settings</span></span>
1. <span data-ttu-id="a86bc-314">tooenable hello 虛擬機器的保護，兩個通訊通道必須 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a86bc-314">tooenable protection of hello virtual machines, two communication channels need toobe established.</span></span> <span data-ttu-id="a86bc-315">hello 第一個通道是 hello 虛擬機器與 hello 處理序伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="a86bc-315">hello first channel is between hello virtual machine and hello process server.</span></span> <span data-ttu-id="a86bc-316">此通道會從 hello VM 收集 hello 資料，並將它傳送 toohello 哪些然後傳送 hello 資料 toohello 主要目標伺服器的處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-316">This channel collects hello data from hello VM and sends it toohello process server which then sends hello data toohello master target server.</span></span> <span data-ttu-id="a86bc-317">Hello 處理序伺服器和受保護的 hello 虛擬機器 toobe 是否 hello 位於相同 Azure 虛擬網路，則您不需要 toouse NAT 設定。</span><span class="sxs-lookup"><span data-stu-id="a86bc-317">If hello process server and hello virtual machine toobe protected are on hello same Azure virtual network then you don't need toouse NAT settings.</span></span> <span data-ttu-id="a86bc-318">否則，請指定 NAT 設定。</span><span class="sxs-lookup"><span data-stu-id="a86bc-318">Otherwise specify NAT settings.</span></span> <span data-ttu-id="a86bc-319">在 Azure 中檢視 hello 處理序伺服器 hello 公用 IP 的位址。</span><span class="sxs-lookup"><span data-stu-id="a86bc-319">View hello public IP address of hello process server in Azure.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image28.png)
2. <span data-ttu-id="a86bc-320">hello 第二個通道是 hello 處理序伺服器與 hello 主要目標伺服器之間。</span><span class="sxs-lookup"><span data-stu-id="a86bc-320">hello second channel is between hello process server and hello master target server.</span></span> <span data-ttu-id="a86bc-321">hello 選項 toouse NAT，或者不會取決於您是使用基礎的 VPN 連線或透過 hello 通訊網際網路。</span><span class="sxs-lookup"><span data-stu-id="a86bc-321">hello option toouse NAT or not depends on whether you are using a VPN based connection or communicating over hello internet.</span></span> <span data-ttu-id="a86bc-322">如果您使用 VPN，請不要選取 NAt，只有當您使用網際網路連線時才選取。</span><span class="sxs-lookup"><span data-stu-id="a86bc-322">Don't select NAt if you're using VPN, but only if you're using an internet connection.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image29.png)

    ![](./media/site-recovery-failback-azure-to-vmware/image30.png)
3. <span data-ttu-id="a86bc-323">如果您沒有刪除 hello 在內部部署虛擬機器所指定，則需要 tooensure 容錯回復 toostill 如果 hello 資料存放區會包含 hello 舊 VMDK 的 hello 容錯回復 VM 取得中建立新的位置。</span><span class="sxs-lookup"><span data-stu-id="a86bc-323">If you haven't deleted hello on-premises virtual machines as specified and if hello datastore you are failing back toostill contains hello old VMDK’s then you will need tooensure that hello failback VM gets created in a new place.</span></span> <span data-ttu-id="a86bc-324">toodo 此選取 hello**進階**設定，並指定替代資料夾 toorestore tooin**資料夾名稱設定**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-324">toodo this select hello **Advanced** settings and specify an alternate Folder toorestore tooin **Folder Name Settings**.</span></span> <span data-ttu-id="a86bc-325">將 hello 保留其預設設定其他選項。</span><span class="sxs-lookup"><span data-stu-id="a86bc-325">Leave hello other options with their default settings.</span></span> <span data-ttu-id="a86bc-326">適用於 hello 資料夾名稱設定 tooall hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-326">Apply hello folder name settings tooall hello servers.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image31.png)
4. <span data-ttu-id="a86bc-327">執行整備檢查 tooensure hello 的虛擬機器會準備 toobe 受到保護後 tooon 內部。</span><span class="sxs-lookup"><span data-stu-id="a86bc-327">Run a Readiness Check tooensure that hello virtual machines are ready toobe protected back tooon-premises.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image32.png)
5. <span data-ttu-id="a86bc-328">等候它 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="a86bc-328">Wait for it toocomplete.</span></span> <span data-ttu-id="a86bc-329">如果已順利在所有 Vm 上，您可以指定 hello 保護計劃的名稱。</span><span class="sxs-lookup"><span data-stu-id="a86bc-329">If it's successfully on all VMs you can specify a name for hello protection plan.</span></span> <span data-ttu-id="a86bc-330">然後按一下 **保護**toobegin。</span><span class="sxs-lookup"><span data-stu-id="a86bc-330">Then click **Protect** toobegin.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image33.png)
6. <span data-ttu-id="a86bc-331">您可以在 vContinuum 中監視進度。</span><span class="sxs-lookup"><span data-stu-id="a86bc-331">You can monitor progress in vContinuum.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image34.png)
7. <span data-ttu-id="a86bc-332">Hello 步驟之後**啟用保護計劃**完成，您可以監視 hello Site Recovery 入口網站中的 VM 防護。</span><span class="sxs-lookup"><span data-stu-id="a86bc-332">After hello step **Activating Protection Plan** finishes you can monitor VM protection in hello Site Recovery portal.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image35.png)
8. <span data-ttu-id="a86bc-333">您可以看到 hello 精確狀態 hello VM 上按一下，然後監視其進度。</span><span class="sxs-lookup"><span data-stu-id="a86bc-333">You can see hello exact status clicking on hello VM and monitoring its progress.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image36.png)

## <a name="prepare-hello-failback-plan"></a><span data-ttu-id="a86bc-334">準備 hello 容錯回復計劃</span><span class="sxs-lookup"><span data-stu-id="a86bc-334">Prepare hello failback plan</span></span>
<span data-ttu-id="a86bc-335">您可以準備使用 vContinuum hello 應用程式可以在任何時間失敗後 toohello 在內部部署站台的容錯回復計劃。</span><span class="sxs-lookup"><span data-stu-id="a86bc-335">You can prepare a failback plan using vContinuum so that hello application can be failed back toohello on-premises site at any time.</span></span> <span data-ttu-id="a86bc-336">這些復原計劃會在站台復原中的非常類似 toohello 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="a86bc-336">These recovery plans are very similar toohello recovery plans in Site Recovery.</span></span>

1. <span data-ttu-id="a86bc-337">啟動 vContinuum，然後選取 [管理方案]  >  [復原]。</span><span class="sxs-lookup"><span data-stu-id="a86bc-337">Launch vContinuum and select **Manage plans** > **Recover.**</span></span> <span data-ttu-id="a86bc-338">您可以看到的所有 Vm 上已使用的 toofail hello 計劃清單。</span><span class="sxs-lookup"><span data-stu-id="a86bc-338">You can see of list of all hello plans that have been used toofail over VMs.</span></span> <span data-ttu-id="a86bc-339">您可以使用 hello 相同計劃 toorecover。</span><span class="sxs-lookup"><span data-stu-id="a86bc-339">You can use hello same plans toorecover.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image37.png)
2. <span data-ttu-id="a86bc-340">選取 hello 保護計劃和所有您想要在其中 toorecover Vm hello。</span><span class="sxs-lookup"><span data-stu-id="a86bc-340">Select hello protection plan and all of hello VMs you want toorecover in it.</span></span> <span data-ttu-id="a86bc-341">當您選取每個 VM，您可以查看更多詳細資料，包括 hello 目標 ESX 伺服器 hello 來源 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a86bc-341">When you select each VM you can see more details including hello target ESX server and hello source VM disk.</span></span> <span data-ttu-id="a86bc-342">按一下**下一步**toobegin hello 復原精靈 」，然後選取您想要 toorecover hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a86bc-342">Click **Next** toobegin hello Recover Wizard and select hello VMs you want toorecover.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image38.png)
3. <span data-ttu-id="a86bc-343">您可以復原根據多個選項，但我們建議您改用**最新標籤**並選取**套用之所有 Vm** tooensure hello hello 虛擬機器的最新資料，將會使用。</span><span class="sxs-lookup"><span data-stu-id="a86bc-343">You can recover based on multiple options but we recommend you use **Latest Tag** and select **Apply for All VMs** tooensure that hello latest data from hello virtual machine will be used.</span></span>
4. <span data-ttu-id="a86bc-344">執行 hello**整備檢查。**</span><span class="sxs-lookup"><span data-stu-id="a86bc-344">Run hello **Readiness Check.**</span></span> <span data-ttu-id="a86bc-345">這會檢查 hello 正確的參數是否已設定的 tooenable VM 復原。</span><span class="sxs-lookup"><span data-stu-id="a86bc-345">This will check if hello right parameters are configured tooenable VM recovery.</span></span> <span data-ttu-id="a86bc-346">按一下**下一步**如果所有的 hello 檢查成功。</span><span class="sxs-lookup"><span data-stu-id="a86bc-346">Click **Next** if all hello checks are successful.</span></span> <span data-ttu-id="a86bc-347">如果未檢查 hello 記錄檔，並解決 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="a86bc-347">If not check hello log and resolve hello errors.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image39.png)
5. <span data-ttu-id="a86bc-348">在**VM 組態**確定 hello 復原設定已正確設定。</span><span class="sxs-lookup"><span data-stu-id="a86bc-348">In **VM Configuration** ensure that hello recovery settings are correctly set.</span></span> <span data-ttu-id="a86bc-349">如果您需要您可以變更 hello VM 設定。</span><span class="sxs-lookup"><span data-stu-id="a86bc-349">You can change hello VM settings if you need to.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image40.png)
6. <span data-ttu-id="a86bc-350">檢閱虛擬機器，將會復原並指定復原順序 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="a86bc-350">Review hello list of virtual machines that will be recovered and specify a recovery order.</span></span> <span data-ttu-id="a86bc-351">請注意，Vm 會列出使用 hello 電腦主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a86bc-351">Note that VMs are listed using hello computer host name.</span></span> <span data-ttu-id="a86bc-352">可能很難 toomap hello 電腦主機名稱 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-352">It might be difficult toomap hello computer host name toohello virtual machine.</span></span>
   <span data-ttu-id="a86bc-353">toomap hello 名稱，請移 toohello 虛擬機器**儀表板**在 Azure 與核取 hello VM 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a86bc-353">toomap hello names, go toohello virtual machines **Dashboard** in Azure and check hello VM host name.</span></span>

    ![](./media/site-recovery-failback-azure-to-vmware/image41.png)
7. <span data-ttu-id="a86bc-354">指定方案名稱，然後選取 [稍後復原] 。</span><span class="sxs-lookup"><span data-stu-id="a86bc-354">Specify a plan name and select **Recover later**.</span></span> <span data-ttu-id="a86bc-355">我們建議 toorecover 稍後因為 hello 初始保護可能不完整。</span><span class="sxs-lookup"><span data-stu-id="a86bc-355">We recommend toorecover later since hello initial protection might not be complete.</span></span>
8. <span data-ttu-id="a86bc-356">按一下**復原**toosave hello 計劃或觸發程序 hello 復原如果您已選取 toorecover 現在和不更新版本。</span><span class="sxs-lookup"><span data-stu-id="a86bc-356">Click on **Recover** toosave hello plan or trigger hello recovery if you've selected toorecover now and not later.</span></span> <span data-ttu-id="a86bc-357">如果已儲存 hello 計劃，您可以檢查 hello 復原狀態 toosee。</span><span class="sxs-lookup"><span data-stu-id="a86bc-357">You can check hello recovery status toosee if hello plan's been saved.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image42.png)

   ![](./media/site-recovery-failback-azure-to-vmware/image43.png)

## <a name="recover-virtual-machines"></a><span data-ttu-id="a86bc-358">復原虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a86bc-358">Recover virtual machines</span></span>
<span data-ttu-id="a86bc-359">建立 hello 計劃之後，您可以復原 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-359">After hello plan's been created, you can recover hello virtual machines.</span></span> <span data-ttu-id="a86bc-360">之前您，請檢查該 hello 虛擬機器已完成同步處理。</span><span class="sxs-lookup"><span data-stu-id="a86bc-360">Before you do check that hello virtual machines have completed synchronization.</span></span> <span data-ttu-id="a86bc-361">如果複寫狀態會顯示 [確定]，完成 hello 保護，並已符合 hello RPO 臨界值。</span><span class="sxs-lookup"><span data-stu-id="a86bc-361">If replication status shows OK then hello protection is completed and hello RPO threshold has been met.</span></span> <span data-ttu-id="a86bc-362">您可以確認 hello VM 屬性中的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="a86bc-362">You can verify health in hello VM properties.</span></span>

![](./media/site-recovery-failback-azure-to-vmware/image44.png)

<span data-ttu-id="a86bc-363">關閉 hello Azure 虛擬機器才能起始 hello 復原。</span><span class="sxs-lookup"><span data-stu-id="a86bc-363">Turn off hello Azure virtual machines before you initiate hello recovery.</span></span> <span data-ttu-id="a86bc-364">這可確保沒有任何拆分，而且使用者將只能存取一份 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a86bc-364">This ensures there's no split brain and that users will only access one copy of hello application.</span></span>

1. <span data-ttu-id="a86bc-365">啟動 hello 儲存計劃。</span><span class="sxs-lookup"><span data-stu-id="a86bc-365">Start hello saved plan.</span></span> <span data-ttu-id="a86bc-366">在 vContinuum 選取**監視器**hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="a86bc-366">In vContinuum select **Monitor** hello plans.</span></span> <span data-ttu-id="a86bc-367">這樣就會列出所有已執行的 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="a86bc-367">This lists all hello plans that have been run.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image45.png)
2. <span data-ttu-id="a86bc-368">在選取的 hello 計劃**復原**按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="a86bc-368">Select hello plan in **Recovery** and click **Start**.</span></span> <span data-ttu-id="a86bc-369">您可以監視復原。</span><span class="sxs-lookup"><span data-stu-id="a86bc-369">You can monitor recovery.</span></span> <span data-ttu-id="a86bc-370">開啟 Vm 之後在您可以在此連接在 vCenter toothem。</span><span class="sxs-lookup"><span data-stu-id="a86bc-370">After VMs have been turned on you can connect toothem in vCenter.</span></span>

   ![](./media/site-recovery-failback-azure-to-vmware/image46.png)

## <a name="protect-tooazure-again-after-failback"></a><span data-ttu-id="a86bc-371">容錯回復之後，再次保護 tooAzure</span><span class="sxs-lookup"><span data-stu-id="a86bc-371">Protect tooAzure again after failback</span></span>
<span data-ttu-id="a86bc-372">容錯回復完成後您可能會想 tooprotect hello 虛擬機器一次。</span><span class="sxs-lookup"><span data-stu-id="a86bc-372">After failback has been completed you'll probably want tooprotect hello virtual machines again.</span></span> <span data-ttu-id="a86bc-373">以下列方式來執行此動作：</span><span class="sxs-lookup"><span data-stu-id="a86bc-373">Do this as follows:</span></span>

1. <span data-ttu-id="a86bc-374">請檢查正在 hello 虛擬機器內部部署和應用程式都可以連線。</span><span class="sxs-lookup"><span data-stu-id="a86bc-374">Check that hello virtual machines on-premises are working and that applications are reachable.</span></span>
2. <span data-ttu-id="a86bc-375">Hello Azure Site Recovery 入口網站中，選取 hello 的虛擬機器，然後予以刪除。</span><span class="sxs-lookup"><span data-stu-id="a86bc-375">In hello Azure Site Recovery portal, select hello virtual machines and delete them.</span></span> <span data-ttu-id="a86bc-376">選取 toodisable hello 保護 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-376">Select toodisable hello protection of hello virtual machines.</span></span> <span data-ttu-id="a86bc-377">這可確保不會再保護 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a86bc-377">This ensures that hello VMs are no more protected.</span></span>
3. <span data-ttu-id="a86bc-378">在 Azure 中刪除 hello 無法透過 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a86bc-378">In Azure delete hello failed over Azure virtual machines</span></span>
4. <span data-ttu-id="a86bc-379">刪除上 vSpehere hello 舊虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a86bc-379">Delete hello old virtual machine on vSpehere.</span></span> <span data-ttu-id="a86bc-380">這些是您先前容錯 tooAzure 的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a86bc-380">These are hello VMs that you previously failed over tooAzure.</span></span>
5. <span data-ttu-id="a86bc-381">在 hello Site Recovery 入口網站中保護 hello 最近容錯移轉的 Vm。</span><span class="sxs-lookup"><span data-stu-id="a86bc-381">In hello Site Recovery portal protect hello VMs that recently failed over.</span></span> <span data-ttu-id="a86bc-382">它們受保護之後您可以將它們 tooa 復原計劃。</span><span class="sxs-lookup"><span data-stu-id="a86bc-382">After they're protected  you can add them tooa recovery plan.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a86bc-383">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a86bc-383">Next steps</span></span>
* <span data-ttu-id="a86bc-384">[閱讀有關](site-recovery-vmware-to-azure-classic.md)複寫 VMware 虛擬機器和實體伺服器 tooAzure 使用增強的 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="a86bc-384">[Read about](site-recovery-vmware-to-azure-classic.md) replicating VMware virtual machines and physical servers tooAzure using hello enhanced deployment.</span></span>
