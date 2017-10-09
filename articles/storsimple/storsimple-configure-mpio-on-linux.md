---
title: "aaaConfigure MPIO StorSimple Linux 主機上的 |Microsoft 文件"
description: "執行 CentOS 6.6 StorSimple 連接 tooa Linux 主機上設定 MPIO"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>在執行 CentOS 的 StorSimple 主機上設定 MPIO
本文說明 hello 步驟需要的 tooconfigure 多重路徑 IO (MPIO)，在 Centos 6.6 主機伺服器上。 hello 主機伺服器是高可用性，透過 iSCSI 啟動器連線的 tooyour Microsoft Azure StorSimple 裝置。 它會描述詳細 hello 自動探索多重路徑裝置和 hello 特定的設定，只為 StorSimple 磁碟區。

此程序是 StorSimple 8000 系列裝置的適用 tooall hello 模型。

> [!NOTE]
> 此程序無法用於 StorSimple 虛擬裝置。 如需詳細資訊，請參閱如何 tooconfigure 裝載虛擬裝置的伺服器。
> 
> 

## <a name="about-multipathing"></a>關於多重路徑
hello 多重路徑功能可讓您 tooconfigure 主機伺服器與存放裝置之間的多個 I/O 路徑。 這些 I/O 路徑是可包含不同纜線、開關、網路介面及控制站的實體 SAN 連線。 多重路徑彙總 hello I/O 路徑 tooconfigure 與 hello 彙總路徑的所有相關聯的新裝置。

多重路徑 hello 目的是一體兩面：

* **高可用性**: hello I/O 路徑 （例如，纜線、 參數、 網路介面或控制站） 的任何項目失敗時，它會提供替代路徑。
* **負載平衡**： 根據您的儲存體裝置 hello 組態，它可以改善 hello 效能偵測 hello I/O 路徑上的負載，並以動態方式重新平衡負載。

### <a name="about-multipathing-components"></a>關於多重路徑元件
Linux 中的多重路徑是由核心元件和下列的使用者空間元件所組成。

* **核心**: hello 主要元件是 hello*裝置對應工具*，排列 I/O，並支援容錯移轉路徑與路徑群組。

* **使用者空間**： 這些是*多重路徑工具*可用於管理多重路徑裝置藉由指示 hello 裝置-多重路徑對應程式模組哪些 toodo。 hello 工具包含：
   
   * **Multipath**︰列出及設定多重路徑的裝置。
   * **Multipathd**： 執行多重路徑和監視 hello 路徑的精靈。
   * **Devmap 名稱**: devmaps 提供有意義的裝置名稱 tooudev。
   * **Kpartx**： 對應線性 devmaps toodevice 分割 toomake 多重路徑對應可分割。
   * **Multipath.conf**： 組態檔是使用的 toooverwrite hello 內建組態資料表的多重路徑服務精靈。

### <a name="about-hello-multipathconf-configuration-file"></a>有關 hello multipath.conf 組態檔
hello 設定檔`/etc/multipath.conf`使許多 hello 多重路徑功能使用者可設定。 hello`multipath`命令和 hello 的核心服務精靈`multipathd`使用此檔案中找到的資訊。 只有在 hello 多重路徑裝置 hello 組態期間參考 hello 檔案。 請確定已進行所有變更，然後再執行 hello`multipath`命令。 如果您修改 hello 檔案之後，您會需要 toostop 並啟動 multipathd hello 變更 tootake 效果的一次。

hello multipath.conf 有五個區段：

- **系統層級的預設值** *(defaults)*：您可以覆寫系統層級預設值。
- **黑名單裝置** *（黑名單）*： 您可以指定不受裝置對應工具的裝置 hello 清單。
- **列入封鎖清單例外狀況** *(blacklist_exceptions)*： 您可以識別視為多重路徑裝置，即使 hello 黑名單中所列的特定裝置 toobe。
- **設定特定的儲存體控制器** *（裝置）*： 您可以指定將會套用的 toodevices 廠商和產品資訊的組態設定。
- **裝置特定設定** *(multipaths)*： 您可以使用此區段 toofine 微調 hello 組態設定的個別 Lun。

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>StorSimple 連接的 tooLinux 主機上設定多重路徑
StorSimple 裝置連線 tooa Linux 主機可以設定為高可用性及負載平衡。 例如，如果 hello Linux 主機有兩個介面連接的 toohello SAN 和 hello 裝置有兩個介面連接 toohello SAN 上的這些介面的這類 hello 相同子網路，則會有 4 個路徑可用。 不過，如果 hello 裝置和主機介面上的每個 DATA 介面是不同的 IP 子網路上 （且無法路由傳送），則只有 2 路徑會提供。 您可以設定多重路徑 tooautomatically 探索所有的 hello 可用的路徑、 選擇這些路徑的負載平衡演算法、 套用特定的組態設定，僅限 StorSimple 磁碟區，然後啟用並驗證多重路徑。

