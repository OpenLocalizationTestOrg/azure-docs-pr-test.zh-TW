---
title: "使用 PowerShell aaaService 網狀架構應用程式升級 |Microsoft 文件"
description: "本文逐步部署 Service Fabric 應用程式、 變更 hello 程式碼，以及使用 PowerShell 升級所推出的 hello 體驗。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>使用 PowerShell 進行 Service Fabric 應用程式升級
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

hello 最常使用且建議的升級方法不受監視的 hello 輪流升級。  Azure Service Fabric 監視 hello 健全狀況 hello 應用程式正在升級根據一組的健全狀況原則。 更新網域 (UD) 升級之後，Service Fabric 評估 hello 應用程式健全狀況並繼續進行下一個更新網域 toohello 或依據 hello 健全狀況原則而定的 hello 升級會失敗。

受監視應用程式升級可使用受管理的 hello 或原生 Api，來執行 PowerShell 或 REST。 如需有關使用 Visual Studio 來執行升級的說明，請參閱 [使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md)。

服務網狀架構監視輪流升級，hello 應用程式系統管理員可以設定 hello 應用程式狀況良好，如果服務網狀架構會使用 toodetermine hello 健康情況評估原則。 此外，hello 系統管理員可以設定 hello 動作 toobe 時 hello 健全狀況評估失敗 （例如，執行自動回復。）本節逐步引導的受監視的其中一個會使用 PowerShell 的 hello SDK 範例的升級。 hello 下列 Microsoft Virtual Academy 影片會引導您完成應用程式升級：<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>步驟 1： 建置並部署 hello 視覺物件範例
建立及發行 hello 應用程式，以滑鼠右鍵按一下 hello 應用程式專案， **VisualObjectsApplication，** ，然後選取 hello**發行**命令。  如需詳細資訊，請參閱 [Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)。  或者，您可以使用 PowerShell toodeploy 您的應用程式。

> [!NOTE]
> Hello Service Fabric 命令的任何可能在 PowerShell 中使用之前，您首先需要 tooconnect toohello 叢集使用 hello `Connect-ServiceFabricCluster` cmdlet。 同樣地，它會假設該叢集具有已設定在本機電腦的 hello。 請參閱 hello 文件[設定 Service Fabric 開發環境](service-fabric-get-started.md)。
> 
> 

