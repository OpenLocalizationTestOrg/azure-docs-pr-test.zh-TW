---
title: "使用 Mahout 和 HDInsight 產生推薦 (SSH) - Azure | Microsoft Docs"
description: "了解如何搭配 HDInsight (Hadoop) 使用 Apache Mahout 機器學習庫來產生電影推薦。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="1201c-103">在 HDInsight 中搭配使用 Apache Mahout 和以 Linux 為基礎的 Hadoop 來產生電影推薦 (SSH)</span><span class="sxs-lookup"><span data-stu-id="1201c-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="1201c-104">了解如何使用搭配 Azure HDInsight 的 [Apache Mahout](http://mahout.apache.org) 機器學習庫產生電影推薦。</span><span class="sxs-lookup"><span data-stu-id="1201c-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="1201c-105">Mahout 是 Apache Hadoop 的[機器學習服務][ml]程式庫。</span><span class="sxs-lookup"><span data-stu-id="1201c-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="1201c-106">Mahout 包含可處理資料的演算法，例如篩選、分類和叢集化。</span><span class="sxs-lookup"><span data-stu-id="1201c-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="1201c-107">在本文中，您會使用推薦引擎，以根據朋友看過的電影來產生電影推薦。</span><span class="sxs-lookup"><span data-stu-id="1201c-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1201c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1201c-108">Prerequisites</span></span>

* <span data-ttu-id="1201c-109">以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1201c-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1201c-110">如需有關建立叢集的資訊，請參閱[開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop][getstarted]。</span><span class="sxs-lookup"><span data-stu-id="1201c-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1201c-111">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="1201c-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1201c-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="1201c-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1201c-113">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1201c-113">An SSH client.</span></span> <span data-ttu-id="1201c-114">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="1201c-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="1201c-115">Mahout 版本控制</span><span class="sxs-lookup"><span data-stu-id="1201c-115">Mahout versioning</span></span>

<span data-ttu-id="1201c-116">如需 HDInsight 中 Mahout 版本的詳細資訊，請參閱 [HDInsight 版本和 Hadoop 元件](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="1201c-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="1201c-117"><a name="recommendations"></a>了解推薦</span><span class="sxs-lookup"><span data-stu-id="1201c-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="1201c-118">Mahout 提供的其中一項功能是推薦引擎。</span><span class="sxs-lookup"><span data-stu-id="1201c-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="1201c-119">這個引擎接受 `userID`、`itemId` 和 `prefValue` (項目的喜好設定) 格式的資料。</span><span class="sxs-lookup"><span data-stu-id="1201c-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="1201c-120">Mahout 接著可以執行共生分析判斷出： *偏好某項目的使用者同時也偏好其他這些項目*。</span><span class="sxs-lookup"><span data-stu-id="1201c-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="1201c-121">接著 Mahout 會以偏好的類似項目判斷使用者，並以此做出推薦。</span><span class="sxs-lookup"><span data-stu-id="1201c-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="1201c-122">以下工作流程是一個使用電影資料的簡化範例：</span><span class="sxs-lookup"><span data-stu-id="1201c-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="1201c-123">**共生**：Joe、Alice 和 Bob 都喜歡*《星際大戰》*、*《帝國大反擊》*和*《絕地大反攻》*。</span><span class="sxs-lookup"><span data-stu-id="1201c-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="1201c-124">Mahout 將判斷喜歡上述任何一部電影的使用者，也會喜歡另外兩部電影。</span><span class="sxs-lookup"><span data-stu-id="1201c-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="1201c-125">**共生**：Bob 和 Alice 同時也喜歡*《威脅潛伏》*、*《複製人全面進攻》*和*《西斯大帝的復仇》*。</span><span class="sxs-lookup"><span data-stu-id="1201c-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="1201c-126">Mahout 將判斷喜歡前三部電影的使用者，也會喜歡這三部電影。</span><span class="sxs-lookup"><span data-stu-id="1201c-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="1201c-127">**相似性推薦**：因為 Joe 喜歡前三部電影，Mahout 會查看具有相似偏好的其他使用者所喜歡但 Joe 還沒看過 (喜歡/評價) 的電影。</span><span class="sxs-lookup"><span data-stu-id="1201c-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="1201c-128">在此情況下，Mahout 將會推薦*《威脅潛伏》*、*《複製人全面進攻》*和*《西斯大帝的復仇》*。</span><span class="sxs-lookup"><span data-stu-id="1201c-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="1201c-129">了解資料</span><span class="sxs-lookup"><span data-stu-id="1201c-129">Understanding the data</span></span>

<span data-ttu-id="1201c-130">[GroupLens 研究][movielens]提供 Mahout 相容格式的電影評價資料，相當方便。</span><span class="sxs-lookup"><span data-stu-id="1201c-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="1201c-131">您可在位於 `/HdiSamples/HdiSamples/MahoutMovieData`的叢集預設儲存體取得這份資料。</span><span class="sxs-lookup"><span data-stu-id="1201c-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="1201c-132">有兩個檔案 `moviedb.txt` 和 `user-ratings.txt`。</span><span class="sxs-lookup"><span data-stu-id="1201c-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="1201c-133">分析期間使用的是 user-ratings.txt 檔案，moviedb.txt 則是在顯示分析結果時用來提供使用者易懂的文字資訊。</span><span class="sxs-lookup"><span data-stu-id="1201c-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="1201c-134">user-ratings.txt 內包含的資料具有 `userID`、`movieID`、`userRating` 和 `timestamp` 結構，可告訴我們每位使用者對於影片的評價為何。</span><span class="sxs-lookup"><span data-stu-id="1201c-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="1201c-135">以下是資料範例：</span><span class="sxs-lookup"><span data-stu-id="1201c-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="1201c-136">執行分析</span><span class="sxs-lookup"><span data-stu-id="1201c-136">Run the analysis</span></span>

<span data-ttu-id="1201c-137">經由叢集的 SSH 連線，使用下列命令來執行推薦工作：</span><span class="sxs-lookup"><span data-stu-id="1201c-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="1201c-138">此工作可能需要幾分鐘的時間才能完成，並可能執行多項 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="1201c-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="1201c-139">檢視輸出</span><span class="sxs-lookup"><span data-stu-id="1201c-139">View the output</span></span>

1. <span data-ttu-id="1201c-140">工作完成後，使用以下命令來檢視所產生的輸出：</span><span class="sxs-lookup"><span data-stu-id="1201c-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="1201c-141">輸出看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="1201c-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="1201c-142">第一欄是 `userID`。</span><span class="sxs-lookup"><span data-stu-id="1201c-142">The first column is the `userID`.</span></span> <span data-ttu-id="1201c-143">'[' 和 ']' 中包含的值是 `movieId`:`recommendationScore`。</span><span class="sxs-lookup"><span data-stu-id="1201c-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="1201c-144">您可以使用輸出和 moviedb.txt，來顯示更多建議的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1201c-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="1201c-145">首先，我們需要使用下列命令將檔案複製到本機上︰</span><span class="sxs-lookup"><span data-stu-id="1201c-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="1201c-146">這個命令會將輸出資料和影片資料檔一起複製到目前目錄中名為 **recommendations.txt** 的檔案中。</span><span class="sxs-lookup"><span data-stu-id="1201c-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="1201c-147">使用下列命令來建立 Python 指令碼，該指令碼會在建議輸出資料中查閱影片名稱：</span><span class="sxs-lookup"><span data-stu-id="1201c-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="1201c-148">開啟編輯器時，請使用下列文字做為檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="1201c-148">When the editor opens, use the following text as the contents of the file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="1201c-149">按下 **CTRL-X**、**Y**，最後再按 **Enter** 鍵儲存資料。</span><span class="sxs-lookup"><span data-stu-id="1201c-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="1201c-150">執行 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1201c-150">Run the Python script.</span></span> <span data-ttu-id="1201c-151">以下命令假設您已在所有檔案的下載目錄中︰</span><span class="sxs-lookup"><span data-stu-id="1201c-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="1201c-152">此命令會查看為使用者 ID 4 所產生的建議。</span><span class="sxs-lookup"><span data-stu-id="1201c-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="1201c-153">**user-ratings.txt** 檔案可用來擷取已評分的影片。</span><span class="sxs-lookup"><span data-stu-id="1201c-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="1201c-154">**moviedb.txt** 檔案用來擷取影片名稱。</span><span class="sxs-lookup"><span data-stu-id="1201c-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="1201c-155">**recommendations.txt** 用來擷取這位使用者的電影建議。</span><span class="sxs-lookup"><span data-stu-id="1201c-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="1201c-156">此命令的輸出類似下列文字︰</span><span class="sxs-lookup"><span data-stu-id="1201c-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="1201c-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span><span class="sxs-lookup"><span data-stu-id="1201c-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="1201c-158">刪除暫存資料</span><span class="sxs-lookup"><span data-stu-id="1201c-158">Delete temporary data</span></span>

<span data-ttu-id="1201c-159">Mahout 工作不會移除處理工作時所建立的暫存資料。</span><span class="sxs-lookup"><span data-stu-id="1201c-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="1201c-160">範例工作中指定 `--tempDir` 參數將暫存檔隔離到特定路徑中以方便刪除。</span><span class="sxs-lookup"><span data-stu-id="1201c-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="1201c-161">若要移除暫存檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1201c-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="1201c-162">如果您要再次執行該命令，您必須也刪除輸出目錄。</span><span class="sxs-lookup"><span data-stu-id="1201c-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="1201c-163">使用以下命令刪除此目錄：</span><span class="sxs-lookup"><span data-stu-id="1201c-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="1201c-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1201c-164">Next steps</span></span>

<span data-ttu-id="1201c-165">您現在已了解如何使用 Mahout，請繼續探索在 HDInsight 上使用資料的其他方法：</span><span class="sxs-lookup"><span data-stu-id="1201c-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="1201c-166">搭配 HDInsight 使用 Hive</span><span class="sxs-lookup"><span data-stu-id="1201c-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1201c-167">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="1201c-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1201c-168">搭配 HDInsight 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="1201c-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
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
