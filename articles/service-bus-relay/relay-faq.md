---
title: "aaaAzure 轉送常見問題集 |Microsoft 文件"
description: "取得有關 Azure 轉送常見問題的解答 toosome。"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Azure 轉送常見問題集

本文提供 [Azure 轉送](https://azure.microsoft.com/services/service-bus/)的一些常見問題集 (FAQ) 答案。 如需一般的 Azure 價格和支援資訊，請參閱 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)。

## <a name="general-questions"></a>一般問題
### <a name="what-is-azure-relay"></a>什麼是 Azure 轉送？
hello [Azure 轉送服務](relay-what-is-it.md)可幫助您更安全地位於內部公司的企業網路 toohello 公用雲端的公開服務，從而完成您的混合式應用程式。 您可以開啟防火牆連接，而不需要干擾變更 tooa 公司網路基礎結構來公開 hello 服務。

### <a name="what-is-a-relay-namespace"></a>什麼是轉送命名空間？
A[命名空間](relay-create-namespace-portal.md)是您可以使用 tooaddress 轉送資源應用程式中的範圍容器。 您必須建立命名空間 toouse 轉送。 這是其中一個 hello 第一個步驟中開始使用。

### <a name="what-happened-tooservice-bus-relay-service"></a>哪些情形的 tooService 匯流排轉送服務？
先前命名為服務匯流排轉送服務的 hello 現在稱為 WCF 轉送。 您可以繼續 toouse 這項服務如往常般。 hello 混合式連線功能是一項服務，從 Azure BizTalk 服務已經 transplanted 的更新的版本。 WCF 轉送和混合式連線繼續 toobe 支援。

## <a name="pricing"></a>價格
部分常見問題集有關此區段答案 hello 轉送定價結構。 如需一般的 Azure 價格資訊，也可以參閱 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)。 如需轉送價格的完整資訊，請參閱[服務匯流排價格詳細資料][Pricing overview]。

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>混合式連接和 WCF 轉送如何收費？
如需轉送定價的完整資訊，請參閱 hello[混合式連線和 WCF 轉送][ Pricing overview] hello 服務匯流排定價詳細資料頁面上的資料表。 此外 toohello 價格註明在該頁面上，您必須支付 hello 佈建您的應用程式的資料中心外部輸出的相關聯的資料傳輸。

### <a name="how-am-i-billed-for-hybrid-connections"></a>混合式連接如何計費？
以下是混合式連線計費案例的三個範例︰

*   案例 1：
    *   您有單一的接聽程式，例如 hello 安裝且持續執行 hello 整個月，混合式連線管理員的執行個體。
    *   您透過 hello 月 hello 連線傳送 3 GB 的資料。 
    *   您的總費用為 $5。
*   案例 2：
    *   您有單一的接聽程式，例如 hello 安裝且持續執行 hello 整個月，混合式連線管理員的執行個體。
    *   您透過 hello 月 hello 連線傳送 10 GB 的資料。
    *   您的總費用為 $7.5。 $5 hello 連線且前 5 GB + $2.50 的 hello 其他 5 GB 的資料。
*   案例 3：
    *   您有兩個執行個體，A 和 B 的 hello 安裝且持續執行 hello 整個月，混合式連線管理員。
    *   您透過連線 A hello 月傳送 3 GB 的資料。
    *   您透過連線 B hello 月傳送 6 GB 的資料。
    *   您的總費用為 $10.5。 這是連接的 $5 + $5 的連線 B + $0.50 （適用於 hello 連線 B 上的第六個 gb)。

請注意，hello 價格 hello 範例中使用適用於僅 hello 混合式連線預覽期間。 價格是主體 toochange 在公開上市的混合式連線時。

### <a name="how-are-hours-calculated-for-relay"></a>如何計算轉送時數？

只能在標準層命名空間中使用 WCF 轉送。 否則轉送的價格和[連線配額](../service-bus-messaging/service-bus-quotas.md)會保持不變。 這表示轉送繼續 toobe 計費根據 hello 訊息 （不是作業） 數目和轉送時數。 如需詳細資訊，請參閱 hello [「 混合式連線和 WCF 轉送 」](https://azure.microsoft.com/pricing/details/service-bus/) hello 定價詳細資料 頁面上的資料表。

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>如果有多個接聽程式連接的 tooa 特定轉送？
在某些情況下，單一轉送可能有多個已連線的接聽程式。 將轉送視為開啟連接的 tooit 至少一個轉送接聽程式時。 加入額外的轉送小時 tooan 開放式轉送接聽程式的結果。 hello 數目的轉送的寄件者 （叫用的用戶端或傳送訊息 toorelays） 會連接的 tooa 轉送不會影響 hello 轉送小時的計算。

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>針對 WCF 轉送如何計算 hello 訊息 」 計費表？
(**這適用於僅 tooWCF 轉送。訊息並不是混合式連線的成本。**)

一般情況下，則可計費訊息的轉送會計算使用 hello 相同方法，用於代理實體 （佇列、 主題和訂用帳戶），先前所述。 但是，請注意以下幾個差異。

傳送訊息 tooa 服務匯流排轉送視為 「 完整透過 」 傳送收到 hello 訊息 toohello 轉送接聽程式。 它不會被視為傳送作業 toohello 服務匯流排轉送，後面接著傳遞 toohello 轉送接聽程式。 要求-回覆樣式服務叫用 (的向上 too64 KB) 針對轉送接聽程式會導致兩個可計費訊息： hello 要求和回應 hello 一個可計費訊息的一個可計費訊息 (假設 hello 回應也 64 KB 或更小)。 這是有別於使用用戶端和服務之間的佇列 toomediate。 如果您使用用戶端和服務之間的佇列 toomediate，hello 相同的要求-回覆模式需要要求傳送 toohello 佇列，緊接著移除佇列/傳遞從 hello 佇列 toohello 服務。 這後面接著回應傳送 tooanother 佇列，並清除佇列/傳遞該佇列 toohello 用戶端。 使用假設整個 （向上 too64 KB) 的大小相同的 hello，hello 傳送 4 的可計費訊息的佇列模式結果。 您將支付兩次的相同模式您完成使用轉送訊息 tooimplement hello hello 數字。 當然，有優點 toousing 佇列 tooachieve 此模式中的，例如持續性和負載調節。 這些好處可能擔負 hello 額外費用。

