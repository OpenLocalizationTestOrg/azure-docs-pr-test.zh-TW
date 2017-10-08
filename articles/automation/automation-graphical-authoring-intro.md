---
title: "aaaGraphical Azure 自動化中撰寫 |Microsoft 文件"
description: "圖形化撰寫可讓您 toocreate runbook Azure 自動化而不需要使用程式碼。 本文章提供簡介 toographical 撰寫，而且所有 hello 詳細資料都需要 toostart 建立圖形化 runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 4b6f840c-e941-4293-a728-b33407317943
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 6ddf18b992d5e5f7f4af95f344007a63ac498549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="graphical-authoring-in-azure-automation"></a>Azure 自動化中的圖形化編寫
## <a name="introduction"></a>簡介
圖形化撰寫可讓您 toocreate runbook Azure 自動化不 hello hello 基礎 Windows PowerShell 或 PowerShell 工作流程的程式碼的複雜度。 您從 cmdlet 與 runbook 的程式庫加入活動 toohello 畫布、 連結在一起，並設定 tooform 工作流程。  如果您曾經使用過 System Center Orchestrator 或服務管理自動化 (SMA)，然後這看起來應該熟悉 tooyou。   

本文章提供簡介 toographical 需要 tooget 開始建立圖形化 runbook 的撰寫與 hello 概念。

## <a name="graphical-runbooks"></a>圖形化 Runbook
Azure 自動化中的所有 Runbook 都是 Windows PowerShell 工作流程。  圖形化和圖形化 PowerShell 工作流程 runbook 產生 hello 自動化背景工作，所執行的 PowerShell 程式碼，但是您不能 tooview 它，或直接修改它。  圖形化 runbook 可以轉換的 tooa 圖形化 PowerShell 工作流程 runbook，反之亦然，但它們不能是轉換的 tooa 文字 runbook。 現有的文字 runbook 無法匯入 hello 圖形化編輯器中。  

## <a name="overview-of-graphical-editor"></a>圖形化編輯器概觀
您可以開啟 hello Azure 入口網站中的 hello 圖形化編輯器，建立或編輯圖形化 runbook。

![圖形化工作區](media/automation-graphical-authoring-intro/runbook-graphical-editor.png)

hello 下列章節說明在 hello 圖形化編輯器中的 hello 控制項。

### <a name="canvas"></a>畫布
hello 畫布是您用來設計您的 runbook。  您從 hello hello 程式庫控制項 toohello runbook 中的節點加入活動，並連接它們的 hello runbook 連結 toodefine hello 邏輯。

您可以在 hello 底部 hello 畫布 toozoom 入和移出使用 hello 控制項。

![圖形化工作區](media/automation-graphical-authoring-intro/runbook-canvas-controls.png)

