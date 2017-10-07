---
title: "aaaAzure 轉送混合式連線通訊協定指南 |Microsoft 文件"
description: "Azure 轉送混合式連線通訊協定指南。"
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# Azure 轉送混合式連線通訊協定
Azure 的轉送是 hello hello Azure 服務匯流排平台的金鑰功能支柱的其中一個。 新的 hello*混合式連線*轉送的功能是根據 HTTP 和 WebSockets 了安全、 開放通訊協定的演變。 它會取代 hello 前者，同樣名為*BizTalk 服務*專屬通訊協定為基礎所建置的功能。 hello 整合混合式連接到 Azure 應用程式服務將會繼續為 toofunction-是。

「混合式連線」可在網路上的兩個應用程式之間，建立雙向的二進位串流通訊，藉此讓其中一方或雙方都能位在 NAT 或防火牆之後。 本文說明 hello 與 hello 混合式連線轉送接聽程式和傳送者角色，以及如何接聽程式接受新的連接中的用戶端連接的用戶端互動。

## 互動模型
hello 混合式連線轉送會提供 rendezvous 中的點 hello Azure 的雲端，這兩個合作對象可以探索並連線 toofrom 自己網路的觀點而言，連接兩個合作對象。 該 rendezvous 點稱為 「 混合式連線 」，在此範例與其他文件，在 hello 應用程式開發介面，還有 hello Azure 入口網站中。 hello 混合式連線的服務端點被指 tooas hello 「 服務 」 的 hello 本文其餘部分。 hello 互動模型會依賴其他許多網路 Api 所建立的 hello 命名法。

沒有先指出整備 toohandle 連入連線，且後續在到達時接受，它們的接聽程式。 在 hello 另一端，連線的用戶端 hello 接聽程式，必須是已接受以進行建立的雙向通訊路徑的連線 toobe 優先連接。
「 連接 」 的 「 接聽 」 和 「 接受 」 是 hello 相同條款您尋找在大部分的通訊端應用程式開發介面。

任何轉送的通訊模型有任一方進行優先的服務端點 hello 「 接聽程式 」 也 「 用戶端 」 以 colloquial 使用，並也可能會導致其他術語多載的傳出連接。 我們因此用於混合式連線的 hello 精確術語如下所示：

連線兩端的 hello 程式稱為 「 用戶端 」，因為它們是用戶端 toohello 服務。 hello 用戶端會等候及接受連線是 「 接聽程式 」，或者是說 toobe 在 hello 「 接聽程式角色。 」 啟動新的連接，透過 hello 服務的接聽程式優先 hello 用戶端或呼叫 hello 「 寄件者 」 中 「 寄件者角色 」。

### 接聽程式互動
hello 接聽程式有四個互動 hello 服務;所有網路詳細資料稍後所都述 hello 參考章節中的這篇文章。

#### 接聽
接聽程式是準備 tooaccept 連線 tooindicate 整備 toohello 服務，它會建立輸出的 WebSocket 連線。 hello 連接交握帶有 hello hello 轉送命名空間，與安全性權杖的權限會授與 hello 「 接聽 」 該名稱上，設定混合式連接名稱。
Hello 服務接受 hello WebSocket，則當 hello 註冊已完成，而且 hello 建立的 web WebSocket 就會保持運作以 hello 控制通道 」 來啟用所有後續的互動。 hello 服務可讓向上 too25 混合式連接上的並行接聽程式。 如果有 2 個以上的作用中接聽程式，則會將連入連線隨機平衡分配給這些接聽程式；但不保證會公平分配。

#### Accept
當寄件者開啟新的連線 hello 服務上，選擇 hello 服務，並通知 hello hello 混合式連接上的作用中接聽程式的其中一個。 此通知會透過 hello 控制開啟通道傳送 toohello 接聽程式為 hello 接聽程式的 hello WebSocket 端點包含 hello URL 必須連接接受 hello 連接 toofor JSON 訊息。

