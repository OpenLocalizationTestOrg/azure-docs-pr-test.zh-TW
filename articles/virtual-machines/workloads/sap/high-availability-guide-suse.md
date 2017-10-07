---
title: "aaaAzure 虛擬機器的高可用性的 SAP NetWeaver SUSE Linux Enterprise Server 上的 SAP 應用程式 |Microsoft 文件"
description: "SAP NetWeaver 在適用於 SAP 應用程式之 SUSE Linux Enterprise Server 上的高可用性指南"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a>SAP NetWeaver 在適用於 SAP 應用程式之 SUSE Linux Enterprise Server 上的 Azure VM 高可用性

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
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

本文說明 toodeploy hello 虛擬機器，設定 hello 虛擬機器、 安裝 hello 叢集架構和安裝高可用性的 SAP NetWeaver 7.50 系統的方式。
在 hello 範例組態中，安裝命令等。會使用 ASCS 執行個體號碼 00、ERS 執行個體號碼 02 和 SAP 系統識別碼 NWS。 hello 名稱 hello 中的資源 （例如虛擬機器、 虛擬網路） hello 範例假設您已使用 hello[交集範本][ template-converged]與 SAP 系統識別碼 NWS toocreate hello 資源。

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
* [SAP HANA SR 效能最佳化案例 (英文)][suse-hana-ha-guide]  
  hello 指南包含所有必要的資訊 tooset SAP HANA 系統複寫在內部。 請使用此指南做為基礎。
* [高度可用 NFS 的存放裝置與 DRBD Pacemaker] [ suse-drbd-guide] hello 指南包含所有必要的資訊 tooset 高可用性的 NFS 伺服器設定。 請使用此指南做為基礎。


## <a name="overview"></a>概觀

tooachieve 高可用性，SAP NetWeaver 需要 NFS 伺服器。 hello NFS 伺服器不同叢集中設定，並可供多個 SAP 系統。

![SAP NetWeaver 高可用性概觀](./media/high-availability-guide-suse/img_001.png)

hello NFS 伺服器，SAP NetWeaver ASCS、 SAP NetWeaver SCS、 SAP NetWeaver 端及 hello SAP HANA 資料庫使用虛擬的主機名稱和虛擬 IP 位址。 在 Azure 上、 負載平衡器需要的 toouse 虛擬 IP 位址。 hello 下列清單顯示 hello hello 負載平衡器組態。

### <a name="nfs-server"></a>NFS 伺服器
* 前端組態
  * IP 位址 10.0.0.4
* 後端組態
  * 連接 tooprimary 應該 hello NFS 叢集一部分的所有虛擬機器的網路介面
* 探查連接埠
  * 連接埠 61000
* 負載平衡規則
  * 2049 TCP 
  * 2049 UDP

### <a name="ascs"></a>(A)SCS
* 前端組態
  * IP 位址 10.0.0.10
* 後端組態
  * 應該是 hello (A) SCS/端叢集一部分的所有虛擬機器的連線的 tooprimary 網路介面
* 探查連接埠
  * 連接埠 620**&lt;nr&gt;**
* 負載平衡規則
  * 32**&lt;nr&gt;** TCP
  * 36**&lt;nr&gt;** TCP
  * 39**&lt;nr&gt;** TCP
  * 81**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="ers"></a>ERS
* 前端組態
  * IP 位址 10.0.0.11
* 後端組態
  * 應該是 hello (A) SCS/端叢集一部分的所有虛擬機器的連線的 tooprimary 網路介面
* 探查連接埠
  * 連接埠 621**&lt;nr&gt;**
* 負載平衡規則
  * 33**&lt;nr&gt;** TCP
  * 5**&lt;nr&gt;**13 TCP
  * 5**&lt;nr&gt;**14 TCP
  * 5**&lt;nr&gt;**16 TCP

### <a name="sap-hana"></a>SAP HANA
* 前端組態
  * IP 位址 10.0.0.12
* 後端組態
  * 連接 tooprimary 應該 hello HANA 叢集一部分的所有虛擬機器的網路介面
* 探查連接埠
  * 連接埠 625**&lt;nr&gt;**
* 負載平衡規則
  * 3**&lt;nr&gt;**15 TCP
  * 3**&lt;nr&gt;**17 TCP

## <a name="setting-up-a-highly-available-nfs-server"></a>設定高可用性的 NFS 伺服器

### <a name="deploying-linux"></a>部署 Linux

