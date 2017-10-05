---
title: "如何搭配雲端服務使用 Azure 診斷 (.NET) | Microsoft Docs"
description: "使用 Azure 診斷從 Azure 雲端服務收集資料，以進行偵錯、測量效能、監視、流量分析等。"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: robb
ms.openlocfilehash: 333d2f26ce043a167fb84858c8327cb39e868ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="8c21c-103">在 Azure 雲端服務中啟用 Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="8c21c-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="8c21c-104">如需有關 Azure 診斷的背景資訊，請參閱 [Azure 診斷概觀](../azure-diagnostics.md) 。</span><span class="sxs-lookup"><span data-stu-id="8c21c-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="8c21c-105">如何在背景工作角色中啟用診斷</span><span class="sxs-lookup"><span data-stu-id="8c21c-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="8c21c-106">本逐步解說說明如何實作 Azure 背景工作角色，該角色使用 .NET EventSource 類別發出遙測資料。</span><span class="sxs-lookup"><span data-stu-id="8c21c-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="8c21c-107">Azure 診斷可用來收集遙測資料，並將資料儲存在 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c21c-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="8c21c-108">建立背景工作角色時，Visual Studio 會自動啟用診斷 1.0 來作為 Azure SDK for .NET 2.4 及更早版本中解決方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="8c21c-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="8c21c-109">下列指示說明建立背景工作角色、從解決方案停用診斷 1.0，以及將診斷 1.2 或 1.3 部署至背景工作角色的程序。</span><span class="sxs-lookup"><span data-stu-id="8c21c-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8c21c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c21c-110">Prerequisites</span></span>
<span data-ttu-id="8c21c-111">本文假設您擁有 Azure 訂用帳戶，並且搭配 Azure SDK 使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8c21c-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="8c21c-112">如果您沒有 Azure 訂用帳戶，可以註冊[免費試用版][Free Trial]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="8c21c-113">請務必[安裝並設定 Azure PowerShell 0.8.7 版或更新版本][Install and configure Azure PowerShell version 0.8.7 or later]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="8c21c-114">步驟 1：建立背景工作角色</span><span class="sxs-lookup"><span data-stu-id="8c21c-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="8c21c-115">啟動 **Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="8c21c-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="8c21c-116">從以 .NET Framework 4.5 為目標的**雲端**範本，建立 **Azure 雲端服務**專案。</span><span class="sxs-lookup"><span data-stu-id="8c21c-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="8c21c-117">將專案命名為 "WadExample" 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="8c21c-118">選取 [ **背景工作角色** ] 並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="8c21c-119">將會建立專案。</span><span class="sxs-lookup"><span data-stu-id="8c21c-119">The project will be created.</span></span>
4. <span data-ttu-id="8c21c-120">在**方案總管**中，按兩下 [WorkerRole1] 屬性檔。</span><span class="sxs-lookup"><span data-stu-id="8c21c-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="8c21c-121">在 [設定] 索引標籤中取消核取 [啟用診斷] 以停用診斷 1.0 (Azure SDK 2.4 和更早版本)。</span><span class="sxs-lookup"><span data-stu-id="8c21c-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="8c21c-122">建置您的解決方案以確認無誤。</span><span class="sxs-lookup"><span data-stu-id="8c21c-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="8c21c-123">步驟 2：實作您的程式碼</span><span class="sxs-lookup"><span data-stu-id="8c21c-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="8c21c-124">以下列程式碼取代 WorkerRole.cs 的內容。</span><span class="sxs-lookup"><span data-stu-id="8c21c-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="8c21c-125">繼承自 [EventSource 類別][EventSource Class]的 SampleEventSourceWriter 類別實作四種記錄方法：**SendEnums**、**MessageMethod**、**SetOther** 和 **HighFreq**。</span><span class="sxs-lookup"><span data-stu-id="8c21c-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="8c21c-126">傳遞至 **WriteEvent** 方法的第一個參數定義個別事件的識別碼。</span><span class="sxs-lookup"><span data-stu-id="8c21c-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="8c21c-127">Run 方法實作一個無限迴圈，每 10 秒呼叫一次在 **SampleEventSourceWriter** 類別中實作的每種記錄方法。</span><span class="sxs-lookup"><span data-stu-id="8c21c-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through the loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="8c21c-128">步驟 3：部署您的背景工作角色</span><span class="sxs-lookup"><span data-stu-id="8c21c-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="8c21c-129">在 [方案總管] 中選取 **WadExample** 專案，然後從 [建置] 功能表選取 [發佈]，以從 Visual Studio 將背景工作角色部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="8c21c-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="8c21c-130">選擇您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c21c-130">Choose your subscription.</span></span>
3. <span data-ttu-id="8c21c-131">在 [Microsoft Azure 發行設定] 對話方塊中，選取 [新建...]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="8c21c-132">在 [建立雲端服務和儲存體帳戶] 對話方塊中，輸入**名稱** (例如 "WadExample") 並選取區域或同質群組。</span><span class="sxs-lookup"><span data-stu-id="8c21c-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="8c21c-133">將 [環境] 設為 [預備]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="8c21c-134">適當地修改其他任何 [設定]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="8c21c-135">部署完成之後，請在 Azure 入口網站中確認您的雲端服務是否處於**執行中**狀態。</span><span class="sxs-lookup"><span data-stu-id="8c21c-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="8c21c-136">步驟 4：建立您的診斷組態檔並安裝擴充功能</span><span class="sxs-lookup"><span data-stu-id="8c21c-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="8c21c-137">執行下列 PowerShell 命令，以下載公用組態檔結構描述定義：</span><span class="sxs-lookup"><span data-stu-id="8c21c-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="8c21c-138">新增 XML 檔案以您**WorkerRole1**專案，以滑鼠右鍵按一下**WorkerRole1**專案，然後選取**新增** -> **新項目...**</span><span class="sxs-lookup"><span data-stu-id="8c21c-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="8c21c-139"> -> [Visual C# 項目] -> [資料] -> [XML 檔案]。</span><span class="sxs-lookup"><span data-stu-id="8c21c-139"> -> **Visual C# items** -> **Data** -> **XML File**.</span></span> <span data-ttu-id="8c21c-140">將檔案命名為 "WadExample.xml"。</span><span class="sxs-lookup"><span data-stu-id="8c21c-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="8c21c-142">將 WadConfig.xsd 與組態檔產生關聯。</span><span class="sxs-lookup"><span data-stu-id="8c21c-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="8c21c-143">確定 WadExample.xml 編輯器視窗是使用中視窗。</span><span class="sxs-lookup"><span data-stu-id="8c21c-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="8c21c-144">按 **F4** 鍵開啟 [屬性] 視窗。</span><span class="sxs-lookup"><span data-stu-id="8c21c-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="8c21c-145">在 [屬性] 視窗中，按一下 [結構描述] 屬性。</span><span class="sxs-lookup"><span data-stu-id="8c21c-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="8c21c-146">按一下 [...]</span><span class="sxs-lookup"><span data-stu-id="8c21c-146">Click the **…**</span></span> <span data-ttu-id="8c21c-147">在 [結構描述] 屬性中。</span><span class="sxs-lookup"><span data-stu-id="8c21c-147">in the **Schemas** property.</span></span> <span data-ttu-id="8c21c-148">按一下 [新增...]</span><span class="sxs-lookup"><span data-stu-id="8c21c-148">Click the **Add…**</span></span> <span data-ttu-id="8c21c-149">按鈕並瀏覽至您儲存 XSD 檔的位置，然後選取檔案 WadConfig.xsd。</span><span class="sxs-lookup"><span data-stu-id="8c21c-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="8c21c-150">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8c21c-150">Click **OK**.</span></span>

