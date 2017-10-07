---
title: "在 Linux 上的 MySQL 效能 aaaOptimize |Microsoft 文件"
description: "深入了解如何 toooptimize MySQL Azure 虛擬機器 (VM) 執行 Linux 上執行。"
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>在 Azure Linux 上最佳化 MySQL 效能
有許多因素會影響 Azure 上的 MySQL 效能，均與虛擬硬體選取和軟體設定有關。 本文著重於透過儲存體、系統和資料庫設定最佳化效能。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。 本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 Linux VM 最佳化與 hello 資源管理員模型的相關資訊，請參閱[最佳化您的 Linux VM 在 Azure 上](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>在 Azure 虛擬機器上利用 RAID
儲存體是 hello 會影響雲端環境中的資料庫效能的關鍵因素。 比較的 tooa 單一磁碟，RAID 可提供透過並行存取速度。 如需詳細資訊，請參閱[標準 RAID 層級](http://en.wikipedia.org/wiki/Standard_RAID_levels)。   

可透過 RAID 改進 Azure 中的磁碟 I/O 輸送量和 I/O 回應時間。 我們的實驗室測試顯示磁碟 I/O 輸送量可以兩倍，且 I/O 回應時間可以降低一半平均的 RAID 磁碟 hello 數目會加倍 （從兩個 toofour、 四個 tooeight 等）。 如需詳細資訊，請參閱 [附錄 A](#AppendixA) 。  

此外 toodisk I/O MySQL 效能會提升增加 hello RAID 層級。  如需詳細資訊，請參閱 [附錄 B](#AppendixB) 。  

您也可以 tooconsider hello 區塊大小。 通常當您有較大的區塊大小時，您的額外負荷會比較低，尤其是大量寫入時。 不過，hello 區塊大小太大時，它可能會加入額外負擔，使您無法利用 RAID。 hello 目前的預設大小為 512 KB，證明 toobe 最常見的實際執行環境的最佳選擇。 如需詳細資訊，請參閱 [附錄 C](#AppendixC) 。   

您可針對不同虛擬機器類型新增的磁碟數目會有所限制。 [Azure 的虛擬機器和雲端服務大小](http://msdn.microsoft.com/library/azure/dn197896.aspx)中有這些限制的詳細說明。 雖然您可以選擇 tooset RAID 設定具有較少的磁碟，您將需要四個連接的資料磁碟 toofollow hello RAID 範例在本文中。  

本文假設您已經建立 Linux 虛擬機器並已安裝及設定 MYSQL 。 如需有關如何開始使用的詳細資訊，請參閱 < 如何在 Azure 上 MySQL tooinstall。  

### <a name="set-up-raid-on-azure"></a>在 Azure 上設定 RAID
hello 下列步驟說明在 Azure 上 toocreate RAID hello Azure 入口網站的使用方式。 您也可以使用 Windows PowerShell 指令碼設定 RAID。
在此範例中，我們將設定具有四個磁碟的 RAID 0。  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>新增資料磁碟 tooyour 虛擬機器
在 hello Azure 入口網站，移 toohello 儀表板，然後選取您想要的資料磁碟 tooadd hello 虛擬機器 toowhich。 在此範例中，hello 虛擬機器是 mysqlnode1。  

<!--![Virtual machines][1]-->

按一下 磁碟，然後按一下連結新項目。

![虛擬機器新增磁碟](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

建立一個新的 500 GB 磁碟。 請確定**主機快取喜好設定**設定得**無**。  完成時，請按一下 [確定] 。

![連接空的磁碟](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


這會將一個空的磁碟新增到虛擬機器中。 再重複執行此步驟三次，您的 RAID 就有四個資料磁碟。  

您可以查看加入 hello 藉由查看 hello 核心訊息記錄檔中 hello 虛擬機器磁碟機。 例如，toosee 這在 Ubuntu，下列命令使用 hello:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>建立以 hello 更多磁碟的 RAID
hello 下列步驟說明如何太[設定軟體 RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

> [!NOTE]
> 如果您使用 hello XFS 檔案系統，執行下列步驟之後您已經建立 RAID, hello。
>
>

在 Debian，Ubuntu 或 Linux 迷你澆，下列命令使用 hello tooinstall XFS:  

    apt-get -y install xfsprogs  

tooinstall XFS 上 Fedora、 CentOS、 或 RHEL、 使用 hello，下列命令：  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>設定新的儲存體路徑
使用下列新的儲存體路徑的命令 tooset hello:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>複製 hello 原始資料 toohello 新儲存體路徑
使用下列命令 toocopy 資料 toohello 新儲存體路徑 hello:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>修改權限，因此可以存取 MySQL （讀取和寫入） hello 資料磁碟
使用下列命令 toomodify 權限的 hello:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>調整排程演算法 hello 磁碟 I/O
Linux 會實作四種類型的 I/O 排程演算法：  

* NOOP 演算法 (沒有作業)
* 期限演算法 (期限)
* 完全公平佇列演算法 (CFQ)
* 預算週期演算法 (預期)  

您可以選取不同的 I/O 排程器，在不同的案例 toooptimize 效能。 在完全隨機存取環境中，沒有顯著的差異 hello CFQ 以及期限之演算法的效能。 我們建議您設定 hello MySQL 資料庫環境 tooDeadline 的穩定性。 如果有大量循序 I/O，CFQ 可能會降低磁碟 I/O 效能。   

針對 SSD 和其他設備，NOOP 或期限可以達到較佳的效能比 hello 預設排程器。   

先前 toohello 核心 2.5，hello 預設 I/O 排程演算法會是期限。 從開始 hello 核心 2.6.18，CFQ 變成 hello 預設 I/O 排程演算法。  您可以指定此設定會在核心開機時，或 hello 系統正在運作時，動態修改此設定。  

下列範例中的 hello 示範 toocheck 以及組 hello hello Debian 發佈系列中的預設排程器 toohello NOOP 演算法。  

### <a name="view-hello-current-io-scheduler"></a>檢視 hello 目前 I/O 排程器
tooview hello 排程器執行下列命令的 hello:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

您會看到下列輸出，指出目前排程器 hello:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>變更 hello 目前裝置 (/ 開發/sda) hello I/O 排程演算法
執行下列命令 toochange hello 目前裝置 hello:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> 單獨針對 /dev/sda 設定此項並不是很有用。 它必須設定所有資料磁碟上 hello 資料庫所在的位置。  
>
>

您應該會看到下列輸出，表示已成功重建 grub.cfg，且該 hello 預設排程器已更新的 tooNOOP hello:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Hello Red Hat 發佈系列，您只需要 hello 下列命令：

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>設定系統檔案作業設定
一個最佳作法是 toodisable hello *atime* hello 檔案系統上的記錄功能。 Atime 是 hello 上次檔案存取時間。 存取檔案，每當 hello 檔案系統記錄 hello hello 記錄檔中的時間戳記。 不過，很少使用這項資訊。 如果您不需要它，可予以停用，將會減少整體的磁碟存取時間。  

toodisable atime 記錄，您需要 toomodify hello 檔案系統的組態檔 /etc/ fstab 並新增 hello **noatime**選項。  

例如，編輯 hello vim /etc/fstab 檔案，新增 hello noatime hello 下列範例所示：  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

然後，重新 hello 檔案系統掛接具有 hello 下列命令：  

    mount -o remount /RAID0

測試 hello 修改結果。 當您修改 hello 測試檔案時，不會更新 hello 存取時間。 下列範例會顯示哪些 hello 程式碼看起來像，修改前後的 hello。

之前：        

![存取修改前的程式碼][5]

之後︰

![存取修改後的程式碼][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>增加 hello 系統的高並行處理的控制代碼的數目上限
MySQL 是高並行存取資料庫。 並行控制代碼的 hello 預設數目為 1024，對於 Linux，這並不足夠。 使用下列步驟 tooincrease hello 最大並行控制代碼的 MySQL 的 hello 系統 toosupport 高並行的 hello。

### <a name="modify-hello-limitsconf-file"></a>修改 hello limits.conf 檔案
tooincrease hello 最大允許並行的控制代碼，並將下列四個線條 hello /etc/security/limits.conf 檔案中的 hello。 請注意，65536 hello hello 系統可支援的最大數目。   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>更新 hello 新限制的 hello 系統
tooupdate hello 系統，執行下列命令的 hello:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>請確定在開機時，會更新 hello 限制
Put 的 hello 遵循 hello /etc/rc.local 檔案中的啟動命令，如此它在開機時才會生效。  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>MySQL 資料庫最佳化
您可以使用 tooconfigure 在 Azure 上 MySQL，hello 您在內部部署電腦使用相同的效能調整的策略。  

hello 主要 I/O 最佳化規則如下：   

* Hello 快取大小增加。
* 減少 I/O 回應時間。  

toooptimize MySQL 伺服器的設定，您可以更新 hello my.cnf 檔案，這是伺服器和用戶端電腦的 hello 預設組態檔。  

hello 下列設定項目是 hello 影響 MySQL 效能的主要因素：  

* **innodb_buffer_pool_size**: hello 緩衝集區包含經過緩衝處理的資料與 hello 索引。 此設定通常 too70 的實體記憶體的百分比。
* **innodb_log_file_size**： 這是 hello 重做記錄檔大小。 您使用的寫入作業將會快速、 可靠且可復原損毀之後的重做記錄檔 tooensure。 這會設定 too512 MB，這樣會提供您足夠的空間的寫入作業記錄。
* **max_connections**：應用程式有時不會正確關閉連線。 較大的值會讓伺服器 hello toorecycle 閒置連線的更多時間。 hello 的連線數目上限為 10000，但是 hello 建議的最大值是 5000。
* **Innodb_file_per_table**： 此設定啟用或停用 hello 能力 InnoDB toostore 資料表在個別的檔案。 開啟 hello 選項 tooensure 可以有效地套用數個進階的管理作業。 從效能觀點來看，它可以加速 hello 資料表空間傳輸，並將 hello 瓦礫管理效能最佳化。 hello 建議使用這個選項的設定是 ON。</br></br>
從 MySQL 5.6 hello 預設設定是 ON，因此不不需要任何動作。 針對先前的版本，hello 預設設定為 OFF。 hello 應該變更設定之前已載入資料，因為只有新建立的資料表會受到影響。
* **innodb_flush_log_at_trx_commit**: hello 預設值為 1，以 hello 範圍設定 too0 ~ 2。 hello 預設值為 hello 獨立 MySQL 資料庫最適合的選項。 hello 設定 2 啟用 hello 大部分的資料完整性，並適用於 MySQL 的叢集中的主機。 hello 值為 0 可讓資料遺失，可能會影響可靠性 （在某些情況下，效能更佳），以及適用於 MySQL 的叢集中的從屬版本。
* **Innodb_log_buffer_size**: hello 記錄緩衝區而不需要 tooflush hello 記錄 toodisk hello 交易認可之前允許交易 toorun。 不過，如果沒有大型二進位物件或文字欄位，hello 快取將會快速耗盡，而且經常磁碟 I/O，將會觸發。 它是進一步增加 hello 的緩衝區大小，如果 Innodb_log_waits 狀態變數不是 0。
* **query_cache_size**: hello 最好的選擇是 toodisable 從 hello 開始。 設定 query_cache_size too0 （這是 MySQL 5.6 hello 預設設定），並使用其他的方法 toospeed 機操作查詢。  

請參閱[附錄 D](#AppendixD)前後 hello 最佳化效能的比較。

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>開啟分析 hello 效能瓶頸的 hello MySQL 慢速查詢記錄檔
hello MySQL 慢速查詢記錄檔可協助您識別用於 MySQL 的 hello 慢速查詢。 啟用 hello MySQL 慢速查詢記錄檔之後，您可以使用 MySQL 工具，像是**mysqldumpslow** tooidentify hello 效能瓶頸。  

預設不會啟用此項目。 開啟 hello 慢速查詢記錄檔可能會耗用一些 CPU 資源。 我們建議您暫時啟用這個選項，以便排解效能瓶頸。 tooturn hello 慢速查詢記錄檔：

1. 修改 hello my.cnf 檔案有新增下列幾行 toohello 結束 hello:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. 重新啟動 hello MySQL 伺服器。

        service  mysql  restart

3. 檢查是否 hello 設定生效使用 hello**顯示**命令。

![Slow-query-log ON][7]   

![Slow-query-log 結果][8]

在此範例中，您可以查看已開啟該 hello 緩慢的查詢功能。 然後，您可以使用 hello **mysqldumpslow**工具 toodetermine 效能瓶頸，並最佳化效能，例如加入索引。

## <a name="appendices"></a>附錄
hello 以下是在目標的實驗室環境中所產生的範例效能測試資料。 提供在 hello 效能資料趨勢的一般背景，具有不同的效能微調方法。 hello 結果可能會因不同的環境或產品版本而異。

### <a name="AppendixA"></a>附錄 A  
**不同 RAID 層級的磁碟效能 (IOPS)**

![不同 RAID 層級的磁碟 IOPS][9]

**測試命令**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> hello 工作負載的這項測試會使用 64 個執行緒，嘗試的 RAID tooreach hello 時間上限。
>
>

### <a name="AppendixB"></a>附錄 B  
**不同 RAID 層級的 MySQL 效能 (輸送量) 比較**   
(XFS檔案系統)

![不同 RAID 層級的 MySQL 效能比較][10]  
![不同 RAID 層級的 MySQL 效能比較][11]

**測試命令**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**不同 RAID 層級的 MySQL 效能 (OLTP) 比較**  
![不同 RAID 層級的 MySQL 效能 (OLTP) 比較][12]

**測試命令**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>附錄 C   
**不同區塊大小的磁碟效能 (IOPS) 比較**  
(XFS檔案系統)

![][13]

**測試命令**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

使用這項測試的 hello 檔案大小 30 GB 和 1 GB，分別為，與 RAID 0 （4 個磁碟） XFS 檔案系統。

### <a name="AppendixD"></a>附錄 D  
**最佳化之前和之後的 MySQL 效能 (輸送量) 比較**  
(XFS檔案系統)

![最佳化之前和之後的 MySQL 效能 (輸送量) 比較][14]

**測試命令**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**預設和最佳化 hello 組態設定如下所示：**

| 參數 | 預設值 | 最佳化 |
| --- | --- | --- |
| **innodb_buffer_pool_size** |None |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

更多詳細的[最佳化組態參數](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html)，請參閱 toohello [MySQL 官方指示](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method)。  

  **測試環境**  

| 硬體 | 詳細資料 |
| --- | --- |
| CPU |AMD Opteron(tm) 處理器 4171 HE/4 核心 |
| 記憶體 |14 GB |
| 磁碟 |10 GB/磁碟 |
| 作業系統 |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

