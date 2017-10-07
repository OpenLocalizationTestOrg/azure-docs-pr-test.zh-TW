---
title: "深入了解 Azure Service Fabric aaaLearn |Microsoft 文件"
description: "了解 hello 核心概念和 Azure Service Fabric 主要區域。 提供擴充的服務網狀架構的概觀以及如何 toocreate microservices。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>因此，您需要關於 Service Fabric toolearn 嗎？
Azure Service Fabric 是分散式的系統平台，可讓您輕鬆 toopackage、 部署及管理可擴充且可靠的 microservices。  Service Fabric 具有大型的介面區，不過，而且有許多 toolearn。  本文提供服務網狀架構的總覽，並描述 hello 核心概念，程式設計模型，應用程式生命週期，叢集和健全狀況監視測試。 讀取 hello[概觀](service-fabric-overview.md)和[microservices 為何？](service-fabric-overview-microservices.md)簡介和 Service Fabric 可以列印文件的是，請使用的 toocreate microservices。 本文不包含完整的內容清單中，但 toooverview 並取得每個區域的 Service Fabric 已啟動的發行項未連結。 

## <a name="core-concepts"></a>核心概念
[Service Fabric 術語](service-fabric-technical-overview.md)，[應用程式模型](service-fabric-application-model.md)，和[支援的程式設計模型](service-fabric-choose-framework.md)提供更多的概念和描述，但以下是 hello 基本概念。

<table><tr><th>核心概念</th><th>設計階段</th><th>執行階段</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>設計階段：應用程式類型、服務類型、應用程式套件和資訊清單、服務套件和資訊清單
應用程式類型是 hello 名稱/版本指派 tooa 集合的服務型別。 這是在 *ApplicationManifest.xml* 檔案中定義，此檔案內嵌在應用程式套件目錄中。 hello 應用程式套件然後複製 toohello Service Fabric 叢集的映像存放區。 然後，您可以從這個應用程式類型，然後執行 hello 叢集內建立具名的應用程式。 

服務類型是 hello 名稱/版本指派 tooa 服務的程式碼封裝、 資料封裝和組態的封裝。 這是在 ServiceManifest.xml 檔案中定義，此檔案內嵌在服務套件目錄中。 hello 服務封裝目錄然後所參考的應用程式封裝*ApplicationManifest.xml*檔案。 Hello 叢集內建立具名的應用程式之後, 您可以建立指定的服務從 hello 的其中一個應用程式類型的服務型別。 服務類型會由其 *ServiceManifest.xml* 檔案來描述。 hello 服務類型是由可執行程式碼服務組態設定，這會在執行階段載入和靜態 hello 服務所耗用的資料所組成。

![Service Fabric 應用程式類型和服務類型][cluster-imagestore-apptypes]

hello 應用程式套件是包含 hello 應用程式類型的磁碟目錄*ApplicationManifest.xml*參考 hello 服務套件的每個服務類型組成 hello 應用程式類型的檔案。 例如，電子郵件應用程式類型應用程式封裝可能包含參考 tooa 佇列服務封裝、 前端服務套件和資料庫的服務封裝。 hello 應用程式封裝目錄中的 hello 檔案會複製的 toohello Service Fabric 叢集的映像存放區。 

服務封裝是包含 hello 服務類型的磁碟目錄*ServiceManifest.xml* hello 程式碼、 靜態資料和設定套件 hello 服務型別的參考的檔案。 hello 服務封裝目錄中的 hello 檔案正由 hello 應用程式類型的*ApplicationManifest.xml*檔案。 例如，服務套件無法參照 toohello 程式碼、 靜態資料和設定套件組成資料庫服務。

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>執行階段︰叢集和節點、具名應用程式、具名服務、分割區及複本
[Service Fabric 叢集](service-fabric-deploy-anywhere.md)是一組由網路連接的虛擬或實體機器，可用來將您的微服務部署到其中並進行管理。 叢集可以調整 toothousands 的機器。

