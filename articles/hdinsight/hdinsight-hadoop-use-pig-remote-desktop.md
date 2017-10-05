---
title: "在 HDInsight 中搭配使用 Hadoop Pig 與遠端桌面 - Azure | Microsoft Docs"
description: "學習如何使用 Pig 命令，從連往 HDInsight 中 Windows 型 Hadoop 叢集的遠端桌面連線執行 Pig Latin 陳述式。"
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="22de6-103">從遠端桌面連線執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="22de6-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="22de6-104">本文件逐步解說如何使用 Pig 命令，從連往 Windows 型 HDInsight 叢集的遠端桌面連線執行 Pig Latin 陳述式。</span><span class="sxs-lookup"><span data-stu-id="22de6-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="22de6-105">Pig Latin 可讓您透過描述資料轉換來建立 MapReduce 應用程式，而不是建立對應和縮減函數。</span><span class="sxs-lookup"><span data-stu-id="22de6-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22de6-106">只有在使用 Windows 作為作業系統的 HDInsight 叢集上才能使用「遠端桌面」。</span><span class="sxs-lookup"><span data-stu-id="22de6-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="22de6-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="22de6-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22de6-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="22de6-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="22de6-109">針對 HDInsight 3.4 或更新版本，請參閱[使用 Pig 搭配 HDInsight 和 SSH](hdinsight-hadoop-use-pig-ssh.md)，以了解如何從命令列以互動方式直接在叢集上執行 Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="22de6-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="22de6-110"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="22de6-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="22de6-111">若要完成本文中的步驟，您需要下列項目。</span><span class="sxs-lookup"><span data-stu-id="22de6-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="22de6-112">Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="22de6-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="22de6-113">執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="22de6-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="22de6-114"><a id="connect"></a>使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="22de6-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="22de6-115">依照 [使用 RDP 連線到 HDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)中的指示，為 HDInsight 叢集啟用遠端桌面，然後進行連線。</span><span class="sxs-lookup"><span data-stu-id="22de6-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="22de6-116"><a id="pig"></a>使用 Pig 命令</span><span class="sxs-lookup"><span data-stu-id="22de6-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="22de6-117">在具有遠端桌面連線後，使用桌面上的圖示來啟動 **Hadoop 命令列** 。</span><span class="sxs-lookup"><span data-stu-id="22de6-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="22de6-118">使用下列命令來啟動 Pig 命令：</span><span class="sxs-lookup"><span data-stu-id="22de6-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="22de6-119">您會看到 `grunt>` 提示字元。</span><span class="sxs-lookup"><span data-stu-id="22de6-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="22de6-120">輸入下列陳述式：</span><span class="sxs-lookup"><span data-stu-id="22de6-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="22de6-121">此命令會將 sample.log 檔案的內容載入至 LOGS 檔案。</span><span class="sxs-lookup"><span data-stu-id="22de6-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="22de6-122">您可以使用下列命令檢視檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="22de6-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="22de6-123">套用規則運算式以僅擷取每筆記錄的記錄層級，來轉換資料：</span><span class="sxs-lookup"><span data-stu-id="22de6-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="22de6-124">轉換之後，您可以使用 **DUMP** 來檢視資料。</span><span class="sxs-lookup"><span data-stu-id="22de6-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="22de6-125">在此案例中為 `DUMP LEVELS;`。</span><span class="sxs-lookup"><span data-stu-id="22de6-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="22de6-126">使用下列陳述式，繼續套用轉換。</span><span class="sxs-lookup"><span data-stu-id="22de6-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="22de6-127">使用 `DUMP` 檢視每個步驟後的轉換結果。</span><span class="sxs-lookup"><span data-stu-id="22de6-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="22de6-128">陳述式</span><span class="sxs-lookup"><span data-stu-id="22de6-128">Statement</span></span></th><th><span data-ttu-id="22de6-129">作用</span><span class="sxs-lookup"><span data-stu-id="22de6-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="22de6-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span><span class="sxs-lookup"><span data-stu-id="22de6-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="22de6-131">移除含有記錄層級之 Null 值的資料列，並將結果儲存到 FILTEREDLEVELS。</span><span class="sxs-lookup"><span data-stu-id="22de6-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="22de6-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="22de6-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="22de6-133">依記錄層級對資料列進行分組，並將結果儲存到 GROUPEDLEVELS。</span><span class="sxs-lookup"><span data-stu-id="22de6-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="22de6-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span><span class="sxs-lookup"><span data-stu-id="22de6-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="22de6-135">建立一組新的資料，其中包含每個唯一記錄層級值和其發生次數。</span><span class="sxs-lookup"><span data-stu-id="22de6-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="22de6-136">這會儲存到 FREQUENCIES</span><span class="sxs-lookup"><span data-stu-id="22de6-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="22de6-137">RESULT = order FREQUENCIES by COUNT desc;</span><span class="sxs-lookup"><span data-stu-id="22de6-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="22de6-138">依計數排序記錄層級 (遞減)，並且儲存到 RESULT</span><span class="sxs-lookup"><span data-stu-id="22de6-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="22de6-139">
6.您也可以使用 `STORE` 陳述式儲存轉換結果。</span><span class="sxs-lookup"><span data-stu-id="22de6-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="22de6-140">例如，下列命令會將 `RESULT` 儲存到叢集之預設儲存體容器中的 **/example/data/pigout** 目錄：</span><span class="sxs-lookup"><span data-stu-id="22de6-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="22de6-141">資料會儲存到所指定目錄中名為 **part-nnnnn**的檔案中。</span><span class="sxs-lookup"><span data-stu-id="22de6-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="22de6-142">如果目錄已經存在，則會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="22de6-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="22de6-143">若要結束 grunt 提示字元，請輸入下列陳述式。</span><span class="sxs-lookup"><span data-stu-id="22de6-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="22de6-144">Pig Latin 批次檔</span><span class="sxs-lookup"><span data-stu-id="22de6-144">Pig Latin batch files</span></span>
<span data-ttu-id="22de6-145">您也可以使用 Pig 命令執行檔案中所含的 Pig Latin。</span><span class="sxs-lookup"><span data-stu-id="22de6-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="22de6-146">結束 grunt 提示字元之後，請開啟**記事本**，並在 **%PIG_HOME%** 目錄中建立名為 **pigbatch.pig** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="22de6-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="22de6-147">在 **pigbatch.pig** 檔案中輸入或貼上下列數行，然後予以儲存：</span><span class="sxs-lookup"><span data-stu-id="22de6-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="22de6-148">使用下列命令，以使用 pig 命令來執行 **pigbatch.pig** 檔案。</span><span class="sxs-lookup"><span data-stu-id="22de6-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="22de6-149">批次工作完成後，您應該會看到下列輸出，而輸出應該會與先前步驟中使用 `DUMP RESULT;` 時相同：</span><span class="sxs-lookup"><span data-stu-id="22de6-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="22de6-150"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="22de6-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="22de6-151">如您所見，Pig 命令可讓您以互動方式執行 MapReduce 作業，或執行批次檔中所儲存的 Pig Latin 工作。</span><span class="sxs-lookup"><span data-stu-id="22de6-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="22de6-152"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="22de6-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="22de6-153">如需 HDInsight 中 Pig 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="22de6-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="22de6-154">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="22de6-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="22de6-155">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="22de6-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="22de6-156">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="22de6-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="22de6-157">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="22de6-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
