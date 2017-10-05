---
title: "在 HDInsight 中搭配使用 Hadoop Hive 與 Curl - Azure | Microsoft Docs"
description: "了解如何使用 Curl 從遠端提交 Pig 工作到 HDInsight。"
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
ms.openlocfilehash: 8a4f217b046121f85be0585eab18d90c44f21b9e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="33e1b-103">使用 REST 以 HDInsight 中的 Hadoop 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="33e1b-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="33e1b-104">了解如何使用 WebHCat REST API 以 Azure HDInsight 叢集上的 Hadoop 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="33e1b-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="33e1b-105">[Curl](http://curl.haxx.se/) 用來示範如何使用原始 HTTP 要求與 HDInsight 互動。</span><span class="sxs-lookup"><span data-stu-id="33e1b-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="33e1b-106">[jq](http://stedolan.github.io/jq/) 公用程式用來處理從 REST 要求傳回的 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="33e1b-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="33e1b-107">如果您已熟悉使用以 Linux 為基礎的 Hadoop 伺服器，但剛接觸 HDInsight，請參閱 [在以 Linux 為基礎的 HDInsight 上安裝 Hadoop 的須知事項](hdinsight-hadoop-linux-information.md)文件。</span><span class="sxs-lookup"><span data-stu-id="33e1b-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <span data-ttu-id="33e1b-108"><a id="curl"></a>執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="33e1b-108"><a id="curl"></a>Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="33e1b-109">在使用 cURL 或與 WebHCat 進行任何其他 REST 通訊時，您必須提供 HDInsight 叢集系統管理員的使用者名稱和密碼來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="33e1b-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="33e1b-110">在本節的所有命令中，將 **USERNAME** 取代為用來驗證叢集的使用者，並將 **PASSWORD** 取代為使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="33e1b-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="33e1b-111">將 **CLUSTERNAME** 取代為您叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="33e1b-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="33e1b-112">透過 [基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)來保護 REST API 的安全。</span><span class="sxs-lookup"><span data-stu-id="33e1b-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="33e1b-113">為確保認證安全地傳送至伺服器，請一律使用安全 HTTP (HTTPS) 提出要求。</span><span class="sxs-lookup"><span data-stu-id="33e1b-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="33e1b-114">從命令列中，使用下列命令來確認您可以連線到 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="33e1b-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="33e1b-115">您應該會收到類似以下文字的回應：</span><span class="sxs-lookup"><span data-stu-id="33e1b-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="33e1b-116">此命令中使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="33e1b-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="33e1b-117">**-u** - 用來驗證要求的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="33e1b-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="33e1b-118">**-G** - 指出此要求是 GET 作業。</span><span class="sxs-lookup"><span data-stu-id="33e1b-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="33e1b-119">所有要求的 URL 開頭 **https://CLUSTERNAME.azurehdinsight.net/templeton/v1** 都相同。</span><span class="sxs-lookup"><span data-stu-id="33e1b-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="33e1b-120">路徑 **/status** 指出要求是要傳回伺服器之 WebHCat (也稱為 Templeton) 的狀態。</span><span class="sxs-lookup"><span data-stu-id="33e1b-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="33e1b-121">您也可以使用下列命令要求 Hive 的版本：</span><span class="sxs-lookup"><span data-stu-id="33e1b-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="33e1b-122">此要求會傳回類似以下文字的回應：</span><span class="sxs-lookup"><span data-stu-id="33e1b-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="33e1b-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="33e1b-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="33e1b-124">使用下列命令建立名為 **log4jLogs** 的資料表：</span><span class="sxs-lookup"><span data-stu-id="33e1b-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="33e1b-125">下列參數可搭配此要求使用：</span><span class="sxs-lookup"><span data-stu-id="33e1b-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="33e1b-126">**-d** - 因為未使用 `-G`，要求會依預設使用 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="33e1b-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="33e1b-127">`-d` 可指定與要求一起傳送的資料值。</span><span class="sxs-lookup"><span data-stu-id="33e1b-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="33e1b-128">**user.name** - 執行命令的使用者。</span><span class="sxs-lookup"><span data-stu-id="33e1b-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="33e1b-129">**execute** - 要執行的 HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="33e1b-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="33e1b-130">**statusdir** - 要寫入此作業狀態的目錄。</span><span class="sxs-lookup"><span data-stu-id="33e1b-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="33e1b-131">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="33e1b-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="33e1b-132">**DROP TABLE** - 如果資料表已存在，則會刪除它。</span><span class="sxs-lookup"><span data-stu-id="33e1b-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="33e1b-133">**CREATE EXTERNAL TABLE** - 在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="33e1b-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="33e1b-134">外部資料表只會將資料表定義儲存在 Hive 中。</span><span class="sxs-lookup"><span data-stu-id="33e1b-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="33e1b-135">資料會留在原來的位置。</span><span class="sxs-lookup"><span data-stu-id="33e1b-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="33e1b-136">當您預期會由外部來源來更新基礎資料時，請使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="33e1b-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="33e1b-137">例如，自動化的資料上傳程序，或其他 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="33e1b-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="33e1b-138">捨棄外部資料表並 **不會** 刪除資料，只會刪除資料表定義。</span><span class="sxs-lookup"><span data-stu-id="33e1b-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="33e1b-139">**ROW FORMAT** - 設定資料格式的方式。</span><span class="sxs-lookup"><span data-stu-id="33e1b-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="33e1b-140">每個記錄中的欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="33e1b-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="33e1b-141">**STORED AS TEXTFILE LOCATION**：資料的儲存位置 (example/data 目錄)，且資料儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="33e1b-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="33e1b-142">**SELECT** - 選擇其資料欄 **t4** 包含值 **[ERROR]** 的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="33e1b-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="33e1b-143">這個陳述式會傳回值 **3**，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="33e1b-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="33e1b-144">請注意，在搭配 Curl 使用時，會以 `+` 字元取代 HiveQL 陳述式之間的空格。</span><span class="sxs-lookup"><span data-stu-id="33e1b-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="33e1b-145">加上引號的值若包含空格，例如分隔符號，則不應以 `+`取代。</span><span class="sxs-lookup"><span data-stu-id="33e1b-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="33e1b-146">**INPUT__FILE__NAME LIKE '%25.log'** - 這個陳述式會限制該搜尋僅能使用其檔名以 .log 結尾的檔案。</span><span class="sxs-lookup"><span data-stu-id="33e1b-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="33e1b-147">`%25` 是 % 的 URL 編碼格式，因此實際的條件是 `like '%.log'`。</span><span class="sxs-lookup"><span data-stu-id="33e1b-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="33e1b-148">% 必須為 URL 編碼，因為會將其視為在 URL 中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="33e1b-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="33e1b-149">此命令應該會傳回可用來檢查工作狀態的工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="33e1b-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="33e1b-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="33e1b-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="33e1b-151">若要檢查作業的狀態，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="33e1b-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="33e1b-152">將 **JOBID** 取代為上一個步驟中所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="33e1b-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="33e1b-153">例如，如果傳回值為 `{"id":"job_1415651640909_0026"}`，則 **JOBID** 會是 `job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="33e1b-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="33e1b-154">如果作業已完成，則狀態會是 **SUCCEEDED**。</span><span class="sxs-lookup"><span data-stu-id="33e1b-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="33e1b-155">此 Curl 要求會傳回含有作業資訊的 JavaScript 物件標記法 (JSON) 文件。</span><span class="sxs-lookup"><span data-stu-id="33e1b-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="33e1b-156">Jq 是用來只擷取狀態值。</span><span class="sxs-lookup"><span data-stu-id="33e1b-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="33e1b-157">工作狀態變更為 [成功] 之後，即可從 Azure Blob 儲存體擷取工作結果。</span><span class="sxs-lookup"><span data-stu-id="33e1b-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="33e1b-158">與查詢一起傳遞的 `statusdir` 參數包含輸出檔案的位置；在此案例中為 **/example/curl**。</span><span class="sxs-lookup"><span data-stu-id="33e1b-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="33e1b-159">此位址會將輸出儲存在叢集預設儲存體的 **example/curl** 目錄中。</span><span class="sxs-lookup"><span data-stu-id="33e1b-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="33e1b-160">您可以使用 [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) 列出並下載這些檔案。</span><span class="sxs-lookup"><span data-stu-id="33e1b-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="33e1b-161">如需搭配 Azure 儲存體使用 Azure CLI 的詳細資訊，請參閱[搭配 Azure 儲存體使用 Azure CLI 2.0](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) 文件。</span><span class="sxs-lookup"><span data-stu-id="33e1b-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="33e1b-162">使用下列陳述式來建立名為 **errorLogs**的新「內部」資料表：</span><span class="sxs-lookup"><span data-stu-id="33e1b-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="33e1b-163">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="33e1b-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="33e1b-164">**CREATE TABLE IF NOT EXISTS** - 建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="33e1b-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="33e1b-165">這個陳述式會建立內部資料表，而內部資料表儲存在 Hive 資料倉儲中，並完全透過 Hive 來管理。</span><span class="sxs-lookup"><span data-stu-id="33e1b-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="33e1b-166">與外部資料表不同之處在於，捨棄內部資料表也會刪除基礎資料。</span><span class="sxs-lookup"><span data-stu-id="33e1b-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="33e1b-167">**STORED AS ORC** - 以最佳化資料列單欄式 (Optimized Row Columnar, ORC) 格式儲存資料。</span><span class="sxs-lookup"><span data-stu-id="33e1b-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="33e1b-168">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="33e1b-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="33e1b-169">**INSERT OVERWRITE ...SELECT**- 從包含 **[ERROR]** 的 **log4jLogs** 資料表選取資料列，然後將資料插入 **errorLogs** 資料表。</span><span class="sxs-lookup"><span data-stu-id="33e1b-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="33e1b-170">**SELECT** - 從新的 **errorLogs** 資料表選取所有資料列。</span><span class="sxs-lookup"><span data-stu-id="33e1b-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="33e1b-171">使用傳回的工作識別碼檢查工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="33e1b-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="33e1b-172">成功之後，如先前所述使用 Azure CLI 來下載並檢視結果。</span><span class="sxs-lookup"><span data-stu-id="33e1b-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="33e1b-173">輸出應包含三行，其中都包含 **[ERROR]**。</span><span class="sxs-lookup"><span data-stu-id="33e1b-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <span data-ttu-id="33e1b-174"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="33e1b-174"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="33e1b-175">Hive 與 HDInsight 搭配使用的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="33e1b-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="33e1b-176">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="33e1b-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="33e1b-177">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="33e1b-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="33e1b-178">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="33e1b-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="33e1b-179">搭配 HDInsight 上的 Hadoop 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="33e1b-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="33e1b-180">如果您搭配使用 Tez 和 Hive，請參閱下列文件所提供的偵錯資訊：</span><span class="sxs-lookup"><span data-stu-id="33e1b-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="33e1b-181">在以 Linux 為基礎的 HDInsight 上使用 Ambari Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="33e1b-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="33e1b-182">如需本文件中使用之 REST API 的詳細資訊，請參閱 [WebHCat 參照 (英文)](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) 文件。</span><span class="sxs-lookup"><span data-stu-id="33e1b-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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


