---
title: "記錄分析資料與在 Azure 自動化 runbook aaaCollecting |Microsoft 文件"
description: "逐步教學課程會逐步引導您建立 runbook 在 Azure 自動化 toocollect 資料到記錄分析以進行分析的 hello OMS 儲存機制。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>使用 Azure 自動化 Runbook 在 Log Analytics 中收集資料
您可以在 Log Analytics 中收集來自各種來源 (包括代理程式上的[資料來源](../log-analytics/log-analytics-data-sources.md)) 的大量資料，以及[收集自 Azure 的資料](../log-analytics/log-analytics-azure-storage.md)。  雖然需要 toocollect 資料，無法存取透過這些標準的來源，則需要有案例。  在這些情況下，您可以使用 hello [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md) toowrite 資料 tooLog 分析來自任何 REST API 用戶端。  常見的方法 tooperform 此資料集合使用 Azure 自動化中的 runbook。   

本教學課程將引導 hello 程序建立和排定在 Azure 自動化 toowrite 資料 tooLog 分析中的 runbook。


## <a name="prerequisites"></a>必要條件
此案例需要下列設定您的 Azure 訂用帳戶中資源的 hello。  兩者都可以是免費帳戶。

- [Log Analytics 工作區](../log-analytics/log-analytics-get-started.md)。
- [Azure 自動化帳戶](../automation/automation-offering-get-started.md)。

## <a name="overview-of-scenario"></a>案例概觀
在本教學課程中，您將撰寫 Runbook 來收集自動化工作的相關資訊。  因此，您會藉由撰寫和測試指令碼在 hello Azure 自動化編輯器中啟動 PowerShell，以實作 Azure 自動化中的 Runbook。  一旦您確認您要收集 hello 所需的資訊，請將寫入該資料 tooLog 分析，並確認 hello 自訂資料類型。  最後，您將固定間隔建立排程 toostart hello runbook。

> [!NOTE]
> 您可以設定 Azure 自動化 toosend 作業資訊 tooLog 分析沒有此 runbook。  此案例中是主要使用的 toosupport hello 教學課程中，並建議您傳送嗨資料 tooa 測試工作區。  


