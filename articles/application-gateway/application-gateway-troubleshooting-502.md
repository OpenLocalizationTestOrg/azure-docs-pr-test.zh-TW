---
title: "aaaTroubleshoot Azure 應用程式閘道不正確的閘道 (502) 錯誤 |Microsoft 文件"
description: "深入了解如何 tootroubleshoot 應用程式閘道 502 錯誤"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>疑難排解應用程式閘道中閘道不正確的錯誤

了解 tootroubleshoot 不正確的閘道 (502) 錯誤收到時使用應用程式閘道的方式。

## <a name="overview"></a>概觀

設定應用程式閘道之後, 使用者可能會遇到的 hello 錯誤的其中一個是 「 伺服器錯誤： 502-網頁伺服器收到無效的回應時做為閘道或 proxy 伺服器 」。 由於 toohello 下列可能會發生此錯誤的原因：

* Azure 應用程式閘道的[後端集區未設定或空白](#empty-backendaddresspool)。
* 無 hello Vm 或中的執行個體的[虛擬機器擴展集均狀況良好](#unhealthy-instances-in-backendaddresspool)。
* 後端 Vm 或執行個體的虛擬機器擴展集[toohello 沒有回應的預設健全狀況探查](#problems-with-default-health-probe.md)。
* 無效或不適當的[自訂健康情況探查設定](#problems-with-custom-health-probe.md)。
* 使用者要求的[要求逾期或連線問題](#request-time-out)。

## <a name="empty-backendaddresspool"></a>空白的 BackendAddressPool

### <a name="cause"></a>原因

如果 hello 應用程式閘道有沒有 Vm 或虛擬機器擴展集設定 hello 後端位址集區中，它無法路由傳送任何客戶要求，並會擲回不正確的閘道錯誤。

### <a name="solution"></a>方案

請確定 hello 後端位址集區不是空的。 這可透過 PowerShell、CLI 或入口網站來完成。

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

hello hello 上述 cmdlet 的輸出應該包含非空白的後端位址集區。 下列範例會傳回兩個針對後端 VM 使用 FQDN 或 IP 位址設定的集區。 hello 的 hello BackendAddressPool 佈建狀態必須是 「 已成功 」。

BackendAddressPoolsText：

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>BackendAddressPool 中狀況不良的執行個體

### <a name="cause"></a>原因

如果所有 BackendAddressPool hello 執行個體都均狀況不良，應用程式閘道將不會包含任何後端 tooroute 使用者的要求。 後端執行個體的狀況良好，但沒有部署的 hello 需要應用程式時，這也可能是 hello 案例。

### <a name="solution"></a>方案

請確認 hello 執行個體的狀況良好，然後 hello 應用程式已正確設定。 核取 hello 後端執行個體是否已從中的其他 VM 可以 toorespond tooa ping hello 相同的 VNet。 如果設定為公用的結束點，請確定瀏覽器要求 toohello web 應用程式能否提供服務。

## <a name="problems-with-default-health-probe"></a>預設健全狀況探查的問題

### <a name="cause"></a>原因

502 錯誤也可能是經常 hello 預設健全狀況探查的指標是無法 tooreach 後端 Vm。 當已佈建應用程式閘道執行個體時，它會自動設定預設健全狀況探查 tooeach BackendAddressPool 使用 hello BackendHttpSetting 的屬性。 沒有使用者輸入所需的 tooset 此探查。 具體而言，設定負載平衡規則時，會在 BackendHttpSetting 和 BackendAddressPool 之間建立關聯。 預設探查已針對每個這些關聯並定期的健全狀況檢查連接 tooeach 中的執行個體 hello BackendAddressPool hello hello BackendHttpSetting 元素中指定的連接埠的應用程式閘道啟動。 下表列出 hello hello 預設健全狀況探查相關聯的值。

| 探查屬性 | 值 | 說明 |
| --- | --- | --- |
| 探查 URL |http://127.0.0.1/ |URL 路徑 |
| 間隔 |30 |探查間隔 (秒) |
| 逾時 |30 |探查逾時 (秒) |
| 狀況不良臨界值 |3 |探查重試計數。 hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。 |

### <a name="solution"></a>方案

* 確定預設網站已設定且正於 127.0.0.1 上進行接聽。
* 如果 BackendHttpSetting 指定 80 以外的通訊埠，hello 預設網站應該設定的 toolisten 在該連接埠。
* hello 呼叫 toohttp://127.0.0.1:port 應該會傳回 HTTP 結果碼為 200。 這應該會傳回 hello 30 秒逾時期間內。
* 確定設定的連接埠已開啟，並確認沒有任何防火牆規則或 Azure 網路安全性群組，會封鎖設定的 hello 連接埠上的傳入或傳出流量。
* 如果 FQDN 或公用 IP 與使用 Azure 傳統 Vm 或雲端服務，請確定該 hello 對應[端點](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json)開啟。
* 如果 hello VM 設定透過 Azure Resource Manager，而且超出 hello 應用程式閘道部署所在的 VNet[網路安全性群組](../virtual-network/virtual-networks-nsg.md)必須設定 hello tooallow 存取所需的連接埠。

## <a name="problems-with-custom-health-probe"></a>自訂健全狀況探查的問題

### <a name="cause"></a>原因

自訂的健全狀況探查允許更大的彈性 toohello 預設探查行為。 當使用自訂探查時，使用者可以設定 hello 探查間隔、 hello URL 路徑 tootest，以及多少失敗的回應 tooaccept 再將標示為狀況不良的 hello 後端集區執行個體。 會新增下列其他屬性的 hello。

| 探查屬性 | 說明 |
| --- | --- |
| 名稱 |Hello 探查的名稱。 這個名稱是使用的 toorefer toohello 探查後端 HTTP 設定中。 |
| 通訊協定 |使用 toosend hello 探查通訊協定。 hello 探查使用 hello hello 後端 HTTP 設定中所定義的通訊協定 |
| Host |主機名稱 toosend hello 探查。 只有當應用程式閘道上設定多站台時適用。 這與 VM 主機名稱不同。 |
| Path |Hello 探查相對路徑。 hello 有效路徑的開頭 '/'。 太傳送嗨探查\<通訊協定\>://\<主機\>:\<連接埠\>\<路徑\> |
| 間隔 |探查間隔 (秒)。 這是兩個連續探查 hello 時間間隔。 |
| 逾時 |探查逾時 (秒)。 如果這個逾時期限內未收到有效的回應，hello 探查被標示為失敗。 |
| 狀況不良臨界值 |探查重試計數。 hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。 |

### <a name="solution"></a>方案

驗證自訂健全狀況探查已正確設定為上述資料表中的 hello 該 hello。 除了上述 toohello 疑難排解步驟，也請確定 hello 下列：

* 請根據 hello 指定正確的 hello 探查[指南](application-gateway-create-probe-ps.md)。
* 如果應用程式閘道設定為單一站台，依預設 hello 主機名稱應指定為 '127.0.0.1'，除非否則在自訂探查設定。
* 請確定呼叫 toohttp: / /\<主機\>:\<連接埠\>\<路徑\>會傳回 HTTP 結果碼為 200。
* 請確認間隔、 逾時和 UnhealtyThreshold hello 可接受範圍內。
* 如果使用 HTTPS 探查，請確定該 hello 後端伺服器不需要 SNI hello 後端伺服器本身上設定 fallback 憑證。 
* 請確認間隔、 逾時與 UnhealtyThreshold hello 可接受範圍內。

## <a name="request-time-out"></a>要求逾時

### <a name="cause"></a>原因

當收到使用者的要求時，應用程式閘道套用 hello 設定規則 toohello 要求，並將其路由 tooa 後端集區執行個體。 可設定的間隔時間 hello 後端執行個體回應的等候。 根據預設，這個間隔為 **30 秒**。 如果應用程式閘道沒有在此時間間隔內收到來自後端應用程式的回應，使用者要求就會看到 502 錯誤。

### <a name="solution"></a>方案

應用程式閘道可讓使用者 tooconfigure BackendHttpSetting，這可以是則會套用 toodifferent 集區透過此設定。 不同的後端集區可以有不同的 BackendHttpSetting，因此可設定不同的要求逾時。

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>後續步驟

如果 hello 上述步驟無法解決 hello 問題，請開啟[支援票證](https://azure.microsoft.com/support/options/)。

