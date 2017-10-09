---
title: "Azure 服務匯流排和事件中心的通訊協定指南中的 aaaAMQP 1.0 |Microsoft 文件"
description: "通訊協定指南 tooexpressions 和 Azure 服務匯流排和事件中心的 AMQP 1.0 的說明"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# Azure 服務匯流排和事件中樞的 AMQP 1.0 通訊協定指南

hello 進階訊息佇列通訊協定 1.0 是以非同步方式，安全地儲存，且可靠地將兩個合作對象之間傳輸訊息的標準化的框架和傳輸通訊協定。 它是 hello Azure Service Bus 訊息和 Azure 事件中心的主要通訊協定。 這兩項服務也支援 HTTPS。 改用 AMQP 已捨棄不用 hello 專屬 SBMP 通訊協定也支援。

AMQP 1.0 是 hello 組成的中介軟體供應商，例如 Microsoft 和 Red Hat 與許多傳訊中介軟體使用者，例如 JP Morgan 尋求代表 hello 涵蓋了金融服務產業的廣泛的業界共同作業的結果。 hello AMQP 通訊協定和延伸模組規格的 hello 技術標準化論壇 OASIS，但它已達成的國際標準，為 ISO/IEC 19494 正式核准。

## 目標

本文簡要摘要說明 hello 核心概念，以及目前正在進行最終處理在 hello OASIS AMQP 技術委員會的草稿延伸模組規格一小群 hello AMQP 1.0 訊息規格的並說明如何在 Azure 服務匯流排實作，這些規格為基礎。

hello 目標是要讓 Azure 服務匯流排 AMQP 1.0 透過任何平台 toobe 無法 toointeract 上使用任何現有的 AMQP 1.0 用戶端堆疊的任何開發人員。

常見的一般用途 AMQP 1.0 堆疊 (例如 Apache Proton 或 AMQP.NET Lite) 已經實作所有核心 AMQP 1.0 軌跡。 這些基本手勢有時會包裝較高層級的 api。Apache 的 Proton 甚至會提供兩個、 hello 命令式 Messenger API 和 hello 反應式反應器 API。

在下列討論 hello，我們假設 hello 管理 AMQP 連線、 工作階段和連結和 hello 框架傳輸和處理流程控制會由 hello 個別堆疊 (例如 Apache PROTON-C)，並不需要太多如果有任何特定從應用程式開發人員注意。 我們以抽象方式假設 hello 存在幾個 API 基本型別，例如 hello 能力 tooconnect 和 toocreate 某種形式的*寄件者*和*接收者*抽象物件，則有一些圖形的`send()`和`receive()`作業分別。

討論 Azure 服務匯流排的進階功能 (例如訊息瀏覽或工作階段管理) 時，將會以 AMQP 詞彙說明這些功能，但也可作為以這個假設 API 抽象概念為基礎的多層式虛擬實作。

## AMQP 是什麼？

AMQP 是框架處理和傳輸通訊協定。 框架處理表示它會為以網路連線的任一方向流入的二進位資料串流提供結構。 hello 結構提供不同的資料區塊，呼叫的描述*框架*，連接的 hello 合作對象之間交換 toobe。 hello 傳輸功能會確認通訊雙方都可以建立共用的了解關於何時應該傳送框架，和當傳輸應該視為已完成。

不同於稍早過期的草稿 hello AMQP 工作小組所產生的版本仍在使用幾個訊息代理人，hello 工作群組的最終狀態，和標準化 AMQP 1.0 通訊協定不並未規定訊息代理程式或任何特定的拓樸 hello 存在訊息代理程式內的實體。

hello 通訊協定可支援佇列和發佈/訂閱實體，如同 Azure 服務匯流排訊息代理程式與互動的對稱式端對端通訊。 它也可用來與傳訊基礎結構互動 hello 互動模式的不同於一般佇列，使用 Azure 事件中心的 hello 案例。 事件中心 tooit，傳送事件時的作用就像佇列，但就像是一個序列的儲存體服務時，會讀取事件有點類似於磁帶磁碟機。 hello 用戶端 hello 可用的資料流到挑選位移，並再提供該位移 toohello 最新可用的所有事件。