在建置之後 hello Visual Studio 專案中的，您可以使用 hello PowerShell 命令[複製 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy hello 應用程式封裝 toohello ImageStore。 如果您想 tooverify hello 應用程式套件在本機，使用 hello[測試 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet。 hello 下一個步驟是 tooregister hello 應用程式 toohello Service Fabric 執行階段使用 hello[暫存器 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) cmdlet。 hello 最後一個步驟是 toostart hello 應用程式的執行個體使用 hello[新增 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet。  這三個步驟是類似 toousing hello**部署**Visual Studio 中的功能表項目。

現在，您可以使用[Service Fabric 總管 tooview hello 叢集和 hello 應用程式](service-fabric-visualizing-your-cluster.md)。 hello 應用程式有可巡覽的 tooin Internet Explorer 中輸入 web 服務[http://localhost:8081/visualobjects](http://localhost:8081/visualobjects) hello 網址列中。  您應該會看到一些浮動囉 」 畫面中移動的視覺物件。  此外，您可以使用[Get ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck hello 應用程式狀態。

## <a name="step-2-update-hello-visual-objects-sample"></a>步驟 2： 更新 hello 視覺物件範例
您可能會注意到，在步驟 1 中已部署的 hello 版本，hello 視覺物件不旋轉。 讓我們來升級此應用程式 tooone，也旋轉 hello 視覺物件。

選取 hello VisualObjects 方案中的 hello VisualObjects.ActorService 專案，並開啟 hello StatefulVisualObjectActor.cs 檔案。 在該檔案中，瀏覽 toohello 方法`MoveObject`，標記為註解`this.State.Move()`，並取消註解`this.State.Move(true)`。 Hello 服務升級後，這項變更會旋轉 hello 物件。

我們還需要 tooupdate hello *ServiceManifest.xml* hello 專案檔 （在下目錄） **VisualObjects.ActorService**。 更新 hello *CodePackage* hello 服務版本 too2.0，和 hello hello 中的對應行*ServiceManifest.xml*檔案。
您可以使用 Visual Studio hello*編輯資訊清單檔案*選項之後，您以滑鼠右鍵按一下 hello 方案 toomake hello 資訊清單檔案變更。

Hello 變更之後，hello 資訊清單看起來應該像 hello 下列 （反白顯示的部分會顯示 hello 變更）：

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

現在 hello *ApplicationManifest.xml*檔案 (hello 下找到**VisualObjects**下 hello 專案**VisualObjects**方案) 是更新的 hello tooversion2.0**VisualObjects.ActorService**專案。 此外，hello 應用程式版本已更新的 too2.0.0.0 從 1.0.0.0。 hello *ApplicationManifest.xml*應該看起來像 hello 下列程式碼片段：

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


現在，選取 只 hello 建置 hello 專案**ActorService**專案，然後以滑鼠右鍵按一下並選取 hello**建置**Visual Studio 中的選項。 如果您選取**全部重建**，因為 hello 程式碼就已經變更，您應該更新 hello 適用於所有的專案版本。 接下來，讓我們套件 hello 已更新應用程式上按一下滑鼠右鍵***VisualObjectsApplication***、 選取 hello 服務網狀架構 功能表，並按一下**封裝**。 這個動作會建立可部署的應用程式封裝。  更新的應用程式已準備好 toobe 部署。

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>步驟 3：決定健康狀態原則並升級參數
熟悉 hello[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和 hello[升級程序](service-fabric-application-upgrade.md)tooget 充分了解各種升級參數、 逾時、 和健全狀況準則套用的 hello. 本逐步解說，hello 服務健全狀況評估準則是設定 toohello 預設 （及建議的） 值，表示所有服務和執行個體應該都是*狀況良好*hello 升級之後。  

不過，讓我們來增加 hello *HealthCheckStableDuration* too60 的秒數 （以便 hello 服務至少 20 秒才 hello 升級會繼續執行 toohello 接下來更新網域是狀況良好）。  我們也設定 hello *UpgradeDomainTimeout* toobe 1200 秒和 hello *UpgradeTimeout* toobe 3000 秒。

最後，我們也設定 hello *UpgradeFailureAction* toorollback。 此選項需要 Service Fabric tooroll 後 hello 應用程式 toohello 舊版 hello 升級期間遇到任何問題。 因此，當開始 （在步驟 4) 中的 hello 升級，hello 下列參數會指定：

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>步驟 4：準備應用程式以進行升級
現在建立 hello 應用程式，並準備好 toobe 升級。 如果您以系統管理員身分開啟 PowerShell 視窗並且輸入 [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps)，它應該會讓您知道它是已部署之 **VisualObjects** 的應用程式類型 1.0.0.0。  

hello 應用程式封裝會儲存在下 hello 下列相對路徑，您未壓縮 hello Service Fabric SDK 層*Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*。 您應該在該目錄中，儲存 hello 應用程式套件中找到 [封裝] 資料夾。 請檢查 hello 時間戳記 tooensure 是 hello （您可能需要適當地也 toomodify hello 路徑） 的最新組建。

現在讓我們複製 hello 更新應用程式封裝 toohello 服務網狀架構 ImageStore （hello 應用程式封裝會儲存由 Service Fabric）。 hello 參數*ApplicationPackagePathInImageStore*通知服務網狀架構，它可以在哪裡找到 hello 應用程式套件。 我們已將更新的 hello 應用程式放在 「 VisualObjects\_V2 」 以 hello 下列命令 （您再適當地可能需要 toomodify 路徑）。

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

hello 下一個步驟是以 Service Fabric，可以使用 hello 執行此應用程式的 tooregister[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)命令：

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

如果 hello 前述的命令不成功，則可能需要重建所有的服務。 步驟 2 所述，您可能必須 tooupdate 您 web 服務版本。

## <a name="step-5-start-hello-application-upgrade"></a>步驟 5： 啟動 hello 應用程式升級
現在，我們所有的設定 toostart hello 應用程式升級使用 hello[開始 ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps)命令：

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


hello 應用程式名稱是 hello 相同所述 hello *ApplicationManifest.xml*檔案。 服務網狀架構會使用哪一個應用程式會取得升級這個名稱 tooidentify。 如果您設定 hello 逾時 toobe 太短，可能會遇到失敗訊息狀態 hello 問題。 請參閱疑難排解一節，toohello 或增加 hello 逾時。

現在，hello 應用程式會繼續進行升級，您可以監視它使用 Service Fabric 總管，或使用 hello [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) PowerShell 命令： 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

在幾分鐘的時間，你使用 hello 上述 PowerShell 命令的 hello 狀態應該會在已升級所有的更新網域 （完成）。 您應該找出您的瀏覽器視窗中的 hello 視覺物件已經啟動旋轉 ！

您可以嘗試從第 2 版 tooversion 3，或從第 2 版 tooversion 做為練習 1 升級。 從第 2 版 tooversion 1 移動也被視為升級。 玩逾時和健全狀況原則 toomake 自己熟悉它們。 當您部署 Azure 叢集概略 tooan 時，hello 參數需要 toobe 集適當。 以穩當的方式是很好的 tooset hello 逾時。

## <a name="next-steps"></a>後續步驟
[使用 Visual Studio 升級您的應用程式](service-fabric-application-upgrade-tutorial.md) 將引導您完成使用 Visual Studio 進行應用程式升級的步驟。

使用 [升級參數](service-fabric-application-upgrade-parameters.md)來控制您應用程式的升級方式。

讓應用程式升級相容所學習如何 toouse[資料序列化](service-fabric-application-upgrade-data-serialization.md)。

了解 toouse 把太升級您的應用程式時所進階的功能[進階主題](service-fabric-application-upgrade-advanced.md)。

藉由參考 toohello 步驟中的修正應用程式升級的一般問題[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)。

