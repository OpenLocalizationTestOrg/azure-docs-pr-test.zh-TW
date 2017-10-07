---
title: "Azure 服務匯流排的基本概念的 aaaOverview |Microsoft 文件"
description: "簡介 toousing Service Bus tooconnect Azure 應用程式 tooother 軟體。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure 服務匯流排

是否要應用程式或服務執行 hello 雲端或內部部署上，它通常需要 toointeract 與其他應用程式或服務。 tooprovide 廣泛實用的方式 toodo 此，Microsoft Azure 提供服務匯流排。 這篇文章探討這項技術，而且您可能會想 toouse 的原因描述它。

## <a name="service-bus-fundamentals"></a>服務匯流排基本概念

不同的情況需要不同的通訊方式。 某些情況下，讓應用程式傳送和接收訊息，透過簡單的佇列是 hello 最佳解決方案。 在其他情況下，普通的佇列仍嫌不足，具有發佈與訂閱機制的佇列會更好。 在某些情況下，就只需要應用程式之間的連線，而不需要佇列。 服務匯流排提供這三個選項，啟用您的應用程式 toointeract 數種不同方式。

Service Bus 是多租用戶雲端服務，這表示 hello 服務由多位使用者共用。 每個使用者，例如應用程式開發人員建立*命名空間*，然後定義需要該命名空間中的 hello 通訊機制。 圖 1 顯示此架構的外觀。

![][1]

**圖 1： 服務匯流排提供連接透過 hello 雲端應用程式的多租用戶服務。**

在一個命名空間內，您可以使用三種不同通訊機制的一或多個執行個體，這些機制各以不同的方式連接應用程式。 hello 選項有：

* 佇列，允許單向通訊。 每個佇列扮演中繼角色 (有時稱為代理人 )，儲存已傳送但尚未接收的訊息。 每個訊息會由單一收件者接收。
* 「主題」提供使用「訂用帳戶」的單向通訊，而單一主題可以有多個訂用帳戶。 類似佇列，主題會做為 broker，但每個訂用帳戶可以選擇性地使用篩選 tooreceive 唯一訊息符合特定準則。
* 轉送，提供雙向通訊。 與佇列和主題不同，轉送不是訊息代理程式，不會儲存途中訊息。 相反地，它只傳送它們的 toohello 目的端應用程式。

您在建立佇列、主題或轉送時會提供名稱。 這個名稱與任何您呼叫您的命名空間結合，建立 hello 物件的唯一識別碼。 應用程式可以提供此名稱 tooService 匯流排，然後使用該佇列、 主題或轉送 toocommunicate 彼此。 

toouse 其中任何物件在 hello 轉送案例中，Windows 應用程式可以使用 Windows Communication Foundation (WCF)。 此服務也稱為 [WCF 轉送](../service-bus-relay/relay-what-is-it.md)。 對於佇列和主題，Windows 應用程式可以使用服務匯流排定義的訊息 API。 toomake 這些物件更容易 toouse 從非 Windows 應用程式，Microsoft 提供 Java、 Node.js 和其他語言的 Sdk。 您也可以透過 HTTP 使用 [REST API](/rest/api/servicebus/)，存取佇列和主題。 

請務必在 hello 雲端中執行，即使服務匯流排本身 toounderstand (也就是在 Microsoft Azure 資料中心)，使用它的應用程式可以執行任何位置。 您可以使用 Azure，比方說或您自己的資料中心內執行的應用程式上執行的服務匯流排 tooconnect 應用程式。 您也可以使用它 tooconnect 在 Azure 或另一個執行的應用程式與內部部署應用程式或平板電腦和電話的雲端平台。 它是甚至可能 tooconnect 家庭應用裝置、 感應器和其他裝置 tooa 管理中心應用程式或其他 tooone。 Service Bus 是通訊機制，可從幾乎任何地方存取 hello 雲端中。 如何使用它相依於您應用程式需要 toodo。

## <a name="queues"></a>佇列

假設您決定使用服務匯流排佇列 tooconnect 兩個應用程式。 圖 2 顯示此情形。

![][2]

**圖 2：服務匯流排佇列提供單向非同步的佇列作業。**

hello 程序很簡單： 寄件者傳送訊息 tooa Service Bus 佇列，以及接收者在稍後收取該訊息。 一個佇列只可以有一個接收者 (如圖 2 所示)。 或多個應用程式可以從 hello 讀取相同的佇列。 在 hello 後者的情況下，只有一個收件者讀取每個訊息。 對於多點傳送服務，您應改用主題。

