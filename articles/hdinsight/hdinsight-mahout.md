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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>透過在 HDInsight 上將 Apache Mahout 與 Hadoop 搭配使用來產生電影推薦 (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

深入了解如何 toouse hello [Apache 砲象兵](http://mahout.apache.org)Azure HDInsight toogenerate 影片建議的機器學習程式庫。 本文件中的 hello 範例會使用 Azure PowerShell toorun 砲象兵工作。

## <a name="prerequisites"></a>必要條件

* 以 Linux 為基礎的 HDInsight 叢集。 如需有關建立叢集的資訊，請參閱[開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop][getstarted]。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>使用 Azure PowerShell 產生推薦

> [!WARNING]
> 本節中的 hello 作業的運作方式是使用 Azure PowerShell。 有許多提供砲象兵 hello 類別的目前無法使用 Azure PowerShell。 無法搭配 Azure PowerShell 的類別清單，請參閱 hello[疑難排解](#troubleshooting)> 一節。
>
> 直接在 hello 叢集上使用 SSH tooconnect tooHDInsight 和執行砲象兵範例的範例，請參閱[產生影片建議使用砲象兵和 HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md)。

建議引擎所提供的砲象兵 hello 函式的其中一個。 此引擎會接受資料格式的 hello `userID`， `itemId`，和`prefValue`(hello hello 項目的使用者喜好設定)。 砲象兵會使用類似項目喜好設定，可以使用的 toomake 建議 hello 資料 toodetermine 使用者。

hello 下列範例是簡化的逐步解說的 hello 建議程序的運作方式：

* **共同出現**: Joe、 Alice 和所有按讚的 Bob*星狀戰爭*，*回 Empire 攻擊 hello*，和*傳回 hello Jedi*。 砲象兵決定使用者類似任何這些影片像 hello 其他兩個。

* **共同出現**: Bob 和 Alice 也喜歡*hello 虛設項目威脅*， *hello 複製程式碼的攻擊*，和*的 hello Sith 復仇*。 砲象兵決定使用者喜歡 hello 先前的三個影片也喜歡這些影片。

* **相似度建議**： 因為 Joe 喜歡 hello 前三個影片、 砲象兵查看電影的其他項目具有相似的偏好喜歡，但 Joe 不保存 （喜歡/評等）。 砲象兵在此情況下，建議*hello 虛設項目威脅*， *hello 複製程式碼的攻擊*，和*的 hello Sith 復仇*。

### <a name="understanding-hello-data"></a>了解 hello 資料

[GroupLens 研究][movielens]提供 Mahout 相容格式的電影評分資料。 此資料可供 hello 預設儲存體，在叢集上`/HdiSamples//HdiSamples/MahoutMovieData`。

有兩個檔案， `moviedb.txt` （hello 電影的相關資訊） 和`user-ratings.txt`。 hello`user-ratings.txt`在分析期間使用檔案。 hello`moviedb.txt`檔案時，使用的 tooprovide 使用者易記文字顯示 hello hello 分析結果。

hello 使用者 ratings.txt 中包含的資料都有一個結構的`userID`， `movieID`， `userRating`，和`timestamp`，它會告訴我們每位使用者如何高評等為電影。 Hello 資料的範例如下：

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>執行 hello 工作

使用下列 Windows PowerShell 指令碼 toorun hello 砲象兵建議引擎會使用 hello 電影資料作業的 hello:

> [!NOTE]
> 這個檔案會提示您使用的 tooconnect tooyour HDInsight 叢集，執行的工作的資訊。 它可能需要幾分鐘 hello 作業 toocomplete 並下載 hello output.txt 檔案。

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> 砲象兵作業不會移除處理 hello 作業時建立的暫存資料。 hello `--tempDir` hello 範例作業 tooisolate hello 暫存檔案中指定參數至特定的目錄。

hello 砲象兵作業不會傳回 hello 輸出 tooSTDOUT。 相反地，它將它儲存在 hello 與指定的輸出目錄**一部分-r-00000**。 hello 指令碼下載此檔案太**output.txt** hello 在工作站上的目前目錄中。

hello 下列文字是 hello 內容，這個檔案的範例：

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

hello 第一個資料行是 hello `userID`。 hello 中包含的值 '[' 和']' 是`movieId`:`recommendationScore`。

hello 指令碼也會下載 hello`moviedb.txt`和`user-ratings.txt`檔案，也就是需要的 tooformat hello 輸出 toobe 更容易閱讀。

### <a name="view-hello-output"></a>檢視 hello 輸出

雖然 hello 產生的輸出可能是 [確定] 以用於應用程式，它並不方便使用。 hello `moviedb.txt` hello 伺服器可以是使用的 tooresolve hello `movieId` tooa 電影名稱。 使用下列 PowerShell 指令碼 toodisplay 建議有名為影片的 hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

使用下列命令 toodisplay hello 建議方便使用的格式的 hello: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

hello 輸出是類似 toohello 下列文字：

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

## <a name="troubleshooting"></a>疑難排解

### <a name="cannot-overwrite-files"></a>無法覆寫檔案

Mahout 工作不會清除在處理期間所建立的暫存檔。 此外，hello 作業就不會覆寫現有的輸出檔。

tooavoid 錯誤執行砲象兵工作時刪除暫存和輸出之間的檔案時執行。 建立 tooremove hello 檔案 hello 先前的指令碼，在本文件中，使用下列 PowerShell 指令碼的 hello:

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

### <a name="nopowershell"></a>不適用於 Azure PowerShell 的類別

使用下列類別的 hello 砲象兵作業會傳回從 Windows PowerShell 中使用時的各種錯誤訊息：

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

使用這些類別、 toohello HDInsight 叢集使用 SSH 連線，並從 hello 命令列執行 hello 工作 toorun 作業。 如需使用 SSH toorun 砲象兵工作的範例，請參閱[產生影片建議使用砲象兵和 HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md)。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何 toouse 砲象兵，探索 HDInsight 上的資料搭配使用的其他方式：

* [搭配 HDInsight 使用 Hive](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [搭配 HDInsight 使用 MapReduce](hdinsight-use-mapreduce.md)

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
