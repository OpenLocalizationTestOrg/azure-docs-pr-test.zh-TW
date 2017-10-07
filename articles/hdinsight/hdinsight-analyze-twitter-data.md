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
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="90c97-103">在 HDInsight 中使用 Hive 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="90c97-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="90c97-104">社交網站是其中一種 hello 主要推進巨量資料採用。</span><span class="sxs-lookup"><span data-stu-id="90c97-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="90c97-105">像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。</span><span class="sxs-lookup"><span data-stu-id="90c97-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="90c97-106">在本教學課程中，您將使用 Twitter，串流處理應用程式開發介面，以取得推文，然後再使用 Azure HDInsight tooget 的 Twitter 使用者傳送嗨大部分推文包含特定的字詞清單中的 Apache hive 控制檔。</span><span class="sxs-lookup"><span data-stu-id="90c97-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90c97-107">hello 本文件中的步驟需要 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="90c97-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="90c97-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="90c97-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="90c97-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="90c97-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="90c97-110">針對步驟特定 tooa linux 叢集，請參閱[分析 Twitter 資料使用 HDInsight (Linux) 中的登錄區](hdinsight-analyze-twitter-data-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="90c97-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90c97-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="90c97-111">Prerequisites</span></span>
<span data-ttu-id="90c97-112">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="90c97-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="90c97-113">**工作站** 。</span><span class="sxs-lookup"><span data-stu-id="90c97-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="90c97-114">tooexecute Windows PowerShell 指令碼，您必須以系統管理員身分執行 Azure PowerShell 並 hello 執行原則設定太*RemoteSigned*。</span><span class="sxs-lookup"><span data-stu-id="90c97-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="90c97-115">請參閱[執行 Windows PowerShell 指令碼][powershell-script]。</span><span class="sxs-lookup"><span data-stu-id="90c97-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="90c97-116">再執行 Windows PowerShell 指令碼，請確定您已連接的 tooyour Azure 訂用帳戶使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="90c97-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="90c97-117">如果您有多個 Azure 訂用帳戶，請使用下列 cmdlet tooset hello 目前訂用帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="90c97-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="90c97-118">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="90c97-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="90c97-119">此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="90c97-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="90c97-120">請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="90c97-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="90c97-121">如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="90c97-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="90c97-122">**Azure HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="90c97-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="90c97-123">如需叢集佈建的指示，請參閱[開始使用 HDInsight][hdinsight-get-started] 或[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="90c97-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="90c97-124">您必須在 hello 教學課程後面 hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="90c97-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="90c97-125">hello 下表列出本教學課程所用的 hello 檔案：</span><span class="sxs-lookup"><span data-stu-id="90c97-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="90c97-126">檔案</span><span class="sxs-lookup"><span data-stu-id="90c97-126">Files</span></span> | <span data-ttu-id="90c97-127">說明</span><span class="sxs-lookup"><span data-stu-id="90c97-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="90c97-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="90c97-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="90c97-129">hello hello Hive 工作的來源資料。</span><span class="sxs-lookup"><span data-stu-id="90c97-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="90c97-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="90c97-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="90c97-131">hello hello Hive 工作的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="90c97-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="90c97-132">hello 預設 Hive 工作輸出檔案名稱是**000000_0**。</span><span class="sxs-lookup"><span data-stu-id="90c97-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="90c97-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="90c97-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="90c97-134">hello 下列 HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="90c97-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="90c97-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="90c97-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="90c97-136">hello Hadoop 工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="90c97-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="90c97-137">取得 Twitter 摘要</span><span class="sxs-lookup"><span data-stu-id="90c97-137">Get Twitter feed</span></span>
<span data-ttu-id="90c97-138">在此教學課程中，您將使用 hello [Twitter 資料流 Api][twitter-streaming-api]。</span><span class="sxs-lookup"><span data-stu-id="90c97-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="90c97-139">hello 串流處理應用程式開發介面，您將使用的特定 Twitter 是[狀態/篩選][twitter-statuses-filter]。</span><span class="sxs-lookup"><span data-stu-id="90c97-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="90c97-140">公用 Blob 容器中已上傳一個包含 10000 推文和 hello Hive 指令碼檔案 （涵蓋在 hello 下一節） 檔案。</span><span class="sxs-lookup"><span data-stu-id="90c97-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="90c97-141">如果您想要 toouse hello 上傳檔案，則可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="90c97-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="90c97-142">[資料推文](https://dev.twitter.com/docs/platform-objects/tweets)會儲存在 hello JavaScript Object Notation (JSON) 格式，其中包含複雜的巢狀的結構。</span><span class="sxs-lookup"><span data-stu-id="90c97-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="90c97-143">您可以不要使用慣用的程式設計語言撰寫多行程式碼，而將此巢狀結構轉換成 Hive 資料表，以利用 HiveQL 這種類似結構化查詢語言 (SQL) 的語言來查詢資料表。</span><span class="sxs-lookup"><span data-stu-id="90c97-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="90c97-144">Twitter 使用 OAuth 授權 tooprovide 存取 tooits API。</span><span class="sxs-lookup"><span data-stu-id="90c97-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="90c97-145">則 OAuth 就是代表允許使用者 tooapprove 應用程式 tooact，而不需要共用其密碼的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="90c97-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="90c97-146">詳細資訊，請參閱[oauth.net](http://oauth.net/)或 hello 絕佳[初級開發人員指南 tooOAuth](http://hueniverse.com/oauth/)從 Hueniverse。</span><span class="sxs-lookup"><span data-stu-id="90c97-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="90c97-147">第一個步驟 toouse hello OAuth 是 toocreate hello Twitter 開發人員網站上的新應用程式。</span><span class="sxs-lookup"><span data-stu-id="90c97-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="90c97-148">**toocreate Twitter 應用程式**</span><span class="sxs-lookup"><span data-stu-id="90c97-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="90c97-149">登入太[https://apps.twitter.com/](https://apps.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="90c97-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="90c97-150">按一下 hello**立即註冊**連結，如果您沒有 Twitter 帳戶。</span><span class="sxs-lookup"><span data-stu-id="90c97-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="90c97-151">按一下 [建立新的應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="90c97-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="90c97-152">輸入 [名稱]、[說明]、[網站]。</span><span class="sxs-lookup"><span data-stu-id="90c97-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="90c97-153">您可以建立 hello 的 URL**網站**欄位。</span><span class="sxs-lookup"><span data-stu-id="90c97-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="90c97-154">hello 下表顯示一些範例值 toouse:</span><span class="sxs-lookup"><span data-stu-id="90c97-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="90c97-155">欄位</span><span class="sxs-lookup"><span data-stu-id="90c97-155">Field</span></span> | <span data-ttu-id="90c97-156">值</span><span class="sxs-lookup"><span data-stu-id="90c97-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="90c97-157">名稱</span><span class="sxs-lookup"><span data-stu-id="90c97-157">Name</span></span> |<span data-ttu-id="90c97-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="90c97-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="90c97-159">說明</span><span class="sxs-lookup"><span data-stu-id="90c97-159">Description</span></span> |<span data-ttu-id="90c97-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="90c97-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="90c97-161">網站</span><span class="sxs-lookup"><span data-stu-id="90c97-161">Website</span></span> |<span data-ttu-id="90c97-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="90c97-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="90c97-163">核取 是，我同意 然後按一下建立 Twitter 應用程式。</span><span class="sxs-lookup"><span data-stu-id="90c97-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="90c97-164">按一下 hello**權限** 索引標籤 hello 預設權限是**唯讀**。</span><span class="sxs-lookup"><span data-stu-id="90c97-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="90c97-165">本教學課程使用預設值即可。</span><span class="sxs-lookup"><span data-stu-id="90c97-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="90c97-166">按一下 hello**機碼和存取權杖** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="90c97-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="90c97-167">按一下 [Create my access token] 。</span><span class="sxs-lookup"><span data-stu-id="90c97-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="90c97-168">按一下**測試 OAuth** hello 右上角的 hello 頁面中。</span><span class="sxs-lookup"><span data-stu-id="90c97-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="90c97-169">記下**消費者金鑰**、**消費者祕密**、**存取權杖**和**存取權杖祕密**。</span><span class="sxs-lookup"><span data-stu-id="90c97-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="90c97-170">您將需要 hello 值在 hello 教學課程後面。</span><span class="sxs-lookup"><span data-stu-id="90c97-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="90c97-171">在本教學課程中，您將使用 Windows PowerShell toomake hello web 服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="90c97-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="90c97-172">如需 .NET C# 範例，請參閱[使用 HDInsight 中的 HBase 分析即時的 Twitter 情感][hdinsight-hbase-twitter-sentiment]。</span><span class="sxs-lookup"><span data-stu-id="90c97-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="90c97-173">hello 其他常用的工具 toomake web 服務呼叫是[ *Curl*][curl]。</span><span class="sxs-lookup"><span data-stu-id="90c97-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="90c97-174">您可以從[這裡][curl-download]下載 Curl。</span><span class="sxs-lookup"><span data-stu-id="90c97-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="90c97-175">當您使用 Windows hello curl 命令時，使用雙引號括住而不是方以單引號包住 hello 選項值。</span><span class="sxs-lookup"><span data-stu-id="90c97-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="90c97-176">**tooget 推文**</span><span class="sxs-lookup"><span data-stu-id="90c97-176">**tooget tweets**</span></span>

1. <span data-ttu-id="90c97-177">開啟 Windows PowerShell 整合式指令碼環境 (ISE) hello。</span><span class="sxs-lookup"><span data-stu-id="90c97-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="90c97-178">(在 hello Windows 8 開始 畫面中，輸入**PowerShell_ISE** ，然後按一下 **Windows PowerShell ISE**。</span><span class="sxs-lookup"><span data-stu-id="90c97-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="90c97-179">請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start]。)</span><span class="sxs-lookup"><span data-stu-id="90c97-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="90c97-180">複製下列指令碼到 hello 指令碼窗格中的 hello:</span><span class="sxs-lookup"><span data-stu-id="90c97-180">Copy hello following script into hello script pane:</span></span>

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

