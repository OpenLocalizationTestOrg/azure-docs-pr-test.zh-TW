---
title: "aaaUse MapReduce 與 PowerShell 搭配 Hadoop-Azure HDInsight |Microsoft 文件"
description: "了解如何 toouse PowerShell tooremotely 執行的 Hadoop 上 HDInsight MapReduce 工作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="c3bb0-103">使用 PowerShell 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="c3bb0-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="c3bb0-104">本文件提供在 HDInsight 叢集上使用 Azure PowerShell toorun 的範例中的 Hadoop MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="c3bb0-105"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="c3bb0-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="c3bb0-106">**Azure HDInsight (HDInsight 上的 Hadoop) 叢集**</span><span class="sxs-lookup"><span data-stu-id="c3bb0-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c3bb0-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3bb0-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c3bb0-109">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="c3bb0-110"><a id="powershell"></a>使用 Azure PowerShell 執行 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="c3bb0-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="c3bb0-111">Azure PowerShell 提供*cmdlet* ，HDInsight 上允許您 tooremotely 執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="c3bb0-112">就內部而言，這就會經由 REST 呼叫太[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) （之前稱為 Templeton） 上執行 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="c3bb0-113">hello 下列指令程式會使用遠端的 HDInsight 叢集中執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="c3bb0-114">**登入 AzureRmAccount**： 驗證 Azure PowerShell tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="c3bb0-115">**新 AzureRmHDInsightMapReduceJobDefinition**： 建立新*作業定義*使用 hello 指定 MapReduce 資訊。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="c3bb0-116">**開始 AzureRmHDInsightJob**： 傳送 hello 工作定義 tooHDInsight、 啟動 hello 工作，並傳回*作業*可以是使用的 toocheck hello hello 工作狀態的物件。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="c3bb0-117">**等候 AzureRmHDInsightJob**： 使用 hello 工作物件 toocheck hello hello 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="c3bb0-118">它會等候 hello 作業完成，或超出 hello 等待時間。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="c3bb0-119">**Get AzureRmHDInsightJobOutput**： 使用 tooretrieve hello hello 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="c3bb0-120">hello 下列步驟示範如何 toouse 這些 cmdlet toorun 中您的 HDInsight 叢集的作業。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="c3bb0-121">使用編輯器中，儲存下列程式碼做為 hello **mapreducejob.ps1**。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="c3bb0-122">開啟新的 **Azure PowerShell** 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="c3bb0-123">變更目錄 toohello 位置 hello **mapreducejob.ps1**檔案，然後使用下列命令 toorun hello 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3bb0-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="c3bb0-124">當您執行 hello 指令碼時，系統會提示您輸入 hello hello HDInsight 叢集名稱和 hello HTTPS/系統管理員帳戶名稱和密碼 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="c3bb0-125">您也可能提示的 tooauthenticate tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="c3bb0-126">Hello 作業完成時，您會收到下列文字的輸出類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="c3bb0-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="c3bb0-127">此輸出會指出該 hello 工作順利完成。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3bb0-128">如果 hello **ExitCode**是值不是 0，請參閱[疑難排解](#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="c3bb0-129">此範例也會儲存下載的 hello 檔案 tooan **output.txt** hello 目錄中，執行中的 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="c3bb0-130">檢視輸出</span><span class="sxs-lookup"><span data-stu-id="c3bb0-130">View output</span></span>

<span data-ttu-id="c3bb0-131">開啟 hello **output.txt**檔案中的文字編輯器 toosee hello 文字和計數 hello 工作所產生。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="c3bb0-132">MapReduce 工作的 hello 輸出檔是不變。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="c3bb0-133">因此如果您重新執行此範例中，您會需要 toochange hello hello 輸出檔名稱。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="c3bb0-134"><a id="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="c3bb0-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="c3bb0-135">如果 hello 作業完成時，會不傳回任何資訊，可能會在處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="c3bb0-136">tooview 錯誤資訊，為這個工作中，加入下列命令 toohello 結尾 hello hello **mapreducejob.ps1**檔、 加以儲存，然後再執行一次。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="c3bb0-137">此 cmdlet 會傳回 hello 資訊寫入 tooSTDERR hello 伺服器上執行 hello 作業時，它可以幫助判斷 hello 作業失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="c3bb0-138"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="c3bb0-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="c3bb0-139">如您所見，Azure PowerShell 提供簡單的方式 toorun MapReduce 工作的 HDInsight 叢集，監視 hello 工作狀態和擷取 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="c3bb0-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="c3bb0-140"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="c3bb0-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="c3bb0-141">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="c3bb0-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="c3bb0-142">在 HDInsight Hadoop 上使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="c3bb0-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="c3bb0-143">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="c3bb0-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c3bb0-144">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="c3bb0-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c3bb0-145">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="c3bb0-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
