---
title: "aaaMonitor 及管理串流分析工作，使用 PowerShell |Microsoft 文件"
description: "深入了解如何 toouse Azure PowerShell 及指令程式 toomonitor 及管理串流分析工作。"
keywords: "azure powershell, azure powershell cmdlet, powershell 命令, powershell 指令碼"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>透過 Azure PowerShell Cmdlet 監視和管理串流分析工作
深入了解如何 toomonitor 和管理執行基本的資料流分析工作的資料流分析資源使用 Azure PowerShell cmdlet 和 powershell 指令碼。

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>執行 Azure PowerShell Cmdlet 進行串流分析的必要條件
* 在您的訂用帳戶中建立「Azure 資源群組」。 hello 以下是範例 Azure PowerShell 指令碼。 如需 Azure PowerShell 資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。  

Azure PowerShell 0.9.8：  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0：  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> 以程式控制方式建立的串流分析工作預設不會啟用監視功能。  您可以手動啟用 hello Azure 入口網站，瀏覽 toohello 作業的 [監視] 頁面中的監視和 hello [啟用] 按鈕，或按一下 [可執行這項操作以程式設計方式位於 hello 步驟[Azure Stream Analytics 監視資料流分析作業以程式設計方式控制程式](stream-analytics-monitor-jobs.md)。
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>用於串流分析的 Azure PowerShell Cmdlet
hello 下列 Azure PowerShell 指令程式可以是使用的 toomonitor 及管理 Azure Stream Analytics 工作。 請注意，Azure PowerShell 有不同的版本。 
**在 hello 範例中所列的 hello 第一個命令是適用於 Azure PowerShell 為 0.9.8，hello 第二個命令會為 Azure PowerShell 1.0。** hello Azure PowerShell 1.0 命令永遠會 「 AzureRM"hello 命令。

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
列出在 hello Azure 訂用帳戶或指定的資源群組中定義的所有串流分析工作，或取得資源群組內的特定作業的作業資訊。

**範例 1**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsJob

這個 PowerShell 命令會傳回 hello Azure 訂用帳戶中的 hello 的所有資料流分析工作的相關資訊。

**範例 2**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

這個 PowerShell 命令會傳回 hello StreamAnalytics 預設中央-美國的資源群組中所有 hello 資料流分析工作的相關資訊。

**範例 3**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

這個 PowerShell 命令傳回 hello StreamAnalytics 預設中央-美國的資源群組中的 hello StreamingJob 的資料流分析工作的相關資訊。

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
列出所有 hello 輸入定義中指定的資料流分析工作，或取得特定的輸入的相關資訊。

**範例 1**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

此 PowerShell 命令會傳回所有 hello 輸入 hello 作業 StreamingJob 中定義的相關資訊。

**範例 2**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

這個 PowerShell 命令會傳回名為 EntryStream hello 作業 StreamingJob 中定義的 hello 輸入相關資訊。

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
列出所有 hello 輸出中指定的資料流分析工作，所定義，或取得有關特定輸出的資訊。

**範例 1**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

此 PowerShell 命令會傳回 hello 輸出 hello 作業 StreamingJob 中定義的相關資訊。

**範例 2**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

此 PowerShell 命令會傳回名為 hello 作業 StreamingJob 中定義的輸出 hello 輸出的相關資訊。

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
取得資料流處理單位，指定區域中的 hello 配額的相關資訊。

**範例 1**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

這個 PowerShell 命令會傳回 hello 美國中部地區中的 hello 配額和使用量的資料流處理單位的相關資訊。

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
取得在串流分析工作中定義之特定轉換的相關資訊。

**範例 1**

Azure PowerShell 0.9.8：  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0：  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

此 PowerShell 命令會傳回呼叫 StreamingJob hello 作業 StreamingJob 中的 hello 轉換的相關資訊。

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
在串流分析工作內建立新的輸入，或更新現有的指定輸入。

hello hello 輸入名稱可以指定在 hello.json 檔案或 hello 命令列。 如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。

如果您指定已存在的輸入，並沒有指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有輸入。

如果您指定 hello – Force 參數，並指定現有的輸入名稱、 hello 輸入將會被取代，但不用確認。

如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立輸入 (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input]區段 hello[資料流分析管理 REST API參考文件庫][stream.analytics.rest.api.reference]。

**範例 1**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

這個 PowerShell 命令會從 hello 檔案 Input.json 建立新的輸入。 如果已經定義 hello hello 輸入的定義檔中指定的名稱與現有的輸入，hello cmdlet 會詢問是否 tooreplace 它。

**範例 2**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

這個 PowerShell 命令呼叫 EntryStream hello 作業中建立新的輸入。 如果已定義具有此名稱的現有輸入，hello cmdlet 會詢問是否 tooreplace 它。

**範例 3**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

這個 PowerShell 命令會取代現有 hello 與 hello 檔案中的 hello 定義稱為 EntryStream 輸入來源的 hello 定義。

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
在 Microsoft Azure 中建立新的資料流分析工作，或更新現有的指定工作的 hello 定義。

hello.json 檔案中或 hello 命令列上，可以指定 hello hello 作業名稱。 如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。

如果您指定工作名稱已存在且未指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有的工作。

如果您指定 hello – Force 參數，並指定現有的作業名稱，將取代 hello 工作定義，但不用確認。

如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立串流分析工作][ msdn-rest-api-create-stream-analytics-job]區段 hello [Stream Analytics Management REST API 參考程式庫][stream.analytics.rest.api.reference]。

