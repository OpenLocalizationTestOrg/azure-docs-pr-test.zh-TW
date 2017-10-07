---
title: "aaaIntegrating 與 Operations Management Suite (OMS) |Microsoft 文件"
description: "此外 toousing hello OMS 的標準功能，您可以在混合式管理環境、 tooprovide 自訂管理案例唯一 tooyour 環境或 tooprovide 自訂整合其他管理應用程式和服務 tooprovide管理您的客戶體驗。  本文提供不同的選項與 OMS 整合的概觀，以及連結 tooarticles 提供詳細的技術資訊。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fc5f3a8a-77f7-4103-bd7e-744c15ffcca7
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: dce752dcdc6c725bbafd49db4a5055750487ecf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-with-operations-management-suite-oms"></a>與 Operations Management Suite (OMS) 進行整合
Operations Management Suite 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。  此外 toousing hello OMS 的標準功能，您可以在混合式管理環境、 tooprovide 自訂管理案例唯一 tooyour 環境或 tooprovide 自訂整合其他管理應用程式和服務 tooprovide管理您的客戶體驗。  本文提供服務整合與 OMS 的不同選項的概觀，以及連結 tooarticles 提供詳細的技術資訊。 

## <a name="log-analytics"></a>Log Analytics
Log Analytics 收集的管理資料都會儲存到裝載於 Azure 的存放庫中。  在跨極大量的資料提供快速分析記錄搜尋中使用 hello 儲存機制中儲存的所有資料都。  整合需求可能 toopopulate hello 儲存機制進行分析，可用的新資料或 tooextract hello 儲存機制 tooprovide 新的視覺效果中的資料或 toointegrate 與其他管理工具。

每一筆 hello 儲存機制中的資料會儲存成一筆記錄。  當您填入 hello 儲存機制時，您應該提供使用者與您的方案使用的 hello 記錄類型和其屬性的描述。  當您擷取資料時，您會需要此資訊 hello 您正在使用的資料。

![填入 hello OMS 儲存機制](media/operations-management-suite-integration/repository.png)

### <a name="populate-hello-log-analytics-repository"></a>填入 hello 記錄分析儲存機制
有多種方法，用來填入 hello OMS 儲存機制。  hello 您所使用的方法，將取決於一些因素，例如 hello 來源資料所在的位置、 hello 格式的 hello 資料，以及哪些需要 toosupport 的用戶端。  一旦 hello 儲存機制中儲存資料，並沒有差別收集方式。

hello 下列各節說明 hello 填入 hello OMS 儲存機制的不同選項。

#### <a name="connected-sources-and-data-sources"></a>連接的來源和資料來源
已連線的來源為 hello hello OMS 儲存機制可以擷取資料的位置。  資料來源和解決方案連線來源上執行，並定義所收集的 hello 特定資料。  如果您的應用程式寫入這些資料來源的資料 tooone，然後您可以收集它藉由設定 hello 資料來源。  例如，如果您的應用程式建立 Syslog 事件，然後他們可以收集 hello Syslog 資料來源所 Linux 代理程式上。

* [Log Analytics 中的資料來源](../log-analytics/log-analytics-data-sources.md)

#### <a name="solutions"></a>解決方案
解決方案會擴充 OMS hello 功能。  解決方案可能 hello 連接來源收集資料，或它可能會在 hello 儲存機制中已收集的記錄上執行分析。  Microsoft 所提供的每個解決方案有個別發行項上 hello 收集資料，它提供 hello 詳細資料。

* [Log Analytics 中的解決方案](../log-analytics/log-analytics-add-solutions.md)

#### <a name="http-data-collector-api"></a>HTTP 資料收集器 API
hello 記錄分析 HTTP 資料收集器 API 是 REST API，可讓您 tooadd JSON 資料 toohello 記錄分析儲存機制。  當您有其他資料來源或解決方案不提供透過其中一個 hello 資料的應用程式時，您可以利用此 API。  它可以從任何用戶端可以呼叫 hello API 並不會依賴 hello 集合排程的任何資料來源或解決方案使用的 toopopulate hello 儲存機制。

* [Log Analytics HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md)

### <a name="retrieve-data-from-hello-log-analytics-repository"></a>Hello 記錄分析儲存機制中擷取資料
有多種方法，從 hello OMS 儲存機制擷取資料。  您可能想要使用 hello OMS 主控台使用者 tooretrieve 資料，並提供各種不同的視覺效果和分析。  您也可以擷取 hello 資料從外部處理序，例如另一個管理解決方案。

#### <a name="log-searches"></a>記錄檔搜尋
使用記錄搜尋透過 hello OMS 儲存機制中儲存的所有資料都。  使用者可能 hello OMS 主控台中執行自己的臨機操作分析，或有視覺效果的特定記錄檔搜尋建立儀表板。  解決方案可以根據預先定義的搜尋包含具有視覺效果的自訂檢視。  您可以使用 hello Log Search API tooaccess 資料從外部應用程式或管理工具的 hello OMS 儲存機制中。  

