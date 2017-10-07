---
title: "aaaMonitor 和使用 hello Azure 入口網站和 PowerShell 管理管線 |Microsoft 文件"
description: "了解 toouse hello Azure 入口網站和 Azure PowerShell toomonitor 和管理 hello Azure data factory 和您所建立的管線的方式。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>監視和管理 Azure Data Factory 管線使用 hello Azure 入口網站和 PowerShell
> [!div class="op_single_selector"]
> * [使用 Azure 入口網站/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [使用監視及管理應用程式](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> hello 監督和管理應用程式提供更佳的支援的監視與管理您的資料管線，以及疑難排解任何問題。 如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)。 


本文說明如何 toomonitor、 管理及使用 Azure 入口網站和 PowerShell 偵錯您的管線。 hello 發行項也會提供資訊 toocreate 警示的方式，以及取得有關失敗的通知。

## <a name="understand-pipelines-and-activity-states"></a>了解管線和活動狀態
Hello Azure 入口網站，您可以使用：

* 以圖表形式檢視 Data Factory。
* 檢視管線中的活動。
* 檢視輸入和輸出資料集。

本章節也說明從一個狀態 tooanother 狀態轉換的資料集配量的方式。   

### <a name="navigate-tooyour-data-factory"></a>瀏覽 tooyour 資料處理站
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 按一下**Data factory** hello hello 左邊的功能表上。 如果您沒有看到它，按一下**更多服務 >**，然後按一下 [ **Data factory**下 hello**智慧 + 分析**類別目錄。

   ![全部瀏覽 -> Data Factory](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. 在 [hello **Data factory**刀鋒視窗中，選取 hello 您感興趣的 data factory。

    ![選取 Data Factory](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   您應該會看到 hello 首頁 hello data factory。

   ![Data Factory 刀鋒視窗](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Data Factory 的圖表檢視
hello**圖表**檢視的 data factory 提供單一的半透明 toomonitor 窗格及管理 hello data factory 和其資產。 toosee hello**圖表**您的 data factory 的檢視，請按一下**圖表**hello data factory 的 hello 首頁上。

![圖表檢視](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

您可以放大、 縮小，縮放 toofit、 縮放 too100%、 鎖定 hello hello 圖表配置和自動定位管線與資料集。 您也可以查看 hello 資料歷程資訊 （也就是顯示選取項目的上游及下游項目）。

### <a name="activities-inside-a-pipeline"></a>管線中的活動
1. 以滑鼠右鍵按一下 hello 管線，然後按一下**開啟管線**toosee hello 中的所有活動的都管線，以及 hello 活動的輸入和輸出資料集。 這項功能時，您的管線包含一個以上的活動和您想要的單一管線 toounderstand hello 作業歷程。

    ![開啟管線功能表](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. 在下列範例的 hello，您會看到複製活動中使用輸入和輸出的 hello 管線。 

    ![管線中的活動](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. 您可以巡覽的 hello data factory 的回復 toohello 首頁按一下 hello **Data factory** hello hello 左上角的階層連結中的連結。

    ![瀏覽後 toodata factory](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>在管線內的每個活動檢視 hello 狀態
您可以藉由檢視任何 hello hello 活動所產生的資料集的 hello 狀態檢視 hello 目前活動的狀態。

按兩下 hello **OutputBlobTable**在 hello**圖表**，您可以看到不同的活動執行內的管線所產生的所有 hello 配量。 您可以看到 hello 複製活動已順利執行 hello 最後八小時，以及產生 hello 配量在 hello**準備**狀態。  

![Hello 管線的狀態](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

hello hello data factory 中的資料集配量可以具有下列狀態的 hello 其中一項：

<table>
<tr>
    <th align="left">State</th><th align="left">子狀態</th><th align="left">說明</th>
</tr>
<tr>
    <td rowspan="8">等候</td><td>ScheduleTime</td><td>hello 時間未針對 hello 配量 toorun 發生。</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>hello 上游相依性未準備好。</td>
</tr>
<tr>
<td>ComputeResources</td><td>hello 計算資源無法使用。</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>所有的 hello 活動執行個體都忙於執行其他配量。</td>
</tr>
<tr>
<td>ActivityResume</td><td>hello 活動已暫停，直到繼續 hello 活動無法執行 hello 配量。</td>
</tr>
<tr>
<td>Retry</td><td>正在重試活動執行。</td>
</tr>
<tr>
<td>驗證</td><td>驗證尚未啟動。</td>
</tr>
<tr>
<td>ValidationRetry</td><td>驗證是等待 toobe 重試。</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>驗證正在進行中。</td>
</tr>
<td>-</td>
<td>正在處理 hello 配量。</td>
</tr>
<tr>
<td rowspan="4">Failed</td><td>TimedOut</td><td>hello 活動的執行時間超過所允許的 hello 活動。</td>
</tr>
<tr>
<td>Canceled</td><td>使用者動作已取消 hello 配量。</td>
</tr>
<tr>
<td>驗證</td><td>驗證失敗。</td>
</tr>
<tr>
<td>-</td><td>hello 配量無法 toobe 產生及/或驗證。</td>
</tr>
<td>就緒</td><td>-</td><td>hello 配量是供取用。</td>
</tr>
<tr>
<td>Skipped</td><td>None</td><td>不是正在處理 hello 配量。</td>
</tr>
<tr>
<td>None</td><td>-</td><td>配量 tooexist 搭配不同的狀態，但已重設。</td>
</tr>
</table>



您可以檢視 hello 配量的詳細資料，依序按一下 [配量上的項目 hello**最近更新配量**刀鋒視窗。

![配量的詳細資料](./media/data-factory-monitor-manage-pipelines/slice-details.png)

如果已經執行多次 hello 配量，您會看到多重資料列的 hello**活動執行**清單。 您可以檢視活動按一下 hello 中的 hello 執行項目，以執行詳細**活動執行**清單。 hello 清單會顯示所有 hello 記錄檔，以及錯誤訊息，如果有的話。 此功能十分有用 tooview 和偵錯記錄檔，而不需要 tooleave 您的 data factory。

![活動執行詳細資料](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

如果 hello 配量不在 hello**準備**狀態，您可以看到未準備好並封鎖 hello hello 中執行的目前配量的 hello 上游配量**未就緒的上游配量**清單。 在您的配量時，此功能十分有用**等候**狀態和您想要在等待 toounderstand hello 上游相依性 hello 配量。

![尚未就緒的上游配量](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>資料集狀態圖表
部署 data factory hello 管線有有效的使用中期間後，hello 資料集配量從一個狀態 tooanother 轉換。 目前，hello 配量狀態會遵循下列狀態圖表 hello:

![狀態圖表](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

hello data factory 中的資料集的狀態轉換流量是 hello 下列： 等候]-> [進度/中-進行中 （驗證）]-> [已備妥/失敗。

的 hello 配量開始**等候**先決條件 toobe 符合其執行之前所等候的狀態。 Hello 活動開始執行，然後 hello 配量進入**In-progress**狀態。 hello 活動執行可能會成功或失敗。 hello 配量會標示為**準備**或**失敗**根據 hello hello 執行結果。

您可以重設回從 hello hello 配量 toogo**準備**或**失敗**狀態 toohello**等候**狀態。 也可以將 hello 配量狀態太**略過**，這樣就不會執行和不處理 hello 配量的 hello 活動。

## <a name="pause-and-resume-pipelines"></a>暫停及繼續管線
您可以使用 Azure Powershell 管理您的管線。 例如，您可以執行 Azure PowerShell Cmdlet 來暫停和繼續執行管線。 

> [!NOTE] 
> hello 圖表檢視不支援暫停和繼續管線。 如果您想 toouse 使用者介面時，使用 hello 監視和管理應用程式。 如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)發行項。 

您可以暫停/暫停管線使用 hello**暫停 AzureRmDataFactoryPipeline** PowerShell cmdlet。 這個指令程式時，您不想 toorun 管線直到問題得到解決為止。 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
例如：

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Hello 管線與已修正 hello 問題之後，您可以藉由執行下列 PowerShell 命令的 hello 繼續暫停的 hello 管線：

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
例如：

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>偵錯管線
Azure Data Factory toodebug 為您提供豐富的功能，並使用 hello Azure 入口網站和 Azure PowerShell 來進行疑難排解管線。

> [!請注意} 很容易 tootroubleshot 使用錯誤 hello 監視和管理應用程式。 如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)發行項。 

### <a name="find-errors-in-a-pipeline"></a>尋找管線中的錯誤
Hello 活動執行會在管線中失敗，hello hello 管線所產生的資料集處於錯誤狀態是因為 hello 錯誤。 您可以偵錯，並使用下列方法 hello 疑難排解 Azure Data Factory 中的錯誤。

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>使用 Azure 入口網站 toodebug 錯誤 hello
1. 在 [hello**資料表**刀鋒視窗中，按一下具有 hello hello 問題配量**狀態**設定得**失敗**。

   ![含有問題配量的資料表刀鋒視窗](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. 在 [hello**資料配量**刀鋒視窗中，按一下 hello 活動執行失敗。

   ![發生錯誤的資料配量](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. 在 [hello**活動執行詳細資料**刀鋒視窗中，您可以下載 hello HDInsight 處理相關聯的 hello 檔案。 按一下**下載**狀態/stderr toodownload hello 錯誤記錄檔，其中包含關於 hello 錯誤詳細資料。

   ![含有錯誤的活動執行詳細資料刀鋒視窗](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>使用 PowerShell toodebug 錯誤
1. 啟動 **PowerShell**。
2. 執行 hello **Get AzureRmDataFactorySlice**命令 toosee hello 配量和其狀態。 您應該會看見 hello 狀態顯示為配量**失敗**。        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   例如：

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   將 **StartDateTime** 取代為您的管線開始時間。 
3. 現在，執行 hello **Get AzureRmDataFactoryRun** cmdlet tooget 詳細 hello 活動執行 hello 配量。

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    例如：

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    StartDateTime hello 值為 hello 您從 hello 上一個步驟記下的 hello 錯誤/問題配量的開始時間。 hello 日期-時間應該用雙引號括住。
4. 您應該會看到類似 toohello 下列 hello 錯誤的相關詳細資料的輸出：

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. 您可以執行 hello**儲存 AzureRmDataFactoryLog** cmdlet 搭配您從 hello 輸出，請參閱，以及使用 hello 下載 hello 記錄檔的識別碼值 hello **-DownloadLogsoption** hello 指令程式。

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>重新執行管線中的失敗

> [!IMPORTANT]
> 它是更容易 tootroubleshoot 錯誤，而且使用重新執行失敗的配量 hello 監視和管理應用程式。 如需有關使用 hello 應用程式的詳細資訊，請參閱[監視和管理使用 hello 監視和管理應用程式的 Data Factory 管線](data-factory-monitor-manage-app.md)。 

### <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站
在疑難排解和偵錯在管線中的失敗之後，您可重新執行失敗瀏覽 toohello 錯誤配量，然後按一下 hello**執行**hello 命令列上的按鈕。

![重新執行失敗的配量](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

萬一 hello 配量驗證失敗是因為原則錯誤 （例如，如果資料無法使用），您可以修正 hello 失敗，並依序按一下 hello 重新驗證**驗證**hello 命令列上的按鈕。

![修正錯誤並進行驗證](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>使用 Azure PowerShell
您可以使用 hello 重新執行失敗**組 AzureRmDataFactorySliceStatus** cmdlet。 請參閱 hello[組 AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx)的語法和 hello 指令程式的其他詳細資料。

**範例：**

hello 下列範例會設定所有的扇區的 hello 資料表 'DAWikiAggregatedData' too'Waiting hello 狀態 ' hello Azure data factory 'WikiADF' 中。

設定 too'UpstreamInPipeline 'P' hello '，這表示 hello 資料表的每個配量和所有相依 （上游） 資料表 hello 的狀態會設定 too'Waiting'。 hello 其他可能的值，這個參數為 「 個人 」。

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>建立警示
當建立、更新或刪除 Azure 資料時 (例如 Data Factory)，Azure 會記錄使用者事件。 您可以對這些事件建立警示。 您可以使用 Data Factory toocapture 多種標準，以及建立度量的警示。 我們建議您使用事件來進行即時監視，使用度量來做歷程記錄。

### <a name="alerts-on-events"></a>事件警示
Azure 事件可讓您深入了解 Azure 資源的情況。 使用 Azure Data Factory 時，下列情況會產生事件：

* 建立、更新或刪除 Data Factory。
* 資料處理 (「回合」形式) 已開始或完成。
* 建立或移除隨選 HDInsight 叢集。

您可以建立這些使用者事件的警示，並設定它們 toosend 電子郵件通知 toohello 系統管理員和 coadministrators hello 訂用帳戶。 此外，您可以指定符合 hello 條件時，需要 tooreceive 電子郵件通知的使用者的其他電子郵件地址。 當您要 tooget 在失敗時收到通知，而且不想 toocontinuously 監視您的 data factory，這個功能會很有用。

> [!NOTE]
> 目前，hello 入口網站不會顯示警示的事件。 使用 hello[監視和管理應用程式](data-factory-monitor-manage-app.md)toosee 所有警示。


#### <a name="specify-an-alert-definition"></a>指定警示定義
toospecify 警示定義，您會建立描述要 toobe 上發生警示的 hello 作業的 JSON 檔案。 在下列範例的 hello，hello 警示會傳送 hello RunFinished 作業的電子郵件通知。 toobe 特定電子郵件通知會傳送 hello data factory 中的執行已完成，而且 hello 執行失敗時 (狀態 = FailedExecution)。

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

您可以移除**子狀態**從 hello JSON 定義，如果您不想 toobe 特定失敗的警示。

此範例會設定您的訂用帳戶中的所有資料處理站的 hello 警示。 如果您想 hello 警示 toobe 設定特定的資料處理站，您可以指定資料處理站**resourceUri**在 hello **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

hello 下表提供 hello 清單可用的作業和狀態 （和子狀態）。

| 作業名稱 | 狀態 | 子狀態 |
| --- | --- | --- |
| RunStarted |已啟動 |啟動中 |
| RunFinished |Failed / Succeeded |FailedResourceAllocation<br/><br/>Succeeded<br/><br/>FailedExecution<br/><br/>TimedOut<br/><br/><已取消<br/><br/>FailedValidation<br/><br/>Abandoned |
| OnDemandClusterCreateStarted |已啟動 | |
| OnDemandClusterCreateSuccessful |Succeeded | |
| OnDemandClusterDeleted |Succeeded | |

請參閱[建立警示規則](https://msdn.microsoft.com/library/azure/dn510366.aspx)hello hello 範例中使用的 JSON 元素的詳細資料。

#### <a name="deploy-hello-alert"></a>部署 hello 警示
toodeploy hello 警示，請使用 hello Azure PowerShell 指令程式**新增 AzureRmResourceGroupDeployment**hello 下列範例所示：

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Hello 資源群組部署已順利完成之後，您會看到下列訊息的 hello:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> 您可以使用 hello[建立警示規則](https://msdn.microsoft.com/library/azure/dn510366.aspx)REST API toocreate 警示規則。 hello JSON 裝載是類似 toohello JSON 範例。  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>擷取 Azure 資源群組部署的 hello 的清單
tooretrieve hello 清單部署 Azure 資源群組部署，請使用 hello cmdlet **Get AzureRmResourceGroupDeployment**hello 下列範例所示：

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>使用者事件疑難排解
1. 您可以查看所有 hello 事件產生後按一下 hello**度量和作業**磚。

    ![度量和作業圖格](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. 按一下 hello**事件**磚 toosee hello 事件。

    ![[事件] 磚](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. 在 [hello**事件**刀鋒視窗中，您可以看到事件、 已篩選的事件，等等的相關詳細資料。

    ![事件刀鋒視窗](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. 按一下**作業**hello 作業的清單中，會造成錯誤。

    ![選取作業](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. 按一下**錯誤**hello 錯誤的相關事件 toosee 詳細資料。

    ![事件錯誤](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

請參閱[Azure Insight cmdlet](https://msdn.microsoft.com/library/mt282452.aspx) PowerShell 指令程式，您可以使用 tooadd，或以移除警示。 以下是一些使用 hello 範例**Get AlertRule** cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

執行的 hello 下列 get-help 命令 toosee 詳細資料及 hello Get AlertRule cmdlet 的範例。

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


如果您看到 hello 警示產生事件 hello 入口網站的刀鋒視窗，但不是會收到電子郵件通知，請檢查指定的 hello 電子郵件地址從外部寄件者是否設定 tooreceive 電子郵件。 電子郵件設定可能已封鎖 hello 警示的電子郵件。

### <a name="alerts-on-metrics"></a>度量的警示
您可以在 Data Factory 中擷取各種度量並建立度量警示。 您可以監視和 hello 下列度量資訊。 您的 data factory 中的 hello 扇區上建立警示：

* **失敗的執行**
* **成功的執行**

這些度量資訊會很有用，並且協助您 tooget hello data factory 中執行的整體失敗和成功的概觀。 每次有配量執行時就會發出度量。 在 hello 開頭 hello 小時，這些度量會彙總，推入 tooyour 儲存體帳戶。 tooenable 度量設定儲存體帳戶。

#### <a name="enable-metrics"></a>啟用度量
tooenable 度量，按一下 [從 hello hello 下列**Data Factory**刀鋒視窗中：

[監視] > [度量] > [診斷設定] > [診斷]

![診斷連結](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

在 [hello**診斷**刀鋒視窗中，按一下 [**上**，選取 hello 儲存體帳戶，然後按一下**儲存**。

![[診斷] 刀鋒視窗](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

它可能會佔用 hello 度量 toobe hello 上可見的 tooone 小時**監視**刀鋒視窗因為度量彙總每小時發生。

### <a name="set-up-an-alert-on-metrics"></a>設定度量警示
按一下 hello **Data Factory 度量**磚：

![Data Factory 度量圖格](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

在 [hello**度量**刀鋒視窗中，按一下 [ **+ 新增警示**hello 工具列上。
![Data Factory 度量刀鋒視窗 > 新增警示](./media/data-factory-monitor-manage-pipelines/add-alert.png)

在 [hello**加入警示規則**頁面上，執行 hello 下列步驟，然後按一下**確定**。

* 輸入 hello 警示的名稱 (範例: 「 失敗通知 」)。
* 輸入 hello 警示的描述 (範例: 「 發生失敗時傳送電子郵件 」)。
* 選取度量 (「失敗的執行」與「成功的執行」)。
* 指定條件和臨界值。   
* 指定 hello 一段時間。
* 指定 tooowners、 參與者與讀者，是否應傳送電子郵件。

![Data Factory 度量刀鋒視窗 > 新增警示規則](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Hello 警示規則已順利新增，hello 刀鋒視窗會關閉，您看到 hello 新的警示上 hello 之後**度量**刀鋒視窗。

![Data Factory 度量刀鋒視窗 > 已新增警示](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

您也應該會看到 hello hello 中的警示數目**警示規則**磚。 按一下 hello**警示規則**磚。

![Data Factory 度量刀鋒視窗 - 新增規則](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

在 [hello**警示規則**刀鋒視窗中，您會看到任何現有的警示。 按一下警示，tooadd**新增警示**hello 工具列上。

![警示規則刀鋒視窗](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>警示通知
Hello 警示規則的比對 hello 條件之後，您應該取得指出啟動 hello 警示的電子郵件。 Hello 問題已解決和 hello 警示條件不符合不再之後，您會收到電子郵件，指出 hello 警示已解決。

此行為不同於事件，其會針對警示規則相符的每個失敗傳送通知。

### <a name="deploy-alerts-by-using-powershell"></a>使用 PowerShell 部署警示
您可以部署警示，如度量 hello 相同事件的方式。

**警示定義**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

取代*subscriptionId*， *resourceGroupName*，和*dataFactoryName* hello 範例以適當的值。

metricName 目前支援兩個值︰

* FailedRuns
* SuccessfulRuns

**部署 hello 警示**

toodeploy hello 警示，請使用 hello Azure PowerShell 指令程式**新增 AzureRmResourceGroupDeployment**hello 下列範例所示：

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

您應該會在部署成功後看到下列訊息：

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

您也可以使用 hello**新增 AlertRule** cmdlet toodeploy 警示規則。 請參閱 hello[新增 AlertRule](https://msdn.microsoft.com/library/mt282468.aspx)如需詳細資訊與範例的主題。  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>移動資料 factory tooa 不同的資源群組或訂用帳戶
您可以移動資料 factory tooa 不同的資源群組或不同的訂用帳戶使用 hello**移動**命令列上的 data factory 的 hello 首頁上的按鈕。

![移動 Data Factory](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

您也可以移動任何相關的資源 （例如警示與 hello data factory 相關聯），以及 hello 資料 factory。

![移動資源對話方塊](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
