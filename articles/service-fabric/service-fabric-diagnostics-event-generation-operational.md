---
title: "服務網狀架構操作通道 aaaAzure |Microsoft 文件"
description: "Hello 操作通道的 Azure Service Fabric 叢集所產生的記錄檔的完整清單。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>作業通道 

hello 操作通道是由從 Service Fabric 執行您的節點和您的叢集上的高階動作的記錄檔所組成。 叢集中，hello Azure 診斷代理程式已部署您的叢集，且預設為啟用 「 診斷 」 時設定 tooread hello 操作通道中的記錄檔中。 深入了解設定 hello [Azure 診斷代理程式](service-fabric-diagnostics-event-aggregation-wad.md)的多個記錄檔或效能計數器您叢集 toopick toomodify hello 診斷組態。 

## <a name="operational-channel-logs"></a>作業通道記錄 

以下是 hello 操作通道中服務的網狀架構所提供的記錄檔的完整清單。 

| EventId | 名稱 | 來源 (工作) | 等級 |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | 資訊 |
| 25621 | NodeOpenedSuccess | FabricNode | 資訊 |
| 25622 | NodeOpenedFailed | FabricNode | 資訊 |
| 25623 | NodeClosing | FabricNode | 資訊 |
| 25624 | NodeClosed | FabricNode | 資訊 |
| 25625 | NodeAborting | FabricNode | 資訊 |
| 25626 | NodeAborted | FabricNode | 資訊 |
| 29627 | ClusterUpgradeStart | CM | 資訊 |
| 29628 | ClusterUpgradeComplete | CM | 資訊 |
| 29629 | ClusterUpgradeRollback | CM | 資訊 |
| 29630 | ClusterUpgradeRollbackComplete | CM | 資訊 |
| 29631 | ClusterUpgradeDomainComplete | CM | 資訊 |
| 23074 | ContainerActivated | 裝載 | 資訊 |
| 23075 | ContainerDeactivated | 裝載 | 資訊 |
| 29620 | ApplicationCreated | CM | 資訊 |
| 29621 | ApplicationUpgradeStart | CM | 資訊 |
| 29622 | ApplicationUpgradeComplete | CM | 資訊 |
| 29623 | ApplicationUpgradeRollback | CM | 資訊 |
| 29624 | ApplicationUpgradeRollbackComplete | CM | 資訊 |
| 29625 | ApplicationDeleted | CM | 資訊 |
| 29626 | ApplicationUpgradeDomainComplete | CM | 資訊 |
| 18566 | ServiceCreated | FM | 資訊 |
| 18567 | ServiceDeleted | FM | 資訊 |

## <a name="next-steps"></a>後續步驟

* 深入了解整體[hello 平台層級的事件產生](service-fabric-diagnostics-event-generation-infra.md)Service Fabric 中
* 修改您[Azure 診斷](service-fabric-diagnostics-event-aggregation-wad.md)組態 toocollect 更記錄
* [設定 Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee 您操作通道記錄
