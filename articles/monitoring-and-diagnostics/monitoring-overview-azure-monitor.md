---
title: "aaaAzure 監視器概觀 |Microsoft 文件"
description: "Azure 監視器會收集用於警示、webhook、自動調整，以及自動化的統計資料。 文章也會列出其他 Microsoft 監視選項。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Azure 監視器的概觀
本文章提供 hello Azure 監視 Microsoft Azure 服務的概觀。 其中也會討論 Azure 監視器沒有以及提供如何指標 tooadditional 相關資訊 toouse Azure 監視器。  如果您偏好的影片介紹，請參閱這篇文章 hello 底部的下一個步驟連結。 

## <a name="why-monitor-your-application-or-system"></a>為什麼要監視您的應用程式或系統
雲端應用程式相當複雜，且具有許多移動組件。 監視提供您的應用程式保持啟動的資料 tooensure 和狀況良好的狀態中執行。 它也可協助您 toostave 關閉潛在的問題或過去的疑難排解。 此外，您可以使用監視資料 toogain 深入了解有關應用程式。 該知識可以幫助您 tooimprove 應用程式效能或可維護性，或自動化需要手動介入的動作。


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure 監視器及 Microsoft 的其他監視產品
Azure 監視器可針對 Microsoft Azure 中的大多數服務提供基本等級的基礎結構計量與記錄。 請勿尚未將其資料放到 Azure 監視的 azure 服務會將它放那里 hello 在未來。

Microsoft 隨附額外的產品和服務，可針對同時擁有內部部署安裝的開發人員、DevOps 及 IT Ops 提供其他監視功能。 如需概觀及了解這些不同產品和服務如何一起運作的相關資訊，請參閱 [Microsoft Azure 中的監視](monitoring-overview.md)。

## <a name="monitoring-sources---compute"></a>監視來源：計算

