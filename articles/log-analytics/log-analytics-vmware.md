---
title: "aaaVMware 記錄分析監控解決方案 |Microsoft 文件"
description: "深入了解如何 hello VMware 監視解決方案可協助管理記錄檔和監視 ESXi 主機。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Log Analytics 中的 VMware 監視 (預覽) 解決方案

![VMware 符號](./media/log-analytics-vmware/vmware-symbol.png)

hello VMware 監視方案中記錄分析是解決方案，可協助您建立集中式的記錄和監視大量的 VMware 記錄方法。 本文說明如何疑難排解、 擷取並管理使用 hello 方案的單一位置中的 hello ESXi 主機。 Hello 方案，您可以查看您所有的單一位置的 ESXi 主機詳細的資料。 您可以看到最上層的事件計數、 狀態和趨勢的 VM 和 ESXi 主機提供透過 hello ESXi 主機記錄。 您可以檢視及搜尋 ESXi 主機集中記錄檔，來進行疑難排解。 而且，您可以根據記錄檔搜尋查詢來建立警示。

hello 解決方案會使用原生 syslog hello ESXi 主機 toopush 資料 tooa 目標 VM 具有 OMS 代理程式功能。 不過，hello 方案不是檔案寫入到 syslog hello 目標 VM 內。 開啟連接埠 1514 hello OMS 代理程式，並接聽 toothis。 在收到 hello 資料，hello OMS 代理程式會將 hello 資料推送至 OMS。

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
使用下列資訊 tooinstall hello 並設定 hello 方案。

* 新增 hello VMware 監視解決方案 tooyour OMS 工作區中使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。

#### <a name="supported-vmware-esxi-hosts"></a>支援的 VMware ESXi 主機
vSphere ESXi 主機 5.5 和 6.0

