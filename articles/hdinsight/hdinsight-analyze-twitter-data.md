---
title: "使用 HDInsight 中的 Hadoop 分析 Twitter 資料 - Azure | Microsoft Docs"
description: "了解如何在 HDInsight 中的 Hadoop 上使用 Hive 來分析 Twitter 資料，以找出特定單字的使用頻率。"
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
ms.openlocfilehash: 711d364c36c3aba699326f4a76d42891ba3219fb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="2e286-103">在 HDInsight 中使用 Hive 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="2e286-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="2e286-104">社群網站是驅使採用巨量資料的其中一個主要動力。</span><span class="sxs-lookup"><span data-stu-id="2e286-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="2e286-105">像 Twitter 之類的網站所提供的公開 API，是分析和了解流行趨勢的一項實用的資料來源。</span><span class="sxs-lookup"><span data-stu-id="2e286-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="2e286-106">在本教學課程中，您將使用 Twitter 串流 API 取得推文，然後使用 Apache Hive on Azure HDInsight 取得傳送了最多內含特定文字之推文的 Twitter 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="2e286-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e286-107">此文件中的步驟需要 Windows 型 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="2e286-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="2e286-108">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="2e286-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2e286-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="2e286-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="2e286-110">如需 Linux 型叢集的特定步驟，請參閱 [在 HDInsight (Linux) 中使用 Hive 分析 Twitter 資料](hdinsight-analyze-twitter-data-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="2e286-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e286-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="2e286-111">Prerequisites</span></span>
<span data-ttu-id="2e286-112">開始進行本教學課程之前，您必須具備下列條件：</span><span class="sxs-lookup"><span data-stu-id="2e286-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="2e286-113">**工作站** 。</span><span class="sxs-lookup"><span data-stu-id="2e286-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="2e286-114">若要執行 Windows PowerShell 指令碼，您必須以系統管理員的身分執行 Azure PowerShell，並將執行原則設為 *RemoteSigned*。</span><span class="sxs-lookup"><span data-stu-id="2e286-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="2e286-115">請參閱[執行 Windows PowerShell 指令碼][powershell-script]。</span><span class="sxs-lookup"><span data-stu-id="2e286-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="2e286-116">執行 Windows PowerShell 指令碼之前，請確定您已使用下列 Cmdlet 連接到 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="2e286-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="2e286-117">如果您有多個 Azure 訂閱，請使用下列 Cmdlet 設定目前的訂閱：</span><span class="sxs-lookup"><span data-stu-id="2e286-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="2e286-118">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="2e286-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="2e286-119">本文件中的步驟會使用可與 Azure Resource Manager 搭配使用的新 HDInsight Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2e286-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2e286-120">請遵循 [安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) 中的步驟來安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2e286-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2e286-121">如果您需要修改指令碼才能使用適用於 Azure Resource Manager 的新 Cmdlet，請參閱 [移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)](hdinsight-hadoop-development-using-azure-resource-manager.md) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2e286-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="2e286-122">**Azure HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="2e286-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="2e286-123">如需叢集佈建的指示，請參閱[開始使用 HDInsight][hdinsight-get-started] 或[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="2e286-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="2e286-124">稍後在教學課程中會用到此叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="2e286-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="2e286-125">下表列出本教學課程中使用的檔案：</span><span class="sxs-lookup"><span data-stu-id="2e286-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="2e286-126">檔案</span><span class="sxs-lookup"><span data-stu-id="2e286-126">Files</span></span> | <span data-ttu-id="2e286-127">說明</span><span class="sxs-lookup"><span data-stu-id="2e286-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2e286-128">/tutorials/twitter/data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="2e286-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="2e286-129">Hive 工作的來源資料。</span><span class="sxs-lookup"><span data-stu-id="2e286-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="2e286-130">/tutorials/twitter/output</span><span class="sxs-lookup"><span data-stu-id="2e286-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="2e286-131">Hive 工作的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e286-131">The output folder for the Hive job.</span></span> <span data-ttu-id="2e286-132">預設 Hive 工作的輸出檔案名稱為 **000000_0**。</span><span class="sxs-lookup"><span data-stu-id="2e286-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="2e286-133">tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="2e286-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="2e286-134">HiveQL 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="2e286-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="2e286-135">/tutorials/twitter/jobstatus</span><span class="sxs-lookup"><span data-stu-id="2e286-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="2e286-136">Hadoop 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="2e286-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="2e286-137">取得 Twitter 摘要</span><span class="sxs-lookup"><span data-stu-id="2e286-137">Get Twitter feed</span></span>
<span data-ttu-id="2e286-138">在本教學課程中，您將使用 [Twitter 串流 API][twitter-streaming-api]。</span><span class="sxs-lookup"><span data-stu-id="2e286-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="2e286-139">您將使用的特定 Twitter 串流 API 為 [statuses/filter][twitter-statuses-filter]。</span><span class="sxs-lookup"><span data-stu-id="2e286-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="2e286-140">已在公用 Blob 容器中上傳含有 10,000 則推文的檔案和 Hive 指令碼檔案 (下一節說明)。</span><span class="sxs-lookup"><span data-stu-id="2e286-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="2e286-141">如果想要使用上傳的檔案，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="2e286-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="2e286-142">[推文資料](https://dev.twitter.com/docs/platform-objects/tweets) 會以包含複雜巢狀結構的 JavaScript 物件標記法 (JSON) 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="2e286-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="2e286-143">您可以不要使用慣用的程式設計語言撰寫多行程式碼，而將此巢狀結構轉換成 Hive 資料表，以利用 HiveQL 這種類似結構化查詢語言 (SQL) 的語言來查詢資料表。</span><span class="sxs-lookup"><span data-stu-id="2e286-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="2e286-144">Twitter 會使用 OAuth 提供對其 API 的授權存取。</span><span class="sxs-lookup"><span data-stu-id="2e286-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="2e286-145">OAuth 是一項驗證通訊協定，可讓使用者在無須共用其密碼的情況下，允許應用程式代表他們執行動作。</span><span class="sxs-lookup"><span data-stu-id="2e286-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="2e286-146">如需詳細資訊，請至 [oauth.net](http://oauth.net/)，或參考 Hueniverse 的 [OAuth 的入門指南](http://hueniverse.com/oauth/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="2e286-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="2e286-147">使用 OAuth 的第一個步驟，是在 Twitter 開發人員網站上建立新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e286-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="2e286-148">**建立 Twitter 應用程式**</span><span class="sxs-lookup"><span data-stu-id="2e286-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="2e286-149">登入 [https://apps.twitter.com/](https://apps.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="2e286-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="2e286-150">如果您沒有 Twitter 帳戶，請按一下 [ **立即註冊** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="2e286-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="2e286-151">按一下 [建立新的應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="2e286-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="2e286-152">輸入 [名稱]、[說明]、[網站]。</span><span class="sxs-lookup"><span data-stu-id="2e286-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="2e286-153">您可以在 [網站] 欄位中自行設定 URL。</span><span class="sxs-lookup"><span data-stu-id="2e286-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="2e286-154">下表列出部分要使用的範例值：</span><span class="sxs-lookup"><span data-stu-id="2e286-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="2e286-155">欄位</span><span class="sxs-lookup"><span data-stu-id="2e286-155">Field</span></span> | <span data-ttu-id="2e286-156">值</span><span class="sxs-lookup"><span data-stu-id="2e286-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="2e286-157">名稱</span><span class="sxs-lookup"><span data-stu-id="2e286-157">Name</span></span> |<span data-ttu-id="2e286-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="2e286-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="2e286-159">說明</span><span class="sxs-lookup"><span data-stu-id="2e286-159">Description</span></span> |<span data-ttu-id="2e286-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="2e286-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="2e286-161">網站</span><span class="sxs-lookup"><span data-stu-id="2e286-161">Website</span></span> |<span data-ttu-id="2e286-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="2e286-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="2e286-163">核取 [是，我同意] 然後按一下 [建立 Twitter 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="2e286-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="2e286-164">按一下 [權限]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2e286-164">Click the **Permissions** tab.</span></span> <span data-ttu-id="2e286-165">預設權限為 [唯讀] 。</span><span class="sxs-lookup"><span data-stu-id="2e286-165">The default permission is **Read only**.</span></span> <span data-ttu-id="2e286-166">本教學課程使用預設值即可。</span><span class="sxs-lookup"><span data-stu-id="2e286-166">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="2e286-167">按一下 **[金鑰和存取權杖** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="2e286-167">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="2e286-168">按一下 [Create my access token] 。</span><span class="sxs-lookup"><span data-stu-id="2e286-168">Click **Create my access token**.</span></span>
8. <span data-ttu-id="2e286-169">按一下位於頁面右上角的 [測試 OAuth]  。</span><span class="sxs-lookup"><span data-stu-id="2e286-169">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="2e286-170">記下**消費者金鑰**、**消費者祕密**、**存取權杖**和**存取權杖祕密**。</span><span class="sxs-lookup"><span data-stu-id="2e286-170">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="2e286-171">稍後在教學課程中會用到這些值。</span><span class="sxs-lookup"><span data-stu-id="2e286-171">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="2e286-172">在本教學課程中，您將使用 Windows PowerShell 發出 Web 服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="2e286-172">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="2e286-173">如需 .NET C# 範例，請參閱[使用 HDInsight 中的 HBase 分析即時的 Twitter 情感][hdinsight-hbase-twitter-sentiment]。</span><span class="sxs-lookup"><span data-stu-id="2e286-173">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="2e286-174">另一項常用來發出 Web 服務呼叫的工具是 [*Curl*][curl]。</span><span class="sxs-lookup"><span data-stu-id="2e286-174">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="2e286-175">您可以從[這裡][curl-download]下載 Curl。</span><span class="sxs-lookup"><span data-stu-id="2e286-175">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="2e286-176">在 Windows 上使用 curl 命令時，對選項值請使用雙引號，而不要使用單引號。</span><span class="sxs-lookup"><span data-stu-id="2e286-176">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="2e286-177">**取得推文**</span><span class="sxs-lookup"><span data-stu-id="2e286-177">**To get tweets**</span></span>

1. <span data-ttu-id="2e286-178">開啟 Windows PowerShell 整合式指令碼環境 (ISE)。</span><span class="sxs-lookup"><span data-stu-id="2e286-178">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="2e286-179">(在 Windows 8 的 [開始] 畫面上輸入 **PowerShell_ISE**，然後按一下 [Windows PowerShell ISE]。</span><span class="sxs-lookup"><span data-stu-id="2e286-179">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="2e286-180">請參閱[在 Windows 8 和 Windows 上啟動 Windows PowerShell][powershell-start]。)</span><span class="sxs-lookup"><span data-stu-id="2e286-180">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="2e286-181">將下列指令碼複製到指令碼窗格中：</span><span class="sxs-lookup"><span data-stu-id="2e286-181">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="2e286-182">設定指令碼中的前五到八個變數：</span><span class="sxs-lookup"><span data-stu-id="2e286-182">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="2e286-183">變數</span><span class="sxs-lookup"><span data-stu-id="2e286-183">Variable</span></span>|<span data-ttu-id="2e286-184">說明</span><span class="sxs-lookup"><span data-stu-id="2e286-184">Description</span></span>
    ---|---
    <span data-ttu-id="2e286-185">$clusterName</span><span class="sxs-lookup"><span data-stu-id="2e286-185">$clusterName</span></span>|<span data-ttu-id="2e286-186">這是您要執行應用程式的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="2e286-186">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="2e286-187">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="2e286-187">$oauth_consumer_key</span></span>|<span data-ttu-id="2e286-188">這是您先前在建立 Twitter 應用程式時所記下的 Twitter 應用程式 **消費者金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="2e286-188">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="2e286-189">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="2e286-189">$oauth_consumer_secret</span></span>|<span data-ttu-id="2e286-190">這是您先前記下的 Twitter 應用程式 **消費者密碼** 。</span><span class="sxs-lookup"><span data-stu-id="2e286-190">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="2e286-191">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="2e286-191">$oauth_token</span></span>|<span data-ttu-id="2e286-192">這是您先前記下的 Twitter 應用程式 **存取權杖** 。</span><span class="sxs-lookup"><span data-stu-id="2e286-192">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="2e286-193">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="2e286-193">$oauth_token_secret</span></span>|<span data-ttu-id="2e286-194">這是您先前記下的 Twitter 應用程式 **存取權杖密碼** 。</span><span class="sxs-lookup"><span data-stu-id="2e286-194">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="2e286-195">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="2e286-195">$destBlobName</span></span>|<span data-ttu-id="2e286-196">這是輸出 Blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="2e286-196">This is the output blob name.</span></span> <span data-ttu-id="2e286-197">預設值為 **tutorials/twitter/data/tweets.txt**。</span><span class="sxs-lookup"><span data-stu-id="2e286-197">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="2e286-198">如果您變更預設值，則 Windows PowerShell 指令碼也必須隨之變更。</span><span class="sxs-lookup"><span data-stu-id="2e286-198">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="2e286-199">$trackString</span><span class="sxs-lookup"><span data-stu-id="2e286-199">$trackString</span></span>|<span data-ttu-id="2e286-200">Web 服務會傳回這些關鍵字的相關推文。</span><span class="sxs-lookup"><span data-stu-id="2e286-200">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="2e286-201">預設值為 **Azure, Cloud, HDInsight**。</span><span class="sxs-lookup"><span data-stu-id="2e286-201">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="2e286-202">如果您變更預設值，則 Windows PowerShell 指令碼也要隨之變更。</span><span class="sxs-lookup"><span data-stu-id="2e286-202">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="2e286-203">$lineMax</span><span class="sxs-lookup"><span data-stu-id="2e286-203">$lineMax</span></span>|<span data-ttu-id="2e286-204">此值會決定指令碼所將讀取的推文數。</span><span class="sxs-lookup"><span data-stu-id="2e286-204">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="2e286-205">讀取 100 則推文大約需要三分鐘。</span><span class="sxs-lookup"><span data-stu-id="2e286-205">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="2e286-206">您可以設定更大的數目，但下載時間將會較久。</span><span class="sxs-lookup"><span data-stu-id="2e286-206">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="2e286-207">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="2e286-207">Press **F5** to run the script.</span></span> <span data-ttu-id="2e286-208">如果發生問題，請選取所有程式碼行，然後按 **F8**，以解決問題。</span><span class="sxs-lookup"><span data-stu-id="2e286-208">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="2e286-209">輸出的結尾應會顯示「完成！</span><span class="sxs-lookup"><span data-stu-id="2e286-209">You shall see "Complete!"</span></span> <span data-ttu-id="2e286-210">」。</span><span class="sxs-lookup"><span data-stu-id="2e286-210">at the end of the output.</span></span> <span data-ttu-id="2e286-211">錯誤訊息會顯示為紅色。</span><span class="sxs-lookup"><span data-stu-id="2e286-211">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="2e286-212">在驗證程序中，您可以使用 Azure 儲存體總管或 Azure PowerShell，在您的 Azure Blob 儲存體上查看輸出檔案 **/tutorials/twitter/data/tweets.txt**。</span><span class="sxs-lookup"><span data-stu-id="2e286-212">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="2e286-213">如需用於列出這些檔案的範例 Windows PowerShell 指令碼，請參閱[搭配 HDInsight 使用 Blob 儲存體][hdinsight-storage-powershell]。</span><span class="sxs-lookup"><span data-stu-id="2e286-213">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="2e286-214">建立 HiveQL 指令碼</span><span class="sxs-lookup"><span data-stu-id="2e286-214">Create HiveQL script</span></span>
<span data-ttu-id="2e286-215">使用 Azure PowerShell 可讓您逐一執行多個 HiveQL 陳述式，或將 HiveQL 陳述式封裝到指令碼檔案中。</span><span class="sxs-lookup"><span data-stu-id="2e286-215">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="2e286-216">在本教學課程中，您將會建立 HiveQL 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2e286-216">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="2e286-217">指令碼檔案必須上傳至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2e286-217">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="2e286-218">在下一節中，您將使用 Azure PowerShell 執行指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="2e286-218">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="2e286-219">已在公用 Blob 容器中上傳 Hive 指令碼檔案和含有 10,000 則推文的檔案。</span><span class="sxs-lookup"><span data-stu-id="2e286-219">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="2e286-220">如果想要使用上傳的檔案，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="2e286-220">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="2e286-221">HiveQL 指令碼將執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="2e286-221">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="2e286-222">**捨棄 tweets_raw 資料表** (若此資料表已存在)。</span><span class="sxs-lookup"><span data-stu-id="2e286-222">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="2e286-223">**建立 tweets_raw Hive 資料表**。</span><span class="sxs-lookup"><span data-stu-id="2e286-223">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="2e286-224">這個暫時的 Hive 結構化資料表會保存要進一步進行擷取、轉換和載入 (ETL) 處理的資料。</span><span class="sxs-lookup"><span data-stu-id="2e286-224">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="2e286-225">如需資料分割的相關資訊，請參閱 [Hive 教學課程][apache-hive-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="2e286-225">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="2e286-226">**載入資料** 。</span><span class="sxs-lookup"><span data-stu-id="2e286-226">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="2e286-227">巢狀 JSON 格式的大型 Tweets 資料集現在已轉換成暫時的 Hive 資料表結構。</span><span class="sxs-lookup"><span data-stu-id="2e286-227">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="2e286-228">**捨棄 tweets 資料表** (若此資料表已存在)。</span><span class="sxs-lookup"><span data-stu-id="2e286-228">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="2e286-229">**建立 tweets 資料表**。</span><span class="sxs-lookup"><span data-stu-id="2e286-229">**Create the tweets table**.</span></span> <span data-ttu-id="2e286-230">您必須先執行另一個 ETL 程序，才能使用 Hive 來查詢 Tweets 資料集。</span><span class="sxs-lookup"><span data-stu-id="2e286-230">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="2e286-231">此 ETL 程序針對您在 "twitter_raw" 資料表中儲存的資料，定義了更詳細的資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="2e286-231">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="2e286-232">**插入覆寫資料表**。</span><span class="sxs-lookup"><span data-stu-id="2e286-232">**Insert overwrite table**.</span></span> <span data-ttu-id="2e286-233">這個複雜的 Hive 指令碼會啟動一組冗長的 MapReduce 工作 (由 Hadoop 叢集執行)。</span><span class="sxs-lookup"><span data-stu-id="2e286-233">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="2e286-234">根據資料集和叢集大小而定，這可能需要 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="2e286-234">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="2e286-235">**插入覆寫目錄**。</span><span class="sxs-lookup"><span data-stu-id="2e286-235">**Insert overwrite directory**.</span></span> <span data-ttu-id="2e286-236">執行查詢，並將資料集輸出至檔案。</span><span class="sxs-lookup"><span data-stu-id="2e286-236">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="2e286-237">此查詢會傳回一份 Twitter 使用者清單，這些使用者傳送了最多含有 "Azure" 一字的推文。</span><span class="sxs-lookup"><span data-stu-id="2e286-237">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="2e286-238">**建立 Hive 指令碼並將它上傳至 Azure**</span><span class="sxs-lookup"><span data-stu-id="2e286-238">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="2e286-239">開啟 Windows PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="2e286-239">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="2e286-240">將下列指令碼複製到指令碼窗格中：</span><span class="sxs-lookup"><span data-stu-id="2e286-240">Copy the following script into the script pane:</span></span>

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="2e286-241">設定指令碼中的前兩個變數：</span><span class="sxs-lookup"><span data-stu-id="2e286-241">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="2e286-242">變數</span><span class="sxs-lookup"><span data-stu-id="2e286-242">Variable</span></span> | <span data-ttu-id="2e286-243">說明</span><span class="sxs-lookup"><span data-stu-id="2e286-243">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="2e286-244">$clusterName</span><span class="sxs-lookup"><span data-stu-id="2e286-244">$clusterName</span></span> |<span data-ttu-id="2e286-245"># 提供您要在其中執行 Hive 工作的 HDInsight 叢集名稱</span><span class="sxs-lookup"><span data-stu-id="2e286-245">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="2e286-246">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="2e286-246">$subscriptionID</span></span> |<span data-ttu-id="2e286-247">輸入您的 Azure 訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="2e286-247">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="2e286-248">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="2e286-248">$sourceDataPath</span></span> |<span data-ttu-id="2e286-249">Hive 查詢將從中讀取資料的 Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="2e286-249">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="2e286-250">您無須變更此變數。</span><span class="sxs-lookup"><span data-stu-id="2e286-250">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="2e286-251">$outputPath</span><span class="sxs-lookup"><span data-stu-id="2e286-251">$outputPath</span></span> |<span data-ttu-id="2e286-252">Hive 查詢將輸出結果的 Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="2e286-252">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="2e286-253">您無須變更此變數。</span><span class="sxs-lookup"><span data-stu-id="2e286-253">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="2e286-254">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="2e286-254">$hqlScriptFile</span></span> |<span data-ttu-id="2e286-255">HiveQL 指令碼檔案的位置和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="2e286-255">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="2e286-256">您無須變更此變數。</span><span class="sxs-lookup"><span data-stu-id="2e286-256">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="2e286-257">按 **F5** 以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="2e286-257">Press **F5** to run the script.</span></span> <span data-ttu-id="2e286-258">如果發生問題，請選取所有程式碼行，然後按 **F8**，以解決問題。</span><span class="sxs-lookup"><span data-stu-id="2e286-258">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="2e286-259">輸出的結尾應會顯示「完成！</span><span class="sxs-lookup"><span data-stu-id="2e286-259">You shall see "Complete!"</span></span> <span data-ttu-id="2e286-260">」。</span><span class="sxs-lookup"><span data-stu-id="2e286-260">at the end of the output.</span></span> <span data-ttu-id="2e286-261">錯誤訊息會顯示為紅色。</span><span class="sxs-lookup"><span data-stu-id="2e286-261">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="2e286-262">在驗證程序中，您可以使用 Azure 儲存體總管或 Azure PowerShell，在您的 Azure Blob 儲存體上查看輸出檔案 **/tutorials/twitter/twitter.hql**。</span><span class="sxs-lookup"><span data-stu-id="2e286-262">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="2e286-263">如需用於列出這些檔案的範例 Windows PowerShell 指令碼，請參閱[搭配 HDInsight 使用 Blob 儲存體][hdinsight-storage-powershell]。</span><span class="sxs-lookup"><span data-stu-id="2e286-263">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="2e286-264">使用 Hive 處理 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="2e286-264">Process Twitter data by using Hive</span></span>
<span data-ttu-id="2e286-265">您已完成所有準備工作。</span><span class="sxs-lookup"><span data-stu-id="2e286-265">You have finished all the preparation work.</span></span> <span data-ttu-id="2e286-266">現在，您可以叫用 Hive 指令碼，並查看結果。</span><span class="sxs-lookup"><span data-stu-id="2e286-266">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="2e286-267">提交 Hive 工作</span><span class="sxs-lookup"><span data-stu-id="2e286-267">Submit a Hive job</span></span>
<span data-ttu-id="2e286-268">使用下列 Window PowerShell 指令碼可執行 Hive 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2e286-268">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="2e286-269">您必須設定第一個變數。</span><span class="sxs-lookup"><span data-stu-id="2e286-269">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="2e286-270">若要使用您在上兩節中上傳的推文和 HiveQL 指令碼，請將 $hqlScriptFile 設定為 "/tutorials/twitter/twitter.hql"。</span><span class="sxs-lookup"><span data-stu-id="2e286-270">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="2e286-271">若要使用已上傳至公用 Blob 的項目，請將 $hqlScriptFile 設定為 "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"。</span><span class="sxs-lookup"><span data-stu-id="2e286-271">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
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

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="2e286-272">查看結果</span><span class="sxs-lookup"><span data-stu-id="2e286-272">Check the results</span></span>
<span data-ttu-id="2e286-273">使用下列 Windows PowerShell 指令碼可查看 Hive 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="2e286-273">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="2e286-274">您必須設定前兩個變數。</span><span class="sxs-lookup"><span data-stu-id="2e286-274">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
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
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> Hive 資料表會使用 \001 做為欄位分隔符號。 <span data-ttu-id="2e286-276">此分隔符號不會顯示在輸出中。</span><span class="sxs-lookup"><span data-stu-id="2e286-276">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="2e286-277">分析結果列示在 Azure Blob 儲存體之後，您可以將資料匯出至 Azure SQL Database/SQL Server，使用 Power Query 將資料匯出至 Excel，或使用 Hive ODBC 驅動程式將應用程式連接到資料。</span><span class="sxs-lookup"><span data-stu-id="2e286-277">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="2e286-278">如需詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]、[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-delay-data]、[使用 Power Query 將 Excel 連接到 HDInsight][hdinsight-power-query] 和[使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 HDInsight][hdinsight-hive-odbc]。</span><span class="sxs-lookup"><span data-stu-id="2e286-278">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e286-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e286-279">Next steps</span></span>
<span data-ttu-id="2e286-280">本教學課程中，我們看到如何將非結構化 JSON 資料集轉換成結構化 Hive 資料表，然後在 Azure 上使用 HDInsight 來查詢、探索和分析來自 Twitter 的資料。</span><span class="sxs-lookup"><span data-stu-id="2e286-280">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="2e286-281">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="2e286-281">To learn more, see:</span></span>

* <span data-ttu-id="2e286-282">[開始使用 HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2e286-282">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="2e286-283">[使用 HDInsight 中的 HBase 分析即時的 Twitter 情感][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="2e286-283">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="2e286-284">[使用 HDInsight 分析航班延誤資料][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="2e286-284">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="2e286-285">[使用 Power Query 將 Excel 連接到 HDInsight][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="2e286-285">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="2e286-286">[使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 HDInsight][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="2e286-286">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="2e286-287">[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="2e286-287">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
