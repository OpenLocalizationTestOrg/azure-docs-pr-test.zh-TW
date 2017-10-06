---
title: "在 Application Insights aaaUse Powershell tooset 警示 |Microsoft 文件"
description: "自動化設定 Application Insights tooget 電子郵件的相關度量的變更。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Application Insights 中使用 PowerShell tooset 警示
您可以自動化的 hello 設定[警示](app-insights-alerts.md)中[Application Insights](app-insights-overview.md)。

此外，您可以[設定 webhook tooautomate 回應 tooan 警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。

> [!NOTE]
> 如果您想 toocreate 資源和警示在 hello 相同的時間，請考慮[使用 Azure Resource Manager 範本](app-insights-powershell.md)。
>
>

## <a name="one-time-setup"></a>單次設定
若您未曾將 PowerShell 與 Azure 訂用帳戶搭配使用：

Hello toorun hello 指令碼所在的電腦上安裝 hello Azure Powershell 模組。

* 安裝 [Microsoft Web Platform Installer (v5 或更高版本)](http://www.microsoft.com/web/downloads/platform.aspx)。
* 它使用 tooinstall Microsoft Azure Powershell

## <a name="connect-tooazure"></a>連接 tooAzure
啟動 Azure PowerShell 和[連接 tooyour 訂閱](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>取得警示
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>Add alert
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>範例 1
電子郵件給我如果 hello 伺服器回應 tooHTTP 要求，超過 5 分鐘的平均值低於 1 秒。 我的 Application Insights 資源稱為 IceCreamWebApp，其位於 Fabrikam 資源群組。 我 hello hello Azure 訂用帳戶擁有者。

hello GUID 是 hello 訂用帳戶 ID （不 hello 檢測金鑰的 hello 應用程式）。

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>範例 2
我使用的應用程式有[trackmetric （)](app-insights-api-custom-events-metrics.md#trackmetric) tooreport 公制，名為"salesPerHour。 」 如果 「 salesPerHour"低於 100，平均過去 24 小時內，傳送電子郵件的同事 toomy。

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

使用 hello hello 相同的規則可用於 hello 公制報告[度量參數](app-insights-api-custom-events-metrics.md#properties)TrackEvent 或 trackPageView 等其他追蹤呼叫。

## <a name="metric-names"></a>度量名稱
| 度量名稱 | 畫面名稱 | 說明 |
| --- | --- | --- |
| `basicExceptionBrowser.count` |瀏覽器例外狀況 |無法攔截 hello 瀏覽器中擲回的例外狀況的計數。 |
| `basicExceptionServer.count` |伺服器例外狀況 |Hello 應用程式所擲回未處理的例外狀況的計數 |
| `clientPerformance.clientProcess.value` |用戶端處理時間 |Hello DOM 載入之前收到 hello 文件的最後一個位元組之間的時間。 系統可能仍在處理非同步要求。 |
| `clientPerformance.networkConnection.value` |頁面載入網路連線時間 |時間 hello 瀏覽器會 tooconnect toohello 網路。 可為 0 (若已快取)。 |
| `clientPerformance.receiveRequest.value` |接收回應時間 |瀏覽器傳送要求 toostarting tooreceive 回應之間的時間。 |
| `clientPerformance.sendRequest.value` |傳送要求時間 |瀏覽器 toosend 要求所花費的時間。 |
| `clientPerformance.total.value` |瀏覽器頁面載入時間 |從使用者要求直至載入 DOM、樣式表、指令碼和影像的經過時間。 |
| `performanceCounter.available_bytes.value` |可用的記憶體 |針對處理程序或系統用途的立即可用實體記憶體。 |
| `performanceCounter.io_data_bytes_per_sec.value` |處理程序 IO 速率 |每個第二個讀取和寫入的 toofiles、 網路和裝置的總位元組數。 |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |例外狀況比率 |每秒擲回的例外狀況。 |
| `performanceCounter.percentage_processor_time.value` |處理程序 CPU |hello hello 處理器 tooexecution 指示用於 hello 應用程式處理序的所有處理序執行緒的經過時間百分比。 |
| `performanceCounter.percentage_processor_total.value` |處理器時間 |花在非閒置執行緒的 hello 處理器時間的 hello 百分比。 |
| `performanceCounter.process_private_bytes.value` |處理程序私人位元組 |以獨佔方式指派 toohello 記憶體受監視應用程式的處理程序。 |
| `performanceCounter.request_execution_time.value` |ASP.NET 要求執行時間 |Hello 最近的要求執行時間。 |
| `performanceCounter.requests_in_application_queue.value` |執行佇列中的 ASP.NET 要求 |Hello 應用程式要求佇列的長度。 |
| `performanceCounter.requests_per_sec.value` |ASP.NET 要求率 |所有要求速率 toohello 應用程式每秒從 ASP.NET。 |
| `remoteDependencyFailed.durationMetric.count` |相依性失敗 |Hello 伺服器應用程式 tooexternal 資源失敗呼叫計數。 |
| `request.duration` |伺服器回應時間 |接收 HTTP 要求到完成傳送 hello 回應之間的時間。 |
| `request.rate` |要求率 |所有要求 toohello 應用程式每秒的速率。 |
| `requestFailed.count` |失敗的要求 |產生回應碼的 HTTP 要求計數 >= 400 |
| `view.count` |頁面檢視 |網頁的用戶端使用者要求計數。 系統會篩選掉綜合流量。 |
| {您的自訂度量名稱} |{您的度量名稱} |所報告您公制值[TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric)或 hello[測量呼叫的參數來追蹤](app-insights-api-custom-events-metrics.md#properties)。 |

hello 度量資訊會傳送不同遙測模組：

| 度量群組 | 收集器模組 |
| --- | --- |
| basicExceptionBrowser、<br/>clientPerformance、<br/>view |[瀏覽器 JavaScript](app-insights-javascript.md) |
| performanceCounter |[效能](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[相依性](app-insights-configuration-with-applicationinsights-config.md) |
| request、<br/>requestFailed |[伺服器要求](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhook
您可以[自動化回應 tooan 警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)。 Azure 會在出現警示時呼叫您選擇的網址。

## <a name="see-also"></a>另請參閱
* [指令碼 tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [從範本建立 Application Insights 和 Web 測試資源](app-insights-powershell.md)
* [自動化結合的 Microsoft Azure 診斷 tooApplication Insights](app-insights-powershell-azure-diagnostics.md)
* [自動化回應 tooan 警示](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
