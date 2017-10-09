---
title: "使用 Curl HDInsight 的 Azure 中的 Hadoop Sqoop aaaUse |Microsoft 文件"
description: "了解如何 tooremotely 提交 Sqoop 作業 tooHDInsight 使用 Curl。"
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
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="a5440-103">使用 Curl 在 HDInsight 中以 Hadoop 執行 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="a5440-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="a5440-104">了解 HDInsight 中 toouse Curl toorun Sqoop 工作在 Hadoop 叢集的方式。</span><span class="sxs-lookup"><span data-stu-id="a5440-104">Learn how toouse Curl toorun Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="a5440-105">Curl 是使用的 toodemonstrate 如何您可以使用與互動 HDInsight 未經處理的 HTTP 要求 toorun、 監視器和 Sqoop 作業擷取 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a5440-105">Curl is used toodemonstrate how you can interact with HDInsight by using raw HTTP requests toorun, monitor, and retrieve hello results of Sqoop jobs.</span></span> <span data-ttu-id="a5440-106">這是利用 hello WebHCat 提供 REST API （先前稱為 Templeton） 您的 HDInsight 叢集來運作。</span><span class="sxs-lookup"><span data-stu-id="a5440-106">This works by using hello WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a5440-107">如果您已熟悉使用 linux Hadoop 伺服器，但新 tooHDInsight，請參閱[資訊使用 on Linux 的 HDInsight](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="a5440-107">If you are already familiar with using Linux-based Hadoop servers, but are new tooHDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a5440-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5440-108">Prerequisites</span></span>
<span data-ttu-id="a5440-109">toocomplete hello 本文中的步驟，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a5440-109">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="a5440-110">HDInsight 叢集上的 Hadoop (Linux 或 Windows 型)</span><span class="sxs-lookup"><span data-stu-id="a5440-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="a5440-111">Curl</span><span class="sxs-lookup"><span data-stu-id="a5440-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="a5440-112">jq</span><span class="sxs-lookup"><span data-stu-id="a5440-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="a5440-113">使用 Curl 提交 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="a5440-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="a5440-114">當使用 WebHCat Curl 或任何其他的 REST 通訊，您必須驗證 hello 要求藉由提供 hello 使用者名稱和 hello HDInsight 叢集系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="a5440-114">When using Curl or any other REST communication with WebHCat, you must authenticate hello requests by providing hello user name and password for hello HDInsight cluster administrator.</span></span> <span data-ttu-id="a5440-115">Hello 統一資源識別元 (URI) 的一部分使用 toosend hello 要求 toohello 伺服器，您也必須使用 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="a5440-115">You must also use hello cluster name as part of hello Uniform Resource Identifier (URI) used toosend hello requests toohello server.</span></span>
> 
> <span data-ttu-id="a5440-116">本章節中的 hello 命令，請將**USERNAME** hello 使用者 tooauthenticate toohello 叢集與取代**密碼**hello hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="a5440-116">For hello commands in this section, replace **USERNAME** with hello user tooauthenticate toohello cluster, and replace **PASSWORD** with hello password for hello user account.</span></span> <span data-ttu-id="a5440-117">取代**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="a5440-117">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>
> 
> <span data-ttu-id="a5440-118">hello REST API 會透過保護[基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。</span><span class="sxs-lookup"><span data-stu-id="a5440-118">hello REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="a5440-119">您永遠應該利用安全 HTTP (HTTPS) toohelp 確保您的認證會安全地傳送 toohello 伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="a5440-119">You should always make requests by using Secure HTTP (HTTPS) toohelp ensure that your credentials are securely sent toohello server.</span></span>
> 
> 

1. <span data-ttu-id="a5440-120">從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="a5440-120">From a command line, use hello following command tooverify that you can connect tooyour HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="a5440-121">您應該會收到類似 toohello 後的回應：</span><span class="sxs-lookup"><span data-stu-id="a5440-121">You should receive a response similar toohello following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="a5440-122">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5440-122">hello parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="a5440-123">**-u** -使用 tooauthenticate hello 要求 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="a5440-123">**-u** - hello user name and password used tooauthenticate hello request.</span></span>
   * <span data-ttu-id="a5440-124">**-G** - 指出這是 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="a5440-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="a5440-125">hello 開頭 hello URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，將會針對所有要求 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="a5440-125">hello beginning of hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be hello same for all requests.</span></span> <span data-ttu-id="a5440-126">hello 路徑**/status**，表示該 hello 要求 tooreturn WebHCat (也稱為 Templeton) 狀態 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a5440-126">hello path, **/status**, indicates that hello request is tooreturn a status of WebHCat (also known as Templeton) for hello server.</span></span> 
2. <span data-ttu-id="a5440-127">使用下列 toosubmit sqoop 工作 hello:</span><span class="sxs-lookup"><span data-stu-id="a5440-127">Use hello following toosubmit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="a5440-128">此命令中使用的 hello 參數如下所示：</span><span class="sxs-lookup"><span data-stu-id="a5440-128">hello parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="a5440-129">**-d** -自`-G`不使用 hello 要求預設 toohello POST 方法。</span><span class="sxs-lookup"><span data-stu-id="a5440-129">**-d** - Since `-G` is not used, hello request defaults toohello POST method.</span></span> <span data-ttu-id="a5440-130">`-d`指定傳送嗨資料值與 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="a5440-130">`-d` specifies hello data values that are sent with hello request.</span></span>

        * <span data-ttu-id="a5440-131">**user.name** -hello 使用者執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="a5440-131">**user.name** - hello user that is running hello command.</span></span>

        * <span data-ttu-id="a5440-132">**命令**-hello Sqoop 命令 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="a5440-132">**command** - hello Sqoop command tooexecute.</span></span>

        * <span data-ttu-id="a5440-133">**statusdir** -hello 為此工作狀態的 hello 目錄寫入。</span><span class="sxs-lookup"><span data-stu-id="a5440-133">**statusdir** - hello directory that hello status for this job will be written to.</span></span>

    <span data-ttu-id="a5440-134">此命令應該會傳回可以用的 toocheck hello hello 工作狀態的作業識別碼。</span><span class="sxs-lookup"><span data-stu-id="a5440-134">This command should return a job ID that can be used toocheck hello status of hello job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="a5440-135">hello 工作，下列命令使用 hello toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="a5440-135">toocheck hello status of hello job, use hello following command.</span></span> <span data-ttu-id="a5440-136">取代**JOBID** hello hello 上一個步驟中傳回的值。</span><span class="sxs-lookup"><span data-stu-id="a5440-136">Replace **JOBID** with hello value returned in hello previous step.</span></span> <span data-ttu-id="a5440-137">例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後**JOBID**會`job_1415651640909_0026`。</span><span class="sxs-lookup"><span data-stu-id="a5440-137">For example, if hello return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="a5440-138">如果 hello 工作已完成，將會 hello 狀態**SUCCEEDED**。</span><span class="sxs-lookup"><span data-stu-id="a5440-138">If hello job has finished, hello state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a5440-139">此 Curl 要求會傳回 JavaScript 物件標記法 (JSON) 文件以 hello 工作; 的相關資訊使用 jq tooretrieve 只 hello 狀態值。</span><span class="sxs-lookup"><span data-stu-id="a5440-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about hello job; jq is used tooretrieve only hello state value.</span></span>
   > 
   > 
2. <span data-ttu-id="a5440-140">一旦 hello hello 作業狀態已變更過**SUCCEEDED**，您可以從 Azure Blob 儲存體擷取 hello hello 作業結果。</span><span class="sxs-lookup"><span data-stu-id="a5440-140">Once hello state of hello job has changed too**SUCCEEDED**, you can retrieve hello results of hello job from Azure Blob storage.</span></span> <span data-ttu-id="a5440-141">hello `statusdir` hello 查詢傳遞的參數包含 hello 位置 hello 輸出檔; 在此情況下， **wasb: / 範例/curl**。</span><span class="sxs-lookup"><span data-stu-id="a5440-141">hello `statusdir` parameter passed with hello query contains hello location of hello output file; in this case, **wasb:///example/curl**.</span></span> <span data-ttu-id="a5440-142">此地址將 hello 工作的 hello 輸出儲存在 hello**範例/curl**目錄 hello HDInsight 叢集所用的預設儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="a5440-142">This address stores hello output of hello job in hello **example/curl** directory on hello default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="a5440-143">您可以列出並下載這些檔案使用 hello [Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="a5440-143">You can list and download these files by using hello [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="a5440-144">Toolist 中的檔案，例如**範例/curl**，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a5440-144">For example, toolist files in **example/curl**, use hello following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="a5440-145">toodownload 檔案，使用下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a5440-145">toodownload a file, use hello following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="a5440-146">您必須指定 hello 使用 hello 包含 hello blob 儲存體帳戶名稱`-a`和`-k`參數或使用組 hello **AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_存取\_金鑰**環境變數。</span><span class="sxs-lookup"><span data-stu-id="a5440-146">You must either specify hello storage account name that contains hello blob by using hello `-a` and `-k` parameters, or set hello **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="a5440-147">如需詳細資訊，請參閱 <a href="hdinsight-upload-data.md" target="_blank"。</span><span class="sxs-lookup"><span data-stu-id="a5440-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="a5440-148">限制</span><span class="sxs-lookup"><span data-stu-id="a5440-148">Limitations</span></span>
* <span data-ttu-id="a5440-149">大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="a5440-149">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="a5440-150">批次處理-與 linux 的 HDInsight，當使用 hello`-batch`切換時執行插入、 Sqoop 會執行多個的插入，而不是批次處理 hello 插入作業。</span><span class="sxs-lookup"><span data-stu-id="a5440-150">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="a5440-151">摘要</span><span class="sxs-lookup"><span data-stu-id="a5440-151">Summary</span></span>
<span data-ttu-id="a5440-152">如本文所示，您可以使用 HDInsight 叢集上的未經處理的 HTTP 要求 toorun、 監視器和檢視 hello 結果的 Sqoop 工作。</span><span class="sxs-lookup"><span data-stu-id="a5440-152">As demonstrated in this document, you can use a raw HTTP request toorun, monitor, and view hello results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="a5440-153">如需有關使用本文章中的 hello REST 介面的詳細資訊，請參閱 hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API 指南</a>。</span><span class="sxs-lookup"><span data-stu-id="a5440-153">For more information on hello REST interface used in this article, see hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5440-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5440-154">Next steps</span></span>
<span data-ttu-id="a5440-155">Hive 與 HDInsight 搭配使用的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="a5440-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="a5440-156">在 HDInsight 上將 Sqoop 與 Hadoop 搭配使用</span><span class="sxs-lookup"><span data-stu-id="a5440-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="a5440-157">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="a5440-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a5440-158">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a5440-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a5440-159">搭配 HDInsight 上的 Hadoop 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="a5440-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a5440-160">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a5440-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


