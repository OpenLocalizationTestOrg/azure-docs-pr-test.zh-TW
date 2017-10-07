---
title: "監視產品比較 aaaMicrosoft |Microsoft 文件"
description: "Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。  這份文件識別包含在 OMS 中的 hello 不同服務，並提供連結 tootheir 詳細內容。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Microsoft 監視產品比較
本文章提供 System Center Operations Manager (SCOM) 與記錄分析 Operations Management Suite (OMS) 之間的比較，其架構、 它們如何監視資源，以及執行 hello 資料分析的 hello 邏輯方面它們收集。  這是 toogive 您基本的了解其差異和相對優勢。  

## <a name="basic-architecture"></a>基本架構
### <a name="system-center-operations-manager"></a>System Center Operations Manager
所有 SCOM 元件都已安裝在您的資料中心。  [代理程式已安裝](http://technet.microsoft.com/library/hh551142.aspx) 於 SCOM 所管理的 Windows 和 Linux 機器上。  代理程式連接太[管理伺服器](https://technet.microsoft.com/library/hh301922.aspx)與 hello SCOM 資料庫和資料倉儲的通訊。  代理程式會依賴網域驗證 tooconnect toomanagement 伺服器。  受信任網域以外可以執行憑證驗證，或連線 tooa[閘道伺服器](https://technet.microsoft.com/library/hh212823.aspx)。

SCOM 需要兩個 SQL 資料庫，一個用於作業中的資料，另一個資料倉儲 toosupport 報告和資料分析。  A [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx)資料上執行 SQL Reporting Services tooreport，從 hello 資料倉儲。 

SCOM 可以使用 [Azure](https://www.microsoft.com/download/details.aspx?id=38414)、[Office 365](https://www.microsoft.com/download/details.aspx?id=43708) 和 [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html)等產品的管理組件來監視雲端資源。  這些管理組件使用一個或多個本機代理程式，為探索 proxy 雲端資源和執行工作流程 toomeasure，其效能和可用性。  Proxy 代理程式也會使用太[監視網路裝置](https://technet.microsoft.com/library/hh212935.aspx)和其他外部資源。

hello Operations 主控台是連線 tooone hello 管理伺服器和允許 hello 管理員 tooview 及分析收集到的資料，並設定 hello SCOM 環境的 Windows 應用程式。  Web 式主控台可以裝載於任何 IIS 伺服器上並透過瀏覽器提供資料分析。

![SCOM 架構](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
大部分的 OMS 元件是 hello Azure 雲端中，因此您可以部署和管理具有最低成本和系統管理工作。  記錄分析所收集的所有資料都會都儲存在 hello OMS 儲存機制。

Log Analytics 也可以從下列三個來源收集資料：

* 實體和虛擬機器執行 Windows 和 hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx)或 Linux 和 hello [Operations Management Suite Agent for Linux](https://technet.microsoft.com/library/mt622052.aspx)。  這些電腦可以是 Azure 或其他雲端中的內部部署或虛擬機器。
* Azure 儲存體帳戶，其具有 Azure 背景工作角色、Web 角色或虛擬機器所收集的 [Azure 診斷](../cloud-services/cloud-services-dotnet-diagnostics.md) 資料。
* [連接 tooa SCOM 管理群組](https://technet.microsoft.com/library/mt484104.aspx)。  在此組態中，與 SCOM 管理伺服器傳送嗨資料 toohello SCOM 資料庫，然後傳遞 toohello OMS 資料存放區 hello 代理程式進行通訊。
  系統管理員會分析收集到的資料，並設定 hello OMS 入口網站，其會裝載於 Azure，而且可以從任何瀏覽器存取記錄分析。  行動裝置應用程式 tooaccess 這項資料可供 hello 標準平台。

![Log Analytics 架構](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>整合 SCOM 與 Log Analytics
記錄分析使用 SCOM 做為資料來源時，您可以利用兩個產品在混合式監視環境中的 hello 功能。  您可以設定現有的 SCOM 代理程式，透過 hello Operations 主控台 toobe OMS 所管理，除了 toocontinuing toorun 管理組件從 SCOM。  
從已連線的 SCOM 管理群組的資料傳送 tooLog 分析使用四種方法之一：

* 事件和效能資料，會由 hello 代理程式收集並傳遞 tooSCOM。  SCOM 中的管理伺服器然後傳送 hello 資料 tooLog 分析。
* 某些事件，例如 IIS 記錄檔和安全性事件繼續 toobe 直接 tooLog 分析會從傳送嗨代理程式。
* 某些解決方案將會提供額外的軟體 toohello 代理程式或軟體必須安裝的 toocollect 額外的資料。  這項資料將通常會傳送直接 tooLog 分析。
* 部分解決方案會直接從 SCOM 管理伺服器，不是來自 hello 代理程式收集資料。  例如，hello[警示管理解決方案](https://technet.microsoft.com/library/mt484092.aspx)它們建立之後，從 SCOM 收集警示。

## <a name="monitoring-logic"></a>監視邏輯
SCOM 和記錄分析與類似從代理程式收集的資料搭配使用，但有基本差異，其定義和實作資料收集其邏輯的方式和它們如何分析其所收集的 hello 資料中。

### <a name="operations-manager"></a>Operations Manager
監視邏輯中實作 SCOM[管理組件](https://technet.microsoft.com/library/hh457558.aspx)其中包含的邏輯來探索元件 toomonitor，測量 hello 健全狀況的這些元件，並收集資料 tooanalyze。  監視資料可與收集事件或效能計數器一樣簡單，或可以使用指令碼中實作的複雜邏輯。  包含完整的監視的管理組件可供各種不同的[Microsoft 和協力廠商應用程式](http://go.microsoft.com/fwlink/?LinkId=82105)加法 toohardware 和網路裝置中。  您可以針對自訂應用程式 [撰寫您自己的管理組件](http://aka.ms/mpauthor) 。

管理組件包含每個執行一些不同的監視功能，例如取樣效能計數器、 檢查 hello 狀態的服務，或執行指令碼的多個工作流程。  每個工作流程會獨立執行，並定義它自己結果，例如哪些資料庫則會寫入 tooand 是否會產生警示。 

您可以覆寫，例如 hello 頻率使用者執行，這些錯誤，請考慮 hello 臨界值的工作流程的詳細資料和 hello hello 它們產生的警示嚴重性。  您也可以加入您自己的工作流程，以提供其他功能。

![覆寫](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

管理組件會安裝在 hello Operations Manager 資料庫，並會自動散發 tooagents 管理伺服器。  每個代理程式會自動下載管理組件，並載入工作流程相關 toohello 應用程式安裝軟體。  Hello 代理程式所收集的資料傳遞到 hello SCOM 資料庫和資料倉儲後 toohello 插入作業的管理伺服器。  hello Operations 主控台可讓您 tooview 和分析這項資料透過自訂檢視、 儀表板和包含 hello 管理組件中的報表。

hello 發佈的管理組件以 hello 下列圖表所示。

![管理組件流程](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>事件和效能集合
Log Analytics 會從使用 Windows 事件記錄檔、IIS 記錄檔和 Syslog 等來源的代理程式系統收集事件和效能計數器。  您可以定義的條件的資料會收集透過 hello 記錄分析入口網站，然後建立記錄檔查詢 tooanalyze hello 收集資料。  當您建立 OMS 工作區時，會定義一組標準準則，而您可以針對特定應用程式定義其他資料。 

![在 Log Analytics 中定義事件記錄檔](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

雖然 SCOM 有許多通常會定義之資料的特定準則的詳細工作流程和 hello 動作應該執行以回應，記錄分析會有多個一般準則的資料收集。  記錄查詢及解決方案提供多目標的準則來分析及已收集後代表 hello 雲端中的特定資料。

#### <a name="solutions"></a>解決方案
解決方案會提供資料收集和分析的額外邏輯。  您可以從 hello 解決方案資源庫選取解決方案 tooadd tooyour OMS 訂用帳戶。

![方案庫](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

在提供的事件和效能計數器收集 hello OMS 儲存機制中分析的 hello 雲端中主要是執行方案。  它們也可以定義其他資料 toobe 收集記錄的查詢或 hello OMS 儀表板中的 hello 方案所提供的其他使用者介面可分析。 

例如，hello[變更追蹤解決方案](https://technet.microsoft.com/library/mt484099.aspx)偵測組態變更代理程式的系統上，並將事件 toohello OMS 儲存機制，可以分析與彙總的多個圖形化檢視偵測到變更。  您可以向下鑽研從 hello 彙總檢視的記錄檔查詢該顯示 hello 詳細 hello 解決方案所收集的資料。

雖然您可以選取哪些解決方案新增 tooyour 訂用帳戶，您目前沒有 hello 能力 toocreate 專屬的解決方案。  您可以選取 hello 事件和效能計數器 toocollect，並建立您自己的記錄檔查詢為基礎的自訂檢視。

記錄分析的監視邏輯 hello 都摘要在下列圖表中的 hello。

![Log Analytics 方案流程](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>健康狀態監視
### <a name="operations-manager"></a>Operations Manager
SCOM 可以 hello 不同元件的應用程式模型，並針對每個提供即時的健全狀況。  這可讓您 toonot 僅檢視偵測到錯誤和經過一段時間的效能，但 toovalidate 也 hello 實際的應用程式或系統的健全狀況和每個元件在任何指定時間。  因為其了解 hello 應用程式所提供的時間週期，在 SCOM 中的 hello 健全狀況引擎也支援服務等級協定 (SLA) 的分析和報告 hello 應用程式可用性的一段時間。

例如，下列的 hello 檢視會顯示 hello 由 SCOM 監視的 SQL 資料庫引擎的即時健全狀況。  每個 hello 資料庫引擎的其中一個 hello 資料庫 hello 健全狀況會顯示 hello 下方 hello 檢視的下半部。

![狀態檢視](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

hello hello 資料庫引擎的其中一個健全狀況總管如下所示 hello 監視器使用的 toodetermine 的整體健康狀況。  這些監視器會 hello SQL 管理組件中定義，並針對探索到的 SCOM 的所有 SQL 資料庫引擎執行。

![健康狀態總管](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

多個系統上的元件可以結合的 toomeasure hello 健全狀況的分散式應用程式。  這特別適合用於包含多個分散式元件的企業營運應用程式。  您可以建立量值的每個元件的 hello 健全狀況模型的彙總套件，到 hello 應用程式的可用性。

Active Directory 是一個管理組件可提供模型 tooanalyze 其分散式的元件的範例。  hello 範例圖表下方顯示 hello 健全狀況的 hello 整體環境和 hello 樹系、 網域和網域控制站之間的關聯性。  每個這些元件包括子元件和多個監視器類似 toohello SQL 上述範例。

![SCOM 圖表檢視](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS 不包含常見的引擎 toomodel 應用程式或測量其即時健康情況。  個別解決方案可能評估 hello 的特定服務的整體健全狀況根據收集的資料，而它們可能會安裝自訂邏輯 hello 代理程式 tooperform 即時分析。  在以存取 toohello OMS 儲存機制的 hello 雲端中執行方案，因為它們通常可以提供比通常是由管理組件的深入分析。 

例如，hello [AD 評估和 SQL 評估解決方案](https://technet.microsoft.com/library/mt484102.aspx)分析收集到的資料，並提供 hello 環境的不同層面的等級。  其中包括改良功能，才能進行的 hello 環境 tooimprove hello 可用性與效能的建議。

![AD 評估方案](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>資料分析
SCOM 和記錄分析每個提供不同功能 tooanalyze 收集資料。  SCOM 檢視和儀表板中有 hello Operations 主控台來分析各種不同的格式，呈現表格式表單中的 hello 資料倉儲中資料的報表中新資料。  記錄分析會提供完整的記錄檔查詢語言和介面來分析 hello OMS 儲存機制中的資料。  SCOM 做為資料來源使用的記錄分析時，hello 儲存機制包含使 hello 記錄分析工具能夠使用的 tooanalyze 資料，從兩個系統，SCOM 所收集的資料。

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Views
Hello Operations 主控台中的檢視可讓您 tooview 不同的資料類型不同的格式，如事件、 警示和狀態資料和效能資料的折線圖通常表格式收集 SCOM。  檢視執行最少的分析或彙總的 hello 資料，但不要讓您根據 tooparticular 準則 toofilter。 

![Views](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

管理組件通常會提供支援 hello 應用程式或系統，它會監視的多個檢視。  這可能包括 hello hello 管理組件探索的不同物件的狀態檢視、 警示檢視偵測到的問題和計數器的效能檢視。

檢視是特別適用於分析 hello hello 環境包括未解決的警示和 hello 健全狀況狀態監視的系統和物件的目前狀態。  您可以向下鑽研 toodetailed 事件或效能資料順序 toodiagnose 中支援的特定警示的根本原因。 同樣地，您可以檢視 hello 效能和健全狀況的不同元件的應用程式 tooassess 其目前的健全狀況。

#### <a name="dashboards"></a>儀表板
Hello 主要使用 Operations 主控台的儀表板 hello 相同的資料檢視但更可自訂，以及可以包含更豐富的視覺效果。  有一組標準儀表板可供您使用，以便針對您的用途輕鬆地自訂。  您也可以使用 PowerShell Widget，其可顯示 PowerShell 查詢所傳回的資料。

![儀表板](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

開發人員需要 hello 能力 tooadd 自訂元件 toodashboards 它們包含在其管理組件。  這些可能是非常特殊的 tooa 特定應用程式，例如 hello 如下所示的 SQL 管理組件中的 hello 儀表板。  此儀表板也可做為自訂版本的範本。

![SQL 儀表板](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>報告
SCOM 中的報表會分析在表格式表單中的 hello 資料倉儲中的資料。  您可加以列印和排程，以便以不同的檔案格式 (包括 PDF、CSV 及 Word) 自動交付。  報表會使用 hello 資料倉儲中的資料，讓它們特別適用於長期趨勢分析。

管理組件通常會提供特定應用程式的自訂報告。  您也可以從可針對自己的應用程式自訂或可供執行臨機操作分析的一般報告庫選取。

以下是範例效能報表，顯示 hello Active Directory Management Pack 所收集的資料。

![報告](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
記錄分析具有[查詢語言](https://technet.microsoft.com/library/mt484120.aspx)，您可以使用 tooperform 分析跨 hello 需要 toocreate 沒有多個應用程式資料的自訂檢視或報表。  由於 OMS 會實 hello 雲端中，查詢和資料分析的效能不主旨 tooany 硬體限制，而且可以快速地分析查詢包括數百萬筆記錄。 

記錄分析中的查詢也是 hello 其他功能的基礎。  您可以將查詢儲存、 匯出其結果 tooExcel，或讓它自動定期執行，並產生其結果符合特定準則的警示。  

![記錄檔查詢流程](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

以下是 Log Analytics 查詢的範例。  在此範例中傳回和分組事件中的 「 已啟動 」 hello 名稱中使用的所有事件識別碼。  hello 使用者只要提供 hello 查詢，並記錄分析會動態產生 hello 使用者介面 tooperform hello 分析。  Hello 清單中選取任何項目將會傳回 hello 詳細事件資料。

![記錄檔查詢](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

此外 tooproviding 臨機操作分析，記錄分析中的查詢可以儲存為未來使用，並且加入的 tooyour [OMS 儀表板](http://technet.microsoft.com/library/mt484090.aspx)hello 下列範例所示。

![OMS 儀表板](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>後續步驟
* 部署 [System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx)。
* 註冊 [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics)。  

