---
title: "Azure 自動化 aaaRunbook 和模組組件庫 |Microsoft 文件"
description: "Runbook 與模組的 Microsoft 和 hello 社群成員可供您 tooinstall，而且您的 Azure 自動化環境中使用。  本文說明如何存取這些資源和 toocontribute runbook toohello 圖庫。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Azure 自動化的 Runbook 和模組資源庫
而不是在 Azure 自動化中建立您自己的 runbook 與模組，您可以存取的各種已經建置由 Microsoft 和 hello 社群的案例。  您可以不加修改地使用這些案例，或者使用它們做為起點並針對您的特定需求進行編輯。

您可以從 hello 取得 runbook [Runbook 庫](#runbooks-in-runbook-gallery)和模組從 hello [PowerShell 資源庫](#modules-in-powerShell-gallery)。  您也可以透過分享您所開發的案例會導致 toohello 社群。

## <a name="runbooks-in-runbook-gallery"></a>Runbook 資源庫中的 Runbook
hello [Runbook 庫](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation)從 Microsoft 和 hello 社群，您可以匯入至 Azure 自動化中提供各種不同的 runbook。 您可以從裝載於 hello hello 組件庫下載 runbook [TechNet 指令碼中心](https://gallery.technet.microsoft.com/scriptcenter/site/upload)，或您可以從 hello 庫 hello Azure 傳統入口網站或 Azure 入口網站直接匯入 runbook。

您可以只匯入直接從 hello Runbook 庫使用 hello Azure 傳統入口網站或 Azure 入口網站。 您無法使用 Windows PowerShell 執行此函式。

> [!NOTE]
> 您應該驗證 hello 內容從 hello Runbook 庫取得，且小心中安裝及執行它們在生產環境中的任何 runbook。 |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport hello Runbook 資源庫以 hello Azure 傳統入口網站的 runbook
1. 在 hello Azure 入口網站中，按一下，**新增**，**應用程式服務**，**自動化**， **Runbook**，**從組件庫**.
2. 選取類別目錄 tooview 相關 runbook，然後選取 runbook tooview 其詳細資料。 當您選取您想要的 hello runbook 時，請按一下 hello 向右箭號按鈕。
   
    ![Runbook 資源庫](media/automation-runbook-gallery/runbook-gallery.png)
3. 檢閱 hello hello runbook 內容，並記下 hello 描述中的任何需求。 當您完成時，請按一下 hello 向右箭號按鈕。
4. 輸入 hello runbook 詳細資料，然後按一下hello 核取記號按鈕。 將已填入 hello runbook 名稱。
5. hello runbook 會出現在 hello **Runbook** hello 自動化帳戶 索引標籤。

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport hello Runbook 資源庫以 hello Azure 入口網站的 runbook
1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。
3. 按一下 [瀏覽資源庫]  按鈕。
   
    ![瀏覽資源庫按鈕](media/automation-runbook-gallery/browse-gallery-button.png)
4. 找出 hello 主機庫項目，然後選取它 tooview 其詳細資料。
   
    ![瀏覽資源庫](media/automation-runbook-gallery/browse-gallery.png)
5. 按一下**檢視原始碼專案**tooview hello 項目在 hello [TechNet 指令碼中心](http://gallery.technet.microsoft.com/)。
6. tooimport 項目，按一下 tooview 其詳細資料，然後按一下hello**匯入** 按鈕。
   
    ![匯入按鈕](media/automation-runbook-gallery/gallery-item-detail.png)
7. （選擇性） 變更 hello hello runbook 名稱，然後按一下**確定**tooimport hello runbook。
8. hello runbook 會出現在 hello **Runbook** hello 自動化帳戶 索引標籤。

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>新增 runbook toohello runbook 資源庫
Microsoft 會鼓勵 tooadd runbook toohello 您認為有用 tooother 客戶的 Runbook 資源庫。  您可以新增 runbook[將資料上傳 toohello 指令碼中心](http://gallery.technet.microsoft.com/site/upload)納入帳戶 hello 下列詳細資料。

* 您必須指定*Windows Azure* hello**類別**和*自動化*hello **Subcategory**的 hello runbook toobe 顯示在 hello 精靈。  
* hello 上載必須是單一.ps1 或.graphrunbook 檔案。  如果 hello runbook 需要任何模組、 子系 runbook 或資產，則您應該列出 hello 送出 hello 描述中，並且在 hello runbook hello 註解區段。  如果您需要多個 runbook 的案例，然後才能上傳每個個別，以及列出 hello 名稱的 hello 相關各項描述中的 runbook。 請確定您使用的相同標記，因此它們會顯示在 hello hello 相同類別目錄。 使用者會有其他 runbook 所需要的 hello 案例 toowork tooread hello 描述 tooknow。
* 如果您要發行，加入 hello 標記"GraphicalPS"**圖形化 runbook** （沒有圖形化工作流程）。 
* 插入 hello 說明使用 PowerShell 或 PowerShell 工作流程的程式碼片段**插入程式碼區段**圖示。
* hello hello 上傳摘要會顯示在 Runbook 庫結果，因此您應該提供詳細的資訊可協助使用者識別的 hello runbook 的 hello 功能 hello。
* 您應指派一個 toothree 的 hello 下列標記 toohello 上傳。  hello runbook 會列出在 hello 精靈中符合 runbook 標記的 hello 類別之下。  Hello 精靈會略過此清單上沒有任何標記。 如果您未指定任何相符的標記，hello runbook 將會列在 hello 其他類別。
  
  * 備份
  * 產能管理
  * 變更控制
  * 法規遵循
  * 開發/測試環境
  * 災害復原
  * 監視
  * 修補
  * 佈建
  * 補救
  * VM 生命週期管理
* 自動化更新 hello 圖庫小時一次，所以不會立即看到您的貢獻。

## <a name="modules-in-powershell-gallery"></a>PowerShell 資源庫中的模組
PowerShell 模組包含 cmdlet，您可以使用您的 runbook 中，您可以安裝在 Azure 自動化中的現有模組在 hello [PowerShell 資源庫](http://www.powershellgallery.com)。  您可以啟動這個組件庫，從 hello Azure 入口網站，並直接在 Azure 自動化安裝，或您可以下載它們並手動進行安裝。  您無法直接從 hello Azure 傳統入口網站安裝 hello 模組，但您也可以將其下載安裝它們，如同任何其他模組。

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport hello 自動化模組資源庫以 hello Azure 入口網站的模組
1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 按一下 hello**資產**磚 tooopen hello 列出的資產清單。
3. 按一下 hello**模組**磚 tooopen hello 模組的清單。
4. 按一下 hello**瀏覽圖庫**啟動按鈕和 hello 瀏覽圖庫刀鋒視窗。
   
    ![模組資源庫](media/automation-runbook-gallery/modules-blade.png) <br>
5. 您啟動 hello 瀏覽圖庫刀鋒視窗之後，您可以搜尋下列欄位的 hello:
   
   * 模組名稱
   * 標記
   * 作者
   * Cmdlet/DSC 資源名稱
6. 找出您感興趣，並選取該 tooview 模組其詳細資料。  
   當您向下鑽研至特定模組時，您可以檢視需 hello 模組，包括連結後 toohello PowerShell 資源庫中，任何必要的相依性，而且所有 hello cmdlet 及/或 hello 模組的 DSC 資源的包含。
   
    ![PowerShell 模組的詳細資料](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. tooinstall hello 模組，直接在 Azure 自動化中，按一下 [hello**匯入**] 按鈕。
   
    ![[匯入模組] 按鈕](media/automation-runbook-gallery/module-import-button.png)
8. 當您按一下 hello 匯入 按鈕時，您會看到您所需 tooimport hello 模組名稱。 如果已安裝所有的 hello 相依性，hello**確定**按鈕將處於使用中。 如果您遺漏相依性，您需要 tooimport 這些之前您可以匯入此模組。
9. 按一下**確定**tooimport hello 模組和 hello 模組刀鋒視窗，將會啟動。 當 Azure 自動化匯入模組 tooyour 帳戶時，它會擷取 hello 模組和 hello 指令程式的相關中繼資料。
   
    ![[匯入模組] 刀鋒視窗](media/automation-runbook-gallery/module-import-blade.png)
   
    因為每個活動需要 toobe 擷取，這可能需要數分鐘。
10. 您會收到通知正在部署該 hello 模組的通知完成時。
11. Hello 模組匯入之後，您會看到 hello 可用的活動，而且您可以使用其在您的 runbook 和預期狀態設定資源。

## <a name="requesting-a-runbook-or-module"></a>要求 Runbook 或模組
您可以將要求傳送太[User Voice](https://feedback.azure.com/forums/246290-azure-automation/)。  如果您需要協助撰寫 runbook，或有 PowerShell 疑問，張貼問題 tooour[論壇](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc)。

## <a name="next-steps"></a>後續步驟
* tooget 啟動 runbook，請參閱[建立或匯入在 Azure 自動化 runbook](automation-creating-importing-runbook.md)
* toounderstand hello 差異 PowerShell 和 PowerShell 工作流程與 runbook，請參閱[學習 PowerShell 工作流程](automation-powershell-workflow.md)

