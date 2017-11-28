---
title: "在 Azure 上叢集 aaaRun MariaDB (MySQL) |Microsoft 文件"
description: "在 Azure 虛擬機器上建立 MariaDB + Galera MySQL 叢集"
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="c6eaa-103">MariaDB (MySQL) 叢集：Azure 教學課程</span><span class="sxs-lookup"><span data-stu-id="c6eaa-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c6eaa-104">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="c6eaa-105">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="c6eaa-106">Microsoft 建議最新的部署使用 hello Azure 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="c6eaa-107">現在可在 hello Azure Marketplace MariaDB Enterprise 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="c6eaa-108">hello 新供應項目就會自動部署 MariaDB Galera 叢集上 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="c6eaa-109">您應該使用 hello 從的 新供應項目[Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/)。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="c6eaa-110">本文章將示範如何 toocreate 多重主機[Galera](http://galeracluster.com/products/)叢集[MariaDBs](https://mariadb.org/en/about/) （穩固、 可擴充且可靠的掉落取代 MySQL） toowork 在 Azure 上的高可用性環境中虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="c6eaa-111">架構概觀</span><span class="sxs-lookup"><span data-stu-id="c6eaa-111">Architecture overview</span></span>
<span data-ttu-id="c6eaa-112">本文說明如何 toocomplete hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="c6eaa-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="c6eaa-113">建立一個三節點的叢集。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="c6eaa-114">從 hello OS 磁碟個別 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="c6eaa-115">建立在 RAID 0/等量設定 tooincrease IOPS 的 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="c6eaa-116">使用 Azure 負載平衡器 toobalance hello 負載 hello 三個節點。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="c6eaa-117">toominimize 重複性工作、 建立包含 MariaDB + Galera 的 VM 映像，並使用它 toocreate hello 另一個叢集 Vm。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![系統架構](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="c6eaa-119">本主題使用 hello [Azure CLI](../../../cli-install-nodejs.md)工具，因此請確定 toodownload 它們並且將它們連接 tooyour Azure 訂用帳戶相應 toohello 指示。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="c6eaa-120">如果您需要提供 hello Azure CLI 參考 toohello 命令，請參閱 hello [Azure CLI 命令參考](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="c6eaa-121">您也需要太[建立 SSH 金鑰驗證]並記下 hello.pem 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="c6eaa-122">建立 hello 範本</span><span class="sxs-lookup"><span data-stu-id="c6eaa-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="c6eaa-123">基礎結構</span><span class="sxs-lookup"><span data-stu-id="c6eaa-123">Infrastructure</span></span>
1. <span data-ttu-id="c6eaa-124">一起建立同質群組 toohold hello 的資源。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="c6eaa-125">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="c6eaa-126">建立儲存體帳戶 toohost 所有的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="c6eaa-127">您不應該超過 40 重度使用的磁碟置於 hello 相同儲存體帳戶 tooavoid 達到 hello 20000 IOPS 儲存體帳戶限制。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="c6eaa-128">在此情況下，您低於該限制，因此您將會儲存所有項目上使用相同帳戶執行簡單的 hello。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="c6eaa-129">尋找 hello hello CentOS 7 虛擬機器映像名稱。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="c6eaa-130">hello 輸出將會類似`5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="c6eaa-131">Hello 下列步驟中使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="c6eaa-132">建立 hello VM 範本，並取代 /path/to/key.pem hello 路徑產生的 hello.pem SSH 金鑰的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="c6eaa-133">將連接用於 hello RAID 組態中的四個 500 GB 資料磁碟 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="c6eaa-134">使用 SSH toosign toohello 範本中 mariadbhatemplate.cloudapp.net:22，在您建立的 VM，然後使用您的私密金鑰的連線。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="c6eaa-135">軟體</span><span class="sxs-lookup"><span data-stu-id="c6eaa-135">Software</span></span>
1. <span data-ttu-id="c6eaa-136">取得 hello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="c6eaa-137">安裝 RAID 支援：</span><span class="sxs-lookup"><span data-stu-id="c6eaa-137">Install RAID support:</span></span>

    <span data-ttu-id="c6eaa-138">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-138">a.</span></span> <span data-ttu-id="c6eaa-139">安裝 mdadm。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="c6eaa-140">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-140">b.</span></span> <span data-ttu-id="c6eaa-141">使用 EXT4 檔案系統中建立 hello RAID0/等量磁碟區設定。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="c6eaa-142">c.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-142">c.</span></span> <span data-ttu-id="c6eaa-143">建立 hello 掛接點目錄。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="c6eaa-144">d.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-144">d.</span></span> <span data-ttu-id="c6eaa-145">擷取 hello hello 新建立的 RAID 裝置的 UUID。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="c6eaa-146">e.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-146">e.</span></span> <span data-ttu-id="c6eaa-147">編輯 /etc/fstab。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="c6eaa-148">f.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-148">f.</span></span> <span data-ttu-id="c6eaa-149">新增 hello 裝置 tooenable 自動掛接在重新開機，使用 hello 值來取代 hello UUID 取自先前 hello **blkid**命令。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="c6eaa-150">g.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-150">g.</span></span> <span data-ttu-id="c6eaa-151">掛接 hello 新磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="c6eaa-152">安裝 MariaDB。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-152">Install MariaDB.</span></span>

    <span data-ttu-id="c6eaa-153">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-153">a.</span></span> <span data-ttu-id="c6eaa-154">建立 hello MariaDB.repo 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="c6eaa-155">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-155">b.</span></span> <span data-ttu-id="c6eaa-156">填滿 hello 儲存機制檔案，以下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6eaa-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="c6eaa-157">c.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-157">c.</span></span> <span data-ttu-id="c6eaa-158">tooavoid 衝突，請移除現有的後置和 mariadb 程式庫。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="c6eaa-159">d.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-159">d.</span></span> <span data-ttu-id="c6eaa-160">使用 Galera 安裝 MariaDB。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="c6eaa-161">移動 hello MySQL 資料目錄 toohello RAID 封鎖裝置。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="c6eaa-162">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-162">a.</span></span> <span data-ttu-id="c6eaa-163">將 hello 目前 MySQL 目錄複製到新位置，並移除 hello 舊的目錄。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="c6eaa-164">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-164">b.</span></span> <span data-ttu-id="c6eaa-165">據以設定 hello 新目錄的權限。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="c6eaa-166">c.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-166">c.</span></span> <span data-ttu-id="c6eaa-167">建立指向 hello 舊目錄 toohello 新位置 hello RAID 磁碟分割上的符號連結。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="c6eaa-168">因為[SELinux 干擾 hello 叢集操作](http://galeracluster.com/documentation-webpages/configuration.html#selinux)，它是必要的 toodisable 它 hello 目前工作階段。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="c6eaa-169">編輯`/etc/selinux/config`toodisable 後續重新啟動它。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="c6eaa-170">驗證 MySQL 執行。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="c6eaa-171">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-171">a.</span></span> <span data-ttu-id="c6eaa-172">啟動 MySQL。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="c6eaa-173">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-173">b.</span></span> <span data-ttu-id="c6eaa-174">安全 hello MySQL 安裝、 設定 hello 根密碼、 移除匿名使用者 toodisable 遠端根登入，然後移除 hello 測試資料庫。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="c6eaa-175">c.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-175">c.</span></span> <span data-ttu-id="c6eaa-176">針對叢集操作，以及 （選擇性） 您的應用程式的 hello 資料庫上建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="c6eaa-177">d.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-177">d.</span></span> <span data-ttu-id="c6eaa-178">停止 MySQL。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="c6eaa-179">建立組態預留位置。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="c6eaa-180">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-180">a.</span></span> <span data-ttu-id="c6eaa-181">編輯 hello MySQL 組態 toocreate hello 叢集設定的預留位置。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="c6eaa-182">不會取代 hello  **`<Variables>`** 或取消註解現在。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="c6eaa-183">從此範本建立 VM 之後才會需要這個動作。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="c6eaa-184">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-184">b.</span></span> <span data-ttu-id="c6eaa-185">編輯 hello  **[galera]** 區段，並清除它。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="c6eaa-186">c.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-186">c.</span></span> <span data-ttu-id="c6eaa-187">編輯 hello **[mariadb]** > 一節。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="c6eaa-188">使用 FirewallD CentOS 7 上，以開啟 hello 防火牆上的必要連接埠。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="c6eaa-189">MySQL： `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c6eaa-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="c6eaa-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c6eaa-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="c6eaa-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c6eaa-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="c6eaa-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="c6eaa-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="c6eaa-193">重新載入 hello 防火牆：`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="c6eaa-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="c6eaa-194">最佳化效能的 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-194">Optimize hello system for performance.</span></span> <span data-ttu-id="c6eaa-195">如需詳細資訊，請參閱[效能調整策略](optimize-mysql.md)。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="c6eaa-196">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-196">a.</span></span> <span data-ttu-id="c6eaa-197">再次編輯 hello MySQL 組態檔。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="c6eaa-198">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-198">b.</span></span> <span data-ttu-id="c6eaa-199">編輯 hello **[mariadb]**區段，並新增下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6eaa-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="c6eaa-200">我們建議 innodb\_buffer\_pool_size 是 VM 記憶體的 70%。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="c6eaa-201">在此範例中，它已設定為 2.45 GB hello 媒體 Azure VM，3.5 gb 的 RAM。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="c6eaa-202">停止 MySQL、 MySQL 服務上啟動 tooavoid 中斷 hello 叢集加入節點，當執行停用及解除佈建 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="c6eaa-203">擷取 hello VM 透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="c6eaa-204">(目前，[發出 hello Azure CLI 工具中的 # 1268年](https://github.com/Azure/azure-xplat-cli/issues/1268)描述 hello 事實 hello Azure CLI 工具所擷取的映像不會擷取 hello 附加資料磁碟。)</span><span class="sxs-lookup"><span data-stu-id="c6eaa-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="c6eaa-205">a.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-205">a.</span></span> <span data-ttu-id="c6eaa-206">關閉 hello 機器透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="c6eaa-207">b.</span><span class="sxs-lookup"><span data-stu-id="c6eaa-207">b.</span></span> <span data-ttu-id="c6eaa-208">按一下**擷取**和 hello 映像名稱指定為**mariadb galera 映像**。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="c6eaa-209">提供描述並核取「我已執行 waagent」。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-209">Provide a description and check "I have run waagent."</span></span>
      
      ![擷取 hello 虛擬機器](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="c6eaa-211">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="c6eaa-211">Create hello cluster</span></span>
<span data-ttu-id="c6eaa-212">使用您建立，然後設定並啟動 hello 叢集 hello 範本建立三個 Vm。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="c6eaa-213">建立的 hello hello mariadb galera 映像中的第一個 CentOS 7 VM 映像中建立，提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6eaa-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="c6eaa-214">虛擬網路名稱︰mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="c6eaa-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="c6eaa-215">子網路︰mariadb</span><span class="sxs-lookup"><span data-stu-id="c6eaa-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="c6eaa-216">機器大小：中型</span><span class="sxs-lookup"><span data-stu-id="c6eaa-216">Machine size: medium</span></span>
 - <span data-ttu-id="c6eaa-217">雲端服務名稱： mariadbha （或您想 toobe mariadbha.cloudapp.net 透過存取的任何名稱）</span><span class="sxs-lookup"><span data-stu-id="c6eaa-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="c6eaa-218">機器名稱：mariadb1</span><span class="sxs-lookup"><span data-stu-id="c6eaa-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="c6eaa-219">使用者名稱：azureuser</span><span class="sxs-lookup"><span data-stu-id="c6eaa-219">Username: azureuser</span></span>
 - <span data-ttu-id="c6eaa-220">SSH 存取權︰已啟用</span><span class="sxs-lookup"><span data-stu-id="c6eaa-220">SSH access: enabled</span></span>
 - <span data-ttu-id="c6eaa-221">傳送嗨 SSH 憑證.pem 檔案，並以您儲存 hello hello 路徑取代 /path/to/key.pem 產生.pem SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c6eaa-222">hello 下列命令會分成多行為了清楚起見，但您應輸入各以一行。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="c6eaa-223">建立兩個的多個虛擬機器連接這些 toohello mariadbha 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="c6eaa-224">變更 hello VM 名稱和 SSH 連接埠 tooa 唯一連接埠與中的其他 Vm 不衝突 hello hello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="c6eaa-225">對於 MariaDB3：</span><span class="sxs-lookup"><span data-stu-id="c6eaa-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="c6eaa-226">您需要 tooget hello 內部 IP 位址的每個 hello 三個 Vm 的 hello 下一個步驟：</span><span class="sxs-lookup"><span data-stu-id="c6eaa-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![取得 IP 位址](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="c6eaa-228">使用 SSH toosign toohello 三個 Vm 中，並且編輯每個 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="c6eaa-229">請取消註解 **`wsrep_cluster_name`** 和 **`wsrep_cluster_address`** 藉由移除 hello  **#**  hello hello 該行開頭。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="c6eaa-230">此外，取代 **`<ServerIP>`** 中 **`wsrep_node_address`** 和 **`<NodeName>`** 中 **`wsrep_node_name`** 以 helloVM 的 IP 位址和名稱，分別以及這些行取消註解。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="c6eaa-231">啟動 hello 叢集上 MariaDB1 並讓它在啟動時執行。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="c6eaa-232">啟動 MariaDB2 與 MariaDB3 上的 MySQL，並讓它在啟動時執行。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="c6eaa-233">負載平衡 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="c6eaa-233">Load balance hello cluster</span></span>
<span data-ttu-id="c6eaa-234">當您建立叢集的 hello Vm 時，您會加入它們至可用性設定組呼叫 clusteravset tooensure 它們被放置在不同容錯網域和更新網域上和，Azure 絕不會維護在所有機器上的一次。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="c6eaa-235">此設定符合 hello toobe 支援 hello Azure 服務等級協定 (SLA) 的需求。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="c6eaa-236">現在使用 hello 三個節點之間的 Azure 負載平衡器 toobalance 要求。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="c6eaa-237">執行下列命令在您的電腦上，使用 Azure CLI hello hello。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="c6eaa-238">hello 命令參數結構是：`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="c6eaa-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="c6eaa-239">hello CLI 設定 hello 負載平衡器探查間隔 too15 秒數，這可能是一個位元太長。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="c6eaa-240">變更在 hello 管理入口網站下**端點**任何 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![編輯端點](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="c6eaa-242">選取**Reconfigure hello Load-Balanced 設定**。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![重新設定 hello 負載平衡集](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="c6eaa-244">變更**探查間隔**too5 的秒數，並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![變更探查間隔](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="c6eaa-246">驗證 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="c6eaa-246">Validate hello cluster</span></span>
<span data-ttu-id="c6eaa-247">hello 硬碟的工作完成。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-247">hello hard work is done.</span></span> <span data-ttu-id="c6eaa-248">hello 叢集必須能夠立即存取在`mariadbha.cloudapp.net:3306`、 的點擊 hello 負載平衡器和之間的路由要求 hello 三個 Vm，順暢而有效率地。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="c6eaa-249">使用您最愛的 MySQL 用戶端 tooconnect，或從這個叢集正在運作的 hello Vm tooverify 的其中一個連接。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="c6eaa-250">然後建立資料庫並填入一些資料。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="c6eaa-251">您所建立的 hello 資料庫傳回下表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="c6eaa-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="c6eaa-252">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6eaa-252">Next steps</span></span>
<span data-ttu-id="c6eaa-253">在本文中，您在執行 CentOS 7 的 Azure 虛擬機器上建立了三個節點的 MariaDB + Galera 高可用性叢集。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="c6eaa-254">hello Vm 進行負載平衡與 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="c6eaa-255">您可能會想在 toolook[另一個方式 toocluster Linux 上的 MySQL](mysql-cluster.md)以及方式太[最佳化和測試 Azure Linux Vm 上的 MySQL 效能](optimize-mysql.md)。</span><span class="sxs-lookup"><span data-stu-id="c6eaa-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[建立 SSH 金鑰驗證]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
