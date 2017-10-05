---
title: "使用 Hive 和 Hadoop 進行網站記錄分析 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 HDInsight 上的 Hive 來分析網站記錄。 您將使用記錄檔做為 HDInsight 資料表的輸入，然後使用 HiveQL 來查詢資料。"
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
ms.openlocfilehash: e1cdb786bb6049980aafc0213abf53013e342618
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="c6371-104">使用 Windows 型 HDInsight 上的 Hive 分析網站的記錄</span><span class="sxs-lookup"><span data-stu-id="c6371-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="c6371-105">了解如何使用 HDInsight 上的 HiveQL 來分析網站的記錄。</span><span class="sxs-lookup"><span data-stu-id="c6371-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="c6371-106">網站記錄分析可用於根據類似活動來區隔對象、依人口統計將網站造訪者分類，以及找出他們檢視的內容、他們來自的網站等。</span><span class="sxs-lookup"><span data-stu-id="c6371-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6371-107">本文件的步驟只適用於 Windows HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6371-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c6371-108">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="c6371-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="c6371-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c6371-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c6371-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c6371-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c6371-111">在此範例中，您將使用 HDInsight 叢集來分析網站記錄檔，以深入了解一天內從外部網站的網站造訪頻率。</span><span class="sxs-lookup"><span data-stu-id="c6371-111">In this sample, you will use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="c6371-112">也將產生使用者遇到的網站錯誤摘要。</span><span class="sxs-lookup"><span data-stu-id="c6371-112">You'll also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="c6371-113">您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="c6371-113">You will learn how to:</span></span>

* <span data-ttu-id="c6371-114">連接至包含網站記錄檔的 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c6371-114">Connect to a Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="c6371-115">建立 Hive 資料表以查詢這些記錄。</span><span class="sxs-lookup"><span data-stu-id="c6371-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="c6371-116">建立 Hive 查詢以分析資料。</span><span class="sxs-lookup"><span data-stu-id="c6371-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="c6371-117">使用 Microsoft Excel 連接到 HDInsight (使用開放式資料庫連接，ODBC) 擷取已分析的資料。</span><span class="sxs-lookup"><span data-stu-id="c6371-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis][img-hdi-weblogs-sample]

## <a name="prerequisites"></a><span data-ttu-id="c6371-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="c6371-119">Prerequisites</span></span>
* <span data-ttu-id="c6371-120">您必須已在 Azure HDInsight 上佈建 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="c6371-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="c6371-121">如需指示，請參閱 [佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="c6371-121">For instructions, see [Provision HDInsight Clusters][hdinsight-provision].</span></span>
* <span data-ttu-id="c6371-122">您必須已安裝 Microsoft Excel 2013 或 Excel 2010。</span><span class="sxs-lookup"><span data-stu-id="c6371-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="c6371-123">您必須有 [Microsoft Hive ODBC 驅動程式](http://www.microsoft.com/download/details.aspx?id=40886) ，才能從 Hive 將資料匯入 Excel 中。</span><span class="sxs-lookup"><span data-stu-id="c6371-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="c6371-124">執行範例</span><span class="sxs-lookup"><span data-stu-id="c6371-124">To run the sample</span></span>
1. <span data-ttu-id="c6371-125">從 [Azure 入口網站](https://portal.azure.com/)的 開始面板 (若您已在該處釘選叢集)，按一下您要在其中執行範例的叢集磚。</span><span class="sxs-lookup"><span data-stu-id="c6371-125">From the [Azure Portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="c6371-126">在叢集刀鋒視窗的 [快速連結] 之下，按一下 [叢集儀表板]，然後從 [叢集儀表板] 刀鋒視窗按一下 [HDInsight 叢集儀表板]。</span><span class="sxs-lookup"><span data-stu-id="c6371-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="c6371-127">或者，您也可以使用下列 URL 直接開啟儀表板：</span><span class="sxs-lookup"><span data-stu-id="c6371-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="c6371-128">出現提示時，使用您佈建叢集時所用的系統管理員使用者名稱和密碼來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="c6371-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="c6371-129">從開啟的網頁中，按一下 [快速啟用資源庫] 索引標籤，然後在 [搭配範例資料的方案] 類別下，按一下 [網站記錄分析] 範例。</span><span class="sxs-lookup"><span data-stu-id="c6371-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="c6371-130">依照網頁上提供的指示完成範例。</span><span class="sxs-lookup"><span data-stu-id="c6371-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6371-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6371-131">Next steps</span></span>
<span data-ttu-id="c6371-132">嘗試下列範例： [使用 Hive 和 HDInsight 分析感應器資料](hdinsight-hive-analyze-sensor-data.md)。</span><span class="sxs-lookup"><span data-stu-id="c6371-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](hdinsight-hive-analyze-sensor-data.md).</span></span>

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md

[img-hdi-weblogs-sample]: ./media/hdinsight-hive-analyze-website-log/hdinsight-weblogs-sample.png
