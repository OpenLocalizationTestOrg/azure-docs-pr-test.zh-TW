---
title: "aaaAzure 容器執行個體和容器協調流程"
description: "了解 Azure 容器執行個體與容器 Orchestrator 的互動方式"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a>Azure 容器執行個體和容器 Orchestrator

由於規模較小和應用程式方向的緣故，容器很適合用於敏捷式傳遞環境和微服務式架構。 自動化及管理大量的容器，以及它們如何互動的 hello 工作即稱為*協調流程*。 熱門容器 orchestrators 包括 Kubernetes、 DC/OS，和 Docker Swarm，均可取得 hello [Azure 容器服務](https://docs.microsoft.com/azure/container-service/)。

Azure 容器執行個體提供了一些 hello 基本排程的協調流程的平台功能，但並未涵蓋這些平台提供，實際上為互補與其 hello 高價值服務。 本文說明 hello Azure 容器執行個體的處理，並與其互動容器 orchestrators 可能會填滿範圍。

## <a name="traditional-orchestration"></a>傳統協調流程

hello 的協調流程的標準定義包括 hello 下列工作：

- **排程**： 指定的容器映像和資源要求，尋找哪些 toorun hello 容器上的適當電腦。
- **親和性/反親和性**：指定一組容器應該在彼此附近執行 (以獲取效能) 或是彼此離得夠遠來執行 (以獲得可用性)。
- **健康情況監視**：監視容器的失敗，並自動為容器重新排程。
- **容錯移轉**： 每部機器上執行的項目追蹤的重新排程要從失敗的機器 toohealthy 節點的容器。
- **調整**： 新增或移除容器執行個體 toomatch 視需要手動或自動。
- **網路**： 提供的重疊網路容器 toocommunicate 協調跨越多部主機電腦。
- **服務探索**： 容器 toolocate 彼此會自動啟用視為即使主機電腦之間移動，而且變更 IP 位址。
- **協調應用程式升級**： 管理容器升級 tooavoid 應用程式停機時間，以及如果發生問題時啟用回復。

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a>使用 Azure 容器執行個體的協調流程：分層式方法

Azure 容器執行個體啟用的分層的方式 tooorchestration，提供所有 hello 排程和管理功能時，需要 toorun 單一容器中，允許 orchestrator 平台 toomanage 多容器工作，其最上層。

因為所有基礎容器執行個體的基礎結構的 hello Azure 所管理，orchestrator 平台不需要與單一容器尋找適當的主機上的機器哪些 toorun tooconcern 本身。 hello 雲端的 hello 彈性可確保一永遠可用。 相反地，hello orchestrator 可以專注於簡化多容器架構，包括縮放比例和協調的升級 hello 開發的 hello 工作。



## <a name="potential-scenarios"></a>可能的案例

雖然 Orchestrator 與 Azure 容器執行個體的整合技術仍未成熟，但我們預期可能會出現幾個不同的環境：

### <a name="orchestration-of-container-instances-exclusively"></a>獨佔的容器執行個體協調流程

因為他們快速地啟動，並由 hello 開立其帳單的第二個，以獨佔方式基礎環境 Azure 容器執行個體提供最快方式 tooget hello 啟動和 toodeal 很大的不同的工作負載。

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a>結合容器執行個體和虛擬機器中的容器

長時間執行的穩定工作負載，來協調容器在叢集中的專用虛擬機器通常會是成本比執行中的 hello 相同容器與容器的執行個體。 不過，容器執行個體提供快速擴展和收縮具有未預期的或存留較短使用量高峰您整體容量 toodeal 的最佳解決方案。 而不是擴充的虛擬機器在叢集中的 hello 數目，則部署到這些電腦的其他容器，hello orchestrator 可以只是排程 hello 使用容器執行個體的其他容器，然後刪除它們，當它們沒有不再需要。

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a>實作範例：Kubernetes 的 Azure 容器執行個體連接器

toodemonstrate 容器協調流程平台如何整合 Azure 容器執行個體，我們已開始建置[Kubernetes 範例連接器][aci-connector-k8s]。 

針對 Kubernetes 模擬 hello hello 連接器[kubelet] [ kubelet-doc]做為節點向無限制的空間，並分派 hello 建立[pod] [pod-doc] Azure 容器執行個體中的容器群組。 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

其他 orchestrators 連接器無法建立同樣的整合平台基本型別 toocombine hello 電源的 hello orchestrator API hello 速度和簡化管理 Azure 容器執行個體中的容器。

> [!WARNING]
> hello ACI 連接器 Kubernetes 是*實驗*不應在生產環境中使用。

## <a name="next-steps"></a>後續步驟

您的第一個容器建立 Azure 容器使用與執行個體 hello[快速入門指南](container-instances-quickstart.md)。

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/