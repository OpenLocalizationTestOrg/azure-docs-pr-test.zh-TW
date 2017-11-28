---
title: "使用指令碼動作在 Hadoop 叢集上安裝 Solr - Azure | Microsoft Docs"
description: "深入了解如何使用指令碼動作來以 Solr 自訂 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="e5d71-103">在 Windows 型 HDInsight 叢集上安裝和使用 Solr</span><span class="sxs-lookup"><span data-stu-id="e5d71-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="e5d71-104">了解如何使用指令碼動作來以 Solr 自訂 Windows 型 HDInsight 叢集，以及如何使用 Solr 搜尋資料。</span><span class="sxs-lookup"><span data-stu-id="e5d71-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5d71-105">本文件的步驟只適用於 Windows HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e5d71-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="e5d71-106">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="e5d71-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="e5d71-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="e5d71-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e5d71-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="e5d71-109">如需搭配以 Linux 為基礎的叢集使用 Solr 的詳細資訊，請參閱 [在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)](hdinsight-hadoop-solr-install-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e5d71-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="e5d71-110">您也可以使用「指令碼動作」 ，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 Solr。</span><span class="sxs-lookup"><span data-stu-id="e5d71-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="e5d71-111">您可以從唯讀的 Azure 儲存體 Blob 取得在 HDInsight 叢集上安裝 Solr 的範例指令碼，網址為 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="e5d71-112">範例指令碼只能與 HDInsight 叢集版本 3.1 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="e5d71-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="e5d71-113">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="e5d71-114">本主題中使用的範例指令碼會以特定組態建立以 Windows 為基礎的 Solr 叢集。</span><span class="sxs-lookup"><span data-stu-id="e5d71-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="e5d71-115">如果您想要以不同的集合、分區、結構描述和複本等項目設定 Solr 叢集，則必須相應修改指令碼和 Solr 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="e5d71-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="e5d71-116">**相關文章**</span><span class="sxs-lookup"><span data-stu-id="e5d71-116">**Related articles**</span></span>

* [<span data-ttu-id="e5d71-117">在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)</span><span class="sxs-lookup"><span data-stu-id="e5d71-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="e5d71-118">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="e5d71-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="e5d71-119">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="e5d71-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="e5d71-120">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="e5d71-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="e5d71-121">什麼是 Solr？</span><span class="sxs-lookup"><span data-stu-id="e5d71-121">What is Solr?</span></span>
<span data-ttu-id="e5d71-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> 是可對資料執行強大全文搜尋作業的企業搜尋平台。</span><span class="sxs-lookup"><span data-stu-id="e5d71-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="e5d71-123">Hadoop 可儲存和管理大量資料，而 Apache Solr 則是提供搜尋功能以便快速擷取資料。</span><span class="sxs-lookup"><span data-stu-id="e5d71-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="e5d71-124">使用入口網站安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="e5d71-124">Install Solr using portal</span></span>
1. <span data-ttu-id="e5d71-125">使用 [自訂建立] 選項，依[在 HDInsight 中建立 Hadoop 叢集](hdinsight-provision-clusters.md)中的描述開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="e5d71-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="e5d71-126">在精靈的 [指令碼動作] 頁面上，按一下 [加入指令碼動作] 以提供有關指令碼動作的詳細資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e5d71-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="e5d71-127">![使用指令碼動作以自訂叢集](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "使用指令碼動作以自訂叢集")</span><span class="sxs-lookup"><span data-stu-id="e5d71-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="e5d71-128">屬性</span><span class="sxs-lookup"><span data-stu-id="e5d71-128">Property</span></span></th><th><span data-ttu-id="e5d71-129">值</span><span class="sxs-lookup"><span data-stu-id="e5d71-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="e5d71-130">名稱</span><span class="sxs-lookup"><span data-stu-id="e5d71-130">Name</span></span></td>
            <td><span data-ttu-id="e5d71-131">指定指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="e5d71-131">Specify a name for the script action.</span></span> <span data-ttu-id="e5d71-132">例如，<b>安裝 Solr</b>。</span><span class="sxs-lookup"><span data-stu-id="e5d71-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="e5d71-133">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="e5d71-133">Script URI</span></span></td>
            <td><span data-ttu-id="e5d71-134">指定為自訂叢集叫用的指令碼統一資源識別項 (URI)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="e5d71-135">例如，<i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="e5d71-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="e5d71-136">節點類型</span><span class="sxs-lookup"><span data-stu-id="e5d71-136">Node Type</span></span></td>
            <td><span data-ttu-id="e5d71-137">指定執行自訂指令碼的節點。</span><span class="sxs-lookup"><span data-stu-id="e5d71-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="e5d71-138">您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="e5d71-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="e5d71-139">參數</span><span class="sxs-lookup"><span data-stu-id="e5d71-139">Parameters</span></span></td>
            <td><span data-ttu-id="e5d71-140">如果指令碼要求，請指定參數。</span><span class="sxs-lookup"><span data-stu-id="e5d71-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="e5d71-141">用來安裝 Solr 的指令碼不需要任何參數，因此可以讓此處空白。</span><span class="sxs-lookup"><span data-stu-id="e5d71-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="e5d71-142">您可以加入一個以上的指令碼動作，以在叢集上安裝多個元件。</span><span class="sxs-lookup"><span data-stu-id="e5d71-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="e5d71-143">加入指令碼之後，請按一下核取記號以開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="e5d71-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="e5d71-144">使用 Solr</span><span class="sxs-lookup"><span data-stu-id="e5d71-144">Use Solr</span></span>
