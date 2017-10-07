---
title: "aaaHigh 可用性的 SAP HANA Azure 虛擬機器 (Vm) 上 |Microsoft 文件"
description: "在 Azure 虛擬機器 (VM) 上，建立 SAP HANA 的高可用性。"
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Azure 虛擬機器 (VM) 上 SAP HANA 的高可用性

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

內部部署，您可以使用任一 HANA 系統複寫，或使用 SAP hana 的共用存放裝置 tooestablish 高可用性。
我們目前只支援在 Azure 上設定 HANA 系統複寫。 SAP HANA 複寫是由一個主要節點以及至少一個從屬節點所組成。 變更 toohello hello 主要節點上的資料會在同步或非同步方式複寫 toohello 從屬節點。

本文說明 toodeploy hello 虛擬機器，設定 hello 虛擬機器的方式、 安裝 hello 叢集架構、 安裝和設定 SAP HANA 系統複寫。
在 hello 範例組態中，安裝命令等執行個體號碼 03 和 HANA 系統識別碼 HDB 用。

讀取 hello 遵循 SAP 附註和白皮書

* SAP Note [1928533]，其中包含：
  * Hello 部署 SAP 軟體所支援的 Azure VM 大小的清單
  * Azure VM 大小的重要容量資訊
  * 支援的 SAP 軟體，以及作業系統 (OS) 與資料庫組合
  * Microsoft Azure 上 Windows 和 Linux 所需的 SAP 核心版本
* SAP Note [2015553] 列出 Azure 中 SAP 支援的 SAP 軟體部署先決條件。
* SAP Note [2205917] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的建議 OS 設定
* SAP Note [1944799] 包含適用於 SUSE Linux Enterprise Server for SAP Applications 的 SAP HANA 指導方針
* SAP Note [2178632] 包含在 Azure 中針對 SAP 回報的所有監視計量詳細資訊。
* SAP 附註[2191498]具有 hello 必要 SAP Host Agent 版本適用於在 Azure 中的 Linux。
* SAP Note [2243692] 包含 Azure 中 Linux 上的 SAP 授權相關資訊。
* SAP Note [1984787] 包含 SUSE LINUX Enterprise Server 12 的一般資訊。
* SAP 附註[1999351] hello Azure 強化監視功能延伸模組適用於 SAP 的其他疑難排解資訊。
* [SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) 包含 Linux 所需的所有 SAP Note。
* [適用於 SAP on Linux 的 Azure 虛擬機器規劃和實作][planning-guide]
* [適用於 SAP on Linux 的 Azure 虛擬機器部署 (本文)][deployment-guide]
* [適用於 SAP on Linux 的 Azure 虛擬機器 DBMS 部署][dbms-guide]
* [SAP HANA SR-IOV 的效能最佳化的案例][ suse-hana-ha-guide] hello 指南包含所有必要的資訊 tooset SAP HANA 系統複寫在內部。 請使用此指南做為基礎。

## <a name="deploying-linux"></a>部署 Linux

SAP hana hello 資源代理程式包含在 SUSE Linux Enterprise Server 中的 SAP 應用程式。
hello Azure Marketplace 包含 BYOS （攜帶您自己訂閱），您可以使用 toodeploy 新的虛擬機器使用的 SAP 應用程式 12 for SUSE Linux Enterprise Server 映像。

### <a name="manual-deployment"></a>手動部署

1. 建立資源群組
1. 建立虛擬網路
1. 建立兩個儲存體帳戶
1. 建立可用性設定組  
   設定更新網域上限
1. 建立負載平衡器 (內部)  
   選取上述步驟的 VNET
1. 建立虛擬機器 1  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   選取儲存體帳戶 1  
   選取可用性設定組  
1. 建立虛擬機器 2  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   選取儲存體帳戶 2   
   選取可用性設定組  
