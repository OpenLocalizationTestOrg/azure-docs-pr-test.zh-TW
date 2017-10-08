---
title: "aaaHow toomonitor 雲端服務 |Microsoft 文件"
description: "了解如何 toomonitor 使用 hello Azure 傳統入口網站的雲端服務。"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>如何 tooMonitor 雲端服務
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

您可以監視`key`hello Azure 傳統入口網站中的雲端服務的效能度量。 您可以設定 hello，層級的監視 toominimal 和每個服務角色的詳細資訊，並且可以自訂監視顯示 hello。 詳細資訊監視資料會儲存在儲存體帳戶，您可以存取外部 hello 入口網站。 

監視的顯示 hello Azure 傳統入口網站中可高度設定。 您可以選擇 hello 度量 toomonitor hello hello 度量清單中的要**監視器** 頁面上，而且您可以選擇在度量圖表上 hello 哪些度量 tooplot**監視器**頁面和 hello 儀表板。 

## <a name="concepts"></a>概念
根據預設，使用 hello hello 角色執行個體 （虛擬機器） 的主機作業系統所收集的效能計數器的新雲端服務提供最低監視。 hello 最小度量是有限的 tooCPU 百分比、 資料、 資料輸出、 磁碟讀取輸送量和磁碟寫入輸送量。 藉由設定詳細資訊監視，您可以收到 hello 虛擬機器 （角色執行個體） 內的效能資料為基礎的其他度量。 hello 詳細資訊度量啟用進一步分析的應用程式作業期間發生的問題。

預設會從角色執行個體的效能計數器資料取樣，並每隔 3 分鐘傳送 hello 角色執行個體。 當您啟用詳細資訊監視時，hello 原始效能計數器資料是彙總每個角色執行個體和每個角色的角色執行個體之間的 5 分鐘、 1 小時和 12 小時的間隔。 hello 彙總的資料都會被清除之後 10 天。

啟用詳細資訊監視，彙總的 hello 之後監視資料會儲存在儲存體帳戶中的資料表。 tooenable 監視角色的詳細資訊，您必須設定連結 toohello 儲存體帳戶的診斷連接字串。 您可以對於不同的角色使用不同的儲存體帳戶。

啟用詳細資訊監視會增加儲存成本相關 toodata 儲存體、 資料傳輸和儲存體交易。 最小監視不需要儲存體帳戶。 會公開在 hello 最小監視層級的 hello 度量的 hello 資料不儲存在儲存體帳戶，即使您設定監視層級 tooverbose hello。

## <a name="how-to-configure-monitoring-for-cloud-services"></a>做法：為雲端服務設定監視功能
使用下列程序 tooconfigure 詳細資訊或最小監視 hello Azure 傳統入口網站中的 hello。 

