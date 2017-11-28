---
title: "與 HDInsight (Hadoop)-Azure 上的登錄區 aaaUse Ambari 檢視 toowork |Microsoft 文件"
description: "了解 toouse hello Hive 檢視從您網頁瀏覽器 toosubmit Hive 查詢的方式。 hello hive 控制檔的檢視是的 hello Ambari Web UI 隨附以 Linux 為基礎的 HDInsight 叢集的一部分。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="5149e-104">使用 hello HDInsight 中的 Hadoop hive 控制檔的檢視</span><span class="sxs-lookup"><span data-stu-id="5149e-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="5149e-105">了解如何 toorun Hive 查詢使用 Ambari hive 控制檔的檢視。</span><span class="sxs-lookup"><span data-stu-id="5149e-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="5149e-106">Ambari 是隨著以 Linux 為基礎的 HDInsight 叢集提供的管理和監視公用程式。</span><span class="sxs-lookup"><span data-stu-id="5149e-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="5149e-107">Ambari 透過提供的 hello 功能之一是 Web UI，它可以是使用的 toorun Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5149e-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="5149e-108">Ambari 有許多本文未討論到的功能。</span><span class="sxs-lookup"><span data-stu-id="5149e-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="5149e-109">如需詳細資訊，請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="5149e-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5149e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5149e-110">Prerequisites</span></span>

* <span data-ttu-id="5149e-111">以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5149e-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5149e-112">如需建立叢集的相關資訊，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="5149e-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5149e-113">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5149e-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5149e-114">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="5149e-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5149e-115">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5149e-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="5149e-116">開啟 hello 登錄區檢視</span><span class="sxs-lookup"><span data-stu-id="5149e-116">Open hello Hive view</span></span>

