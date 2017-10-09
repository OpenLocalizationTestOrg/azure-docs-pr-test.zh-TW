---
title: "Hadoop 叢集的 Azure 上的 aaaUse 指令碼動作 tooinstall Solr |Microsoft 文件"
description: "了解如何 toocustomize HDInsight 叢集 Solr 使用指令碼動作。"
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
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="128a3-103">在 Windows 型 HDInsight 叢集上安裝和使用 Solr</span><span class="sxs-lookup"><span data-stu-id="128a3-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="128a3-104">了解如何使用指令碼動作 Solr toocustomize Windows 為基礎的 HDInsight 叢集以及如何 toouse Solr toosearch 資料。</span><span class="sxs-lookup"><span data-stu-id="128a3-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="128a3-105">hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。</span><span class="sxs-lookup"><span data-stu-id="128a3-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="128a3-106">Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。</span><span class="sxs-lookup"><span data-stu-id="128a3-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="128a3-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="128a3-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="128a3-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="128a3-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="128a3-109">如需搭配以 Linux 為基礎的叢集使用 Solr 的詳細資訊，請參閱 [在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)](hdinsight-hadoop-solr-install-linux.md)</span><span class="sxs-lookup"><span data-stu-id="128a3-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="128a3-110">您也可以使用「指令碼動作」 ，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 Solr。</span><span class="sxs-lookup"><span data-stu-id="128a3-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="128a3-111">範例指令碼 tooinstall Solr 在 HDInsight 叢集上的都可從唯讀的 Azure 儲存體 blob [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="128a3-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="128a3-112">hello 範例指令碼僅適用於 HDInsight 叢集版本 3.1。</span><span class="sxs-lookup"><span data-stu-id="128a3-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="128a3-113">如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="128a3-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="128a3-114">使用本主題中的 hello 範例指令碼會建立 windows Solr 叢集使用特定的組態。</span><span class="sxs-lookup"><span data-stu-id="128a3-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="128a3-115">如果您想具有不同的集合、 分區、 結構描述、 複本和等等的 tooconfigure hello Solr 叢集中，您必須修改 hello 指令碼和 Solr 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="128a3-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="128a3-116">**相關文章**</span><span class="sxs-lookup"><span data-stu-id="128a3-116">**Related articles**</span></span>

* [<span data-ttu-id="128a3-117">在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)</span><span class="sxs-lookup"><span data-stu-id="128a3-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="128a3-118">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="128a3-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="128a3-119">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="128a3-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="128a3-120">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="128a3-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="128a3-121">什麼是 Solr？</span><span class="sxs-lookup"><span data-stu-id="128a3-121">What is Solr?</span></span>
<span data-ttu-id="128a3-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> 是可對資料執行強大全文搜尋作業的企業搜尋平台。</span><span class="sxs-lookup"><span data-stu-id="128a3-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="128a3-123">雖然 Hadoop 可讓儲存和管理大量的資料，Apache Solr 提供 hello 搜尋功能 tooquickly 擷取 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="128a3-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="128a3-124">使用入口網站安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="128a3-124">Install Solr using portal</span></span>
1. <span data-ttu-id="128a3-125">啟動 建立叢集使用 hello**自訂建立**選項，依照[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-provision-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="128a3-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="128a3-126">在 [hello**指令碼動作**頁面 hello 精靈] 中，按一下**加入指令碼動作**tooprovide 詳細 hello 指令碼動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="128a3-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="128a3-127">![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "使用指令碼動作 toocustomize 叢集")</span><span class="sxs-lookup"><span data-stu-id="128a3-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="128a3-128">屬性</span><span class="sxs-lookup"><span data-stu-id="128a3-128">Property</span></span></th><th><span data-ttu-id="128a3-129">值</span><span class="sxs-lookup"><span data-stu-id="128a3-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="128a3-130">名稱</span><span class="sxs-lookup"><span data-stu-id="128a3-130">Name</span></span></td>
            <td><span data-ttu-id="128a3-131">指定 hello 指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="128a3-131">Specify a name for hello script action.</span></span> <span data-ttu-id="128a3-132">例如，<b>安裝 Solr</b>。</span><span class="sxs-lookup"><span data-stu-id="128a3-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="128a3-133">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="128a3-133">Script URI</span></span></td>
            <td><span data-ttu-id="128a3-134">指定 hello 統一資源識別元 (URI) toohello 指令碼會叫用的 toocustomize hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="128a3-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="128a3-135">例如，<i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="128a3-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="128a3-136">節點類型</span><span class="sxs-lookup"><span data-stu-id="128a3-136">Node Type</span></span></td>
            <td><span data-ttu-id="128a3-137">指定 hello hello 自訂指令碼執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="128a3-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="128a3-138">您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。</span><span class="sxs-lookup"><span data-stu-id="128a3-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="128a3-139">參數</span><span class="sxs-lookup"><span data-stu-id="128a3-139">Parameters</span></span></td>
            <td><span data-ttu-id="128a3-140">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="128a3-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="128a3-141">hello 指令碼 tooinstall Solr 不需要任何參數，因此您可以讓此處空白。</span><span class="sxs-lookup"><span data-stu-id="128a3-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="128a3-142">您可以在 hello 叢集上新增多個指令碼動作 tooinstall 多個元件。</span><span class="sxs-lookup"><span data-stu-id="128a3-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="128a3-143">加入 hello 指令碼之後，按一下 建立 hello 叢集 hello 核取記號 toostart。</span><span class="sxs-lookup"><span data-stu-id="128a3-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="128a3-144">使用 Solr</span><span class="sxs-lookup"><span data-stu-id="128a3-144">Use Solr</span></span>
<span data-ttu-id="128a3-145">您必須從以某些資料檔案編製 Solr 的索引來開始。</span><span class="sxs-lookup"><span data-stu-id="128a3-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="128a3-146">然後，您可以使用 Solr toorun 搜尋查詢 hello 編製索引的資料。</span><span class="sxs-lookup"><span data-stu-id="128a3-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="128a3-147">執行下列步驟 toouse Solr HDInsight 叢集中的 hello:</span><span class="sxs-lookup"><span data-stu-id="128a3-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="128a3-148">**使用遠端桌面通訊協定 (RDP) tooremote 成 hello HDInsight 叢集安裝 Solr**。</span><span class="sxs-lookup"><span data-stu-id="128a3-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="128a3-149">Hello Azure 入口網站，為您建立與 Solr 安裝，且再到遠端 hello 叢集 hello 叢集啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="128a3-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="128a3-150">如需指示，請參閱[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="128a3-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="128a3-151">**上傳資料檔案以對 Solr 編製索引**。</span><span class="sxs-lookup"><span data-stu-id="128a3-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="128a3-152">當您建立索引 Solr 時，您放入您可能需要 toosearch 上的文件。</span><span class="sxs-lookup"><span data-stu-id="128a3-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="128a3-153">tooindex Solr，使用 RDP tooremote 到 hello 叢集中，瀏覽 toohello 桌面，開啟 hello Hadoop 命令列，並瀏覽過**C:\apps\dist\solr-4.7.2\example\exampledocs**。</span><span class="sxs-lookup"><span data-stu-id="128a3-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="128a3-154">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="128a3-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="128a3-155">您會看到下列輸出 hello 主控台上的 hello:</span><span class="sxs-lookup"><span data-stu-id="128a3-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="128a3-156">hello post.jar 公用程式索引兩份範例文件，Solr **solr.xml**和**monitor.xml**。</span><span class="sxs-lookup"><span data-stu-id="128a3-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="128a3-157">hello post.jar 公用程式和 hello 範例文件會提供與 Solr 安裝。</span><span class="sxs-lookup"><span data-stu-id="128a3-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="128a3-158">**使用 hello Solr hello 內的儀表板 toosearch 編製索引的文件**。</span><span class="sxs-lookup"><span data-stu-id="128a3-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="128a3-159">在 hello RDP 工作階段 toohello HDInsight 叢集化，開啟 Internet Explorer 中，並啟動 hello Solr 儀表板在**http://headnodehost:8983/solr #/**。</span><span class="sxs-lookup"><span data-stu-id="128a3-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="128a3-160">從 hello 左窗格中，從 hello**核心選取器**下拉式清單中，選取**collection1**，內，按一下 **查詢**。</span><span class="sxs-lookup"><span data-stu-id="128a3-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="128a3-161">範例、 以及 tooselect 傳回 Solr 中的所有 hello 文件會都提供下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="128a3-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="128a3-162">在 hello **q**文字方塊中，輸入 **\*:**\*。</span><span class="sxs-lookup"><span data-stu-id="128a3-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="128a3-163">這會傳回所有的 hello 文件會編製索引 Solr 中。</span><span class="sxs-lookup"><span data-stu-id="128a3-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="128a3-164">如果您想要 toosearch hello 文件中的特定字串，您可以輸入該字串。</span><span class="sxs-lookup"><span data-stu-id="128a3-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="128a3-165">在 hello **wt**文字方塊中，選取 hello 輸出格式。</span><span class="sxs-lookup"><span data-stu-id="128a3-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="128a3-166">預設值是 [ **json**]。</span><span class="sxs-lookup"><span data-stu-id="128a3-166">Default is **json**.</span></span> <span data-ttu-id="128a3-167">按一下 [ **執行查詢**]。</span><span class="sxs-lookup"><span data-stu-id="128a3-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="128a3-168">![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Solr 儀表板上執行查詢")</span><span class="sxs-lookup"><span data-stu-id="128a3-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="128a3-169">hello 輸出傳回 hello 我們用於索引 Solr 的兩個文件。</span><span class="sxs-lookup"><span data-stu-id="128a3-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="128a3-170">hello 輸出看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="128a3-170">hello output resembles hello following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
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
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
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
4. <span data-ttu-id="128a3-171">**建議使用： Hello 備份編製索引資料從 Solr tooAzure hello HDInsight 叢集相關聯的 Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="128a3-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="128a3-172">很好的作法是，您應該備份到 Azure Blob 儲存體的 hello Solr 叢集節點 hello 編製索引的資料。</span><span class="sxs-lookup"><span data-stu-id="128a3-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="128a3-173">執行下列步驟 toodo 因此 hello:</span><span class="sxs-lookup"><span data-stu-id="128a3-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="128a3-174">從 hello RDP 工作階段中，開啟 Internet Explorer 中，並點 toohello 下列 URL:</span><span class="sxs-lookup"><span data-stu-id="128a3-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="128a3-175">您應該會看到如下所示的回應：</span><span class="sxs-lookup"><span data-stu-id="128a3-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="128a3-176">在 hello 遠端工作階段中，瀏覽過 {SOLR_HOME}\{集合} \data 中。</span><span class="sxs-lookup"><span data-stu-id="128a3-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="128a3-177">透過 hello 範例指令碼建立 hello 叢集中，這應該是**C:\apps\dist\solr-4.7.2\example\solr\collection1\data**。</span><span class="sxs-lookup"><span data-stu-id="128a3-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="128a3-178">在這個位置，您應該會看到快照集資料夾，以建立一個名稱類似太**快照集。*時間戳記** *。</span><span class="sxs-lookup"><span data-stu-id="128a3-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="128a3-179">壓縮 hello 快照集資料夾，並將它上傳 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="128a3-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="128a3-180">從 hello Hadoop 命令列使用下列命令的 hello 巡覽 toohello hello 快照集資料夾位置：</span><span class="sxs-lookup"><span data-stu-id="128a3-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="128a3-181">此命令，複製 hello 快照集太/範例/資料/hello 預設儲存體中的 hello 容器下的帳戶與 hello 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="128a3-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="128a3-182">使用 Azure PowerShell 安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="128a3-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="128a3-183">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="128a3-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="128a3-184">hello 範例會示範如何使用 Azure PowerShell 的 Spark tooinstall。</span><span class="sxs-lookup"><span data-stu-id="128a3-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="128a3-185">您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="128a3-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="128a3-186">使用 .NET SDK 安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="128a3-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="128a3-187">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="128a3-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="128a3-188">hello 範例會示範如何 tooinstall Spark 使用 hello.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="128a3-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="128a3-189">您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。</span><span class="sxs-lookup"><span data-stu-id="128a3-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="128a3-190">另請參閱</span><span class="sxs-lookup"><span data-stu-id="128a3-190">See also</span></span>
* [<span data-ttu-id="128a3-191">在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)</span><span class="sxs-lookup"><span data-stu-id="128a3-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="128a3-192">[在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="128a3-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="128a3-193">[使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="128a3-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="128a3-194">[開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="128a3-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="128a3-195">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：關於安裝 Spark 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="128a3-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="128a3-196">[在 HDInsight 叢集上安裝 R][hdinsight-install-r]：關於安裝 R 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="128a3-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="128a3-197">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install.md)：關於安裝 Giraph 的指令碼動作範例。</span><span class="sxs-lookup"><span data-stu-id="128a3-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
