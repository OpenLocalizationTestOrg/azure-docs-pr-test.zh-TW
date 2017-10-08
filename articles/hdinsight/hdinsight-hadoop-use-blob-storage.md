---
title: "從 HDFS 相容 aaaQuery 資料 Azure 儲存體的 Azure HDInsight |Microsoft 文件"
description: "了解如何從 Azure 儲存體和 Azure Data Lake Store toostore tooquery 資料產生您的分析。"
keywords: "blob 儲存體,hdfs,結構化資料,非結構化資料,data lake store,Hadoop 輸入,Hadoop 輸出, hadoop 儲存體, hdfs 輸入,hdfs 輸出,hdfs 儲存體,wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="70197-104">搭配 Azure HDInsight 叢集使用 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="70197-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="70197-105">tooanalyze HDInsight 叢集中的資料，您可以儲存在 Azure 儲存體、 Azure 資料湖存放區，或兩者的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="70197-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="70197-106">這兩個儲存體選項可讓您 toosafely 刪除 HDInsight 叢集所使用的計算，而不會遺失使用者資料。</span><span class="sxs-lookup"><span data-stu-id="70197-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="70197-107">Hadoop 支援 hello 預設檔案系統的概念。</span><span class="sxs-lookup"><span data-stu-id="70197-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="70197-108">hello 預設的檔案系統表示預設配置和授權單位。</span><span class="sxs-lookup"><span data-stu-id="70197-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="70197-109">它也可以使用的 tooresolve 相對路徑。</span><span class="sxs-lookup"><span data-stu-id="70197-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="70197-110">在 hello HDInsight 叢集建立程序，您可以指定 blob 容器，在 Azure 儲存體為 hello 預設檔案系統，或使用 HDInsight 3.5，您可以選取 Azure 儲存體或 Azure Data Lake Store hello 預設檔案系統，有一些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="70197-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="70197-111">做為預設 hello 和連結的儲存體使用 Data Lake Store 的 hello 提供支援，請參閱[HDInsight 叢集 Availabilities](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters)。</span><span class="sxs-lookup"><span data-stu-id="70197-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="70197-112">在本文中，您將了解 Azure 儲存體與 HDInsight 叢集搭配運作的方式。</span><span class="sxs-lookup"><span data-stu-id="70197-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="70197-113">toolearn Data Lake Store 的 HDInsight 叢集的運作方式查看[使用 Azure 資料湖存放區與 Azure HDInsight 叢集](hdinsight-hadoop-use-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="70197-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="70197-114">如需建立 HDInsight 叢集的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="70197-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="70197-115">Azure 儲存體是強大的一般用途儲存體解決方案，其完美整合了 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="70197-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="70197-116">HDInsight 可用於 blob 容器的 Azure 儲存體中為 hello 預設檔案系統 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="70197-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="70197-117">透過 Hadoop 分散式的檔案系統 (HDFS) 介面，直接可以處理結構化或非結構化資料儲存為 blob hello 整組 HDInsight 中的元件。</span><span class="sxs-lookup"><span data-stu-id="70197-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="70197-118">建立 Azure 儲存體帳戶時，有數個選項可供使用。</span><span class="sxs-lookup"><span data-stu-id="70197-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="70197-119">hello 下表提供與 HDInsight 支援哪些選項的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="70197-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="70197-120">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="70197-120">Storage account type</span></span> | <span data-ttu-id="70197-121">儲存層</span><span class="sxs-lookup"><span data-stu-id="70197-121">Storage tier</span></span> | <span data-ttu-id="70197-122">支援 HDInsight</span><span class="sxs-lookup"><span data-stu-id="70197-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="70197-123">一般用途的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="70197-123">General-purpose Storage Account</span></span> | <span data-ttu-id="70197-124">標準</span><span class="sxs-lookup"><span data-stu-id="70197-124">Standard</span></span> | <span data-ttu-id="70197-125">__是__</span><span class="sxs-lookup"><span data-stu-id="70197-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="70197-126">進階</span><span class="sxs-lookup"><span data-stu-id="70197-126">Premium</span></span> | <span data-ttu-id="70197-127">否</span><span class="sxs-lookup"><span data-stu-id="70197-127">No</span></span> |
> | <span data-ttu-id="70197-128">Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="70197-128">Blob Storage Account</span></span> | <span data-ttu-id="70197-129">經常性存取</span><span class="sxs-lookup"><span data-stu-id="70197-129">Hot</span></span> | <span data-ttu-id="70197-130">否</span><span class="sxs-lookup"><span data-stu-id="70197-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="70197-131">非經常性存取</span><span class="sxs-lookup"><span data-stu-id="70197-131">Cool</span></span> | <span data-ttu-id="70197-132">否</span><span class="sxs-lookup"><span data-stu-id="70197-132">No</span></span> |

<span data-ttu-id="70197-133">我們不建議您儲存商務資料使用 hello 預設 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="70197-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="70197-134">在每個使用 tooreduce 之後，刪除 hello 預設 blob 容器儲存體成本是很好的作法。</span><span class="sxs-lookup"><span data-stu-id="70197-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="70197-135">請注意該 hello 預設容器包含應用程式與系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="70197-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="70197-136">刪除 hello 容器前請確定 tooretrieve hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="70197-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="70197-137">不支援多個叢集共用一個 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="70197-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="70197-138">HDInsight 儲存架構</span><span class="sxs-lookup"><span data-stu-id="70197-138">HDInsight storage architecture</span></span>
<span data-ttu-id="70197-139">下列圖表中的 hello 提供 hello HDInsight 的使用 Azure 儲存體的儲存體架構的抽象檢視：</span><span class="sxs-lookup"><span data-stu-id="70197-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="70197-140">![Hadoop 叢集使用 hello HDFS API tooaccess，並將結構化及未結構化資料儲存在 Blob 儲存體。] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight 儲存體架構")</span><span class="sxs-lookup"><span data-stu-id="70197-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="70197-141">HDInsight 提供在本機存取 toohello 分散式檔案系統附加 toohello 計算節點。</span><span class="sxs-lookup"><span data-stu-id="70197-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="70197-142">可以使用來存取此檔案系統 hello 完整格式 URI，例如：</span><span class="sxs-lookup"><span data-stu-id="70197-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="70197-143">此外，HDInsight 可讓您 tooaccess 資料儲存在 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="70197-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="70197-144">hello 語法為：</span><span class="sxs-lookup"><span data-stu-id="70197-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="70197-145">以下是搭配 HDInsight 叢集使用 Azure 儲存體帳戶時的一些考量。</span><span class="sxs-lookup"><span data-stu-id="70197-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="70197-146">**Hello 連接的 tooa 叢集的儲存體帳戶中的容器：**因為 hello 帳戶名稱和金鑰相關聯 hello 叢集建立期間，您會有這些容器中的完整存取 toohello blob。</span><span class="sxs-lookup"><span data-stu-id="70197-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="70197-147">**公用容器或公用 blob 儲存體帳戶不在連線 tooa 叢集：**您有唯讀權限 toohello blob hello 容器中的。</span><span class="sxs-lookup"><span data-stu-id="70197-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="70197-148">公用容器可讓您 tooget 可用該容器中，並取得容器中繼資料的所有 blob 的清單。</span><span class="sxs-lookup"><span data-stu-id="70197-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="70197-149">公用 blob 可讓您 tooaccess hello blob 才知道 hello 正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="70197-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="70197-150">如需詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">限制存取 toocontainers 和 blob</a>。</span><span class="sxs-lookup"><span data-stu-id="70197-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="70197-151">**無法儲存體帳戶中的私用容器連接 tooa 叢集：**您無法存取 hello 容器中的 hello blob，除非您定義 hello 儲存體帳戶，當您送出 hello WebHCat 作業。</span><span class="sxs-lookup"><span data-stu-id="70197-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="70197-152">稍後在本文中會加以說明。</span><span class="sxs-lookup"><span data-stu-id="70197-152">This is explained later in this article.</span></span>