hello URL 可以和 hello 接聽程式，而無需任何額外的工作必須直接使用。
hello 編碼資訊只適用於一段時間，基本上只要為 hello 寄件者是願意 toowait hello 連接 toobe 建立端對端，但總 tooa 最大值為 30 秒。 hello URL 只能用於一次連線嘗試成功。 只要 hello 與 hello rendezvous 建立 URL 時，所有的其他活動的這個 WebSocket 連線是否從要轉送的 WebSocket 和 toohello 寄件者，而不需要任何介入的情況下或 hello 服務所解譯。

#### 續訂
hello 安全性權杖必須使用的 tooregister hello 接聽程式和維護 hello 接聽程式時，控制通道可能會過期。 hello 權杖到期不會影響進行中的連接，但可能會 hello 控制通道 toobe hello 服務或到期 hello 快照之後，即卸除。 hello 「 更新 」 作業是 hello 接聽程式的 JSON 訊息可以傳送 hello 控制通道，與相關聯的 tooreplace hello 權杖，以便 hello 控制通道可以維持長時間。

#### Ping
如果 hello 控制通道處於閒置一段時間，媒介 hello 方式，例如負載平衡器或 Nat 可以卸除 hello TCP 連線。 hello"的 ping"作業可避免的 hello 連線傳送 hello 通道可提醒 hello 網路路由的所有成員上少量資料的目的在於 toobe 運作，，並也可做為 「 即時 」 測試 hello 接聽程式。 Hello ping 失敗時，如果 hello 控制通道應該被視為無法使用，而且 hello 接聽程式應重新連接。

### 傳送者互動
hello 寄件者只需要單一 hello 服務互動： 連接。

#### 連線
hello 「 連接 」 作業會開啟 hello 服務，提供 hello 名稱，hello 混合式連接及 （選擇性，但需要依預設） 上的 WebSocket 開會 hello 查詢字串中的 「 傳送 」 權限的安全性權杖。 hello 服務然後互動方式，與先前說明的 hello hello 接聽程式，並 hello 接聽程式建立和此 WebSocket 會合連線。 已接受 hello WebSocket 之後，該 WebSocket 上的所有進一步互動都有使用已連線的接聽程式。

### 互動摘要
此互動模型 hello 結果會是該 hello 寄件者用戶端來自與 「 乾淨的 」 WebSocket，也就是連接的 tooa 接聽程式，並且需要任何進一步 preambles 或準備的信號交換。 此模型會讓幾乎任何現有 WebSocket 用戶端實作 tooreadily 利用 hello 混合式連線服務到其 WebSocket 用戶端層提供正確建構的 URL。

hello 接聽程式的 WebSocket 取得透過接受互動 hello 會合連線也是乾淨的而且可以要傳 tooany 現有 WebSocket 伺服器實作與一些區分 「 接受 」 的最小額外抽象概念其架構的區域網路接聽程式和混合式連線遠端上的作業 [接受] 作業。

## 通訊協定參考資料

本章節描述先前所述的 hello 通訊協定互動的 hello 詳細資料。

所有 WebSocket 連線都是在連接埠 443 上進行以作為從 HTTPS 1.1 (經常遭到某些 WebSocket 架構或 API 擷取) 開始的升級。 此處的描述不偏袒任何實作，不會建議您採用特定架構。

### 接聽程式通訊協定
hello 接聽程式通訊協定是由兩個連接筆勢和三個訊息作業所組成。

#### 接聽程式控制通道連線
hello 控制通道是以建立 WebSocket 連接開啟：

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

hello`namespace-address`是 hello 主機 hello 混合式連接，通常是 hello 表單 hello Azure 轉送命名空間的完整的網域名稱`{myname}.servicebus.windows.net`。

hello 查詢字串參數選項，如下所示。

