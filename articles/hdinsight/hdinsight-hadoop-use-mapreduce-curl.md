---
title: "搭配使用 MapReduce 和 Curl 與 HDInsight 中的 Hadoop - Azure | Microsoft Docs"
description: "了解如何使用 Curl 從遠端搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 8238bb829df95dcb8c99c0b7fff53c627a56f47c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="33b24-103">使用 REST 搭配 HDInsight 上的 Hadoop 執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="33b24-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="33b24-104">學習如何使用 WebHCat REST API 在 HDInsight 叢集的 Hadoop 上執行 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="33b24-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="33b24-105">Curl 用來示範如何使用原始 HTTP 要求與 HDInsight 互動，以執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="33b24-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="33b24-106">如果您已熟悉使用以 Linux 為基礎的 Hadoop 伺服器，但剛接觸 HDInsight，請參閱[在以 Linux 為基礎的 HDInsight 上安裝 Hadoop 的須知事項](hdinsight-hadoop-linux-information.md)文件。</span><span class="sxs-lookup"><span data-stu-id="33b24-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="33b24-107"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="33b24-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="33b24-108">一個 Hadoop on HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="33b24-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="33b24-109">Curl</span><span class="sxs-lookup"><span data-stu-id="33b24-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="33b24-110">jq</span><span class="sxs-lookup"><span data-stu-id="33b24-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="33b24-111"><a id="curl"></a>使用 Curl 執行 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="33b24-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="33b24-112">在使用 Curl 或與 WebHCat 進行任何其他 REST 通訊時，您必須提供 HDInsight 叢集管理員使用者名稱和密碼來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="33b24-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="33b24-113">您必須使用叢集名稱，作為用來將要求傳送至伺服器之 URI 的一部分。</span><span class="sxs-lookup"><span data-stu-id="33b24-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="33b24-114">針對本節中的命令，將 **USERNAME** 取代為向叢集驗證的使用者，並將 **PASSWORD** 取代為使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="33b24-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="33b24-115">將 **CLUSTERNAME** 取代為您叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="33b24-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="33b24-116">使用 [基本存取驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)來保護 REST API 的安全。</span><span class="sxs-lookup"><span data-stu-id="33b24-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="33b24-117">您應該一律使用 HTTPS 提出要求，確保認證安全地傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="33b24-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="33b24-118">從命令列中，使用下列命令來確認您可以連線到 HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="33b24-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="33b24-119">您應該會收到類似下列 JSON 的回應：</span><span class="sxs-lookup"><span data-stu-id="33b24-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="33b24-120">此命令中使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="33b24-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="33b24-121">**-u**：指出用來驗證要求的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="33b24-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="33b24-122">**-G**：指出此作業是 GET 要求</span><span class="sxs-lookup"><span data-stu-id="33b24-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="33b24-123">所有要求的 URI 開頭 **https://CLUSTERNAME.azurehdinsight.net/templeton/v1** 都相同。</span><span class="sxs-lookup"><span data-stu-id="33b24-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="33b24-124">若要提交 MapReduce 工作，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="33b24-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="33b24-125">URI 結尾 (/mapreduce/jar) 會告訴 WebHCat，此要求會從 jar 檔案中的類別啟動 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="33b24-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="33b24-126">此命令中使用的參數如下：</span><span class="sxs-lookup"><span data-stu-id="33b24-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="33b24-127">**-d**：未使用 `-G`，因此要求會依預設使用 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="33b24-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="33b24-128">`-d` 可指定與要求一起傳送的資料值。</span><span class="sxs-lookup"><span data-stu-id="33b24-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="33b24-129">**user.name**：執行命令的使用者</span><span class="sxs-lookup"><span data-stu-id="33b24-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="33b24-130">**jar**：包含要執行之類別的 jar 檔案位置</span><span class="sxs-lookup"><span data-stu-id="33b24-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="33b24-131">**class**：包含 MapReduce 邏輯的類別</span><span class="sxs-lookup"><span data-stu-id="33b24-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="33b24-132">**arg**︰要傳遞到 MapReduce 作業的引數。</span><span class="sxs-lookup"><span data-stu-id="33b24-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="33b24-133">在此案例中，是用於輸出的輸入文字檔和目錄</span><span class="sxs-lookup"><span data-stu-id="33b24-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="33b24-134">此命令應該會傳回可用來檢查工作狀態的工作識別碼：</span><span class="sxs-lookup"><span data-stu-id="33b24-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="33b24-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="33b24-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="33b24-136">若要檢查作業的狀態，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="33b24-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="33b24-137">將 **JOBID** 取代為上一個步驟中所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="33b24-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="33b24-138">例如，如果傳回值為 `{"id":"job_1415651640909_0026"}`，則 JOBID 會是 `job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="33b24-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="33b24-139">如果作業已完成，傳回的狀態會是 `SUCCEEDED`。</span><span class="sxs-lookup"><span data-stu-id="33b24-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="33b24-140">此 Curl 要求會傳回含有作業資訊的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="33b24-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="33b24-141">jq 是用來只擷取狀態值。</span><span class="sxs-lookup"><span data-stu-id="33b24-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="33b24-142">當作業狀態變更為 `SUCCEEDED` 之後，您就可以從 Azure Blob 儲存體擷取作業結果。</span><span class="sxs-lookup"><span data-stu-id="33b24-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="33b24-143">隨查詢一起傳遞的 `statusdir` 參數包含輸出檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="33b24-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="33b24-144">在此範例中，位置是 `/example/curl`。</span><span class="sxs-lookup"><span data-stu-id="33b24-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="33b24-145">此位址會將作業的輸出儲存在叢集預設儲存體的 `/example/curl` 中。</span><span class="sxs-lookup"><span data-stu-id="33b24-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="33b24-146">您可以使用 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) 列出並下載這些檔案。</span><span class="sxs-lookup"><span data-stu-id="33b24-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="33b24-147">如需從 Azure CLI 使用 Blob 的詳細資訊，請參閱[搭配 Azure 儲存體使用 Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs) 文件。</span><span class="sxs-lookup"><span data-stu-id="33b24-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="33b24-148"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="33b24-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="33b24-149">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="33b24-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="33b24-150">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="33b24-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="33b24-151">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="33b24-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="33b24-152">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="33b24-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="33b24-153">搭配 HDInsight 上的 Hadoop 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="33b24-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="33b24-154">如需本文中使用的 REST 介面的詳細資訊，請參閱 [WebHCat 參照](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)。</span><span class="sxs-lookup"><span data-stu-id="33b24-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>