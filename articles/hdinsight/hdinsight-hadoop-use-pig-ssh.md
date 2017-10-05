---
title: "在 HDInsight 叢集上搭配使用 Hadoop Pig 與 SSH - Azure | Microsoft Docs"
description: "學習如何使用 SSH 連線到以 Linux 為基礎的 Hadoop 叢集，然後使用 Pig 命令以互動方式或批次工作形式執行 Pig Latin 陳述式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e4c893ef4bfa573dd9fbc9c9b0ae296720769842
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-the-pig-command-ssh"></a><span data-ttu-id="9af79-103">使用 Pig 命令 (SSH) 在以 Linux 為基礎的叢集上執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="9af79-103">Run Pig jobs on a Linux-based cluster with the Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="9af79-104">了解如何透過與 HDInsight 叢集的 SSH 連線以互動方式執行 Pig 作業。</span><span class="sxs-lookup"><span data-stu-id="9af79-104">Learn how to interactively run Pig jobs from an SSH connection to your HDInsight cluster.</span></span> <span data-ttu-id="9af79-105">Pig Latin 程式設計語言可讓您描述套用至輸入資料來產生想要輸出的轉換。</span><span class="sxs-lookup"><span data-stu-id="9af79-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9af79-106">此文件中的步驟需要以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9af79-106">The steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9af79-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="9af79-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9af79-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9af79-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9af79-109"><a id="ssh"></a>使用 SSH 連線</span><span class="sxs-lookup"><span data-stu-id="9af79-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="9af79-110">使用 SSH 連線到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9af79-110">Use SSH to connect to your HDInsight cluster.</span></span> <span data-ttu-id="9af79-111">下列範例會以名為 **sshuser**的帳戶連線至名為 **myhdinsight** 的叢集：</span><span class="sxs-lookup"><span data-stu-id="9af79-111">The following example connects to a cluster named **myhdinsight** as the account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="9af79-112">**如果您提供憑證金鑰進行 SSH 驗證** (在建立 HDInsight 叢集時)，可能需要指定用戶端系統上私密金鑰的位置。</span><span class="sxs-lookup"><span data-stu-id="9af79-112">**If you provided a certificate key for SSH authentication** when you created the HDInsight cluster, you may need to specify the location of the private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="9af79-113">**如果您提供密碼進行 SSH 驗證** (在建立 HDInsight 叢集時)，請在出現提示時提供密碼。</span><span class="sxs-lookup"><span data-stu-id="9af79-113">**If you provided a password for SSH authentication** when you created the HDInsight cluster, provide the password when prompted.</span></span>

<span data-ttu-id="9af79-114">如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="9af79-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9af79-115"><a id="pig"></a>使用 Pig 命令</span><span class="sxs-lookup"><span data-stu-id="9af79-115"><a id="pig"></a>Use the Pig command</span></span>