![非計算資源的監視與診斷模型](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

包含 hello 計算服務 
- 雲端服務 
- 虛擬機器 
- 虛擬機器擴展集 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>應用程式 - 診斷記錄檔、應用程式記錄檔及計量
應用程式可以 hello 計算模型中的 hello 客體作業系統上執行。 它們會發出自己的記錄檔和計量集合。 Azure 監視依賴 hello Azure 診斷擴充功能 （Windows 或 Linux） toocollect 大部分的應用程式層級度量和記錄檔。 hello 類型包括

* 效能計數器
* 應用程式記錄檔
* Windows 事件記錄檔
* .NET 事件來源
* IIS 記錄檔
* 以資訊清單為基礎的 ETW
* 損毀傾印
* 客戶錯誤記錄檔

沒有 hello 診斷擴充功能，只有幾個計量，例如 CPU 使用量可用。 

### <a name="host-and-guest-vm-metrics"></a>主機和客體 VM 計量
hello 先前所列的計算資源都有專用的主機 VM 和客體作業系統與它們互動。 hello 主機 VM 和客體作業系統是根 VM 的 hello 對等項目和 hello HYPER-V hypervisor 模型中的客體 VM。 您可以同時收集這兩者的計量。 您也可以在 hello 客體作業系統上收集診斷記錄檔。   

### <a name="activity-log"></a>活動記錄檔
您可以在 hello Azure 基礎結構所偵測到您資源的相關資訊的搜尋 hello （先前稱為操作或稽核記錄檔） 的活動記錄檔。 hello 記錄包含資源時所建立或終結的時間等資訊。  如需詳細資訊，請參閱[活動記錄概觀](monitoring-overview-activity-logs.md)。 

## <a name="monitoring-sources---everything-else"></a>監視來源：其他項目

![計算資源的監視與診斷模型](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>資源 - 計量和診斷記錄檔
可收集度量和診斷的記錄檔會根據 hello 資源類型而有所不同。 比方說，Web 應用程式會提供對 hello 磁碟 IO 和百分比的 CPU 統計資料。 服務匯流排佇列沒有那些計量，而是改為提供佇列大小和訊息輸送量等計量。 [支援的計量](monitoring-supported-metrics.md)中提供可針對每個資源收集的計量清單。 

### <a name="host-and-guest-vm-metrics"></a>主機和客體 VM 計量
您的資源和特定主機或客體 VM 之間不一定具有 1:1 的對應，因此沒有計量可供使用。

### <a name="activity-log"></a>活動記錄檔
hello 活動記錄檔是 hello 與計算資源相同。  

## <a name="uses-for-monitoring-data"></a>監視資料的用途
一旦您收集資料，您可以執行 hello 與其依照 Azure 監視器

### <a name="route"></a>路由
您可以串流即時監視資料 tooother 位置。

範例包括：

- 傳送 tooApplication Insights，因此您可以使用其更豐富的視覺效果與分析工具。
- 傳送 tooEvent 中心，因此您可以在路由 toothird 廠商工具。 

### <a name="store-and-archive"></a>儲存與封存
某些監視資料已經在 Azure 監視器中儲存一段時間且可供使用。 
- 計量會儲存 30 天。 
- 活動記錄項目會儲存 90 天。 
- 診斷記錄完全不會儲存。 

如果您想要 toostore 資料超過 hello 上面所列的時間週期，您可以使用 Azure 儲存體。 監視資料會根據您設定的保留原則，保留於您的儲存體帳戶中。 您需要資料所佔用的 Azure 儲存體中的 hello 空間 hello 的 toopay。 

幾個方式 toouse 這項資料：

- 資料寫入後，您可以讓其他位於 Azure 之內或之外的工具讀取該資料並加以處理。
- 您下載 hello 資料在本機上的本機封存，或變更您保留原則 hello 雲端 tookeep 資料中的很長的時間。  
- 將 hello 資料保留在 Azure 儲存體無限期地進行封存。 

### <a name="query"></a>查詢
您可以使用 hello Azure 監視 REST API，跨平台命令列介面 (CLI) 命令，PowerShell cmdlet 或 hello.NET SDK tooaccess hello hello 系統或 Azure 儲存體中的資料

範例包括：

* 針對您所撰寫的自訂監視應用程式取得資料
* 建立自訂查詢，並傳送該資料 tooa 第三方應用程式。

### <a name="visualize"></a>視覺化
視覺化您的監視資料圖形和圖表，可協助您找到趨勢比 hello 資料本身，尋找更快。  

幾個視覺化方法包括︰

* 使用 hello Azure 入口網站
* 路由資料 tooAzure Application Insights
* 路由資料 tooMicrosoft PowerBI
* 路由 hello tooa 協力廠商視覺效果工具使用資料是即時資料流，或從 Azure 儲存體中封存讀取擁有 hello 工具


### <a name="automate"></a>自動化
您可以使用監視資料 tootrigger 警示，或甚至整個處理程序。 範例包括：

* 使用資料 tooautoscale 運算執行個體向上或向下根據應用程式負載。
* 在某個計量超過預先定義的臨界值時傳送電子郵件。
* 呼叫 web URL (webhook) tooexecute Azure 外部系統中的動作
* 在 Azure 自動化 tooperform 任何各種工作啟動 runbook

## <a name="methods-of-accessing-azure-monitor"></a>存取 Azure 監視器的方法
一般情況下，您可以操作資料追蹤功能、 路由及使用其中一種 hello 遵循方法擷取。 並非所有方法都適用所有動作或資料類型。

* [Azure 入口網站](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [跨平台命令列介面 (CLI)](insights-cli-samples.md)
* [REST API](https://docs.microsoft.com/rest/api/monitor/)
* [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>後續步驟
深入了解
- 僅 Azure 監視器的影片逐步解說位於  
[開始使用 Azure 監視器](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor)。 在[探索 Microsoft Azure 監視和診斷 (英文)](https://channel9.msdn.com/events/Ignite/2016/BRK2234) 和[來自 Ignite 2016 的 Azure 監視器影片 (英文)](https://myignite.microsoft.com/videos/4977) 可取得額外影片，該影片說明您可以使用 Azure 監視器的案例
- 透過 hello Azure 監視器 介面中執行[開始使用 Azure 監視器](monitoring-get-started.md)
- 設定 hello [Azure 診斷延伸模組](../azure-diagnostics.md)集或 Service Fabric 應用程式，如果您正嘗試 toodiagnose 問題，您的雲端服務，虛擬機器中擴充虛擬機器。
- [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/)如果您在應用程式服務 Web 應用程式中嘗試 toodiagnostic 問題。
- [疑難排解 Azure 儲存體](../storage/common/storage-e2e-troubleshooting.md) 
- [記錄分析](https://azure.microsoft.com/documentation/services/log-analytics/)和 hello [Operations Management Suite](https://www.microsoft.com/oms/)
