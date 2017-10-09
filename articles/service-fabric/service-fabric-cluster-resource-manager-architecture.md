---
title: "aaaResource Manager 架構 |Microsoft 文件"
description: "Service Fabric 叢集資源管理員的架構概觀。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 6c4421f9-834b-450c-939f-1cb4ff456b9b
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9ea80273d0566a2ac25143ada3662875656b57b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-architecture-overview"></a>叢集資源管理員架構概觀
hello Service Fabric 叢集資源管理員會提供集中的服務執行於 hello 叢集中。 它會管理在 hello 叢集中，特別是使用尊重 tooresource 耗用量和任何放置規則的 hello 服務 hello 預期狀態。 

在叢集中的 toomanage hello 資源，hello Service Fabric 叢集資源管理員都必須有數個資訊片段：

- 目前有哪些服務
- 每個服務的目前 (或預設) 資源耗用量 
- hello 剩餘叢集容量 
- hello 叢集中的節點 hello hello 產能 
- 每個節點上所耗用的資源的 hello 數量

經過一段時間，可以變更的特定服務的 hello 資源耗用量，服務通常很重視多個資源類型。 在不同的服務之間，可能會同時測量真正實物和實體資源。 服務可能追蹤實體計量，例如記憶體和磁碟耗用量。 服務可能較關心邏輯計量，例如 "WorkQueueDepth" 或 "TotalRequests"。 邏輯與實體度量可在 hello 相同叢集中。 度量可以橫跨多個服務或特定 tooa 特定服務。

## <a name="other-considerations"></a>其他考量
hello 的擁有者和運算子的 hello 叢集可以不同於 hello 服務和應用程式的作者，或在最小值為 hello 相同穿不同 hats 的人員。 當您開發應用程式時，您知道它所需的一些事項。 您必須估計的 hello 便會取用的資源和不同的服務應部署。 比方說，hello web 層都需要 toorun 節點公開 toohello 網際網路上的時不應該 hello 資料庫服務。 另舉一例，hello web 服務可能會限制 CPU 和網路，同時 hello 資料層服務在意更多記憶體和磁碟的耗用量。 不過，處理實際執行環境，該服務的網站即時事件或使用者管理升級 toohello 服務的 hello 人有不同的工作 toodo，而且需要不同的工具。 

Hello 叢集和服務是動態的：

- hello hello 叢集中的節點數目可以擴增和縮減
- 不同大小和類型的節點可能轉瞬即逝
- 服務可能建立、移除和變更所需的資源配置和放置規則
- 升級或其他管理作業無法回復透過 hello 應用程式在 hello 叢集基礎結構層級
- 隨時都可能發生問題。

## <a name="cluster-resource-manager-components-and-data-flow"></a>叢集資源管理員元件和資料流程
hello 叢集資源管理員會在這些服務每個服務物件有 tootrack hello 需求的每個服務和 hello 消耗的資源。 hello 叢集資源管理員有兩個概念的部分： 在每個節點和容錯的服務執行的代理程式。 hello 上每個節點追蹤載入的代理程式從報表服務，彙總，並定期回報。 hello 叢集資源管理員服務彙總所有 hello 資訊從 hello 本機代理程式，並根據其目前組態的回應。

讓我們看看下列圖表中的 hello:

<center>
![資源平衡器架構][Image1]
</center>

執行階段可能發生許多變化。 例如，假設 hello 量資源的某些服務取用的變更，某些服務失敗，以及一些節點結合與離開 hello 叢集。 在節點上的所有 hello 變更會彙總，並定期傳送 toohello 叢集資源管理員服務 (1，2) 它們會在此再次彙總、 分析，然後儲存。 每隔幾秒，服務會查看 hello 變更，並判斷是否需要任何動作 (3)。 比方說，它無法發現一些空白節點，已加入 toohello 叢集。 如此一來，它決定 toomove 某些服務 toothose 節點。 hello 叢集資源管理員無法同時也請注意，特定的節點已多載，或特定服務已失敗或已刪除，釋放資源的其他位置。

讓我們看看下列圖表中的 hello，請參閱接下來的情況。 讓我們假設該 hello 叢集資源管理員決定不需要變更。 它會協調與其他系統服務 （在特定 hello 容錯移轉管理員) toomake hello 必要的變更。 然後會傳送 hello 必要命令 toohello 適當的節點 (4)。 例如，假設的 hello Node5 已多載，並因此決定 Node5 tooNode4 toomove 服務 B，注意到資源管理員。 在 hello hello 重新設定 (5) 結尾，hello 叢集看起來像這樣：

<center>
![資源平衡器架構][Image2]
</center>

## <a name="next-steps"></a>後續步驟
- hello 叢集資源管理員有許多選擇可用來描述 hello 叢集。 toofind 出更多相關資訊，請參閱這篇文章上[描述 Service Fabric 叢集](./service-fabric-cluster-resource-manager-cluster-description.md)
- 重新平衡 hello 叢集 hello 叢集資源管理員的主要責任，強制執行放置規則。 如需有關設定這些行為的詳細資訊，請參閱[平衡 Service Fabric 叢集](./service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-1.png
[Image2]:./media/service-fabric-cluster-resource-manager-architecture/Service-Fabric-Resource-Manager-Architecture-Activity-2.png
