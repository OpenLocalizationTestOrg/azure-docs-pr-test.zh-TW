---
title: "設定 Azure 中 Linux VM 上的 MySQL| Microsoft Docs"
description: "了解如何在 Azure 中的 Linux 虛擬機器 (Ubuntu 或 RedHat 系列 OS) 上安裝 MySQL 堆疊"
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
ms.openlocfilehash: 0ee70bda954cf0a193d43b5b47702e7b2c37844d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-mysql-on-azure"></a><span data-ttu-id="82522-103">如何在 Azure 上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="82522-103">How to install MySQL on Azure</span></span>
<span data-ttu-id="82522-104">本文將示範如何在執行 Linux 的 Azure 虛擬機器上安裝和設定 MySQL</span><span class="sxs-lookup"><span data-stu-id="82522-104">In this article, you will learn how to install and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="82522-105">在虛擬機器上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="82522-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="82522-106">您必須已經具有執行 Linux 的 Microsoft Azure 虛擬機器，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="82522-106">You must already have a Microsoft Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="82522-107">請參閱 [Azure Linux VM 教學課程](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，建立並設定以 `mysqlnode` 為 VM 名稱，`azureuser` 為使用者的 Linux VM，然後再繼續進行下一步。</span><span class="sxs-lookup"><span data-stu-id="82522-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create and set up a Linux VM with `mysqlnode` as the VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="82522-108">在此情況下，請使用連接埠 3306 作為 MySQL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="82522-108">In this case, use 3306 port as the MySQL port.</span></span>  

<span data-ttu-id="82522-109">連接到您透過 putty 建立的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="82522-109">Connect to the Linux VM you created via putty.</span></span> <span data-ttu-id="82522-110">如果這是您第一次使用 Azure Linux VM，請在[這裡](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)看看如何使用 putty 連接到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="82522-110">If this is the first time you use Azure Linux VM, see how to use putty connect to a Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="82522-111">本文的範例將使用儲存機制封裝安裝 MySQL5.6。</span><span class="sxs-lookup"><span data-stu-id="82522-111">We will use repository package to install MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="82522-112">事實上，MySQL5.6 的效能改良功能比 MySQL5.5 更多。</span><span class="sxs-lookup"><span data-stu-id="82522-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="82522-113">詳細資訊請參閱 [這裡](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/)。</span><span class="sxs-lookup"><span data-stu-id="82522-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-to-install-mysql56-on-ubuntu"></a><span data-ttu-id="82522-114">如何在 Ubuntu 上安裝 MySQL5.6</span><span class="sxs-lookup"><span data-stu-id="82522-114">How to install MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="82522-115">以下範例將使用 Azure 中採用 Ubuntu 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="82522-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="82522-116">步驟 1：將 MySQL Server 5.6 參數安裝至 `root` 使用者：</span><span class="sxs-lookup"><span data-stu-id="82522-116">Step 1: Install MySQL Server 5.6   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="82522-117">安裝 mysql-server 5.6：</span><span class="sxs-lookup"><span data-stu-id="82522-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="82522-118">在安裝期間，會出現一個快顯對話方塊視窗，要求您設定下方的 MySQL 根密碼，請在這裡設定密碼。</span><span class="sxs-lookup"><span data-stu-id="82522-118">During installation, you will see a dialog window poping up to ask you to set MySQL root password below, and you need set the password here.</span></span>
  
    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="82522-120">再次輸入密碼以進行確認。</span><span class="sxs-lookup"><span data-stu-id="82522-120">Input the password again to confirm.</span></span>

    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="82522-122">步驟 2：登入 MySQL Server</span><span class="sxs-lookup"><span data-stu-id="82522-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="82522-123">MySQL Server 安裝完成之後，MySQL 服務便會自動啟動 。</span><span class="sxs-lookup"><span data-stu-id="82522-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="82522-124">您可以使用 `root` 使用者的身分登入 MySQL Server。</span><span class="sxs-lookup"><span data-stu-id="82522-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="82522-125">使用下列命令以登入和輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="82522-125">Use the below command to login and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="82522-126">步驟 3：管理執行中的 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="82522-126">Step 3: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="82522-127">(a) 取得 MySQL 服務的狀態</span><span class="sxs-lookup"><span data-stu-id="82522-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="82522-128">(b) 啟動 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="82522-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="82522-129">(b) 停止 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="82522-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="82522-130">(d) 重新啟動 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="82522-130">(d) Restart the MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-to-install-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="82522-131">如何在 Redhat OS 系列 (例如 CentOS、Oracle Linux) 上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="82522-131">How to install MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="82522-132">以下範例將使用執行 CentOS 或 Oracle Linux 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="82522-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="82522-133">步驟 1：將 MySQL Yum 存放庫參數新增至 `root` 使用者：</span><span class="sxs-lookup"><span data-stu-id="82522-133">Step 1: Add the MySQL Yum repository   Switch to `root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="82522-134">下載並安裝 MySQL 發行套件：</span><span class="sxs-lookup"><span data-stu-id="82522-134">Download and install the MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="82522-135">步驟 2：編輯下方檔案，以允許 MySQL 儲存機制下載 MySQL5.6 套件檔案。</span><span class="sxs-lookup"><span data-stu-id="82522-135">Step 2: Edit below file to enable the MySQL repository for downloading the MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="82522-136">將此檔案的每個值更新為下列值：</span><span class="sxs-lookup"><span data-stu-id="82522-136">Update each value of this file to below:</span></span>
  
        \# *Enable to use MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="82522-137">步驟 3：從 MySQL 存放庫安裝 MySQL 安裝 MySQL：</span><span class="sxs-lookup"><span data-stu-id="82522-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="82522-138">將安裝 MySQL RPM 封裝和所有相關的封裝。</span><span class="sxs-lookup"><span data-stu-id="82522-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="82522-139">步驟 4：管理執行中的 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="82522-139">Step 4: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="82522-140">(a) 查看 MySQL 伺服器的服務狀態：</span><span class="sxs-lookup"><span data-stu-id="82522-140">(a) Check the service status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="82522-141">(b) 查看 MySQL Server 的預設連接埠是否正在執行：</span><span class="sxs-lookup"><span data-stu-id="82522-141">(b) Check whether the default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="82522-142">(c) 啟動 MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="82522-142">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="82522-143">(d) 停止 MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="82522-143">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="82522-144">(e) 將 MySQL 設為在啟動系統啟動：</span><span class="sxs-lookup"><span data-stu-id="82522-144">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-to-install-mysql-on-suse-linux"></a><span data-ttu-id="82522-145">如何在 SUSE Linux 上安裝 MySQL</span><span class="sxs-lookup"><span data-stu-id="82522-145">How to install MySQL on SUSE Linux</span></span>
