---
title: "自動化 Azure Service Fabric 應用程式管理 | Microsoft Docs"
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
ms.openlocfilehash: fb3c2a77ea887289eebf343e223c190781d0e4c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="automate-the-application-lifecycle-using-powershell"></a>使用 PowerShell 自動化應用程式生命週期
[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md) 的許多層面都可以自動化。  本文示範如何使用 Powershell，自動化部署、升級、移除和測試 Azure Service Fabric 應用程式的常見工作。  也可使用應用程式管理的 Managed 和 HTTP API。 如需詳細資訊，請參閱 [應用程式生命週期](service-fabric-application-lifecycle.md) 。  

## <a name="prerequisites"></a>必要條件
在您移至本文中的工作之前，請務必︰

* 熟悉 [Service Fabric 技術概觀](service-fabric-technical-overview.md)中所述的 Service Fabric 概念。
* [安裝執行階段、SDK 和工具](service-fabric-get-started.md)，這也會安裝 **ServiceFabric** PowerShell 模組。
* [啟用 PowerShell 指令碼執行](service-fabric-get-started.md#enable-powershell-script-execution)。
* 啟動本機叢集。  以系統管理員身分啟動新的 PowerShell 視窗，然後從 SDK 資料夾執行叢集安裝指令碼 ︰ `& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* 在您執行本文中的任何 PowerShell 命令之前，請先使用 [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) 連線至本機 Service Fabric 叢集：`Connect-ServiceFabricCluster localhost:19000`
* 下列工作需要 v1 應用程式封裝才能部署，並需要 v2 應用程式封裝才能進行升級。 下載 [**WordCount** 範例應用程式](http://aka.ms/servicefabricsamples) (位於快速入門範例)。 在 Visual Studio 中建置並封裝此應用程式 (以滑鼠右鍵按一下方案總管中的 [WordCount]，然後選取 [封裝])。 將 `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` 中的 v1 封裝複製到 `C:\Temp\WordCount`。 將 `C:\Temp\WordCount` 複製到 `C:\Temp\WordCountV2`，並建立 v2 應用程式封裝以便升級。 在文字編輯器中開啟 `C:\Temp\WordCountV2\ApplicationManifest.xml`。 在 **ApplicationManifest** 元素中，將 **ApplicationTypeVersion** 屬性從 "1.0.0" 變更為 "2.0.0" 以更新應用程式版本號碼。 儲存已變更的 ApplicationManifest.xml 檔案。

## <a name="task-deploy-a-service-fabric-application"></a>工作：部署 Service Fabric 應用程式
在您建置並封裝應用程式 (或下載應用程式封裝) 之後，您可以將應用程式部署至本機 Service Fabric 叢集。 部署牽涉到上傳應用程式封裝、註冊應用程式類型，以及建立應用程式執行個體。 使用本節中的指示，將新的應用程式部署至叢集。

### <a name="step-1-upload-the-application-package"></a>步驟 1：上傳應用程式封裝
上傳應用程式封裝至映像存放區，會將它放在一個可存取至內部 Service Fabric 元件的位置。  應用程式封裝包含必要的應用程式資訊清單、服務資訊清單，以及用來建立應用程式和服務執行個體的程式碼、組態和資料封裝。 如果您想要在本機確認應用程式套件，使用 [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) cmdlet。  [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) 命令會上傳套件。 例如：

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-the-application-type"></a>步驟 2：註冊應用程式類型
註冊應用程式封裝，讓應用程式類型和應用程式資訊清單中宣告的版本可供使用。 系統會讀取在步驟 1 所上傳的套件，請確認套件 (相當於在本機執行 [Test-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage))、處理套件內容，然後將處理過的套件複製到內部系統位置。  執行 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet：

```powershell
Register-ServiceFabricApplicationType WordCount
```
若要查看在叢集中註冊的應用程式類型，請執行 [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet：

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-the-application-instance"></a>步驟 3：建立應用程式執行個體
透過 [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) 命令，應用程式可以藉由使用已成功註冊的任何應用程式類型版本來進行具現化。 每個應用程式的名稱是在部署時宣告且開頭必須為 **fabric:** 配置，並且是每個應用程式執行個體的唯一名稱。 應用程式類型名稱和應用程式類型版本是在應用程式封裝的 **ApplicationManifest.xml** 檔案中宣告。 如果已在目標應用程式類型的應用程式資訊清單中定義任何預設服務，則這些服務也會一併建立。

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

[Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) 命令會列出所有已成功建立的應用程式執行個體及其整體狀態。 [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) 命令會列出所有已指定應用程式執行個體內成功建立的服務執行個體。 會列出預設的服務 (若有的話)。

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>工作：升級 Service Fabric 應用程式
您可以使用已更新的應用程式封裝，升級先前部署的 Service Fabric 應用程式。 這項工作會升級先前在「工作：部署 Service Fabric 應用程式」中部署的 WordCount 應用程式。 如需詳細資訊，請參閱 [Service Fabric 應用程式升級](service-fabric-application-upgrade.md) 。

為了簡化此範例的內容，在先決條件中建立的 WordCountV2 應用程式封裝只更新了應用程式版本號碼。 有一個更真實的相關案例，其涉及更新您的服務程式碼、組態或資料檔案，然後使用已更新的版本號碼重建並封裝應用程式。  

### <a name="step-1-upload-the-updated-application-package"></a>步驟 1：上傳已更新的應用程式封裝
WordCount v1 應用程式已準備好進行升級。 如果您以系統管理員身分開啟 PowerShell 視窗並且輸入[**Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps)，您會看到已部署 1.0.0 版的 WordCount 應用程式類型。  

現在將更新的應用程式封裝複製到 Service Fabric 映像存放區 (Service Fabric 在其中儲存應用程式封裝)。 參數 **ApplicationPackagePathInImageStore** 會通知 Service Fabric 可以在哪裡找到應用程式封裝。 下列命令會將應用程式封裝複製到映像存放區中的 **WordCountV2** ：  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-the-updated-application-type"></a>步驟 2：註冊已更新的應用程式類型
下一步是將新版本的應用程式註冊至 Service Fabric，可以藉由使用 [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet 來執行：

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-the-upgrade"></a>步驟 3：開始升級
各種升級參數、逾時和健全狀況準則可以套用至應用程式升級。 若要深入了解，請詳閱[應用程式升級參數](service-fabric-application-upgrade-parameters.md)和[升級程序](service-fabric-application-upgrade.md)文件。 所有服務和執行個體在升級之後都應該是「狀況良好」。  將 **HealthCheckStableDuration** 設定為 60 秒 (如此一來，在升級繼續至下一個升級網域之前，至少有 20 秒的時間服務是健康狀態良好的)。  同時也要將 **UpgradeDomainTimeout** 設為 1200 秒，將 **UpgradeTimeout** 設為 3000 秒。 最後，將 **UpgradeFailureAction** 設為**回復**，以要求 Service Fabric 在升級期間遇到任何失敗時，將應用程式回復為舊版。

您現在可以藉由使用 [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) Cmdlet 啟動應用程式升級：

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

請注意，應用程式名稱與先前部署的 v1.0.0 應用程式名稱相同 (fabric:/WordCount)。 Service Fabric 會使用這個名稱來識別要升級哪一個應用程式。 如果您設定的逾時太短，您可能會遇到逾時失敗訊息，指出此問題。 請參閱 [疑難排解應用程式升級](service-fabric-application-upgrade-troubleshooting.md)，或增加逾時。

### <a name="step-4-check-upgrade-progress"></a>步驟 4︰檢查升級進度
您可以使用 [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)，或使用 [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) Cmdlet，監視應用程式升級進度：

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

幾分鐘後，[Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) Cmdlet 會顯示已升級 (完成) 所有升級網域。

## <a name="task-test-a-service-fabric-application"></a>工作：測試 Service Fabric 應用程式
為了撰寫高品質的服務，開發人員必須能夠產生這類不可靠的基礎結構錯誤，才能測試其服務的穩定性。 Service Fabric 讓開發人員可以引發錯誤動作，並且藉由使用混亂和容錯移轉的測試案例以測試失敗情況下的服務。  如需其他資訊，請詳閱[錯誤分析服務簡介](service-fabric-testability-overview.md)。

### <a name="step-1-run-the-chaos-test-scenario"></a>步驟 1：執行混亂測試案例
混亂測試案例會在整個 Service Fabric 叢集中產生錯誤。 此案例會壓縮錯誤，通常是將幾個月或幾年壓縮到幾小時。 交錯錯誤和高錯誤率的組合，可以找到會在其他情形下被遺漏的極端狀況。 下列範例會執行 60 分鐘的混亂測試案例。

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-the-failover-test-scenario"></a>步驟 2：執行容錯移轉測試案例
容錯移轉測試案例的目標是特定服務資料分割，而不是整個叢集，並且讓其他服務不會受到影響。 案例會在您的商務邏輯執行時，在服務驗證中反覆一連串模擬的錯誤。 服務驗證中若有失敗，表示有需要進一步調查的問題。 容錯移轉測試一次只會引發一個錯誤，不像混亂測試案例，會引發多個錯誤。 下列範例會對下列網狀架構執行容錯移轉測試 60 分鐘：/WordCount/WordCountService service。

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>工作：移除 Service Fabric 應用程式
您可以刪除已部署應用程式的執行個體，從叢集中移除已佈建的應用程式類型，以及從 ImageStore 移除應用程式封裝。

### <a name="step-1-remove-an-application-instance"></a>步驟 1：移除應用程式執行個體
當不再需要應用程式執行個體時，您可以藉由使用 [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) Cmdlet 來永久移除。 這也會自動移除屬於應用程式的所有服務，同時永久移除所有服務狀態。 此作業無法回復，且應用程式狀態無法復原。

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-the-application-type"></a>步驟 2：取消註冊應用程式類型
當您不再需要特定應用程式類型版本時，藉由使用 [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) Cmdlet 來取消註冊。 取消註冊未使用類型，會釋放映像存放區上應用程式封裝所使用的儲存空間。 只要沒有對應的應用程式進行具現化，或擱置中的應用程式升級進行參考，則應用程式類型即可取消註冊。

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-the-application-package"></a>步驟 3：移除應用程式封裝
在取消註冊應用程式類型之後，可以藉由使用 [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) Cmdlet，從 ImageStore 移除應用程式封裝。

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>後續步驟
[Service Fabric 應用程式生命週期](service-fabric-application-lifecycle.md)

[部署應用程式](service-fabric-deploy-remove-applications.md)

[應用程式升級](service-fabric-application-upgrade.md)

[Azure Service Fabric Cmdlet](/powershell/azure/overview?view=azureservicefabricps)