<span data-ttu-id="70197-153">hello hello 建立程序和它們的索引鍵中所定義的儲存體帳戶會儲存在 %HADOOP_HOME%/conf/core-site.xml hello 叢集節點上。</span><span class="sxs-lookup"><span data-stu-id="70197-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="70197-154">HDInsight hello 預設行為是 toouse hello core-site.xml 檔案中定義的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70197-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="70197-155">您可以使用 [Ambari](./hdinsight-hadoop-manage-ambari.md) 來修改此設定</span><span class="sxs-lookup"><span data-stu-id="70197-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="70197-156">多個 WebHCat 工作 (包括 Hive、MapReduce、Hadoop 資料流和 Pig) 可隨身夾帶儲存體帳戶的說明和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="70197-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="70197-157">(目前適用於含儲存體帳戶的 Pig，但不適用於中繼資料)。如需詳細資訊，請參閱 [在其他儲存體帳戶和 Metastores 上使用 HDInsight 叢集](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx)。</span><span class="sxs-lookup"><span data-stu-id="70197-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="70197-158">Blob 可使用於結構化和非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="70197-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="70197-159">Blob 容器以機碼/值組來儲存資料，沒有目錄階層。</span><span class="sxs-lookup"><span data-stu-id="70197-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="70197-160">不過，可用於 hello 斜線字元 （/） hello 起來當做檔案儲存在目錄結構內的索引鍵名稱 toomake。</span><span class="sxs-lookup"><span data-stu-id="70197-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="70197-161">例如，Blob 的機碼可能是 *input/log1.txt*。</span><span class="sxs-lookup"><span data-stu-id="70197-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="70197-162">實際*輸入*目錄存在，但 toohello hello 索引鍵名稱中的 hello 斜線字元顯示，因為它有 hello 外觀的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="70197-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="70197-163"><a id="benefits"></a>Azure 儲存體的優點</span><span class="sxs-lookup"><span data-stu-id="70197-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="70197-164">hello 隱含不共計算叢集和儲存體資源的效能成本，只要 hello hello 計算叢集建立 hello Azure 區域，其中 hello 高速網路可讓內關閉 toohello 儲存體帳戶資源的方式hello 運算節點時很有效率 tooaccess hello Azure 儲存體內的資料。</span><span class="sxs-lookup"><span data-stu-id="70197-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="70197-165">有數個優點，而不是 HDFS 的 Azure 儲存體中儲存 hello 資料相關聯：</span><span class="sxs-lookup"><span data-stu-id="70197-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="70197-166">**資料重複使用及共用：** HDFS 中的 hello 資料則位於 hello 運算叢集。</span><span class="sxs-lookup"><span data-stu-id="70197-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="70197-167">只有 hello 應用程式具有存取 toohello 運算叢集可以使用 HDFS Api 使用 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="70197-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="70197-168">可以存取 Azure 儲存體中的 hello 資料，透過 hello HDFS 應用程式開發介面或是透過 hello [Blob Storage REST Api][blob-storage-restAPI]。</span><span class="sxs-lookup"><span data-stu-id="70197-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="70197-169">因此，應用程式 （包括其他 HDInsight 叢集） 和工具的較大的集可以是使用的 tooproduce 及取用 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="70197-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="70197-170">**資料封存：**將資料儲存在 Azure 儲存體可讓用來安全地刪除而不會遺失使用者資料的計算 toobe hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="70197-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="70197-171">**資料儲存體成本：** DFS 中儲存資料，如 hello 長期會比將 hello 資料儲存在 Azure 儲存體，因為運算叢集的 hello 成本高於 Azure 儲存體 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="70197-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="70197-172">此外，因為 hello 資料並沒有重新載入，每個計算叢集產生 toobe，您也會儲存資料載入成本。</span><span class="sxs-lookup"><span data-stu-id="70197-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="70197-173">**彈性向外延展：**雖然 HDFS 提供向外延展檔案系統、 hello 小數位數取決於您所建立的叢集節點的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="70197-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="70197-174">變更 hello 標尺可能會變得更複雜的程序比依賴 hello 彈性調整自動取得 Azure 儲存體中的功能。</span><span class="sxs-lookup"><span data-stu-id="70197-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="70197-175">**異地複寫：**Azure 儲存體可以進行異地複寫。</span><span class="sxs-lookup"><span data-stu-id="70197-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="70197-176">雖然這可讓您地理修復與資料冗餘，容錯移轉 toohello 進行地理複寫的位置會嚴重影響效能，而且它可能會產生額外費用。</span><span class="sxs-lookup"><span data-stu-id="70197-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="70197-177">讓我們的建議是好好 toochoose hello 地理複寫，只有當 hello 資料值的 hello 值得 hello 額外成本。</span><span class="sxs-lookup"><span data-stu-id="70197-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="70197-178">某些 MapReduce 作業和封裝可能會建立不真的想 toostore Azure 儲存體中的中繼結果。</span><span class="sxs-lookup"><span data-stu-id="70197-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="70197-179">情況下，您可以選擇在 toostore hello 資料 hello 本機 HDFS。</span><span class="sxs-lookup"><span data-stu-id="70197-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="70197-180">事實上，在 Hive 工作和其他程序中，HDInsight 會使用 DFS 來儲存許多這些中繼結果。</span><span class="sxs-lookup"><span data-stu-id="70197-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="70197-181">大部分 HDFS 命令 (例如，<b>ls</b>、<b>copyFromLocal</b> 和 <b>mkdir</b>) 仍可正常運作。</span><span class="sxs-lookup"><span data-stu-id="70197-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="70197-182">只有 hello 命令特定 toohello 原生 HDFS 實作 （此為參考的 tooas DFS），例如<b>fschk</b>和<b>dfsadmin</b>，在 Azure 儲存體中顯示不同的行為。</span><span class="sxs-lookup"><span data-stu-id="70197-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="70197-183">建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="70197-183">Create Blob containers</span></span>
<span data-ttu-id="70197-184">toouse blob，您先建立[Azure 儲存體帳戶][azure-storage-create]。</span><span class="sxs-lookup"><span data-stu-id="70197-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="70197-185">這個過程，您可以指定 hello 儲存體帳戶建立所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="70197-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="70197-186">hello 叢集和 hello 儲存體帳戶必須裝載在 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="70197-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="70197-187">hello Hive 中繼存放區的 SQL Server 資料庫和 Oozie 中繼存放區的 SQL Server 資料庫必須也位於 hello 相同的區域。</span><span class="sxs-lookup"><span data-stu-id="70197-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="70197-188">它存在的話，每當您建立每個 blob 所屬 tooa Azure 儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="70197-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="70197-189">此容器可能是在 HDInsight 外建立的現有 Blob，也可能是為 HDInsight 叢集建立的容器。</span><span class="sxs-lookup"><span data-stu-id="70197-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="70197-190">hello 預設 Blob 容器儲存叢集特定資訊，例如作業歷程記錄和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="70197-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="70197-191">不要與多個 HDInsight 叢集共用預設 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="70197-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="70197-192">這可能會損毀作業歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="70197-192">This might corrupt job history.</span></span> <span data-ttu-id="70197-193">建議的 toouse 不同的容器，每個叢集，並將共用的資料放在部署的所有相關的叢集，而不是 hello 預設儲存體帳戶中指定的連結儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70197-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="70197-194">如需如何設定連結儲存體帳戶的詳細資訊，請參閱[建立 HDInsight 叢集][hdinsight-creation]。</span><span class="sxs-lookup"><span data-stu-id="70197-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="70197-195">不過您之後可以重複使用的預設儲存體容器 hello 原始的 HDInsight 叢集已被刪除。</span><span class="sxs-lookup"><span data-stu-id="70197-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="70197-196">HBase 叢集，您實際上可以藉由建立使用已刪除 HBase 叢集所用的 hello 預設 blob 容器的新 HBase 叢集保留 hello HBase 資料表的結構描述和資料。</span><span class="sxs-lookup"><span data-stu-id="70197-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="70197-197">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="70197-197">Use hello Azure portal</span></span>
<span data-ttu-id="70197-198">當從 hello 入口網站中建立的 HDInsight 叢集，您可以 hello 選項 （如下所示） tooprovide hello 儲存體帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="70197-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="70197-199">您也可以指定是否要與 hello 叢集相關聯的額外儲存體帳戶，以及若是如此，選擇 從資料湖存放區或另一個 Azure 儲存體 blob，作為 hello 額外的存放裝置。</span><span class="sxs-lookup"><span data-stu-id="70197-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![HDinsight hadoop 建立資料來源](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="70197-201">不支援在 hello HDInsight 叢集以外的不同位置中使用額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70197-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="70197-202">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="70197-202">Use Azure PowerShell</span></span>
<span data-ttu-id="70197-203">如果您[安裝及設定 Azure PowerShell][powershell-install]，您可以使用儲存體帳戶和容器中的 hello Azure PowerShell 提示 toocreate 下列 hello:</span><span class="sxs-lookup"><span data-stu-id="70197-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="70197-204">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="70197-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="70197-205">如果您有[安裝並設定 hello Azure CLI](../cli-install-nodejs.md)，hello 下列命令可以使用的 tooa 儲存體帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="70197-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="70197-206">hello`--type`參數表示 hello 儲存體帳戶複寫的方式。</span><span class="sxs-lookup"><span data-stu-id="70197-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="70197-207">如需詳細資訊，請參閱 [Azure 儲存體複寫](../storage/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="70197-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="70197-208">請勿使用 ZRS，因為 ZRS 不支援分頁 Blob、檔案、資料表或佇列。</span><span class="sxs-lookup"><span data-stu-id="70197-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="70197-209">您必須提示的 toospecify hello 地理區域中建立 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70197-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="70197-210">您應該建立 hello 儲存體帳戶中 hello 您計劃建立您的 HDInsight 叢集的同一個地區。</span><span class="sxs-lookup"><span data-stu-id="70197-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="70197-211">Hello 儲存體帳戶建立之後，請使用下列命令 tooretrieve hello 儲存體帳戶金鑰的 hello:</span><span class="sxs-lookup"><span data-stu-id="70197-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="70197-212">toocreate 容器，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="70197-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="70197-213">定址 Azure 儲存體中的檔案</span><span class="sxs-lookup"><span data-stu-id="70197-213">Address files in Azure storage</span></span>
<span data-ttu-id="70197-214">存取 Azure 儲存體中的檔案從 HDInsight hello URI 配置為：</span><span class="sxs-lookup"><span data-stu-id="70197-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="70197-215">hello URI 配置提供未加密的存取 (以 hello *wasb:*前置詞)，SSL 加密存取 (使用*wasbs*)。</span><span class="sxs-lookup"><span data-stu-id="70197-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="70197-216">我們建議您使用*wasbs*只要做得到，即使在存取內部的資料 hello Azure 中相同的區域。</span><span class="sxs-lookup"><span data-stu-id="70197-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="70197-217">hello &lt;BlobStorageContainerName&gt;識別 hello Azure 儲存體中的 hello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="70197-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="70197-218">hello &lt;StorageAccountName&gt;識別 hello Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="70197-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="70197-219">需要使用完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="70197-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="70197-220">如果沒有&lt;BlobStorageContainerName&gt;也&lt;StorageAccountName&gt;已指定，會使用 hello 預設檔案系統。</span><span class="sxs-lookup"><span data-stu-id="70197-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="70197-221">Hello hello 預設檔案系統上的檔案，您可以使用相對路徑或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="70197-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="70197-222">例如，hello *hadoop-mapreduce-examples.jar*隨附的 HDInsight 叢集的檔案可以參考的 tooby 使用 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="70197-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="70197-223">hello 檔案名稱為<i>hadoop examples.jar</i>中 2.1 和 1.6 版的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="70197-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="70197-224">hello&lt;路徑&gt;hello 檔案或目錄 HDFS 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="70197-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="70197-225">因為 Azure 儲存體中的容器僅是機碼值存放區，所以並沒有真正的階層式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="70197-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="70197-226">Blob 機碼內的斜線字元 ( / ) 會被解釋為目錄分隔符號。</span><span class="sxs-lookup"><span data-stu-id="70197-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="70197-227">例如，hello blob 名稱*hadoop-mapreduce-examples.jar*是：</span><span class="sxs-lookup"><span data-stu-id="70197-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="70197-228">當使用 HDInsight 外部 blob，大部分的公用程式不要辨識 hello WASB 格式和改為預期為基本的路徑格式，例如`example/jars/hadoop-mapreduce-examples.jar`。</span><span class="sxs-lookup"><span data-stu-id="70197-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="70197-229">存取 blob</span><span class="sxs-lookup"><span data-stu-id="70197-229">Access blobs</span></span> 


### <span data-ttu-id="70197-230"><a name="access-blobs-using-azure-powershell"></a> 使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="70197-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="70197-231">本章節中的 hello 命令提供使用 PowerShell tooaccess 資料儲存在 blob 中的基本範例。</span><span class="sxs-lookup"><span data-stu-id="70197-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="70197-232">如需更完整範例使用 HDInsight 的自訂，請參閱 hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools)。</span><span class="sxs-lookup"><span data-stu-id="70197-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="70197-233">使用下列命令 toolist hello 與 blob 相關 cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="70197-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![與 Blob 相關的 Power Shell Cmdlet 清單。][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="70197-235">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="70197-235">Upload files</span></span>
<span data-ttu-id="70197-236">請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="70197-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="70197-237">下載檔案</span><span class="sxs-lookup"><span data-stu-id="70197-237">Download files</span></span>
<span data-ttu-id="70197-238">hello 下列指令碼下載的區塊 blob toohello 目前資料夾。</span><span class="sxs-lookup"><span data-stu-id="70197-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="70197-239">執行 hello 指令碼，才能變更 hello 目錄 tooa 資料夾具有寫入權限。</span><span class="sxs-lookup"><span data-stu-id="70197-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="70197-240">提供 hello 資源群組名稱和 hello 叢集名稱，您可以使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="70197-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="70197-241">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="70197-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="70197-242">列出檔案</span><span class="sxs-lookup"><span data-stu-id="70197-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="70197-243">使用未定義的儲存體帳戶執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="70197-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="70197-244">這個範例會示範如何 toolist 期間未定義的儲存體帳戶中的資料夾 hello 建立程序。</span><span class="sxs-lookup"><span data-stu-id="70197-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="70197-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="70197-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="70197-246">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="70197-246">Use Azure CLI</span></span>
<span data-ttu-id="70197-247">使用下列命令 toolist hello 與 blob 相關命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="70197-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="70197-248">**使用 Azure CLI tooupload 檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="70197-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="70197-249">**使用 Azure CLI toodownload 檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="70197-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="70197-250">**使用 Azure CLI toodelete 檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="70197-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="70197-251">**使用 Azure CLI toolist 檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="70197-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="70197-252">使用其他儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="70197-252">Use additional storage accounts</span></span>

<span data-ttu-id="70197-253">在建立時的 HDInsight 叢集，您可以指定您想要與其 tooassociate hello Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70197-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="70197-254">此外 toothis 儲存體帳戶，您可以加入額外的儲存體帳戶從 hello 相同 Azure 訂用帳戶或不同的 Azure 訂閱 hello 建立程序期間，或在建立叢集之後。</span><span class="sxs-lookup"><span data-stu-id="70197-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="70197-255">如需關於新增其他儲存體帳戶的指示，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="70197-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="70197-256">不支援在 hello HDInsight 叢集以外的不同位置中使用額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="70197-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70197-257">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70197-257">Next steps</span></span>
<span data-ttu-id="70197-258">在本文中，您學到如何 toouse HDFS 相容與 HDInsight 的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="70197-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="70197-259">這可讓您 toobuild 可擴充、 長期來看，保存資料擷取方案和使用 HDInsight toounlock hello 內部資訊 hello 儲存結構化和非結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="70197-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="70197-260">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="70197-260">For more information, see:</span></span>

* <span data-ttu-id="70197-261">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="70197-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="70197-262">開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="70197-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="70197-263">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="70197-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="70197-264">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="70197-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="70197-265">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="70197-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="70197-266">[使用 Azure 儲存體共用存取簽章 toorestrict 存取 toodata 與 HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="70197-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
