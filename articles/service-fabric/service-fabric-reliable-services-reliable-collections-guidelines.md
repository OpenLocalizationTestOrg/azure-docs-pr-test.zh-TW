---
title: "aaaGuidelines （& s) 中 Azure Service Fabric 可靠集合的建議 |Microsoft 文件"
description: "使用 Service Fabric Reliable Collection 的指導方針與建議"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a>Azure Service Fabric 中 Reliable Collection 的指導方針與建議
本節提供使用 Reliable State Manager 和 Reliable Collection 的指導方針。 hello 目標是避免常犯的錯誤 toohelp 使用者。

hello 指導方針會組織成簡單的建議前置詞與 hello 詞彙*不要*，*考慮*，*避免*和*不*。

* 請不要修改讀取作業所傳回自訂類型的物件 (例如 `TryPeekAsync` 或 `TryGetValueAsync`)。 可靠的集合，就像並行的集合，傳回參考 toohello 物件並不是複本。
* 不要再修改它傳回的自訂型別物件的深層複本 hello。 由於結構和內建型別是由值傳遞，您不需要 toodo 在其上的深層複本。
* 請不要針對逾時使用 `TimeSpan.MaxValue` 。 逾時應該使用的 toodetect 死結。
* 在認可、中止或處置交易之後，請勿使用該交易。
* 不要 hello 其所建立的交易範圍外使用列舉型別。
* 請不要在另一個交易的 `using` 陳述式內建立交易，因為它會造成死結。
* 務必確保 `IComparable<TKey>` 實作是正確的。 hello 系統，不需要相依性`IComparable<TKey>`合併檢查點和資料列。
* 讀取意圖 tooupdate 的項目時，請勿使用更新鎖定它 tooprevent 特定類別的死結。
* 請考慮您的項目 （例如，TKey + 可靠字典 Tvalue>） 80 Kb 以下： 更好的較小 hello。 這會減少 hello 大型物件堆積使用量，以及磁碟和網路 IO 要求的數量。 通常，它可減少時只有一小部份 hello 值正在更新複寫重複的資料。 常見的方式 tooachieve 可靠字典中，這是第 toobreak 中的資料列 toomultiple 資料列。
* 請考慮使用備份和還原功能 toohave 災害復原。
* 避免混用單一實體的作業和多實體作業 (例如`GetCountAsync`， `CreateEnumerableAsync`) hello 中相同的交易，因為 toohello 不同隔離等級。
* 請務必處理 InvalidOperationException。 可以由各種原因而 hello 系統中止使用者交易。 比方說，當 hello 可靠狀態管理員已變更其主要角色或是長時間執行交易封鎖 hello 交易記錄截斷。 在這種情況下，使用者可能會收到 InvalidOperationException，指出他們的交易已終止。 假設，hello hello 交易終止並不會要求使用者 hello，最佳的方式 toohandle 這個例外狀況是 toodispose hello 交易，檢查是否已收到信號 hello 取消語彙基元 （或 hello hello 複本角色已變更），如果不建立新的交易並重試。  

以下是一些事情 tookeep 記住：

* hello 預設逾時值為四個秒所有 hello 可靠集合的應用程式開發介面。 大部分使用者應該使用 hello 預設逾時。
* hello 預設取消語彙基元是`CancellationToken.None`可靠 api 的集合。
* hello 索引鍵的型別參數 (*TKey*) 必須正確實作可靠的字典`GetHashCode()`和`Equals()`。 索引鍵必須是不可變的。
* tooachieve hello 可靠集合的高可用性，每個服務應該有至少一個目標和最小複本集大小為 3。
* 次要的 hello 的 「 讀取 」 操作可讀取不是仲裁認可的版本。
  這表示從單一次要複本讀取的資料版本進度可能有誤。
  從主要複本讀取一定最穩定︰進度一定不會有誤。

### <a name="next-steps"></a>後續步驟
* [使用 Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [交易和鎖定](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Reliable State Manager 與 Collection 內部](service-fabric-reliable-services-reliable-collections-internals.md)
* 管理資料
  * [備份與還原](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [序列化與升級](service-fabric-application-upgrade-data-serialization.md)
  * [Reliable State Manager 組態](service-fabric-reliable-services-configuration.md)
* 其他
  * [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
  * [可靠的集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
