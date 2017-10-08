---
title: "aaaConnect tooAzure HDInsight 使用 Data Lake Tools for Visual Studio |Microsoft 文件"
description: "了解 tooinstall 與使用 Data Lake Tools for Visual Studio tooconnect tooHadoop Azure HDInsight 和執行的 Hive 查詢中的叢集。"
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
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>連線 tooAzure HDInsight 並執行使用 Data Lake Tools for Visual Studio 的 Hive 查詢

了解如何 toouse Data Lake Tools for Visual Studio tooconnect tooHadoop 叢集[Azure HDInsight](hdinsight-hadoop-introduction.md)和提交 Hive 查詢。 如需使用 HDInsight 的詳細資訊，請參閱[簡介 tooHDInsight](hdinsight-hadoop-introduction.md)和[開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。 如需連接 tooa Storm 叢集的詳細資訊，請參閱[開發 C# 拓撲上 HDInsight 使用 Visual Studio 的 Apache Storm 的](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

資料湖 Tools for Visual Studio 可以使用的 tooaccess Data Lake Analytics 和 HDInsight。  Hello 資料湖工具有關的資訊，請參閱[教學課程： 開發 U-SQL 指令碼，使用 Data Lake Tools for Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md)。

**必要條件**

toocomplete 此教學課程和使用 hello Data Lake 工具在 Visual Studio 中，您將需要下列 hello:

* Azure HDInsight 叢集： toocreate 一個，請參閱[開始使用 linux 的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* 使用下列軟體的 hello 的工作站：
  
  * Windows 10、Windows 8.1、Windows 8 或 Windows 7。
  * Visual Studio 2013/2015/2017。
    
    > [!NOTE]
    > 目前，hello 資料湖 Tools for Visual Studio 只隨附 hello 英文版。
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>安裝 Data Lake Tools for Visual Studio

預設會針對 Visual Studio 2017 安裝 Data Lake Tools。 對於較舊版本，您可以使用安裝 hello [Web Platform Installer](https://www.microsoft.com/web/downloads/)。 您必須選擇 hello 符合您的 Visual Studio 版本。 如果您沒有安裝 Visual Studio，您可以安裝 hello 最新版的 Visual Studio Community 和 Azure SDK 使用 hello [Web Platform Installer](https://www.microsoft.com/web/downloads/):

![Data Lake Tools for Visual Studio Web Platform installer。](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "使用 Web Platform Installer tooinstall 資料湖 Tools for Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>連接 tooAzure 訂用帳戶
Data Lake Tools for Visual Studio 可讓您 tooconnect tooyour HDInsight 叢集，執行一些基本的管理作業，並執行 Hive 查詢。

> [!NOTE]
> 連接 tooa 泛型 Hadoop 叢集上的資訊，請參閱[撰寫和提交 Hive 查詢使用 Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx)。
> 
> 

**tooconnect tooyour Azure 訂用帳戶**

1. 開啟 Visual Studio。
2. 從 hello**檢視**功能表上，按一下 [**伺服器總管**tooopen hello 伺服器總管] 視窗。
3. 展開 [Azure]，然後展開 [HDInsight]。
   
   > [!NOTE]
   > 請注意 hello **HDInsight 工作清單**視窗應開啟。 如果您沒有看到它，按一下**其他視窗**從 hello**檢視**功能表，然後再按一下**HDInsight 工作清單視窗**。  
   > 
   > 
4. 輸入您的 Azure 訂用帳戶認證，然後按一下登入 。 這只是如果您已從 Visual Studio，在此工作站上，永遠不會連接 toohello Azure 訂用帳戶所需。
5. 在 [伺服器總管] 中，您會看到現有 HDInsight 叢集的清單。 如果您沒有任何叢集，您可以建立一個使用 hello Azure 入口網站、 Azure PowerShell 或 hello HDInsight SDK。 如需詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。
   
   ![Data Lake Tools for Visual Studio Server Explorer 叢集清單](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Data Lake Tools for Visual Studio Server Explorer")
6. 展開某個 HDInsight 叢集。 您將會看到 **Hive 資料庫**、預設儲存體帳戶、連結的儲存體帳戶，以及 **Hadoop 服務記錄**。 您可以進一步展開 hello 實體。

您已連接 tooyour Azure 訂用帳戶之後，您會無法 toodo hello 下列：

**tooconnect toohello 從 Visual Studio Azure 入口網站**

* 從 伺服器總管 中，展開 Azure > HDInsight，在 HDInsight 叢集上按一下滑鼠右鍵，然後按一下在 Azure 入口網站中管理叢集。

**tooask 問題，並從 Visual Studio 提供意見反應**

* 從 hello**工具**功能表上，按一下  **HDInsight**，然後按一下 **MSDN 論壇**tooask 問題，或按一下**提供意見反應**。

## <a name="navigate-hello-linked-resources"></a>瀏覽 hello 連結資源
從伺服器總管 中，您可以看到 hello 預設儲存體帳戶和任何連結儲存體帳戶。 如果您展開 hello 預設儲存體帳戶時，您可以看見 hello 容器 hello 儲存體帳戶上。 標示 hello 預設儲存體帳戶和 hello 預設容器。 您也可以在 hello 容器 tooview hello 內容。

![Data Lake Tools for Visual Studio Server Explorer 清單連結資源](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "清單連結資源")

在開啟容器後，您可以使用下列按鈕 tooupload、 刪除和下載 blob 的 hello:

![Data Lake Tools for Visual Studio Server Explorer Blob 作業](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "更新、刪除和下載 Blob")

## <a name="run-a-hive-query"></a>執行 HIVE 查詢
[Apache Hive](http://hive.apache.org) 是以 Hadoop 為基礎的資料倉儲基礎結構，用來提供資料摘要、查詢和分析。 Data Lake Tools for Visual Studio 支援從 Visual Studio 執行 Hive 查詢。 如需 Hive 的詳細資訊，請參閱[使用 Hive 搭配 HDInsight](hdinsight-use-hive.md)。

很耗時 tootest 針對 HDInsight 叢集的 Hive 指令碼。 這可能需要數分鐘以上的時間。 資料湖 Tools for Visual Studio 是能夠驗證而連接 tooa 即時叢集不在本機的 Hive 指令碼。

資料湖 Tools for Visual Studio 也可讓使用者 toosee 什麼內 hello Hive 工作是藉由收集和面對 hello YARN 記錄檔的特定登錄區工作。

### <a name="view-hello-hivesampletable"></a>檢視 hello **hivesampletable**
所有 HDInsight 叢集皆隨附一個稱為 *hivesampletable*的範例 Hive 資料表。 我們將使用此資料表 tooshow，您如何 toolist Hive 資料表、 檢視 hello 資料表結構描述，並列出 hello 中的資料列 hello Hive 資料表。

**toolist Hive 資料表和檢視 Hive 資料表結構描述**

1. 從**伺服器總管**，依序展開**Azure** > **HDInsight** > hello 叢集，您所選擇的 > **Hive 資料庫** > **預設** > **hivesampletable** toosee hello 資料表結構描述。
2. 以滑鼠右鍵按一下**hivesampletable**，然後按一下**檢視前 100 個資料列**toolist hello 資料列。 它會遵循使用 hive 控制檔的 ODBC 驅動程式的 Hive 查詢的對等 toorunning hello:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   您可以自訂 hello 資料列計數。
   
   ![Data Lake Tools：HDInsight Hive Visual Studio 結構描述查詢](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Hive 查詢結果")

### <a name="create-hive-tables"></a>建立 Hive 資料表
您可以使用 hello GUI toocreate Hive 資料表，或使用 Hive 查詢。 如需使用 Hive 查詢的相關資訊，請參閱 [執行 Hive 查詢](#run.queries)。

**toocreate Hive 資料表**

1. 從 [伺服器總管] 中，展開 [Azure] > [HDInsight 叢集] > 某個 HDInsight 叢集 > [Hive 資料庫]，然後在 [預設] 上按一下滑鼠右鍵，並按一下 [建立資料表]。
2. 設定 hello 資料表。
3. 按一下**Create Table** toosubmit hello 作業 toocreate hello 新 Hive 資料表。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具會建立 Hive 資料表](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "建立 Hive 資料表")

### <a name="run.queries"></a>驗證和執行 Hive 查詢
有兩種方式 toocreate 和執行的 Hive 查詢：

* 建立特定查詢
* 建立 Hive 應用程式

**toocreate，驗證和執行臨機操作查詢**

1. 從 [伺服器總管] 中，展開 [Azure]，然後展開 [HDInsight 叢集]。
2. 以滑鼠右鍵按一下您想 toorun hello 查詢，然後再按一下 hello 叢集**撰寫 Hive 查詢**。
3. 輸入 hello Hive 查詢。 請注意 hello 登錄區編輯器支援 IntelliSense。 編輯您的 Hive 指令碼時，載入 Visual Studio 支援的資料湖工具 hello 遠端中繼資料。 例如，當您輸入"SELECT * FROM"，IntelliSense 就會列出的 hello 所有 hello 建議的資料表名稱。 指定資料表名稱時，依 hello IntelliSense 列出 hello 資料行名稱。 hello 工具支援幾乎所有 hive 控制檔的 DML 陳述式，子查詢，並 hello 內建的 Udf。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具 IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Data Lake Tools：HDInsight Visual Studio 工具 IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > 將會建議只有 hello 中繼資料的 hello 叢集在 HDInsight 工具列中選取。
   > 
   > 
4. （選擇性）： 按一下**驗證指令碼**toocheck hello 指令碼語法錯誤。
   
    ![Data Lake Tools︰Data Lake Tools for Visual Studio 本機驗證](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "驗證指令碼")
5. 按一下 [提交] 或 [提交 (進階)]。 以進階選項送出 hello，您需要設定**工作名稱**，**引數**，**額外的組態**，和**狀態目錄**hello 指令碼：
   
    ![HDInsight Hadoop Hive 查詢](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "提交查詢")
   
    您送出 hello 作業之後，您會看到**Hive 工作摘要**視窗。
   
    ![HDInsight Hadoop Hive 查詢的摘要](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Hive 作業摘要")
6. 使用 hello**重新整理**太 hello 作業狀態變更為止按鈕 tooupdate hello 狀態**已完成**。
7. 按一下 hello hello 底部 toosee hello 下列連結：**工作查詢**，**作業輸出**，**作業記錄**，或**Yarn 記錄**。

**toocreate 和執行 Hive 方案**

1. 從 hello**檔案**功能表上，按一下 **新增**，然後按一下**專案**。
2. 選取**HDInsight** hello 左窗格中，選取**hive 控制檔的應用程式**hello 中央窗格中，輸入 hello 屬性，然後按一下**確定**。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具新 Hive 專案](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "從 Visual Studio 建立 Hive 應用程式")
3. 從**方案總管 中**，連按兩下**Script.hql** tooopen 它。
4. toovalidate hello Hive 指令碼，您可以按一下 hello**驗證指令碼**按鈕，或在 hello 登錄區編輯器 hello 指令碼上按一下滑鼠右鍵，然後按一下**驗證指令碼**hello 操作功能表中。

### <a name="view-hive-jobs"></a>檢視 Hive 工作
您可以檢視 Hive 工作的工作查詢、工作輸出、工作記錄和 Yarn 記錄。 如需詳細資訊，請參閱 hello 上一個螢幕擷取畫面。

hello 最新版本的 hello 工具可讓您 toosee 什麼內部 Hive 工作是藉由收集和面對 YARN 記錄檔。 YARN 記錄可協助您調查效能問題。 如需 HDInsight 如何收集 YARN 記錄的詳細資訊，請參閱[透過程式設計方式存取 HDInsight 應用程式記錄](hdinsight-hadoop-access-yarn-app-logs.md)。

**tooview Hive 工作**

1. 從 [伺服器總管] 中，展開 [Azure]，然後展開 [HDInsight]。
2. 在某個 HDInsight 叢集上按一下滑鼠右鍵，然後按一下檢視工作 。 您會看到一份 hello Hive hello 叢集執行的工作。
3. 按一下 hello 工作清單 tooselect 中的工作，然後使用 hello **Hive 工作摘要**視窗 tooopen**工作查詢**，**作業輸出**，**作業記錄**，或**Yarn 記錄**。
   
    ![Data Lake Tools：HDInsight Visual Studio 工具檢視 Hive 作業](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "檢視 Hive 作業")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>透過 HiveServer2 的更快速路徑 Hive 執行
> [!NOTE]
> 此功能僅適用於 HDInsight 叢集 3.2 版及更新版本。
> 
> 

hello Data Lake Tools 使用 toosubmit Hive 工作透過[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (也稱為 Templeton)。 花費很長的時間 tooreturn 工作詳細資料和錯誤資訊。
順序 toosolve 在此效能問題，hello 資料湖工具執行 hive 控制檔直接 HiveServer2，透過的 hello 叢集中的作業，讓它會略過 RDP/SSH。
加法 toobetter 效能降低，使用者也可以檢視 Tez 圖形上的登錄區，並且 hello 工作詳細資料。

若為 HDInsight 叢集 3.2 版或更新版本，您可以看見 [透過 HiveServer2 執行] 按鈕：

![透過 hiveserver2 執行 Data Lake visual studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "使用 HiveServer2 執行 Hive 查詢")

您可以查看並 hello 中即時資料流處理的記錄檔中 Tez 執行 hello Hive 查詢時，請參閱 hello 作業圖形。

![Data Lake visual studio Tools 快速路徑 hive 執行](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "檢視作業圖形")

**透過 HiveServer2 執行查詢與透過 WebHCat 提交查詢之間的差異**

雖然透過 HiveServer2 執行查詢有許多效能方面的優點，但這方法仍然有幾項限制。 某些 hello 限制不適用於生產使用方式。 hello 下表顯示 hello 差異：

|  | 透過 HiveServer2 執行 | 透過 WebHCat 提交 |
| --- | --- | --- |
| 執行查詢 |排除 WebHCat （其會啟動 MapReduce 工作名為"TempletonControllerJob"） 中的 hello 額外負荷。 |只要查詢是透過 WebHCat 來執行，WebHCat 就會啟動帶來額外延遲的 MapReduce 工作。 |
| 將記錄檔串流回來 |近乎即時進行。 |只有當 hello 工作完成時，才 hello 工作執行記錄可用。 |
| 檢視工作歷程記錄 |如果查詢是透過 HiveServer2 執行，系統將不會保留查詢的工作歷程記錄 (工作記錄檔、工作輸出)。 hello 應用程式可以檢視 YARN UI 中，使用有限的資訊。 |如果查詢是透過 WebHCat 執行，系統會保留查詢的工作歷程記錄 (工作記錄檔、工作輸出)，且可讓您使用 Visual Studio/HDInsight SDK/PowerShell 來檢視。 |
| 關閉視窗 |執行透過 HiveServer2 是 「 同步 」 的方式，因此您必須保持開啟的視窗; hello如果關閉 hello 視窗將會取消 hello 查詢執行。 |透過 WebHCat 提交是 「 非同步 」 的方式，因此您可以送出 hello 透過 WebHCat 的查詢，然後關閉 Visual Studio。 您可以返回並隨時查看 hello 結果。 |

### <a name="tez-hive-job-performance-graph"></a>Tez Hive 工作效能圖表
hello 資料湖工具支援顯示效能圖表 hello Hive 工作已執行由 hello Tez 執行引擎。 如需啟用 Tez 的資訊，請參閱[在 HDInsight 中使用 Hive](hdinsight-use-hive.md)。 之後您提交的 Hive 工作在 Visual Studio 中，Visual Studio 會顯示 hello 圖形，hello 工作完成時。  您可能需要 tooclick hello**重新整理**按鈕 tooget hello 最新的作業狀態。

> [!NOTE]
> 此功能只適用於高於 3.2.4.593 版的 HDInsight 叢集，而且只能用於已完成的工作 (如果您透過 WebHCat 提交作業，此圖形會在您透過 HiveServer2 執行查詢時顯示)。 這適用於以 Windows 和 Linux 為基礎的叢集。
> 
> 

![hadoop hive tez 效能圖](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "作業狀態")

toohelp 您了解您的 Hive 查詢更好，hello 工具加入 hello Hive 運算子檢視此版本中。 您只需要 toodouble 按一下 hello 頂點 hello 作業圖形的而且您可以看到所有 hello 運算子內 hello 頂點。 您可以也將滑鼠停留在特定運算子 tooview 這位操作員的詳細資料。

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Tez 工作上 Hive 的工作執行檢視
hello 工作執行檢視，可以使用在 Tez 工作上的登錄區 tooget 結構化和視覺化 Hive 工作的資訊及取得更多工作詳細資料。 效能問題時，您可以使用 hello 檢視 tooget 進一步詳細資料。 比方說，每項工作的運作方式，且 hello 詳細資訊 （資料讀取/寫入、 排程/開始/結束時間等），每個工作，以便您可以微調作業的設定或以視覺化方式檢視 hello 資訊為基礎的系統架構。

![Data Lake Visual Studio Tools 工作執行檢視](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "工作執行檢視")

## <a name="run-pig-scripts"></a>執行 Pig 指令碼
資料湖 Tools for Visual Studio 支援建立和提交 Pig 指令碼 tooHDInsight 叢集。 使用者可以 Pig 從範本建立專案，並再送出 hello 指令碼 tooHDInsight 叢集。

## <a name="feedbacks--known-issues"></a>意見反應和已知問題
* 目前 HiveServer2 結果會以純文字形式顯示，但不太理想。 我們正努力修正該問題。
* 如果 hello 結果會啟動具有 NULL 值，目前不會顯示 hello 結果。 我們已修正此問題，如果您被封鎖於此問題，則可以免費 toodrop 我們電子郵件或請連絡支援小組。
* Visual Studio 所建立的 hello HQL 指令碼是根據使用者的所在地區設定編碼。 如果使用者上傳 hello 指令碼 toocluster 為二進位，則它可能無法正確執行。

## <a name="next-steps"></a>後續步驟
在本文中，您學會 tooconnect tooHDInsight 從 Visual Studio 中，使用 hello Data Lake (HDInsight) 的叢集工具封裝，以及如何 toorun Hive 查詢。 如需詳細資訊，請參閱：

* [在 HDInsight 中使用 Hadoop Hive](hdinsight-use-hive.md)
* [開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)
* [在 HDInsight 上提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)
* [在 HDInsight 中使用 Hadoop 分析 Twitter 資料](hdinsight-analyze-twitter-data.md)

