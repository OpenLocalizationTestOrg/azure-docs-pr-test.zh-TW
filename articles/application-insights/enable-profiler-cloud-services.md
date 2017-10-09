---
title: "雲端服務資源上的 Azure 應用程式 Insights Profiler aaaEnable |Microsoft 文件"
description: "了解 tooset 向上 hello 程式碼剖析工具的 ASP.NET 應用程式裝載 Azure 雲端服務資源的方式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: b9ac3bca513bf4518f44780389a9f2945f6ccc98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a>在 Azure 雲端服務資源上啟用 Application Insights Profiler

本逐步解說示範如何 tooenable Azure 應用程式 Insights 分析工具在 ASP.NET 應用程式上的裝載的 Azure 雲端服務資源。 hello 範例包括 Azure 虛擬機器、 虛擬機器擴展集和 Azure Service Fabric 支援。 hello 範例全都依賴支援 hello Azure Resource Manager 部署模型的範本。 如需有關 hello 部署模型的詳細資訊，請檢閱[Azure Resource Manager vs 傳統部署： 了解部署模型及 hello 資源的狀態](/azure-resource-manager/resource-manager-deployment-model)。

## <a name="overview"></a>概觀

hello 下列圖表說明 Azure 雲端服務資源的 hello 程式碼剖析工具的運作方式。 其使用 Azure 虛擬機器作為範例。

![概觀](./media/enable-profiler-compute/overview.png)toocollect 資訊進行處理，以及顯示 hello Azure 入口網站，您必須安裝 hello Azure 雲端服務資源的 hello 診斷代理程式元件。 hello hello 逐步解說的其餘部分指引如何 tooinstall 及設定 hello 診斷代理程式 tooenable Insights 程式碼剖析工具應用程式。

## <a name="prerequisites-for-hello-walkthrough"></a>Hello 逐步解說的必要條件

* 部署資源管理員範本 hello Vm 上安裝 hello 程式碼剖析工具代理程式 ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) 或調整規模設定 ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json))。

* 啟用 Application Insights 執行個體以進行分析。 如需指示，請參閱[啟用 hello 設定檔](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler)。

* .NET framework 4.6.1 或更新版本安裝在 hello 目標 Azure 雲端服務資源。

## <a name="create-a-resource-group-in-your-azure-subscription"></a>在您的 Azure 訂用帳戶中建立資源群組
hello 下列範例將示範如何 toocreate 資源群組使用 PowerShell 指令碼：

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a>在 hello 資源群組中建立 Application Insights 資源
在 hello **Application Insights**刀鋒視窗中，輸入您為資源，hello 資訊，如本範例所示： 

