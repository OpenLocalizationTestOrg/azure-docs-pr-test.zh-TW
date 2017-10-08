---
title: "aaaUse HDInsight 的 Azure 中的遠端桌面的 Hadoop Pig |Microsoft 文件"
description: "了解如何 toouse hello Pig 命令 toorun Pig 拉丁陳述式從 HDInsight 中的遠端桌面連線 tooa Windows 為基礎的 Hadoop 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="30b0d-103">從遠端桌面連線執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="30b0d-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="30b0d-104">本文件提供逐步解說使用 hello Pig 命令 toorun Pig 拉丁陳述式從遠端桌面連線 tooa Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="30b0d-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="30b0d-105">Pig 拉丁可讓您透過描述資料轉換的 toocreate MapReduce 應用程式，而非對應並減少函式。</span><span class="sxs-lookup"><span data-stu-id="30b0d-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30b0d-106">只有在使用 Windows 做為 hello 作業系統的 HDInsight 叢集上使用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="30b0d-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="30b0d-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="30b0d-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="30b0d-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="30b0d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="30b0d-109">HDInsight 3.4 或更高，請參閱[HDInsight 和 SSH 搭配使用 Pig](hdinsight-hadoop-use-pig-ssh.md)有關以互動方式執行 Pig 工作直接在 hello 叢集從命令列。</span><span class="sxs-lookup"><span data-stu-id="30b0d-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="30b0d-110"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="30b0d-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="30b0d-111">toocomplete hello 本文中的步驟，您將需要下列 hello。</span><span class="sxs-lookup"><span data-stu-id="30b0d-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="30b0d-112">Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="30b0d-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="30b0d-113">執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="30b0d-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="30b0d-114"><a id="connect"></a>使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="30b0d-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="30b0d-115">Hello HDInsight 叢集，啟用遠端桌面，然後依照指示 hello 連接 tooit[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="30b0d-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="30b0d-116"><a id="pig"></a>使用 hello Pig 命令</span><span class="sxs-lookup"><span data-stu-id="30b0d-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="30b0d-117">您有遠端桌面連線之後，請啟動 hello **Hadoop 命令列**hello 桌面上使用 hello 圖示。</span><span class="sxs-lookup"><span data-stu-id="30b0d-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="30b0d-118">使用下列 toostart hello Pig 命令 hello:</span><span class="sxs-lookup"><span data-stu-id="30b0d-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="30b0d-119">您會看到 `grunt>` 提示字元。</span><span class="sxs-lookup"><span data-stu-id="30b0d-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="30b0d-120">輸入下列陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="30b0d-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="30b0d-121">此命令會載入 hello 記錄檔中的 hello hello sample.log 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="30b0d-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="30b0d-122">您可以使用下列命令的 hello 檢視 hello hello 檔案內容：</span><span class="sxs-lookup"><span data-stu-id="30b0d-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="30b0d-123">Hello 資料轉換從每一筆記錄套用的規則運算式 tooextract 只有 hello 記錄層級：</span><span class="sxs-lookup"><span data-stu-id="30b0d-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="30b0d-124">您可以使用**傾印**tooview hello hello 轉換後的資料。</span><span class="sxs-lookup"><span data-stu-id="30b0d-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="30b0d-125">在此案例中為 `DUMP LEVELS;`。</span><span class="sxs-lookup"><span data-stu-id="30b0d-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="30b0d-126">繼續使用下列陳述式的 hello 套用轉換。</span><span class="sxs-lookup"><span data-stu-id="30b0d-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="30b0d-127">使用`DUMP`tooview hello 結果的每個步驟之後的 hello 轉換。</span><span class="sxs-lookup"><span data-stu-id="30b0d-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="30b0d-128">陳述式</span><span class="sxs-lookup"><span data-stu-id="30b0d-128">Statement</span></span></th><th><span data-ttu-id="30b0d-129">作用</span><span class="sxs-lookup"><span data-stu-id="30b0d-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="30b0d-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="30b0d-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="30b0d-131">移除包含 hello 記錄層級的 null 值的資料列，並將 hello 結果儲存到 FILTEREDLEVELS。</span><span class="sxs-lookup"><span data-stu-id="30b0d-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="30b0d-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="30b0d-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="30b0d-133">群組 hello 的記錄層級的資料列，並將 hello 結果儲存到 GROUPEDLEVELS。</span><span class="sxs-lookup"><span data-stu-id="30b0d-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="30b0d-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="30b0d-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="30b0d-135">建立一組新的資料，其中包含每個唯一記錄層級值和其發生次數。</span><span class="sxs-lookup"><span data-stu-id="30b0d-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="30b0d-136">這會儲存到 FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="30b0d-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="30b0d-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="30b0d-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="30b0d-138">訂單 hello 記錄層級計數 （遞減），並儲存成結果</span><span class="sxs-lookup"><span data-stu-id="30b0d-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="30b0d-139">
6.您也可以儲存轉換的 hello 結果使用 hello`STORE`陳述式。</span><span class="sxs-lookup"><span data-stu-id="30b0d-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="30b0d-140">例如，下列命令的 hello 儲存 hello `RESULT` toohello **/example/data/pigout**目錄中為您的叢集 hello 預設儲存體容器：</span><span class="sxs-lookup"><span data-stu-id="30b0d-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="30b0d-141">hello 資料會儲存在名為的檔案中的 hello 指定目錄**一部分 nnnnn**。</span><span class="sxs-lookup"><span data-stu-id="30b0d-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="30b0d-142">如果 hello 目錄已經存在，您會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="30b0d-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="30b0d-143">tooexit hello 提示字元中，grunt 輸入 hello 陳述式之後。</span><span class="sxs-lookup"><span data-stu-id="30b0d-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="30b0d-144">Pig Latin 批次檔</span><span class="sxs-lookup"><span data-stu-id="30b0d-144">Pig Latin batch files</span></span>
<span data-ttu-id="30b0d-145">您也可以使用 hello Pig 命令 toorun Pig 拉丁包含在檔案中。</span><span class="sxs-lookup"><span data-stu-id="30b0d-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="30b0d-146">結束 hello grunt 提示字元後, 開啟**記事本**並建立新的檔案命名為**pigbatch.pig**在 hello **%pig_home%**目錄。</span><span class="sxs-lookup"><span data-stu-id="30b0d-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="30b0d-147">型別或貼上 hello 下列各行至 hello **pigbatch.pig**檔案，並將其儲存：</span><span class="sxs-lookup"><span data-stu-id="30b0d-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="30b0d-148">使用 hello 遵循 toorun hello **pigbatch.pig**使用 hello pig 命令的檔案。</span><span class="sxs-lookup"><span data-stu-id="30b0d-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="30b0d-149">Hello 批次工作完成時，您應該會看到下列輸出，應該是 hello 相同做為當您使用的 hello `DUMP RESULT;` hello 前述步驟中：</span><span class="sxs-lookup"><span data-stu-id="30b0d-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="30b0d-150"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="30b0d-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="30b0d-151">如您所見，hello Pig 命令可讓您 toointeractively 執行 MapReduce 作業，或執行批次檔中儲存的 Pig 拉丁作業。</span><span class="sxs-lookup"><span data-stu-id="30b0d-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="30b0d-152"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="30b0d-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="30b0d-153">如需 HDInsight 中 Pig 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="30b0d-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="30b0d-154">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="30b0d-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="30b0d-155">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="30b0d-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="30b0d-156">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="30b0d-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="30b0d-157">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="30b0d-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
