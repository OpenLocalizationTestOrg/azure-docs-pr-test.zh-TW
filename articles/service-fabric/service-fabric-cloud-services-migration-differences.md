---
title: "雲端服務和服務網狀架構之間的 aaaDifferences |Microsoft 文件"
description: "概念的概觀，移轉的雲端服務 tooService 網狀架構的應用程式。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 0b87b1d3-88ad-4658-a465-9f05a3376dee
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: bbc5ef4fe0fe1b0da55454cb6b766925030198fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-hello-differences-between-cloud-services-and-service-fabric-before-migrating-applications"></a>深入了解雲端服務和服務網狀架構的 hello 差異，然後再移轉應用程式。
Microsoft Azure Service Fabric 是可高度擴充、 可靠的分散式應用程式的 hello 新一代雲端應用程式平台。 其中導入了許多封裝、部署、更新及管理分散式雲端應用程式的新功能。 

這是從雲端服務 tooService 網狀架構入門指南 toomigrating 應用程式。 內容著重於雲端服務與 Service Fabric 之間的架構及設計差異。

## <a name="applications-and-infrastructure"></a>應用程式與基礎結構
雲端服務和服務網狀架構基本差別在於 hello Vm、 工作負載和應用程式之間的關聯性。 Hello 程式碼撰寫 tooperform 特定工作，或提供服務的工作負載的定義。

* **雲端服務的重點是將應用程式部署為 VM。** hello 您撰寫的程式碼是緊密結合的 tooa VM 執行個體，例如 Web 或背景工作角色。 toodeploy 雲端服務中的工作負載 toodeploy 其中一個或多個 VM 執行個體執行的 hello 工作負載。 應用程式與 VM 沒有區別，因此對於應用程式也沒有正式的定義。 應用程式可以視為雲端服務部署中的一組 Web 或背景工作角色，或是整個雲端服務部署。 在此範例中，應用程式會顯示為一組角色執行個體。

![雲端服務應用程式和拓撲][1]

* **Service Fabric 是關於部署應用程式 tooexisting Vm 或 Windows 或 Linux 上執行 Service Fabric 的機器。** 您撰寫的 hello 服務是從基礎基礎結構，抽象的 hello Service Fabric 應用程式平台，好讓應用程式可以部署的 toomultiple 環境的 hello 完全解除解合。 工作負載服務網狀架構中稱為 「 服務 」，而一或多個服務會一起 hello Service Fabric 應用程式平台執行的正式定義應用程式中。 多個應用程式可以是已部署的 tooa 單一 Service Fabric 叢集。

![Service Fabric 應用程式和拓撲][2]

Service Fabric 本身是在 Windows 或 Linux 執行的應用程式平台層，而雲端服務是用來部署受 Azure 管理且連接工作負載的 VM。
hello Service Fabric 應用程式模型有許多優點：

* 部署快速。 建立 VM 執行個體可能非常耗時。 在 Service Fabric 一旦 tooform 叢集，主控 hello Service Fabric 應用程式平台，只會部署 Vm。 從該點上，應用程式封裝可以非常快速地是已部署的 toohello 叢集。
* 高密度裝載。 在雲端服務中，一個背景工作角色 VM 裝載一個工作負載。 在 Service Fabric 應用程式的不同的 hello Vm 加以執行，這表示您可以部署大量的應用程式 tooa 少數幾個 Vm，可降低整體成本較大的部署。
* hello Service Fabric 平台可以執行任何位置，具有 Windows Server 或 Linux 機器，它是 Azure 或內部部署。 hello 平台透過 hello 基礎結構提供一個抽象層，讓您的應用程式可以在不同的環境中執行。 
* 管理分散式應用程式。 Service Fabric 是平台，不只裝載分散式應用程式，但也可協助管理其生命週期獨立 hello 裝載 VM 或電腦生命週期。

## <a name="application-architecture"></a>應用程式架構
hello 架構的雲端服務應用程式通常包括許多外部服務相依性，例如服務匯流排、 Azure 資料表和 Blob 儲存體、 SQL、 Redis，和其他人 toomanage hello 狀態和資料的應用程式和網站之間的通訊和雲端服務部署中的背景工作角色。 完整雲端服務應用程式的範例如下：  

![雲端服務架構][9]

