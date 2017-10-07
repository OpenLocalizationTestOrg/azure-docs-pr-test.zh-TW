---
title: "使用負載平衡集 aaaClusterize MySQL |Microsoft 文件"
description: "設定負載平衡、 高可用性與 hello 傳統部署模型，在 Azure 上建立 Linux MySQL 叢集"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="2855c-103">使用 Linux 上的負載平衡集 tooclusterize MySQL</span><span class="sxs-lookup"><span data-stu-id="2855c-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2855c-104">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="2855c-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="2855c-105">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="2855c-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="2855c-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="2855c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="2855c-107">A [Resource Manager 範本](https://azure.microsoft.com/documentation/templates/mysql-replication/)時才能使用需要 toodeploy MySQL 叢集。</span><span class="sxs-lookup"><span data-stu-id="2855c-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="2855c-108">這篇文章探討，並說明 hello 不同的方法可用 toodeploy 高可用性以 Linux 為基礎的服務在 Microsoft Azure 中，瀏覽做為入門的 MySQL Server 高可用性。</span><span class="sxs-lookup"><span data-stu-id="2855c-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="2855c-109">您可在 [第 9 頻道](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)(英文) 上找到說明此方法的影片。</span><span class="sxs-lookup"><span data-stu-id="2855c-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="2855c-110">我們會依據 DRBD、Corosync 和 Pacemaker，說明無共用、兩個節點、單一主要的 MySQL 高可用性解決方案。</span><span class="sxs-lookup"><span data-stu-id="2855c-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="2855c-111">一次只會有一個節點執行 MySQL。</span><span class="sxs-lookup"><span data-stu-id="2855c-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="2855c-112">讀取和寫入從 hello DRBD 資源也是有限的 tooonly 一個節點一次。</span><span class="sxs-lookup"><span data-stu-id="2855c-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="2855c-113">沒有 LVS，像是 VIP 解決方案需要，因為您將使用在 Microsoft Azure tooprovide 循環配置資源的功能和端點偵測、 移除和依正常程序復原 hello VIP 的負載平衡集。</span><span class="sxs-lookup"><span data-stu-id="2855c-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="2855c-114">hello VIP 是指派的 Microsoft Azure，當您初次建立 hello 雲端服務的全域路由傳送 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="2855c-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="2855c-115">還有其他可能架構可供 MySQL 使用，包括 NBD 叢集、Percona、Galera 以及數種中繼軟體解決方案 (包括至少有一個可作為 [VM Depot](http://vmdepot.msopentech.com) 上的 VM)。</span><span class="sxs-lookup"><span data-stu-id="2855c-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="2855c-116">只要這些解決方案可以複寫在單點傳播與多點傳送或廣播，而不依賴共用存放裝置或多個網路介面，hello 案例應該在 Microsoft Azure 上的簡單 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="2855c-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="2855c-117">這些叢集架構可以延伸 tooother 產品，例如 PostgreSQL 和 OpenLDAP 不要以類似的方式。</span><span class="sxs-lookup"><span data-stu-id="2855c-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="2855c-118">例如，已透過多個主要 OpenLDAP 成功測試使用無共用的負載平衡程序，您可以在我們的第 9 頻道 (Channel 9) 部落格上觀看此測試。</span><span class="sxs-lookup"><span data-stu-id="2855c-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="2855c-119">準備就緒</span><span class="sxs-lookup"><span data-stu-id="2855c-119">Get ready</span></span>
<span data-ttu-id="2855c-120">您需要 hello 下列資源與能力：</span><span class="sxs-lookup"><span data-stu-id="2855c-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="2855c-121">Microsoft Azure 帳戶與有效的訂閱，無法 toocreate 至少兩個 Vm （XS 已在此範例中使用）</span><span class="sxs-lookup"><span data-stu-id="2855c-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="2855c-122">網路和子網路</span><span class="sxs-lookup"><span data-stu-id="2855c-122">A network and a subnet</span></span>
  - <span data-ttu-id="2855c-123">同質群組</span><span class="sxs-lookup"><span data-stu-id="2855c-123">An affinity group</span></span>
  - <span data-ttu-id="2855c-124">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="2855c-124">An availability set</span></span>
  - <span data-ttu-id="2855c-125">hello 能力 toocreate Vhd 在 hello 與 hello 雲端服務相同的區域，並且將它們附加 toohello Linux Vm</span><span class="sxs-lookup"><span data-stu-id="2855c-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="2855c-126">測試環境</span><span class="sxs-lookup"><span data-stu-id="2855c-126">Tested environment</span></span>
* <span data-ttu-id="2855c-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="2855c-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="2855c-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="2855c-128">DRBD</span></span>
  * <span data-ttu-id="2855c-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="2855c-129">MySQL Server</span></span>
  * <span data-ttu-id="2855c-130">Corosync 和 Pacemaker</span><span class="sxs-lookup"><span data-stu-id="2855c-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="2855c-131">同質群組</span><span class="sxs-lookup"><span data-stu-id="2855c-131">Affinity group</span></span>
<span data-ttu-id="2855c-132">登入 toohello Azure 傳統入口網站建立同質群組 hello 解決方案選取**設定**，以及建立同質群組。</span><span class="sxs-lookup"><span data-stu-id="2855c-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="2855c-133">配置的資源建立稍後將會指派 toothis 同質群組。</span><span class="sxs-lookup"><span data-stu-id="2855c-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="2855c-134">網路</span><span class="sxs-lookup"><span data-stu-id="2855c-134">Networks</span></span>
<span data-ttu-id="2855c-135">建立新的網路時，並在 hello 網路內建立子網路。</span><span class="sxs-lookup"><span data-stu-id="2855c-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="2855c-136">此範例使用內部只有一個 /24 子網路的 10.10.10.0/24 網路。</span><span class="sxs-lookup"><span data-stu-id="2855c-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="2855c-137">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2855c-137">Virtual machines</span></span>
<span data-ttu-id="2855c-138">第一個 Ubuntu 13.10 VM 建立使用 Endorsed Ubuntu 圖庫映像，並呼叫的 hello `hadb01`。</span><span class="sxs-lookup"><span data-stu-id="2855c-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="2855c-139">Hello 處理程序稱為 hadb 中建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2855c-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="2855c-140">這個名稱會說明 hello 共用，請加入更多資源時，會有 hello 服務的負載平衡本質。</span><span class="sxs-lookup"><span data-stu-id="2855c-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="2855c-141">hello 建立`hadb01`使用 hello 入口網站是較為簡單和已完成。</span><span class="sxs-lookup"><span data-stu-id="2855c-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="2855c-142">SSH 的端點會自動建立，並已選取 hello 新網路。</span><span class="sxs-lookup"><span data-stu-id="2855c-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="2855c-143">現在您可以建立可用性設定組 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="2855c-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="2855c-144">Hello （技術上來說，建立 hello 雲端服務） 時，會建立第一個 VM 之後, 建立 hello 第二個 VM， `hadb02`。</span><span class="sxs-lookup"><span data-stu-id="2855c-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="2855c-145">Hello 第二個 VM、 hello 圖庫使用 Ubuntu 13.10 VM，請使用 hello 入口網站，但使用現有的雲端服務， `hadb.cloudapp.net`，而不是建立一個新。</span><span class="sxs-lookup"><span data-stu-id="2855c-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="2855c-146">應該會自動選取 hello 網路和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2855c-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="2855c-147">並建立 SSH 端點。</span><span class="sxs-lookup"><span data-stu-id="2855c-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="2855c-148">建立兩個 Vm 之後，記下 hello SSH 連接埠`hadb01`(TCP 22) 和`hadb02`（自動由 Azure 指派）。</span><span class="sxs-lookup"><span data-stu-id="2855c-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="2855c-149">連接的儲存體</span><span class="sxs-lookup"><span data-stu-id="2855c-149">Attached storage</span></span>
<span data-ttu-id="2855c-150">連接新的磁碟 tooboth Vm，然後在 hello 程序中建立 5 GB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="2855c-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="2855c-151">hello 磁碟會裝載於您的主要作業系統磁碟的使用中的 hello VHD 容器。</span><span class="sxs-lookup"><span data-stu-id="2855c-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="2855c-152">建立並附加磁碟之後，沒有任何需要 toorestart Linux 因為 hello 核心會看到 hello 新裝置。</span><span class="sxs-lookup"><span data-stu-id="2855c-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="2855c-153">此裝置通常是 `/dev/sdc`。</span><span class="sxs-lookup"><span data-stu-id="2855c-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="2855c-154">請檢查`dmesg`hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="2855c-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="2855c-155">在每個 VM 上建立的分割區使用`cfdisk`（主要 Linux 磁碟分割） 和寫入 hello 新磁碟分割表格。</span><span class="sxs-lookup"><span data-stu-id="2855c-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="2855c-156">請勿在此磁碟分割上建立檔案系統。</span><span class="sxs-lookup"><span data-stu-id="2855c-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="2855c-157">設定 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="2855c-157">Set up hello cluster</span></span>
<span data-ttu-id="2855c-158">在這兩個 Ubuntu Vm 上使用 APT tooinstall Corosync、 Pacemaker 和 DRBD。</span><span class="sxs-lookup"><span data-stu-id="2855c-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="2855c-159">toodo 因此與`apt-get`，請執行 hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="2855c-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="2855c-160">此時請勿安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="2855c-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="2855c-161">Debian 和 Ubuntu 安裝指令碼將會在初始化 MySQL 資料目錄`/var/lib/mysql`，但是因為 hello 目錄將會取代 DRBD 檔案系統中，您需要稍後 tooinstall MySQL。</span><span class="sxs-lookup"><span data-stu-id="2855c-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="2855c-162">驗證 (使用`/sbin/ifconfig`)，這兩個 Vm 使用 hello 10.10.10.0/24 子網路中的位址，及它們可以依照名稱 ping 彼此。</span><span class="sxs-lookup"><span data-stu-id="2855c-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="2855c-163">您也可以使用`ssh-keygen`和`ssh-copy-id`toomake 確定這兩個 Vm 可透過 SSH 通訊而不需要密碼。</span><span class="sxs-lookup"><span data-stu-id="2855c-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="2855c-164">設定 DRBD</span><span class="sxs-lookup"><span data-stu-id="2855c-164">Set up DRBD</span></span>
<span data-ttu-id="2855c-165">建立會使用基礎 hello DRBD 資源`/dev/sdc1`分割 tooproduce`/dev/drbd1`可以使用 ext3 格式化，並在主要和次要節點中使用的資源。</span><span class="sxs-lookup"><span data-stu-id="2855c-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="2855c-166">開啟`/etc/drbd.d/r0.res`並複製 hello 遵循這兩個 Vm 上的資源定義：</span><span class="sxs-lookup"><span data-stu-id="2855c-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="2855c-167">使用初始化 hello 資源`drbdadm`這兩個 Vm 上：</span><span class="sxs-lookup"><span data-stu-id="2855c-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="2855c-168">在 hello 主要 VM (`hadb01`)，強制的 hello DRBD 資源的擁有權 （主要）：</span><span class="sxs-lookup"><span data-stu-id="2855c-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="2855c-169">如果您檢查/proc/drbd hello 內容 (`sudo cat /proc/drbd`) 在這兩個 Vm，您應該看到`Primary/Secondary`上`hadb01`和`Secondary/Primary`上`hadb02`、 與 hello 方案此時一致。</span><span class="sxs-lookup"><span data-stu-id="2855c-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="2855c-170">hello 5 GB 的磁碟會透過任何費用 toocustomers hello 10.10.10.0/24 網路同步處理。</span><span class="sxs-lookup"><span data-stu-id="2855c-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="2855c-171">同步處理 hello 磁碟之後，您可以建立 hello 檔案系統上`hadb01`。</span><span class="sxs-lookup"><span data-stu-id="2855c-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="2855c-172">為了測試用途，我們使用 ext2，但 hello 下列程式碼會建立 ext3 檔案系統：</span><span class="sxs-lookup"><span data-stu-id="2855c-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="2855c-173">掛接 hello DRBD 資源</span><span class="sxs-lookup"><span data-stu-id="2855c-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="2855c-174">您現在準備好 toomount hello DRBD 資源`hadb01`。</span><span class="sxs-lookup"><span data-stu-id="2855c-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="2855c-175">Debian 及其衍生版本會使用 `/var/lib/mysql` 做為 MySQL 的資料目錄。</span><span class="sxs-lookup"><span data-stu-id="2855c-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="2855c-176">因為您尚未安裝 MySQL，請建立 hello 目錄，並掛接 hello DRBD 資源。</span><span class="sxs-lookup"><span data-stu-id="2855c-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="2855c-177">tooperform 這個選項時，執行下列程式碼的 hello `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="2855c-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="2855c-178">設定 MySQL</span><span class="sxs-lookup"><span data-stu-id="2855c-178">Set up MySQL</span></span>
<span data-ttu-id="2855c-179">現在您已準備好 tooinstall MySQL 上`hadb01`:</span><span class="sxs-lookup"><span data-stu-id="2855c-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="2855c-180">在 `hadb02`中，您有兩個選擇。</span><span class="sxs-lookup"><span data-stu-id="2855c-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="2855c-181">您可以安裝 mysql 伺服器，這樣會建立 /var/lib/mysql，填入新的資料目錄，然後移除 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="2855c-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="2855c-182">tooperform 這個選項時，執行下列程式碼的 hello `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="2855c-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="2855c-183">hello 第二個選項太 toofailover`hadb02`並安裝 mysql 伺服器那里。</span><span class="sxs-lookup"><span data-stu-id="2855c-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="2855c-184">安裝指令碼將會注意到 hello 現有安裝，並不會修改它。</span><span class="sxs-lookup"><span data-stu-id="2855c-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="2855c-185">執行 hello 下列程式碼上`hadb01`:</span><span class="sxs-lookup"><span data-stu-id="2855c-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="2855c-186">執行 hello 下列程式碼上`hadb02`:</span><span class="sxs-lookup"><span data-stu-id="2855c-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="2855c-187">如果您現在不打算 toofailover DRBD，hello 第一個選項是雖然論證那麼漂亮更容易。</span><span class="sxs-lookup"><span data-stu-id="2855c-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="2855c-188">安裝完成後，您可以開始使用 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="2855c-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="2855c-189">執行 hello 下列程式碼上`hadb02`（或任一個的 hello 伺服器是作用中，根據 tooDRBD）：</span><span class="sxs-lookup"><span data-stu-id="2855c-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="2855c-190">這個最後一個陳述式即可有效停用此資料表中的 hello 根使用者的驗證。</span><span class="sxs-lookup"><span data-stu-id="2855c-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="2855c-191">這應由您的生產等級 GRANT 陳述式取代，這裡僅是為了說明的目的才包括此陳述式。</span><span class="sxs-lookup"><span data-stu-id="2855c-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="2855c-192">如果您想從外部 hello Vm （這是本指南用途 hello） toomake 查詢時，您也需要 tooenable MySQL 的網路功能。</span><span class="sxs-lookup"><span data-stu-id="2855c-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="2855c-193">在這兩個 Vm 上開啟`/etc/mysql/my.cnf`並移過`bind-address`。</span><span class="sxs-lookup"><span data-stu-id="2855c-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="2855c-194">變更 hello 位址 127.0.0.1 從 too0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="2855c-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="2855c-195">在儲存 hello 檔案之後, 發出`sudo service mysql restart`您目前的主要伺服器上。</span><span class="sxs-lookup"><span data-stu-id="2855c-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="2855c-196">建立 hello MySQL 負載平衡集</span><span class="sxs-lookup"><span data-stu-id="2855c-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="2855c-197">返回 toohello 入口網站，請移過`hadb01`，然後選擇 **端點**。</span><span class="sxs-lookup"><span data-stu-id="2855c-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="2855c-198">toocreate 的端點，選擇 MySQL (TCP 3306) hello 下拉式清單並選取從**建立新的負載平衡集**。</span><span class="sxs-lookup"><span data-stu-id="2855c-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="2855c-199">名稱 hello 負載平衡的端點`lb-mysql`。</span><span class="sxs-lookup"><span data-stu-id="2855c-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="2855c-200">設定**時間**too5 秒，最小值。</span><span class="sxs-lookup"><span data-stu-id="2855c-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="2855c-201">建立 hello 端點之後，請繼續太`hadb02`，選擇**端點**，並建立端點。</span><span class="sxs-lookup"><span data-stu-id="2855c-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="2855c-202">選擇`lb-mysql`，然後從 hello 下拉式清單中選取 MySQL。</span><span class="sxs-lookup"><span data-stu-id="2855c-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="2855c-203">您也可以使用 Azure CLI hello 這個步驟。</span><span class="sxs-lookup"><span data-stu-id="2855c-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="2855c-204">您現在可以 hello 叢集的手動作業所需的所有項目。</span><span class="sxs-lookup"><span data-stu-id="2855c-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="2855c-205">測試 hello 負載平衡集</span><span class="sxs-lookup"><span data-stu-id="2855c-205">Test hello load-balanced set</span></span>
<span data-ttu-id="2855c-206">您可以使用任何 MySQL 用戶端，或使用特定應用程式 (例如以 Azure 網站身分執行的 phpMyAdmin)，從機器外部執行測試。</span><span class="sxs-lookup"><span data-stu-id="2855c-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="2855c-207">在此案例中，您在另一個 Linux 方塊上使用 MySQL 的命令列工具：</span><span class="sxs-lookup"><span data-stu-id="2855c-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="2855c-208">手動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="2855c-208">Manually failing over</span></span>
<span data-ttu-id="2855c-209">您可以透過關閉 MySQL、切換 DRBD 的主要 VM，然後重新啟動 MySQL 來模擬容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="2855c-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="2855c-210">tooperform 這個工作中，執行下列程式碼上 hadb01 hello:</span><span class="sxs-lookup"><span data-stu-id="2855c-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="2855c-211">接著，在 hadb02 上：</span><span class="sxs-lookup"><span data-stu-id="2855c-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="2855c-212">手動容錯移轉後，您可以重複遠端查詢，它應可正常運作。</span><span class="sxs-lookup"><span data-stu-id="2855c-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="2855c-213">設定 Corosync</span><span class="sxs-lookup"><span data-stu-id="2855c-213">Set up Corosync</span></span>
<span data-ttu-id="2855c-214">Corosync 是所需的 Pacemaker toowork hello 基礎叢集基礎結構。</span><span class="sxs-lookup"><span data-stu-id="2855c-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="2855c-215">活動訊號 （和其他方法，例如 Ultramonkey） Corosync 對於分割的 hello CRM 功能，Pacemaker 仍比較類似 tooHeartbeat 功能時。</span><span class="sxs-lookup"><span data-stu-id="2855c-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="2855c-216">hello 主要條件約束 Corosync 在 Azure 上的是 Corosync 慣用透過廣播多點傳送透過單點傳播通訊，但 Microsoft Azure 網路只支援單點傳播。</span><span class="sxs-lookup"><span data-stu-id="2855c-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="2855c-217">還好，Corosync 具備有效的單點傳送模式。</span><span class="sxs-lookup"><span data-stu-id="2855c-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="2855c-218">hello 唯一實際的條件約束是，因為所有節點並未在彼此都通訊，您需要 toodefine hello 節點在您的組態檔，包括其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2855c-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="2855c-219">單點傳播與變更繫結位址、 節點清單，以及記錄目錄，我們可以使用 hello Corosync 範例檔案 (使用 Ubuntu `/var/log/corosync` hello 範例檔案使用時`/var/log/cluster`)，並啟用仲裁工具。</span><span class="sxs-lookup"><span data-stu-id="2855c-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="2855c-220">使用下列 hello`transport: udpu`指示詞和 hello 手動定義兩個節點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2855c-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="2855c-221">執行 hello 下列程式碼上`/etc/corosync/corosync.conf`兩個節點：</span><span class="sxs-lookup"><span data-stu-id="2855c-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="2855c-222">複製兩部 VM 上的這個組態檔，並在這兩個節點中啟動 Corosync：</span><span class="sxs-lookup"><span data-stu-id="2855c-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="2855c-223">後，馬上開始 hello 服務，hello 叢集應該建立 hello 目前環形，而且應該 constituted 仲裁。</span><span class="sxs-lookup"><span data-stu-id="2855c-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="2855c-224">我們可以檢查這項功能，藉由檢閱記錄檔，或藉由執行下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="2855c-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="2855c-225">您會看到下列映像的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="2855c-225">You will see output similar toohello following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="2855c-227">設定 Pacemaker</span><span class="sxs-lookup"><span data-stu-id="2855c-227">Set up Pacemaker</span></span>
<span data-ttu-id="2855c-228">Pacemaker 使用 hello 資源的叢集 toomonitor、 定義主要複本會跟著中斷，並切換這些資源 toosecondaries。</span><span class="sxs-lookup"><span data-stu-id="2855c-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="2855c-229">在所有其他選擇中，您可從一組可用指令碼或從 LSB (如 init) 指令碼來定義資源。</span><span class="sxs-lookup"><span data-stu-id="2855c-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="2855c-230">我們想要 Pacemaker 太"自己的"hello DRBD 資源、 hello 掛接點，以及 hello MySQL 服務。</span><span class="sxs-lookup"><span data-stu-id="2855c-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="2855c-231">如果 Pacemaker 可以開啟和關閉 DRBD，掛接和卸載，並再啟動和停止 MySQL 中 hello 向右的順序不正確的項目時，即會發生以 hello 主要安裝程式完成。</span><span class="sxs-lookup"><span data-stu-id="2855c-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="2855c-232">首次安裝 Pacemaker 時，您的組態應十分簡單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2855c-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="2855c-233">執行檢查 hello 組態`sudo crm configure show`。</span><span class="sxs-lookup"><span data-stu-id="2855c-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="2855c-234">然後建立檔案 (例如`/tmp/cluster.conf`) 以 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="2855c-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="2855c-235">Hello 檔案載入 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="2855c-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="2855c-236">您只需要 toodo 這在一個節點。</span><span class="sxs-lookup"><span data-stu-id="2855c-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="2855c-237">請確定開機時會啟動兩個節點的 Pacemaker：</span><span class="sxs-lookup"><span data-stu-id="2855c-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="2855c-238">使用`sudo crm_mon –L`，確認其中一個節點已經成為 hello hello 叢集主機，並正在 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2855c-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="2855c-239">您可以使用裝載與 ps toocheck hello 資源正在執行。</span><span class="sxs-lookup"><span data-stu-id="2855c-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="2855c-240">下列螢幕擷取畫面顯示 hello`crm_mon`具有一個節點停止 （藉由選取 Ctrl + C 結束）：</span><span class="sxs-lookup"><span data-stu-id="2855c-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="2855c-242">此快照說明兩個節點 (一個主要和一個從屬)：</span><span class="sxs-lookup"><span data-stu-id="2855c-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="2855c-244">測試</span><span class="sxs-lookup"><span data-stu-id="2855c-244">Testing</span></span>
<span data-ttu-id="2855c-245">您已準備好開始自動容錯移轉模擬。</span><span class="sxs-lookup"><span data-stu-id="2855c-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="2855c-246">有兩種方式 toodo 這： 彈性和固定。</span><span class="sxs-lookup"><span data-stu-id="2855c-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="2855c-247">hello 彈性的方式使用 hello 叢集關機函式： ``crm_standby -U `uname -n` -v on``。</span><span class="sxs-lookup"><span data-stu-id="2855c-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="2855c-248">如果您使用 hello 主機上，hello 從屬會高於。</span><span class="sxs-lookup"><span data-stu-id="2855c-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="2855c-249">請記住 tooset 這個回復 toooff。</span><span class="sxs-lookup"><span data-stu-id="2855c-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="2855c-250">如果不這麼做，crm_mon 會顯示一個待命中的節點。</span><span class="sxs-lookup"><span data-stu-id="2855c-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="2855c-251">hello 不易正在關機而關閉 hello 主要 VM (hadb01) 透過 hello 入口網站，或變更 hello 層上 hello VM，也就是停止 (關機）。</span><span class="sxs-lookup"><span data-stu-id="2855c-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="2855c-252">這有助於 Corosync 和 Pacemaker 信號向該 hello 為主版頁面的進行。</span><span class="sxs-lookup"><span data-stu-id="2855c-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="2855c-253">您可以測試這種情況 （適用於維護期間），但您也可以強制 hello 案例凍結 hello VM。</span><span class="sxs-lookup"><span data-stu-id="2855c-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="2855c-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="2855c-254">STONITH</span></span>
<span data-ttu-id="2855c-255">它應該是可能 tooissue hello Azure CLI 就不需 STONITH 指令碼可控制實體裝置透過 VM 關機。</span><span class="sxs-lookup"><span data-stu-id="2855c-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="2855c-256">您可以使用`/usr/lib/stonith/plugins/external/ssh`做為基底和啟用 STONITH hello 叢集組態中的。</span><span class="sxs-lookup"><span data-stu-id="2855c-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="2855c-257">Azure CLI 應該全域安裝，而且 hello 發行設定和設定檔應該要載入的 hello 叢集的使用者。</span><span class="sxs-lookup"><span data-stu-id="2855c-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="2855c-258">Hello 資源的範例程式碼位於[GitHub](https://github.com/bureado/aztonith)。</span><span class="sxs-lookup"><span data-stu-id="2855c-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="2855c-259">加入 hello 太之後變更 hello 叢集設定`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="2855c-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="2855c-260">hello 指令碼不會執行向上/向下檢查。</span><span class="sxs-lookup"><span data-stu-id="2855c-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="2855c-261">hello 原始 SSH 資源 15 ping 檢查，但 Azure VM 的復原時間可能是多個變數。</span><span class="sxs-lookup"><span data-stu-id="2855c-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="2855c-262">限制</span><span class="sxs-lookup"><span data-stu-id="2855c-262">Limitations</span></span>
<span data-ttu-id="2855c-263">hello 下列限制適用於：</span><span class="sxs-lookup"><span data-stu-id="2855c-263">hello following limitations apply:</span></span>

* <span data-ttu-id="2855c-264">hello linbit DRBD 資源指令碼為 Pacemaker 使用中的資源管理 DRBD`drbdadm down`時關閉一個節點，即使 hello 節點就會處於待命狀態。</span><span class="sxs-lookup"><span data-stu-id="2855c-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="2855c-265">因為 hello 從屬不需要同步處理 hello DRBD 資源 hello master 取得寫入時，這並不理想。</span><span class="sxs-lookup"><span data-stu-id="2855c-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="2855c-266">如果 hello master 不 graciously 失敗，hello 從屬伺服器可以接管較舊的檔案系統狀態。</span><span class="sxs-lookup"><span data-stu-id="2855c-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="2855c-267">可能解決此問題的方法有兩種：</span><span class="sxs-lookup"><span data-stu-id="2855c-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="2855c-268">在所有叢集節點中透過本機 (未叢集化) 看門狗強制執行 `drbdadm up r0`</span><span class="sxs-lookup"><span data-stu-id="2855c-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="2855c-269">編輯 hello linbit DRBD 指令碼，並確定`down`中不會呼叫`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="2855c-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="2855c-270">hello 負載平衡器需要至少五秒 toorespond，讓應用程式應該是叢集感知，而且可以容許更多的逾時。</span><span class="sxs-lookup"><span data-stu-id="2855c-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="2855c-271">其他架構也可提供協助，例如應用程式內部佇列、查詢中繼軟體等。</span><span class="sxs-lookup"><span data-stu-id="2855c-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="2855c-272">MySQL 微調是寫入可管理的速度完成的必要 tooensure 而快取為可能 toominimize 記憶體遺失經常會排清的 toodisk。</span><span class="sxs-lookup"><span data-stu-id="2855c-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="2855c-273">寫入效能是在 VM 中相依互連 hello 虛擬交換器，因為這是 hello DRBD tooreplicate hello 裝置使用的機制。</span><span class="sxs-lookup"><span data-stu-id="2855c-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
