---
title: "在 HDInsight 中搭配使用 Hadoop Pig 與 PowerShell - Azure | Microsoft Docs"
description: "了解如何使用 Azure PowerShell 將 Pig 工作提交至 HDInsight 上的 Hadoop 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="03efc-103">使用 Azure PowerShell 執行 Pig 工作與 HDInsight</span><span class="sxs-lookup"><span data-stu-id="03efc-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="03efc-104">本文件提供使用 Azure PowerShell 將 Pig 工作提交至 HDInsight 叢集上的 Hadoop 的範例。</span><span class="sxs-lookup"><span data-stu-id="03efc-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="03efc-105">Pig 可讓您使用可建立資料轉換模型的語言 (Pig Latin) 撰寫 MapReduce 工作，而不是撰寫對應和歸納函數。</span><span class="sxs-lookup"><span data-stu-id="03efc-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="03efc-106">本文件不提供範例中使用的 Pig Latin 陳述式所執行的工作詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="03efc-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="03efc-107">如需此範例中使用的 Pig Latin 相關資訊，請參閱 [在 HDInsight 上搭配 Hadoop 使用 Pig](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="03efc-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="03efc-108"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="03efc-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="03efc-109">**Azure HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="03efc-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="03efc-110">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="03efc-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="03efc-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="03efc-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="03efc-112">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="03efc-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="03efc-113"><a id="powershell"></a>使用 PowerShell 執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="03efc-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="03efc-114">Azure PowerShell 提供 *Cmdlet* ，可讓您從遠端在 HDInsight 上執行 Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="03efc-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="03efc-115">就內部而言，PowerShell 會使用 REST 呼叫 HDInsight 叢集上執行的 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat)。</span><span class="sxs-lookup"><span data-stu-id="03efc-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="03efc-116">在遠端 HDInsight 叢集上執行 Pig 工作時，會使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="03efc-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="03efc-117">**Login-AzureRmAccount**：向您的 Azure 訂用帳戶驗證 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="03efc-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="03efc-118">**New-AzureRmHDInsightPigJobDefinition**：使用指定的 Pig Latin 陳述式建立*作業定義*</span><span class="sxs-lookup"><span data-stu-id="03efc-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="03efc-119">**Start-AzureRmHDInsightJob**：將工作定義傳送至 HDInsight、啟動工作，然後傳回可用來檢查工作狀態的 *工作* 物件</span><span class="sxs-lookup"><span data-stu-id="03efc-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="03efc-120">**Wait-AzureRmHDInsightJob**：使用工作物件來檢查工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="03efc-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="03efc-121">它會等到作業完成，或超過等候時間。</span><span class="sxs-lookup"><span data-stu-id="03efc-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="03efc-122">**Get-AzureRmHDInsightJobOutput**：用來擷取工作的輸出</span><span class="sxs-lookup"><span data-stu-id="03efc-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="03efc-123">下列步驟示範如何使用這些 Cmdlet，在您的 HDInsight 叢集上執行工作。</span><span class="sxs-lookup"><span data-stu-id="03efc-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="03efc-124">使用編輯器，將下列程式碼儲存為 **pigjob.ps1**。</span><span class="sxs-lookup"><span data-stu-id="03efc-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="03efc-125">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="03efc-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="03efc-126">開啟新的 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="03efc-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="03efc-127">將目錄變更至 **pigjob.ps1** 檔案的位置，然後使用下列命令來執行指令碼：</span><span class="sxs-lookup"><span data-stu-id="03efc-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="03efc-128">系統會提示您登入 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="03efc-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="03efc-129">接著，您必須提供 HDInsight 叢集的 HTTP/管理帳戶名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="03efc-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="03efc-130">作業完成時，應該會傳回與下面文字類似的資訊：</span><span class="sxs-lookup"><span data-stu-id="03efc-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="03efc-131"><a id="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="03efc-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="03efc-132">如果在工作完成時未傳回任何資訊，則可能是處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="03efc-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="03efc-133">若要檢視這項工作的錯誤資訊，請將下列命令新增至 **pigjob.ps1** 檔案的結尾，並儲存它，然後重新予以執行。</span><span class="sxs-lookup"><span data-stu-id="03efc-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="03efc-134">這會傳回執行工作時寫入至伺服器上之 STDERR 的資訊，而且可能有助於判斷工作的失敗原因。</span><span class="sxs-lookup"><span data-stu-id="03efc-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="03efc-135"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="03efc-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="03efc-136">如您所見，Azure PowerShell 提供簡單的方法，在 HDInsight 叢集上執行 Pig 工作、監視工作狀態，以及擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="03efc-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="03efc-137"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="03efc-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="03efc-138">如需 HDInsight 中 Pig 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="03efc-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="03efc-139">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="03efc-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="03efc-140">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="03efc-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="03efc-141">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="03efc-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="03efc-142">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="03efc-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