hello AMQP 1.0 通訊協定是設計的 toobe 可延伸，進一步啟用規格 tooenhance 其功能。 hello 本文所討論三個延伸模組規格說明這點。 透過其中設定 hello 原生 AMQP TCP 連接埠可能會很困難的現有 HTTPS/WebSockets 基礎結構通訊，繫結規格會定義如何 toolayer AMQP 透過 WebSockets。 與要求/回應中的 hello 訊息基礎結構互動方式為管理用途或 tooprovide 進階功能，hello AMQP 管理規格會定義 hello 所需的基本互動基本型別。 同盟的授權模型整合，hello AMQP 宣告型安全性規格會定義如何 tooassociate 並更新與連結相關聯的授權權杖。

## 基本 AMQP 案例

本節說明包括建立連線，工作階段和連結，以及從服務匯流排實體，例如佇列、 主題和訂用帳戶傳輸訊息 tooand Azure 服務匯流排與 AMQP 1.0 hello 基本使用方式。

hello 最可靠來源 toolearn AMQP 的運作方式是 hello AMQP 1.0 規格，但 hello 規格寫入 tooprecisely 指南實作，而不 tooteach hello 通訊協定。 本節著重於盡可能介紹描述服務匯流排如何使用 AMQP 1.0 的術語。 您可以檢閱更詳盡的簡介 tooAMQP，以及更廣泛的討論，AMQP 1.0，[視訊本課][this video course]。

### 連線和工作階段

通訊程式 AMQP 呼叫 hello*容器*; 這些包含*節點*、 哪些 hello 通訊那些容器內的實體。 佇列就屬於這類節點。 AMQP 允許多工作業，因此在單一連接可以用於許多節點; 之間的通訊路徑例如，應用程式用戶端可以同時從一個佇列，並傳送 tooanother 透過接收 hello 相同網路連線。

![][1]

hello 網路連線所以錨定 hello 容器。 它是由接聽和接受傳入的 TCP 連線的 「 hello receiver 角色，在進行的傳出 TCP 通訊端連線 tooa 容器 hello 用戶端角色中的 hello 容器啟始。 hello 連接交握包括交涉 hello 通訊協定版本、 宣告或交涉 hello 使用傳輸層安全性 (TLS/SSL) 和在 hello 連接範圍 SASL 為基礎的驗證/授權交握。

Azure 服務匯流排需要隨時都能 TLS hello 使用。 它支援連線透過 TCP 連接埠 5671、 使 hello TCP 連線進入 hello AMQP 通訊協定交握之前先重疊與 TLS 和也支援透過 TCP 連接埠 5672 連線 hello 伺服器，立即提供的強制升級連接 tooTLS 使用 hello AMQP 規定的模型。 hello AMQP WebSockets 繫結建立通道，然後是相等的 tooAMQP 5671 連線的 TCP 連接埠 443。

設定之後 hello 連線和 TLS，服務匯流排提供兩個 SASL 機制選項：

* SASL 純常用於傳遞使用者名稱和密碼認證 tooa 伺服器。 服務匯流排沒有帳戶，但是有具名的[共用存取安全性規則](service-bus-sas.md)，這些規則可授予權限並與某個金鑰相關聯。 hello 規則會使用的名稱為 hello 使用者名稱和 hello 索引鍵 （base64 編碼的文字） 會使用與 hello 密碼。 hello hello 選擇規則相關聯的權限會決定允許 hello 連接上的 hello 作業。
* SASL 就會使用 ANONYMOUS hello 用戶端想 toouse hello 宣告型安全性 (CBS) 模型，稍後會說明時，略過 SASL 授權。 使用此選項，用戶端可以連線以匿名方式短暫期間哪些 hello 用戶端可以只與 hello CBS 端點互動，必須先完成 hello CBS 交握。

建立 hello 傳輸連線之後，hello 容器每個宣告 hello 框架大小上限願意 toohandle，以及之後的閒置逾時它們會單方面中斷連線，如果 hello 連接上沒有任何活動。