| 參數 | 必要 | 說明 |
| --- | --- | --- |
| `sb-hc-action` |是 |參數必須是 hello 接聽程式的角色 hello **sb hc 動作 = 接聽** |
| `{path}` |是 |hello URL 編碼的命名空間路徑的 hello 預先設定的混合式連接 tooregister 此接聽程式上。 此運算式是固定的附加的 toohello`$hc/`路徑部分。 |
| `sb-hc-token` |是\* |hello 接聽程式必須提供有效且以 URL 編碼服務匯流排共用存取權杖 hello 命名空間或授與 hello 的混合式連接**接聽**右。 |
| `sb-hc-id` |否 |用戶端提供的這個選擇性識別碼可讓您進行端對端診斷追蹤。 |

如果因為 toohello 混合式連線路徑未註冊，或無效或遺漏語彙基元或其他一些錯誤而失敗 hello WebSocket 連線，使用 hello 一般 HTTP 1.1 狀態的意見反應模型提供 hello 錯誤回應。 狀態描述會包含錯誤追蹤識別碼，以供您告知 Azure 支援人員︰

| 代碼 | 錯誤 | 說明 |
| --- | --- | --- |
| 404 |找不到 |hello 混合式連接的路徑不正確或 hello 基底 URL 的格式不正確。 |
| 401 |未經授權 |hello 安全性權杖是遺漏或格式不正確或無效。 |
| 403 |禁止 |此路徑，此動作無效 hello 安全性權杖。 |
| 500 |內部錯誤 |發生錯誤 hello 服務中。 |

如果 hello WebSocket 連接刻意 hello 服務之後關閉它一開始設定，這樣使用適當 WebSocket 通訊協定錯誤的程式碼也包含追蹤的描述性的錯誤訊息以及通訊的 hello 原因識別碼。 控制通道不會關閉 hello 服務而不會發生錯誤狀況。 至於正常關機則為用戶端所為。

| WS 狀態 | 說明 |
| --- | --- |
| 1001 |已刪除或停用 hello 混合式連線路徑。 |
| 1008 |hello 安全性權杖已過期，因此違反 hello 授權原則。 |
| 1011 |發生錯誤 hello 服務中。 |

### 接受交握
hello [接受] 會傳送通知 hello 服務 toohello 接聽程式的先前建立的控制通道透過 WebSocket 文字框架中的 JSON 訊息。 沒有任何回覆 toothis 訊息。

hello 訊息包含 JSON 物件名為 [接受]，它會定義下列屬性，此時 hello:

* **位址**– hello URL 字串 toobe 用來建立 hello WebSocket toothe 服務 tooaccept 連入連線。
* **識別碼**– hello 這個連線的唯一識別碼。 Hello 識別碼 hello 寄件者用戶端所提供的則 hello 寄件者提供值，否則就是系統產生值。
* **connectHeaders** – 所有的 HTTP 標頭已提供 hello 寄件者，也包含 hello 秒 WebSocket 通訊協定和延伸 WebSocket 秒模組標頭所 toohello 轉送端點。

#### 接受訊息

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

hello 位址 URL 提供在 hello JSON 訊息會由 hello 接聽程式建立 hello WebSocket 接受或拒絕 hello 寄件者通訊端。

#### 接受的 hello 通訊端
tooaccept，hello 接聽程式會建立 WebSocket 連接 toohello 提供位址。

如果 hello [接受] 訊息執行`Sec-WebSocket-Protocol`標頭，預期該 hello 接聽程式只接受 hello WebSocket，如果支援該通訊協定。 此外，它將 hello 標頭設定為建立 WebSocket hello。

hello 同樣適用 toohello`Sec-WebSocket-Extensions`標頭。 如果 hello framework 支援擴充功能，它應該設定 hello hello 所需的標頭 toohello 伺服器端回覆`Sec-WebSocket-Extensions`hello 延伸模組的交握。

必須當做 hello URL-建立 hello 是接受通訊端，但包含下列參數：

