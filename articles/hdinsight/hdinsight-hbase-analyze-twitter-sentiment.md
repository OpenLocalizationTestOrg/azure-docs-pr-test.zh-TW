---
title: "使用 HBase-Azure aaaAnalyze 即時 Twitter 情緒 |Microsoft 文件"
description: "深入了解如何從 Twitter HDInsight (Hadoop) 叢集中使用 HBase 巨量資料 toodo 即時情緒分析。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5c798ad3-a20d-4385-a463-f4f7705f9566
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jgao
ms.openlocfilehash: 87e5c0c0a90d222a3f0bc3c3f3fce1e938320480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-real-time-twitter-sentiment-with-hbase-in-hdinsight"></a><span data-ttu-id="7b14b-103">使用 HDInsight 中的 HBase 分析即時的 Twitter 情感</span><span class="sxs-lookup"><span data-stu-id="7b14b-103">Analyze real-time Twitter sentiment with HBase in HDInsight</span></span>
<span data-ttu-id="7b14b-104">深入了解如何 toodo 即時[情緒分析](http://en.wikipedia.org/wiki/Sentiment_analysis)的巨量資料從 Twitter 利用 HDInsight HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b14b-104">Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data from Twitter by using a HBase cluster in HDInsight.</span></span>

<span data-ttu-id="7b14b-105">社交網站是其中一種 hello 主要推進巨量資料採用。</span><span class="sxs-lookup"><span data-stu-id="7b14b-105">Social websites are one of hello major driving forces for big data adoption.</span></span> <span data-ttu-id="7b14b-106">像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。</span><span class="sxs-lookup"><span data-stu-id="7b14b-106">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span> <span data-ttu-id="7b14b-107">在本教學課程中，您可以開發主控台串流服務應用程式和 ASP.NET web 應用程式 tooperform hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7b14b-107">In this tutorial, you develop a console streaming service application and an ASP.NET web application tooperform hello following:</span></span>

![HDInsight HBase Analyze Twitter sentiment][img-app-arch]

* <span data-ttu-id="7b14b-109">hello 串流處理應用程式</span><span class="sxs-lookup"><span data-stu-id="7b14b-109">hello streaming application</span></span>

  * <span data-ttu-id="7b14b-110">取得地理標記排行推文中使用 hello Twitter 即時串流應用程式開發介面嗎</span><span class="sxs-lookup"><span data-stu-id="7b14b-110">get geo-tagged tweets in real time by using hello Twitter streaming API</span></span>
  * <span data-ttu-id="7b14b-111">評估 hello 人氣的這些推文</span><span class="sxs-lookup"><span data-stu-id="7b14b-111">evaluate hello sentiment of these tweets</span></span>
  * <span data-ttu-id="7b14b-112">儲存對 HBase 中的資訊使用 hello Microsoft HBase SDK hello 人氣</span><span class="sxs-lookup"><span data-stu-id="7b14b-112">store hello sentiment information in HBase by using hello Microsoft HBase SDK</span></span>
* <span data-ttu-id="7b14b-113">hello Azure 網站應用程式</span><span class="sxs-lookup"><span data-stu-id="7b14b-113">hello Azure Websites application</span></span>

  * <span data-ttu-id="7b14b-114">使用 ASP.NET web 應用程式中繪製 hello 即時統計的結果上 Bing 地圖服務。</span><span class="sxs-lookup"><span data-stu-id="7b14b-114">plot hello real-time statistical results on Bing maps by using an ASP.NET web application.</span></span> <span data-ttu-id="7b14b-115">Hello 推文的視覺效果是類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="7b14b-115">A visualization of hello tweets is similar toohello following screenshot:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]

    <span data-ttu-id="7b14b-117">如果您不能 tooquery 推文與特定關鍵字 tooget 的 hello 推文中的 hello 表示意見是正數、 負數或中性。</span><span class="sxs-lookup"><span data-stu-id="7b14b-117">You are able tooquery tweets with certain keywords tooget a sense of if hello expressed opinion in hello tweets is positive, negative, or neutral.</span></span>

