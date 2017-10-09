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
# <a name="how-tooinstall-mysql-on-azure"></a>如何在 Azure 上 MySQL tooinstall
在本文中，您將學習如何 tooinstall 上及設定 MySQL 執行 Linux 的 Azure 虛擬機器。

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>在虛擬機器上安裝 MySQL
> [!NOTE]
> 您必須已經在順序 toocomplete 本教學課程執行 Linux 的 Microsoft Azure 虛擬機器。 請參閱[Azure Linux VM 教學課程](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)toocreate 並設定與 Linux VM`mysqlnode`做為 hello VM 名稱和`azureuser`之前的使用者身分。
> 
> 

在此情況下，使用 3306 連接埠作為 hello MySQL 連接埠。  

連接 toohello Linux VM 建立透過 putty 連線。 如果這是 hello 第一次使用 Azure Linux VM，請參閱 < 如何 toouse putty 連線 tooa Linux VM[這裡](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

例如在本文中，我們將使用儲存機制封裝 tooinstall MySQL5.6。 事實上，MySQL5.6 的效能改良功能比 MySQL5.5 更多。  詳細資訊請參閱 [這裡](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/)。

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>如何在 Ubuntu 上 MySQL5.6 tooinstall
以下範例將使用 Azure 中採用 Ubuntu 的 Linux VM。

* 步驟 1： 安裝 MySQL Server 5.6 太切換`root`使用者：
  
            #[azureuser@mysqlnode:~]sudo su -
  
    安裝 mysql-server 5.6：
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    在安裝期間，您會看到對話方塊視窗 poping 向上 tooask tooset MySQL 根密碼，而且您需要 hello 密碼在此設定。
  
    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    輸入的 hello 密碼再次 tooconfirm。

    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* 步驟 2：登入 MySQL Server
  
    MySQL Server 安裝完成之後，MySQL 服務便會自動啟動 。 您可以使用 `root` 使用者的身分登入 MySQL Server。
    使用以下命令 toologin 和輸入的密碼 hello。
  
             #[root@mysqlnode ~]# mysql -uroot -p
* 步驟 3： 管理執行 MySQL 服務的 hello
  
    (a) 取得 MySQL 服務的狀態
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) 啟動 MySQL 服務
  
             #[root@mysqlnode ~]# service mysql start
  
    (b) 停止 MySQL 服務
  
             #[root@mysqlnode ~]# service mysql stop
  
    （d） 重新啟動 hello MySQL 服務
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Red Hat 作業系統系列上的 tooinstall MySQL 像 CentOS，Oracle Linux
以下範例將使用執行 CentOS 或 Oracle Linux 的 Linux VM。

* 步驟 1： 加入 MySQL Yum 儲存機制交換器 hello 太`root`使用者：
  
            #[azureuser@mysqlnode:~]sudo su -
  
    下載並安裝 hello MySQL 版本套件：
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* 步驟 2： 編輯下列檔案 tooenable hello MySQL 儲存機制下載 hello MySQL5.6 封裝。
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    更新這個檔案 toobelow 的每個值：
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* 步驟 3：從 MySQL 存放庫安裝 MySQL 安裝 MySQL：
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    將安裝 MySQL RPM 封裝和所有相關的封裝。
* 步驟 4： 管理執行 MySQL 服務的 hello
  
    （a） 檢查 hello MySQL 伺服器 hello 服務狀態：
  
           #[root@mysqlnode ~]#service mysqld status
  
    （b） 檢查是否要執行 hello 預設連接埠的 MySQL 伺服器：
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    （c） 啟動 hello MySQL 伺服器：

           #[root@mysqlnode ~]#service mysqld start

    （d） 停止 hello MySQL 伺服器：

           #[root@mysqlnode ~]#service mysqld stop

    （e） 當 hello 系統啟動時，請設定 MySQL toostart:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>如何 tooinstall SUSE Linux 上的 MySQL
以下範例將使用執行 OpenSUSE 的 Linux VM。

* 步驟 1：下載及安裝 MySQL Server
  
    切換太`root`使用者已透過下列命令：  
  
           #sudo su -
  
    下載及安裝 MySQL Server 封裝：
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* 步驟 2： 管理執行 MySQL 服務的 hello
  
    （a） 檢查 hello MySQL 伺服器 hello 狀態：
  
           #[root@mysqlnode ~]# rcmysql status
  
    （b） 檢查是否 hello hello MySQL 伺服器的預設連接埠：
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    （c） 啟動 hello MySQL 伺服器：

           #[root@mysqlnode ~]# rcmysql start

    （d） 停止 hello MySQL 伺服器：

           #[root@mysqlnode ~]# rcmysql stop

    （e） 當 hello 系統啟動時，請設定 MySQL toostart:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>後續步驟
按一下 [這裡](https://www.mysql.com/)，了解更多 MySQL 使用方式和相關資訊。

