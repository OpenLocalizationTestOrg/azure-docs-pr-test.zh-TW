---
title: "aaaUse 指令碼動作 tooinstall 以 Linux 為基礎的 HDInsight 的 Azure 上 Solr |Microsoft 文件"
description: "了解如何 tooinstall Solr 上以 Linux 為基礎的 HDInsight Hadoop 叢集使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="dfce2-103">在 HDInsight Hadoop 叢集上安裝和使用 Solr</span><span class="sxs-lookup"><span data-stu-id="dfce2-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="dfce2-104">深入了解如何使用指令碼動作 tooinstall Solr Azure HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="dfce2-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="dfce2-105">Solr 是強大的搜尋平台，可對 Hadoop 管理的資料執行企業級搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="dfce2-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="dfce2-106">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dfce2-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="dfce2-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="dfce2-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dfce2-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfce2-109">這份文件中使用的 hello 範例指令碼會使用特定的組態安裝 Solr 4.9。</span><span class="sxs-lookup"><span data-stu-id="dfce2-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="dfce2-110">如果您想具有不同的集合、 分區、 結構描述、 複本和等等的 tooconfigure hello Solr 叢集中，您必須修改 hello 指令碼和 Solr 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="dfce2-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="dfce2-111"><a name="whatis"></a>什麼是 Solr</span><span class="sxs-lookup"><span data-stu-id="dfce2-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="dfce2-112">[Apache Solr](http://lucene.apache.org/solr/features.html) 是可對資料執行強大全文搜尋作業的企業搜尋平台。</span><span class="sxs-lookup"><span data-stu-id="dfce2-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="dfce2-113">雖然 Hadoop 可讓儲存和管理大量的資料，Apache Solr 提供 hello 搜尋功能 tooquickly 擷取 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="dfce2-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="dfce2-114">Microsoft 完全支援元件時附上 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dfce2-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="dfce2-115">自訂元件，例如 Solr，會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="dfce2-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="dfce2-116">Microsoft 支援服務可能不是自訂元件無法 tooresolve 發生問題。</span><span class="sxs-lookup"><span data-stu-id="dfce2-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="dfce2-117">您可能需要 tooengage hello 開放原始碼社群尋求協助。</span><span class="sxs-lookup"><span data-stu-id="dfce2-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="dfce2-118">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="dfce2-119">哪些 hello 指令碼會執行</span><span class="sxs-lookup"><span data-stu-id="dfce2-119">What hello script does</span></span>

<span data-ttu-id="dfce2-120">此指令碼會進行下列變更 toohello HDInsight 叢集的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="dfce2-121">將 Solr 4.9 安裝至 `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="dfce2-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="dfce2-122">建立使用者**solrusr**，也就是使用的 toorun hello Solr 服務</span><span class="sxs-lookup"><span data-stu-id="dfce2-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="dfce2-123">設定**solruser**做為 hello 擁有者`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="dfce2-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="dfce2-124">加入會自動啟動 Solr 的 [Upstart](http://upstart.ubuntu.com/) 組態。</span><span class="sxs-lookup"><span data-stu-id="dfce2-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="dfce2-125"><a name="install"></a>使用指令碼動作安裝 Solr</span><span class="sxs-lookup"><span data-stu-id="dfce2-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="dfce2-126">範例指令碼 tooinstall Solr 在 HDInsight 叢集上的將會位於下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="dfce2-127">toocreate 具有 Solr 安裝的叢集，hello 步驟使用 hello[建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dfce2-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="dfce2-128">在 hello 建立過程中，使用下列步驟 tooinstall Solr hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="dfce2-129">從 hello__叢集摘要__刀鋒視窗，select__Advanced settings__，然後__編寫指令碼動作__。</span><span class="sxs-lookup"><span data-stu-id="dfce2-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="dfce2-130">使用下列資訊 toopopulate hello 表單 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="dfce2-131">**名稱**： 輸入 hello 指令碼動作的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="dfce2-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="dfce2-132">**SCRIPT URI**：https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="dfce2-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="dfce2-133">**HEAD**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="dfce2-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="dfce2-134">**WORKER**：勾選此選項</span><span class="sxs-lookup"><span data-stu-id="dfce2-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="dfce2-135">**動物園管理員**： 檢查 hello 動物園管理員節點上的這個選項 tooinstall</span><span class="sxs-lookup"><span data-stu-id="dfce2-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="dfce2-136">**參數**：將此欄位保留空白</span><span class="sxs-lookup"><span data-stu-id="dfce2-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="dfce2-137">在 hello 底部 hello**編寫指令碼動作**刀鋒視窗中，使用 hello**選取**按鈕 toosave hello 組態。</span><span class="sxs-lookup"><span data-stu-id="dfce2-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="dfce2-138">最後，使用 hello**下一步**按鈕 tooreturn toohello__叢集摘要__</span><span class="sxs-lookup"><span data-stu-id="dfce2-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="dfce2-139">從 hello__叢集摘要__頁面上，選取__建立__toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="dfce2-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="dfce2-140"><a name="usesolr"></a>如何在 HDInsight 中使用 Solr</span><span class="sxs-lookup"><span data-stu-id="dfce2-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfce2-141">本節中的 hello 步驟示範基本的 Solr 功能。</span><span class="sxs-lookup"><span data-stu-id="dfce2-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="dfce2-142">如需有關使用 Solr 的詳細資訊，請參閱 hello [Apache Solr 網站](http://lucene.apache.org/solr/)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="dfce2-143">索引資料</span><span class="sxs-lookup"><span data-stu-id="dfce2-143">Index data</span></span>

<span data-ttu-id="dfce2-144">使用下列步驟 tooadd 範例資料 tooSolr hello，然後進行查詢：</span><span class="sxs-lookup"><span data-stu-id="dfce2-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="dfce2-145">連線使用 SSH toohello HDInsight 叢集：</span><span class="sxs-lookup"><span data-stu-id="dfce2-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="dfce2-146">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="dfce2-147">在本文件稍後的步驟會使用 SSL 通道 tooconnect toohello Solr web UI。</span><span class="sxs-lookup"><span data-stu-id="dfce2-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="dfce2-148">toouse 這些步驟，您必須建立 SSL 通道，然後再設定您的瀏覽器 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="dfce2-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="dfce2-149">如需詳細資訊，請參閱 hello[使用 SSH 通道，與 HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dfce2-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="dfce2-150">使用下列命令 toohave Solr 索引範例資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="dfce2-151">hello 會傳回下列輸出 toohello 主控台：</span><span class="sxs-lookup"><span data-stu-id="dfce2-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="dfce2-152">hello`post.jar`公用程式將 hello **solr.xml**和**monitor.xml**文件 toohello 索引。</span><span class="sxs-lookup"><span data-stu-id="dfce2-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="dfce2-153">使用下列命令 tooquery hello Solr REST API 的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="dfce2-154">此命令會搜尋**collection1**針對比對任何文件 **\*:\***  (編碼為\*%3a\* hello 查詢字串中)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="dfce2-155">下列 JSON 文件的 hello 是 hello 回應的範例：</span><span class="sxs-lookup"><span data-stu-id="dfce2-155">hello following JSON document is an example of hello response:</span></span>

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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="dfce2-156">使用 hello Solr 儀表板</span><span class="sxs-lookup"><span data-stu-id="dfce2-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="dfce2-157">hello Solr 儀表板是 web UI，讓您透過網頁瀏覽器與 Solr toowork。</span><span class="sxs-lookup"><span data-stu-id="dfce2-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="dfce2-158">hello Solr 儀表板不會直接在從您的 HDInsight 叢集的 hello 網際網路上公開。</span><span class="sxs-lookup"><span data-stu-id="dfce2-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="dfce2-159">您可以使用 SSH 通道 tooaccess 它。</span><span class="sxs-lookup"><span data-stu-id="dfce2-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="dfce2-160">如需有關如何使用 SSH 通道的詳細資訊，請參閱 hello[使用 SSH 通道，與 HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)文件。</span><span class="sxs-lookup"><span data-stu-id="dfce2-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="dfce2-161">一旦您已建立的 SSH 通道，請使用下列步驟 toouse hello Solr 儀表板的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="dfce2-162">判斷 hello hello 主要叢集前端節點的主機名稱：</span><span class="sxs-lookup"><span data-stu-id="dfce2-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="dfce2-163">使用 SSH tooconnect toohello 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="dfce2-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="dfce2-164">例如： `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="dfce2-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="dfce2-165">如需有關如何使用 SSH 的詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="dfce2-166">使用下列命令 tooget hello 完整主機名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="dfce2-167">此命令會傳回下列主機名稱值類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="dfce2-168">儲存 hello 值傳回，稍後使用。</span><span class="sxs-lookup"><span data-stu-id="dfce2-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="dfce2-169">在瀏覽器中，連接太**http://HOSTNAME:8983/solr #/**，其中**HOSTNAME**是您決定在 hello 先前步驟中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="dfce2-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="dfce2-170">hello 要求路由傳送 hello SSH 通道 toohello Solr web UI 上您的叢集。</span><span class="sxs-lookup"><span data-stu-id="dfce2-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="dfce2-171">hello 頁面會顯示下列影像類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-171">hello page appears similar toohello following image:</span></span>

    ![Solr 儀表板的映像](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="dfce2-173">從 hello 左窗格中，使用 hello**核心選取器**下拉式 tooselect **collection1**。</span><span class="sxs-lookup"><span data-stu-id="dfce2-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="dfce2-174">數個項目應該會出現在 **collection1** 底下。</span><span class="sxs-lookup"><span data-stu-id="dfce2-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="dfce2-175">從下列項目 hello **collection1**，選取**查詢**。</span><span class="sxs-lookup"><span data-stu-id="dfce2-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="dfce2-176">使用下列值 toopopulate hello 搜尋頁面的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="dfce2-177">在 hello **q**文字方塊中，輸入 **\*:**\*。</span><span class="sxs-lookup"><span data-stu-id="dfce2-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="dfce2-178">此查詢會傳回 Solr 中所有的 hello 文件會編製索引。</span><span class="sxs-lookup"><span data-stu-id="dfce2-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="dfce2-179">如果您想要 toosearch hello 文件中的特定字串，您可以輸入該字串。</span><span class="sxs-lookup"><span data-stu-id="dfce2-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="dfce2-180">在 hello **wt**文字方塊中，選取 hello 輸出格式。</span><span class="sxs-lookup"><span data-stu-id="dfce2-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="dfce2-181">預設值是 [ **json**]。</span><span class="sxs-lookup"><span data-stu-id="dfce2-181">Default is **json**.</span></span>

     <span data-ttu-id="dfce2-182">最後，選取 hello**執行查詢**在 hello hello 搜尋 pate 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dfce2-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="dfce2-184">hello 輸出傳回的 hello 兩份文件，就像加入 toohello 先前索引。</span><span class="sxs-lookup"><span data-stu-id="dfce2-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="dfce2-185">hello 輸出類似 toohello 之後，JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="dfce2-185">hello output is similar toohello following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="dfce2-186">啟動和停止 Solr</span><span class="sxs-lookup"><span data-stu-id="dfce2-186">Starting and stopping Solr</span></span>

<span data-ttu-id="dfce2-187">使用下列命令 toomanually 停止和啟動 Solr hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="dfce2-188">備份已編製索引的資料</span><span class="sxs-lookup"><span data-stu-id="dfce2-188">Backup indexed data</span></span>

<span data-ttu-id="dfce2-189">使用下列步驟 tooback Solr toohello 預設儲存體叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="dfce2-190">Toohello 叢集使用 SSH 連線，然後使用下列命令 tooget hello hello 前端節點的主機名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfce2-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="dfce2-191">使用下列命令 toocreate hello 編製索引資料的快照集的 hello。</span><span class="sxs-lookup"><span data-stu-id="dfce2-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="dfce2-192">取代**HOSTNAME** hello hello 前一個命令所傳回的名稱：</span><span class="sxs-lookup"><span data-stu-id="dfce2-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="dfce2-193">hello 回應是類似 toohello 下列 XML:</span><span class="sxs-lookup"><span data-stu-id="dfce2-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="dfce2-194">將目錄變更太`/usr/hdp/current/solr/example/solr`。</span><span class="sxs-lookup"><span data-stu-id="dfce2-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="dfce2-195">在這裡每個集合有一個子目錄。</span><span class="sxs-lookup"><span data-stu-id="dfce2-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="dfce2-196">每個集合目錄包含`data`包含 hello hello 集合快照集目錄。</span><span class="sxs-lookup"><span data-stu-id="dfce2-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="dfce2-197">toocreate 經過壓縮的封存的 hello 快照集資料夾，使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="dfce2-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="dfce2-198">取代 hello `snapshot.20150806185338855` hello 的集合名稱的 hello 快照集的值。</span><span class="sxs-lookup"><span data-stu-id="dfce2-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="dfce2-199">此命令會建立名為封存**snapshot.20150806185338855.tgz**，其中包含 hello hello 內容**snapshot.20150806185338855**目錄。</span><span class="sxs-lookup"><span data-stu-id="dfce2-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="dfce2-200">然後，您可以儲存 hello 封存 toohello 叢集的主要儲存體使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="dfce2-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="dfce2-201">如需有關使用 Solr 備份和還原的詳細資訊，請參閱 [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfce2-202">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfce2-202">Next steps</span></span>

* <span data-ttu-id="dfce2-203">[在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="dfce2-204">使用叢集自訂 tooinstall Giraph 上 HDInsight Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="dfce2-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="dfce2-205">Giraph 可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="dfce2-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="dfce2-206">[在 HDInsight 叢集上安裝 Hue](hdinsight-hadoop-hue-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="dfce2-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="dfce2-207">使用 HDInsight Hadoop 叢集上的叢集自訂 tooinstall 色調。</span><span class="sxs-lookup"><span data-stu-id="dfce2-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="dfce2-208">色調是一組 Web 應用程式使用 toointeract 與 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="dfce2-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
