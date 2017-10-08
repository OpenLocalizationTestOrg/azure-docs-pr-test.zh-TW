---
title: "資源群組 aaaAutomate 移除 |Microsoft 文件"
description: "PowerShell 工作流程版本的 Azure 自動化案例，包括 runbook tooremove 以您訂用帳戶所有資源都群組。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: 
ms.assetid: b848e345-fd5d-4b9d-bc57-3fe41d2ddb5c
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: magoedte
ms.openlocfilehash: d7ff8064842385d57b0eebdf7b263150c958255f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automate-removal-of-resource-groups"></a>Azure 自動化案例 - 自動移除資源群組
許多客戶會建立一個以上的資源群組。 有些可能會用來管理生產應用程式，其他的可能會用來作為開發、測試和預備環境。 自動化 hello 部署這些資源是一件事，但無法 toodecommission hello 按鈕的資源群組是另一個。 您可以使用 Azure 自動化來簡化這個一般管理工作。 這是有幫助您正在使用 Azure 訂用帳戶具有消費限制，透過像 MSDN 或 Microsoft Partner Network Cloud Essentials 計畫 hello 成員優惠。

此案例中以 PowerShell runbook 為基礎，而且是設計的 tooremove 您指定從您的訂用帳戶的一或多個資源群組。 hello runbook hello 預設設定是 tootest 後再繼續。 這可確保您不小心刪除 hello 資源群組之前，您已準備好 toocomplete 此程序。   

## <a name="getting-hello-scenario"></a>取得 hello 案例
此案例包含 PowerShell runbook，您可以下載從 hello [PowerShell 資源庫](https://www.powershellgallery.com/packages/Remove-ResourceGroup/1.0/DisplayScript)。 您也可以匯入它直接從 hello [Runbook 庫](automation-runbook-gallery.md)hello Azure 入口網站中。<br><br>

| Runbook | 說明 |
| --- | --- |
| Remove-ResourceGroup |從 hello 訂用帳戶中移除一或多個 Azure 資源群組和相關聯的資源。 |

<br>
定義這個 runbook hello 下列輸入的參數：

| 參數 | 說明 |
| --- | --- |
| NameFilter (必要) |指定名稱篩選 toolimit hello 資源群組，您想刪除。 您可以使用逗號分隔清單傳遞多個值。<br>hello 篩選不區分大小寫，而且會比對任何資源群組含有 hello 字串。 |
| PreviewMode (選擇性) |執行 hello runbook toosee 哪些資源群組，就會刪除，但會採取任何動作。<br>hello 預設值是**true** toohelp 避免意外刪除一個或多個資源群組傳遞 toohello runbook。 |

## <a name="install-and-configure-this-scenario"></a>安裝和設定此案例
### <a name="prerequisites"></a>必要條件
此 runbook 會驗證使用 hello [Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。    

### <a name="install-and-publish-hello-runbooks"></a>安裝和發佈 runbook hello
下載 hello runbook 之後，您可以使用匯入它 hello 程序中的[匯入 runbook 的程序](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)。 它已經成功匯入您的自動化帳戶之後，請發行 hello runbook。

## <a name="using-hello-runbook"></a>使用 hello runbook
hello 下列步驟將引導您完成 hello 執行此 runbook 和您熟悉它的運作方式的說明。 您只測試 hello runbook 在這個範例中，不實際刪除 hello 資源群組。  

1. 從 hello Azure 入口網站，開啟您的自動化帳戶，然後按一下**Runbook**。
2. 選取 hello**移除 ResourceGroup** runbook 按一下**啟動**。
3. 當您啟動 hello runbook 時、 hello**啟動 Runbook**刀鋒視窗隨即開啟，而且您可以設定 hello 參數。 Hello 中輸入名稱的資源群組訂閱您的測試使用，而且會導致沒有壞處，如果意外刪除。<br> ![Remove-ResouceGroup 參數](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-input-parameters.png)

   > [!NOTE]
   > 請確定**Previewmode**設定得**true** tooavoid 刪除 hello 選取資源群組。  **請注意**此 runbook 將不會移除 hello 資源群組包含執行此 runbook 的 hello 自動化帳戶。  
   >
   >
4. 設定所有 hello 參數值之後，按一下**確定**，和 hello runbook 將執行排入佇列。  

tooview hello 詳細資料的 hello**移除 ResourceGroup** hello Azure 入口網站，選取在 runbook 工作**作業**hello runbook 中。 hello 工作摘要顯示 hello 輸入的參數及 hello 輸出串流此外 toogeneral hello 工作的資訊和發生的任何例外狀況。<br> ![Remove-ResourceGroup Runbook 作業狀態](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-status.png)。

hello**工作摘要**包括從 hello 輸出、 警告和錯誤資料流的訊息。 選取**輸出**tooview 詳細 hello runbook 執行的結果。<br> ![Remove-ResourceGroup Runbook 輸出結果](media/automation-scenario-remove-resourcegroup/remove-resourcegroup-runbook-job-output.png)

## <a name="next-steps"></a>後續步驟
* tooget 開始建立您自己的 runbook，請參閱[建立或匯入 Azure 自動化中的 runbook](automation-creating-importing-runbook.md)。
* 請參閱 < 開始使用 PowerShell 工作流程 runbook tooget[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)。