hello 下列程序描述如何 tooconfigure 多重路徑有兩個網路介面的 StorSimple 裝置時使用兩個網路介面連接的 tooa 主機。

## <a name="prerequisites"></a>必要條件
本節詳述 hello CentOS 伺服器與您的 StorSimple 裝置的組態先決條件。

### <a name="on-centos-host"></a>在 CentOS 主機上
1. 確定 CentOS 主機已啟用 2 個網路介面。 輸入：
   
    `ifconfig`
   
    hello 下列範例顯示 hello 時輸出兩張網路介面 (`eth0`和`eth1`) 存在於 hello 主機上。
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. 在 CentOS 伺服器上安裝 *iSCSI-initiator-utils* 。 執行下列步驟 tooinstall hello *iSCSI 啟動器-公用程式*。
   
   1. 以 `root` 身分登入到 CentOS 主機。
   2. 安裝 hello *iSCSI 啟動器-公用程式*。 輸入：
      
       `yum install iscsi-initiator-utils`
   3. 之後 hello *iSCSI 啟動器-公用程式*已順利安裝，請啟動 hello iSCSI 服務。 輸入：
      
       `service iscsid start`
      
       上的情況下，`iscsid`可能不會實際啟動並 hello`--force`可能需要的選項
   4. iSCSI 啟動器已啟用在開機時，使用 hello tooensure`chkconfig`命令 tooenable hello 服務。
      
       `chkconfig iscsi on`
   5. tooverify，但是該已正確地安裝程式中，執行 hello 命令：
      
       `chkconfig --list | grep iscsi`
      
       下方顯示一項範例輸出。
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       從 hello 上述範例中，您可以看到 iSCSI 環境，將執行層級 2、 3、 4 和 5 上開機時執行。
3. 安裝 *device-mapper-multipath*。 輸入：
   
    `yum install device-mapper-multipath`
   
    hello 安裝將會啟動。 型別**Y** toocontinue 出現確認提示時。

### <a name="on-storsimple-device"></a>在 StorSimple 裝置上
您的 StorSimple 裝置應該︰

