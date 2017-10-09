---
title: "aaaUser 起始 Azure 自動化 Runbook 中的動作記錄分析 |Microsoft 文件"
description: "本文說明如何 toorun 自動化 runbook 的記錄分析搜尋結果視。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 53c25431572babd5fd54bf964e4683077e2a4c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="take-action-with-an-automation-runbook-from-a-log-analytics-log-search-result"></a>從 Log Analytics 記錄搜尋結果利用自動化 Runbook 採取動作

從 Azure Log Analytics 中的記錄搜尋結果，您現在可以選取**採取的動作**toorun 自動化 runbook。  hello runbook 可用 tooremediate hello 問題或執行某些其他動作，例如收集疑難排解資訊、 傳送電子郵件，或建立服務要求。 

## <a name="components-and-features-used"></a>使用的元件和功能
* [Azure 自動化帳戶](../automation/automation-offering-get-started.md)
* [Log Analytics 工作區](../log-analytics/log-analytics-overview.md)

## <a name="tooinitiate-runbook-from-log-search"></a>從記錄檔搜尋 tooinitiate runbook

您開始建立記錄檔搜尋 tootake 事件和啟動 runbook，以從您的記錄搜尋結果的動作，，並從 hello 結果叫用 runbook 隨。  這可以從 hello Azure 中的 hello 記錄搜尋功能來達成或[OMS 入口網站](../log-analytics/log-analytics-log-searches.md)。  在此範例中，我們會從 hello 與基本示範這項功能的 Azure 入口網站執行記錄搜尋。

1. 在 hello Azure 入口網站，hello 中樞功能表上按一下 **更多服務**選取**記錄分析**。  
2. 在 hello 記錄分析刀鋒視窗中，選取您的記錄分析工作區，hello 工作區刀鋒視窗上選取**記錄搜尋**。  
3. Hello 記錄搜尋 刀鋒視窗中，執行記錄搜尋。  
4. 從 hello 記錄搜尋結果中，按一下 hello 橢圓形 toohello 左邊的 hello 欄位，並從 hello 快顯視窗，選取一個**採取的動作**。<br><br> ![從搜尋結果中選取採取動作](./media/log-analytics-log-search-takeaction/log-search-takeaction-menuoption.png) 
5. 從 hello 採取動作刀鋒視窗中，選取**執行 runbook**，在 hello**執行 runbook**刀鋒視窗，您可以選取 runbook toorun。  您可以選取任何 runbook 中 hello 是連結的 toohello 記錄分析工作區的自動化帳戶。  請注意 hello 下列：

    * Runbook 是依標籤來組織。
    * Runbook 輸入的參數值可以直接從 hello 搜尋結果的 hello 欄位中選取。  顯示所有 hello 可用的欄位從 hello 結果 tooselect 即會出現下拉式清單。  
    * 您也可以選擇 toorun hello runbook 上[混合式 runbook 背景工作](../automation/automation-hybrid-runbook-worker.md)您已安裝在具有 hello 問題，如果您有對應的混合式 Runbook 背景工作群組只包含該機器為成員的 hello 電腦上。  如果 hello hello Hybrid Worker 群組名稱符合 hello hello 記錄搜尋結果中的 hello 電腦名稱，然後會自動選取 hello 群組。    

6. 按一下 之後**執行**，hello runbook 作業刀鋒視窗會開啟 tooallow 您 tooreview hello hello 工作狀態。   

如果您選取的 runbook 時設定的 toobe[記錄分析警示從呼叫](../automation/automation-invoke-runbook-from-omsla-alert.md)，它有輸入的參數呼叫**WebhookData**也就是**物件**型別。  如果 hello 輸入的參數是必要的因此它可以將 hello JSON 格式化字串轉換成物件類型可讓您將 runbook 活動中參照的特定項目上的 toofilter 需要 toopass hello 搜尋結果 toohello runbook。  您可以選取**搜尋結果 （物件）** hello 下拉式清單中。<br><br> ![選取 Webhook 資料物件給 Runbook 參數](media/log-analytics-log-search-takeaction/select-runbook-and-properties.png)   
    
## <a name="next-steps"></a>後續步驟

* 檢閱 hello[記錄分析記錄搜尋參考](log-analytics-search-reference.md)tooview hello 的所有搜尋欄位和 facet 用於記錄分析。
* toolearn tooinvoke 自動化 runbook 自動檢閱[呼叫 Azure 自動化 runbook 從 OMS 記錄分析警示](../automation/automation-invoke-runbook-from-omsla-alert.md)。  
