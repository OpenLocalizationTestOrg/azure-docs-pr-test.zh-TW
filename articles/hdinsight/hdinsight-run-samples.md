---
title: "HDInsight 的 Azure 中的範例 aaaRun hello Hadoop |Microsoft 文件"
description: "開始使用提供的 hello 範例與 hello Azure HDInsight 服務。 使用 PowerShell 指令碼在資料叢集上執行 MapReduce 程式。"
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
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="0054e-104">在以 Windows 為基礎的 HDInsight 中執行 Hadoop MapReduce 範例</span><span class="sxs-lookup"><span data-stu-id="0054e-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="0054e-105">Toohelp 開始使用 Azure HDInsight Hadoop 叢集上執行 MapReduce 工作時，會提供一組的樣本。</span><span class="sxs-lookup"><span data-stu-id="0054e-105">A set of samples are provided toohelp you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="0054e-106">這些範例都可以在每個 hello HDInsight 上您所建立的受管理的叢集。</span><span class="sxs-lookup"><span data-stu-id="0054e-106">These samples are made available on each of hello HDInsight managed clusters that you create.</span></span> <span data-ttu-id="0054e-107">執行這些範例熟悉使用 Azure PowerShell cmdlet toorun 工作在 Hadoop 叢集上。</span><span class="sxs-lookup"><span data-stu-id="0054e-107">Running these samples familiarize you with using Azure PowerShell cmdlets toorun jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="0054e-108">[字數統計][hdinsight-sample-wordcount]：計算文字檔中的文字出現次數。</span><span class="sxs-lookup"><span data-stu-id="0054e-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="0054e-109">[**C# 串流字數統計**][hdinsight-sample-csharp-streaming]： 計數 word 出現在文字檔案，使用 hello Hadoop 串流介面。</span><span class="sxs-lookup"><span data-stu-id="0054e-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using hello Hadoop streaming interface.</span></span>
* <span data-ttu-id="0054e-110">[**Pi 估計工具**][hdinsight-sample-pi-estimator]： 使用統計 (odd Monte Carlo) 方法 tooestimate hello pi 的值。</span><span class="sxs-lookup"><span data-stu-id="0054e-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span>
* <span data-ttu-id="0054e-111">[10-GB Graysort][hdinsight-sample-10gb-graysort]：使用 HDInsight 在 10 GB 檔案上執行一般用途的 GraySort。</span><span class="sxs-lookup"><span data-stu-id="0054e-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="0054e-112">有三個作業 toorun: Teragen toogenerate hello 資料、 Terasort toosort hello 資料，以及 Teravalidate tooconfirm hello 資料的正確排序。</span><span class="sxs-lookup"><span data-stu-id="0054e-112">There are three jobs toorun: Teragen toogenerate hello data, Terasort toosort hello data, and Teravalidate tooconfirm that hello data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="0054e-113">hello 原始程式碼位於 hello 附錄。</span><span class="sxs-lookup"><span data-stu-id="0054e-113">hello source code can be found in hello Appendix.</span></span>

<span data-ttu-id="0054e-114">很多其他文件存在於 hello web Hadoop 相關的技術，例如 Java 為基礎的 MapReduce 程式設計和串流處理，以及使用 Windows PowerShell 中的 hello cmdlet 的相關文件的指令碼。</span><span class="sxs-lookup"><span data-stu-id="0054e-114">Much additional documentation exists on hello web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about hello cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="0054e-115">如需有關這些資源的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0054e-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="0054e-116">在 HDInsight 上開發 Hadoop 的 Java MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="0054e-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="0054e-117">在 HDInsight 上提交 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="0054e-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="0054e-118">[簡介 tooAzure HDInsight][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="0054e-118">[Introduction tooAzure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="0054e-119">時至今日，很多人選擇 Hive 和 Pig 而非 MapReduce。</span><span class="sxs-lookup"><span data-stu-id="0054e-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="0054e-120">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="0054e-120">For more information, see:</span></span>

* [<span data-ttu-id="0054e-121">在 HDInsight 中使用 Hive</span><span class="sxs-lookup"><span data-stu-id="0054e-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0054e-122">在 HDInsight 中使用 Pig</span><span class="sxs-lookup"><span data-stu-id="0054e-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="0054e-123">**必要條件**：</span><span class="sxs-lookup"><span data-stu-id="0054e-123">**Prerequisites**:</span></span>

* <span data-ttu-id="0054e-124">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="0054e-124">**An Azure subscription**.</span></span> <span data-ttu-id="0054e-125">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="0054e-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0054e-126">**HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="0054e-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="0054e-127">如需 hello 各種方式，可以在其中建立此類叢集的指示，請參閱[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="0054e-127">For instructions on hello various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="0054e-128">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="0054e-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0054e-129">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，將會在 2017 年 1 月 1 日前移除。</span><span class="sxs-lookup"><span data-stu-id="0054e-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="0054e-130">此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="0054e-130">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="0054e-131">中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0054e-131">Follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="0054e-132">如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="0054e-132">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="0054e-133"><a name="hdinsight-sample-wordcount"></a>字數統計 - Java</span><span class="sxs-lookup"><span data-stu-id="0054e-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="0054e-134">toosubmit MapReduce 專案，您先建立 MapReduce 工作定義。</span><span class="sxs-lookup"><span data-stu-id="0054e-134">toosubmit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="0054e-135">Hello 工作定義，在您指定 hello MapReduce 程式 jar 檔案和 hello hello jar 檔案位置，也就是**wasb:///example/jars/hadoop-mapreduce-examples.jar**、 hello 類別名稱和 hello 引數。</span><span class="sxs-lookup"><span data-stu-id="0054e-135">In hello job definition, you specify hello MapReduce program jar file and hello location of hello jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, hello class name, and hello arguments.</span></span>  <span data-ttu-id="0054e-136">hello wordcount MapReduce 程式會採用兩個引數： hello 原始程式檔是使用的 toocount 字和 hello 輸出的位置。</span><span class="sxs-lookup"><span data-stu-id="0054e-136">hello wordcount MapReduce program takes two arguments: hello source file that is used toocount words, and hello location for output.</span></span>

<span data-ttu-id="0054e-137">hello 原始程式碼位於 hello[附錄 A](#apendix-a---the-word-count-MapReduce-program-in-java)。</span><span class="sxs-lookup"><span data-stu-id="0054e-137">hello source code can be found in hello [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="0054e-138">Hello 程序的開發 Java MapReduce 程式，請參閱- [HDInsight 中的 Hadoop 的開發 Java MapReduce 程式](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="0054e-138">For hello procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="0054e-139">**toosubmit word 計數 MapReduce 工作**</span><span class="sxs-lookup"><span data-stu-id="0054e-139">**toosubmit a word count MapReduce job**</span></span>

1. <span data-ttu-id="0054e-140">開啟 **Windows PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="0054e-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="0054e-141">如需指示，請參閱[安裝和設定 Azure PowerShell][powershell-install-configure]。</span><span class="sxs-lookup"><span data-stu-id="0054e-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="0054e-142">貼上下列 PowerShell 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="0054e-142">Paste hello following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
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

    # Get hello job output
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

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="0054e-143">hello MapReduce 工作會產生名為*一部分-r-00000*，其中包含文字和 hello 計數。</span><span class="sxs-lookup"><span data-stu-id="0054e-143">hello MapReduce job produces a file named *part-r-00000*, which contains words and hello counts.</span></span> <span data-ttu-id="0054e-144">hello 指令碼會使用 hello **findstr** toolist 所有 hello 文字的命令包含*"there"*。</span><span class="sxs-lookup"><span data-stu-id="0054e-144">hello script uses hello **findstr** command toolist all hello words that contains *"there"*.</span></span>
3. <span data-ttu-id="0054e-145">設定 hello 前三個變數，並執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0054e-145">Set hello first three variables, and run hello script.</span></span>

## <span data-ttu-id="0054e-146"><a name="hdinsight-sample-csharp-streaming"></a>字數統計 - C# 串流</span><span class="sxs-lookup"><span data-stu-id="0054e-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="0054e-147">Hadoop 提供串流處理的應用程式開發介面 tooMapReduce，可讓您 toowrite 對應和減少 Java 以外的語言中的函式。</span><span class="sxs-lookup"><span data-stu-id="0054e-147">Hadoop provides a streaming API tooMapReduce, which enables you toowrite map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="0054e-148">在此教學課程中的 hello 步驟適用於僅 tooWindows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="0054e-148">hello steps in this tutorial apply only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="0054e-149">如需 Linux HDInsight 叢集的串流範例，請參閱 [開發適用於 HDInsight 的 Python 串流程式](hdinsight-hadoop-streaming-python.md)。</span><span class="sxs-lookup"><span data-stu-id="0054e-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="0054e-150">在 hello 範例、 hello 對應工具和減壓器 hello 是讀取從 hello 輸入的可執行檔[stdin] [ stdin-stdout-stderr] （線條的線條），並發出 hello 輸出太[stdout] [stdin-stdout-stderr].</span><span class="sxs-lookup"><span data-stu-id="0054e-150">In hello example, hello mapper and hello reducer are executables that read hello input from [stdin][stdin-stdout-stderr] (line-by-line) and emit hello output too[stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="0054e-151">hello 程式計算所有 hello 文字中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="0054e-151">hello program counts all hello words in hello text.</span></span>

<span data-ttu-id="0054e-152">當可執行檔您針對指定**自行**，每個對應工具 」 工作會啟動可執行檔當做個別處理序的 hello hello 對應工具初始化時。</span><span class="sxs-lookup"><span data-stu-id="0054e-152">When an executable is specified for **mappers**, each mapper task launches hello executable as a separate process when hello mapper is initialized.</span></span> <span data-ttu-id="0054e-153">當 hello 對應工具 」 工作執行時，會將其輸入轉換成線條，而摘要 hello 行 toohello [stdin] [ stdin-stdout-stderr] hello 程序。</span><span class="sxs-lookup"><span data-stu-id="0054e-153">As hello mapper task runs, it converts its input into lines, and feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="0054e-154">在 hello 同時，hello 對應工具會收集 hello 行導向的輸出從 hello stdout hello 程序。</span><span class="sxs-lookup"><span data-stu-id="0054e-154">In hello meantime, hello mapper collects hello line-oriented output from hello stdout of hello process.</span></span> <span data-ttu-id="0054e-155">將每一行轉換為索引鍵/值組，可用來收集做為 「 hello 對應工具 」 的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="0054e-155">It converts each line into a key/value pair, which is collected as hello output of hello mapper.</span></span> <span data-ttu-id="0054e-156">根據預設，對齊第一個定位字元 toohello hello 前置詞是 hello 機碼，而 hello 的 hello 行 （不含 hello Tab 字元） 的其餘部分則 hello。</span><span class="sxs-lookup"><span data-stu-id="0054e-156">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span> <span data-ttu-id="0054e-157">如果 hello 列沒有任何 Tab 字元，整行視為 hello 金鑰和 hello 值為 null。</span><span class="sxs-lookup"><span data-stu-id="0054e-157">If there is no Tab character in hello line, entire line is considered as hello key, and hello value is null.</span></span>

<span data-ttu-id="0054e-158">當可執行檔您針對指定**reducers**，每個減壓器工作會啟動可執行檔當做個別處理序的 hello hello 減壓器初始化時。</span><span class="sxs-lookup"><span data-stu-id="0054e-158">When an executable is specified for **reducers**, each reducer task launches hello executable as a separate process when hello reducer is initialized.</span></span> <span data-ttu-id="0054e-159">當 hello 減壓器工作執行時，會將其輸入的索引鍵/值組轉換成線條，而摘要 hello 行 toohello [stdin] [ stdin-stdout-stderr] hello 程序。</span><span class="sxs-lookup"><span data-stu-id="0054e-159">As hello reducer task runs, it converts its input key/values pairs into lines, and it feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="0054e-160">在 hello 同時，hello 減壓器 hello 列導向輸出會從收集 hello [stdout] [ stdin-stdout-stderr] hello 程序。</span><span class="sxs-lookup"><span data-stu-id="0054e-160">In hello meantime, hello reducer collects hello line-oriented output from hello [stdout][stdin-stdout-stderr] of hello process.</span></span> <span data-ttu-id="0054e-161">它會轉換為 hello 的 hello 減壓器的輸出會收集每個行 tooa 機碼值組。</span><span class="sxs-lookup"><span data-stu-id="0054e-161">It converts each line tooa key/value pair, which is collected as hello output of hello reducer.</span></span> <span data-ttu-id="0054e-162">根據預設，對齊第一個定位字元 toohello hello 前置詞是 hello 機碼，而 hello 的 hello 行 （不含 hello Tab 字元） 的其餘部分則 hello。</span><span class="sxs-lookup"><span data-stu-id="0054e-162">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span>

<span data-ttu-id="0054e-163">**資料流 word 計數工作 toosubmit C#**</span><span class="sxs-lookup"><span data-stu-id="0054e-163">**toosubmit a C# streaming word count job**</span></span>

* <span data-ttu-id="0054e-164">請依照下列中的 hello 程序[字數統計-Java](#word-count-java)，並取代 hello 行下 hello 工作定義：</span><span class="sxs-lookup"><span data-stu-id="0054e-164">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="0054e-165">應該 hello 輸出檔：</span><span class="sxs-lookup"><span data-stu-id="0054e-165">hello output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="0054e-166"><a name="hdinsight-sample-pi-estimator"></a>PI 估算器</span><span class="sxs-lookup"><span data-stu-id="0054e-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="0054e-167">hello pi 估計工具會使用統計 (odd Monte Carlo) 方法 tooestimate hello pi 的值。</span><span class="sxs-lookup"><span data-stu-id="0054e-167">hello pi estimator uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="0054e-168">內部單位隨機放置點方形也落在該方塊內有與 hello 圓形的可能性相等 toohello 區域的圓形 pi/4。</span><span class="sxs-lookup"><span data-stu-id="0054e-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="0054e-169">hello pi 的值可以估計 hello 4R，其中 R 是 hello 比率 hello hello 圓形 toohello 總數 hello 正方形中的點內的點的數字的值。</span><span class="sxs-lookup"><span data-stu-id="0054e-169">hello value of pi can be estimated from hello value of 4R, where R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="0054e-170">hello 較大 hello 範例使用的點數，hello 佳 hello 估計值。</span><span class="sxs-lookup"><span data-stu-id="0054e-170">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="0054e-171">此範例所提供的 hello 指令碼提交 Hadoop jar 作業，設定成 toorun 值 16 的對應，每一個都是必要的 toocompute 10 百萬範例點 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="0054e-171">hello script provided for this sample submits a Hadoop jar job and is set up toorun with a value 16 maps, each of which is required toocompute 10 million sample points by hello parameter values.</span></span> <span data-ttu-id="0054e-172">這些參數值可以變更 pi tooimprove hello 估計值。</span><span class="sxs-lookup"><span data-stu-id="0054e-172">These parameter values can be changed tooimprove hello estimated value of pi.</span></span> <span data-ttu-id="0054e-173">如需參考，hello pi 的前 10 個小數位數是 3.1415926535。</span><span class="sxs-lookup"><span data-stu-id="0054e-173">For reference, hello first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="0054e-174">**toosubmit pi 估計工具工作**</span><span class="sxs-lookup"><span data-stu-id="0054e-174">**toosubmit a pi estimator job**</span></span>

* <span data-ttu-id="0054e-175">請依照下列中的 hello 程序[字數統計-Java](#word-count-java)，並取代 hello 行下 hello 工作定義：</span><span class="sxs-lookup"><span data-stu-id="0054e-175">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="0054e-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span><span class="sxs-lookup"><span data-stu-id="0054e-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="0054e-177">本範例使用不太大的 10GB 資料，所以執行起來相對較快。</span><span class="sxs-lookup"><span data-stu-id="0054e-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="0054e-178">它會使用由 Owen O'Malley 和 Arun Murthy 贏得 hello 年度一般用途 (「 daytona 」) tb 排序基準在 2009 年率的 0.578 TB/分鐘 (以分鐘為單位 173 100 TB) 所開發的 hello MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0054e-178">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy that won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="0054e-179">如需有關這個和其他排序基準測試的詳細資訊，請參閱 hello [Sortbenchmark](http://sortbenchmark.org/)站台。</span><span class="sxs-lookup"><span data-stu-id="0054e-179">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="0054e-180">本範例使用三組 MapReduce 程式：</span><span class="sxs-lookup"><span data-stu-id="0054e-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="0054e-181">**TeraGen**是您可以使用的資料 toosort toogenerate hello 資料列的 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="0054e-181">**TeraGen** is a MapReduce program that you can use toogenerate hello rows of data toosort.</span></span>
2. <span data-ttu-id="0054e-182">**TeraSort**範例 hello 輸入的資料，並使用 MapReduce toosort hello 資料到訂單總數。</span><span class="sxs-lookup"><span data-stu-id="0054e-182">**TeraSort** samples hello input data and uses MapReduce toosort hello data into a total order.</span></span> <span data-ttu-id="0054e-183">TeraSort 是標準的 MapReduce 函式，除了使用已排序的清單定義每個減少 hello 索引鍵範圍的取樣 N-1 索引鍵的自訂 partitioner 排序。</span><span class="sxs-lookup"><span data-stu-id="0054e-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="0054e-184">特別是，所有的索引鍵這類範例 [i-1] < = 索引鍵 < 範例 [i] 傳送 tooreduce 我。</span><span class="sxs-lookup"><span data-stu-id="0054e-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="0054e-185">這保證的 hello 輸出減少 i 全部都是小於 hello 輸出減少 i + 1。</span><span class="sxs-lookup"><span data-stu-id="0054e-185">This guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>
3. <span data-ttu-id="0054e-186">**TeraValidate**是全域排序會驗證該 hello 輸出的 MapReduce 程式。</span><span class="sxs-lookup"><span data-stu-id="0054e-186">**TeraValidate** is a MapReduce program that validates that hello output is globally sorted.</span></span> <span data-ttu-id="0054e-187">它在 hello 輸出目錄中，會建立一個對應，每個檔案和每個對應可確保每個索引鍵是否小於或等於前一個 toohello。</span><span class="sxs-lookup"><span data-stu-id="0054e-187">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="0054e-188">hello 對應函式也會產生記錄的 hello 前和最後一個索引鍵的每個檔案，以及 hello reduce 函式可確保該 hello i 檔案的第一個索引鍵大於檔案 i-1 hello 最後一個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0054e-188">hello map function also generates records of hello first and last keys of each file, and hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="0054e-189">任何問題報告做為輸出的 hello 減少 hello 索引鍵次序不對的。</span><span class="sxs-lookup"><span data-stu-id="0054e-189">Any problems are reported as an output of hello reduce with hello keys that are out of order.</span></span>

<span data-ttu-id="0054e-190">hello 輸入和所有的三個應用程式所使用的輸出格式讀取並寫入 hello 正確格式的 hello 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="0054e-190">hello input and output format, used by all three applications, reads and writes hello text files in hello right format.</span></span> <span data-ttu-id="0054e-191">hello hello 輸出減少複寫設定 too1，而不是 hello 預設為 3，因為 hello 基準內容不需要 hello 輸出資料會複寫 toomultiple 節點上。</span><span class="sxs-lookup"><span data-stu-id="0054e-191">hello output of hello reduce has replication set too1, instead of hello default 3, because hello benchmark contest does not require that hello output data be replicated on toomultiple nodes.</span></span>

<span data-ttu-id="0054e-192">Hello 範例中，每個對應 tooone hello MapReduce 程式 hello 簡介 > 中所述的所需三項工作：</span><span class="sxs-lookup"><span data-stu-id="0054e-192">Three tasks are required by hello sample, each corresponding tooone of hello MapReduce programs described in hello introduction:</span></span>

1. <span data-ttu-id="0054e-193">產生排序執行 hello hello 資料**TeraGen** MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="0054e-193">Generate hello data for sorting by running hello **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="0054e-194">排序 hello 資料執行 hello **TeraSort** MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="0054e-194">Sort hello data by running hello **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="0054e-195">確認 hello 資料已經執行 hello 正確排序**TeraValidate** MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="0054e-195">Confirm that hello data has been correctly sorted by running hello **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="0054e-196">**toosubmit hello 工作**</span><span class="sxs-lookup"><span data-stu-id="0054e-196">**toosubmit hello jobs**</span></span>

* <span data-ttu-id="0054e-197">請依照下列中的 hello 程序[字數統計-Java](#word-count-java)，並使用 hello 遵循工作定義：</span><span class="sxs-lookup"><span data-stu-id="0054e-197">Follow hello procedure in [Word count - Java](#word-count-java), and use hello following job definitions:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0054e-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0054e-198">Next steps</span></span>
<span data-ttu-id="0054e-199">從這個發行項與 hello 文件中每個 hello 範例，您學到如何 toorun hello 範例隨附 hello HDInsight 叢集使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0054e-199">From this article and hello articles in each of hello samples, you learned how toorun hello samples included with hello HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="0054e-200">如需有關搭配使用 Pig、 Hive 和 MapReduce 與 HDInsight 的教學課程，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="0054e-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="0054e-201">[開始使用登錄區中的 Hadoop，HDInsight tooanalyze 行動話筒使用中][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0054e-201">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="0054e-202">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="0054e-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="0054e-203">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="0054e-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="0054e-204">[在 HDInsight 中提交 Hadoop 作業][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="0054e-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="0054e-205">[Azure HDInsight SDK 文件][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="0054e-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---hello-word-count-source-code"></a><span data-ttu-id="0054e-206">附錄 A-hello Word 計數原始程式碼</span><span class="sxs-lookup"><span data-stu-id="0054e-206">Appendix A - hello Word count source code</span></span>

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a><span data-ttu-id="0054e-207">附錄 B-hello 字數統計資料流來源的程式碼</span><span class="sxs-lookup"><span data-stu-id="0054e-207">Appendix B - hello word count streaming source code</span></span>
<span data-ttu-id="0054e-208">hello MapReduce 程式會使用 hello cat.exe 應用程式做為對應介面 toostream hello 文字到 hello 主控台和 hello wc.exe 應用程式，當做 hello 減少介面 toocount hello 從文件資料流傳送的字組數目。</span><span class="sxs-lookup"><span data-stu-id="0054e-208">hello MapReduce program uses hello cat.exe application as a mapping interface toostream hello text into hello console and hello wc.exe application as hello reduce interface toocount hello number of words that are streamed from a document.</span></span> <span data-ttu-id="0054e-209">Hello 對應工具和減壓器字元，由列列 hello 標準輸入資料流 (stdin) 從讀寫 toohello 標準輸出資料流 (stdout)。</span><span class="sxs-lookup"><span data-stu-id="0054e-209">Both hello mapper and reducer read characters, line-by-line, from hello standard input stream (stdin) and write toohello standard output stream (stdout).</span></span>

```csharp
// hello source code for hello cat.exe (Mapper).

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

<span data-ttu-id="0054e-210">hello hello cat.cs 檔案使用中的對應工具程式碼[StreamReader] [ streamreader] tooread hello 字元的 hello 內送資料流 toohello 主控台中，哪些然後寫入 hello 資料流 toohello 標準輸出資料流的物件以靜態 hello [Console.Writeline] [ console-writeline]方法。</span><span class="sxs-lookup"><span data-stu-id="0054e-210">hello mapper code in hello cat.cs file uses a [StreamReader][streamreader] object tooread hello characters of hello incoming stream toohello console, which then writes hello stream toohello standard output stream with hello static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// hello source code for wc.exe (Reducer) is:

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

<span data-ttu-id="0054e-211">hello 減壓器 hello wc.cs 檔案使用中的程式碼[StreamReader] [ streamreader] hello 標準輸入資料流已由 hello cat.exe 對應工具的輸出物件 tooread 字元。</span><span class="sxs-lookup"><span data-stu-id="0054e-211">hello reducer code in hello wc.cs file uses a [StreamReader][streamreader]   object tooread characters from hello standard input stream that have been output by hello cat.exe mapper.</span></span> <span data-ttu-id="0054e-212">在讀取 hello 字元以 hello [Console.Writeline] [ console-writeline]方法，它會計算 hello 文字，來計算空格和每個字 hello 結尾行結尾字元。</span><span class="sxs-lookup"><span data-stu-id="0054e-212">As it reads hello characters with hello [Console.Writeline][console-writeline] method, it counts hello words by counting spaces and end-of-line characters at hello end of each word.</span></span> <span data-ttu-id="0054e-213">然後再寫入 hello 總 toohello 標準輸出資料流以 hello [Console.Writeline] [ console-writeline]方法。</span><span class="sxs-lookup"><span data-stu-id="0054e-213">It then writes hello total toohello standard output stream with hello [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---hello-pi-estimator-source-code"></a><span data-ttu-id="0054e-214">附錄 C-hello Pi 估計工具的原始程式碼</span><span class="sxs-lookup"><span data-stu-id="0054e-214">Appendix C - hello Pi estimator source code</span></span>
<span data-ttu-id="0054e-215">使用下列檢查 hello pi 估計工具包含 hello 對應工具和減壓器函式的 Java 程式碼。</span><span class="sxs-lookup"><span data-stu-id="0054e-215">hello pi estimator Java code that contains hello mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="0054e-216">hello 對應程式會產生指定的數目的內部單位正方形隨機放置點，並再計算 hello hello 圓圈內的這些點的數目。</span><span class="sxs-lookup"><span data-stu-id="0054e-216">hello mapper program generates a specified number of points placed at random inside of a unit square and then counts hello number of those points that are inside hello circle.</span></span> <span data-ttu-id="0054e-217">hello 減壓器程式會將它們列入計算 hello 對應工具中的點，並接著評估 hello 從 hello 公式 4R，其中 R 是 hello 比例計算 hello 圓形 toohello 總數 hello 正方形中的點內的點的 hello 數目的 pi 值。</span><span class="sxs-lookup"><span data-stu-id="0054e-217">hello reducer program accumulates points counted by hello mappers and then estimates hello value of pi from hello formula 4R, where R is hello ratio of hello number of points counted inside hello circle toohello total number of points that are within hello square.</span></span>

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
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

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
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
//Assume hello current point is H(index).
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
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
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

//count points inside/outside of hello inscribed circle of hello square
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
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
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

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
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
//@return hello estimated value of Pi.
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
// multiple writers toohello same file.
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

## <a name="appendix-d---hello-10gb-graysort-source-code"></a><span data-ttu-id="0054e-218">附錄 D-hello 10gb graysort 原始程式碼</span><span class="sxs-lookup"><span data-stu-id="0054e-218">Appendix D - hello 10gb graysort source code</span></span>
<span data-ttu-id="0054e-219">hello hello TeraSort MapReduce 程式碼會檢查這一節。</span><span class="sxs-lookup"><span data-stu-id="0054e-219">hello code for hello TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
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
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
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
        * An inner trie node that contains 256 children based on hello next
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
        * A leaf trie node that does string compares toofigure out where hello given
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
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
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
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
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
        // pick up hello rest
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