* 至少有兩個介面已啟用 iSCSI。 兩個介面會在您的 StorSimple 裝置上啟用 iSCSI tooverify 執行 hello hello StorSimple 裝置的 Azure 傳統入口網站中所述步驟：
  
  1. 登入您的 StorSimple 裝置 hello 傳統入口網站。
  2. 選取您的 StorSimple Manager 服務，請按一下**裝置**選擇 hello 特定 StorSimple 裝置。 按一下**設定**和確認 hello 網路介面設定。 下面顯示的螢幕擷取畫面包含已啟用 iSCSI 的兩個網路介面。 以下 DATA 2 和 DATA 3 兩個 10 GbE 介面都已啟用 iSCSI。
     
      ![MPIO StorSimple DATA 2 設定](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![MPIO StorSimple DATA 3 設定](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      在 hello**設定**頁面
     
     1. 確定這兩個網路介面都已啟用 iSCSI。 hello**具備 iSCSI 功能**欄位應該設定太**是**。
     2. 請確定 hello 網路介面有 hello 相同的速度，都應該是 1 GbE 或 10 GbE。
     3. 請注意 hello IPv4 位址的 hello iSCSI 啟用的介面，並儲存供稍後使用 hello 主機上。
* 應該從 hello CentOS 伺服器 hello StorSimple 裝置上的 iSCSI 介面。
      tooverify，您必須在主機伺服器上的 tooprovide hello IP 位址，您的 StorSimple iSCSI 的網路介面。 hello 所使用的命令和 hello DATA2 與對應的輸出 (10.126.162.25) 和 DATA3 (10.126.162.26) 如下所示：
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>硬體組態
我們建議您連接 hello 兩個 iSCSI 網路介面上不同的路徑，以獲得備援。 hello 圖顯示 hello 建議的硬體組態的高可用性和負載平衡 CentOS 伺服器和 StorSimple 裝置的多重路徑。

![StorSimple tooLinux 主機的 MPIO 硬體設定](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Hello 前圖所示：

* StorSimple 裝置處於具有兩個控制器的主動-被動組態中。
* 兩個 SAN 交換器會連接的 tooyour 裝置控制器。
* 兩個 iSCSI 啟動器會在 StorSimple 裝置上啟用。
* CentOS 主機已啟用 2 個網路介面。

如果 hello 主應用程式和資料的介面為可路由傳送，上述組態的 hello 會產生您裝置和 hello 主機之間的 4 個不同的路徑。

> [!IMPORTANT]
> * 建議您不要對多重路徑功能混合使用 1 GbE 與 10 GbE 網路介面。 使用兩個網路介面，這兩個 hello 介面應該 hello 相同型別。
> * 在您的 StorSimple 裝置上，DATA0、DATA1、DATA4 和 DATA5 為 1 GbE 介面，而 DATA2 和 DATA3 則為 10 GbE 網路介面。
> 
> 

## <a name="configuration-steps"></a>組態步驟
多重路徑的 hello 組態步驟將包含設定自動探索，指定 hello 負載平衡演算法 toouse，啟用多重路徑及最後驗證 hello 組態 hello 可用的路徑。 每個步驟是在 hello 下列各節中詳細討論。

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>步驟 1：為自動探索設定多重路徑
hello 多重路徑支援的裝置可以自動探索並設定。

1. 初始化 `/etc/multipath.conf` 檔案。 輸入：
   
     `mpathconf --enable`
   
    hello 上述命令會建立`sample/etc/multipath.conf`檔案。
2. 啟動多重路徑服務。 輸入：
   
    `service multipathd start`
   
    您會看到下列輸出的 hello:
   
    `Starting multipathd daemon:`
3. 啟用多重路徑的自動探索。 輸入：
   
    `mpathconf --find_multipaths y`
   
    這將會修改預設值區段 hello 您`multipath.conf`如下所示：
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>步驟 2：為 StorSimple 磁碟區設定多重路徑
根據預設，所有的裝置會黑色 hello multipath.conf 檔案中所列，並將被略過。 您必須從 StorSimple 裝置的磁碟區 toocreate 黑名單例外狀況 tooallow 多重路徑。

1. 編輯 hello`/etc/mulitpath.conf`檔案。 輸入：
   
    `vi /etc/multipath.conf`
2. Hello multipath.conf 檔案中，找出 hello blacklist_exceptions 區段。 您的 StorSimple 裝置需要 toobe 列為黑名單例外，這一節。 您可以取消註解相關程式碼行中此檔案 toomodify 它 （使用僅限 hello 特定模型的 hello 您使用的裝置） 如下所示：
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>步驟 3：設定循環配置資源多重路徑
此負載平衡演算法會使用所有 hello 可用 multipaths toohello 主動控制站以平衡且循環配置資源的方式。

1. 編輯 hello`/etc/multipath.conf`檔案。 輸入：
   
    `vi /etc/multipath.conf`
2. 在 hello`defaults`區段，集合 hello`path_grouping_policy`太`multibus`。 hello`path_grouping_policy`指定 hello 預設路徑群組原則 tooapply toounspecified multipaths。 hello 預設值區段看起來如下所示。
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> hello 的最常見的值`path_grouping_policy`包括：
> 
> * failover = 每一個優先順序群組 1 個路徑
> * multibus = 1 個優先順序群組中的所有有效路徑
> 
> 

### <a name="step-4-enable-multipathing"></a>步驟 4：啟用多重路徑
1. 重新啟動 hello`multipathd`服務精靈。 輸入：
   
    `service multipathd restart`
2. hello 輸出將會如下所示：
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>步驟 5：驗證多重路徑
1. 先確定的 iSCSI 連線建立 hello StorSimple 裝置，如下所示：
   
   a. 探索您的 StorSimple 裝置。 輸入：
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    當 DATA0 IP 位址是 10.126.162.25 和輸出的 iSCSI 流量的 hello StorSimple 裝置上開啟連接埠 3260 hello 輸出如下所示：
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    複製 hello 您 StorSimple 裝置的 IQN `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`，從上述輸出中的 hello。

   b. 使用目標 IQN toohello 裝置連線。 hello StorSimple 裝置在 hello iSCSI 目標。 輸入：

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    hello 下列範例顯示輸出與目標 IQN 的`iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`。 hello 輸出會指出您已成功在裝置上連線 toohello 兩個已啟用 iSCSI 的網路介面。

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    如果您看到只有一部主機的介面和以下兩個路徑，則您需要 tooenable 這兩個主機上的 hello 介面供 iSCSI。 您可以依照 hello[詳細 Linux 文件中的指示](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html)。

2. 磁碟區是公開的 toohello CentOS 伺服器 hello 的 StorSimple 裝置。 如需詳細資訊，請參閱[步驟 6： 建立磁碟區](storsimple-deployment-walkthrough.md#step-6-create-a-volume)透過 hello StorSimple 裝置上的 Azure 傳統入口網站。

3. 請確認 hello 可用的路徑。 輸入：

      ```
      multipath –l
      ```

      hello 下列範例會顯示兩個網路介面的 hello 輸出在 StorSimple 裝置連線的 tooa 單一主機網路介面上使用兩個可用的路徑。

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>多重路徑疑難排解
如果您在多重路徑設定期間遇到任何問題，請參閱本節所提供的一些實用秘訣。

問： 我看不到中的 hello 變更`multipath.conf`生效的檔案。

A. 如果您進行了任何變更 toohello`multipath.conf`檔案中，您將需要 toorestart hello 多重路徑服務。 輸入下列命令的 hello:

    service multipathd restart

問： 我已啟用 hello StorSimple 裝置上的兩個網路介面和 hello 主機上的兩個網路介面。 當我列出 hello 可用的路徑時，請看只有兩個路徑。 我所期望 toosee 四個可用的路徑。

A. 確定 hello 兩個路徑都在 hello 上相同的子網路和路由傳送。 如果 hello 網路介面位於不同的 Vlan，且無法路由傳送，您會看到只有兩個路徑。 其中一種方式 tooverify 這是 toomake 確定可連線從 hello StorSimple 裝置上的網路介面的這兩個 hello 主機介面。 您必須太[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)為這項驗證僅可透過支援工作階段。

問： 當我列出可用的路徑時，我看不到任何輸出。

A. 一般而言，看不到任何多重路徑的路徑建議問題與 hello 多重路徑精靈，並最有可能是任何在此處的問題在於 hello`multipath.conf`檔案。

也很值得，就可以看到某些磁碟連接 toohello 目標之後為無回應 hello 多重路徑清單也可能表示您不需要任何磁碟。

* 使用下列命令 toorescan hello SCSI 匯流排的 hello:
  
    `$ rescan-scsi-bus.sh ` (屬於 sg3_utils 封包)
* 輸入下列命令的 hello:
  
    `$ dmesg | grep sd*`
     
     或
  
    `$ fdisk –l`
  
    這些將傳回最近新增磁碟的詳細資料。
* toodetermine 是否 StorSimple 磁碟時，使用下列命令的 hello:
  
    `cat /sys/block/<DISK>/device/model`
  
    這會傳回一個字串，判斷它是否為 StorSimple 磁碟。

有一個比較不可能的可能原因也可能是 iscsid pid 過時。 使用 hello iSCSI 工作階段中的下列關閉的命令 toolog hello:

    iscsiadm -m node --logout -p <Target_IP>

重複此命令在 hello iSCSI 目標，也就是您的 StorSimple 裝置上的所有連接的 hello 網路介面。 一旦您已登出所有 hello iSCSI 工作階段，請使用 hello iSCSI 目標 IQN tooreestablish hello iSCSI 工作階段。 輸入下列命令的 hello:

    iscsiadm -m node --login -T <TARGET_IQN>


問： 我不確定我的裝置是否已列入允許清單。

A. tooverify 您的裝置是否在允許清單中，使用下列疑難排解互動式命令 hello:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


如需詳細資訊，請移至太[使用多重路徑的互動式命令進行疑難排解](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html)。

## <a name="list-of-useful-commands"></a>有用的命令清單
| 在系統提示您進行確認時，輸入  | 命令 | 說明 |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |啟動 iSCSI 服務 |
| &nbsp; |`service iscsid stop` |停止 iSCSI 服務 |
| &nbsp; |`service iscsid restart` |重新啟動 iSCSI 服務 |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |探索在指定的 hello 上可用的目標位址 |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |登入 toohello iSCSI 目標 |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |登出 hello iSCSI 目標 |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |列印 iSCSI 啟動器名稱 |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |請檢查 hello hello iSCSI 工作階段與 hello 主機上探索到的磁碟區的狀態 |
| &nbsp; |`iscsi –m session` |顯示所有 hello 主機與 hello StorSimple 裝置之間建立的 hello iSCSI 工作階段 |
|  | | |
| **多重路徑** |`service multipathd start` |啟動多重路徑 daemon |
| &nbsp; |`service multipathd stop` |停止多重路徑 daemon |
| &nbsp; |`service multipathd restart` |重新啟動多重路徑 daemon |
| &nbsp; |`chkconfig multipathd on` </br> 或 </br> `mpathconf –with_chkconfig y` |在開機時啟用多重路徑精靈 toostart |
| &nbsp; |`multipathd –k` |啟動 hello 互動式主控台進行疑難排解 |
| &nbsp; |`multipath –l` |列出多重路徑連接和裝置 |
| &nbsp; |`mpathconf --enable` |在 `/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>後續步驟
當您要在 Linux 主機上設定 MPIO，您可能也需要 toorefer toohello 遵循 CentoS 6.6 文件：

* [在 CentOS 上設定 MPIO](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Linux 訓練指南](http://linux-training.be/files/books/LinuxAdm.pdf)

