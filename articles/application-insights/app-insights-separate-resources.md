---
title: "aaaSeparating 遙測從開發、 測試和發行 Azure Application Insights |Microsoft 文件"
description: "開發、 測試和生產戳記直接遙測 toodifferent 資源。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>區分開發、測試及生產環境的遙測

當您開發 hello 下一版的 web 應用程式時，您不想註冊 hello toomix [Application Insights](app-insights-overview.md) hello 新的版本與 hello 已發行版本的遙測。 tooavoid 混淆的可能性，傳送嗨遙測，從不同的開發階段 tooseparate Application Insights 資源，使用個別的檢測金鑰 (ikeys)。 toomake 它更容易 toochange hello 檢測金鑰為版本從移動一個階段 tooanother 可能很有用的 tooset hello ikey hello 組態檔案中的程式碼而不是。 

(如果您的系統是「Azure 雲端服務」，有[另一個設定個別 ikey 的方法](app-insights-cloudservices.md))。

## <a name="about-resources-and-instrumentation-keys"></a>關於資源和檢測金鑰

在為 Web 應用程式設定 Application Insights 監視時，您會在 Microsoft Azure 中建立 Application Insights 資源。 您在 hello 順序 toosee 在 Azure 入口網站中開啟此資源，並分析 hello 遙測收集從您的應用程式。 hello 資源由*檢測金鑰*(ikey)。 當您安裝 hello Application Insights 封裝 toomonitor 應用程式，您將它設定為與 hello 檢測金鑰，讓它知道 toosend hello 遙測的其中。

您通常會選擇 toouse 不同資源或單一的共用的資源在不同案例中：

* 獨立的不同應用程式 - 為每個應用程式使用不同的資源和 ikey。
* 使用多個元件或角色的一個商務應用程式-[單一共用的資源](app-insights-monitor-multi-role-apps.md)針對所有 hello 元件應用程式。 遙測可以篩選或依 hello cloud_RoleName 屬性。
* 開發、 測試和發行集使用個別的資源和 ikey '的戳記' hello 系統的版本或實際執行階段。
* A | B 測試 - 使用單一資源。 建立 TelemetryInitializer tooadd 識別 hello 變化屬性 toohello 遙測。


## <a name="dynamic-ikey"></a> 動態檢測金鑰

toomake 方便您的生產環境中，階段之間移動的 toochange hello ikey hello 的程式碼在設定程式碼，而不是 hello 組態檔中。

在初始設定方法，例如 global.aspx.cs ASP.NET 服務中設定 hello 機碼：

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

在此範例中，hello 不同資源的 hello ikeys 會放置在不同版本的 hello web 組態檔。 正在交換 hello web 的組態檔的可執行的 hello 發行指令碼一部分-將會交換 hello 目標資源。

### <a name="web-pages"></a>網頁
hello iKey 也會在您的應用程式中的網頁，hello [hello 快速入門刀鋒視窗中取得的指令碼](app-insights-javascript.md)。 常值到 hello 指令碼中編碼，並不會從 hello 伺服器狀態產生它。 例如，在 ASP.NET 應用程式中：

*Razor 中的 JavaScript*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>建立其他 Application Insights 資源
tooseparate 遙測不同的應用程式元件，或針對不同的戳記 （開發/測試/生產環境） 的 hello 相同元件，則您將必須 toocreate 新的 Application Insights 資源。

在 hello [portal.azure.com](https://portal.azure.com)，加入 Application Insights 資源：

![按一下 新增，然後按一下Application Insights](./media/app-insights-separate-resources/01-new.png)

* **應用程式類型**會影響您在 hello 概觀刀鋒視窗，然後 hello 中可用的屬性上看到[度量總管](app-insights-metrics-explorer.md)。 如果您沒有看到您的應用程式的類型，請選擇其中一種 web 網頁的 hello web 類型。
* **資源群組** 可讓您輕鬆管理屬性，例如 [存取控制](app-insights-resources-roles-access-control.md)。 您可以對開發、測試和生產環境使用不同的資源群組。
* **訂用帳戶** 是您在 Azure 中的付款帳戶。
* **位置** 是我們保留您資料的地方。 目前無法變更位置。 
* **新增 toodashboard**可以在 Azure 首頁上放置快速存取磚以取得您的資源。 

建立 hello 資源需要花幾秒鐘的時間。 完成時，您會看到警示。

(您可以撰寫[PowerShell 指令碼](app-insights-powershell-script-create-resource.md)toocreate 資源自動。)

### <a name="getting-hello-instrumentation-key"></a>取得 hello 檢測金鑰
hello 檢測金鑰會識別您所建立的 hello 資源。 

![按一下 Essentials，請按一下 hello 檢測金鑰 CTRL + C](./media/app-insights-separate-resources/02-props.png)

您需要 hello 檢測金鑰的所有 hello 資源 toowhich 您的應用程式會傳送資料。

## <a name="filter-on-build-number"></a>篩選組建編號
當您發行應用程式的新版本時，您會想從不同的組建 toobe 無法 tooseparate hello 遙測。

您可以設定 hello 應用程式版本屬性，以便您可以篩選[搜尋](app-insights-diagnostic-search.md)和[度量總管](app-insights-metrics-explorer.md)結果。

![針對屬性進行篩選](./media/app-insights-separate-resources/050-filter.png)

有數種不同的方法設定的 hello 應用程式版本屬性。

* 直接設定：

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* 包裝在該行[遙測初始設定式](app-insights-api-custom-events-metrics.md#defaults)tooensure 一致地設定所有 TelemetryClient 執行個體。
* [ASP.NET]集合中的 hello 版本`BuildInfo.config`。 hello web 模組將挑選 hello hello BuildLabel 節點版本。 在您的專案中包含這個檔案，並記住 tooset hello 永遠複製屬性在 [方案總管]。

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] 在 MSBuild 中自動產生 BuildInfo.config。 toodo，加入幾行 tooyour`.csproj`檔案：

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    這會產生檔案，稱為*yourProjectName*。BuildInfo.config。 hello 發行程序重新命名它 tooBuildInfo.config。

    當您使用 Visual Studio 建置 hello 組建標籤會包含預留位置 (AutoGen_...)。 但是，MSBuild 以建立時，其中已填入 hello 正確的版本號碼。

    tooallow MSBuild toogenerate 版本號碼，將版本設定 hello 喜歡`1.0.*`AssemblyReference.cs 中

## <a name="version-and-release-tracking"></a>版本和版次追蹤
tootrack hello 應用程式版本，請確定`buildinfo.config`由您的 Microsoft Build Engine 程序所產生。 在您的 .csproj 檔案中加入：  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

當有 hello 組建資訊時，hello Application Insights web 模組自動加入**應用程式版本**做為屬性 tooevery 項目的遙測資料。 可讓您 toofilter 版本執行時[診斷搜尋](app-insights-diagnostic-search.md)，或當您[瀏覽度量](app-insights-metrics-explorer.md)。

不過，請注意，hello 組建版本號碼會產生僅供 Microsoft Build Engine，不是由 hello 開發人員建置 Visual Studio 中的 hello。

### <a name="release-annotations"></a>版本註解
如果您使用 Visual Studio Team Services 時，您可以[取得註解標記](app-insights-annotations.md)加入 tooyour 圖表，每當您發行新版本。 hello 下列影像顯示此標記的顯示方式。

![圖表上版本註解範例的螢幕擷取畫面](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>後續步驟

* [多個角色的共用資源](app-insights-monitor-multi-role-apps.md)
* [建立遙測初始設定式 toodistinguish A |B 變異](app-insights-api-filtering-sampling.md#add-properties)