#### <a name="prepare-a-linux-server"></a>準備 Linux 伺服器
從 hello ESXi 主機建立 Linux 作業系統的 VM tooreceive 所有 syslog 資料。 hello [OMS Linux 代理程式](log-analytics-linux-agents.md)是所有的 ESXi 主機 syslog 資料 hello 集合點。 您可以使用多個 ESXi 主機 tooforward 記錄 tooa 單一 Linux 伺服器，如 hello 下列範例所示。  

   ![syslog 流程](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>設定 syslog 收集
1. 設定 VSphere 的 syslog 轉送。 設定 syslog 轉送的詳細的資訊 toohelp，請參閱[ESXi 上設定 syslog 5.x 和 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322)。 跳過**ESXi 主機組態** > **軟體** > **進階設定** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. 在 hello *Syslog.global.logHost*欄位中，加入您的 Linux 伺服器和 hello 連接埠號碼*1514年*。 例如，`tcp://hostname:1514` 或 `tcp://123.456.789.101:1514`。
3. 開啟 syslog hello ESXi 主機防火牆。 [ESXi 主機組態]  >  [軟體]  >  [安全性設定檔]  >  [防火牆]，然後開啟 [屬性]。  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. 請檢查該 syslog 已正確設定的 hello vSphere 主控台 tooverify。 確認 hello ESXI 主機的連接埠**1514年**設定。
5. 下載並安裝適用於 Linux 的 OMS 代理程式 hello hello Linux 伺服器上。 如需詳細資訊，請參閱 hello [OMS agent for Linux 的文件](https://github.com/Microsoft/OMS-Agent-for-Linux)。
6. Hello OMS Agent for Linux 安裝之後，請前往 toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d 目錄複製 hello vmware_esxi.conf 檔案 toohello /etc/opt/microsoft/omsagent/conf/omsagent.d 目錄和 hello 變更 hello 擁有者/群組與 hello 檔案的權限。 例如：

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. 執行來重新啟動 hello OMS Agent for Linux `sudo /opt/microsoft/omsagent/bin/service_control restart`。
8. 測試的使用 hello hello hello Linux 伺服器和 hello ESXi 主機之間的連線能力`nc`hello ESXi 主機上的命令。 例如：

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. 在 hello OMS 入口網站，執行記錄檔中的搜尋`Type=VMware_CL`。 當 OMS 會收集 hello syslog 資料時，它會保留 hello syslog 格式。 在 hello 入口網站，某些特定的欄位所擷取，例如*Hostname*和*ProcessName*。  

    ![類型](./media/log-analytics-vmware/type.png)  

    如果您檢視的記錄搜尋結果會類似上述的 toohello 映像，您要設定 toouse hello OMS VMware 監視方案儀表板。  

## <a name="vmware-data-collection-details"></a>VMware 資料收集詳細資料
hello VMware 監視解決方案使用 hello OMS Agents for Linux，您已啟用的 ESXi 主機從收集各種效能度量和記錄資料。

hello 下表顯示資料收集方法，以及如何收集資料的其他詳細資料。

| 平台 | OMS Agent for Linux | SCOM 代理程式 | Azure 儲存體 | SCOM 是否為必要項目？ | 透過管理群組傳送的 SCOM 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |每隔 3 分鐘 |

下表中的 hello 顯示 hello VMware 監視解決方案所收集的資料欄位的範例：

| 欄位名稱 | 說明 |
| --- | --- |
| Device_s |VMware 儲存裝置 |
| ESXIFailure_s |失敗類型 |
| EventTime_t |事件發生的時間 |
| HostName_s |ESXi 主機名稱 |
| Operation_s |建立 VM或刪除 VM |
| ProcessName_s |事件名稱 |
| ResourceId_s |hello VMware 主機名稱 |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |VMware SCSI 的狀態 |
| SyslogMessage_s |syslog 資料 |
| UserName_s |建立或刪除 VM 的使用者 |
| VMName_s |VM 名稱 |
| 電腦 |主機電腦 |
| TimeGenerated |產生時間 hello 資料 |
| DataCenter_s |VMware 資料中心 |
| StorageLatency_s |儲存體延遲 (毫秒) |

## <a name="vmware-monitoring-solution-overview"></a>VMware 監視解決方案概觀
hello VMware 磚會出現在 hello OMS 入口網站。 它提供任何失敗的高階檢視。 當您按一下 hello 磚時，您會進入儀表板檢視。

![圖格](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>瀏覽 hello 儀表板檢視
在 [hello **VMware**儀表板] 檢視中，依組織的刀鋒視窗：

* 失敗狀態計數
* 依事件計數的主機前幾名
* 前幾名事件計數
* 虛擬機器活動
* ESXi 主機磁碟的事件

![解決方案1](./media/log-analytics-vmware/solutionview1-1.png)

![解決方案2](./media/log-analytics-vmware/solutionview1-2.png)

按一下任何刀鋒視窗 tooopen 適合 hello 刀鋒視窗會顯示詳細的資訊的記錄分析搜尋窗格。

您可以從這裡編輯 hello 搜尋查詢 toomodify 會針對特定項目。 如需 OMS 搜尋 hello 基本概念的教學課程，請參閱 hello [OMS 記錄搜尋教學課程。](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>尋找 ESXi 主機事件
單一 ESXi 主機會產生多個記錄檔，取決於其程序。 hello VMware 監視解決方案集中管理它們，並摘要說明 hello 事件計數。 這個集中式的檢視可幫助您了解哪些 ESXi 主機有大量的事件，以及在您的環境中最常發生哪些事件。

![事件](./media/log-analytics-vmware/events.png)

您可以按一下 ESXi 主機或事件類型，進一步深入探詢。

當您按一下的 ESXi 主機名稱時，可以檢視該 ESXi 主機的資訊。 如果您想 toonarrow 結果 hello 事件類型，新增`“ProcessName_s=EVENT TYPE”`搜尋查詢中。 您可以選取**ProcessName** hello 搜尋篩選器中。 縮小 hello 的資訊。

![深入探詢](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>尋找高 VM 活動
在任何 ESXi 主機上皆可以建立及刪除虛擬機器。 它可協助系統管理員 tooidentify 多少 ESXi 主機建立的 Vm。 在中開啟，可協助 toounderstand 效能及容量規劃。 管理您的環境時，持續追蹤 VM 活動事件極為重要。

![深入探詢](./media/log-analytics-vmware/vmactivities1.png)

如果您想要讓其他 ESXi 主機 toosee VM 建立資料，請按一下 ESXi 主機名稱。

![深入探詢](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>常見的搜尋查詢
hello 解決方案包含其他有用的查詢，可協助您管理您的 ESXi 主機，例如高的儲存空間、 儲存體延遲，以及路徑失敗。

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![查詢](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>儲存查詢
儲存搜尋查詢是 OMS 中的標準功能，可協助您保留任何您認為有用的查詢。 您建立查詢，您有幫助之後，按一下以儲存它 hello**我的最愛**。 已儲存的查詢可讓您輕鬆地重複使用它稍後從 hello[我的儀表板](log-analytics-dashboards.md)頁面，您可以在其中建立您自己自訂的儀表板。

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>從查詢建立警示
您已建立您的查詢之後，您可能會想 toouse hello 查詢 tooalert 您特定事件發生時。 請參閱[記錄分析中的警示](log-analytics-alerts.md)如需有關資訊 toocreate 警示。 如需警示查詢和其他查詢範例的範例，請參閱 hello[監視 VMware 使用 OMS 記錄分析](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics)部落格文章。

## <a name="frequently-asked-questions"></a>常見問題集
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>我需要設定 hello ESXi 主機上的 toodo？ 它會對我目前的環境造成什麼影響？
hello 解決方案會使用原生 ESXi 主機 Syslog 轉送機制 hello。 您不需要任何額外的 Microsoft 軟體 hello ESXi 主機 toocapture hello 記錄上。 它應該會有影響很小 tooyour 現有環境。 不過，您需要 tooset syslog 轉送 ESXI 功能。

### <a name="do-i-need-toorestart-my-esxi-host"></a>我需要 toorestart 我的 ESXi 主機嗎？
否。 此處理序不需要重新啟動。 有時候，vSphere 不會正確更新 hello syslog。 在這種情況下，登入 toohello ESXi 主機並重新載入 hello syslog。 同樣地，您不需要 toorestart hello 主機，讓此程序未中斷 tooyour 環境。

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>我可以增加或減少記錄傳送的資料 tooOMS hello 磁碟區嗎？
是，您可以這麼做。 您可以在 vSphere 使用 hello ESXi 主機記錄層級設定。 記錄檔集合根據 hello*資訊*層級。 因此，如果您想 tooaudit VM 建立或刪除，您需要 tookeep hello*資訊*hostd 層級。 如需詳細資訊，請參閱 hello [VMware 知識庫](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658)。

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>為什麼 Hostd 不提供資料 tooOMS？ My 記錄檔設定為 tooinfo。
時發生 ESXi 主機的 bug hello syslog 時間戳記。 如需詳細資訊，請參閱 hello [VMware 知識庫](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202)。 套用 hello 因應措施之後，Hostd 應該正常運作。

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>我可以擁有多個 ESXi 主機轉送 syslog 資料 tooa 單一 VM 與 omsagent 嗎？
是。 您可以有多個 ESXi 主機轉送 tooa omsagent 與單一 VM。

### <a name="why-dont-i-see-data-flowing-into-oms"></a>為什麼我沒有看到資料流入 OMS？
這有幾個原因：

* hello ESXi 主機未正確達到資料 toohello VM 執行 omsagent。 tootest，執行下列步驟的 hello:

  1. tooconfirm，登入使用 ssh toohello ESXi 主機，然後執行下列命令的 hello:`nc -z ipaddressofVM 1514`

      如果不成功，vSphere hello 可能是進階組態設定不會更正。 請參閱[設定 syslog 收集](#configure-syslog-collection)如需有關如何 tooset 向上 hello ESXi 主機 syslog 轉送資訊。
  2. 如果 syslog 連接埠連線成功，但您仍然看不到任何資料，然後重新載入 hello syslog hello ESXi 主機上的使用 ssh toorun hello 下列命令：` esxcli system syslog reload`
* hello 與 OMS Agent 的 VM 設定不正確。 tootest，執行下列步驟的 hello:

  1. OMS 會接聽 toohello 連接埠 1514年，並將資料推入 OMS。 tooverify，並且已開啟，執行下列命令的 hello:`netstat -a | grep 1514`
  2. 您應該會看到連接埠 `1514/tcp` 已開啟。 如果不這麼做，請確認該 hello omsagent 已正確安裝。 如果看不到 hello 連接埠資訊，則不在 hello VM 上開啟 hello syslog 連接埠。

     1. 確認執行 OMS 代理程式時，使用該 hello `ps -ef | grep oms`。 如果未執行，請執行 hello 命令來啟動 hello 程序` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. 開啟 hello`/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf`檔案。

         確認 hello 適當的使用者和群組設定有效，類似於：`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         如果 hello 檔案不存在或 hello 使用者和群組設定有誤，採取更正動作[準備 Linux 伺服器](#prepare-a-linux-server)。

## <a name="next-steps"></a>後續步驟
* 使用[記錄搜尋](log-analytics-log-searches.md)中記錄分析 tooview 詳細的 VMware 主機的資料。
* [建立您自己的儀表板](log-analytics-dashboards.md)來顯示 VMware 主機的資料。
* 在特定的 VMware 主機事件發生時[建立警示](log-analytics-alerts.md)。
