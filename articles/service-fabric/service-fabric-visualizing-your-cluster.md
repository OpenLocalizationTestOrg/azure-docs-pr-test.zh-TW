---
title: "aaaVisualizing 叢集使用 Service Fabric 總管 |Microsoft 文件"
description: "Service Fabric 總管是一種 Web 型工具，可檢查和管理 Microsoft Azure Service Fabric 叢集中的雲端應用程式和節點。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>使用 Service Fabric 總管視覺化叢集
Service Fabric 總管是一個 Web 型工具，可檢查和管理 Azure Service Fabric 叢集中的應用程式與節點。 Service Fabric 總管是直接叢集中裝載 hello，因此永遠可使用，不論執行您的叢集。

## <a name="video-tutorial"></a>影片教學課程

Service Fabric 總管，toouse 的監看的 toolearn hello 遵循 Microsoft Virtual Academy 視訊：

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>連接 tooService 網狀架構總管
如果您已依照 hello 指示太[準備開發環境](service-fabric-get-started.md)，您可以在本機叢集上啟動 Service Fabric 總管瀏覽 toohttp://localhost:19080 / 總管。

## <a name="understand-hello-service-fabric-explorer-layout"></a>了解 hello Service Fabric 總管版面配置
您可以在 hello 左邊使用 hello 樹狀結構來巡覽 Service Fabric 總管。 Hello hello 樹狀結構根目錄之，在 hello 叢集儀表板會提供您的叢集，包括應用程式和節點健全狀況摘要的概觀。

![Service Fabric 總管叢集儀表板][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>檢視 hello 叢集配置
Service Fabric 叢集中的節點會橫跨容錯網域和升級網域的二維方格放置。 這個位置可確保您的應用程式仍可在硬體故障和應用程式升級 hello 存在。 您可以檢視如何使用 hello 叢集對應配置 hello 目前的叢集。

![Service Fabric 總管叢集對應][sfx-cluster-map]

### <a name="view-applications-and-services"></a>檢視應用程式和服務
hello 叢集包含兩個子樹： 一個適用於應用程式，而另一個節點。

您可以使用透過 Service Fabric 的邏輯階層 hello 應用程式檢視 toonavigate： 應用程式、 服務、 資料分割和複本。

Hello 下列範例中，在 hello 應用程式**MyApp**包含兩個服務， **MyStatefulService**和**WebService**。 由於 **MyStatefulService** 可設定狀態，因此它包含一個具有一個主要複本和兩個次要複本的資料分割。 對比之下，WebSvcService 則無狀態，而且只包含單一執行個體。

![Service Fabric 總管應用程式檢視][sfx-application-tree]

在 hello 樹狀結構的每個層級，hello 主窗格會顯示 hello 項目相關資訊。 例如，您可以看到 hello 健康狀態，以及針對特定服務的版本。

![Service Fabric 總管基本資訊窗格][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>檢視 hello 叢集節點
hello 節點檢視會顯示 hello 實體 hello 叢集配置。 對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。 更具體地說，您可以看到目前在那裡執行的複本。

## <a name="actions"></a>動作
Service Fabric 總管提供快速的方式 tooinvoke 節點、 應用程式，以及在您的叢集服務的動作。

例如，toodelete 應用程式執行個體中，選擇 hello 應用程式從 hello hello 左側的樹狀結構，然後選擇**動作** > **刪除應用程式**。

![在 Service Fabric 總管中刪除應用程式][sfx-delete-application]

> [!TIP]
> 您可以執行相同動作 hello 按一下 hello 省略符號 下一步 tooeach 項目。
>
>

hello 下表列出可用的每個實體的 hello 動作：

| **實體** | **動作** | **說明** |
| --- | --- | --- |
| 應用程式類型 |解除佈建類型 |移除 hello 叢集映像存放區中的 hello 應用程式套件。 需要先移除該型別 toobe 的所有應用程式。 |
| 應用程式 |刪除應用程式 |刪除 hello 應用程式，包括所有服務和其狀態 （如果有的話）。 |
| 服務 |刪除服務 |刪除 hello 服務和其狀態 （如果有的話）。 |
| 節點 |啟動 |啟動 hello 節點。 |
| 節點 | 停用 (暫停) | 暫停 hello 節點處於目前狀態。 服務繼續 toorun，但 Service Fabric 不會主動移動任何項目拖曳至或關閉它除非它是必要的 tooprevent 中斷或資料不一致。 這個動作是常用的 tooenable 偵錯不會移動期間檢查特定節點 tooensure 上的服務。 | |
| 節點 | 停用 (重新啟動) | 安全地移除所有記憶體內部服務，並關閉持續性服務。 通常 hello 主機處理序或電腦需要 toobe 重新啟動時使用。 | |
| 節點 | 停用 (移除資料) | 安全地關閉 hello 節點上執行建置足夠的備援複本之後的所有服務。 通常於節點 (或至少其儲存體) 永久性地移除委任時使用。 | |
| 節點 | 移除節點狀態 | 從 hello 叢集移除節點的複本的知識。 通常在已失敗的節點被視為無法回復時使用。 | |
| 節點 | 重新啟動 | 重新啟動 hello 節點，以模擬在節點失敗。 如需詳細資訊，請參閱[這裡](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)。 | |

由於許多動作所破壞性，您可能會要求您 tooconfirm 您的意圖 hello 動作完成之前。

> [!TIP]
> 可透過 Service Fabric 總管來執行每個動作也可以透過 PowerShell 或 REST API，tooenable 自動化來執行。
>
>

您也可以使用指定的應用程式類型和版本的 Service Fabric 總管 toocreate 應用程式執行個體。 在 hello 樹狀結構檢視中，選擇 hello 應用程式類型，然後按一下 hello**建立應用程式執行個體**連結 hello 右窗格中，您想要 下一步 toohello 版本。

![在 Service Fabric Explorer 中建立應用程式執行個體][sfx-create-app-instance]

> [!NOTE]
> 透過 Service Fabric Explorer 建立的應用程式執行個體目前無法參數化。 會使用預設參數值來建立它們。
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>連接 tooa 遠端 Service Fabric 叢集
如果您知道 hello 叢集端點，且有足夠的權限可以從任何瀏覽器來存取 Service Fabric 總管。 這是因為 Service Fabric 總管 hello 叢集中執行的只是另一個服務。

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>探索遠端叢集的 hello Service Fabric 總管端點
指定的叢集，tooreach Service Fabric 總管指向您的瀏覽器：

http://&lt;your-cluster-endpoint&gt;:19080/Explorer

Azure 的叢集，hello 完整的 URL 也會提供在 hello 叢集 essentials 窗格中的 hello Azure 入口網站。

### <a name="connect-tooa-secure-cluster"></a>Tooa 安全叢集連線
您可以控制用戶端存取 tooyour Service Fabric 叢集可以使用憑證或使用 Azure Active Directory (AAD)。

如果您嘗試在安全的叢集上的 tooconnect tooService Fabric 總管，然後根據 hello 叢集設定您將會是需要的 toopresent 用戶端憑證或使用 AAD 登入。

## <a name="next-steps"></a>後續步驟
* [Testability 概觀](service-fabric-testability-overview.md)
* [在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)
* [使用 PowerShell 部署 Service Fabric 應用程式](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
