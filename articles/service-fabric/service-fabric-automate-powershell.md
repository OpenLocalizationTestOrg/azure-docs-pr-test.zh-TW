---
title: "aaaAutomate Azure Service Fabric 應用程式管理 |Microsoft 文件"
description: "藉由使用 PowerShell 來部署、升級、測試和移除 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>自動化 hello 應用程式生命週期使用 PowerShell
Hello 的許多層面[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)可以自動化。  本文示範 toouse PowerShell tooautomate 常見的部署、 升級、 移除和測試 Azure Service Fabric 應用程式的工作。  也可使用應用程式管理的 Managed 和 HTTP API。 如需詳細資訊，請參閱 [應用程式生命週期](service-fabric-application-lifecycle.md) 。  

## <a name="prerequisites"></a>必要條件
在移動 toohello hello 文件中的工作之前，務必：

* 讓您熟悉 hello 中所述的 Service Fabric 概念[Service Fabric 的技術概觀](service-fabric-technical-overview.md)。
* [安裝 hello 執行階段、 SDK 和工具](service-fabric-get-started.md)，這也會安裝 hello **ServiceFabric** PowerShell 模組。
* [啟用 PowerShell 指令碼執行](service-fabric-get-started.md#enable-powershell-script-execution)。
* 啟動本機叢集。  啟動新的 PowerShell 視窗，以系統管理員，並從 hello SDK 資料夾執行 hello 叢集安裝指令碼：`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* 在本文中執行任何 PowerShell 命令之前，先 toohello 本機 Service Fabric 叢集使用連線[Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* 下列工作的 hello 需要 v1 應用程式封裝 toodeploy 和 v2 應用程式封裝進行升級。 下載 hello [ **WordCount**範例應用程式](http://aka.ms/servicefabricsamples)（位於 hello 快速入門範例）。 建置並封裝在 Visual Studio 中的 hello 應用程式 (以滑鼠右鍵按一下**WordCount**在方案總管，然後選取**封裝**)。 Hello v1 封裝副本中的`C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug`太`C:\Temp\WordCount`。 複製`C:\Temp\WordCount`太`C:\Temp\WordCountV2`，建立 hello v2 應用程式封裝的升級。 在文字編輯器中開啟 `C:\Temp\WordCountV2\ApplicationManifest.xml`。 在 hello **Secretscertificate**元素中，變更 hello **ApplicationTypeVersion**太屬性從 「 1.0.0""2.0.0"tooupdate hello 應用程式版本號碼。 儲存變更的 hello ApplicationManifest.xml 檔案。

## <a name="task-deploy-a-service-fabric-application"></a>工作：部署 Service Fabric 應用程式
您已建置並封裝 hello 應用程式 （或下載 hello 應用程式封裝） 之後，您可以部署到本機的 Service Fabric 叢集中的 hello 應用程式。 如果部署涉及 hello 應用程式套件上傳、 註冊 hello 應用程式類型，以及建立 hello 應用程式執行個體。 使用此區段 toodeploy 新的應用程式 tooa 叢集 hello 指示。

### <a name="step-1-upload-hello-application-package"></a>步驟 1： 上傳 hello 應用程式套件
上傳 hello 應用程式封裝 toohello 映像存放區將它放在位置存取 toointernal Service Fabric 元件。  hello 應用程式套件包含 hello 必要應用程式資訊清單中，服務資訊清單，然後程式碼中，設定和資料封裝 toocreate hello 應用程式及服務執行個體。 如果您想 tooverify hello 應用程式套件在本機，使用 hello[測試 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet。  hello[複製 ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)上傳 hello 封裝的命令。 例如：

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>步驟 2： 註冊 hello 應用程式類型
Hello 應用程式類型和可用的 hello 應用程式資訊清單中宣告使用的版本，可讓註冊的 hello 應用程式套件。 hello 系統讀取 hello 封裝上傳 hello 步驟 1 中，確認 hello 封裝 (對等 toorunning[測試 ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage)在本機上)，處理 hello 套件內容，並將複製 hello 處理封裝 tooan內部系統位置。  執行 hello[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCount
```
執行 hello 的 hello 叢集中的所有 hello 應用程式類型都註冊的 toosee [Get ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>步驟 3： 建立 hello 應用程式執行個體
應用程式可以使用任何應用程式類型版本，已成功註冊使用 hello 具現化[新增 ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)命令。 部署時間，而且必須以 hello 開頭，每個應用程式的 hello 名稱在宣告**網狀架構：**配置，而且是唯一的每個應用程式執行個體。 hello 應用程式類型名稱和應用程式類型版本的宣告中 hello **ApplicationManifest.xml** hello 應用程式封裝的檔案。 如果任何預設的服務定義 hello hello 目標應用程式類型應用程式資訊清單中，這些會建立在這個階段。

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

hello [Get ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication)命令會列出所有已成功建立，以及它們的總體狀態的應用程式執行個體。 hello [Get ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps)命令會列出所有已成功建立指定的應用程式執行個體中的 hello 服務執行個體。 會列出預設的服務 (若有的話)。

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>工作：升級 Service Fabric 應用程式
您可以使用已更新的應用程式封裝，升級先前部署的 Service Fabric 應用程式。 這項工作會升級已部署的 hello WordCount 應用程式 」 工作： 部署 Service Fabric 應用程式。 」 如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md) 。

此範例中，只有 hello 應用程式版本號碼的 tookeep 事項簡單已更新 hello WordCountV2 hello 必要條件中建立的應用程式封裝中。 更新您的服務程式碼、 組態或資料檔案然後重建，並封裝 hello 與更新的版本號碼的應用程式牽涉到更真實的案例。  

### <a name="step-1-upload-hello-updated-application-package"></a>步驟 1: Hello 更新的應用程式套件上傳
hello WordCount v1 應用程式已準備好 toobe 升級。 如果您開啟 PowerShell 視窗當做系統管理員並使用 type [ **Get ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps)，您會看到 1.0.0 版的 hello WordCount 應用程式類型部署。  

現在複製 hello 更新應用程式封裝 toohello Service Fabric 映像存放區 （hello 應用程式封裝會儲存由 Service Fabric）。 hello 參數**ApplicationPackagePathInImageStore**通知服務網狀架構，它可以在哪裡找到 hello 應用程式套件。 下列命令複製太 hello 應用程式套件的 hello**WordCountV2** hello 映像存放區中：  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>步驟 2： 註冊 hello 更新應用程式類型
hello 下一個步驟是 tooregister hello 新版 hello 應用程式與服務網狀架構，可以執行使用 hello[暫存器 ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet:

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>步驟 3： 啟動 hello 升級
各種升級參數、 逾時和健全狀況準則會套用的 tooapplication 升級。 閱讀 hello[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和[升級程序](service-fabric-application-upgrade.md)toolearn 詳細文件。 所有服務和執行個體都應該*狀況良好*hello 升級之後。  設定 hello **HealthCheckStableDuration** too60 的秒數 （以便 hello 服務至少 20 秒才 hello 升級會繼續執行 toohello 下一個升級網域是狀況良好）。  也組 hello **UpgradeDomainTimeout** too1200 的秒數和 hello **UpgradeTimeout** too3000 秒。 最後，設定 hello **UpgradeFailureAction**太**復原**，Service Fabric 回復要求 hello toohello 舊版本時，應用程式，如果在升級期間發生失敗。

您現在可以啟動 hello 應用程式升級使用 hello[開始 ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

注意 hello 先前部署 v1.0.0 應用程式名稱，該 hello 應用程式名稱是 hello 相同 (fabric: / WordCount)。 服務網狀架構會使用哪一個應用程式會取得升級這個名稱 tooidentify。 如果您設定 hello 逾時 toobe 太短，可能會遇到逾時失敗訊息狀態 hello 問題。 請參閱太[疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)，或增加 hello 逾時。

### <a name="step-4-check-upgrade-progress"></a>步驟 4︰檢查升級進度
您可以使用，以監視應用程式升級進度[Service Fabric 總管](service-fabric-visualizing-your-cluster.md)，或使用 hello [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet:

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

在幾分鐘的時間，hello [Get ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) cmdlet 會顯示已升級所有的升級網域 （完成）。

## <a name="task-test-a-service-fabric-application"></a>工作：測試 Service Fabric 應用程式
toowrite 高品質的服務，開發人員需要 toobe 無法 tooinduce 不可靠的基礎結構錯誤 tootest hello 穩定性其服務。 服務網狀架構可讓開發人員 hello 能力 tooinduce 錯誤動作和測試服務中使用失敗的 hello 與否 hello chaos 和容錯移轉的測試案例。  閱讀[簡介 toohello 錯誤 Analysis Service](service-fabric-testability-overview.md)如需詳細資訊。

### <a name="step-1-run-hello-chaos-test-scenario"></a>步驟 1： 執行 hello chaos 測試案例
hello chaos 測試案例會產生錯誤，整個 hello 整個 Service Fabric 叢集。 hello 案例壓縮通常透過月或年 tooa 看到幾個小時的錯誤。 具有較高的錯誤速率交錯錯誤 hello 組合尋找會遺漏的極端案例。 hello 下列範例會執行 hello chaos 測試案例的 60 分鐘的時間。

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>步驟 2： 執行 hello 容錯移轉的測試案例
hello 容錯移轉測試案例的目標特定的服務資料分割，而不是 hello 整個叢集，而且它會離開其他服務不會受到影響。 hello 案例逐一一連串的模擬的錯誤的服務驗證您的商務邏輯執行時。 服務驗證中若有失敗，表示有需要進一步調查的問題。 hello 容錯移轉測試，會產生只有一個以上的錯誤，一次，但不要的 toohello chaos 測試案例，這會導致多個錯誤。 hello 下列範例會執行 hello 容錯移轉測試 60 分鐘針對 hello fabric: / WordCount/WordCountService 服務。

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>工作：移除 Service Fabric 應用程式
您可以刪除部署的應用程式的執行個體從 hello 叢集中，移除 hello 佈建應用程式類型，從 hello ImageStore 移除 hello 應用程式封裝。

### <a name="step-1-remove-an-application-instance"></a>步驟 1：移除應用程式執行個體
當不再需要應用程式執行個體時，您可以永久移除使用 hello[移除 ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet。 這也會自動移除屬於 toohello 應用程式中，永久移除所有的服務狀態的所有服務。 此作業無法回復，且應用程式狀態無法復原。

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>步驟 2： 取消註冊 hello 應用程式類型
當您不再需要特定版本的應用程式類型時，將它移除註冊使用 hello[取消註冊 ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet。 取消登錄未使用的型別版本使用儲存空間 hello hello 映像存放區中的應用程式套件。 只要沒有對應的應用程式進行具現化，或擱置中的應用程式升級進行參考，則應用程式類型即可取消註冊。

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>步驟 3： 移除 hello 應用程式封裝
Hello 應用程式類型的註冊之後，hello 應用程式封裝可以從移除 hello 映像存放區使用 hello[移除 ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet。

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>後續步驟
[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)

[部署應用程式](service-fabric-deploy-remove-applications.md)

[應用程式升級](service-fabric-application-upgrade.md)

[Azure Service Fabric Cmdlet](/powershell/azure/overview?view=azureservicefabricps)

