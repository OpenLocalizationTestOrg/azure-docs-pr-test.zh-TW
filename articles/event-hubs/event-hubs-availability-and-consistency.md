---
title: "aaaAvailability 和 Azure 事件中心的一致性 |Microsoft 文件"
description: "Tooprovide hello 最大數量可用性以及與 Azure 事件中心使用一致的分割區。"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>事件中樞的可用性和一致性

## <a name="overview"></a>概觀
Azure 事件中心採用[分割模型](event-hubs-features.md#partitions)tooimprove 可用性和平行處理單一事件中心內。 例如，如果事件中心有四個資料分割，而且這些資料分割的其中一個會從負載平衡作業中的一部伺服器 tooanother 移，您仍可以傳送及接收來自其他三個資料分割。 此外，讓多個資料分割可讓您 toohave 更多的並行讀取器處理您的資料，改善您的彙總輸送量。 了解的資料分割和排序分散式系統中的 hello 含意是解決方案設計的重要層面。

toohelp 說明 hello 排序與可用性之間的取捨，請參閱 hello [CAP 理論](https://en.wikipedia.org/wiki/CAP_theorem)，也稱為 Brewer 的理論。 此理論討論之間的一致性、 可用性和資料分割容錯的 hello 選擇。

Brewer 的理論會定義一致性和可用性，如下所示：
* 分割容錯： hello 處理資料，即使在磁碟分割失敗，就會發生資料處理系統 toocontinue 的能力。
* 可用性：非失敗節點會在合理的時間 (不含錯誤或逾時) 內傳回合理的回應。
* ： 讀取保證一致性 tooreturn hello 最新的寫入給定的用戶端。

## <a name="partition-tolerance"></a>分割區容錯
「事件中樞」是建置在已分割的資料模型上。 您可以在安裝期間，在事件中樞設定 hello 資料分割數目，但是您之後無法變更此值。 由於您必須使用事件中心使用資料分割，您將 toomake 決策，以可用性和一致性應用程式。

## <a name="availability"></a>Availability
hello 最簡單的方式 tooget 入門事件中心是 toouse hello 預設行為。 如果您建立新`EventHubClient`物件，並使用 hello`Send`方法，您的事件會自動發佈事件中樞中的資料分割之間。 此行為可讓您 hello 最大的時間。

需要 hello 最大執行時間的使用案例，此模型是慣用的。

## <a name="consistency"></a>一致性
在某些情況下，hello 的事件排序可能很重要。 例如，您可以您的後端系統 tooprocess update 命令之前刪除命令。 在本例中，您可以在事件上設定 hello 資料分割索引鍵，或使用`PartitionSender`物件 tooonly 傳送事件 tooa 特定資料分割。 這樣可以確保，當這些事件會讀取來自 hello 磁碟分割，它們會讀取順序。

此設定，請注意，如果您要傳送的 hello 特定資料分割 toowhich 無法使用時，您會收到錯誤回應。 為的比較點，如果您不需要同質 tooa 單一資料分割，hello 事件中心服務會傳送您事件 toohello 下一個可用的磁碟分割。

一個可能的解決方案 tooensure 排序，同時也執行時間，盡量將 tooaggregate 事件做為您的事件處理應用程式的一部分。 這個 hello 最簡單的方式 tooaccomplish 是 toostamp 自訂的序號屬性與事件。 下列程式碼的 hello 顯示範例：

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

這個範例事件中樞，以傳送您的事件 tooone hello 可用的資料分割，並從您的應用程式設定 hello 對應序號。 此解決方案需要狀態 toobe 保持為您處理的應用程式，但可讓您的寄件者比較可能 toobe 可用的端點。

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞服務概觀](event-hubs-what-is-event-hubs.md)
* [建立事件中樞](event-hubs-create.md)