<span data-ttu-id="7b14b-118">如需完整的 Visual Studio 方案範例，請前往 GitHub： [即時社交情感分析應用程式](https://github.com/maxluk/tweet-sentiment)。</span><span class="sxs-lookup"><span data-stu-id="7b14b-118">A complete Visual Studio solution sample can be found on GitHub: [Realtime social sentiment analysis app](https://github.com/maxluk/tweet-sentiment).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7b14b-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b14b-119">Prerequisites</span></span>
<span data-ttu-id="7b14b-120">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7b14b-120">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="7b14b-121">**HDInsight 中的 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-121">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="7b14b-122">如需有關建立叢集的指示，請參閱[開始在 HDInsight 中搭配使用 HBase 與 Hadoop][hbase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-122">For instructions about creating clusters, see  [Get started using HBase with Hadoop in HDInsight][hbase-get-started].</span></span> 

* <span data-ttu-id="7b14b-123">安裝 Visual Studio 2013/2015/2017 的**工作站**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-123">**A workstation** with Visual Studio 2013/2015/2017 installed.</span></span> <span data-ttu-id="7b14b-124">如需指示，請參閱 [安裝 Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7b14b-124">For instructions, see [Installing Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).</span></span>

## <a name="create-a-twitter-application-id-and-secrets"></a><span data-ttu-id="7b14b-125">建立 Twitter 應用程式 ID 和密碼</span><span class="sxs-lookup"><span data-stu-id="7b14b-125">Create a Twitter application ID and secrets</span></span>
<span data-ttu-id="7b14b-126">資料流 Api 使用的 Twitter hello [OAuth](http://oauth.net/) tooauthorize 要求。</span><span class="sxs-lookup"><span data-stu-id="7b14b-126">hello Twitter streaming APIs use [OAuth](http://oauth.net/) tooauthorize requests.</span></span> <span data-ttu-id="7b14b-127">第一個步驟 toouse hello OAuth 是 toocreate hello Twitter 開發人員網站上的新應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b14b-127">hello first step toouse OAuth is toocreate a new application on hello Twitter developer site.</span></span>

<span data-ttu-id="7b14b-128">**toocreate Twitter 應用程式識別碼和密碼**</span><span class="sxs-lookup"><span data-stu-id="7b14b-128">**toocreate Twitter application ID and secrets**</span></span>

1. <span data-ttu-id="7b14b-129">登入太[Twitter 應用程式](https://apps.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="7b14b-129">Sign in too[Twitter Apps](https://apps.twitter.com/).</span></span> <span data-ttu-id="7b14b-130">按一下 hello**立即註冊**連結，如果您沒有 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b14b-130">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="7b14b-131">按一下 [建立新的應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="7b14b-131">Click **Create New App**.</span></span>
3. <span data-ttu-id="7b14b-132">輸入 [名稱]、[描述] 和 [網站]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-132">Enter a **Name**, **Description**, and **Website**.</span></span> <span data-ttu-id="7b14b-133">hello Twitter 應用程式名稱必須是唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="7b14b-133">hello Twitter application name must be a unique name.</span></span> <span data-ttu-id="7b14b-134">hello 網站欄位不是真的用。</span><span class="sxs-lookup"><span data-stu-id="7b14b-134">hello Website field is not really used.</span></span> <span data-ttu-id="7b14b-135">不是有效的 URL 一定 toobe。</span><span class="sxs-lookup"><span data-stu-id="7b14b-135">It doesn't have toobe a valid URL.</span></span>
4. <span data-ttu-id="7b14b-136">核取 是，我同意 然後按一下建立 Twitter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b14b-136">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="7b14b-137">按一下 hello**權限**索引標籤，然後再按一下**唯讀**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-137">Click hello **Permissions** tab, and then click **Read only**.</span></span> <span data-ttu-id="7b14b-138">hello 唯讀權限不足，本教學課程。</span><span class="sxs-lookup"><span data-stu-id="7b14b-138">hello read-only permission is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="7b14b-139">按一下 hello**機碼和存取權杖** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7b14b-139">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="7b14b-140">按一下**建立我的存取權杖**上 hello hello 頁面的底部。</span><span class="sxs-lookup"><span data-stu-id="7b14b-140">Click **Create my access token** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="7b14b-141">複製 hello**取用者金鑰 （應用程式開發介面）**，**取用者密碼 （應用程式開發介面機密）**，**存取權杖**，和**存取語彙基元秘**值。</span><span class="sxs-lookup"><span data-stu-id="7b14b-141">Copy hello **Consumer Key (API Key)**, **Consumer Secret (API Secret)**, **Access token**, and **Access token secret** values.</span></span> <span data-ttu-id="7b14b-142">您稍後在 hello 教學課程需要這些值。</span><span class="sxs-lookup"><span data-stu-id="7b14b-142">You need these values later in hello tutorial.</span></span>

    > <span data-ttu-id="7b14b-143">![注意] hello 測試 OAuth 按鈕無法再運作。</span><span class="sxs-lookup"><span data-stu-id="7b14b-143">![NOTE] hello Test OAuth button does not work anymore.</span></span>

## <a name="create-twitter-streaming-service"></a><span data-ttu-id="7b14b-144">建立 Twitter 串流服務</span><span class="sxs-lookup"><span data-stu-id="7b14b-144">Create Twitter streaming service</span></span>
<span data-ttu-id="7b14b-145">您需要的 toocreate 應用程式 tooget 推文，計算推文人氣分數，並傳送嗨處理推文字 tooHBase。</span><span class="sxs-lookup"><span data-stu-id="7b14b-145">You need toocreate an application tooget tweets, calculate tweet sentiment score, and send hello processed tweet words tooHBase.</span></span>

<span data-ttu-id="7b14b-146">**toocreate hello 串流處理應用程式**</span><span class="sxs-lookup"><span data-stu-id="7b14b-146">**toocreate hello streaming application**</span></span>

1. <span data-ttu-id="7b14b-147">開啟 **Visual Studio**，建立名為 **TweetSentimentStreaming** 的 Visual C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b14b-147">Open **Visual Studio**, and create a Visual C# console application called **TweetSentimentStreaming**.</span></span>
2. <span data-ttu-id="7b14b-148">從**Package Manager Console**，請執行 hello 以下命令：</span><span class="sxs-lookup"><span data-stu-id="7b14b-148">From **Package Manager Console**, run hello following commands:</span></span>

        Install-Package Microsoft.HBase.Client -version 0.4.2.0
        Install-Package TweetinviAPI -version 1.0.0.0

    <span data-ttu-id="7b14b-149">這些命令會安裝 hello [HBase.NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/)套件 hello 用戶端程式庫 tooaccess hello HBase 叢集，且 hello [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/)封裝，也就是使用的 tooaccess hello Twitter API。</span><span class="sxs-lookup"><span data-stu-id="7b14b-149">These commands install hello [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is hello client library tooaccess hello HBase cluster, and hello [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/) package, which is used tooaccess hello Twitter API.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7b14b-150">在本文中使用的 hello 範例使用上述指定的 hello 版本已經過測試。</span><span class="sxs-lookup"><span data-stu-id="7b14b-150">hello sample used in this article has been tested using hello version specified above.</span></span>  <span data-ttu-id="7b14b-151">您可以移除 hello-版本交換器 tooinstall hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="7b14b-151">You can remove hello -version switch tooinstall hello latest version.</span></span>
   >
   >
3. <span data-ttu-id="7b14b-152">從**方案總管 中**，新增**System.Configuration** toohello 參考。</span><span class="sxs-lookup"><span data-stu-id="7b14b-152">From **Solution Explorer**, add **System.Configuration** toohello reference.</span></span>
4. <span data-ttu-id="7b14b-153">加入新的類別檔案 toohello 專案呼叫**HBaseWriter.cs**，然後將 hello 程式碼取代 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7b14b-153">Add a new class file toohello project called **HBaseWriter.cs**, and then replace hello code with hello following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling;
        using org.apache.hadoop.hbase.rest.protobuf.generated;
        using Microsoft.HBase.Client;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class HBaseWriter
            {
                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "https://<Enter Your Cluster Name>.azurehdinsight.net/";
                const string HADOOPUSERNAME = "admin"; //hello default name is "admin"
                const string HADOOPUSERPASSWORD = "<Enter hello Hadoop User Password>";

                const string HBASETABLENAME = "tweets_by_words";
                const string COUNT_ROW_KEY = "~ROWCOUNT";
                const string COUNT_COLUMN_NAME = "d:COUNT";

                long rowCount = 0;

                // Sentiment dictionary file and hello punctuation characters
                const string DICTIONARYFILENAME = @"..\..\dictionary.tsv";
                private static char[] _punctuationChars = new[] {
            ' ', '!', '\"', '#', '$', '%', '&', '\'', '(', ')', '*', '+', ',', '-', '.', '/',   //ascii 23--47
            ':', ';', '<', '=', '>', '?', '@', '[', ']', '^', '_', '`', '{', '|', '}', '~' };   //ascii 58--64 + misc.

                // For writting tooHBase
                HBaseClient client;

                // a sentiment dictionary for estimate sentiment. It is loaded from a physical file.
                Dictionary<string, DictionaryItem> dictionary;

                // use multithread write
                Thread writerThread;
                Queue<ITweet> queue = new Queue<ITweet>();
                bool threadRunning = true;

                // This function connects tooHBase, loads hello sentiment dictionary, and starts hello thread for writting.
                public HBaseWriter()
                {
                    ClusterCredentials credentials = new ClusterCredentials(new Uri(CLUSTERNAME), HADOOPUSERNAME, HADOOPUSERPASSWORD);
                    client = new HBaseClient(credentials);

                    // create hello HBase table if it doesn't exist
                    if (!client.ListTablesAsync().Result.name.Contains(HBASETABLENAME))
                    {
                        TableSchema tableSchema = new TableSchema();
                        tableSchema.name = HBASETABLENAME;
                        tableSchema.columns.Add(new ColumnSchema { name = "d" });
                        client.CreateTableAsync(tableSchema).Wait();
                        Console.WriteLine("Table \"{0}\" is created.", HBASETABLENAME);
                    }

                    // Read current row count cell
                    rowCount = GetRowCount();

                    // Load sentiment dictionary from a file
                    LoadDictionary();

                    // Start a thread for writting tooHBase
                    writerThread = new Thread(new ThreadStart(WriterThreadFunction));
                    writerThread.Start();
                }

                ~HBaseWriter()
                {
                    threadRunning = false;
                }

                private long GetRowCount()
                {
                    try
                    {
                        RequestOptions options = RequestOptions.GetDefaultOptions();
                        options.RetryPolicy = RetryPolicy.NoRetry;
                        var cellSet = client.GetCellsAsync(HBASETABLENAME, COUNT_ROW_KEY, null, null, options).Result;
                        if (cellSet.rows.Count != 0)
                        {
                            var countCol = cellSet.rows[0].values.Find(cell => Encoding.UTF8.GetString(cell.column) == COUNT_COLUMN_NAME);
                            if (countCol != null)
                            {
                                return Convert.ToInt64(Encoding.UTF8.GetString(countCol.data));
                            }
                        }
                    }
                    catch(Exception ex)
                    {
                        if (ex.InnerException.Message.Equals("hello remote server returned an error: (404) Not Found.", StringComparison.OrdinalIgnoreCase))
                        {
                            return 0;
                        }
                        else
                        {
                            throw ex;
                        }

                    }

                    return 0;
                }

                // Enqueue hello Tweets received
                public void WriteTweet(ITweet tweet)
                {
                    lock (queue)
                    {
                        queue.Enqueue(tweet);
                    }
                }

                // Load sentiment dictionary from a file
                private void LoadDictionary()
                {
                    List<string> lines = File.ReadAllLines(DICTIONARYFILENAME).ToList();
                    var items = lines.Select(line =>
                    {
                        var fields = line.Split('\t');
                        var pos = 0;
                        return new DictionaryItem
                        {
                            Type = fields[pos++],
                            Length = Convert.ToInt32(fields[pos++]),
                            Word = fields[pos++],
                            Pos = fields[pos++],
                            Stemmed = fields[pos++],
                            Polarity = fields[pos++]
                        };
                    });

                    dictionary = new Dictionary<string, DictionaryItem>();
                    foreach (var item in items)
                    {
                        if (!dictionary.Keys.Contains(item.Word))
                        {
                            dictionary.Add(item.Word, item);
                        }
                    }
                }

                // Calculate sentiment score
                private int CalcSentimentScore(string[] words)
                {
                    Int32 total = 0;
                    foreach (string word in words)
                    {
                        if (dictionary.Keys.Contains(word))
                        {
                            switch (dictionary[word].Polarity)
                            {
                                case "negative": total -= 1; break;
                                case "positive": total += 1; break;
                            }
                        }
                    }
                    if (total > 0)
                    {
                        return 1;
                    }
                    else if (total < 0)
                    {
                        return -1;
                    }
                    else
                    {
                        return 0;
                    }
                }

                // Popular a CellSet object toobe written into HBase
                private void CreateTweetByWordsCells(CellSet set, ITweet tweet)
                {
                    // Split hello Tweet into words
                    string[] words = tweet.Text.ToLower().Split(_punctuationChars);

                    // Calculate sentiment score base on hello words
                    int sentimentScore = CalcSentimentScore(words);
                    var word_pairs = words.Take(words.Length - 1)
                                        .Select((word, idx) => string.Format("{0} {1}", word, words[idx + 1]));
                    var all_words = words.Concat(word_pairs).ToList();

                    // For each word in hello Tweet add a row toohello HBase table
                    foreach (string word in all_words)
                    {
                        string time_index = (ulong.MaxValue - (ulong)tweet.CreatedAt.ToBinary()).ToString().PadLeft(20) + tweet.IdStr;
                        string key = word + "_" + time_index;

                        // Create a row
                        var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };

                        // Add columns toohello row, including Tweet identifier, language, coordinator(if available), and sentiment
                        var value = new Cell { column = Encoding.UTF8.GetBytes("d:id_str"), data = Encoding.UTF8.GetBytes(tweet.IdStr) };
                        row.values.Add(value);

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:lang"), data = Encoding.UTF8.GetBytes(tweet.Language.ToString()) };
                        row.values.Add(value);

                        if (tweet.Coordinates != null)
                        {
                            var str = tweet.Coordinates.Longitude.ToString() + "," + tweet.Coordinates.Latitude.ToString();
                            value = new Cell { column = Encoding.UTF8.GetBytes("d:coor"), data = Encoding.UTF8.GetBytes(str) };
                            row.values.Add(value);
                        }

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:sentiment"), data = Encoding.UTF8.GetBytes(sentimentScore.ToString()) };
                        row.values.Add(value);

                        set.rows.Add(row);
                    }
                }

                // Write a Tweet (CellSet) tooHBase
                public void WriterThreadFunction()
                {
                    try
                    {
                        while (threadRunning)
                        {
                            if (queue.Count > 0)
                            {
                                CellSet set = new CellSet();
                                lock (queue)
                                {
                                    do
                                    {
                                        ITweet tweet = queue.Dequeue();
                                        CreateTweetByWordsCells(set, tweet);
                                    } while (queue.Count > 0);
                                }

                                // Write hello Tweet by words cell set toohello HBase table
                                client.StoreCellsAsync(HBASETABLENAME, set).Wait();
                                Console.WriteLine("\tRows written: {0}", set.rows.Count);
                            }
                            Thread.Sleep(100);
                        }
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine("Exception: " + ex.Message);
                    }
                }
            }
            public class DictionaryItem
            {
                public string Type { get; set; }
                public int Length { get; set; }
                public string Word { get; set; }
                public string Pos { get; set; }
                public string Stemmed { get; set; }
                public string Polarity { get; set; }
            }
        }
5. <span data-ttu-id="7b14b-154">設定 hello 常數 hello 先前的程式碼，包括**CLUSTERNAME**， **HADOOPUSERNAME**， **HADOOPUSERPASSWORD**，和 DICTIONARYFILENAME。</span><span class="sxs-lookup"><span data-stu-id="7b14b-154">Set hello constants in hello previous code, including **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**, and DICTIONARYFILENAME.</span></span> <span data-ttu-id="7b14b-155">hello DICTIONARYFILENAME 是 hello 檔名和 hello direction.tsv hello 位置。</span><span class="sxs-lookup"><span data-stu-id="7b14b-155">hello DICTIONARYFILENAME is hello filename and hello location of hello direction.tsv.</span></span>  <span data-ttu-id="7b14b-156">您可以從下載 hello 檔案**https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-156">hello file can be downloaded from **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**.</span></span> <span data-ttu-id="7b14b-157">如果您想 toochange hello HBase 資料表名稱時，您必須據此變更 hello hello web 應用程式中的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="7b14b-157">If you want toochange hello HBase table name, you must change hello table name in hello web application accordingly.</span></span>
6. <span data-ttu-id="7b14b-158">開啟**Program.cs**，並取代 hello 下列中的 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="7b14b-158">Open **Program.cs**, and replace hello code with hello following:</span></span>

        using System;
        using System.Diagnostics;
        using Tweetinvi;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class Program
            {
                const string TWITTERAPPACCESSTOKEN = "<Enter Twitter App Access Token>";
                const string TWITTERAPPACCESSTOKENSECRET = "<Enter Twitter Access Token Secret>";
                const string TWITTERAPPAPIKEY = "<Enter Twitter App API Key>";
                const string TWITTERAPPAPISECRET = "<Enter Twitter App API Secret>";

                static void Main(string[] args)
                {
                    Auth.SetUserCredentials(TWITTERAPPAPIKEY, TWITTERAPPAPISECRET, TWITTERAPPACCESSTOKEN, TWITTERAPPACCESSTOKENSECRET);

                    Stream_FilteredStreamExample();
                }

                private static void Stream_FilteredStreamExample()
                {
                    for (;;)
                    {
                        try
                        {
                            HBaseWriter hbase = new HBaseWriter();
                            var stream = Stream.CreateFilteredStream();
                            stream.AddLocation(new Coordinates(90, -180), new Coordinates(-90,180));

                            var tweetCount = 0;
                            var timer = Stopwatch.StartNew();

                            stream.MatchingTweetReceived += (sender, args) =>
                            {
                                tweetCount++;
                                var tweet = args.Tweet;

                                // Write Tweets tooHBase
                                hbase.WriteTweet(tweet);

                                if (timer.ElapsedMilliseconds > 1000)
                                {
                                    if (tweet.Coordinates != null)
                                    {
                                        Console.ForegroundColor = ConsoleColor.Green;
                                        Console.WriteLine("\n{0}: {1} {2}", tweet.Id, tweet.Language.ToString(), tweet.Text);
                                        Console.ForegroundColor = ConsoleColor.White;
                                        Console.WriteLine("\tLocation: {0}, {1}", tweet.Coordinates.Longitude, tweet.Coordinates.Latitude);
                                    }

                                    timer.Restart();
                                    Console.WriteLine("\tTweets/sec: {0}", tweetCount);
                                    tweetCount = 0;
                                }
                            };

                            stream.StartStreamMatchingAllConditions();
                        }
                        catch (Exception ex)
                        {
                            Console.WriteLine("Exception: {0}", ex.Message);
                        }
                    }
                }

            }
        }
7. <span data-ttu-id="7b14b-159">設定包括 hello 常數**TWITTERAPPACCESSTOKEN**， **TWITTERAPPACCESSTOKENSECRET**， **TWITTERAPPAPIKEY**和**TWITTERAPPAPISECRET**.</span><span class="sxs-lookup"><span data-stu-id="7b14b-159">Set hello constants including **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** and **TWITTERAPPAPISECRET**.</span></span>

<span data-ttu-id="7b14b-160">串流服務，請按 toorun hello **F5**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-160">toorun hello streaming service, press **F5**.</span></span> <span data-ttu-id="7b14b-161">hello 下面是 hello 主控台應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="7b14b-161">hello following is a screenshot of hello console application:</span></span>

![hdinsight.hbase.twitter.sentiment.streaming.service][img-streaming-service]

<span data-ttu-id="7b14b-163">保留 hello 串流處理您開發 hello web 應用程式，因此您需要更多資料 toouse 時執行的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b14b-163">Keep hello streaming console application running while you develop hello web application, so you have more data toouse.</span></span> <span data-ttu-id="7b14b-164">tooexamine hello 資料插入至 hello 資料表，您可以使用 HBase 殼層。</span><span class="sxs-lookup"><span data-stu-id="7b14b-164">tooexamine hello data inserted into hello table, you can use HBase Shell.</span></span> <span data-ttu-id="7b14b-165">請參閱 [開始在 HDInsight 中使用 HBase](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data)。</span><span class="sxs-lookup"><span data-stu-id="7b14b-165">See [Get started with HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data).</span></span>

## <a name="visualize-real-time-sentiment"></a><span data-ttu-id="7b14b-166">將即時情感視覺化</span><span class="sxs-lookup"><span data-stu-id="7b14b-166">Visualize real-time sentiment</span></span>
<span data-ttu-id="7b14b-167">在本節中，您可以建立 ASP.NET MVC web 應用程式 tooread hello 即時的人氣資料從 Bing 地圖服務上的 HBase 和繪圖 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7b14b-167">In this section, you create an ASP.NET MVC web application tooread hello real-time sentiment data from HBase and plot hello data on Bing maps.</span></span>

<span data-ttu-id="7b14b-168">**toocreate ASP.NET MVC Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="7b14b-168">**toocreate an ASP.NET MVC Web application**</span></span>

1. <span data-ttu-id="7b14b-169">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7b14b-169">Open Visual Studio.</span></span>
2. <span data-ttu-id="7b14b-170">依序按一下 [檔案]、[新增] 及 [專案]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-170">Click **File**, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="7b14b-171">輸入下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b14b-171">Enter hello following information:</span></span>

   * <span data-ttu-id="7b14b-172">範本類別： **Visual C#/Web**</span><span class="sxs-lookup"><span data-stu-id="7b14b-172">Template category: **Visual C#/Web**</span></span>
   * <span data-ttu-id="7b14b-173">範本： **ASP.NET Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="7b14b-173">Template: **ASP.NET Web Application**</span></span>
   * <span data-ttu-id="7b14b-174">名稱： **TweetSentimentWeb**</span><span class="sxs-lookup"><span data-stu-id="7b14b-174">Name: **TweetSentimentWeb**</span></span>
   * <span data-ttu-id="7b14b-175">位置：**C:\Tutorials**</span><span class="sxs-lookup"><span data-stu-id="7b14b-175">Location: **C:\Tutorials**</span></span>
4. <span data-ttu-id="7b14b-176">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7b14b-176">Click **OK**.</span></span>
5. <span data-ttu-id="7b14b-177">在 [選取範本] 中按一下 **MVC**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-177">In **Select a template**, click **MVC**.</span></span>
6. <span data-ttu-id="7b14b-178">在 [Microsoft Azure] 中按一下 [管理訂用帳戶]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-178">In **Microsoft Azure**, click **Manage Subscriptions**.</span></span>
7. <span data-ttu-id="7b14b-179">在 [管理 Microsoft Azure 訂用帳戶] 中按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-179">From **Manage Microsoft Azure Subscriptions**, click **Sign in**.</span></span>
8. <span data-ttu-id="7b14b-180">輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="7b14b-180">Enter your Azure credentials.</span></span> <span data-ttu-id="7b14b-181">您的 Azure 訂用帳戶資訊會顯示在 hello**帳戶** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7b14b-181">Your Azure subscription information is shown on hello **Accounts** tab.</span></span>
9. <span data-ttu-id="7b14b-182">按一下**關閉**tooclose hello**管理 Microsoft Azure 訂用帳戶**視窗。</span><span class="sxs-lookup"><span data-stu-id="7b14b-182">Click **Close** tooclose hello **Manage Microsoft Azure Subscriptions** window.</span></span>
10. <span data-ttu-id="7b14b-183">在 [新增 ASP.NET 專案 - TweetSentimentWeb] 中按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-183">From **New ASP.NET Project - TweetSentimentWeb**, click **OK**.</span></span>
11. <span data-ttu-id="7b14b-184">從**設定 Microsoft Azure 站台設定**，選取 hello**區域**也就是最接近 tooyou。</span><span class="sxs-lookup"><span data-stu-id="7b14b-184">From **Configure Microsoft Azure Site Settings**, select hello **Region** that is closest tooyou.</span></span> <span data-ttu-id="7b14b-185">您不需要 toospecify 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="7b14b-185">You don't need toospecify a database server.</span></span>
12. <span data-ttu-id="7b14b-186">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7b14b-186">Click **OK**.</span></span>

<span data-ttu-id="7b14b-187">**tooinstall NuGet 封裝**</span><span class="sxs-lookup"><span data-stu-id="7b14b-187">**tooinstall NuGet packages**</span></span>

1. <span data-ttu-id="7b14b-188">從 hello**工具**功能表上，按一下  **Nuget 套件管理員**，然後按一下 **Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-188">From hello **Tools** menu, click **Nuget Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="7b14b-189">hello 主控台面板會開啟在 hello hello 頁面底部。</span><span class="sxs-lookup"><span data-stu-id="7b14b-189">hello console panel is opened at hello bottom of hello page.</span></span>
2. <span data-ttu-id="7b14b-190">使用 hello 下列命令 tooinstall hello [HBase.NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/)套件，也就是 hello 用戶端程式庫 tooaccess HBase 叢集：</span><span class="sxs-lookup"><span data-stu-id="7b14b-190">Use hello following command tooinstall hello [HBase .NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) package, which is hello client library tooaccess HBase cluster:</span></span>

        Install-Package Microsoft.HBase.Client

<span data-ttu-id="7b14b-191">**tooadd HBaseReader 類別**</span><span class="sxs-lookup"><span data-stu-id="7b14b-191">**tooadd HBaseReader class**</span></span>

1. <span data-ttu-id="7b14b-192">在 [方案總管] 中展開 **TweetSentiment**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-192">From **Solution Explorer**, expand **TweetSentiment**.</span></span>
2. <span data-ttu-id="7b14b-193">以滑鼠右鍵按一下 [模型]，然後依序按一下 [新增] 和 [類別]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-193">Right-click **Models**, click **Add**, and then click **Class**.</span></span>
3. <span data-ttu-id="7b14b-194">在 hello**名稱**欄位中，輸入**HBaseReader.cs**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-194">In hello **Name** field, type **HBaseReader.cs**, and then click **Add**.</span></span>
4. <span data-ttu-id="7b14b-195">Hello 程式碼取代 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7b14b-195">Replace hello code with hello following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Web;

        using System.Configuration;
        using System.Threading.Tasks;
        using System.Text;
        using Microsoft.HBase.Client;
        using org.apache.hadoop.hbase.rest.protobuf.generated;

        namespace TweetSentimentWeb.Models
        {
            public class HBaseReader
            {
                // For reading Tweet sentiment data from HDInsight HBase
                HBaseClient client;

                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "<HBaseClusterName>";
                const string HADOOPUSERNAME = "<HBaseClusterHadoopUserName>"
                const string HADOOPUSERPASSWORD = "<HBaseCluserUserPassword>";
                const string HBASETABLENAME = "tweets_by_words";

                // hello constructor
                public HBaseReader()
                {
                    ClusterCredentials creds = new ClusterCredentials(
                                    new Uri(CLUSTERNAME),
                                    HADOOPUSERNAME,
                                    HADOOPUSERPASSWORD);
                    client = new HBaseClient(creds);
                }

                // Query Tweets sentiment data from hello HBase table asynchronously
                public async Task<IEnumerable<Tweet>> QueryTweetsByKeywordAsync(string keyword)
                {
                    List<Tweet> list = new List<Tweet>();

                    // Demonstrate Filtering hello data from hello past 6 hours hello row key
                    string timeIndex = (ulong.MaxValue -
                        (ulong)DateTime.UtcNow.Subtract(new TimeSpan(6, 0, 0)).ToBinary()).ToString().PadLeft(20);
                    string startRow = keyword + "_" + timeIndex;
                    string endRow = keyword + "|";
                    Scanner scanSettings = new Scanner
                    {
                        batch = 100000,
                        startRow = Encoding.UTF8.GetBytes(startRow),
                        endRow = Encoding.UTF8.GetBytes(endRow)
                    };

                    // Make async scan call
                    ScannerInformation scannerInfo =
                        await client.CreateScannerAsync(HBASETABLENAME, scanSettings);

                    CellSet next;

                    while ((next = await client.ScannerGetNextAsync(scannerInfo)) != null)
                    {
                        foreach (CellSet.Row row in next.rows)
                        {
                            // find hello cell with string pattern "d:coor"
                            var coordinates =
                                row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:coor");

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');

                                var sentimentField =
                                    row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:sentiment");
                                Int32 sentiment = 0;
                                if (sentimentField != null)
                                {
                                    sentiment = Convert.ToInt32(Encoding.UTF8.GetString(sentimentField.data));
                                }

                                list.Add(new Tweet
                                {
                                    Longtitude = Convert.ToDouble(lonlat[0]),
                                    Latitude = Convert.ToDouble(lonlat[1]),
                                    Sentiment = sentiment
                                });
                            }

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');
                            }
                        }
                    }

                    return list;
                }
            }

            public class Tweet
            {
                public string IdStr { get; set; }
                public string Text { get; set; }
                public string Lang { get; set; }
                public double Longtitude { get; set; }
                public double Latitude { get; set; }
                public int Sentiment { get; set; }
            }
        }
