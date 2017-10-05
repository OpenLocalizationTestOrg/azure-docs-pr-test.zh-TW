---
title: "Reliable Services 架構 | Microsoft Docs"
description: "具狀態與無狀態之 Reliable Services 架構概觀"
services: service-fabric
documentationcenter: .net
author: AlanWarwick
manager: timlt
editor: vturecek
ms.assetid: af002ae6-7f6d-4769-b049-82aa1ba0891b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/30/2016
ms.author: alanwar
redirect_url: /azure/service-fabric/service-fabric-reliable-services-introduction
ms.openlocfilehash: a00a16945356b9731485554e06df46528b5c7bb2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>具狀態與無狀態 Reliable Services 的架構
Azure Service Fabric 可靠服務可能是具狀態或無狀態。 每一種服務都在特定架構內執行。 本文將會說明這些架構。
請參閱 [Reliable Services 概觀](service-fabric-reliable-services-introduction.md) ，以取得具狀態與無狀態服務之間差異的詳細資訊。

## <a name="stateful-reliable-services"></a>具狀態可靠的服務
### <a name="architecture-of-a-stateful-service"></a>具狀態服務的架構
![具狀態服務的架構圖](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>具狀態可靠的服務
具狀態可靠的服務可以從 StatefulService 或 StatefulServiceBase 類別衍生。 這兩個基底類別都由 Service Fabric 所提供。 這兩個基底類別可為具狀態服務提供各種支援和抽象層級以便與 Service Fabric 互動，以及做為 Service Fabric 叢集內的服務參與。

StatefulService 衍生自 StatefulServiceBase。 StatefulServiceBase 提供服務更多的彈性，但需要對 Service Fabric 內部運作有更多了解。
請參閱 [Reliable Services 概觀](service-fabric-reliable-services-introduction.md)和 [Reliable Services 進階用法](service-fabric-reliable-services-advanced-usage.md)，以取得使用 StatefulService 和 StatefulServiceBase 類別撰寫服務細節的詳細資訊。

這兩個基底類別會管理服務實作的存留期和角色。 如果服務實作在服務實作生命週期中的那些點有工作要執行，或是想要建立通訊接聽程式物件，服務實作可能會覆寫任一基底類別的虛擬方法。 請注意雖然服務實作可能會實作自己的通訊接聽程式物件並公開 ICommunicationListener，在上圖中，通訊接聽程式由 Service Fabric 實作，因為服務實作使用 Service Fabric 所實作的通訊接聽程式。

具狀態可靠的服務會使用可靠的狀態管理員來利用可靠的集合。 可靠的集合是對服務而言高度可用的本機資料結構，也就是，不論服務容錯移轉，一律可以使用。 可靠的集合的每個類型是由可靠的狀態提供者所實作。
如需可靠的集合的詳細資訊，請參閱 [可靠的集合概觀](service-fabric-reliable-services-reliable-collections.md)

### <a name="reliable-state-manager-and-state-providers"></a>可靠的狀態管理員和狀態提供者
可靠的狀態管理員是用以管理可靠的狀態提供者的物件。 它具有建立、刪除、列舉和確保可靠的狀態提供者持續保存且高度可用的功能。 可靠的狀態提供者執行個體代表持續保存且高度可用之資料結構的執行個體，例如字典或佇列。

每個可靠的狀態提供者會公開具狀態服務所使用的介面，以和可靠的狀態提供者互動。 例如，IReliableDictionary 用來與可靠的字典互動，而 IReliableQueue 用來與可靠的佇列互動。 所有可靠的狀態提供者都實作 IReliableState 介面。

可靠的狀態管理員具有名為 IReliableStateManager 的介面，其可讓您從具狀態服務進行存取。 與可靠的狀態提供者的介面會透過 IReliableStateManager 傳回。

可靠的狀態管理員使用外掛程式架構，因此新類型的可靠的集合可以動態地插入。

可靠的字典和可靠的佇列是建立在高效能版本的差異存放區實作上。

### <a name="transactional-replicator"></a>交易式複寫器
交易式複寫器元件負責確保服務的狀態 (也就是可靠狀態管理員和可靠集合的狀態)，在執行服務的所有複本之間都一致。 也可確保狀態保存在記錄檔中。 可靠狀態管理員透過私用機制與交易式複寫器互動。

交易式複寫器使用網路通訊協定來與服務執行個體的其他複本溝通狀態，如此所有複本都有最新的狀態資訊。

交易式複寫器使用記錄來保存狀態資訊，因此狀態資訊可以保存經歷處理序或節點當機。 記錄檔的介面是透過私用機制。

### <a name="log"></a>記錄檔
記錄元件提供高效能的持續性存放區，它可以針對寫入旋轉或固態磁碟而最佳化。  記錄檔的設計是讓持續性儲存體 (亦即硬碟) 能在執行具狀態服務的節點本機。 如此即可達到低延遲及高輸送量 (相較於非節點本機的遠端持續性儲存體)。

記錄元件會使用多個記錄檔。 有一個所有複本都會使用的全節點共用記錄檔，因為它可在儲存狀態資料時提供最低的延遲與最高的輸送量。 依預設，共用記錄檔放在 Service Fabric 節點工作目錄中，但它也可以設定為放在另一個位置上，最好是放在僅保留給共用記錄檔的磁碟上。 服務的每個複本也有專用記錄檔，而且專用記錄檔放在服務的工作目錄內。 沒有任何機制，可用來將專用記錄檔設定為放在不同的位置上。

共用記錄檔是複本狀態資訊的過渡區域，而專用記錄檔則是其保存所在位置的最終目的地。 在這種設計中，狀態資訊會先寫入共用記錄檔，然後在背景中延遲地移到專用記錄檔。 如此，對共用記錄檔的寫入延遲會最小且輸送量會最高，因而允許服務進度更快速。

完成讀取和寫入共用記錄檔的方式為直接 IO 至磁碟上預先配置給共用記錄檔的空間。 為了讓專用記錄檔能以最有效方式使用磁碟機上的磁碟空間，專用記錄檔會建立為 NTFS 疏鬆檔案。 請注意，這將允許過度佈建磁碟空間，因此 OS 將會使用遠超過實際使用的磁碟空間顯示專用記錄檔。

除了對記錄檔的最小使用者模式介面，記錄檔會撰寫為核心模式驅動程式。 藉由以核心模式驅動程式方式執行，記錄檔可以提供最高的效能給使用它的所有服務。

如需設定記錄的詳細資訊，請參閱 [設定具狀態的 Reliable Services](service-fabric-reliable-services-configuration.md)。

## <a name="stateless-reliable-service"></a>無狀態的可靠的服務
### <a name="architecture-of-a-stateless-service"></a>無狀態服務的架構
![無狀態服務的架構圖](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>無狀態的可靠的服務
無狀態服務實作衍生自 StatelessService 類別或 StatelessServiceBase 類別。 StatelessServiceBase 類別比 StatelessService 允許更多彈性。
這兩個基底類別會管理服務的存留期和角色。

如果服務在服務生命週期中的那些點有工作要執行，或是想要建立通訊接聽程式物件，服務實作可能會覆寫任一基底類別的虛擬方法。 請注意雖然服務可能會實作自己的通訊接聽程式物件並公開 ICommunicationListener，在上圖中，通訊接聽程式由 Service Fabric 實作，因為服務實作使用 Service Fabric 所實作的通訊接聽程式。

請參閱 [Reliable Services 概觀](service-fabric-reliable-services-introduction.md)和 [Reliable Services 進階用法](service-fabric-reliable-services-advanced-usage.md)，以取得使用 StatelessService 和 StatelessServiceBase 類別撰寫服務細節的詳細資訊。

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>後續步驟
如需 Service Fabric 的詳細資訊，請參閱：

[可靠的服務概觀](service-fabric-reliable-services-introduction.md)

[快速入門](service-fabric-reliable-services-quick-start.md)

[可靠的集合概觀](service-fabric-reliable-services-reliable-collections.md)

[可靠的服務的進階用法](service-fabric-reliable-services-advanced-usage.md)

[可靠的服務組態](service-fabric-reliable-services-configuration.md)  

