---
title: "在 Azure 中的 Linux VM 上的 MySQL 向上 aaaSet |Microsoft 文件"
description: "了解如何 tooinstall hello MySQL 堆疊在 Azure 中的 Linux 虛擬機器 （Ubuntu 或 RedHat 系列作業系統）"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="7bcae-103">如何在 Azure 上 MySQL tooinstall</span><span class="sxs-lookup"><span data-stu-id="7bcae-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="7bcae-104">在本文中，您將學習如何 tooinstall 上及設定 MySQL 執行 Linux 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7bcae-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="7bcae-105">在虛擬機器上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="7bcae-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="7bcae-106">您必須已經在順序 toocomplete 本教學課程執行 Linux 的 Microsoft Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7bcae-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="7bcae-107">請參閱[Azure Linux VM 教學課程](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)toocreate 並設定與 Linux VM`mysqlnode`做為 hello VM 名稱和`azureuser`之前的使用者身分。</span><span class="sxs-lookup"><span data-stu-id="7bcae-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="7bcae-108">在此情況下，使用 3306 連接埠作為 hello MySQL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="7bcae-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="7bcae-109">連接 toohello Linux VM 建立透過 putty 連線。</span><span class="sxs-lookup"><span data-stu-id="7bcae-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="7bcae-110">如果這是 hello 第一次使用 Azure Linux VM，請參閱 < 如何 toouse putty 連線 tooa Linux VM[這裡](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7bcae-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7bcae-111">例如在本文中，我們將使用儲存機制封裝 tooinstall MySQL5.6。</span><span class="sxs-lookup"><span data-stu-id="7bcae-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="7bcae-112">事實上，MySQL5.6 的效能改良功能比 MySQL5.5 更多。</span><span class="sxs-lookup"><span data-stu-id="7bcae-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="7bcae-113">詳細資訊請參閱 [這裡](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/)。</span><span class="sxs-lookup"><span data-stu-id="7bcae-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="7bcae-114">如何在 Ubuntu 上 MySQL5.6 tooinstall</span><span class="sxs-lookup"><span data-stu-id="7bcae-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="7bcae-115">以下範例將使用 Azure 中採用 Ubuntu 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="7bcae-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="7bcae-116">步驟 1： 安裝 MySQL Server 5.6 太切換`root`使用者：</span><span class="sxs-lookup"><span data-stu-id="7bcae-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="7bcae-117">安裝 mysql-server 5.6：</span><span class="sxs-lookup"><span data-stu-id="7bcae-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="7bcae-118">在安裝期間，您會看到對話方塊視窗 poping 向上 tooask tooset MySQL 根密碼，而且您需要 hello 密碼在此設定。</span><span class="sxs-lookup"><span data-stu-id="7bcae-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="7bcae-120">輸入的 hello 密碼再次 tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="7bcae-120">Input hello password again tooconfirm.</span></span>

    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="7bcae-122">步驟 2：登入 MySQL Server</span><span class="sxs-lookup"><span data-stu-id="7bcae-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="7bcae-123">MySQL Server 安裝完成之後，MySQL 服務便會自動啟動 。</span><span class="sxs-lookup"><span data-stu-id="7bcae-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="7bcae-124">您可以使用 `root` 使用者的身分登入 MySQL Server。</span><span class="sxs-lookup"><span data-stu-id="7bcae-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="7bcae-125">使用以下命令 toologin 和輸入的密碼 hello。</span><span class="sxs-lookup"><span data-stu-id="7bcae-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="7bcae-126">步驟 3： 管理執行 MySQL 服務的 hello</span><span class="sxs-lookup"><span data-stu-id="7bcae-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="7bcae-127">(a) 取得 MySQL 服務的狀態</span><span class="sxs-lookup"><span data-stu-id="7bcae-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="7bcae-128">(b) 啟動 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="7bcae-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="7bcae-129">(b) 停止 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="7bcae-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="7bcae-130">（d） 重新啟動 hello MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="7bcae-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="7bcae-131">Red Hat 作業系統系列上的 tooinstall MySQL 像 CentOS，Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="7bcae-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="7bcae-132">以下範例將使用執行 CentOS 或 Oracle Linux 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="7bcae-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="7bcae-133">步驟 1： 加入 MySQL Yum 儲存機制交換器 hello 太`root`使用者：</span><span class="sxs-lookup"><span data-stu-id="7bcae-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="7bcae-134">下載並安裝 hello MySQL 版本套件：</span><span class="sxs-lookup"><span data-stu-id="7bcae-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="7bcae-135">步驟 2： 編輯下列檔案 tooenable hello MySQL 儲存機制下載 hello MySQL5.6 封裝。</span><span class="sxs-lookup"><span data-stu-id="7bcae-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="7bcae-136">更新這個檔案 toobelow 的每個值：</span><span class="sxs-lookup"><span data-stu-id="7bcae-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="7bcae-137">步驟 3：從 MySQL 存放庫安裝 MySQL 安裝 MySQL：</span><span class="sxs-lookup"><span data-stu-id="7bcae-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="7bcae-138">將安裝 MySQL RPM 封裝和所有相關的封裝。</span><span class="sxs-lookup"><span data-stu-id="7bcae-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="7bcae-139">步驟 4： 管理執行 MySQL 服務的 hello</span><span class="sxs-lookup"><span data-stu-id="7bcae-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="7bcae-140">（a） 檢查 hello MySQL 伺服器 hello 服務狀態：</span><span class="sxs-lookup"><span data-stu-id="7bcae-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="7bcae-141">（b） 檢查是否要執行 hello 預設連接埠的 MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="7bcae-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="7bcae-142">（c） 啟動 hello MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="7bcae-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="7bcae-143">（d） 停止 hello MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="7bcae-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="7bcae-144">（e） 當 hello 系統啟動時，請設定 MySQL toostart:</span><span class="sxs-lookup"><span data-stu-id="7bcae-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="7bcae-145">如何 tooinstall SUSE Linux 上的 MySQL</span><span class="sxs-lookup"><span data-stu-id="7bcae-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="7bcae-146">以下範例將使用執行 OpenSUSE 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="7bcae-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="7bcae-147">步驟 1：下載及安裝 MySQL Server</span><span class="sxs-lookup"><span data-stu-id="7bcae-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="7bcae-148">切換太`root`使用者已透過下列命令：</span><span class="sxs-lookup"><span data-stu-id="7bcae-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="7bcae-149">下載及安裝 MySQL Server 封裝：</span><span class="sxs-lookup"><span data-stu-id="7bcae-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="7bcae-150">步驟 2： 管理執行 MySQL 服務的 hello</span><span class="sxs-lookup"><span data-stu-id="7bcae-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="7bcae-151">（a） 檢查 hello MySQL 伺服器 hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="7bcae-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="7bcae-152">（b） 檢查是否 hello hello MySQL 伺服器的預設連接埠：</span><span class="sxs-lookup"><span data-stu-id="7bcae-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="7bcae-153">（c） 啟動 hello MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="7bcae-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="7bcae-154">（d） 停止 hello MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="7bcae-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="7bcae-155">（e） 當 hello 系統啟動時，請設定 MySQL toostart:</span><span class="sxs-lookup"><span data-stu-id="7bcae-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="7bcae-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7bcae-156">Next Step</span></span>
<span data-ttu-id="7bcae-157">按一下 [這裡](https://www.mysql.com/)，了解更多 MySQL 使用方式和相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7bcae-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