3. <span data-ttu-id="90c97-181">Hello 指令碼中設定 hello 前五個 tooeight 變數：</span><span class="sxs-lookup"><span data-stu-id="90c97-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="90c97-182">變數</span><span class="sxs-lookup"><span data-stu-id="90c97-182">Variable</span></span>|<span data-ttu-id="90c97-183">說明</span><span class="sxs-lookup"><span data-stu-id="90c97-183">Description</span></span>
    ---|---
    <span data-ttu-id="90c97-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="90c97-184">$clusterName</span></span>|<span data-ttu-id="90c97-185">這是您想要 toorun hello 應用程式的 hello HDInsight 叢集的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="90c97-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="90c97-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="90c97-186">$oauth_consumer_key</span></span>|<span data-ttu-id="90c97-187">這是 hello Twitter 應用程式**取用者索引鍵**您記下稍早建立 hello Twitter 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="90c97-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="90c97-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="90c97-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="90c97-189">這是 hello Twitter 應用程式**取用者秘密**您稍早記下。</span><span class="sxs-lookup"><span data-stu-id="90c97-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="90c97-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="90c97-190">$oauth_token</span></span>|<span data-ttu-id="90c97-191">這是 hello Twitter 應用程式**存取權杖**您稍早記下。</span><span class="sxs-lookup"><span data-stu-id="90c97-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="90c97-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="90c97-192">$oauth_token_secret</span></span>|<span data-ttu-id="90c97-193">這是 hello Twitter 應用程式**存取語彙基元秘**您稍早記下。</span><span class="sxs-lookup"><span data-stu-id="90c97-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="90c97-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="90c97-194">$destBlobName</span></span>|<span data-ttu-id="90c97-195">這是 hello 輸出 blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="90c97-195">This is hello output blob name.</span></span> <span data-ttu-id="90c97-196">hello 預設值是**tutorials/twitter/data/tweets.txt**。</span><span class="sxs-lookup"><span data-stu-id="90c97-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="90c97-197">如果您變更 hello 預設值，您將會據以需要 tooupdate hello Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="90c97-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="90c97-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="90c97-198">$trackString</span></span>|<span data-ttu-id="90c97-199">hello web 服務會傳回推文相關的 toothese 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="90c97-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="90c97-200">hello 預設值是**Azure 雲端中，HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="90c97-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="90c97-201">如果您變更 hello 預設值，您也會據以更新 hello Windows PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="90c97-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="90c97-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="90c97-202">$lineMax</span></span>|<span data-ttu-id="90c97-203">hello 值會決定多少推文 hello 指令碼會讀取。</span><span class="sxs-lookup"><span data-stu-id="90c97-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="90c97-204">它會採用三分鐘 tooread 100 推文。</span><span class="sxs-lookup"><span data-stu-id="90c97-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="90c97-205">您可以設定較大數目，但需要更多時間 toodownload。</span><span class="sxs-lookup"><span data-stu-id="90c97-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="90c97-206">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="90c97-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="90c97-207">如果遇到問題，以解決這個問題，選取所有的 hello 行，然後按**F8**。</span><span class="sxs-lookup"><span data-stu-id="90c97-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="90c97-208">輸出的結尾應會顯示「完成！</span><span class="sxs-lookup"><span data-stu-id="90c97-208">You shall see "Complete!"</span></span> <span data-ttu-id="90c97-209">在 hello hello 輸出結尾。</span><span class="sxs-lookup"><span data-stu-id="90c97-209">at hello end of hello output.</span></span> <span data-ttu-id="90c97-210">錯誤訊息會顯示為紅色。</span><span class="sxs-lookup"><span data-stu-id="90c97-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="90c97-211">做為驗證程序中，您可以檢查 hello 輸出檔， **/tutorials/twitter/data/tweets.txt**，您使用 Azure 儲存體總管或 Azure PowerShell 的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="90c97-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="90c97-212">如需用於列出這些檔案的範例 Windows PowerShell 指令碼，請參閱[搭配 HDInsight 使用 Blob 儲存體][hdinsight-storage-powershell]。</span><span class="sxs-lookup"><span data-stu-id="90c97-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="90c97-213">建立 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="90c97-213">Create HiveQL script</span></span>
