---
title: "從 PowerShell 使用 Mahout HDInsight 產生推薦 - Azure | Microsoft Docs"
description: "了解如何從您的用戶端上執行的 PowerShell 指令碼搭配 HDInsight (Hadoop) 使用 Apache Mahout 機器學習庫來產生電影推薦。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 934de9ca2df48b29ef7a56d5729d59d77875ea7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="5c3e6-103">透過在 HDInsight 上將 Apache Mahout 與 Hadoop 搭配使用來產生電影推薦 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="5c3e6-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="5c3e6-104">了解如何使用搭配 Azure HDInsight 的 [Apache Mahout](http://mahout.apache.org) 機器學習庫產生電影推薦。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span> <span data-ttu-id="5c3e6-105">本文件中的範例使用 Azure PowerShell 來執行 Mahout 作業。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c3e6-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c3e6-106">Prerequisites</span></span>

* <span data-ttu-id="5c3e6-107">以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5c3e6-108">如需有關建立叢集的資訊，請參閱[開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop][getstarted]。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c3e6-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5c3e6-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="5c3e6-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c3e6-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="5c3e6-112"><a name="recommendations"></a>使用 Azure PowerShell 產生推薦</span><span class="sxs-lookup"><span data-stu-id="5c3e6-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="5c3e6-113">本節中的作業是使用 Azure PowerShell 運作。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-113">The job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="5c3e6-114">Mahout 提供的許多類別目前無法搭配 Azure PowerShell 使用。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="5c3e6-115">如需無法搭配 Azure PowerShell 使用的類別清單，請參閱 [疑難排解](#troubleshooting) 一節。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="5c3e6-116">如需使用 SSH 連線到 HDInsight 並在叢集上直接執行 Mahout 範例的範例，請參閱[使用 Mahout 和 HDInsight (SSH) 來產生電影推薦](hdinsight-hadoop-mahout-linux-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="5c3e6-117">Mahout 提供的其中一項功能是推薦引擎。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-117">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="5c3e6-118">這個引擎接受 `userID``itemId` 和 `prefValue` (使用者偏好的項目) 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span></span> <span data-ttu-id="5c3e6-119">Mahout 會使用資料以偏好的類似項目判斷使用者，並以此做出推薦。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="5c3e6-120">下列範例是簡化的逐步解說，說明建議程序如何運作：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-120">The following example is a simplified walk-through of how the recommendation process works:</span></span>

* <span data-ttu-id="5c3e6-121">**共生**：Joe、Alice 和 Bob 都喜歡*《星際大戰》*、*《帝國大反擊》*和*《絕地大反攻》*。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="5c3e6-122">Mahout 將判斷喜歡上述任何一部電影的使用者，也會喜歡另外兩部電影。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-122">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="5c3e6-123">**共生**：Bob 和 Alice 同時也喜歡*《威脅潛伏》*、*《複製人全面進攻》*和*《西斯大帝的復仇》*。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="5c3e6-124">Mahout 將判斷喜歡前三部電影的使用者，也會喜歡這些電影。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-124">Mahout determines that users who liked the previous three movies also like these movies.</span></span>

* <span data-ttu-id="5c3e6-125">**相似性推薦**：因為 Joe 喜歡前三部電影，Mahout 會查看具有相似偏好的其他使用者所喜歡但 Joe 還沒看過 (喜歡/評價) 的電影。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="5c3e6-126">在此情況下，Mahout 將會推薦*《威脅潛伏》*、*《複製人全面進攻》*和*《西斯大帝的復仇》*。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="5c3e6-127">了解資料</span><span class="sxs-lookup"><span data-stu-id="5c3e6-127">Understanding the data</span></span>

<span data-ttu-id="5c3e6-128">[GroupLens 研究][movielens]提供 Mahout 相容格式的電影評分資料。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="5c3e6-129">您可在位於 `/HdiSamples//HdiSamples/MahoutMovieData` 的叢集預設儲存體取得這份資料。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="5c3e6-130">有兩份檔案：`moviedb.txt` (電影相關資訊) 和 `user-ratings.txt`。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="5c3e6-131">`user-ratings.txt` 檔案是用於分析期間。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-131">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="5c3e6-132">`moviedb.txt` 檔案是在顯示分析結果時，用來提供易懂的文字。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span></span>

<span data-ttu-id="5c3e6-133">user-ratings.txt 內包含的資料具有 `userID`、`movieID`、`userRating` 和 `timestamp` 結構，可告訴我們每位使用者對於影片的評價為何。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="5c3e6-134">以下是資料範例：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-134">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-the-job"></a><span data-ttu-id="5c3e6-135">執行工作</span><span class="sxs-lookup"><span data-stu-id="5c3e6-135">Run the job</span></span>

<span data-ttu-id="5c3e6-136">使用下列 Windows PowerShell 指令碼執行工作，以透過 Mahout 推薦引擎來處理影片資料：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="5c3e6-137">這個檔案會提示您輸入用來連接到 HDInsight 叢集並執行作業的資訊。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span></span> <span data-ttu-id="5c3e6-138">可能需要幾分鐘的時間來完成作業，並且下載 output.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-138">It may take several minutes for the jobs to complete and download the output.txt file.</span></span>

<span data-ttu-id="5c3e6-139">[!code-powershell[主要](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span><span class="sxs-lookup"><span data-stu-id="5c3e6-139">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span></span>

> [!NOTE]
> <span data-ttu-id="5c3e6-140">Mahout 工作不會移除處理工作時所建立的暫存資料。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-140">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="5c3e6-141">範例工作中所指定的 `--tempDir` 參數會將暫存檔隔離到特定的目錄。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-141">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span></span>

<span data-ttu-id="5c3e6-142">Mahout 工作不會將輸出傳回 STDOUT。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-142">The Mahout job does not return the output to STDOUT.</span></span> <span data-ttu-id="5c3e6-143">相反地，其會將該輸出儲存在指定的輸出目錄 **part-r-00000**中。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-143">Instead, it stores it in the specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="5c3e6-144">指令碼會下載這個檔案到您工作站上目前目錄的 **output.txt** 檔。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-144">The script downloads this file to **output.txt** in the current directory on your workstation.</span></span>

<span data-ttu-id="5c3e6-145">下列文字是此檔案內容的範例：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-145">The following text is an example of the content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="5c3e6-146">第一欄是 `userID`。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-146">The first column is the `userID`.</span></span> <span data-ttu-id="5c3e6-147">'[' 和 ']' 中包含的值是 `movieId`:`recommendationScore`。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-147">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="5c3e6-148">指令碼也會下載使輸出格式更具可讀性所需的 `moviedb.txt` 和 `user-ratings.txt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-148">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span></span>

### <a name="view-the-output"></a><span data-ttu-id="5c3e6-149">檢視輸出</span><span class="sxs-lookup"><span data-stu-id="5c3e6-149">View the output</span></span>

<span data-ttu-id="5c3e6-150">雖然產生的輸出可以在應用程式中使用，但使用者不容易判讀。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-150">Although the generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="5c3e6-151">來自伺服器的 `moviedb.txt`可用來解決電影名稱的 `movieId`。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-151">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span></span> <span data-ttu-id="5c3e6-152">使用下列 PowerShell 指令碼來顯示建議的影片名稱︰</span><span class="sxs-lookup"><span data-stu-id="5c3e6-152">Use the following PowerShell script to display recommendations with movie names:</span></span>

<span data-ttu-id="5c3e6-153">[!code-powershell[主要](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span><span class="sxs-lookup"><span data-stu-id="5c3e6-153">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span></span>

<span data-ttu-id="5c3e6-154">使用下列命令，以易懂的格式來顯示建議：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-154">Use the following command to display the recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="5c3e6-155">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-155">The output is similar to the following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, The (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of the Dove, The (1997)            4.6666665
    People vs. Larry Flynt, The (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="5c3e6-156"><a name="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="5c3e6-156"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="5c3e6-157">無法覆寫檔案</span><span class="sxs-lookup"><span data-stu-id="5c3e6-157">Cannot overwrite files</span></span>

<span data-ttu-id="5c3e6-158">Mahout 工作不會清除在處理期間所建立的暫存檔。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-158">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="5c3e6-159">此外，作業也不會覆寫現有的輸出檔。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-159">In addition, the jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="5c3e6-160">為了避免執行 Mahout 作業時發生錯誤，請在每次執行之前刪除暫存檔和輸出檔。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-160">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="5c3e6-161">若要移除本文件中先前指令碼所建立的檔案，請使用下列 PowerShell 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="5c3e6-161">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have to get a list and delete one at a time
# Start with the output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next the temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="5c3e6-162"><a name="nopowershell"></a>不適用於 Azure PowerShell 的類別</span><span class="sxs-lookup"><span data-stu-id="5c3e6-162"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="5c3e6-163">當從 Windows PowerShell 中使用的 Mahout 作業利用到下列類別時，會傳回各種錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-163">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="5c3e6-164">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="5c3e6-164">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="5c3e6-165">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="5c3e6-165">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="5c3e6-166">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="5c3e6-166">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="5c3e6-167">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="5c3e6-167">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="5c3e6-168">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="5c3e6-168">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="5c3e6-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="5c3e6-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="5c3e6-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="5c3e6-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="5c3e6-171">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="5c3e6-171">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="5c3e6-172">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="5c3e6-172">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="5c3e6-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="5c3e6-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="5c3e6-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="5c3e6-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="5c3e6-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="5c3e6-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="5c3e6-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="5c3e6-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="5c3e6-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="5c3e6-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="5c3e6-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="5c3e6-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="5c3e6-179">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="5c3e6-179">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="5c3e6-180">若要執行用到這些類別的作業，請使用 SSH 連接至 HDInsight 叢集，然後從命令列執行作業。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-180">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span></span> <span data-ttu-id="5c3e6-181">如需使用 SSH 來執行 Mahout 作業的範例，請參閱[使用 Mahout 和 HDInsight (SSH) 來產生電影推薦](hdinsight-hadoop-mahout-linux-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="5c3e6-181">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c3e6-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c3e6-182">Next steps</span></span>

<span data-ttu-id="5c3e6-183">您現在已了解如何使用 Mahout，請繼續探索在 HDInsight 上使用資料的其他方法：</span><span class="sxs-lookup"><span data-stu-id="5c3e6-183">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="5c3e6-184">搭配 HDInsight 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="5c3e6-184">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5c3e6-185">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="5c3e6-185">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5c3e6-186">搭配 HDInsight 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="5c3e6-186">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
