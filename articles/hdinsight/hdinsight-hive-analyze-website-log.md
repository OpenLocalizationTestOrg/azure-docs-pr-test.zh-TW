---
title: "對網站記錄分析 Azure HDInsight 的 Hive 與 Hadoop aaaUse |Microsoft 文件"
description: "了解 toouse Hive 與 HDInsight tooanalyze 網站的記錄檔。 您將使用做為輸入到 HDInsight 資料表中，記錄檔，並使用 HiveQL tooquery hello 資料。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6fb7b5c2-8df4-40b1-a9e2-6815080004f9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 9cbce3cc8cf8bc3ad104dc4ca6a5628802c8fe89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-windows-based-hdinsight-tooanalyze-logs-from-websites"></a><span data-ttu-id="e0ec4-104">使用以 Windows 為基礎的 HDInsight tooanalyze 記錄檔，從網站的登錄區</span><span class="sxs-lookup"><span data-stu-id="e0ec4-104">Use Hive with Windows-based HDInsight tooanalyze logs from websites</span></span>
<span data-ttu-id="e0ec4-105">了解與 HDInsight tooanalyze toouse HiveQL 從網站的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-105">Learn how toouse HiveQL with HDInsight tooanalyze logs from a website.</span></span> <span data-ttu-id="e0ec4-106">網站記錄分析可使用的 toosegment 觀眾根據類似的活動，分類人口統計資料和 toofind 出 hello 他們所檢視的內容，它們來自，hello 網站以及等等的站台訪客。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-106">Website log analysis can be used toosegment your audience based on similar activities, categorize site visitors by demographics, and toofind out hello content they view, hello websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0ec4-107">hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-107">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="e0ec4-108">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="e0ec4-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e0ec4-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="e0ec4-111">在此範例中，您將使用 HDInsight 叢集 tooanalyze 網站記錄檔 tooget 深入了解 hello 頻率造訪 toohello 網站，從外部網站一天。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-111">In this sample, you will use an HDInsight cluster tooanalyze website log files tooget insight into hello frequency of visits toohello website from external websites in a day.</span></span> <span data-ttu-id="e0ec4-112">您也將產生 hello 使用者遇到的網站錯誤的摘要。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-112">You'll also generate a summary of website errors that hello users experience.</span></span> <span data-ttu-id="e0ec4-113">您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="e0ec4-113">You will learn how to:</span></span>

* <span data-ttu-id="e0ec4-114">連接 tooa Azure Blob 儲存體，其中包含網站記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-114">Connect tooa Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="e0ec4-115">建立 HIVE 資料表 tooquery 這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-115">Create HIVE tables tooquery those logs.</span></span>
* <span data-ttu-id="e0ec4-116">建立 HIVE 查詢 tooanalyze hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-116">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="e0ec4-117">使用 Microsoft Excel tooconnect tooHDInsight （藉由使用開放式資料庫連接 (ODBC) tooretrieve hello 分析資料。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-117">Use Microsoft Excel tooconnect tooHDInsight (by using open database connectivity (ODBC) tooretrieve hello analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="e0ec4-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="e0ec4-119">Prerequisites</span></span>
* <span data-ttu-id="e0ec4-120">您必須已在 Azure HDInsight 上佈建 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="e0ec4-121">如需指示，請參閱 [佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="e0ec4-122">您必須已安裝 Microsoft Excel 2013 或 Excel 2010。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="e0ec4-123">您必須擁有[Microsoft Hive ODBC 驅動程式](http://www.microsoft.com/download/details.aspx?id=40886)tooimport Hive 到 Excel 的資料。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) tooimport data from Hive into Excel.</span></span>

## <a name="toorun-hello-sample"></a><span data-ttu-id="e0ec4-124">toorun hello 範例</span><span class="sxs-lookup"><span data-stu-id="e0ec4-124">toorun hello sample</span></span>
1. <span data-ttu-id="e0ec4-125">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello （如果您釘選 hello 叢集那里） 的開始面板，按一下 要 toorun hello 範例 hello 叢集磚。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-125">From hello [Azure Portal](https://portal.azure.com/), from hello Startboard (if you pinned hello cluster there), click hello cluster tile on which you want toorun hello sample.</span></span>
2. <span data-ttu-id="e0ec4-126">從 hello 叢集刀鋒視窗中，在**快速連結**，按一下 **叢集儀表板**，然後從 hello**叢集儀表板**刀鋒視窗中，按一下  **HDInsight 叢集儀表板**。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-126">From hello cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from hello **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="e0ec4-127">或者，您可以使用下列 URL 的 hello 直接開啟 hello 儀表板：</span><span class="sxs-lookup"><span data-stu-id="e0ec4-127">Alternatively, you can directly open hello dashboard by using hello following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="e0ec4-128">出現提示時，使用 hello 系統管理員使用者名稱和佈建 hello 叢集時所使用的密碼驗證。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-128">When prompted, authenticate by using hello administrator user name and password you used when provisioning hello cluster.</span></span>
3. <span data-ttu-id="e0ec4-129">從開啟的 hello 網頁上，按一下 [hello**快速入口圖庫**] 索引標籤，然後在 hello**解決方案的範例資料**分類中，按一下 hello**網站記錄檔分析**範例。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-129">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="e0ec4-130">請遵循 hello hello 網頁 toofinish hello 範例上所提供的指示。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-130">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0ec4-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0ec4-131">Next steps</span></span>
<span data-ttu-id="e0ec4-132">請嘗試下列範例中的 hello:[分析感應器資料使用 HDInsight 的 Hive](hdinsight-hive-analyze-sensor-data.md)。</span><span class="sxs-lookup"><span data-stu-id="e0ec4-132">Try hello following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
