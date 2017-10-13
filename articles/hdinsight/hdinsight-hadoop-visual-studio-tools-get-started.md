---
title: "使用 Data Lake Tools for Visual Studio 連線至 Azure HDInsight | Microsoft Docs"
description: "了解如何安裝和使用 Data Lake Tools for Visual Studio 來連線到 Azure HDInsight 中的 Hadoop 叢集及執行 Hive 查詢。"
keywords: "hadoop 工具,hive 查詢,visual studio,visual studio hadoop"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: f7eff70ece5e8dc7e0c5983871d40bd1f6eafff2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-azure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>使用 Data Lake Tools for Visual Studio 連線至 Azure HDInsight 及執行 Hive 查詢

了解如何使用 Data Lake Tools for Visual Studio 來連線到 [Azure HDInsight](hdinsight-hadoop-introduction.md) 中的 Hadoop 叢集及提交 Hive 查詢。 如需使用 HDInsight 的詳細資訊，請參閱 [HDInsight 簡介](hdinsight-hadoop-introduction.md)和[開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。 如需連線到 Storm 叢集的詳細資訊，請參閱[使用 Visual Studio 開發 HDInsight 上 Apache Storm 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

Data Lake Tools for Visual Studio 可用來存取 Data Lake Analytics 和 HDInsight。  如需 Data Lake Tools 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md)。

**必要條件**

若要完成本教學課程並使用 Visual Studio 中的 Data Lake Tools，您需要下列項目：

* Azure HDInsight 叢集︰若要建立叢集，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* 已安裝下列軟體的工作站：
  
  * Windows 10、Windows 8.1、Windows 8 或 Windows 7。
  * Visual Studio 2013/2015/2017。
    
    > [!NOTE]
    > Data Lake Tools for Visual Studio 目前只有英文版。
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>安裝 Data Lake Tools for Visual Studio

預設會針對 Visual Studio 2017 安裝 Data Lake Tools。 對於較舊版本，您可以使用 [Web Platform Installer](https://www.microsoft.com/web/downloads/) 來安裝。 您必須選擇與 Visual Studio 版本相符的封裝。 如果您沒有安裝 Visual Studio，可以使用 [Web Platform Installer](https://www.microsoft.com/web/downloads/)，來安裝最新的 Visual Studio Community 和 Azure SDK：

![Data Lake Tools for Visual Studio Web 平台安裝程式。](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "使用 Web 平台安裝程式來安裝 Data Lake Tools for Visual Studio")

## <a name="connect-to-azure-subscriptions"></a>連線到 Azure 訂用帳戶
Data Lake Tools for Visual Studio 可讓您連線到您的 HDInsight 叢集、執行一些基本管理作業，以及執行 Hive 查詢。

> [!NOTE]
> 如需連線到一般 Hadoop 叢集的相關資訊，請參閱 [使用 Visual Studio 撰寫和提交 Hive 查詢](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx)。
> 
> 

**連線到您的 Azure 訂用帳戶**

1. 開啟 Visual Studio。
2. 從 [檢視] 功能表中，按一下 [伺服器總管] 以開啟 [伺服器總管] 視窗。
3. 展開 [Azure]，然後展開 [HDInsight]。
   
   > [!NOTE]
   > 請注意，[HDInsight 工作清單] 視窗此時應該會開啟。 如果您沒有看到該視窗，請按一下 [檢視] 功能表的 [其他視窗]，然後按一下 [HDInsight 工作清單視窗]。  
   > 
   > 
4. 輸入您的 Azure 訂用帳戶認證，然後按一下 [登入] 。 只有當您從未在此工作站上從 Visual Studio 連線到 Azure 訂用帳戶時，才需要這樣做。
5. 在 [伺服器總管] 中，您會看到現有 HDInsight 叢集的清單。 如果您沒有任何叢集，可以使用 Azure 入口網站、Azure PowerShell 或 HDInsight SDK 來建立一個。 如需詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。
   
   ![Data Lake Tools for Visual Studio Server Explorer 叢集清單](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Data Lake Tools for Visual Studio Server Explorer")
6. 展開某個 HDInsight 叢集。 您將會看到 **Hive 資料庫**、預設儲存體帳戶、連結的儲存體帳戶，以及 **Hadoop 服務記錄**。 您可以進一步展開這些實體。

在連線到您的 Azure 訂用帳戶之後，您將可以執行下列工作：

**從 Visual Studio 連線到 Azure 入口網站**

* 從 [伺服器總管] 中，展開 [Azure] > [HDInsight]，在 HDInsight 叢集上按一下滑鼠右鍵，然後按一下 [在 Azure 入口網站中管理叢集]。

**從 Visual Studio 提出問題及提供意見反應**

* 從 [工具] 功能表中，按一下 [HDInsight]，然後按一下 [MSDN 論壇] 來提出問題，或按一下 [提供意見反應]。

## <a name="navigate-the-linked-resources"></a>瀏覽連結的資源
從 [伺服器總管] 中，您可以看到預設的儲存體帳戶，以及任何連結的儲存體帳戶。 如果您展開預設儲存體帳戶，您可以看到儲存體帳戶上的容器。 預設儲存體帳戶和預設容器皆已標示。 您也可以在任何容器上按一下滑鼠右鍵來檢視該容器。

![Data Lake Tools for Visual Studio Server Explorer 清單連結資源](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "清單連結資源")

開啟容器之後，您可以使用下列按鈕來上傳、刪除及下載 Blob：

![Data Lake Tools for Visual Studio Server Explorer Blob 作業](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "更新、刪除和下載 Blob")

## <a name="run-a-hive-query"></a>執行 HIVE 查詢
[Apache Hive](http://hive.apache.org) 是以 Hadoop 為基礎的資料倉儲基礎結構，用來提供資料摘要、查詢和分析。 Data Lake Tools for Visual Studio 支援從 Visual Studio 執行 Hive 查詢。 如需 Hive 的詳細資訊，請參閱[使用 Hive 搭配 HDInsight](hdinsight-use-hive.md)。

針對 HDInsight 叢集測試 Hive 指令碼十分耗時。 這可能需要數分鐘以上的時間。 Data Lake Tools for Visual Studio 可以在本機驗證 Hive 指令碼，而不需要連線到即時叢集。

Data Lake Tools for Visual Studio 也可讓使用者透過收集和呈現特定 Hive 工作的 YARN 記錄，來查看 Hive 工作的內容。

### <a name="view-the-hivesampletable"></a>檢視 **hivesampletable**
所有 HDInsight 叢集皆隨附一個稱為 *hivesampletable*的範例 Hive 資料表。 我們將使用此資料表來示範如何列出 Hive 資料表、檢視資料表結構描述，以及列出 Hive 資料表中的資料列。

**列出 Hive 資料表和檢視 Hive 資料表結構描述**

1. 從 [伺服器總管] 中，展開 [Azure] > [HDInsight] > 選擇的叢集 > [Hive 資料庫] > [預設] > [hivesampletable] 來查看資料表結構描述。
2. 在 [hivesampletable] 上按一下滑鼠右鍵，然後按一下 [檢視前 100 個資料列] 來列出資料列。 這相當於使用 Hive ODBC 驅動程式來執行下列 Hive 查詢：
   
     SELECT * FROM hivesampletable LIMIT 100
   
   您可以自訂資料列計數。
   
   ![Data Lake Tools：HDInsight Hive Visual Studio 結構描述查詢](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Hive 查詢結果")

### <a name="create-hive-tables"></a>建立 Hive 資料表
您可以使用 GUI 來建立 Hive 資料表或使用 Hive 查詢。 如需使用 Hive 查詢的相關資訊，請參閱 [執行 Hive 查詢](#run.queries)。

**建立 Hive 資料表**

1. 從 [伺服器總管] 中，展開 [Azure] > [HDInsight 叢集] > 某個 HDInsight 叢集 > [Hive 資料庫]，然後在 [預設] 上按一下滑鼠右鍵，並按一下 [建立資料表]。
2. 設定資料表。
3. 按一下 [ **建立資料表** ] 以提交工作來建立新 Hive 資料表。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具會建立 Hive 資料表](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "建立 Hive 資料表")

### <a name="run.queries"></a>驗證和執行 Hive 查詢
有兩種方式可建立和執行 Hive 查詢：

* 建立特定查詢
* 建立 Hive 應用程式

**建立、驗證和執行特定查詢**

1. 從 [伺服器總管] 中，展開 [Azure]，然後展開 [HDInsight 叢集]。
2. 在您想要執行查詢的叢集上按一下滑鼠右鍵，然後按一下 [ **撰寫 Hive 查詢**]。
3. 輸入 Hive 查詢。 請注意，Hive 編輯器支援 Intellisense。 Data Lake Tools for Visual Studio 支援在編輯 Hive 指令碼時載入遠端中繼資料。 例如，當您輸入 "SELECT * FROM"，IntelliSense 會列出所有建議的資料表名稱。 在指定了資料表名稱時，IntelliSense 會列出資料行名稱。 此工具幾乎支援所有的 Hive DML 陳述式、子查詢以及內建 UDF。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具 IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Data Lake Tools：HDInsight Visual Studio 工具 IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > 只會建議 HDInsight [工具列] 中已選取的叢集中繼資料。
   > 
   > 
4. (選擇性)：按一下 [ **驗證指令碼** ] 檢查指令碼語法錯誤。
   
    ![Data Lake Tools︰Data Lake Tools for Visual Studio 本機驗證](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "驗證指令碼")
5. 按一下 [提交] 或 [提交 (進階)]。 您可以利用進階提交選項來設定指令碼的 [工作名稱]、[引數]、[其他組態] 和 [狀態目錄]：
   
    ![HDInsight Hadoop Hive 查詢](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "提交查詢")
   
    提交工作之後，您會看到 [Hive 工作摘要  ] 視窗。
   
    ![HDInsight Hadoop Hive 查詢的摘要](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Hive 作業摘要")
6. 使用 [重新整理] 按鈕來更新狀態，直到工作狀態變更為 [已完成] 為止。
7. 按一下底部的連結以查看下列內容：[工作查詢]、[工作輸出]、[工作記錄] 或 [Yarn 記錄]。

**建立和執行 Hive 方案**

1. 從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。
2. 從左窗格中選取 [HDInsight]，選取中間窗格中的 [Hive 應用程式]，輸入屬性，然後按一下 [確定]。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具新 Hive 專案](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "從 Visual Studio 建立 Hive 應用程式")
3. 從 [方案總管] 中，按兩下 **Script.hql** 來開啟它。
4. 若要驗證 Hive 指令碼，您可以按一下 [驗證指令碼] 按鈕，或在 Hive 編輯器中的指令碼上按一下滑鼠右鍵，然後按一下內容功能表中的 [驗證指令碼]。

### <a name="view-hive-jobs"></a>檢視 Hive 工作
您可以檢視 Hive 工作的工作查詢、工作輸出、工作記錄和 Yarn 記錄。 如需詳細資訊，請參閱上一個螢幕擷取畫面。

此工具的最新版本可讓您透過收集和呈現 YARN 記錄來查看 Hive 工作的內容。 YARN 記錄可協助您調查效能問題。 如需 HDInsight 如何收集 YARN 記錄的詳細資訊，請參閱[透過程式設計方式存取 HDInsight 應用程式記錄](hdinsight-hadoop-access-yarn-app-logs.md)。

**檢視 Hive 工作**

1. 從 [伺服器總管] 中，展開 [Azure]，然後展開 [HDInsight]。
2. 在某個 HDInsight 叢集上按一下滑鼠右鍵，然後按一下 [檢視工作 ]。 您會看到在該叢集上執行之 Hive 工作的清單。
3. 按一下工作清單中的某個工作來選取它，然後使用 [Hive 工作摘要] 視窗來開啟 [工作查詢]、[工作輸出]、[工作記錄] 或 [Yarn 記錄]。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具檢視 Hive 作業](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "檢視 Hive 作業")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>透過 HiveServer2 的更快速路徑 Hive 執行
> [!NOTE]
> 此功能僅適用於 HDInsight 叢集 3.2 版及更新版本。
> 
> 

Data Lake Tools 用來透過 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (也稱為 Templeton) 提交 Hive 工作。 傳回工作詳細資料和錯誤資訊所需的時間很長。
為了解決此效能問題，Data Lake Tools 會透過 HiveServer2 直接在叢集中執行 Hive 工作，以便略過 RDP/SSH。
除了提升效能，使用者也可以檢視 Tez 圖形上的 Hive 和工作詳細資料。

若為 HDInsight 叢集 3.2 版或更新版本，您可以看見 [透過 HiveServer2 執行] 按鈕：

![透過 hiveserver2 執行 Data Lake visual studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "使用 HiveServer2 執行 Hive 查詢")

而且，如果 Hive 查詢是在 Tez 中執行，您可以即時查看串流送回的記錄檔，以及查看工作圖形。

![Data Lake visual studio Tools 快速路徑 hive 執行](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "檢視作業圖形")

**透過 HiveServer2 執行查詢與透過 WebHCat 提交查詢之間的差異**

雖然透過 HiveServer2 執行查詢有許多效能方面的優點，但這方法仍然有幾項限制。 且某些限制不適合做為生產用途。 下表為這兩種方法的差異：

|  | 透過 HiveServer2 執行 | 透過 WebHCat 提交 |
| --- | --- | --- |
| 執行查詢 |會排除 WebHCat 中的額外負荷 (WebHCat 會啟動叫做「TempletonControllerJob」的 MapReduce 工作)。 |只要查詢是透過 WebHCat 來執行，WebHCat 就會啟動帶來額外延遲的 MapReduce 工作。 |
| 將記錄檔串流回來 |近乎即時進行。 |只在工作結束時才提供工作執行記錄檔。 |
| 檢視工作歷程記錄 |如果查詢是透過 HiveServer2 執行，系統將不會保留查詢的工作歷程記錄 (工作記錄檔、工作輸出)。 您可以在 YARN UI 中檢視應用程式的有限資訊。 |如果查詢是透過 WebHCat 執行，系統會保留查詢的工作歷程記錄 (工作記錄檔、工作輸出)，且可讓您使用 Visual Studio/HDInsight SDK/PowerShell 來檢視。 |
| 關閉視窗 |透過 HiveServer2 執行的方式是「同步進行」的，因此您必須讓視窗保持開啟；如果視窗關閉，系統就會取消執行查詢。 |透過 WebHCat 提交的方式是「非同步進行」的，因此您可以透過 WebHCat 提交查詢，然後關閉 Visual Studio。 您隨時可以回來查看結果。 |

### <a name="tez-hive-job-performance-graph"></a>Tez Hive 工作效能圖表
Data Lake Tools 支援顯示由 Tez 執行引擎執行之 Hive 工作的效能圖形。 如需啟用 Tez 的資訊，請參閱[在 HDInsight 中使用 Hive](hdinsight-use-hive.md)。 您提交 Visual Studio 中的 Hive 工作之後，Visual Studio 會在工作完成時顯示圖形。  您可能會需要按一下 [重新整理  ] 按鈕來取得最新的工作狀態。

> [!NOTE]
> 此功能只適用於高於 3.2.4.593 版的 HDInsight 叢集，而且只能用於已完成的工作 (如果您透過 WebHCat 提交作業，此圖形會在您透過 HiveServer2 執行查詢時顯示)。 這適用於以 Windows 和 Linux 為基礎的叢集。
> 
> 

![hadoop hive tez 效能圖](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "作業狀態")

為協助您更了解 Hive 查詢，此工具在本版本中新增了 Hive 運算子檢視功能。 您只需按兩下工作圖形的頂點，即可查看頂點內的所有運算子。 您也可將滑鼠停留在特定運算子上方，以檢視該運算子的更多詳細資料。

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Tez 工作上 Hive 的工作執行檢視
Tez 工作上 Hive 的工作執行檢視可用來取得結構化和視覺化 Hive 工作的資訊，以及取得更多工作詳細資料。 發生效能問題時，您可以使用此檢視來取得進一步的詳細資料。 例如，每個工作的運作方式和每個工作的詳細資訊 (資料讀取/寫入、排程/開始/結束時間等)，以便根據視覺化資訊微調工作組態或系統架構。

![Data Lake Visual Studio Tools 工作執行檢視](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "工作執行檢視")

## <a name="run-pig-scripts"></a>執行 Pig 指令碼
Data Lake Tools for Visual Studio 支援建立 Pig 指令碼並提交至 HDInsight 叢集。 使用者可以從範本建立 Pig 專案，然後再提交指令碼至 HDInsight 叢集。

## <a name="feedbacks--known-issues"></a>意見反應和已知問題
* 目前 HiveServer2 結果會以純文字形式顯示，但不太理想。 我們正努力修正該問題。
* 如果結果是以 NULL 值開頭，目前就不會顯示結果。 我們已修正此問題，如果您因為此問題而遭到封鎖，歡迎寄電子郵件給我們，或連絡支援小組。
* Visual Studio 所建立的 HQL 指令碼是根據使用者的所在區域設定進行編碼。 如果使用者將指令碼以二進位格式上傳至叢集，則可能無法正常執行。

## <a name="next-steps"></a>後續步驟
在本文中，您學會如何使用 Data Lake (HDInsight) Tools 套件從 Visual Studio 連線到 HDInsight 叢集，以及如何執行 Hive 查詢。 如需詳細資訊，請參閱：

* [在 HDInsight 中使用 Hadoop Hive](hdinsight-use-hive.md)
* [開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)
* [在 HDInsight 上提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)
* [在 HDInsight 中使用 Hadoop 分析 Twitter 資料](hdinsight-analyze-twitter-data.md)

