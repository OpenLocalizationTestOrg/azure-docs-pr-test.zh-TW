---
title: "aaaReliable 服務架構 |Microsoft 文件"
description: "可設定狀態，而且無狀態服務的 hello 可靠的服務架構的概觀"
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
ms.openlocfilehash: d2d0ec9600275ae248ab7717be269cc7204a1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="architecture-for-stateful-and-stateless-reliable-services"></a>具狀態與無狀態 Reliable Services 的架構
Azure Service Fabric 可靠服務可能是具狀態或無狀態。 每一種服務都在特定架構內執行。 本文將會說明這些架構。
請參閱 hello[可靠的服務概觀](service-fabric-reliable-services-introduction.md)如需有關 hello 可設定狀態，而且無狀態服務之間的差異。

## <a name="stateful-reliable-services"></a>具狀態可靠的服務
### <a name="architecture-of-a-stateful-service"></a>具狀態服務的架構
![具狀態服務的架構圖](./media/service-fabric-reliable-services-platform-architecture/reliable-stateful-service-architecture.png)

### <a name="stateful-reliable-service"></a>具狀態可靠的服務
可設定狀態 Reliable Service 可以衍生自 hello StatefulService 或 StatefulServiceBase 類別。 這兩個基底類別都由 Service Fabric 所提供。 提供了各種層級支援與 hello 具狀態服務 toointerface Service Fabric-與 tooparticipate hello Service Fabric 叢集內的服務為抽象。

StatefulService 衍生自 StatefulServiceBase。 StatefulServiceBase 提供服務更多的彈性，但需要更多的了解 hello 內部的 Service Fabric。
請參閱 hello[可靠的服務概觀](service-fabric-reliable-services-introduction.md)和[可靠的服務的進階用法](service-fabric-reliable-services-advanced-usage.md)如需使用 hello StatefulService 和 StatefulServiceBase 類別撰寫服務的 hello 細節.

這兩個基底類別會管理 hello 存留期和 hello 服務實作的角色。 hello 服務實作可能會覆寫虛擬方法的其中一個基底類別，或如果 hello 服務實作這些要點牢記在 hello 服務實作的生命週期--在有工作 toodo 想 toocreate 通訊接聽程式物件。 請注意，雖然服務實作可能會實作公開 ICommunicationListener，hello 圖，在自己的通訊接聽程式物件 hello 通訊接聽程式實作透過 Service Fabric-hello 服務實作會使用由服務網狀架構所實作的通訊接聽程式。

可設定狀態 Reliable Service 會使用 hello 穩定的狀態，請管理員 tootake 利用可靠的集合。 可靠的集合是本機資料結構，其中是高可用性 toohello 服務--也就是說，它們永遠都可以使用，不論服務容錯移轉。 可靠的集合的每個類型是由可靠的狀態提供者所實作。
如需有關可靠集合的詳細資訊，請參閱 hello[可靠集合概觀](service-fabric-reliable-services-reliable-collections.md)。

### <a name="reliable-state-manager-and-state-providers"></a>可靠的狀態管理員和狀態提供者
管理可靠狀態提供者的 hello 物件 hello 穩定的狀態管理員。 它有 hello 功能 toocreate、 刪除、 列舉，並確定 hello 可靠狀態提供者持續性、 高可用性。 可靠的狀態提供者執行個體代表持續保存且高度可用之資料結構的執行個體，例如字典或佇列。

每一個穩定的狀態提供者會公開可由具狀態服務 toointeract 與 hello 穩定的狀態提供者的介面。 比方說，IReliableDictionary 時，使用與 hello 可靠的字典，toointerface IReliableQueue 是使用的 toointerface 與 hello 可靠的佇列。 所有的穩定的狀態提供者實作 hello IReliableState 介面。

hello 穩定的狀態管理員具有名為 IReliableStateManager，允許存取 tooit 從具狀態服務的介面。 透過 IReliableStateManager 傳回介面 tooreliable 狀態提供者。

hello 可靠狀態管理員會使用外掛程式的架構，讓新類型的可靠的集合可以插入動態。

hello 可靠字典和可靠的佇列是建置在 hello 實作的高效能、 版本設定的差異存放區中。

### <a name="transactional-replicator"></a>交易式複寫器
hello 異動複寫器元件會負責確保 hello 狀態 （也就是 hello 可靠狀態管理員和 hello 可靠集合中的 hello 狀態） 的服務在執行 hello 服務的所有複本上一致的。 它也可確保 hello 狀態會保存在 hello 記錄檔中。 hello 與 hello 異動複寫器透過私人機制穩定的狀態管理員介面。

