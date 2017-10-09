---
title: "使用 PowerShell HDInsight 的 Azure 中的 Hadoop Pig aaaUse |Microsoft 文件"
description: "了解使用 Azure PowerShell HDInsight 上 toosubmit Pig 工作 tooa Hadoop 叢集的方式。"
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
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="7e943-103">使用 HDInsight 的 Azure PowerShell toorun Pig 工作</span><span class="sxs-lookup"><span data-stu-id="7e943-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="7e943-104">本文件提供使用 Azure PowerShell toosubmit Pig 工作 tooa Hadoop HDInsight 叢集上的範例。</span><span class="sxs-lookup"><span data-stu-id="7e943-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="7e943-105">Pig 可讓您使用資料轉換為模型語言 （Pig 拉丁） 的 toowrite MapReduce 工作，而非對應並減少函式。</span><span class="sxs-lookup"><span data-stu-id="7e943-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="7e943-106">這份文件不提供 hello 範例中使用的 hello Pig 拉丁陳述式所執行的工作詳細的的描述。</span><span class="sxs-lookup"><span data-stu-id="7e943-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="7e943-107">Hello Pig 拉丁此範例中使用的相關資訊，請參閱[的 Hadoop HDInsight 上搭配使用 Pig](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="7e943-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="7e943-108"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="7e943-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7e943-109">**Azure HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="7e943-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7e943-110">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="7e943-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7e943-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="7e943-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7e943-112">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="7e943-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="7e943-113"><a id="powershell"></a>使用 PowerShell 執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="7e943-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="7e943-114">Azure PowerShell 提供*cmdlet* ，可讓您執行 tooremotely Pig 工作在 HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="7e943-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="7e943-115">就內部而言，PowerShell 會使用 REST 呼叫太[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="7e943-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="7e943-116">hello 下列指令程式可用時在遠端的 HDInsight 叢集上執行 Pig 工作：</span><span class="sxs-lookup"><span data-stu-id="7e943-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="7e943-117">**登入 AzureRmAccount**： 驗證 Azure PowerShell tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7e943-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="7e943-118">**新 AzureRmHDInsightPigJobDefinition**： 建立*作業定義*使用 hello 指定 Pig 拉丁陳述式</span><span class="sxs-lookup"><span data-stu-id="7e943-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="7e943-119">**開始 AzureRmHDInsightJob**： 傳送 hello 工作定義 tooHDInsight、 啟動 hello 工作，並傳回*作業*可以是使用的 toocheck hello hello 工作狀態的物件</span><span class="sxs-lookup"><span data-stu-id="7e943-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="7e943-120">**等候 AzureRmHDInsightJob**： 使用 hello 工作物件 toocheck hello hello 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="7e943-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="7e943-121">它會等候 hello 作業已完成，或已超過 hello 等待時間。</span><span class="sxs-lookup"><span data-stu-id="7e943-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="7e943-122">**Get AzureRmHDInsightJobOutput**： 使用 tooretrieve hello hello 工作輸出</span><span class="sxs-lookup"><span data-stu-id="7e943-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="7e943-123">hello 下列步驟示範如何 toouse 這些 cmdlet toorun 您的 HDInsight 叢集上的工作。</span><span class="sxs-lookup"><span data-stu-id="7e943-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="7e943-124">使用編輯器中，儲存下列程式碼做為 hello **pigjob.ps1**。</span><span class="sxs-lookup"><span data-stu-id="7e943-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="7e943-125">開啟新的 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="7e943-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="7e943-126">變更目錄 toohello 位置 hello **pigjob.ps1**檔案，然後使用下列命令 toorun hello 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e943-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="7e943-127">您必須提示的 toolog tooyour Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="7e943-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="7e943-128">然後，系統會詢問 hello HTTPs/系統管理員帳戶名稱和密碼 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7e943-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="7e943-129">Hello 作業完成時，它應該傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="7e943-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="7e943-130"><a id="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="7e943-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="7e943-131">如果 hello 作業完成時，會不傳回任何資訊，可能會在處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7e943-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="7e943-132">tooview 錯誤資訊，為這個工作中，加入下列命令 toohello 結尾 hello hello **pigjob.ps1**檔、 加以儲存，然後再執行一次。</span><span class="sxs-lookup"><span data-stu-id="7e943-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="7e943-133">這會傳回 hello 資訊寫入 tooSTDERR hello 伺服器上執行 hello 作業時，它可以幫助判斷 hello 作業失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="7e943-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="7e943-134"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="7e943-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="7e943-135">如您所見，Azure PowerShell 提供簡單的方式 toorun Pig 工作 HDInsight 叢集，監視 hello 工作狀態和擷取 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="7e943-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="7e943-136"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="7e943-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="7e943-137">如需 HDInsight 中 Pig 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="7e943-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="7e943-138">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e943-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="7e943-139">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="7e943-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7e943-140">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e943-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7e943-141">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="7e943-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