隸屬於叢集的機器或 VM 即稱為節點。 需為每個節點指派節點名稱 (字串)。 節點具有各種特性，如 placement 屬性。 每個電腦或 VM 皆有自動啟動的 Windows 服務 `FabricHost.exe`，該服務會在開機時開始執行，然後啟動兩個執行檔：`Fabric.exe` 和 `FabricGateway.exe`。 這些兩個可執行檔組成 hello 節點。 針對開發或測試案例，您可以藉由執行多個 `Fabric.exe` 和 `FabricGateway.exe` 執行個體，在單一電腦或 VM 上裝載多個節點。

具名應用程式是執行一或多個特定功能之具名服務的集合。 服務會執行完整且獨立的函數 (其可獨立於其他服務啟動和執行)，並且是由程式碼、組態和資料組成。 應用程式封裝複製的 toohello 映像存放區之後，您會藉由指定 hello 應用程式套件的應用程式類型 （使用其名稱/版本） 建立 hello hello 叢集內的應用程式的執行個體。 系統會為每個應用程式類型執行個體指派一個看起來如下的 URI 名稱：*fabric:/MyNamedApp*。 在叢集中，您可以從單一應用程式類型建立多個具名應用程式。 也可以從不同的應用程式類型建立具名應用程式。 每個具名應用程式都是獨立管理和控制版本。

建立具名的應用程式之後, 您可以藉由指定 hello 服務類型 （使用其名稱/版本） 的其中一個服務類型 （具名的服務） 執行個體建立 hello 叢集內。 需為每個服務類型執行個體指派一個 URI (名稱範圍需在其具名應用程式的 URI 之下)。 例如，如果您建立服務應用程式命名為"MyNamedApp"中的名為"MyDatabase"，hello URI 看起來像： *fabric: / MyNamedApp/MyDatabase*。 您可以在具名應用程式內建立一或多個具名服務。 每個具名服務可以有自己的分割配置和執行個體/複本計數。 

服務類型有兩種：無狀態和具狀態。 無狀態服務可以將持續狀態儲存外部儲存體服務中，例如 Azure 儲存體、Azure SQL Database 或 Azure Cosmos DB。 Hello 服務完全沒有持續性儲存體時，請使用無狀態的服務。 可設定狀態的服務會使用 Service Fabric toomanage 其可靠的集合或 Reliable Actors 程式設計模型透過您的服務狀態。 

建立具名服務時，您需指定資料分割配置。 含有大量狀態服務分割 hello 資料在資料分割。 每個資料分割會負責 hello 完整 hello 服務，則會分散到 hello 叢集節點狀態的一部分。 在分割內，無狀態的具名服務會有執行個體，而具狀態的具名服務則有複本。 通常，無狀態具名服務只會有 1 個分割，因為它們有沒有內部狀態。 具狀態的具名服務會在複本中維持其狀態，且每個資料分割都有自己的複本集。 讀取和寫入作業會執行一個複本 （稱為 hello 主要）。 變更 toostate 寫入作業會從複寫 toomultiple （稱為作用中次要資料庫） 的其他複本。 

hello 下列圖表顯示 hello 應用程式和服務執行個體、 資料分割和複本之間的關聯性。