hello 異動複寫器使用網路通訊協定 toocommunicate 狀態與 hello 服務執行個體的其他複本，使所有複本都有最新狀態資訊。

hello 異動複寫器使用 toopersist 狀態資訊的記錄檔，讓 hello 狀態資訊便會存在著處理程序，或節點當機。 hello 介面 toohello 記錄是透過私用的機制。

### <a name="log"></a>記錄檔
hello 記錄元件提供高效能的持續性存放區，可以針對寫入 toospinning 或固態硬碟進行最佳化。  hello hello 記錄檔的設計是 hello 永續性儲存體 （也就是硬碟） toobe 本機 toohello 節點執行 hello 可設定狀態的服務。 這樣低的延遲和高輸送量，做為比較的 tooremote 永續性儲存體，這不是本機 toohello 節點。

hello 記錄元件會使用多個記錄檔。 沒有節點全共用的記錄檔，讓它可以提供 hello 最低延遲和最高輸送量的儲存狀態資料做為所有複本。 根據預設，hello 共用記錄檔會置於 hello Service Fabric 節點工作目錄，但也可能是設定的 toobe 放在另一個位置，最好是在 hello 共用記錄的保留磁碟上。 每個複本 hello 服務也會有專用的記錄檔和 hello 專用的記錄檔會放置在 hello 服務的工作目錄。 放在不同的位置沒有機制 tooconfigure hello 專用記錄 toobe。

hello 共用的記錄為 hello 複本的狀態資訊的過渡期區域，hello 專用的記錄檔之後再保存 hello 最終目的地。 在這個設計中，hello 狀態資訊是第一個寫入的 toohello 共用的記錄檔，然後再執行延遲移 hello 背景 toohello 專用的記錄檔。 如此一來，hello 寫入 toohello 共用記錄檔中會有 hello 最低延遲和高的輸送量更快讓 hello 服務 toomake 進度。

讀取和寫入 toohello 共用記錄檔會透過直接 IO toopreallocated 空間 hello hello 共用記錄檔的磁碟上完成。 tooallow hello 專用的記錄檔的磁碟機上的磁碟空間使用最佳的 hello 專用的記錄檔會建立為 NTFS 的疏鬆檔案。 請注意，這可讓過度佈建的磁碟空間 hello OS 將會顯示 hello 專用使用更多磁碟空間超過實際使用的記錄檔。

除了基本使用者模式的介面 toohello 記錄檔 hello 記錄會寫入成為核心模式驅動程式。 核心模式驅動程式的身分執行，hello 記錄可藉由提供 hello 最高的效能 tooall 服務使用它。

如需設定 hello 記錄檔的詳細資訊，請參閱[設定可設定狀態的可靠服務](service-fabric-reliable-services-configuration.md)。

## <a name="stateless-reliable-service"></a>無狀態的可靠的服務
### <a name="architecture-of-a-stateless-service"></a>無狀態服務的架構
![無狀態服務的架構圖](./media/service-fabric-reliable-services-platform-architecture/reliable-stateless-service-architecture.png)

### <a name="stateless-reliable-service"></a>無狀態的可靠的服務
無狀態服務實作衍生自 hello StatelessService 或 StatelessServiceBase 類別。 hello StatelessServiceBase 類別可讓更多的彈性比 hello StatelessService 類別。
這兩個基底類別會管理 hello 存留期和服務的角色。

如果 hello 服務工作 toodo hello 服務生命週期--在這些時間點，或者它想 toocreate 通訊接聽程式物件，hello 服務實作可能會覆寫虛擬方法的其中一個基底類別。 請注意，雖然 hello 服務可能會實作公開 ICommunicationListener，hello 圖，在自己的通訊接聽程式物件 hello 通訊接聽程式會實作由服務網狀架構，因為該服務實作會使用通訊服務網狀架構所實作的接聽程式。

請參閱 hello[可靠的服務概觀](service-fabric-reliable-services-introduction.md)和[可靠的服務的進階用法](service-fabric-reliable-services-advanced-usage.md)如需撰寫使用 hello StatelessService 和 StatelessServiceBase 類別服務的 hello 細節.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
如需 Service Fabric 的詳細資訊，請參閱：

[可靠的服務概觀](service-fabric-reliable-services-introduction.md)

[快速入門](service-fabric-reliable-services-quick-start.md)

[可靠的集合概觀](service-fabric-reliable-services-reliable-collections.md)

[可靠的服務的進階用法](service-fabric-reliable-services-advanced-usage.md)

[可靠的服務組態](service-fabric-reliable-services-configuration.md)  

