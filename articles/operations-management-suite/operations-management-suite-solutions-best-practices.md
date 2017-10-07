---
title: "aaaOMSManagement 解決方案的最佳作法 |Microsoft 文件"
description: 
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 08cf1c101e301d24fb5c2bf4bc02a978e508a198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-management-solutions-in-operations-management-suite-oms-preview"></a>在 Operations Management Suite (OMS) 中建立管理解決方案的最佳作法 (預覽)
> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 如下所述的任何結構描述是主體 toochange。  

本文提供在 Operations Management Suite (OMS) 中[建立管理解決方案檔](operations-management-suite-solutions-solution-file.md)的最佳作法。  本資訊會在識別出其他最佳作法時更新。

## <a name="data-sources"></a>資料來源
- 資料來源可以[使用 Resource Manager 範本設定](../log-analytics/log-analytics-template-workspace-configuration.md)，但不應該將資源來源包含在解決方案檔中。  hello 原因是，設定資料來源目前不是具有等冪性，這表示您的方案無法覆寫 hello 使用者的工作區中現有的組態。<br><br>比方說，解決方案可能需要從 hello 應用程式事件記錄檔的警告和錯誤事件。  如果這樣做為資料來源中指定您的方案，您可能會如果 hello 使用者具有這設定其工作區中移除資訊事件。  如果您包含所有事件，然後您可能會收集 hello 使用者的工作區中的過多的資訊事件。

- 如果您的方案需要從其中一個 hello 標準的資料來源的資料，然後您應該定義此做為必要條件。  狀態文件中的 hello 客戶必須 hello 資料來源上設定自己。  
- 新增[資料流量的驗證](../log-analytics/log-analytics-view-designer-tiles.md)tooany 檢視在您的方案 tooinstruct hello 使用者在資料來源上設定必要的資料 toobe 該需要 toobe 訊息收集。  找不到必要的資料時，此訊息會顯示 hello 檢視的 hello 磚上。


## <a name="runbooks"></a>Runbook
- 新增[自動化排程](../automation/automation-schedules.md)每個 runbook 需要定期 toorun 您方案中。
- 包含 hello [IngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5)中您撰寫資料 toohello 記錄分析儲存機制的 runbook 所使用的方案 toobe。  設定 hello 方案太[參考](operations-management-suite-solutions-solution-file.md#solution-resource)讓它保持如果 hello 方案中移除此資源。  這可讓多個方案 tooshare hello 模組。
- 使用[自動化變數](../automation/automation-schedules.md)tooprovide 值的使用者可能會稍後想 toochange toohello 方案。  即使 hello 方案設定的 toocontain hello 變數，仍可以變更它的值。

## <a name="views"></a>Views
- 所有的解決方案應該包含顯示 hello 使用者入口網站中的單一檢視。  hello 檢視可以包含多個[視覺效果部分](../log-analytics/log-analytics-view-designer-parts.md)tooillustrate 不同的資料集。
- 新增[資料流量的驗證](../log-analytics/log-analytics-view-designer-tiles.md)tooany 檢視在您的方案 tooinstruct hello 使用者在資料來源上設定必要的資料 toobe 該需要 toobe 訊息收集。
- 設定 hello 方案太[包含](operations-management-suite-solutions-solution-file.md#solution-resource)hello 檢視，如此就會移除如果 hello 方案中移除。

## <a name="alerts"></a>Alerts
- 當做 hello 方案檔中的參數定義 hello 收件者清單，讓安裝 hello 方案時，hello 使用者可以定義它們。
- 設定 hello 方案太[參考](operations-management-suite-solutions-solution-file.md#solution-resource)警示規則，讓該使用者可以變更其組態。  它們可能會想 toomake 變更，例如修改 hello 收件者清單中，變更 hello hello 警示的閾值或停用 hello 警示規則。 


## <a name="next-steps"></a>後續步驟
* 逐步解說 hello 基本程序[設計和建立管理方案](operations-management-suite-solutions-creating.md)。
* 了解如何太[建立的方案檔](operations-management-suite-solutions-solution-file.md)。
* [新增已儲存的搜尋和警示](operations-management-suite-solutions-resources-searches-alerts.md)tooyour 管理解決方案。
* [加入檢視](operations-management-suite-solutions-resources-views.md)tooyour 管理解決方案。
* [將自動化 runbook 及其他資源新增](operations-management-suite-solutions-resources-automation.md)tooyour 管理解決方案。

