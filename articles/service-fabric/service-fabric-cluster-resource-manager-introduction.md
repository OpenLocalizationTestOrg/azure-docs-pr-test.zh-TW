---
title: "aaaIntroducing hello Service Fabric 叢集資源管理員 |Microsoft 文件"
description: "簡介 toohello Service Fabric 叢集資源管理員。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: cfab735b-923d-4246-a2a8-220d4f4e0c64
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: e815925880e2f3a755294de1dcfb9b88fbdde08a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-hello-service-fabric-cluster-resource-manager"></a>介紹 hello Service Fabric 叢集資源管理員
傳統上管理的 IT 系統或線上服務是特定實體或虛擬機器 toothose 特定服務或系統所專用。 服務已建構為層次。 有「Web」層和「資料」或「儲存體」層。 應用程式會有訊息層，以及一組電腦專用 toocaching 和縮小流動要求。 每個層或工作負載類型有特定電腦專用的 tooit: hello 資料庫有幾個機器專用的 tooit，hello 網頁伺服器一些。 如果特定類型的工作負載造成 hello 機器上 toorun 太忙碌，您會加入更多具有該相同的組態 toothat 層的機器。 不過，並非所有的工作負載無法向外延展輕鬆-特別與 hello 資料層通常會取代較大的機器的機器。 簡單。 如果電腦失敗，一部分 hello 整體應用程式會執行較低容量直到 hello 機器無法還原。 仍然相當簡單 (但不一定有趣)。

現在不過 hello 世界的服務和軟體的架構已變更。 應用程式採用相應放大設計更加常見。 使用容器或微服務 (或兩者) 來建置應用程式很常見。 現在，您可能仍然只有少數機器，它們不只執行工作負載的單一執行個體。 它們可能甚至會執行多個不同的工作負載在 hello 相同的時間。 您現在有很多不同類型的服務 (但都沒有充分利用整部機器的資源)，這些服務可能有數百個不同的執行個體。 每個具名執行個體有一或多個執行個體或複本來支援高可用性 (HA)。 根據這些工作負載，和它們是忙碌程度 hello 大小，您可能會發現自己具有數百部或數千部電腦。 

