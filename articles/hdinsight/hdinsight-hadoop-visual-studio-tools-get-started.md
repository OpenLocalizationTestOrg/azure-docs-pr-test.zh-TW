---
title: "使用 Data Lake Tools for Visual Studio 連線至 Azure HDInsight | Microsoft Docs"
description: "了解如何安裝和使用 Data Lake Tools for Visual Studio 來連線到 Azure HDInsight 中的 Hadoop 叢集及執行 Hive 查詢。"
keywords: "hadoop 工具,hive 查詢,visual studio,visual studio hadoop"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: f7eff70ece5e8dc7e0c5983871d40bd1f6eafff2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-azure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="01cba-104">使用 Data Lake Tools for Visual Studio 連線至 Azure HDInsight 及執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="01cba-104">Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio</span></span>

<span data-ttu-id="01cba-105">了解如何使用 Data Lake Tools for Visual Studio 來連線到 [Azure HDInsight](hdinsight-hadoop-introduction.md) 中的 Hadoop 叢集及提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-105">Learn how to use Data Lake Tools for Visual Studio to connect to Hadoop clusters in [Azure HDInsight](hdinsight-hadoop-introduction.md) and submit Hive queries.</span></span> <span data-ttu-id="01cba-106">如需使用 HDInsight 的詳細資訊，請參閱 [HDInsight 簡介](hdinsight-hadoop-introduction.md)和[開始使用 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-106">For more information about using HDInsight, see [Introduction to HDInsight](hdinsight-hadoop-introduction.md) and [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span> <span data-ttu-id="01cba-107">如需連線到 Storm 叢集的詳細資訊，請參閱[使用 Visual Studio 開發 HDInsight 上 Apache Storm 的 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-107">For more information about connecting to a Storm cluster, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="01cba-108">Data Lake Tools for Visual Studio 可用來存取 Data Lake Analytics 和 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="01cba-108">Data Lake Tools for Visual Studio can be used to access both Data Lake Analytics and HDInsight.</span></span>  <span data-ttu-id="01cba-109">如需 Data Lake Tools 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-109">For the information about Data Lake Tools, see [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).</span></span>

<span data-ttu-id="01cba-110">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="01cba-110">**Prerequisites**</span></span>

<span data-ttu-id="01cba-111">若要完成本教學課程並使用 Visual Studio 中的 Data Lake Tools，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="01cba-111">To complete this tutorial and use the Data Lake Tools in Visual Studio, you'll need the following:</span></span>

* <span data-ttu-id="01cba-112">Azure HDInsight 叢集︰若要建立叢集，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="01cba-112">An Azure HDInsight cluster: To create one, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>
* <span data-ttu-id="01cba-113">已安裝下列軟體的工作站：</span><span class="sxs-lookup"><span data-stu-id="01cba-113">A workstation with the following software:</span></span>
  
  * <span data-ttu-id="01cba-114">Windows 10、Windows 8.1、Windows 8 或 Windows 7。</span><span class="sxs-lookup"><span data-stu-id="01cba-114">Windows 10, Windows 8.1, Windows 8, or Windows 7.</span></span>
  * <span data-ttu-id="01cba-115">Visual Studio 2013/2015/2017。</span><span class="sxs-lookup"><span data-stu-id="01cba-115">Visual Studio 2013/2015/2017.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="01cba-116">Data Lake Tools for Visual Studio 目前只有英文版。</span><span class="sxs-lookup"><span data-stu-id="01cba-116">Currently, the Data Lake Tools for Visual Studio only come with the English version.</span></span>
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="01cba-117">安裝 Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01cba-117">Install Data Lake Tools for Visual Studio</span></span>

<span data-ttu-id="01cba-118">預設會針對 Visual Studio 2017 安裝 Data Lake Tools。</span><span class="sxs-lookup"><span data-stu-id="01cba-118">Data Lake Tools is installed by default for Visual Studio 2017.</span></span> <span data-ttu-id="01cba-119">對於較舊版本，您可以使用 [Web Platform Installer](https://www.microsoft.com/web/downloads/) 來安裝。</span><span class="sxs-lookup"><span data-stu-id="01cba-119">For older versions, you can install it using the [Web Platform Installer](https://www.microsoft.com/web/downloads/).</span></span> <span data-ttu-id="01cba-120">您必須選擇與 Visual Studio 版本相符的封裝。</span><span class="sxs-lookup"><span data-stu-id="01cba-120">You must choose the one that matches your version of Visual Studio.</span></span> <span data-ttu-id="01cba-121">如果您沒有安裝 Visual Studio，可以使用 [Web Platform Installer](https://www.microsoft.com/web/downloads/)，來安裝最新的 Visual Studio Community 和 Azure SDK：</span><span class="sxs-lookup"><span data-stu-id="01cba-121">If you don't have Visual Studio installed, you can install the latest Visual Studio Community and Azure SDK using the [Web Platform Installer](https://www.microsoft.com/web/downloads/):</span></span>

<span data-ttu-id="01cba-122">![Data Lake Tools for Visual Studio Web 平台安裝程式。](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "使用 Web 平台安裝程式來安裝 Data Lake Tools for Visual Studio")</span><span class="sxs-lookup"><span data-stu-id="01cba-122">![Data Lake Tools for Visual Studio Web Platform installer.](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Use Web Platform Installer to install Data Lake Tools for Visual Studio")</span></span>

## <a name="connect-to-azure-subscriptions"></a><span data-ttu-id="01cba-123">連線到 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="01cba-123">Connect to Azure subscriptions</span></span>
<span data-ttu-id="01cba-124">Data Lake Tools for Visual Studio 可讓您連線到您的 HDInsight 叢集、執行一些基本管理作業，以及執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-124">Data Lake Tools for Visual Studio allows you to connect to your HDInsight clusters, perform some basic management operations, and run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="01cba-125">如需連線到一般 Hadoop 叢集的相關資訊，請參閱 [使用 Visual Studio 撰寫和提交 Hive 查詢](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx)。</span><span class="sxs-lookup"><span data-stu-id="01cba-125">For information on connecting to a generic Hadoop cluster, see [Write and submit Hive queries using Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).</span></span>
> 
> 

<span data-ttu-id="01cba-126">**連線到您的 Azure 訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="01cba-126">**To connect to your Azure subscription**</span></span>

1. <span data-ttu-id="01cba-127">開啟 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="01cba-127">Open Visual Studio.</span></span>
2. <span data-ttu-id="01cba-128">從 [檢視] 功能表中，按一下 [伺服器總管] 以開啟 [伺服器總管] 視窗。</span><span class="sxs-lookup"><span data-stu-id="01cba-128">From the **View** menu, click **Server Explorer** to open the Server Explorer window.</span></span>
3. <span data-ttu-id="01cba-129">展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="01cba-129">Expand **Azure**, and then expand **HDInsight**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01cba-130">請注意，[HDInsight 工作清單] 視窗此時應該會開啟。</span><span class="sxs-lookup"><span data-stu-id="01cba-130">Notice the **HDInsight Task List** window should be open.</span></span> <span data-ttu-id="01cba-131">如果您沒有看到該視窗，請按一下 [檢視] 功能表的 [其他視窗]，然後按一下 [HDInsight 工作清單視窗]。</span><span class="sxs-lookup"><span data-stu-id="01cba-131">If you don't see it, click **Other Windows** from the **View** menu, and then click **HDInsight Task List Window**.</span></span>  
   > 
   > 
4. <span data-ttu-id="01cba-132">輸入您的 Azure 訂用帳戶認證，然後按一下 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="01cba-132">Enter your Azure subscription credentials, and then click **Sign In**.</span></span> <span data-ttu-id="01cba-133">只有當您從未在此工作站上從 Visual Studio 連線到 Azure 訂用帳戶時，才需要這樣做。</span><span class="sxs-lookup"><span data-stu-id="01cba-133">This is only required if you have never connected to the Azure subscription from Visual Studio on this workstation.</span></span>
5. <span data-ttu-id="01cba-134">在 [伺服器總管] 中，您會看到現有 HDInsight 叢集的清單。</span><span class="sxs-lookup"><span data-stu-id="01cba-134">In Server Explorer, you'll see a list of existing HDInsight clusters.</span></span> <span data-ttu-id="01cba-135">如果您沒有任何叢集，可以使用 Azure 入口網站、Azure PowerShell 或 HDInsight SDK 來建立一個。</span><span class="sxs-lookup"><span data-stu-id="01cba-135">If you don't have any clusters, you can create one by using the Azure portal, Azure PowerShell, or the HDInsight SDK.</span></span> <span data-ttu-id="01cba-136">如需詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-136">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
   
   <span data-ttu-id="01cba-137">![Data Lake Tools for Visual Studio Server Explorer 叢集清單](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Data Lake Tools for Visual Studio Server Explorer")</span><span class="sxs-lookup"><span data-stu-id="01cba-137">![Data Lake Tools for Visual Studio Server Explorer cluster list](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Data Lake Tools for Visual Studio Server Explorer")</span></span>
6. <span data-ttu-id="01cba-138">展開某個 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="01cba-138">Expand an HDInsight cluster.</span></span> <span data-ttu-id="01cba-139">您將會看到 **Hive 資料庫**、預設儲存體帳戶、連結的儲存體帳戶，以及 **Hadoop 服務記錄**。</span><span class="sxs-lookup"><span data-stu-id="01cba-139">You'll see **Hive Databases**, a default storage account, linked storage accounts, and **Hadoop Service log**.</span></span> <span data-ttu-id="01cba-140">您可以進一步展開這些實體。</span><span class="sxs-lookup"><span data-stu-id="01cba-140">You can further expand the entities.</span></span>

<span data-ttu-id="01cba-141">在連線到您的 Azure 訂用帳戶之後，您將可以執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="01cba-141">After you've connected to your Azure subscription, you'll be able to do the following:</span></span>

<span data-ttu-id="01cba-142">**從 Visual Studio 連線到 Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="01cba-142">**To connect to the Azure portal from Visual Studio**</span></span>

* <span data-ttu-id="01cba-143">從 [伺服器總管] 中，展開 [Azure] > [HDInsight]，在 HDInsight 叢集上按一下滑鼠右鍵，然後按一下 [在 Azure 入口網站中管理叢集]。</span><span class="sxs-lookup"><span data-stu-id="01cba-143">From Server Explorer, expand **Azure** > **HDInsight**, right-click an HDInsight cluster, and then click **Manage Cluster in Azure portal**.</span></span>

<span data-ttu-id="01cba-144">**從 Visual Studio 提出問題及提供意見反應**</span><span class="sxs-lookup"><span data-stu-id="01cba-144">**To ask questions and provide feedback from Visual Studio**</span></span>

* <span data-ttu-id="01cba-145">從 [工具] 功能表中，按一下 [HDInsight]，然後按一下 [MSDN 論壇] 來提出問題，或按一下 [提供意見反應]。</span><span class="sxs-lookup"><span data-stu-id="01cba-145">From the **Tools** menu, click **HDInsight**, and then click **MSDN Forum** to ask questions, or click **Give Feedback**.</span></span>

## <a name="navigate-the-linked-resources"></a><span data-ttu-id="01cba-146">瀏覽連結的資源</span><span class="sxs-lookup"><span data-stu-id="01cba-146">Navigate the linked resources</span></span>
<span data-ttu-id="01cba-147">從 [伺服器總管] 中，您可以看到預設的儲存體帳戶，以及任何連結的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="01cba-147">From Server Explorer, you can see the default storage account and any linked storage accounts.</span></span> <span data-ttu-id="01cba-148">如果您展開預設儲存體帳戶，您可以看到儲存體帳戶上的容器。</span><span class="sxs-lookup"><span data-stu-id="01cba-148">If you expand the default storage account, you can see the containers on the storage account.</span></span> <span data-ttu-id="01cba-149">預設儲存體帳戶和預設容器皆已標示。</span><span class="sxs-lookup"><span data-stu-id="01cba-149">The default storage account and the default container are marked.</span></span> <span data-ttu-id="01cba-150">您也可以在任何容器上按一下滑鼠右鍵來檢視該容器。</span><span class="sxs-lookup"><span data-stu-id="01cba-150">You can also right-click any of the containers to view the contents.</span></span>

<span data-ttu-id="01cba-151">![Data Lake Tools for Visual Studio Server Explorer 清單連結資源](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "清單連結資源")</span><span class="sxs-lookup"><span data-stu-id="01cba-151">![Data Lake Tools for Visual Studio server explorer list linked resources](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "list linked resources")</span></span>

<span data-ttu-id="01cba-152">開啟容器之後，您可以使用下列按鈕來上傳、刪除及下載 Blob：</span><span class="sxs-lookup"><span data-stu-id="01cba-152">After opening a container, you can use the following buttons to upload, delete, and download blobs:</span></span>

<span data-ttu-id="01cba-153">![Data Lake Tools for Visual Studio Server Explorer Blob 作業](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "更新、刪除和下載 Blob")</span><span class="sxs-lookup"><span data-stu-id="01cba-153">![Data Lake Tools for Visual Studio server explorer blob operations](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "upload, delete, and download blobs")</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="01cba-154">執行 HIVE 查詢</span><span class="sxs-lookup"><span data-stu-id="01cba-154">Run a Hive query</span></span>
<span data-ttu-id="01cba-155">[Apache Hive](http://hive.apache.org) 是以 Hadoop 為基礎的資料倉儲基礎結構，用來提供資料摘要、查詢和分析。</span><span class="sxs-lookup"><span data-stu-id="01cba-155">[Apache Hive](http://hive.apache.org) is a data warehouse infrastructure built on Hadoop for providing data summarization, queries, and analysis.</span></span> <span data-ttu-id="01cba-156">Data Lake Tools for Visual Studio 支援從 Visual Studio 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-156">Data Lake Tools for Visual Studio supports running Hive queries from Visual Studio.</span></span> <span data-ttu-id="01cba-157">如需 Hive 的詳細資訊，請參閱[使用 Hive 搭配 HDInsight](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-157">For more information about Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="01cba-158">針對 HDInsight 叢集測試 Hive 指令碼十分耗時。</span><span class="sxs-lookup"><span data-stu-id="01cba-158">It is time consuming to test Hive script against an HDInsight cluster.</span></span> <span data-ttu-id="01cba-159">這可能需要數分鐘以上的時間。</span><span class="sxs-lookup"><span data-stu-id="01cba-159">It could take several minutes or more.</span></span> <span data-ttu-id="01cba-160">Data Lake Tools for Visual Studio 可以在本機驗證 Hive 指令碼，而不需要連線到即時叢集。</span><span class="sxs-lookup"><span data-stu-id="01cba-160">Data Lake Tools for Visual Studio is capable of validating Hive script locally without connecting to a live cluster.</span></span>

<span data-ttu-id="01cba-161">Data Lake Tools for Visual Studio 也可讓使用者透過收集和呈現特定 Hive 工作的 YARN 記錄，來查看 Hive 工作的內容。</span><span class="sxs-lookup"><span data-stu-id="01cba-161">Data Lake Tools for Visual Studio also enables users to see what’s inside the Hive job by collecting and surfacing the YARN logs of certain Hive jobs.</span></span>

### <a name="view-the-hivesampletable"></a><span data-ttu-id="01cba-162">檢視 **hivesampletable**</span><span class="sxs-lookup"><span data-stu-id="01cba-162">View the **hivesampletable**</span></span>
<span data-ttu-id="01cba-163">所有 HDInsight 叢集皆隨附一個稱為 *hivesampletable*的範例 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="01cba-163">All HDInsight clusters come with a sample Hive table called *hivesampletable*.</span></span> <span data-ttu-id="01cba-164">我們將使用此資料表來示範如何列出 Hive 資料表、檢視資料表結構描述，以及列出 Hive 資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="01cba-164">We'll use this table to show you how to list Hive tables, view the table schemas, and list the rows in the Hive table.</span></span>

<span data-ttu-id="01cba-165">**列出 Hive 資料表和檢視 Hive 資料表結構描述**</span><span class="sxs-lookup"><span data-stu-id="01cba-165">**To list Hive tables and view Hive table schema**</span></span>

1. <span data-ttu-id="01cba-166">從 [伺服器總管] 中，展開 [Azure] > [HDInsight] > 選擇的叢集 > [Hive 資料庫] > [預設] > [hivesampletable] 來查看資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="01cba-166">From **Server Explorer**, expand **Azure** > **HDInsight** > the cluster of your choice > **Hive Databases** > **Default** > **hivesampletable** to see the table schema.</span></span>
2. <span data-ttu-id="01cba-167">在 [hivesampletable] 上按一下滑鼠右鍵，然後按一下 [檢視前 100 個資料列] 來列出資料列。</span><span class="sxs-lookup"><span data-stu-id="01cba-167">Right-click **hivesampletable**, and then click **View Top 100 Rows** to list the rows.</span></span> <span data-ttu-id="01cba-168">這相當於使用 Hive ODBC 驅動程式來執行下列 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="01cba-168">It is equivalent to running the following Hive query using Hive ODBC driver:</span></span>
   
     <span data-ttu-id="01cba-169">SELECT * FROM hivesampletable LIMIT 100</span><span class="sxs-lookup"><span data-stu-id="01cba-169">SELECT * FROM hivesampletable LIMIT 100</span></span>
   
   <span data-ttu-id="01cba-170">您可以自訂資料列計數。</span><span class="sxs-lookup"><span data-stu-id="01cba-170">You can customize the row count.</span></span>
   
   <span data-ttu-id="01cba-171">![Data Lake Tools：HDInsight Hive Visual Studio 結構描述查詢](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Hive 查詢結果")</span><span class="sxs-lookup"><span data-stu-id="01cba-171">![Data Lake Tools: HDInsight Hive Visual Studio schema query](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Hive query results")</span></span>

### <a name="create-hive-tables"></a><span data-ttu-id="01cba-172">建立 Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="01cba-172">Create Hive tables</span></span>
<span data-ttu-id="01cba-173">您可以使用 GUI 來建立 Hive 資料表或使用 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-173">You can use the GUI to create a Hive table or use Hive queries.</span></span> <span data-ttu-id="01cba-174">如需使用 Hive 查詢的相關資訊，請參閱 [執行 Hive 查詢](#run.queries)。</span><span class="sxs-lookup"><span data-stu-id="01cba-174">For information about using Hive queries, see [Run Hive queries](#run.queries).</span></span>

<span data-ttu-id="01cba-175">**建立 Hive 資料表**</span><span class="sxs-lookup"><span data-stu-id="01cba-175">**To create a Hive table**</span></span>

1. <span data-ttu-id="01cba-176">從 [伺服器總管] 中，展開 [Azure] > [HDInsight 叢集] > 某個 HDInsight 叢集 > [Hive 資料庫]，然後在 [預設] 上按一下滑鼠右鍵，並按一下 [建立資料表]。</span><span class="sxs-lookup"><span data-stu-id="01cba-176">From **Server Explorer**, expand **Azure** > **HDInsight Clusters** an HDInsight cluster > **Hive Databases**, then right-click **default**, and click **Create Table**.</span></span>
2. <span data-ttu-id="01cba-177">設定資料表。</span><span class="sxs-lookup"><span data-stu-id="01cba-177">Configure the table.</span></span>
3. <span data-ttu-id="01cba-178">按一下 [ **建立資料表** ] 以提交工作來建立新 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="01cba-178">Click **Create Table** to submit the job to create the new Hive table.</span></span>
   
    <span data-ttu-id="01cba-179">![Data Lake Tools：HDInsight Visual Studio 工具會建立 Hive 資料表](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "建立 Hive 資料表")</span><span class="sxs-lookup"><span data-stu-id="01cba-179">![Data Lake Tools: HDInsight Visual Studio Tools create hive table](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Create Hive table")</span></span>

### <span data-ttu-id="01cba-180"><a name="run.queries"></a>驗證和執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="01cba-180"><a name="run.queries"></a>Validate and run Hive queries</span></span>
<span data-ttu-id="01cba-181">有兩種方式可建立和執行 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="01cba-181">There are two ways to create and run Hive queries:</span></span>

* <span data-ttu-id="01cba-182">建立特定查詢</span><span class="sxs-lookup"><span data-stu-id="01cba-182">Create ad-hoc queries</span></span>
* <span data-ttu-id="01cba-183">建立 Hive 應用程式</span><span class="sxs-lookup"><span data-stu-id="01cba-183">Create a Hive application</span></span>

<span data-ttu-id="01cba-184">**建立、驗證和執行特定查詢**</span><span class="sxs-lookup"><span data-stu-id="01cba-184">**To create, validate, and run ad-hoc queries**</span></span>

1. <span data-ttu-id="01cba-185">從 [伺服器總管] 中，展開 [Azure]，然後展開 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="01cba-185">From **Server Explorer**, expand **Azure**, and then expand **HDInsight Clusters**.</span></span>
2. <span data-ttu-id="01cba-186">在您想要執行查詢的叢集上按一下滑鼠右鍵，然後按一下 [ **撰寫 Hive 查詢**]。</span><span class="sxs-lookup"><span data-stu-id="01cba-186">Right-click the cluster where you want to run the query, and then click **Write a Hive Query**.</span></span>
3. <span data-ttu-id="01cba-187">輸入 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-187">Enter the Hive queries.</span></span> <span data-ttu-id="01cba-188">請注意，Hive 編輯器支援 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="01cba-188">Notice the Hive editor supports IntelliSense.</span></span> <span data-ttu-id="01cba-189">Data Lake Tools for Visual Studio 支援在編輯 Hive 指令碼時載入遠端中繼資料。</span><span class="sxs-lookup"><span data-stu-id="01cba-189">Data Lake Tools for Visual Studio supports loading the remote metadata when you are editing your Hive script.</span></span> <span data-ttu-id="01cba-190">例如，當您輸入 "SELECT * FROM"，IntelliSense 會列出所有建議的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="01cba-190">For example, when you type "SELECT * FROM", the IntelliSense lists all the suggested table names.</span></span> <span data-ttu-id="01cba-191">在指定了資料表名稱時，IntelliSense 會列出資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="01cba-191">When a table name is specified, the column names are listed by the IntelliSense.</span></span> <span data-ttu-id="01cba-192">此工具幾乎支援所有的 Hive DML 陳述式、子查詢以及內建 UDF。</span><span class="sxs-lookup"><span data-stu-id="01cba-192">The tools support almost all Hive DML statements, subqueries, and the built-in UDFs.</span></span>
   
    <span data-ttu-id="01cba-193">![Data Lake Tools：HDInsight Visual Studio 工具 IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="01cba-193">![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")</span></span>
   
    <span data-ttu-id="01cba-194">![Data Lake Tools：HDInsight Visual Studio 工具 IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")</span><span class="sxs-lookup"><span data-stu-id="01cba-194">![Data Lake Tools: HDInsight Visual Studio Tools IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01cba-195">只會建議 HDInsight [工具列] 中已選取的叢集中繼資料。</span><span class="sxs-lookup"><span data-stu-id="01cba-195">Only the metadata of the clusters that is selected in HDInsight Toolbar will be suggested.</span></span>
   > 
   > 
4. <span data-ttu-id="01cba-196">(選擇性)：按一下 [ **驗證指令碼** ] 檢查指令碼語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="01cba-196">(Optional): Click **Validate Script** to check the script syntax errors.</span></span>
   
    <span data-ttu-id="01cba-197">![Data Lake Tools︰Data Lake Tools for Visual Studio 本機驗證](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "驗證指令碼")</span><span class="sxs-lookup"><span data-stu-id="01cba-197">![Data Lake Tools: Data Lake Tools for Visual Studio local validation](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Validate script")</span></span>
5. <span data-ttu-id="01cba-198">按一下 [提交] 或 [提交 (進階)]。</span><span class="sxs-lookup"><span data-stu-id="01cba-198">Click **Submit** or **Submit (Advanced)**.</span></span> <span data-ttu-id="01cba-199">您可以利用進階提交選項來設定指令碼的 [工作名稱]、[引數]、[其他組態] 和 [狀態目錄]：</span><span class="sxs-lookup"><span data-stu-id="01cba-199">With the advanced submit option, you'll configure **Job Name**, **Arguments**, **Additional Configurations**, and **Status Directory** for the script:</span></span>
   
    <span data-ttu-id="01cba-200">![HDInsight Hadoop Hive 查詢](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "提交查詢")</span><span class="sxs-lookup"><span data-stu-id="01cba-200">![HDInsight Hadoop hive query](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Submit queries")</span></span>
   
    <span data-ttu-id="01cba-201">提交工作之後，您會看到 [Hive 工作摘要  ] 視窗。</span><span class="sxs-lookup"><span data-stu-id="01cba-201">After you submit the job, you see a **Hive Job Summary** window.</span></span>
   
    <span data-ttu-id="01cba-202">![HDInsight Hadoop Hive 查詢的摘要](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Hive 作業摘要")</span><span class="sxs-lookup"><span data-stu-id="01cba-202">![Summary of an HDInsight Hadoop Hive query](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Hive job summary")</span></span>
6. <span data-ttu-id="01cba-203">使用 [重新整理] 按鈕來更新狀態，直到工作狀態變更為 [已完成] 為止。</span><span class="sxs-lookup"><span data-stu-id="01cba-203">Use the **Refresh** button to update the status until the job status changes to **Completed**.</span></span>
7. <span data-ttu-id="01cba-204">按一下底部的連結以查看下列內容：[工作查詢]、[工作輸出]、[工作記錄] 或 [Yarn 記錄]。</span><span class="sxs-lookup"><span data-stu-id="01cba-204">Click the links at the bottom to see the following: **Job Query**, **Job Output**, **Job log**, or **Yarn log**.</span></span>

<span data-ttu-id="01cba-205">**建立和執行 Hive 方案**</span><span class="sxs-lookup"><span data-stu-id="01cba-205">**To create and run a Hive solution**</span></span>

1. <span data-ttu-id="01cba-206">從 [檔案] 功能表中，按一下 [新增]，再按 [專案]。</span><span class="sxs-lookup"><span data-stu-id="01cba-206">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="01cba-207">從左窗格中選取 [HDInsight]，選取中間窗格中的 [Hive 應用程式]，輸入屬性，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="01cba-207">Select **HDInsight** from the left pane, select **Hive Application** in the middle pane, enter the properties, and then click **OK**.</span></span>
   
    <span data-ttu-id="01cba-208">![Data Lake Tools：HDInsight Visual Studio 工具新 Hive 專案](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "從 Visual Studio 建立 Hive 應用程式")</span><span class="sxs-lookup"><span data-stu-id="01cba-208">![Data Lake Tools: HDInsight Visual Studio Tools new hive project](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Create Hive applications from Visual Studio")</span></span>
3. <span data-ttu-id="01cba-209">從 [方案總管] 中，按兩下 **Script.hql** 來開啟它。</span><span class="sxs-lookup"><span data-stu-id="01cba-209">From **Solution Explorer**, double-click **Script.hql** to open it.</span></span>
4. <span data-ttu-id="01cba-210">若要驗證 Hive 指令碼，您可以按一下 [驗證指令碼] 按鈕，或在 Hive 編輯器中的指令碼上按一下滑鼠右鍵，然後按一下內容功能表中的 [驗證指令碼]。</span><span class="sxs-lookup"><span data-stu-id="01cba-210">To validate the Hive script, you can click the **Validate Script** button, or right-click the script in the Hive editor, and then click **Validate Script** from the context menu.</span></span>

### <a name="view-hive-jobs"></a><span data-ttu-id="01cba-211">檢視 Hive 工作</span><span class="sxs-lookup"><span data-stu-id="01cba-211">View Hive jobs</span></span>
<span data-ttu-id="01cba-212">您可以檢視 Hive 工作的工作查詢、工作輸出、工作記錄和 Yarn 記錄。</span><span class="sxs-lookup"><span data-stu-id="01cba-212">You can view job queries, job output, job logs, and Yarn logs for Hive jobs.</span></span> <span data-ttu-id="01cba-213">如需詳細資訊，請參閱上一個螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="01cba-213">For more information, see the previous screenshot.</span></span>

<span data-ttu-id="01cba-214">此工具的最新版本可讓您透過收集和呈現 YARN 記錄來查看 Hive 工作的內容。</span><span class="sxs-lookup"><span data-stu-id="01cba-214">The most recent release of the tools allows you to see what’s inside your Hive jobs by collecting and surfacing  YARN logs.</span></span> <span data-ttu-id="01cba-215">YARN 記錄可協助您調查效能問題。</span><span class="sxs-lookup"><span data-stu-id="01cba-215">A YARN log can help you investigating performance issues.</span></span> <span data-ttu-id="01cba-216">如需 HDInsight 如何收集 YARN 記錄的詳細資訊，請參閱[透過程式設計方式存取 HDInsight 應用程式記錄](hdinsight-hadoop-access-yarn-app-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-216">For more information about how HDInsight collects YARN logs, see [Access HDInsight Application Logs Programmatically](hdinsight-hadoop-access-yarn-app-logs.md).</span></span>

<span data-ttu-id="01cba-217">**檢視 Hive 工作**</span><span class="sxs-lookup"><span data-stu-id="01cba-217">**To view Hive jobs**</span></span>

1. <span data-ttu-id="01cba-218">從 [伺服器總管] 中，展開 [Azure]，然後展開 [HDInsight]。</span><span class="sxs-lookup"><span data-stu-id="01cba-218">From **Server Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
2. <span data-ttu-id="01cba-219">在某個 HDInsight 叢集上按一下滑鼠右鍵，然後按一下 [檢視工作 ]。</span><span class="sxs-lookup"><span data-stu-id="01cba-219">Right-click an HDInsight cluster, and then click **View Jobs**.</span></span> <span data-ttu-id="01cba-220">您會看到在該叢集上執行之 Hive 工作的清單。</span><span class="sxs-lookup"><span data-stu-id="01cba-220">You'll see a list of the Hive jobs that ran on the cluster.</span></span>
3. <span data-ttu-id="01cba-221">按一下工作清單中的某個工作來選取它，然後使用 [Hive 工作摘要] 視窗來開啟 [工作查詢]、[工作輸出]、[工作記錄] 或 [Yarn 記錄]。</span><span class="sxs-lookup"><span data-stu-id="01cba-221">Click a job in the job list to select it, and then use the **Hive Job Summary** window to open **Job Query**, **Job Output**, **Job Log**, or **Yarn log**.</span></span>
   
    <span data-ttu-id="01cba-222">![Data Lake Tools：HDInsight Visual Studio 工具檢視 Hive 作業](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "檢視 Hive 作業")</span><span class="sxs-lookup"><span data-stu-id="01cba-222">![Data Lake Tools: HDInsight Visual Studio Tools view Hive jobs](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "View Hive jobs")</span></span>

### <a name="faster-path-hive-execution-via-hiveserver2"></a><span data-ttu-id="01cba-223">透過 HiveServer2 的更快速路徑 Hive 執行</span><span class="sxs-lookup"><span data-stu-id="01cba-223">Faster path Hive execution via HiveServer2</span></span>
> [!NOTE]
> <span data-ttu-id="01cba-224">此功能僅適用於 HDInsight 叢集 3.2 版及更新版本。</span><span class="sxs-lookup"><span data-stu-id="01cba-224">This feature only works on HDInsight cluster version 3.2 and newer.</span></span>
> 
> 

<span data-ttu-id="01cba-225">Data Lake Tools 用來透過 [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (也稱為 Templeton) 提交 Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="01cba-225">The Data Lake Tools used to submit Hive jobs via [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (also known as Templeton).</span></span> <span data-ttu-id="01cba-226">傳回工作詳細資料和錯誤資訊所需的時間很長。</span><span class="sxs-lookup"><span data-stu-id="01cba-226">It took a long time to return job details and error information.</span></span>
<span data-ttu-id="01cba-227">為了解決此效能問題，Data Lake Tools 會透過 HiveServer2 直接在叢集中執行 Hive 工作，以便略過 RDP/SSH。</span><span class="sxs-lookup"><span data-stu-id="01cba-227">In order to solve this performance issue, the Data Lake Tools executes Hive jobs directly in the cluster through HiveServer2, so that it bypasses RDP/SSH.</span></span>
<span data-ttu-id="01cba-228">除了提升效能，使用者也可以檢視 Tez 圖形上的 Hive 和工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="01cba-228">In addition to better performance, users can also view Hive on Tez graphs, and the Task details.</span></span>

<span data-ttu-id="01cba-229">若為 HDInsight 叢集 3.2 版或更新版本，您可以看見 [透過 HiveServer2 執行] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="01cba-229">For HDInsight cluster version 3.2 or later, you can see an **Execute via HiveServer2** button:</span></span>

<span data-ttu-id="01cba-230">![透過 hiveserver2 執行 Data Lake visual studio Tools](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "使用 HiveServer2 執行 Hive 查詢")</span><span class="sxs-lookup"><span data-stu-id="01cba-230">![Data Lake visual studio Tools execute via hiveserver2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Execute Hive queries using HiveServer2")</span></span>

<span data-ttu-id="01cba-231">而且，如果 Hive 查詢是在 Tez 中執行，您可以即時查看串流送回的記錄檔，以及查看工作圖形。</span><span class="sxs-lookup"><span data-stu-id="01cba-231">And you can see the logs streamed back in real-time and see the job graphs if the Hive query is executed in Tez.</span></span>

<span data-ttu-id="01cba-232">![Data Lake visual studio Tools 快速路徑 hive 執行](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "檢視作業圖形")</span><span class="sxs-lookup"><span data-stu-id="01cba-232">![Data Lake visual studio Tools fast path hive execution](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "View job graphs")</span></span>

<span data-ttu-id="01cba-233">**透過 HiveServer2 執行查詢與透過 WebHCat 提交查詢之間的差異**</span><span class="sxs-lookup"><span data-stu-id="01cba-233">**Difference between executing queries via HiveServer2 and Submitting Queries via WebHCat**</span></span>

<span data-ttu-id="01cba-234">雖然透過 HiveServer2 執行查詢有許多效能方面的優點，但這方法仍然有幾項限制。</span><span class="sxs-lookup"><span data-stu-id="01cba-234">Even though executing queries via HiveServer2 has many performance benefits, it has several limitations.</span></span> <span data-ttu-id="01cba-235">且某些限制不適合做為生產用途。</span><span class="sxs-lookup"><span data-stu-id="01cba-235">Some of the limitations are not suitable for production usage.</span></span> <span data-ttu-id="01cba-236">下表為這兩種方法的差異：</span><span class="sxs-lookup"><span data-stu-id="01cba-236">The following table shows the differences:</span></span>

|  | <span data-ttu-id="01cba-237">透過 HiveServer2 執行</span><span class="sxs-lookup"><span data-stu-id="01cba-237">Executing via HiveServer2</span></span> | <span data-ttu-id="01cba-238">透過 WebHCat 提交</span><span class="sxs-lookup"><span data-stu-id="01cba-238">Submitting via WebHCat</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01cba-239">執行查詢</span><span class="sxs-lookup"><span data-stu-id="01cba-239">Execute queries</span></span> |<span data-ttu-id="01cba-240">會排除 WebHCat 中的額外負荷 (WebHCat 會啟動叫做「TempletonControllerJob」的 MapReduce 工作)。</span><span class="sxs-lookup"><span data-stu-id="01cba-240">Eliminates the overhead in WebHCat (which launches a MapReduce Job named “TempletonControllerJob”).</span></span> |<span data-ttu-id="01cba-241">只要查詢是透過 WebHCat 來執行，WebHCat 就會啟動帶來額外延遲的 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="01cba-241">As long as a query is executed via WebHCat, WebHCat will launch a MapReduce job which introduces additional latency.</span></span> |
| <span data-ttu-id="01cba-242">將記錄檔串流回來</span><span class="sxs-lookup"><span data-stu-id="01cba-242">Stream logs back</span></span> |<span data-ttu-id="01cba-243">近乎即時進行。</span><span class="sxs-lookup"><span data-stu-id="01cba-243">In near real-time.</span></span> |<span data-ttu-id="01cba-244">只在工作結束時才提供工作執行記錄檔。</span><span class="sxs-lookup"><span data-stu-id="01cba-244">The job execution logs are available only when the job is finished.</span></span> |
| <span data-ttu-id="01cba-245">檢視工作歷程記錄</span><span class="sxs-lookup"><span data-stu-id="01cba-245">View job history</span></span> |<span data-ttu-id="01cba-246">如果查詢是透過 HiveServer2 執行，系統將不會保留查詢的工作歷程記錄 (工作記錄檔、工作輸出)。</span><span class="sxs-lookup"><span data-stu-id="01cba-246">If a query is executed via HiveServer2, its job history (job log, job output) is not preserved.</span></span> <span data-ttu-id="01cba-247">您可以在 YARN UI 中檢視應用程式的有限資訊。</span><span class="sxs-lookup"><span data-stu-id="01cba-247">The application can be viewed in YARN UI with limited information.</span></span> |<span data-ttu-id="01cba-248">如果查詢是透過 WebHCat 執行，系統會保留查詢的工作歷程記錄 (工作記錄檔、工作輸出)，且可讓您使用 Visual Studio/HDInsight SDK/PowerShell 來檢視。</span><span class="sxs-lookup"><span data-stu-id="01cba-248">If a query is executed via WebHCat, it’s job history (job log, job output) is preserved and can be viewed using Visual Studio/HDInsight SDK/PowerShell.</span></span> |
| <span data-ttu-id="01cba-249">關閉視窗</span><span class="sxs-lookup"><span data-stu-id="01cba-249">Close window</span></span> |<span data-ttu-id="01cba-250">透過 HiveServer2 執行的方式是「同步進行」的，因此您必須讓視窗保持開啟；如果視窗關閉，系統就會取消執行查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-250">Executing via HiveServer2 is a “synchronous” way so you must keep the windows open; if the windows are closed then the query execution will be canceled.</span></span> |<span data-ttu-id="01cba-251">透過 WebHCat 提交的方式是「非同步進行」的，因此您可以透過 WebHCat 提交查詢，然後關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="01cba-251">Submitting via WebHCat is a “asynchronous” way so you can submit the query via WebHCat and close Visual Studio.</span></span> <span data-ttu-id="01cba-252">您隨時可以回來查看結果。</span><span class="sxs-lookup"><span data-stu-id="01cba-252">You can come back and see the results at any time.</span></span> |

### <a name="tez-hive-job-performance-graph"></a><span data-ttu-id="01cba-253">Tez Hive 工作效能圖表</span><span class="sxs-lookup"><span data-stu-id="01cba-253">Tez Hive job performance graph</span></span>
<span data-ttu-id="01cba-254">Data Lake Tools 支援顯示由 Tez 執行引擎執行之 Hive 工作的效能圖形。</span><span class="sxs-lookup"><span data-stu-id="01cba-254">The Data Lake Tools support showing performance graphs for the Hive jobs ran by the Tez execution engine.</span></span> <span data-ttu-id="01cba-255">如需啟用 Tez 的資訊，請參閱[在 HDInsight 中使用 Hive](hdinsight-use-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="01cba-255">For information on enabling Tez, see [use Hive in HDInsight](hdinsight-use-hive.md).</span></span> <span data-ttu-id="01cba-256">您提交 Visual Studio 中的 Hive 工作之後，Visual Studio 會在工作完成時顯示圖形。</span><span class="sxs-lookup"><span data-stu-id="01cba-256">After you submit a Hive job in Visual Studio, Visual Studio shows you the graph when the job is completed.</span></span>  <span data-ttu-id="01cba-257">您可能會需要按一下 [重新整理  ] 按鈕來取得最新的工作狀態。</span><span class="sxs-lookup"><span data-stu-id="01cba-257">You might need to click the **Refresh** button to get the latest job status.</span></span>

> [!NOTE]
> <span data-ttu-id="01cba-258">此功能只適用於高於 3.2.4.593 版的 HDInsight 叢集，而且只能用於已完成的工作 (如果您透過 WebHCat 提交作業，此圖形會在您透過 HiveServer2 執行查詢時顯示)。</span><span class="sxs-lookup"><span data-stu-id="01cba-258">This feature is only available for HDInsight cluster version above 3.2.4.593, and can only work for completed jobs (if you submitted your job through WebHCat; this graph will show when you execute your query through HiveServer2).</span></span> <span data-ttu-id="01cba-259">這適用於以 Windows 和 Linux 為基礎的叢集。</span><span class="sxs-lookup"><span data-stu-id="01cba-259">This works for both Windows and Linux-based clusters.</span></span>
> 
> 

<span data-ttu-id="01cba-260">![hadoop hive tez 效能圖](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "作業狀態")</span><span class="sxs-lookup"><span data-stu-id="01cba-260">![hadoop hive tez performance graph](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Job status")</span></span>

<span data-ttu-id="01cba-261">為協助您更了解 Hive 查詢，此工具在本版本中新增了 Hive 運算子檢視功能。</span><span class="sxs-lookup"><span data-stu-id="01cba-261">To help you understand your Hive query better, the tools add the Hive Operator view in this release.</span></span> <span data-ttu-id="01cba-262">您只需按兩下工作圖形的頂點，即可查看頂點內的所有運算子。</span><span class="sxs-lookup"><span data-stu-id="01cba-262">You just need to double-click on the vertices of the job graph and you can see all the operators inside the vertex.</span></span> <span data-ttu-id="01cba-263">您也可將滑鼠停留在特定運算子上方，以檢視該運算子的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="01cba-263">You can also hover on a particular operator to view more details of this operator.</span></span>

### <a name="task-execution-view-for-hive-on-tez-jobs"></a><span data-ttu-id="01cba-264">Tez 工作上 Hive 的工作執行檢視</span><span class="sxs-lookup"><span data-stu-id="01cba-264">Task execution view for Hive on Tez jobs</span></span>
<span data-ttu-id="01cba-265">Tez 工作上 Hive 的工作執行檢視可用來取得結構化和視覺化 Hive 工作的資訊，以及取得更多工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="01cba-265">The Task execution view for Hive on Tez jobs can be used to get structured & visualized information for Hive jobs, and get more job details.</span></span> <span data-ttu-id="01cba-266">發生效能問題時，您可以使用此檢視來取得進一步的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="01cba-266">When there are performance issues, you can use the view to get further details.</span></span> <span data-ttu-id="01cba-267">例如，每個工作的運作方式和每個工作的詳細資訊 (資料讀取/寫入、排程/開始/結束時間等)，以便根據視覺化資訊微調工作組態或系統架構。</span><span class="sxs-lookup"><span data-stu-id="01cba-267">For example, how each task operates and the detailed information about each task (data read/write, schedule/start/end time, etc.), so that you can tune job configurations or system architecture based on the visualized information.</span></span>

<span data-ttu-id="01cba-268">![Data Lake Visual Studio Tools 工作執行檢視](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "工作執行檢視")</span><span class="sxs-lookup"><span data-stu-id="01cba-268">![Data Lake Visual Studio Tools task execution view](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Task execution view")</span></span>

## <a name="run-pig-scripts"></a><span data-ttu-id="01cba-269">執行 Pig 指令碼</span><span class="sxs-lookup"><span data-stu-id="01cba-269">Run Pig scripts</span></span>
<span data-ttu-id="01cba-270">Data Lake Tools for Visual Studio 支援建立 Pig 指令碼並提交至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="01cba-270">Data Lake Tools for Visual Studio supports creating and submit Pig scripts to HDInsight clusters.</span></span> <span data-ttu-id="01cba-271">使用者可以從範本建立 Pig 專案，然後再提交指令碼至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="01cba-271">Users can create a Pig project from template, and then submit the script to HDInsight clusters.</span></span>

## <a name="feedbacks--known-issues"></a><span data-ttu-id="01cba-272">意見反應和已知問題</span><span class="sxs-lookup"><span data-stu-id="01cba-272">Feedbacks & Known issues</span></span>
* <span data-ttu-id="01cba-273">目前 HiveServer2 結果會以純文字形式顯示，但不太理想。</span><span class="sxs-lookup"><span data-stu-id="01cba-273">Currently HiveServer2 results are displayed in pure text fashion which is not ideal.</span></span> <span data-ttu-id="01cba-274">我們正努力修正該問題。</span><span class="sxs-lookup"><span data-stu-id="01cba-274">We are working on fixing that.</span></span>
* <span data-ttu-id="01cba-275">如果結果是以 NULL 值開頭，目前就不會顯示結果。</span><span class="sxs-lookup"><span data-stu-id="01cba-275">If the results are started with NULL values, currently the results are not shown.</span></span> <span data-ttu-id="01cba-276">我們已修正此問題，如果您因為此問題而遭到封鎖，歡迎寄電子郵件給我們，或連絡支援小組。</span><span class="sxs-lookup"><span data-stu-id="01cba-276">We have fixed this issue and if you are blocked on this issue, feel free to drop us an email or contact support team.</span></span>
* <span data-ttu-id="01cba-277">Visual Studio 所建立的 HQL 指令碼是根據使用者的所在區域設定進行編碼。</span><span class="sxs-lookup"><span data-stu-id="01cba-277">The HQL script created by Visual Studio is encoded depending on user’s local region setting.</span></span> <span data-ttu-id="01cba-278">如果使用者將指令碼以二進位格式上傳至叢集，則可能無法正常執行。</span><span class="sxs-lookup"><span data-stu-id="01cba-278">It may not execute correctly if user uploads the script to cluster as binary.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01cba-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01cba-279">Next steps</span></span>
<span data-ttu-id="01cba-280">在本文中，您學會如何使用 Data Lake (HDInsight) Tools 套件從 Visual Studio 連線到 HDInsight 叢集，以及如何執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="01cba-280">In this article, you learned how to connect to HDInsight clusters from Visual Studio, using the Data Lake (HDInsight) Tools package, and how to run a Hive query.</span></span> <span data-ttu-id="01cba-281">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="01cba-281">For more information, see:</span></span>

* [<span data-ttu-id="01cba-282">在 HDInsight 中使用 Hadoop Hive</span><span class="sxs-lookup"><span data-stu-id="01cba-282">Use Hadoop Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="01cba-283">開始在 HDInsight 中使用 Hadoop</span><span class="sxs-lookup"><span data-stu-id="01cba-283">Get started using Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="01cba-284">在 HDInsight 上提交 Hadoop 工作</span><span class="sxs-lookup"><span data-stu-id="01cba-284">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* [<span data-ttu-id="01cba-285">在 HDInsight 中使用 Hadoop 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="01cba-285">Analyze Twitter data with Hadoop in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)

