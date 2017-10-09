---
title: "使用 PowerShell-Azure 從砲象兵 HDInsight aaaGenerate 建議 |Microsoft 文件"
description: "了解如何 toouse hello Apache 砲象兵機器學習您的用戶端上執行的 PowerShell 指令碼程式庫 toogenerate 影片建議與 HDInsight (Hadoop)。"
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
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="ef863-103">透過在 HDInsight 上將 Apache Mahout 與 Hadoop 搭配使用來產生電影推薦 (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ef863-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="ef863-104">深入了解如何 toouse hello [Apache 砲象兵](http://mahout.apache.org)Azure HDInsight toogenerate 影片建議的機器學習程式庫。</span><span class="sxs-lookup"><span data-stu-id="ef863-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="ef863-105">本文件中的 hello 範例會使用 Azure PowerShell toorun 砲象兵工作。</span><span class="sxs-lookup"><span data-stu-id="ef863-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef863-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="ef863-106">Prerequisites</span></span>

* <span data-ttu-id="ef863-107">以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ef863-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ef863-108">如需有關建立叢集的資訊，請參閱[開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop][getstarted]。</span><span class="sxs-lookup"><span data-stu-id="ef863-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef863-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="ef863-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ef863-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ef863-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="ef863-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef863-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="ef863-112"><a name="recommendations"></a>使用 Azure PowerShell 產生推薦</span><span class="sxs-lookup"><span data-stu-id="ef863-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="ef863-113">本節中的 hello 作業的運作方式是使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ef863-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="ef863-114">有許多提供砲象兵 hello 類別的目前無法使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ef863-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="ef863-115">無法搭配 Azure PowerShell 的類別清單，請參閱 hello[疑難排解](#troubleshooting)> 一節。</span><span class="sxs-lookup"><span data-stu-id="ef863-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="ef863-116">直接在 hello 叢集上使用 SSH tooconnect tooHDInsight 和執行砲象兵範例的範例，請參閱[產生影片建議使用砲象兵和 HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="ef863-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="ef863-117">建議引擎所提供的砲象兵 hello 函式的其中一個。</span><span class="sxs-lookup"><span data-stu-id="ef863-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="ef863-118">此引擎會接受資料格式的 hello `userID`， `itemId`，和`prefValue`(hello hello 項目的使用者喜好設定)。</span><span class="sxs-lookup"><span data-stu-id="ef863-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="ef863-119">砲象兵會使用類似項目喜好設定，可以使用的 toomake 建議 hello 資料 toodetermine 使用者。</span><span class="sxs-lookup"><span data-stu-id="ef863-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="ef863-120">hello 下列範例是簡化的逐步解說的 hello 建議程序的運作方式：</span><span class="sxs-lookup"><span data-stu-id="ef863-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="ef863-121">**共同出現**: Joe、 Alice 和所有按讚的 Bob*星狀戰爭*，*回 Empire 攻擊 hello*，和*傳回 hello Jedi*。</span><span class="sxs-lookup"><span data-stu-id="ef863-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="ef863-122">砲象兵決定使用者類似任何這些影片像 hello 其他兩個。</span><span class="sxs-lookup"><span data-stu-id="ef863-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="ef863-123">**共同出現**: Bob 和 Alice 也喜歡*hello 虛設項目威脅*， *hello 複製程式碼的攻擊*，和*的 hello Sith 復仇*。</span><span class="sxs-lookup"><span data-stu-id="ef863-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="ef863-124">砲象兵決定使用者喜歡 hello 先前的三個影片也喜歡這些影片。</span><span class="sxs-lookup"><span data-stu-id="ef863-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="ef863-125">**相似度建議**： 因為 Joe 喜歡 hello 前三個影片、 砲象兵查看電影的其他項目具有相似的偏好喜歡，但 Joe 不保存 （喜歡/評等）。</span><span class="sxs-lookup"><span data-stu-id="ef863-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="ef863-126">砲象兵在此情況下，建議*hello 虛設項目威脅*， *hello 複製程式碼的攻擊*，和*的 hello Sith 復仇*。</span><span class="sxs-lookup"><span data-stu-id="ef863-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="ef863-127">了解 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ef863-127">Understanding hello data</span></span>

<span data-ttu-id="ef863-128">[GroupLens 研究][movielens]提供 Mahout 相容格式的電影評分資料。</span><span class="sxs-lookup"><span data-stu-id="ef863-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="ef863-129">此資料可供 hello 預設儲存體，在叢集上`/HdiSamples//HdiSamples/MahoutMovieData`。</span><span class="sxs-lookup"><span data-stu-id="ef863-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="ef863-130">有兩個檔案， `moviedb.txt` （hello 電影的相關資訊） 和`user-ratings.txt`。</span><span class="sxs-lookup"><span data-stu-id="ef863-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="ef863-131">hello`user-ratings.txt`在分析期間使用檔案。</span><span class="sxs-lookup"><span data-stu-id="ef863-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="ef863-132">hello`moviedb.txt`檔案時，使用的 tooprovide 使用者易記文字顯示 hello hello 分析結果。</span><span class="sxs-lookup"><span data-stu-id="ef863-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="ef863-133">hello 使用者 ratings.txt 中包含的資料都有一個結構的`userID`， `movieID`， `userRating`，和`timestamp`，它會告訴我們每位使用者如何高評等為電影。</span><span class="sxs-lookup"><span data-stu-id="ef863-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="ef863-134">Hello 資料的範例如下：</span><span class="sxs-lookup"><span data-stu-id="ef863-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="ef863-135">執行 hello 工作</span><span class="sxs-lookup"><span data-stu-id="ef863-135">Run hello job</span></span>

<span data-ttu-id="ef863-136">使用下列 Windows PowerShell 指令碼 toorun hello 砲象兵建議引擎會使用 hello 電影資料作業的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef863-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="ef863-137">這個檔案會提示您使用的 tooconnect tooyour HDInsight 叢集，執行的工作的資訊。</span><span class="sxs-lookup"><span data-stu-id="ef863-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="ef863-138">它可能需要幾分鐘 hello 作業 toocomplete 並下載 hello output.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef863-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="ef863-139">砲象兵作業不會移除處理 hello 作業時建立的暫存資料。</span><span class="sxs-lookup"><span data-stu-id="ef863-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="ef863-140">hello `--tempDir` hello 範例作業 tooisolate hello 暫存檔案中指定參數至特定的目錄。</span><span class="sxs-lookup"><span data-stu-id="ef863-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="ef863-141">hello 砲象兵作業不會傳回 hello 輸出 tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="ef863-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="ef863-142">相反地，它將它儲存在 hello 與指定的輸出目錄**一部分-r-00000**。</span><span class="sxs-lookup"><span data-stu-id="ef863-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="ef863-143">hello 指令碼下載此檔案太**output.txt** hello 在工作站上的目前目錄中。</span><span class="sxs-lookup"><span data-stu-id="ef863-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="ef863-144">hello 下列文字是 hello 內容，這個檔案的範例：</span><span class="sxs-lookup"><span data-stu-id="ef863-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="ef863-145">hello 第一個資料行是 hello `userID`。</span><span class="sxs-lookup"><span data-stu-id="ef863-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="ef863-146">hello 中包含的值 '[' 和']' 是`movieId`:`recommendationScore`。</span><span class="sxs-lookup"><span data-stu-id="ef863-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="ef863-147">hello 指令碼也會下載 hello`moviedb.txt`和`user-ratings.txt`檔案，也就是需要的 tooformat hello 輸出 toobe 更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="ef863-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="ef863-148">檢視 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="ef863-148">View hello output</span></span>

<span data-ttu-id="ef863-149">雖然 hello 產生的輸出可能是 [確定] 以用於應用程式，它並不方便使用。</span><span class="sxs-lookup"><span data-stu-id="ef863-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="ef863-150">hello `moviedb.txt` hello 伺服器可以是使用的 tooresolve hello `movieId` tooa 電影名稱。</span><span class="sxs-lookup"><span data-stu-id="ef863-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="ef863-151">使用下列 PowerShell 指令碼 toodisplay 建議有名為影片的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef863-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="ef863-152">使用下列命令 toodisplay hello 建議方便使用的格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef863-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="ef863-153">hello 輸出是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="ef863-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
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
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="ef863-154"><a name="troubleshooting"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="ef863-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="ef863-155">無法覆寫檔案</span><span class="sxs-lookup"><span data-stu-id="ef863-155">Cannot overwrite files</span></span>

<span data-ttu-id="ef863-156">Mahout 工作不會清除在處理期間所建立的暫存檔。</span><span class="sxs-lookup"><span data-stu-id="ef863-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="ef863-157">此外，hello 作業就不會覆寫現有的輸出檔。</span><span class="sxs-lookup"><span data-stu-id="ef863-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="ef863-158">tooavoid 錯誤執行砲象兵工作時刪除暫存和輸出之間的檔案時執行。</span><span class="sxs-lookup"><span data-stu-id="ef863-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="ef863-159">建立 tooremove hello 檔案 hello 先前的指令碼，在本文件中，使用下列 PowerShell 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="ef863-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="ef863-160"><a name="nopowershell"></a>不適用於 Azure PowerShell 的類別</span><span class="sxs-lookup"><span data-stu-id="ef863-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="ef863-161">使用下列類別的 hello 砲象兵作業會傳回從 Windows PowerShell 中使用時的各種錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="ef863-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="ef863-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="ef863-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="ef863-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="ef863-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="ef863-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="ef863-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="ef863-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="ef863-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="ef863-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="ef863-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="ef863-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="ef863-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="ef863-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="ef863-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="ef863-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="ef863-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="ef863-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="ef863-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="ef863-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="ef863-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="ef863-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="ef863-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="ef863-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="ef863-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="ef863-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="ef863-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="ef863-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="ef863-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="ef863-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="ef863-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="ef863-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="ef863-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="ef863-178">使用這些類別、 toohello HDInsight 叢集使用 SSH 連線，並從 hello 命令列執行 hello 工作 toorun 作業。</span><span class="sxs-lookup"><span data-stu-id="ef863-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="ef863-179">如需使用 SSH toorun 砲象兵工作的範例，請參閱[產生影片建議使用砲象兵和 HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="ef863-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef863-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef863-180">Next steps</span></span>

<span data-ttu-id="ef863-181">既然您已經學會如何 toouse 砲象兵，探索 HDInsight 上的資料搭配使用的其他方式：</span><span class="sxs-lookup"><span data-stu-id="ef863-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="ef863-182">搭配 HDInsight 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="ef863-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ef863-183">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="ef863-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ef863-184">搭配 HDInsight 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="ef863-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
