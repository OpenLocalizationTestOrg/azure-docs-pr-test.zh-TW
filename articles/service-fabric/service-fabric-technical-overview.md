---
title: "aaaLearn Azure Service Fabric 術語 |Microsoft 文件"
description: "Service Fabric 的術語概觀 討論在 hello hello 文件其餘部分使用主要術語概念和詞彙。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Service Fabric 術語概觀
Service Fabric 是分散式的系統平台，可讓您輕鬆 toopackage、 部署及管理可擴充且可靠的 microservices。 使用 Service Fabric toounderstand hello 條款 hello 文件中使用此主題詳細資料 hello 術語。

hello 本節所列的概念也將討論在 hello 遵循 Microsoft Virtual Academy 影片：<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">核心概念</a>，<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">設計階段概念</a>，和<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">執行階段概念</a>.

## <a name="infrastructure-concepts"></a>基礎結構概念
**叢集**：由虛擬或實體機器連結組成的網路，微服務可於其中部署和管理。  叢集可以調整 toothousands 的機器。

**節點**：屬於叢集一部分的電腦或 VM 都稱為節點。 需為每個節點指派節點名稱 (字串)。 節點具有各種特性，如 placement 屬性。 每個電腦或 VM 皆有自動啟動的 Windows 服務 `FabricHost.exe`，該服務會在開機時開始執行，然後啟動兩個執行檔：`Fabric.exe` 和 `FabricGateway.exe`。 這些兩個可執行檔組成 hello 節點。 在測試案例中，您可以藉由執行 `Fabric.exe` 和 `FabricGateway.exe` 的多個執行個體，在單一電腦或 VM 上裝載多個節點。

## <a name="application-concepts"></a>應用程式概念
**應用程式類型**: hello 指派的名稱/版本 tooa 集合的服務型別。 定義在`ApplicationManifest.xml`檔案中，內嵌在應用程式封裝目錄，然後複製 toohello Service Fabric 叢集的映像存放區。 然後，您可以從這個應用程式類型，hello 叢集內建立具名的應用程式。

讀取 hello[應用程式模型](service-fabric-application-model.md)文件以取得詳細資訊。

**應用程式封裝**: hello 應用程式類型的磁碟目錄`ApplicationManifest.xml`檔案。 參考 hello 組成 hello 應用程式類型每種服務類型的服務封裝。 hello 應用程式封裝目錄中的 hello 檔案會複製的 tooService 網狀架構叢集的映像存放區。 例如，電子郵件應用程式類型應用程式封裝可能包含參考 tooa 佇列服務封裝、 前端服務套件和資料庫的服務封裝。

**應用程式命名為**： 應用程式封裝複製的 toohello 映像存放區後，您藉由指定 hello 應用程式套件的應用程式類型 （使用其名稱/版本） 建立 hello hello 叢集內的應用程式的執行個體。 每個應用程式類型的執行個體會被指派一個看起來像這樣的 URI 名稱： `"fabric:/MyNamedApp"`。 在叢集中，您可以從單一應用程式類型建立多個具名應用程式。 也可以從不同的應用程式類型建立具名應用程式。 每個具名應用程式都是獨立管理和控制版本。      

**服務類型**: hello 名稱/版本指派 tooa 服務的程式碼封裝、 資料封裝和組態的封裝。 定義在`ServiceManifest.xml`內嵌在服務封裝目錄與 hello 服務封裝目錄中的檔案，然後應用程式封裝所參考`ApplicationManifest.xml`檔案。 Hello 叢集內建立具名的應用程式之後, 您可以建立指定的服務從 hello 的其中一個應用程式類型的服務型別。 hello 服務類型`ServiceManifest.xml`檔案描述 hello 服務。

讀取 hello[應用程式模型](service-fabric-application-model.md)文件以取得詳細資訊。

服務分為兩種：