他們也會宣告支援的並行通道數量。 通道是 hello 連接之上的傳輸單向、 輸出、 虛擬路徑。 工作階段會從 hello 互連的容器 tooform 雙向通訊路徑的每個通道。

工作階段的視窗型流量控制模型;建立工作階段時，每個合作對象宣告框架數目是願意 tooaccept 到其接收視窗。 因為 hello 合作對象的交換框架，傳送框架填滿視窗和傳輸停止 hello 視窗已滿時，才 hello 視窗取得重設或擴展使用 hello*流程 performative* (*performative*為 hello AMQP 通訊協定層級筆勢 hello 兩個合作對象之間交換的術語)。

此視窗為基礎的模型是約略相當 toohello TCP 概念的視窗型流量控制，但在 hello hello 通訊端中的工作階段層級。 hello 通訊協定的概念，允許多個並行工作階段的存在，因此高優先順序流量無法超過節流的正常流量中緊迫類似，高速公路 express 的通道。

Azure 服務匯流排目前只對每個連線使用一個工作階段。 hello 服務匯流排最大的畫面格大小為 262144 位元組 （256 K 位元組） 的服務匯流排一般和事件中心。 進階服務匯流排則為 1,048,576 (1 MB)。 服務匯流排並無任何特定工作階段層級節流 windows，但重設 hello 視窗定期連結層級流程控制的一部分 (請參閱[hello 下一節](#links))。

連線、通道和工作階段都是暫時的。 如果 hello 基礎連接摺疊的連線，TLS 通道、 SASL 授權內容和工作階段必須重新建立。

### 連結

AMQP 會透過連結傳輸訊息。 連結已啟用傳輸訊息，以單一方向; 的工作階段建立的通訊路徑hello 傳輸狀態交涉是透過 hello 連結和連接的 hello 合作對象之間的雙向。

![][2]

可以依其中一個容器建立連結，在任何時候，而且透過現有的工作階段，讓 AMQP 不同於其他許多通訊協定，包括 HTTP 和 MQTT，hello 啟始的傳輸與傳輸路徑所在 hello 合作對象建立獨佔權限hello 通訊端連線。

hello 起始連結的容器會要求相反容器 tooaccept hello 連結，並選擇傳送者或接收者的角色。 因此，請容器可以啟動建立單向或雙向通訊路徑，以 hello 後者化為成對的連結。

連結會以節點命名並產生關聯。 Hello 開頭所述，節點會 hello 通訊容器內的實體。

在服務匯流排節點是直接的對等 tooa 佇列、 主題、 訂用帳戶或無法傳送信件子佇列的佇列或訂閱。 hello 節點名稱用於 AMQP 因此是實體的 hello 相對 hello hello 服務匯流排命名空間內名稱。 如果佇列名為 **myqueue**，這也是它的 AMQP 節點名稱。 主題的訂用帳戶到 「 訂閱 」 資源集合，因此，訂用帳戶正在排序透過遵循 hello HTTP API 慣例**sub**或主題**mytopic** hello AMQP 節點名稱**mytopic/訂用帳戶/sub**。

hello 連線的用戶端也是必要的 toouse 建立連結; 的本機節點名稱Service Bus 不精準有關這些節點名稱，而且無法解譯。 AMQP 1.0 用戶端堆疊通常會使用這些暫時的節點名稱是唯一的 hello 用戶端 hello 範圍中配置 tooassure。

### 傳輸

建立連結後，即可透過該連結傳輸訊息。 在 AMQP，傳輸會執行與明確的通訊協定筆勢 (hello*傳輸*performative)，將訊息從傳送者 tooreceiver 移透過連結。 傳送已完成時，它 「 結束 」，這表示這兩個合作對象已建立該傳輸的 hello 結果的共用了解。

![][3]

在 hello 簡單的情況下，hello 寄件者可以選擇 toosend 訊息 「"預先決定，這表示 hello 用戶端不想要的 hello 結果，而且 hello 接收者不會提供任何意見 hello 運算結果的 hello。 這個模式是 hello AMQP 通訊協定層級，在服務匯流排支援，但未公開在任何 hello 用戶端應用程式開發介面。

hello 一般案例是尚未，傳送郵件，與 hello 接收器則表示接受或拒絕使用 hello*配置*performative。 在 hello 接收者無法接受 hello 訊息，因為任何原因 hello 拒絕訊息包含 hello 原因，是 AMQP 所定義的錯誤結構資訊時，就會發生拒絕。 如果訊息會被拒絕，因為 Service Bus 內部 toointernal 錯誤，hello 服務會傳回可用於提供診斷提示 toosupport 人員，如果您提出支援要求該結構內的額外資訊。 稍後您會將了解錯誤的詳細資訊。

拒絕的特殊形式，為 hello*釋放*狀態時，表示該 hello 接收者有沒有技術 objection toohello 傳輸時，但也沒有興趣侷限 hello 傳輸。 確認案例存在，比方說，當訊息傳遞 tooa 服務匯流排用戶端，而且 hello 用戶端選擇太"放棄"hello 訊息因為它無法執行所產生的處理 hello 訊息; hello 工作hello 訊息傳遞本身不是錯誤。 該狀態的一種變化為 hello*修改*狀態，允許變更 toohello 訊息會在釋放。 服務匯流排目前不會使用該狀態。

hello AMQP 1.0 規格定義的進一步配置狀態，稱為*收到*，特別是幫助的 toohandle 連結復原。 連結復原可讓 reconstituting hello 狀態的連結和任何暫止的新的連接和工作階段，當 hello 先前連線和工作階段已遺失的傳遞項目。

Service Bus 不支援連結復原。如果 hello 用戶端將會遺失尚未訊息 hello 連接 tooService 匯流排傳送暫止，該訊息傳輸都會遺失，和 hello 用戶端必須重新連接，重新建立 hello 連結，然後重試 hello 傳輸。

因此，服務匯流排和事件中心支援 「 至少一次 」 傳輸其中 hello 寄件者可以確保 hello 訊息具有已儲存並接受，但並不支援 「 正好一次 」 在 hello AMQP 層級，其中 hello 系統會嘗試 toorecover 傳輸hello 連結，並繼續 toonegotiate hello 傳遞狀態 tooavoid 出現重複的 hello 訊息傳輸。

傳送 toocompensate 可能重複，服務匯流排佇列和主題支援重複的偵測為選擇性功能。 重複偵測記錄 hello 的所有傳入訊息的訊息識別碼，在使用者定義的時間間隔，然後以無訊息模式所傳送的所有訊息的卸除 hello 相同的訊息識別碼的相同期間。

### 流量控制

此外 toohello 工作階段層級流程控制模型先前所討論，每個連結都有它自己的流程控制模型。 工作階段層級流程控制會防止 hello 容器具有 toohandle 太多框架之後連結層級流程控制放 hello 負責多少訊息它想 toohandle 從連結的應用程式, 和時。

![][4]

在連結上傳輸只會發生在 hello 寄件者有足夠*連結信用*。 連結信用為計數器設定 hello 接收者使用 hello*流程*performative，也就是範圍 tooa 連結。 當 hello 寄件者指派連結信用額度時，它會嘗試註冊該信用 toouse 所傳遞訊息。 每個訊息傳遞遞減 1 hello 連結剩餘的信用額度。 當 hello 連結信用額度用完時，便會停止傳遞項目。

Hello receiver 角色服務匯流排時，它立即提供 hello 寄件者很大的連結信用額度，以便立即傳送訊息。 當使用連結信用額度時，服務匯流排偶爾會將傳送*流程*performative toohello 寄件者 tooupdate hello 連結信用結餘。

在 hello 寄件者角色中，服務匯流排傳送訊息 toouse 上任何未處理的連結信用額度。

「 接收 」 呼叫 hello API 層級會轉譯成*流程*performative 傳送 hello 用戶端，匯流排和 Service Bus 取用的第一次所花的 hello 信用額度的 tooService 可用，解除鎖定 hello 佇列中，鎖定的訊息和轉移。 如果不沒有傳遞隨時可用的任何訊息，任何連結的任何未完成信用額度與建立特定的實體會維持記錄順序抵達，和訊息會鎖定，可供使用時，toouse 傳送任何未處理的信用額度。

hello 傳輸到其中一種 hello 終端機的狀態結束時釋放 hello 訊息鎖定*接受*，*拒絕*，或*釋放*。 hello 終止狀態時從服務匯流排移除 hello 訊息*接受*。 它會保留在服務匯流排和 toohello 下一個接收者時傳送嗨到達 hello 的任何其他狀態傳遞。 到達 hello toorepeated 拒絕或釋放到期的 hello 實體所允許的最大傳遞計數時，服務匯流排會自動將 hello 訊息移到 hello 實體無效信件佇列。

即使 hello 服務匯流排應用程式開發介面不會直接公開這類選項今天，較低層級 AMQP 通訊協定用戶端可以使用 hello 連結信用模型 tooturn hello"提取 style"之間的互動"推送型 」 模型發出一個單位的每個接收要求的信用卡藉由發出大量的連結點數，不需要任何進一步的互動，您可以使用，然後接收訊息。 透過 hello 支援推播[MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount)或[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)屬性設定。 時，它們不是零，hello AMQP 用戶端會使用它作為 hello 連結信用額度。

在此內容中，它的重要 toounderstand hello 的 hello hello 實體內的 hello 訊息鎖定的 hello 到期時鐘，啟動時 hello 訊息取自 hello 實體不當 hello 訊息放 hello 網路上。 只要 hello 用戶端藉由發出連結信用指出整備 tooreceive 訊息，它就會因此預期的 toobe 主動提取訊息 hello 網路而且會準備 toohandle 它們。 否則即使傳送 hello 訊息之前，可能已過期 hello 訊息鎖定。 hello 使用的連結信用流量控制應直接反映 hello 立即整備 toodeal 使用可用的訊息分派 toohello 接收器。

在 [摘要] hello 下列各節提供的圖解概觀 hello performative 流程不同的應用程式開發介面互動期間發生。 每一節會說明不同的邏輯作業。 其中一些互動可能很「緩慢」，這表示它們可能只會在有需要時執行。 建立訊息寄件者在傳送 hello 第一個訊息或要求之前，不一定會網路互動。

hello 下表中的 hello 箭號顯示 hello performative 資料流程方向。

#### 建立訊息接收者

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={entity name},<br/>target={client link id}<br/>) |用戶端會做為接收者附加 tooentity |
| 附加的 hello 連結的服務匯流排回覆 |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={entity name},<br/>target={client link id}<br/>) |

