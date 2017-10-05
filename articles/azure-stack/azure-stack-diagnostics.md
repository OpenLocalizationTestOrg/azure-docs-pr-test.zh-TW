---
title: "Azure Stack 中的診斷功能 | Microsoft Docs"
description: "如何在 Azure Stack 中收集記錄檔以進行診斷"
services: azure-stack
documentationcenter: 
author: adshar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: adshar
ms.openlocfilehash: 70004cfd83360ac4c66fd4c90632d341709d2e6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="0a021-103">Azure Stack 診斷工具</span><span class="sxs-lookup"><span data-stu-id="0a021-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="0a021-104">Azure Stack 是元件共同作業並與彼此互動的大型集合。</span><span class="sxs-lookup"><span data-stu-id="0a021-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="0a021-105">所有這些元件都將會產生自己的唯一記錄，這表示診斷問題將很快就成為極富挑戰性的工作，尤其是針對來自多個互動的 Azure Stack 元件的錯誤。</span><span class="sxs-lookup"><span data-stu-id="0a021-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="0a021-106">我們的診斷工具協助確定記錄集合機制簡單而有效。</span><span class="sxs-lookup"><span data-stu-id="0a021-106">Our diagnostics tools help make sure the log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="0a021-107">下圖說明記錄收集工具在 Azure Stack 中的運作方式：</span><span class="sxs-lookup"><span data-stu-id="0a021-107">The following diagram shows how log collection tools in Azure Stack work:</span></span>

