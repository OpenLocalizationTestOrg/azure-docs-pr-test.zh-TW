---
title: "aaaMy 第一個圖形化 Azure 自動化中的 runbook |Microsoft 文件"
description: "教學課程會引導您進行 hello 建立、 測試和發佈的簡單圖形化 runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "runbook, runbook 範本, runbook 自動化, azure runbook"
ms.assetid: dcb88f19-ed2b-4372-9724-6625cd287c8a
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/17/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 964cf8bae75ca597959bfc39b2b07c22bbc9acb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-graphical-runbook"></a>我的第一個圖形化 Runbook

> [!div class="op_single_selector"]
> * [圖形化](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell 工作流程](automation-first-runbook-textual.md)
> 
> 

本教學課程將引導您完成建立 hello[圖形化 runbook](automation-runbook-types.md#graphical-runbooks) Azure 自動化中。  我們開始測試，我們會說明如何 tootrack hello hello runbook 工作的狀態時，發行的簡易 runbook。  然後我們修改 hello runbook tooactually 管理在此情況下啟動 Azure 虛擬機器的 Azure 資源。  然後我們完成 hello 教學課程，讓 hello runbook 更強固的加入 runbook 的參數和條件式連結。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您必須遵循的 hello。

* Azure 訂用帳戶。  如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。
* [Azure 自動化帳戶](automation-sec-configure-azure-runas-account.md)toohold hello runbook 並驗證 tooAzure 資源。  此帳戶必須具有權限 toostart，停止 hello 虛擬機器。
* Azure 虛擬機器。  我們將會停止並啟動這台電腦，因此它不應該是生產環境。

## <a name="step-1---create-runbook"></a>步驟 1 - 建立 Runbook
我們先建立輸出的 hello 文字的簡單 runbook *Hello World*。

1. 在 hello Azure 入口網站，開啟您的自動化帳戶。  
   hello 自動化帳戶 頁面可讓您快速檢視 hello 資源此帳戶中。  您應該已經有一些資產。  其中大部分都是會自動包含在新的自動化帳戶的 hello 模組。  您也應該擁有 hello 認證資產中所述 hello[必要條件](#prerequisites)。
2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。<br> ![Runbook 控制項](media/automation-first-runbook-graphical/runbooks-resources-tile.png)
3. 建立新的 runbook 上 hello 即可**新增 runbook**  按鈕，然後**建立新的 runbook**。
4. Hello runbook hello 命名*MyFirstRunbook 圖形*。
5. 在此情況下，我們會 toocreate[圖形化 runbook](automation-graphical-authoring-intro.md)因此選取**圖形**如**Runbook 類型**。<br> ![新的 Runbook](media/automation-first-runbook-graphical/create-new-runbook.png)<br>
6. 按一下**建立**toocreate hello runbook 和開啟 hello 圖形化編輯器。

## <a name="step-2---add-activities-toohello-runbook"></a>步驟 2-新增活動 toohello runbook
hello 左邊 hello hello 編輯器的程式庫控制項，可讓您 tooselect 活動 tooadd tooyour runbook。  我們會 tooadd **Write-output** cmdlet toooutput 文字從 hello runbook。

1. Hello 程式庫控制項，在中，按一下 hello [搜尋] 文字方塊以及類型**Write-output**。  hello 搜尋結果將會顯示如下。 <br> ![Microsoft.PowerShell.Utility](media/automation-first-runbook-graphical/search-powershell-cmdlet-writeoutput.png)
2. 捲動 toohello hello 清單的底部。  您可以請按滑鼠右鍵**Write-output**選取**新增 toocanvas**或按一下 hello 橢圓形下一個 toohello 指令程式，然後選取**新增 toocanvas**。
3. 按一下 hello **Write-output** hello 畫布上的活動。  這會開啟 hello 組態控制刀鋒視窗中，可讓您 tooconfigure hello 活動。
4. hello**標籤**預設 toohello hello cmdlet 名稱，但我們可以將它變更 toosomething 更易懂。 它也變更*寫入 Hello World toooutput*。
5. 按一下**參數**tooprovide hello cmdlet 參數的值。  
   部分指令程式有多個參數集，而且您需要 tooselect 哪些您的一個 toouse。 在此情況下， **Write-output**設有只有一個參數，因此您不需要 tooselect 其中一個。 <br> ![Write-Output 屬性](media/automation-first-runbook-graphical/write-output-properties-b.png)
6. 選取 hello **InputObject**參數。  這是我們可以在此指定 hello 文字 toosend toohello 輸出資料流 hello 參數。
7. 在 hello**資料來源**下拉式清單中，選取**PowerShell 運算式**。  hello**資料來源**下拉式清單提供不同的來源，您會使用 toopopulate 參數值。  
   您可以使用來自這類來源的輸出，例如另一個活動、自動化資產或 PowerShell 運算式。  在此情況下，我們只是想 toooutput hello 文字*Hello World*。 我們可以使用 PowerShell 運算式，並指定字串。
8. 在 hello**運算式**方塊中，輸入*"Hello World"* ，然後按一下**確定**兩次 tooreturn toohello 畫布。<br> ![PowerShell Expression](media/automation-first-runbook-graphical/expression-hello-world.png)
9. 按一下以儲存 hello runbook**儲存**。<br> ![儲存 Runbook](media/automation-first-runbook-graphical/runbook-toolbar-save-revised20165.png)

## <a name="step-3---test-hello-runbook"></a>步驟 3-測試 hello runbook
我們發行 hello runbook toomake 之前它可用在生產環境中，我們想要 tootest 它 toomake 確定它是否正常運作。  測試 Runbook 時，您會執行其 **草稿** 版本，並以互動方式檢視其輸出。

1. 按一下**測試窗格**tooopen hello 測試刀鋒視窗。<br> ![測試窗格](media/automation-first-runbook-graphical/runbook-toolbar-test-revised20165.png)
2. 按一下**啟動**toostart hello 測試。  這應該是 hello 才啟用選項。
3. A [runbook 工作](automation-runbook-execution.md)建立 hello 窗格中顯示及其狀態。  
   做為啟動 hello 作業狀態*排入佇列*表示它正在等待在 hello 雲端 toobecome 可用的 runbook worker。  然後移動太*起始*背景工作宣告 hello 作業時，然後*執行*hello runbook 實際開始執行時。  
4. 當 hello runbook 作業完成時，會顯示其輸出。 在我們的情況中，我們應該會看到 Hello World。<br> ![](media/automation-first-runbook-graphical/runbook-test-results.png)
5. 關閉 hello 測試刀鋒視窗 tooreturn toohello 畫布。

## <a name="step-4---publish-and-start-hello-runbook"></a>步驟 4-發佈和啟動 hello runbook
我們建立的 hello runbook 仍處於草稿模式。 我們需要 toopublish 前我們可以在生產環境中執行它。  當您發行的 runbook 時，您以覆寫現有已發佈版本 hello hello 草稿版本。  在我們的案例中，我們已發佈版本還沒有因為我們剛才建立 hello runbook。

1. 按一下**發行**toopublish hello runbook，然後**是**出現提示時。<br> ![](media/automation-first-runbook-graphical/runbook-toolbar-publish-revised20166.png)
2. 當您捲動左的 tooview hello runbook 在 hello **Runbook**刀鋒視窗中，顯示**撰寫狀態**的**發佈**。
3. 捲軸背景 toohello 右 tooview hello 刀鋒視窗的**MyFirstRunbook**。  
   hello hello 頂端的選項讓我們 toostart hello runbook、 排程在未來，hello toostart 或建立[webhook](automation-webhooks.md)讓它可以啟動透過 HTTP 呼叫。
4. 我們只是想 toostart hello runbook 因此按一下**啟動**然後**是**出現提示時。<br> ![啟動 Runbook](media/automation-first-runbook-graphical/runbook-controls-start-revised20165.png)
5. 作業刀鋒視窗會開啟供我們建立的 hello runbook 工作。  我們可以關閉此刀鋒視窗中，但在此情況下我們維持開啟，因此我們可以觀看 hello 作業的進度。
6. 中會顯示 hello 作業狀態**工作摘要**和相符項目 hello 我們了解我們所測試 hello runbook 時的狀態。<br> ![工作摘要](media/automation-first-runbook-graphical/runbook-job-summary.png)
7. 一次 hello runbook 狀態顯示*已完成*，按一下 **輸出**。 hello**輸出**刀鋒視窗會開啟，而且我們可以看到我們*Hello World* hello 窗格中。<br> ![工作摘要](media/automation-first-runbook-graphical/runbook-job-output.png)  
8. 關閉 hello 輸出刀鋒視窗。
9. 按一下**所有記錄檔**tooopen hello 資料流刀鋒視窗中的 hello runbook 工作。  我們應該只會看到*Hello World*在 hello 輸出資料流，但這會顯示 runbook 作業，例如 Verbose 和錯誤的其他資料流 hello runbook 是否寫入 toothem。<br> ![工作摘要](media/automation-first-runbook-graphical/runbook-job-AllLogs.png)
10. 關閉刀鋒視窗中的所有記錄 hello 和 hello 作業 刀鋒視窗 tooreturn toohello MyFirstRunbook 刀鋒視窗。
11. 按一下**作業**tooopen hello 作業刀鋒視窗，這個 runbook。  這會列出這個 runbook 所建立的所有 hello 作業。 我們只能看到列出因為我們只執行 hello 作業一次一項作業。<br> ![作業](media/automation-first-runbook-graphical/runbook-control-jobs.png)
12. 您可以按一下此工作 tooopen hello 我們開始 hello runbook 時，我們會檢視的相同 [工作] 窗格。  這可讓您 toogo 回時間和檢視 hello 詳細資料中針對特定 runbook 所建立的任何作業。

## <a name="step-5---create-variable-assets"></a>步驟 5 - 建立變數資產
我們已經測試並發行我們 Runbook，但是到目前為止，它似乎並不實用。 我們想要 toohave 它管理的 Azure 資源。  我們設定 hello runbook tooauthenticate 之前，我們會建立變數 toohold hello 訂用帳戶 ID，而且我們設定在步驟 6 中的 hello 活動 tooauthenticate 之後參考它。  包括參考 toohello 訂用帳戶內容，讓您 tooeasily 工作在多個訂用帳戶之間。  繼續之前，請從 hello 關閉 hello 瀏覽窗格的 [訂閱] 選項複製訂用帳戶 ID。  

1. 在 hello 自動化帳戶刀鋒視窗中，按一下 hello**資產**磚與 hello**資產**開啟刀鋒視窗。
2. 在 hello 資產刀鋒視窗中，按一下 hello**變數**磚。
3. 在 hello 變數刀鋒視窗中，按一下 **加入變數**。<br>![自動化變數](media/automation-first-runbook-graphical/create-new-subscriptionid-variable.png)
4. 在 hello 新變數 刀鋒視窗，在 hello**名稱**方塊中，輸入**AzureSubscriptionId**在 hello**值**中，輸入您的訂用帳戶識別碼。  保留*字串*hello**類型**hello 的預設值和**加密**。  
5. 按一下**建立**toocreate hello 變數。  

## <a name="step-6---add-authentication-toomanage-azure-resources"></a>步驟 6-新增驗證 toomanage Azure 資源
既然我們已經有變數 toohold 我們訂用帳戶 ID，我們可以使用 hello 執行身分認證的參照的 tooin hello 設定我們 runbook tooauthenticate[必要條件](#prerequisites)。  方法是新增 hello Azure 執行身分連線**資產**和**新增 AzureRMAccount** cmdlet toohello 畫布。  

1. 開啟 hello 圖形化編輯器，依序按一下**編輯**hello MyFirstRunbook 刀鋒視窗上。<br> ![編輯 Runbook](media/automation-first-runbook-graphical/runbook-controls-edit-revised20165.png)
2. 我們不需要 hello**寫入 Hello World toooutput**失效，所以它以滑鼠右鍵按一下並選取**刪除**。
3. 在 hello 程式庫控制項，依序展開**連線**並加入**AzureRunAsConnection** toohello 畫布上選取**新增 toocanvas**。
4. Hello 畫布上選取**AzureRunAsConnection** hello 組態控制在窗格中，輸入**取得執行做為連接**在 hello**標籤**文字方塊。  這是 hello 連線
5. 在 hello 程式庫控制項，輸入**新增 AzureRmAccount** hello 搜尋 文字方塊中。
6. 新增**新增 AzureRmAccount** toohello 畫布。<br> ![](media/automation-first-runbook-graphical/search-powershell-cmdlet-addazurermaccount.png)
7. 將滑鼠停留在**取得執行做為連接**直到 hello 底部 hello 圖形上會出現一個圓圈。 按一下 hello 圓形，然後拖曳 hello 箭號太**新增 AzureRmAccount**。  您所建立的 hello 箭號是*連結*。  hello runbook 以開始**取得執行做為連接**，然後執行**新增 AzureRmAccount**。<br> ![建立活動之間的連結](media/automation-first-runbook-graphical/runbook-link-auth-activities.png)
8. Hello 畫布上選取**新增 AzureRmAccount** hello 組態控制窗格類型和**登入 tooAzure**在 hello**標籤**文字方塊。
9. 按一下**參數**和 hello 活動參數設定刀鋒視窗隨即出現。
10. **新增 AzureRmAccount**有多個參數集，因此我們需要一個 tooselect 之前，我們可以提供參數值。  按一下**參數設定**]，然後選取 [hello **ServicePrincipalCertificatewithSubscriptionId**參數集。
11. 一旦您選取 hello 參數集時，會顯示 hello 參數在 hello 活動參數設定 刀鋒視窗。  按一下 [APPLICATIONID]。<br> ![加入 Azure RM 帳戶參數](media/automation-first-runbook-graphical/add-azurermaccount-params.png)
12. 在 hello 參數值刀鋒視窗中，選取 **活動輸出**hello**資料來源**並選取**取得執行做為連接**從 hello 清單中，在 hello**欄位路徑**文字方塊中的型別**ApplicationId**，然後按一下**確定**。  我們會指定 hello 屬性 hello 欄位路徑 hello 名稱，因為 hello 活動會輸出具有多個屬性的物件。
13. 按一下**CERTIFICATETHUMBPRINT**，然後在 hello 參數值刀鋒視窗中，選取**活動輸出**hello**資料來源**。  選取**取得執行做為連接**從 hello 清單中，在 hello**欄位路徑**文字方塊中的型別**CertificateThumbprint**，然後按一下 **[確定]**。
14. 按一下**SERVICEPRINCIPAL**，然後在 hello 參數值刀鋒視窗中，選取**ConstantValue** hello**資料來源**，按一下 hello 選項**True**，然後按一下**確定**。
15. 按一下**TENANTID**，然後在 hello 參數值刀鋒視窗中，選取**活動輸出**hello**資料來源**。  選取**取得執行做為連接**從 hello 清單中，在 hello**欄位路徑**文字方塊中的型別**TenantId**，然後按一下 **[確定]**兩次。  
16. 在 hello 程式庫控制項，輸入**組 AzureRmContext** hello 搜尋 文字方塊中。
17. 新增**組 AzureRmContext** toohello 畫布。
18. Hello 畫布上選取**組 AzureRmContext** hello 組態控制窗格類型和**指定訂用帳戶 Id**在 hello**標籤**文字方塊。
19. 按一下**參數**和 hello 活動參數設定刀鋒視窗隨即出現。
20. **設定 AzureRmContext**有多個參數集，因此我們需要一個 tooselect 之前，我們可以提供參數值。  按一下**參數設定**]，然後選取 [hello **SubscriptionId**參數集。  
21. 一旦您選取 hello 參數集時，會顯示 hello 參數在 hello 活動參數設定 刀鋒視窗。  按一下 [SubscriptionID] 
22. 在 hello 參數值刀鋒視窗中，選取 **變數資產**hello**資料來源**選取**AzureSubscriptionId**從 hello 清單，然後按一下**確定**兩次。   
23. 將滑鼠停留在**登入 tooAzure**直到 hello 底部 hello 圖形上會出現一個圓圈。 按一下 hello 圓形，然後拖曳 hello 箭號太**指定訂用帳戶 Id**。

您的 runbook 看起來應該像 hello 遵循此時： <br>![Runbook 驗證組態](media/automation-first-runbook-graphical/runbook-auth-config.png)

## <a name="step-7---add-activity-toostart-a-virtual-machine"></a>步驟 7-新增活動 toostart 虛擬機器
我們在這裡新增**開始 AzureRmVM**活動 toostart 虛擬機器。  您可以挑選任何虛擬機器，您的 Azure 訂閱，而且現在您硬，名稱為 hello cmdlet。

1. 在 hello 程式庫控制項，輸入**開始 AzureRm** hello 搜尋 文字方塊中。
2. 新增**開始 AzureRmVM** toohello 畫布，然後按一下並拖曳它下方**指定訂用帳戶 Id**。
3. 將滑鼠停留在**指定訂用帳戶 Id**直到 hello 底部 hello 圖形上會出現一個圓圈。  按一下 hello 圓形，然後拖曳 hello 箭號太**開始 AzureRmVM**。
4. 選取 [Start-AzureRmVM]。  按一下**參數**然後**參數設定**tooview hello 設定**開始 AzureRmVM**。  選取 hello **ResourceGroupNameParameterSetName**參數集。 請注意，[ResourceGroupName] 和 [名稱] 旁邊具有驚嘆號。  這表示它們是必要的參數。  也請注意這兩者應該是字串值。
5. 選取 [Start-AzureRmVM] 。  選取**PowerShell 運算式**hello**資料來源**和 hello 名稱中的 hello 虛擬機器以我們開始此 runbook 的雙引號括住的類型。  按一下 [確定] 。<br>![Start-AzureRmVM 名稱參數值](media/automation-first-runbook-graphical/runbook-startvm-nameparameter.png)
6. 選取 [ResourceGroupName]。 使用**PowerShell 運算式**hello**資料來源**和 hello 名稱中的 hello 資源群組以雙引號括住的類型。  按一下 [確定] 。<br> ![Start-AzureRmVM 參數](media/automation-first-runbook-graphical/startazurermvm-params.png)
7. 以便我們可以測試 hello runbook，請按一下 [測試] 窗格。
8. 按一下**啟動**toostart hello 測試。  在完成時，請檢查該 hello 虛擬機器已啟動。

您的 runbook 看起來應該像 hello 遵循此時： <br>![Runbook 驗證組態](media/automation-first-runbook-graphical/runbook-startvm.png)

## <a name="step-8---add-additional-input-parameters-toohello-runbook"></a>步驟 8-新增額外的輸入的參數 toohello runbook
我們 runbook 目前啟動 hello 的虛擬機器在 hello 我們 hello 中指定的資源群組中**開始 AzureRmVM** cmdlet。  我們的 runbook 會是我們無法同時指定 hello runbook 啟動時的更實用。  我們現在加入輸入的參數 toohello runbook tooprovide 該功能。

1. 開啟 hello 圖形化編輯器，依序按一下**編輯**上 hello **MyFirstRunbook**窗格。
2. 按一下**輸入和輸出**然後**加入輸入**tooopen hello Runbook 輸入參數 窗格。<br> ![Runbook 輸入和輸出](media/automation-first-runbook-graphical/runbook-toolbar-InputandOutput-revised20165.png)
3. 指定*VMName* hello**名稱**。  保留*字串*hello**類型**，但變更**強制**太*是*。  按一下 [確定] 。
4. 建立第二個必要的輸入的參數，呼叫*ResourceGroupName* ，然後按一下**確定**tooclose hello**輸入和輸出**窗格。<br> ![Runbook 輸入參數](media/automation-first-runbook-graphical/start-azurermvm-params-outputs.png)
5. 選取 hello**開始 AzureRmVM**活動，然後按一下**參數**。
6. 變更 hello**資料來源**如**名稱**太**Runbook 輸入**，然後選取  **VMName**。<br>
7. 變更 hello**資料來源**如**ResourceGroupName**太**Runbook 輸入**，然後選取  **ResourceGroupName**。<br> ![Start-AzureVM 參數](media/automation-first-runbook-graphical/start-azurermvm-params-runbookinput.png)
8. 儲存 hello runbook 並開啟 hello 測試窗格。  請注意，您可以現在提供值給 hello hello 測試中使用兩個輸入的變數。
9. 關閉 hello 測試窗格。
10. 按一下**發行**toopublish hello 新版 hello runbook。
11. 停止 hello hello 上一個步驟中啟動的虛擬機器。
12. 按一下**啟動**toostart hello runbook。  型別在 hello **VMName**和**ResourceGroupName**要 toostart hello 虛擬機器。<br> ![Start Runbook](media/automation-first-runbook-graphical/runbook-start-inputparams.png)
13. Hello runbook 完成時，請檢查該 hello 虛擬機器已啟動。

## <a name="step-9---create-a-conditional-link"></a>步驟 9 - 建立條件式連結
我們現在修改 hello runbook，使它只會嘗試 toostart hello 虛擬機器未啟動。  您可以加入**Get AzureRmVM**取得 hello hello 虛擬機器的執行個體層級狀態的 cmdlet toohello runbook。 接著您將新增的 PowerShell 工作流程程式碼模組稱為**取得狀態**PowerShell 的程式碼片段，碼 toodetermine hello 虛擬機器狀態是否正在執行或已停止。  條件式連結從 hello**取得狀態**模組只會執行**開始 AzureRmVM**如果停止 hello 目前執行中狀態。  最後，我們會輸出訊息 tooinform 您 hello VM 是否已成功啟動或不使用 hello PowerShell Write-output cmdlet。

1. 開啟**MyFirstRunbook** hello 圖形化編輯器中。
2. 移除 hello 連結之間**指定訂用帳戶 Id**和**開始 AzureRmVM**按一下它，然後按 hello*刪除*索引鍵。
3. 在 hello 程式庫控制項，輸入**Get AzureRm** hello 搜尋 文字方塊中。
4. 新增**Get AzureRmVM** toohello 畫布。
5. 選取**Get AzureRmVM**然後**參數設定**tooview hello 設定**Get AzureRmVM**。  選取 hello **GetVirtualMachineInResourceGroupNameParamSet**參數集。  請注意，[ResourceGroupName] 和 [名稱] 旁邊具有驚嘆號。  這表示它們是必要的參數。  也請注意這兩者應該是字串值。
6. 在 [名稱] 的 [資料來源] 底下，選取 [Runbook 輸入]，然後選取 [VMName]。  按一下 [確定] 。
7. 在 [ResourceGroupName] 的 [資料來源] 底下，選取 [Runbook 輸入]，然後選取 [ResourceGroupName]。  按一下 [確定] 。
8. 在 狀態 的 資料來源 底下，選取 常數值，然後按一下True。  按一下 [確定] 。  
9. 建立連結，以從**指定訂用帳戶 Id**太**Get AzureRmVM**。
10. 在 hello 程式庫控制項中展開**Runbook 控制**並加入**程式碼**toohello 畫布。  
11. 建立連結，以從**Get AzureRmVM**太**程式碼**。  
12. 按一下**程式碼**和 hello 組態在窗格中，變更標籤太**取得狀態**。
13. 選取**程式碼**參數和 hello**程式碼編輯器**刀鋒視窗隨即出現。  
14. 在 hello 程式碼編輯器中，貼上下列程式碼片段的 hello:
    
     ```
     $StatusesJson = $ActivityOutput['Get-AzureRmVM'].StatusesText
     $Statuses = ConvertFrom-Json $StatusesJson
     $StatusOut =""
     foreach ($Status in $Statuses){
     if($Status.Code -eq "Powerstate/running"){$StatusOut = "running"}
     elseif ($Status.Code -eq "Powerstate/deallocated") {$StatusOut = "stopped"}
     }
     $StatusOut
     ```
15. 建立連結，以從**取得狀態**太**開始 AzureRmVM**。<br> ![程式碼模組的 Runbook](media/automation-first-runbook-graphical/runbook-startvm-get-status.png)  
16. 選取 hello 連結，並在 hello 設定窗格中，變更**套用條件**太**是**。   請注意 hello 連結會開啟 tooa 虛線一行指出 hello 目標活動只能執行是否 hello 條件解析 tootrue。  
17. Hello**條件運算式**，型別*$ActivityOutput [' 取得狀態 ']-eq"Stopped"*。  **開始 AzureRmVM**現在僅執行如果 hello 虛擬機器已停止。
18. 在 hello 程式庫控制項，依序展開**Cmdlet**然後**Microsoft.PowerShell.Utility**。
19. 新增**Write-output** toohello 畫布兩次。<br> ![Write-Output 的 Runbook](media/automation-first-runbook-graphical/runbook-startazurermvm-complete.png)
20. Hello 上第一個**Write-output**控制，請按一下**參數**並變更 hello**標籤**值太*通知 VM 啟動*。
21. 如**InputObject**，變更**資料來源**太**PowerShell 運算式**hello 運算式中的類型和*"$VMName 已順利啟動。 」*.
22. Hello 上第二個**Write-output**控制，請按一下**參數**並變更 hello**標籤**值太*通知 VM 啟動失敗*
23. 如**InputObject**，變更**資料來源**太**PowerShell 運算式**hello 運算式中的類型和*"$VMName 無法啟動。 」*.
24. 建立連結，以從**開始 AzureRmVM**太**通知 VM 啟動**和**通知 VM 啟動失敗**。
25. 選取 hello 連結太**通知 VM 啟動**並變更**套用條件**太**True**。
26. Hello**條件運算式**，型別*$ActivityOutput [' 開始-AzureRmVM']。IsSuccessStatusCode-eq $true*。  此寫入輸出控制現在僅執行 hello 虛擬機器已順利啟動。
27. 選取 hello 連結太**通知 VM 啟動失敗**並變更**套用條件**太**True**。
28. Hello**條件運算式**，型別*$ActivityOutput [' 開始-AzureRmVM']。IsSuccessStatusCode ne $true*。  此寫入輸出現在控制才會執行，如果未成功啟動 hello 虛擬機器。
29. 儲存 hello runbook 並開啟 hello 測試窗格。
30. 啟動 hello runbook 與 hello 虛擬機器已停止，並開始時間。

## <a name="next-steps"></a>後續步驟
* toolearn 詳細資料圖形化撰寫，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)
* 請參閱 < 開始使用 PowerShell runbook tooget[我的第一個 PowerShell runbook](automation-first-runbook-textual-powershell.md)
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)