**範例 1**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

這個 PowerShell 命令會從 JobDefinition.json 中的 hello 定義建立新的工作。 如果已經定義 hello hello 工作定義檔中指定的名稱與現有的工作，hello cmdlet 會詢問是否 tooreplace 它。

**範例 2**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

這個 PowerShell 命令會取代 StreamingJob 的 hello 工作定義。

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
在串流分析工作內建立新的輸出，或更新現有的輸出。  

hello.json 檔案中或 hello 命令列上，可以指定 hello hello 輸出名稱。 如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。

如果您指定已存在的輸出，且未指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有的輸出。

如果您指定 hello – Force 參數，並指定現有的輸出名稱、 hello 輸出將會被取代，但不用確認。

如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立輸出 (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output]區段 hello[資料流分析管理 REST API參考文件庫][stream.analytics.rest.api.reference]。

**範例 1**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

這個 PowerShell 命令建立新的輸出 hello 作業 StreamingJob 中稱為 「 輸出 」。 如果已定義具有此名稱的現有輸出，hello cmdlet 會詢問是否 tooreplace 它。

**範例 2**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

這個 PowerShell 命令會取代 「 輸出 」 hello 作業 StreamingJob 中的 hello 定義。

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
建立新的轉換資料流分析工作內，或更新現有 hello 的轉換。

hello.json 檔案中或 hello 命令列上，則可以指定 hello 轉換 hello 名稱。 如果同時指定 hello hello 命令列上的名稱必須 hello 與 hello 檔案中的 hello 一個相同。

如果您指定的轉換已經存在，且未指定 hello – Force 參數，hello cmdlet 會詢問是否 tooreplace hello 現有的轉換。

如果您指定 hello – Force 參數，並指定現有的轉換名稱，將取代 hello 轉換，但不用確認。

如需 hello JSON 檔案的結構與內容的詳細資訊，請參閱 toohello[建立轉換 (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] hello 區段[資料流分析管理REST API 參考文件庫][stream.analytics.rest.api.reference]。

**範例 1**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

這個 PowerShell 命令建立新的轉換稱為 StreamingJobTransform hello 作業 StreamingJob 中。 如果現有的轉換已經定義此名稱，hello cmdlet 會詢問是否 tooreplace 它。

**範例 2**

Azure PowerShell 0.9.8：  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0：  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 這個 PowerShell 命令會取代在 hello 工作 StreamingJob StreamingJobTransform hello 定義。

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
以非同步方式從 Microsoft Azure 中的 Stream Analytics 作業刪除特定的輸入。  
如果您指定 hello – Force 參數，輸入 hello 將會刪除但不用確認。

**範例 1**

Azure PowerShell 0.9.8：  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0：  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

這個 PowerShell 命令，移除 hello 輸入的 EventStream hello 作業 StreamingJob 中。  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
以非同步方式從 Microsoft Azure 中刪除特定的 Stream Analytics 作業。  
如果您指定 hello – Force 參數，hello 作業將會刪除但不用確認。

**範例 1**

Azure PowerShell 0.9.8：  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0：  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

這個 PowerShell 命令移除 hello 作業 StreamingJob。  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
以非同步方式從 Microsoft Azure 中的 Stream Analytics 作業刪除特定的輸出。  
如果您指定 hello – Force 參數，hello 輸出將會刪除但不用確認。

**範例 1**

Azure PowerShell 0.9.8：  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0：  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

此 PowerShell 命令移除 hello hello 作業 StreamingJob 中輸出輸出。  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
以非同步方式部署和啟動 Microsoft Azure 中的 Stream Analytics 作業。

**範例 1**

Azure PowerShell 0.9.8：  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0：  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

這個 PowerShell 命令，開始 hello 的作業 StreamingJob 自訂輸出的開始時間設定 tooDecember 12，2012，12:12:12 UTC。

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
以非同步方式停止在 Microsoft Azure 中執行 Stream Analytics 作業，並取消配置正在使用的資源。 hello 工作定義和中繼資料依然會有效 hello Azure 入口網站和管理 Api，透過您訂用帳戶內，hello 作業可以編輯和重新啟動。 您不被支付 hello 停止狀態中的工作。

**範例 1**

Azure PowerShell 0.9.8：  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0：  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

這個 PowerShell 命令停止 hello 工作 StreamingJob。  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
測試資料流分析 tooconnect tooa hello 能力指定輸入。

**範例 1**

Azure PowerShell 0.9.8：  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0：  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

此 PowerShell 命令測試 hello 連線狀態的 hello 輸入 EntryStream StreamingJob 中的。  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
測試資料流分析 tooconnect tooa hello 能力指定輸出。

**範例 1**

Azure PowerShell 0.9.8：  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0：  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

此 PowerShell 命令測試 hello 連線狀態的 hello 輸出 StreamingJob 中的輸出。  

## <a name="get-support"></a>取得支援
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。 

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

