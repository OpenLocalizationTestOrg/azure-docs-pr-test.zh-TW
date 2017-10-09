---
title: "aaaAzure 事件中心功能概觀 |Microsoft 文件"
description: "Azure 事件中樞功能的概觀和詳細資料"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>事件中樞功能概觀

事件中樞是可調整的事件處理服務，它會擷取和處理大量的事件和資料，具有低延遲和高可靠性。 請參閱[事件中心是什麼？](event-hubs-what-is-event-hubs.md)的 hello 服務的高階概觀。

這篇文章會根據在 hello hello 資訊[概觀](event-hubs-what-is-event-hubs.md)，並提供有關事件中心元件和功能的技術和實作詳細資料。

## <a name="event-publishers"></a>事件發佈者

傳送資料 tooan 事件中心是事件產生者的任何實體或*事件發行者*。 事件發佈者可以使用 HTTPS 或 AMQP 1.0 發佈事件。 事件發行者使用共用存取簽章 (SAS) 權杖的 tooidentify 本身 tooan 事件中樞，並可以有唯一的識別，或使用一般的 SAS 權杖。

### <a name="publishing-an-event"></a>發佈事件

您可以透過 AMQP 1.0 或 HTTPS 來發佈事件。 事件中心提供[用戶端程式庫和類別](event-hubs-dotnet-framework-api-overview.md)發行的.NET 用戶端事件 tooan 事件中樞。 對於其他執行階段和平台，您可以使用任何 AMQP 1.0 用戶端 (如 [Apache Qpid](http://qpid.apache.org/))。 您可以單獨發佈事件，或以批次方式進行。 不論是單一事件或批次，單次發行 (事件資料執行個體) 的上限為 256KB。 發佈大於此臨界值的事件會導致錯誤。 它是 「 發行者 」 toobe hello 事件中心內的資料分割感知的最佳作法，並指定 tooonly*資料分割索引鍵*（hello 下一節中引進），或其透過 SAS 權杖的身分識別。

hello 選擇 toouse AMQP 或 HTTPS 為 toohello 特定使用案例。 在加法 tootransport 層級安全性 (TLS) 或 SSL/TLS，AMQP 還需要 hello 建立持續性的雙向通訊端。 AMQP 時，有較高的網路成本初始化 hello 工作階段，不過 HTTPS 需要額外的 SSL 負荷的每個要求。 對於頻繁的發行者，AMQP 的效能較高。

![事件中樞](./media/event-hubs-features/partition_keys.png)

事件中心，可確保共用的資料分割索引鍵值的所有事件所都傳遞順序，以及 toohello 中相同資料分割。 如果發行者原則中使用資料分割索引鍵，然後 hello hello 發行者的身分識別和 hello hello 資料分割索引鍵的值必須符合。 否則便會發生錯誤。

### <a name="publisher-policy"></a>發佈者原則

事件中樞可讓您透過發佈者 原則更精確地控制事件發佈者。 發行者原則是專門設計的執行階段功能 toofacilitate 大量獨立事件發行者。 使用發行者原則，每個發行者使用它自己的唯一識別碼發佈事件 tooan 事件中心時使用下列機制 hello:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

您不需要事先，toocreate 發行者名稱，但它們必須符合 hello SAS 權杖發行事件時，在訂單 tooensure 獨立發行者的身分識別時使用。 當使用發行者原則，hello **PartitionKey**設定 toohello 發行者名稱的值。 toowork 正常運作，這些值必須相符。

## <a name="capture"></a>擷取

[事件中心擷取](event-hubs-capture-overview.md)可讓您 tooautomatically 擷取 hello 事件中心中的資料流，並將它儲存 tooyour 選擇 Blob 儲存體帳戶，或 Azure 資料湖服務帳戶。 您可以從 hello Azure 入口網站中啟用擷取，並指定最小值和時間視窗 tooperform hello 擷取。 使用擷取的事件中樞，您指定您自己的 Azure Blob 儲存體帳戶和容器，或 Azure 資料湖服務帳戶，也就是使用的 toostore hello 擷取的資料。 擷取的資料會寫入 hello Apache Avro 格式。

## <a name="partitions"></a>分割數

事件中心提供訊息串流透過分割式取用者模式中的每一個取用者只會讀取的特定子集或資料分割，hello 訊息資料流。 此模式能水平擴充事件處理規模，並提供佇列和主題缺少的其他串流導向功能。

資料分割是經過排序且保存在事件中樞內的事件序列。 較新的事件送達時，會加入此序列的 toohello 結尾。 您可以將資料分割視為一種「認可記錄」。

![事件中樞](./media/event-hubs-features/partition.png)

事件中樞會保留資料的 hello 事件中樞中的所有資料分割適用於已設定的保留時間。 事件會隨著時間經過而到期，因此您無法明確地予以刪除。 資料分割各自獨立，只包含其本身的資料序列，通常會以不同的速度成長。

![事件中樞](./media/event-hubs-features/multiple_partitions.png)

hello 資料分割數目指定在建立，而且必須介於 2 到 32 之間。 hello 資料分割計數就無法變更，，因此設定資料分割計數時，您應該考慮長期的小數位數。 資料分割是與取用應用程式所需 toohello 下游平行處理原則的資料組織機制。 hello 事件中心的資料分割數目直接關係 toohello 數目的並行讀取器中，您預期 toohave。 您可以增加 hello 32 以外的資料分割數目連絡 hello 事件中心小組。

雖然資料分割可以識別，而且可以傳送 toodirectly，不建議直接傳送 tooa 磁碟分割。 相反地，您可以使用較高的層級建構 hello 中導入[事件發行者](#event-publishers)和[容量](#capacity)區段。 

資料分割會填入一連串的事件資料，其中包含 hello 主體 hello 事件、 使用者定義的屬性包，以及中繼資料，例如它 hello 資料分割中的位移和 hello 串流序列中的編號。

如需有關資料分割和 hello 取捨可用性和可靠性的詳細資訊，請參閱 hello[事件中心程式設計指南](event-hubs-programming-guide.md#partition-key)和 hello[可用性和事件中心的一致性](event-hubs-availability-and-consistency.md)發行項.

### <a name="partition-key"></a>資料分割索引鍵

您可以使用[資料分割索引鍵](event-hubs-programming-guide.md#partition-key)toomap 內送事件資料至特定的資料分割的資料組織 hello 用途。 hello 資料分割索引鍵是寄件者提供的值傳遞至事件中心。 它會處理透過靜態雜湊函式，會建立 hello 資料分割指派。 如果您在發佈事件時未指定資料分割索引鍵，系統會使用循環配置資源指派。

hello 事件發行者只會知道其資料分割索引鍵，不 hello 分割 toowhich hello 事件發行。 此種減少方式的索引鍵和資料分割，以隔離就不需要太多有關 hello 下游處理 tooknow hello 寄件者。 每個裝置或使用者唯一識別適當的資料分割索引鍵，但是其他屬性，例如地理位置也可以使用的 toogroup 相關事件至單一資料分割。

## <a name="sas-tokens"></a>SAS 權杖

事件中心採用*共用存取簽章*，所提供在 hello 命名空間和事件中心層級。 SAS 權杖可自 SAS 金鑰產生，它是經過特定格式編碼的 URL SHA 雜湊。 使用 hello 名稱 hello 金鑰 （原則） 和 hello 語彙基元，事件中心可以重新產生 hello 雜湊，因此驗證 hello 寄件者。 一般而言，建立的事件發佈者 SAS 權杖只具備特定事件中樞的**傳送**權限。 此 SAS 權杖 URL 機制是 hello 發行者原則中介紹的發行者識別的 hello 基礎。 如需使用 SAS 的詳細資訊，請參閱[使用服務匯流排的共用存取簽章驗證](../service-bus-messaging/service-bus-sas.md)。

## <a name="event-consumers"></a>事件取用者

任何從事件中樞讀取事件資料的實體就稱為「事件取用者」。 透過 hello AMQP 1.0 工作階段的所有事件中心取用者都連接，並透過 hello 工作階段傳遞事件可用時。 hello 用戶端不需要 toopoll 資料可用性。

### <a name="consumer-groups"></a>用戶群組

事件中心的 hello 發佈/訂閱機制透過啟用*取用者群組*。 取用者群組是檢視整個事件中樞 (狀態、位置或位移) 的窗口。 取用者群組可讓多個取用應用程式 tooeach 擁有 hello 事件資料流，並依自己的步調獨立 tooread hello 資料流的不同檢視，和他們自己的位移。

在資料流處理架構，每一個下游應用程式等同 tooa 取用者群組。 如果您想 toowrite 事件資料 toolong 長期的儲存體，該儲存體寫入器應用程式是取用者群組。 複雜的事件處理可以由另一個獨立的取用者群組來執行。 您只能透過取用者群組來存取資料分割。 每一取用者群組的一個分割區上最多可以有 5 個並行讀取器；不過，**建議在每一取用者群組的一個分割區上只有一個作用中的接收器**。 事件中心，會有預設取用者群組，而且您可以建立標準層次事件中心 too20 取用者群組。

hello 如下 hello 取用者群組 URI 慣例的範例：

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

hello 下圖顯示 hello 事件中心資料流處理架構：

![事件中樞](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>串流位移

*位移*hello 位置上的磁碟分割內的事件。 您可以將位移視為用戶端指標。 hello 位移是一個位元組的 hello 事件編號。 此位移可讓事件取用者 （讀取器） toospecify 希望從中讀取事件 toobegin hello 事件資料流中的點。 您可以指定 hello 位移為時間戳記或位移值。 取用者負責儲存 hello 事件中心服務之外自己位移的值。 在資料分割內，每個事件都含有一個位移。

![事件中樞](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>檢查點

*設立檢查點* 是讀取器在資料分割事件序列中標記或認可其位置的程序。 檢查點檢查 hello 責任 hello 取用者與取用者群組內每個分割區為基礎，就會發生。 此的責任表示，每個取用者群組、 每個資料分割讀取器必須追蹤 hello 事件資料流，其目前位置，並將它視為 hello 資料流完成時，可以通知 hello 服務。

如果讀取器會中斷從資料分割，當它重新連線時開始讀取先前已提交 hello 最後一個讀取器該分割的取用者群組中的 hello 檢查點。 當 hello 讀取器連接時，它會傳遞這個位移的 toohello 事件中樞 toospecify hello 位置在哪一個 toostart 讀取。 如此一來，您可以使用檢查點 tooboth 事件標示為 「 完成 」，下游應用程式和 tooprovide 復原，如果在不同電腦上執行的讀取器之間的容錯移轉，就會發生。 它藉由指定較低的位移，從這個檢查點程序是可能 tooreturn tooolder 資料。 透過這項機制，檢查點可提供容錯移轉彈性，並支援事件串流重播。

### <a name="common-consumer-tasks"></a>常見的取用者工作

所有事件中樞取用者都會透過 AMQP 1.0 工作階段 (狀態感知的雙向通訊通道) 來連線。 每個資料分割有 AMQP 1.0 工作階段，可促進 hello 傳輸的資料分割所隔離的事件。

#### <a name="connect-tooa-partition"></a>連接 tooa 磁碟分割

連線時 toopartitions，它是常見的作法 toouse 租用機制 toocoordinate 讀取器連接 toospecific 資料分割。 如此一來，它可能會取用者群組 toohave 只能有一個作用中讀取器中的每個資料分割。 檢查點，租用及管理讀取器已經過簡化使用 hello [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) .NET 用戶端類別。 hello 事件處理器主機是智慧型取用者代理程式。

#### <a name="read-events"></a>讀取事件

特定資料分割開啟 AMQP 1.0 工作階段和連結後，事件會由 hello 事件中心服務傳遞 toohello AMQP 1.0 用戶端。 相較於以提取為基礎的機制 (如 HTTP GET)，這個傳遞機制能產生更高的輸送量和較低的延遲。 當事件傳送 toohello 用戶端，每個事件資料執行個體包含重要的中繼資料，例如所使用的 toofacilitate hello 事件序列上的檢查點的 hello 位移和序號數目。

事件資料︰
* Offset
* 序號
* 內文
* 使用者屬性
* 系統屬性

它是您的責任 toomanage hello 位移。

## <a name="capacity"></a>容量

事件中心具有高度可調整的平行架構，有數個關鍵因素 tooconsider 時調整大小和擴充。

### <a name="throughput-units"></a>輸送量單位

事件中心 hello 輸送量容量由*輸送量單位*。 輸送量單位是預先購買的容量單位。 單一輸送量單位包括 hello 下列容量：

* 每秒 （何者先） 的第二個或 1000年事件 too1 MB 總輸入：
* 向上 too2 MB，每秒輸出：

輸入已超出 hello 購買的輸送量單位的 hello 產能，節流和[ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)傳回。 輸出不會產生節流例外狀況，但仍會限制的 toohello 容量的 hello 購買的輸送量單位。 如果您收到發佈速率例外狀況或預期 toosee 較高的輸出，是確定 toocheck hello 命名空間已購買的輸送量單位數量。 您可以管理 hello 輸送量單位**標尺**刀鋒視窗中的 hello 命名空間中 hello [Azure 入口網站](https://portal.azure.com)。 您也可以管理輸送量單位以程式設計方式使用 hello[事件中心 Api](event-hubs-api-overview.md)。

輸送量單位是以每小時計費，採預先購買制。 一經購買，您至少必須支付一個小時的輸送量單位費用。 Too20 輸送量單位可以購買事件中樞命名空間和 hello 命名空間中所有事件中心都共用。

可以連絡 Azure 支援人員，20，too100 輸送量單位，向上的區塊中購買更多的輸送量單位。 之後，您還可以購買以 100 個輸送量為單位的區塊。

我們建議您衡量輸送量單位和資料分割 tooachieve 最佳規模。 每個資料分割有一個輸送量單位的規模上限。 hello 輸送量單元數目應該要小於或等於 toohello 事件中心中的資料分割數目。

如需詳細的事件中樞價格資訊，請參閱[事件中樞價格](https://azure.microsoft.com/pricing/details/event-hubs/)。

## <a name="next-steps"></a>後續步驟

如需有關事件中心的詳細資訊，請造訪下列連結查看 hello:

* 開始使用[事件中樞教學課程][Event Hubs tutorial]
* [事件中樞程式設計指南](event-hubs-programming-guide.md)
* [事件中樞的可用性和一致性](event-hubs-availability-and-consistency.md)
* [事件中樞常見問題集](event-hubs-faq.md)
* [事件中樞範例][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[事件中樞範例]: https://github.com/Azure/azure-event-hubs/tree/master/samples
