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
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>MariaDB (MySQL) 叢集：Azure 教學課程
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。 本文涵蓋 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello Azure 資源管理員的模型。

> [!NOTE]
> 現在可在 hello Azure Marketplace MariaDB Enterprise 叢集。 hello 新供應項目就會自動部署 MariaDB Galera 叢集上 Azure 資源管理員。 您應該使用 hello 從的 新供應項目[Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/)。
>
>

本文章將示範如何 toocreate 多重主機[Galera](http://galeracluster.com/products/)叢集[MariaDBs](https://mariadb.org/en/about/) （穩固、 可擴充且可靠的掉落取代 MySQL） toowork 在 Azure 上的高可用性環境中虛擬機器。

## <a name="architecture-overview"></a>架構概觀
本文說明如何 toocomplete hello 下列步驟：

- 建立一個三節點的叢集。
- 從 hello OS 磁碟個別 hello 資料磁碟。
- 建立在 RAID 0/等量設定 tooincrease IOPS 的 hello 資料磁碟。
- 使用 Azure 負載平衡器 toobalance hello 負載 hello 三個節點。
- toominimize 重複性工作、 建立包含 MariaDB + Galera 的 VM 映像，並使用它 toocreate hello 另一個叢集 Vm。

![系統架構](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> 本主題使用 hello [Azure CLI](../../../cli-install-nodejs.md)工具，因此請確定 toodownload 它們並且將它們連接 tooyour Azure 訂用帳戶相應 toohello 指示。 如果您需要提供 hello Azure CLI 參考 toohello 命令，請參閱 hello [Azure CLI 命令參考](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。 您也需要太[建立 SSH 金鑰驗證]並記下 hello.pem 檔案位置。
>
>

## <a name="create-hello-template"></a>建立 hello 範本
### <a name="infrastructure"></a>基礎結構
1. 一起建立同質群組 toohold hello 的資源。

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. 建立虛擬網路。

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. 建立儲存體帳戶 toohost 所有的磁碟。 您不應該超過 40 重度使用的磁碟置於 hello 相同儲存體帳戶 tooavoid 達到 hello 20000 IOPS 儲存體帳戶限制。 在此情況下，您低於該限制，因此您將會儲存所有項目上使用相同帳戶執行簡單的 hello。

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. 尋找 hello hello CentOS 7 虛擬機器映像名稱。

        azure vm image list | findstr CentOS
   hello 輸出將會類似`5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`。

   Hello 下列步驟中使用該名稱。
5. 建立 hello VM 範本，並取代 /path/to/key.pem hello 路徑產生的 hello.pem SSH 金鑰的儲存位置。

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. 將連接用於 hello RAID 組態中的四個 500 GB 資料磁碟 toohello VM。

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. 使用 SSH toosign toohello 範本中 mariadbhatemplate.cloudapp.net:22，在您建立的 VM，然後使用您的私密金鑰的連線。

### <a name="software"></a>軟體
1. 取得 hello 根目錄。

        sudo su

2. 安裝 RAID 支援：

    a. 安裝 mdadm。

              yum install mdadm

    b. 使用 EXT4 檔案系統中建立 hello RAID0/等量磁碟區設定。

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. 建立 hello 掛接點目錄。

              mkdir /mnt/data
    d. 擷取 hello hello 新建立的 RAID 裝置的 UUID。

              blkid | grep /dev/md0
    e. 編輯 /etc/fstab。

              vi /etc/fstab
    f. 新增 hello 裝置 tooenable 自動掛接在重新開機，使用 hello 值來取代 hello UUID 取自先前 hello **blkid**命令。

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. 掛接 hello 新磁碟分割。

              mount /mnt/data

3. 安裝 MariaDB。

    a. 建立 hello MariaDB.repo 檔案。

                vi /etc/yum.repos.d/MariaDB.repo

    b. 填滿 hello 儲存機制檔案，以下列內容的 hello:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid 衝突，請移除現有的後置和 mariadb 程式庫。

           yum remove postfix mariadb-libs-*
    d. 使用 Galera 安裝 MariaDB。

           yum install MariaDB-Galera-server MariaDB-client galera

4. 移動 hello MySQL 資料目錄 toohello RAID 封鎖裝置。

    a. 將 hello 目前 MySQL 目錄複製到新位置，並移除 hello 舊的目錄。

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. 據以設定 hello 新目錄的權限。

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. 建立指向 hello 舊目錄 toohello 新位置 hello RAID 磁碟分割上的符號連結。

           ln -s /mnt/data/mysql /var/lib/mysql

5. 因為[SELinux 干擾 hello 叢集操作](http://galeracluster.com/documentation-webpages/configuration.html#selinux)，它是必要的 toodisable 它 hello 目前工作階段。 編輯`/etc/selinux/config`toodisable 後續重新啟動它。

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. 驗證 MySQL 執行。

   a. 啟動 MySQL。

           service mysql start
   b. 安全 hello MySQL 安裝、 設定 hello 根密碼、 移除匿名使用者 toodisable 遠端根登入，然後移除 hello 測試資料庫。

           mysql_secure_installation
   c. 針對叢集操作，以及 （選擇性） 您的應用程式的 hello 資料庫上建立的使用者。

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. 停止 MySQL。

            service mysql stop
7. 建立組態預留位置。

   a. 編輯 hello MySQL 組態 toocreate hello 叢集設定的預留位置。 不會取代 hello  **`<Variables>`** 或取消註解現在。 從此範本建立 VM 之後才會需要這個動作。

            vi /etc/my.cnf.d/server.cnf
   b. 編輯 hello  **[galera]** 區段，並清除它。

   c. 編輯 hello **[mariadb]** > 一節。

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
8. 使用 FirewallD CentOS 7 上，以開啟 hello 防火牆上的必要連接埠。

   * MySQL： `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * 重新載入 hello 防火牆：`firewall-cmd --reload`

9. 最佳化效能的 hello 系統。 如需詳細資訊，請參閱[效能調整策略](optimize-mysql.md)。

   a. 再次編輯 hello MySQL 組態檔。

            vi /etc/my.cnf.d/server.cnf
   b. 編輯 hello **[mariadb]**區段，並新增下列內容的 hello:

   > [!NOTE]
   > 我們建議 innodb\_buffer\_pool_size 是 VM 記憶體的 70%。 在此範例中，它已設定為 2.45 GB hello 媒體 Azure VM，3.5 gb 的 RAM。
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. 停止 MySQL、 MySQL 服務上啟動 tooavoid 中斷 hello 叢集加入節點，當執行停用及解除佈建 hello 機器。

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. 擷取 hello VM 透過 hello 入口網站。 (目前，[發出 hello Azure CLI 工具中的 # 1268年](https://github.com/Azure/azure-xplat-cli/issues/1268)描述 hello 事實 hello Azure CLI 工具所擷取的映像不會擷取 hello 附加資料磁碟。)

    a. 關閉 hello 機器透過 hello 入口網站。

    b. 按一下**擷取**和 hello 映像名稱指定為**mariadb galera 映像**。 提供描述並核取「我已執行 waagent」。
      
      ![擷取 hello 虛擬機器](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>建立 hello 叢集
使用您建立，然後設定並啟動 hello 叢集 hello 範本建立三個 Vm。

1. 建立的 hello hello mariadb galera 映像中的第一個 CentOS 7 VM 映像中建立，提供下列資訊的 hello:

 - 虛擬網路名稱︰mariadbvnet
 - 子網路︰mariadb
 - 機器大小：中型
 - 雲端服務名稱： mariadbha （或您想 toobe mariadbha.cloudapp.net 透過存取的任何名稱）
 - 機器名稱：mariadb1
 - 使用者名稱：azureuser
 - SSH 存取權︰已啟用
 - 傳送嗨 SSH 憑證.pem 檔案，並以您儲存 hello hello 路徑取代 /path/to/key.pem 產生.pem SSH 金鑰。

   > [!NOTE]
   > hello 下列命令會分成多行為了清楚起見，但您應輸入各以一行。
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
2. 建立兩個的多個虛擬機器連接這些 toohello mariadbha 雲端服務。 變更 hello VM 名稱和 SSH 連接埠 tooa 唯一連接埠與中的其他 Vm 不衝突 hello hello 相同雲端服務。

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
  對於 MariaDB3：

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
3. 您需要 tooget hello 內部 IP 位址的每個 hello 三個 Vm 的 hello 下一個步驟：

    ![取得 IP 位址](./media/mariadb-mysql-cluster/IP.png)
4. 使用 SSH toosign toohello 三個 Vm 中，並且編輯每個 hello 設定檔。

        sudo vi /etc/my.cnf.d/server.cnf

    請取消註解 **`wsrep_cluster_name`** 和 **`wsrep_cluster_address`** 藉由移除 hello  **#**  hello hello 該行開頭。
    此外，取代 **`<ServerIP>`** 中 **`wsrep_node_address`** 和 **`<NodeName>`** 中 **`wsrep_node_name`** 以 helloVM 的 IP 位址和名稱，分別以及這些行取消註解。
5. 啟動 hello 叢集上 MariaDB1 並讓它在啟動時執行。

        sudo service mysql bootstrap
        chkconfig mysql on
6. 啟動 MariaDB2 與 MariaDB3 上的 MySQL，並讓它在啟動時執行。

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>負載平衡 hello 叢集
當您建立叢集的 hello Vm 時，您會加入它們至可用性設定組呼叫 clusteravset tooensure 它們被放置在不同容錯網域和更新網域上和，Azure 絕不會維護在所有機器上的一次。 此設定符合 hello toobe 支援 hello Azure 服務等級協定 (SLA) 的需求。

現在使用 hello 三個節點之間的 Azure 負載平衡器 toobalance 要求。

執行下列命令在您的電腦上，使用 Azure CLI hello hello。

hello 命令參數結構是：`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

hello CLI 設定 hello 負載平衡器探查間隔 too15 秒數，這可能是一個位元太長。 變更在 hello 管理入口網站下**端點**任何 hello Vm。

![編輯端點](./media/mariadb-mysql-cluster/Endpoint.PNG)

選取**Reconfigure hello Load-Balanced 設定**。

![重新設定 hello 負載平衡集](./media/mariadb-mysql-cluster/Endpoint2.PNG)

變更**探查間隔**too5 的秒數，並儲存變更。

![變更探查間隔](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>驗證 hello 叢集
hello 硬碟的工作完成。 hello 叢集必須能夠立即存取在`mariadbha.cloudapp.net:3306`、 的點擊 hello 負載平衡器和之間的路由要求 hello 三個 Vm，順暢而有效率地。

使用您最愛的 MySQL 用戶端 tooconnect，或從這個叢集正在運作的 hello Vm tooverify 的其中一個連接。

     mysql -u cluster -h mariadbha.cloudapp.net -p

然後建立資料庫並填入一些資料。

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

您所建立的 hello 資料庫傳回下表中的 hello:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
在本文中，您在執行 CentOS 7 的 Azure 虛擬機器上建立了三個節點的 MariaDB + Galera 高可用性叢集。 hello Vm 進行負載平衡與 Azure 負載平衡器。

您可能會想在 toolook[另一個方式 toocluster Linux 上的 MySQL](mysql-cluster.md)以及方式太[最佳化和測試 Azure Linux Vm 上的 MySQL 效能](optimize-mysql.md)。

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
