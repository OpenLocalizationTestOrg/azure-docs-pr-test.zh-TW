---
title: "aaaMonitor 及管理在資料管線-Azure |Microsoft 文件"
description: "了解 toouse hello 監視和管理應用程式 toomonitor 和管理 Azure data factory 管線和管線的方式。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>監視和管理 Azure Data Factory 管線使用 hello 監視和管理應用程式
> [!div class="op_single_selector"]
> * [使用 Azure 入口網站/Azure PowerShell](data-factory-monitor-manage-pipelines.md)
> * [使用監視及管理應用程式](data-factory-monitor-manage-app.md)
>
>

本文說明 toouse hello 監視和管理應用程式 toomonitor、 管理和偵錯您的 Data Factory 管線的方式。 它也提供 toocreate 發出 tooget 在失敗時收到通知的警示資訊。 您可以開始使用 hello 應用程式所遵循的看 hello 視訊：

> [!NOTE]
> hello 使用者介面顯示 hello 視訊可能不完全與 hello 入口網站中看到的內容。 舊一點，但概念還是維持不 hello 相同。 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>啟動 hello 監視和管理應用程式
toolaunch hello 監視和管理應用程式中，按一下 hello**監視和管理**磚 hello **Data Factory** data factory 的刀鋒視窗。

