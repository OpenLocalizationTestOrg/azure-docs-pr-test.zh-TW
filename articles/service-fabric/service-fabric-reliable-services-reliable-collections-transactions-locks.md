---
title: "aaaTransactions 和 Azure Service Fabric 可靠集合中的鎖定模式 |Microsoft 文件"
description: "Azure Service Fabric Reliable State Manager 和 Reliable Collections 交易和鎖定。"
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
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a>Azure Service Fabric Reliable Collections 中的交易和鎖定模式

## <a name="transaction"></a>交易
交易就是以單一工作邏輯單元執行的一連串作業。
交易必須呈現出 hello 下列 ACID 屬性。 (請參閱：https://technet.microsoft.com/en-us/library/ms190612)
* **不可部分完成性**︰交易必須是不可部分完成的工作單位。 換句話說，執行其所有資料修改，或完全不執行。
* **一致性**︰交易完成時，所有資料必須維持一致的狀態。 所有的內部資料結構必須正確 hello hello 交易的結尾處。
* **隔離**： 並行的交易所做的修改都必須與其他並行的交易所做的 hello 修改。 hello IReliableState 執行 hello 作業取決於用於作業中 itransaction:: hello 隔離等級。
* **持久性**: 交易已完成之後，其作用便永遠就地 hello 系統中。 hello 修改依然會保存即使在系統失敗的 hello 事件。

### <a name="isolation-levels"></a>隔離層級
隔離等級定義 hello 程度 toowhich hello 交易必須是與其他交易所做的修改隔離。
可靠的集合支援兩種隔離等級：

* **可重複讀取**： 指定陳述式不能讀取已修改但尚未認可的其他交易的資料和任何其他交易可以修改已讀取的 hello 目前交易中，直到 hello 目前的資料交易完成。 如需詳細資訊，請參閱 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。
* **快照集**： 指定在交易中任何陳述式所讀取的資料是 hello hello hello 交易開始時就存在的 hello 資料交易一致性版本。
  hello 交易可以辨識 hello hello 交易開始之前所認可的資料修改。
  Hello 開頭 hello 目前交易之後，其他交易所進行的資料修改將不會顯示 toostatements hello 目前交易中執行。
  hello 效果是在交易中的 hello 陳述式會取得 hello 認可資料的快照集，存在於 hello hello 交易開始。
  可靠的集合的快照集都是一致的。
  如需詳細資訊，請參閱 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。

可靠的集合會自動選擇 hello 隔離層級 toouse 交易的建立 hello 時根據 hello 作業和 hello hello 複本角色指定讀取作業。
以下是 hello 資料表，顯示隔離層級預設值為佇列和可靠的字典的作業。

| 作業 \ 角色 | 主要 | 次要 |
| --- |:--- |:--- |
| 單一實體讀取 |可重複讀取 |快照 |
| 列舉、計數 |快照 |快照 |

> [!NOTE]
> 單一實體作業的常見範例包括 `IReliableDictionary.TryGetValueAsync`、`IReliableQueue.TryPeekAsync`。
> 

Hello 可靠字典和 hello 可靠的佇列支援讀取程式寫入。
換句話說，任何寫入交易內，就會看見 tooa 下列讀取的所屬 toohello 相同的交易。

## <a name="locks"></a>鎖定
可靠的集合中使用嚴格的所有交易實作兩都階段鎖定： 交易不會釋放它所取得 hello 交易終止因中止或認可為止的 hello 鎖定。

可靠的字典會針對所有單一實體作業使用資料列層級鎖定。
可靠的佇列則會針對嚴格交易的 FIFO 屬性交換並行。
可靠的佇列會使用作業層級的鎖定，允許一次有 `TryPeekAsync` 和/或 `TryDequeueAsync` 的一個交易，以及有 `EnqueueAsync` 的一個交易。
請注意該 toopreserve FIFO，如果`TryPeekAsync`或`TryDequeueAsync`曾經觀察的 hello 可靠的佇列是空的它們也會鎖定`EnqueueAsync`。

寫入作業一律會採取「獨佔」鎖定。
對於讀取作業，hello 鎖定取決於一些因素。
任何使用快照隔離所完成的讀取作業都是無鎖定的。
任何可重複讀取作業預設都會採用共用鎖定。
不過，支援可重複讀取的任何讀取作業，如 hello 使用者可以要求的更新鎖定，而不是 hello 共用鎖定。
更新鎖定是死結的對稱的鎖定使用 tooprevent 常見的多個交易鎖定資源並在稍後更新時所發生形式。

hello 下表中可以找到 hello 鎖定相容性矩陣：

| 要求 \ 授與 | None | 共用 | 更新 | 獨佔 |
| --- |:--- |:--- |:--- |:--- |
| 共用 |無衝突 |無衝突 |衝突 |衝突 |
| 更新 |無衝突 |無衝突 |衝突 |衝突 |
| 獨佔 |無衝突 |衝突 |衝突 |衝突 |

Hello 可靠集合的應用程式開發介面中的逾時引數用於死結偵測。
例如，兩筆交易 （T1 和 T2） 嘗試 tooread，並更新 K1。
它有可能 toodeadlock，因為它們都得到擁有 hello 共用鎖定。
在此情況下，其中之一或兩者的 hello 作業會逾時。

此死結案例就是更新鎖定可如何防止死結的絕佳範例。

## <a name="next-steps"></a>後續步驟
* [使用可靠的集合](service-fabric-work-with-reliable-collections.md)
* [Reliable Services 通知](service-fabric-reliable-services-notifications.md)
* [備份與還原 Reliable Services (災害復原)](service-fabric-reliable-services-backup-restore.md)
* [Reliable State Manager 組態](service-fabric-reliable-services-configuration.md)
* [可靠的集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