突然管理您的環境不像管理少數電腦專用的 toosingle 類型的工作負載這麼簡單。 您的伺服器都是虛擬的而不會再有名稱 (您切換從心態[寵物 toocattle](http://www.slideshare.net/randybias/architectures-for-open-and-scalable-clouds/20)畢竟)。 小於 hello 機器和更多有關 hello 服務本身相關的組態。 是工作負載專用的 tooa 單一執行個體的硬體是 hello 的主要過去的動作。 服務本身已經變成小型分散式系統，跨越多個較小型商用硬體。

因為您的應用程式不再是一系列的單片分散到數個層，您現在有許多與更多的組合 toodeal。 由誰決定什麼類型的工作負載可在哪些硬體上執行，或可執行多少工作負載？ 哪些工作負載使用於 hello 相同硬體和衝突？ 當機器關機時，您如何知道該機器上正在執行什麼項目？ 由誰負責確保工作負載會再次開始執行？ 您等到 hello （虛擬）？ 機器 toocome 後或執行您的工作負載會自動容錯移轉 tooother 機器和繼續執行？ 是否需要使用者介入？ 在這個環境中升級？

為開發人員和運算子處理在此環境中，我們 toowant 協助管理此複雜部分。 A 招聘 binge，然後再 toohide hello 複雜性與人員可能不是 hello 正確的答案，因此我們要怎麼做？

## <a name="introducing-orchestrators"></a>Orchestrator 簡介
「 Orchestrator 」 是軟體可協助管理員管理這種環境的 hello 一般詞彙。 Orchestrators 是 hello 元件，需要在要求中，如 「 我想在我的環境中執行此服務的五個副本 」。 他們嘗試 toomake hello 環境符合 hello 預期狀態，不論會發生什麼事。

Orchestrator (不是人類) 是當機器失敗或工作負載基於某些意外因素而終止時，要迅速採取動作的事物。 大部分 Orchestrator 不是只處理失敗而已。 其他功能還包括管理新的部署、處理升級，以及處理資源耗用量和管理。 所有 orchestrators 基本上都都是關於維護 hello 環境中設定的一些所需的狀態。 您想要能夠 tootell orchestrator toobe 什麼想並讓它不要 hello 困難。 以 Mesos、Docker Datacenter/Docker Swarm、Kubernetes 和 Service Fabric 為基礎的 Aurora，全都是 Orchestrator 的例子。 這些 orchestrators 正在主動開發的 toomeet hello 需求的生產環境中的實際工作負載。 

## <a name="orchestration-as-a-service"></a>協調流程即服務
hello 叢集資源管理員是負責處理協調流程中 Service Fabric hello 系統元件。 hello 叢集資源管理員的工作分成三個部分：

1. 強制執行規則
2. 將您的環境最佳化
3. 協助其他程序

toosee hello 叢集資源管理員的運作方式，遵循 Microsoft Virtual Academy 視訊的監看式 hello:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=d4tka66yC_5706218965">
<img src="./media/service-fabric-cluster-resource-manager-introduction/ConceptsAndDemoVid.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="what-it-isnt"></a>哪些不是它的性質
在傳統的多層式架構應用程式中，總是有[負載平衡器](https://en.wikipedia.org/wiki/Load_balancing_(computing))。 通常這是網路負載平衡器 (NLB) 或根據其中它濃度 hello 網路堆疊中的應用程式負載平衡器 (ALB)。 某些負載平衡器是以硬體為基礎 (例如 F5 的 BigIP 供應項目)，有些則是以軟體為基礎 (例如 Microsoft 的 NLB)。 在其他環境中，您可能會在這個角色中看到像 HAProxy、nginx、Istio 或 Envoy 這樣的項目。 在這些架構中，負載平衡的 hello 工作是 tooensure 無狀態工作負載 （大約） 收到 hello 相同數量的工作。 平衡負載策略各不相同。 某些平衡器就會傳送每個不同的呼叫 tooa 不同的伺服器。 有些則是提供工作階段關聯/綁定。 更進階的平衡器會使用實際負載估計或報告 tooroute 呼叫根據預期的成本和目前機器工作負載。

網路平衡器或訊息路由器嘗試 tooensure hello web/背景工作層保持大致平衡。 平衡 hello 資料層的策略是與相依 hello 資料儲存機制上的不同。 平衡 hello 資料層會依賴資料分區化中，快取，受管理的檢視表、 預存程序，與其他存放區特有的機制。

雖然這些策略的某些很有趣，hello Service Fabric 叢集資源管理員不是任何項目如網路負載平衡器或快取。 網路負載平衡器會藉由分散前端之間的流量來平衡前端。 hello Service Fabric 叢集資源管理員有不同的策略。 基本上，Service Fabric 移動*服務*toowhere 他們進行 hello 最有意義，必須要有流量或載入 toofollow。 比方說，它可能會移動，因為有的 hello 服務不會進行的工作量會目前冷服務 toonodes。 hello 節點可能會冷，因為已存在的 hello 服務已刪除或移動到其他位置。 另舉一例，hello 叢集資源管理員也無法移動離開電腦的服務。 可能是 hello 機器即將 toobe 升級，或因為耗用量的 tooa 高峰 hello 在其上執行的服務為多載。 Alernatively，可能會增加 hello 服務的資源需求。 如此一來執行此機器 toocontinue 上沒有足夠的資源。 

Hello 叢集資源管理員是負責移動周圍的服務，因為它包含在網路負載平衡器中，您會發現不同的功能集相較之下的 toowhat。 這是因為網路負載平衡器會提供網路流量 toowhere 服務已經是，即使該位置不適合用來執行 hello 服務本身。 hello Service Fabric 叢集資源管理員採用本質上不同的策略來確保 hello 叢集中的 hello 資源都有效利用。

## <a name="next-steps"></a>後續步驟
- 如 hello 叢集資源管理員中的 hello 架構和資訊流程的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-architecture.md)
- hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。 toofind 深入了解度量資訊，請參閱這篇文章上[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)
- 如需有關設定服務的詳細資訊，請參閱[深入了解設定服務](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- 度量資訊是如何 hello Service Fabric 叢集資源管理員管理耗用量和 hello 叢集中的容量。 更多關於度量和如何 tooconfigure 它們簽出 toolearn[這篇文章](service-fabric-cluster-resource-manager-metrics.md)
- hello 叢集資源管理員可搭配服務網狀架構管理功能。 深入了解該整合、 toofind 讀取[這篇文章](service-fabric-cluster-resource-manager-management-integration.md)
- toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)
