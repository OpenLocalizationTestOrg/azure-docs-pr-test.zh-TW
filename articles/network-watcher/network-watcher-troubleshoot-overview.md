---
title: "疑難排解在 Azure 網路監看員 aaaIntroduction tooresource |Microsoft 文件"
description: "此頁面提供 hello 網路監看員資源疑難排解功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>簡介 tooresource 疑難排解在 Azure 網路監看員

虛擬網路閘道可提供 Azure 中內部部署資源與其他虛擬網路之間的連線。 監視這些閘道和其連線是關鍵 tooensuring 通訊並不被中斷。 網路監看員提供 hello 功能 tootroubleshoot 虛擬網路閘道與連線。 這可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。 呼叫時，網路監看員診斷 hello 虛擬網路閘道或連線和 hello 傳回適當結果 hello 健全狀況。 此要求是長時間執行的交易，一旦完成 hello 診斷會傳回 hello 結果。

![入口網站][2]

## <a name="results"></a>結果

hello 初步傳回的結果就會為 hello hello 資源健全狀況的整體概況。 Hello 之後 > 一節中所示，可以提供更深入的資訊資源：

hello 下列清單是 hello 值傳回以 hello 疑難排解應用程式開發介面：

* **startTime** -此值為 hello hello 疑難排解應用程式開發介面呼叫已啟動的時間。
* **endTime** -此值為 hello hello 疑難排解結束的時間。
* **code** - 如果有單一診斷失敗，此值為 UnHealthy。
* **結果**-結果是 hello 連接或 hello 虛擬網路閘道上傳回結果的集合。
    * **識別碼**-此值為 hello 錯誤類型。
    * **摘要**-此值為 hello 錯誤的摘要。
    * **詳細**-這個值會提供 hello 錯誤的詳細的描述。
    * **recommendedActions** -這個屬性是建議的動作 tootake 的集合。
      * **actionText** -這個值包含描述何種動作 tootake 的 hello 文字。
      * **actionUri** -這個值提供如何 hello URI toodocumentation tooact。
      * **actionUriText** -此值為 hello 動作文字的簡短描述。

下列表格顯示 hello 不同的錯誤類型 (在從上述清單中的 hello 結果 id) 所提供的 hello 和如果 hello 錯誤就會建立記錄檔。

### <a name="gateway"></a>閘道器

| 錯誤類型 | 原因 | 記錄檔|
|---|---|---|
| NoFault | 未偵測到任何錯誤時。 |是|
| GatewayNotFound | 找不到閘道或閘道尚未佈建。 |否|
| PlannedMaintenance |  閘道執行個體正在進行維護。  |否|
| UserDrivenUpdate | 當正在更新使用者時。 這可能是調整大小作業。 | 否 |
| VipUnResponsive | 無法連線到 hello hello 閘道的主要執行個體。 這會 hello 健全狀況探查失敗。 | 否 |
| PlatformInActive | 沒有與 hello 平台的問題。 | 否|
| ServiceNotRunning | hello 基礎服務並未執行。 | 否|
| NoConnectionsFoundForGateway | 沒有連線存在 hello 閘道上。 這只是警告。| 否|
| ConnectionsNotConnected | 未建立連線。 這只是警告。| 是|
| GatewayCPUUsageExceeded | hello 目前閘道器 CPU 使用量為 > 95%。 | 是 |

### <a name="connection"></a>連線

