---
title: "透過 VPN 閘道與 Azure 網路監看員 aaaDiagnose 在內部部署連線 |Microsoft 文件"
description: "本文說明如何 toodiagnose 內部部署連線，透過 VPN 閘道與 Azure 網路監看員資源疑難排解。"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>透過 VPN 閘道診斷內部部署連線

Azure VPN 閘道，可讓您處理您的內部部署網路與 Azure 虛擬網路之間的安全連接的 hello 需求的 toocreate 混合式解決方案。 因為您的需求都是唯一的所以是在內部部署 VPN 裝置 hello 選擇。 Azure 目前支援[數個 VPN 裝置](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable)，不斷地驗證與 hello 裝置廠商合作。 設定內部部署 VPN 裝置之前，檢閱 hello 裝置特定的組態設定。 同樣地，Azure VPN 閘道也使用一組用於建立連線的[受支援 IPsec 參數](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec)來進行設定。 目前沒有任何方式 toospecify 或選取特定的 hello Azure VPN 閘道的 IPsec 參數組合。 建立內部部署與 Azure 之間成功連線，hello 內部部署 VPN 裝置設定必須符合 Azure VPN 閘道所規定的 hello IPsec 參數。 如果 hello 都設定正確，沒有連線中斷且到目前為止疑難排解這些問題不是簡單式，而且通常是花了小時 tooidentify 並修正 hello 問題。

Hello Azure 網路監看員與疑難排解功能，您可以 toodiagnose 與您的閘道連線的任何問題，而且在幾分鐘內有足夠的資訊 toomake 做出明智的決策 toorectify hello 問題。

## <a name="scenario"></a>案例

您希望 Azure 與內部部署之間 tooconfigure 站台間連線使用 FortiGate hello 內部部署 VPN 閘道。 tooachieve 此案例中，您需要安裝程式的 hello:

1. 虛擬網路閘道 hello Azure 上的 VPN 閘道
1. 本機網路閘道-hello[在內部部署 (FortiGate) VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway)Azure 雲端中的表示法
1. 站對站連線 （原則式）- [hello VPN 閘道與 hello 之間連線的內部路由器](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [設定 FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

前往可以找到的詳細的逐步指導方針設定站對站組態：[使用 hello Azure 入口網站的站對站連接建立 VNet](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)。

其中一個 hello 重要的組態步驟設定 hello IPsec 通訊參數，任何設定錯誤導致連線能力 tooloss hello 與內部網路與 Azure 之間。 目前 Azure VPN 閘道已設定的 toosupport hello 的階段 1 之後 IPsec 參數。 請注意，如先前所述，您無法修改這些設定。  您可以看到在 hello 表中，hello Azure VPN 閘道支援的加密演算法為 AES256、 AES128、 和 3DES。

### <a name="ike-phase-1-setup"></a>IKE 第 1 階段設定

| **屬性** | **原則式** | **路由式和標準或高效能 VPN 閘道** |
| --- | --- | --- |
| IKE 版本 |IKEv1 |IKEv2 |
| Diffie-Hellman 群組 |群組 2 (1024 位元) |群組 2 (1024 位元) |
| 驗證方法 |預先共用金鑰 |預先共用金鑰 |
| 加密演算法 |AES256 AES128 3DES |AES256 3DES |
| 雜湊演算法 |SHA1(SHA128) |SHA1(SHA128)、SHA2(SHA256) |
| 階段 1 安全性關聯 (SA) 存留期 (時間) |28,800 秒 |10,800 秒 |

身為使用者，您會需要的 tooconfigure 您 FortiGate 設定的範例可以找到上[GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt)。 不知情的情況下您可以設定您 FortiGate toouse sha-512 為 hello 雜湊演算法。 此演算法並非原則式連線所支援的演算法，因此您的 VPN 連線會運作。

這些問題不難 tootroubleshoot 和根本原因通常是非直覺式。 在此情況下，您可以開啟支援票證 tooget 說明解決 hello 問題。 但有了 Azure 網路監看員疑難排解 API 後，您可以自行識別這些問題。

## <a name="troubleshooting-using-azure-network-watcher"></a>使用 Azure 網路監看員進行疑難排解

toodiagnose 您的連線，連線 tooAzure PowerShell，並起始 hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet。 您可以找到 hello 詳細資料上使用這個指令程式在[疑難排解虛擬網路閘道與連線-PowerShell](network-watcher-troubleshoot-manage-powershell.md)。 這個指令程式會在 toofew 分鐘 toocomplete。

Hello 指令程式完成之後，您可以瀏覽 toohello hello cmdlet 中指定的儲存位置 tooget 詳細上 hello 問題和記錄檔的相關資訊。 Azure 網路監看員會建立包含下列記錄檔的 hello zip 資料夾：

![1][1]

開啟 hello 檔案稱為 IKEErrors.txt 並顯示 hello 下列錯誤訊息，指出發生問題之內部 IKE 設定組態不正確。

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

如有提到在此情況下，您可以從 hello Scrubbed wfpdiag.txt 有關 hello 錯誤，取得詳細的資訊`ERROR_IPSEC_IKE_POLICY_MATCH`該負責人 tooconnection，未正常運作。

另一個常見設定錯誤是指定不正確的共用的金鑰的 hello。 如果在上述範例中已指定不同的共用的金鑰的 hello，hello IKEErrors.txt 顯示 hello 下列錯誤： `Error: Authentication failed. Check shared key`。

Azure 網路監看員的疑難排解功能可讓您 toodiagnose 和 hello 輕鬆簡單的 PowerShell cmdlet 疑難排解您的 VPN 閘道與連接。 目前，我們支援診斷 hello 下列條件，朝向加入更多條件。

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
| ConnectionsNotConnected | 無 hello 連線的連線。 這只是警告。| 是|
| GatewayCPUUsageExceeded | 目前閘道使用量 hello CPU 使用量為 > 95%。 | 是 |

### <a name="connection"></a>連線

| 錯誤類型 | 原因 | 記錄檔|
|---|---|---|
| NoFault | 未偵測到任何錯誤時。 |是|
| GatewayNotFound | 找不到閘道或閘道尚未佈建。 |否|
| PlannedMaintenance | 閘道執行個體正在進行維護。  |否|
| UserDrivenUpdate | 當正在更新使用者時。 這可能是調整大小作業。  | 否 |
| VipUnResponsive | 無法連線到 hello hello 閘道的主要執行個體。 它會發生在 hello 健全狀況探查失敗。 | 否 |
| ConnectionEntityNotFound | 缺少連線組態。 | 否 |
| ConnectionIsMarkedDisconnected | hello 連接標示為 「 中斷連接 」。 |否|
| ConnectionNotConfiguredOnGateway | hello 基礎服務沒有設定連接的 hello。 | 是 |
| ConnectionMarkedStandy | 基礎服務的 hello 會標示為待命。| 是|
| 驗證 | 預先共用的金鑰不相符。 | 是|
| PeerReachability | 無法連線到 hello 對等的閘道。 | 是|
| IkePolicyMismatch | hello 等閘道有 Azure 不支援的 IKE 原則。 | 是|
| WfpParse 錯誤 | 剖析 hello WFP 記錄時發生錯誤。 |是|

## <a name="next-steps"></a>後續步驟

學習使用 PowerShell 和 Azure 自動化的 toocheck VPN 閘道連線造訪[疑難排解 Azure 網路監看員監視 VPN 閘道](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
