---
title: "在 Azure Service Fabric 可設定狀態服務 aaaIntroduction tooReliable 集合 |Microsoft 文件"
description: "Service Fabric 可設定狀態服務可提供可靠的集合，可讓您 toowrite 高可用、 可擴充且低度延遲的雲端應用程式。"
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
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a>在 Azure Service Fabric 可設定狀態服務簡介 tooReliable 集合
可靠的集合可讓您 toowrite 高可用、 可擴充且低度延遲的雲端應用程式就好像您在撰寫單一電腦的應用程式。 hello 中 hello 類別**Microsoft.ServiceFabric.Data.Collections**命名空間提供一組自動讓您的狀態具有高可用性的集合。 開發人員需要 tooprogram 只有 toohello 可靠集合的應用程式開發介面，並讓可靠管理複寫的 hello 和本機狀態的集合。

hello 可靠的集合和其他高可用性的技術 （例如 Redis、 Azure 資料表服務和 Azure 佇列服務） 之間的主要差異是，hello 狀態就會保留在本機在 hello 服務執行個體時也要成為高可用性。 這表示：

* 所有讀取都在本機，可保障低延遲及高輸送量讀取。
* 所有寫入都造成 hello 最小網路 Io 數目，會導致低度延遲及高輸送量寫入。

![集合的演化圖。](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

可靠的集合可以視為 hello 自然演進而來的 hello **System.Collections**類別： 一組新的集合，而不會增加複雜度 hello 雲端和多部電腦的應用程式所設計hello 開發人員。 因此，可靠的集合是：

* 可複寫：進行狀態變更複寫以確保高可用性。
* 保存： 資料會保存的 toodisk 為持久性免於大規模中斷 （例如，資料中心停電）。
* 非同步： 應用程式開發介面會非同步 tooensure 產生 IO 時不會封鎖執行緒。
* 因此您可以輕鬆地管理多個可靠的集合，在服務中異動： 應用程式開發介面利用 hello 抽象的交易。

可靠的集合會提供強式一致性可確保超出 hello 方塊 toomake 思考更輕鬆的應用程式狀態。
強式一致性是由確保的交易的認可完成 hello 整筆交易有登入的複本，包括 hello 主要多數仲裁之後，才完成。
tooachieve 較弱的一致性，應用程式可以了解後 toohello 用戶端要求者 hello 非同步認可傳回之前。

hello 可靠集合 Api 是發展的並行集合應用程式開發介面 (位於 hello **System.Collections.Concurrent**命名空間):

* 因為不同於並行的集合，複寫和保存 hello operations 非同步： 傳回的工作。
* 沒有 out 參數： 使用`ConditionalValue<T>`tooreturn bool 和而不是 out 參數的值。 `ConditionalValue<T>`就像`Nullable<T>`，但不需要 T toobe 結構。
* 交易： 在交易中的多個可靠集合上使用交易物件 tooenable hello 使用者 toogroup 動作。

現在，Microsoft.ServiceFabric.Data.Collections 包含三個集合：

* [可靠的字典](https://msdn.microsoft.com/library/azure/dn971511.aspx)：表示可複寫、交易式和非同步索引鍵/值組的集合。 類似太**ConcurrentDictionary**、 兩者 hello 索引鍵和 hello 值可以是任何類型。
* [可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)：表示可複寫、交易式和非同步的嚴格先進先出 (FIFO) 佇列。 類似太**ConcurrentQueue**，hello 值可以是任何類型。
* [可靠的並行佇列](service-fabric-reliable-services-reliable-concurrent-queue.md)︰代表儘可能最佳的複寫、交易與非同步排序序列，以達到高輸送量。 類似 toohello **ConcurrentQueue**，hello 值可以是任何類型。

## <a name="next-steps"></a>後續步驟
* [Reliable Collection 指導方針與建議](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [使用 Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [交易和鎖定](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [Reliable State Manager 與 Collection 內部](service-fabric-reliable-services-reliable-collections-internals.md)
* 管理資料
  * [備份與還原](service-fabric-reliable-services-backup-restore.md)
  * [Notifications](service-fabric-reliable-services-notifications.md)
  * [可靠的集合序列化](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [序列化與升級](service-fabric-application-upgrade-data-serialization.md)
  * [Reliable State Manager 組態](service-fabric-reliable-services-configuration.md)
* 其他
  * [Reliable Services 快速入門](service-fabric-reliable-services-quick-start.md)
  * [可靠的集合的開發人員參考資料](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
