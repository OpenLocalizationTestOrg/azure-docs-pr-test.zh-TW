---
title: "Service Fabric aaaAzure 模式和案例 |Microsoft 文件"
description: "了解最佳作法，並證明，可重複使用的模式 toodesign 開發及操作您 microservices 服務網狀架構上。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a>Service Fabric 模式和案例
如果您要尋找在建置大型 microservices 使用 Azure Service Fabric，了解設計和建置此平台即服務 (PaaS) hello 專家。 開始使用適當的架構，然後了解如何 toooptimize 資源應用程式。 hello[服務網狀架構 Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344)課程回答 hello 問題最常詢問真實世界的客戶服務網狀架構案例和應用程式區域。
 
了解如何 toodesign，開發，以及操作您 microservices 上服務的網狀架構使用的最佳作法和經過驗證、 可重複使用的模式。 取得 Service Fabric 的概觀，然後深入了解涵蓋叢集最佳化和安全性、移轉舊版應用程式、大規模 IoT、裝載遊戲引擎等的主題。 查閱持續傳遞不同的工作負載，並取得 hello Linux 支援和容器的詳細資訊。 

## <a name="introduction"></a>簡介
瀏覽最佳作法，並了解為何選擇平台即服務 (PaaS) 而不是基礎結構即服務 (IaaS)。 在下列經過證實的應用程式設計原則取得 hello 詳細資料。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">簡介 tooService 網狀架構</a></td></tr>
</table>

## <a name="cluster-planning-and-management"></a>叢集規劃與管理
觀看此處的 Azure Service Fabric，了解容量規劃、叢集最佳化和叢集安全性。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">叢集規劃與管理</a></td></tr>
</table>

## <a name="hyper-scale-web"></a>超大規模 Web
檢閱超大規模 Web 的概念，包括可用性和可靠性、超規模以及狀態管理。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">超大規模 Web</a></td></tr>
</table>

## <a name="iot"></a>IoT
Azure Service Fabric，包括 hello Azure IoT 管線、 多租用戶和 IoT 大規模 hello 內容中，瀏覽 hello 物聯網 (IoT)。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></td></tr>
</table>

## <a name="gaming"></a>玩遊戲
察看回合制遊戲、互動式遊戲，以及裝載現有的遊戲引擎。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">遊戲</a></td></tr>
</table>

## <a name="continuous-delivery"></a>持續傳遞
探索相關概念，包括使用 Visual Studio Team Services、建置/封裝/發佈工作流程、多重環境設定及服務套件/共用的連續整合/連續傳遞。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">持續傳遞</a></td></tr>
</table>

## <a name="migration"></a>移轉
深入了解從移轉的雲端服務，除了 toomigration 的舊版應用程式。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">移轉</a></td></tr>
</table>

## <a name="containers-and-linux-support"></a>容器和 Linux 支援
取得 hello 回應 toohello 問題時，「 為什麼容器嗎？ 」 深入了解 Windows 容器、 Linux 支援和 Linux 容器協調流程的 hello 預覽。 此外，了解如何 toomigrate.NET Core 應用程式 tooLinux。

<table><tr><th>影片</th><th>PowerPoint 簡報</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">容器和 Linux 支援</a></td></tr>
</table>

## <a name="next-steps"></a>後續步驟
既然您已了解 Service Fabric 模式和案例，深入了解如何太[建立和管理叢集](service-fabric-deploy-anywhere.md)，[移轉雲端服務應用程式 tooService 網狀架構](service-fabric-cloud-services-migration-worker-role-stateless-service.md)，[設定持續傳遞](service-fabric-set-up-continuous-integration.md)，和[部署容器](service-fabric-containers-overview.md)。
