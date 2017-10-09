---
title: "在 Microsoft monitoring 產品 aaaAlert 管理 |Microsoft 文件"
description: "警示表示有一些需要系統管理員注意的問題。  這篇文章描述如何建立及管理 System Center Operations Manager (SCOM) 和記錄分析中警示的 hello 差異，並提供運用 hello 這兩項產品的混合式警示管理策略中的最佳作法。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>使用 Microsoft 監視管理警示
警示表示有一些需要系統管理員注意的問題。  在如何建立警示、如何管理和分析警示以及在偵測到嚴重問題時如何通知您的方面，System Center Operations Manager (SCOM) 與 Operations Management Suite (OMS) 中的 Log Analytics 之間有一些顯著的差異。

## <a name="alerts-in-operations-manager"></a>Operations Manager 中的警示
SCOM 中的警示會產生個別的規則或監視 tooindicate 特定問題。  監視可能會產生警示時即會進入錯誤狀態，而規則可能會產生警示的 tooindicate 有些嚴重的問題不是直接相關的 toohello 受管理物件的健全狀況。  管理組件包含各種不同的工作流程建立 hello 應用程式的警示或所管理的服務。  設定新的管理組件的 hello 程序的一部分微調 tooensure 沒有過多警示，您不認為重要的問題。

![SCOM 警示檢視](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM 警示具有的狀態，可以由系統管理員變更，因為它們的運作 tooresolve hello 問題提供完整的警示管理。  Hello 問題已經解決，當 hello 管理員會設定 hello 警示 tooclosed 此時它不會再出現在檢視中顯示作用中警示。  Hello 監視器傳回 tooa 狀況良好狀態時，就可以自動解決警示所產生的監視。

![警示狀態](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Log Analytics 中的警示
定期自動執行的記錄檔查詢會建立 Log Analytics 中的警示。  您可以從任何記錄檔查詢來建立警示規則。  如果 hello 查詢會傳回符合指定的 hello 準則的結果，則會建立警示。  這可能是偵測到特定事件時，會建立警示的特定查詢，或者您可以使用更一般的查詢會搜尋任何錯誤事件相關 tooa 特定應用程式。

記錄檔分析警示會寫入為事件 toohello OMS 儲存機制，而且可以用記錄查詢擷取。  它們不需要像 SCOM 事件的狀態，讓您可以指出 hello 問題已經解決時。

![OMS 警示](media/operations-management-suite-monitoring-alerts/oms-alert.png)

SCOM 做為資料來源使用的記錄分析時，SCOM 警示會在建立並修改寫入 toohello OMS 儲存機制。  

![SCOM 警示](media/operations-management-suite-monitoring-alerts/scom-alert.png)

hello[警示管理解決方案](http://technet.microsoft.com/library/mt484092.aspx)tooretrieve 組不同的警示提供作用中警示和數個常用查詢的摘要。  這可讓您更有效地分析的警示數目多於 SCOM 中報告的警示數目。  您可以向下鑽研從 hello 摘要 toodetailed 資料，並建立臨機操作查詢 tooretrieve 組不同的警示。

![警示管理解決方案](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>通知
SCOM 中的通知傳送給您的郵件或文字回應 tooalerts 符合特定準則。  您可以建立不同的通知訂閱 hello hello 警示、 hello 偵測到的問題種類或 hello 的嚴重性，有不同的人為 hello 物件正在監視這類準則而收到通知的一天的時間。

幾個訂用帳戶可以是使用的 tooimplement 大量的管理組件的完成通知策略。

![SCOM 警示](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

如果已透過在每個 [警示規則](http://technet.microsoft.com/library/mt614775.aspx)上設定電子郵件通知動作來建立警示，則 Log Analytics 可以透過郵件通知您。  它並沒有訂閱使用單一規則 toomultiple 警示 SCOM hello hello 能力。  您也需要 toocreate 您自己的警示規則因為 OMS 不提供任何預先設定。

![Log Analytics 警示](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

您無法完全管理 SCOM 警示中記錄分析透過因為您只可以修改這些 hello Operations 主控台中。  Log Analytics 可做為警示管理程序的一部分，以提供 SCOM 單獨沒有的分析工具。

## <a name="alert-remediation"></a>警示補救
[補救](http://technet.microsoft.com/library/mt614775.aspx)參考警示所識別的 tooan 嘗試 tooautomatically 正確 hello 問題。

SCOM 可讓您 toorun 診斷和復原中回應 tooa 監視進入狀況不良的狀態。  發生這種情況同時 toohello 監視器建立 hello 警示。  診斷和復原通常會實作成 hello 代理程式執行的指令碼中。  診斷嘗試 toogather hello 的詳細資訊時偵測到問題修復嘗試 toocorrect hello 問題。

記錄分析可讓您 toostart [Azure 自動化 runbook](https://azure.microsoft.com/documentation/services/automation/)或呼叫回應 tooa 記錄分析警示中的 webhook。  Runbook 可以包含 PowerShell 中所實作的複雜邏輯。  hello 指令碼在 Azure 中執行，並可從 hello 雲端存取任何 Azure 資源或可用的外部資源。  Azure 自動化沒有 hello 能力 tooexecute runbook 在您的本機資料中心的伺服器上，但這項功能目前不提供啟動回應 tooLog 分析警示中的 hello runbook 時。

SCOM 中的復原和 OMS 中的 runbook 都可包含 PowerShell 指令碼，但是復原會更難 toocreate 及管理，因為它們必須包含在管理組件。  Runbook 會儲存在 Azure 自動化中，而 Azure 自動化提供功能來撰寫、測試和管理 Runbook。

如果您使用做為資料來源的 SCOM 供記錄分析，您可以建立使用記錄檔查詢 tooretrieve SCOM 警示儲存在 hello OMS 儲存機制的記錄分析警示。  這樣可讓您的 Azure 自動化 runbook toorun 回應 tooa SCOM 警示中。  當然，因為 hello runbook 將會在 Azure 中執行，這就無法復原的內部部署問題的可行策略。

## <a name="next-steps"></a>後續步驟
* 瞭解 hello[在 System Center Operations Manager (SCOM) 警示](https://technet.microsoft.com/library/hh212913.aspx)。