* **無狀態：** hello 服務的永續性狀態會儲存在外部儲存體服務，例如 Azure 儲存體、 Azure SQL Database 或 Azure Cosmos DB 時，請使用無狀態的服務。 Hello 服務完全沒有持續性儲存體時，請使用無狀態的服務。 例如，計算機服務其中值會傳遞 toohello 服務，就會使用這些值執行計算並傳回結果。
* **可設定狀態：**具狀態服務要使用 Service Fabric toomanage 其可靠的集合或 Reliable Actors 程式設計模型透過您的服務狀態。 指定您想 toospread 您那一州透過 （適用於延展性） 當多少個資料分割建立具名的服務。 也會指定多少次 tooreplicate 您 （提供可靠性） 的節點之間的狀態。 每個具名服務都有一個主要複本和多個次要複本。 您可以撰寫 toohello 主要複本，以修改您指定的服務狀態。 Service Fabric 然後複寫此狀態 tooall hello 次要複本保持同步您的狀態。當主要複本失敗，且會升級現有的次要複本 tooa 主要複本時，會自動偵測 Service Fabric。 然後 Service Fabric 會建立新的次要複本。  

**服務封裝**: hello 服務類型的磁碟目錄`ServiceManifest.xml`檔案。 這個檔案會參考 hello 程式碼、 靜態資料和設定封裝 hello 服務類型。 hello 服務封裝目錄中的 hello 檔案正由 hello 應用程式類型的`ApplicationManifest.xml`檔案。 例如，服務套件無法參照 toohello 程式碼、 靜態資料和設定套件組成資料庫服務。

**名為 Service**： 之後建立具名的應用程式，您可以藉由指定 hello 服務類型 （使用其名稱/版本） 建立的其中一個 hello 叢集內的服務類型執行個體。 需為每個服務類型執行個體指派一個 URI (名稱範圍需在其具名應用程式的 URI 之下)。 例如，如果您建立服務應用程式命名為"MyNamedApp"中的名為"MyDatabase"，hello URI 看起來像： `"fabric:/MyNamedApp/MyDatabase"`。 在具名應用程式中，可以建立數個具名服務。 每個具名服務可以有自己的分割配置和執行個體/複本計數。

**程式碼封裝**: hello 服務類型的可執行檔 （通常是 EXE 或 DLL 檔案） 的磁碟目錄。 hello 程式碼封裝目錄中的 hello 檔案正由 hello 服務型別的`ServiceManifest.xml`檔案。 建立指定的服務時，hello 程式碼封裝是複製的 toohello 節點選取的 toorun hello 名為 service。 然後 hello 程式碼開始執行。 程式碼封裝執行檔分成兩種：

* **客體可執行檔**： 可執行檔，以執行-hello 主機作業系統上 （Windows 或 Linux）。 也就是這些可執行檔連結 tooor 參考任何 Service Fabric 執行階段檔案，並因此不會使用程式設計模型的任何服務網狀架構。 這些可執行檔都無法 toouse 某些 Service Fabric 功能，例如 hello 命名服務端點的探索。 客體可執行檔無法報告負載度量特定 tooeach 服務執行個體。
* **服務主機的可執行檔**： 使用 Service Fabric 連結 tooService 網狀架構執行階段檔案，程式設計模型啟用 Service Fabric 功能的可執行檔。 例如，具名服務執行個體可以在 Service Fabric 命名服務註冊端點，也可以報告負載度量。      

**資料封裝**: hello 服務類型的靜態、 唯讀資料檔案 （通常相片，音效及視訊檔案） 的磁碟目錄。 hello 資料封裝目錄中的 hello 檔案正由 hello 服務型別的`ServiceManifest.xml`檔案。 Hello 資料套件建立具名的服務時，就複製的 toohello 節點選取的 toorun hello 名為 service。  hello 程式碼開始執行，並且現在可以存取 hello 資料檔案。

**組態封裝**： 包含 hello 服務類型的靜態的磁碟目錄，唯讀的組態檔 （通常是文字檔案）。 hello 組態封裝目錄中的 hello 檔案正由 hello 服務型別的`ServiceManifest.xml`檔案。 建立指定的服務時，hello 組態套件中的 hello 檔案複製的 toohello 其中一個或多個節點選取的 toorun hello 名為 service。 然後 hello 程式碼開始執行，並且現在可以存取 hello 設定檔。

**容器**：根據預設，Service Fabric 會以處理序形式部署和啟動這些服務。 Service Fabric 也可以在容器映像中部署服務。 容器是虛擬化 hello 基礎作業系統與應用程式的虛擬化技術。 應用程式和其執行階段、 相依性，以及系統程式庫容器內執行的作業系統建構完整的私用存取 toohello 容器自己隔離檢視中。 Service Fabric 支援 Linux 上的 Docker 容器和 Windows Server 容器。  如需詳細資訊，請參閱 [Service Fabric 和容器](service-fabric-containers-overview.md)。

