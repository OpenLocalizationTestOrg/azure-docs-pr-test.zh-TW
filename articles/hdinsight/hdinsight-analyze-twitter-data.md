---
title: "aaaAnalyze HDInsight 的 Azure 中的 Hadoop Twitter 資料 |Microsoft 文件"
description: "了解如何 toouse Hive tooanalyze Twitter 中的資料在 Hadoop 上 HDInsight toofind hello 特定單字的使用頻率。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>在 HDInsight 中使用 Hive 分析 Twitter 資料
社交網站是其中一種 hello 主要推進巨量資料採用。 像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。
在本教學課程中，您將使用 Twitter，串流處理應用程式開發介面，以取得推文，然後再使用 Azure HDInsight tooget 的 Twitter 使用者傳送嗨大部分推文包含特定的字詞清單中的 Apache hive 控制檔。

> [!IMPORTANT]
> hello 本文件中的步驟需要 Windows 為基礎的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 針對步驟特定 tooa linux 叢集，請參閱[分析 Twitter 資料使用 HDInsight (Linux) 中的登錄區](hdinsight-analyze-twitter-data-linux.md)。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **工作站** 。

    tooexecute Windows PowerShell 指令碼，您必須以系統管理員身分執行 Azure PowerShell 並 hello 執行原則設定太*RemoteSigned*。 請參閱[執行 Windows PowerShell 指令碼][powershell-script]。

    再執行 Windows PowerShell 指令碼，請確定您已連接的 tooyour Azure 訂用帳戶使用下列 cmdlet 的 hello:

    ```powershell
    Login-AzureRmAccount
    ```

    如果您有多個 Azure 訂用帳戶，請使用下列 cmdlet tooset hello 目前訂用帳戶的 hello:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > 使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。 此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。
    >
    > 請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。 如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。

* **Azure HDInsight 叢集**。 如需叢集佈建的指示，請參閱[開始使用 HDInsight][hdinsight-get-started] 或[佈建 HDInsight 叢集][hdinsight-provision]。 您必須在 hello 教學課程後面 hello 叢集名稱。

hello 下表列出本教學課程所用的 hello 檔案：

| 檔案 | 說明 |
| --- | --- |
| /tutorials/twitter/data/tweets.txt |hello hello Hive 工作的來源資料。 |
| /tutorials/twitter/output |hello hello Hive 工作的輸出資料夾。 hello 預設 Hive 工作輸出檔案名稱是**000000_0**。 |
| tutorials/twitter/twitter.hql |hello 下列 HiveQL 指令碼檔案。 |
| /tutorials/twitter/jobstatus |hello Hadoop 工作的狀態。 |

## <a name="get-twitter-feed"></a>取得 Twitter 摘要
在此教學課程中，您將使用 hello [Twitter 資料流 Api][twitter-streaming-api]。 hello 串流處理應用程式開發介面，您將使用的特定 Twitter 是[狀態/篩選][twitter-statuses-filter]。

> [!NOTE]
> 公用 Blob 容器中已上傳一個包含 10000 推文和 hello Hive 指令碼檔案 （涵蓋在 hello 下一節） 檔案。 如果您想要 toouse hello 上傳檔案，則可以略過本節。

