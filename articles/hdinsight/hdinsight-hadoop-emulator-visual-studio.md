---
title: "適用於 Visual Studio 與 Hortonworks 沙箱-Azure HDInsight aaaData Lake 工具 |Microsoft 文件"
description: "了解如何 toouse hello for Visual Studio 與 hello Hortonworks 沙箱本機 VM 中執行 Azure 資料湖工具。 您可以使用這些工具來建立及 hello 沙箱，以及檢視工作的輸出和記錄上執行 Hive 和 Pig 工作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Hello Azure 資料湖 tools for Visual Studio 使用 hello Hortonworks 沙箱

Azure Data Lake 包含使用於一般 Hadoop 叢集的工具。 本文件提供 hello 步驟需要 toouse hello Data Lake 工具與 hello Hortonworks 沙箱本機的虛擬機器中執行。

使用 hello Hortonworks 沙箱可讓您在本機開發環境上的 Hadoop toowork。 您已經開發了解決方案，並想 toodeploy 之後它在標尺，您可以再移動 tooan HDInsight 叢集。

## <a name="prerequisites"></a>必要條件

* hello Hortonworks 沙箱，您的開發環境上執行的虛擬機器中。 本文件所撰寫，並與 hello 沙箱 Oracle VirtualBox 中執行測試。 如需 hello 沙箱設定資訊，請參閱 hello [hello Hortonworks 沙箱快速入門。](hdinsight-hadoop-emulator-get-started.md) 文件。

* Visual Studio 2013、Visual Studio 2015 或 Visual Studio 2017 (任一版本)。

