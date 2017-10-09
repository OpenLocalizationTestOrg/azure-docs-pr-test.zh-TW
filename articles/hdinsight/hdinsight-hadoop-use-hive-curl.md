---
title: "使用 Curl HDInsight 的 Azure 中的 Hadoop Hive aaaUse |Microsoft 文件"
description: "了解如何 tooremotely 提交 Pig 工作 tooHDInsight 使用 Curl。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="f42ea-103">使用 REST 以 HDInsight 中的 Hadoop 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="f42ea-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="f42ea-104">了解如何 toouse hello WebHCat REST API toorun Hive 查詢的 Hadoop 上的 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f42ea-104">Learn how toouse hello WebHCat REST API toorun Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="f42ea-105">[Curl](http://curl.haxx.se/)是使用的 toodemonstrate 如何您可以使用與互動 HDInsight 未經處理的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="f42ea-105">[Curl](http://curl.haxx.se/) is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="f42ea-106">hello [jq](http://stedolan.github.io/jq/)公用程式是使用的 tooprocess REST 要求所傳回的 hello JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="f42ea-106">hello [jq](http://stedolan.github.io/jq/) utility is used tooprocess hello JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="f42ea-107">如果您已熟悉使用 linux Hadoop 伺服器，但新 tooHDInsight，請參閱 hello[配備相關以 Linux 為基礎的 HDInsight 上的 Hadoop tooknow](hdinsight-hadoop-linux-information.md)文件。</span><span class="sxs-lookup"><span data-stu-id="f42ea-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see hello [What you need tooknow about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="f42ea-108"><a id="curl"></a>執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="f42ea-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="f42ea-109">當使用 WebHCat cURL 或任何其他的 REST 通訊，您必須驗證 hello 要求藉由提供 hello 使用者名稱和 hello HDInsight 叢集系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="f42ea-109">When using cURL or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="f42ea-110">本章節中的 hello 命令，請將**USERNAME** hello 使用者 tooauthenticate toohello 叢集與取代**密碼**hello hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="f42ea-110">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="f42ea-111">取代**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="f42ea-111">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="f42ea-112">hello REST API 會透過保護[基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。</span><span class="sxs-lookup"><span data-stu-id="f42ea-112">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="f42ea-113">toohelp 確保您的認證會安全地傳送 toohello 伺服器，請務必要求使用安全 HTTP (HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="f42ea-113">toohelp ensure that your credentials are securely sent toohello server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="f42ea-114">從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="f42ea-114">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="f42ea-115">您會收到回應類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="f42ea-115">You receive a response similar toohello following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="f42ea-116">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="f42ea-116">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="f42ea-117">**-u** -使用 tooauthenticate hello 要求 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f42ea-117">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="f42ea-118">**-G** - 指出此要求是 GET 作業。</span><span class="sxs-lookup"><span data-stu-id="f42ea-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="f42ea-119">hello 開頭 hello URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，hello 相同的所有要求。</span><span class="sxs-lookup"><span data-stu-id="f42ea-119">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="f42ea-120">hello 路徑**/status**，表示該 hello 要求 tooreturn WebHCat (也稱為 Templeton) 狀態 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f42ea-120">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> <span data-ttu-id="f42ea-121">您也可以使用下列命令的 hello 要求 Hive hello 版本：</span><span class="sxs-lookup"><span data-stu-id="f42ea-121">You can also request hello version of Hive by using hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="f42ea-122">此要求會傳回回應類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="f42ea-122">This request returns a response similar toohello following text:</span></span>

       <span data-ttu-id="f42ea-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="f42ea-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="f42ea-124">遵循 toocreate 名為的資料表使用 hello **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="f42ea-124">Use hello following toocreate a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="f42ea-125">hello 遵循與這個要求所使用的參數：</span><span class="sxs-lookup"><span data-stu-id="f42ea-125">hello following parameters used with this request:</span></span>

   * <span data-ttu-id="f42ea-126">**-d** -自`-G`不使用 hello 要求預設 toohello POST 方法。</span><span class="sxs-lookup"><span data-stu-id="f42ea-126">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="f42ea-127">`-d`指定傳送嗨資料值與 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="f42ea-127">`-d` specifies hello data values that are sent with hello request.</span></span>

     * <span data-ttu-id="f42ea-128">**user.name** -hello 使用者執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="f42ea-128">**user.name** - hello user that is running hello command.</span></span>
     * <span data-ttu-id="f42ea-129">**執行**-hello HiveQL 陳述式 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="f42ea-129">**execute** - hello HiveQL statements tooexecute.</span></span>
     * <span data-ttu-id="f42ea-130">**statusdir** -寫入 hello 目錄 hello 這項作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="f42ea-130">**statusdir** - hello directory that hello status for this job is written to.</span></span>

     <span data-ttu-id="f42ea-131">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42ea-131">These statements perform hello following actions:</span></span>
   * <span data-ttu-id="f42ea-132">**DROP TABLE** -如果 hello 資料表已經存在，就會刪除。</span><span class="sxs-lookup"><span data-stu-id="f42ea-132">**DROP TABLE** - If hello table already exists, it is deleted.</span></span>
   * <span data-ttu-id="f42ea-133">**CREATE EXTERNAL TABLE** - 在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="f42ea-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="f42ea-134">外部資料表儲存區中的 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="f42ea-134">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="f42ea-135">hello 資料會保留在 hello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="f42ea-135">hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f42ea-136">當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="f42ea-136">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="f42ea-137">例如，自動化的資料上傳程序，或其他 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="f42ea-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="f42ea-138">卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="f42ea-138">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="f42ea-139">**資料列格式**-hello 資料格式化的方式。</span><span class="sxs-lookup"><span data-stu-id="f42ea-139">**ROW FORMAT** - How hello data is formatted.</span></span> <span data-ttu-id="f42ea-140">每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="f42ea-140">hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="f42ea-141">**儲存為文字檔位置**-hello 資料會儲存 （hello 範例/資料目錄），則會儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="f42ea-141">**STORED AS TEXTFILE LOCATION** - Where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="f42ea-142">**選取**-選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。</span><span class="sxs-lookup"><span data-stu-id="f42ea-142">**SELECT** - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="f42ea-143">這個陳述式會傳回值 **3**，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="f42ea-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f42ea-144">請注意 hello HiveQL 陳述式之間的空格會被 hello`+`字元 Curl 搭配使用時。</span><span class="sxs-lookup"><span data-stu-id="f42ea-144">Notice that hello spaces between HiveQL statements are replaced by hello `+` character when used with Curl.</span></span> <span data-ttu-id="f42ea-145">引號內的值包含空格，例如 hello 分隔符號應該不會被取代的`+`。</span><span class="sxs-lookup"><span data-stu-id="f42ea-145">Quoted values that contain a space, such as hello delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="f42ea-146">**'%25.log' 像 INPUT__FILE__NAME** -此陳述式的限制 hello 搜尋 tooonly 使用檔案結尾。 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f42ea-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits hello search tooonly use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f42ea-147">hello`%25`是 %，hello URL 編碼形式，因此 hello 實際的條件是`like '%.log'`。</span><span class="sxs-lookup"><span data-stu-id="f42ea-147">hello `%25` is hello URL encoded form of %, so hello actual condition is `like '%.log'`.</span></span> <span data-ttu-id="f42ea-148">hello %有 toobe URL 編碼，因為它會被視為在 Url 中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="f42ea-148">hello % has toobe URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="f42ea-149">此命令應該會傳回可以用的 toocheck hello hello 工作狀態的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="f42ea-149">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

       <span data-ttu-id="f42ea-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="f42ea-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="f42ea-151">hello 工作，下列命令使用 hello toocheck hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="f42ea-151">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="f42ea-152">取代**JOBID** hello hello 上一個步驟中傳回的值。</span><span class="sxs-lookup"><span data-stu-id="f42ea-152">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="f42ea-153">例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後**JOBID**會`job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="f42ea-153">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="f42ea-154">如果 hello 工作已完成，則會 hello 狀態**SUCCEEDED**。</span><span class="sxs-lookup"><span data-stu-id="f42ea-154">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f42ea-155">此 Curl 要求會傳回 JavaScript 物件標記法 (JSON) 文件以 hello 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f42ea-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job.</span></span> <span data-ttu-id="f42ea-156">使用 Jq tooretrieve 只 hello 狀態值。</span><span class="sxs-lookup"><span data-stu-id="f42ea-156">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="f42ea-157">一旦 hello hello 作業狀態已變更過**SUCCEEDED**，您可以從 Azure Blob 儲存體擷取 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="f42ea-157">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="f42ea-158">hello `statusdir` hello 查詢傳遞的參數包含 hello 位置 hello 輸出檔; 在此情況下， **/範例/curl**。</span><span class="sxs-lookup"><span data-stu-id="f42ea-158">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="f42ea-159">此位址在 hello 儲存 hello 輸出**範例/curl** hello 中的目錄的叢集預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="f42ea-159">This address stores hello output in hello **example/curl** directory in hello clusters default storage.</span></span>

    <span data-ttu-id="f42ea-160">您可以列出並下載這些檔案使用 hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f42ea-160">You can list and download these files by using hello [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="f42ea-161">如需有關使用 Azure CLI hello 與 Azure 儲存體的詳細資訊，請參閱 hello[與 Azure 儲存體使用 Azure CLI 2.0](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs)文件。</span><span class="sxs-lookup"><span data-stu-id="f42ea-161">For more information on using hello Azure CLI with Azure Storage, see hello [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="f42ea-162">下列陳述式 toocreate 名為 'internal' 新的資料表使用 hello**錯誤記錄檔**:</span><span class="sxs-lookup"><span data-stu-id="f42ea-162">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="f42ea-163">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42ea-163">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="f42ea-164">**CREATE TABLE IF NOT EXISTS** - 建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="f42ea-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="f42ea-165">此陳述式會建立內部資料表中，hello Hive 資料倉儲中所儲存且受完全登錄區。</span><span class="sxs-lookup"><span data-stu-id="f42ea-165">This statement creates an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="f42ea-166">不同於外部資料表，卸除內部資料表，將會刪除 hello 基礎資料。</span><span class="sxs-lookup"><span data-stu-id="f42ea-166">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="f42ea-167">**儲存 AS ORC** -hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。</span><span class="sxs-lookup"><span data-stu-id="f42ea-167">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="f42ea-168">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="f42ea-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="f42ea-169">**INSERT OVERWRITE ...選取**-選取資料列從 hello **log4jLogs**包含資料表**[錯誤]**，然後插入到 hello hello 資料**錯誤記錄檔**資料表。</span><span class="sxs-lookup"><span data-stu-id="f42ea-169">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>
   * <span data-ttu-id="f42ea-170">**選取**-選取所有資料列，從新的 hello**錯誤記錄檔**資料表。</span><span class="sxs-lookup"><span data-stu-id="f42ea-170">**SELECT** - Selects all rows from hello new **errorLogs** table.</span></span>

6. <span data-ttu-id="f42ea-171">使用 hello 傳回 toocheck hello hello 工作狀態的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="f42ea-171">Use hello job ID returned toocheck hello status of hello job.</span></span> <span data-ttu-id="f42ea-172">成功後，使用 Azure CLI 如先前所述 toodownload 和檢視 hello 結果 hello。</span><span class="sxs-lookup"><span data-stu-id="f42ea-172">Once it has succeeded, use hello Azure CLI as described previously toodownload and view hello results.</span></span> <span data-ttu-id="f42ea-173">hello 輸出應包含三行，其中包含**[錯誤]**。</span><span class="sxs-lookup"><span data-stu-id="f42ea-173">hello output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="f42ea-174"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="f42ea-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="f42ea-175">Hive 與 HDInsight 搭配使用的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="f42ea-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="f42ea-176">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="f42ea-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="f42ea-177">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="f42ea-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="f42ea-178">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="f42ea-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f42ea-179">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="f42ea-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="f42ea-180">如果您正在使用 Hive Tez，請參閱下列文件的偵錯資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f42ea-180">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="f42ea-181">使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視</span><span class="sxs-lookup"><span data-stu-id="f42ea-181">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="f42ea-182">如需有關 hello 本文件中使用的 REST API 的詳細資訊，請參閱 hello [WebHCat 參考](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)文件。</span><span class="sxs-lookup"><span data-stu-id="f42ea-182">For more information on hello REST API used in this document, see hello [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


