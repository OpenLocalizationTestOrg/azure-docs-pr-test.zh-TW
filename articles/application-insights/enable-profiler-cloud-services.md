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
# <a name="enable-application-insights-profiler-on-an-azure-cloud-services-resource"></a><span data-ttu-id="289c6-103">在 Azure 雲端服務資源上啟用 Application Insights Profiler</span><span class="sxs-lookup"><span data-stu-id="289c6-103">Enable Application Insights Profiler on an Azure Cloud Services resource</span></span>

<span data-ttu-id="289c6-104">本逐步解說示範如何 tooenable Azure 應用程式 Insights 分析工具在 ASP.NET 應用程式上的裝載的 Azure 雲端服務資源。</span><span class="sxs-lookup"><span data-stu-id="289c6-104">This walkthrough demonstrates how tooenable Azure Application Insights Profiler on an ASP.NET application hosted by an Azure Cloud Services resource.</span></span> <span data-ttu-id="289c6-105">hello 範例包括 Azure 虛擬機器、 虛擬機器擴展集和 Azure Service Fabric 支援。</span><span class="sxs-lookup"><span data-stu-id="289c6-105">hello examples include support for Azure Virtual Machines, virtual machine scale sets, and Azure Service Fabric.</span></span> <span data-ttu-id="289c6-106">hello 範例全都依賴支援 hello Azure Resource Manager 部署模型的範本。</span><span class="sxs-lookup"><span data-stu-id="289c6-106">hello examples all rely on templates that support hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="289c6-107">如需有關 hello 部署模型的詳細資訊，請檢閱[Azure Resource Manager vs 傳統部署： 了解部署模型及 hello 資源的狀態](/azure-resource-manager/resource-manager-deployment-model)。</span><span class="sxs-lookup"><span data-stu-id="289c6-107">For more information about hello deployment model, review [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](/azure-resource-manager/resource-manager-deployment-model).</span></span>

## <a name="overview"></a><span data-ttu-id="289c6-108">概觀</span><span class="sxs-lookup"><span data-stu-id="289c6-108">Overview</span></span>

<span data-ttu-id="289c6-109">hello 下列圖表說明 Azure 雲端服務資源的 hello 程式碼剖析工具的運作方式。</span><span class="sxs-lookup"><span data-stu-id="289c6-109">hello following diagram illustrates how hello profiler works for Azure Cloud Services resources.</span></span> <span data-ttu-id="289c6-110">其使用 Azure 虛擬機器作為範例。</span><span class="sxs-lookup"><span data-stu-id="289c6-110">It uses an Azure virtual machine as an example.</span></span>

<span data-ttu-id="289c6-111">![概觀](./media/enable-profiler-compute/overview.png)toocollect 資訊進行處理，以及顯示 hello Azure 入口網站，您必須安裝 hello Azure 雲端服務資源的 hello 診斷代理程式元件。</span><span class="sxs-lookup"><span data-stu-id="289c6-111">![Overview](./media/enable-profiler-compute/overview.png) toocollect information for processing and display on hello Azure portal, you must install hello Diagnostics Agent component for hello Azure Cloud Services resources.</span></span> <span data-ttu-id="289c6-112">hello hello 逐步解說的其餘部分指引如何 tooinstall 及設定 hello 診斷代理程式 tooenable Insights 程式碼剖析工具應用程式。</span><span class="sxs-lookup"><span data-stu-id="289c6-112">hello rest of hello walkthrough provides guidance on how tooinstall and configure hello Diagnostics Agent tooenable Application Insights Profiler.</span></span>

## <a name="prerequisites-for-hello-walkthrough"></a><span data-ttu-id="289c6-113">Hello 逐步解說的必要條件</span><span class="sxs-lookup"><span data-stu-id="289c6-113">Prerequisites for hello walkthrough</span></span>

* <span data-ttu-id="289c6-114">部署資源管理員範本 hello Vm 上安裝 hello 程式碼剖析工具代理程式 ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) 或調整規模設定 ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json))。</span><span class="sxs-lookup"><span data-stu-id="289c6-114">A deployment Resource Manager template that installs hello profiler agents on hello VMs ([WindowsVirtualMachine.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)) or scale sets ([WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)).</span></span>