5. <span data-ttu-id="7b14b-196">內部 hello **HBaseReader**類別中，變更 hello 常數值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b14b-196">Inside hello **HBaseReader** class, change hello constant values as follows:</span></span>

   * <span data-ttu-id="7b14b-197">**CLUSTERNAME**: hello HBase 叢集名稱，例如*https://<HBaseClusterName>.azurehdinsight.net/*。</span><span class="sxs-lookup"><span data-stu-id="7b14b-197">**CLUSTERNAME**: hello HBase cluster name, for example, *https://<HBaseClusterName>.azurehdinsight.net/*.</span></span>
   * <span data-ttu-id="7b14b-198">**HADOOPUSERNAME**: hello HBase 叢集 Hadoop 使用者使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="7b14b-198">**HADOOPUSERNAME**: hello HBase cluster Hadoop user user name.</span></span> <span data-ttu-id="7b14b-199">hello 預設名稱是*admin*。</span><span class="sxs-lookup"><span data-stu-id="7b14b-199">hello default name is *admin*.</span></span>
   * <span data-ttu-id="7b14b-200">**HADOOPUSERPASSWORD**: hello HBase 叢集的 Hadoop 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="7b14b-200">**HADOOPUSERPASSWORD**: hello HBase cluster Hadoop user password.</span></span>
   * <span data-ttu-id="7b14b-201">**HBASETABLENAME** = "tweets_by_words";</span><span class="sxs-lookup"><span data-stu-id="7b14b-201">**HBASETABLENAME** = "tweets_by_words";</span></span>

     <span data-ttu-id="7b14b-202">hello HBase 資料表名稱是**"tweets_by_words";**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-202">hello HBase table name is **"tweets_by_words";**.</span></span> <span data-ttu-id="7b14b-203">hello 值必須符合您傳送 hello 串流服務，以便 hello web 應用程式，讀取 hello hello hello 數值相同 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="7b14b-203">hello values must match hello values you sent in hello streaming service, so that hello web application reads hello data from hello same HBase table.</span></span>