| 參數 | 必要 | 說明 |
| --- | --- | --- |
| `sb-hc-action` |是 |Hello 參數必須是接受通訊端`sb-hc-action=accept` |
| `{path}` |是 |（請參閱下列段落的 hello） |
| `sb-hc-id` |否 |請參閱先前的**識別碼**描述。 |

`{path}`是 hello URL 編碼的命名空間路徑預先設定混合式連接的 tooregister 上此接聽程式。 此運算式是固定的附加的 toothe`$hc/`路徑部分。 

hello`path`運算式可能會擴充與後置字元分隔的斜線之後會遵循 hello 註冊的名稱的查詢字串運算式。 這可讓 hello 寄件者用戶端 toopass 分派引數 toohello 接受接聽程式時，就會可能 tooinclude HTTP 標頭。 hello 預期的情況下則該 hello 接聽項架構剖析出 hello 固定的路徑部分和路徑中的 hello 註冊的名稱也會讓 hello 其餘部分，可能是不含前面加上任何查詢字串引數`sb-`，可用 toohello 應用程式制定 tooaccept 是否 hello 連線。

如需詳細資訊，請參閱下列 「 寄件者通訊協定 」 一節的 hello。

如果沒有發生錯誤，hello 服務可用來回覆，如下所示：

| 代碼 | 錯誤 | 說明 |
| --- | --- | --- |
| 403 |禁止 |hello URL 不是有效的。 |
| 500 |內部錯誤 |發生錯誤 hello 服務中 |

在建立 hello 連線之後，hello 伺服器關閉 hello WebSocket hello 寄件者 WebSocket 關閉，或是以 hello 下列狀態：

| WS 狀態 | 說明 |
| --- | --- |
| 1001 |hello 寄件者用戶端 hello 連接會關閉。 |
| 1001 |已刪除或停用 hello 混合式連線路徑。 |
| 1008 |hello 安全性權杖已過期，因此違反 hello 授權原則。 |
| 1011 |發生錯誤 hello 服務中。 |

#### 拒絕 hello 通訊端
檢查 hello 「 接受 」 訊息以便 hello 狀態碼和狀態描述通訊 hello 拒絕的原因可以傳送回 toohello 寄件者不需要類似的交握之後，請拒絕 hello 通訊端。

hello 通訊協定的設計選擇這裡是 toouse WebSocket 交握 （亦即設計的 tooend 中定義的錯誤狀態），因此接聽程式的用戶端實作可以繼續 toorely WebSocket 用戶端上，而不需要採用額外、 祼 HTTP 用戶端。

tooreject hello 通訊端，hello 用戶端會採用 hello 位址 URI 從 hello 「 接受 」 訊息與附加兩個的查詢字串參數 tooit，，如下所示：

| 參數 | 必要 | 說明 |
| --- | --- | --- |
| StatusCode |是 |數字型 HTTP 狀態碼。 |
| statusDescription |是 |Hello 拒絕人類可讀取的原因。 |

hello 產生 URI，就會使用 tooestablish WebSocket 連接。

當正確完成時，因為尚未建立任何 WebSocket，此交握會刻意失敗，而其 HTTP 錯誤碼為 410。 如果發生錯誤，下列程式碼的 hello 描述 hello 錯誤：

| 代碼 | 錯誤 | 說明 |
| --- | --- | --- |
| 403 |禁止 |hello URL 不是有效的。 |
| 500 |內部錯誤 |發生錯誤 hello 服務中。 |

### 接聽程式權杖更新
關於 tooexpire hello 接聽程式的權杖時，它可以傳送 hello 建立控制通道透過文字框架訊息 toohello 服務來取代。 訊息包含稱為 JSON 物件`renewToken`，而後者可定義下列屬性，此時 hello:

* **語彙基元**– 有效且以 URL 編碼的服務匯流排共用存取 token，為命名空間或授與 hello 的混合式連接**接聽**右。

#### renewToken 訊息

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

如果 hello 權杖驗證失敗，存取被拒，和 hello 雲端服務關閉並出現錯誤的 hello 控制通道 WebSocket。 否則不會有回覆。