1. <span data-ttu-id="9af79-116">連線之後，使用下列命令來啟動 Pig 命令列介面 (CLI)：</span><span class="sxs-lookup"><span data-stu-id="9af79-116">Once connected, start the Pig command-line interface (CLI) by using the following command:</span></span>

        pig

    <span data-ttu-id="9af79-117">隨後，您應該會看到 `grunt>` 提示字元。</span><span class="sxs-lookup"><span data-stu-id="9af79-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="9af79-118">輸入下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="9af79-118">Enter the following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="9af79-119">此命令會將 sample.log 檔案的內容載入至 LOGS。</span><span class="sxs-lookup"><span data-stu-id="9af79-119">This command loads the contents of the sample.log file into LOGS.</span></span> <span data-ttu-id="9af79-120">您可以使用下列陳述式檢視檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="9af79-120">You can view the contents of the file by using the following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="9af79-121">接下來是轉換資料，方法是套用規則運算式，並使用下列陳述式僅擷取每筆記錄的記錄層級：</span><span class="sxs-lookup"><span data-stu-id="9af79-121">Next, transform the data by applying a regular expression to extract only the logging level from each record by using the following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="9af79-122">轉換之後，您可以使用 **DUMP** 來檢視資料。</span><span class="sxs-lookup"><span data-stu-id="9af79-122">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="9af79-123">在此案例中，請使用 `DUMP LEVELS;`。</span><span class="sxs-lookup"><span data-stu-id="9af79-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="9af79-124">使用下列表格中的陳述式繼續套用轉換：</span><span class="sxs-lookup"><span data-stu-id="9af79-124">Continue applying transformations by using the statements in the following table:</span></span>

    | <span data-ttu-id="9af79-125">Pig Latin 陳述式</span><span class="sxs-lookup"><span data-stu-id="9af79-125">Pig Latin statement</span></span> | <span data-ttu-id="9af79-126">陳述式的作用</span><span class="sxs-lookup"><span data-stu-id="9af79-126">What the statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="9af79-127">移除含有記錄層級之 Null 值的資料列，並將結果儲存到 `FILTEREDLEVELS`。</span><span class="sxs-lookup"><span data-stu-id="9af79-127">Removes rows that contain a null value for the log level and stores the results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="9af79-128">依記錄層級對資料列進行分組，並將結果儲存到 `GROUPEDLEVELS`。</span><span class="sxs-lookup"><span data-stu-id="9af79-128">Groups the rows by log level and stores the results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="9af79-129">建立一組資料，其中包含每個唯一記錄層級值和其發生次數。</span><span class="sxs-lookup"><span data-stu-id="9af79-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="9af79-130">資料集會儲存到 `FREQUENCIES`。</span><span class="sxs-lookup"><span data-stu-id="9af79-130">The data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="9af79-131">依計數排序記錄層級 (遞減)，並且儲存到 `RESULT`。</span><span class="sxs-lookup"><span data-stu-id="9af79-131">Orders the log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="9af79-132">使用 `DUMP` 檢視每個步驟後的轉換結果。</span><span class="sxs-lookup"><span data-stu-id="9af79-132">Use `DUMP` to view the result of the transformation after each step.</span></span>

5. <span data-ttu-id="9af79-133">您也可以使用 `STORE` 陳述式儲存轉換結果。</span><span class="sxs-lookup"><span data-stu-id="9af79-133">You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="9af79-134">例如，下列陳述式會將 `RESULT` 儲存到叢集之預設儲存體上的 `/example/data/pigout` 目錄：</span><span class="sxs-lookup"><span data-stu-id="9af79-134">For example, the following statement saves the `RESULT` to the `/example/data/pigout` directory on the default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="9af79-135">資料會儲存到所指定目錄中名為 `part-nnnnn` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="9af79-135">The data is stored in the specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="9af79-136">如果目錄已經存在，則會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="9af79-136">If the directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="9af79-137">若要結束 grunt 提示字元，請輸入下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="9af79-137">To exit the grunt prompt, enter the following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="9af79-138">Pig Latin 批次檔</span><span class="sxs-lookup"><span data-stu-id="9af79-138">Pig Latin batch files</span></span>

<span data-ttu-id="9af79-139">您也可以使用 Pig 命令執行檔案中所含的 Pig Latin。</span><span class="sxs-lookup"><span data-stu-id="9af79-139">You can also use the Pig command to run Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="9af79-140">結束 grunt 提示字元之後，請使用下列命令將 STDIN 以管道方式輸出到名為 `pigbatch.pig` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="9af79-140">After exiting the grunt prompt, use the following command to pipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="9af79-141">此檔案會建立在 SSH 使用者帳戶的主目錄中。</span><span class="sxs-lookup"><span data-stu-id="9af79-141">This file is created in the home directory for the SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="9af79-142">輸入或貼上下列數行，然後在完成後使用 Ctrl+D。</span><span class="sxs-lookup"><span data-stu-id="9af79-142">Type or paste the following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="9af79-143">使用下列命令，以使用 Pig 命令來執行 `pigbatch.pig` 檔案。</span><span class="sxs-lookup"><span data-stu-id="9af79-143">Use the following command to run the `pigbatch.pig` file by using the Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="9af79-144">當批次作業完成時，您會看到下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="9af79-144">Once the batch job finishes, you see the following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="9af79-145"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="9af79-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9af79-146">如需有關 HDInsight 中 Pig 的一般資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="9af79-146">For general information on Pig in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="9af79-147">搭配 HDInsight 上的 Hadoop 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="9af79-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9af79-148">如需搭配 HDInsight 上的 Hadoop 使用之其他方式的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="9af79-148">For more information on other ways to work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="9af79-149">搭配 HDInsight 上的 Hadoop 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="9af79-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9af79-150">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9af79-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