[資料推文](https://dev.twitter.com/docs/platform-objects/tweets)會儲存在 hello JavaScript Object Notation (JSON) 格式，其中包含複雜的巢狀的結構。 您可以不要使用慣用的程式設計語言撰寫多行程式碼，而將此巢狀結構轉換成 Hive 資料表，以利用 HiveQL 這種類似結構化查詢語言 (SQL) 的語言來查詢資料表。

Twitter 使用 OAuth 授權 tooprovide 存取 tooits API。 則 OAuth 就是代表允許使用者 tooapprove 應用程式 tooact，而不需要共用其密碼的驗證通訊協定。 詳細資訊，請參閱[oauth.net](http://oauth.net/)或 hello 絕佳[初級開發人員指南 tooOAuth](http://hueniverse.com/oauth/)從 Hueniverse。

第一個步驟 toouse hello OAuth 是 toocreate hello Twitter 開發人員網站上的新應用程式。

**toocreate Twitter 應用程式**

1. 登入太[https://apps.twitter.com/](https://apps.twitter.com/)。 按一下 hello**立即註冊**連結，如果您沒有 Twitter 帳戶。
2. 按一下 [建立新的應用程式] 。
3. 輸入 [名稱]、[說明]、[網站]。 您可以建立 hello 的 URL**網站**欄位。 hello 下表顯示一些範例值 toouse:

   | 欄位 | 值 |
   | --- | --- |
   |  名稱 |MyHDInsightApp |
   |  說明 |MyHDInsightApp |
   |  網站 |http://www.myhdinsightapp.com |
4. 核取 是，我同意 然後按一下建立 Twitter 應用程式。
5. 按一下 hello**權限** 索引標籤 hello 預設權限是**唯讀**。 本教學課程使用預設值即可。
6. 按一下 hello**機碼和存取權杖** 索引標籤。
7. 按一下 [Create my access token] 。
8. 按一下**測試 OAuth** hello 右上角的 hello 頁面中。
9. 記下**消費者金鑰**、**消費者祕密**、**存取權杖**和**存取權杖祕密**。 您將需要 hello 值在 hello 教學課程後面。

在本教學課程中，您將使用 Windows PowerShell toomake hello web 服務呼叫。 如需 .NET C# 範例，請參閱[使用 HDInsight 中的 HBase 分析即時的 Twitter 情感][hdinsight-hbase-twitter-sentiment]。 hello 其他常用的工具 toomake web 服務呼叫是[ *Curl*][curl]。 您可以從[這裡][curl-download]下載 Curl。

> [!NOTE]
> 當您使用 Windows hello curl 命令時，使用雙引號括住而不是方以單引號包住 hello 選項值。

**tooget 推文**

1. 開啟 Windows PowerShell 整合式指令碼環境 (ISE) hello。 (在 hello Windows 8 開始 畫面中，輸入**PowerShell_ISE** ，然後按一下 **Windows PowerShell ISE**。 請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start]。)
2. 複製下列指令碼到 hello 指令碼窗格中的 hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Hello 指令碼中設定 hello 前五個 tooeight 變數：

    變數|說明
    ---|---
    $clusterName|這是您想要 toorun hello 應用程式的 hello HDInsight 叢集的 hello 名稱。
    $oauth_consumer_key|這是 hello Twitter 應用程式**取用者索引鍵**您記下稍早建立 hello Twitter 應用程式時。
    $oauth_consumer_secret|這是 hello Twitter 應用程式**取用者秘密**您稍早記下。
    $oauth_token|這是 hello Twitter 應用程式**存取權杖**您稍早記下。
    $oauth_token_secret|這是 hello Twitter 應用程式**存取語彙基元秘**您稍早記下。
    $destBlobName|這是 hello 輸出 blob 名稱。 hello 預設值是**tutorials/twitter/data/tweets.txt**。 如果您變更 hello 預設值，您將會據以需要 tooupdate hello Windows PowerShell 指令碼。
    $trackString|hello web 服務會傳回推文相關的 toothese 關鍵字。 hello 預設值是**Azure 雲端中，HDInsight**。 如果您變更 hello 預設值，您也會據以更新 hello Windows PowerShell 指令碼。
    $lineMax|hello 值會決定多少推文 hello 指令碼會讀取。 它會採用三分鐘 tooread 100 推文。 您可以設定較大數目，但需要更多時間 toodownload。

1. 按**F5** toorun hello 指令碼。 如果遇到問題，以解決這個問題，選取所有的 hello 行，然後按**F8**。
2. 輸出的結尾應會顯示「完成！ 在 hello hello 輸出結尾。 錯誤訊息會顯示為紅色。

做為驗證程序中，您可以檢查 hello 輸出檔， **/tutorials/twitter/data/tweets.txt**，您使用 Azure 儲存體總管或 Azure PowerShell 的 Azure Blob 儲存體。 如需用於列出這些檔案的範例 Windows PowerShell 指令碼，請參閱[搭配 HDInsight 使用 Blob 儲存體][hdinsight-storage-powershell]。

## <a name="create-hiveql-script"></a>建立 HiveQL 指令碼
使用 Azure PowerShell，您可以執行多個下列 HiveQL 陳述式一次，或封裝 hello HiveQL 陳述式到指令碼檔案。 在本教學課程中，您將會建立 HiveQL 指令碼。 hello 指令碼檔案必須上傳的 tooAzure Blob 儲存體。 在 hello 下一步 區段中，您將使用 Azure PowerShell 執行 hello 指令碼檔案。

> [!NOTE]
> 在 公用 Blob 容器中已上傳 hello Hive 指令碼檔案和包含 10000 推文的檔案。 如果您想要 toouse hello 上傳檔案，則可以略過本節。

hello 下列 HiveQL 指令碼將會執行下列 hello:

1. **卸除 hello tweets_raw 資料表**以防 hello 資料表已經存在。
2. **建立 hello tweets_raw Hive 資料表**。 此結構化的資料表，保留 hello 資料更進一步的暫存區擷取、 轉換和載入 (ETL) 處理。 如需資料分割的相關資訊，請參閱 [Hive 教學課程][apache-hive-tutorial]。
3. **載入資料**hello 來源資料夾中 /tutorials/twitter/data。 巢狀的 JSON 格式 hello 推文大型資料集現在已轉換成暫存的 Hive 資料表結構。
4. **卸除 hello 推文資料表**以防 hello 資料表已經存在。
5. **建立 hello 推文資料表**。 您可以使用 Hive 查詢 hello 推文資料集之前，您需要 toorun 另一個 ETL 處理序。 此 ETL 程序定義儲存 hello"twitter_raw 」 資料表中的 hello 資料的更詳細的資料表結構描述。
6. **插入覆寫資料表**。 這個複雜的 Hive 指令碼會啟動一組很長的 MapReduce 工作由 hello Hadoop 叢集。 根據您的叢集您資料集和 hello 大小，這可能需要 10 分鐘。
7. **插入覆寫目錄**。 執行查詢和輸出 hello 資料集 tooa 檔案。 此查詢會傳回一份 Twitter 使用者傳送 hello word"Azure"所含的大部分推文。

**toocreate Hive 指令碼，並將它上傳 tooAzure**

1. 開啟 Windows PowerShell ISE。
2. 複製下列指令碼到 hello 指令碼窗格中的 hello:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

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

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
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

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Hello 指令碼中設定 hello 前兩個變數：

   | 變數 | 說明 |
   | --- | --- |
   |  $clusterName |輸入您想要 toorun hello 應用程式 hello HDInsight 叢集名稱。 |
   |  $subscriptionID |輸入您的 Azure 訂用帳戶 ID。 |
   |  $sourceDataPath |hello hello Hive 查詢將會讀取 hello 資料從 Azure Blob 儲存體位置。 您不需要 toochange 這個變數。 |
   |  $outputPath |hello hello Hive 查詢輸出 hello 結果的 Azure Blob 儲存體位置。 您不需要 toochange 這個變數。 |
   |  $hqlScriptFile |hello 位置和 hello hello 下列 HiveQL 指令碼檔案的檔案名稱。 您不需要 toochange 這個變數。 |
4. 按**F5** toorun hello 指令碼。 如果遇到問題，以解決這個問題，選取所有的 hello 行，然後按**F8**。
5. 輸出的結尾應會顯示「完成！ 在 hello hello 輸出結尾。 錯誤訊息會顯示為紅色。

做為驗證程序中，您可以檢查 hello 輸出檔， **/tutorials/twitter/twitter.hql**，您使用 Azure 儲存體總管或 Azure PowerShell 的 Azure Blob 儲存體。 如需用於列出這些檔案的範例 Windows PowerShell 指令碼，請參閱[搭配 HDInsight 使用 Blob 儲存體][hdinsight-storage-powershell]。

## <a name="process-twitter-data-by-using-hive"></a>使用 Hive 處理 Twitter 資料
您已完成所有 hello 準備工作。 現在，您可以叫用 hello Hive 指令碼，並檢查 hello 結果。

### <a name="submit-a-hive-job"></a>提交 Hive 工作
使用下列 Windows PowerShell 指令碼 toorun hello Hive 指令碼的 hello。 您將需要 tooset hello 第一個變數。

> [!NOTE]
> toouse hello 推文和 hello 在 hello 最後兩個區段中，設定 $hqlScriptFile too"/tutorials/twitter/twitter.hql 您上傳下列 HiveQL 指令碼 」。 為您 toouse hello 的已上傳的 tooa 公用 blob，設定得 $hqlScriptFile"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"。

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>檢查 hello 結果
使用下列 Windows PowerShell 指令碼 toocheck hello Hive 工作輸出的 hello。 您將需要 tooset hello 前兩個變數。

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> hello Hive 資料表使用 \001 hello 欄位分隔符號。 hello 輸出中看不到 hello 分隔符號。

Hello 分析結果放置在 Azure Blob 儲存體之後，您可以匯出 hello 資料 tooan Azure SQL 資料庫/SQL server、 使用 Power Query 匯出 hello 資料 tooExcel 或您的應用程式 toohello 資料連接使用 hello hive 控制檔的 ODBC 驅動程式。 如需詳細資訊，請參閱[與 HDInsight 的使用 Sqoop][hdinsight-use-sqoop]，[飛行延遲使用分析資料 HDInsight][hdinsight-analyze-flight-delay-data]， [有了 Power Query 連接 Excel tooHDInsight][hdinsight-power-query]，和[以 hello Microsoft Hive ODBC 驅動程式連接的 Excel tooHDInsight][hdinsight-hive-odbc]。

## <a name="next-steps"></a>後續步驟
在本教學課程中，我們已經看到如何 tootransform 結構化的 Hive 資料表 tooquery，非結構化 JSON 資料集探索及分析 Azure 上使用 HDInsight Twitter 的資料。 toolearn 詳細資訊，請參閱：

* [開始使用 HDInsight][hdinsight-get-started]
* [使用 HDInsight 中的 HBase 分析即時的 Twitter 情感][hdinsight-hbase-twitter-sentiment]
* [使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-delay-data]
* [有了 Power Query 連接 Excel tooHDInsight][hdinsight-power-query]
* [Excel tooHDInsight 連接以 hello Microsoft Hive ODBC 驅動程式][hdinsight-hive-odbc]
* [搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