![監視在 hello Data Factory 首頁上的磚](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

您應該會看到 hello 監視和管理應用程式在個別視窗中開啟。  

![監視及管理應用程式](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> 如果您看到該 hello 網頁瀏覽器卡在 授權，清除 hello**封鎖第三方 cookie 和站台資料**- 核取方塊或保留選取它，建立的例外狀況**login.microsoftonline.com**然後再試一次 tooopen hello 應用程式。


Hello 中間窗格中的 hello 活動視窗清單，您會看到每次執行活動的活動視窗。 例如，如果您的 hello 活動排程 toorun 每小時 5 小時以上，您會看到五個資料配量與相關聯的五個活動視窗。 如果您沒有看到活動 windows hello hello 底部的清單中，請勿 hello 遵循：
 
- 更新 hello**開始時間**和**結束時間**篩選在 hello 頂端 toomatch hello 開始和結束時間的管線，，然後按一下hello**套用** 按鈕。  
- hello 活動視窗清單不會自動重新整理。 按一下 hello**重新整理**hello hello 工具列上的按鈕**活動 Windows**清單。  

如果您沒有 Data Factory 的應用程式 tootest 這些步驟，請勿 hello 教學課程：[從 Blob 儲存體 tooSQL 資料庫使用 Data Factory 複製資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。

## <a name="understand-hello-monitoring-and-management-app"></a>了解 hello 監視和管理應用程式
有三個索引標籤左側 hello:**資源總管**，**監視檢視**，和**警示**。 hello 第一個索引標籤 (**資源總管**) 預設會選取。

### <a name="resource-explorer"></a>資源總管
您會看到下列 hello:

* 資源總管 hello**樹狀檢視**hello 左窗格中。
* hello**圖表檢視**在 hello 中間窗格中的 hello 最上方。
* hello**活動 Windows**在 hello 中間窗格中的 hello 下方的清單。
* hello**屬性**，**活動視窗總管**，和**指令碼**hello 右窗格中的索引標籤。

在資源總管 中，您會看到 hello data factory 中的樹狀檢視中的所有資源 （管線、 資料集、 連結的服務）。 當您在 [資源總管] 中選取物件時：

* hello 相關聯的實體會反白顯示 hello 圖表檢視中的 Data Factory。
* [相關聯活動 windows](data-factory-scheduling-and-execution.md) hello 活動視窗底部 hello 清單中反白顯示。  
* hello 右窗格中，hello hello 所選物件的屬性會顯示 hello 屬性 視窗中。
* 顯示 hello hello 所選取物件的 JSON 定義時，如果適用的話。 例如︰連結的服務、資料集或管線。

![資源總管](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

請參閱 hello[排程與執行](data-factory-scheduling-and-execution.md)文件以取得詳細的概念性資訊，關於活動視窗。

### <a name="diagram-view"></a>圖表檢視
hello data factory 的圖表檢視會提供單一的半透明 toomonitor 窗格，以及管理 data factory 和及其資產。 當您在 hello 圖表檢視中選取的 Data Factory 實體 （資料集/管線）：

* hello 資料 factory 實體 hello 樹狀結構檢視中選取。
* hello 相關聯的 windows hello 活動視窗 清單中反白顯示的活動。
* hello hello 所選物件的屬性會顯示 hello 屬性 視窗中。

Hello 管線 （不在暫停狀態） 啟用時，它會顯示綠色列：

![管線執行中](./media/data-factory-monitor-manage-app/PipelineRunning.png)

您可以暫停、 繼續或終止 hello 圖表檢視中選取它，並使用 hello 按鈕 hello 命令列上的管線。

![暫停/繼續 hello 命令列上](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
有三個命令 列按鈕的 hello 圖表檢視中的 hello 管線。 您可以使用 hello 第二個按鈕 toopause hello 管線。 暫停不會終止 hello 目前正在執行的活動，並讓他們繼續 toocompletion。 hello 第三個按鈕暫停 hello 管線，並終止其現有的執行活動。 hello 第一個按鈕繼續 hello 管線。 當您的管線已暫停，hello hello 管線變更色彩。 例如，暫停的管線看起來像在下列映像的 hello: 

![管線已暫停](./media/data-factory-monitor-manage-app/PipelinePaused.png)

您可以複選的兩個或多個管線使用 hello Ctrl 鍵。 您可以使用 hello 命令列按鈕 toopause/繼續多個管線，一次。

您也可以以滑鼠右鍵按一下管線並選取選項 toosuspend 繼續或終止管線。 

![管線的內容功能表](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

按一下 hello**開啟管線**選項 toosee hello 管線中的所有 hello 活動。 

![開啟管線功能表](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

在開啟的 hello 管線檢視中，您會看到 hello 管線中的所有活動。 在這個範例中只有一個活動：複製活動。 

![已開啟的管線](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo 回 toohello 前一個檢視中，按一下 hello hello 上方的階層連結功能表中的 hello data factory 名稱。

在 hello 管線檢視中，當您選取的輸出資料集，或當您將滑鼠移 hello 輸出資料集，您會看到該資料集的 hello 活動 Windows 快顯視窗。

![活動時段快顯視窗](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

您可以按一下活動視窗 toosee 詳細資料，hello**屬性**hello 右窗格中的視窗。

![活動時段屬性](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

Hello 右窗格中，切換 toohello**活動視窗總管**索引標籤上的 toosee 更多詳細資料。

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

另請參閱**解析變數**每次執行的嘗試在 hello 活動**嘗試**> 一節。

![解析的變數](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

切換 toohello**指令碼**toosee hello JSON 指令碼定義 hello 所選物件的索引標籤上。   

![指令碼索引標籤](./media/data-factory-monitor-manage-app/ScriptTab.png)

您可以在三個地方看到活動時段：

* hello 活動 Windows hello 圖表檢視 （中間窗格） 中的快顯。
* hello 右窗格中的 hello 活動 Windows 檔案總管。
* hello 活動 Windows hello 下方窗格中的清單。

在 hello 活動 Windows 快顯視窗和活動 Windows 檔案總管 中，您可以捲動 toohello 前一週和 hello 使用下一週 hello 左邊和右邊的箭號。

![活動時段總管的向左/向右箭號](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

在 hello hello 圖表檢視底部，您會看到這些按鈕： 放大、 縮小、 縮放 tooFit 縮放 100%，而鎖定配置。 hello**鎖定配置**按鈕會讓您不小心移動了資料表和管線 hello 圖表檢視中。 此按鈕預設為開啟。 您可以將它關閉，並在 hello 圖表中四處移動實體。 當您將它關閉時，您可以使用 hello 最後一個按鈕 tooautomatically 位置資料表和管線。 您也可以使用 hello 滑鼠滾輪，放大或縮小。

![圖表檢視縮放命令](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>活動時段清單
在 hello hello 中間窗格底部的 hello 活動視窗清單會顯示您選取 hello 資源總管或 hello 圖表檢視中的 hello 資料集的所有活動視窗。 根據預設，hello 清單是依遞減順序表示，您會看見 hello 最新活動視窗頂端 hello。

![活動時段清單](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

這份清單不會自動重新整理，因此 hello 工具列 toomanually 上的使用 hello 重新整理按鈕重新整理。  

活動視窗可以是其中一種 hello 下列狀態：

<table>
<tr>
    <th align="left">狀態</th><th align="left">子狀態</th><th align="left">說明</th>
</tr>
<tr>
    <td rowspan="8">等候</td><td>ScheduleTime</td><td>hello 時間未針對 hello 活動視窗 toorun 發生。</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>hello 上游相依性未準備好。</td>
</tr>
<tr>
<td>ComputeResources</td><td>hello 計算資源無法使用。</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>所有的 hello 活動執行個體都忙於執行其他活動視窗。</td>
</tr>
<tr>
<td>ActivityResume</td><td>hello 活動已暫停，直到它繼續時，無法執行 hello 活動視窗。</td>
</tr>
<tr>
<td>Retry</td><td>正在重試 hello 活動執行。</td>
</tr>
<tr>
<td>驗證</td><td>驗證尚未啟動。</td>
</tr>
<tr>
<td>ValidationRetry</td><td>驗證是等待 toobe 重試。</td>
</tr>
<tr>
<tr>
<td rowspan="2">InProgress</td><td>Validating</td><td>驗證正在進行中。</td>
</tr>
<td>-</td>
<td>正在處理 hello 活動視窗。</td>
</tr>
<tr>
<td rowspan="4">Failed</td><td>TimedOut</td><td>hello 活動的執行時間超過所允許的 hello 活動。</td>
</tr>
<tr>
<td>Canceled</td><td>hello 活動視窗已取消的使用者動作。</td>
</tr>
<tr>
<td>驗證</td><td>驗證失敗。</td>
</tr>
<tr>
<td>-</td><td>hello 活動視窗無法 toobe 產生或驗證。</td>
</tr>
<td>就緒</td><td>-</td><td>hello 活動視窗已準備好耗用量。</td>
</tr>
<tr>
<td>Skipped</td><td>-</td><td>未處理 hello 活動視窗。</td>
</tr>
<tr>
<td>None</td><td>-</td><td>活動視窗 tooexist 搭配不同的狀態，但已重設。</td>
</tr>
</table>


當您按一下活動視窗 hello 清單中的時，您會看到相關的詳細資料，在 hello**活動 Windows 檔案總管**或 hello**屬性**上 hello 右視窗。

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>重新整理活動時段
hello 詳細資料不會自動重新整理，因此使用 hello 命令列 toomanually 重新整理 hello 活動 windows 清單中的 [hello 重新整理] 按鈕 （hello 第二個按鈕）。  

### <a name="properties-window"></a>[屬性] 視窗
hello 屬性 視窗是在 hello 最右邊的窗格中的 hello 監視和管理應用程式。

![[屬性] 視窗](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

它會顯示您選取 hello 資源總管 （樹狀結構檢視） 中的 hello 項目的屬性或活動視窗清單。

### <a name="activity-window-explorer"></a>活動時段總管
hello**活動視窗總管**視窗是在 hello hello 監視和管理應用程式的最右邊的窗格中。 它會顯示有關您在 hello 活動 Windows 快顯視窗或 hello 活動視窗 清單中選取的 hello 活動視窗的詳細資料。

![活動時段總管](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

您可以切換 tooanother 活動視窗頂端 hello hello 行事曆 檢視中按一下。 您也可以使用 hello 左側的箭號右邊的箭號按鈕，在 hello 頂端 toosee 活動 windows hello 從上一週，或 hello 下週。

您可以使用 hello 底部窗格 toorerun hello 活動視窗中的 hello 工具列按鈕，或重新整理在 hello 窗格中的 hello 詳細資料。

### <a name="script"></a>指令碼
您可以使用 hello**指令碼** 索引標籤 tooview hello hello 的 JSON 定義會選取 Data Factory 實體 （連結的服務、 資料集或管線）。

![指令碼索引標籤](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>使用系統檢視
hello 監視和管理應用程式包含預先建立的系統檢視表 (**最近活動 windows**，**失敗活動 windows**，**進行中活動 windows**)，可讓您針對您的 data factory tooview 最近/失敗/進行中活動視窗。

切換 toohello**監視檢視**hello 左側，按一下索引標籤。

![[監視檢視] 索引標籤](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

目前，有三個支援的系統檢視。 選取選項 toosee 最近活動 windows、 失敗的活動視窗或進行中活動 windows hello 活動視窗 （在 hello hello 中間窗格底端） 清單中的。

當您選取 hello**最近活動 windows**選項，您會看到所有的最近活動 windows hello 的遞減順序**上次嘗試時間**。

您可以使用 hello**失敗活動 windows**檢視 toosee 所有失敗的活動 windows hello 清單中。 選取失敗的活動視窗中將 hello 清單 toosee 詳細資訊，請參閱 hello**屬性**視窗或 hello**活動視窗總管**。 您也可以下載失敗的活動時段的任何記錄檔。

## <a name="sort-and-filter-activity-windows"></a>排序與篩選活動時段
變更 hello**開始時間**和**結束時間**hello 命令列 toofilter 活動視窗中的設定。 變更 hello 開始時間和結束時間之後，按一下 hello 按鈕下一步 toohello 結束時間 toorefresh hello 活動視窗清單。

![開始及結束時間](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> 目前，所有時間都都以 UTC 格式 hello 監視和管理應用程式中。
>
>

在 hello**活動視窗清單**，按一下 hello 的資料行的名稱 (例如： 狀態)。

![活動時段清單的資料行功能表](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

您可以執行下列 hello:

* 以遞增順序排序。
* 以遞減順序排序。
* 根據一或多個值 (Ready、Waiting 等) 來篩選。

當您在資料行上指定篩選器時，您會看見 hello 篩選按鈕啟用該資料行，這表示 hello 資料行中的 hello 值已篩選的值。

![Hello 活動視窗清單的資料行上篩選](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

您可以使用 hello 相同的快顯視窗 tooclear 篩選。 tooclear 所有篩選 hello 活動視窗的清單，請按一下 hello 命令列上的 hello 清除篩選按鈕。

![清除所有篩選器，如 hello 活動視窗清單](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>執行批次動作
### <a name="rerun-selected-activity-windows"></a>重新執行已選取的活動時段
選取活動視窗，按一下向下箭號，第一個命令列按鈕 hello，hello 並選取**重新執行** / **重新執行與上游管線中**。 當您選取 hello**重新執行與上游管線中**選項時，它可重新執行所有的上游活動視窗以及。
    ![重新執行某個活動時段](./media/data-factory-monitor-manage-app/ReRunSlice.png)

也可以在 hello 清單中選取多個活動視窗並且在 hello 予以重新執行相同的時間。 您可能想 toofilter 活動 windows hello 狀態為基礎 (例如：**失敗**)-，然後更正，導致 hello 活動 windows toofail hello 問題之後重新執行失敗的 hello 活動視窗。 請參閱下列區段，如需詳細資訊，關於篩選活動 windows hello 清單中的 hello。  

### <a name="pauseresume-multiple-pipelines"></a>暫停/繼續多個管線
您可以使用 hello Ctrl 鍵的多重選取的兩個或多個管線。 您可以使用 hello 命令 列按鈕 （這會反白顯示 hello 下列映像中的 hello 紅色矩形） toopause/繼續它們。

![暫停/繼續 hello 命令列上](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>建立警示
hello**警示**頁面可讓您建立警示及檢視/編輯/刪除現有的警示。 您也可以停用/啟用警示。 toosee hello 警示 頁面上，按一下 hello**警示** 索引標籤。

![[警示] 索引標籤](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate 警示
1. 按一下**新增警示**tooadd 警示。 您會看到 hello**詳細資料**頁面。

    ![建立警示：[詳細資料] 頁面](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. 指定 hello**名稱**和**描述**hello 警示，然後按一下**下一步**。 您應該會看見 hello**篩選**頁面。

    ![建立警示：[篩選器] 頁面](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. 選取 hello**事件**，**狀態**，和**子狀態**（選擇性） 您想 toocreate Data Factory 服務警示，並按一下**下一步**. 您應該會看見 hello**收件者**頁面。

    ![建立警示：[收件者] 頁面](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. 選取 hello**電子郵件訂閱管理員**選項及/或輸入**其他管理員電子郵件**，然後按一下**完成**。 您應該會看到 hello 清單中的 hello 警示。

    ![警示清單](./media/data-factory-monitor-manage-app/AlertsList.png)

在 hello 警示清單中，使用與 hello 警示 tooedit/刪除/停用/啟用警示相關聯的 hello 按鈕。

### <a name="eventstatussubstatus"></a>事件/狀態/子狀態
hello 下表提供 hello 清單可用的事件和狀態 （和子狀態）。

| 事件名稱 | 狀態 | 子狀態 |
| --- | --- | --- |
| 活動執行已開始 |已啟動 |啟動中 |
| 活動執行已結束 |Succeeded |Succeeded |
| 活動執行已結束 |Failed |資源配置失敗<br/><br/>執行失敗<br/><br/>Timed Out<br/><br/>Failed Validation<br/><br/>Abandoned |
| 已開始建立隨選 HDI 叢集 |已啟動 |-|
| 已成功建立隨選 HDI 叢集 |Succeeded |-|
| 已刪除隨選 HDI 叢集 |Succeeded |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit、 刪除或停用警示

使用下列按鈕 （以紅色反白顯示） tooedit、 刪除或停用警示的 hello。

![警示按鈕](./media/data-factory-monitor-manage-app/AlertButtons.png)