<span data-ttu-id="82522-146">以下範例將使用執行 OpenSUSE 的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="82522-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="82522-147">步驟 1：下載及安裝 MySQL Server</span><span class="sxs-lookup"><span data-stu-id="82522-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="82522-148">透過下列命令切換至 `root` 使用者：</span><span class="sxs-lookup"><span data-stu-id="82522-148">Switch to `root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="82522-149">下載及安裝 MySQL Server 封裝：</span><span class="sxs-lookup"><span data-stu-id="82522-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="82522-150">步驟 2：管理執行中的 MySQL 服務</span><span class="sxs-lookup"><span data-stu-id="82522-150">Step 2: Manage the running MySQL service</span></span>
  
    <span data-ttu-id="82522-151">(a) 查看 MySQL 伺服器的狀態：</span><span class="sxs-lookup"><span data-stu-id="82522-151">(a) Check the status of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="82522-152">(b) 查看 MySQL 伺服器的預設連接埠：</span><span class="sxs-lookup"><span data-stu-id="82522-152">(b) Check whether the default port of the MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="82522-153">(c) 啟動 MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="82522-153">(c) Start the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="82522-154">(d) 停止 MySQL 伺服器：</span><span class="sxs-lookup"><span data-stu-id="82522-154">(d) Stop the MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="82522-155">(e) 將 MySQL 設為在啟動系統啟動：</span><span class="sxs-lookup"><span data-stu-id="82522-155">(e) Set MySQL to start when the system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="82522-156">下一步</span><span class="sxs-lookup"><span data-stu-id="82522-156">Next Step</span></span>
<span data-ttu-id="82522-157">按一下 [這裡](https://www.mysql.com/)，了解更多 MySQL 使用方式和相關資訊。</span><span class="sxs-lookup"><span data-stu-id="82522-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