1. 新增資料磁碟
1. Hello 負載平衡器設定
    1. 建立前端 IP 集區
        1. 開啟 hello 負載平衡器，選取前端 IP 集區，然後按一下 [新增]
        1. 輸入 hello hello 前端 IP 集區 （例如前端 hana） 名稱
       1. Click OK
        1. 建立 hello 前端 IP 集區之後，請記下其 IP 位址
    1. 建立後端集區
        1. 開啟 hello 負載平衡器選取後端集區，按一下 [新增]
        1. 輸入 hello 名稱 hello 新後端集區 （例如 hana-後端）
        1. 按一下 [新增虛擬機器]
        1. 選取您稍早建立可用性設定組的 hello
        1. 選取 hello 的 hello SAP HANA 叢集的虛擬機器
        1. Click OK
    1. 建立健康狀態探查
       1. 開啟 hello 負載平衡器選取健全狀況探查，按一下 [新增]
        1. 輸入新健全狀況探查 hello (例如 hp hana) hello 名稱
        1. 選取 TCP 當做通訊協定、連接埠 625**03**，保留間隔 5 和狀況不良閾值 2
        1. Click OK
    1. 建立負載平衡規則
        1. 開啟 hello 負載平衡器，選取負載平衡規則並按一下 [新增]
        1. 輸入 hello hello 新的負載平衡器規則名稱 (例如 hana-lb-3**03**15)
        1. 選取 hello 前端 IP 位址、 後端集區和健全狀況探查您稍早建立 （例如前端 hana）
        1. 保留通訊協定 TCP，輸入連接埠 3**03**15
        1. 增加閒置逾時 too30 分鐘數
       1. **請確定 tooenable 浮動 IP**
        1. Click OK
        1. 重複上述步驟，hello 埠 3**03**17

### <a name="deploy-with-template"></a>透過範本進行部署
您可以使用其中一個 hello 快速入門範本 github toodeploy 上所有必要的資源。 hello 範本部署 hello 虛擬機器、 hello 負載平衡器、 可用性設定組等等。請遵循這些步驟 toodeploy hello 範本：

1. 開啟 hello[資料庫範本][ template-multisid-db]或 hello[交集範本][ template-converged] hello Azure 入口網站上 hello 資料庫範本只建立 hello資料庫的負載平衡規則而 hello 交集的範本也會建立 hello 負載平衡規則 ASCS/SCS 和端 (只有 Linux) 執行個體。 如果您計劃 tooinstall SAP NetWeaver 架構系統，而且也想 tooinstall hello ASCS/SCS 執行個體上 hello 相同機器，請使用 hello[交集範本][template-converged]。
1. 輸入下列參數的 hello
    1. SAP 系統識別碼  
       輸入 hello 想 tooinstall 的 SAP 系統的 hello SAP 的系統識別碼。 hello 識別碼將用於做為前置詞已部署的 hello 資源。
    1. 堆疊類型 （僅適用於您使用 hello 交集的範本）  
       選取 hello SAP NetWeaver 堆疊類型
    1. OS 類型  
       選取其中一個 hello Linux 散發套件。 在此範例中，請選取 SLES 12 BYOS
    1. DB 類型  
       選取 HANA
    1. SAP 系統大小  
       將提供的 SAPS hello 新系統的 hello 數量。 如果您不確定需要多少的 SAPS hello 系統，請要求您的 SAP 技術合作夥伴或系統整合者
    1. 系統可用性  
       選取 HA
    1. 管理員使用者名稱和管理員密碼  
       會建立新的使用者，可以使用的 toolog toohello 機器上。
    1. 新的或現有的子網路  
       決定應該建立新的虛擬網路和子網路，或是應該使用現有子網路。 如果您已經連接的 tooyour 在內部部署網路的虛擬網路，選取現有的。
    1. 子網路識別碼  
    hello 識別碼 hello 子網路 toowhich hello 虛擬機器應該連接到。 選取您的 VPN 或 Express Route 虛擬網路 tooconnect hello 虛擬機器 tooyour 在內部部署網路的 hello 子網路。 hello 識別碼通常看起來像 /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>設定 Linux HA

是 [A]-適用 tooall 節點、 [1]-1 或 2 僅適用於 toonode-僅適用於 toonode 2 有前置 hello 下列項目。

1. [A] SLES 適用於 SAP BYOS 只-註冊 SLES toobe 無法 toouse hello 儲存機制
1. [A] 僅限 SLES for SAP BYOS - 新增公用雲端模組
1. [A] 更新 SLES
    ```bash
    sudo zypper update

    ```