* hello [Azure SDK for.NET](https://azure.microsoft.com/downloads/) 2.7.1 或更新版本。

* hello [Azure 資料湖 tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)。

## <a name="configure-passwords-for-hello-sandbox"></a>設定密碼 hello 沙箱

請確定該 hello Hortonworks 沙箱正在執行。 然後遵循 hello 中的 hello 步驟[開始 hello Hortonworks 沙箱](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords)文件。 下列步驟設定 hello hello SSH 密碼`root`帳戶，而且 hello Ambari`admin`帳戶。 當您從 Visual Studio 連接 toohello 沙箱時，會使用這些密碼。

## <a name="connect-hello-tools-toohello-sandbox"></a>連接 hello 工具 toohello 沙箱

1. 開啟 Visual Studio，選取 [檢視]，然後選取 [伺服器總管]。

2. 從**伺服器總管**，以滑鼠右鍵按一下 hello **HDInsight**項目，然後選取**連接 tooHDInsight 模擬器**。

    ![螢幕擷取畫面的伺服器總管 中，與連接 tooHDInsight 反白顯示的模擬器](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. 從 hello**連接 tooHDInsight 模擬器**對話方塊方塊中，輸入您設定如 Ambari hello 密碼。

    ![對話方塊的螢幕擷取畫面，其中密碼文字方塊已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    選取**下一步**toocontinue。

4. 使用 hello**密碼**欄位 tooenter hello 密碼在您設定 hello`root`帳戶。 保留 hello hello 預設值的其他欄位。

    ![對話方塊的螢幕擷取畫面，其中密碼文字方塊已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    選取**下一步**toocontinue。

5. 等候 hello 服務 toofinish 的驗證。 在某些情況下，驗證可能失敗，而且提示您 tooupdate hello 組態。 如果驗證失敗時，選取**更新**，並等候 hello 設定及驗證 hello 服務 toofinish。

    ![對話方塊的螢幕擷取畫面，其中 [更新] 按鈕已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > hello 更新程序會使用 Ambari toomodify hello Hortonworks 沙箱組態 toowhat 所預期的 hello Data Lake tools for Visual Studio。

6. 驗證已完成之後，請選取**完成**toocomplete 組態。
    ![對話方塊的螢幕擷取畫面，其中 [完成] 按鈕已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > 根據您的開發環境和 hello 配置 toohello 虛擬機器記憶體的數量 hello 速度，它可以花幾分鐘的時間 tooconfigure 並驗證 hello 服務。

執行這些步驟之後，您現在可以**HDInsight 本機叢集**hello] 下的項目在 [伺服器總管**HDInsight** > 一節。

## <a name="write-a-hive-query"></a>撰寫 Hive 查詢

Hive 會提供類似 SQL 的查詢語言 (HiveQL)，以便處理結構化資料。 使用 hello 遵循步驟 toolearn toorun 隨 hello 本機叢集對查詢的方式。

1. 在**伺服器總管**，hello hello 本機叢集之前，加入的項目上按一下滑鼠右鍵，然後選取**撰寫 Hive 查詢**。

    ![[伺服器總管] 的螢幕擷取畫面，其中 [撰寫 Hive 查詢] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    新的查詢視窗隨即開啟。 這裡您可以快速地撰寫並送出查詢 toohello 本機叢集。

2. 在 hello 新查詢視窗中，輸入下列命令的 hello:

        select count(*) from sample_08;

    toorun hello 查詢中，選取**送出**hello hello 視窗上方。 保留 hello 其他值 (**批次**和伺服器名稱) 在 hello 預設值。

    ![查詢視窗中，強調顯示 hello 送出按鈕的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    您也可以使用 hello 下拉式選單接下來太**送出**tooselect**進階**。 進階的選項可讓您 tooprovide 其他選項時您送出 hello 作業。

    ![[提交指令碼] 對話方塊的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. 您送出 hello 查詢之後，會顯示 hello 作業狀態。 在處理 Hadoop 所 hello 工作狀態會顯示 hello 工作的相關資訊。 **工作狀態**提供 hello hello 工作狀態。 hello 狀態會定期更新，或者您可以使用 hello 重新整理圖示 toorefresh hello 狀態以手動方式。

    ![[作業檢視] 對話方塊的螢幕擷取畫面，其中 [作業狀態] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    之後 hello**工作狀態**變更太**已經完成**，導向非循環圖 (DAG) 會顯示。 此圖說明處理 hello Hive 查詢時，已由 Tez 的 hello 執行路徑。 Tez 是 hello 預設執行引擎 Hive hello 本機叢集上。

    > [!NOTE]
    > Tez 也是 hello 預設值，當您使用 linux 的 HDInsight 叢集。 它不是 hello Windows 為基礎的 HDInsight 上的預設值。 toouse 它，您必須新增 hello 列`set hive.execution.engine = tez;`toohello Hive 查詢的開頭。

    使用 hello**作業輸出**連結 tooview hello 輸出。 在此情況下，它是 823 hello hello sample_08 資料表中資料列數目。 您可以檢視 hello 工作的相關診斷資訊使用 hello**作業記錄**和**下載 YARN 記錄**連結。

4. 您也可以執行 Hive 工作以互動方式變更 hello**批次**欄位太**互動式**。 接著，選取 [執行]。

    ![[互動式] 與 [執行] 按鈕已反白顯示的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    資料流 hello 處理 toohello 期間所產生的輸出記錄檔的互動式查詢**HiveServer2 輸出**視窗。

    > [!NOTE]
    > hello 資訊是 hello 相同可從 hello**作業記錄**連結作業完成之後。

    ![輸出記錄的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>建立 Hive 專案

您也可以建立包含多個 Hive 指令碼的專案。 當您將相關的指令碼，或想 toostore 指令碼在版本控制系統，請使用專案。

1. 在 Visual Studio 中，選取 [檔案]、[新增]，然後選取 [專案]。

2. 從 hello 專案清單中，展開**範本**，依序展開**Azure 資料湖**，然後選取**HIVE (HDInsight)**。 從範本 hello 清單，選取**hive 控制檔的範例**。 輸入名稱和位置，然後選取 [確定]。

    ![[新增專案] 視窗的螢幕擷取畫面，其中 [Azure Data Lake]、[HIVE]、[Hive 範例] 與 [確定] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

hello **hive 控制檔的範例**專案包含兩個指令碼， **WebLogAnalysis.hql**和**SensorDataAnalysis.hql**。 您可以送出使用這些指令碼 hello 相同**送出**hello hello 視窗上方的按鈕。

## <a name="create-a-pig-project"></a>建立 Pig 專案

Hive 提供類似 SQL 的語言來處理結構化的資料，Pig 的運作方式是藉由對資料執行轉換。 Pig 提供可讓您 toodevelop 的語言 （Pig 拉丁） 轉換的管線。 toouse Pig 與 hello 本機叢集，請遵循下列步驟：

1. 開啟 Visual Studio，並依序選取 [檔案] > [新增] 和 [專案]。 從 hello 專案清單中，展開**範本**，依序展開**Azure 資料湖**，然後選取**Pig (HDInsight)**。 從範本 hello 清單，選取**Pig 應用程式**。 輸入名稱、位置，然後選取 [確定]。

    ![[新增專案] 視窗的螢幕擷取畫面，其中 [Azure Data Lake]、[Pig]、[Pig 應用程式] 與 [確定] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. 輸入下列文字，做為 hello 內容的 hello hello **script.pig**與此專案所建立的檔案。

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    而 Pig Hive 比使用不同的語言，您要執行 hello 作業的方式之間會保持一致這兩種語言，透過 hello**送出** 按鈕。 選取 hello 旁邊的下拉式清單**送出**Pig 顯示進階送出 對話方塊。

    ![[提交指令碼] 對話方塊的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. 也會顯示 hello 工作狀態和輸出，做為 Hive 查詢 hello 相同。

    ![已完成 Pig 作業的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>檢視作業

資料湖工具也可讓您 tooeasily 檢視已在 Hadoop 執行的作業有關的資訊。 使用下列步驟 toosee hello 工作已執行 hello 本機叢集上的 hello。

1. 從**伺服器總管**，hello 本機叢集，以滑鼠右鍵按一下，然後選取**檢視工作**。 已提交的 toohello 叢集中的作業清單隨即出現。

    ![[伺服器總管] 的螢幕擷取畫面，其中 [檢視作業] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. 從 hello 工作清單，選取其中一個 tooview hello 工作詳細資料。

    ![螢幕擷取畫面的作業瀏覽器中，使用其中一個 hello 反白顯示的作業](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    執行 Hive 或 Pig 查詢，包括連結 tooview hello 輸出和記錄檔資訊之後，您看見類似 toowhat 所顯示的 hello 資訊。

3. 您也可以修改並重新送出 hello 作業，從這裡。

## <a name="view-hive-databases"></a>檢視 Hive 資料庫

1. 在**伺服器總管**，展開 hello **HDInsight 本機叢集**項目，然後展開**Hive 資料庫**。 hello**預設**和**xademo**會顯示 hello 本機叢集上的資料庫。 展開資料庫顯示 hello hello 資料庫內的資料表。

    ![[伺服器總管] 的螢幕擷取畫面，其中資料庫已展開](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. 展開資料表，會顯示 hello 該資料表的資料行。 hello tooquickly 檢視的資料，以滑鼠右鍵按一下資料表，然後選取**檢視前 100 個資料列**。

    ![[伺服器總管] 的螢幕擷取畫面，其中資料表已展開且 [檢視前 100 個資料列] 已選取](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>資料庫和資料表屬性

您可以檢視資料庫或資料表的 hello 的屬性。 選取**屬性**hello 屬性 視窗中顯示 hello 選取項目的詳細資料。 例如，請參閱 hello 資訊 hello 下列螢幕擷取畫面所示：

![[屬性] 視窗的螢幕擷取畫面](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>建立資料表

toocreate 資料表，以滑鼠右鍵按一下資料庫，然後選取**Create Table**。

![[伺服器總管] 的螢幕擷取畫面，其中 [建立資料表] 已反白顯示](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

然後，您可以建立 hello 資料表使用的表單。 您可以在 hello hello 下列螢幕擷取畫面底部，查看 hello 原始 HiveQL 使用的 toocreate hello 資料表。

![螢幕擷取畫面的 hello 表單使用 toocreate 資料表](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>後續步驟

* [學習 hello ropes 的 hello Hortonworks 沙箱](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop 教學課程 - 開始使用 HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
