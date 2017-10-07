---
title: "Azure 自動化 Runbook 的記錄分析警示 aaaCalling |Microsoft 文件"
description: "本文提供的概觀 tooinvoke 自動化 runbook 從 Microsoft OMS 記錄分析警示。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/31/2017
ms.author: magoedte
ms.openlocfilehash: 8b745d6e6c2b0294d676e010f52855cd51741cf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="calling-an-azure-automation-runbook-from-an-oms-log-analytics-alert"></a>從 OMS Log Analytics Alert 呼叫 Azure 自動化 Runbook | Microsoft Docs

如果結果符合特定準則，例如長時間的突然增加處理器使用率 」 或 「 企業營運應用程式的特定應用程式處理序重大 toohello 功能中的警示記錄中記錄分析 toocreate 設定警示時失敗該警示可以自動執行自動化 runbook 在嘗試 tooauto hello Windows 事件記錄檔中寫入對應的事件和-補救 hello 問題。  

有兩個選項 toocall runbook 設定 hello 警示時。  具體而言，

1. 使用 Webhook。
   * 如果您的 OMS 工作區不是連結的 tooan 自動化帳戶，這是 hello 唯一可用的選項。
   * 如果您沒有自動化帳戶連結 tooan OMS 工作區，此選項，還是可以。  

2. 直接選取 Runbook。
   * Hello OMS 工作區是連結的 tooan 自動化帳戶時，才使用此選項。  

## <a name="calling-a-runbook-using-a-webhook"></a>使用 Webhook 來呼叫 Runbook

Webhook 可讓您 toostart 特定 runbook 在 Azure 自動化中透過單一 HTTP 要求。  然後再設定 hello[記錄分析警示](../log-analytics/log-analytics-alerts.md#alert-rules)toocall hello runbook 使用 webhook 為警示的動作，您將需要 toofirst 建立 webhook hello runbook 將會使用這個方法呼叫。  檢閱並遵循 hello 中的 hello 步驟[建立 webhook](automation-webhooks.md#creating-a-webhook)發行項，並記得 toorecord hello webhook URL，這樣您就可以設定 hello 警示規則時參考它。   

## <a name="calling-a-runbook-directly"></a>直接呼叫 Runbook

如果您擁有 hello 自動化及控制供應項目中安裝並設定您的 OMS 工作區，設定 hello hello 警示的 Runbook 動作選項時，您可以檢視所有 runbook 從 hello**選取 runbook**下拉式清單然後選取您想 toorun 回應 toohello 警示中的 hello 特定 runbook。  選取的 hello runbook 可以在 hello Azure 雲端或混合式 runbook 背景工作的工作區中執行。  使用 hello runbook 選項建立 hello 警示時，會建立 webhook hello runbook。  如果您移 toohello 自動化帳戶，並瀏覽 toohello webhook 刀鋒視窗中的 hello 選取 runbook，您可以看到 hello webhook。  如果您刪除 hello 警示時，不刪除 hello webhook，但 hello 使用者可以手動刪除 hello webhook。  它並不是問題，如果沒有刪除 hello webhook，它是只被遺棄項目，最後需要 toobe 刪除順序 toomaintain 組織的自動化帳戶。  

## <a name="characteristics-of-a-runbook-for-both-options"></a>Runbook 的特性 (適用於兩個選項)

這兩種方法來呼叫 hello runbook 從 hello 記錄分析警示有不同的行為特性，需要 toobe 瞭解之後再設定您的警示規則。  

* 您必須擁有名為 **WebhookData** (也就是**物件**類型) 的 Runbook 輸入參數。  它可以是強制性或選擇性。  hello 警示傳遞 hello 搜尋結果 toohello runbook 使用此輸入的參數。

        param  
         (  
          [Parameter (Mandatory=$true)]  
          [object] $WebhookData  
         )

*  您必須擁有程式碼 tooconvert hello WebhookData tooa PowerShell 物件。

    `$SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value`

    *$SearchResults*將物件的陣列，每個物件都包含一個搜尋結果中的值的 hello 欄位

### <a name="webhookdata-inconsistencies-between-hello-webhook-option-and-runbook-option"></a>WebhookData hello webhook 選項 runbook 選項之間的不一致

* 設定警示的 toocall Webhook 時, 輸入 webhook URL，您建立 runbook，然後按一下 hello**測試 Webhook**  按鈕。  hello 產生 WebhookData 傳送 toohello runbook 未包含*。SearchResult*或*。SearchResults*。

*  如果您將儲存該警示，當 hello 警示觸發程序，並呼叫 hello webhook，hello WebhookData 傳送 toohello runbook 包含*。SearchResult*。
* 如果您建立警示，並將它設定 toocall runbook （這也會建立 webhook），當 hello 警示傳送 WebhookData toohello runbook 所含的觸發程序*。SearchResults*。

因此在 hello 上述程式碼範例，您將需要 tooget *。SearchResult*如果 hello 警示呼叫 webhook，並將需要 tooget *。SearchResults*如果 hello 警示直接呼叫 runbook。

## <a name="example-walkthrough"></a>範例逐步解說

我們將示範如何將使用下列範例圖形化 runbook，以便啟動 Windows 服務的 hello。<br><br> ![啟動 Windows 服務圖形化 Runbook](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice.png)<br>

hello runbook 都有一個輸入的參數型別的**物件**，而呼叫**WebhookData**並包含從 hello 警示包含傳入的 hello webhook 資料*。SearchResults*。<br><br> ![Runbook 輸入參數](media/automation-invoke-runbook-from-omsla-alert/automation-runbook-restartservice-inputparameter.png)<br>

例如，在記錄分析，我們建立兩個自訂欄位， *SvcDisplayName_CF*和*SvcState_CF*，tooextract hello 服務顯示名稱和 hello hello 服務狀態 （也就是執行中或已停止）從 hello 事件寫入 toohello 系統事件記錄檔。  我們以 hello 下列搜尋查詢再建立警示規則： `Type=Event SvcDisplayName_CF="Print Spooler" SvcState_CF="stopped"` ，以便我們可以偵測 hello 列印多工緩衝處理器服務停止 hello Windows 系統上。  它可以是任何感興趣服務的但此範例中我們會參考 hello 既存的服務 hello Windows 作業系統隨附的其中一個。  hello 警示動作是設定的 tooexecute 我們在此範例中所用的 runbook，並執行位於 hello Hybrid Runbook Worker，hello 目標系統上已啟用哪。   

hello runbook 的程式碼活動**取得服務名稱從 LA**會將 hello JSON 格式化字串轉換成的物件類型和 hello 項目上的篩選器*SvcDisplayName_CF* hello tooextract hello 顯示名稱Windows 服務，並將此變數傳遞到 hello 下一個活動的 hello 服務已停止然後再嘗試 toorestart 會確認它。  *SvcDisplayName_CF*是[自訂欄位](../log-analytics/log-analytics-custom-fields.md)記錄分析 toodemonstrate 中建立此範例。

    $SearchResults = (ConvertFrom-Json $WebhookData.RequestBody).SearchResults.value
    $SearchResults.SvcDisplayName_CF  

當 hello 服務停止時，記錄分析中的 hello 警示規則會偵測到相符項目觸發 hello runbook 和傳送嗨警示內容 toohello runbook。 hello runbook 將會採取的動作 tooverify hello 服務已停止，和如果因此嘗試 toorestart hello 服務，並確認已正確地啟動，並輸出 hello 結果。     

或者如果您沒有自動化帳戶連結 tooyour OMS 工作區，您會設定 hello 警示規則 webhook 動作 tootrigger hello runbook 並設定 hello runbook tooconvert hello JSON 格式的字串和篩選*.SearchResult*遵循先前所述的 hello 指引。    

## <a name="next-steps"></a>後續步驟

* toolearn 深入了解記錄分析中的警示和如何 toocreate 其中一個，請參閱[記錄分析中的警示](../log-analytics/log-analytics-alerts.md)。

* 如何 tootrigger runbook 使用 webhook，請參閱的 toounderstand [Azure 自動化 webhook](automation-webhooks.md)。
