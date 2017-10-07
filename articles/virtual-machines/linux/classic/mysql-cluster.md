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
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>使用 Linux 上的負載平衡集 tooclusterize MySQL
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 A [Resource Manager 範本](https://azure.microsoft.com/documentation/templates/mysql-replication/)時才能使用需要 toodeploy MySQL 叢集。

這篇文章探討，並說明 hello 不同的方法可用 toodeploy 高可用性以 Linux 為基礎的服務在 Microsoft Azure 中，瀏覽做為入門的 MySQL Server 高可用性。 您可在 [第 9 頻道](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)(英文) 上找到說明此方法的影片。

我們會依據 DRBD、Corosync 和 Pacemaker，說明無共用、兩個節點、單一主要的 MySQL 高可用性解決方案。 一次只會有一個節點執行 MySQL。 讀取和寫入從 hello DRBD 資源也是有限的 tooonly 一個節點一次。

沒有 LVS，像是 VIP 解決方案需要，因為您將使用在 Microsoft Azure tooprovide 循環配置資源的功能和端點偵測、 移除和依正常程序復原 hello VIP 的負載平衡集。 hello VIP 是指派的 Microsoft Azure，當您初次建立 hello 雲端服務的全域路由傳送 IPv4 位址。

還有其他可能架構可供 MySQL 使用，包括 NBD 叢集、Percona、Galera 以及數種中繼軟體解決方案 (包括至少有一個可作為 [VM Depot](http://vmdepot.msopentech.com) 上的 VM)。 只要這些解決方案可以複寫在單點傳播與多點傳送或廣播，而不依賴共用存放裝置或多個網路介面，hello 案例應該在 Microsoft Azure 上的簡單 toodeploy。

這些叢集架構可以延伸 tooother 產品，例如 PostgreSQL 和 OpenLDAP 不要以類似的方式。 例如，已透過多個主要 OpenLDAP 成功測試使用無共用的負載平衡程序，您可以在我們的第 9 頻道 (Channel 9) 部落格上觀看此測試。

## <a name="get-ready"></a>準備就緒
您需要 hello 下列資源與能力：

  - Microsoft Azure 帳戶與有效的訂閱，無法 toocreate 至少兩個 Vm （XS 已在此範例中使用）
  - 網路和子網路
  - 同質群組
  - 可用性設定組
  - hello 能力 toocreate Vhd 在 hello 與 hello 雲端服務相同的區域，並且將它們附加 toohello Linux Vm

### <a name="tested-environment"></a>測試環境
* Ubuntu 13.10
  * DRBD
  * MySQL Server
  * Corosync 和 Pacemaker

### <a name="affinity-group"></a>同質群組
登入 toohello Azure 傳統入口網站建立同質群組 hello 解決方案選取**設定**，以及建立同質群組。 配置的資源建立稍後將會指派 toothis 同質群組。

### <a name="networks"></a>網路
建立新的網路時，並在 hello 網路內建立子網路。 此範例使用內部只有一個 /24 子網路的 10.10.10.0/24 網路。

### <a name="virtual-machines"></a>虛擬機器
第一個 Ubuntu 13.10 VM 建立使用 Endorsed Ubuntu 圖庫映像，並呼叫的 hello `hadb01`。 Hello 處理程序稱為 hadb 中建立新的雲端服務。 這個名稱會說明 hello 共用，請加入更多資源時，會有 hello 服務的負載平衡本質。 hello 建立`hadb01`使用 hello 入口網站是較為簡單和已完成。 SSH 的端點會自動建立，並已選取 hello 新網路。 現在您可以建立可用性設定組 hello Vm。

Hello （技術上來說，建立 hello 雲端服務） 時，會建立第一個 VM 之後, 建立 hello 第二個 VM， `hadb02`。 Hello 第二個 VM、 hello 圖庫使用 Ubuntu 13.10 VM，請使用 hello 入口網站，但使用現有的雲端服務， `hadb.cloudapp.net`，而不是建立一個新。 應該會自動選取 hello 網路和可用性設定組。 並建立 SSH 端點。

建立兩個 Vm 之後，記下 hello SSH 連接埠`hadb01`(TCP 22) 和`hadb02`（自動由 Azure 指派）。

### <a name="attached-storage"></a>連接的儲存體
連接新的磁碟 tooboth Vm，然後在 hello 程序中建立 5 GB 的磁碟。 hello 磁碟會裝載於您的主要作業系統磁碟的使用中的 hello VHD 容器。 建立並附加磁碟之後，沒有任何需要 toorestart Linux 因為 hello 核心會看到 hello 新裝置。 此裝置通常是 `/dev/sdc`。 請檢查`dmesg`hello 輸出。

在每個 VM 上建立的分割區使用`cfdisk`（主要 Linux 磁碟分割） 和寫入 hello 新磁碟分割表格。 請勿在此磁碟分割上建立檔案系統。

## <a name="set-up-hello-cluster"></a>設定 hello 叢集
在這兩個 Ubuntu Vm 上使用 APT tooinstall Corosync、 Pacemaker 和 DRBD。 toodo 因此與`apt-get`，請執行 hello 下列程式碼：

    sudo apt-get install corosync pacemaker drbd8-utils.

此時請勿安裝 MySQL。 Debian 和 Ubuntu 安裝指令碼將會在初始化 MySQL 資料目錄`/var/lib/mysql`，但是因為 hello 目錄將會取代 DRBD 檔案系統中，您需要稍後 tooinstall MySQL。

驗證 (使用`/sbin/ifconfig`)，這兩個 Vm 使用 hello 10.10.10.0/24 子網路中的位址，及它們可以依照名稱 ping 彼此。 您也可以使用`ssh-keygen`和`ssh-copy-id`toomake 確定這兩個 Vm 可透過 SSH 通訊而不需要密碼。

### <a name="set-up-drbd"></a>設定 DRBD
建立會使用基礎 hello DRBD 資源`/dev/sdc1`分割 tooproduce`/dev/drbd1`可以使用 ext3 格式化，並在主要和次要節點中使用的資源。

1. 開啟`/etc/drbd.d/r0.res`並複製 hello 遵循這兩個 Vm 上的資源定義：

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

2. 使用初始化 hello 資源`drbdadm`這兩個 Vm 上：

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. 在 hello 主要 VM (`hadb01`)，強制的 hello DRBD 資源的擁有權 （主要）：

        sudo drbdadm primary --force r0

如果您檢查/proc/drbd hello 內容 (`sudo cat /proc/drbd`) 在這兩個 Vm，您應該看到`Primary/Secondary`上`hadb01`和`Secondary/Primary`上`hadb02`、 與 hello 方案此時一致。 hello 5 GB 的磁碟會透過任何費用 toocustomers hello 10.10.10.0/24 網路同步處理。

同步處理 hello 磁碟之後，您可以建立 hello 檔案系統上`hadb01`。 為了測試用途，我們使用 ext2，但 hello 下列程式碼會建立 ext3 檔案系統：

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>掛接 hello DRBD 資源
您現在準備好 toomount hello DRBD 資源`hadb01`。 Debian 及其衍生版本會使用 `/var/lib/mysql` 做為 MySQL 的資料目錄。 因為您尚未安裝 MySQL，請建立 hello 目錄，並掛接 hello DRBD 資源。 tooperform 這個選項時，執行下列程式碼的 hello `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>設定 MySQL
現在您已準備好 tooinstall MySQL 上`hadb01`:

    sudo apt-get install mysql-server

在 `hadb02`中，您有兩個選擇。 您可以安裝 mysql 伺服器，這樣會建立 /var/lib/mysql，填入新的資料目錄，然後移除 hello 的內容。 tooperform 這個選項時，執行下列程式碼的 hello `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

hello 第二個選項太 toofailover`hadb02`並安裝 mysql 伺服器那里。 安裝指令碼將會注意到 hello 現有安裝，並不會修改它。

執行 hello 下列程式碼上`hadb01`:

    sudo drbdadm secondary –force r0

執行 hello 下列程式碼上`hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

如果您現在不打算 toofailover DRBD，hello 第一個選項是雖然論證那麼漂亮更容易。 安裝完成後，您可以開始使用 MySQL 資料庫。 執行 hello 下列程式碼上`hadb02`（或任一個的 hello 伺服器是作用中，根據 tooDRBD）：

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> 這個最後一個陳述式即可有效停用此資料表中的 hello 根使用者的驗證。 這應由您的生產等級 GRANT 陳述式取代，這裡僅是為了說明的目的才包括此陳述式。

如果您想從外部 hello Vm （這是本指南用途 hello） toomake 查詢時，您也需要 tooenable MySQL 的網路功能。 在這兩個 Vm 上開啟`/etc/mysql/my.cnf`並移過`bind-address`。 變更 hello 位址 127.0.0.1 從 too0.0.0.0。 在儲存 hello 檔案之後, 發出`sudo service mysql restart`您目前的主要伺服器上。

### <a name="create-hello-mysql-load-balanced-set"></a>建立 hello MySQL 負載平衡集
返回 toohello 入口網站，請移過`hadb01`，然後選擇 **端點**。 toocreate 的端點，選擇 MySQL (TCP 3306) hello 下拉式清單並選取從**建立新的負載平衡集**。 名稱 hello 負載平衡的端點`lb-mysql`。 設定**時間**too5 秒，最小值。

建立 hello 端點之後，請繼續太`hadb02`，選擇**端點**，並建立端點。 選擇`lb-mysql`，然後從 hello 下拉式清單中選取 MySQL。 您也可以使用 Azure CLI hello 這個步驟。

您現在可以 hello 叢集的手動作業所需的所有項目。

### <a name="test-hello-load-balanced-set"></a>測試 hello 負載平衡集
您可以使用任何 MySQL 用戶端，或使用特定應用程式 (例如以 Azure 網站身分執行的 phpMyAdmin)，從機器外部執行測試。 在此案例中，您在另一個 Linux 方塊上使用 MySQL 的命令列工具：

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>手動容錯移轉
您可以透過關閉 MySQL、切換 DRBD 的主要 VM，然後重新啟動 MySQL 來模擬容錯移轉。

tooperform 這個工作中，執行下列程式碼上 hadb01 hello:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

接著，在 hadb02 上：

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

手動容錯移轉後，您可以重複遠端查詢，它應可正常運作。

## <a name="set-up-corosync"></a>設定 Corosync
Corosync 是所需的 Pacemaker toowork hello 基礎叢集基礎結構。 活動訊號 （和其他方法，例如 Ultramonkey） Corosync 對於分割的 hello CRM 功能，Pacemaker 仍比較類似 tooHeartbeat 功能時。

hello 主要條件約束 Corosync 在 Azure 上的是 Corosync 慣用透過廣播多點傳送透過單點傳播通訊，但 Microsoft Azure 網路只支援單點傳播。

還好，Corosync 具備有效的單點傳送模式。 hello 唯一實際的條件約束是，因為所有節點並未在彼此都通訊，您需要 toodefine hello 節點在您的組態檔，包括其 IP 位址。 單點傳播與變更繫結位址、 節點清單，以及記錄目錄，我們可以使用 hello Corosync 範例檔案 (使用 Ubuntu `/var/log/corosync` hello 範例檔案使用時`/var/log/cluster`)，並啟用仲裁工具。

> [!NOTE]
> 使用下列 hello`transport: udpu`指示詞和 hello 手動定義兩個節點的 IP 位址。

執行 hello 下列程式碼上`/etc/corosync/corosync.conf`兩個節點：

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

複製兩部 VM 上的這個組態檔，並在這兩個節點中啟動 Corosync：

    sudo service start corosync

後，馬上開始 hello 服務，hello 叢集應該建立 hello 目前環形，而且應該 constituted 仲裁。 我們可以檢查這項功能，藉由檢閱記錄檔，或藉由執行下列程式碼的 hello:

    sudo corosync-quorumtool –l

您會看到下列映像的輸出類似 toohello:

![corosync-quorumtool -l sample output](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>設定 Pacemaker
Pacemaker 使用 hello 資源的叢集 toomonitor、 定義主要複本會跟著中斷，並切換這些資源 toosecondaries。 在所有其他選擇中，您可從一組可用指令碼或從 LSB (如 init) 指令碼來定義資源。

我們想要 Pacemaker 太"自己的"hello DRBD 資源、 hello 掛接點，以及 hello MySQL 服務。 如果 Pacemaker 可以開啟和關閉 DRBD，掛接和卸載，並再啟動和停止 MySQL 中 hello 向右的順序不正確的項目時，即會發生以 hello 主要安裝程式完成。

首次安裝 Pacemaker 時，您的組態應十分簡單，如下所示：

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. 執行檢查 hello 組態`sudo crm configure show`。
2. 然後建立檔案 (例如`/tmp/cluster.conf`) 以 hello 下列資源：

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

3. Hello 檔案載入 hello 組態。 您只需要 toodo 這在一個節點。

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. 請確定開機時會啟動兩個節點的 Pacemaker：

        sudo update-rc.d pacemaker defaults

5. 使用`sudo crm_mon –L`，確認其中一個節點已經成為 hello hello 叢集主機，並正在 hello 的所有資源。 您可以使用裝載與 ps toocheck hello 資源正在執行。

下列螢幕擷取畫面顯示 hello`crm_mon`具有一個節點停止 （藉由選取 Ctrl + C 結束）：

![crm_mon node stopped](./media/mysql-cluster/image002.png)

此快照說明兩個節點 (一個主要和一個從屬)：

![crm_mon operational master/slave](./media/mysql-cluster/image003.png)

## <a name="testing"></a>測試
您已準備好開始自動容錯移轉模擬。 有兩種方式 toodo 這： 彈性和固定。

hello 彈性的方式使用 hello 叢集關機函式： ``crm_standby -U `uname -n` -v on``。 如果您使用 hello 主機上，hello 從屬會高於。 請記住 tooset 這個回復 toooff。 如果不這麼做，crm_mon 會顯示一個待命中的節點。

hello 不易正在關機而關閉 hello 主要 VM (hadb01) 透過 hello 入口網站，或變更 hello 層上 hello VM，也就是停止 (關機）。 這有助於 Corosync 和 Pacemaker 信號向該 hello 為主版頁面的進行。 您可以測試這種情況 （適用於維護期間），但您也可以強制 hello 案例凍結 hello VM。

## <a name="stonith"></a>STONITH
它應該是可能 tooissue hello Azure CLI 就不需 STONITH 指令碼可控制實體裝置透過 VM 關機。 您可以使用`/usr/lib/stonith/plugins/external/ssh`做為基底和啟用 STONITH hello 叢集組態中的。 Azure CLI 應該全域安裝，而且 hello 發行設定和設定檔應該要載入的 hello 叢集的使用者。

Hello 資源的範例程式碼位於[GitHub](https://github.com/bureado/aztonith)。 加入 hello 太之後變更 hello 叢集設定`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> hello 指令碼不會執行向上/向下檢查。 hello 原始 SSH 資源 15 ping 檢查，但 Azure VM 的復原時間可能是多個變數。

## <a name="limitations"></a>限制
hello 下列限制適用於：

* hello linbit DRBD 資源指令碼為 Pacemaker 使用中的資源管理 DRBD`drbdadm down`時關閉一個節點，即使 hello 節點就會處於待命狀態。 因為 hello 從屬不需要同步處理 hello DRBD 資源 hello master 取得寫入時，這並不理想。 如果 hello master 不 graciously 失敗，hello 從屬伺服器可以接管較舊的檔案系統狀態。 可能解決此問題的方法有兩種：
  * 在所有叢集節點中透過本機 (未叢集化) 看門狗強制執行 `drbdadm up r0`
  * 編輯 hello linbit DRBD 指令碼，並確定`down`中不會呼叫`/usr/lib/ocf/resource.d/linbit/drbd`
* hello 負載平衡器需要至少五秒 toorespond，讓應用程式應該是叢集感知，而且可以容許更多的逾時。 其他架構也可提供協助，例如應用程式內部佇列、查詢中繼軟體等。
* MySQL 微調是寫入可管理的速度完成的必要 tooensure 而快取為可能 toominimize 記憶體遺失經常會排清的 toodisk。
* 寫入效能是在 VM 中相依互連 hello 虛擬交換器，因為這是 hello DRBD tooreplicate hello 裝置使用的機制。