#### 建立訊息傳送者

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |沒有動作 |
| 沒有動作 |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={client link id},<br/>target={entity name}<br/>) |

#### 建立訊息傳送者 (錯誤)

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |沒有動作 |
| 沒有動作 |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source=null,<br/>target=null<br/>)<br/><br/><-- detach(<br/>handle={numeric handle},<br/>closed=**true**,<br/>error={error info}<br/>) |

#### 將訊息接收者/傳送者關閉

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |沒有動作 |
| 沒有動作 |<-- detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |

#### 傳送 (成功)

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |沒有動作 |
| 沒有動作 |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |

#### 傳送 (錯誤)

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |沒有動作 |
| 沒有動作 |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**rejected**(<br/>error={error info}<br/>)<br/>) |

#### 接收

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> flow(<br/>link-credit=1<br/>) |沒有動作 |
| 沒有動作 |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=**receiver**,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |沒有動作 |

#### 多訊息接收

| 用戶端 | 服務匯流排 |
| --- | --- |
| --> flow(<br/>link-credit=3<br/>) |沒有動作 |
| 沒有動作 |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| 沒有動作 |< transfer(<br/>delivery-id={numeric handle+1},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| 沒有動作 |< transfer(<br/>delivery-id={numeric handle+2},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id+2},<br/>settled=**true**,<br/>state=**accepted**<br/>) |沒有動作 |

