---
title: "aaaStart/停止 Vm，在離峰時間 [預覽] 方案 |Microsoft 文件"
description: "hello VM 管理解決方案啟動和停止您的 Azure 資源管理員虛擬機器上排程並主動從記錄分析監視。"
services: automation
documentationCenter: 
authors: mgoedtel
manager: carmonm
editor: 
ms.assetid: 06c27f72-ac4c-4923-90a6-21f46db21883
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: magoedte
ms.openlocfilehash: 6cbe16dfb40bf13f29d9e58ca0bc8c5c7979879d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="startstop-vms-during-off-hours-preview-solution-in-automation"></a>自動化中的在離峰期間啟動/停止 VM [預覽] 方案

在離峰時間 [預覽] 方案 hello 啟動/停止 Vm 啟動和停止您的 Azure 資源管理員虛擬機器上的使用者定義的排程，並提供深入了解的開始和停止您的虛擬機器與 OMS 的 hello 自動化工作的 hello 成功記錄分析。  

## <a name="prerequisites"></a>必要條件

- hello runbook 使用[Azure 執行身分帳戶](automation-offering-get-started.md#authentication-methods)。  hello 執行身分帳戶是 hello 慣用的驗證方法，因為它會使用憑證驗證，而不使用密碼，可能會過期或經常變更。  

- 此解決方案只能管理 Vm 處於 hello 相同訂用帳戶所在 hello 自動化帳戶。  

- 這個解決方案只會部署下列 Azure 區域-澳洲東南部、 美國東部、 東南亞和西歐 toohello。  管理 hello VM 排程的 hello runbook 可鎖定目標的任何區域中的 Vm。  

- toosend 電子郵件通知 hello 啟動和停止 VM runbook 完成時，Office 365 商務級訂用帳戶是必要的。  

## <a name="solution-components"></a>方案元件

這個解決方案包含下列資源，將匯入及新增 tooyour 自動化帳戶的 hello。

### <a name="runbooks"></a>Runbook

Runbook | 說明|
--------|------------|
CleanSolution-MS-Mgmt-VM | 當您從您的訂用帳戶移 toodelete hello 方案，此 runbook 將移除包含的所有資源及排程。|  
SendMailO365-MS-Mgmt | 此 Runbook 會透過 Office 365 Exchange 傳送電子郵件。|
StartByResourceGroup-MS-Mgmt-VM | 此 runbook 會預期的 toostart Vm (這兩種傳統和 ARM Vm)，位於指定的 Azure 資源群組清單。
StopByResourceGroup-MS-Mgmt-VM | 此 runbook 會預期的 toostop Vm (這兩種傳統和 ARM Vm)，位於指定的 Azure 資源群組清單。|
<br>

### <a name="variables"></a>變數

變數 | 說明|
---------|------------|
**SendMailO365-MS-Mgmt** Runbook ||
SendMailO365-IsSendEmail-MS-Mgmt | 指定 StartByResourceGroup-MS-Mgmt-VM 和 StopByResourceGroup-MS-Mgmt-VM Runbook 是否可以在完成時傳送電子郵件通知。  選取**True** tooenable 和**False** toodisable 電子郵件警示。 預設值為 [False]。| 
**StartByResourceGroup-MS-Mgmt-VM** Runbook ||
StartByResourceGroup-ExcludeList-MS-Mgmt-VM | 請輸入 VM 名稱 toobe 排除管理作業。使用不含空格的 semi-colon(;) 分隔名稱。 值會區分大小寫並支援萬用字元 (星號)。|
StartByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | 文字可以附加 toohello hello 電子郵件訊息本文開頭。|
StartByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | 指定 hello hello 包含 hello 電子郵件 runbook 的自動化帳戶名稱。  **請勿修改此變數。**|
StartByResourceGroup-SendMailO365-EmailRunbookName-MS-Mgmt | 指定 hello hello 電子郵件的 runbook 名稱。  這會使用 hello StartByResourceGroup MS-Mgmt VM 和 StopByResourceGroup MS-Mgmt VM runbook toosend 電子郵件。  **請勿修改此變數。**|
StartByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | 指定 hello hello 資源群組含有 hello 電子郵件的 runbook 名稱。  **請勿修改此變數。**|
StartByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | 指定 hello hello 電子郵件的主旨列的 hello 文字。|  
StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | 指定 hello hello 電子郵件的收件者。  使用不含空格的分號 (;) 輸入不同的名稱。|
StartByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | 請輸入 VM 名稱 toobe 排除管理作業。使用不含空格的 semi-colon(;) 分隔名稱。 值會區分大小寫並支援萬用字元 (星號)。  預設值 （星號） 會將包含 hello 訂用帳戶所有資源群組。|
StartByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | 指定包含此解決方案所管理的 Vm toobe hello 訂用帳戶。  這必須是 hello hello 此解決方案的自動化帳戶所在的相同訂用帳戶。|
**StopByResourceGroup-MS-Mgmt-VM** Runbook ||
StopByResourceGroup-ExcludeList-MS-Mgmt-VM | 請輸入 VM 名稱 toobe 排除管理作業。使用不含空格的 semi-colon(;) 分隔名稱。 值會區分大小寫並支援萬用字元 (星號)。|
StopByResourceGroup-SendMailO365-EmailBodyPreFix-MS-Mgmt | 文字可以附加 toohello hello 電子郵件訊息本文開頭。|
StopByResourceGroup-SendMailO365-EmailRunBookAccount-MS-Mgmt | 指定 hello hello 包含 hello 電子郵件 runbook 的自動化帳戶名稱。  **請勿修改此變數。**|
StopByResourceGroup-SendMailO365-EmailRunbookResourceGroup-MS-Mgmt | 指定 hello hello 資源群組含有 hello 電子郵件的 runbook 名稱。  **請勿修改此變數。**|
StopByResourceGroup-SendMailO365-EmailSubject-MS-Mgmt | 指定 hello hello 電子郵件的主旨列的 hello 文字。|  
StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt | 指定 hello hello 電子郵件的收件者。  使用不含空格的分號 (;) 輸入不同的名稱。|
StopByResourceGroup-TargetResourceGroups-MS-Mgmt-VM | 請輸入 VM 名稱 toobe 排除管理作業。使用不含空格的 semi-colon(;) 分隔名稱。 值會區分大小寫並支援萬用字元 (星號)。  預設值 （星號） 會將包含 hello 訂用帳戶所有資源群組。|
StopByResourceGroup-TargetSubscriptionID-MS-Mgmt-VM | 指定包含此解決方案所管理的 Vm toobe hello 訂用帳戶。  這必須是 hello hello 此解決方案的自動化帳戶所在的相同訂用帳戶。|  
<br>

### <a name="schedules"></a>排程

排程 | 說明|
---------|------------|
StartByResourceGroup-Schedule-MS-Mgmt | StartByResourceGroup runbook，以便執行此解決方案所管理的 Vm hello 啟動的排程。 建立時，它會預設 tooUTC 時區。|
StopByResourceGroup-Schedule-MS-Mgmt | StopByResourceGroup runbook，以便執行此解決方案所管理的 Vm 的 hello 關閉的排程。 建立時，它會預設 tooUTC 時區。|

### <a name="credentials"></a>認證

認證 | 說明|
-----------|------------|
O365Credential | 指定有效 Office 365 使用者帳戶 toosend 的電子郵件。  如果變數 SendMailO365-IsSendEmail-MS-Mgmt 過設定，才需要**True**。

## <a name="configuration"></a>組態

執行下列步驟 tooadd hello 啟動/停止 Vm，在離峰時間 [預覽] 方案 tooyour 自動化帳戶期間的 hello，然後設定 [hello 變數 toocustomize hello 方案。

1. 從 hello 首頁螢幕 hello Azure 入口網站中，選取 hello **Marketplace**磚。  如果 hello 磚不再是已釘選的 tooyour 首頁-畫面上，從 hello 左側瀏覽窗格中，選取 **新增**。  
2. 在 hello Marketplace 刀鋒視窗中，輸入**啟動 VM** hello 搜尋方塊，然後選取 hello 方案中**啟動/停止 Vm，在離峰時間 [預覽]** hello 搜尋結果中。  
3. 在 hello**啟動/停止 Vm，在離峰時間 [預覽]** hello 刀鋒視窗中選取方案，檢閱 hello 摘要資訊，然後按一下**建立**。  
4. hello**將方案加入**刀鋒視窗會顯示您可以將它匯入自動化訂用帳戶之前，會提示的 tooconfigure hello 方案。<br><br> ![VM 管理的新增方案刀鋒視窗](media/automation-solution-vm-management/vm-management-solution-add-solution-blade.png)<br><br>
5.  在 hello**將方案加入**刀鋒視窗中，選取**工作區**和您在這裡選取 OMS 工作區所連結的 toohello hello 自動化帳戶的同一個 Azure 訂閱時，或建立新的 OMS 工作區。  如果您沒有 OMS 工作區，您可以選取**建立新的工作區**在 hello **OMS 工作區**刀鋒視窗中執行下列 hello: 
   - 指定的名稱 hello 新**OMS 工作區**。
   - 選取**訂用帳戶**toolink tooby 從清單中選取 hello 下拉式清單選取 hello 預設值是否不適當。
   - 對於 [資源群組]，您可以建立新的資源群組，或選取現有的資源群組。  
   - 選取 [位置] 。  提供讓您選取的 hello 唯一位置就是目前**澳洲東南部**，**美國東部**，**東南亞**，和**西歐**。
   - 選取 **定價層**。  hello 方案提供兩個層級： 釋放，OMS 付費層。  hello 免費層的資料收集的每日保留週期及 runbook 工作執行階段的分鐘數的 hello 數量的上限。  hello OMS 付費層上 hello 每日收集的資料量沒有限制。  

        > [!NOTE]
        > 雖然 hello 獨立付費層會顯示為一個選項，並不適用。  如果您選取它，並繼續您訂用帳戶中的 hello 建立此解決方案，它將會失敗。  當此解決方案正式發行時，將會解決這個問題。<br>如果您使用此解決方案，則它只會使用自動化工作分鐘數並記錄擷取。  hello 解決方案不會新增其他 OMS 節點 tooyour 環境。  

6. 提供所需的 hello 資訊在 hello 之後**OMS 工作區**刀鋒視窗中，按一下 **建立**。  在驗證 hello 資訊並建立 hello 工作區時，您可以追蹤在其進度**通知**hello 功能表。  您將會傳回 toohello**將方案加入**刀鋒視窗。  
7. 在 hello**將方案加入**刀鋒視窗中，選取**自動化帳戶**。  如果您要建立新的 OMS 工作區，您必須 tooalso 建立新的自動化帳戶，將會與 hello 新 OMS 工作區之前，指定包含您的 Azure 訂用帳戶、 資源群組與區域產生關聯。  您可以選取**建立自動化帳戶**在 hello**加入自動化帳戶**刀鋒視窗中，提供下列 hello: 
  - 在 hello**名稱**欄位中，輸入 hello hello 自動化帳戶名稱。

    所有其他選項會自動填入根據選取的 hello OMS 工作區，不能修改這些選項。  Azure 執行身分帳戶是包含在此解決方案中的 hello runbook hello 預設驗證方法。  一旦您按一下**確定**、 hello 組態選項會進行驗證，並建立 hello 自動化帳戶。  您可以追蹤其進度下的**通知**hello 功能表。 

    不然，您可以選取現有的自動化執行身分帳戶。  請注意，您所選取的 hello 帳戶不能連結的 tooanother OMS 工作區，否則訊息將會出現在 [hello] 刀鋒視窗 tooinform 您。  如果已經連結，您將需要 tooselect 不同的自動化執行身分帳戶，或另外新建一個。<br><br> ![自動化帳戶已連結 tooOMS 工作區](media/automation-solution-vm-management/vm-management-solution-add-solution-blade-autoacct-warning.png)<br>

8. 最後在 hello**將方案加入**刀鋒視窗中，選取**組態**和 hello**參數**刀鋒視窗隨即出現。  在 hello**參數**刀鋒視窗中，系統會提示您：  
   - 指定 hello**目標資源群組名稱**，這是包含此解決方案所管理的 Vm toobe 資源群組名稱。  您可以輸入多個名稱，然後使用分號加以分隔 (這些值需區分大小寫)。  如果您想 tootarget Vm hello 訂用帳戶中的所有資源群組中，會支援使用萬用字元。
   - 選取**排程**這是週期性的日期和時間啟動和停止 hello hello 中 VM 的目標資源群組。  根據預設，hello 的排程都會設定的 toohello UTC 時區為準，並不提供選取不同的區域。  如果您想 tooconfigure hello 排程 tooyour 特定時區設定 hello 方案之後，請參閱[修改 hello 啟動和關閉排程](#modifying-the-startup-and-shutdown-schedule)下方。    

10. 當您完成設定 hello 解決方案所需的 hello 初始設定時，選取**建立**。  會驗證所有設定，然後它會嘗試 toodeploy hello 方案，您的訂用帳戶中。  此程序可能需要幾秒 toocomplete，而且您可以追蹤在其進度**通知**hello 功能表。 

## <a name="collection-frequency"></a>收集頻率

Automation 作業記錄檔和工作資料流資料會內嵌到 hello OMS 儲存機制每隔五分鐘。  

## <a name="using-hello-solution"></a>使用 hello 解決方案

當您新增 hello VM 管理解決方案，在您的 OMS 工作區 hello **StartStopVM 檢視**磚加入 tooyour OMS 儀表板。  這個磚會顯示計數和 hello runbook 工作 hello 解決方案已啟動並成功完成的圖形表示。<br><br> ![VM 管理 StartStopVM 檢視圖格](media/automation-solution-vm-management/vm-management-solution-startstopvm-view-tile.png)  

在您的自動化帳戶可以存取並管理 hello 解決方案選取 hello**解決方案**磚，然後從 hello**解決方案**刀鋒視窗中，選取 hello 方案**開始停止 VM [工作區]**從 hello 清單。<br><br> ![自動化方案清單](media/automation-solution-vm-management/vm-management-solution-autoaccount-solution-list.png)  

選取 hello 方案將會顯示 hello**開始停止 VM [工作區]**方案刀鋒視窗中，您可以在其中檢閱重要的詳細資料，例如 hello **StartStopVM**磚，例如您的 OMS 工作區中的顯示的計數和 hello runbook 工作 hello 解決方案已啟動並成功完成的圖形表示。<br><br> ![自動化 VM 方案刀鋒視窗](media/automation-solution-vm-management/vm-management-solution-solution-blade.png)  

從這裡您也可以開啟 OMS 工作區，並進行進一步分析的 hello 工作記錄。  只要按一下**所有設定**，並在 hello**設定**刀鋒視窗中，選取**快速入門**，然後在 hello**快速入門**刀鋒視窗選取**OMS 入口網站**。   這樣會開啟新的索引標籤或新的瀏覽器工作階段，並顯示與您的自動化帳戶和訂用帳戶相關聯的 OMS 工作區。  


### <a name="configuring-e-mail-notifications"></a>設定電子郵件通知

tooenable 電子郵件通知時 hello 啟動和停止 VM runbook 完成，您就需要 toomodify hello **O365Credential**認證和最少 hello 下列變數：

 - SendMailO365-IsSendEmail-MS-Mgmt
 - StartByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt
 - StopByResourceGroup-SendMailO365-EmailToAddress-MS-Mgmt

tooconfigure hello **O365Credential**認證，執行下列步驟的 hello:

1. 從您的自動化帳戶，按一下 **所有設定**hello hello 視窗上方。 
2. 在 hello**設定**刀鋒視窗中的 hello 區段下**自動化資源**，選取**資產**。 
3. 在 hello**資產**刀鋒視窗中，選取 hello**認證**磚與 hello**認證**刀鋒視窗中，選取 hello **O365Credential**。  
4. 輸入有效的 Office 365 使用者名稱和密碼，然後按一下**儲存**toosave 您的變更。  

tooconfigure hello 變數反白顯示較舊版本，執行下列步驟的 hello:

1. 從您的自動化帳戶，按一下 **所有設定**hello hello 視窗上方。 
2. 在 hello**設定**刀鋒視窗中的 hello 區段下**自動化資源**，選取**資產**。 
3. 在 hello**資產**刀鋒視窗中，選取 hello**變數**磚與 hello**變數**刀鋒視窗中，選取上面所列的 hello 變數，然後修改下列 hello 其值描述為其指定在 hello[變數](##variables)前面一節。  
4. 按一下**儲存**toosave hello 變更 toohello 變數。   

### <a name="modifying-hello-startup-and-shutdown-schedule"></a>修改 hello 啟動和關閉排程

管理此解決方案中的 hello 啟動和關閉排程會遵循相同步驟中所述的 hello[排程在 Azure 自動化 runbook](automation-schedules.md)。  請記住，您無法修改 hello 排程設定。  您將需要 toodisable hello 現有的排程，然後建立一個新，然後連結 toohello **StartByResourceGroup MS-Mgmt VM**或**StopByResourceGroup MS-Mgmt VM** runbook 的 hello排程要 tooapply。   

## <a name="log-analytics-records"></a>Log Analytics 記錄

自動化 hello OMS 儲存機制中建立兩種類型的記錄。

### <a name="job-logs"></a>作業記錄檔

屬性 | 說明|
----------|----------|
呼叫者 |  誰 hello 作業。  可能的值為電子郵件地址或排程作業的系統。|
類別 | Hello 的資料類型的分類。  自動化，hello 值為 JobLogs。|
CorrelationId | 為 hello 相互關聯識別碼 hello runbook 工作的 GUID。|
JobId | 為 hello 識別碼 hello runbook 工作的 GUID。|
operationName | 指定在 Azure 中執行作業的 hello 型別。  自動化，hello 值會是工作。|
resourceId | 指定在 Azure 中的 hello 資源類型。  自動化，hello 值為 hello 與 hello runbook 相關聯的自動化帳戶。|
ResourceGroup | 指定 hello runbook 工作的 hello 資源群組的名稱。|
ResourceProvider | 指定 hello 提供 hello 資源，您可以部署和管理的 Azure 服務。  自動化，hello 值會是 Azure 自動化。|
ResourceType | 指定在 Azure 中的 hello 資源類型。  自動化，hello 值為 hello 與 hello runbook 相關聯的自動化帳戶。|
resultType | hello hello runbook 工作的狀態。  可能的值包括：<br>- Started (已啟動)<br>- Stopped (已停止)<br>- Suspended (暫止)<br>- Failed (失敗)<br>- Succeeded|
resultDescription | 描述 hello runbook 工作的結果狀態。  可能的值包括：<br>- Job is started (工作已啟動)<br>- Job Failed (工作失敗)<br>- Job Completed|
RunbookName | 指定 hello hello runbook 名稱。|
SourceSystem | 指定 hello 資料送出 hello 來源系統。  自動化，hello 值將會是： OpsManager|
StreamType | 指定事件 hello 型別。 可能的值包括：<br>- Verbose<br>- Output<br>- Error<br>- Warning|
SubscriptionId | 指定 hello 作業 hello 訂用帳戶識別碼。
時間 | 日期和時間 hello runbook 工作執行時。|


### <a name="job-streams"></a>作業串流

屬性 | 說明|
----------|----------|
呼叫者 |  誰 hello 作業。  可能的值為電子郵件地址或排程作業的系統。|
類別 | Hello 的資料類型的分類。  自動化，hello 值為 JobStreams。|
JobId | 為 hello 識別碼 hello runbook 工作的 GUID。|
operationName | 指定在 Azure 中執行作業的 hello 型別。  自動化，hello 值會是工作。|
ResourceGroup | 指定 hello runbook 工作的 hello 資源群組的名稱。|
resourceId | 指定在 Azure 中的 hello 資源識別碼。  自動化，hello 值為 hello 與 hello runbook 相關聯的自動化帳戶。|
ResourceProvider | 指定 hello 提供 hello 資源，您可以部署和管理的 Azure 服務。  自動化，hello 值會是 Azure 自動化。|
ResourceType | 指定在 Azure 中的 hello 資源類型。  自動化，hello 值為 hello 與 hello runbook 相關聯的自動化帳戶。|
resultType | 產生 hello 在 hello 時間 hello 事件 hello runbook 工作的結果。  可能的值包括：<br>- InProgres|
resultDescription | 包含從 hello runbook hello 輸出資料流。|
RunbookName | hello hello runbook 名稱。|
SourceSystem | 指定 hello 資料送出 hello 來源系統。  自動化，hello 值將會是 OpsManager|
StreamType | hello 工作資料流類型。 可能的值包括：<br>-Progress (進度)<br>- Output (輸出)<br>- Warning (警告)<br>- Error (錯誤)<br>- Debug (偵錯)<br>- Verbose|
時間 | 日期和時間 hello runbook 工作執行時。|

當您執行會傳回記錄的類別目錄的任何記錄搜尋**JobLogs**或**JobStreams**，您可以選取 hello **JobLogs**或**JobStreams**檢視可顯示一組圖格 hello hello 搜尋所傳回的更新彙總。

## <a name="sample-log-searches"></a>記錄檔搜尋範例

hello 下表提供此解決方案所收集的作業記錄的範例記錄搜尋。 

查詢 | 說明|
----------|----------|
尋找已順利完成的 Runbook StartVM 作業 | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Succeeded &#124; measure count() by JobId_g|
尋找已順利完成的 Runbook StopVM 作業 | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" ResultType=Failed &#124; measure count() by JobId_g
顯示 StartVM 和 StopVM Runbook 不同時間的作業狀態 | Category=JobLogs RunbookName_s="StartByResourceGroup-MS-Mgmt-VM" OR "StopByResourceGroup-MS-Mgmt-VM" NOT(ResultType="started") | measure Count() by ResultType interval 1day|

## <a name="removing-hello-solution"></a>移除 hello 解決方案

如果您決定您不再需要 toouse hello 方案任何進一步的您可以將它刪除 hello 自動化帳戶。  刪除 hello 方案只會移除 hello runbook、 hello 排程或加入 hello 方案時所建立的變數，將不會刪除它。  這些資產您將需要 toodelete 手動如果您不使用它們與其他 runbook。  

toodelete hello 方案，請執行下列步驟的 hello:

1.  從您的自動化帳戶中，選取 hello**解決方案**磚。  
2.  在 hello**解決方案**刀鋒視窗中，選取 hello 方案**開始停止 VM [工作區]**。  在 hello **VMManagementSolution [工作區]**刀鋒視窗中的，從 hello 功能表上，按一下**刪除**。<br><br> ![刪除 VM 管理解決方案](media/automation-solution-vm-management/vm-management-solution-delete.png)
3.  在 hello**刪除方案**視窗中，確認您想要 toodelete hello 解決方案。
4.  在驗證 hello 資訊並刪除 hello 方案時，您可以追蹤在其進度**通知**hello 功能表。  您將會傳回 toohello **VMManagementSolution [工作區]** hello 程序 tooremove 解決方案開始之後的刀鋒視窗。  

hello 自動化帳戶與 OMS 工作區不會刪除此程序的一部分。  如果您不想 tooretain hello OMS 工作區，您必須 toomanually 刪除它。  這都可以從 hello Azure 入口網站也完成。   從 hello 首頁螢幕 hello Azure 入口網站中，選取**記錄分析**然後在 hello**記錄分析**刀鋒視窗中，選取 hello 工作區中，按一下**刪除**hello 的功能表hello 工作區設定 刀鋒視窗。  
      
## <a name="next-steps"></a>後續步驟

- toolearn 深入了解 tooconstruct 不同的搜尋查詢和檢閱 hello 自動化作業記錄檔記錄分析，請參閱[中記錄分析記錄搜尋](../log-analytics/log-analytics-log-searches.md)
- 深入了解 runbook 執行時，如何 toomonitor runbook 作業和其他技術的詳細資訊，請參閱 toolearn[追蹤 runbook 工作](automation-runbook-execution.md)
- toolearn 深入了解 OMS 記錄分析和資料集合來源，請參閱[收集 Azure 儲存體中的資料記錄分析概觀](../log-analytics/log-analytics-azure-storage.md)






   