### <a name="before-you-begin"></a>開始之前
* 建立*傳統*監視資料的儲存體帳戶 toostore hello。 您可以對於不同的角色使用不同的儲存體帳戶。 如需詳細資訊，請參閱[如何 toocreate 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。
* 對於雲端服務角色啟用 Azure 診斷。 請參閱「 [為雲端服務設定診斷功能](cloud-services-dotnet-diagnostics.md)」。

請確認 hello 診斷連接字串中已有 hello 角色組態。 您無法開啟詳細資訊監視，直到您啟用 Azure 診斷，並包含在 hello 角色設定中的診斷連接字串。   

> [!NOTE]
> 目標為 Azure SDK 2.5 專案未自動 hello 診斷連接字串中包含 hello 專案範本。 這些專案，您需要 toomanually 新增 hello 診斷連接字串 toohello 角色組態。
> 
> 

**toomanually 新增診斷連接字串 tooRole 組態**

1. 在 Visual Studio 中開啟 hello 雲端服務專案
2. 按兩下 hello**角色**tooopen hello 角色設計工具，然後選取 hello**設定** 索引標籤
3. 尋找名為 **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**的設定。 
4. 如果此設定不存在，按一下 上 hello**加入設定**按鈕 tooadd 它 toohello 設定及變更 hello 類型 hello 新設定太**ConnectionString**
5. Hello 上的 [設定連接字串 hello hello 值**...** ] 按鈕。 儲存體帳戶，這會開啟一個對話方塊，可讓您 tooselect 中。
   
    ![Visual Studio 設定](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>監視層級 tooverbose toochange hello 或最小
1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，開啟 hello**設定**hello 雲端服務部署的頁面。
2. 在 [層級] 中，按一下 [詳細資訊] 或 [最小]。 
3. 按一下 [儲存] 。

開啟詳細資訊監視之後，您應該會開始看到 hello hello 一小時內監視 hello Azure 傳統入口網站中的資料。

hello 原始效能計數器資料和彙總監視的資料會儲存在 hello hello 部署識別碼 hello 角色所限定的資料表中的儲存體帳戶中。 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>做法：接收雲端服務計量的警示
您可以按照雲端服務監視度量接收警示。 在 hello**管理服務**頁面 hello Azure 傳統入口網站，您可以建立規則 tootrigger 警示，當您選擇的 hello 度量到達您所指定的值。 您也可以選擇傳送嗨在警示觸發時 toohave 電子郵件。 如需詳細資訊，請參閱 [做法：在 Azure 中接收警示通知及管理警示規則](http://go.microsoft.com/fwlink/?LinkId=309356)。

## <a name="how-to-add-metrics-toohello-metrics-table"></a>如何： 加入度量 toohello 度量資料表
1. 在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，開啟 hello**監視器**hello 雲端服務的頁面。
   
    根據預設，hello 度量表會顯示 hello 可用度量的子集。 hello 圖會顯示 hello 預設詳細資訊度量的雲端服務，也就是限制的 toohello Memory\Available MBytes 效能計數器，其中在 hello 角色層級彙總的資料。 使用**加入度量**tooselect 其他彙總並在角色層級度量 toomonitor hello Azure 傳統入口網站。
   
    ![詳細資訊顯示](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tooadd 度量 toohello 計量表：
   
   1. 按一下**加入度量**tooopen **選擇度量**，如下所示。
      
       hello 第一個可用的度量是展開的 tooshow 可用的選項。 每個度量，hello top 選項會顯示所有角色的彙總監視資料。 此外，您可以選擇個別角色 toodisplay 資料。
      
       ![Add metrics](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect 度量 toodisplay
      
      * 按一下向下箭號的 hello 的 hello 度量 tooexpand hello 監視選項。
      * 選取 hello 核取方塊，每個監視您想要 toodisplay 選項。
        
        您可以向上 too50 度量 hello 度量資料表中顯示。
        
        > [!TIP]
        > 在設定監視的詳細資訊，hello 度量清單可以包含數十個度量。 toodisplay 捲軸，暫留在 [hello] 對話方塊中的 hello 右側。 toofilter hello 清單中，按一下 hello 搜尋圖示，並在 hello 搜尋方塊中輸入文字，如下所示。
        > 
        > 
        
        ![加入度量搜尋](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. 完成選取度量後，按一下 [確定] \(核取記號)。
   
    hello 選定的度量會加入 toohello 度量資料表，如下所示。
   
    ![監視度量](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete 度量，以從 hello 度量資料表中，按一下 hello 度量 tooselect，再按**刪除度量**。 (只有在您選取度量時，才會看見 [刪除度量]。)

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tooadd 自訂度量 toohello 度量資料表
hello **Verbose**監視層級提供一份您可以監視的預設計量 hello 入口網站上。 此外 toothese 您可以監視的任何自訂的度量或透過 hello 入口網站應用程式所定義的效能計數器。

hello 下列步驟假設您已開啟**Verbose**監視層級，並且已設定您的應用程式 toocollect 和傳送自訂效能計數器。 

toodisplay hello 自訂效能計數器中的 hello 需要 tooupdate hello 設定 wad 控制項容器中的入口網站：

1. 開啟您的診斷儲存體帳戶中的 hello wad 控制項容器的 blob。 您可以使用 Visual Studio 或任何其他儲存體總管 toodo 這。
   
    ![Visual Studio 伺服器總管](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. 瀏覽 hello blob 路徑使用 hello 模式**DeploymentId/RoleName/RoleInstance** toofind hello 設定角色執行個體。 
   
    ![Visual Studio 儲存體總管](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. 下載您的角色執行個體的 hello 組態檔，並更新 tooinclude 任何自訂效能計數器。 例如 toomonitor *Disk Write Bytes/sec* hello *C 磁碟機*新增下的 hello 下列**PerformanceCounters\Subscriptions**節點
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. 儲存 hello 變更以及上傳 hello 設定檔後 toohello 相同的位置覆寫 hello hello blob 中現有的檔案。
5. 切換 tooVerbose hello Azure 傳統入口網站設定中的模式。 如果您已經以詳細資訊模式將會有 tootoggle toominimal 來回 tooverbose。
6. hello 自訂效能計數器將會出現在 [hello**加入度量**] 對話方塊。 

## <a name="how-to-customize-hello-metrics-chart"></a>如何： 自訂 hello 度量圖表
1. 在 hello 度量資料表中，選取 too6 度量 tooplot hello 度量圖表上。 tooselect 公制，請按一下左側的 hello 核取方塊。 tooremove hello 度量圖表中，從度量資訊，請清除其 hello 度量資料表中的核取方塊。
   
    當您 hello 度量資料表中選取度量，hello 度量隨即新增 toohello 度量圖表。 在窄的顯示器上**多個 n**下拉式清單包含標準標頭不適合 hello 顯示。
2. 相對的值 （只針對每個標準的最終值） 和絕對值 （Y 軸顯示） 顯示之間 tooswitch 選取相對或絕對頂端 hello hello 圖表。
   
    ![相對或絕對](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. toochange hello 時間範圍 hello 度量圖表會顯示中，選取 1 小時、 24 小時或 7 天在 hello hello 圖表的頂端。
   
    ![監視顯示期間](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    在 hello 儀表板的度量圖表上繪製的度量的 hello 方法會不同。 一組標準度量可和度量資訊會加入或移除選取 hello 度量標頭。

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>hello 儀表板上 toocustomize hello 度量圖表
1. 開啟 hello 雲端服務的 hello 儀表板。
2. 從新增或移除度量 hello 圖表：
   
   * tooplot hello 圖表標頭中的 hello 度量新 hello 度量，請選取核取方塊。 窄的顯示畫面中，按一下向下箭號的 hello  ***n* ??度量**tooplot 度量 hello 圖表標頭區域無法顯示。
   * toodelete 在 hello 圖上，清除 hello 核取方塊，其標頭所繪製的度量。
   
3. 切換 [相對] 和 [絕對] 顯示。
4. 選擇 1 小時、 24 小時或 7 天的資料 toodisplay。

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>如何： 存取外部 hello Azure 傳統入口網站的詳細資訊監視資料
詳細資訊監視資料會儲存在您指定每個角色的 hello 儲存體帳戶中的資料表。 每個雲端服務部署中，六個資料表會針對建立 hello 角色。 個別 (5 分鐘、1 小時和 12 小時) 建立 2 個表格。 其中一個資料表會儲存角色層級彙總。hello 角色執行個體的其他資料表存放區的彙總。 

hello 資料表名稱具有下列格式的 hello:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

其中：

* *deploymentID*為 hello 分派 toohello 雲端服務部署的 GUID
* aggregation_interval = 5M、1H 或 12H
* 角色層級彙總 = R
* 角色執行個體彙總 = RI

例如，hello 下列資料表會儲存在 1 小時的時間間隔的彙總資料的詳細資訊監視資料：

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
