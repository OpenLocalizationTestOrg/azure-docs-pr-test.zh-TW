---
title: "Azure Service Fabric aaaReport 並檢查健全狀況 |Microsoft 文件"
description: "了解 toosend 健康情況報告的方式，從您的服務程式碼，以及如何提供您的服務使用該 Azure Service Fabric hello 健全狀況監視工具 toocheck hello 健全狀況。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>回報和檢查服務健康情況
當您的服務時遇到問題時，能力 toorespond tooand 修正事件及中斷相依於您能力 toodetect hello 問題快速。 如果您所回報的問題與失敗 toohello Azure Service Fabric 健全狀況管理員從服務程式碼，您可以使用標準的健全狀況監視 Service Fabric 提供 toocheck hello 健全狀況狀態的工具。

有三種方式，您可以報告的 hello 服務健全狀況：

* 使用 [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) 或 [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) 物件。  
  您可以使用 hello`Partition`和`CodePackageActivationContext`tooreport hello 健全狀況的項目屬於的 hello 目前內容的物件。 比方說，做為複本的一部分執行的程式碼可以在該複本，其所屬的 hello 磁碟分割和 hello 應用程式，即屬於上報告健全狀況。
* 使用 `FabricClient`。   
  您可以使用`FabricClient`tooreport 健全狀況從 hello 服務程式碼如果 hello 叢集不是[安全](service-fabric-cluster-security.md)或如果 hello 服務以系統管理員權限執行。 大部分的實際案例不會使用不安全的叢集，或提供系統管理員權限。 與`FabricClient`，您可以報告的任何實體會屬於 hello 叢集的健全狀況。 在理想情況下，不過，服務程式碼應該只能傳送相關的 tooits 自己健全狀況報表。
* 使用 REST Api hello hello 叢集、 應用程式、 部署的應用程式、 服務、 服務封裝、 資料分割、 複本或節點層級。 這可以是從容器內的使用的 tooreport 健全狀況。

這篇文章會引導您從 hello 服務程式碼的健康情況報告的範例。 hello 範例也會示範如何提供 Service Fabric hello 工具可以使用的 toocheck hello 健全狀況狀態。 本文是快速介紹 toohello 健全狀況監視功能的 Service Fabric 預定的 toobe。 如需詳細資訊，您可以閱讀 hello 系列有關健康情況深入開頭 hello hello 本文結尾處的連結的文件。

## <a name="prerequisites"></a>必要條件
您必須安裝下列元件 hello:

* Visual Studio 2015 或 Visual Studio 2017
* Service Fabric SDK

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate 安全的本機開發叢集
* 以管理員權限，開啟 PowerShell 並執行下列命令的 hello:

![命令會顯示如何 toocreate 安全的開發人員叢集](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy 應用程式並檢查其健全狀況
1. 以系統管理員身分開啟 Visual Studio。
2. 建立專案使用 hello**可設定狀態服務**範本。
   
    ![建立與具狀態服務搭配使用的 Service Fabric 應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. 按**F5** toorun hello 應用程式中偵錯模式。 hello 應用程式是部署的 toohello 本機叢集。
4. Hello 應用程式執行之後，hello 通知區域中的 hello 本機叢集管理員圖示上按一下滑鼠右鍵，然後選取 **管理本機叢集**從 hello 快顯功能表 tooopen Service Fabric 總管。
   
    ![從通知區域開啟 Service Fabric 總管](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. 如同此映像，應該會顯示 hello 應用程式健全狀況。 此時，hello 應用程式應該是狀況良好且未發生錯誤。
   
    ![Service Fabric 總管中狀況良好的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. 您也可以使用 PowerShell 來檢查 hello 健全狀況。 您可以使用```Get-ServiceFabricApplicationHealth```toocheck 應用程式的健全狀況，而且您可以使用```Get-ServiceFabricServiceHealth```toocheck 服務的健全狀況。 hello hello PowerShell 中的相同應用程式是在這個影像的健康情況報告。
   
    ![PowerShell 中狀況良好的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>tooadd 自訂健全狀況事件 tooyour 服務程式碼
Visual Studio 中的 hello Service Fabric 專案範本包含範例程式碼。 hello 下列步驟示範如何報告自訂健全狀況事件，以及在您的服務程式碼。 這類報表會自動顯示 hello 標準工具中的健全狀況監視，Service Fabric 提供，例如 Service Fabric 總管、 Azure 入口網站的健全狀況檢視和 PowerShell。

1. 重新開啟您先前建立在 Visual Studio 中的 hello 應用程式，或建立新的應用程式使用 hello**可設定狀態服務**Visual Studio 範本。
2. 開啟 hello Stateful1.cs 檔案，並尋找 hello`myDictionary.TryGetValueAsync`呼叫 hello`RunAsync`方法。 您可以看到這個方法會傳回`result`保存 hello hello 計數器的目前值，因為此應用程式中的 hello 主要邏輯是 tookeep 計數執行。 如果這是實際的應用程式，而且 hello 缺乏結果表示失敗，您會想 tooflag 該事件。
3. tooreport hello 缺乏結果代表發生失敗時的健全狀況事件加入 hello 下列步驟。
   
    a. 新增 hello`System.Fabric.Health`命名空間 toohello Stateful1.cs 檔案。
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. 新增下列程式碼之後 hello hello`myDictionary.TryGetValueAsync`呼叫
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    我們會回報複本健全狀況，因為它是從具狀態服務回報的。 hello`HealthInformation`參數儲存報告的 hello 健全狀況問題的相關資訊。
   
    如果您建立無狀態服務，使用下列程式碼的 hello
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. 如果您的服務正在執行以管理員權限，或如果 hello 叢集不[安全](service-fabric-cluster-security.md)，您也可以使用`FabricClient`tooreport 健全狀況 hello 步驟中所示。  
   
    a. 建立 hello `FabricClient` hello 後的執行個體`var myDictionary`宣告。
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. 新增下列程式碼之後 hello hello`myDictionary.TryGetValueAsync`呼叫。
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. 讓我們來模擬此失敗，並查看顯示在 hello 健全狀況監視工具。 註解 hello hello 健全狀況報告您先前加入的程式碼中的第一行 toosimulate hello 失敗。 您標記為註解 hello 第一行之後，hello 程式碼看起來類似下列範例中的 hello。
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   此程式碼就會引發 hello 健康情況報告，每次`RunAsync`執行。 Hello 變更之後，按**F5** toorun hello 應用程式。
6. Hello 應用程式執行之後，開啟 Service Fabric 總管 toocheck hello hello 應用程式健全狀況。 目前，Service Fabric 總管會顯示 hello 應用程式狀況不良。 這是因為已從 hello 程式碼，我們加入先前報告的 hello 錯誤。
   
    ![Service Fabric 總管中狀況不良的應用程式](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. 如果您選取 hello 主要複本的 Service Fabric 總管 hello 樹狀檢視中，您會看到**健全狀況狀態**太表示錯誤。 Service Fabric 總管也會顯示 hello 健康情況報告詳細資料，加入 toohello `HealthInformation` hello 程式碼中的參數。 您可以看到相同的健康情況報告，在 PowerShell 中的 hello 和 hello Azure 入口網站。
   
    ![Service Fabric 總管中的複本健康情況](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

除非取代為另一個報表，或刪除此複本之前，此報表會保留在 hello 健全狀況管理員。 因為我們並未設定`TimeToLive`健全狀況報表在 hello`HealthInformation`物件 hello 報表永久有效。

我們建議您應該在 hello 最細微的層級，即在此情況下 hello 複本回報健全狀況。 您也可以回報 `Partition`的健全狀況。

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

tooreport 健全狀況`Application`， `DeployedApplication`，和`DeployedServicePackage`，使用`CodePackageActivationContext`。

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>後續步驟
* [深入了解 Service Fabric 健康情況](service-fabric-health-introduction.md)
* [回報服務健全狀況的 REST API](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [回報應用程式健全狀況的 REST API](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