<span data-ttu-id="7b14b-204">**tooadd TweetsController 控制器**</span><span class="sxs-lookup"><span data-stu-id="7b14b-204">**tooadd TweetsController controller**</span></span>

1. <span data-ttu-id="7b14b-205">在 [方案總管] 中展開 **TweetSentimentWeb**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-205">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="7b14b-206">以滑鼠右鍵按一下 [控制器]，然後依序按一下 [新增] 和 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-206">Right-click **Controllers**, click **Add**, and then click **Controller**.</span></span>
3. <span data-ttu-id="7b14b-207">按一下 **Web API 2 Controller - Empty**，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="7b14b-207">Click **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
4. <span data-ttu-id="7b14b-208">在 hello**控制器名稱**欄位中，輸入**TweetsController**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-208">In hello **Controller name** field, type **TweetsController**, and then click **Add**.</span></span>
5. <span data-ttu-id="7b14b-209">從**方案總管 中**，按兩下 TweetsController.cs tooopen hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b14b-209">From **Solution Explorer**, double-click TweetsController.cs tooopen hello file.</span></span>
6. <span data-ttu-id="7b14b-210">修改 hello 檔案，讓它看起來類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7b14b-210">Modify hello file, so it looks like hello following:</span></span>

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;

        using System.Threading.Tasks;
        using TweetSentimentWeb.Models;

        namespace TweetSentimentWeb.Controllers
        {
            public class TweetsController : ApiController
            {
                HBaseReader hbase = new HBaseReader();

                public async Task<IEnumerable<Tweet>> GetTweetsByQuery(string query)
                {
                    return await hbase.QueryTweetsByKeywordAsync(query);
                }
            }
        }

