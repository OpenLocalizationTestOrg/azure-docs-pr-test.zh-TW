---
title: "以 Windows 為基礎的 HDInsight 的 Azure Tez UI aaaUse |Microsoft 文件"
description: "了解 toouse hello Tez UI toodebug Tez Windows 為基礎的 HDInsight HDInsight 上的工作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>使用 Windows 為基礎的 HDInsight 上的 hello Tez UI toodebug Tez 工作
hello Tez UI 是可以使用的 toounderstand 和偵錯工作 Tez 作為 hello 執行引擎在 Windows 為基礎的 HDInsight 叢集上的網頁。 hello Tez UI 允許 toovisualize hello 工作的已連接的項目圖形下鑽研至每個項目，以及擷取統計資料和記錄資訊。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Windows 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="prerequisites"></a>必要條件
* 以 Windows 為基礎的 HDInsight 叢集。 如需建立新叢集的步驟，請參閱 [開始使用以 Windows 為基礎的 HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md)。

  > [!IMPORTANT]
  > 只有在 2016 年 2 月 8 日之後建立的 Windows 為基礎的 HDInsight 叢集上使用 hello Tez UI。
  >
  >
* 以 Windows 為基礎的遠端桌面用戶端。

## <a name="understanding-tez"></a>了解 Tez
Tez 是 Hadoop 中資料處理用的可延伸架構，資料處理的速度比傳統的 MapReduce 處理方式還要快。 Windows 為基礎的 HDInsight 叢集，它是選擇性的引擎，您可以使用下列命令為 Hive 查詢的一部份的 hello 啟用登錄區：

    set hive.execution.engine=tez;

已提交的 tooTez 工作時，它會建立導向非循環圖 (DAG) 描述 hello hello 作業所需的 hello 動作的執行順序。 個別的動作稱為頂點，和執行一段 hello 整體的作業。 hello 實際執行的 hello 頂點所描述的工作稱為工作，並可能散佈在 hello 叢集中的多個節點。

### <a name="understanding-hello-tez-ui"></a>了解 hello Tez UI
hello Tez UI 是 web 網頁會提供有關處理序正在執行，或有先前執行的使用 Tez。 它可讓您 tooview hello Tez，所產生的 DAG 如何分散在叢集中，例如工作和頂點，錯誤訊息所使用的記憶體計數器。 它可能提供有用的資訊，在下列案例的 hello:

* 監視長時間執行處理程序，檢視 hello 對應的進度，並減少的工作。
* 分析成功或失敗的處理序 toolearn 歷程記錄資料，處理方式可提升或失敗的原因。

## <a name="generate-a-dag"></a>產生 DAG
如果工作使用 hello 的 Tez 引擎目前正在執行，或已在過去的 hello 已執行 hello Tez UI 只會包含資料。 簡單的 Hive 查詢通常不用 Tez 就能解決，但更複雜的查詢 (會進行篩選、分組、排序、 聯結等) 通常需要使用 Tez。

使用下列步驟 toorun Hive 查詢將會執行使用 Tez hello。

