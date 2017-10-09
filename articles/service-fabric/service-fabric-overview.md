---
title: "在 Azure 上的 Service Fabric 的 aaaOverview |Microsoft 文件"
description: "服務網狀架構，其中組成應用程式的許多 microservices tooprovide 規模和恢復功能的概觀。 Service Fabric 是分散式的系統平台使用 toobuild 可擴充、 可靠且和輕鬆管理 hello 雲端應用程式。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Azure Service Fabric 概觀
Azure Service Fabric 是分散式的系統平台，可讓您輕鬆 toopackage、 部署及管理可擴充且可靠的 microservices 和容器。 服務網狀架構也會討論 hello 在開發和管理雲端原生應用程式的重大挑戰。 開發人員與管理員能夠避免複雜的基礎結構問題，專注於實作關鍵且嚴格要求之可調整、可信賴且可管理的工作負載。 Service Fabric 代表 hello 新一代平台，用於建立和管理這些企業級、 第 1 層、 雲端規模應用程式容器中執行。

此短片將介紹 Service Fabric 和微服務：<center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>由微服務組成的應用程式 
Service Fabric 可讓您 toobuild 及管理可擴充且可靠 microservices 機器的共用集區上，以執行在較高的密度，這是指 tooas 叢集所組成的應用程式。 它提供複雜、 輕量級的執行階段 toobuild 分散，可擴充且無狀態，可設定狀態 microservices 執行容器中。 它也提供完整的應用程式管理功能 tooprovision、 部署、 監視、 升級/修補程式，以及刪除已部署的應用程式包括容器化的服務。

Service Fabric 提供技術支援給現今許多 Microsoft 服務，包括 Azure SQL Database、Azure Cosmos DB、Cortana、Microsoft Power BI、Microsoft Intune、「Azure 事件中樞」、「Azure IoT 中樞」、Dynamics 365、「商務用 Skype」以及許多核心 Azure 服務。

Service Fabric 這量身訂做的 toocreate 原生的雲端服務可以從小型專案開始，如有需要而且成長 toomassive 縮放比例和數百或數千部電腦。

現今的網際網路級別服務是使用微服務建立。 微服務範例包括通訊協定閘道器、使用者設定檔、購物車、清查處理、佇列和快取。 Service Fabric 是一個微服務平台，為可以是無狀態或具狀態的每個微服務 (或容器) 都提供一個唯一的名稱。

Service Fabric 提供完整執行階段和生命週期管理功能 tooapplications 這些 microservices 組成。 它會裝載 microservices 內部部署和啟動 hello Service Fabric 叢集中的容器。 從虛擬機器 toocontainers 移動讓訂單量級增加密度中。 同樣地，另一個重要性順序中密度就可能會從這些容器中的容器 toomicroservices 移動時。 例如，單一 Azure SQL Database 叢集是由數百個機器所組成，這些機器執行數萬個容器，而容器總共裝載了數十萬個資料庫。 每個資料庫都是 Service Fabric 的可設定狀態微服務。 