<span data-ttu-id="7b14b-211">**tooadd heatmap.js**</span><span class="sxs-lookup"><span data-stu-id="7b14b-211">**tooadd heatmap.js**</span></span>

1. <span data-ttu-id="7b14b-212">在 [方案總管] 中展開 **TweetSentimentWeb**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-212">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="7b14b-213">以滑鼠右鍵按一下 [指令碼]，然後依序按一下 [新增] 和 [JavaScript 檔案]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-213">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="7b14b-214">在 hello**項目名稱**欄位中，輸入**heatmap.js**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-214">In hello **Item name** field, type **heatmap.js**.</span></span>
4. <span data-ttu-id="7b14b-215">貼上下列程式碼到 hello 檔案 hello。</span><span class="sxs-lookup"><span data-stu-id="7b14b-215">Paste hello following code into hello file.</span></span> <span data-ttu-id="7b14b-216">Alastair Aitchison 寫入 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7b14b-216">hello code was written by Alastair Aitchison.</span></span> <span data-ttu-id="7b14b-217">如需詳細資訊，請參閱 [BBing 地圖 AJAX v7 HeatMap 程式庫](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/)。</span><span class="sxs-lookup"><span data-stu-id="7b14b-217">For more information, see [Bing Maps AJAX v7 HeatMap Library](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/).</span></span>

        /*******************************************************************************
        * Author: Alastair Aitchison
        * Website: http://alastaira.wordpress.com
        * Date: 15th April 2011
        *
        * Description:
        * This JavaScript file provides an algorithm that can be used tooadd a heatmap
        * overlay on a Bing Maps v7 control. hello intensity and temperature palette
        * of hello heatmap are designed toobe easily customisable.
        *
        * Requirements:
        * hello heatmap layer itself is created dynamically on hello client-side using
        * hello HTML5 &lt;canvas> element, and therefore requires a browser that supports
        * this element. It has been tested on IE9, Firefox 3.6/4 and
        * Chrome 10 browsers. If you can confirm whether it works on other browsers or
        * not, I'd love toohear from you!
        *
        * Usage:
        * hello HeatMapLayer constructor requires:
        * - A reference tooa map object
        * - An array or Microsoft.Maps.Location items
        * - Optional parameters toocustomise hello appearance of hello layer
        *  (Radius,, Unit, Intensity, and ColourGradient), and a callback function
        */

        var HeatMapLayer = function (map, locations, options) {

            /* Private Properties */
            var _map = map,
                _canvas,
                _temperaturemap,
                _locations = [],
                _viewchangestarthandler,
                _viewchangeendhandler;

            // Set default options
            var _options = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 1000,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'meters',

                // Colour temperature gradient of hello map
                colourgradient: {
                    "0.00": 'rgba(255,0,255,20)',  // Magenta
                    "0.25": 'rgba(0,0,255,40)',    // Blue
                    "0.50": 'rgba(0,255,0,80)',    // Green
                    "0.75": 'rgba(255,255,0,120)', // Yellow
                    "1.00": 'rgba(255,0,0,150)'    // Red
                },

                // Callback function toobe fired after heatmap layer has been redrawn
                callback: null
            };

            /* Private Methods */
            function _init() {
                var _mapDiv = _map.getRootElement();

                if (_mapDiv.childNodes.length >= 3 && _mapDiv.childNodes[2].childNodes.length >= 2) {
                    // Create hello canvas element
                    _canvas = document.createElement('canvas');
                    _canvas.style.position = 'relative';

                    var container = document.createElement('div');
                    container.style.position = 'absolute';
                    container.style.left = '0px';
                    container.style.top = '0px';
                    container.appendChild(_canvas);

                    _mapDiv.childNodes[2].childNodes[1].appendChild(container);

                    // Override defaults with any options passed in hello constructor
                    _setOptions(options);

                    // Load array of location data
                    _setPoints(locations);

                    // Create a colour gradient from hello suppied colourstops
                    _temperaturemap = _createColourGradient(_options.colourgradient);

                    // Wire up hello event handler tooredraw heatmap canvas
                    _viewchangestarthandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangestart', _clearHeatMap);
                    _viewchangeendhandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangeend', _createHeatMap);

                    _createHeatMap();

                    delete _init;
                } else {
                    setTimeout(_init, 100);
                }
            }

            // Resets hello heat map
            function _clearHeatMap() {
                var ctx = _canvas.getContext("2d");
                ctx.clearRect(0, 0, _canvas.width, _canvas.height);
            }

            // Creates a colour gradient from supplied colour stops on initialisation
            function _createColourGradient(colourstops) {
                var ctx = document.createElement('canvas').getContext('2d');
                var grd = ctx.createLinearGradient(0, 0, 256, 0);
                for (var c in colourstops) {
                    grd.addColorStop(c, colourstops[c]);
                }
                ctx.fillStyle = grd;
                ctx.fillRect(0, 0, 256, 1);
                return ctx.getImageData(0, 0, 256, 1).data;
            }

            // Applies a colour gradient toohello intensity map
            function _colouriseHeatMap() {
                var ctx = _canvas.getContext("2d");
                var dat = ctx.getImageData(0, 0, _canvas.width, _canvas.height);
                var pix = dat.data; // pix is a CanvasPixelArray containing height x width x 4 bytes of data (RGBA)
                for (var p = 0, len = pix.length; p < len;) {
                    var a = pix[p + 3] * 4; // get hello alpha of this pixel
                    if (a != 0) { // If there is any data tooplot
                        pix[p] = _temperaturemap[a]; // set hello red value of hello gradient that corresponds toothis alpha
                        pix[p + 1] = _temperaturemap[a + 1]; //set hello green value based on alpha
                        pix[p + 2] = _temperaturemap[a + 2]; //set hello blue value based on alpha
                    }
                    p += 4; // Move on toohello next pixel
                }
                ctx.putImageData(dat, 0, 0);
            }

            // Sets any options passed in
            function _setOptions(options) {
                for (attrname in options) {
                    _options[attrname] = options[attrname];
                }
            }

            // Sets hello heatmap points from an array of Microsoft.Maps.Locations  
            function _setPoints(locations) {
                _locations = locations;
            }

            // Main method toodraw hello heatmap
            function _createHeatMap() {
                // Ensure hello canvas matches hello current dimensions of hello map
                // This also has hello effect of resetting hello canvas
                _canvas.height = _map.getHeight();
                _canvas.width = _map.getWidth();

                _canvas.style.top = -_canvas.height / 2 + 'px';
                _canvas.style.left = -_canvas.width / 2 + 'px';

                // Calculate hello pixel radius of each heatpoint at hello current map zoom
                if (_options.unit == "pixels") {
                    radiusInPixel = _options.radius;
                } else {
                    radiusInPixel = _options.radius / _map.getMetersPerPixel();
                }

                var ctx = _canvas.getContext("2d");

                // Convert lat/long toopixel location
                var pixlocs = _map.tryLocationToPixel(_locations, Microsoft.Maps.PixelReference.control);
                var shadow = 'rgba(0, 0, 0, ' + _options.intensity + ')';
                var mapWidth = 256 * Math.pow(2, _map.getZoom());

                // Create hello Intensity Map by looping through each location
                for (var i = 0, len = pixlocs.length; i < len; i++) {
                    var x = pixlocs[i].x;
                    var y = pixlocs[i].y;

                    if (x < 0) {
                        x += mapWidth * Math.ceil(Math.abs(x / mapWidth));
                    }

                    // Create radial gradient centred on this point
                    var grd = ctx.createRadialGradient(x, y, 0, x, y, radiusInPixel);
                    grd.addColorStop(0.0, shadow);
                    grd.addColorStop(1.0, 'transparent');

                    // Draw hello heatpoint onto hello canvas
                    ctx.fillStyle = grd;
                    ctx.fillRect(x - radiusInPixel, y - radiusInPixel, 2 * radiusInPixel, 2 * radiusInPixel);
                }

                // Apply hello specified colour gradient toohello intensity map
                _colouriseHeatMap();

                // Call hello callback function, if specified
                if (_options.callback) {
                    _options.callback();
                }
            }

            /* Public Methods */

            this.Show = function () {
                if (_canvas) {
                    _canvas.style.display = '';
                }
            };

            this.Hide = function () {
                if (_canvas) {
                    _canvas.style.display = 'none';
                }
            };

            // Sets options for intensity, radius, colourgradient etc.
            this.SetOptions = function (options) {
                _setOptions(options);
            }

            // Sets an array of Microsoft.Maps.Locations from which hello heatmap is created
            this.SetPoints = function (locations) {
                // Reset hello existing heatmap layer
                _clearHeatMap();
                // Pass in hello new set of locations
                _setPoints(locations);
                // Recreate hello layer
                _createHeatMap();
            }

            // Removes hello heatmap layer from hello DOM
            this.Remove = function () {
                _canvas.parentNode.parentNode.removeChild(_canvas.parentNode);

                if (_viewchangestarthandler) { Microsoft.Maps.Events.removeHandler(_viewchangestarthandler); }
                if (_viewchangeendhandler) { Microsoft.Maps.Events.removeHandler(_viewchangeendhandler); }

                _locations = null;
                _temperaturemap = null;
                _canvas = null;
                _options = null;
                _viewchangestarthandler = null;
                _viewchangeendhandler = null;
            }

            // Call hello initialisation routine
            _init();
        };

        // Call hello Module Loaded method
        Microsoft.Maps.moduleLoaded('HeatMapModule');