### 訊息

hello 下列各節說明使用服務匯流排 hello 標準 AMQP 訊息區段中的屬性，以及它們如何對應 toohello 服務匯流排 API 集。

#### 頁首

| 欄位名稱 | 使用量 | API 名稱 |
| --- | --- | --- |
| 持久 |- |- |
| 優先順序 |- |- |
| ttl |此訊息 toolive 的時間 |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| first-acquirer |- |- |
| delivery-count |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| 欄位名稱 | 使用量 | API 名稱 |
| --- | --- | --- |
| message-id |應用程式為此訊息定義的自由格式識別碼。 用於重複偵測。 |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| user-id |應用程式定義的使用者識別碼，服務匯流排無法加以解譯。 |無法透過 hello 服務匯流排 API 存取。 |
| 太|應用程式定義的目的地識別碼，服務匯流排無法加以解譯。 |[To](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| 主旨 |應用程式定義的訊息用途識別碼，服務匯流排無法加以解譯。 |[Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| 回覆太|應用程式定義的回覆路徑指示器，服務匯流排無法加以解譯。 |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlation-id |應用程式定義的相互關聯識別碼，服務匯流排無法加以解譯。 |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| Content-Type |Hello 主體中，未解譯的服務匯流排應用程式定義的內容類型指標。 |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| content-encoding |應用程式定義的內容編碼指標 hello 主體中，由 Service Bus 不解譯。 |無法透過 hello 服務匯流排 API 存取。 |
| absolute-expiry-time |宣告在哪一個絕對的立即 hello 訊息過期。 在輸入時忽略 (觀察到標頭 TTL)，在輸出時授權具權威性。 |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| creation-time |宣告在哪些時間 hello 訊息已建立。 服務匯流排未使用 |無法透過 hello 服務匯流排 API 存取。 |
| group-id |應用程式為一組相關訊息所定義的識別碼。 用於服務匯流排工作階段。 |[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| group-sequence |識別 hello 相對序號 hello 訊息，在工作階段的計數器。 服務匯流排會忽略。 |無法透過 hello 服務匯流排 API 存取。 |
| reply-to-group-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## 進階服務匯流排功能

本章節涵蓋 Azure Service Bus 草稿延伸 tooAMQP，目前正在開發中 hello OASIS 技術委員會的 AMQP 為基礎的進階的功能。 服務匯流排實作這些草稿 hello 最新版本，並採用這些草稿達到標準狀態導入的變更。

> [!NOTE]
> 服務匯流排訊息進階作業透過要求/回應模式受到支援。 hello 文件說明的 hello 詳細資料，這些作業的[服務匯流排 AMQP 1.0： 要求-回應為基礎的作業](service-bus-amqp-request-response.md)。
> 
> 

### AMQP 管理

hello AMQP 管理規格為 hello hello 草稿延伸，這裡所討論的第一個。 此規格會定義一組通訊協定筆勢 hello AMQP 通訊協定的最上層可讓以 hello 透過 AMQP 訊息基礎結構的管理互動。 hello 規格會定義泛型作業例如*建立*，*讀取*，*更新*，和*刪除*管理內的實體訊息基礎架構和一組查詢作業。

所有這些筆勢需要要求/回應與之間的互動 hello 用戶端 hello 訊息基礎結構，並因此 hello 規格會定義如何 toomodel 互動模式在 AMQP 之上： hello 用戶端連線 toohello 傳訊基礎結構，初始化工作階段，並再建立一對的連結。 上一個連結，hello 用戶端做為寄件者，並在其他 hello 它做為收件者，如此會建立一組可做為雙向通道的連結。

| 邏輯作業 | 用戶端 | 服務匯流排 |
| --- | --- | --- |
| 建立要求回應路徑 |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=**null**,<br/>target=”myentity/$management”<br/>) |沒有動作 |
| 建立要求回應路徑 |沒有動作 |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=null,<br/>target=”myentity”<br/>) |
| 建立要求回應路徑 |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=”myentity/$management”,<br/>target=”myclient$id”<br/>) | |
| 建立要求回應路徑 |沒有動作 |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=”myentity”,<br/>target=”myclient$id”<br/>) |

