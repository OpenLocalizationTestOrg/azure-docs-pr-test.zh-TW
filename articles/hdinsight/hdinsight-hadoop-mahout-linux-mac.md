---
title: "使用砲象兵和 HDInsight (SSH)-Azure aaaGenerate 建議 |Microsoft 文件"
description: "了解如何 toouse hello Apache 砲象兵機器學習服務文件庫 toogenerate 影片建議與 HDInsight (Hadoop)。"
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
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>在 HDInsight 中搭配使用 Apache Mahout 和以 Linux 為基礎的 Hadoop 來產生電影推薦 (SSH)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

深入了解如何 toouse hello [Apache 砲象兵](http://mahout.apache.org)Azure HDInsight toogenerate 影片建議的機器學習程式庫。

Mahout 是 Apache Hadoop 的[機器學習服務][ml]程式庫。 Mahout 包含可處理資料的演算法，例如篩選、分類和叢集化。 在本文中，您可以使用建議引擎 toogenerate 影片建議過您的朋友的電影為基礎的。

## <a name="prerequisites"></a>必要條件

* 以 Linux 為基礎的 HDInsight 叢集。 如需有關建立叢集的資訊，請參閱[開始在 HDInsight 中使用以 Linux 為基礎的 Hadoop][getstarted]。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* SSH 用戶端。 如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

## <a name="mahout-versioning"></a>Mahout 版本控制

更多的砲象兵 HDInsight 中的 hello 版本的詳細資訊，請參閱[HDInsight 版本和 Hadoop 元件](hdinsight-component-versioning.md)。

## <a name="recommendations"></a>了解推薦

建議引擎所提供的砲象兵 hello 函式的其中一個。 此引擎會接受資料格式的 hello `userID`， `itemId`，和`prefValue`(hello hello 項目喜好設定)。 砲象兵接著就可以執行共同分析 toodetermine:*使用者擁有的喜好設定項目也有這些喜好設定的其他項目*。 砲象兵接著會判斷使用者與類似項目參考，它可以是使用的 toomake 建議。

hello 下列工作流程是使用電影資料的簡化的範例：

* **共同**: Joe、 Alice 和所有按讚的 Bob*星狀戰爭*，*回 Empire 攻擊 hello*，和*傳回 hello Jedi*。 砲象兵決定使用者類似任何這些影片像 hello 其他兩個。

* **共同**: Bob 和 Alice 也喜歡*hello 虛設項目威脅*， *hello 複製程式碼的攻擊*，和*的 hello Sith 復仇*。 砲象兵決定使用者喜歡 hello 先前的三個影片也喜歡這些三個影片。

* **相似度建議**： 因為 Joe 喜歡 hello 前三個影片、 砲象兵查看電影的其他項目具有相似的偏好喜歡，但 Joe 不保存 （喜歡/評等）。 砲象兵在此情況下，建議*hello 虛設項目威脅*， *hello 複製程式碼的攻擊*，和*的 hello Sith 復仇*。

### <a name="understanding-hello-data"></a>了解 hello 資料

[GroupLens 研究][movielens]提供 Mahout 相容格式的電影評價資料，相當方便。 您可在位於 `/HdiSamples/HdiSamples/MahoutMovieData`的叢集預設儲存體取得這份資料。

有兩個檔案 `moviedb.txt` 和 `user-ratings.txt`。 在分析期間，使用 hello 使用者 ratings.txt 檔案，而 moviedb.txt 顯示 hello hello 分析結果時，使用的 tooprovide 使用者易記文字資訊。

hello 使用者 ratings.txt 中包含的資料都有一個結構的`userID`， `movieID`， `userRating`，和`timestamp`，它會告訴我們每位使用者如何高評等為電影。 Hello 資料的範例如下：

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>執行 hello 分析

從 SSH 連線 toohello 叢集中，使用下列命令 toorun hello 建議工作 hello:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> hello 作業可能需要幾分鐘的時間 toocomplete，並可能會執行多個 MapReduce 作業。

## <a name="view-hello-output"></a>檢視 hello 輸出

1. Hello 作業完成之後，請使用下列命令 tooview hello 產生輸出的 hello:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    hello 輸出會出現，如下所示：

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    hello 第一個資料行是 hello `userID`。 hello 中包含的值 '[' 和']' 是`movieId`:`recommendationScore`。

2. 您可以於 hello 建議使用 hello 輸出，以及 hello moviedb.txt，tooprovide 的詳細資訊。 首先，我們需要在本機上使用下列命令的 hello toocopy hello 檔案：

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    此命令複製 hello 輸出資料 tooa 檔名為**recommendations.txt** hello 目前目錄，連同 hello 電影資料檔案中。

3. 使用下列命令 toocreate 查閱 hello 建議輸出中的 hello 資料的電影名稱的 Python 指令碼的 hello:

    ```bash
    nano show_recommendations.py
    ```

    當 hello 編輯器開啟時，使用 hello hello hello 檔案內容為下列文字：

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

    按**Ctrl X**， **Y**，最後再**Enter** toosave hello 資料。

4. 執行 hello Python 指令碼。 hello 下列命令假設您已下載的所有 hello 檔案 hello 目錄中：

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    此命令會在產生的使用者識別碼 4 hello 建議。

    * hello**使用者 ratings.txt**檔案是使用的 tooretrieve 電影已評等。

    * hello **moviedb.txt**檔案是使用的 tooretrieve hello hello 電影名稱。

    * hello **recommendations.txt**是使用的 tooretrieve hello 影片建議，此使用者。

     hello 輸出此命令為類似 toohello 下列文字：

        Tibet (1997)，在七個年份分數 = 5.0 印第安納州 Jones 和 hello 最後聖戰 (1989)，分數 = 5.0 Jaws (1975)，分數 = 5.0 意義上與 Sensibility (1995 年) 分數 = 5.0 獨立性天 (ID4) (1996 年) 分數 = 5.0 我最好的朋友婚禮 (1997)，分數 = 5.0 Jerry Maguire (1996年)，分數 = 5.0 Scream 2 (1997 年) 分數 = 5.0 時間 tooKill，(1996 年) 分數 = 5.0

## <a name="delete-temporary-data"></a>刪除暫存資料

砲象兵作業不會移除處理 hello 作業時建立的暫存資料。 hello `--tempDir` hello 範例作業 tooisolate hello 暫存檔中指定參數為輕鬆刪除一個特定路徑。 tooremove hello 暫存檔案，請使用下列命令的 hello:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> 若要再次 toorun hello 命令，您也必須刪除 hello 輸出目錄。 使用下列 toodelete hello 這個目錄：
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>後續步驟

既然您已經學會如何 toouse 砲象兵，探索 HDInsight 上的資料搭配使用的其他方式：

* [搭配 HDInsight 使用 Hive](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [搭配 HDInsight 使用 MapReduce](hdinsight-use-mapreduce.md)

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
