---
title: "在 OMS 中的管理解決方案 aaaBuild |Microsoft 文件"
description: "管理解決方案會擴充 hello 功能 Operations Management Suite (OMS) 藉由提供封裝的管理案例，客戶可以加入 tootheir OMS 工作區。  本文章提供有關如何建立管理方案 toobe 您自己的環境中使用，或進行可用 tooyour 客戶。"
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
ms.date: 03/20/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dea4c0d9e608d9fe4aa41088705958c9fe999372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-and-build-a-management-solution-in-operations-management-suite-oms-preview"></a>在 Operations Management Suite (OMS) 中設計和建置管理解決方案 (預覽)
> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 如下所述的任何結構描述是主體 toochange。

[管理解決方案](operations-management-suite-solutions.md)hello 功能 Operations Management Suite (OMS) 提供擴充的封裝的管理案例，客戶可以加入 tootheir OMS 工作區。  這篇文章會呈現基本程序 toodesign，並建置適用於最常見的需求的管理解決方案。  如果您是新 toobuilding 管理解決方案，您可以使用這個程序做為起點，並且運用 hello 概念對於更複雜的方案，當您的需求不同時。

## <a name="what-is-a-management-solution"></a>何謂管理解決方案？

管理解決方案包含 OMS 並搭配 tooachieve 特定監視案例使用的 Azure 資源。  它們被實作為[資源管理範本](../azure-resource-manager/resource-manager-template-walkthrough.md)包含詳細資料請參閱 tooinstall 和 hello 方案安裝時設定其所包含的資源。

hello 基本策略是 toostart 管理解決方案，藉由建置 hello Azure 環境中的個別元件。  一旦您擁有 hello 功能正常運作，然後您可以啟動封裝到[管理方案檔](operations-management-suite-solutions-solution-file.md)。 


## <a name="design-your-solution"></a>設計您的解決方案
hello 下列圖表顯示 hello 最常見的管理解決方案的模式。  在此模式中的 hello 不同元件下方的 hello 中討論。

![OMS 解決方案概觀](media/operations-management-suite-solutions/solution-overview.png)


### <a name="data-sources"></a>資料來源
hello 設計解決方案的第一個步驟決定您需要從 hello 記錄分析儲存機制的 hello 資料。  這項資料可能會收集由[資料來源](../log-analytics/log-analytics-data-sources.md)或[另一個解決方案](operations-management-suite-solutions.md)，或您的方案可能需要 tooprovide hello 程序 toocollect 它。

有數種方式可以收集在 hello 記錄分析儲存機制中所述的資料來源[記錄分析中的資料來源](../log-analytics/log-analytics-data-sources.md)。  這包括 hello Windows 事件記錄檔中的事件或由產生 Syslog 此外 tooperformance 計數器 Windows 和 Linux 用戶端。  您也可以從 Azure 監視器所收集的 Azure 資源來收集資料。  

如果您需要不是透過任何 hello 可用資料來源，可存取的資料，則您可以使用 hello [HTTP 資料收集器 API](../log-analytics/log-analytics-data-collector-api.md)可讓您 toowrite 資料 toohello 記錄分析儲存機制從可以呼叫其他任何用戶端應用程式開發介面。  hello 最常見的管理解決方案中的自訂資料收集的方法是 toocreate [Azure 自動化中的 runbook](../automation/automation-runbook-types.md) ，收集所需的 hello 資料從 Azure 或外部的資源，並使用 hello 資料收集器 API toowritetoohello 儲存機制。  

### <a name="log-searches"></a>記錄檔搜尋
[記錄搜尋](../log-analytics/log-analytics-log-searches.md)會使用的 tooextract 和分析 hello 記錄分析儲存機制中的資料。  它們可供檢視與中新增 tooallowing hello 使用者 tooperform 臨機操作資料分析 hello 儲存機制中的警示。  

您應該定義您認為會很有幫助 toohello 使用者，即使它們未使用的任何檢視或警示的任何查詢。  這些將可用的 toothem 為已儲存的搜尋在 hello 入口網站，而且您也可以包含在[清單查詢的視覺效果部分](../log-analytics/log-analytics-view-designer-parts.md#list-of-queries-part)在您的自訂檢視。

### <a name="alerts"></a>Alerts
[記錄分析中的警示](../log-analytics/log-analytics-alerts.md)找出問題透過[記錄搜尋](#log-searches)針對 hello hello 儲存機制中的資料。  它們通知 hello 使用者或自動執行動作以回應。 您應該識別應用程式的不同警示條件，並在解決方案檔中包含對應的警示規則。

如果 hello 問題可能與自動化的程序予以更正，然後將通常會建立 runbook 在 Azure 自動化 tooperform 此修復。  大部分的 Azure 服務可以使用管理[cmdlet](/powershell/azure/overview)哪些 hello runbook 會運用 tooperform 這類功能。

如果您的解決方案需要在回應 tooan 警示中，外部功能，則您可以使用[webhook 回應](../log-analytics/log-analytics-alerts-actions.md)。  這可讓您 toocall 將資訊傳送 hello 警示中的外部 web 服務。

### <a name="views"></a>Views
記錄分析中的檢視是使用的 toovisualize hello 記錄分析儲存機制中的資料。  每個解決方案通常會包含具有單一檢視[磚](../log-analytics/log-analytics-view-designer-tiles.md)hello 使用者的主要儀表板上顯示。  hello 檢視表可以包含任意數目的[視覺效果部分](../log-analytics/log-analytics-view-designer-parts.md)tooprovide hello 收集的資料 toohello 使用者的不同視覺效果。

您[建立使用 hello 檢視表設計工具的自訂檢視](../log-analytics/log-analytics-view-designer.md)其中您可以稍後匯出包含在您的方案檔。  


## <a name="create-solution-file"></a>建立解決方案檔
一旦您設定並測試 hello 元件將成為方案的一部分，您可以[建立您的方案檔](operations-management-suite-solutions-solution-file.md)。  您將實作中的 hello 解決方案元件[Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)包含[方案資源](operations-management-suite-solutions-solution-file.md#solution-resource)與關聯性 toohello 中的其他資源 hello 檔案。  


## <a name="test-your-solution"></a>測試解決方案
雖然您開發您的方案，您將需要 tooinstall，並在您的工作區中進行測試。  您可以使用任何可用的 hello 方法太[測試，並安裝資源管理員範本](../azure-resource-manager/resource-group-template-deploy.md)。

## <a name="publish-your-solution"></a>發佈您的解決方案
一旦您完成並測試您的方案，您還可以讓透過下列來源任一 hello 可用 toocustomers。

- **Azure 快速入門範本**。  [Azure 快速入門範本](https://azure.microsoft.com/resources/templates/)是一組透過 GitHub hello 社群所提供的資源管理員範本。  您可以對您的方案提供下列資訊在 hello[參與指南](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE)。
- **Azure Marketplace**。  hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) toodistribute 可讓您，並將您的方案 tooother Isv，開發人員和 IT 專業人員。  您可以了解如何 toopublish 您方案 tooAzure Marketplace 在[如何 toopublish 及管理在 hello Azure Marketplace 提供項目](../marketplace-publishing/marketplace-publishing-getting-started.md)。



## <a name="next-steps"></a>後續步驟
* 了解如何太[建立的方案檔](operations-management-suite-solutions-solution-file.md)管理解決方案。
* 瞭解 hello[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。
* 搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。