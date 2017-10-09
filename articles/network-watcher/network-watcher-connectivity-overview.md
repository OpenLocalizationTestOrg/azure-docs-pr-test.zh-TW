---
title: "在 Azure 網路監看員 aaaIntroduction tooconnectivity 核取 |Microsoft 文件"
description: "此頁面提供 hello 網路監看員連線功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a>Azure 網路監看員的簡介 tooconnectivity 簽入

hello 連線功能的網路監看員提供 hello 功能 toocheck 直接的 TCP 連線，從虛擬機器 tooa 虛擬機器 (VM)、 完整的網域名稱 (FQDN) 的 URI，或 IPv4 位址。 網路案例很複雜，它們在實作時使用網路安全性群組、防火牆、使用者定義的路由和 Azure 所提供的資源。 複雜的設定使得針對連線問題進行疑難排解成為一項挑戰。 網路監看員有助於縮短的時間 toofind hello 和偵測連線問題。 傳回的 hello 結果可以提供深入了解有連線問題是否由於 tooa 平台或使用者組態問題。 連線可以使用 [PowerShell](network-watcher-connectivity-powershell.md)、[Azure CLI](network-watcher-connectivity-cli.md) 和 [REST API](network-watcher-connectivity-rest.md) 來檢查。

> [!IMPORTANT]
> 連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。 Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="response"></a>Response

下表中的 hello 顯示 hello 連線能力檢查已完成執行時，傳回的屬性。

|屬性  |說明  |
|---------|---------|
|ConnectionStatus     | hello hello 連線能力檢查狀態。 可能的結果是 **Reachable** 和 **Unreachable**。        |
|AvgLatencyInMs     | 平均延遲期間 hello 連線能力檢查，以毫秒為單位。 (只有在檢查狀態為可連線時顯示)        |
|MinLatencyInMs     | Hello 連線期間的最小延遲檢查，以毫秒為單位。 (只有在檢查狀態為可連線時顯示)        |
|MaxLatencyInMs     | 最大延遲期間 hello 連線檢查以毫秒為單位。 (只有在檢查狀態為可連線時顯示)        |
|ProbesSent     | Hello 檢查期間傳送的探查數目。 最大值是 100。        |
|ProbesFailed     | Hello 檢查期間失敗的探查數目。 最大值是 100。        |
|Hops     | 躍點路徑來躍點從來源 toodestination。        |
|Hops[].Type     | 資源類型。 可能的值為 **Source**、**VirtualAppliance**、**VnetLocal** 和 **Internet**。        |
|Hops[].Id | Hello 躍點的唯一識別碼。|
|Hops[].Address | Hello 躍點 IP 位址。|
|Hops[].ResourceId | Hello 躍點如果 hello 躍點是一項 Azure 資源的資源識別碼。 如果是網際網路資源，ResourceID 是 **Internet**。 |
|Hops[].NextHopIds | hello hello 採取的下一個躍點的唯一識別項。|
|Hops[].Issues | 在該躍點的 hello 檢查期間遇到之問題的集合。 如果有任何問題，hello 值是空白的。|
|Hops[].Issues[].Origin | 在 hello 目前躍點，在發生問題。 可能的值包括：<br/> **輸入**-位於 hello 連結從 hello 前一個躍點 toohello 目前躍點的問題<br/>**輸出**-位於 hello 連結從 hello 目前躍點 toohello 下一個躍點的問題<br/>**本機**-位於 hello 目前躍點的問題。|
|Hops[].Issues[].Severity | hello 偵測到的 hello 問題嚴重性。 可能的值為 **Error** 和 **Warning**。 |
|Hops[].Issues[].Type |找到問題的 hello 型別。 可能的值包括： <br/>**CPU**<br/>**記憶體**<br/>**GuestFirewall**<br/>**DnsResolution**<br/>**NetworkSecurityRule**<br/>**UserDefinedRoute** |
|Hops[].Issues[].Context |找到的 hello 問題有關的詳細資料。|
|Hops[].Issues[].Context[].key |傳回的 hello 機碼值組的機碼。|
|Hops[].Issues[].Context[].value |傳回 hello 機碼值組的值。|

hello 以下是上一個躍點找到問題的範例。

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a>錯誤類型

hello 連線能力檢查傳回 hello 連線相關的錯誤類型。 hello 下表提供 hello 傳回目前的錯誤類型的清單。

|類型  |說明  |
|---------|---------|
|CPU     | 高 CPU 使用率。       |
|記憶體     | 高記憶體使用率。       |
|GuestFirewall     | 由於 tooa 虛擬機器防火牆組態會封鎖流量。        |
|DNSResolution     | Hello 目的地位址的 DNS 解析失敗。        |
|NetworkSecurityRule    | NSG 規則封鎖流量 (傳回規則)        |
|UserDefinedRoute|流量會卸除，因為 tooa 使用者定義或系統路由。 |

### <a name="next-steps"></a>後續步驟

深入了解如何瀏覽 tooverify 連線 tooa 資源：[檢查連線與 Azure 網路監看員](network-watcher-connectivity-powershell.md)。

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

