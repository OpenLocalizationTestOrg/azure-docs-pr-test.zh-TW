---
title: "在 Azure 堆疊 aaaDiagnostics |Microsoft 文件"
description: "Toocollect 記錄檔以 Azure 堆疊中的診斷資訊的方式"
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
ms.openlocfilehash: a4a5ddf29e75df710e9fae366d6ac16e6fb36d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="c7a2d-103">Azure Stack 診斷工具</span><span class="sxs-lookup"><span data-stu-id="c7a2d-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="c7a2d-104">Azure Stack 是元件共同作業並與彼此互動的大型集合。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="c7a2d-105">所有這些元件都將會產生自己的唯一記錄，這表示診斷問題將很快就成為極富挑戰性的工作，尤其是針對來自多個互動的 Azure Stack 元件的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="c7a2d-106">我們的診斷工具協助確定 hello 記錄機制進行簡單而有效。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-106">Our diagnostics tools help make sure hello log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="c7a2d-107">hello 圖說明如何記錄收集工具在 Azure 堆疊工作：</span><span class="sxs-lookup"><span data-stu-id="c7a2d-107">hello following diagram shows how log collection tools in Azure Stack work:</span></span>

![記錄收集工具](media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="c7a2d-109">追蹤收集器</span><span class="sxs-lookup"><span data-stu-id="c7a2d-109">Trace Collector</span></span>
 
<span data-ttu-id="c7a2d-110">預設會啟用 hello 追蹤收集器。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-110">hello Trace Collector is enabled by default.</span></span> <span data-ttu-id="c7a2d-111">它持續 hello 背景中執行 Azure 堆疊上，從 元件服務收集所有事件追蹤的 Windows (ETW) 記錄檔並將它們儲存在一般的本機共用上。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-111">It continuously runs in hello background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="c7a2d-112">hello 下面是有關 hello 追蹤收集器的重要事項 tooknow:</span><span class="sxs-lookup"><span data-stu-id="c7a2d-112">hello following are important things tooknow about hello Trace Collector:</span></span>
 
* <span data-ttu-id="c7a2d-113">hello 追蹤收集器會持續執行預設的大小限制。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-113">hello Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="c7a2d-114">hello 預設允許的大小上限 (200 MB) 的每個檔案是**不**截止大小。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-114">hello default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="c7a2d-115">大小檢查會定期發生 （目前每隔 10 分鐘），而且如果 hello 目前的檔案是 > = 200 MB 時，它會儲存並產生新的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-115">A size check occurs periodically (currently every 10 minutes) and if hello current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="c7a2d-116">Hello 檔案大小總計產生每個事件工作階段上也沒有為 8 GB （設定） 的限制。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-116">There is also an 8 GB (configurable) limit on hello total file size generated per event session.</span></span> <span data-ttu-id="c7a2d-117">一旦達到此限制時，建立新的時，會刪除 hello 最舊的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-117">Once this limit is reached, hello oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="c7a2d-118">Hello 記錄檔沒有 5 天的天數。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-118">There is a 5-day age limit on hello logs.</span></span> <span data-ttu-id="c7a2d-119">此限制也可設定。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="c7a2d-120">每個元件會定義 hello 追蹤組態屬性，透過 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-120">Each component defines hello trace configuration properties through a JSON file.</span></span> <span data-ttu-id="c7a2d-121">hello JSON 檔案儲存在`C:\TraceCollector\Configuration`。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-121">hello JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="c7a2d-122">如果有需要，這些檔案都可以編輯 toochange hello 存在時間和大小限制的 hello 收集記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-122">If necessary, these files can be edited toochange hello age and size limits of hello collected logs.</span></span> <span data-ttu-id="c7a2d-123">變更 toothese 檔案需要重新啟動 hello *Microsoft Azure 堆疊追蹤收集器*hello 的服務變更 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-123">Changes toothese files require a restart of hello *Microsoft Azure Stack Trace Collector* service for hello changes tootake effect.</span></span>
* <span data-ttu-id="c7a2d-124">hello 下列範例是追蹤組態 JSON 檔 FabricRingServices 作業從 hello XRP VM:</span><span class="sxs-lookup"><span data-stu-id="c7a2d-124">hello following example is a trace configuration JSON file for FabricRingServices Operations from hello XRP VM:</span></span> 

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

* <span data-ttu-id="c7a2d-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="c7a2d-126">此參數控制 hello 檔案 tookeep 存留期。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-126">This parameter controls hello age of files tookeep.</span></span> <span data-ttu-id="c7a2d-127">較舊的記錄檔將會受到刪除。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-127">Older log files are deleted.</span></span>
* <span data-ttu-id="c7a2d-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="c7a2d-129">此參數控制 hello 大小閾值，單一檔案。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-129">This parameter controls hello size threshold for a single file.</span></span> <span data-ttu-id="c7a2d-130">如果達到 hello 大小，則會建立新的.etl 檔案。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-130">If hello size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="c7a2d-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="c7a2d-132">此參數控制 hello 從事件工作階段產生的 hello.etl 檔案的大小總計。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-132">This parameter controls hello total size of hello .etl files generated from an event session.</span></span> <span data-ttu-id="c7a2d-133">如果 hello 檔案總大小大於此參數值，則會刪除較舊的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-133">If hello total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="c7a2d-134">記錄收集工具</span><span class="sxs-lookup"><span data-stu-id="c7a2d-134">Log collection tool</span></span>
 
<span data-ttu-id="c7a2d-135">hello PowerShell 命令`Get-AzureStackLog`可以是從所有 Azure 堆疊環境中的 hello 元件使用的 toocollect 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-135">hello PowerShell command `Get-AzureStackLog` can be used toocollect logs from all hello components  in an Azure Stack environment.</span></span> <span data-ttu-id="c7a2d-136">其會將它們以 ZIP 檔案儲存在使用者定義的位置。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="c7a2d-137">如果我們的技術支援小組需要記錄檔 toohelp 疑難排解問題，可能會要求 toorun 這項工具。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-137">If our technical support team needs your logs toohelp troubleshoot an issue, they may ask you toorun this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="c7a2d-138">這些記錄檔可能包含個人識別資訊 (PII)。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="c7a2d-139">在您公開公佈任何記錄檔之前，請先將這點納入考量。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="c7a2d-140">目前，我們會收集下列記錄類型的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7a2d-140">We currently collect hello following log types:</span></span>
*   <span data-ttu-id="c7a2d-141">**Azure Stack 部署記錄**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="c7a2d-142">**Windows 事件記錄**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-142">**Windows event logs**</span></span>
*   <span data-ttu-id="c7a2d-143">**Panther 記錄**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-143">**Panther logs**</span></span>

     <span data-ttu-id="c7a2d-144">tootroubleshoot VM 建立問題。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-144">tootroubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="c7a2d-145">**叢集記錄**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-145">**Cluster logs**</span></span>
*   <span data-ttu-id="c7a2d-146">**儲存體診斷記錄**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="c7a2d-147">**ETW 記錄**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-147">**ETW logs**</span></span>

    <span data-ttu-id="c7a2d-148">這些是 hello 追蹤收集器所收集而且儲存在共用從哪裡`Get-AzureStackLog`擷取它們。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-148">These are collected by hello Trace Collector and stored in a share from where `Get-AzureStackLog` retrieves them.</span></span>
 
<span data-ttu-id="c7a2d-149">tooidentify 所有 hello 取得從所有的 hello 元件收集的記錄檔，請參閱 toohello`<Logs>`位於 hello 客戶設定檔中的標記`C:\EceStore\<Guid>\<GuidWithMaxFileSize>`。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-149">tooidentify all hello logs that get collected from all hello components, refer toohello `<Logs>` tags in hello customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="toorun-get-azurestacklog"></a><span data-ttu-id="c7a2d-150">toorun Get AzureStackLog</span><span class="sxs-lookup"><span data-stu-id="c7a2d-150">toorun Get-AzureStackLog</span></span>
1.  <span data-ttu-id="c7a2d-151">以登入 AzureStack\AzureStackAdmin hello 主機上。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-151">Log in as AzureStack\AzureStackAdmin on hello host.</span></span>
2.  <span data-ttu-id="c7a2d-152">以系統管理員身分開啟 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="c7a2d-153">執行 `Get-AzureStackLog`。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-153">Run `Get-AzureStackLog`.</span></span>  

    <span data-ttu-id="c7a2d-154">**範例**</span><span class="sxs-lookup"><span data-stu-id="c7a2d-154">**Examples**</span></span>

    - <span data-ttu-id="c7a2d-155">為所有角色收集所有記錄：</span><span class="sxs-lookup"><span data-stu-id="c7a2d-155">Collect all logs for all roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="c7a2d-156">從 VirtualMachines 與 BareMetal 角色收集記錄：</span><span class="sxs-lookup"><span data-stu-id="c7a2d-156">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="c7a2d-157">收集記錄檔篩選記錄檔以取得 hello 過去 8 小時的日期與 VirtualMachines 和 BareMetal 角色：</span><span class="sxs-lookup"><span data-stu-id="c7a2d-157">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for hello past 8 hours:</span></span>

        `Get-AzureStackLog -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="c7a2d-158">如果 hello`FromDate`和`ToDate`如果未指定參數、 記錄檔預設會收集 hello 過去 4 小時。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-158">If hello `FromDate` and `ToDate` parameters are not specified, logs are collected for hello past 4 hours by default.</span></span>

<span data-ttu-id="c7a2d-159">目前，您可以使用 hello`FilterByRole`參數 toofilter 記錄檔集合，由下列角色的 hello:</span><span class="sxs-lookup"><span data-stu-id="c7a2d-159">Currently, you can use hello `FilterByRole` parameter toofilter log collection by hello following roles:</span></span>

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


<span data-ttu-id="c7a2d-160">幾件事 toonote:</span><span class="sxs-lookup"><span data-stu-id="c7a2d-160">A few things toonote:</span></span>

* <span data-ttu-id="c7a2d-161">此命令將會需要一些時間來收集記錄，視乎將收集哪些角色記錄。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-161">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="c7a2d-162">促成因素包括 hello 指定記錄檔集合與 hello hello Azure 堆疊環境中的節點數目的持續時間。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-162">Contributing factors include hello time duration specified for log collection, and hello numbers of nodes in hello Azure Stack environment.</span></span>
* <span data-ttu-id="c7a2d-163">記錄檔收集完成之後，請檢查 hello hello 中建立的新資料夾`-OutputPath`hello 命令中指定的參數。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-163">After log collection completes, check hello new folder created in hello `-OutputPath` parameter specified in hello command.</span></span>
* <span data-ttu-id="c7a2d-164">呼叫檔案`Get-AzureStackLog_Output.log`hello 包含 hello zip 檔案的資料夾中建立並包含 hello 命令輸出中，可以用於疑難排解記錄檔集合中的任何失敗。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-164">A file called `Get-AzureStackLog_Output.log` is created in hello folder containing hello zip files and includes hello command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="c7a2d-165">每個角色在個別 ZIP 檔案皆有其記錄。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-165">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="c7a2d-166">tooinvestigate 特定錯誤，記錄檔可能需要從多個元件。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-166">tooinvestigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="c7a2d-167">系統和基礎結構的所有 vm 的事件記錄檔會收集在 hello *VirtualMachines*角色。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-167">System and Event logs for all infrastructure VMs are collected in hello *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="c7a2d-168">系統和所有主機的事件記錄檔會收集在 hello *BareMetal*角色。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-168">System and Event logs for all hosts are collected in hello *BareMetal* role.</span></span>
    -   <span data-ttu-id="c7a2d-169">容錯移轉叢集和 HYPER-V 事件記錄檔會收集在 hello*儲存體*角色。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-169">Failover Cluster and Hyper-V event logs are collected in hello *Storage* role.</span></span>
    -   <span data-ttu-id="c7a2d-170">ACS 的記錄檔會收集在 hello*儲存體*和*ACS*角色。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-170">ACS logs are collected in hello *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="c7a2d-171">如需詳細資訊，您可以參考 toohello 客戶設定檔。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-171">For more details, you can refer toohello customer configuration file.</span></span> <span data-ttu-id="c7a2d-172">調查 hello `<Logs>` hello 不同角色的標記。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-172">Investigate hello `<Logs>` tags for hello different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="c7a2d-173">我們會強制執行大小和存在時間限制，所以您確定不會取得大量湧入記錄檔的儲存體空間 toomake 基本 tooensure 有效率地利用所收集的 toohello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-173">We are enforcing size and age limits toohello logs collected as it is essential tooensure efficient utilization of your storage space toomake sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="c7a2d-174">強調的是，當診斷的問題，您通常需要記錄檔，可能不存在 toothese 限制強制執行到期。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-174">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due toothese limits being enforced.</span></span> <span data-ttu-id="c7a2d-175">因此，**強烈建議**您卸載記錄 tooan 外部儲存空間 （在公用 Azure 儲存體帳戶、 內部額外存放裝置等等） 來 too12 每 8 小時，讓它們那里取決於 1-3 個月您的需求。</span><span class="sxs-lookup"><span data-stu-id="c7a2d-175">Hence, it is **highly recommended** that you offload your logs tooan external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 too12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7a2d-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7a2d-176">Next steps</span></span>
[<span data-ttu-id="c7a2d-177">Microsoft Azure Stack 疑難排解</span><span class="sxs-lookup"><span data-stu-id="c7a2d-177">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)