每一個訊息分成兩個部分：一組屬性 (各為機碼/值組) 和訊息承載。 hello 裝載可以是二進位、 文字或甚至是 XML。 使用方式，取決於哪些應用程式正在 toodo。 例如，應用程式傳送新的銷售資料的相關訊息可能會包含 hello 屬性**賣方 ="Ava"**和**量 = 10000**。 hello 訊息本文可能包含 hello 銷售帶正負號合約掃描的影像或者，如果沒有，保持空白。

接收者以兩種不同的方法從服務匯流排佇列讀取訊息。 hello 第一個選項，稱為 *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*、 從 hello 佇列移除訊息和立即將它刪除。 這個選項很簡單，但是如果 hello 接收者損毀它完成處理 hello 訊息之前，hello 訊息就會遺失。 它從 hello 佇列中已移除，因為沒有其他收件者可以存取它。 

hello 第二個選項，  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*，目的在於 toohelp 與此問題。 像**ReceiveAndDelete**、 **PeekLock**讀取從 hello 佇列移除訊息。 不過它不會刪除 hello 訊息。 相反地，它會鎖定 hello 訊息，因此看不見 tooother 接收者，然後等待三個事件的其中一個：

* 如果 hello 接收者處理程序成功 hello 訊息，則會呼叫[complete （)](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)，並 hello 佇列刪除 hello 訊息。 
* 如果 hello 接收者決定時，無法成功處理 hello 訊息，則會呼叫[Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon)。 hello 佇列然後 hello 鎖定移除 hello 訊息，並讓您可以使用 tooother 接收者。
* 如果 hello 接收者 （依預設為 60 秒） 呼叫這些方法都可設定的一段時間內，hello 佇列會假設失敗 hello 收件者。 在此情況下，其行為就如同已經呼叫 hello 接收者**放棄**，進行 hello 訊息可用 tooother 接收者。

請注意，這裡會發生什麼情況： hello 相同訊息可能會傳送兩次，可能是 tootwo 不同的接收者。 使用服務匯流排佇列的應用程式對此事件必須有因應之道。 toomake 重複偵測更容易，每個訊息都有唯一[MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId)屬性，預設會保持 hello 相同無論多少次 hello 訊息從佇列讀取。 

佇列在許多情況下都很有用。 它們可讓應用程式 toocommunicate 即使兩者都不在 hello 執行相同的時間，項目與批次和行動應用程式特別有用。 如果佇列有多個接收者，由於傳送的訊息會襲捲這些接收者，此佇列也提供自動的負載平衡。

## <a name="topics"></a>主題

因為它們是很有用，佇列不一定 hello 絕佳的解決方案。 有時，服務匯流排主題更適合。 圖 3 闡明此概念。

![][3]

**圖 3： 根據 hello 訂閱應用程式指定的篩選器，它可以接收部分或所有的 hello 訊息傳送 tooa Service Bus 主題。**

A*主題*類似許多方式 tooa 佇列中。 寄件者送出 hello 訊息 tooa 主題，送出的郵件 tooa 佇列，而且這些訊息的外觀 hello 與佇列相同的方式。 hello 差異是，各個主題可讓每個接收應用程式 toocreate 自己*訂用帳戶*藉由定義*篩選*。 訂閱者接著會看到符合該篩選條件 hello 訊息。 例如，圖 3 顯示一個傳送者、一個主題及三個訂閱者，而訂閱者各有其本身的篩選：

* 訂閱者 」 1 收到包含 hello 屬性的訊息*賣方 ="Ava"*。
* 訂閱者 2 收到的訊息包含 hello 屬性*賣方 ="Ruby"*和 （或) 包含*量*其值大於 100000 的屬性。 可能是 Ruby 是 hello 銷售經理，因此她想 toosee 她自己的銷售和所有大型的銷售，無論誰可讓它們。
* 訂閱者 3 已經過設定其篩選器*True*，這表示它會接收所有訊息。 例如，此應用程式可能會負責維護稽核記錄，因此需要 toosee 所有 hello 訊息。

