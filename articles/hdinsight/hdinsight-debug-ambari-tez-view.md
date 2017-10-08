---
title: "aaaUse Ambari Tez 檢視與 HDInsight 的 Azure |Microsoft 文件"
description: "了解 toouse hello Ambari Tez HDInsight 上檢視 toodebug Tez 作業的方式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>HDInsight 上使用 Ambari 檢視 toodebug Tez 作業

hello Ambari Web UI hdinsight 包含 Tez 檢視可以使用使用 Tez toounderstand 和偵錯作業。 hello Tez 檢視可讓您 toovisualize hello 作業的已連接的項目圖形下鑽研至每個項目，以及擷取統計資料和記錄資訊。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 元件版本設定](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="prerequisites"></a>必要條件

* 以 Linux 為基礎的 HDInsight 叢集。 如需建立叢集的步驟，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。
* 支援 HTML5 的新式網頁瀏覽器。

## <a name="understanding-tez"></a>了解 Tez

Tez 是 Hadoop 中資料處理用的可延伸架構，資料處理的速度比傳統的 MapReduce 處理方式還要快。 以 Linux 為基礎的 HDInsight 叢集，則是 Hive hello 預設的引擎。

Tez 建立導向非循環圖 (DAG) 來描述 hello 順序的作業所需的動作。 個別的動作稱為頂點，和執行一段 hello 整體的作業。 hello 實際執行的 hello 頂點所描述的工作稱為工作，並可能散佈在 hello 叢集中的多個節點。

### <a name="understanding-hello-tez-view"></a>了解 hello Tez 檢視

hello Tez 檢視上執行的處理序中提供的歷程記錄資訊和資訊。 這項資訊顯示作業如何分散到叢集。 它也會顯示使用工作和頂點，計數器以及錯誤相關的資訊 toohello 作業。 它可能提供有用的資訊，在下列案例的 hello:

* 監視長時間執行處理程序，檢視 hello 對應的進度，並減少的工作。
* 分析成功或失敗的處理序 toolearn 歷程記錄資料，處理方式可提升或失敗的原因。

## <a name="generate-a-dag"></a>產生 DAG

hello Tez 檢視只包含資料，如果工作使用 hello Tez 引擎目前正在執行，或先前執行。 簡單的 Hive 查詢可不使用 Tez 進行解析。 複雜的查詢會執行諸如篩選、群組、排序、聯結等等 使用 hello Tez 引擎。

使用下列步驟 toorun 使用 Tez 的 Hive 查詢的 hello:

1. 在 web 瀏覽器中，瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME** hello 您的 HDInsight 叢集名稱。

2. 從 hello 頁面頂端的 hello hello 功能表上，選取 hello**檢視**圖示。 此圖示看起來像一系列正方形。 在出現的 hello 下拉式清單中選取**Hive 檢視**。

    ![選取 [Hive 檢視]](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. 當 hello Hive 檢視載入時，貼上 hello 以下查詢 hello 查詢編輯器中，並按一下**執行**。

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Hello 作業完成後，您應該會看到 hello 輸出顯示在 hello**查詢程序結果**> 一節。 hello 結果應該類似 toohello 下列文字：

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. 選取 hello**記錄** 索引標籤。您會看到下列文字的資訊類似 toohello:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    儲存 hello**應用程式識別碼**值，這個值用於 hello 下一節。

## <a name="use-hello-tez-view"></a>使用 hello Tez 檢視

1. 從 hello 頁面頂端的 hello hello 功能表上，選取 hello**檢視**圖示。 在出現的 hello 下拉式清單中選取**Tez 檢視**。

    ![選取 [Tez 檢視]](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Hello Tez 檢視載入時，您會看到一份目前正在執行，或者已被 hive 查詢執行 hello 叢集上。

    ![所有 DAG](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. 如果您有只有一個項目時，它是您已執行 hello 前一節中的 hello 查詢。 如果您有多個項目，您可以使用 hello 頁面頂端的 hello hello 欄位進行搜尋。

4. 選取 hello**查詢識別碼**Hive 查詢。 會顯示 hello 查詢的相關資訊。

    ![DAG 詳細資料](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. 此頁面上的 hello 索引標籤可讓您 tooview hello 下列資訊：

    * **查詢詳細資料**: hello Hive 查詢的相關詳細資料。
    * **時間軸**：每個處理階段所耗費時間的相關資訊。
    * **設定**: hello 組態用於這個查詢。

    從__查詢詳細資料__您可以使用 hello 連結 toofind hello 資訊__應用程式__或 hello __DAG__這個查詢。
    
    * hello__應用程式__連結顯示 hello 這個查詢的 YARN 應用程式的相關資訊。 您可以從這裡存取 hello YARN 應用程式記錄檔。
    * hello __DAG__連結顯示 hello 導向非循環的圖形這個查詢的相關資訊。 您可以從此處檢視 hello DAG 的圖形表示法。 您也可以尋找 hello DAG 中的 hello 頂點上的資訊。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何 toouse hello Tez 檢視，深入了解[HDInsight 上使用 Hive](hdinsight-use-hive.md)。

如需詳細 Tez 上的技術資訊，請參閱 hello [Hortonworks Tez 頁面](http://hortonworks.com/hadoop/tez/)。

在 HDInsight 中使用 Ambari 的詳細資訊，請參閱[使用 hello Ambari Web UI 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)
