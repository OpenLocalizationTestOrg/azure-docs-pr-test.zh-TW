---
title: "在 HDInsight 中執行 Hadoop 範例 - Azure | Microsoft Docs"
description: "利用提供的範例開始使用 Azure HDInsight 服務。 使用 PowerShell 指令碼在資料叢集上執行 MapReduce 程式。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 741cce6f2c81efed1e4bd0547fcb46a231815263
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="f057e-104">在以 Windows 為基礎的 HDInsight 中執行 Hadoop MapReduce 範例</span><span class="sxs-lookup"><span data-stu-id="f057e-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="f057e-105">我們提供了一組範例，協助您使用 Azure HDInsight 並開始在 Hadoop 叢集上執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="f057e-105">A set of samples are provided to help you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="f057e-106">這些範例可套用在您所建立的每個 HDInsight 受管理叢集上。</span><span class="sxs-lookup"><span data-stu-id="f057e-106">These samples are made available on each of the HDInsight managed clusters that you create.</span></span> <span data-ttu-id="f057e-107">執行這些範例可協助您熟悉使用 Azure PowerShell Cmdlet 在 Hadoop 叢集上執行作業。</span><span class="sxs-lookup"><span data-stu-id="f057e-107">Running these samples familiarize you with using Azure PowerShell cmdlets to run jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="f057e-108">[字數統計][hdinsight-sample-wordcount]：計算文字檔中的文字出現次數。</span><span class="sxs-lookup"><span data-stu-id="f057e-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="f057e-109">[C# 串流字數統計][hdinsight-sample-csharp-streaming]：使用 Hadoop 串流介面計算文字檔中的文字出現次數。</span><span class="sxs-lookup"><span data-stu-id="f057e-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using the Hadoop streaming interface.</span></span>
* <span data-ttu-id="f057e-110">[Pi 估算器][hdinsight-sample-pi-estimator]：使用統計 (擬蒙特卡羅法) 方法來估計 Pi 的值。</span><span class="sxs-lookup"><span data-stu-id="f057e-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span>
* <span data-ttu-id="f057e-111">[10-GB Graysort][hdinsight-sample-10gb-graysort]：使用 HDInsight 在 10 GB 檔案上執行一般用途的 GraySort。</span><span class="sxs-lookup"><span data-stu-id="f057e-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="f057e-112">有三個工作可執行：Teragen、Terasort 和 Teravalidate，分別用來產生資料、排序資料，以及確認資料已適當排序。</span><span class="sxs-lookup"><span data-stu-id="f057e-112">There are three jobs to run: Teragen to generate the data, Terasort to sort the data, and Teravalidate to confirm that the data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="f057e-113">原始程式碼可以在附錄中找到。</span><span class="sxs-lookup"><span data-stu-id="f057e-113">The source code can be found in the Appendix.</span></span>

<span data-ttu-id="f057e-114">網路上有許多 Hadoop 相關技術 (例如 Java 型 MapReduce 程式設計和串流) 的文件可供參考，此外也有適用於 Windows PowerShell 指令碼之 Cmdlet 的相關文件。</span><span class="sxs-lookup"><span data-stu-id="f057e-114">Much additional documentation exists on the web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about the cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="f057e-115">如需有關這些資源的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f057e-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="f057e-116">在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="f057e-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="f057e-117">在 HDInsight 上提交 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="f057e-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="f057e-118">[Azure HDInsight 簡介][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="f057e-118">[Introduction to Azure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="f057e-119">時至今日，很多人選擇 Hive 和 Pig 而非 MapReduce。</span><span class="sxs-lookup"><span data-stu-id="f057e-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="f057e-120">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f057e-120">For more information, see:</span></span>

* [<span data-ttu-id="f057e-121">在 HDInsight 中使用 Hive</span><span class="sxs-lookup"><span data-stu-id="f057e-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f057e-122">在 HDInsight 中使用 Pig</span><span class="sxs-lookup"><span data-stu-id="f057e-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="f057e-123">**必要條件**：</span><span class="sxs-lookup"><span data-stu-id="f057e-123">**Prerequisites**:</span></span>

* <span data-ttu-id="f057e-124">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f057e-124">**An Azure subscription**.</span></span> <span data-ttu-id="f057e-125">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="f057e-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f057e-126">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="f057e-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="f057e-127">如需可建立此類叢集之各種方式的指示，請參閱 [在 HDInsight 中使用 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f057e-127">For instructions on the various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="f057e-128">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="f057e-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f057e-129">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，將會在 2017 年 1 月 1 日前移除。</span><span class="sxs-lookup"><span data-stu-id="f057e-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="f057e-130">本文件中的步驟會使用可與 Azure Resource Manager 搭配使用的新 HDInsight Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f057e-130">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="f057e-131">請遵循[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) 中的步驟來安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f057e-131">Follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="f057e-132">如果您需要修改指令碼才能使用適用於 Azure Resource Manager 的新 Cmdlet，請參閱[移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)](hdinsight-hadoop-development-using-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="f057e-132">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="f057e-133"><a name="hdinsight-sample-wordcount"></a>字數統計 - Java</span><span class="sxs-lookup"><span data-stu-id="f057e-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="f057e-134">如果要提交 MapReduce 專案，您可以先建立 MapReduce 工作定義。</span><span class="sxs-lookup"><span data-stu-id="f057e-134">To submit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="f057e-135">在工作定義中，您指定 MapReduce 程式 jar 檔案和該 jar 檔案的位置，這會是 **wasb:///example/jars/hadoop-mapreduce-examples.jar**、類別名稱和引數。</span><span class="sxs-lookup"><span data-stu-id="f057e-135">In the job definition, you specify the MapReduce program jar file and the location of the jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, the class name, and the arguments.</span></span>  <span data-ttu-id="f057e-136">字數統計 MapReduce 程式會採用兩個引數：用來統計字數的原始程式檔與輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="f057e-136">The wordcount MapReduce program takes two arguments: the source file that is used to count words, and the location for output.</span></span>

<span data-ttu-id="f057e-137">原始程式碼可以在 [附錄 A](#apendix-a---the-word-count-MapReduce-program-in-java)中找到。</span><span class="sxs-lookup"><span data-stu-id="f057e-137">The source code can be found in the [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="f057e-138">如需開發 Java MapReduce 程式之程序，請參閱 - [在 HDInsight 中針對 Hadoop 開發 Java MapReduce 程式](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="f057e-138">For the procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="f057e-139">**提交字數統計 MapReduce 工作**</span><span class="sxs-lookup"><span data-stu-id="f057e-139">**To submit a word count MapReduce job**</span></span>

1. <span data-ttu-id="f057e-140">開啟 **Windows PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="f057e-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="f057e-141">如需指示，請參閱[安裝和設定 Azure PowerShell][powershell-install-configure]。</span><span class="sxs-lookup"><span data-stu-id="f057e-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="f057e-142">貼上下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="f057e-142">Paste the following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define the MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit the job and wait for job completion
    $cred = Get-Credential -Message "Enter the HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get the job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download the job output to the workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display the output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="f057e-143">MapReduce 工作會產生一個名為 *part-r-00000*的檔案，內有文字和字數。</span><span class="sxs-lookup"><span data-stu-id="f057e-143">The MapReduce job produces a file named *part-r-00000*, which contains words and the counts.</span></span> <span data-ttu-id="f057e-144">指令碼使用 **findstr** 命令列出包含 "there" 的所有文字。</span><span class="sxs-lookup"><span data-stu-id="f057e-144">The script uses the **findstr** command to list all the words that contains *"there"*.</span></span>
3. <span data-ttu-id="f057e-145">設定前三個變數，然後執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="f057e-145">Set the first three variables, and run the script.</span></span>

## <span data-ttu-id="f057e-146"><a name="hdinsight-sample-csharp-streaming"></a>字數統計 - C# 串流</span><span class="sxs-lookup"><span data-stu-id="f057e-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="f057e-147">Hadoop 提供 MapReduce 一個串流 API，可讓您以 Java 以外的語言撰寫 map 和 reduce 函數。</span><span class="sxs-lookup"><span data-stu-id="f057e-147">Hadoop provides a streaming API to MapReduce, which enables you to write map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="f057e-148">本教學課程的步驟只適用於 Windows HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f057e-148">The steps in this tutorial apply only to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="f057e-149">如需 Linux HDInsight 叢集的串流範例，請參閱 [開發適用於 HDInsight 的 Python 串流程式](hdinsight-hadoop-streaming-python.md)。</span><span class="sxs-lookup"><span data-stu-id="f057e-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="f057e-150">在範例中，mapper 和 reducer 是從 [stdin][stdin-stdout-stderr] 讀取輸入 (循行) 並將輸出發出到 [stdout][stdin-stdout-stderr] 的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="f057e-150">In the example, the mapper and the reducer are executables that read the input from [stdin][stdin-stdout-stderr] (line-by-line) and emit the output to [stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="f057e-151">程式會計算內容中的所有文字。</span><span class="sxs-lookup"><span data-stu-id="f057e-151">The program counts all the words in the text.</span></span>

<span data-ttu-id="f057e-152">在已為 **mappers**指定可執行檔的情況下，當 mapper 初始化時，每個 mapper 工作都會將可執行檔啟動成為個別的處理程序。</span><span class="sxs-lookup"><span data-stu-id="f057e-152">When an executable is specified for **mappers**, each mapper task launches the executable as a separate process when the mapper is initialized.</span></span> <span data-ttu-id="f057e-153">當 mapper 工作執行時，它會將輸入傳換成行，並將這些行饋送至處理程序的 [stdin][stdin-stdout-stderr]。</span><span class="sxs-lookup"><span data-stu-id="f057e-153">As the mapper task runs, it converts its input into lines, and feeds the lines to the [stdin][stdin-stdout-stderr] of the process.</span></span>

<span data-ttu-id="f057e-154">同時，mapper 會收集來自處理程序 stdout 的行導向輸出。</span><span class="sxs-lookup"><span data-stu-id="f057e-154">In the meantime, the mapper collects the line-oriented output from the stdout of the process.</span></span> <span data-ttu-id="f057e-155">它會將每一行轉換成索引鍵/值組，其會做為 mapper 的輸出來收集。</span><span class="sxs-lookup"><span data-stu-id="f057e-155">It converts each line into a key/value pair, which is collected as the output of the mapper.</span></span> <span data-ttu-id="f057e-156">根據預設，從一行的前置詞一直到第一個定位字元即是索引鍵，行的其餘部分 (不包含定位字元) 則為值。</span><span class="sxs-lookup"><span data-stu-id="f057e-156">By default, the prefix of a line up to the first Tab character is the key, and the remainder of the line (excluding the Tab character) is the value.</span></span> <span data-ttu-id="f057e-157">如果行中沒有定位字元，則整行都會被視為索引鍵，而值則為 null。</span><span class="sxs-lookup"><span data-stu-id="f057e-157">If there is no Tab character in the line, entire line is considered as the key, and the value is null.</span></span>

<span data-ttu-id="f057e-158">在已為 **reducers**指定可執行檔的情況下，當 reducer 初始化時，每個 reducer 工作都會將可執行檔啟動成為個別的處理程序。</span><span class="sxs-lookup"><span data-stu-id="f057e-158">When an executable is specified for **reducers**, each reducer task launches the executable as a separate process when the reducer is initialized.</span></span> <span data-ttu-id="f057e-159">當 reducer 工作執行時，它會將輸入索引鍵/值組傳換成行，並將這些行饋送至處理程序的 [stdin][stdin-stdout-stderr]。</span><span class="sxs-lookup"><span data-stu-id="f057e-159">As the reducer task runs, it converts its input key/values pairs into lines, and it feeds the lines to the [stdin][stdin-stdout-stderr] of the process.</span></span>

<span data-ttu-id="f057e-160">同時，reducer 會收集來自處理程序 [stdout][stdin-stdout-stderr] 的行導向輸出。</span><span class="sxs-lookup"><span data-stu-id="f057e-160">In the meantime, the reducer collects the line-oriented output from the [stdout][stdin-stdout-stderr] of the process.</span></span> <span data-ttu-id="f057e-161">它會將每一行轉換成索引鍵/值組，其會做為 reducer 的輸出來收集。</span><span class="sxs-lookup"><span data-stu-id="f057e-161">It converts each line to a key/value pair, which is collected as the output of the reducer.</span></span> <span data-ttu-id="f057e-162">根據預設，從一行的前置詞一直到第一個定位字元即是索引鍵，行的其餘部分 (不包含定位字元) 則為值。</span><span class="sxs-lookup"><span data-stu-id="f057e-162">By default, the prefix of a line up to the first Tab character is the key, and the remainder of the line (excluding the Tab character) is the value.</span></span>

<span data-ttu-id="f057e-163">**提交 C# 串流字數統計工作**</span><span class="sxs-lookup"><span data-stu-id="f057e-163">**To submit a C# streaming word count job**</span></span>

* <span data-ttu-id="f057e-164">遵循[字數統計 - Java](#word-count-java) 中的程序，並使用下行內容取代作業定義：</span><span class="sxs-lookup"><span data-stu-id="f057e-164">Follow the procedure in [Word count - Java](#word-count-java), and replace the job definition with the following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="f057e-165">輸出檔案應該為：</span><span class="sxs-lookup"><span data-stu-id="f057e-165">The output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="f057e-166"><a name="hdinsight-sample-pi-estimator"></a>PI 估算器</span><span class="sxs-lookup"><span data-stu-id="f057e-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="f057e-167">Pi 估算器會使用統計 (擬蒙特卡羅法) 方法來估計 pi 的值。</span><span class="sxs-lookup"><span data-stu-id="f057e-167">The pi estimator uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="f057e-168">單位正方形內隨機散佈的點，也會落在該正方形的內切圓之內，且機率等於圓面積 Pi/4。</span><span class="sxs-lookup"><span data-stu-id="f057e-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="f057e-169">Pi 的值可從 4R 的值來估計，其中 R 是圓內點數佔正方形內總點數的比例。</span><span class="sxs-lookup"><span data-stu-id="f057e-169">The value of pi can be estimated from the value of 4R, where R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="f057e-170">使用的樣本點越多，估計越準確。</span><span class="sxs-lookup"><span data-stu-id="f057e-170">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="f057e-171">此範例的提供指令碼會提交 Hadoop jar 工作，且設定為以 16 個對應的值來執行，每個對應都必須依參數值來計算 1 千萬個樣本點。</span><span class="sxs-lookup"><span data-stu-id="f057e-171">The script provided for this sample submits a Hadoop jar job and is set up to run with a value 16 maps, each of which is required to compute 10 million sample points by the parameter values.</span></span> <span data-ttu-id="f057e-172">這些參數可變更來改善 Pi 的估計值。</span><span class="sxs-lookup"><span data-stu-id="f057e-172">These parameter values can be changed to improve the estimated value of pi.</span></span> <span data-ttu-id="f057e-173">Pi 的前 10 位小數是 3.1415926535，供您參考。</span><span class="sxs-lookup"><span data-stu-id="f057e-173">For reference, the first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="f057e-174">**提交 Pi 估算器工作**</span><span class="sxs-lookup"><span data-stu-id="f057e-174">**To submit a pi estimator job**</span></span>

* <span data-ttu-id="f057e-175">遵循[字數統計 - Java](#word-count-java) 中的程序，並使用下行內容取代作業定義：</span><span class="sxs-lookup"><span data-stu-id="f057e-175">Follow the procedure in [Word count - Java](#word-count-java), and replace the job definition with the following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="f057e-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span><span class="sxs-lookup"><span data-stu-id="f057e-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="f057e-177">本範例使用不太大的 10GB 資料，所以執行起來相對較快。</span><span class="sxs-lookup"><span data-stu-id="f057e-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="f057e-178">本範例使用 Owen O'Malley 和 Arun Murthy 所開發的 MapReduce 應用程式，此應用程式於 2009 年的年度一般目的 (「耐力賽」) TB 排序效能評定中，以 0.578TB/分鐘 (173 分鐘內達到 100TB) 的速率獲勝。</span><span class="sxs-lookup"><span data-stu-id="f057e-178">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy that won the annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="f057e-179">如需此效能評比和其他排序效能評比的詳細資訊，請參閱 [Sortbenchmark](http://sortbenchmark.org/) 網站。</span><span class="sxs-lookup"><span data-stu-id="f057e-179">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="f057e-180">本範例使用三組 MapReduce 程式：</span><span class="sxs-lookup"><span data-stu-id="f057e-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="f057e-181">**TeraGen** 是可用來產生排序資料列的 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="f057e-181">**TeraGen** is a MapReduce program that you can use to generate the rows of data to sort.</span></span>
2. <span data-ttu-id="f057e-182">**TeraSort** 可取樣輸入資料並利用 MapReduce 將資料依全序排列。</span><span class="sxs-lookup"><span data-stu-id="f057e-182">**TeraSort** samples the input data and uses MapReduce to sort the data into a total order.</span></span> <span data-ttu-id="f057e-183">TeraSort 是 MapReduce 函數的標準排序，但自訂分割器除外，它使用 N-1 個樣本索引鍵的排序清單來定義每次歸納的索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="f057e-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="f057e-184">尤其是，會傳送使得 sample[i-1] <= key < sample[i] 的所有索引鍵給歸納 i。</span><span class="sxs-lookup"><span data-stu-id="f057e-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="f057e-185">這保證歸納 i 的輸出全都小於歸納 i+1 的輸出。</span><span class="sxs-lookup"><span data-stu-id="f057e-185">This guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>
3. <span data-ttu-id="f057e-186">**TeraValidate** 是一個驗證全域排序輸出的 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="f057e-186">**TeraValidate** is a MapReduce program that validates that the output is globally sorted.</span></span> <span data-ttu-id="f057e-187">它會在輸出目錄中為每一個檔案建立一個對應，而每個對應可確保每一個索引鍵一定小於或等於前一個對應。</span><span class="sxs-lookup"><span data-stu-id="f057e-187">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="f057e-188">對應函數也會產生每個檔案的第一個和最後一個索引鍵的記錄，而歸納函數可確保檔案 i 的第一個索引鍵大於檔案 i-1 的最後一個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f057e-188">The map function also generates records of the first and last keys of each file, and the reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="f057e-189">任何問題皆會回報為具錯誤索引鍵的歸納輸出。</span><span class="sxs-lookup"><span data-stu-id="f057e-189">Any problems are reported as an output of the reduce with the keys that are out of order.</span></span>

<span data-ttu-id="f057e-190">這三個應用程式所使用的輸入和輸出格式會以正確格式讀取和寫入文字檔。</span><span class="sxs-lookup"><span data-stu-id="f057e-190">The input and output format, used by all three applications, reads and writes the text files in the right format.</span></span> <span data-ttu-id="f057e-191">歸納的輸出將複寫設為 1，而不是預設值 3，因為效能評定競賽不需要將輸出資料複寫至多個節點。</span><span class="sxs-lookup"><span data-stu-id="f057e-191">The output of the reduce has replication set to 1, instead of the default 3, because the benchmark contest does not require that the output data be replicated on to multiple nodes.</span></span>

<span data-ttu-id="f057e-192">範例需要三項工作，各對應至簡介中描述的其中一個 MapReduce 程式：</span><span class="sxs-lookup"><span data-stu-id="f057e-192">Three tasks are required by the sample, each corresponding to one of the MapReduce programs described in the introduction:</span></span>

1. <span data-ttu-id="f057e-193">執行 **TeraGen** MapReduce 工作來產生要排序的資料。</span><span class="sxs-lookup"><span data-stu-id="f057e-193">Generate the data for sorting by running the **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="f057e-194">執行 **TeraSort** MapReduce 工作來排序資料。</span><span class="sxs-lookup"><span data-stu-id="f057e-194">Sort the data by running the **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="f057e-195">執行 **TeraValidate** MapReduce 工作來確認資料排序正確。</span><span class="sxs-lookup"><span data-stu-id="f057e-195">Confirm that the data has been correctly sorted by running the **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="f057e-196">**提交工作**</span><span class="sxs-lookup"><span data-stu-id="f057e-196">**To submit the jobs**</span></span>

* <span data-ttu-id="f057e-197">遵循[字數統計 - Java](#word-count-java) 中的程序，並使用下列工作定義：</span><span class="sxs-lookup"><span data-stu-id="f057e-197">Follow the procedure in [Word count - Java](#word-count-java), and use the following job definitions:</span></span>

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a><span data-ttu-id="f057e-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f057e-198">Next steps</span></span>
<span data-ttu-id="f057e-199">透過本文和關於各範例的文章，您已了解如何使用 Azure PowerShell 執行 HDInsight 叢集隨附的範例。</span><span class="sxs-lookup"><span data-stu-id="f057e-199">From this article and the articles in each of the samples, you learned how to run the samples included with the HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="f057e-200">如需透過 HDInsight 使用 Pig、Hive 和 MapReduce 的教學課程，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="f057e-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="f057e-201">[開始在 HDInsight 中搭配 Hive 使用 Hadoop 以分析行動電話使用][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f057e-201">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="f057e-202">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f057e-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f057e-203">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f057e-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f057e-204">[在 HDInsight 中提交 Hadoop 作業][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="f057e-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="f057e-205">[Azure HDInsight SDK 文件][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="f057e-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---the-word-count-source-code"></a><span data-ttu-id="f057e-206">附錄 A - 字數統計原始程式碼</span><span class="sxs-lookup"><span data-stu-id="f057e-206">Appendix A - The Word count source code</span></span>

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---the-word-count-streaming-source-code"></a><span data-ttu-id="f057e-207">附錄 B - 字數統計串流原始程式碼</span><span class="sxs-lookup"><span data-stu-id="f057e-207">Appendix B - The word count streaming source code</span></span>
<span data-ttu-id="f057e-208">MapReduce 程式使用 cat.exe 應用程式做為對應介面以將文字串流至主控台，並使用 wc.exe 應用程式做為縮減介面以計算從文件串流的字數。</span><span class="sxs-lookup"><span data-stu-id="f057e-208">The MapReduce program uses the cat.exe application as a mapping interface to stream the text into the console and the wc.exe application as the reduce interface to count the number of words that are streamed from a document.</span></span> <span data-ttu-id="f057e-209">mapper 和 reducer 都會從標準輸入資料流 (stdin) 逐行讀取字元並寫入至標準輸出資料流 (stdout)。</span><span class="sxs-lookup"><span data-stu-id="f057e-209">Both the mapper and reducer read characters, line-by-line, from the standard input stream (stdin) and write to the standard output stream (stdout).</span></span>

```csharp
// The source code for the cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

<span data-ttu-id="f057e-210">cat.cs 檔案中的 mapper 程式碼會使用 [StreamReader][streamreader] 物件，將連入串流的字元讀取至主控台，再由主控台以靜態 [Console.Writeline][console-writeline] 方法將串流寫入標準輸出串流。</span><span class="sxs-lookup"><span data-stu-id="f057e-210">The mapper code in the cat.cs file uses a [StreamReader][streamreader] object to read the characters of the incoming stream to the console, which then writes the stream to the standard output stream with the static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// The source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

<span data-ttu-id="f057e-211">wc.cs 檔案中的 reducer 程式碼會使用 [StreamReader][streamreader] 物件，從已經由 cat.exe mapper 輸出的標準輸入串流讀取字元。</span><span class="sxs-lookup"><span data-stu-id="f057e-211">The reducer code in the wc.cs file uses a [StreamReader][streamreader]   object to read characters from the standard input stream that have been output by the cat.exe mapper.</span></span> <span data-ttu-id="f057e-212">當它使用 [Console.Writeline][console-writeline] 方法讀取字元時，它會藉由計算空格和每個字尾端的行尾字元來計算字數。</span><span class="sxs-lookup"><span data-stu-id="f057e-212">As it reads the characters with the [Console.Writeline][console-writeline] method, it counts the words by counting spaces and end-of-line characters at the end of each word.</span></span> <span data-ttu-id="f057e-213">然後使用 [Console.Writeline][console-writeline] 方法將總計寫入標準輸出串流。</span><span class="sxs-lookup"><span data-stu-id="f057e-213">It then writes the total to the standard output stream with the [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---the-pi-estimator-source-code"></a><span data-ttu-id="f057e-214">附錄 C - Pi 估算器原始程式碼</span><span class="sxs-lookup"><span data-stu-id="f057e-214">Appendix C - The Pi estimator source code</span></span>
<span data-ttu-id="f057e-215">以下提供包含 mapper 和 reducer 函數的 Pi 估算器 Java 程式碼以進行檢查。</span><span class="sxs-lookup"><span data-stu-id="f057e-215">The pi estimator Java code that contains the mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="f057e-216">對應器程式會產生單位正方形內隨機散佈的一定點數，然後計算落在圓內的點數。</span><span class="sxs-lookup"><span data-stu-id="f057e-216">The mapper program generates a specified number of points placed at random inside of a unit square and then counts the number of those points that are inside the circle.</span></span> <span data-ttu-id="f057e-217">Reducer 程式會累計 mapper 所計算的點數，然後從公式 4R 估計 Pi 的值，其中 R 是圓內計算的點數佔正方形內總點數的比例。</span><span class="sxs-lookup"><span data-stu-id="f057e-217">The reducer program accumulates points counted by the mappers and then estimates the value of pi from the formula 4R, where R is the ratio of the number of points counted inside the circle to the total number of points that are within the square.</span></span>

```java
/**
* Licensed to the Apache Software Foundation (ASF) under one
* or more contributor license agreements. See the NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. The ASF licenses this file
* to you under the Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with the License. You may obtain a copy of the License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed to in writing, software
* distributed under the License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See the License for the specific language governing permissions and
* limitations under the License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program to estimate the value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of the inscribed circle of the square.
//
//Reducer:
//Accumulate points inside/outside results from the mappers.
//Let numTotal = numInside + numOutside.
//The fraction numInside/numTotal is a rational approximation of
//the value (Area of the circle)/(Area of the square),
//where the area of the inscribed circle is Pi/4
//and the area of unit square is 1.
//Then, Pi is estimated value to be 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is the index.
//Halton sequence is used to generate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize to H(startindex),
//so the sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume the current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of the inscribed circle of the square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from the (offset+1)th sample.
//@param size the number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of the inscribed circle of the square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from the mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing the file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from the mappers.
// @param isInside Is the points inside?
// @param values An iterator to a list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output to a file.
@Override
public void close() throws IOException {
//write output to a file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return the estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers to the same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---the-10gb-graysort-source-code"></a><span data-ttu-id="f057e-218">附錄 D - 10gb Graysort 原始程式碼</span><span class="sxs-lookup"><span data-stu-id="f057e-218">Appendix D - The 10gb graysort source code</span></span>
<span data-ttu-id="f057e-219">本節顯示 TeraSort MapReduce 程式的程式碼以進行檢查。</span><span class="sxs-lookup"><span data-stu-id="f057e-219">The code for the TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed to the Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See the NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  The ASF licenses this file
    * to you under the Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with the License.  You may obtain a copy of the License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed to in writing, software
    * distributed under the License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See the License for the specific language governing permissions and
    * limitations under the License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates the sampled split points, launches the job,
    * and waits for it to finish.
    * <p>
    * To run the program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on the next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares to figure out where the given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read the cut points from the given sequence file.
        * @param fs the file system
        * @param p the path to read
        * @param job the job config
        * @return the strings to split the partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find the correct
        * partition quickly.
        * @param splits the list of cut points
        * @param lower the lower bound of partitions 0..numPartitions-1
        * @param upper the upper bound of partitions 0..numPartitions-1
        * @param prefix the prefix that we have already checked against
        * @param maxDepth the maximum depth we will build a trie for
        * @return the trie node that will divide the splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on to the prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up the rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
