---
title: "Azure 雲端服務應用程式 toomicroservices aaaConvert |Microsoft 文件"
description: "本指南會比較雲端服務 Web 和背景工作角色和服務網狀架構無狀態服務 toohelp 從雲端服務 tooService 網狀架構的移轉。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>引導 tooconverting Web 和背景工作角色 tooService Fabric 無狀態服務
本文說明如何 toomigrate 您雲端服務 Web 和背景工作角色 tooService Fabric 無狀態服務。 這是應用程式的整體架構即將 toostay 大致 hello 相同 hello 簡單的移轉路徑從雲端服務 tooService 網狀架構。

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>雲端服務專案 tooService 網狀架構應用程式專案
 雲端服務專案和 Service Fabric 應用程式專案有類似的結構和兩個代表 hello 部署單位，您的應用程式-也就是說，它們每個會定義所部署的 toorun hello 完整封裝您的應用程式。 雲端服務專案包含一個或多個 Web 角色和背景工作角色。 同樣地，Service Fabric 應用程式專案也包含一個或多個服務。 

hello 的差異是 hello 雲端服務專案 couples hello 與 VM 部署的應用程式部署，因此會包含 VM 組態設定，而 hello Service Fabric 應用程式專案只會定義將部署的應用程式Service Fabric 叢集中的現有 Vm tooa 組。 一旦透過 Resource Manager 範本或透過 hello Azure 入口網站和應用程式可以是多個 Service Fabric 部署 tooit，只會部署 hello Service Fabric 叢集本身。

![Service Fabric 和雲端服務專案的比較][3]

## <a name="worker-role-toostateless-service"></a>背景工作角色 toostateless 服務
就概念而言，背景工作角色代表無狀態工作負載，這表示是相同的 hello 工作負載的每個執行個體，並要求可以在任何時間是路由的 tooany 執行個體。 每個執行個體不是預期的 tooremember hello 前一個要求。 狀態 hello 負載運作的外部狀態存放區，例如 Azure 資料表儲存體或 Azure 文件 DB 上管理。 在 Service Fabric 中，這類工作負載是以無狀態服務來代表。 最簡單方法 toomigrating hello 背景工作角色 tooService 網狀架構都可以做到轉換背景工作角色程式碼 tooa 無狀態服務。

![背景工作角色 tooStateless 服務][4]

## <a name="web-role-toostateless-service"></a>Web 角色 toostateless 服務
類似 tooWorker 角色，Web 角色也代表無狀態工作負載，因此在概念上太可以對應的 tooa Service Fabric 無狀態服務。 不過，和 Web 角色不同的是，Service Fabric 不支援 IIS。 toomigrate 從 Web 角色 tooa 無狀態服務的 web 應用程式需要第一個移動 tooa web 架構可以自我裝載，不需依賴 IIS 或 System.Web，例如 ASP.NET Core 1。

| **應用程式** | **支援** | **移轉路徑** |
| --- | --- | --- |
| ASP.NET Web Forms |否 |轉換 tooASP.NET 核心 1 MVC |
| ASP.NET MVC |移轉 |升級 tooASP.NET 核心 1 MVC |
| ASP.NET Web API |移轉 |使用自我裝載的伺服器或 ASP.NET Core 1 |
| ASP.NET Core 1 |是 |N/A |

## <a name="entry-point-api-and-lifecycle"></a>進入點 API 和生命週期
背景工作角色和 Service Fabric 服務 API 提供類似的進入點： 

| **進入點** | **背景工作角色** | **Service Fabric 服務** |
| --- | --- | --- |
| Processing |`Run()` |`RunAsync()` |
| VM 啟動 |`OnStart()` |N/A |
| VM 停止 |`OnStop()` |N/A |
| 開啟接聽程式以接收用戶端要求 |N/A |<ul><li> `CreateServiceInstanceListener()` (針對無狀態)</li><li>`CreateServiceReplicaListener()` (針對具狀態)</li></ul> |

### <a name="worker-role"></a>背景工作角色
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Service Fabric 無狀態服務
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

兩者都有主要的 [執行] 覆寫 toobegin 處理。 Service Fabric 服務將 `Run`、`Start` 和 `Stop` 結合為單一進入點 `RunAsync`。 您的服務應該開始運作`RunAsync`正常啟動，且應該停止運作時 hello`RunAsync`方法的 CancellationToken 發出信號。 

有幾項 hello 生命週期和背景工作角色和服務網狀架構服務的存留期之間的主要差異：

* **生命週期：** hello 最大的差異是背景工作角色是 VM，因此其生命週期是繫結的 toohello VM，包括何時 hello VM 啟動和停止事件。 Service Fabric 服務具有是分開 hello VM 生命週期，所以它不包含事件的 VM 或電腦啟動和停止，hello 的主控件時，因為它們不相關的生命週期。
* **存留期：**的背景工作角色執行個體就會回收如果 hello`Run`方法即會結束。 hello `RunAsync` Service Fabric 服務中的方法不過可以執行 toocompletion 而且 hello 服務執行個體將保持註冊。 

Service Fabric 為接聽用戶端要求的服務提供選擇性的通訊設定進入點。 Hello RunAsync 和通訊的進入點是在 Service Fabric 服務-服務可能會選擇 tooonly 接聽 tooclient 要求，或只處理迴圈，及 / 或執行-這就是為什麼 hello RunAsync 方法允許 tooexit 不含選擇性覆寫重新啟動 hello 服務執行個體，因為它可能會繼續 toolisten 用戶端要求。

## <a name="application-api-and-environment"></a>應用程式 API 和環境
hello 雲端服務環境 API 提供的資訊和 hello 目前 VM 執行個體，以及其他 VM 角色執行個體的相關資訊的功能。 Service Fabric 提供 tooits 執行階段相關的資訊，以及目前在執行某些 hello 節點服務的相關資訊。 