訂閱者 tooa 主題可與佇列讀取訊息使用[ReceiveAndDelete 或 PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)。 不同於佇列，不過，單一訊息傳送 tooa 主題可以接收多個訂用帳戶。 這個方法時，通常稱為*發佈和訂閱*(或*pub/sub*)，是很有用，每當有多個應用程式有興趣 hello 相同的訊息。 藉由定義 hello 右篩選，每個訂閱者可以點選入只需要 toosee hello 訊息資料流 hello 部分。

## <a name="relays"></a>轉送

佇列和主題都是透過訊息代理程式來提供單向非同步通訊。 流量只往一個方向流動，傳送者和接收者之間並未直接連接。 但如果不想要這種連線又該如何？ 假設您的應用程式需要 tooboth 傳送和接收訊息，或可能是您想要它們之間的直接連結，也不需要 broker toostore 訊息。 這類 tooaddress 情況下，服務匯流排提供*轉送*，如圖 4 所示。

![][4]

**圖 4：服務匯流排轉送在應用程式之間提供同步、雙向的通訊。**

hello 有關轉送的問題 tooask 如下： 為何要使用它？ 即使我不需要的佇列，為什麼會讓通訊透過雲端服務而不只是直接互動的應用程式嗎？hello 回應是指直接可以比您想像更困難。

假設您想 tooconnect 兩個內部部署應用程式，同時公司的資料中心內執行。 每個應用程式都位於防火牆後面，且每個資料中心可能使用網路位址轉譯 (NAT)。 hello 防火牆會封鎖所有但少數的連接埠和 NAT 上的內送資料表示 hello 電腦執行每個應用程式沒有您可以直接從外部 hello 資料中心達到的固定的 IP 位址。 而不需一些額外的協助，這些應用程式透過連接 hello 公用網際網路是有問題。

服務匯流排轉送有所幫助。 toocommunicate 雙向透過轉送，每個應用程式建立與服務匯流排的輸出 TCP 連線，則會保持開啟。 Hello 兩個應用程式之間的所有通訊都都透過這些連接。 因為每個連線已建立從內部 hello datacenter hello 防火牆允許連入流量 tooeach 應用程式而不需要開啟新的連接埠。 這個方法也會取得 hello NAT 問題，因為每個應用程式在整個 hello 通訊 hello 雲端存有一致的端點。 藉由交換 hello 轉送的資料，hello 應用程式可以避免 hello 問題會否則讓通訊更加困難。 

toouse 服務匯流排轉送，應用程式依賴 hello Windows Communication Foundation (WCF)。 服務匯流排提供，可讓您可以直接透過轉送的 Windows 應用程式 toointeract WCF 繫結。 已使用 WCF 應用程式通常可以指定其中一個繫結，然後溝通 tooeach 其他透過轉送。 然而，與佇列和主題不同，雖然可能從非 Windows 應用程式中使用轉送，但需要投入一些程式設計工作。沒有標準的程式庫可用。

與佇列和主題不同，應用程式不會明確建立轉送。 相反地，希望 tooreceive 訊息應用程式會建立 TCP 連線的服務匯流排，轉送時自動建立。 Hello 連線中斷，就會刪除 hello 轉送。 tooenable 的應用程式 toofind hello 轉送伺服器建立特定的接聽程式，服務匯流排所提供的登錄，可讓應用程式 toolocate 特定轉送依名稱。

轉送是 hello 絕佳的解決方案，當您需要應用程式之間的直接通訊。 舉例來說，假設有一個在內部部署資料中心執行的飛機訂票系統，且必須從自助登機亭、行動裝置和其他電腦來存取此系統。 在所有這些系統上執行的應用程式無法依賴 hello 雲端 toocommunicate 中的服務匯流排轉送，只要它們可能會執行。

## <a name="summary"></a>摘要

應用程式連接一律已建置完整的解決方案的一部分，而且 hello 範圍的情況需要使用應用程式和服務 toocommunicate 彼此設定 tooincrease 還有更多的應用程式與裝置連線的 toohello 網際網路。 藉由提供以雲端為基礎的技術達成透過佇列、 主題和轉送的通訊，Service Bus 以外的工具 toomake 這個必要的函式更容易 tooimplement 和更廣泛。

## <a name="next-steps"></a>後續步驟

現在，您學到的 Azure 服務匯流排的 hello 基本概念，請遵循這些連結 toolearn 更多。

* 如何 toouse[服務匯流排佇列](service-bus-dotnet-get-started-with-queues.md)
* 如何 toouse[服務匯流排主題](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* 如何 toouse[服務匯流排轉送](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [服務匯流排範例](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
