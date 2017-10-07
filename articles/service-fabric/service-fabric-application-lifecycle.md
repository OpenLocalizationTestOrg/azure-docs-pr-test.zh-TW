---
title: "在 Service Fabric aaaApplication 生命週期 |Microsoft 文件"
description: "描述開發、部署、測試、升級、維護和移除 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 08837cca-5aa7-40da-b087-2b657224a097
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 36cd6081010e83cb8226c8f85d1e912ac9eebd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-lifecycle"></a>Service Fabric 應用程式生命週期
因為與其他平台，在 Azure Service Fabric 應用程式通常會經歷下列階段 hello： 設計、 開發、 測試、 部署、 升級、 維護和移除。 Service Fabric 提供的雲端應用程式，從開發到部署、 每日的管理和維護 tooeventual 解除委任 hello 供應用程式完整生命週期第一級的支援。 hello 服務模型可讓數個不同角色 tooparticipate 獨立 hello 應用程式生命週期中。 本文章提供 hello 應用程式開發介面的概觀和 hello hello 階段 hello Service Fabric 應用程式生命週期的不同角色如何使用它們。

hello 下列 Microsoft Virtual Academy 影片說明如何 toomanage 應用程式生命週期：<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-application-lifecycle/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="service-model-roles"></a>服務模型角色
hello 服務模型角色如下：

* **服務開發人員**： 開發可以重新設定與 hello 的多個應用程式中使用的模組化和泛型服務相同或不同的類型。 例如，佇列服務可以用於建立票證應用程式 ( 技術支援中心) 或電子商務應用程式 (購物車)。
* **應用程式開發人員**： 特定需求或案例，整合服務 toosatisfy 的集合，藉以建立應用程式。 例如，電子商務網站可能會整合 「 JSON 無狀態前端服務 」，「 拍賣可設定狀態服務 」 和 「 佇列可設定狀態服務 」 toobuild 拍賣解決方案。
* **應用程式系統管理員**： 決定 hello 應用程式組態 （填寫 hello 組態範本參數）、 （對應 tooavailable 資源） 的部署和服務品質。 例如，應用程式系統管理員決定 hello 應用程式的 hello 語言地區設定 （英文 hello 美國或日本為日文）。 以不同方式部署的應用程式可以有不同的設定。
* **運算子**： 將 hello 應用程式組態和 hello 應用程式系統管理員所指定的需求為基礎的應用程式部署。 比方說，運算子會佈建和 hello 應用程式部署並確保它在 Azure 中執行。 運算子會監視應用程式健全狀況和效能資訊，並視需要維護 hello 實體基礎結構。

## <a name="develop"></a>開發
1. A*服務開發人員*開發不同類型的服務使用 hello [Reliable Actors](service-fabric-reliable-actors-introduction.md)或[可靠服務](service-fabric-reliable-services-introduction.md)程式設計模型。
2. A*服務開發人員*以宣告方式描述組成一或多個程式碼、 組態和資料封裝的服務資訊清單檔中的 hello 開發的服務型別。
3. 然後， *應用程式開發人員* 建置使用不同服務類型的應用程式。
4. *應用程式開發人員*以宣告方式描述應用程式資訊清單中的 hello 應用程式類型所參考的 hello 組成服務的 hello 服務資訊清單和適當地覆寫，而參數化不同組態和部署設定的 hello 組成的服務。

如需範例，請參閱[開始使用可靠的執行者](service-fabric-reliable-actors-get-started.md)和[開始使用可靠的服務](service-fabric-reliable-services-quick-start.md)。

## <a name="deploy"></a>部署
1. *應用程式系統管理員*調整藉由指定 hello 適當參數的 hello hello 應用程式類型 tooa 特定應用程式部署的 toobe tooa Service Fabric 叢集**ApplicationType**hello 應用程式資訊清單中的項目。
2. *運算子*上傳 hello 應用程式封裝 toohello 叢集映像存放區使用 hello [ **CopyApplicationPackage**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_)或 hello [ **複製 ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)。 hello 應用程式套件包含 hello 應用程式資訊清單和 hello 服務封裝集合。 Service Fabric 將從儲存在 hello 映像存放區，這可以是 Azure blob 存放區或 hello Service Fabric 系統服務的 hello 應用程式封裝的應用程式部署。
3. hello*運算子*然後佈建 hello 從 hello 已上傳的應用程式封裝使用 hello hello 目標叢集中的應用程式類型[ **ProvisionApplicationAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_)，hello [**暫存器 ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype)，或使用 hello [**佈建應用程式**的REST作業](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application).
4. 佈建 hello 應用程式之後,*運算子*啟動 hello 與 hello 參數 hello 所提供的應用程式*應用程式系統管理員*使用 hello [ **CreateApplicationAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CreateApplicationAsync_System_Fabric_Description_ApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_)，hello [**新增 ServiceFabricApplication** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricapplication)，或使用 hello [**建立應用程式**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/create-an-application)。
5. Hello 應用程式部署完成之後，*運算子*使用 hello [ **CreateServiceAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_CreateServiceAsync_System_Fabric_Description_ServiceDescription_System_TimeSpan_System_Threading_CancellationToken_)，hello [ **新 ServiceFabricService** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice)，或使用 hello [ **Create Service** REST 作業](https://docs.microsoft.com/rest/api/servicefabric/create-a-service)toocreate 新服務執行個體 hello 應用程式為基礎可用的服務類型。
6. hello 應用程式現在正在 hello Service Fabric 叢集中執行。

如需範例，請參閱 [部署應用程式](service-fabric-deploy-remove-applications.md) 。

## <a name="test"></a>測試
1. 在部署 toohello 本機開發叢集或測試叢集之後,*服務開發人員*執行 hello 內建的容錯移轉的測試案例使用 hello [ **FailoverTestScenarioParameters**](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenarioparameters#System_Fabric_Testability_Scenario_FailoverTestScenarioParameters)和[ **FailoverTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.failovertestscenario#System_Fabric_Testability_Scenario_FailoverTestScenario)類別或 hello [ **Invoke ServiceFabricFailoverTestScenario** cmdlet](/powershell/module/servicefabric/invoke-servicefabricfailovertestscenario?view=azureservicefabricps). hello 容錯移轉的測試案例很重要，則仍然可以使用且運作的轉換和容錯移轉 tooensure 逐步執行指定的服務。
2. hello*服務開發人員*然後執行 hello 內建 chaos 測試案例使用 hello [ **ChaosTestScenarioParameters** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenarioparameters#System_Fabric_Testability_Scenario_ChaosTestScenarioParameters)和[ **ChaosTestScenario** ](https://docs.microsoft.com/dotnet/api/system.fabric.testability.scenario.chaostestscenario#System_Fabric_Testability_Scenario_ChaosTestScenario)類別或 hello [ **Invoke ServiceFabricChaosTestScenario** cmdlet](/powershell/module/servicefabric/invoke-servicefabricchaostestscenario?view=azureservicefabricps)。 hello chaos 測試案例隨機產生多個節點、 程式碼封裝，以及複本錯誤到 hello 叢集中。
3. hello*服務開發人員*[測試服務對服務通訊](service-fabric-testability-scenarios-service-communication.md)撰寫移動周圍 hello 叢集的主要複本的測試案例。

請參閱[簡介 toohello 錯誤 Analysis Service](service-fabric-testability-overview.md)如需詳細資訊。

## <a name="upgrade"></a>升級
1. A*服務開發人員*更新 hello 組成服務的 hello 具現化應用程式和/或修正 bug，並提供新版本的 hello 服務資訊清單。
2. *應用程式開發人員*會覆寫和參數化 hello hello 一致服務的組態和部署設定，並提供新版本的 hello 應用程式資訊清單。 hello 應用程式開發人員之後納入 hello 應用程式中的 hello 的 hello 服務資訊清單的新版本，並提供更新的應用程式封裝中的 hello 應用程式類型的新版本。
3. *應用程式系統管理員*納入 hello 目標應用程式中的 hello 新版 hello 應用程式類型，藉由更新 hello 適當的參數。
4. *運算子*上傳 hello 更新的應用程式封裝 toohello 叢集映像存放區使用 hello [ **CopyApplicationPackage**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_CopyApplicationPackage_System_String_System_String_System_String_)或 hello [**複製 ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps)。 hello 應用程式套件包含 hello 應用程式資訊清單和 hello 服務封裝集合。
5. *運算子*佈建 hello 新版 hello hello 目標叢集中的應用程式使用 hello [ **ProvisionApplicationAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_ProvisionApplicationAsync_System_String_System_TimeSpan_System_Threading_CancellationToken_)，hello [**暫存器 ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/register-servicefabricapplicationtype)，或使用 hello [**佈建應用程式**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/provision-an-application)。
6. *運算子*升級 hello 目標應用程式 toohello 新版本使用 hello [ **UpgradeApplicationAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpgradeApplicationAsync_System_Fabric_Description_ApplicationUpgradeDescription_System_TimeSpan_System_Threading_CancellationToken_)，hello [ **開始 ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationupgrade)，或使用 hello [**升級應用程式**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/upgrade-an-application)。
7. *運算子*檢查 hello 使用 hello 升級的進度[ **GetApplicationUpgradeProgressAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_GetApplicationUpgradeProgressAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_)，hello [ **Get ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricapplicationupgrade)，或使用 hello [**取得應用程式升級進度**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/get-the-progress-of-an-application-upgrade1)。
8. 如有必要，hello*運算子*修改並重新套用 hello 使用 hello 目前應用程式升級 hello 參數[ **UpdateApplicationUpgradeAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UpdateApplicationUpgradeAsync_System_Fabric_Description_ApplicationUpgradeUpdateDescription_System_TimeSpan_System_Threading_CancellationToken_)，hello [**更新 ServiceFabricApplicationUpgrade** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/update-servicefabricapplicationupgrade)，或使用 hello [**更新應用程式升級**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/update-an-application-upgrade).
9. 如有必要，hello*運算子*回復 hello 使用 hello 目前應用程式升級[ **RollbackApplicationUpgradeAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RollbackApplicationUpgradeAsync_System_Uri_System_TimeSpan_System_Threading_CancellationToken_)，hello [**開始 ServiceFabricApplicationRollback** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/start-servicefabricapplicationrollback)，或使用 hello [**復原應用程式升級**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/rollback-an-application-upgrade)。
10. Service Fabric 升級 hello 目標應用程式，而不會遺失其組成服務的任何 hello 可用性 hello 叢集中執行。

請參閱 hello[應用程式升級的教學課程](service-fabric-application-upgrade-tutorial.md)範例。

## <a name="maintain"></a>維護
1. 針對作業系統升級和修補程式，Service Fabric 介面以 hello Azure 基礎結構 tooguarantee 可用性 hello 叢集中執行的所有 hello 應用程式。
2. 升級和修補 toohello Service Fabric 平台，Service Fabric 升級而不會遺失任何 hello hello 叢集上執行的應用程式的可用性。
3. *應用程式系統管理員*核准 hello 新增或移除從叢集中的節點之後分析歷史容量使用資料及預估的未來需求。
4. *運算子*新增和移除節點指定 hello*應用程式系統管理員*。
5. 當您從 hello 叢集中移除 tooor 現有的節點加入新的節點時，Service Fabric 自動負載平衡 hello hello 叢集 tooachieve 達到最佳效能的所有節點之間執行應用程式。

## <a name="remove"></a>移除
1. *運算子*可以刪除執行中服務 hello 叢集中的特定執行個體，而不移除 hello 整個應用程式使用 hello [ **DeleteServiceAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient#System_Fabric_FabricClient_ServiceManagementClient_DeleteServiceAsync_System_Fabric_Description_DeleteServiceDescription_System_TimeSpan_System_Threading_CancellationToken_)hello [**移除 ServiceFabricService** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricservice)，或使用 hello [**刪除服務**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/delete-a-service)。  
2. *運算子*也可以刪除應用程式執行個體和其所有的服務使用 hello [ **DeleteApplicationAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_DeleteApplicationAsync_System_Fabric_Description_DeleteApplicationDescription_System_TimeSpan_System_Threading_CancellationToken_)，hello [ **移除 ServiceFabricApplication** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/remove-servicefabricapplication)，或使用 hello [**刪除應用程式**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/delete-an-application)。
3. 一旦 hello 應用程式及服務已停止，hello*運算子*可以解除佈建 hello 應用程式類型使用 hello [ **UnprovisionApplicationAsync**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_UnprovisionApplicationAsync_System_String_System_String_System_TimeSpan_System_Threading_CancellationToken_)，hello [**取消註冊 ServiceFabricApplicationType** cmdlet](https://docs.microsoft.com/powershell/servicefabric/vlatest/unregister-servicefabricapplicationtype)，或使用 hello [**解除佈建應用程式**REST 作業](https://docs.microsoft.com/rest/api/servicefabric/unprovision-an-application). 解除佈建 hello 應用程式類型不會從 hello ImageStore 移除 hello 應用程式套件。 您必須手動移除 hello 應用程式套件。
4. *運算子*移除 hello 應用程式套件從 hello ImageStore 使用 hello [ **RemoveApplicationPackage**方法](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.applicationmanagementclient#System_Fabric_FabricClient_ApplicationManagementClient_RemoveApplicationPackage_System_String_System_String_)或 hello [ **移除 ServiceFabricApplicationPackage** cmdlet](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps)。

如需範例，請參閱 [部署應用程式](service-fabric-deploy-remove-applications.md) 。

## <a name="next-steps"></a>後續步驟
如需開發、測試及管理 Service Fabric 應用程式和服務的詳細資訊，請參閱：

* [Reliable Actors](service-fabric-reliable-actors-introduction.md)
* [Reliable Services](service-fabric-reliable-services-introduction.md)
* [部署應用程式](service-fabric-deploy-remove-applications.md)
* [應用程式升級](service-fabric-application-upgrade.md)
* [Testability 概觀](service-fabric-testability-overview.md)
