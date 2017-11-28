---
title: "在 HDInsight 叢集的 Azure 上 aaaUse 透過 SSH 的 Hadoop Pig |Microsoft 文件"
description: "深入了解如何使用 SSH 的連接 tooa linux Hadoop 叢集，然後使用 hello Pig 命令 toorun Pig 拉丁陳述式，以互動方式或以批次作業。"
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
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="8ba2a-103">Pig 工作在叢集上執行 linux 與 hello Pig 命令 (SSH)</span><span class="sxs-lookup"><span data-stu-id="8ba2a-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="8ba2a-104">了解 toointeractively 從 SSH 連線 tooyour HDInsight 叢集中執行 Pig 工作的方式。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="8ba2a-105">hello Pig 拉丁程式設計語言，可讓您輸入的套用的 toohello 資料 tooproduce hello 預期輸出 toodescribe 轉換。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ba2a-106">hello 本文件中的步驟需要以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8ba2a-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8ba2a-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="8ba2a-109"><a id="ssh"></a>使用 SSH 連線</span><span class="sxs-lookup"><span data-stu-id="8ba2a-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="8ba2a-110">使用 SSH tooconnect tooyour HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="8ba2a-111">hello 下列範例會連接名為 tooa 叢集**myhdinsight** hello 帳戶命名為**sshuser**:</span><span class="sxs-lookup"><span data-stu-id="8ba2a-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="8ba2a-112">**如果您提供的 SSH 驗證憑證金鑰**當您建立 hello HDInsight 叢集，您可能需要 toospecify hello 位置 hello 私密金鑰的用戶端系統上。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="8ba2a-113">**如果您提供密碼 SSH 驗證**建立 hello HDInsight 叢集，提供 hello 密碼提示。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="8ba2a-114">如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="8ba2a-115"><a id="pig"></a>使用 hello Pig 命令</span><span class="sxs-lookup"><span data-stu-id="8ba2a-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="8ba2a-116">一旦連接之後，請使用下列命令的 hello 啟動 hello Pig 命令列介面 (CLI):</span><span class="sxs-lookup"><span data-stu-id="8ba2a-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="8ba2a-117">隨後，您應該會看到 `grunt>` 提示字元。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="8ba2a-118">輸入下列陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ba2a-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="8ba2a-119">此命令會載入記錄檔中的 hello hello sample.log 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="8ba2a-120">您可以使用下列陳述式的 hello 檢視 hello hello 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="8ba2a-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="8ba2a-121">接下來，從每一筆記錄套用的規則運算式 tooextract 只有 hello 記錄層級，使用下列陳述式的 hello 轉換 hello 資料：</span><span class="sxs-lookup"><span data-stu-id="8ba2a-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="8ba2a-122">您可以使用**傾印**tooview hello hello 轉換後的資料。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="8ba2a-123">在此案例中，請使用 `DUMP LEVELS;`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="8ba2a-124">繼續使用 hello 下表中的 hello 陳述式來套用轉換：</span><span class="sxs-lookup"><span data-stu-id="8ba2a-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="8ba2a-125">Pig Latin 陳述式</span><span class="sxs-lookup"><span data-stu-id="8ba2a-125">Pig Latin statement</span></span> | <span data-ttu-id="8ba2a-126">哪些 hello 陳述式會執行</span><span class="sxs-lookup"><span data-stu-id="8ba2a-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="8ba2a-127">移除包含 hello 記錄層級的 null 值的資料列，並將結果 hello `FILTEREDLEVELS`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="8ba2a-128">群組 hello 記錄層級的資料列，並會儲存成 hello 結果`GROUPEDLEVELS`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="8ba2a-129">建立一組資料，其中包含每個唯一記錄層級值和其發生次數。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="8ba2a-130">hello 資料集就會儲存至`FREQUENCIES`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="8ba2a-131">依計數 （遞減） 排序 hello 記錄層級，並且將儲存到`RESULT`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="8ba2a-132">使用`DUMP`tooview hello 結果的每個步驟之後的 hello 轉換。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="8ba2a-133">您也可以儲存轉換的 hello 結果使用 hello`STORE`陳述式。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="8ba2a-134">例如，陳述式之後的 hello 儲存 hello `RESULT` toohello `/example/data/pigout` hello 預設儲存體叢集上的目錄：</span><span class="sxs-lookup"><span data-stu-id="8ba2a-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="8ba2a-135">hello 資料會儲存在名為的檔案中的 hello 指定目錄`part-nnnnn`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="8ba2a-136">如果 hello 目錄已經存在，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="8ba2a-137">tooexit hello 提示字元中，grunt 輸入陳述式之後的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ba2a-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="8ba2a-138">Pig Latin 批次檔</span><span class="sxs-lookup"><span data-stu-id="8ba2a-138">Pig Latin batch files</span></span>

<span data-ttu-id="8ba2a-139">您也可以使用 hello Pig 命令 toorun Pig 拉丁包含在檔案中。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="8ba2a-140">結束 hello grunt 提示字元後, 使用 hello 下列命令到名為 toopipe STDIN `pigbatch.pig`。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="8ba2a-141">此檔案會建立 hello hello SSH 使用者帳戶的主目錄中。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="8ba2a-142">輸入或貼上 hello 下列行，然後再使用 Ctrl + D 完成。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="8ba2a-143">使用 hello 下列命令 toorun hello`pigbatch.pig`使用 hello Pig 命令的檔案。</span><span class="sxs-lookup"><span data-stu-id="8ba2a-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="8ba2a-144">一旦 hello 批次工作完成時，您會看見 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="8ba2a-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="8ba2a-145"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="8ba2a-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="8ba2a-146">Pig HDInsight 中的一般資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ba2a-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="8ba2a-147">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="8ba2a-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="8ba2a-148">如需有關其他方式 toowork Hadoop HDInsight 上使用，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="8ba2a-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="8ba2a-149">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="8ba2a-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="8ba2a-150">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="8ba2a-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
