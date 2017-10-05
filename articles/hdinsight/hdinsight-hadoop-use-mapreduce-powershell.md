---
title: "搭配使用 MapReduce 和 PowerShell 與 Hadoop - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 PowerShell 從遠端搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop。"
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
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="78f6e-103">使用 PowerShell 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="78f6e-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="78f6e-104">本文件提供使用 Azure PowerShell 在 HDInsight 叢集的 Hadoop 中執行 MapReduce 工作的範例。</span><span class="sxs-lookup"><span data-stu-id="78f6e-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="78f6e-105"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="78f6e-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="78f6e-106">**Azure HDInsight (HDInsight 上的 Hadoop) 叢集**</span><span class="sxs-lookup"><span data-stu-id="78f6e-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="78f6e-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="78f6e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78f6e-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="78f6e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="78f6e-109">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="78f6e-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="78f6e-110"><a id="powershell"></a>使用 Azure PowerShell 執行 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="78f6e-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="78f6e-111">Azure PowerShell 提供 *Cmdlet* ，可讓您從遠端在 HDInsight 上執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="78f6e-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="78f6e-112">在內部，您可以使用在 HDInsight 叢集上執行的 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (先前稱為 Templeton) 的 REST 呼叫來達到此目的。</span><span class="sxs-lookup"><span data-stu-id="78f6e-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="78f6e-113">在遠端 HDInsight 叢集中執行 MapReduce 工作時，會使用下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="78f6e-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="78f6e-114">**Login-AzureRmAccount**：向您的 Azure 訂用帳戶驗證 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="78f6e-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="78f6e-115">**New-AzureRmHDInsightMapReduceJobDefinition**：使用指定的 MapReduce 資訊建立新的「工作定義」。</span><span class="sxs-lookup"><span data-stu-id="78f6e-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="78f6e-116">**Start-AzureRmHDInsightJob**：將工作定義傳送至 HDInsight、啟動工作，然後傳回可用來檢查工作狀態的「工作」物件。</span><span class="sxs-lookup"><span data-stu-id="78f6e-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="78f6e-117">**Wait-AzureRmHDInsightJob**：使用工作物件來檢查工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="78f6e-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="78f6e-118">它會等到工作完成，或等到等候時間超過。</span><span class="sxs-lookup"><span data-stu-id="78f6e-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="78f6e-119">**Get-AzureRmHDInsightJobOutput**：用來擷取工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="78f6e-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="78f6e-120">下列步驟示範如何使用這些 Cmdlet，在您的 HDInsight 叢集中執行工作。</span><span class="sxs-lookup"><span data-stu-id="78f6e-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="78f6e-121">使用編輯器，將下列程式碼儲存為 **mapreducejob.ps1**。</span><span class="sxs-lookup"><span data-stu-id="78f6e-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="78f6e-122">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="78f6e-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="78f6e-123">開啟新的 **Azure PowerShell** 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="78f6e-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="78f6e-124">將目錄變更至 **mapreducejob.ps1** 檔案的位置，然後使用下列命令來執行指令碼：</span><span class="sxs-lookup"><span data-stu-id="78f6e-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="78f6e-125">當您執行指令碼時，系統會提示您的 HDInsight 叢集名稱和 HTTPS/管理帳戶名稱以及叢集的密碼。</span><span class="sxs-lookup"><span data-stu-id="78f6e-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="78f6e-126">系統可能也會提示您驗證 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="78f6e-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="78f6e-127">在作業完成時，您會收到類似下列文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="78f6e-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="78f6e-128">此輸出表示工作已順利完成。</span><span class="sxs-lookup"><span data-stu-id="78f6e-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78f6e-129">如果 **ExitCode** 的值不是 0，請參閱 [疑難排解](#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="78f6e-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="78f6e-130">此範例也會將下載的檔案儲存到您執行指令碼所在目錄中的 **output.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="78f6e-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="78f6e-131">檢視輸出</span><span class="sxs-lookup"><span data-stu-id="78f6e-131">View output</span></span>

<span data-ttu-id="78f6e-132">使用文字編輯器開啟 **output.txt** 檔案，以查看作業所產生的單字和計數。</span><span class="sxs-lookup"><span data-stu-id="78f6e-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="78f6e-133">MapReduce 工作的輸出檔是固定不變的。</span><span class="sxs-lookup"><span data-stu-id="78f6e-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="78f6e-134">因此，如果您重新執行此範例，則需要變更輸出檔的名稱。</span><span class="sxs-lookup"><span data-stu-id="78f6e-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="78f6e-135"><a id="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="78f6e-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="78f6e-136">如果在工作完成時未傳回任何資訊，則可能是處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="78f6e-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="78f6e-137">若要檢視這項工作的錯誤資訊，請將下列命令新增至 **mapreducejob.ps1** 檔案的結尾，並儲存它，然後重新予以執行。</span><span class="sxs-lookup"><span data-stu-id="78f6e-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="78f6e-138">這個 Cmdlet 會傳回執行作業時寫入至伺服器上之 STDERR 的資訊，而且可能有助於判斷作業的失敗原因。</span><span class="sxs-lookup"><span data-stu-id="78f6e-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="78f6e-139"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="78f6e-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="78f6e-140">如您所見，Azure PowerShell 提供簡單的方法，在 HDInsight 叢集上執行 MapReduce 工作、監視工作狀態，以及擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="78f6e-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="78f6e-141"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="78f6e-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="78f6e-142">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="78f6e-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="78f6e-143">在 HDInsight Hadoop 上使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="78f6e-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="78f6e-144">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="78f6e-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="78f6e-145">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="78f6e-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="78f6e-146">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="78f6e-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
