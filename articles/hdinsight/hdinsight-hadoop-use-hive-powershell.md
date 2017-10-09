---
title: "使用 PowerShell HDInsight 的 Azure 中的 Hadoop Hive aaaUse |Microsoft 文件"
description: "在 HDInsight 上的 Hadoop 使用 PowerShell toorun Hive 查詢。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="67f5b-103">使用 PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="67f5b-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="67f5b-104">本文件提供使用 Azure PowerShell hello Azure 資源群組模式 toorun Hive 查詢中 HDInsight 叢集上的 Hadoop 中的範例。</span><span class="sxs-lookup"><span data-stu-id="67f5b-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="67f5b-105">這份文件不提供 hello 範例中所用的 hello HiveQL 陳述式所執行的工作詳細的的描述。</span><span class="sxs-lookup"><span data-stu-id="67f5b-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="67f5b-106">在 hello HiveQL 這個範例中所使用的資訊，請參閱[的 HDInsight 上的 Hadoop Hive 使用](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="67f5b-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="67f5b-107">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="67f5b-107">**Prerequisites**</span></span>

* <span data-ttu-id="67f5b-108">**Azure HDInsight 叢集**： 不論是否 hello 叢集是 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="67f5b-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="67f5b-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="67f5b-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="67f5b-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="67f5b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="67f5b-111">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="67f5b-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="67f5b-112">使用 Azure PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="67f5b-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="67f5b-113">Azure PowerShell 提供*cmdlet* ，HDInsight 上允許您 tooremotely 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="67f5b-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="67f5b-114">就內部而言，hello cmdlet 進行 REST 呼叫太[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="67f5b-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="67f5b-115">hello 下列指令程式會使用遠端的 HDInsight 叢集中執行 Hive 查詢時：</span><span class="sxs-lookup"><span data-stu-id="67f5b-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="67f5b-116">**新增 AzureRmAccount**： 驗證 Azure PowerShell tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="67f5b-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="67f5b-117">**新 AzureRmHDInsightHiveJobDefinition**： 建立*作業定義*使用 hello 指定 HiveQL 陳述式</span><span class="sxs-lookup"><span data-stu-id="67f5b-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="67f5b-118">**開始 AzureRmHDInsightJob**： 傳送 hello 工作定義 tooHDInsight、 啟動 hello 工作，並傳回*作業*可以是使用的 toocheck hello hello 工作狀態的物件</span><span class="sxs-lookup"><span data-stu-id="67f5b-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="67f5b-119">**等候 AzureRmHDInsightJob**： 使用 hello 工作物件 toocheck hello hello 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="67f5b-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="67f5b-120">它會等候 hello 作業完成，或超出 hello 等待時間。</span><span class="sxs-lookup"><span data-stu-id="67f5b-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="67f5b-121">**Get AzureRmHDInsightJobOutput**： 使用 tooretrieve hello hello 工作輸出</span><span class="sxs-lookup"><span data-stu-id="67f5b-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="67f5b-122">**叫用 AzureRmHDInsightHiveJob**： 使用 toorun HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="67f5b-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="67f5b-123">此 cmdlet 區塊 hello 查詢完成時，則會傳回 hello 結果</span><span class="sxs-lookup"><span data-stu-id="67f5b-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="67f5b-124">**使用 AzureRmHDInsightCluster**： 集 hello hello 目前叢集 toouse **Invoke AzureRmHDInsightHiveJob**命令</span><span class="sxs-lookup"><span data-stu-id="67f5b-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="67f5b-125">hello 下列步驟示範如何 toouse 這些 cmdlet toorun 中您的 HDInsight 叢集的工作：</span><span class="sxs-lookup"><span data-stu-id="67f5b-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="67f5b-126">使用編輯器中，儲存下列程式碼做為 hello **hivejob.ps1**。</span><span class="sxs-lookup"><span data-stu-id="67f5b-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="67f5b-127">開啟新的 **Azure PowerShell** 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="67f5b-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="67f5b-128">變更目錄 toohello 位置 hello **hivejob.ps1**檔案，然後使用下列命令 toorun hello 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="67f5b-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="67f5b-129">Hello 指令碼執行時，您將會提示的 tooenter hello 叢集名稱和 hello HTTPS/系統管理帳戶認證 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="67f5b-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="67f5b-130">您也可能提示的 toolog tooyour Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="67f5b-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="67f5b-131">Hello 作業完成時，它會傳回資訊的類似 toohello 遵循 thext:</span><span class="sxs-lookup"><span data-stu-id="67f5b-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="67f5b-132">如先前所述， **Invoke-hive**可以是使用的 toorun 查詢，並等候 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="67f5b-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="67f5b-133">使用下列方式叫用 Hive 指令碼 toosee hello:</span><span class="sxs-lookup"><span data-stu-id="67f5b-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="67f5b-134">hello 輸出看起來類似下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="67f5b-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="67f5b-135">對於較長的 HiveQL 查詢，您可以使用 hello Azure PowerShell **Here-string** cmdlet 或下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="67f5b-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="67f5b-136">下列程式碼片段說明如何 hello toouse hello **Invoke-hive** cmdlet toorun 下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="67f5b-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="67f5b-137">hello HiveQL 指令碼檔案必須上傳 toowasb: / /。</span><span class="sxs-lookup"><span data-stu-id="67f5b-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="67f5b-138">如需 **Here-Strings** 的詳細資訊，請參閱<a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">使用 Windows PowerShell Here-Strings</a>。</span><span class="sxs-lookup"><span data-stu-id="67f5b-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="67f5b-139">疑難排解</span><span class="sxs-lookup"><span data-stu-id="67f5b-139">Troubleshooting</span></span>

<span data-ttu-id="67f5b-140">如果 hello 作業完成時，會不傳回任何資訊，可能會在處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="67f5b-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="67f5b-141">tooview 錯誤資訊，為這個工作中，加入下列 toohello 結尾 hello hello **hivejob.ps1**檔、 加以儲存，然後再執行一次。</span><span class="sxs-lookup"><span data-stu-id="67f5b-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="67f5b-142">此 cmdlet 會傳回執行 hello 作業時，會寫入 tooSTDERR hello 伺服器的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="67f5b-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="67f5b-143">摘要</span><span class="sxs-lookup"><span data-stu-id="67f5b-143">Summary</span></span>

<span data-ttu-id="67f5b-144">如您所見，Azure PowerShell 提供簡單的方式 toorun HDInsight 叢集中的 Hive 查詢、 監視器 hello 工作的狀態，和擷取 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="67f5b-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67f5b-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67f5b-145">Next steps</span></span>

<span data-ttu-id="67f5b-146">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="67f5b-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="67f5b-147">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="67f5b-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="67f5b-148">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="67f5b-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="67f5b-149">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="67f5b-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="67f5b-150">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="67f5b-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
