---
title: "在 HDInsight 中搭配使用 Hadoop Hive 與 PowerShell - Azure | Microsoft Docs"
description: "使用 PowerShell 在 HDInsight 的 Hadoop 中執行 Hive 查詢"
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
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="5ce4d-103">使用 PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5ce4d-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="5ce4d-104">本文件提供在 Azure 資源群組模式中使用 Azure PowerShell 的範例，以便在 HDInsight 叢集的 Hadoop 中執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5ce4d-105">本文件不提供範例中使用的 HiveQL 陳述式所執行的工作詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="5ce4d-106">如需此範例中使用的 HiveQL 的相關資訊，請參閱 [在 HDInsight 上搭配 Hadoop 使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="5ce4d-107">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="5ce4d-107">**Prerequisites**</span></span>

* <span data-ttu-id="5ce4d-108">**Azure HDInsight 叢集**︰不論叢集是 Windows 型或 Linux 型。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5ce4d-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5ce4d-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5ce4d-111">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="5ce4d-112">使用 Azure PowerShell 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="5ce4d-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="5ce4d-113">Azure PowerShell 提供 *Cmdlet* ，可讓您從遠端在 HDInsight 上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="5ce4d-114">就內部而言，Cmdlet 會對 HDInsight 叢集上的 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) 進行 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="5ce4d-115">在遠端 HDInsight 叢集中執行 Hive 查詢時，會使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="5ce4d-116">**Add-AzureRmAccount**：向您的 Azure 訂用帳戶驗證 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ce4d-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="5ce4d-117">**New-AzureRmHDInsightHiveJobDefinition**：使用指定的 HiveQL 陳述式建立「作業定義」</span><span class="sxs-lookup"><span data-stu-id="5ce4d-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="5ce4d-118">**Start-AzureRmHDInsightJob**：將工作定義傳送至 HDInsight、啟動工作，然後傳回可用來檢查工作狀態的 *工作* 物件</span><span class="sxs-lookup"><span data-stu-id="5ce4d-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="5ce4d-119">**Wait-AzureRmHDInsightJob**：使用工作物件來檢查工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="5ce4d-120">它會等到工作完成，或等到等候時間超過。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="5ce4d-121">**Get-AzureRmHDInsightJobOutput**：用來擷取工作的輸出</span><span class="sxs-lookup"><span data-stu-id="5ce4d-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="5ce4d-122">**Invoke-AzureRmHDInsightHiveJob**：用來執行 HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="5ce4d-123">這個 Cmdlet 會阻止查詢完成，然後傳回結果</span><span class="sxs-lookup"><span data-stu-id="5ce4d-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="5ce4d-124">**Use-AzureRmHDInsightCluster**：設定要用於 **Invoke-AzureRmHDInsightHiveJob** 命令的目前的叢集</span><span class="sxs-lookup"><span data-stu-id="5ce4d-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="5ce4d-125">下列步驟示範如何使用這些 Cmdlet，在您的 HDInsight 叢集中執行工作：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="5ce4d-126">使用編輯器，將下列程式碼儲存為 **hivejob.ps1**。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="5ce4d-127">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="5ce4d-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="5ce4d-128">開啟新的 **Azure PowerShell** 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="5ce4d-129">將目錄變更至 **hivejob.ps1** 檔案的位置，然後使用下列命令來執行指令碼：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="5ce4d-130">執行指令碼時，系統會提示您輸入叢集名稱和該叢集的 HTTPS/管理帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="5ce4d-131">系統可能也會提示您登入 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="5ce4d-132">作業完成時，應該會傳回類似下列文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="5ce4d-133">如前所述， **Invoke-Hive** 可以用來執行查詢，並等候回應。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="5ce4d-134">使用下列指令碼，查看 Invoke-Hive 如何運作：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="5ce4d-135">[!code-powershell[主要](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="5ce4d-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="5ce4d-136">輸出看起來會像下列文字：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="5ce4d-137">如果 HiveQL 查詢的時間很長，您可以使用 Azure PowerShell **Here-Strings** Cmdlet 或 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="5ce4d-138">下列程式碼片段說明如何使用 **Invoke-Hive** Cmdlet 來執行 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="5ce4d-139">您必須將 HiveQL 指令碼檔案上傳至 wasb://。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="5ce4d-140">如需 **Here-Strings** 的詳細資訊，請參閱<a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">使用 Windows PowerShell Here-Strings</a>。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5ce4d-141">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5ce4d-141">Troubleshooting</span></span>

<span data-ttu-id="5ce4d-142">如果在工作完成時未傳回任何資訊，則可能是處理期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="5ce4d-143">若要檢視這項工作的錯誤資訊，請將下列內容新增至 **hivejob.ps1** 檔案的結尾，並儲存它，然後重新予以執行。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="5ce4d-144">這個 Cmdlet 會傳回執行作業時寫入伺服器上之 STDERR 的資訊。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="5ce4d-145">摘要</span><span class="sxs-lookup"><span data-stu-id="5ce4d-145">Summary</span></span>

<span data-ttu-id="5ce4d-146">如您所見，Azure PowerShell 提供簡單的方法，在 HDInsight 叢集中執行 Hive 查詢、監視工作狀態，以及擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="5ce4d-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ce4d-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ce4d-147">Next steps</span></span>

<span data-ttu-id="5ce4d-148">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="5ce4d-149">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5ce4d-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="5ce4d-150">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="5ce4d-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5ce4d-151">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5ce4d-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5ce4d-152">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5ce4d-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