<span data-ttu-id="5149e-117">您可以從 Azure 入口網站; hello 的 Ambari 檢視選取您的 HDInsight 叢集，然後選取**Ambari 檢視**從 hello**快速連結**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5149e-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![hello 入口網站的快速連結 區段](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="5149e-119">從 hello 清單中的檢視，選取 hello __Hive 檢視__。</span><span class="sxs-lookup"><span data-stu-id="5149e-119">From hello list of views, select hello __Hive View__.</span></span>

![hello 所選取的登錄區檢視](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="5149e-121">在存取 Ambari，即提示的 tooauthenticate toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="5149e-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="5149e-122">輸入 hello admin (預設`admin`) 帳戶名稱和您建立時使用的密碼 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="5149e-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="5149e-123">您應該會看到下列映像頁面類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="5149e-123">You should see a page similar toohello following image:</span></span>

![Hello hello 登錄區檢視的查詢工作表的映像](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="5149e-125"><a name="hivequery"></a>執行查詢</span><span class="sxs-lookup"><span data-stu-id="5149e-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="5149e-126">toorun hive 查詢，使用 hello hello 登錄區檢視中的下列步驟。</span><span class="sxs-lookup"><span data-stu-id="5149e-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="5149e-127">從 hello__查詢__索引標籤中，貼上下列 HiveQL 陳述式 hello 工作表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="5149e-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="5149e-128">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="5149e-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5149e-129">`DROP TABLE`-刪除 hello 資料表與 hello 資料檔，萬一 hello 資料表已經存在。</span><span class="sxs-lookup"><span data-stu-id="5149e-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="5149e-130">`CREATE EXTERNAL TABLE` - 在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="5149e-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="5149e-131">外部資料表儲存區中的 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="5149e-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="5149e-132">hello 資料會保留在 hello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="5149e-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="5149e-133">`ROW FORMAT`的 hello 資料格式化方式。</span><span class="sxs-lookup"><span data-stu-id="5149e-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="5149e-134">在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="5149e-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="5149e-135">`STORED AS TEXTFILE LOCATION`-Hello 儲存資料，並儲存成文字。</span><span class="sxs-lookup"><span data-stu-id="5149e-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="5149e-136">`SELECT`-選取其中的資料行 t4 包含 hello 值 [錯誤] 的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="5149e-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="5149e-137">當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="5149e-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="5149e-138">例如，自動化的資料上傳程序，或透過其他 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="5149e-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="5149e-139">卸除的外部資料表沒有*不*刪除 hello 資料、 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="5149e-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5149e-140">保留 hello__資料庫__選取項目在__預設__。</span><span class="sxs-lookup"><span data-stu-id="5149e-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="5149e-141">本文件中的 hello 範例會使用隨附 HDInsight hello 預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="5149e-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="5149e-142">toostart hello 查詢，使用 hello **Execute**下方 hello 工作表 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5149e-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="5149e-143">會呈現橙色和 hello 文字變更太**停止**。</span><span class="sxs-lookup"><span data-stu-id="5149e-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="5149e-144">Hello 查詢完成時，一旦 hello**結果**索引標籤會顯示 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="5149e-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="5149e-145">下列文字的 hello 是 hello hello 查詢結果：</span><span class="sxs-lookup"><span data-stu-id="5149e-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="5149e-146">hello**記錄** 索引標籤可以是使用的 tooview hello 工作所建立的 hello 記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="5149e-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="5149e-147">hello**將結果儲存**中 hello 上方的下拉式清單對話方塊方 hello**查詢程序結果**區段可讓您 toodownload 或儲存結果。</span><span class="sxs-lookup"><span data-stu-id="5149e-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="5149e-148">選取 hello 前四行的這項查詢，然後選取**Execute**。</span><span class="sxs-lookup"><span data-stu-id="5149e-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="5149e-149">請注意，沒有結果 hello 作業完成時。</span><span class="sxs-lookup"><span data-stu-id="5149e-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="5149e-150">使用 hello **Execute**按鈕時 hello 查詢的一部分時，才執行 hello 選陳述式選取。</span><span class="sxs-lookup"><span data-stu-id="5149e-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="5149e-151">在此情況下，hello 選取範圍沒有包含 hello 最終的陳述式會從 hello 資料表擷取資料列。</span><span class="sxs-lookup"><span data-stu-id="5149e-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="5149e-152">如果您選取只在該行，並使用**Execute**，您應該會看到 hello 預期結果。</span><span class="sxs-lookup"><span data-stu-id="5149e-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="5149e-153">tooadd 工作表中，使用 hello**新工作表**在 hello hello 底部的按鈕**查詢編輯器**。</span><span class="sxs-lookup"><span data-stu-id="5149e-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="5149e-154">Hello 新工作表中輸入下列 HiveQL 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="5149e-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="5149e-155">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="5149e-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="5149e-156">**CREATE TABLE IF NOT EXISTS** - 建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="5149e-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="5149e-157">因為 hello**外部**不是關鍵字，會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="5149e-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="5149e-158">內部資料表會儲存在 hello Hive 資料倉儲和 Hive 完全管理。</span><span class="sxs-lookup"><span data-stu-id="5149e-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="5149e-159">不同於外部資料表，卸除內部資料表，將會刪除 hello 基礎資料。</span><span class="sxs-lookup"><span data-stu-id="5149e-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="5149e-160">**儲存 AS ORC** -hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。</span><span class="sxs-lookup"><span data-stu-id="5149e-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="5149e-161">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="5149e-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="5149e-162">**INSERT OVERWRITE ...選取**-選取資料列從 hello **log4jLogs**包含資料表`[ERROR]`，然後插入 hello 資料到 hello 和**錯誤記錄檔**資料表。</span><span class="sxs-lookup"><span data-stu-id="5149e-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="5149e-163">使用 hello **Execute**按鈕 toorun 此查詢。</span><span class="sxs-lookup"><span data-stu-id="5149e-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="5149e-164">hello**結果**hello 查詢傳回零個資料列時 索引標籤不包含任何資訊。</span><span class="sxs-lookup"><span data-stu-id="5149e-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="5149e-165">hello 狀態應顯示為**SUCCEEDED** hello 查詢完成後。</span><span class="sxs-lookup"><span data-stu-id="5149e-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="5149e-166">視覺解說</span><span class="sxs-lookup"><span data-stu-id="5149e-166">Visual explain</span></span>

<span data-ttu-id="5149e-167">toodisplay 視覺效果的 hello 查詢計畫中，選取 hello **Visual 說明**下方 hello 工作表的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5149e-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="5149e-168">hello **Visual 說明**hello 查詢的檢視可能有助於瞭解 hello 流向複雜的查詢。</span><span class="sxs-lookup"><span data-stu-id="5149e-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="5149e-169">您可以檢視此檢視的文字對等項目使用 hello**解釋**hello 查詢編輯器中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5149e-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="5149e-170">Tez UI</span><span class="sxs-lookup"><span data-stu-id="5149e-170">Tez UI</span></span>

<span data-ttu-id="5149e-171">toodisplay hello Tez UI hello 查詢中，選取 hello **Tez**下方 hello 工作表的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5149e-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5149e-172">Tez 是未使用的 tooresolve 所有查詢。</span><span class="sxs-lookup"><span data-stu-id="5149e-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="5149e-173">您不需要使用 Tez 便可解析許多查詢。</span><span class="sxs-lookup"><span data-stu-id="5149e-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="5149e-174">如果 Tez 使用的 tooresolve hello 查詢導向非循環圖 (DAG) 會顯示的 hello。</span><span class="sxs-lookup"><span data-stu-id="5149e-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="5149e-175">如果您需要 tooview hello DAG 的查詢，您已在過去，hello 執行或偵錯 hello Tez 程序，使用 hello [Tez 檢視](hdinsight-debug-ambari-tez-view.md)改為。</span><span class="sxs-lookup"><span data-stu-id="5149e-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="5149e-176">檢視工作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="5149e-176">View job history</span></span>

<span data-ttu-id="5149e-177">hello__作業__索引標籤會顯示的 Hive 查詢歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="5149e-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Hello 作業歷程記錄的映像](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="5149e-179">資料庫資料表</span><span class="sxs-lookup"><span data-stu-id="5149e-179">Database tables</span></span>

<span data-ttu-id="5149e-180">您可以使用 hello__資料表__toowork Hive 資料庫內的資料表與索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="5149e-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Hello 資料表索引標籤的映像](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="5149e-182">儲存的查詢</span><span class="sxs-lookup"><span data-stu-id="5149e-182">Saved queries</span></span>

<span data-ttu-id="5149e-183">從 hello 查詢索引標籤上，您可以選擇儲存查詢。</span><span class="sxs-lookup"><span data-stu-id="5149e-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="5149e-184">儲存之後，您可以重複使用 hello 查詢從 hello__儲存查詢__ 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5149e-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![[儲存的查詢] 索引標籤影像](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="5149e-186">使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="5149e-186">User-defined functions</span></span>

<span data-ttu-id="5149e-187">您也可以透過使用者定義函數 (UDF) 擴充 Hive。</span><span class="sxs-lookup"><span data-stu-id="5149e-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="5149e-188">UDF 可讓您 tooimplement 功能或 HiveQL 不容易模型化的邏輯。</span><span class="sxs-lookup"><span data-stu-id="5149e-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="5149e-189">hello UDF 索引標籤頂端的 hello Hive 檢視 hello 可讓您 toodeclare 和儲存一組的 Udf。</span><span class="sxs-lookup"><span data-stu-id="5149e-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="5149e-190">這些 Udf 可以搭配 hello**查詢編輯器**。</span><span class="sxs-lookup"><span data-stu-id="5149e-190">These UDFs can be used with hello **Query Editor**.</span></span>

![[UDF] 索引標籤影像](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="5149e-192">一旦您加入 UDF toohello hive 控制檔 檢視中，**插入 udf**按鈕會出現在 hello 底部 hello**查詢編輯器**。</span><span class="sxs-lookup"><span data-stu-id="5149e-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="5149e-193">選取此項目會顯示 hello hello hive 控制檔 檢視中定義的 Udf 的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5149e-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="5149e-194">選取的 UDF 會加入下列 HiveQL 陳述式 tooyour 查詢 tooenable hello UDF。</span><span class="sxs-lookup"><span data-stu-id="5149e-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="5149e-195">例如，如果您已經定義 UDF 以 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5149e-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="5149e-196">資源名稱：myudfs</span><span class="sxs-lookup"><span data-stu-id="5149e-196">Resource name: myudfs</span></span>

* <span data-ttu-id="5149e-197">資源路徑︰/myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="5149e-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="5149e-198">UDF 名稱：myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="5149e-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="5149e-199">UDF 類別名稱：com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="5149e-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="5149e-200">使用 hello**插入 udf**按鈕會顯示名為的項目**myudfs**，與另一個下拉式清單的每個 UDF 定義該資源。</span><span class="sxs-lookup"><span data-stu-id="5149e-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="5149e-201">在此案例中為 **myawesomeudf**。</span><span class="sxs-lookup"><span data-stu-id="5149e-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="5149e-202">選取此項目就會加入下列 toohello 開頭 hello 查詢 hello:</span><span class="sxs-lookup"><span data-stu-id="5149e-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="5149e-203">然後，您可以在查詢中使用 hello UDF。</span><span class="sxs-lookup"><span data-stu-id="5149e-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="5149e-204">例如： `SELECT myawesomeudf(name) FROM people;`。</span><span class="sxs-lookup"><span data-stu-id="5149e-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="5149e-205">如需有關如何使用 Udf 與 HDInsight 上的登錄區的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="5149e-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="5149e-206">在 HDInsight 中搭配 Hive 與 Pig 使用 Python</span><span class="sxs-lookup"><span data-stu-id="5149e-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="5149e-207">如何自訂的 Hive UDF tooHDInsight tooadd</span><span class="sxs-lookup"><span data-stu-id="5149e-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="5149e-208">Hive 設定</span><span class="sxs-lookup"><span data-stu-id="5149e-208">Hive settings</span></span>

<span data-ttu-id="5149e-209">設定可以是使用的 toochange Hive 的各種設定。</span><span class="sxs-lookup"><span data-stu-id="5149e-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="5149e-210">例如，變更 Hive 從 Tez （hello 預設值） tooMapReduce hello 執行引擎。</span><span class="sxs-lookup"><span data-stu-id="5149e-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="5149e-211"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="5149e-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5149e-212">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="5149e-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="5149e-213">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5149e-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="5149e-214">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="5149e-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5149e-215">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5149e-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5149e-216">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5149e-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
