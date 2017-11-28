---
title: "在 HDInsight 中搭配使用 Hadoop Sqoop 與 Curl - Azure | Microsoft Docs"
description: "了解如何使用 Curl 從遠端提交 Sqoop 工作到 HDInsight。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0975aedf58c6e110726dd3308eae5f9ad3907cc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="6ecf2-103">使用 Curl 在 HDInsight 中以 Hadoop 執行 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="6ecf2-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="6ecf2-104">了解如何使用 Curl 在 HDInsight 中的 Hadoop 叢集上執行 Sqoop 作業。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="6ecf2-105">本文件使用 Curl 示範如何使用未經處理的 HTTP 要求來與 HDInsight 互動，以便執行、監視和擷取 Sqoop 作業的結果。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="6ecf2-106">要想執行這些作業，就要使用 HDInsight 叢集所提供的 WebHCat REST API (先前稱為 Templeton)。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="6ecf2-107">如果您已熟悉使用以 Linux 為基礎的 Hadoop 伺服器，但剛接觸 HDInsight，請參閱[在 Linux 上使用 HDInsight 的相關資訊](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6ecf2-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="6ecf2-108">Prerequisites</span></span>
<span data-ttu-id="6ecf2-109">若要完成本文中的步驟，您需要下列項目。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="6ecf2-110">HDInsight 叢集上的 Hadoop (Linux 或 Windows 型)</span><span class="sxs-lookup"><span data-stu-id="6ecf2-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="6ecf2-111">Curl</span><span class="sxs-lookup"><span data-stu-id="6ecf2-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="6ecf2-112">jq</span><span class="sxs-lookup"><span data-stu-id="6ecf2-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="6ecf2-113">使用 Curl 提交 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="6ecf2-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="6ecf2-114">在使用 Curl 或與 WebHCat 進行任何其他 REST 通訊時，您必須提供 HDInsight 叢集系統管理員的使用者名稱和密碼來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="6ecf2-115">您也必須在用來將要求傳送至伺服器的統一資源識別項 (URI) 中使用叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="6ecf2-116">在本節的所有命令中，將 **USERNAME** 取代為用來驗證叢集的使用者，並將 **PASSWORD** 取代為使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="6ecf2-117">將 **CLUSTERNAME** 取代為您叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="6ecf2-118">透過 [基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)來保護 REST API 的安全。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="6ecf2-119">您應該一律使用安全 HTTP (HTTPS) 提出要求，確保認證安全地傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="6ecf2-120">從命令列中，使用下列命令來確認您可以連線到 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="6ecf2-121">您應該會收到如下所示的回應：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="6ecf2-122">此命令中使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="6ecf2-123">**-u** - 用來驗證要求的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="6ecf2-124">**-G** - 指出這是 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="6ecf2-125">所有要求的 URL 開頭 **https://CLUSTERNAME.azurehdinsight.net/templeton/v1** 都會相同。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="6ecf2-126">路徑 **/status** 指出要求是要傳回伺服器之 WebHCat (也稱為 Templeton) 的狀態。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="6ecf2-127">使用以下命令提交 Sqoop 作業：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="6ecf2-128">此命令中使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="6ecf2-129">**-d** - 因為未使用 `-G`，要求會依預設使用 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="6ecf2-130">`-d` 可指定與要求一起傳送的資料值。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="6ecf2-131">**user.name** - 執行命令的使用者。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="6ecf2-132">**命令** - 要執行的 Sqoop 命令。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="6ecf2-133">**statusdir** - 要寫入此工作狀態的目錄。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="6ecf2-134">此命令應該會傳回可用來檢查工作狀態的工作識別碼。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="6ecf2-135">若要檢查工作的狀態，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="6ecf2-136">將 **JOBID** 取代為上一個步驟中所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="6ecf2-137">例如，如果傳回值為 `{"id":"job_1415651640909_0026"}`，則 **JOBID** 會是 `job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="6ecf2-138">如果工作已完成，則狀態會是 [ **成功**]。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6ecf2-139">此 Curl 要求會傳回含有工作資訊的 JavaScript Object Notation (JSON) 文件；jq 可用來僅擷取狀態值。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="6ecf2-140">工作狀態變更為 [成功] 之後，即可從 Azure Blob 儲存體擷取工作結果。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="6ecf2-141">隨查詢一起傳送的 `statusdir` 參數包含輸出檔案的位置；在此案例中為 **wasb:///example/curl**。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="6ecf2-142">此位址會將作業輸出儲存至 HDInsight 叢集所使用之預設儲存體容器的 **example/curl** 目錄中。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="6ecf2-143">您可以使用 [Azure CLI](../cli-install-nodejs.md) 列出並下載這些檔案。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="6ecf2-144">例如，若要列出 **example/curl** 中的檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="6ecf2-145">若要下載檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="6ecf2-146">您必須使用 `-a` 和 `-k` 參數指定包含 Blob 的儲存體帳戶名稱，或是設定 **AZURE\_STORAGE\_ACCOUNT** 和 **AZURE\_STORAGE\_ACCESS\_KEY** 環境變數。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="6ecf2-147">如需詳細資訊，請參閱 <a href="hdinsight-upload-data.md" target="_blank"。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="6ecf2-148">限制</span><span class="sxs-lookup"><span data-stu-id="6ecf2-148">Limitations</span></span>
* <span data-ttu-id="6ecf2-149">大量匯出 - 使用 Linux 型 HDInsight，用來將資料匯出至 Microsoft SQL Server 或 Azure SQL Database 的 Sqoop 連接器目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="6ecf2-150">批次處理 - 使用 Linux 型 HDInsight，執行插入時若使用 `-batch` 參數，Sqoop 將會執行多個插入，而不是批次處理插入作業。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="6ecf2-151">摘要</span><span class="sxs-lookup"><span data-stu-id="6ecf2-151">Summary</span></span>
<span data-ttu-id="6ecf2-152">如這份文件所示，您可以使用原始 HTTP 要求來執行、監視和檢視 HDInsight 叢集上的 Sqoop 作業結果。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="6ecf2-153">如需本文中使用的 REST 介面的詳細資訊，請參閱 <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API 指南</a>。</span><span class="sxs-lookup"><span data-stu-id="6ecf2-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ecf2-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ecf2-154">Next steps</span></span>
<span data-ttu-id="6ecf2-155">Hive 與 HDInsight 搭配使用的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="6ecf2-156">在 HDInsight 上將 Sqoop 與 Hadoop 搭配使用</span><span class="sxs-lookup"><span data-stu-id="6ecf2-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="6ecf2-157">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="6ecf2-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="6ecf2-158">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="6ecf2-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6ecf2-159">搭配 HDInsight 上的 Hadoop 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="6ecf2-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="6ecf2-160">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="6ecf2-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