![服務內的分割和複本][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>資料分割、調整大小和可用性
[資料分割](service-fabric-concepts-partitioning.md)不是唯一 tooService 網狀架構。 資料分割是一種知名的資料分割形式，也稱為分區化。 大量的狀態可設定狀態服務分割 hello 資料在資料分割。 每個資料分割會負責 hello hello 服務完成狀態的一部分。 

每個資料分割的 hello 複本會散佈到 hello 叢集節點，可讓您指定的服務狀態太[標尺](service-fabric-concepts-scalability.md)。 Hello 資料需要成長，成長的資料分割，以及 Service Fabric 重新平衡節點 toomake 有效率地使用硬體資源之間的資料分割。 如果您加入新的節點 toohello 叢集時，Service Fabric 會增加 hello 數目的節點之間重新平衡 hello 磁碟分割複本。 整體應用程式的效能改善，而存取 toomemory 競爭會減少。 如果未有效率地使用 hello hello 叢集中的節點，您可以減少 hello hello 叢集中的節點數目。 Service Fabric 再次重新平衡節點的每個節點上的 hello 硬體 toomake 更妥善運用的 hello 減少數目之間的 hello 磁碟分割複本。

在分割內，無狀態的具名服務會有執行個體，而具狀態的具名服務則有複本。 通常，無狀態具名服務只會有 1 個分割，因為它們有沒有內部狀態。 hello 磁碟分割執行個體提供[可用性](service-fabric-availability-services.md)。 如果一個執行個體失敗，其他執行個體 toooperate 會繼續正常執行，然後 Service Fabric 建立的新執行個體。 具狀態的具名服務會在複本中維持其狀態，且每個資料分割都有自己的複本集。 讀取和寫入作業會執行一個複本 （稱為 hello 主要）。 變更 toostate 寫入作業會從複寫 toomultiple （稱為作用中次要資料庫） 的其他複本。 Service Fabric 複本應該失敗、 建立新的複本，從 hello 現有複本。

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Service Fabric 的無狀態與具狀態微服務
服務網狀架構可讓您 toobuild microservices 或容器所組成的應用程式。 無狀態 （例如閘道通訊協定和 web proxy） microservices 不會維護外要求，其來自 hello 服務可變動的狀態。 Azure 雲端服務背景工作角色即為無狀態服務的範例。 （例如使用者帳戶、 資料庫、 裝置、 購物車和佇列） 的可設定狀態 microservices 維護超出 hello 要求和回應的可變動、 授權狀態。 現今的網際網路級別應用程式包含無狀態與可設定狀態微服務的組合。 

服務網狀架構的索引鍵 differentation 是其著重於建置可設定狀態服務，不論是透過 hello[內建的程式設計模型](service-fabric-choose-framework.md)或使用容器化的可設定狀態服務。 hello[應用程式案例](service-fabric-application-scenarios.md)說明使用具狀態服務的 hello 案例。

為什麼必須連同無狀態的可設定狀態 microservices？hello 兩個主要的原因如下：

* 您可以建立高輸送量、 低度延遲，失敗容錯的線上交易處理 (OLTP) 服務所保留的程式碼，並關閉上的資料 hello 同一部電腦。 其中的一些範例包括互動式店面、搜尋、物聯網 (IoT) 系統、交易系統、信用卡處理和詐欺偵測系統，以及個人記錄管理。
* 您可以簡化應用程式的設計。 可設定狀態的 microservices 移除 hello 需要其他佇列，並快取，也就是傳統上需要 tooaddress hello 可用性和延遲需求完全無狀態應用程式。 可設定狀態的服務自然為高可用性和低度延遲，可減少整體應用程式中的移動部分 toomanage 的 hello 數目。

## <a name="supported-programming-models"></a>支援的程式設計模型
Service Fabric 提供多個方式 toowrite 並管理您的服務。 服務可以使用 hello 服務網狀架構 Api tootake 充分善用 hello 平台的功能和應用程式架構。 服務也可以是以任何語言撰寫並裝載於 Service Fabric 叢集上的已編譯可執行程式。 如需詳細資訊，請參閱[支援的程式設計模型](service-fabric-choose-framework.md)。

### <a name="containers"></a>容器
根據預設，Service Fabric 會以處理程序形式部署和啟用這些服務。 Service Fabric 也可以在[容器](service-fabric-containers-overview.md)中部署服務。 重要的是，您可以混合在 hello 容器中處理序中的服務和服務相同的應用程式。 Service Fabric 支援在 Windows Server 2016 上部署 Linux 容器和 Windows 容器。 您可以在容器中部署現有的應用程式、無狀態服務或具狀態服務。 

### <a name="reliable-services"></a>Reliable Services
[可靠的服務](service-fabric-reliable-services-introduction.md)是一種輕量型架構的撰寫與 hello Service Fabric 平台整合，並受益於 hello 組完整的平台功能的服務。 可靠的服務可以是無狀態 （類似 toomost 服務平台，例如網頁伺服器或 Azure 雲端服務中的背景工作角色），其中保存外部的解決方案，例如 Azure DB 或 Azure 資料表儲存體中的狀態。 可靠的服務也可以是可設定狀態，直接在 hello 服務本身使用可靠的集合，其中保存狀態。 狀態透過複寫變得[高度可用](service-fabric-availability-services.md)，並透過[資料分割](service-fabric-concepts-partitioning.md)散發，全由 Service Fabric 自動管理。

### <a name="reliable-actors"></a>Reliable Actors
之上可靠的服務，hello [Reliable Actor](service-fabric-reliable-actors-introduction.md)架構是一種應用程式架構，以實作 hello Virtual Actor 模式，根據 hello 執行者設計模式。 hello Reliable Actor framework 會使用稱為執行者的單一執行緒執行獨立的單位計算和狀態。 hello Reliable Actor framework 也提供內建的執行者和預先設定的狀態持續性和向外延展組態的通訊。

### <a name="aspnet-core"></a>ASP.NET Core
Service Fabric 與 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 整合，可作為建置 Web 和 API 應用程式的最高等級程式設計模型

### <a name="guest-executables"></a>客體可執行檔
[客體可執行檔](service-fabric-deploy-existing-app.md)是以任何語言所撰寫，且與其他服務一同裝載於 Service Fabric 叢集的現有任意可執行檔。 客體可執行檔未直接與 Service Fabric API 整合。 不過他們仍然可以享受功能 hello 平台優惠，例如自訂的健全狀況和載入報告，並藉由呼叫 REST Api 服務探索能力。 它們也具備完整的應用程式生命週期支援。 

## <a name="application-lifecycle"></a>應用程式生命週期
因為與其他平台，服務網狀架構上的應用程式通常會經歷下列階段 hello： 設計、 開發、 測試、 部署、 升級、 維護和移除。 Service Fabric 提供的雲端應用程式，從開發到部署、 每日的管理和維護 tooeventual 解除委任 hello 供應用程式完整生命週期第一級的支援。 hello 服務模型可讓數個不同角色 tooparticipate 獨立 hello 應用程式生命週期中。 [Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)提供 hello 應用程式開發介面的概觀和 hello hello 階段 hello Service Fabric 應用程式生命週期的不同角色如何使用它們。 

可以使用管理 hello 整個應用程式生命週期[PowerShell cmdlet](/powershell/module/ServiceFabric/)， [C# Api](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient)， [Java 應用程式開發介面](/java/api/system.fabric._application_management_client)，和[REST Api](/rest/api/servicefabric/)。 您亦可使用 [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) 或 [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md) 等工具，設定持續整合/持續部署管線。

hello 下列 Microsoft Virtual Academy 影片說明如何 toomanage 應用程式生命週期：<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>測試應用程式與服務
toocreate 真正雲端規模服務很重要 tooverify 應用程式和服務可以承受真實世界失敗。 hello 錯誤分析服務可供測試服務網狀架構建置的服務。 以 hello[錯誤 Analysis Service](service-fabric-testability-overview.md)，您可以產生有意義的錯誤，並針對您的應用程式執行完成的測試案例。 這些錯誤和情況下執行，並驗證 hello 許多狀態和轉換，服務會在其存留期，發生在受控制、 安全且一致的方式。

[動作](service-fabric-testability-actions.md)可鎖定服務並以個別錯誤執行測試。 服務開發人員可以使用這些建置組塊 toowrite 複雜的案例。 模擬錯誤的範例如下︰

* 重新啟動節點 toosimulate 任意數目的其中一部電腦或 VM 重新開機的情況。
* 移動您可設定狀態服務 toosimulate 負載平衡、 容錯移轉或應用程式升級的複本。
* 叫用上可設定狀態服務 toocreate 其中寫入作業無法繼續進行，因為沒有足夠的 「 備份 」 或"secondary"複本 tooaccept 新資料的情況下遺失仲裁。
* 叫用可設定狀態服務 toocreate 完全時抹除所有記憶體中狀態的情況下遺失資料。

[案例](service-fabric-testability-scenarios.md)是由一或多個動作組成的複雜作業。 hello 錯誤分析服務提供兩個內建的完整案例：

* [Chaos 案例](service-fabric-controlled-chaos.md)-模擬連續交錯錯誤 （依正常程序和不正常） hello 叢集在一段很長的時間。
* [容錯移轉狀況](service-fabric-testability-scenarios.md#failover-test)-hello chaos 測試案例的目標特定的服務資料分割，同時又不影響其他服務的版本。

## <a name="clusters"></a>叢集
[Service Fabric 叢集](service-fabric-deploy-anywhere.md)是一組由網路連接的虛擬或實體機器，可用來將您的微服務部署到其中並進行管理。 叢集可以調整 toothousands 的機器。 隸屬於叢集的機器或 VM 稱為叢集模式。 需為每個節點指派節點名稱 (字串)。 節點具有各種特性，如 placement 屬性。 每部電腦或 VM 皆有自動啟動服務 `FabricHost.exe`，此服務會在開機時開始執行，然後啟動兩個可執行檔：Fabric.exe 和 FabricGateway.exe。 這些兩個可執行檔組成 hello 節點。 在測試案例中，您可以藉由執行 `Fabric.exe` 和 `FabricGateway.exe` 的多個執行個體，在單一電腦或 VM 上裝載多個節點。

您可在執行 Windows Server 或 Linux 的虛擬機器或實體機器上，建立 Service Fabric 叢集。 您可以 toodeploy 而且具有一組互相連接的 Windows Server 或 Linux 電腦在任何環境中執行 Service Fabric 應用程式： 內部部署，在 Microsoft Azure 或任何雲端提供者上。

hello 下列 Microsoft Virtual Academy 影片說明 Service Fabric 叢集：<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Azure 上的叢集
在 Azure 上執行 Service Fabric 叢集提供與其他 Azure 功能和服務整合，讓作業與 hello 叢集的管理更容易且更可靠。 叢集為 Azure Resource Manager 資源，因此您可如同 Azure 中的其他任何資源般建立叢集模型。 資源管理員也會提供便於管理 hello 叢集用作單一單元的所有資源。 Azure 上的叢集會與 Azure 診斷及 Log Analytics 整合。 叢集節點類型是[虛擬機器擴展集](/azure/virtual-machine-scale-sets/index)，因此內建自動調整功能。

您可以在 Azure 上建立叢集，透過 hello [Azure 入口網站](service-fabric-cluster-creation-via-portal.md)，從[範本](service-fabric-cluster-creation-via-arm.md)，或從[Visual Studio](service-fabric-cluster-creation-via-visual-studio.md)。

在 Linux 上的 Service Fabric hello 預覽可讓您 toobuild、 部署和管理 Linux 上的高可用性、 高擴充性應用程式，就如同在 Windows 上。 hello Service Fabric 架構 （可靠的服務和 Reliable Actors） 可用於 Java on Linux，加法 tooC # (.NET Core)。 您也可以使用任何語言或架構來建置 [來賓可執行檔服務](service-fabric-deploy-existing-app.md) 。 此外，hello 預覽也支援協調 Docker 容器。 客體可執行檔或原生的 Service Fabric 服務，使用 hello Service Fabric 架構，可以執行 docker 容器。 如需詳細資訊，請參閱 [Linux 上的 Service Fabric](service-fabric-linux-overview.md)。

由於 Linux 上的 Service Fabric 是預覽，有一些 Windows 上支援的功能在 Linux 上並不支援。 詳細資訊，讀取 toolearn [Service Fabric on Linux 和 Windows 之間的差異](service-fabric-linux-windows-differences.md)。

### <a name="standalone-clusters"></a>獨立叢集
Service Fabric 會提供安裝套件您 toocreate 獨立 Service Fabric 叢集內部部署或在任何雲端提供者。 獨立叢集授與您想要的位置 hello 自由 toohost 叢集。 如果您的資料是主體 toocompliance 或法規的條件約束，或者您想 tookeep 資料區域，您可以主控您自己的叢集和應用程式。 Service Fabric 應用程式可以在多個裝載環境中有任何變更，執行的因此從一個裝載環境 tooanother 知識的建置應用程式會有一段。 

[建立您的第一個 Service Fabric 獨立叢集](service-fabric-get-started-standalone-cluster.md)

尚不支援 Linux 獨立叢集。

### <a name="cluster-security"></a>叢集安全性
叢集必須是安全的 tooprevent 未經授權的使用者連接 tooyour 叢集，尤其是當它已在其上執行的實際執行工作負載。 雖然可能 toocreate 不安全的叢集，這樣做可讓匿名使用者 tooconnect tooit 如果管理端點會公開 toohello 公用網際網路。 它不是不安全的叢集上的可能 toolater 啟用 security： 叢集安全性在叢集建立時啟用。

hello 叢集安全性案例包括：
* 節點對節點安全性
* 用戶端對節點安全性
* 角色型存取控制 (RBAC)

如需詳細資訊，請參閱[保護叢集](service-fabric-cluster-security.md)。

### <a name="scaling"></a>調整大小
如果您加入新的節點 toohello 叢集，則 Service Fabric 重新平衡 hello 磁碟分割複本和執行個體跨 hello 增加的節點數目。 整體應用程式的效能改善，而存取 toomemory 競爭會減少。 如果未有效率地使用 hello hello 叢集中的節點，您可以減少 hello hello 叢集中的節點數目。 Service Fabric 再次重新平衡 hello 磁碟分割複本，每個節點上的 hello 硬體的更有效地使用執行個體的節點 toomake hello 減少數目之間。 您可透過[手動](service-fabric-cluster-scale-up-down.md)或[程式設計方式](service-fabric-cluster-programmatic-scaling.md)，調整 Azure 上叢集的規模。 您可[手動](service-fabric-cluster-windows-server-add-remove-nodes.md)調整獨立叢集的規模。

### <a name="cluster-upgrades"></a>叢集升級
Hello Service Fabric 執行階段的新版本會定期發行。 在叢集上執行執行階段或網狀架構升級，以確保一律執行[支援的版本](service-fabric-support.md)。 此外 toofabric 升級，您也可以更新叢集組態，例如憑證或應用程式連接埠。

Service Fabric 叢集是由您所擁有，但由 Microsoft 部分管理的資源。 Microsoft 會負責基礎 OS 和執行叢集上的 fabric 升級修補 hello。 您可以設定叢集 tooreceive 自動架構升級，當 Microsoft 發行新的版本，或選擇 tooselect 您想要支援的網狀架構版本。 透過 Azure 入口網站 hello 或資源管理員，可以設定網狀架構和設定升級。 如需詳細資訊，請參閱[升級 Service Fabric 叢集](service-fabric-cluster-upgrade.md)。 

獨立叢集是由您完全擁有的資源。 您必須負責修補 hello 基礎作業系統，然後啟動 fabric 升級。 如果您的叢集可以連接太[https://www.microsoft.com/download](https://www.microsoft.com/download)、 您可以設定您的叢集 tooautomatically 下載和佈建 hello 新的 Service Fabric 執行階段封裝。 然後您就會起始 hello 升級。 如果您的叢集無法存取[https://www.microsoft.com/download](https://www.microsoft.com/download)，您可以手動下載 hello 新的執行階段封裝從網際網路連線機器，並再啟動 hello 升級。 如需詳細資訊，請參閱[升級獨立 Service Fabric 叢集](service-fabric-cluster-upgrade-windows-server.md)。

## <a name="health-monitoring"></a>健康狀況監視
導入了 Service Fabric[健全狀況模型](service-fabric-health-introduction.md)設計 tooflag 狀況不良的叢集，並在特定實體 （例如叢集節點和服務複本） 的應用程式狀況。 hello 健全狀況模型會使用健全狀況 reporters （系統元件和 watchdogs）。 hello 目標是簡單、 快速地診斷並修復。 服務寫入器需要 toothink 預先關於健全狀況和如何太[設計健全狀況報告](service-fabric-report-health.md#design-health-reporting)。 應該報告可能會影響健全狀況的任何條件，尤其是它可以幫助旗標關閉 toohello 根本的問題。 hello 健全狀況資訊可以在偵錯和調查一旦 hello 服務已啟動且在執行大規模生產環境中儲存的時間和精力。

感興趣的條件來識別 hello Service Fabric reporters 監視器。 它們會依據其本機檢視回報這些條件。 hello[健全狀況存放區](service-fabric-health-introduction.md#health-store)彙總健全狀況資料傳送所有 reporters toodetermine 是否實體的全域狀況良好。 預定的 toobe 豐富、 彈性且容易 toouse hello 模型。 hello 健康情況報告的 hello 品質決定 hello 精確度的 hello hello 叢集健全狀況檢視。 不正確顯示出健康不良的問題之誤報，會對升級或其他使用健康狀態資料的服務產生負面影響。 這類服務的範例包括修復服務和警示機制。 因此，思考是擷取感興趣 hello 條件的所需的 tooprovide 報告的最佳可能方式。

報告可從以下項目完成：
* hello 監視 Service Fabric 服務複本或執行個體。
* 內部監視程式會部署為 Service Fabric 服務 (例如，可監視條件和問題報告的 Service Fabric 無狀態服務)。 hello watchdogs 可部署的所有節點上，或可以是相關的 toohello 監視的服務。
* 內部 watchdogs hello Service Fabric 節點上執行，但不會實作為 Service Fabric 服務。
* 外部 watchdogs 探查 hello 資源從外部 hello Service Fabric 叢集 （例如，像是 Gomez 監視服務）。

Hello 方塊中，從 Service Fabric 元件報告 hello 叢集中的所有實體健全狀況。 [系統健康狀態報告](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)可讓您全盤掌握叢集和應用程式功能，並透過健康狀態標記問題。 應用程式和服務，實體實作，且從 hello 觀點來看 hello Service Fabric 執行階段的運作正確，請確認系統健康情況報告。 hello 報告，請勿提供任何健全狀況監視 hello 服務 hello 商務邏輯或偵測無回應的處理程序。 tooadd 健全狀況資訊 tooyour 特定服務的邏輯[實作自訂的健康狀況報告](service-fabric-report-health.md)在您的服務。

Service Fabric 提供多種太[檢視健康情況報告](service-fabric-view-entities-aggregated-health.md)hello health store 中的彙總資料：
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 或其他視覺效果工具。
* 健康狀態查詢 (透過[PowerShell](/powershell/module/ServiceFabric/)，hello [C# FabricClient Api](/api/system.fabric.fabricclient.healthclient)和[Java FabricClient Api](/java/api/system.fabric._health_client)，或[REST Api](/rest/api/servicefabric))。
* 一般查詢傳回的實體清單有一個 hello 屬性 （透過 PowerShell、 hello API 或 REST） 的健全狀況。

下列 Microsoft Virtual Academy 視訊描述 hello 服務網狀架構健全狀況模型，以及如何使用 hello:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>後續步驟
* 深入了解如何 toocreate [Azure 叢集](service-fabric-cluster-creation-via-portal.md)或[獨立 Windows 上的叢集](service-fabric-cluster-creation-for-windows-server.md)。
* 嘗試建立服務，使用 hello[可靠服務](service-fabric-reliable-services-quick-start.md)或[Reliable Actors](service-fabric-reliable-actors-get-started.md)程式設計模型。
* 了解如何太[從雲端服務移轉](service-fabric-cloud-services-migration-differences.md)。
* 了解太[監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。 
* 了解太[測試您的應用程式及服務](service-fabric-testability-overview.md)。
* 了解太[管理，以及協調叢集資源](service-fabric-cluster-resource-manager-introduction.md)。
* 查看 hello [Service Fabric 範例](http://aka.ms/servicefabricsamples)。
* 了解 [Service Fabric 支援選項](service-fabric-support.md)。
* 讀取 hello[團隊部落格](https://blogs.msdn.microsoft.com/azureservicefabric/)文章和公告。


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