* [Log Analytics 中的記錄檔搜尋](../log-analytics/log-analytics-log-searches.md)
* [Log Analytics 記錄檔搜尋 REST API](../log-analytics/log-analytics-log-search-api.md)
* [Log Analytics Cmdlet](https://msdn.microsoft.com/library/mt188224.aspx)

#### <a name="custom-views"></a>自訂檢視
hello 檢視表設計工具可讓您 toocreate 自訂檢視 hello OMS 主控台中，為使用者提供的方案中的 hello 資料分析與視覺效果。  每個檢視包含 hello hello 主控台，您定義的記錄搜尋為基礎的視覺效果部份的數字的主要頁面顯示磚。

* [Log Analytics 檢視設計工具](../log-analytics/log-analytics-view-designer.md)

#### <a name="power-bi"></a>Power BI
記錄分析可以自動將資料匯出 hello OMS 儲存機制到 Power BI，您可以利用其視覺效果與分析工具。  在排程中，因此 hello 資料會維持 toodate 最新狀態，它會執行這個匯出中。 

* [匯出記錄分析資料 tooPower BI](../log-analytics/log-analytics-powerbi.md)

## <a name="automation"></a>自動化
OMS 可以自動化處理序 tooreact toocollected 資料或 tooperform 其他管理功能。  它可能從您的應用程式收集資料，並將其插入到 hello OMS 儲存機制，或您可以將自動化回應 toodata hello 儲存機制中找到的已知問題的 hello 更正。 

![自動化](media/operations-management-suite-integration/automate.png)

### <a name="runbooks"></a>Runbook
Azure 自動化中的 Runbook 會在 hello Azure 雲端中執行 PowerShell 指令碼和工作流程。  Toomanage 在 Azure 中任何其他資源，或是可以從 hello 雲端存取，您可以使用它們。  也可以使用混合式 Runbook 背景工作角色在本機資料中心執行 Runbook。  您可以從 hello Azure 入口網站或從外部處理序使用的一些方法，例如 PowerShell 啟動 runbook 或 hello 自動化應用程式開發介面。

* [在 Azure 自動化中啟動 Runbook](../automation/automation-starting-a-runbook.md)
* [Azure 自動化 Cmdlet](https://msdn.microsoft.com/library/dn690262.aspx)
* [自動化 REST API](https://msdn.microsoft.com/library/mt662285.aspx)
* [自動化 .NET](https://msdn.microsoft.com//library/mt465763.aspx)

### <a name="alerts"></a>Alerts
警示規則，自動執行根據 tooa 排程的記錄搜尋。  如果 hello 結果符合特定準則 hello 產生警示可以在 Azure 自動化中啟動 runbook，或者呼叫 webhook 就可以開始外部處理序。  這些回應都可以包含 hello 警示包括 hello 記錄搜尋中傳回的 hello 資料的詳細資料。

* [Log Analytics 中的警示](../log-analytics/log-analytics-alerts.md)
* [Log Analytics 警示 API](../log-analytics/log-analytics-api-alerts.md)

## <a name="backup-and-site-recovery"></a>備份與站台復原
Azure 備份和站台復原提供讓您保護您的企業資料，並確認伺服器和應用程式的 hello 可用性的服務。  您可以利用這些服務 tooperform 這種情況下，提供您的應用程式的備份服務為起始的虛擬機器容錯移轉。

* [Azure 備份 Cmdlet](https://msdn.microsoft.com/library/mt619253.aspx)
* [Azure Site Recovery REST API](https://msdn.microsoft.com/library/azure/mt750497.aspx)
* [Azure Site Recovery Cmdlet](https://msdn.microsoft.com/library/mt637930.aspx)

## <a name="custom-solutions"></a>自訂解決方案
在您的工作區中，或是在客戶的工作區中，您可以將整合邏輯封裝成自訂方案 toorun。  您的方案可以包含任何的 hello 整合方法中新增 tooother 資源 tooprovide 本文章中完整管理案例。  hello 方案中的 hello 資源被封裝，使所有其建立 hello 資源 hello 方案中移除時，都會從 hello OMS 工作區和 Azure 訂用帳戶移除。

例如，您的方案可能包括自動化 runbook toogather 及處理資料，然後填入 hello 記錄分析儲存機制使用 hello HTTP 資料收集器 API。  您也可以包含自訂的檢視顯示及分析 hello 收集資料。  

* 建立自訂解決方案 (即將推出)    

## <a name="next-steps"></a>後續步驟
* 參考 hello [OMS SDK](operations-management-suite-sdk.md)如需技術資訊，對自動化 OMS 服務。  

