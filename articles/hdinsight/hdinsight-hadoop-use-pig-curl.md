---
title: "與 HDInsight 的 Azure 中的其餘部分的 Hadoop Pig aaaUse |Microsoft 文件"
description: "了解 toouse REST toorun Pig 拉丁工作在 Hadoop 上的中 Azure HDInsight 叢集的方式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="17d84-103">使用 REST 在 HDInsight 上搭配 Hadoop 執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="17d84-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="17d84-104">了解 toorun Pig 拉丁藉由 REST 要求 tooan Azure HDInsight 叢集的工作。</span><span class="sxs-lookup"><span data-stu-id="17d84-104">Learn how toorun Pig Latin jobs by making REST requests tooan Azure HDInsight cluster.</span></span> <span data-ttu-id="17d84-105">Curl 是您可以互動方式使用 hello WebHCat REST API 的 HDInsight 的使用的 toodemonstrate。</span><span class="sxs-lookup"><span data-stu-id="17d84-105">Curl is used toodemonstrate how you can interact with HDInsight using hello WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="17d84-106">如果您已熟悉使用 linux Hadoop 伺服器，但新 tooHDInsight，請參閱[以 Linux 為基礎的 HDInsight 秘訣](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="17d84-106">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="17d84-107"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="17d84-107"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="17d84-108">Azure HDInsight (HDInsight 上的 Hadoop) 叢集 (Linux 型或 Windows 型)</span><span class="sxs-lookup"><span data-stu-id="17d84-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="17d84-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="17d84-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="17d84-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="17d84-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="17d84-111">Curl</span><span class="sxs-lookup"><span data-stu-id="17d84-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="17d84-112">jq</span><span class="sxs-lookup"><span data-stu-id="17d84-112">jq</span></span>](http://stedolan.github.io/jq/)

## <span data-ttu-id="17d84-113"><a id="curl"></a>使用 Curl 執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="17d84-113"><a id="curl"></a>Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="17d84-114">hello REST API 會透過保護[基本存取驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。</span><span class="sxs-lookup"><span data-stu-id="17d84-114">hello REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="17d84-115">一律使用安全 HTTP (HTTPS) tooensure 您的認證會安全地傳送 toohello 伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="17d84-115">Always make requests by using Secure HTTP (HTTPS) tooensure that your credentials are securely sent toohello server.</span></span>
>
> <span data-ttu-id="17d84-116">當使用本節中的 hello 命令，來取代`USERNAME`hello 使用者 tooauthenticate toohello 叢集與取代`PASSWORD`hello hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="17d84-116">When using hello commands in this section, replace `USERNAME` with hello user tooauthenticate toohello cluster, and replace `PASSWORD` with hello password for hello user account.</span></span> <span data-ttu-id="17d84-117">取代`CLUSTERNAME`與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="17d84-117">Replace `CLUSTERNAME` with hello name of your cluster.</span></span>
>


1. <span data-ttu-id="17d84-118">從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="17d84-118">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="17d84-119">您應該會收到下列 JSON 回應 hello:</span><span class="sxs-lookup"><span data-stu-id="17d84-119">You should receive hello following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="17d84-120">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="17d84-120">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="17d84-121">**-u**: hello 使用者名稱和密碼使用 tooauthenticate hello 要求</span><span class="sxs-lookup"><span data-stu-id="17d84-121">**-u**: hello user name and password used tooauthenticate hello request</span></span>
    * <span data-ttu-id="17d84-122">**-G**：指出此要求是 GET 要求</span><span class="sxs-lookup"><span data-stu-id="17d84-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="17d84-123">hello 開頭 hello URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，hello 相同的所有要求。</span><span class="sxs-lookup"><span data-stu-id="17d84-123">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is hello same for all requests.</span></span> <span data-ttu-id="17d84-124">hello 路徑**/status**，表示該 hello 要求 WebHCat (也稱為 Templeton) tooreturn hello 狀態 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="17d84-124">hello path, **/status**, indicates that hello request is tooreturn hello status of WebHCat (also known as Templeton) for hello server.</span></span>

2. <span data-ttu-id="17d84-125">使用下列程式碼 toosubmit Pig 拉丁作業 toohello 叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="17d84-125">Use hello following code toosubmit a Pig Latin job toohello cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="17d84-126">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="17d84-126">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="17d84-127">**-d**： 因為`-G`不使用 hello 要求預設 toohello POST 方法。</span><span class="sxs-lookup"><span data-stu-id="17d84-127">**-d**: Because `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="17d84-128">`-d`指定傳送嗨資料值與 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="17d84-128">`-d` specifies hello data values that are sent with hello request.</span></span>

    * <span data-ttu-id="17d84-129">**user.name**: hello 執行使用者的 hello 命令</span><span class="sxs-lookup"><span data-stu-id="17d84-129">**user.name**: hello user who is running hello command</span></span>
    * <span data-ttu-id="17d84-130">**執行**: hello Pig 拉丁陳述式 tooexecute</span><span class="sxs-lookup"><span data-stu-id="17d84-130">**execute**: hello Pig Latin statements tooexecute</span></span>
    * <span data-ttu-id="17d84-131">**statusdir**: hello 的這項作業狀態的 hello 目錄寫入</span><span class="sxs-lookup"><span data-stu-id="17d84-131">**statusdir**: hello directory that hello status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="17d84-132">請注意會以 hello 取代 Pig 拉丁陳述式中的 hello 空格`+`字元 Curl 搭配使用時。</span><span class="sxs-lookup"><span data-stu-id="17d84-132">Notice that hello spaces in Pig Latin statements are replaced by hello `+` character when used with Curl.</span></span>

    <span data-ttu-id="17d84-133">此命令應該會傳回可以用的 toocheck hello 狀態 hello 工作，例如作業識別碼：</span><span class="sxs-lookup"><span data-stu-id="17d84-133">This command should return a job ID that can be used toocheck hello status of hello job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="17d84-134">hello 工作，下列命令使用 hello toocheck hello 狀態</span><span class="sxs-lookup"><span data-stu-id="17d84-134">toocheck hello status of hello job, use hello following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="17d84-135">取代`JOBID`hello hello 上一個步驟中傳回的值。</span><span class="sxs-lookup"><span data-stu-id="17d84-135">Replace `JOBID` with hello value returned in hello previous step.</span></span> <span data-ttu-id="17d84-136">例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後`JOBID`是`job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="17d84-136">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="17d84-137">如果 hello 工作已完成，則會 hello 狀態**SUCCEEDED**。</span><span class="sxs-lookup"><span data-stu-id="17d84-137">If hello job has finished, hello state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="17d84-138">傳回 JavaScript 物件標記法 (JSON) 文件以 hello 作業和 jq 資訊是使用的 tooretrieve 此 Curl 要求只 hello 狀態值。</span><span class="sxs-lookup"><span data-stu-id="17d84-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job, and jq is used tooretrieve only hello state value.</span></span>

## <span data-ttu-id="17d84-139"><a id="results"></a>檢視結果</span><span class="sxs-lookup"><span data-stu-id="17d84-139"><a id="results"></a>View results</span></span>

<span data-ttu-id="17d84-140">Hello hello 工作狀態變更時太**SUCCEEDED**，您可以擷取 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="17d84-140">When hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job.</span></span> <span data-ttu-id="17d84-141">hello `statusdir` hello 查詢傳遞的參數包含 hello 位置 hello 輸出檔; 在此情況下， `/example/pigcurl`。</span><span class="sxs-lookup"><span data-stu-id="17d84-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="17d84-142">HDInsight 可以使用 Azure 儲存體或 Azure 資料湖存放區為 hello 預設資料儲存區。</span><span class="sxs-lookup"><span data-stu-id="17d84-142">HDInsight can use either Azure Storage or Azure Data Lake Store as hello default data store.</span></span> <span data-ttu-id="17d84-143">有各種方式 tooget hello 根據哪一種您使用的資料。</span><span class="sxs-lookup"><span data-stu-id="17d84-143">There are various ways tooget at hello data depending on which one you use.</span></span> <span data-ttu-id="17d84-144">如需詳細資訊，請參閱 hello 儲存體 區段的 hello[以 Linux 為基礎的 HDInsight 資訊](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store)文件。</span><span class="sxs-lookup"><span data-stu-id="17d84-144">For more information, see hello storage section of hello [Linux-based HDInsight information](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <span data-ttu-id="17d84-145"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="17d84-145"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="17d84-146">本文件中所示範，您可以使用您的 HDInsight 叢集上的未經處理的 HTTP 要求 toorun、 監視器和檢視 hello 結果的 Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="17d84-146">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="17d84-147">如需有關使用本文章中的 hello REST 介面的詳細資訊，請參閱 hello [WebHCat 參考](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)。</span><span class="sxs-lookup"><span data-stu-id="17d84-147">For more information about hello REST interface used in this article, see hello [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <span data-ttu-id="17d84-148"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="17d84-148"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="17d84-149">如需 HDInsight 上 Pig 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="17d84-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="17d84-150">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="17d84-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="17d84-151">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="17d84-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="17d84-152">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="17d84-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="17d84-153">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="17d84-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