**分割配置**：建立具名的服務時，要指定分割配置。 含有大量狀態服務分割 hello 資料跨資料分割，hello 叢集節點間散佈 hello 狀態。 這可讓您指定的服務狀態 tooscale。 在分割內，無狀態的具名服務會有執行個體，而具狀態的具名服務則有複本。 通常，無狀態具名服務只會有 1 個分割，因為它們有沒有內部狀態。 hello 磁碟分割執行個體提供可用性。如果一個執行個體失敗，其他執行個體 toooperate 會繼續正常執行，並接著服務網狀架構將會建立新的執行個體。 名為服務的可設定狀態會維持其複本中的狀態和每個分割區有自己的複本集中，所有 hello 狀態保持同步。Service Fabric 複本應該失敗、 建立新的複本，從 hello 現有複本。

讀取 hello[可靠的資料分割 Service Fabric 服務](service-fabric-concepts-partitioning.md)文件以取得詳細資訊。

## <a name="system-services"></a>系統服務
有系統所建立的每個群集提供服務的 hello Service Fabric 平台功能。

**命名服務**： 每個 Service Fabric 叢集已命名的服務，它會解析 hello 叢集中的服務名稱 tooa 位置。 您可以管理 hello 服務名稱和屬性、 類似 tooan 網際網路網域名稱服務 (DNS) 設定為 hello 叢集。 服務名稱和位置，則用戶端安全地進行通訊與使用 hello 命名服務 tooresolve hello 叢集中任何節點。  應用程式移動，例如因為 toofailures、 資源平衡或 hello 叢集的調整大小的 hello hello 叢集內。 您可以開發服務和用戶端，但解析 hello 目前網路位置。 用戶端取得 hello 實際電腦 IP 位址和連接埠目前正在執行。

讀取[與服務通訊](service-fabric-connect-and-communicate-with-services.md)如需有關 hello 用戶端與服務通訊 hello 命名服務所使用的 Api。

**映像儲存區服務**︰每個 Service Fabric 叢集都有一個映像儲存區服務，其中保存已部署且版本化的應用程式封裝。 複製應用程式封裝 toohello 映像存放區，然後再註冊該應用程式封裝內所包含的 hello 應用程式型別。 佈建 hello 應用程式類型之後，您會從它建立具名的應用程式。 刪除所有其具名的應用程式之後，您可以取消註冊從 hello 映像存放區的服務應用程式類型。

讀取[了解 hello ImageStoreConnectionString 設定](service-fabric-image-store-connection-string.md)如需有關 hello 映像存放區服務。

讀取 hello[部署應用程式](service-fabric-deploy-remove-applications.md)發行項，如需有關部署應用程式 toohello 映像存放區服務。

## <a name="built-in-programming-models"></a>內建的程式設計模型
有可供您 toobuild Service Fabric 服務的.NET Framework 程式設計模型：

**可靠的服務**: API toobuild 無狀態與可設定狀態服務。 具狀態服務將其狀態儲存在 Reliable Collections 中 (例如字典或佇列)。 您也可以取得 tooplug 中各種的通訊堆疊，例如 Web API 和 Windows Communication Foundation (WCF)。

**Reliable Actors**: API toobuild 無狀態與可設定狀態的物件透過 hello 虛擬執行者的程式設計模型。 當您有多個獨立的計算/狀態單位時，此模型相當實用。 因為此模型使用輪流式執行緒模型，所以呼叫 tooother 執行者或服務，因為個別的動作項目無法處理其他內送要求，直到其所有的傳出要求已完成的最佳 tooavoid 程式碼。

讀取 hello[選擇服務的程式設計模型](service-fabric-choose-framework.md)文件以取得詳細資訊。

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>後續步驟
深入了解 Service Fabric toolearn:

* [Service Fabric 概觀](service-fabric-overview.md)
* [為什麼 microservices 接近 toobuilding 應用程式嗎？](service-fabric-overview-microservices.md)
* [應用程式案例](service-fabric-application-scenarios.md)