4. <span data-ttu-id="8c21c-151">以下列 XML 取代 WadExample.xml 組態檔的內容，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="8c21c-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="8c21c-152">此組態檔可定義兩個要收集的效能計數器：一個用於 CPU 使用率，一個用於記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="8c21c-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="8c21c-153">組態會接著定義四個事件，分別對應至 SampleEventSourceWriter 類別中的方法。</span><span class="sxs-lookup"><span data-stu-id="8c21c-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="8c21c-154">步驟 5：在您的背景工作角色上安裝診斷</span><span class="sxs-lookup"><span data-stu-id="8c21c-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="8c21c-155">用於管理 Web 角色或背景工作角色上之診斷的 PowerShell Cmdlet 為：Set-AzureServiceDiagnosticsExtension、Get-AzureServiceDiagnosticsExtension 和 Remove-AzureServiceDiagnosticsExtension。</span><span class="sxs-lookup"><span data-stu-id="8c21c-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="8c21c-156">開啟 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8c21c-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="8c21c-157">執行指令碼，在您的背景工作角色上安裝診斷 (以 wadexample 儲存體帳戶的儲存體帳戶金鑰取代 *StorageAccountKey*，並以 *WadExample.xml* 檔案的路徑取代 *config_path*)：</span><span class="sxs-lookup"><span data-stu-id="8c21c-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="8c21c-158">步驟 6：查看您的遙測資料</span><span class="sxs-lookup"><span data-stu-id="8c21c-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="8c21c-159">在 Visual Studio 的 [伺服器總管] 中，巡覽至 wadexample 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c21c-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="8c21c-160">在雲端服務執行約 5 分鐘之後，您應該會看到資料表 **WADEnumsTable**、**WADHighFreqTable**、**WADMessageTable**、**WADPerformanceCountersTable** 和 **WADSetOtherTable**。</span><span class="sxs-lookup"><span data-stu-id="8c21c-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="8c21c-161">按兩下其中一份資料表以檢視收集的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="8c21c-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="8c21c-163">組態檔結構描述</span><span class="sxs-lookup"><span data-stu-id="8c21c-163">Configuration File Schema</span></span>
<span data-ttu-id="8c21c-164">診斷組態檔定義當診斷代理程式啟動時，用來初始化診斷組態設定的值。</span><span class="sxs-lookup"><span data-stu-id="8c21c-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="8c21c-165">如需相關的有效值和範例，請參閱 [最新的結構描述參考](https://msdn.microsoft.com/library/azure/mt634524.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8c21c-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8c21c-166">疑難排解</span><span class="sxs-lookup"><span data-stu-id="8c21c-166">Troubleshooting</span></span>
<span data-ttu-id="8c21c-167">如果您遇到困難，請參閱 [Azure 診斷的疑難排解](../azure-diagnostics-troubleshooting.md) ，以解決常見的問題。</span><span class="sxs-lookup"><span data-stu-id="8c21c-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c21c-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c21c-168">Next Steps</span></span>
<span data-ttu-id="8c21c-169">[請參閱相關的 Azure 虛擬機器診斷文章清單](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics)，以變更您收集的資料、為問題進行疑難排解，或深入了解一般的診斷。</span><span class="sxs-lookup"><span data-stu-id="8c21c-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
