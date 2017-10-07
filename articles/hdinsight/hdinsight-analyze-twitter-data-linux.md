---
title: "aaaAnalyze Twitter 資料與 Apache Hive-Azure HDInsight |Microsoft 文件"
description: "了解 toouse 使用 Hive 和 Hadoop 上 HDInsight tootransform 原始 TWitter 資料至可搜尋的 Hive 資料表。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1e249ed-5f57-40d6-b3bc-a1b4d9a871d3
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 02c4d027c7bbf390ac1c3724c14f8d549ea5195e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-and-hadoop-on-hdinsight"></a>在 HDInsight 上使用 Hive 與 Hadoop 分析 Twitter 資料

深入了解如何 toouse Apache Hive tooprocess Twitter 資料。 hello 結果是的 Twitter 使用者傳送嗨大部分推文包含特定單字的清單。

> [!IMPORTANT]
> 本文件中的 hello 步驟 HDInsight 3.6 上測試。
>
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="get-hello-data"></a>取得 hello 資料

Twitter 可讓您 tooretrieve hello[資料的每個推文](https://dev.twitter.com/docs/platform-objects/tweets)為 JavaScript 物件標記法 (JSON) 文件，透過 REST API。 [OAuth](http://oauth.net)需要驗證 toohello 應用程式開發介面。

### <a name="create-a-twitter-application"></a>建立 Twitter 應用程式

1. 從網頁瀏覽器登入太[https://apps.twitter.com/](https://apps.twitter.com/)。 按一下 hello**註冊現在**連結，如果您沒有 Twitter 帳戶。

2. 按一下 [建立新的應用程式] 。

3. 輸入 [名稱]、[說明]、[網站]。 您可以建立 hello 的 URL**網站**欄位。 hello 下表顯示一些範例值 toouse:

   | 欄位 | 值 |
   |:--- |:--- |
   | 名稱 |MyHDInsightApp |
   | 說明 |MyHDInsightApp |
   | 網站 |http://www.myhdinsightapp.com |

4. 核取 是，我同意 然後按一下建立 Twitter 應用程式。

5. 按一下 hello**權限** 索引標籤 hello 預設權限是**唯讀**。

6. 按一下 hello**機碼和存取權杖** 索引標籤。

7. 按一下 [Create my access token] 。

8. 按一下**測試 OAuth** hello 右上角的 hello 頁面中。

9. 記下**消費者金鑰**、**消費者祕密**、**存取權杖**和**存取權杖祕密**。

### <a name="download-tweets"></a>下載的推文

hello 下列 Python 程式碼會下載 10000 推文，從 Twitter 和儲存名為 tooa 檔案**tweets.txt**。

> [!NOTE]
> 因為已安裝 Python hello HDInsight 叢集，在執行步驟的 hello。

1. 連線使用 SSH toohello HDInsight 叢集：

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

3. 使用 hello 下列命令 tooinstall [Tweepy](http://www.tweepy.org/)， [Progressbar](https://pypi.python.org/pypi/progressbar/2.2)，和其他必要的套件：

   ```bash
   sudo apt install python-dev libffi-dev libssl-dev
   sudo apt remove python-openssl
   pip install virtualenv
   mkdir gettweets
   cd gettweets
   virtualenv gettweets
   source gettweets/bin/activate
   pip install tweepy progressbar pyOpenSSL requests[security]
   ```

4. 使用 hello 下列命令 toocreate 名為**gettweets.py**:

   ```bash
   nano gettweets.py
   ```

5. 使用 hello 文字之後做為 hello 內容的 hello **gettweets.py**檔案：

   ```python
   #!/usr/bin/python

   from tweepy import Stream, OAuthHandler
   from tweepy.streaming import StreamListener
   from progressbar import ProgressBar, Percentage, Bar
   import json
   import sys

   #Twitter app information
   consumer_secret='Your consumer secret'
   consumer_key='Your consumer key'
   access_token='Your access token'
   access_token_secret='Your access token secret'

   #hello number of tweets we want tooget
   max_tweets=10000

   #Create hello listener class that receives and saves tweets
   class listener(StreamListener):
       #On init, set hello counter toozero and create a progress bar
       def __init__(self, api=None):
           self.num_tweets = 0
           self.pbar = ProgressBar(widgets=[Percentage(), Bar()], maxval=max_tweets).start()

       #When data is received, do this
       def on_data(self, data):
           #Append hello tweet toohello 'tweets.txt' file
           with open('tweets.txt', 'a') as tweet_file:
               tweet_file.write(data)
               #Increment hello number of tweets
               self.num_tweets += 1
               #Check toosee if we have hit max_tweets and exit if so
               if self.num_tweets >= max_tweets:
                   self.pbar.finish()
                   sys.exit(0)
               else:
                   #increment hello progress bar
                   self.pbar.update(self.num_tweets)
           return True

       #Handle any errors that may occur
       def on_error(self, status):
           print status

   #Get hello OAuth token
   auth = OAuthHandler(consumer_key, consumer_secret)
   auth.set_access_token(access_token, access_token_secret)
   #Use hello listener class for stream processing
   twitterStream = Stream(auth, listener())
   #Filter for these topics
   twitterStream.filter(track=["azure","cloud","hdinsight"])
   ```

    > [!IMPORTANT]
    > Hello 預留位置文字取代為您的 twitter 應用程式中的下列項目與 hello 資訊的 hello:
    >
    > * `consumer_secret`
    > * `consumer_key`
    > * `access_token`
    > * `access_token_secret`

6. 使用**Ctrl + X**，然後**Y** toosave hello 檔案。

7. 使用下列命令 toorun hello 檔 hello 和下載推文：

    ```bash
    python gettweets.py
    ```

    進度指示器隨即出現。 它算是 too100 %hello 下載推文。

   > [!NOTE]
   > 如果花費 hello 進度列 tooadvance 很長的時間，您應該變更 hello 篩選 tootrack 趨勢主題。 在篩選中的 hello 主題相關的許多推文時，您可以快速取得 hello 需要 10000 推文。

### <a name="upload-hello-data"></a>上傳 hello 資料

tooupload hello 資料 tooHDInsight 儲存體，下列命令使用 hello:

   ```bash
   hdfs dfs -mkdir -p /tutorials/twitter/data
   hdfs dfs -put tweets.txt /tutorials/twitter/data/tweets.txt
```

這些命令會將 hello 資料儲存在 hello 叢集中的所有節點均可都存取的位置。

## <a name="run-hello-hiveql-job"></a>執行 hello HiveQL 工作

1. 使用下列命令 toocreate 檔案包含下列 HiveQL 陳述式的 hello:

   ```bash
   nano twitter.hql
   ```

    使用 hello hello hello 檔案內容為下列文字：

   ```hiveql
   set hive.exec.dynamic.partition = true;
   set hive.exec.dynamic.partition.mode = nonstrict;
   -- Drop table, if it exists
   DROP TABLE tweets_raw;
   -- Create it, pointing toward hello tweets logged from Twitter
   CREATE EXTERNAL TABLE tweets_raw (
       json_response STRING
   )
   STORED AS TEXTFILE LOCATION '/tutorials/twitter/data';
   -- Drop and recreate hello destination table
   DROP TABLE tweets;
   CREATE TABLE tweets
   (
       id BIGINT,
       created_at STRING,
       created_at_date STRING,
       created_at_year STRING,
       created_at_month STRING,
       created_at_day STRING,
       created_at_time STRING,
       in_reply_to_user_id_str STRING,
       text STRING,
       contributors STRING,
       retweeted STRING,
       truncated STRING,
       coordinates STRING,
       source STRING,
       retweet_count INT,
       url STRING,
       hashtags array<STRING>,
       user_mentions array<STRING>,
       first_hashtag STRING,
       first_user_mention STRING,
       screen_name STRING,
       name STRING,
       followers_count INT,
       listed_count INT,
       friends_count INT,
       lang STRING,
       user_location STRING,
       time_zone STRING,
       profile_image_url STRING,
       json_response STRING
   );
   -- Select tweets from hello imported data, parse hello JSON,
   -- and insert into hello tweets table
   FROM tweets_raw
   INSERT OVERWRITE TABLE tweets
   SELECT
       cast(get_json_object(json_response, '$.id_str') as BIGINT),
       get_json_object(json_response, '$.created_at'),
       concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
       substr (get_json_object(json_response, '$.created_at'),27,4)),
       substr (get_json_object(json_response, '$.created_at'),27,4),
       case substr (get_json_object(json_response,    '$.created_at'),5,3)
           when "Jan" then "01"
           when "Feb" then "02"
           when "Mar" then "03"
           when "Apr" then "04"
           when "May" then "05"
           when "Jun" then "06"
           when "Jul" then "07"
           when "Aug" then "08"
           when "Sep" then "09"
           when "Oct" then "10"
           when "Nov" then "11"
           when "Dec" then "12" end,
       substr (get_json_object(json_response, '$.created_at'),9,2),
       substr (get_json_object(json_response, '$.created_at'),12,8),
       get_json_object(json_response, '$.in_reply_to_user_id_str'),
       get_json_object(json_response, '$.text'),
       get_json_object(json_response, '$.contributors'),
       get_json_object(json_response, '$.retweeted'),
       get_json_object(json_response, '$.truncated'),
       get_json_object(json_response, '$.coordinates'),
       get_json_object(json_response, '$.source'),
       cast (get_json_object(json_response, '$.retweet_count') as INT),
       get_json_object(json_response, '$.entities.display_url'),
       array(
           trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
           trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
       array(
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
           trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
       trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
       trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
       get_json_object(json_response, '$.user.screen_name'),
       get_json_object(json_response, '$.user.name'),
       cast (get_json_object(json_response, '$.user.followers_count') as INT),
       cast (get_json_object(json_response, '$.user.listed_count') as INT),
       cast (get_json_object(json_response, '$.user.friends_count') as INT),
       get_json_object(json_response, '$.user.lang'),
       get_json_object(json_response, '$.user.location'),
       get_json_object(json_response, '$.user.time_zone'),
       get_json_object(json_response, '$.user.profile_image_url'),
       json_response
   WHERE (length(json_response) > 500);
   ```

2. 按下**Ctrl + X**，然後按下**Y** toosave hello 檔案。
3. 使用下列命令 toorun hello HiveQL hello 檔案中包含的 hello:

   ```bash
   beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i twitter.hql
   ```

    此命令執行 hello hello **twitter.hql**檔案。 Hello 查詢完成後，您會看到`jdbc:hive2//localhost:10001/>`提示字元。

4. 從 hello beeline 提示字元中，使用下列查詢 tooverify 資料已匯入的 hello:

   ```hiveql
   SELECT name, screen_name, count(1) as cc
       FROM tweets
       WHERE text like "%Azure%"
       GROUP BY name,screen_name
       ORDER BY cc DESC LIMIT 10;
   ```

    此查詢會傳回最多包含 hello 單字的 10 個推文**Azure** hello 訊息文字中。

## <a name="next-steps"></a>後續步驟

您已經學會如何 tootransform 至結構化的 Hive 資料表中的非結構化的 JSON 資料集。 深入了解 HDInsight 上的登錄區 toolearn，請參閱下列文件的 hello:

* [開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [使用 HDInsight 分析航班延誤資料](hdinsight-analyze-flight-delay-data-linux.md)

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter
