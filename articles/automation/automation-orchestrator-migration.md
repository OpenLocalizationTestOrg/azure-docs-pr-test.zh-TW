---
title: "從 Orchestrator tooAzure 自動化 aaaMigrating |Microsoft 文件"
description: "描述如何 toomigrate runbook 和整合組件從 System Center Orchestrator tooAzure 自動化。"
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>從 Orchestrator tooAzure 自動化 (Beta) 移轉
[System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) 中的 Runbook 是根據來自專為 Orchestrator 編寫的整合套件的活動，而 Azure 自動化中的 Runbook 則是根據 Windows PowerShell。  [圖形化 runbook](automation-runbook-types.md#graphical-runbooks) Azure 自動化中有類似的外觀 tooOrchestrator runbook 活動代表 PowerShell cmdlet、 子系 runbook 和資產。

hello [System Center Orchestrator 移轉工具組](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all)包含工具 tooassist 您轉換從 Orchestrator tooAzure 自動化的 runbook。  此外 tooconverting hello runbook 本身，您必須轉換 hello runbook，Windows PowerShell 指令程式搭配使用 toointegration 模組 hello 活動與 hello 整合套件。  

以下是 hello 轉換 Orchestrator runbook tooAzure 自動化的基本程序。  Hello 的以下各節中詳細說明每個步驟。

1. 下載 hello [System Center Orchestrator 移轉工具組](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all)包含 hello 工具和本文所討論的模組。
2. 匯入 [標準活動模組](#standard-activities-module) 到 Azure 自動化。  這包括已轉換的 Runbook 可能使用的標準 Orchestrator 活動的轉換版本。
3. 針對存取 System Center 的 Runbook 所使用的整合套件，將 [System Center Orchestrator 整合模組](#system-center-orchestrator-integration-modules) 匯入至 Azure 自動化。
4. 轉換的自訂和協力廠商的整合套件使用 hello[整合套件轉換器](#integration-pack-converter)和匯入至 Azure 自動化。
5. 轉換使用 hello 的 Orchestrator runbook [Runbook 轉換器](#runbook-converter)並安裝在 Azure 自動化中。
6. 手動因為 hello Runbook 轉換器不會轉換這些資源，請在 Azure 自動化中建立必要的 Orchestrator 資產。
7. 設定[Hybrid Runbook Worker](#hybrid-runbook-worker)本機資料中心轉換 toorun runbook 將會存取本機資源中。

## <a name="service-management-automation"></a>服務管理自動化
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) 會儲存在 Orchestrator，例如本機資料中心執行 runbook 和它會使用 hello Azure 自動化為相同的整合模組。 hello [Runbook 轉換器](#runbook-converter)轉換 Orchestrator runbook toographical runbook 雖然 SMA 中不支援它。  您仍然可以安裝 hello[標準活動模組](#standard-activities-module)和[System Center Orchestrator 整合模組](#system-center-orchestrator-integration-modules)入 SMA，但您必須手動[重寫您的 runbook](http://technet.microsoft.com/library/dn469262.aspx)。

## <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker
Orchestrator 中的 Runbook 會儲存在資料庫伺服器上，並在 Runbook 伺服器上執行，都是在本機資料中心中。  Azure 自動化中的 Runbook 會儲存在 hello Azure 雲端，而且可以執行在本機資料中心使用[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)。  這是如何您通常會執行 runbook，因為它們是在本機伺服器上的設計的 toorun 轉換從 Orchestrator。

## <a name="integration-pack-converter"></a>整合套件轉換器
hello 整合套件轉換器會將轉換使用 hello 所建立的整合套件[Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration 模組根據可以匯入至 Azure 自動化的 Windows PowerShell 或Service Management Automation。  

當您執行 hello 整合組件轉換程式時，您會有一個精靈，可讓您 tooselect 整合組件 (.oip) 檔案。  hello 精靈則列出 hello 該整合套件中包含的活動，並可讓您將移轉之 tooselect。  當您完成 hello 精靈時，它會建立包含對應的 cmdlet 針對每個 hello 原始的整合套件中的 hello 活動的整合模組。

### <a name="parameters"></a>參數
Hello 整合套件中之活動的任何屬性都是 cmdlet 的轉換的 tooparameters 的 hello hello 整合模組內對應。  Windows PowerShell Cmdlet 有一組 [一般參數](http://technet.microsoft.com/library/hh847884.aspx) ，可以搭配所有 Cmdlet 使用。  例如，hello-Verbose 參數會造成 cmdlet toooutput 詳細其作業的相關資訊。  任何 cmdlet 可能會不有一個參數，以做為一般的參數名稱相同的 hello。  如果活動沒有屬性，以做為一般的參數名稱相同的 hello，hello 精靈會提示您 tooprovide hello 參數名稱。

### <a name="monitor-activities"></a>監視器活動
監視 Orchestrator 開頭中的 runbook[監視活動](http://technet.microsoft.com/library/hh403827.aspx)和連續執行等候 toobe 叫用特定的事件。  Azure 自動化不支援監視 runbook，因此將不會轉換 hello 整合套件中的任何監視活動。  相反地，預留位置 cmdlet 會建立在 hello 監視活動的 hello 整合模組。  這個 cmdlet 具有任何功能，但它可讓其使用的任何轉換的 runbook toobe 安裝。  此 runbook 將不會在 Azure 自動化中，可以 toorun，但也可以安裝，讓您可以修改它。

### <a name="integration-packs-that-cannot-be-converted"></a>無法轉換的整合套件
未建立與 OIT 的整合套件無法轉換以 hello 整合套件轉換器。 另外還有一些 Microsoft 提供的整合套件目前無法使用此工具轉換。  這些整合套件的已轉換版本已 [提供下載](#system-center-orchestrator-integration-modules) ，使得可以將它們安裝在 Azure 自動化或 Service Management Automation 中。

## <a name="standard-activities-module"></a>標準活動模組
Orchestrator 包含未包含在整合套件中、但會使用許多 Runbook 的一組 [標準活動](http://technet.microsoft.com/library/hh403832.aspx) 。  hello 標準活動模組是整合模組，其中包含這些活動的每個對等的 cmdlet。  您必須在匯入使用標準活動的任何轉換的 Runbook 之前，於 Azure 自動化中安裝此整合模組。

此外 toosupporting 轉換 runbook、 hello 標準活動模組中的 hello cmdlet 可供其他人熟悉 Orchestrator toobuild 新的 runbook 在 Azure 自動化中。  雖然所有 hello 標準活動的 hello 功能可以執行 cmdlet，它們可能會以不同的方式操作。  hello hello 轉換的標準活動運作模組中 cmdlet hello 相同為其對應的活動和使用 hello 相同的參數。  這可協助 hello 現有 Orchestrator runbook 作者在其轉換 tooAzure 自動化 runbook。

## <a name="system-center-orchestrator-integration-modules"></a>System Center Orchestrator 整合模組
Microsoft 提供[整合套件](http://technet.microsoft.com/library/hh295851.aspx)建置 runbook tooautomate System Center 元件和其他產品。  部分這些整合套件目前根據 OIT，但目前不能轉換的 toointegration 模組由於已知問題。  [System Center Orchestrator 整合模組](https://www.microsoft.com/download/details.aspx?id=49555) 包含這些整合套件的已轉換版本，可以匯入 Azure 自動化和 Service Management Automation 中。  

根據這項工具的 hello RTM 版本，更新 hello OIT 以 hello 將發行的整合套件轉換器可以轉換為基礎的整合套件的版本。  指引也會提供的 tooassist 轉換不使用活動與 hello 整合套件的 runbook，您可以根據 OIT。

## <a name="runbook-converter"></a>Runbook Converter
hello Runbook 轉換器轉換的 Orchestrator runbook[圖形化 runbook](automation-runbook-types.md#graphical-runbooks) ，可以匯入 Azure 自動化。  

Runbook 轉換器實作為 PowerShell 模組 cmdlet 呼叫**ConvertFrom SCORunbook**執行 hello 轉換。  當您安裝 hello 工具時，它會建立 hello 指令程式會載入的快顯 tooa PowerShell 工作階段。   

以下是 hello 基本程序 tooconvert Orchestrator runbook，並匯入 Azure 自動化。  hello 下列各節提供更多詳細資料使用 hello 工具並使用轉換的 runbook。

1. 從 Orchestrator 匯出一或多個 Runbook。
2. 取得 hello runbook 中的所有活動的整合模組。
3. 將轉換 hello Orchestrator runbook 在 hello 匯出的檔案。
4. 檢閱記錄檔 toovalidate hello 轉換和 toodetermine 中的資訊的任何必要的手動工作。
5. 將轉換的 Runbook 匯入至 Azure 自動化。
6. 在 Azure 自動化中建立任何必要的資產。
7. 編輯 Azure 自動化 toomodify 中的 hello runbook 所需的活動。

### <a name="using-runbook-converter"></a>使用 Runbook Converter
hello 語法**ConvertFrom SCORunbook**如下所示：

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath-路徑 toohello 匯出檔案包含 hello runbook tooconvert。
* 模組-以逗號分隔整合模組包含 hello runbook 中的活動的清單。
* OutputFolder-路徑 toohello 資料夾 toocreate 轉換圖形化 runbook。

下列範例命令會將轉換 hello 名的匯出檔案中的 runbook hello **MyRunbooks.ois_export**。  這些 runbook 使用 hello Active Directory 與 Data Protection Manager 的整合套件。

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>記錄檔
hello Runbook 轉換器會建立下列記錄檔中 hello hello hello 與相同的位置轉換 runbook。  如果 hello 檔案已經存在，它們將會複寫的 hello 上次的轉換資訊。

| 檔案 | 內容 |
|:--- |:--- |
| Runbook Converter - Progress.log |Hello 轉換包括成功轉換的每個活動的資訊和警告不會轉換每個活動的詳細的步驟。 |
| Runbook Converter - Summary.log |最後一個轉換，包括任何警告和待處理工作，您需要建立 hello 轉換 runbook 所需的變數，例如 tooperform hello 摘要。 |

### <a name="exporting-runbooks-from-orchestrator"></a>從 Orchestrator 匯出 Runbook
hello Runbook 轉換器可搭配從 Orchestrator 含有一或多個 runbook 的匯出檔案。  它會建立對應的 Azure 自動化 runbook 的每個 Orchestrator runbook hello 匯出檔案中。  

tooexport 從 Orchestrator，runbook 在 Runbook Designer 中的 hello runbook hello 名稱上按一下滑鼠右鍵，然後選取**匯出**。  tooexport 所有 runbook 在資料夾中，以滑鼠右鍵都按一下 hello 名稱 hello 資料夾，然後選取**匯出**。

### <a name="runbook-activities"></a>Runbook 活動
hello Runbook 轉換器，將轉換 hello Azure 自動化中的 Orchestrator runbook tooa 對應活動中的每個活動。  無法轉換這些活動，預留位置活動被建立在 hello runbook 警告文字中。  您匯入至 Azure 自動化的 hello 轉換 runbook 之後，您必須將這些活動的任何取代有效執行所需的 hello 功能的活動。

在 hello 任何 Orchestrator 活動[標準活動模組](#standard-activities-module)會轉換。  不過，在此模組有一些標準 Orchestrator 活動，並不會被轉換。  例如，**傳送平台事件**因為 hello 事件是特定 tooOrchestrator 具有任何 Azure 自動化對等項目。

[監視活動](https://technet.microsoft.com/library/hh403827.aspx)不會因為在 Azure 自動化中沒有對等的 toothem 轉換。  hello 例外狀況是監視器中的活動[轉換整合套件](#integration-pack-converter)要轉換的 toohello 預留位置活動。

從任何活動[轉換整合套件](#integration-pack-converter)會被轉換，如果您提供 hello 路徑 toohello 整合模組以 hello**模組**參數。  System Center 整合套件，您可以使用 hello [System Center Orchestrator 整合模組](#system-center-orchestrator-integration-modules)。

### <a name="orchestrator-resources"></a>Orchestrator 資源
hello Runbook 轉換器只能轉換 runbook、 不其他 Orchestrator 資源，例如計數器、 變數或連接。  Azure 自動化中不支援計數器。  支援變數和連線，但是您必須手動建立它們。  hello 記錄檔將會通知您若 hello runbook 需要這類資源，並指定對應的資源，您需要在 Azure 自動化中的 toocreate hello 正確轉換 runbook toooperate。

比方說，runbook 可能會在活動中使用變數 toopopulate 特定值。  hello 轉換後的 runbook 將轉換 hello 活動，並指定為 hello Orchestrator 變數名稱相同的 hello 在 Azure 自動化變數資產。  這會記錄在 hello **Runbook 轉換程式 Summary.log**建立 hello 轉換後的檔案。  您將需要 toomanually 之前使用 hello runbook 在 Azure 自動化中建立此變數的資產。

### <a name="input-parameters"></a>輸入參數
中 Orchestrator 的 Runbook 會接受輸入的參數以 hello**初始化資料**活動。  如果正在轉換的 hello runbook 中包含這個活動中，則[輸入的參數](automation-graphical-authoring-intro.md#runbook-input-and-output)在 hello Azure 自動化 runbook 建立的每個參數 hello 活動。  A[工作流程指令碼控制項](automation-graphical-authoring-intro.md#activities)hello 轉換 runbook 擷取並傳回每個參數中建立活動。  Hello runbook 中使用的輸入的參數的任何活動參考此活動 toohello 輸出。

hello，不會使用這項策略的原因是 hello Orchestrator runbook 中的 toobest 鏡像 hello 功能。  新的圖形化 runbook 中的活動應該直接參考 tooinput 參數使用 Runbook 的輸入的資料來源。

### <a name="invoke-runbook-activity"></a>叫用 Runbook 活動
中 Orchestrator 的 Runbook 啟動其他 runbook 以 hello**叫用 Runbook**活動。 如果正在轉換的 hello runbook 中包含這個活動與 hello**等候完成**設定選項，然後為它建立之 runbook 活動轉換 hello runbook 中。  如果 hello**等候完成**未設定選項，則工作流程指令碼活動會建立使用**Start-azureautomationrunbook** toostart hello runbook。  您匯入至 Azure 自動化的 hello 轉換 runbook 之後，您必須修改此活動與 hello hello 活動中指定的資訊。

## <a name="related-articles"></a>相關文章
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [服務管理自動化](https://technet.microsoft.com/library/dn469260.aspx)
* [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)
* [Orchestrator 標準活動](http://technet.microsoft.com/library/hh403832.aspx)
* [下載 System Center Orchestrator 遷移工具組](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
