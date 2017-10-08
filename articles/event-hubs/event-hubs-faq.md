---
title: "aaaAzure 事件中心常見問題集 |Microsoft 文件"
description: "Azure 事件中樞常見問題集 (FAQ)"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>事件中樞常見問題集

## <a name="general"></a>一般

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>Hello 事件中心基本和標準層之間的差異為何？

hello Azure 事件中心標準層級提供沒有 hello 基本層級提供的功能。 下列功能的 hello 隨附於標準：
* 較長的事件保留期
* 其他代理的連線的詳細資訊，與用於多個包含 hello 號碼 overage 電量
* 超過單一消費者群組
* [擷取](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

如需有關定價層，包括事件中心專用的請參閱 hello[事件中心定價詳細資料](https://azure.microsoft.com/pricing/details/event-hubs/)。

### <a name="what-are-event-hubs-throughput-units"></a>事件中樞輸送量單位是什麼？

您明確地選取事件中心輸送量單位、 透過 hello Azure 入口網站或事件中心的資源管理員範本。 輸送量單位會套用 tooall 事件中心事件中樞命名空間中的，每個輸送量單位都具備 hello 命名空間 toohello 下列功能：

* 向上 too1 MB，每秒的輸入事件 （事件傳送到事件中心），但不超過 1000 個的輸入事件、 管理作業或控制 API 呼叫每秒。
* 向上 too2 MB 每秒的輸出事件 （取用自事件中心）。
* 向上 too84 GB 的儲存體事件 （足以應付 hello 預設 24 小時的保留期限）。

事件中心輸送量單位會每小時計費，根據 hello hello 指定小時所選單位的數目上限。

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>事件中樞的輸送量單位限制如何實施？
如果 hello 輸入輸送量總計或命名空間中的所有事件中心的 hello 總輸入事件率超過 hello 彙總輸送量單位額度，寄件者已節流，以及收到錯誤，指出已超過該 hello 輸入配額。

如果 hello 輸出輸送量總計或 hello 輸出事件率總計命名空間中的所有事件中心超過 hello 彙總輸送量單位額度，接收者已節流，以及收到錯誤，指出已超過該 hello 輸出配額。 Ingress 和 egress 強制執行配額分開，如此任何寄件者可能會導致事件耗用量 tooslow 關閉，也不可以接收者防止事件傳送到事件中心。

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>有 hello 可供選取的輸送量單位數目的限制嗎？
每個命名空間的預設配額為 20 個輸送量單位。 您可以藉由提出支援票證來要求較大的輸送量單位配額。 超過 20 輸送量單位限制 hello，配套中有 20 到 100 個輸送量單位。 請注意，使用超過 20 個輸送量單位移除 hello 能力 toochange hello 輸送量單元數目不提出支援票證。

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>我可以使用單一 AMQP 連線 toosend 並接收來自多個事件中心？
是的所有的 hello 事件中心位於 hello 是相同的命名空間。

### <a name="what-is-hello-maximum-retention-period-for-events"></a>事件的 hello 最大保留期限是什麼？
事件中樞標準層目前支援的最大保留期間為 7 天。 請注意，事件中樞的立意並非作為永久的資料存放區。 保留期限才會大於 24 小時適用於案例很方便 tooreplay 事件流入 hello 相同的系統。例如，tootrain 或確認新的機器學習模型上現有的資料。 如果您需要訊息保留超過 7 天，啟用[事件中心擷取](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)上您的事件中樞會提取 hello 資料，從您的事件中樞 toohello 儲存體帳戶或您所選擇的 Azure 資料湖服務帳戶。 啟用擷取將會產生費用，費用根據您購買的輸送量單位而定。

### <a name="where-is-azure-event-hubs-available"></a>哪裡可以取得 Azure 事件中樞？
在所有支援的 Azure 區域皆提供 Azure 事件中樞。 如需清單，請瀏覽 hello [Azure 區域](https://azure.microsoft.com/regions/)頁面。  

## <a name="best-practices"></a>最佳作法

### <a name="how-many-partitions-do-i-need"></a>我需要多少個分割區？
請切記 hello 事件中心上的資料分割計數，不能修改在安裝之後。 這一點之後，它是您開始使用之前需要多少個資料分割有關的重要 toothink。 

事件中心是設計的 tooallow 每個取用者群組的單一資料分割讀取器。 在大部分的使用情況下，hello 四個磁碟分割的預設值即已足夠。 如果您要尋找 tooscale 您處理的事件，您可能想 tooconsider 加入額外的磁碟分割。 不過，在您的命名空間中的 hello 彙總輸送量受限於 hello 輸送量單元數目的磁碟分割，沒有任何特定輸送量限制。 隨著您增加輸送量單元數目 hello 命名空間中，您可能需要額外的磁碟分割 tooallow 並行讀取器 tooachieve 他們自己的最大輸送量。

不過，如果您的模型，其中您的應用程式的同質 tooa 特定資料分割，增加的資料分割的 hello 數目可能不任何好處 tooyou。 如需此概念的詳細資訊，請參閱[可用性和一致性](event-hubs-availability-and-consistency.md)。

## <a name="pricing"></a>價格

### <a name="where-can-i-find-more-pricing-information"></a>哪裡可以找到更多定價資訊？
如需事件中心定價的完整資訊，請參閱 hello[事件中心定價詳細資料](https://azure.microsoft.com/pricing/details/event-hubs/)。

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>保留事件中樞事件超過 24 小時需要計費嗎？
hello 事件中心標準層並允許訊息保留超過 24 小時，最多 7 天的期間。 如果 hello hello 總數的預存的事件大小超過 hello hello 數目所選的輸送量單位 (每個輸送量單位 84 GB) 的儲存額度，收費 hello 大小超過允許的 hello hello 發行 Azure Blob 儲存體費率。 hello 每個輸送量單位的儲存額度涵蓋 24 小時 （hello 預設值） 的保留期限所有儲存體費用，即使 hello 輸送量單位已用完 toohello 最大輸入額度。

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>Hello 事件中心儲存體大小如何計算及收費？
hello 所有儲存的事件，包括所有的事件中心內事件標頭或磁碟儲存結構的內部負荷的大小總計的 hello 整天測量。 在 hello hello 天結尾，會計算 hello 儲存體大小峰值。 hello 每日的儲存額度是根據 hello 最小數目 （每個輸送量單位提供 84 GB 的額度） hello 天期間選取的輸送量單位計算。 如果 hello 總大小超過 hello 以日計費儲存體額度，使用 Azure Blob 儲存體費率來計費 hello 過多的儲存體 (在 hello**本機備援儲存體**速率)。

### <a name="how-are-event-hubs-ingress-events-calculated"></a>事件中樞輸入事件的計算方式為何？
每個事件傳送 tooan 事件中心會計入為可計費訊息。 *輸入事件*定義的資料單位，小於或等於為 too64 KB。 小於或等於任何事件 too64 KB 的大小會被視為 toobe 一個可計費事件。 如果 hello 事件大於 64KB，就會根據 toohello 事件大小 64KB 的倍數來計算 hello 可計費的事件數目。 例如，8 KB 的事件傳送 toohello 事件中心計費為一個事件，但傳送 toohello 事件中心的 96 KB 訊息會以兩個事件計費。

取用自事件中心，以及管理操作和控制呼叫，例如檢查點，都不會計入為可計費輸入事件，但總 toohello 輸送量單位額度累積的事件。

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>請勿代理的連線費用 tooEvent 中樞嗎？
連線費用 適用於只有在使用 hello AMQP 通訊協定時。 沒有任何使用 HTTP，不論 hello 多少傳送系統與裝置的事件傳送的連線費用。 如果您計劃 toouse AMQP (例如 tooachieve 效率事件資料流或 tooenable 雙向通訊 IoT 命令與控制案例中的)，請參閱 hello[事件中心定價資訊](https://azure.microsoft.com/pricing/details/event-hubs/)頁面詳細說明如何許多連接會包含在每個服務層。

### <a name="how-is-event-hubs-capture-billed"></a>事件中樞擷取如何計費？
Hello 命名空間中的任何事件中樞已啟用的 hello 擷取選項時，會啟用擷取。 事件中樞擷取依據購買的輸送量單位每小時計費。 增加或減少 hello 輸送量單位計數時，事件中心擷取計費會反映這些變更整個小時為單位遞增。 如需事件中樞擷取計費的詳細資訊，請參閱[事件中樞定價資訊](https://azure.microsoft.com/pricing/details/event-hubs/)。

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>將我計費 hello 我選取擷取的事件中心的儲存體帳戶？
當在事件中樞上啟用擷取時，會使用您提供的儲存體帳戶。 因為這是您的儲存體帳戶時，會使用票據的 tooyour Azure 訂用帳戶此組態的任何變更。

## <a name="quotas"></a>配額

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>是否有任何與事件中樞相關聯的配額？
如需所有事件中樞配額的清單，請參閱[配額](event-hubs-quotas.md)。

## <a name="troubleshooting"></a>疑難排解

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>有哪些 hello 例外狀況產生的事件中樞與建議的動作？
如需可能的事件中樞例外狀況清單，請參閱[例外狀況概觀](event-hubs-messaging-exceptions.md)。

### <a name="diagnostic-logs"></a>診斷記錄檔
事件中心支援兩種[診斷記錄檔](event-hubs-diagnostic-logs.md)-擷取錯誤記錄檔和操作記錄檔-這兩種在 json 中表示，而且可以透過開啟 hello Azure 入口網站。

### <a name="support-and-sla"></a>支援與 SLA
事件中心的技術支援是透過 hello[社群論壇](https://social.msdn.microsoft.com/forums/azure/home)。 計費及訂用帳戶管理支援均為免費提供。

toolearn 深入了解我們的 SLA，請參閱 hello[服務等級協定](https://azure.microsoft.com/support/legal/sla/)頁面。

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