hello Azure Marketplace 包含您可以使用 toodeploy 新的虛擬機器的 SAP 應用程式 12 for SUSE Linux Enterprise Server 映像。
您可以使用其中一個 hello 快速入門範本 github toodeploy 上所有必要的資源。 hello 範本部署 hello 虛擬機器、 hello 負載平衡器、 可用性設定組等等。請遵循這些步驟 toodeploy hello 範本：

1. 開啟 hello [SAP 檔案伺服器範本][ template-file-server] hello Azure 入口網站中   
1. 輸入下列參數的 hello
   1. 資源前置詞  
      輸入您想要 toouse hello 前置詞。 hello 值用於部署的 hello 資源做為前置詞。
   2. OS 類型  
      選取其中一個 hello Linux 散發套件。 在此範例中，請選取 SLES 12
   3. 管理員使用者名稱和管理員密碼  
      會建立新的使用者，可以使用的 toolog toohello 機器上。
   4. 子網路識別碼  
      hello 識別碼 hello 子網路 toowhich hello 虛擬機器應該連接到。 如果您想要 toocreate 新的虛擬網路，或選取 hello 子網路的 VPN 或 Express Route 虛擬網路 tooconnect hello 虛擬機器 tooyour 在內部部署網路將會保留空白。 hello 識別碼通常看起來像 /subscriptions/**&lt;訂用帳戶 id&gt;**/resourceGroups/**&lt;資源群組名稱&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;虛擬網路名稱&gt;**/subnets/**&lt;子網路名稱&gt;**

### <a name="installation"></a>安裝

hello 下列項目會加上  **[A]** -適用 tooall 節點**[1]** -適用 toonode 1 或**[2]** -適用 toonode 2。

1. **[A]** 更新 SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** 啟用 SSH 存取

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** 啟用 SSH 存取

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** 啟用 SSH 存取

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** 安裝 HA 擴充功能
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** 設定主機名稱解析   

   您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。 這個範例會示範如何 toouse hello /etc/hosts 檔案。
   取代 hello IP 位址和下列命令的 hello hello 主機名稱

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   插入 hello 下列各行太/等/主機。 變更您的環境的 hello IP 位址和主機名稱 toomatch   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. **[1]** 安裝叢集
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**新增節點 toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**變更 hacluster 密碼 toohello 相同的密碼

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**設定 corosync toouse 其他傳輸，並加入節點清單。 否則叢集將無法運作。
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   然後重新啟動 hello corosync 服務

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** 安裝 drbd 元件

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**建立 hello drbd 裝置的資料分割

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** 建立 LVM 組態

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. **[A]**建立 hello NFS drbd 裝置

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   插入新 drbd 裝置 hello 和結束的 hello 組態

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   建立 hello drbd 裝置並啟動

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. **[1]** 略過首次同步處理

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. **[1]**組 hello 主要節點

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. **[1]**等候同步處理新 drbd 裝置 hello

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]** Drbd 裝置 hello 上建立檔案系統

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a>設定叢集架構

1. **[1]**變更 hello 預設設定

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**新增 hello NFS drbd 裝置 toohello 叢集設定

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**建立 hello NFS 伺服器

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**建立 hello NFS 檔案系統資源

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**建立 hello NFS 匯出

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. **[1]**建立虛擬 IP 資源和 hello 內部負載平衡器的健全狀況探查

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**建立 hello STONITH 裝置

編輯 hello hello 虛擬機器的權限之後，您可以設定 hello STONITH 裝置 hello 叢集中。

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]** STONITH 裝置 hello 使用

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a>設定 (A)SCS

### <a name="deploying-linux"></a>部署 Linux

hello Azure Marketplace 包含您可以使用 toodeploy 新的虛擬機器的 SAP 應用程式 12 for SUSE Linux Enterprise Server 映像。 hello marketplace 映像包含 SAP NetWeaver hello 資源代理的程式。

您可以使用其中一個 hello 快速入門範本 github toodeploy 上所有必要的資源。 hello 範本部署 hello 虛擬機器、 hello 負載平衡器、 可用性設定組等等。請遵循這些步驟 toodeploy hello 範本：

1. 開啟 hello [ASCS/SCS 多重 SID 範本][ template-multisid-xscs]或 hello[交集範本][ template-converged]上 hello Azure 入口網站的 hello ASCS/SCS 僅限範本建立 hello 負載平衡規則的 SAP NetWeaver ASCS/SCS hello 和端 (只有 Linux) 執行個體，而 hello 交集的範本也會建立資料庫 （例如 Microsoft SQL Server 或 SAP HANA） hello 負載平衡規則。 如果您計劃 tooinstall SAP NetWeaver 架構系統，而且也想 tooinstall hello 資料庫在 hello 相同的電腦，請使用 hello[交集範本][template-converged]。
1. 輸入下列參數的 hello
   1. 資源前置詞 (僅限 ASCS/SCS 多重 SID 範本)  
      輸入您想要 toouse hello 前置詞。 hello 值用於部署的 hello 資源做為前置詞。
   3. Sap 系統識別碼 (僅限交集範本)  
      輸入 hello 想 tooinstall 的 SAP 系統的 hello SAP 的系統識別碼。 hello 識別碼用於部署的 hello 資源做為前置詞。
   4. 堆疊類型  
      選取 hello SAP NetWeaver 堆疊類型
   5. OS 類型  
      選取其中一個 hello Linux 散發套件。 在此範例中，請選取 SLES 12 BYOS
   6. DB 類型  
      選取 HANA
   7. SAP 系統大小  
      提供的 SAPS hello 新系統的 hello 數量。 如果您不確定需要多少的 SAPS hello 系統，請要求您的 SAP 技術合作夥伴或系統整合者
   8. 系統可用性  
      選取 HA
   9. 管理員使用者名稱和管理員密碼  
      會建立新的使用者，可以使用的 toolog toohello 機器上。
   10. 子網路識別碼  
   hello 識別碼 hello 子網路 toowhich hello 虛擬機器應該連接到。  如果您想 toocreate 新的虛擬網路，或選取 hello 相同子網路，您在使用或建立為 hello NFS 伺服器部署的一部分，則會保留空白。 hello 識別碼通常看起來像 /subscriptions/**&lt;訂用帳戶 id&gt;**/resourceGroups/**&lt;資源群組名稱&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;虛擬網路名稱&gt;**/subnets/**&lt;子網路名稱&gt;**

### <a name="installation"></a>安裝

hello 下列項目會加上  **[A]** -適用 tooall 節點**[1]** -適用 toonode 1 或**[2]** -適用 toonode 2。

1. **[A]** 更新 SLES

   <pre><code>
   sudo zypper update
   </code></pre>

1. **[1]** 啟用 SSH 存取

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. **[2]** 啟用 SSH 存取

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. **[1]** 啟用 SSH 存取

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. **[A]** 安裝 HA 擴充功能
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. **[A]** 更新 SAP 資源代理程式  
   
   修補程式 hello 資源代理程式套件是必要的 toouse hello 新的設定，這篇文章中所述。 您可以檢查，如果已經以 hello 下列命令安裝 hello 修補程式

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   hello 輸出應類似於

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   如果 hello grep 命令找不到 hello IS_ERS 參數，您需要在所列的 tooinstall hello 修補程式[hello SUSE 下載頁面](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. **[A]** 設定主機名稱解析   

   您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。 這個範例會示範如何 toouse hello /etc/hosts 檔案。
   取代 hello IP 位址和下列命令的 hello hello 主機名稱

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   插入 hello 下列各行太/等/主機。 變更您的環境的 hello IP 位址和主機名稱 toomatch   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. **[1]** 安裝叢集
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. **[2]**新增節點 toocluster
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. **[A]**變更 hacluster 密碼 toohello 相同的密碼

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. **[A]**設定 corosync toouse 其他傳輸，並加入節點清單。 否則叢集將無法運作。
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

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
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   然後重新啟動 hello corosync 服務

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. **[A]** 安裝 drbd 元件

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. **[A]**建立 hello drbd 裝置的資料分割

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. **[A]** 建立 LVM 組態

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. **[A]**建立 hello SCS drbd 裝置

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   插入新 drbd 裝置 hello 和結束的 hello 組態

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   建立 hello drbd 裝置並啟動

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. **[A]**建立 hello 端 drbd 裝置

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   插入新 drbd 裝置 hello 和結束的 hello 組態

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   建立 hello drbd 裝置並啟動

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. **[1]** 略過首次同步處理

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. **[1]**組 hello 主要節點

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. **[1]**等候同步處理新 drbd 裝置 hello

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. **[1]** Drbd 裝置 hello 上建立檔案系統

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a>設定叢集架構

**[1]**變更 hello 預設設定

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a>準備進行 SAP NetWeaver 安裝

1. **[A]**建立 hello 共用目錄

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. **[A]** 設定 autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   使用下列命令建立檔案

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   重新啟動 autofs toomount hello 新的共用

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. **[A]** 設定分頁檔
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   重新啟動 hello 代理程式 tooactivate hello 變更

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a>安裝 SAP NetWeaver ASCS/ERS

1. **[1]**建立虛擬 IP 資源和 hello 內部負載平衡器的健全狀況探查

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。 它並不重要上執行哪些節點 hello 資源。

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. **[1]** 安裝 SAP NetWeaver ASCS  

   為根 hello 使用虛擬的主機名稱，例如對應 hello 負載平衡器前端組態 hello ASCS toohello IP 位址的第一個節點上安裝 SAP NetWeaver ASCS <b>nws ascs</b>， <b>10.0.0.10</b>和 hello 執行個體號碼，例如用於 hello 負載平衡器的 hello 探查<b>00</b>。

   您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. **[1]**建立虛擬 IP 資源和 hello 內部負載平衡器的健全狀況探查

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。 它並不重要上執行哪些節點 hello 資源。

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. **[2]** 安裝 SAP NetWeaver ERS  

   為根 hello 使用 toohello 的 hello 負載平衡器前端組態 hello 端的 IP 位址，例如對應虛擬主機名稱的第二個節點上安裝 SAP NetWeaver 端<b>nws 端</b>， <b>10.0.0.11</b>hello，例如用於 hello 探查的 hello 負載平衡器的執行個體號碼和<b>02</b>。

   您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > 請使用 SWPM SP 20 PL 05 或更高版本。 較低版本未正確設定 hello 權限和 hello 安裝將會失敗。
   > 

1. **[1]**調整 hello ASCS/SCS 和端執行個體的設定檔
 
   * ASCS/SCS 設定檔

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * ERS 設定檔

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. **[A]** 設定保持運作

   透過軟體負載平衡器路由傳送 hello hello ASCS/SCS hello SAP NetWeaver 應用程式伺服器之間的通訊。 hello 負載平衡器會中斷非作用中連線之後可設定的逾時。 tooprevent 這需要 tooset hello SAP NetWeaver ASCS/SCS 設定檔中的參數，並變更 hello Linux 系統設定。 如需詳細資訊，請閱讀 [SAP Note 1410736][1410736]。
   
   hello ASCS/SCS 設定檔參數時/encni/set_so_keepalive 已經 hello 最後一個步驟中加入。

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. **[A]** Hello 安裝後設定 hello SAP 使用者
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. **[1]**新增 hello ASCS 和 SAP 端服務 toohello sapservice 檔案

   加入 hello ASCS 服務項目 toohello 第二個節點和複製 hello 端服務項目 toohello 第一個節點。

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. **[1]**建立 hello SAP 叢集資源

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。 它並不重要上執行哪些節點 hello 資源。

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

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

#### <a name="1-create-hello-stonith-devices"></a>**[1]**建立 hello STONITH 裝置

編輯 hello hello 虛擬機器的權限之後，您可以設定 hello STONITH 裝置 hello 叢集中。

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a>**[1]** STONITH 裝置 hello 使用

啟用 hello STONITH 裝置

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a>安裝資料庫

此範例會安裝並設定 SAP HANA 系統複寫。 SAP HANA hello 相同叢集 hello SAP NetWeaver ASCS/SCS 以及端將會執行。 您也可以將 SAP HANA 安裝在專用叢集上。 如需詳細資訊，請參閱 [Azure 虛擬機器 (VM) 上的 SAP HANA 高可用性][sap-hana-ha]。

### <a name="prepare-for-sap-hana-installation"></a>準備進行 SAP HANA 安裝

我們通常建議針對儲存資料和記錄檔的磁碟區使用 LVM。 為了測試用途，您也可以選擇 toostore hello 資料和記錄檔直接在一般的磁碟上。

1. **[A]** LVM  
   以下的 hello 範例假設 hello 虛擬機器有四個資料磁碟連接是應該使用的 toocreate 兩個磁碟區。
   
   建立您想 toouse 的所有磁碟的實體磁碟區。
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   建立 hello 資料檔案的磁碟區群組，一個 hello 記錄檔的磁碟區群組，一個用於 hello 共用目錄的 SAP HANA
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   建立 hello 邏輯磁碟區
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   建立 hello 掛接目錄，並複製 hello 的所有邏輯磁碟區的 UUID
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   建立 hello autofs 項目三個邏輯磁碟區
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   插入此列 toosudo vi /etc/auto.direct
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   掛接 hello 新磁碟區
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. **[A]** 一般磁碟  

   針對小型或示範系統，您可以將 HANA 資料和記錄檔放在一個磁碟上。 hello 下列命令 /dev/sdc 上建立資料分割並格式化與 xfs。
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   插入此列 too/etc/auto.direct
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   建立 hello 目標目錄，並將 hello 磁碟掛接。
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a>安裝 SAP HANA

hello 下列步驟為基礎的 hello 第 4 章[SAP HANA SR-IOV 的效能最佳化的案例指南][ suse-hana-ha-guide] tooinstall SAP HANA 系統複寫。 請仔細閱讀，然後再繼續 hello 安裝。

1. **[A]**從 hello HANA DVD 執行 hdblcm
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. **[A]** 升級 SAP 主機代理程式

   Hello 從下載最新 SAP Host Agent 封存 hello [SAP Softwarecenter] [ sap-swcenter]並執行 hello 下列命令 tooupgrade hello 代理程式。 取代 hello 路徑 toohello 封存 toopoint toohello 您下載的檔案。
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. **[1]** 建立 HANA 複寫 (以 root 身分執行)  

   執行下列命令的 hello。 請確定 tooreplace 粗體字串 （HANA 系統識別碼 HDB 和執行個體編號 03），與 SAP HANA 安裝 hello 值。
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. **[A]** 建立金鑰儲存區項目 (以 root 身分執行)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. **[1]** 備份資料庫 (以 root 身分執行)

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. **[1]**切換 toohello HANA sapsid 使用者，並建立 hello 主要站台。

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. **[2]**切換 toohello HANA sapsid 使用者，並建立 hello 次要站台。

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. **[1]** 建立 SAP HANA 叢集資源

   首先，建立 hello 拓撲。
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   接下來，建立 hello HANA 資源
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   請確定 hello 叢集狀態為 [確定]，且已啟動的所有資源。 它並不重要上執行哪些節點 hello 資源。

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. **[1]**安裝 hello SAP NetWeaver 資料庫執行個體

   安裝 hello SAP NetWeaver 資料庫執行個體做為使用虛擬的主機名稱，例如對應 hello 負載平衡器前端組態 hello 資料庫 toohello IP 位址的根目錄<b>nws db</b>和<b>10.0.0.12</b>.

   您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a>SAP NetWeaver 應用程式伺服器安裝

請遵循這些步驟 tooinstall SAP 應用程式伺服器。 hello 以下步驟假設您安裝 hello hello ASCS/SCS 從不同的伺服器上的應用程式伺服器和 HANA 伺服器。 否則某些 hello 執行下列步驟 （例如設定主機名稱解析） 不需要。

1. 設定主機名稱解析    
   您可以使用 DNS 伺服器，或修改 hello /etc/hosts 所有節點上。 這個範例會示範如何 toouse hello /etc/hosts 檔案。
   取代 hello IP 位址和下列命令的 hello hello 主機名稱
   ```bash
   sudo vi /etc/hosts
   ```
   插入 hello 下列各行太/等/主機。 變更您的環境的 hello IP 位址和主機名稱 toomatch    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. 建立 hello sapmnt 目錄

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. 設定 autofs
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   使用下列命令建立新檔案

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   重新啟動 autofs toomount hello 新的共用

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. 設定分頁檔
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   重新啟動 hello 代理程式 tooactivate hello 變更

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. 安裝 SAP NetWeaver 應用程式伺服器

   安裝主要或其他的 SAP NetWeaver 應用程式伺服器。

   您可以使用 hello sapinst 參數 SAPINST_REMOTE_ACCESS_USER tooallow 非根使用者 tooconnect toosapinst。

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. 更新 SAP HANA 安全存放區

   更新 hello SAP HANA 安全儲存 toopoint toohello 虛擬名稱 hello SAP HANA 系統複寫設定。
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a>後續步驟
* [適用於 SAP 的 Azure 虛擬機器規劃和實作][planning-guide]
* [適用於 SAP 的 Azure 虛擬機器部署][deployment-guide]
* [適用於 SAP 的 Azure 虛擬機器 DBMS 部署][dbms-guide]
* toolearn tooestablish 高可用性和 Azure （大型執行個體） 上的 SAP HANA 災害復原計劃的看到[SAP HANA （大型執行個體） 高可用性和災害復原在 Azure 上的](hana-overview-high-availability-disaster-recovery.md)。
* toolearn tooestablish 高可用性和災害復原的 SAP HANA 規劃 Azure Vm 上的看到[SAP HANA 的高可用性 Azure 虛擬機器 (Vm) 上][sap-hana-ha]