Service Fabric 應用程式也可以選擇 toouse hello 相同的外部服務的完整應用程式中。 使用此雲端服務架構的範例，hello 簡單的移轉路徑從雲端服務 tooService 網狀架構是 tooreplace 僅 hello 雲端服務部署 Service Fabric 應用程式，保留 hello 整體架構 hello 相同。 hello Web 和背景工作角色可以是移植的 tooService Fabric 無狀態服務以最少的程式碼變更。

![簡單移轉後的 Service Fabric 架構][10]

在這個階段，hello 系統應該繼續 toowork 如常 hello 相同。 善加利用 Service Fabric 的具狀態服務，若適用則外部狀態存放區可初始化為具狀態服務。 這是比更為複雜的簡易移轉，Web 和背景工作角色 tooService 網狀架構無狀態服務，因為它需要撰寫自訂之前 hello 外部服務一樣，提供對等的功能 tooyour 應用程式的服務。 這樣做的 hello 優點包括： 

* 移除外部相依性 
* 統一的 hello 部署、 管理及升級模型。 

初始化這些服務的基礎結構之結果的範例如下：

![完整移轉後的 Service Fabric 架構][11]

## <a name="communication-and-workflow"></a>通訊與工作流程
大部分的雲端服務應用程式由一個以上的層組成。 同樣地，Service Fabric 應用程式由一個以上的服務組成 (通常是許多服務)。 二種常見的通訊模型為直接通訊及透過外部耐久性儲存體。

### <a name="direct-communication"></a>直接通訊
使用直接通訊，層之間可以透過各自所公開的端點直接通訊。 在無狀態的環境，例如雲端服務，此表示選取的 VM 角色執行個體可以隨機或 toobalance 循環配置資源負載，而連線 tooits 端點直接。

![雲端服務直接通訊][5]

 直接通訊是 Service Fabric 中常見的通訊模型。 hello Service Fabric 和雲端服務之間的主要差異是雲端服務中您連線 tooa VM，而您可以在 Service Fabric 連線 tooa 服務。 這是重要差異，原因如下：

* 在 Service Fabric 服務未繫結的 toohello Vm 中裝載這些;服務可能移動在 hello 叢集中，而且事實上，周圍的預期的 toomove 基於各種原因： 資源平衡、 容錯移轉、 應用程式和基礎結構升級和放置或載入條件約束。 這表示服務執行個體的位址可隨時變更。 
* Service Fabric 中的 VM 可以託管多個服務，且每個有獨特的端點。

Service Fabric 提供服務探索機制，稱為 hello 命名服務，可以使用的 tooresolve 服務的端點位址。 

![Service Fabric 直接通訊][6]

### <a name="queues"></a>佇列
在無狀態的環境，例如雲端服務的各層之間常見的通訊機制是 toouse 外部儲存體佇列 toodurably 儲存從某一層 tooanother 的工作。 常見的案例是傳送作業 tooan Azure 佇列的 web 層或服務匯流排背景工作角色執行個體可以清除佇列並處理 hello 作業的位置。

![雲端服務佇列通訊][7]

相同的通訊模式可用於 Service Fabric hello。 移轉現有的雲端服務應用程式 tooService 網狀架構時，這非常有用。 

![Service Fabric 直接通訊][8]

## <a name="next-steps"></a>後續步驟
hello 簡單的移轉路徑，從 網狀架構是 tooreplace 只 hello Service Fabric 應用程式，讓雲端服務部署 hello 整體架構的應用程式大致上的雲端服務 tooService hello 相同。 hello 下列文章提供的指引 toohelp 轉換 Web 或背景工作角色 tooa Service Fabric 無狀態服務。

* [簡單的移轉： 轉換 Web 或背景工作角色 tooa Service Fabric 無狀態服務](service-fabric-cloud-services-migration-worker-role-stateless-service.md)

<!--Image references-->
[1]: ./media/service-fabric-cloud-services-migration-differences/topology-cloud-services.png
[2]: ./media/service-fabric-cloud-services-migration-differences/topology-service-fabric.png
[5]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-direct.png
[6]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-direct.png
[7]: ./media/service-fabric-cloud-services-migration-differences/cloud-service-communication-queues.png
[8]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-communication-queues.png
[9]: ./media/service-fabric-cloud-services-migration-differences/cloud-services-architecture.png
[10]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-simple.png
[11]: ./media/service-fabric-cloud-services-migration-differences/service-fabric-architecture-full.png