<span data-ttu-id="e5d71-145">您必須從以某些資料檔案編製 Solr 的索引來開始。</span><span class="sxs-lookup"><span data-stu-id="e5d71-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="e5d71-146">然後，您可以使用 Solr 來對已編製索引的資料執行搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="e5d71-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="e5d71-147">執行下列步驟以在 HDInsight 叢集中使用 Solr：</span><span class="sxs-lookup"><span data-stu-id="e5d71-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="e5d71-148">**使用遠端桌面通訊協定 (RDP) 遠端登入到已安裝 Solr 的 HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="e5d71-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="e5d71-149">從 Azure 入口網站，針對您所建立且已安裝 Solr 的叢集啟用遠端桌面，然後遠端登入到叢集。</span><span class="sxs-lookup"><span data-stu-id="e5d71-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="e5d71-150">如需指示，請參閱 [使用 RDP 連接至 HDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="e5d71-151">**上傳資料檔案以對 Solr 編製索引**。</span><span class="sxs-lookup"><span data-stu-id="e5d71-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="e5d71-152">在對 Solr 編製索引時，會在其中放置可能需要搜尋的文件。</span><span class="sxs-lookup"><span data-stu-id="e5d71-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="e5d71-153">若要對 Solr 編製索引，請使用 RDP 遠端登入到叢集、瀏覽至桌面、開啟 Hadoop 命令列，然後瀏覽至 **C:\apps\dist\solr-4.7.2\example\exampledocs**。</span><span class="sxs-lookup"><span data-stu-id="e5d71-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="e5d71-154">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="e5d71-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="e5d71-155">您會在主控台上看到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e5d71-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="e5d71-156">post.jar 公用程式使用 **solr.xml** 和 **monitor.xml** 這兩個範例文件對 Solr 編製索引。</span><span class="sxs-lookup"><span data-stu-id="e5d71-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="e5d71-157">您可以在 Solr 安裝內取得 post.jar 公用程式和範例文件。</span><span class="sxs-lookup"><span data-stu-id="e5d71-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="e5d71-158">**使用 Solr 儀表板在已編製索引的文件內執行搜尋**。</span><span class="sxs-lookup"><span data-stu-id="e5d71-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="e5d71-159">在連往 HDInsight 叢集的 RDP 工作階段內，開啟 Internet Explorer，然後在 **http://headnodehost:8983/solr/#/** 啟動 Solr 儀表板。</span><span class="sxs-lookup"><span data-stu-id="e5d71-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="e5d71-160">在左窗格的 [核心選取器] 下拉式清單中，選取 [collection1]，然後在其中按一下 [查詢]。</span><span class="sxs-lookup"><span data-stu-id="e5d71-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="e5d71-161">舉例來說，若要選取並傳回 Solr 中的所有文件，請提供下列值：</span><span class="sxs-lookup"><span data-stu-id="e5d71-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="e5d71-162">在 [q] 文字方塊中輸入 **:**\*\*。</span><span class="sxs-lookup"><span data-stu-id="e5d71-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="e5d71-163">如此便會傳回已在 Solr 中編製索引的所有文件。</span><span class="sxs-lookup"><span data-stu-id="e5d71-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="e5d71-164">如果您想要搜尋文件內的特定字串，您可以在此輸入該字串。</span><span class="sxs-lookup"><span data-stu-id="e5d71-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="e5d71-165">在 [ **wt** ] 文字方塊中，選取輸出格式。</span><span class="sxs-lookup"><span data-stu-id="e5d71-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="e5d71-166">預設值是 [ **json**]。</span><span class="sxs-lookup"><span data-stu-id="e5d71-166">Default is **json**.</span></span> <span data-ttu-id="e5d71-167">按一下 [ **執行查詢**]。</span><span class="sxs-lookup"><span data-stu-id="e5d71-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="e5d71-168">![使用指令碼動作以自訂叢集](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "在 Solr 儀表板上執行查詢")</span><span class="sxs-lookup"><span data-stu-id="e5d71-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="e5d71-169">輸出中會傳回兩個我們之前用於對 Solr 編製索引的文件。</span><span class="sxs-lookup"><span data-stu-id="e5d71-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="e5d71-170">輸出結果類似下面：</span><span class="sxs-lookup"><span data-stu-id="e5d71-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="e5d71-171">**建議步驟：從 Solr 將已編製索引的資料備份到與 HDInsight 叢集相關聯的 Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="e5d71-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="e5d71-172">您最好從 Solr 叢集節點將已編製索引的資料備份到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e5d71-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="e5d71-173">請執行下列步驟來進行此作業：</span><span class="sxs-lookup"><span data-stu-id="e5d71-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="e5d71-174">從 RDP 工作階段開啟 Internet Explorer，然後指向下列 URL：</span><span class="sxs-lookup"><span data-stu-id="e5d71-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="e5d71-175">您應該會看到如下所示的回應：</span><span class="sxs-lookup"><span data-stu-id="e5d71-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="e5d71-176">在遠端工作階段中，瀏覽至 {SOLR_HOME}\{Collection}\data。</span><span class="sxs-lookup"><span data-stu-id="e5d71-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="e5d71-177">若是透過範例指令碼建立的叢集，則應該是 **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**。</span><span class="sxs-lookup"><span data-stu-id="e5d71-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="e5d71-178">在此位置中，您應該會看到以類似「snapshot.timestamp」的名稱建立的快照資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5d71-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="e5d71-179">壓縮快照資料夾，並上傳至 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e5d71-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="e5d71-180">從 Hadoop 命令列使用下列命令瀏覽至快照資料夾的位置：</span><span class="sxs-lookup"><span data-stu-id="e5d71-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="e5d71-181">此命令會將快照複製到與叢集相關聯之預設儲存體帳戶內的容器下的 /example/data/。</span><span class="sxs-lookup"><span data-stu-id="e5d71-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="e5d71-182">使用 Azure PowerShell 安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="e5d71-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="e5d71-183">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="e5d71-184">此範例示範如何使用 Azure PowerShell 安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="e5d71-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="e5d71-185">您需要自訂指令碼以使用 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="e5d71-186">使用 .NET SDK 安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="e5d71-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="e5d71-187">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="e5d71-188">此範例示範如何使用 .NET SDK 安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="e5d71-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="e5d71-189">您需要自訂指令碼以使用 [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="e5d71-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="e5d71-190">另請參閱</span><span class="sxs-lookup"><span data-stu-id="e5d71-190">See also</span></span>
* [<span data-ttu-id="e5d71-191">在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)</span><span class="sxs-lookup"><span data-stu-id="e5d71-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="e5d71-192">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="e5d71-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="e5d71-193">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="e5d71-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="e5d71-194">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="e5d71-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="e5d71-195">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：關於安裝 Spark 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="e5d71-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="e5d71-196">[在 HDInsight 叢集上安裝 R][hdinsight-install-r]：關於安裝 R 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="e5d71-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="e5d71-197">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install.md)：關於安裝 Giraph 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="e5d71-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
