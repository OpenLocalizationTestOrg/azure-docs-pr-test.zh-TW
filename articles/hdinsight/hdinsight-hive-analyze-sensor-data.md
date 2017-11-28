---
title: "使用 Hive 及 Hadoop 分析感應器資料 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Hive 查詢主控台搭配 HDInsight (Hadoop) 分析感應器資料，然後在 Microsoft Excel 中使用 Power View 將資料視覺化。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 3abb71c12b4769bebd808276f8bdd832aad22d7a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="212b0-103">在 HDInsight 的 Hadoop 上使用 Hive 查詢主控台分析感應器資料</span><span class="sxs-lookup"><span data-stu-id="212b0-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="212b0-104">了解如何使用 Hive 查詢主控台搭配 HDInsight (Hadoop) 分析感應器資料，然後在 Microsoft Excel 中使用 Power View 將資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="212b0-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="212b0-105">本文件的步驟只適用於 Windows HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="212b0-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="212b0-106">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="212b0-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="212b0-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="212b0-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="212b0-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="212b0-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="212b0-109">在此範例中，您會使用 Hive 來處理歷程記錄資料，並找出暖氣及空調系統的問題。</span><span class="sxs-lookup"><span data-stu-id="212b0-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="212b0-110">具體而言，您會執行下列工作，找出無法穩定維持所設定之溫度的系統：</span><span class="sxs-lookup"><span data-stu-id="212b0-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="212b0-111">建立 Hive 資料表來查詢逗點分隔值 (CSV) 檔案中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="212b0-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="212b0-112">建立 Hive 查詢以分析資料。</span><span class="sxs-lookup"><span data-stu-id="212b0-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="212b0-113">若要擷取已分析的資料，請使用 Microsoft Excel 連接到 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="212b0-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="212b0-114">若要將資料視覺化，請使用 Power View。</span><span class="sxs-lookup"><span data-stu-id="212b0-114">To visualize the data, use Power View.</span></span>

![A diagram of the solution architecture](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="212b0-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="212b0-116">Prerequisites</span></span>

* <span data-ttu-id="212b0-117">HDInsight (Hadoop) 叢集：如需建立叢集的相關資訊，請參閱 [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="212b0-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="212b0-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="212b0-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="212b0-119">Microsoft Excel 用於搭配 [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US)進行資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="212b0-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="212b0-120">Microsoft Hive ODBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="212b0-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="212b0-121">執行範例</span><span class="sxs-lookup"><span data-stu-id="212b0-121">To run the sample</span></span>

1. <span data-ttu-id="212b0-122">請使用網頁瀏覽器瀏覽至下列 URL：</span><span class="sxs-lookup"><span data-stu-id="212b0-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="212b0-123">將 `<clustername>` 替換為 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="212b0-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="212b0-124">出現提示時，使用您佈建此叢集時所用的系統管理員使用者名稱和密碼來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="212b0-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="212b0-125">從開啟的網頁中，按一下 [Getting Started Gallery] 索引標籤，然後在 [搭配範例資料的方案] 類別下，按一下 [感應器資料分析] 範例。</span><span class="sxs-lookup"><span data-stu-id="212b0-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![開始使用資源庫映像](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="212b0-127">依照網頁上提供的指示完成範例。</span><span class="sxs-lookup"><span data-stu-id="212b0-127">Follow the instructions provided on the web page to finish the sample.</span></span>