1. [1] 啟用 SSH 存取
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] 啟用 SSH 存取
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] 啟用 SSH 存取
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] 安裝 HA 擴充功能
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] 設定磁碟配置
    1. LVM  
    我們通常會建議 toouse LVM 磁碟區的儲存資料和記錄檔。 以下的 hello 範例假設 hello 虛擬機器有四個資料磁碟連接是應該使用的 toocreate 兩個磁碟區。
        * 建立您想 toouse 的所有磁碟的實體磁碟區。
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * 建立 hello 資料檔案的磁碟區群組，一個 hello 記錄檔的磁碟區群組，一個用於 hello 共用目錄的 SAP HANA
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * 建立 hello 邏輯磁碟區
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * 建立 hello 掛接目錄，並複製 hello 的所有邏輯磁碟區的 UUID
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * 建立 hello fstab 項目三個邏輯磁碟區
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    插入此線條太/等/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * 掛接 hello 新磁碟區
    <pre><code>
    sudo mount -a
    </code></pre>
    1. 一般磁碟  
       針對小型或示範系統，您可以將 HANA 資料和記錄檔放在一個磁碟上。 hello 下列命令 /dev/sdc 上建立資料分割並格式化與 xfs。
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>請記下 /dev/sdc1 hello 識別碼
    sudo /sbin/blkid  sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] 設定適用於所有主機的主機名稱解析  
    您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。 這個範例會示範如何 toouse hello /etc/hosts 檔案。
   取代 hello IP 位址和下列命令的 hello hello 主機名稱
    ```bash
    sudo vi /etc/hosts
    ```
    插入 hello 下列各行太/等/主機。 變更您的環境的 hello IP 位址和主機名稱 toomatch    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] 安裝叢集
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] 新增節點 toocluster
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] 變更 hacluster 密碼 toohello 相同的密碼
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] 設定 corosync toouse 其他傳輸，並加入節點清單。 否則叢集將無法運作。
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    新增下列內容的粗體 toohello 檔 hello。
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    然後重新啟動 hello corosync 服務

    ```bash
    sudo service corosync restart
    
    ```

1. [A] 安裝 HANA HA 套件  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>安裝 SAP HANA

請依照第 4 章 hello [SAP HANA SR-IOV 的效能最佳化的案例指南][ suse-hana-ha-guide] tooinstall SAP HANA 系統複寫。

1. [A] 從 hello HANA DVD 執行 hdblcm
    * 選擇安裝 -> 1
    * 選取要安裝的其他元件 -> 1
    * 輸入安裝路徑 [/hana/shared]：-> ENTER
    * 輸入本機主機名稱 [..]：-> ENTER
    * 您想 tooadd 其他主機 toohello 系統嗎？ (y/n) [n]：-> ENTER
    * 輸入 SAP HANA 系統識別碼︰<SID of HANA e.g. HDB>
    * 輸入執行個體號碼 [00]：   
  HANA 執行個體號碼。 如果您使用 hello Azure 範本，或遵循上述的 hello 範例，使用 03
    * 選取資料庫模式 / 輸入索引 [1]：-> ENTER
    * 選取系統使用量 / 輸入索引 [4]：  
  選取 hello 系統使用量
    * 輸入資料磁碟區的位置 [/hana/data/HDB]：-> ENTER
    * 輸入記錄檔磁碟區的位置 [/hana/log/HDB]：-> ENTER
    * 是否限制記憶體配置上限？ [n]：-> ENTER
    * 輸入主機的憑證主機名稱 '...'[…]:]-> [ENTER
    * 輸入 SAP 主機代理程式使用者 (sapadm) 密碼：
    * 確認 SAP 主機代理程式使用者 (sapadm) 密碼：
    * 輸入系統管理員 (hdbadm) 密碼：
    * 確認系統管理員 (hdbadm) 密碼：
    * 輸入系統管理員主目錄 [/usr/sap/HDB/home]：-> ENTER
    * 輸入系統管理員登入殼層 [/bin/sh]：-> ENTER
    * 輸入系統管理員使用者識別碼 [1001]：-> ENTER
    * 輸入使用者群組 (sapsys) 的識別碼 [79]：-> ENTER
    * 輸入資料庫使用者 (SYSTEM) 密碼：
    * 確認資料庫使用者 (SYSTEM) 密碼：
    * 是否在電腦重新開機後重新啟動系統？ [n]：-> ENTER
    * 您想 toocontinue 嗎？ (y/n)：  
  驗證摘要的 hello 並輸入 y toocontinue
1. [A] 升級 SAP 主機代理程式  
  Hello 從下載最新 SAP Host Agent 封存 hello [SAP Softwarecenter] [ sap-swcenter]並執行 hello 下列命令 tooupgrade hello 代理程式。 取代 hello 路徑 toohello 封存 toopoint toohello 您下載的檔案。
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] 建立 HANA 複寫 (以 root 身分執行)  
    執行下列命令的 hello。 請確定 tooreplace 粗體字串 （HANA 系統識別碼 HDB 和執行個體編號 03），與 SAP HANA 安裝 hello 值。
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] 建立金鑰儲存區項目 (以 root 身分執行)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] 備份資料庫 (以 root 身分執行)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] 切換 toohello sapsid 使用者 (例如 hdbadm)，並建立 hello 主要站台。
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] 切換 toohello sapsid 使用者 (例如 hdbadm)，並建立 hello 次要站台。
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>設定叢集架構

變更 hello 預設設定

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>現在我們可以載入 hello 檔案 toohello 叢集
sudo crm configure load update crm-defaults.txt
</pre>

