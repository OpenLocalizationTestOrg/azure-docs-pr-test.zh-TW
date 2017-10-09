---
title: "使用 Hive 和 Hadoop-Azure HDInsight aaaAnalyze 感應器資料 |Microsoft 文件"
description: "了解如何使用 tooanalyze 感應器資料 hello Hive 查詢主控台與 HDInsight (Hadoop)，然後在 Microsoft Excel 中使用 PowerView hello 資料視覺化。"
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
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="9e9ef-103">分析在 HDInsight 中的 Hadoop 使用 hello Hive 查詢主控台感應器資料</span><span class="sxs-lookup"><span data-stu-id="9e9ef-103">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="9e9ef-104">了解如何使用 tooanalyze 感應器資料 hello Hive 查詢主控台與 HDInsight (Hadoop)，然後使用 Power View 在 Microsoft Excel 中的 hello 資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-104">Learn how tooanalyze sensor data by using hello Hive Query Console with HDInsight (Hadoop), then visualize hello data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e9ef-105">hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="9e9ef-106">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="9e9ef-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9e9ef-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="9e9ef-109">在此範例中，您可以使用 Hive tooprocess 歷程記錄資料，並找出問題與暖氣和空調系統。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-109">In this sample, you use Hive tooprocess historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="9e9ef-110">具體來說，必須識別系統是無法 tooreliably 維護組溫度藉由執行下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e9ef-110">Specifically, you identify systems are not able tooreliably maintain a set temperature by performing hello following tasks:</span></span>

* <span data-ttu-id="9e9ef-111">建立 HIVE 資料表 tooquery 資料儲存在逗號分隔值 (CSV) 檔案。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-111">Create HIVE tables tooquery data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="9e9ef-112">建立 HIVE 查詢 tooanalyze hello 資料。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-112">Create HIVE queries tooanalyze hello data.</span></span>
* <span data-ttu-id="9e9ef-113">tooretrieve hello 分析資料，請使用 Microsoft Excel tooconnect tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-113">tooretrieve hello analyzed data, use Microsoft Excel tooconnect tooHDInsight.</span></span>
* <span data-ttu-id="9e9ef-114">toovisualize hello 資料，請使用 Power View。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-114">toovisualize hello data, use Power View.</span></span>

![Hello 方案架構圖](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="9e9ef-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e9ef-116">Prerequisites</span></span>

* <span data-ttu-id="9e9ef-117">HDInsight (Hadoop) 叢集：如需建立叢集的相關資訊，請參閱 [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="9e9ef-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="9e9ef-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="9e9ef-119">Microsoft Excel 用於搭配 [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US)進行資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="9e9ef-120">Microsoft Hive ODBC 驅動程式</span><span class="sxs-lookup"><span data-stu-id="9e9ef-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a><span data-ttu-id="9e9ef-121">toorun hello 範例</span><span class="sxs-lookup"><span data-stu-id="9e9ef-121">toorun hello sample</span></span>

1. <span data-ttu-id="9e9ef-122">從您網頁瀏覽器中，瀏覽 toohello 下列 URL:</span><span class="sxs-lookup"><span data-stu-id="9e9ef-122">From your web browser, navigate toohello following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="9e9ef-123">取代`<clustername>`hello 名稱，為您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-123">Replace `<clustername>` with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="9e9ef-124">出現提示時，使用 hello 系統管理員使用者名稱和密碼時佈建此叢集所使用驗證。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-124">When prompted, authenticate by using hello administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="9e9ef-125">從開啟的 hello 網頁上，按一下 [hello**快速入口圖庫**] 索引標籤，然後在 hello**解決方案的範例資料**分類中，按一下 hello**感應器資料分析**範例。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-125">From hello web page that opens, click hello **Getting Started Gallery** tab, and then under hello **Solutions with Sample Data** category, click hello **Sensor Data Analysis** sample.</span></span>

    ![開始使用資源庫映像](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="9e9ef-127">請遵循 hello hello 網頁 toofinish hello 範例上所提供的指示。</span><span class="sxs-lookup"><span data-stu-id="9e9ef-127">Follow hello instructions provided on hello web page toofinish hello sample.</span></span>