* <span data-ttu-id="289c6-115">啟用 Application Insights 執行個體以進行分析。</span><span class="sxs-lookup"><span data-stu-id="289c6-115">An Application Insights instance enabled for profiling.</span></span> <span data-ttu-id="289c6-116">如需指示，請參閱[啟用 hello 設定檔](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler)。</span><span class="sxs-lookup"><span data-stu-id="289c6-116">For instructions, see [Enable hello profile](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-profiler#enable-the-profiler).</span></span>

* <span data-ttu-id="289c6-117">.NET framework 4.6.1 或更新版本安裝在 hello 目標 Azure 雲端服務資源。</span><span class="sxs-lookup"><span data-stu-id="289c6-117">.NET Framework 4.6.1 or later installed on hello target Azure Cloud Services resource.</span></span>

## <a name="create-a-resource-group-in-your-azure-subscription"></a><span data-ttu-id="289c6-118">在您的 Azure 訂用帳戶中建立資源群組</span><span class="sxs-lookup"><span data-stu-id="289c6-118">Create a resource group in your Azure subscription</span></span>
<span data-ttu-id="289c6-119">hello 下列範例將示範如何 toocreate 資源群組使用 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="289c6-119">hello following example demonstrates how toocreate a resource group by using a PowerShell script:</span></span>

```
New-AzureRmResourceGroup -Name "Replace_With_Resource_Group_Name" -Location "Replace_With_Resource_Group_Location"
```

## <a name="create-an-application-insights-resource-in-hello-resource-group"></a><span data-ttu-id="289c6-120">在 hello 資源群組中建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="289c6-120">Create an Application Insights resource in hello resource group</span></span>
<span data-ttu-id="289c6-121">在 hello **Application Insights**刀鋒視窗中，輸入您為資源，hello 資訊，如本範例所示：</span><span class="sxs-lookup"><span data-stu-id="289c6-121">On hello **Application Insights** blade, enter hello information for your resource, as shown in this example:</span></span> 

![[Application Insights] 刀鋒視窗](./media/enable-profiler-compute/createai.png)

## <a name="apply-an-application-insights-instrumentation-key-in-hello-azure-resource-manager-template"></a><span data-ttu-id="289c6-123">套用 hello Azure Resource Manager 範本中的 Application Insights 檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="289c6-123">Apply an Application Insights instrumentation key in hello Azure Resource Manager template</span></span>

1. <span data-ttu-id="289c6-124">如果您尚未下載 hello 範本，從下載[GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json)。</span><span class="sxs-lookup"><span data-stu-id="289c6-124">If you haven't downloaded hello template yet, download it from [GitHub](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachine.json).</span></span>

2. <span data-ttu-id="289c6-125">尋找 hello Application Insights 金鑰。</span><span class="sxs-lookup"><span data-stu-id="289c6-125">Find hello Application Insights key.</span></span>
   
   ![Hello 金鑰的位置](./media/enable-profiler-compute/copyaikey.png)

3. <span data-ttu-id="289c6-127">取代 hello 範本的值。</span><span class="sxs-lookup"><span data-stu-id="289c6-127">Replace hello template value.</span></span>
   
   ![取代 hello 範本中的值](./media/enable-profiler-compute/copyaikeytotemplate.png)

## <a name="create-an-azure-vm-toohost-hello-web-application"></a><span data-ttu-id="289c6-129">建立 Azure VM toohost hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="289c6-129">Create an Azure VM toohost hello web application</span></span>
1. <span data-ttu-id="289c6-130">建立安全字串 toosave hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="289c6-130">Create a secure string toosave hello password.</span></span>

   ```
   $password = ConvertTo-SecureString -String "Replace_With_Your_Password" -AsPlainText -Force
   ```

2. <span data-ttu-id="289c6-131">部署 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="289c6-131">Deploy hello Azure Resource Manager template.</span></span>

   <span data-ttu-id="289c6-132">變更 hello PowerShell 主控台 toohello 資料夾包含資源管理員範本中的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="289c6-132">Change hello directory in hello PowerShell console toohello folder that contains your Resource Manager template.</span></span> <span data-ttu-id="289c6-133">toodeploy hello 範本，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="289c6-133">toodeploy hello template, run hello following command:</span></span>

   ```
   New-AzureRmResourceGroupDeployment -ResourceGroupName "Replace_With_Resource_Group_Name" -TemplateFile .\WindowsVirtualMachine.json -adminUsername "Replace_With_your_user_name" -adminPassword $password -dnsNameForPublicIP "Replace_WIth_your_DNS_Name" -Verbose
   ```

<span data-ttu-id="289c6-134">Hello 指令碼順利執行之後，您應該尋找名為的 VM **MyWindowsVM**資源群組中。</span><span class="sxs-lookup"><span data-stu-id="289c6-134">After hello script runs successfully, you should find a VM named **MyWindowsVM** in your resource group.</span></span>

## <a name="configure-web-deploy-on-hello-vm"></a><span data-ttu-id="289c6-135">Hello VM 上設定 Web Deploy</span><span class="sxs-lookup"><span data-stu-id="289c6-135">Configure Web Deploy on hello VM</span></span>
<span data-ttu-id="289c6-136">確定已在您的 VM 上啟用 Web Deploy，如此便可從 Visual Studio 發佈您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="289c6-136">Make sure that Web Deploy is enabled on your VM so you can publish your web application from Visual Studio.</span></span>

<span data-ttu-id="289c6-137">透過 WebPI，手動在 VM 上的 Web Deploy tooinstall 看到[安裝和設定 Web Deploy IIS 8.0 或稍後](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later)。</span><span class="sxs-lookup"><span data-stu-id="289c6-137">tooinstall Web Deploy on a VM manually via WebPI, see [Installing and Configuring Web Deploy on IIS 8.0 or Later](https://docs.microsoft.com/en-us/iis/install/installing-publishing-technologies/installing-and-configuring-web-deploy-on-iis-80-or-later).</span></span> <span data-ttu-id="289c6-138">如需如何 tooautomate 安裝 Web Deploy 利用 Azure 資源管理員範本，請參閱[建立、 設定和部署 web 應用程式 tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/)。</span><span class="sxs-lookup"><span data-stu-id="289c6-138">For an example of how tooautomate installing Web Deploy by using an Azure Resource Manager template, see [Create, configure, and deploy a web application tooan Azure VM](https://azure.microsoft.com/en-us/resources/templates/201-web-app-vm-dsc/).</span></span>

<span data-ttu-id="289c6-139">如果您要部署 ASP.NET MVC 應用程式，請移至 tooServer 管理員中，選取**新增角色及功能** > **網頁伺服器 (IIS)** > **Web 伺服器**  > **應用程式開發**，並在伺服器上啟用 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="289c6-139">If you are deploying an ASP.NET MVC application, go tooServer Manager, select **Add Roles and Features** > **Web Server (IIS)** > **Web Server** > **Application Development**, and enable ASP.NET 4.5 on your server.</span></span>

![新增 ASP.NET](./media/enable-profiler-compute/addaspnet45.png)

## <a name="install-hello-azure-application-insights-sdk-for-your-project"></a><span data-ttu-id="289c6-141">安裝 hello Azure Application Insights SDK 為您的專案</span><span class="sxs-lookup"><span data-stu-id="289c6-141">Install hello Azure Application Insights SDK for your project</span></span>
1. <span data-ttu-id="289c6-142">在 Visual Studio 中，開啟您的 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="289c6-142">Open your ASP.NET web application in Visual Studio.</span></span>

2. <span data-ttu-id="289c6-143">Hello 專案上按一下滑鼠右鍵，然後選取**新增** > **已連接服務**。</span><span class="sxs-lookup"><span data-stu-id="289c6-143">Right-click hello project and select **Add** > **Connected Services**.</span></span>

3. <span data-ttu-id="289c6-144">選取 [Application Insights] 。</span><span class="sxs-lookup"><span data-stu-id="289c6-144">Select **Application Insights**.</span></span>

4. <span data-ttu-id="289c6-145">在 hello 頁面上，依照 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="289c6-145">Follow hello instructions on hello page.</span></span> <span data-ttu-id="289c6-146">選取您稍早建立的 hello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="289c6-146">Select hello Application Insights resource that you created earlier.</span></span>

5. <span data-ttu-id="289c6-147">選取 hello**註冊** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="289c6-147">Select hello **Register** button.</span></span>


## <a name="publish-hello-project-tooan-azure-vm"></a><span data-ttu-id="289c6-148">發行 hello 專案 tooan Azure VM</span><span class="sxs-lookup"><span data-stu-id="289c6-148">Publish hello project tooan Azure VM</span></span>
<span data-ttu-id="289c6-149">有數種方式 toopublish 應用程式 tooan Azure VM。</span><span class="sxs-lookup"><span data-stu-id="289c6-149">There are several ways toopublish an application tooan Azure VM.</span></span> <span data-ttu-id="289c6-150">其中一個方法是 Visual Studio 2017 toouse。</span><span class="sxs-lookup"><span data-stu-id="289c6-150">One way is toouse Visual Studio 2017.</span></span>

1. <span data-ttu-id="289c6-151">Hello 專案上按一下滑鼠右鍵，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="289c6-151">Right-click hello project and select **Publish**.</span></span>

2. <span data-ttu-id="289c6-152">選取**Microsoft Azure 虛擬機器**hello 為發行目標，並遵循 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="289c6-152">Select **Microsoft Azure Virtual Machines** as hello publish target and follow hello steps.</span></span>

   ![Publish-FromVS](./media/enable-profiler-compute/publishtoVM.png)

3. <span data-ttu-id="289c6-154">針對您的應用程式執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="289c6-154">Run a load test against your application.</span></span> <span data-ttu-id="289c6-155">您應該在 hello Application Insights 執行個體的入口網站網頁上會看到結果。</span><span class="sxs-lookup"><span data-stu-id="289c6-155">You should see results on hello Application Insights instance portal webpage.</span></span>


## <a name="enable-hello-profiler"></a><span data-ttu-id="289c6-156">啟用 hello 程式碼剖析工具</span><span class="sxs-lookup"><span data-stu-id="289c6-156">Enable hello profiler</span></span>
1. <span data-ttu-id="289c6-157">移 tooyour Application Insights**效能**刀鋒視窗，然後選取**設定**。</span><span class="sxs-lookup"><span data-stu-id="289c6-157">Go tooyour Application Insights **Performance** blade and select **Configure**.</span></span>
   
   ![設定圖示](./media/enable-profiler-compute/enableprofiler1.png)
 
2. <span data-ttu-id="289c6-159">選取 [啟用分析工具]。</span><span class="sxs-lookup"><span data-stu-id="289c6-159">Select **Enable Profiler**.</span></span>
   
   ![啟用分析工具圖示](./media/enable-profiler-compute/enableprofiler2.png)

## <a name="add-a-performance-test-tooyour-application"></a><span data-ttu-id="289c6-161">加入效能測試 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="289c6-161">Add a performance test tooyour application</span></span>
<span data-ttu-id="289c6-162">讓我們可以收集應用程式 Insights 分析工具中顯示一些範例資料 toobe，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="289c6-162">Follow these steps so we can collect some sample data toobe displayed in Application Insights Profiler:</span></span>

1. <span data-ttu-id="289c6-163">瀏覽您稍早建立的 toohello Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="289c6-163">Browse toohello Application Insights resource that you created earlier.</span></span> 

2. <span data-ttu-id="289c6-164">移 toohello**可用性**刀鋒視窗並加入傳送 web 要求 tooyour 應用程式 URL 的效能測試。</span><span class="sxs-lookup"><span data-stu-id="289c6-164">Go toohello **Availability** blade and add a performance test that sends web requests tooyour application URL.</span></span> 

   ![新增效能測試](./media/enable-profiler-compute/AvailabilityTest.png)

## <a name="view-your-performance-data"></a><span data-ttu-id="289c6-166">檢視效能資料</span><span class="sxs-lookup"><span data-stu-id="289c6-166">View your performance data</span></span>

1. <span data-ttu-id="289c6-167">等待 10-15 分鐘，讓 hello profiler toocollect 和分析 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="289c6-167">Wait 10-15 minutes for hello profiler toocollect and analyze hello data.</span></span> 

2. <span data-ttu-id="289c6-168">移 toohello**效能**刀鋒視窗，在您的 Application Insights 資源和在負載之下，如何執行您的應用程式的檢視。</span><span class="sxs-lookup"><span data-stu-id="289c6-168">Go toohello **Performance** blade in your Application Insights resource and view how your application is performing when it's under load.</span></span>

   ![檢視效能](./media/enable-profiler-compute/aiperformance.png)

3. <span data-ttu-id="289c6-170">在選取的 hello 圖示**範例**tooopen hello**追蹤檢視**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="289c6-170">Select hello icon under **Examples** tooopen hello **Trace View** blade.</span></span>

   ![開啟刀鋒視窗中檢視追蹤 hello](./media/enable-profiler-compute/traceview.png)


## <a name="work-with-an-existing-template"></a><span data-ttu-id="289c6-172">使用現有的範本</span><span class="sxs-lookup"><span data-stu-id="289c6-172">Work with an existing template</span></span>

1. <span data-ttu-id="289c6-173">部署範本中，找出 hello Azure 診斷資源宣告。</span><span class="sxs-lookup"><span data-stu-id="289c6-173">Locate hello Azure Diagnostics resource declaration in your deployment template.</span></span>
   
   <span data-ttu-id="289c6-174">如果您不需要宣告，您可以建立一個 hello 下列範例中的 hello 宣告類似。</span><span class="sxs-lookup"><span data-stu-id="289c6-174">If you don't have a declaration, you can create one that resembles hello declaration in hello following example.</span></span> <span data-ttu-id="289c6-175">您可以更新從 hello hello 範本[Azure 資源總管網站](https://resources.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="289c6-175">You can update hello template from hello [Azure Resource Explorer website](https://resources.azure.com).</span></span>

2. <span data-ttu-id="289c6-176">從變更 hello 發行者`Microsoft.Azure.Diagnostics`太`AIP.Diagnostics.Test`。</span><span class="sxs-lookup"><span data-stu-id="289c6-176">Change hello publisher from `Microsoft.Azure.Diagnostics` too`AIP.Diagnostics.Test`.</span></span>

3. <span data-ttu-id="289c6-177">如需 `typeHandlerVersion`，請使用 `0.0`。</span><span class="sxs-lookup"><span data-stu-id="289c6-177">For `typeHandlerVersion`, use `0.0`.</span></span>

4. <span data-ttu-id="289c6-178">請確定`autoUpgradeMinorVersion`設定得`true`。</span><span class="sxs-lookup"><span data-stu-id="289c6-178">Make sure that `autoUpgradeMinorVersion` is set too`true`.</span></span>

5. <span data-ttu-id="289c6-179">新增新的 hello`ApplicationInsightsProfiler`接收器執行個體在 hello`WadCfg`設定物件，如下列範例中的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="289c6-179">Add hello new `ApplicationInsightsProfiler` sink instance in hello `WadCfg` settings object, as shown in hello following example:</span></span>

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

## <a name="enable-hello-profiler-on-virtual-machine-scale-sets"></a><span data-ttu-id="289c6-180">啟用虛擬機器擴展集上的 hello 程式碼剖析工具</span><span class="sxs-lookup"><span data-stu-id="289c6-180">Enable hello profiler on virtual machine scale sets</span></span>
<span data-ttu-id="289c6-181">toosee tooenable hello 分析工具時，如何下載 hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json)範本。</span><span class="sxs-lookup"><span data-stu-id="289c6-181">toosee how tooenable hello profiler, download hello [WindowsVirtualMachineScaleSet.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/WindowsVirtualMachineScaleSet.json) template.</span></span> <span data-ttu-id="289c6-182">適用於的 hello 中的 VM 範本 toohello 診斷延伸模組資源 hello 虛擬機器規模集的相同變更。</span><span class="sxs-lookup"><span data-stu-id="289c6-182">Apply hello same changes in a VM template toohello diagnostics extension resource for hello virtual machine scale set.</span></span>

<span data-ttu-id="289c6-183">請確定 hello 規模集中的每個執行個體具有 toohello 存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="289c6-183">Make sure that each instance in hello scale set has access toohello internet.</span></span> <span data-ttu-id="289c6-184">hello 程式碼剖析工具代理程式就可以傳送 hello 收集範例 tooApplication Insights 供顯示及分析。</span><span class="sxs-lookup"><span data-stu-id="289c6-184">hello Profiler Agent can then send hello collected samples tooApplication Insights for display and analysis.</span></span>

## <a name="enable-hello-profiler-on-service-fabric-applications"></a><span data-ttu-id="289c6-185">啟用 Service Fabric 應用程式上的 hello 程式碼剖析工具</span><span class="sxs-lookup"><span data-stu-id="289c6-185">Enable hello profiler on Service Fabric applications</span></span>
1. <span data-ttu-id="289c6-186">佈建 hello Service Fabric 叢集 toohave hello Azure 診斷擴充功能安裝 hello 程式碼剖析工具代理程式。</span><span class="sxs-lookup"><span data-stu-id="289c6-186">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent.</span></span>

2. <span data-ttu-id="289c6-187">安裝 hello 專案中的 hello Application Insights SDK 和設定 hello Application Insights 金鑰。</span><span class="sxs-lookup"><span data-stu-id="289c6-187">Install hello Application Insights SDK in hello project and configure hello Application Insights key.</span></span>

3. <span data-ttu-id="289c6-188">新增應用程式程式碼 tooinstrument 遙測。</span><span class="sxs-lookup"><span data-stu-id="289c6-188">Add application code tooinstrument telemetry.</span></span>

### <a name="provision-hello-service-fabric-cluster-toohave-hello-azure-diagnostics-extension-that-installs-hello-profiler-agent"></a><span data-ttu-id="289c6-189">佈建 hello Service Fabric 叢集 toohave hello hello 程式碼剖析工具代理程式所安裝的 Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="289c6-189">Provision hello Service Fabric cluster toohave hello Azure Diagnostics extension that installs hello Profiler Agent</span></span>
<span data-ttu-id="289c6-190">Service Fabric 叢集不一定是安全的。</span><span class="sxs-lookup"><span data-stu-id="289c6-190">A Service Fabric cluster can be secure or non-secure.</span></span> <span data-ttu-id="289c6-191">您可以設定一個閘道叢集 toobe 不安全，它不需要憑證才能進行存取。</span><span class="sxs-lookup"><span data-stu-id="289c6-191">You can set one gateway cluster toobe non-secure so it doesn't require a certificate for access.</span></span> <span data-ttu-id="289c6-192">裝載商務邏輯和資料的叢集應該是安全的。</span><span class="sxs-lookup"><span data-stu-id="289c6-192">Clusters that host business logic and data should be secure.</span></span> <span data-ttu-id="289c6-193">您可以啟用 hello 分析工具在安全和非安全 Service Fabric 叢集上。</span><span class="sxs-lookup"><span data-stu-id="289c6-193">You can enable hello profiler on both secure and non-secure Service Fabric clusters.</span></span> <span data-ttu-id="289c6-194">本逐步解說使用不安全的叢集範例 tooexplain 做哪些變更都需要的 tooenable hello 分析工具。</span><span class="sxs-lookup"><span data-stu-id="289c6-194">This walkthrough uses a non-secure cluster as an example tooexplain what changes are required tooenable hello profiler.</span></span> <span data-ttu-id="289c6-195">您可以佈建在 hello 的安全叢集相同的方式。</span><span class="sxs-lookup"><span data-stu-id="289c6-195">You can provision a secure cluster in hello same way.</span></span>

1. <span data-ttu-id="289c6-196">下載 [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json)。</span><span class="sxs-lookup"><span data-stu-id="289c6-196">Download [ServiceFabricCluster.json](https://github.com/Azure/azure-docs-json-samples/blob/master/application-insights/ServiceFabricCluster.json).</span></span> <span data-ttu-id="289c6-197">VM 和虛擬機器擴展集的做法一樣，使用您的 Application Insights 金鑰來取代 `Application_Insights_Key`：</span><span class="sxs-lookup"><span data-stu-id="289c6-197">As you did for VMs and virtual machine scale sets, replace `Application_Insights_Key` with your Application Insights key:</span></span>

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

2. <span data-ttu-id="289c6-198">使用 PowerShell 指令碼部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="289c6-198">Deploy hello template by using a PowerShell script:</span></span>

   ```
   Login-AzureRmAccount
   New-AzureRmResourceGroup -Name [Your_Resource_Group_Name] -Location [Your_Resource_Group_Location] -Verbose -Force
   New-AzureRmResourceGroupDeployment -Name [Choose_An_Arbitrary_Name] -ResourceGroupName [Your_Resource_Group_Name] -TemplateFile [Path_To_Your_Template]

   ```

### <a name="install-hello-application-insights-sdk-in-hello-project-and-configure-hello-application-insights-key"></a><span data-ttu-id="289c6-199">安裝 hello 專案中的 hello Application Insights SDK 和設定 hello Application Insights 金鑰</span><span class="sxs-lookup"><span data-stu-id="289c6-199">Install hello Application Insights SDK in hello project and configure hello Application Insights key</span></span>
<span data-ttu-id="289c6-200">從 hello 安裝 Application Insights SDK hello [NuGet 封裝](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/)。</span><span class="sxs-lookup"><span data-stu-id="289c6-200">Install hello Application Insights SDK from hello [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="289c6-201">確定您已安裝穩定版本 2.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="289c6-201">Make sure that you install a stable version, 2.3 or later.</span></span> 

<span data-ttu-id="289c6-202">如需在您的專案中設定 Application Insights 的相關資訊，請參閱[將 Service Fabric 與 Application Insights 搭配使用](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md)。</span><span class="sxs-lookup"><span data-stu-id="289c6-202">For information about configuring Application Insights in your projects, see [Using Service Fabric with Application Insights](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/blob/dev/appinsights/ApplicationInsights.md).</span></span>

### <a name="add-application-code-tooinstrument-telemetry"></a><span data-ttu-id="289c6-203">新增應用程式程式碼 tooinstrument 遙測</span><span class="sxs-lookup"><span data-stu-id="289c6-203">Add application code tooinstrument telemetry</span></span>
1. <span data-ttu-id="289c6-204">對任何您想 tooinstrument 程式碼，加入 using 陳述式前後。</span><span class="sxs-lookup"><span data-stu-id="289c6-204">For any piece of code that you want tooinstrument, add a using statement around it.</span></span> 

   <span data-ttu-id="289c6-205">在下列範例的 hello，hello`RunAsync`方法是執行一些工作，而且 hello`telemetryClient`類別會在啟動之後，會擷取 hello 遙測。</span><span class="sxs-lookup"><span data-stu-id="289c6-205">In hello following  example, hello `RunAsync` method is doing some work, and hello `telemetryClient` class captures hello telemetry after it starts.</span></span> <span data-ttu-id="289c6-206">hello 事件跨越 hello 應用程式需要唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="289c6-206">hello event needs a unique name across hello application.</span></span>

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

2. <span data-ttu-id="289c6-207">部署您的應用程式 toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="289c6-207">Deploy your application toohello Service Fabric cluster.</span></span> <span data-ttu-id="289c6-208">如 hello 應用程式 toorun 等候 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="289c6-208">Wait for hello app toorun for 10 minutes.</span></span> <span data-ttu-id="289c6-209">更好的效果，您可以在 hello 應用程式執行負載測試。</span><span class="sxs-lookup"><span data-stu-id="289c6-209">For better effect, you can run a load test on hello app.</span></span> <span data-ttu-id="289c6-210">移 toohello Application Insights 入口網站的**效能**刀鋒視窗中，而且您應該會看到顯示程式碼剖析追蹤的範例。</span><span class="sxs-lookup"><span data-stu-id="289c6-210">Go toohello Application Insights portal's **Performance** blade, and you should see examples of profiling traces appear.</span></span>

<!---
Commenting out these sections for now
## Enable hello Profiler on Cloud Services applications
[TODO]
## Enable hello Profiler on classic Azure Virtual Machines
[TODO]
## Enable hello Profiler on on-premise servers
[TODO]
--->

## <a name="next-steps"></a><span data-ttu-id="289c6-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="289c6-211">Next steps</span></span>

- <span data-ttu-id="289c6-212">在[分析工具的疑難排解](app-insights-profiler.md#troubleshooting)中尋找針對分析工具問題進行疑難排解的說明。</span><span class="sxs-lookup"><span data-stu-id="289c6-212">Find help with troubleshooting profiler issues in [Profiler troubleshooting](app-insights-profiler.md#troubleshooting).</span></span>

- <span data-ttu-id="289c6-213">如需詳細資訊中的 hello 分析工具[應用程式 Insights Profiler](app-insights-profiler.md)。</span><span class="sxs-lookup"><span data-stu-id="289c6-213">Read more about hello profiler in [Application Insights Profiler](app-insights-profiler.md).</span></span>
