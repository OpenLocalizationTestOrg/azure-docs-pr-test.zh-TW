---
title: "使用負載平衡集將 MySQL 叢集化 | Microsoft Docs"
description: "在 Azure 上安裝以傳統部署模型建立的負載平衡、高可用性 Linux MySQL 叢集"
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
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="6f7a2-103">在 Linux 上使用負載平衡集合將 MySQL 叢集化</span><span class="sxs-lookup"><span data-stu-id="6f7a2-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f7a2-104">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="6f7a2-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="6f7a2-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="6f7a2-107">如果您需要部署 MySQL 叢集，則可取得 [Resource Manager 範本](https://azure.microsoft.com/documentation/templates/mysql-replication/)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="6f7a2-108">本文探索與說明要在 Microsoft Azure 上部署高度可用 Linux 架構服務的其他可用方法，首先從 MySQL Server 高可用性開始。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="6f7a2-109">您可在 [第 9 頻道](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)(英文) 上找到說明此方法的影片。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="6f7a2-110">我們會依據 DRBD、Corosync 和 Pacemaker，說明無共用、兩個節點、單一主要的 MySQL 高可用性解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="6f7a2-111">一次只會有一個節點執行 MySQL。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="6f7a2-112">也限制一次只會有一個節點從 DRBD 資源讀取和寫入。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="6f7a2-113">因為您將使用 Microsoft Azure 中的負載平衡集合，來提供循環配置資源功能和 VIP 的端點偵測、移除及正常復原，所以不需要 VIP 解決方案 (如 LVS)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="6f7a2-114">VIP 是一個可全域路由的 IPv4 位址，會在您第一次建立雲端服務時由 Microsoft Azure 指定。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="6f7a2-115">還有其他可能架構可供 MySQL 使用，包括 NBD 叢集、Percona、Galera 以及數種中繼軟體解決方案 (包括至少有一個可作為 [VM Depot](http://vmdepot.msopentech.com) 上的 VM)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="6f7a2-116">只要這些解決方案可以在單點傳送與多點傳送上複寫或廣播，且不仰賴共用儲存體或多個網路介面，那麼應不難在 Microsoft Azure 上部署這些案例。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="6f7a2-117">您可以將這些叢集架構以類似的方式延伸到其他產品，如 PostgreSQL 和 OpenLDAP。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="6f7a2-118">例如，已透過多個主要 OpenLDAP 成功測試使用無共用的負載平衡程序，您可以在我們的第 9 頻道 (Channel 9) 部落格上觀看此測試。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="6f7a2-119">準備就緒</span><span class="sxs-lookup"><span data-stu-id="6f7a2-119">Get ready</span></span>
<span data-ttu-id="6f7a2-120">您需要下列資源和功能：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="6f7a2-121">具備有效訂用帳戶的 Microsoft Azure 帳戶，能夠建立至少兩個 VM (在此範例中使用 XS)</span><span class="sxs-lookup"><span data-stu-id="6f7a2-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="6f7a2-122">網路和子網路</span><span class="sxs-lookup"><span data-stu-id="6f7a2-122">A network and a subnet</span></span>
  - <span data-ttu-id="6f7a2-123">同質群組</span><span class="sxs-lookup"><span data-stu-id="6f7a2-123">An affinity group</span></span>
  - <span data-ttu-id="6f7a2-124">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="6f7a2-124">An availability set</span></span>
  - <span data-ttu-id="6f7a2-125">能夠在與雲端服務相同的區域中建立 VHD，並將它們連接至 Linux VM</span><span class="sxs-lookup"><span data-stu-id="6f7a2-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="6f7a2-126">測試環境</span><span class="sxs-lookup"><span data-stu-id="6f7a2-126">Tested environment</span></span>
* <span data-ttu-id="6f7a2-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="6f7a2-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="6f7a2-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="6f7a2-128">DRBD</span></span>
  * <span data-ttu-id="6f7a2-129">MySQL Server</span><span class="sxs-lookup"><span data-stu-id="6f7a2-129">MySQL Server</span></span>
  * <span data-ttu-id="6f7a2-130">Corosync 和 Pacemaker</span><span class="sxs-lookup"><span data-stu-id="6f7a2-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="6f7a2-131">同質群組</span><span class="sxs-lookup"><span data-stu-id="6f7a2-131">Affinity group</span></span>
<span data-ttu-id="6f7a2-132">建立解決方案的同質群組，方法是登入 Azure 傳統入口網站，選取 [設定]，然後建立同質群組。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="6f7a2-133">並將稍後建立的配置資源指派給此同質群組。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="6f7a2-134">網路</span><span class="sxs-lookup"><span data-stu-id="6f7a2-134">Networks</span></span>
<span data-ttu-id="6f7a2-135">建立新網路，並在該網路內建立一個子網路。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="6f7a2-136">此範例使用內部只有一個 /24 子網路的 10.10.10.0/24 網路。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="6f7a2-137">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6f7a2-137">Virtual machines</span></span>
<span data-ttu-id="6f7a2-138">使用經過背書的 Ubuntu 映像庫映像來建立第一個 Ubuntu 13.10 VM，並將它命名為 `hadb01`。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="6f7a2-139">在此程序中會建立一個名為 hadb 的新雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="6f7a2-140">此名稱可說明新增更多資源時，服務將具備的共用、負載平衡性質。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="6f7a2-141">已使用入口網站順利完成建立 `hadb01`。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="6f7a2-142">系統會自動建立 SSH 的端點，並選取新的網路。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="6f7a2-143">您可以為 VM 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="6f7a2-144">建立第一個 VM 後 (從技術角度來看，也就是建立雲端服務時)，我們會建立第二個 VM `hadb02`。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="6f7a2-145">在第二個 VM 中，透過入口網站使用資源庫中的 Ubuntu 13.10 VM，但使用現有的雲端服務 `hadb.cloudapp.net`，而非建立新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="6f7a2-146">系統應會自動選取網路和可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="6f7a2-147">並建立 SSH 端點。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="6f7a2-148">在建立這兩部 VM 之後，請記下 `hadb01` 的 SSH 連接埠 (TCP 22) 及 `hadb02` (由 Azure 自動指派)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="6f7a2-149">連接的儲存體</span><span class="sxs-lookup"><span data-stu-id="6f7a2-149">Attached storage</span></span>
<span data-ttu-id="6f7a2-150">將新磁碟連接至這兩部 VM，並在此程序中建立 5 GB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="6f7a2-151">這些磁碟將在 VHD 容器中託管，並供我們的主要作業系統磁碟使用。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="6f7a2-152">在建立並連接磁碟後，我們不需要重新啟動 Linux，因為核心將會看到新裝置。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="6f7a2-153">此裝置通常是 `/dev/sdc`。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="6f7a2-154">檢查輸出的 `dmesg`。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="6f7a2-155">在每個 VM 上，使用 `cfdisk` 建立磁碟分割 (主要是 Linux 磁碟分割)，並寫入新的磁碟分割資料表。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="6f7a2-156">請勿在此磁碟分割上建立檔案系統。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="6f7a2-157">設定叢集</span><span class="sxs-lookup"><span data-stu-id="6f7a2-157">Set up the cluster</span></span>
<span data-ttu-id="6f7a2-158">在這兩部 Ubuntu VM 上使用 APT 來安裝 Corosync、Pacemaker 和 DRBD。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="6f7a2-159">若要利用 `apt-get` 這麼做，請執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="6f7a2-160">此時請勿安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="6f7a2-161">Debian 和 Ubuntu 安裝指令碼將會初始化 `/var/lib/mysql` 上的 MySQL 資料目錄，但因為 DRBD 檔案系統會取代此目錄，所以您必須稍後安裝 MySQL。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="6f7a2-162">驗證 (使用 `/sbin/ifconfig`) 這兩部 VM 是否使用 10.10.10.0/24 子網路中的位址，以及它們是否可以根據名稱互相 Ping 到對方。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="6f7a2-163">您也可以使用 `ssh-keygen` 和 `ssh-copy-id`，來確定這兩部 VM 無需密碼即可透過 SSH 彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="6f7a2-164">設定 DRBD</span><span class="sxs-lookup"><span data-stu-id="6f7a2-164">Set up DRBD</span></span>
<span data-ttu-id="6f7a2-165">建立使用基礎 `/dev/sdc1` 磁碟分割的 DRBD 資源，以產生能夠使用 ext3 進行格式化的 `/dev/drbd1` 資源，以供主要和次要節點使用。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="6f7a2-166">開啟 `/etc/drbd.d/r0.res` 並複製兩部 VM 上的下列資源定義：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="6f7a2-167">在這兩部 VM 上使用 `drbdadm` 來初始化資源：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="6f7a2-168">在主要 VM (`hadb01`) 上，強制執行 DRBD 資源的擁有權 (主要)：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="6f7a2-169">如果您在這兩個 VM 上檢查 /proc/drbd (`sudo cat /proc/drbd`) 的內容，應可在 `hadb01` 上看到 `Primary/Secondary` 且在 `hadb02` 上看到 `Secondary/Primary` (此時應與解決方案一致)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="6f7a2-170">客戶可免費透過 10.10.10.0/24 網路同步處理這個 5 GB 磁碟。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="6f7a2-171">同步處理此磁碟後，您可以在 `hadb01` 上建立檔案系統。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="6f7a2-172">基於測試目的，我們會使用 ext2，但下列程式碼將建立 ext3 檔案系統：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="6f7a2-173">掛接 DRBD 資源</span><span class="sxs-lookup"><span data-stu-id="6f7a2-173">Mount the DRBD resource</span></span>
<span data-ttu-id="6f7a2-174">您現在即可在 `hadb01` 上掛接 DRBD 資源。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="6f7a2-175">Debian 及其衍生版本會使用 `/var/lib/mysql` 做為 MySQL 的資料目錄。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="6f7a2-176">因為您尚未安裝 MySQL，請建立此目錄並掛接 DRBD 資源。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="6f7a2-177">若要執行此選項，請在 `hadb01` 上執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="6f7a2-178">設定 MySQL</span><span class="sxs-lookup"><span data-stu-id="6f7a2-178">Set up MySQL</span></span>
<span data-ttu-id="6f7a2-179">現在您可以開始在 `hadb01`上安裝 MySQL：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="6f7a2-180">在 `hadb02`中，您有兩個選擇。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="6f7a2-181">您可以安裝 mysql-server，這將會建立 /var/lib/mysql，並在其中填入新的資料目錄，然後移除內容。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="6f7a2-182">若要執行此選項，請在 `hadb02` 上執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="6f7a2-183">第二個選擇是容錯移轉至 `hadb02`，然後在那裡安裝 mysql-server。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="6f7a2-184">安裝指令碼將會注意到現有安裝，且不會對它執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="6f7a2-185">在 `hadb01` 上執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="6f7a2-186">在 `hadb02` 上執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="6f7a2-187">如果您不打算現在容錯移轉 DRBD，雖然第一個選擇可以說是較為繁瑣，但相對是比較容易的。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="6f7a2-188">安裝完成後，您可以開始使用 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="6f7a2-189">在 `hadb02` (或對 DRBD 而言為作用中伺服器的任一部伺服器) 上執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="6f7a2-190">最後一個陳述式會有效地停用此資料表中根使用者的驗證。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="6f7a2-191">這應由您的生產等級 GRANT 陳述式取代，這裡僅是為了說明的目的才包括此陳述式。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="6f7a2-192">如果您想要在 VM 外進行查詢 (這是本指南的目的)，您還必須啟用 MySQL 的網路功能。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="6f7a2-193">在兩部 VM 上，開啟 `/etc/mysql/my.cnf` 並移至 `bind-address`。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="6f7a2-194">將位址從 127.0.0.1 變更為 0.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="6f7a2-195">儲存檔案後，在您目前的主要 VM 上發佈 `sudo service mysql restart` 。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="6f7a2-196">建立 MySQL 負載平衡集</span><span class="sxs-lookup"><span data-stu-id="6f7a2-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="6f7a2-197">回到入口網站，移至 `hadb01`，然後選擇 [端點]。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="6f7a2-198">若要建立端點，從下拉式清單選擇 [MySQL (TCP 3306)]，然後選取 [建立新的負載平衡集]。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="6f7a2-199">替負載平衡端點 `lb-mysql` 命名。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="6f7a2-200">將 [時間] 設定為 5 秒 (最小值)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="6f7a2-201">建立端點後，請移至 `hadb02`，選擇 [端點]，然後建立端點。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="6f7a2-202">選擇 `lb-mysql`，然後從下拉式清單選取 MySQL。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="6f7a2-203">在此步驟中，您也可以使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="6f7a2-204">您現在已具備手動叢集作業所需的一切。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="6f7a2-205">設定負載平衡集</span><span class="sxs-lookup"><span data-stu-id="6f7a2-205">Test the load-balanced set</span></span>
<span data-ttu-id="6f7a2-206">您可以使用任何 MySQL 用戶端，或使用特定應用程式 (例如以 Azure 網站身分執行的 phpMyAdmin)，從機器外部執行測試。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="6f7a2-207">在此案例中，您在另一個 Linux 方塊上使用 MySQL 的命令列工具：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="6f7a2-208">手動容錯移轉</span><span class="sxs-lookup"><span data-stu-id="6f7a2-208">Manually failing over</span></span>
<span data-ttu-id="6f7a2-209">您可以透過關閉 MySQL、切換 DRBD 的主要 VM，然後重新啟動 MySQL 來模擬容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="6f7a2-210">若要執行此工作，請在 hadb01 上執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="6f7a2-211">接著，在 hadb02 上：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="6f7a2-212">手動容錯移轉後，您可以重複遠端查詢，它應可正常運作。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="6f7a2-213">設定 Corosync</span><span class="sxs-lookup"><span data-stu-id="6f7a2-213">Set up Corosync</span></span>
<span data-ttu-id="6f7a2-214">Corosync 是需要 Pacemaker 才能運作的基礎叢集基礎結構。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="6f7a2-215">若是 Heartbeat (及其他方法，如 Ultramonkey)，Corosync 是 CRM 功能的分割，而 Pacemaker 會維持類似 Hearbeat 的功能。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="6f7a2-216">Corosync 在 Azure 上的主要限制是，Corosync 偏好的通訊順序為多點傳送大於廣播大於單點傳送，但 Microsoft Azure 網路僅支援單點傳送。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="6f7a2-217">還好，Corosync 具備有效的單點傳送模式。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="6f7a2-218">唯一的真正限制是，因為所有節點彼此之間不會神奇地自動 進行通訊，您必須在組態檔中定義節點，包括其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="6f7a2-219">我們可以使用 Corosync 範例檔案進行單點傳送和變更繫結位址、節點清單和記錄目錄 (Ubuntu 會使用 `/var/log/corosync`，而範例檔案會使用 `/var/log/cluster`)，以及啟用仲裁工具。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="6f7a2-220">對兩個節點使用下列 `transport: udpu` 指示詞和手動定義的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="6f7a2-221">在 `/etc/corosync/corosync.conf` 上對兩個節點執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="6f7a2-222">複製兩部 VM 上的這個組態檔，並在這兩個節點中啟動 Corosync：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="6f7a2-223">在啟動服務不久後，系統應會在目前環中建立叢集，並組成仲裁。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="6f7a2-224">我們可以透過檢閱記錄檔或執行下列程式碼來檢查此功能：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="6f7a2-225">您將看到類似下圖的輸出：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-225">You will see output similar to the following image:</span></span>

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="6f7a2-227">設定 Pacemaker</span><span class="sxs-lookup"><span data-stu-id="6f7a2-227">Set up Pacemaker</span></span>
<span data-ttu-id="6f7a2-228">Pacemaker 會使用叢集來監視資源，定義在主要 VM 故障時將這些資源切換到次要 VM。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="6f7a2-229">在所有其他選擇中，您可從一組可用指令碼或從 LSB (如 init) 指令碼來定義資源。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="6f7a2-230">我們要 Pacemaker「擁有」DRBD 資源、掛接點及 MySQL 服務。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="6f7a2-231">如果 Pacemaker 可以在主要 VM 發生問題時，依正確順序來開啟與關閉 DRBD、掛接/取消掛接 DRBD，然後啟動和停止 MySQL，則安裝便已完成。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="6f7a2-232">首次安裝 Pacemaker 時，您的組態應十分簡單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="6f7a2-233">執行 `sudo crm configure show` 以檢查組態。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="6f7a2-234">然後使用下列資源來建立檔案 (如 `/tmp/cluster.conf`)：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

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

3. <span data-ttu-id="6f7a2-235">將檔案載入組態中。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-235">Load the file into the configuration.</span></span> <span data-ttu-id="6f7a2-236">您只需要在一個節點做一次這個動作。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="6f7a2-237">請確定開機時會啟動兩個節點的 Pacemaker：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="6f7a2-238">使用 `sudo crm_mon –L`，驗證其中一個節點已成為叢集的主要節點，並且正在執行所有資源。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="6f7a2-239">您可以使用掛接和 PS 來檢查資源是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="6f7a2-240">下列螢幕擷取畫面顯示 `crm_mon`，且其中一個節點已停止 (選取 Ctrl+C 以結束)：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![crm_mon node stopped](./media/mysql-cluster/image002.png)

<span data-ttu-id="6f7a2-242">此快照說明兩個節點 (一個主要和一個從屬)：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-242">This screenshot shows both nodes, one master and one slave:</span></span>

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="6f7a2-244">測試</span><span class="sxs-lookup"><span data-stu-id="6f7a2-244">Testing</span></span>
<span data-ttu-id="6f7a2-245">您已準備好開始自動容錯移轉模擬。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="6f7a2-246">作法有二：軟式和硬式。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="6f7a2-247">軟式方法使用叢集的關機功能：``crm_standby -U `uname -n` -v on``。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="6f7a2-248">如果您在主要 VM 上使用此選項，從屬 VM 便會取代主要 VM。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="6f7a2-249">記得將此選項設回 off。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-249">Remember to set this back to off.</span></span> <span data-ttu-id="6f7a2-250">如果不這麼做，crm_mon 會顯示一個待命中的節點。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="6f7a2-251">硬式方法是透過入口網站將主要 VM (hadb01) 關機，或變更 VM 上的執行層級 (例如，終止、關機)。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="6f7a2-252">這會藉由發出主要 VM 出現故障的訊號來協助 Corosync 和 Pacemaker。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="6f7a2-253">您可以測試這個方法 (在維護期間非常有用)，但您也可以透過凍結 VM 來強制執行此案例。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="6f7a2-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="6f7a2-254">STONITH</span></span>
<span data-ttu-id="6f7a2-255">它應該能透過 Azure CLI 發出 VM 關機命令，來代替可控制實體裝置的 STONITH 指令碼。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="6f7a2-256">您可以使用 `/usr/lib/stonith/plugins/external/ssh` 做為基礎，並在叢集的組態中啟用 STONITH。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="6f7a2-257">系統應會全域安裝 Azure CLI，並載入叢集使用者的發佈設定和設定檔。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="6f7a2-258">您可在 [GitHub](https://github.com/bureado/aztonith) 上找到資源的範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="6f7a2-259">變更叢集的組態，方法是將下列程式碼新增至 `sudo crm configure`：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="6f7a2-260">此指令碼不會執行使用/停用檢查。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="6f7a2-261">原始的 SSH 資源會有 15 個 Ping 檢查，但 Azure VM 的復原時間可能會有較多的變數。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="6f7a2-262">限制</span><span class="sxs-lookup"><span data-stu-id="6f7a2-262">Limitations</span></span>
<span data-ttu-id="6f7a2-263">套用下列限制：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-263">The following limitations apply:</span></span>

* <span data-ttu-id="6f7a2-264">在 Pacemaker 中，將 DRBD 當成資源進行管理的 Linbit DRBD 資源指令碼會在關閉節點時使用 `drbdadm down`，即使該節點只是進入待命中狀態也一樣。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="6f7a2-265">因為主要 VM 在開始遭到寫入時，從屬 VM 並不會同步處理 DRBD 資源，所以這不是理想的作法。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="6f7a2-266">如果主要 VM 不是順利關機，從屬 VM 會接收較舊的檔案系統狀態。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="6f7a2-267">可能解決此問題的方法有兩種：</span><span class="sxs-lookup"><span data-stu-id="6f7a2-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="6f7a2-268">在所有叢集節點中透過本機 (未叢集化) 看門狗強制執行 `drbdadm up r0`</span><span class="sxs-lookup"><span data-stu-id="6f7a2-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="6f7a2-269">在 `/usr/lib/ocf/resource.d/linbit/drbd` 中編輯 linbit DRBD 指令碼，以確保不會呼叫 `down`</span><span class="sxs-lookup"><span data-stu-id="6f7a2-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="6f7a2-270">負載平衡器至少需要 5 秒的時間進行回應，因此應用程式應為叢集感知且應可容許逾時。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="6f7a2-271">其他架構也可提供協助，例如應用程式內部佇列、查詢中繼軟體等。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="6f7a2-272">若要確保寫入作業會以可管理的步調結束，且會儘可能頻繁地將快取清除到磁碟以減少記憶體損失，MySQL 調整是有必要的。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="6f7a2-273">VM 互連中的寫入效能將會取決於虛擬開關，因為虛擬開關是 DRBD 用來複寫裝置的機制。</span><span class="sxs-lookup"><span data-stu-id="6f7a2-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