如需 hello microservices 方法的詳細資訊，請參閱[為什麼 microservices 方法 toobuilding 應用程式嗎？](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>容器部署和協調流程
Service Fabric 是將微服務部署至整個機器叢集的 Microsoft [容器協調者](service-fabric-cluster-resource-manager-introduction.md)。 可以在許多方面與使用 hello 開發 Microservices[程式設計模型的 Service Fabric](service-fabric-choose-framework.md)， [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)，toodeploying[您選擇的任何程式碼](service-fabric-deploy-existing-app.md)。 重要的是，您可以混合在處理序中的服務和服務容器的 hello 都相同的應用程式。 如果您只想太[部署和管理容器](service-fabric-containers-overview.md)，Service Fabric 是完美的選擇為容器協調者。

## <a name="any-os-any-cloud"></a>任何 OS、任何雲端
Service Fabric 可在任何環境執行。 您可以在許多環境 (包括 Azure 或內部部署、Windows Server 上或 Linux 上) 建立 Service Fabric 的叢集。 您甚至可以在其他公用雲端上建立叢集。 此外，在 hello SDK 中的 hello 開發環境是**相同**toohello 生產環境中的，與涉及任何模擬器。 換句話說，內容會在本機開發叢集上執行部署 toohello 叢集在其他環境中。

![Service Fabric 平台][Image1]

如需有關建立叢集，在內部部署，讀取[在 Windows Server 或 Lunix 上建立叢集](service-fabric-deploy-anywhere.md)或 azure 中建立叢集[hello Azure 入口網站透過](service-fabric-cluster-creation-via-portal.md)。

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Service Fabric 的無狀態與具狀態微服務
服務網狀架構可讓您 toobuild microservices 或容器所組成的應用程式。 無狀態 （例如閘道通訊協定和 web proxy） microservices 不會維護外要求，其來自 hello 服務可變動的狀態。 Azure 雲端服務背景工作角色即為無狀態服務的範例。 （例如使用者帳戶、 資料庫、 裝置、 購物車和佇列） 的可設定狀態 microservices 維護超出 hello 要求和回應的可變動、 授權狀態。 現今的網際網路級別應用程式包含無狀態與可設定狀態微服務的組合。 

服務網狀架構的索引鍵 differentation 是其著重於建置可設定狀態服務，不論是透過 hello[內建的程式設計模型](service-fabric-choose-framework.md)或使用容器化的可設定狀態服務。 hello[應用程式案例](service-fabric-application-scenarios.md)說明使用具狀態服務的 hello 案例。


## <a name="application-lifecycle-management"></a>應用程式生命週期管理
Service Fabric 提供 hello 供應用程式完整生命週期和 CI/CD 包括容器的雲端應用程式的支援。 這個生命週期包含開發到部署、 每日的管理與維護 tooeventual 解除委任。

Service Fabric 應用程式生命週期管理功能會啟用應用程式系統管理員和 IT 運算子 toouse 簡單、 低觸控式工作流程 tooprovision、 部署修補程式，及監視應用程式。 這些內建的工作流程會大幅降低 IT 運算子 tookeep 應用程式持續可用的 hello 負擔。

大多數應用程式都是由無狀態和具狀態微服務、容器及其他一起部署之可執行檔的組合所構成。 Hello 應用程式上有強式型別，服務網狀架構可讓 hello 部署多個應用程式執行個體。 每個執行個體都能獨立管理與升級。 重要的是，Service Fabric 可以部署容器或任何可執行檔，並讓它們都變得可靠。 例如，Service Fabric 可以部署 .NET、ASP.NET Core、node.js、Windows 容器、Linux 容器、Java 虛擬機器、指令碼、Angular 或實際上任何構成您應用程式的項目。

Service Fabric 已與 CI/CD 工具 (例如 [Visual Studio Team Services](https://www.visualstudio.com/team-services/)、[Jenkins](https://jenkins.io/index.html) 及 [Octopus Deploy](https://octopus.com/)) 整合，並且可與任何其他常用的 CI/CD 工具搭配使用。

如需應用程式生命週期管理的詳細資訊，請參閱[應用程式生命週期](service-fabric-application-lifecycle.md)。 如需有關如何 toodeploy 任何程式碼，請參閱[部署客體可執行檔](service-fabric-deploy-existing-app.md)。

## <a name="key-capabilities"></a>主要功能
藉由使用 Service Fabric，您可以：

* 部署執行以零程式碼變更的 Windows 或 Linux 的 tooAzure 或 tooon 內部部署資料中心。 寫入一次，並再部署任何地方 tooany Service Fabric 叢集。
* 開發可擴充的應用程式所組成的 microservices hello Service Fabric 程式設計模型、 容器或任何程式碼使用。
* 開發高度可靠的無狀態與可設定狀態微服務。 使用可設定狀態的 microservices 簡化 hello 設計應用程式。 
* 使用 hello novel Reliable Actors 的程式設計模型 toocreate 雲端物件使用包含自動程式碼和狀態。
* 部署並協調包含 Windows 容器和 Linux 容器的容器。 Service Fabric 是一個資料感知、具狀態的容器協調者。
* 以每部機器上數百或數千個應用程式或容器的高密度方式，快速部署應用程式。
* 部署 hello 相同的應用程式並存，並個別升級每個應用程式的不同的版本。
* 管理您的應用程式，而無需任何停機，包括中斷和不分行升級 hello 生命週期。
* 向外擴充或調整在 hello 叢集中的節點數目。 隨著您調整節點，應用程式也會自動調整。
* 監視和診斷的應用程式的 hello 健全狀況和設定原則執行自動修復。
* 觀賞 hello 協調 hello 叢集中的 hello 轉散發的應用程式的資源平衡器。 Service Fabric 從失敗復原，並能最佳化 hello 分配的可用資源為基礎的負載。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
* 其他資訊：
  * [為什麼 microservices 接近 toobuilding 應用程式嗎？](service-fabric-overview-microservices.md)
  * [術語概觀](service-fabric-technical-overview.md)
* 設定 Service Fabric [開發環境](service-fabric-get-started.md)  
* 了解 [Service Fabric 支援選項](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