1. 在 web 瀏覽器中，瀏覽 toohttps://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME** hello 您的 HDInsight 叢集名稱。
2. 從 hello 頁面頂端的 hello hello 功能表上，選取 hello**登錄區編輯器**。 這會顯示頁面，以下列範例查詢中的 hello。

        Select * from hivesampletable

    清除 hello 範例查詢，並以 hello 下列取代它。

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. 選取 hello**送出** 按鈕。 hello**作業工作階段**在 hello hello 頁面底部的區段會顯示 hello hello 查詢狀態。 一次太 hello 狀態變更**已完成**，選取 hello**檢視詳細資料**連結 tooview hello 結果。 hello**作業輸出**應該類似 toohello 下列：

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>使用 hello Tez UI
> [!NOTE]
> hello Tez UI 才可用從 hello 桌面 hello 叢集前端節點，因此您必須使用遠端桌面 tooconnect toohello 前端節點。
>
>

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取您的 HDInsight 叢集。 從 hello hello HDInsight 刀鋒視窗頂端，選取 hello**遠端桌面**圖示。 這會顯示 hello 遠端桌面刀鋒視窗

    ![遠端桌面圖示](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. 從 hello 遠端桌面刀鋒視窗中，選取**連接**tooconnect toohello 叢集前端節點。 出現提示時，使用 hello 叢集遠端桌面使用者名稱和密碼 tooauthenticate hello 連線。

    ![遠端桌面連線圖示](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > 如果您未啟用遠端桌面連線，提供使用者名稱、 密碼以及到期日，然後選取 **啟用**tooenable 遠端桌面。 已啟用它，一旦使用上一個步驟 tooconnect hello。
   >
   >
3. 一旦連接之後，在 hello 遠端桌面上，hello 右上角 hello 瀏覽器中，選取 hello 齒輪圖示開啟 Internet Explorer，然後選取**相容性檢視設定**。
4. 從 hello 底部**相容性檢視設定**，清除 hello 核取方塊**在相容性檢視中顯示的內部網路網站**和**使用 Microsoft 相容性清單**，然後選取**關閉**。
5. 在 Internet Explorer 中，瀏覽 toohttp://headnodehost:8188/tezui / #/。 這會顯示 hello Tez UI

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    Hello Tez UI 載入時，您會看到一份目前正在執行，或者已被 Dag 執行 hello 叢集上。 hello 預設檢視包含 hello Dag 名稱、 識別碼、 傳送者、 狀態、 開始時間、 結束時間、 持續時間、 應用程式識別碼和佇列。 可以在 hello hello 頁面的右邊使用 hello 齒輪圖示加入更多的資料行。

    如果您有只有一個項目，即是您已執行 hello 前一節中的 hello 查詢。 如果您有多個項目，您可以搜尋 hello hello Dag，上面的欄位中輸入搜尋準則，然後叫用**Enter**。
6. 選取 hello **Dag 名稱**hello 最近 DAG 項目。 這會顯示 hello DAG，及 hello 選項 toodownload zip 包含 hello DAG 的相關資訊的 JSON 檔案的相關資訊。

    ![DAG 詳細資料](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. 上述 hello **DAG 詳細資料**是數個可以使用的 toodisplay hello DAG 資訊的連結。

   * [DAG 計數器] 顯示此 DAG 的計數器資訊。
   * [圖形檢視] 顯示此 DAG 的圖形表示。
   * **所有的頂點**顯示此 DAG 中的 hello 頂點清單。
   * **所有工作**此 DAG 中顯示的所有頂點的 hello 工作清單。
   * **所有 TaskAttempts** hello 的顯示資訊的這個 DAG 嘗試 toorun 工作。

     > [!NOTE]
     > 當您捲動頂點、 工作和 TaskAttempts hello 資料行顯示，請注意，有連結 tooview**計數器**和**檢視或下載記錄檔**每個資料列。
     >
     >

     如果發生與 hello 作業失敗，hello DAG 詳細資料會顯示失敗狀態以及連結 tooinformation hello 失敗的工作有關。 下方 hello DAG 詳細資料，將會顯示診斷資訊。
8. 選取 [圖形檢視]。 這會顯示 hello DAG 的圖形表示法。 您可以透過在 hello 檢視 toodisplay 資訊中的每個頂點放置 hello 滑鼠。

    ![圖形檢視](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. 按一下 上一個頂點會載入 hello**端點詳細資料**該項目。 按一下 hello**對應 1**頂點 toodisplay 詳細資料，此項目。 選取**確認**tooconfirm hello 瀏覽。

    ![頂點詳細資料](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. 請注意現在有 hello 頁面頂端的 hello 相關的 toovertices 和工作的連結。

    > [!NOTE]
    > 您可以也到達此頁面移回太**DAG 詳細資料**、 選取**端點詳細資料**，然後選取 hello**對應 1**頂點。
    >
    >

    * [頂點計數器] 顯示此頂點的計數器資訊。
    * [工作] 顯示此頂點的工作。
    * **工作嘗試**顯示此頂點嘗試 toorun 工作的相關資訊。
    * [來源與接收] 顯示此頂點的資料來源和接收。

      > [!NOTE]
      > 當與 hello 上一個功能表，您可以捲動 hello 資料行顯示的工作時，工作嘗試，以及來源和 Sinks__ toodisplay 連結 toomore 資訊每個項目。
      >
      >
11. 選取**工作**，接著選取 hello 項目是具名**00_000000**。 這會顯示這項工作的 [工作詳細資料]。 在此畫面中，您可以檢視 [工作計數器] 和 [工作嘗試]。

    ![作業詳細資料](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>後續步驟
既然您已經學會如何 toouse hello Tez 檢視，深入了解[HDInsight 上使用 Hive](hdinsight-use-hive.md)。

如需詳細 Tez 上的技術資訊，請參閱 hello [Hortonworks Tez 頁面](http://hortonworks.com/hadoop/tez/)。