| 錯誤類型 | 原因 | 記錄檔|
|---|---|---|
| NoFault | 未偵測到任何錯誤時。 |是|
| GatewayNotFound | 找不到閘道或閘道尚未佈建。 |否|
| PlannedMaintenance | 閘道執行個體正在進行維護。  |否|
| UserDrivenUpdate | 當正在更新使用者時。 這可能是調整大小作業。  | 否 |
| VipUnResponsive | 無法連線到 hello hello 閘道的主要執行個體。 它會發生在 hello 健全狀況探查失敗。 | 否 |
| ConnectionEntityNotFound | 缺少連線組態。 | 否 |
| ConnectionIsMarkedDisconnected | hello 連接會標示為 「 已中斷連線]。 |否|
| ConnectionNotConfiguredOnGateway | hello 基礎服務沒有設定連接的 hello。 | 是 |
| ConnectionMarkedStandy | 基礎服務的 hello 會標示為待命。| 是|
| 驗證 | 預先共用的金鑰不相符。 | 是|
| PeerReachability | 無法連線到 hello 對等的閘道。 | 是|
| IkePolicyMismatch | hello 等閘道有 Azure 不支援的 IKE 原則。 | 是|
| WfpParse 錯誤 | 剖析 hello WFP 記錄時發生錯誤。 |是|

## <a name="supported-gateway-types"></a>支援的閘道類型

hello 下列清單顯示 hello 支援顯示支援的閘道和連接與疑難排解網路監看員。
|  |  |
|---------|---------|
|**閘道類型**   |         |
|VPN      | 支援        |
|ExpressRoute | 不支援 |
|Hypernet | 不支援|
|**VPN 類型** | |
|路由式 | 支援|
|原則式 | 不支援|
|**連線類型**||
|IPsec| 支援|
|VNet2Vnet| 支援|
|ExpressRoute| 不支援|
|Hypernet| 不支援|
|VPNClient| 不支援|

## <a name="log-files"></a>記錄檔

hello 資源疑難排解記錄檔會儲存在儲存體帳戶中，資源疑難排解完成之後。 hello 下列影像顯示 hello 範例內容，卻造成錯誤的呼叫。

![zip 檔案][1]

> [!NOTE]
> 在某些情況下，只有一群 hello 記錄檔會寫入 toostorage。

如需從 azure 儲存體帳戶下載檔案的指示，請參閱太[開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 另一項可用工具為儲存體總管。 儲存體總管的詳細資訊可以在這裡找到在 hello 下列連結：[存放裝置總管](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

hello **ConnectionStats.txt**檔案包含的 hello 連線，包括輸入和輸出的位元組、 連線狀態，以及已建立連線的 hello 時間 hello 的整體統計資料。

> [!NOTE]
> Hello hello zip 檔案中傳回的唯一疑難排解應用程式開發介面的 hello 呼叫 toohello 恢復狀況良好，如果是**ConnectionStats.txt**檔案。

下列範例類似 toohello hello 這個檔案的內容︰

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

hello **CPUStats.txt**檔案包含 CPU 使用量，以及適用於測試的 hello 階段的記憶體。  下列範例類似 toohello 是這個檔案 hello 內容：

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

hello **IKEErrors.txt**檔案包含在監視期間找不到任何 IKE 錯誤。

hello 下列範例顯示 hello IKEErrors.txt 之檔案的內容。 您的錯誤可能是根據 hello 問題而不同。

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

hello **Scrubbed wfpdiag.txt**記錄檔包含 hello wfp 記錄檔。 此記錄包含套件置放和 IKE/AuthIP 失敗的記錄。

hello 下列範例顯示 hello hello Scrubbed wfpdiag.txt 檔案內容。 在此範例中，連線 hello 共用的金鑰不正確，因為從 hello 下 hello 第 3 個列所示。 下列範例中的 hello 為 hello 記錄可能會根據 hello 問題很冗長只 hello 整個記錄檔的程式碼片段。

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

hello **wfpdiag.txt.sum**檔案是顯示 hello 緩衝區和處理的事件記錄檔。

hello 下列範例是 hello wfpdiag.txt.sum 檔案內容。
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>後續步驟

了解如何 toodiagnose VPN 閘道和透過連線 hello 入口網站瀏覽[閘道疑難排解-Azure 入口網站](network-watcher-troubleshoot-manage-portal.md)。
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