使用 hello 所開啟的轉送**netTCPRelay** WCF 繫結會將訊息視為為個別的訊息，而資料流經 hello 系統的資料流。 當您使用此繫結時，只 hello 寄件者和接聽程式會顯示出來 hello hello 個別傳送和接收之訊息的框架。 針對使用 hello 的轉送**netTCPRelay**繫結時，所有資料會被視為資料流以供計算可計費訊息。 在此情況下，服務匯流排計算 hello 透過以 5 分鐘為基礎的每個個別轉送傳送或接收的資料量總計。 然後，將除以該總資料量 64 KB toodetermine hello 該轉送的可計費訊息數目在該時間內。

## <a name="quotas"></a>配額
| 配額名稱 | Scope | 類型 | 超出時的行為 | 值 |
| --- | --- | --- | --- | --- |
| 轉送上的並行接聽程式 |實體 |靜態 |其他連接的後續要求會遭到拒絕，並收到 hello 呼叫程式碼例外狀況。 |25 |
| 並行轉送接聽程式 |全系統 |靜態 |其他連接的後續要求會遭到拒絕，並收到 hello 呼叫程式碼例外狀況。 |2,000 |
| 服務命名空間中所有轉送端點的並行轉送連線 |全系統 |靜態 |- |5,000 |
| 每個服務命名空間的轉送端點 |全系統 |靜態 |- |10,000 |
| [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) 和 [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) 轉送的訊息大小 |全系統 |靜態 |將會拒絕超出這些配額的內送訊息和所呼叫的程式碼的 hello 收到例外狀況。 |64 KB |
| [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) 和 [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) 轉送的訊息大小 |全系統 |靜態 |- |無限制 |

### <a name="does-relay-have-any-usage-quotas"></a>轉送是否有任何使用量配額？
根據預設，對於所有雲端服務，Microsoft 會設定針對所有客戶的訂用帳戶計算的彙總每月使用量配額。 我們了解有時候您的需求可能會超過這些限制。 您可以隨時連絡客戶服務部門，讓我們知道您的需求並適當地調整這些限制。 服務匯流排的 hello 整體使用量配額如下：

* 50 億則訊息
* 2 百萬個轉送小時

雖然我們保留 hello 右 toodisable 超過其每月的使用量配額的帳戶，我們提供電子郵件通知，就能讓多個嘗試 toocontact hello 客戶之前採取任何動作。 超出這些配額的客戶仍需負責支付額外費用。

### <a name="naming-restrictions"></a>命名限制
轉送命名空間名稱的長度必須介於 6 到 50 個字元之間。

## <a name="subscription-and-namespace-management"></a>訂用帳戶和命名空間管理
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>我要如何移轉命名空間 tooanother Azure 訂用帳戶？

toomove 一個 Azure 訂用帳戶 tooanother 訂用帳戶中的命名空間，可以是使用 hello [Azure 入口網站](https://portal.azure.com)或使用 PowerShell 命令。 toomove 命名空間 tooanother 訂用帳戶，hello 命名空間必須已經是使用中。 hello 使用者執行 hello 命令必須是這兩個 hello 來源與目標訂用帳戶的系統管理員使用者。

#### <a name="azure-portal"></a>Azure 入口網站

toouse hello Azure 入口網站 toomigrate Azure 轉送命名空間，從一個訂用帳戶 tooanother 訂用帳戶，請參閱[移動資源 tooa 新資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md#use-portal)。 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove 從一個 Azure 訂用帳戶 tooanother 訂用帳戶，使用下列的命令順序的 hello 命名空間。 tooexecute 這項作業，hello 命名空間必須已經是作用中，且執行 hello PowerShell 命令的 hello 使用者必須是這兩個 hello 來源與目標訂用帳戶的系統管理員使用者。

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>疑難排解
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>有哪些 hello 例外狀況的 Azure 應用程式開發介面，轉送，所產生，也建議可以採取的動作嗎？
如需常見例外狀況的描述以及您可以採取的建議動作，請參閱[轉送例外狀況][Relay exceptions]。

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>什麼是共用的存取簽章，而且可以使用哪些語言 toogenerate 簽章？
共用存取簽章 (SAS) 是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。 如需有關如何 toogenerate 自己簽章中節點、 PHP、 Java、 C 和 C# 中，請參閱資訊[搭配共用的存取簽章的服務匯流排驗證][Shared Access Signatures]。

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>它是可能 toowhitelist 轉送端點嗎？
是。 hello 轉接用戶端會建立連接 toohello Azure 轉送服務使用的完整的網域名稱。 客戶可以在防火牆上新增 `*.servicebus.windows.net` 項目以支援 DNS 白名單。

## <a name="next-steps"></a>後續步驟
* [建立命名空間](relay-create-namespace-portal.md)
* [開始使用 .NET](relay-hybrid-connections-dotnet-get-started.md)
* [開始使用 Node](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md