## <a name="1-install-data-collector-api-module"></a>1.安裝資料收集器 API 模組
每個[hello HTTP 資料收集器 API 的要求](../log-analytics/log-analytics-data-collector-api.md#create-a-request)必須適當地格式化，並包含授權標頭。  您可以在您的 runbook，但您可以減少使用模組，可簡化此程序所需的程式碼的 hello 數量。  您可以使用的其中一個模組是[OMSIngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI)hello PowerShell 資源庫中。

toouse[模組](../automation/automation-integration-modules.md)在 runbook 中使用，它必須安裝在您的自動化帳戶。  Hello 接著可以使用相同的帳戶中的任何 runbook hello hello 模組中的函式。  在自動化帳戶中選取 [資產] > [模組] > [新增模組]，即可安裝新的模組。  

hello PowerShell 資源庫但是可讓您快速選項 toodeploy 模組直接 tooyour 自動化帳戶，因此您可以使用該選項在此教學課程。  

![OMSIngestionAPI 模組](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. 跳過[PowerShell 資源庫](https://www.powershellgallery.com/)。
2. 搜尋 **OMSIngestionAPI**。
3. 按一下 hello**部署 tooAzure 自動化** 按鈕。
4. 選取您的自動化帳戶，然後按一下**確定**tooinstall hello 模組。


## <a name="2-create-automation-variables"></a>2.建立自動化變數
[自動化變數](..\automation\automation-variables.md)會保留值，以供自動化帳戶中的所有 Runbook 使用。  它們會使 runbook 更多彈性，可讓您 toochange 而不需要編輯這些值 hello 實際的 runbook。 每個來自 hello HTTP 資料收集器 API 要求需要 hello 識別碼和金鑰的 hello OMS 工作區中，而且變數資產是理想的 toostore 這項資訊。  

![變數](media/operations-management-suite-runbook-datacollect/variables.png)

1. 在 hello Azure 入口網站，瀏覽 tooyour 自動化帳戶。
2. 選取 [共用資源] 下方的 [變數]。
2. 按一下**加入變數**和建立 hello hello 下表中的兩個變數。

| 屬性 | 工作區識別碼值 | 工作區索引鍵值 |
|:--|:--|:--|
| 名稱 | WorkspaceId | WorkspaceKey |
| 類型 | String | String |
| 值 | 記錄分析工作區的工作區識別碼 hello 中貼上。 | 主要或次要金鑰，記錄分析工作區的 hello 入貼上。 |
| 已加密 | 否 | 是 |



## <a name="3-create-runbook"></a>3.建立 Runbook

Azure 自動化有 hello 入口網站，您可以在其中編輯及測試您的 runbook 中的編輯器。  您已擁有 hello 選項 toouse hello 指令碼編輯器 toowork 與[直接 PowerShell](../automation/automation-edit-textual-runbook.md)或[建立圖形化 runbook](../automation/automation-graphical-authoring-intro.md)。  在本教學課程中，您將使用 PowerShell 指令碼。 

![編輯 Runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. 瀏覽 tooyour 自動化帳戶。  
2. 按一下 [Runbook] > [新增 Runbook] > [建立新的 Runbook]。
3. Hello runbook 名稱 中輸入**收集自動化工作**。  Hello runbook 類型 選取**PowerShell**。
4. 按一下**建立**toocreate hello runbook 並開始 hello 編輯器。
5. 複製並貼上下列程式碼至 hello runbook hello。  如需 hello 程式碼的說明，請參閱 toohello hello 指令碼中的註解。
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4.測試 Runbook
Azure 自動化中包含環境太[測試您的 runbook](../automation/automation-testing-runbook.md)之前將它發行。  您可以檢查 hello hello runbook 所收集的資料，並確認它寫入 tooLog 分析如預期般之前發行它 tooproduction。 
 
![測試 Runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. 按一下**儲存**toosave hello runbook。
1. 按一下**測試窗格**tooopen hello runbook hello 測試環境中的。
3. 因為您的 runbook 具有參數，所以您提示的 tooenter 它們的值。  輸入 hello hello 資源群組名稱，然後 hello 自動化帳戶從您進行 toocollect 作業資訊。
4. 按一下**啟動**toohello 啟動 hello runbook。
3. hello runbook 的狀態將會開始**排入佇列**會太之前**執行**。  
3. hello runbook 應該顯示 hello 工作收集 json 格式的詳細資訊輸出。  如果沒有列出任何工作，然後可能已有建立 hello 自動化帳戶中 hello 過去一小時內沒有工作。  嘗試啟動 hello 自動化帳戶中的任何 runbook，然後再次執行 hello 測試。
4. 請確定 hello 輸出不會顯示 hello 中的任何錯誤張貼命令 tooLog 分析。  您應該有類似 toohello 後的訊息。

    ![張貼輸出](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5.確認 Log Analytics 中的記錄
一旦 hello runbook 完成在測試中，且您確認已成功收到 hello 輸出，您可以確認已建立使用 hello 記錄[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)。

![記錄輸出](media/operations-management-suite-runbook-datacollect/log-output.png)

1. 在 hello Azure 入口網站，選取您的記錄分析工作區。
2. 按一下 [記錄搜尋]。
3. 下列命令的型別 hello`Type=AutomationJob_CL`按一下 hello [搜尋] 按鈕。 請注意 hello 記錄類型包含 _CL hello 指令碼中未指定的。  該尾碼是自動附加的 toohello 記錄類型 tooindicate 它是自訂的記錄檔類型。
4. 您應該會看到傳回表示該 hello runbook 正常運作的一或多個記錄。


## <a name="6-publish-hello-runbook"></a>6.發行 hello runbook
一旦您確認該 hello runbook 正確運作，您需要 toopublish，讓您可以在生產環境中執行它。  您可以繼續 tooedit，並測試 hello runbook 而不需修改 hello 已發佈的版本。  

![發佈 Runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. 傳回 tooyour 自動化帳戶。
2. 按一下 [Runbook]，並選取 [收集自動化工作]。
3. 按一下 [編輯]，然後按一下 [發佈]。
4. 按一下**是**集的 tooverify 先前想 toooverwrite hello 當發行版本。

## <a name="7-set-logging-options"></a>7.設定記錄選項 
測試中，您不能 tooview[詳細資訊輸出](../automation/automation-runbook-output-and-messages.md#message-streams)因為您在 hello 指令碼中設定 hello $VerbosePreference 變數。  針對實際執行，您需要 hello runbook tooset hello 記錄內容，如果您想 tooview 詳細資訊輸出。  在本教學課程中使用的 hello runbook，這會顯示傳送 tooLog 分析 hello json 資料。

![記錄和追蹤](media/operations-management-suite-runbook-datacollect/logging.png)

1. 在您的 runbook 的 hello 屬性選取**記錄與追蹤**下**Runbook 設定**。
2. 變更 hello 設定**記錄詳細資訊記錄**太**上**。
3. 按一下 [儲存] 。

## <a name="8-schedule-runbook"></a>8.排程 Runbook
hello 最常見方式 toostart runbook 會收集監視的資料是 tooschedule 它 toorun 自動。  您可以建立[Azure 自動化中的排程](../automation/automation-schedules.md)並將它附加 tooyour runbook。

![排程 Runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. 在您的 runbook 的 hello 屬性，選取**排程**下**資源**。
2. 按一下**加入排程** > **排程 tooyour runbook 連結** > **建立新的排程**。
5. Hello hello 排程，然後按一下值中的型別**建立**。

| 屬性 | 值 |
|:--|:--|
| 名稱 | AutomationJobs-Hourly |
| 啟動 | 選取任何至少 5 分鐘過去 hello 目前時間的時間。 |
| 週期性 | 週期性 |
| 重複頻率 | 1 小時 |
| 設定到期日 | 否 |

Hello 排程建立之後，您必須將用於每次這個排程啟動 hello runbook tooset hello 參數值。

6. 按一下 [設定參數與回合設定]。
7. 填入 **ResourceGroupName** 和 **AutomationAccountName** 的值。
8. 按一下 [確定] 。 

## <a name="9-verify-runbook-starts-on-schedule"></a>9.驗證 Runbook 會依排程啟動
每次啟動 Runbook 時，都會[建立作業](../automation/automation-runbook-execution.md)且會記錄任何輸出。  事實上，這些是的 hello 收集 hello runbook 的相同工作。  您可以確認該 hello runbook 啟動如預期般 hello hello 排程的開始時間經過後檢查 hello hello runbook 工作。

![工作](media/operations-management-suite-runbook-datacollect/jobs.png)

1. 在您的 runbook 的 hello 屬性，選取**作業**下**資源**。
2. 您應該會看到每個時間 hello runbook 工作的清單已啟動。
3. 按一下其中一個 hello 作業 tooview 其詳細資料。
4. 按一下**所有記錄檔**tooview hello 記錄檔和 hello runbook 的輸出。
5. 捲動 toohello 底部 toofind 項目類似 toohello 下面的影像。<br>![詳細資訊](media/operations-management-suite-runbook-datacollect/verbose.png)
6. 按一下這個項目 tooview hello json 的詳細資料已傳送 tooLog 分析。



## <a name="next-steps"></a>後續步驟
- 使用[檢視表設計工具](../log-analytics/log-analytics-view-designer.md)toocreate 檢視顯示 hello 您收集了 toohello 記錄分析儲存機制的資料。
- 封裝您的 runbook 中[管理解決方案](operations-management-suite-solutions-creating.md)toodistribute toocustomers。
- 深入了解 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/)。
- 深入了解 [Azure 自動化](https://docs.microsoft.com/azure/automation/)。
- 深入了解 hello [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md)。