### <a name="create-stonith-device"></a>建立 STONITH 裝置

hello STONITH 裝置會使用針對 Microsoft Azure 服務主體 tooauthorize。 請遵循這些步驟 toocreate 服務主體。

1. 跳過<https://portal.azure.com>
1. 開啟 hello Azure Active Directory 刀鋒視窗  
   請移 tooProperties 並寫下 hello 目錄識別碼。這是 hello**租用戶識別碼**。
1. 按一下 [應用程式註冊]
1. 按一下 [新增]
1. 輸入名稱、選取應用程式類型 [Web 應用程式/API]、輸入登入 URL (例如 http://localhost )，然後按一下 [建立]
1. hello 登入 URL 不是，它可以是任何有效的 URL
1. 選取 hello 新的應用程式，然後按一下 hello 設定 索引標籤中的 索引鍵
1. 輸入新金鑰的說明、選取 [永不過期]，然後按一下 [儲存]
1. 記下 hello 值。 它會當做 hello 使用**密碼**hello 服務主體
1. 請記下 hello 應用程式識別碼。它作為 hello 使用者名稱 (**登入識別碼**hello 步驟中) 的 hello 服務主體

hello 服務主體沒有權限 tooaccess 您的 Azure 資源預設。 您需要 toogive hello 服務主體的權限 toostart 和停止 （取消配置） hello 叢集的所有虛擬機器。

1. 移 toohttps://portal.azure.com
1. 開啟 hello 所有資源刀鋒視窗
1. 選取 hello 虛擬機器
1. 選取 [存取控制 (IAM)]
1. 按一下 [新增]
1. 選取 hello 角色擁有者
1. 輸入 hello hello 先前建立的應用程式名稱
1. Click OK

編輯 hello hello 虛擬機器的權限之後，您可以設定 hello STONITH 裝置 hello 叢集中。

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>現在我們可以載入 hello 檔案 toohello 叢集
sudo crm configure load update crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>建立 SAP HANA 資源

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>現在我們可以載入 hello 檔案 toohello 叢集
sudo crm configure load update crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>現在我們可以載入 hello 檔案 toohello 叢集
sudo crm configure load update crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>測試叢集設定
hello 下列章節說明如何測試您的設定。 每一個測試會假設是根而且 hello SAP HANA 主要在 hello 虛擬機器 saphanavm1 上執行。

#### <a name="fencing-test"></a>隔離測試

您可以藉由停用 hello 網路介面上節點 saphanavm1 測試 hello hello 圍欄代理程式的安裝程式。

<pre><code>
sudo ifdown eth0
</code></pre>

hello 虛擬機器應該立即取得重新啟動或停止根據您的叢集設定。
如果您設定 hello stonith 動作 toooff，hello 虛擬機器將會停止而且 hello 資源移轉的 toohello 虛擬機器中執行。

如果您設定 AUTOMATED_REGISTER 一旦再次啟動 hello 虛擬機器，hello SAP HANA 資源將會失敗為次要 toostart ="false"。 在此情況下，您需要藉由執行下列命令的 hello 做為次要 tooconfigure hello HANA 執行個體：

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>測試手動容錯移轉

您可以測試的手動容錯移轉節點 saphanavm1 上停止 hello pacemaker 服務。
<pre><code>
service pacemaker stop
</code></pre>

Hello 容錯移轉之後，您可以重新啟動 hello 服務。 hello saphanavm1 上的 SAP HANA 資源將會失敗 toostart 為次要資料庫設定 AUTOMATED_REGISTER ="false"。 在此情況下，您需要藉由執行下列命令的 hello 做為次要 tooconfigure hello HANA 執行個體：

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>測試移轉

您可以藉由執行下列命令的 hello 移轉 hello SAP HANA 主要節點
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

這應該移轉 hello SAP HANA 主要節點和包含 hello 虛擬 IP 位址 toosaphanavm2 hello 群組。
hello saphanavm1 上的 SAP HANA 資源將會失敗 toostart 為次要資料庫設定 AUTOMATED_REGISTER ="false"。 在此情況下，您需要藉由執行下列命令的 hello 做為次要 tooconfigure hello HANA 執行個體：

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

hello 移轉會需要一次刪除 toobe 位置條件約束。

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

您也需要 toocleanup hello hello 次要節點資源狀態

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>後續步驟
* [適用於 SAP 的 Azure 虛擬機器規劃和實作][planning-guide]
* [適用於 SAP 的 Azure 虛擬機器部署][deployment-guide]
* [適用於 SAP 的 Azure 虛擬機器 DBMS 部署][dbms-guide]
* toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。 