<span data-ttu-id="7b14b-218">**tooadd twitterStream.js**</span><span class="sxs-lookup"><span data-stu-id="7b14b-218">**tooadd twitterStream.js**</span></span>

1. <span data-ttu-id="7b14b-219">在 [方案總管] 中展開 **TweetSentimentWeb**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-219">From **Solution Explorer**, expand **TweetSentimentWeb**.</span></span>
2. <span data-ttu-id="7b14b-220">以滑鼠右鍵按一下 [指令碼]，然後依序按一下 [新增] 和 [JavaScript 檔案]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-220">Right-click **Scripts**, click **Add**, click **JavaScript File**.</span></span>
3. <span data-ttu-id="7b14b-221">在 hello**項目名稱**欄位中，輸入**twitterStream.js**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-221">In hello **Item name** field, type**twitterStream.js**.</span></span>
4. <span data-ttu-id="7b14b-222">複製並貼上下列程式碼到 hello 檔案 hello:</span><span class="sxs-lookup"><span data-stu-id="7b14b-222">Copy and paste hello following code into hello file:</span></span>

        var liveTweetsPos = [];
        var liveTweets = [];
        var liveTweetsNeg = [];
        var map;
        var heatmap;
        var heatmapNeg;
        var heatmapPos;

        function initialize() {
            // Initialize hello map
            var options = {
                credentials: "AvFJTZPZv8l3gF8VC3Y7BPBd0r7LKo8dqKG02EAlqg9WAi0M7la6zSIT-HwkMQbx",
                center: new Microsoft.Maps.Location(23.0, 8.0),
                mapTypeId: Microsoft.Maps.MapTypeId.ordnanceSurvey,
                labelOverlay: Microsoft.Maps.LabelOverlay.hidden,
                zoom: 2.5
            };
            var map = new Microsoft.Maps.Map(document.getElementById('map_canvas'), options);

            // Heatmap options for positive, neutral and negative layers

            var heatmapOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels'
            };

            var heatmapPosOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 255, 191, 1)',
                    0.3: 'rgba(0, 255, 127, 1)',
                    0.4: 'rgba(0, 255, 63, 1)',
                    0.5: 'rgba(0, 127, 0, 1)',
                    0.7: 'rgba(0, 159, 0, 1)',
                    0.8: 'rgba(0, 191, 0, 1)',
                    0.9: 'rgba(0, 223, 0, 1)',
                    1.0: 'rgba(0, 255, 0, 1)'
                }
            };

            var heatmapNegOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 191, 255, 1)',
                    0.3: 'rgba(0, 127, 255, 1)',
                    0.4: 'rgba(0, 63, 255, 1)',
                    0.5: 'rgba(0, 0, 127, 1)',
                    0.7: 'rgba(0, 0, 159, 1)',
                    0.8: 'rgba(0, 0, 191, 1)',
                    0.9: 'rgba(0, 0, 223, 1)',
                    1.0: 'rgba(0, 0, 255, 1)'
                }
            };

            // Register and load hello Client Side HeatMap Module
            Microsoft.Maps.registerModule("HeatMapModule", "scripts/heatmap.js");
            Microsoft.Maps.loadModule("HeatMapModule", {
                callback: function () {
                    // Create heatmap layers for positive, neutral and negative tweets
                    heatmapPos = new HeatMapLayer(map, liveTweetsPos, heatmapPosOptions);
                    heatmap = new HeatMapLayer(map, liveTweets, heatmapOptions);
                    heatmapNeg = new HeatMapLayer(map, liveTweetsNeg, heatmapNegOptions);
                }
            });

            $("#searchbox").val("xbox");
            $("#searchBtn").click(onsearch);
            $("#positiveBtn").click(onPositiveBtn);
            $("#negativeBtn").click(onNegativeBtn);
            $("#neutralBtn").click(onNeutralBtn);
            $("#neutralBtn").button("toggle");
        }

        function onsearch() {
            var uri = 'api/tweets?query=';
            var query = $('#searchbox').val();
            $.getJSON(uri + query)
                .done(function (data) {
                    liveTweetsPos = [];
                    liveTweets = [];
                    liveTweetsNeg = [];

                    // On success, 'data' contains a list of tweets.
                    $.each(data, function (key, item) {
                        addTweet(item);
                    });

                    if (!$("#neutralBtn").hasClass('active')) {
                        $("#neutralBtn").button("toggle");
                    }
                    onNeutralBtn();
                })
                .fail(function (jqXHR, textStatus, err) {
                    $('#statustext').text('Error: ' + err);
                });
        }

        function addTweet(item) {
            //Add tweet toohello heat map arrays.
            var tweetLocation = new Microsoft.Maps.Location(item.Latitude, item.Longtitude);
            if (item.Sentiment > 0) {
                liveTweetsPos.push(tweetLocation);
            } else if (item.Sentiment < 0) {
                liveTweetsNeg.push(tweetLocation);
            } else {
                liveTweets.push(tweetLocation);
            }
        }

        function onPositiveBtn() {
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmapPos.SetPoints(liveTweetsPos);
            heatmapPos.Show();
            heatmapNeg.Hide();
            heatmap.Hide();

            $('#statustext').text('Tweets: ' + liveTweetsPos.length + "   " + getPosNegRatio());
        }

        function onNeutralBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmap.SetPoints(liveTweets);
            heatmap.Show();
            heatmapNeg.Hide();
            heatmapPos.Hide();

            $('#statustext').text('Tweets: ' + liveTweets.length + "   " + getPosNegRatio());
        }

        function onNegativeBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }

            heatmapNeg.SetPoints(liveTweetsNeg);
            heatmapNeg.Show();
            heatmap.Hide();;
            heatmapPos.Hide();;

            $('#statustext').text('Tweets: ' + liveTweetsNeg.length + "\t" + getPosNegRatio());
        }

        function getPosNegRatio() {
            if (liveTweetsNeg.length == 0) {
                return "";
            }
            else {
                var ratio = liveTweetsPos.length / liveTweetsNeg.length;
                var str = parseFloat(Math.round(ratio * 10) / 10).toFixed(1);
                return "Positive/Negative Ratio: " + str;
            }
        }