![[Application Insights] 刀鋒視窗](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a>套用 hello Azure Resource Manager 範本中的 Application Insights 檢測金鑰

1. 如果您尚未下載 hello 範本，從下載[GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)。

2. 尋找 hello Application Insights 金鑰。
   
   ![Hello 金鑰的位置](./media/enable-profiler-compute/copyaikey.png)

3. 取代 hello 範本的值。
   
   ![取代 hello 範本中的值](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a>建立 Azure VM toohost hello web 應用程式
1. 建立安全字串 toosave hello 密碼。

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. 部署 hello Azure Resource Manager 範本。

   變更 hello PowerShell 主控台 toohello 資料夾包含資源管理員範本中的 hello 目錄。 toodeploy hello 範本，執行下列命令的 hello:

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

Hello 指令碼順利執行之後，您應該尋找名為的 VM **MyWindowsVM**資源群組中。

## <a name="configure-web-deploy-on-hello-vm"></a>Hello VM 上設定 Web Deploy
確定已在您的 VM 上啟用 Web Deploy，如此便可從 Visual Studio 發佈您的 Web 應用程式。

透過 WebPI，手動在 VM 上的 Web Deploy tooinstall 看到[安裝和設定 Web Deploy IIS 8.0 或稍後](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later)。 如需如何 tooautomate 安裝 Web Deploy 利用 Azure 資源管理員範本，請參閱[建立、 設定和部署 web 應用程式 tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/)。

如果您要部署 ASP.NET MVC 應用程式，請移至 tooServer 管理員中，選取**新增角色及功能** > **網頁伺服器 (IIS)** > **Web 伺服器**  > **應用程式開發**，並在伺服器上啟用 ASP.NET 4.5。

![新增 ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a>安裝 hello Azure Application Insights SDK 為您的專案
1. 在 Visual Studio 中，開啟您的 ASP.NET Web 應用程式。

2. Hello 專案上按一下滑鼠右鍵，然後選取**新增** > **已連接服務**。

3. 選取 [Application Insights] 。

4. 在 hello 頁面上，依照 hello 指示。 選取您稍早建立的 hello Application Insights 資源。

5. 選取 hello**註冊** 按鈕。


## <a name="publish-hello-project-tooan-azure-vm"></a>發行 hello 專案 tooan Azure VM
有數種方式 toopublish 應用程式 tooan Azure VM。 其中一個方法是 Visual Studio 2017 toouse。

1. Hello 專案上按一下滑鼠右鍵，然後選取**發行**。

2. 選取**Microsoft Azure 虛擬機器**hello 為發行目標，並遵循 hello 步驟。

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. 針對您的應用程式執行負載測試。 您應該在 hello Application Insights 執行個體的入口網站網頁上會看到結果。


## <a name="enable-hello-profiler"></a>啟用 hello 程式碼剖析工具
1. 移 tooyour Application Insights**效能**刀鋒視窗，然後選取**設定**。
   
   ![設定圖示](./media/enable-profiler-compute/enableprofiler1.png)
 
2. 選取 [啟用分析工具]。
   
   ![啟用分析工具圖示](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a>加入效能測試 tooyour 應用程式
讓我們可以收集應用程式 Insights 分析工具中顯示一些範例資料 toobe，請遵循下列步驟：

1. 瀏覽您稍早建立的 toohello Application Insights 資源。 

2. 移 toohello**可用性**刀鋒視窗並加入傳送 web 要求 tooyour 應用程式 URL 的效能測試。 

   ![新增效能測試](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a>檢視效能資料

1. 等待 10-15 分鐘，讓 hello profiler toocollect 和分析 hello 資料。 

2. 移 toohello**效能**刀鋒視窗，在您的 Application Insights 資源和在負載之下，如何執行您的應用程式的檢視。

   ![檢視效能](./media/enable-profiler-compute/aiperformance.png)

3. 在選取的 hello 圖示**範例**tooopen hello**追蹤檢視**刀鋒視窗。

   ![開啟刀鋒視窗中檢視追蹤 hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a>使用現有的範本

1. 部署範本中，找出 hello Azure 診斷資源宣告。
   
   如果您不需要宣告，您可以建立一個 hello 下列範例中的 hello 宣告類似。 您可以更新從 hello hello 範本[Azure 資源總管網站](https://resources.azure.com)。

2. 從變更 hello 發行者`Microsoft.Azure.Diagnostics`太`AIP.Diagnostics.Test`。

3. 如需 `typeHandlerVersion`，請使用 `0.0`。

4. 請確定`autoUpgradeMinorVersion`設定得`true`。

5. 新增新的 hello`ApplicationInsightsProfiler`接收器執行個體在 hello`WadCfg`設定物件，如下列範例中的 hello 中所示：

```
"resources": [
        {
          "type": "extensions",
          "name": "Microsoft.Insights.VMDiagnosticsSettings",
          "apiVersion": "2016-03-30",
          "properties": {
            "publisher": "AIP.Diagnostics.Test",
            "type": "IaaSDiagnostics",
            "typeHandlerVersion": "0.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "WadCfg": {
                "SinksConfig": {
                  "Sink": [
                    {
                      "name": "Give a descriptive short name. E.g.: MyApplicationInsightsProfilerSink",
                      "ApplicationInsightsProfiler": "Enter hello Application Insights instance instrumentation key guid here"
                    }
                  ]
                },
                "DiagnosticMonitorConfiguration": {
                    ...
                }
                ...
              }
              ...
            }
            ...
          }
          ...
]
```

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a>啟用虛擬機器擴展集上的 hello 程式碼剖析工具
toosee tooenable hello 分析工具時，如何下載 hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)範本。 適用於的 hello 中的 VM 範本 toohello 診斷延伸模組資源 hello 虛擬機器規模集的相同變更。

請確定 hello 規模集中的每個執行個體具有 toohello 存取網際網路。 hello 程式碼剖析工具代理程式就可以傳送 hello 收集範例 tooApplication Insights 供顯示及分析。

## <a name="enable-hello-profiler-on-service-fabric-applications"></a>啟用 Service Fabric 應用程式上的 hello 程式碼剖析工具
1. 佈建 hello Service Fabric 叢集 toohave hello Azure 診斷擴充功能安裝 hello 程式碼剖析工具代理程式。

2. 安裝 hello 專案中的 hello Application Insights SDK 和設定 hello Application Insights 金鑰。

3. 新增應用程式程式碼 tooinstrument 遙測。

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a>佈建 hello Service Fabric 叢集 toohave hello hello 程式碼剖析工具代理程式所安裝的 Azure 診斷擴充功能
Service Fabric 叢集不一定是安全的。 您可以設定一個閘道叢集 toobe 不安全，它不需要憑證才能進行存取。 裝載商務邏輯和資料的叢集應該是安全的。 您可以啟用 hello 分析工具在安全和非安全 Service Fabric 叢集上。 本逐步解說使用不安全的叢集範例 tooexplain 做哪些變更都需要的 tooenable hello 分析工具。 您可以佈建在 hello 的安全叢集相同的方式。

1. 下載 [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json)。 VM 和虛擬機器擴展集的做法一樣，使用您的 Application Insights 金鑰來取代 `Application_Insights_Key`：

   ```
   "publisher": "AIP.Diagnostics.Test",
                 "settings": {
                   "WadCfg": {
                     "SinksConfig": {
                       "Sink": [
                         {
                           "name": "MyApplicationInsightsProfilerSinkVMSS",
                           "ApplicationInsightsProfiler": "[Application_Insights_Key]"
                         }
                       ]
                     },
   ```

2. 使用 PowerShell 指令碼部署 hello 範本：

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a>安裝 hello 專案中的 hello Application Insights SDK 和設定 hello Application Insights 金鑰
從 hello 安裝 Application Insights SDK hello [NuGet 封裝](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)。 確定您已安裝穩定版本 2.3 或更新版本。 

如需在您的專案中設定 Application Insights 的相關資訊，請參閱[將 Service Fabric 與 Application Insights 搭配使用](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md)。

### <a name="add-application-code-tooinstrument-telemetry"></a>新增應用程式程式碼 tooinstrument 遙測
1. 對任何您想 tooinstrument 程式碼，加入 using 陳述式前後。 

   在下列範例的 hello，hello`RunAsync`方法是執行一些工作，而且 hello`telemetryClient`類別會在啟動之後，會擷取 hello 遙測。 hello 事件跨越 hello 應用程式需要唯一的名稱。

   ```
   protected override async Task RunAsync(CancellationToken cancellationToken)
       {
           // TODO: Replace hello following sample code with your own logic
           //       or remove this RunAsync override if it's not needed in your service.

           while (true)
           {
               using( var operation = telemetryClient.StartOperation<RequestTelemetry>("[Insert_Event_Unique_Name]"))
               {
                   cancellationToken.ThrowIfCancellationRequested();

                   ++this.iterations;

                   ServiceEventSource.Current.ServiceMessage(this.Context, "Working-{0}", this.iterations);

                   await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
               }

           }
       }
   ```

2. 部署您的應用程式 toohello Service Fabric 叢集。 如 hello 應用程式 toorun 等候 10 分鐘。 更好的效果，您可以在 hello 應用程式執行負載測試。 移 toohello Application Insights 入口網站的**效能**刀鋒視窗中，而且您應該會看到顯示程式碼剖析追蹤的範例。

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a>後續步驟

- 在[分析工具的疑難排解](app-insights-profiler.md#troubleshooting)中尋找針對分析工具問題進行疑難排解的說明。

- 如需詳細資訊中的 hello 分析工具[應用程式 Insights Profiler](app-insights-profiler.md)。