就地具有該配對的連結，hello 要求/回應實作十分簡單： 要求是傳送 tooan 實體，以了解此模式的 hello 訊息基礎結構內的訊息。 在該要求訊息中的 hello*回覆至*欄位 hello*屬性*部份設定 toohello*目標*到哪些 toodeliver hello 回應 hello 連結的識別項。 處理實體 hello 處理 hello 要求，然後提供 hello 回應 hello 透過會連結其*目標*識別碼符合指定的 hello*回覆給*識別項。

hello 模式很明顯地會需要這些 hello 用戶端容器和 hello hello 回覆目的地的用戶端產生識別項是唯一跨越所有用戶端，並基於安全性理由，也難以 toopredict。

hello 訊息交換用於 hello 管理通訊協定，用於所有其他通訊協定相同的模式，就可能發生在 hello 應用程式層級; 該使用 hello它們不會定義新的 AMQP 通訊協定層級手勢。 這是刻意設計的，以便應用程式立即利用符合 AMQP 1.0 堆疊規範的這些擴充功能。

服務匯流排未目前實作任何 hello 核心功能 hello 管理規格中，但基本 hello 宣告型安全性功能以及幾乎所有 hello hello 管理規格所定義的要求/回應模式hello 進階 hello 下列各節所述的功能。