<span data-ttu-id="7b14b-223">**toomodify hello layout.cshtml**</span><span class="sxs-lookup"><span data-stu-id="7b14b-223">**toomodify hello layout.cshtml**</span></span>

1. <span data-ttu-id="7b14b-224">在 [方案總管] 中，依序展開 **TweetSentimentWeb**、**Views** 及 **Shared**，然後按兩下 _**Layout.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-224">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Shared**, and then double-click _**Layout.cshtml**.</span></span>
2. <span data-ttu-id="7b14b-225">取代 hello 下列 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="7b14b-225">Replace hello content with hello following:</span></span>

        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>@ViewBag.Title</title>
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
            <!-- Bing Maps -->
            <script type="text/javascript" src="http://ecn.dev.virtualearth.net/mapcontrol/mapcontrol.ashx?v=7.0&mkt=en-gb"></script>
            <!-- Spatial Dashboard JavaScript -->
            <script src="~/Scripts/twitterStream.js" type="text/javascript"></script>
        </head>
        <body onload="initialize()">
            <div class="navbar navbar-inverse navbar-fixed-top">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                    </div>
                    <div class="navbar-collapse collapse">
                        <div class="row">
                            <ul class="nav navbar-nav col-lg-5">
                                <li class="col-lg-12">
                                    <div class="navbar-form">
                                        <input id="searchbox" type="search" class="form-control">
                                        <button type="button" id="searchBtn" class="btn btn-primary">Go</button>
                                    </div>
                                </li>
                            </ul>
                            <ul class="nav navbar-nav col-lg-7">
                                <li>
                                    <div class="navbar-form">
                                        <div class="btn-group" data-toggle="buttons-radio">
                                            <button type="button" id="positiveBtn" class="btn btn-primary">Positive</button>
                                            <button type="button" id="neutralBtn" class="btn btn-primary">Neutral</button>
                                            <button type="button" id="negativeBtn" class="btn btn-primary">Negative</button>
                                        </div>
                                    </div>
                                </li>
                                <li><span id="statustext" class="navbar-text"></span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            <div class="map_container">
                @RenderBody()
            </div>
            @Scripts.Render("~/bundles/jquery")
            @Scripts.Render("~/bundles/bootstrap")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="7b14b-226">**toomodify hello Index.cshtml**</span><span class="sxs-lookup"><span data-stu-id="7b14b-226">**toomodify hello Index.cshtml**</span></span>