| WS 狀態 | 說明 |
| --- | --- |
| 1008 |hello 安全性權杖已過期，因此違反 hello 授權原則。 |

## 傳送者通訊協定
建立接聽程式的有效相同 toohello 方式 hello 寄件者通訊協定。
hello 的目標是的 hello 端對端的最大透明度 WebSocket。 連線 toois hello 一樣 hello 接聽程式，但 hello 「 動作 」 不同，且此語彙基元的 hello 位址需要不同的權限：

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

hello*命名空間位址*是 hello 主機 hello 混合式連接，通常是 hello 表單 hello Azure 轉送命名空間的完整的網域名稱`{myname}.servicebus.windows.net`。

hello 要求可以包含任意額外 HTTP 標頭，包括應用程式定義的。 所有提供標頭流程 toohello 接聽程式，且可以找到上 hello`connectHeader`物件 hello**接受**控制 」 訊息。

hello 查詢字串參數選項，如下所示：

| 參數 | 必要？ | 說明 |
| --- | --- | --- |
| `sb-hc-action` |是 |Hello 參數必須是 hello 寄件者角色， `action=connect`。 |
| `{path}` |是 |（請參閱下列段落的 hello） |
| `sb-hc-token` |是\* |hello 接聽程式必須提供有效且以 URL 編碼服務匯流排共用存取權杖 hello 命名空間或授與 hello 的混合式連接**傳送**右。 |
| `sb-hc-id` |否 |選擇性的識別碼，可讓端對端診斷追蹤，而且 hello 期間所使用的 toohello 接聽程式接受交握。 |

hello`{path}`是 hello URL 編碼的命名空間路徑的 hello 預先設定混合式連接的 tooregister 上此接聽程式。 hello`path`運算式可以使用後置字元和查詢字串運算式 toocommunicate 進一步擴充。 如果 hello 混合式連接已註冊 hello 路徑下`hyco`，hello`path`運算式可以是`hyco/suffix?param=value&...`後面接著 hello 此處定義的查詢字串參數。 完整運算式則可能如下所示︰

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

hello`path`運算式就會傳遞 toohello hello 位址 hello [接受] 控制訊息中所包含的 URI 中的接聽程式。

如果因為 toohello 混合式連接的路徑未註冊、 無效或遺漏語彙基元或其他一些錯誤而失敗 hello WebSocket 連線，使用 hello 一般 HTTP 1.1 狀態的意見反應模型提供 hello 錯誤回應。 狀態描述會包含錯誤追蹤識別碼，以供您告知 Azure 支援人員︰

| 代碼 | 錯誤 | 說明 |
| --- | --- | --- |
| 404 |找不到 |hello 混合式連接的路徑不正確或 hello 基底 URL 的格式不正確。 |
| 401 |未經授權 |hello 安全性權杖是遺漏或格式不正確或無效。 |
| 403 |禁止 |此路徑，此動作，hello 安全性權杖無效。 |
| 500 |內部錯誤 |發生錯誤 hello 服務中。 |

Hello WebSocket 連接刻意關閉 hello 服務，它有初始設定之後，如果這樣做的 hello 原因所以通訊使用適當 WebSocket 通訊協定錯誤的程式碼以及同時也包含一個描述性的錯誤訊息追蹤識別碼。

| WS 狀態 | 說明 |
| --- | --- |
| 1000 |hello 通訊端關閉 hello 接聽程式。 |
| 1001 |已刪除或停用 hello 混合式連線路徑。 |
| 1008 |hello 安全性權杖已過期，因此違反 hello 授權原則。 |
| 1011 |發生錯誤 hello 服務中。 |

## 後續步驟
* [轉送常見問題集](relay-faq.md)
* [建立命名空間](relay-create-namespace-portal.md)
* [開始使用 .NET](relay-hybrid-connections-dotnet-get-started.md)
* [開始使用 Node](relay-hybrid-connections-node-get-started.md)

