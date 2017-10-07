---
title: "aaaDiagnostics 工具 tootroubleshoot StorSimple 8000 裝置 |Microsoft 文件"
description: "描述 hello StorSimple 裝置模式，並說明如何 toouse Windows PowerShell for StorSimple toochange hello 裝置模式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>使用 hello StorSimple 診斷工具 tootroubleshoot 8000 系列裝置的問題

## <a name="overview"></a>概觀

hello StorSimple 診斷工具診斷問題的相關的 toosystem、 效能、 網路和 StorSimple 裝置的硬體元件健全狀況。 hello 診斷工具可在各種情況中。 這些案例包括工作負載規劃、 部署 StorSimple 裝置、 評估 hello 網路環境中，以及決定 hello 效能的操作的裝置。 本文章提供 hello 診斷工具的概觀，並說明如何使用 hello 工具，StorSimple 裝置。

hello 診斷工具的目的主要是用於 StorSimple 8000 系列在內部部署的裝置 （8100 和 8600）。

## <a name="run-diagnostics-tool"></a>執行診斷工具

此工具可以透過您的 StorSimple 裝置 hello Windows PowerShell 介面執行。 有兩種 tooaccess hello 裝置的本機介面：

* [使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。
* [從遠端存取 hello 工具透過 hello Windows PowerShell for StorSimple](storsimple-remote-connect.md)。

在本文中，我們假設您已經連接透過 putty 連線 toohello 裝置序列主控台。

#### <a name="toorun-hello-diagnostics-tool"></a>toorun hello 診斷工具

一旦您已經連接的裝置 hello toohello Windows PowerShell 介面，執行下列步驟 toorun hello cmdlet hello。
1. 登入 toohello 裝置序列主控台中的 hello 步驟[使用 PuTTY tooconnect toohello 裝置序列主控台](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console)。

2. 輸入下列命令的 hello:

    `Invoke-HcsDiagnostics`

    如果未指定 hello 範圍參數，hello 指令程式會執行所有的 hello 診斷測試。 這些測試包括系統、硬體元件健全狀況、網路和效能。 
    
    toorun 只為特定的測試，請指定 hello 範圍參數。 比方說，toorun 只有 hello 網路測試類型

    `Invoke-HcsDiagnostics -Scope Network`

3. 選取並複製從 hello PuTTY hello 輸出至文字檔案，供進一步分析 視窗。

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>案例 toouse hello 診斷工具

使用 hello 診斷工具 tootroubleshoot hello 網路、 效能、 系統與硬體系統的健康情況 hello。 以下是可能的情況：

* **裝置離線** - StorSimple 8000 系列裝置已離線。 不過，從 hello Windows PowerShell 介面，看來，這兩個 hello 控制站正在執行。
    * 您可以使用此工具 toothen 判斷 hello 網路狀態。
         
         > [!NOTE]
         > 請勿 hello 註冊 （或透過安裝精靈進行設定） 之前，先在裝置上使用此工具 tooassess 效能和網路設定。 有效的 IP 在安裝精靈並註冊期間指派 toohello 裝置。 在未註冊的裝置上，您可以執行此 Cmdlet 診斷硬體健全狀況和系統。 使用 hello 範圍參數，例如：
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **持續性的裝置問題**-您遇到看上去 toopersist 裝置問題。 比方說，註冊失敗。 您可能也會發生問題的裝置 hello 裝置已成功註冊而且可運作一段時間之後。
    * 在此情況下，請使用此工具進行初步疑難排解，再向 Microsoft 支援服務登記服務要求。 我們建議您執行這項工具的工具，並擷取 hello 輸出。 然後，您可以提供此輸出 tooSupport tooexpedite 疑難排解。
    * 如果發生任何硬體元件或叢集失敗，您應該登記支援要求。

* **裝置效能低落** - StorSimple 裝置變慢。
    * 在此情況下，與範圍參數集 tooperformance 執行這個指令程式。 分析 hello 輸出。 收到 hello 雲端讀取寫入延遲。 使用 hello 報告延遲為最大可達成的目標，在內部資料處理 hello、 一些額外負荷的因素，然後再部署 hello hello 系統上的工作負載。 如需詳細資訊，請移至太[使用 hello 網路測試 tootroubleshoot 裝置效能](#network-test)。


## <a name="diagnostics-test-and-sample-outputs"></a>診斷測試和輸出範例

### <a name="hardware-test"></a>硬體測試

這項測試會判斷 hello 狀態 hello 硬體元件、 hello USM 韌體，以及在您的系統上執行的 hello 磁碟韌體。

* hello 硬體元件報告這些元件失敗的 hello 測試或不存在於 hello 系統。
* hello USM 韌體和磁碟的韌體版本 hello 控制器 0，控制器 1 會報告與您的系統中的共用元件。 如需硬體元件的完整清單，請移至︰

    * [主要機箱中的元件](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [EBOD 機箱中的元件](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> 如果 hello 硬體測試報告失敗的元件，[登入 Microsoft 支援服務的服務要求](storsimple-contact-microsoft-support.md)。

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>在 8100 裝置上執行硬體測試的輸出範例

以下是 StorSimple 8100 裝置的輸出範例。 在 hello 8100 機型的裝置，hello EBOD 機箱不存在。 因此，不會報告 hello EBOD 控制器元件。

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>系統測試

這項測試會報告 hello 系統資訊、 hello 可用的更新、 hello 叢集資訊，以及您的裝置 hello 服務資訊。

* hello 系統資訊包括 hello 模型、 裝置序號、 時區、 控制站狀態，以及 hello 系統上執行的 hello 詳細的軟體版本。 各種系統參數回報為 hello 輸出太移 toounderstand hello[解譯系統資訊](#appendix-interpreting-system-information)。

* hello 更新可用性將會報告是否有可用的 hello 一般和維護模式及其相關聯的套件名稱。 如果`RegularUpdates`和`MaintenanceModeUpdates`是`false`，這表示無法使用 hello 更新時。 您的裝置已是最新狀態。
* hello 叢集資訊包含 hello 有關各種邏輯元件的所有 hello HCS 叢集群組和其各自的狀態。 如果您看到 hello 報表，本節中的離線叢集群組[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。
* hello 服務資訊包括 hello 名稱和所有 hello HCS 的狀態，並且在您的裝置上執行的 Ci 服務。 這項資訊是很有幫助 hello Microsoft 支援服務疑難排解 hello 裝置問題。

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>在 8100 裝置上執行系統測試的輸出範例

以下是範例的輸出 hello 8100 裝置上執行的系統測試。

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>網路測試

這項測試會驗證 hello hello 網路介面、 連接埠、 DNS 和 NTP 伺服器連線、 SSL 憑證、 儲存體帳戶認證、 連線 toohello 更新伺服器，及您的 StorSimple 裝置上的 web proxy 連線的狀態。

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>僅啟用 DATA0 時的網路測試輸出範例

以下是 hello 8100 裝置之範例的輸出。 您可以在 hello 輸出中看到的：
* 只有啟用和設定 DATA 0 和 DATA 1 網路介面。
* 2-5 的資料不會啟用 hello 入口網站中。
* hello DNS 伺服器組態無效，而且 hello 裝置可以透過 hello DNS 伺服器連線。
* hello NTP 伺服器連線也是正常的。
* 連接埠 80 和 443 已開啟。 但已封鎖連接埠 9354。 根據 hello[系統的網路需求](storsimple-system-requirements.md)，您針對 hello 服務匯流排通訊需要 tooopen 此連接埠。
* hello SSL 憑證無效。
* hello 裝置可以連線 toohello 儲存體帳戶： _myss8000storageacct_。
* hello 連線 tooUpdate 伺服器無效。
* hello web proxy 未設定此裝置上。

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>啟用 DATA0 和 DATA1 時的網路測試輸出範例

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>效能測試

這項測試會報告透過 hello 雲端讀寫延遲為您的裝置 hello 雲端效能。 此工具可以使用的 tooestablish 的可讓您與 StorSimple 的 hello 雲端效能基準線。 hello 工具報告 hello 最大的效能 （如 讀寫延遲的最佳情況下），您可以取得您的連線。

當 hello 工具報告 hello 最大可達成的效能，我們可以使用部署時的目標 hello 工作負載時 hello 報告的讀寫延遲。

hello 測試會模擬 hello 與 hello hello 裝置上的不同的磁碟區類型相關聯的 blob 大小。 固定在本機之磁碟區的一般分層和備份使用 64 KB blob 大小。 勾選封存選項的分層磁碟區使用 512 KB blob 資料大小。 如果您的裝置有階層式和本機固定磁碟區設定，只有 hello 測試對應 too64 KB 的 blob 執行資料大小。

此工具 toouse，執行下列步驟的 hello:

1.  首先，混合建立分層磁碟區和勾選封存選項的分層磁碟區。 此動作可確保該 hello 工具會執行 hello 測試 64 KB 到 512 KB 的 blob 大小。

2. 您已建立並設定 hello 磁碟區之後，請執行 hello 指令程式。 輸入：

    `Invoke-HcsDiagnostics -Scope Performance`

3. 記下 hello 工具回報的 hello 讀取寫入延遲。 這項測試可能需要幾分鐘的時間 toorun 回報 hello 結果。

4. 如果 hello 連線延遲時間全部 hello 預期的範圍，則 hello hello 工具回報的延遲可用來當做最大可達成的目標部署的 hello 工作負載時。 考量內部資料處理時的一些額外負荷。

    如果報告 hello 讀寫延遲 hello 診斷工具是高：

    1. 設定 blob 服務儲存體分析，並分析 hello 輸出 toounderstand hello 延遲 hello Azure 儲存體帳戶。 如需詳細指示，請移太[啟用及設定儲存體分析](../storage/common/storage-enable-and-view-metrics.md)。 如果這些延遲也是您收到 hello StorSimple 診斷工具的 高 和 比較 toohello 數字，則您需要 toolog 搭配 Azure 儲存體服務要求。

    2. 如果 hello 儲存體帳戶延遲低，請連絡您的網路中的任何延遲問題您網路系統管理員 tooinvestigate。

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>在 8100 裝置上執行效能測試的輸出範例

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>附錄︰解譯系統資訊

以下是描述哪些 hello hello 系統資訊的各種 Windows PowerShell 參數對應至資料表。 

| PowerShell 參數    | 說明  |
|-------------------------|------------------|
| 執行個體識別碼             | 每個控制器都有相關聯的唯一識別碼或 GUID。|
| 名稱                    | hello 的 hello 裝置 hello Azure 入口網站的裝置部署期間設定的易記名稱。 hello 預設易記名稱為 hello 裝置序號。 |
| 模型                   | 您的 StorSimple 8000 系列裝置 hello 模型。 hello 模型可以是 8100 或 8600。|
| SerialNumber            | 指派在 hello 工廠 hello 裝置序號，並為 15 個字元。 例如，8600-SHX0991003G44HT 表示：<br> 8600 – 是 hello 裝置模型。<br>SHX – hello 製造站台。<br> 0991003 – 特定產品。 <br> G44HT hello 最後 5 位數會遞增 toocreate 唯一序號。 這可能不是連續的組合。|
| TimeZone                | hello 裝置時區中的設定 hello Azure 入口網站裝置部署期間。|
| CurrentController       | 您所連接的 toothrough hello Windows PowerShell 介面，您的 StorSimple 裝置 hello 控制器。|
| ActiveController        | hello 控制器為作用中裝置上，且它會控制所有 hello 網路和磁碟作業。 這可以是控制器 0 或控制器 1。  |
| Controller0Status       | 在您的裝置上的控制器 0 hello 狀態。 hello 控制器狀態可以是一般處於修復模式，或無法連線。|
| Controller1Status       | 您的裝置上的 hello 控制器 1 的狀態。  hello 控制器狀態可以是一般處於修復模式，或無法連線。|
| SystemMode              | hello StorSimple 裝置的整體狀態。 hello 裝置狀態可以是正常現象，維護，或已解除任務 （對應 toodeactivated hello Azure 入口網站中的）。|
| FriendlySoftwareVersion | hello 易記字串對應 toohello 裝置軟體版本。 執行 Update 4 的系統，hello 易記的軟體版本將會是 StorSimple 8000 系列 Update 4.0。|
| HcsSoftwareVersion      | 在您的裝置上執行 hello HCS 軟體版本。 比方說，hello HCS 軟體版本對應 tooStorSimple 8000 系列 Update 4.0 是 6.3.9600.17820。 |
| ApiVersion              | hello hello HCS 裝置的 Windows PowerShell API hello 軟體版本。|
| VhdVersion              | hello 的 hello 裝置 hello 原廠映像的軟體版本所隨附。 如果您重設您的裝置 toofactory 預設值，然後它會執行此軟體版本。|
| OSVersion               | hello hello Windows 伺服器作業系統 hello 裝置上執行的軟體版本。 hello StorSimple 裝置根據 hello 對應 too6.3.9600 的 Windows Server 2012 R2。|
| CisAgentVersion         | hello StorSimple 裝置上執行的 Ci 代理程式的版本。 此代理程式可協助您與 Azure 中執行的 hello StorSimple Manager 服務通訊。|
| MdsAgentVersion         | hello 版本對應 toohello Mds 的代理程式在您的 StorSimple 裝置上執行。 此代理程式將資料 toohello 監視和診斷服務 (MDS)。|
| Lsisas2Version          | hello 版本對應 toohello LSI 的驅動程式在您的 StorSimple 裝置上。|
| 容量                | 以位元組為單位的 hello 裝置 hello 總容量。|
| RemoteManagementMode    | 指出是否可以透過其 Windows PowerShell 介面從遠端管理的裝置 hello。 |
| FipsMode                | 指出是否要在裝置上啟用 hello 美國聯邦資訊處理標準 (FIPS) 模式。 hello FIPS 140 標準會定義核准 hello 保護機密資料的美國聯邦政府電腦系統所使用的密碼編譯演算法。 如果是執行 Update 4 或更新版本的裝置，預設會啟用 FIPS 模式。 |

## <a name="next-steps"></a>後續步驟

* 了解 hello [hello Invoke HcsDiagnostics cmdlet 的語法](https://technet.microsoft.com/library/mt795371.aspx)。

* 深入了解如何太[部署問題進行疑難排解](storsimple-troubleshoot-deployment.md)StorSimple 裝置上。