### 宣告型授權

hello AMQP 宣告型授權 (CBS) 規格草稿 hello 管理規格要求/回應模式為基礎，並說明如何 toouse 同盟與 AMQP 搭配安全性權杖的通用的模型。

hello 簡介 > 中所討論的 AMQP hello 預設安全性模式根據 SASL，並整合與 hello AMQP 連接交握。 使用 SASL 優點 hello 它所提供的機制的一組已定義從正式依賴 SASL 任何通訊協定有哪些好處可擴充的模型。 這些機制包括"PLAIN"的使用者名稱和密碼、 「 外部 」 toobind tooTLS 層級安全性和 「 匿名 」 tooexpress hello 缺乏明確驗證/授權和其他的機制可讓多種不同的傳輸傳送驗證和/或授權的憑證或語彙基元。

AMQP 的 SASL 整合有兩個缺點︰

* 所有認證和權杖都都限定範圍的 toohello 連接。 傳訊基礎結構可能會想 tooprovide 區分每個實體為基礎; 的存取控制例如，允許 hello 持有人權杖 toosend tooqueue A 但 tooqueue b。Hello 連接上所錨定 hello 授權內容，用於無法 toouse 單一連接及尚未使用不同的存取語彙基元佇列 A 和 b。
* 存取權杖的有效時間通常有限。 此有效性需要 hello 使用者 tooperiodically 重新取得權杖，並提供發行新的權杖，如果 hello 使用者的存取權限已變更的機會 toohello 權杖簽發者 toorefuse。 AMQP 連線可能會持續很長的時間。 hello SASL 模型僅提供機會 tooset 語彙基元在連接時，可能是 hello 訊息基礎結構，也就是說 toodisconnect hello 用戶端或時，有 hello 權杖到期必須允許與一直持續不斷地的通訊 tooaccept hello 風險用戶端使用者具有存取權限可能已暫時 hello 中撤銷。

服務匯流排所實作的 hello AMQP CBS 規格，這些問題的兩個啟用精緻的因應措施： 它可讓用戶端與每個節點和那些權杖到期，而不會中斷 hello 訊息流程之前 tooupdate tooassociate 存取權杖。

CBS 定義名為的虛擬管理節點*$cbs*，toobe hello 訊息基礎結構所提供。 hello 管理節點接受語彙基元，代表 hello 訊息基礎結構中的任何其他節點。

hello 通訊協定手勢都是要求/回覆交換 hello 管理規格所定義。 表示 hello 用戶端會建立一組以 hello 連結*$cbs*節點，然後將要求的輸出連結，然後等候 hello 回應 hello hello 輸入的連結。

hello 要求訊息具有下列應用程式屬性的 hello:

| Key | 選用 | 值類型 | 值內容 |
| --- | --- | --- | --- |
| operation |否 |字串 |**put-token** |
| 類型 |否 |字串 |處於 put 的 hello 語彙基元 hello 型別。 |
| 名稱 |否 |字串 |套用 hello"audience"toowhich hello token。 |
| expiration |是 |timestamp |hello hello 權杖的到期時間。 |

hello*名稱*屬性會識別哪一個 hello 與語彙基元必須是相關聯的 hello 實體。 服務匯流排中的 hello 路徑 toohello 佇列或主題/訂用帳戶。 hello*類型*屬性會識別 hello 語彙基元類型：

| 權杖類型 | 權杖描述 | 主體類型 | 注意事項 |
| --- | --- | --- | --- |
| amqp:jwt |JSON Web 權杖 (JWT) |AMQP 值 (字串) |尚未提供。 |
| amqp:swt |簡單 Web 權杖 (SWT) |AMQP 值 (字串) |僅支援 AAD/ACS 所簽發的 SWT 權杖 |
| servicebus.windows.net:sastoken |服務匯流排 SAS 權杖 |AMQP 值 (字串) |- |

權杖會賦予權限。 服務匯流排知道三個基本權限：「傳送」可進行傳送、「接聽」可進行接收，以「管理」可進行管理實體。 AAD/ACS 所簽發的 SWT 權杖會明確將這些權限納入為宣告。 服務匯流排 SAS 權杖，請參閱 toorules hello 命名空間或實體上設定，且這些規則已設定權限。 簽章與 hello 與該規則相關聯的索引鍵的 hello 權杖而讓 hello 語彙基元 express hello 個別權限。 hello 語彙基元相關聯的實體使用*put 語彙基元*允許 hello 連線用戶端 toointeract 與 hello 實體，每個 hello 權杖 權限。 Hello 用戶端會接替 hello 連結*寄件者*角色需要 hello 「 傳送 」 權限; 採用性 hello*接收者*角色需要 hello 「 接聽 」 權限。

hello 回覆訊息具有 hello 下列*應用程式屬性*值

| Key | 選用 | 值類型 | 值內容 |
| --- | --- | --- | --- |
| status-code |否 |int |HTTP 回應碼 **[RFC2616]**。 |
| status-description |是 |字串 |Hello 狀態的描述。 |

hello 用戶端可以呼叫*put 語彙基元*重複和 hello 訊息基礎結構中的任何實體。 hello 語彙基元是已設定領域的 toohello 目前的用戶端和錨定 hello 目前連接上，表示 hello 伺服器卸除任何保留的語彙基元 hello 連線的時候。

目前服務匯流排實作 hello 只允許 CBS 搭配 hello SASL 方法 「 匿名 」。 SSL/TLS 連線一律必須存在先前 toohello SASL 交握。

hello 匿名機制，因此必須受到 hello 選擇 AMQP 1.0 用戶端。 Hello 初始連接信號交換期間，包括建立 hello 初始工作階段的匿名存取方式，不需要知道的建立者 hello 連接的服務匯流排發生。

一旦建立 hello 連接和工作階段，附加 hello 連結 toohello *$cbs*節點及傳送嗨*put 語彙基元*要求是 hello，僅允許的作業。 必須設定有效的語彙基元，成功使用*put 語彙基元*要求 20 秒內某些實體節點建立 hello 連線之後，否則 hello 會單方面中斷連線的服務匯流排。

hello 用戶端負責後續追蹤的權杖到期。 當權杖到期時，服務匯流排立即卸除所有連結 hello 連接 toohello 個別實體。 tooprevent hello，用戶端可以使用一個新隨時透過 hello 虛擬取代 hello 節點 hello 語彙基元*$cbs*管理節點與 hello 相同*put 語彙基元*軌跡，以及 hello，而不取得hello 裝載的方式流量在不同的連結上的流量。

## 後續步驟

toolearn 深入了解 AMQP，請造訪下列連結查看 hello:

* [服務匯流排 AMQP 概觀]
* [適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]
* [Windows Server 服務匯流排中的 AMQP]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[服務匯流排 AMQP 概觀]: service-bus-amqp-overview.md
[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server 服務匯流排中的 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