1. <span data-ttu-id="7b14b-227">在 [方案總管] 中，依序展開 **TweetSentimentWeb**、**Views** 及 **Home**，然後按兩下 **Index.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-227">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Views**, expand **Home**, and then double-click **Index.cshtml**.</span></span>
2. <span data-ttu-id="7b14b-228">取代 hello 下列 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="7b14b-228">Replace hello content with hello following:</span></span>

        @{
            ViewBag.Title = "Tweet Sentiment";
        }

        <div class="map_container">
            <div id="map_canvas"/>
        </div>

<span data-ttu-id="7b14b-229">**toomodify hello site.css 檔案**</span><span class="sxs-lookup"><span data-stu-id="7b14b-229">**toomodify hello site.css file**</span></span>

1. <span data-ttu-id="7b14b-230">在 [方案總管] 中，依序展開 **TweetSentimentWeb** 和 **Content**，然後按兩下 **Site.css**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-230">From **Solution Explorer**, expand **TweetSentimentWeb**, expand **Content**, and then double-click **Site.css**.</span></span>
2. <span data-ttu-id="7b14b-231">加入下列程式碼 toohello 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="7b14b-231">Append hello following code toohello file:</span></span>

        /* make container, and thus map, 100% width */
        .map_container {
            width: 100%;
            height: 100%;
        }

        #map_canvas{
          height:100%;
        }

        #tweets{
          position: absolute;
          top: 60px;
          left: 75px;
          z-index:1000;
          font-size: 30px;
        }

<span data-ttu-id="7b14b-232">**toomodify hello global.asax 檔案**</span><span class="sxs-lookup"><span data-stu-id="7b14b-232">**toomodify hello global.asax file**</span></span>

1. <span data-ttu-id="7b14b-233">在 [方案總管] 中展開 **TweetSentimentWeb**，然後按兩下 **Global.asax**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-233">From **Solution Explorer**, expand **TweetSentimentWeb**, and then double-click **Global.asax**.</span></span>
2. <span data-ttu-id="7b14b-234">新增下列 hello**使用**陳述式：</span><span class="sxs-lookup"><span data-stu-id="7b14b-234">Add hello following **using** statement:</span></span>

        using System.Web.Http;
3. <span data-ttu-id="7b14b-235">加入下列行內 hello hello **application_start （)**函式：</span><span class="sxs-lookup"><span data-stu-id="7b14b-235">Add hello following lines inside hello **Application_Start()** function:</span></span>

        // Register API routes
        GlobalConfiguration.Configure(WebApiConfig.Register);

    <span data-ttu-id="7b14b-236">修改 hello hello API 路由 toomake hello Web API 控制器工作 hello MVC 應用程式內註冊。</span><span class="sxs-lookup"><span data-stu-id="7b14b-236">Modify hello registration of hello API routes toomake hello Web API controller work inside hello MVC application.</span></span>

<span data-ttu-id="7b14b-237">**toorun hello web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="7b14b-237">**toorun hello web application**</span></span>

1. <span data-ttu-id="7b14b-238">請確認該 hello 串流服務主控台應用程式仍在執行，才可看到 hello 的即時變更。</span><span class="sxs-lookup"><span data-stu-id="7b14b-238">Verify that hello streaming service console application is still running so you can see hello real-time changes.</span></span>
2. <span data-ttu-id="7b14b-239">按**F5** toorun hello web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="7b14b-239">Press **F5** toorun hello web application:</span></span>

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]
3. <span data-ttu-id="7b14b-241">在 [hello] 文字方塊中，輸入關鍵字，然後按一下**移**。</span><span class="sxs-lookup"><span data-stu-id="7b14b-241">In hello text box, enter a keyword, and then click **Go**.</span></span>  <span data-ttu-id="7b14b-242">收集 hello HBase 資料表中的 hello 資料，根據某些關鍵字可能會找不到。</span><span class="sxs-lookup"><span data-stu-id="7b14b-242">Depending on hello data collected in hello HBase table, some keywords might not be found.</span></span> <span data-ttu-id="7b14b-243">請嘗試一些常用的關鍵字，例如 "love"、"xbox" 和 "playstation"。</span><span class="sxs-lookup"><span data-stu-id="7b14b-243">Try some common keywords, such as "love," "xbox," and "playstation."</span></span>
4. <span data-ttu-id="7b14b-244">之間切換**正數**，**中性**，和**負數**toocompare hello 主旨的人氣。</span><span class="sxs-lookup"><span data-stu-id="7b14b-244">Toggle among **Positive**, **Neutral**, and **Negative** toocompare sentiment on hello subject.</span></span>
5. <span data-ttu-id="7b14b-245">讓 hello 串流服務，請執行另一個小時，，然後搜尋 hello 相同的關鍵字，並比較 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7b14b-245">Let hello streaming service run for another hour, and then search hello same keywords, and compare hello results.</span></span>

<span data-ttu-id="7b14b-246">（選擇性） 您可以部署 hello 應用程式 tooAzure 網站。</span><span class="sxs-lookup"><span data-stu-id="7b14b-246">Optionally, you can deploy hello application tooAzure Websites.</span></span> <span data-ttu-id="7b14b-247">如需指示，請參閱[開始使用 Azure 網站和 ASP.NET][website-get-started]。</span><span class="sxs-lookup"><span data-stu-id="7b14b-247">For instructions, see [Get started with Azure Websites and ASP.NET][website-get-started].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b14b-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b14b-248">Next Steps</span></span>
<span data-ttu-id="7b14b-249">在本教學課程中，您學到如何 tooget 推文、 分析推文，儲存 hello 人氣資料 tooHBase，並顯示 hello 即時 Twitter 情緒資料 tooBing 對應的 hello 人氣。</span><span class="sxs-lookup"><span data-stu-id="7b14b-249">In this tutorial, you learned how tooget tweets, analyze hello sentiment of tweets, save hello sentiment data tooHBase, and present hello real-time Twitter sentiment data tooBing maps.</span></span> <span data-ttu-id="7b14b-250">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="7b14b-250">toolearn more, see:</span></span>

* <span data-ttu-id="7b14b-251">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7b14b-251">[Get started with HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="7b14b-252">在 HDInsight 中設定 HBase 複寫</span><span class="sxs-lookup"><span data-stu-id="7b14b-252">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* <span data-ttu-id="7b14b-253">[在 HDInsight 中使用 Hadoop 分析 Twitter 資料][hdinsight-analyze-twitter-data]</span><span class="sxs-lookup"><span data-stu-id="7b14b-253">[Analyze Twitter data with Hadoop in HDInsight][hdinsight-analyze-twitter-data]</span></span>
* <span data-ttu-id="7b14b-254">[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="7b14b-254">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="7b14b-255">[開發 HDInsight 的 Java MapReduce 程式][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="7b14b-255">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[website-get-started]: ../app-service-web/app-service-web-get-started-dotnet.md



[img-app-arch]: ./media/hdinsight-hbase-analyze-twitter-sentiment/AppArchitecture.png
[img-twitter-app]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterApp.png
[img-streaming-service]: ./media/hdinsight-hbase-analyze-twitter-sentiment/StreamingService.png
[img-bing-map]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterSentimentBingMap.png



[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-analyze-twitter-data]: hdinsight-analyze-twitter-data.md




[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