### <a name="library-control"></a>程式庫控制項
hello 程式庫控制項是您在其中選取[活動](#activities)tooadd tooyour runbook。  您會將其加入連接它們 tooother 活動 toohello 畫布。  它包含 hello 下表中所述的四個區段。

| 區段 | 說明 |
|:--- |:--- |
| Cmdlet |您在 runbook 中包含所有可用的 hello cmdlet。  Cmdlet 是依模組組織。  所有您已安裝在您的自動化帳戶中的 hello 模組會使用。 |
| Runbook |納入您的自動化帳戶中的 hello runbook。 這些 runbook 可以加入 toohello 畫布 toobe 做為子 runbook。 只有 runbook 的 hello 相同核心類型為 hello 正在編輯的 runbook 會顯示。圖形化 runbook 只能以 PowerShell 為基礎的 runbook 會顯示，而顯示的圖形化 PowerShell 工作流程 runbook 只能 PowerShell-工作流程式 runbook。 |
| Assets |包含 hello[自動化資產](http://msdn.microsoft.com/library/dn939988.aspx)中您可以使用您在 runbook 中的自動化帳戶。  當您新增的資產 tooa runbook 時，它會將工作流程活動，以取得 hello 選的資產。  在變數的資產的 hello 案例中，您可以選取是否 tooadd 活動 tooget hello hello 變數或設定變數。 |
| Runbook 控制項 |包含可在目前的 Runbook 中使用的 Runbook 控制項活動。 A*聯合*接受多個輸入，並等待，直到所有已完成之前繼續 hello 工作流程。 A*程式碼*活動執行的 PowerShell 或 PowerShell 工作流程的程式碼，根據 hello 圖形化 runbook 類型的一或多行。  您可以使用此活動的自訂程式碼或困難 tooachieve 與其他活動的功能。 |

### <a name="configuration-control"></a>組態控制項
hello 組態控制會為您提供詳細資料的 hello 畫布上選取的物件。 此控制項中可用的 hello 屬性將取決於 hello 選取物件類型。  當您在 hello 設定控制項中選取的選項時，就會開啟其他刀鋒視窗中訂單 tooprovide 額外資訊。

### <a name="test-control"></a>測試控制項
hello 圖形化編輯器初次啟動時，不會顯示 hello 測試控制項。 當您以互動方式 [測試圖形化 Runbook](#graphical-runbook-procedures)時會開啟。  

## <a name="graphical-runbook-procedures"></a>圖形化 Runbook 程序
### <a name="exporting-and-importing-a-graphical-runbook"></a>匯出和匯入圖形化 Runbook
您可以只匯出 hello 的圖形化 runbook 已發佈的版本。  如果尚未發行 hello runbook，然後 hello**匯出發行**按鈕將會停用。  當您按一下 hello**匯出發行**按鈕，hello runbook 是下載的 tooyour 本機電腦。  hello hello 檔案名稱符合 hello hello runbook 名稱*graphrunbook*延伸模組。

![匯出已發行](media/automation-graphical-authoring-intro/runbook-export.png)

您可以將圖形化 PowerShell 工作流程的 runbook 檔案匯入選取 hello**匯入**選項新增 runbook 時。   當您選取 hello 檔案 tooimport 時，您可以保留相同的 hello**名稱**或提供一個新。  後選取 hello 檔案，而且如果您嘗試 tooselect 不正確，會看到訊息，記下有可能發生的衝突，並在轉換期間，可能會有不同的類型，它會評估 hello Runbook 類型 欄位會顯示 hello 的 runbook 類型語法錯誤。  

![匯入 Runbook](media/automation-graphical-authoring-intro/runbook-import-revised20165.png)

### <a name="testing-a-graphical-runbook"></a>測試圖形化 Runbook
離開 hello 發佈版本保持不變，hello runbook，或您可以在已發行前測試新的 runbook 時，您可以在 hello Azure 入口網站中測試 hello 的 runbook 的草稿版本。 這可讓您 tooverify hello runbook，再取代已發行的版本的 hello 正常運作。 當您測試 runbook 時，會執行 hello 草稿 runbook 並完成的它會執行任何動作。 建立工作記錄，但輸出會顯示在 hello 測試輸出窗格。 

開啟 hello runbook 進行編輯，以開啟 runbook 的 hello 測試控制項，然後按一下 hello**測試窗格** 按鈕。

![測試窗格按鈕](media/automation-graphical-authoring-intro/runbook-edit-test-pane.png)

hello 測試控制項將會提示的任何輸入參數，而且您可以按一下 hello 啟動 hello runbook**啟動** 按鈕。

![測試控制項按鈕](media/automation-graphical-authoring-intro/runbook-test-start.png)

### <a name="publishing-a-graphical-runbook"></a>發行圖形化 Runbook
Azure 自動化中的每個 Runbook 有草稿和已發行的版本。 只有 hello 已發佈版本可用 toobe 執行，且 hello 草稿版本可供編輯。 hello 已發佈 」 版本不會受到任何變更 toohello 草稿版本。 準備好 toobe 可用 hello 草稿版本時，您應發佈該使用 hello 草稿版本覆寫 hello 已發佈 」 版本。

您可以藉由開啟 hello runbook 進行編輯，然後再按一下 hello 發佈圖形化 runbook**發行** 按鈕。

![發佈按鈕](media/automation-graphical-authoring-intro/runbook-edit-publish.png)

尚未發行 Runbook 時，它的狀態為 **新增**。  發行時，它的狀態為 **已發行**。  如果已發行，而且 hello 草稿 」 和 「 已發佈的版本不同，您可以編輯 hello runbook、 hello runbook 都有狀態**中編輯**。

![Runbook 狀態](media/automation-graphical-authoring-intro/runbook-statuses-revised20165.png) 

您也可以 hello 選項 toorevert toohello 已發佈 」 版本的 runbook。  這會擲回了自 hello runbook 的上次發佈，並以 hello 已發佈 」 版本取代 hello hello runbook 草稿版本進行任何變更。

![還原 toopublished 按鈕](media/automation-graphical-authoring-intro/runbook-edit-revert-published.png)

## <a name="activities"></a>活動
活動是 runbook 的 hello 建置組塊。  活動可以是 PowerShell Cmdlet、子 Runbook 或工作流程活動。  您以滑鼠右鍵按一下 hello 控制項程式庫中，選取新增的活動 toohello runbook**新增 toocanvas**。  您可以按一下並拖曳到任何地方 hello 畫布您喜歡的 hello 活動 tooplace。  hello 的 hello hello 活動 hello 畫布上的位置不會影響 hello hello runbook 以任何方式作業。  您將版面配置可能您的 runbook，不過您覺得最適合 toovisualize 其作業。 

![新增 toocanvas](media/automation-graphical-authoring-intro/add-to-canvas-revised20165.png)

選取 hello 畫布 tooconfigure hello 活動及其屬性和參數 hello 組態刀鋒視窗中。  您可以變更 hello**標籤**是描述性 tooyou 的 hello 活動 toosomething。  正在執行 hello 原始 cmdlet，您只要變更它將會使用 hello 圖形編輯器的顯示名稱。  hello 標籤內必須是唯一 hello runbook。 

### <a name="parameter-sets"></a>參數集
參數集定義 hello 強制與選用參數，將會接受針對特定 cmdlet 的值。  所有的 Cmdlet 至少有一個參數集，而某些則有多個。  如果 Cmdlet 有多個參數集，然後您必須選取可以設定參數之前，將使用參數集。  您可以設定的 hello 參數將取決於您選擇的 hello 參數集。  您可以變更所選取活動所使用的 hello 參數組**參數設定**並選取 其他設定。  在此情況下，您設定的任何參數值都會遺失。

在下列範例的 hello，hello Get AzureRmVM cmdlet 都有三個參數集。  您無法設定參數值，直到您選取其中一個 hello 參數集。  hello ListVirtualMachineInResourceGroupParamSet 參數集傳回的所有虛擬機器的資源群組中，單一的選擇性參數。  hello GetVirtualMachineInResourceGroupParamSet 適用於指定您想 tooreturn，而且有兩個必要和選擇性參數的 hello 的虛擬機器。

![參數集](media/automation-graphical-authoring-intro/get-azurermvm-parameter-sets.png)

#### <a name="parameter-values"></a>參數值
當您指定參數的值時，您會選取資料來源 toodetermine hello 值指定的方式。  hello 可用於特定參數的資料來源將取決於該參數的 hello 有效值。  例如，Null 不是不允許 null 值的參數可用的選項。

| 資料來源 | 說明 |
|:--- |:--- |
| 常數值 |輸入 hello 參數的值。  這只適用於下列資料類型的 hello: Int32、 Int64、 字串、 Boolean、 DateTime、 交換器。 |
| 活動輸出 |活動前面 hello 工作流程中的 hello 目前活動的輸出。  將列出所有有效的活動。  選取剛才 hello 活動 toouse hello 參數值的輸出。  如果 hello 活動輸出具有多個屬性的物件，然後您可以輸入 hello hello 屬性名稱選取 hello 活動之後。 |
| Runbook 輸入 |選取 runbook 的輸入的參數做為輸入的 toohello 活動參數。 |
| 變數資產 |選取「自動化變數」做為輸入。 |
| 認證資產 |選取「自動化認證」做為輸入。 |
| 憑證資產 |選取「自動化憑證」做為輸入。 |
| 連線資產 |選取「自動化連線」做為輸入。 |
| PowerShell 運算式 |指定簡單 [PowerShell 運算式](#powershell-expressions)。  hello 活動與 hello 結果用於 hello 參數值之前，就會評估 hello 運算式。  您可以使用變數 toorefer toohello 輸出的活動或 runbook 的輸入的參數。 |
| 未設定 |清除先前設定的任何值。 |

#### <a name="optional-additional-parameters"></a>選擇性的其他參數
所有指令程式將會有 hello 選項 tooprovide 其他參數。  這些是 PowerShell 一般參數或其他自訂參數。  您會看到一個文字方塊，您可以在其中使用 PowerShell 語法提供參數。  比方說，toouse hello **Verbose**一般參數，您會指定**"-Verbose: $True"**。

### <a name="retry-activity"></a>重試活動
**重試行**允許執行多次，直到符合特定條件時，活動 toobe 十分類似迴圈。  您可以使用這項功能之活動的應該執行多次，容易發生錯誤，可能需要一個以上的嘗試成功，或測試的有效資料的 hello 活動 hello 輸出資訊。    

當您對活動啟用重試時，您可以設定延遲和條件。  hello 延遲是 hello 時間 （以秒數或分鐘為單位） 該 hello runbook 之前會先等待再次執行 hello 活動。  如果未不指定任何延遲，然後 hello 活動會再次執行此作業完成之後，立即。 

![活動重試延遲](media/automation-graphical-authoring-intro/retry-delay.png)

hello 重試條件是在每個階段 hello 活動執行後會評估的 PowerShell 運算式。  如果 hello 運算式解析 tooTrue，然後 hello 活動會執行一次。  如果 hello 運算式解析 tooFalse 然後 hello 活動不會執行一次，並移 toohello 下一個活動上的 hello runbook。 

![活動重試延遲](media/automation-graphical-authoring-intro/retry-condition.png)

hello 重試條件可以使用名為 $RetryData 提供存取 tooinformation 有關 hello 活動重試。  這個變數具有 hello 下表中的 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| NumberOfAttempts |已執行的 hello 活動的次數。 |
| 輸出 |輸出 hello 從上次執行的 hello 活動。 |
| TotalDuration |逾時 hello 活動已啟動後經過 hello 第一次。 |
| StartedAt |第一次啟動時間以 UTC 格式 hello 活動。 |

以下是活動重試條件的範例。

    # Run hello activity exactly 10 times.
    $RetryData.NumberOfAttempts -ge 10 

    # Run hello activity repeatedly until it produces any output.
    $RetryData.Output.Count -ge 1 

    # Run hello activity repeatedly until 2 minutes has elapsed. 
    $RetryData.TotalDuration.TotalMinutes -ge 2

設定活動的重試條件之後，hello 活動包含兩個視覺提示 tooremind 您。  其中一個會以 hello 活動 hello 其他時，則您檢閱 hello 活動 hello 組態。

![活動重試視覺指示器](media/automation-graphical-authoring-intro/runbook-activity-retry-visual-cue.png)

### <a name="workflow-script-control"></a>工作流程指令碼控制項
程式碼控制項是特殊的活動可接受 PowerShell 或 PowerShell 工作流程指令碼，根據訂單 tooprovide 功能，否則無法使用中正在撰寫圖形化 runbook hello 類型而定。  它不能接受參數，但它可以對活動輸出和 Runbook 輸入參數使用變數。  Hello 活動的任何輸出會加入 toohello databus 除非它有沒有傳出中連結的情況下，它會加入 hello runbook 的 toohello 輸出。

例如 hello 下列程式碼會執行使用名 $NumberOfDays 的 runbook 輸入的變數的日期計算。  接著會做為輸出 toobe hello runbook 中後續活動所使用的傳送計算的日期時間。

    $DateTimeNow = (Get-Date).ToUniversalTime()
    $DateTimeStart = ($DateTimeNow).AddDays(-$NumberOfDays)}
    $DateTimeStart


## <a name="links-and-workflow"></a>連結和工作流程
圖形化 Runbook 中的 **連結** 在連接兩個活動。  它會顯示 hello 畫布上，為箭號指向 hello 來源活動 toohello 目的地活動。  hello 活動中執行，hello hello 箭頭方向與 hello 目的地活動 hello 來源活動完成之後啟動。  

### <a name="create-a-link"></a>建立連結
建立所選取的 hello 來源活動的兩個活動和 hello 圓形之間的連結在 hello hello 圖形的底端。  拖曳 hello 箭號 toohello 目的地活動和版本。

![建立連結](media/automation-graphical-authoring-intro/create-link-revised20165.png)

在 hello 組態刀鋒視窗中選取 hello 連結 tooconfigure 其屬性。  這會將包含下表中的 hello hello 連結類型所述。

| 連結類型 | 說明 |
|:--- |:--- |
| 管線 |hello 目的地活動會執行一次針對每個物件輸出 hello 來源活動。  hello 目的地活動不會執行，如果 hello 來源活動會不產生任何輸出。  Hello 來源活動的輸出可做為物件。 |
| 順序 |hello 目的地活動只執行一次。  在收到 hello 來源活動的物件陣列。  Hello 來源活動的輸出可做為物件的陣列。 |

### <a name="starting-activity"></a>啟動活動
圖形化 Runbook 會從沒有連入連結的任何活動開始。  通常這是一個活動會當做 hello 啟動 hello runbook 的活動。  如果多個活動並沒有連入的連結，然後 hello runbook 一開始會以平行方式執行。  它會依照 hello 連結 toorun 其他活動完成時每個。

### <a name="conditions"></a>條件
當您在連結上指定條件時，如果 hello 條件解析 tootrue 只執行 hello 目的地活動。  您通常會使用 $ActivityOutput 變數 hello 來源活動的條件 tooretrieve hello 輸出中。  

管線連結，您指定單一物件、 條件和 hello 條件會評估每個物件輸出 hello 來源活動。  每個物件符合 hello 條件，接著執行 hello 目的地活動。  比方說，Get AzureRmVm 來源活動，請使用下列語法的 hello 可用於條件式管線連結 tooretrieve 中的虛擬機器 hello 資源群組名稱只*Group1*。  

    $ActivityOutput['Get Azure VMs'].Name -match "Group1"

序列連結 hello 條件只會評估一次因為單一陣列會傳回包含所有的物件輸出 hello 來源活動。  因為這個緣故，序列連結不能用於篩選管線連結類似，但是將只會決定要執行 hello 下一個活動。 採用下列一組活動我們啟動 VM runbook 中的 hello。<br> ![具有順序的條件式連結](media/automation-graphical-authoring-intro/runbook-conditional-links-sequence.png)<br>
有三個要驗證已提供代表 VM 名稱與資源群組名稱中也就是 hello 適當的動作 tootake 順序 toodetermine tootwo runbook 輸入的參數的值-啟動單一 VM 的不同序列連結、 在 hello 中啟動所有的 Vm資源群組或訂用帳戶中的所有 Vm。  Hello 序列連線 tooAzure 和取得單一 VM 之間的連結，以下是 hello 條件邏輯：

    <# 
    Both VMName and ResourceGroupName runbook input parameters have values 
    #>
    (
    (($VMName -ne $null) -and ($VMName.Length -gt 0))
    ) -and (
    (($ResourceGroupName -ne $null) -and ($ResourceGroupName.Length -gt 0))
    )

當您使用條件式連結時，提供 hello 來源活動 tooother 活動在該分支中的 hello 資料將會篩選 hello 條件。  如果活動是 hello 來源 toomultiple 連結，然後 hello 每個分支中的可用 tooactivities 將取決於連接 toothat 分支 hello 連結中的 hello 條件的資料。

例如，hello**開始 AzureRmVm**下方 hello runbook 中的活動開始的所有虛擬機器。  它有兩個條件式連結。  hello 的第一個條件式連結會使用 hello 運算式*$ActivityOutput [' 開始-AzureRmVM']。IsSuccessStatusCode-eq $true* toofilter 如果 hello 開始 AzureRmVm 活動順利完成。  hello 第二個使用 hello 運算式*$ActivityOutput [' 開始-AzureRmVM']。IsSuccessStatusCode ne $true* toofilter 如果 hello 開始 AzureRmVm 活動失敗 toostart hello 虛擬機器。  

![條件式連結範例](media/automation-graphical-authoring-intro/runbook-conditional-links.png)

遵循 hello 第一個連結，並使用 Get-azurevm hello 活動輸出的任何活動，才會出現在 hello Get-azurevm 已執行的時間啟動的 hello 虛擬機器。  遵循 hello 第二個連結的任何活動，才會出現在 hello Get-azurevm 已執行的時間停止的 hello hello 虛擬機器。  Hello 第三個連結的任何活動會取得所有虛擬機器，不論其執行狀態。

### <a name="junctions"></a>接合
接合是一個特殊的活動，將會等候直到所有內送的分支完成。  這可讓您 toorun 平行的多個活動，並確保所有已在繼續之前完成。

雖然接合可以有無限的數量的連入連結，但這些連結只有一個可以是管線。  hello 傳入順序連結數目，不會受到限制。  您仍能繼續使用多個連入管線連結 toocreate hello 連接點，並儲存 hello runbook 中使用，但是執行時，它將會失敗。

下列 hello 範例是 runbook 啟動虛擬機器的一組同時下載修補程式 toobe 套用 toothose 機器時的一部分。  連接是使用的 tooensure hello runbook 會繼續執行之前，會完成這兩個處理程序。

![接合](media/automation-graphical-authoring-intro/runbook-junction.png)

### <a name="cycles"></a>循環
循環時，目的地活動連結回 tooits 來源活動或 tooanother 活動，最後連結回 tooits 來源。  圖形化編寫目前不允許循環。  如果您的 Runbook 有循環，它會適當地儲存，但是它執行時會收到錯誤。

![循環](media/automation-graphical-authoring-intro/runbook-cycle.png)

### <a name="sharing-data-between-activities"></a>在活動之間共用資料
連出連結的活動所輸出的任何資料寫入 toohello *databus* hello runbook。  Hello runbook 中的任何活動可以 hello databus toopopulate 參數值使用的資料，或包含在指令碼中。  活動可以存取任何先前的活動 hello 工作流程中的 hello 的輸出。     

Hello 資料寫入 toohello databus 的方式取決於 hello hello 活動上的連結類型。  如**管線**，hello 資料會輸出為多個物件。  如**順序**連結，hello 資料會輸出為陣列。  如果只有一個值，則會輸出為單一元素陣列。

您可以存取使用兩種方法之一 hello databus 上的資料。  第一次使用**活動輸出**資料來源的 toopopulate 另一個活動的參數。  如果 hello 輸出是物件，您可以指定單一的屬性。

![活動輸出](media/automation-graphical-authoring-intro/activity-output-datasource-revised20165.png)

您也可以擷取的活動中的 hello 輸出**PowerShell 運算式**資料來源或從**工作流程指令碼**ActivityOutput 變數包含的活動。  如果 hello 輸出是物件，您可以指定單一的屬性。  ActivityOutput 變數會使用下列語法的 hello。

    $ActivityOutput['Activity Label']
    $ActivityOutput['Activity Label'].PropertyName 

### <a name="checkpoints"></a>檢查點
您可以在圖形化 PowerShell 工作流程 Runbook 中設定[檢查點](automation-powershell-workflow.md#checkpoints)，方法是在任何活動上選取「檢查點 Runbook」。  這會造成檢查點 toobe hello 活動執行後設定。

![Checkpoint](media/automation-graphical-authoring-intro/set-checkpoint.png)

檢查點只能在圖形化 PowerShell 工作流程 Runbook 中啟用，無法在圖形化 Runbook 中使用。  如果 hello runbook 使用 Azure 指令程式，您應該遵循任何檢查點的活動，具有新增 AzureRMAccount，以防 hello runbook 已暫停，重新啟動從這個檢查點，在不同的背景工作上。 

## <a name="authenticating-tooazure-resources"></a>驗證 tooAzure 資源
Azure 自動化中管理的 Azure 資源的 Runbook 將需要驗證 tooAzure。  hello[執行身分帳戶](automation-offering-get-started.md#creating-an-automation-account)(也參考的 tooas 服務主體) 是 hello 預設方法 tooaccess 自動化 runbook 您訂用帳戶中的 Azure 資源管理員資源。  您可以新增此功能 tooa 圖形化 runbook 加入 hello **AzureRunAsConnection**連線資產，使用 hello PowerShell [Get-automationconnection](https://technet.microsoft.com/library/dn919922%28v=sc.16%29.aspx) cmdlet，並[新增 AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet toohello 畫布。 Hello 下列範例所示。<br>![執行身分驗證活動](media/automation-graphical-authoring-intro/authenticate-run-as-account.png)<br>
hello 取得執行做為連接活動 (也就是 Get-automationconnection)，設定了名為 AzureRunAsConnection 常數值的資料來源。<br>![執行身分連線組態](media/automation-graphical-authoring-intro/authenticate-runas-parameterset.png)<br>
hello 下一個活動，新增-AzureRmAccount hello runbook 中新增 hello 驗證執行身分帳戶使用。<br>
![Add-AzureRmAccount 參數集](media/automation-graphical-authoring-intro/authenticate-conn-to-azure-parameter-set.png)<br>
Hello 參數**APPLICATIONID**， **CERTIFICATETHUMBPRINT**，和**TENANTID**您將需要 toospecify hello 屬性名稱的 hello hello 欄位路徑，因為hello 活動輸出具有多個屬性的物件。  否則，當您執行 hello runbook 時，它將會失敗嘗試 tooauthenticate。  這是您需要在最小的 tooauthenticate hello 與您的 runbook 執行身分帳戶。

toomaintain 回溯相容性的訂閱者建立自動化帳戶使用[Azure AD 使用者帳戶](automation-create-aduser-account.md)toomanage Azure 傳統部署或 Azure 資源管理員資源的 hello tooauthenticate 方法是與 hello Add-azureaccount cmdlet[認證資產](automation-credentials.md)，代表具有存取 toohello Azure 帳戶的 Active Directory 使用者。

您可以加入認證資產 toohello 畫布後面接著 Add-azureaccount 活動來將此功能 tooa 圖形化 runbook。  Add-azureaccount 使用其輸入 hello 認證活動。  Hello 下列範例所示。

![驗證活動](media/automation-graphical-authoring-intro/authentication-activities.png)

您尚未 tooauthenticate 在 hello 開頭 hello runbook 並在每個檢查點之後。  這表示在任何 Checkpoint-Workflow 活動之後加入額外的 Add-AzureAccount 活動。 您不需要新增認證活動，因為您可以使用 hello 相同 

![活動輸出](media/automation-graphical-authoring-intro/authentication-activity-output.png)

## <a name="runbook-input-and-output"></a>Runbook 輸入和輸出
### <a name="runbook-input"></a>Runbook 輸入
如果 hello 目前當做子系啟動 hello runbook 透過 hello Azure 入口網站或從另一個 runbook 時，runbook 可能需要從使用者輸入。
例如，如果您有建立虛擬機器的 runbook，您可能需要 tooprovide 的資訊，例如 hello 名稱 hello 虛擬機器和其他內容每次啟動 hello runbook。  

您透過定義一或多個輸入參數來接受 Runbook 的輸入。  您為每個時間 hello runbook 啟動這些參數提供值。  當您啟動 runbook 以 hello Azure 入口網站時，它會提示您 tooprovide hello 每個 hello runbook 的輸入參數的值。

您可以存取 runbook 的輸入的參數，依序按一下 hello**輸入和輸出**hello runbook 的工具列上的按鈕。  

![Runbook 輸入輸出](media/automation-graphical-authoring-intro/runbook-edit-input-output.png) 

這會開啟 hello**輸入和輸出**控制項，您可以在此編輯現有的輸入的參數，或按一下 建立新**加入輸入**。 

![加入輸入](media/automation-graphical-authoring-intro/runbook-edit-add-input.png)

每個輸入的參數是由 hello 下表中的 hello 屬性所定義。

| 屬性 | 說明 |
|:--- |:--- |
| 名稱 |hello 參數 hello 唯一名稱。  這只能包含數字字元，而且不能包含空格。 |
| 說明 |Hello 輸入參數的選擇性描述。 |
| 類型 |Hello 參數值所預期的資料類型。  時提示輸入 hello Azure 入口網站會針對每個參數提供適當的控制項 hello 資料類型。 |
| 強制 |指定是否必須提供 hello 參數的值。  hello runbook 無法啟動，如果您未提供值的每個必要參數，但是沒有定義了預設值。 |
| 預設值 |指定哪些值用於 hello 參數，如果未提供一個。  這可以是 Null 或特定值。 |

### <a name="runbook-output"></a>Runbook 輸出
連出連結沒有任何活動所建立的資料將會加入 toohello [hello runbook 的輸出](http://msdn.microsoft.com/library/azure/dn879148.aspx)。  hello 輸出儲存與 hello runbook 工作時，則可以使用 tooa 父 runbook hello runbook 可做為子系。  

## <a name="powershell-expressions"></a>PowerShell 運算式
圖形化撰寫 hello 優點之一您提供 hello 能力 toobuild 以 PowerShell 的基本知識的 runbook。  目前，您需要使用 tooknow 的位元的 PowerShell 雖然填入某些[參數值](#activities)和設定[連結條件](#links-and-workflow)。  本章節提供的快速介紹 tooPowerShell 運算式可能不熟悉它的使用者。  PowerShell 的完整詳細資料位於 [使用 Windows PowerShell 撰寫指令碼](http://technet.microsoft.com/library/bb978526.aspx)。 

### <a name="powershell-expression-data-source"></a>PowerShell 運算式資料來源
您可以使用的 PowerShell 運算式做為資料來源 toopopulate hello 值[活動參數](#activities)hello 一些 PowerShell 程式碼的結果。  這可以是執行一些簡單函式的單行程式碼，或執行一些複雜邏輯的多行程式碼。  任何不是命令的輸出指派 tooa 變數是輸出 toohello 參數值。 

例如，下列命令的 hello 就能輸出 hello 目前的日期。 

    Get-Date

hello 下列命令建立的字串 hello 從目前的日期並將它指派 tooa 變數。  hello 變數的 hello 內容便會傳送 toohello 輸出 

    $string = "hello current date is " + (Get-Date)
    $string

hello 下列命令目前的日期評估 hello 並傳回指出是否 hello 當天工作日或週末的字串。 

    $date = Get-Date
    if (($date.DayOfWeek = "Saturday") -or ($date.DayOfWeek = "Sunday")) { "Weekend" }
    else { "Weekday" }


### <a name="activity-output"></a>活動輸出
toouse hello hello runbook，請使用下列語法的 hello 與使用 hello $ActivityOutput 變數中前一項活動的輸出。

    $ActivityOutput['Activity Label'].PropertyName

例如，您可能需要的虛擬機器的 hello 名稱的屬性的活動在此情況下，您可以使用下列運算式 hello。

    $ActivityOutput['Get-AzureVm'].Name

如果需要 hello 虛擬機器物件，而不是只屬性，則您的 hello 屬性則會傳回 hello 整個物件使用 hello 語法。

    $ActivityOutput['Get-AzureVm']

您也可以使用更複雜的運算式，例如 hello 下列會串連文字 toohello 虛擬機器名稱中的 hello 輸出的活動。

    "hello computer name is " + $ActivityOutput['Get-AzureVm'].Name


### <a name="conditions"></a>條件
使用[比較運算子](https://technet.microsoft.com/library/hh847759.aspx)toocompare 值，或判斷值是否符合指定的模式。  比較會傳回 $true 或 $false 的值。

例如，下列條件的 hello 決定是否 hello 虛擬機器活動的名稱*Get-azurevm*目前*停止*。 

    $ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped"

hello 以下條件會檢查是否 hello 相同的虛擬機器處於任何狀態以外*停止*。

    $ActivityOutput["Get-AzureVM"].PowerState –ne "Stopped"

您可以使用[邏輯運算子](https://technet.microsoft.com/library/hh847789.aspx) (例如 **-and** 或 **-or**) 加入多個條件。  例如，hello 下列條件檢查是否 hello hello 前一個範例中的相同虛擬機器的狀態*停止*或*停止*。

    ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopped") -or ($ActivityOutput["Get-AzureVM"].PowerState –eq "Stopping") 


### <a name="hashtables"></a>雜湊表
[雜湊表](http://technet.microsoft.com/library/hh847780.aspx) 是傳回一組值時很有用的名稱/值組。  某些活動的屬性可能是雜湊表而不是簡單值。  您可能也會看到如雜湊表稱為 tooas 字典。 

您可以建立雜湊表以 hello，請使用下列語法。  雜湊表可以包含任意數目的項目，但是每個項目都由一個名稱和值定義。

    @{ <name> = <value>; [<name> = <value> ] ...}

例如，hello 下列運算式會建立雜湊表 toobe hello 資料來源中用於預期雜湊表值的網際網路搜尋活動參數。

    $query = "Azure Automation"
    $count = 10
    $h = @{'q'=$query; 'lr'='lang_ja';  'count'=$Count}
    $h

hello 下列範例會使用呼叫活動的輸出*取得 Twitter 連接*toopopulate 雜湊表。

    @{'ApiKey'=$ActivityOutput['Get Twitter Connection'].ConsumerAPIKey;
      'ApiSecret'=$ActivityOutput['Get Twitter Connection'].ConsumerAPISecret;
      'AccessToken'=$ActivityOutput['Get Twitter Connection'].AccessToken;
      'AccessTokenSecret'=$ActivityOutput['Get Twitter Connection'].AccessTokenSecret}



## <a name="next-steps"></a>後續步驟
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md) 
* tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)
* tooknow 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)
* toounderstand 如何使用 tooauthenticate hello 自動化執行身分帳戶，請參閱[設定 Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)