<span data-ttu-id="90c97-214">使用 Azure PowerShell，您可以執行多個下列 HiveQL 陳述式一次，或封裝 hello HiveQL 陳述式到指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="90c97-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="90c97-215">在本教學課程中，您將會建立 HiveQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="90c97-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="90c97-216">hello 指令碼檔案必須上傳的 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="90c97-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="90c97-217">在 hello 下一步 區段中，您將使用 Azure PowerShell 執行 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="90c97-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="90c97-218">在 公用 Blob 容器中已上傳 hello Hive 指令碼檔案和包含 10000 推文的檔案。</span><span class="sxs-lookup"><span data-stu-id="90c97-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="90c97-219">如果您想要 toouse hello 上傳檔案，則可以略過本節。</span><span class="sxs-lookup"><span data-stu-id="90c97-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="90c97-220">hello 下列 HiveQL 指令碼將會執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="90c97-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="90c97-221">**卸除 hello tweets_raw 資料表**以防 hello 資料表已經存在。</span><span class="sxs-lookup"><span data-stu-id="90c97-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="90c97-222">**建立 hello tweets_raw Hive 資料表**。</span><span class="sxs-lookup"><span data-stu-id="90c97-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="90c97-223">此結構化的資料表，保留 hello 資料更進一步的暫存區擷取、 轉換和載入 (ETL) 處理。</span><span class="sxs-lookup"><span data-stu-id="90c97-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="90c97-224">如需資料分割的相關資訊，請參閱 [Hive 教學課程][apache-hive-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="90c97-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="90c97-225">**載入資料**hello 來源資料夾中 /tutorials/twitter/data。</span><span class="sxs-lookup"><span data-stu-id="90c97-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="90c97-226">巢狀的 JSON 格式 hello 推文大型資料集現在已轉換成暫存的 Hive 資料表結構。</span><span class="sxs-lookup"><span data-stu-id="90c97-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="90c97-227">**卸除 hello 推文資料表**以防 hello 資料表已經存在。</span><span class="sxs-lookup"><span data-stu-id="90c97-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="90c97-228">**建立 hello 推文資料表**。</span><span class="sxs-lookup"><span data-stu-id="90c97-228">**Create hello tweets table**.</span></span> <span data-ttu-id="90c97-229">您可以使用 Hive 查詢 hello 推文資料集之前，您需要 toorun 另一個 ETL 處理序。</span><span class="sxs-lookup"><span data-stu-id="90c97-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="90c97-230">此 ETL 程序定義儲存 hello"twitter_raw 」 資料表中的 hello 資料的更詳細的資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="90c97-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="90c97-231">**插入覆寫資料表**。</span><span class="sxs-lookup"><span data-stu-id="90c97-231">**Insert overwrite table**.</span></span> <span data-ttu-id="90c97-232">這個複雜的 Hive 指令碼會啟動一組很長的 MapReduce 工作由 hello Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="90c97-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="90c97-233">根據您的叢集您資料集和 hello 大小，這可能需要 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="90c97-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="90c97-234">**插入覆寫目錄**。</span><span class="sxs-lookup"><span data-stu-id="90c97-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="90c97-235">執行查詢和輸出 hello 資料集 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="90c97-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="90c97-236">此查詢會傳回一份 Twitter 使用者傳送 hello word"Azure"所含的大部分推文。</span><span class="sxs-lookup"><span data-stu-id="90c97-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="90c97-237">**toocreate Hive 指令碼，並將它上傳 tooAzure**</span><span class="sxs-lookup"><span data-stu-id="90c97-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="90c97-238">開啟 Windows PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="90c97-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="90c97-239">複製下列指令碼到 hello 指令碼窗格中的 hello:</span><span class="sxs-lookup"><span data-stu-id="90c97-239">Copy hello following script into hello script pane:</span></span>

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

3. <span data-ttu-id="90c97-240">Hello 指令碼中設定 hello 前兩個變數：</span><span class="sxs-lookup"><span data-stu-id="90c97-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="90c97-241">變數</span><span class="sxs-lookup"><span data-stu-id="90c97-241">Variable</span></span> | <span data-ttu-id="90c97-242">說明</span><span class="sxs-lookup"><span data-stu-id="90c97-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="90c97-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="90c97-243">$clusterName</span></span> |<span data-ttu-id="90c97-244">輸入您想要 toorun hello 應用程式 hello HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="90c97-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="90c97-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="90c97-245">$subscriptionID</span></span> |<span data-ttu-id="90c97-246">輸入您的 Azure 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="90c97-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="90c97-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="90c97-247">$sourceDataPath</span></span> |<span data-ttu-id="90c97-248">hello hello Hive 查詢將會讀取 hello 資料從 Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="90c97-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="90c97-249">您不需要 toochange 這個變數。</span><span class="sxs-lookup"><span data-stu-id="90c97-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="90c97-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="90c97-250">$outputPath</span></span> |<span data-ttu-id="90c97-251">hello hello Hive 查詢輸出 hello 結果的 Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="90c97-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="90c97-252">您不需要 toochange 這個變數。</span><span class="sxs-lookup"><span data-stu-id="90c97-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="90c97-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="90c97-253">$hqlScriptFile</span></span> |<span data-ttu-id="90c97-254">hello 位置和 hello hello 下列 HiveQL 指令碼檔案的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="90c97-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="90c97-255">您不需要 toochange 這個變數。</span><span class="sxs-lookup"><span data-stu-id="90c97-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="90c97-256">按**F5** toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="90c97-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="90c97-257">如果遇到問題，以解決這個問題，選取所有的 hello 行，然後按**F8**。</span><span class="sxs-lookup"><span data-stu-id="90c97-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="90c97-258">輸出的結尾應會顯示「完成！</span><span class="sxs-lookup"><span data-stu-id="90c97-258">You shall see "Complete!"</span></span> <span data-ttu-id="90c97-259">在 hello hello 輸出結尾。</span><span class="sxs-lookup"><span data-stu-id="90c97-259">at hello end of hello output.</span></span> <span data-ttu-id="90c97-260">錯誤訊息會顯示為紅色。</span><span class="sxs-lookup"><span data-stu-id="90c97-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="90c97-261">做為驗證程序中，您可以檢查 hello 輸出檔， **/tutorials/twitter/twitter.hql**，您使用 Azure 儲存體總管或 Azure PowerShell 的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="90c97-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="90c97-262">如需用於列出這些檔案的範例 Windows PowerShell 指令碼，請參閱[搭配 HDInsight 使用 Blob 儲存體][hdinsight-storage-powershell]。</span><span class="sxs-lookup"><span data-stu-id="90c97-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="90c97-263">使用 Hive 處理 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="90c97-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="90c97-264">您已完成所有 hello 準備工作。</span><span class="sxs-lookup"><span data-stu-id="90c97-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="90c97-265">現在，您可以叫用 hello Hive 指令碼，並檢查 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="90c97-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="90c97-266">提交 Hive 工作</span><span class="sxs-lookup"><span data-stu-id="90c97-266">Submit a Hive job</span></span>
<span data-ttu-id="90c97-267">使用下列 Windows PowerShell 指令碼 toorun hello Hive 指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="90c97-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="90c97-268">您將需要 tooset hello 第一個變數。</span><span class="sxs-lookup"><span data-stu-id="90c97-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="90c97-269">toouse hello 推文和 hello 在 hello 最後兩個區段中，設定 $hqlScriptFile too"/tutorials/twitter/twitter.hql 您上傳下列 HiveQL 指令碼 」。</span><span class="sxs-lookup"><span data-stu-id="90c97-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="90c97-270">為您 toouse hello 的已上傳的 tooa 公用 blob，設定得 $hqlScriptFile"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"。</span><span class="sxs-lookup"><span data-stu-id="90c97-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

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

### <a name="check-hello-results"></a><span data-ttu-id="90c97-271">檢查 hello 結果</span><span class="sxs-lookup"><span data-stu-id="90c97-271">Check hello results</span></span>
<span data-ttu-id="90c97-272">使用下列 Windows PowerShell 指令碼 toocheck hello Hive 工作輸出的 hello。</span><span class="sxs-lookup"><span data-stu-id="90c97-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="90c97-273">您將需要 tooset hello 前兩個變數。</span><span class="sxs-lookup"><span data-stu-id="90c97-273">You will need tooset hello first two variables.</span></span>

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
> hello Hive 資料表使用 \001 hello 欄位分隔符號。 <span data-ttu-id="90c97-275">hello 輸出中看不到 hello 分隔符號。</span><span class="sxs-lookup"><span data-stu-id="90c97-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="90c97-276">Hello 分析結果放置在 Azure Blob 儲存體之後，您可以匯出 hello 資料 tooan Azure SQL 資料庫/SQL server、 使用 Power Query 匯出 hello 資料 tooExcel 或您的應用程式 toohello 資料連接使用 hello hive 控制檔的 ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="90c97-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="90c97-277">如需詳細資訊，請參閱[與 HDInsight 的使用 Sqoop][hdinsight-use-sqoop]，[飛行延遲使用分析資料 HDInsight][hdinsight-analyze-flight-delay-data]， [有了 Power Query 連接 Excel tooHDInsight][hdinsight-power-query]，和[以 hello Microsoft Hive ODBC 驅動程式連接的 Excel tooHDInsight][hdinsight-hive-odbc]。</span><span class="sxs-lookup"><span data-stu-id="90c97-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="90c97-278">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90c97-278">Next steps</span></span>
<span data-ttu-id="90c97-279">在本教學課程中，我們已經看到如何 tootransform 結構化的 Hive 資料表 tooquery，非結構化 JSON 資料集探索及分析 Azure 上使用 HDInsight Twitter 的資料。</span><span class="sxs-lookup"><span data-stu-id="90c97-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="90c97-280">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="90c97-280">toolearn more, see:</span></span>

* <span data-ttu-id="90c97-281">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="90c97-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="90c97-282">[使用 HDInsight 中的 HBase 分析即時的 Twitter 情感][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="90c97-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="90c97-283">[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="90c97-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="90c97-284">[有了 Power Query 連接 Excel tooHDInsight][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="90c97-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="90c97-285">[Excel tooHDInsight 連接以 hello Microsoft Hive ODBC 驅動程式][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="90c97-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="90c97-286">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="90c97-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