| **環境工作** | **雲端服務** | **Service Fabric** |
| --- | --- | --- |
| 組態設定和變更通知 |`RoleEnvironment` |`CodePackageActivationContext` |
| 本機儲存體 |`RoleEnvironment` |`CodePackageActivationContext` |
| 端點資訊 |`RoleInstance` <ul><li>目前的執行個體︰`RoleEnvironment.CurrentRoleInstance`</li><li>其他角色和執行個體︰`RoleEnvironment.Roles`</li> |<ul><li>`NodeContext` (針對目前的節點位址)</li><li>`FabricClient` 和 `ServicePartitionResolver` (針對服務端點探索)</li> |
| 環境模擬 |`RoleEnvironment.IsEmulated` |N/A |
| 同時變更事件 |`RoleEnvironment` |N/A |

## <a name="configuration-settings"></a>組態設定
雲端服務中的組態設定會設定的 VM 角色，並套用 tooall 該 VM 角色執行個體。 這些設定是 ServiceConfiguration.*.cscfg 檔案中所設定的索引鍵/值組，並可直接透過 RoleEnvironment 進行存取。 在 Service Fabric 設定適用於個別 tooeach 服務和 tooeach 應用程式，而不是 tooa VM，因為 VM 可以裝載多個服務和應用程式。 服務包含三個封裝：

* **程式碼：** hello 服務可執行檔、 二進位檔、 Dll 以及任何其他檔案包含服務需要 toorun。
* **組態：** 服務的所有組態檔和設定。
* **資料：** hello 服務相關聯的靜態資料檔案。

這些封裝每一個都可以獨立設定版本和升級。 類似 tooCloud 服務，設定封裝可以透過程式設計方式存取的 api，有可用的 toonotify hello 服務組態的封裝變更的事件。 Settings.xml 檔案可以用於索引鍵-值組態和以程式設計方式存取類似 toohello 應用程式設定區段的 App.config 檔案。 不過，和雲端服務不同的是，Service Fabric 組態封裝可以包含任何格式的任何組態檔，無論是 XML、JSON、YAML 或自訂的二進位格式。 

### <a name="accessing-configuration"></a>存取組態
#### <a name="cloud-services"></a>雲端服務
透過 `RoleEnvironment`即可存取 ServiceConfiguration.*.cscfg 中的組態設定。 這些設定會全域可用 tooall hello 中的角色執行個體相同的雲端服務部署。

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
每個服務都有自己的個別組態封裝。 可供叢集中所有應用程式存取的全域組態設定沒有內建機制。 使用 Service Fabric 特殊 Settings.xml 組態檔內組態封裝時，可以是 hello 應用程式層級，讓應用程式層級的組態設定可以覆寫 Settings.xml 中的值。

組態設定是透過 hello 服務每個服務執行個體內存取`CodePackageActivationContext`。

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>組態更新事件
#### <a name="cloud-services"></a>雲端服務
hello`RoleEnvironment.Changed`事件就會使用的 toonotify 所有角色執行個體變更時，就會都發生在 hello 環境中，例如組態變更。 這是使用的 tooconsume 組態更新，而不需要回收角色執行個體，或重新啟動背景工作處理序。

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Hello 三種封裝類型服務的程式碼、 組態中和資料層中有更新、 加入或移除封裝時，通知的服務執行個體的事件。 服務可以包含多個各類型的封裝。 例如，服務可以有多個組態封裝，每個都個別設定版本並可升級。 

這些事件是在不需要重新啟動 hello 服務執行個體的服務封裝中的可用 tooconsume 變更。

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>啟動工作
啟動工作是應用程式啟動前所採取的動作。 啟動工作是常用的 toorun 安裝指令碼，使用提高的權限。 雲端服務和 Service Fabric 皆支援啟動工作。 hello 主要差異在於，在雲端服務、 啟動工作是繫結的 tooa VM 因為它是一部分的角色執行個體，而服務網狀架構中的啟動工作是繫結的 tooa 服務，不是繫結的 tooany 特定 VM。

| 雲端服務 | Service Fabric |
| --- | --- | --- |
| 組態位置 |ServiceDefinition.csdef |
| 權限 |「有限」或「提高」 |
| 排序 |「簡單」、「背景」、「前景」 |

### <a name="cloud-services"></a>雲端服務
雲端服務中的啟動進入點是在 ServiceDefinition.csdef 中針對每個角色進行設定。 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
Service Fabric 中的啟動進入點是在 ServiceManifest.xml 中針對每個服務進行設定。

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>開發環境的注意事項
雲端服務和服務網狀架構會使用 Visual Studio 與整合專案範本，以及支援偵錯、 設定及部署在本機和 tooAzure。 雲端服務和 Service Fabric 也都提供本機開發執行階段環境。 hello 的差異在於 hello 雲端服務的開發執行階段會模擬 hello 於所執行的 Azure 環境中，Service Fabric 不會使用模擬器-它會使用 hello 完成 Service Fabric 執行階段。 hello Service Fabric 本機開發電腦執行的環境是 hello 在生產環境中執行的相同環境。

## <a name="next-steps"></a>後續步驟
深入了解有關服務網狀架構可靠的服務和 hello 雲端服務和 Service Fabric 應用程式架構 toounderstand tootake 利用完整的 hello 的 Service Fabric 功能的設定方式之間的基本差異。

* [開始使用 Service Fabric Reliable Services](service-fabric-reliable-services-quick-start.md)
* [雲端服務和服務網狀架構之間的概念指南 toohello 差異](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
