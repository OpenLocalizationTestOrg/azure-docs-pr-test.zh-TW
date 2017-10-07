---
title: "aaaApplication 案例及設計 |Microsoft 文件"
description: "Service Fabric 中雲端應用程式類別概觀。 討論使用具狀態和無狀態服務的應用程式設計。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Service Fabric 應用程式案例
Azure Service Fabric 提供可靠及有彈性的平台，可讓您 toowrite，並執行許多類型的商務應用程式和服務。 這些應用程式和 microservices 可以是無狀態或狀態，而這些資源平衡跨虛擬機器 toomaximize 效率。 服務網狀架構的 hello 獨特的架構可讓您 tooperform 近乎即時資料分析、 記憶體中計算、 平行交易，並在應用程式中處理的事件。 您可以輕鬆地根據變更的資源需求上下調整 (其實是收發) 您的應用程式。

在 Azure 中的 hello Service Fabric 平台適合 hello 下列種類的應用程式：

* **高可用性的服務**：Service Fabric 服務藉由建立多個次要服務複本，提供快速的容錯移轉。 如果節點、 處理序或個別的服務關閉 toohardware 或其他失敗的原因，其中一個 hello 次要複本不升級的 tooa 最少的服務遺失的主要複本。
* **可延展服務**： 個別的服務可以分割，以便狀態 toobe 跨 hello 叢集向外延展。 此外，可建立及 hello 立即移除個別的服務。 服務可以快速且輕鬆地向外延展從少數節點 toothousands 許多節點，節點上的執行個體上的幾個執行個體，並再調整中同樣地，根據您的資源需求。 您可以使用 Service Fabric toobuild 這些服務，並管理其完整的生命週期。
* **計算在非靜態資料**： 服務網狀架構可讓您 toobuild 資料、 輸入/輸出和計算密集的可設定狀態之應用程式。 Service Fabric 允許應用程式中的 hello 共置處理 （運算） 和資料。 一般而言，當您的應用程式需要存取 toodata，是相關聯的外部資料快取或儲存層的網路延遲。 使用具狀態的 Service Fabric 服務可以消除這種延遲，讓更多高效能的讀取和寫入發揮功效。 例如，假設您的應用程式為客戶執行近乎即時的選項建議 (來回時間低於 100 毫秒)。 hello 延遲和效能特性 （其中 hello 計算建議的選取項目將會共置 hello 資料與規則） 的 Service Fabric 服務提供回應體驗 toohello 使用者與 hello 標準實作比較從遠端儲存體 toofetch hello 必要資料模型。  
* **工作階段架構的互動式應用程式**：如果您的應用程式 (例如線上遊戲或立即訊息) 需要低度延遲讀取和寫入，Service Fabric 就很有用。 服務網狀架構可讓您 toobuild 這些互動、 可設定狀態的應用程式而不需要 toocreate 個別存放區或快取，無狀態應用程式的需求。 (這會增加延遲且可能造成一致性問題)。
* **分析資料及執行工作流程**: hello 快速讀取和寫入的 Service Fabric 啟用應用程式必須可靠地處理或資料流的事件。 服務網狀架構也可讓說明處理管線，其中結果必須是可靠而傳遞的應用程式上 toohello 接下來處理階段而不會遺失。 這其中包括交易和財務系統，其中的資料一致性和計算保證是不可或缺。
* **資料收集、 處理和 IoT**： 由於 Service Fabric 處理大型小數位數，而且具有低度延遲透過其可設定狀態的服務，非常適合用於資料處理數百萬個裝置上的 hello hello 裝置與 hello 計算的資料共置。
我們已有數名客戶使用 Service Fabric 建置 IoT 系統，包括 [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/)、[Schneider Electric](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/)、[Mesh Systems](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/)。

## <a name="application-design-case-studies"></a>應用程式設計個案研究
Hello 上發佈的數字的顯示方式 Service Fabric 這項使用的 toodesign 應用程式的案例研究[Service Fabric 團隊部落格](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)和 hello [microservices 解決方案網站](https://azure.microsoft.com/solutions/microservice-applications/)。

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>設計由無狀態與具狀態的微服務組成的應用程式
使用「Azure 雲端服務」背景工作角色來建置應用程式，即是一個無狀態服務的範例。 相較之下，可設定狀態的 microservices 會維持其 hello 要求與回應以外的授權狀態。 這會提供高可用性，透過簡單的 Api 來提供交易式複寫所支援的保證 hello 狀態的一致性。 Service Fabric 可設定狀態服務 democratize 高可用性，使其 tooall 種應用程式，而不只是資料庫和其他資料存放區。 這是自然的進展。 應用程式已經有使用單純的關聯式資料庫的高可用性 tooNoSQL 資料庫移動。 現在他們的 「 熱 」 的狀態和資料管理中額外的效能提升也不失可靠性、 一致性或可用性，可以有 hello 應用程式本身。

建置時 microservices 所組成的應用程式，您通常會有無狀態的 web 應用程式 （ASP.NET、 Node.js、 等等） 的組合到無狀態與可設定狀態之商務中介層服務進行呼叫，所有部署到 hello 相同 Service Fabric 叢集使用 hello Service Fabric 部署命令。 每個服務無關考慮 tooscale、 可靠性和資源使用量，可大幅改善在開發和生命週期管理的靈活度。

可設定狀態的 microservices 簡化應用程式的設計，因此他們移除 hello 其他佇列的 hello 需要向來必要的 tooaddress 的快取 hello 完全無狀態應用程式的可用性和延遲需求。 因為可設定狀態的服務自然是高度可用且低延遲，這表示整個應用程式中有較少的移動部分 toomanage。 hello 下圖說明 hello 差異設計是無狀態的應用程式，可以設定狀態的其中一個。 藉由運用 hello[可靠服務](service-fabric-reliable-services-introduction.md)和[Reliable Actors](service-fabric-reliable-actors-introduction.md)程式設計模型，可設定狀態服務減少應用程式複雜度但達到高輸送量和低度延遲。

## <a name="an-application-built-using-stateless-services"></a>使用無狀態服務建置的應用程式
![使用無狀態服務的應用程式][Image1]

## <a name="an-application-built-using-stateful-services"></a>使用可設定狀態的服務建置的應用程式
![使用無狀態服務的應用程式][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟

* 接聽太[客戶案例研究](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* 閱讀[客戶案例研究](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* 深入了解[模式和案例](service-fabric-patterns-and-scenarios.md)

* 開始建置無狀態與可設定狀態的服務，以 hello Service Fabric[可靠服務](service-fabric-reliable-services-quick-start.md)和[可靠執行者](service-fabric-reliable-actors-get-started.md)程式設計模型。
* 另請參閱下列主題中的 hello:
  * [Microservices 詳細說明](service-fabric-overview-microservices.md)
  * [定義及管理服務狀態](service-fabric-concepts-state.md)
  * [Service Fabric 服務的可用性](service-fabric-availability-services.md)
  * [調整 Service Fabric 服務](service-fabric-concepts-scalability.md)
  * [分割 Service Fabric 服務](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
