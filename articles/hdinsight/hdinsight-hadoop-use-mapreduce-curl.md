---
title: "aaaUse MapReduce 和 Curl HDInsight 的 Azure 中的 Hadoop |Microsoft 文件"
description: "了解如何 tooremotely 執行 MapReduce 工作的 Hadoop HDInsight 上使用 Curl。"
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
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="bbbe5-103">使用 REST 搭配 HDInsight 上的 Hadoop 執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="bbbe5-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="bbbe5-104">了解 HDInsight 叢集上的 Hadoop 上 toouse hello WebHCat REST API toorun MapReduce 作業的方式。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-104">Learn how toouse hello WebHCat REST API toorun MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="bbbe5-105">Curl 是使用的 toodemonstrate 如何您可以使用與互動 HDInsight 未經處理的 HTTP 要求 toorun MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="bbbe5-106">如果您已熟悉使用 linux Hadoop 伺服器，但是您新 tooHDInsight，請參閱 hello[配備 HDInsight 上的 Linux Hadoop 有關 tooknow](hdinsight-hadoop-linux-information.md)文件。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-106">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see hello [What you need tooknow about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <span data-ttu-id="bbbe5-107"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="bbbe5-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="bbbe5-108">一個 Hadoop on HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="bbbe5-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="bbbe5-109">Curl</span><span class="sxs-lookup"><span data-stu-id="bbbe5-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="bbbe5-110">jq</span><span class="sxs-lookup"><span data-stu-id="bbbe5-110">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="bbbe5-111"><a id="curl"></a>使用 Curl 執行 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="bbbe5-111"><a id="curl"></a>Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="bbbe5-112">當您 WebHCat 的情況下，使用 Curl 或任何其他的 REST 通訊時，您必須藉由提供 hello HDInsight 叢集系統管理員使用者名稱和密碼驗證 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-112">When you use Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="bbbe5-113">您必須使用 hello 叢集名稱做為 hello 使用的 toosend hello 要求 toohello 伺服器 URI 的一部分。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-113">You must use hello cluster name as part of hello URI that is used toosend hello requests toohello server.</span></span>
>
> <span data-ttu-id="bbbe5-114">本章節中的 hello 命令，請將**USERNAME**與 hello 使用者 tooauthenticate toohello 叢集和**密碼**hello hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-114">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="bbbe5-115">取代**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-115">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
>
> <span data-ttu-id="bbbe5-116">hello REST API 會受到使用[基本存取驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-116">hello REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="bbbe5-117">您永遠應該使用您的認證會安全地傳送 toohello 伺服器的 HTTPS tooensure 提出要求。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-117">You should always make requests by using HTTPS tooensure that your credentials are securely sent toohello server.</span></span>


1. <span data-ttu-id="bbbe5-118">從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="bbbe5-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="bbbe5-119">您應該會收到下列 JSON 回應類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="bbbe5-119">You should receive a response similar toohello following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="bbbe5-120">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="bbbe5-120">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="bbbe5-121">**-u**： 指出使用 tooauthenticate hello 要求 hello 使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="bbbe5-121">**-u**: Indicates hello user name and password used tooauthenticate hello request</span></span>
   * <span data-ttu-id="bbbe5-122">**-G**：指出此作業是 GET 要求</span><span class="sxs-lookup"><span data-stu-id="bbbe5-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="bbbe5-123">hello 開頭的 URI，hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，hello 相同的所有要求。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-123">hello beginning of hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span>

2. <span data-ttu-id="bbbe5-124">toosubmit MapReduce 工作，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="bbbe5-124">toosubmit a MapReduce job, use hello following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="bbbe5-125">hello 結尾 hello URI (/ mapreduce/jar) 會告知 WebHCat 此要求會啟動 MapReduce 工作，從 jar 檔案中的類別。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-125">hello end of hello URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="bbbe5-126">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="bbbe5-126">hello parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="bbbe5-127">**-d**:`-G`未使用，所以 hello 要求預設 toohello POST 方法。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-127">**-d**: `-G` is not used, so hello request defaults toohello POST method.</span></span> <span data-ttu-id="bbbe5-128">`-d`指定傳送嗨資料值與 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-128">`-d` specifies hello data values that are sent with hello request.</span></span>
    * <span data-ttu-id="bbbe5-129">**user.name**: hello 執行使用者的 hello 命令</span><span class="sxs-lookup"><span data-stu-id="bbbe5-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="bbbe5-130">**jar**: hello jar 檔案的包含類別 toobe hello 位置執行</span><span class="sxs-lookup"><span data-stu-id="bbbe5-130">**jar**: hello location of hello jar file that contains class toobe ran</span></span>
    * <span data-ttu-id="bbbe5-131">**類別**: hello 包含 hello MapReduce 邏輯類別</span><span class="sxs-lookup"><span data-stu-id="bbbe5-131">**class**: hello class that contains hello MapReduce logic</span></span>
    * <span data-ttu-id="bbbe5-132">**arg**: hello 引數 toobe 傳遞 toohello MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-132">**arg**: hello arguments toobe passed toohello MapReduce job.</span></span> <span data-ttu-id="bbbe5-133">Hello 在此情況下，輸入用於 hello 輸出的文字檔案和 hello 目錄</span><span class="sxs-lookup"><span data-stu-id="bbbe5-133">In this case, hello input text file and hello directory that are used for hello output</span></span>

     <span data-ttu-id="bbbe5-134">此命令應該會傳回可以用的 toocheck hello hello 工作狀態的作業識別碼：</span><span class="sxs-lookup"><span data-stu-id="bbbe5-134">This command should return a job ID that can be used toocheck hello status of hello job:</span></span>

       <span data-ttu-id="bbbe5-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="bbbe5-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="bbbe5-136">hello 工作，下列命令使用 hello toocheck hello 狀態：</span><span class="sxs-lookup"><span data-stu-id="bbbe5-136">toocheck hello status of hello job, use hello following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="bbbe5-137">取代 hello **JOBID** hello hello 上一個步驟中傳回的值。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-137">Replace hello **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="bbbe5-138">例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後將 JOBID hello `job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-138">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then hello JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="bbbe5-139">如果 hello 作業已完成，傳回是 hello 狀態`SUCCEEDED`。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-139">If hello job is complete, hello state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bbbe5-140">此 Curl 要求傳回 JSON 文件以 hello 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-140">This Curl request returns a JSON document with information about hello job.</span></span> <span data-ttu-id="bbbe5-141">使用 Jq tooretrieve 只 hello 狀態值。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-141">Jq is used tooretrieve only hello state value.</span></span>

4. <span data-ttu-id="bbbe5-142">Hello hello 工作狀態變更時太`SUCCEEDED`，您可以從 Azure Blob 儲存體擷取 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-142">When hello state of hello job has changed too`SUCCEEDED`, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="bbbe5-143">hello `statusdir` hello 查詢傳遞的參數包含 hello hello 輸出檔位置。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-143">hello `statusdir` parameter that is passed with hello query contains hello location of hello output file.</span></span> <span data-ttu-id="bbbe5-144">在此範例中，是 hello 位置`/example/curl`。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-144">In this example, hello location is `/example/curl`.</span></span> <span data-ttu-id="bbbe5-145">此位址在 hello 叢集預設儲存體中儲存 hello 工作的 hello 輸出`/example/curl`。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-145">This address stores hello output of hello job in hello clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="bbbe5-146">您可以列出並下載這些檔案使用 hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-146">You can list and download these files by using hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="bbbe5-147">如需使用 Azure CLI hello 從 blob 的詳細資訊，請參閱 hello[使用 hello 與 Azure 儲存體的 Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs)文件。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-147">For more information on working with blobs from hello Azure CLI, see hello [Using hello Azure CLI 2.0 with Azure Storage](../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <span data-ttu-id="bbbe5-148"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="bbbe5-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="bbbe5-149">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="bbbe5-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="bbbe5-150">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="bbbe5-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="bbbe5-151">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="bbbe5-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="bbbe5-152">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="bbbe5-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="bbbe5-153">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="bbbe5-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="bbbe5-154">如需有關使用本文章中的 hello REST 介面的詳細資訊，請參閱 hello [WebHCat 參考](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)。</span><span class="sxs-lookup"><span data-stu-id="bbbe5-154">For more information about hello REST interface that is used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