![記錄收集工具](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="0a021-109">追蹤收集器</span><span class="sxs-lookup"><span data-stu-id="0a021-109">Trace Collector</span></span>
 
<span data-ttu-id="0a021-110">「追蹤收集器」預設為啟用。</span><span class="sxs-lookup"><span data-stu-id="0a021-110">The Trace Collector is enabled by default.</span></span> <span data-ttu-id="0a021-111">它將會持續在背景中執行，在 Azure Stack 上從元件服務收集 Windows 事件追蹤 (ETW) 記錄，並將其儲存在一般本機共用上。</span><span class="sxs-lookup"><span data-stu-id="0a021-111">It continuously runs in the background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="0a021-112">下列是需要知道「追蹤收集器」的重要事項：</span><span class="sxs-lookup"><span data-stu-id="0a021-112">The following are important things to know about the Trace Collector:</span></span>
 
* <span data-ttu-id="0a021-113">「追蹤收集器」會持續以預設大小限制執行。</span><span class="sxs-lookup"><span data-stu-id="0a021-113">The Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="0a021-114">每個檔案預設的允許大小上限 (200 MB) 並**不**是截止大小。</span><span class="sxs-lookup"><span data-stu-id="0a021-114">The default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="0a021-115">大小檢查將會定期執行 (目前為每隔 10 分鐘)，而如果目前檔案 > = 200 MB 時，其將會儲存並產生新的檔案。</span><span class="sxs-lookup"><span data-stu-id="0a021-115">A size check occurs periodically (currently every 10 minutes) and if the current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="0a021-116">每個事件工作階段總檔案大小也有 8 GB (可設定) 的限制。</span><span class="sxs-lookup"><span data-stu-id="0a021-116">There is also an 8 GB (configurable) limit on the total file size generated per event session.</span></span> <span data-ttu-id="0a021-117">一旦達到此限制，建立新檔案時將會同時刪除最舊的檔案。</span><span class="sxs-lookup"><span data-stu-id="0a021-117">Once this limit is reached, the oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="0a021-118">記錄限制只會記錄 5 天。</span><span class="sxs-lookup"><span data-stu-id="0a021-118">There is a 5-day age limit on the logs.</span></span> <span data-ttu-id="0a021-119">此限制也可設定。</span><span class="sxs-lookup"><span data-stu-id="0a021-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="0a021-120">每個元件會透過 JSON 檔案定義追蹤組態屬性。</span><span class="sxs-lookup"><span data-stu-id="0a021-120">Each component defines the trace configuration properties through a JSON file.</span></span> <span data-ttu-id="0a021-121">JSON 檔案會儲存於 `C:\TraceCollector\Configuration`。</span><span class="sxs-lookup"><span data-stu-id="0a021-121">The JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="0a021-122">如有必要，可以編輯這些檔案來變更收集記錄的時間和大小限制。</span><span class="sxs-lookup"><span data-stu-id="0a021-122">If necessary, these files can be edited to change the age and size limits of the collected logs.</span></span> <span data-ttu-id="0a021-123">變更這些檔案將會需要重新啟動「Microsoft Azure Stack 追蹤收集器」 服務，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="0a021-123">Changes to these files require a restart of the *Microsoft Azure Stack Trace Collector* service for the changes to take effect.</span></span>
* <span data-ttu-id="0a021-124">下列範例是適用於來自 XRP 虛擬機器 FabricRingServices 作業的追蹤組態 JSON 檔：</span><span class="sxs-lookup"><span data-stu-id="0a021-124">The following example is a trace configuration JSON file for FabricRingServices Operations from the XRP VM:</span></span> 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* <span data-ttu-id="0a021-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="0a021-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="0a021-126">此參數將會控制保留檔案的時間。</span><span class="sxs-lookup"><span data-stu-id="0a021-126">This parameter controls the age of files to keep.</span></span> <span data-ttu-id="0a021-127">較舊的記錄檔將會受到刪除。</span><span class="sxs-lookup"><span data-stu-id="0a021-127">Older log files are deleted.</span></span>
* <span data-ttu-id="0a021-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="0a021-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="0a021-129">此參數控制單一檔案的大小臨界值。</span><span class="sxs-lookup"><span data-stu-id="0a021-129">This parameter controls the size threshold for a single file.</span></span> <span data-ttu-id="0a021-130">如果達到大小限制，則會建立新的 .etl 檔案。</span><span class="sxs-lookup"><span data-stu-id="0a021-130">If the size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="0a021-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="0a021-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="0a021-132">此參數控制事件工作階段所產生 .etl 檔的總大小。</span><span class="sxs-lookup"><span data-stu-id="0a021-132">This parameter controls the total size of the .etl files generated from an event session.</span></span> <span data-ttu-id="0a021-133">如果總檔案大小大於此參數值，則較舊的檔案將會受到刪除。</span><span class="sxs-lookup"><span data-stu-id="0a021-133">If the total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="0a021-134">記錄收集工具</span><span class="sxs-lookup"><span data-stu-id="0a021-134">Log collection tool</span></span>
 
<span data-ttu-id="0a021-135">PowerShell 命令 `Get-AzureStackLog` 可用來收集 Azure Stack 環境中所有元件的記錄。</span><span class="sxs-lookup"><span data-stu-id="0a021-135">The PowerShell command `Get-AzureStackLog` can be used to collect logs from all the components  in an Azure Stack environment.</span></span> <span data-ttu-id="0a021-136">其會將它們以 ZIP 檔案儲存在使用者定義的位置。</span><span class="sxs-lookup"><span data-stu-id="0a021-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="0a021-137">如果我們的技術支援小組需要您的記錄，以便針對問題進行疑難排解，小組可能會要求您執行此工具。</span><span class="sxs-lookup"><span data-stu-id="0a021-137">If our technical support team needs your logs to help troubleshoot an issue, they may ask you to run this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="0a021-138">這些記錄檔可能包含個人識別資訊 (PII)。</span><span class="sxs-lookup"><span data-stu-id="0a021-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="0a021-139">在您公開公佈任何記錄檔之前，請先將這點納入考量。</span><span class="sxs-lookup"><span data-stu-id="0a021-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="0a021-140">我們目前將會收集下列記錄類型︰</span><span class="sxs-lookup"><span data-stu-id="0a021-140">We currently collect the following log types:</span></span>
*   <span data-ttu-id="0a021-141">**Azure Stack 部署記錄**</span><span class="sxs-lookup"><span data-stu-id="0a021-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="0a021-142">**Windows 事件記錄**</span><span class="sxs-lookup"><span data-stu-id="0a021-142">**Windows event logs**</span></span>
*   <span data-ttu-id="0a021-143">**Panther 記錄**</span><span class="sxs-lookup"><span data-stu-id="0a021-143">**Panther logs**</span></span>

     <span data-ttu-id="0a021-144">若是針對 RDP 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0a021-144">To troubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="0a021-145">**叢集記錄**</span><span class="sxs-lookup"><span data-stu-id="0a021-145">**Cluster logs**</span></span>
*   <span data-ttu-id="0a021-146">**儲存體診斷記錄**</span><span class="sxs-lookup"><span data-stu-id="0a021-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="0a021-147">**ETW 記錄**</span><span class="sxs-lookup"><span data-stu-id="0a021-147">**ETW logs**</span></span>

    <span data-ttu-id="0a021-148">這些是「追蹤收集器」所收集且儲存在共用中，可使用 `Get-AzureStackLog` 進行擷取。</span><span class="sxs-lookup"><span data-stu-id="0a021-148">These are collected by the Trace Collector and stored in a share from where `Get-AzureStackLog` retrieves them.</span></span>
 
<span data-ttu-id="0a021-149">若要識別收集來自所有元件的所有記錄，請參閱「位於 `C:\EceStore\<Guid>\<GuidWithMaxFileSize>` 客戶設定檔中的 `<Logs>` 標記」。</span><span class="sxs-lookup"><span data-stu-id="0a021-149">To identify all the logs that get collected from all the components, refer to the `<Logs>` tags in the customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="to-run-get-azurestacklog"></a><span data-ttu-id="0a021-150">執行 Get-AzureStackLog</span><span class="sxs-lookup"><span data-stu-id="0a021-150">To run Get-AzureStackLog</span></span>
1.  <span data-ttu-id="0a021-151">以 AzureStack\AzureStackAdmin 身分登入主機。</span><span class="sxs-lookup"><span data-stu-id="0a021-151">Log in as AzureStack\AzureStackAdmin on the host.</span></span>
2.  <span data-ttu-id="0a021-152">以系統管理員身分開啟 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="0a021-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="0a021-153">執行 `Get-AzureStackLog`。</span><span class="sxs-lookup"><span data-stu-id="0a021-153">Run `Get-AzureStackLog`.</span></span>  

    <span data-ttu-id="0a021-154">**範例**</span><span class="sxs-lookup"><span data-stu-id="0a021-154">**Examples**</span></span>

    - <span data-ttu-id="0a021-155">為所有角色收集所有記錄：</span><span class="sxs-lookup"><span data-stu-id="0a021-155">Collect all logs for all roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="0a021-156">從 VirtualMachines 與 BareMetal 角色收集記錄：</span><span class="sxs-lookup"><span data-stu-id="0a021-156">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="0a021-157">從 VirtualMachines 和 BareMetal 角色收集記錄，且記錄日期篩選為過去 8 小時：</span><span class="sxs-lookup"><span data-stu-id="0a021-157">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for the past 8 hours:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="0a021-158">如果未指定 `FromDate` 和 `ToDate` 參數，預設為將會收集過去 4 小時的記錄。</span><span class="sxs-lookup"><span data-stu-id="0a021-158">If the `FromDate` and `ToDate` parameters are not specified, logs are collected for the past 4 hours by default.</span></span>

<span data-ttu-id="0a021-159">目前您可以透過下列角色使用 `FilterByRole` 參數來篩選記錄集合：</span><span class="sxs-lookup"><span data-stu-id="0a021-159">Currently, you can use the `FilterByRole` parameter to filter log collection by the following roles:</span></span>

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


<span data-ttu-id="0a021-160">幾個注意事項：</span><span class="sxs-lookup"><span data-stu-id="0a021-160">A few things to note:</span></span>

* <span data-ttu-id="0a021-161">此命令將會需要一些時間來收集記錄，視乎將收集哪些角色記錄。</span><span class="sxs-lookup"><span data-stu-id="0a021-161">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="0a021-162">促成因素包括指定收集記錄的進行時間，以及 Azure Stack 環境中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="0a021-162">Contributing factors include the time duration specified for log collection, and the numbers of nodes in the Azure Stack environment.</span></span>
* <span data-ttu-id="0a021-163">完成記錄收集之後，請檢查以命令指定 `-OutputPath` 參數所建立的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="0a021-163">After log collection completes, check the new folder created in the `-OutputPath` parameter specified in the command.</span></span>
* <span data-ttu-id="0a021-164">名為 `Get-AzureStackLog_Output.log` 的檔案將會在包含 ZIP 檔案的資料夾中建立，並包括命令輸出，可以用於針對記錄集合中的任何失敗進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="0a021-164">A file called `Get-AzureStackLog_Output.log` is created in the folder containing the zip files and includes the command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="0a021-165">每個角色在個別 ZIP 檔案皆有其記錄。</span><span class="sxs-lookup"><span data-stu-id="0a021-165">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="0a021-166">若要調查特定失敗原因，則可能需要多個元件的記錄。</span><span class="sxs-lookup"><span data-stu-id="0a021-166">To investigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="0a021-167">所有基礎結構虛擬機器的系統和事件記錄，皆會收集在「VirtualMachines」角色中。</span><span class="sxs-lookup"><span data-stu-id="0a021-167">System and Event logs for all infrastructure VMs are collected in the *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="0a021-168">所有主機的系統和事件記錄，皆會收集在「BareMetal」角色中。</span><span class="sxs-lookup"><span data-stu-id="0a021-168">System and Event logs for all hosts are collected in the *BareMetal* role.</span></span>
    -   <span data-ttu-id="0a021-169">容錯移轉叢集和 Hyper-V 事件記錄，皆會收集在「Storage」角色中。</span><span class="sxs-lookup"><span data-stu-id="0a021-169">Failover Cluster and Hyper-V event logs are collected in the *Storage* role.</span></span>
    -   <span data-ttu-id="0a021-170">ACS 記錄則會收集在「Storage」和「ACS」角色中。</span><span class="sxs-lookup"><span data-stu-id="0a021-170">ACS logs are collected in the *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="0a021-171">如需詳細資訊，您可以參考客戶設定檔。</span><span class="sxs-lookup"><span data-stu-id="0a021-171">For more details, you can refer to the customer configuration file.</span></span> <span data-ttu-id="0a021-172">為不同角色調查 `<Logs>`標記。</span><span class="sxs-lookup"><span data-stu-id="0a021-172">Investigate the `<Logs>` tags for the different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="0a021-173">我們將會強制執行大小和時間限制，因為確保您能有效率地利用儲存空間，以及其不會因記錄而塞滿極其重要。</span><span class="sxs-lookup"><span data-stu-id="0a021-173">We are enforcing size and age limits to the logs collected as it is essential to ensure efficient utilization of your storage space to make sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="0a021-174">強調的是當診斷問題時，因為強制執行這些限制，您通常需要的記錄可能已不存在。</span><span class="sxs-lookup"><span data-stu-id="0a021-174">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due to these limits being enforced.</span></span> <span data-ttu-id="0a021-175">因此，我們**強烈建議**您每隔 8 到 12 個小時將記錄卸載到外部存放裝置空間 (公用 Azure 中的儲存體帳戶、額外內部存放裝置等)，並視需求保存 1-3 個月。</span><span class="sxs-lookup"><span data-stu-id="0a021-175">Hence, it is **highly recommended** that you offload your logs to an external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 to 12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0a021-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a021-176">Next steps</span></span>
[<span data-ttu-id="0a021-177">Microsoft Azure Stack 疑難排解</span><span class="sxs-lookup"><span data-stu-id="0a021-177">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)
