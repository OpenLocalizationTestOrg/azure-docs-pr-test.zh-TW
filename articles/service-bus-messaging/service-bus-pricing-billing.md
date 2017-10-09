---
title: "aaaService 匯流排定價和計費 |Microsoft 文件"
description: "服務匯流排定價結構的概觀。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>服務匯流排定價與計費
服務匯流排提供基本、標準和[進階](service-bus-premium-messaging.md)層。 您可以針對建立的每個服務匯流排服務命名空間選擇一個服務層，此選取層會套用至該命名空間內建立的所有實體。

> [!NOTE]
> 如需目前服務匯流排定價的詳細資訊，請參閱 hello [Azure 服務匯流排定價頁面](https://azure.microsoft.com/pricing/details/service-bus/)，和 hello [Service Bus 常見問題集](service-bus-faq.md#pricing)。
>
>

服務匯流排會使用下列兩個計量器佇列和主題/訂閱 hello:

1. **傳訊作業**：定義為針對佇列或主題/訂用帳戶服務端點的 API 呼叫。 此計量器將取代傳送或收到 hello 主要單元的可計費的使用量，對佇列和主題/訂閱訊息。
2. **代理連線**： 定義為 hello 尖峰數目持續連線開啟針對佇列、 主題或訂用帳戶在指定的一小時取樣期間內。 這個計費表只會套用在 hello 標準層次中，您可以在其中開啟其他連接 （連接之前，每個佇列/主題/訂閱的有限的 too100） 名義上的每個連線費用。

hello**標準**層批量與佇列和主題/訂閱，導致磁碟區為基礎的折扣的 too80 %hello 最高使用量層級執行的作業。 此外，還有每個月，可讓您 tooperform too12.5 百萬個作業，每個月免費 $ 10 美元的標準層基本費。

hello **Premium**層提供資源隔離層 hello CPU 和記憶體，以便在隔離狀態執行的每個客戶工作負載。 此資源容器稱為「傳訊單位」 。 每個進階命名空間都會被配置至少一個傳訊單位。 您可以為每個服務匯流排進階命名空間購買 1、2 或 4 個傳訊單位。 單一的工作負載或實體可以跨越多個傳訊單位，可在將變更 hello 傳訊單位數目，雖然計費是 24 小時或每日速率費用。 hello 結果是您 Service Bus 為基礎的解決方案的效能可預測且可重複。 此效能不僅更可預測並可取得，而且還更快速。

請注意，每個 Azure 訂用帳戶每月一次計費 hello 標準層基本費。 這表示您建立單一標準層的服務匯流排命名空間之後，您將會無法 toocreate 許多其他標準命名空間為您想在該相同的 Azure 訂用帳戶，而不會產生其他基底的費用。

hello[服務匯流排定價](https://azure.microsoft.com/pricing/details/service-bus/)表摘要說明 hello hello Basic、 Standard 和 Premium 層之間的功能差異。

## <a name="messaging-operations"></a>傳訊作業
Hello 新計價模型的一部分，變更的佇列和主題/訂閱計費。 這些實體會從每個每個作業的訊息 toobilling 計費轉換。 「 作業 」 是指 tooany API 進行呼叫時，對佇列或主題/訂閱服務端點。 這包括管理、傳送/接收和工作階段狀態的作業。

| 作業類型 | 說明 |
| --- | --- |
| 管理 |對佇列或主題/訂用帳戶執行的建立、讀取、更新、刪除 (CRUD)。 |
| 訊息 |用佇列或主題/訂用帳戶傳送和接收訊息。 |
| 工作階段狀態 |取得或設定佇列或主題/訂用帳戶上的工作階段狀態。 |

成本的詳細資訊，請參閱列在 hello hello 價格[服務匯流排定價](https://azure.microsoft.com/pricing/details/service-bus/)頁面。

## <a name="brokered-connections"></a>代理連線
*Brokered connections* 內含的客戶使用量模式，牽涉到針對佇列、主題或訂用帳戶而「持續連線」的大量傳送者/接收者。 持續連線的傳送者/接收者是指使用 AMQP 或 HTTP 進行連線，且接收逾時為非零值 (例如 HTTP 長時間輪詢) 的對象。 具有立即逾時的 HTTP 傳送者和接收者並不會產生代理連線。

連線配額及其他服務限制，請參閱 hello [Service Bus 配額](service-bus-quotas.md)發行項。

hello 標準層移除 hello 命名空間每個代理的連線限制，並計算代理的連線使用量跨 hello Azure 訂用帳戶。 如需詳細資訊，請參閱 hello[代理連線](https://azure.microsoft.com/pricing/details/service-bus/)資料表。

> [!NOTE]
> 1,000 個代理的連線隨附與 hello 標準訊息層級 （透過 hello 基本費），而且可以橫跨所有佇列、 主題和訂用帳戶相關聯的 hello Azure 訂用帳戶內。
>
>

<br />

> [!NOTE]
> 計費根據並行連線的 hello 尖峰數目和每小時根據每月 744 小時按比例。
>
>

| 高階層 |
| --- |
| 代理的連線不會向 hello Premium 層中。 |

如需代理連線的詳細資訊，請參閱 hello[常見問題集](#faq)本主題稍後的章節。

## <a name="faq"></a>常見問題集

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>什麼是代理連線，以及如何支付它們的費用？
代理的連線的定義 hello 下列其中一種：

1. 來自用戶端 tooa Service Bus 佇列或主題/訂閱的 AMQP 連線。
2. HTTP 呼叫 tooreceive 訊息從服務匯流排主題或佇列接收逾時值大於零。

服務匯流排 hello 尖峰數目超過 hello 的並行代理連線費用包含數量 （hello 標準層中為 1,000 個）。 每小時測量，除以中一個月 744 小時來按比例和加總每月計費週期的 hello 透過尖峰。 在針對 hello hello 依比例每小時尖峰總數 hello 計費期的 hello 結束套用 hello 包含數量 （每個月的 1,000 個代理連線）。

例如：

1. 10,000 台裝置均透過單一 AMQP 連線進行連線，並接收來自服務匯流排主題的命令。 hello 裝置傳送遙測事件 tooan 事件中心。 如果所有裝置都連線 12 小時內每一天，將套用下列連線費用的 hello (加法 tooany 中其他的服務匯流排主題費用): 10,000 個連線 * 12 小時 * 31 天 / 744 = 5,000 個代理連線。 Hello 每月額度 1,000 個代理連線之後, 您收取 4,000 個代理連線，速率為每個代理連線，總計 $120 個 $0.03 hello。
2. 10,000 台裝置透過 HTTP 從服務匯流排佇列接收訊息，並指定非零的逾時值。 如果所有裝置都連線 12 小時內每一天，您會看到下列連線費用 hello (加法 tooany 中其他的服務匯流排費用): 10,000 個 HTTP 接收連線 * 每天 12 小時 * 31 天/744 小時 = 5,000 個代理連線。

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>代理的連線費用套用 tooqueues 和主題/訂閱嗎？
是。 沒有任何使用 HTTP，不論 hello 多少傳送系統與裝置的事件傳送的連線費用。 使用逾時大於零的 HTTP 來接收事件，有時也稱為「長時間輪詢」，會產生代理連線的費用。 AMQP 連線都會產生代理的連線費用，無論 hello 連線正在使用的 toosend 或接收。 請注意，在基本層命名空間中，可以免費使用 100 個代理連線。 這也是 hello hello Azure 訂用帳戶所允許的代理連線的數目上限。 hello 個 Azure 訂用帳戶中的所有標準命名空間的前 1,000 個代理的連線是包含在任何額外的收費 （除了基本費 hello）。 因為這些額度足以 toocover 許多服務對服務傳訊案例中，代理的連線費用通常就要注意如果您計劃大量用戶端; toouse AMQP 或 HTTP 長期輪詢例如，tooachieve 效率事件資料流或啟用雙向通訊對許多裝置或應用程式執行個體。

## <a name="next-steps"></a>後續步驟
* 如需服務匯流排定價的完整詳細資訊，請參閱 hello[服務匯流排定價頁面](https://azure.microsoft.com/pricing/details/service-bus/)。
* 請參閱 hello [Service Bus 常見問題集](service-bus-faq.md#pricing)的一些常見的常見問題集有關服務匯流排定價和計費。

[Azure portal]: https://portal.azure.com
