---
title: "從 HDFS 相容的 Azure 儲存體查詢資料 - Azure HDInsight | Microsoft Docs"
description: "了解如何從 Azure 儲存體和 Azure Data Lake Store 查詢資料以儲存分析的結果。"
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
ms.openlocfilehash: a44c2b363f7ebb593b9a9c5bd9e0d4fc3b4c31bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="790fb-104">搭配 Azure HDInsight 叢集使用 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="790fb-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="790fb-105">若要分析 HDInsight 叢集中的資料，您可以在 Azure 儲存體、Azure Data Lake Store，或兩者中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="790fb-106">這兩種儲存體選項都可讓您安全地刪除用於計算的 HDInsight 叢集，而不會遺失使用者資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="790fb-107">Hadoop 支援預設檔案系統的概念。</span><span class="sxs-lookup"><span data-stu-id="790fb-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="790fb-108">預設檔案系統意指預設配置和授權。</span><span class="sxs-lookup"><span data-stu-id="790fb-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="790fb-109">也可用來解析相對路徑。</span><span class="sxs-lookup"><span data-stu-id="790fb-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="790fb-110">進行 HDInsight 叢集建立程序時，您可以指定 Azure Blob 儲存體中的 Blob 容器作為預設檔案系統，或在使用 HDInsight 3.5 時，選取 Azure 儲存體或 Azure Data Lake Store 作為預設檔案系統，有一些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="790fb-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> <span data-ttu-id="790fb-111">如需了解使用 Data Lake Store 作為預設及連結儲存體的支援能力，請參閱 [HDInsight 叢集的可用性](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters)。</span><span class="sxs-lookup"><span data-stu-id="790fb-111">For the supportability of using Data Lake Store as both the default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="790fb-112">在本文中，您將了解 Azure 儲存體與 HDInsight 叢集搭配運作的方式。</span><span class="sxs-lookup"><span data-stu-id="790fb-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="790fb-113">若要深入了解 Data Lake Store 與 HDInsight 叢集搭配運作的方式，請參閱[使用 Azure Data Lake Store 搭配 Azure HDInsight 叢集](hdinsight-hadoop-use-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="790fb-113">To learn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="790fb-114">如需建立 HDInsight 叢集的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="790fb-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="790fb-115">Azure 儲存體是強大的一般用途儲存體解決方案，其完美整合了 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="790fb-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="790fb-116">HDInsight 可以使用 Azure 儲存體中的 Blob 容器做為叢集的預設檔案系統。</span><span class="sxs-lookup"><span data-stu-id="790fb-116">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="790fb-117">透過 Hadoop 分散式檔案系統 (HDFS) 介面，HDInsight 中的完整元件集可直接處理儲存為 Blob 的結構化或非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-117">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="790fb-118">建立 Azure 儲存體帳戶時，有數個選項可供使用。</span><span class="sxs-lookup"><span data-stu-id="790fb-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="790fb-119">下表提供 HDInsight 所支援選項的相關資訊︰</span><span class="sxs-lookup"><span data-stu-id="790fb-119">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="790fb-120">儲存體帳戶類型</span><span class="sxs-lookup"><span data-stu-id="790fb-120">Storage account type</span></span> | <span data-ttu-id="790fb-121">儲存層</span><span class="sxs-lookup"><span data-stu-id="790fb-121">Storage tier</span></span> | <span data-ttu-id="790fb-122">支援 HDInsight</span><span class="sxs-lookup"><span data-stu-id="790fb-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="790fb-123">一般用途的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="790fb-123">General-purpose Storage Account</span></span> | <span data-ttu-id="790fb-124">標準</span><span class="sxs-lookup"><span data-stu-id="790fb-124">Standard</span></span> | <span data-ttu-id="790fb-125">__是__</span><span class="sxs-lookup"><span data-stu-id="790fb-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="790fb-126">進階</span><span class="sxs-lookup"><span data-stu-id="790fb-126">Premium</span></span> | <span data-ttu-id="790fb-127">否</span><span class="sxs-lookup"><span data-stu-id="790fb-127">No</span></span> |
> | <span data-ttu-id="790fb-128">Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="790fb-128">Blob Storage Account</span></span> | <span data-ttu-id="790fb-129">經常性存取</span><span class="sxs-lookup"><span data-stu-id="790fb-129">Hot</span></span> | <span data-ttu-id="790fb-130">否</span><span class="sxs-lookup"><span data-stu-id="790fb-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="790fb-131">非經常性存取</span><span class="sxs-lookup"><span data-stu-id="790fb-131">Cool</span></span> | <span data-ttu-id="790fb-132">否</span><span class="sxs-lookup"><span data-stu-id="790fb-132">No</span></span> |

<span data-ttu-id="790fb-133">不建議您使用預設的 Blob 容器來儲存商務資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-133">We do not recommend that you use the default blob container for storing business data.</span></span> <span data-ttu-id="790fb-134">最好在每次使用後刪除預設的 Blob 容器，以減少儲存成本。</span><span class="sxs-lookup"><span data-stu-id="790fb-134">Deleting the default blob container after each use to reduce storage cost is a good practice.</span></span> <span data-ttu-id="790fb-135">請注意，預設容器包含應用程式與系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="790fb-135">Note that the default container contains application and system logs.</span></span> <span data-ttu-id="790fb-136">請務必先擷取記錄檔再刪除容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-136">Make sure to retrieve the logs before deleting the container.</span></span>

<span data-ttu-id="790fb-137">不支援多個叢集共用一個 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="790fb-138">HDInsight 儲存架構</span><span class="sxs-lookup"><span data-stu-id="790fb-138">HDInsight storage architecture</span></span>
<span data-ttu-id="790fb-139">下圖提供使用 Azure 儲存體之 HDInsight 儲存架構的摘要檢視：</span><span class="sxs-lookup"><span data-stu-id="790fb-139">The following diagram provides an abstract view of the HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="790fb-140">![Hadoop 叢集會使用 HDFS API 來存取和儲存 Blob 儲存體中的結構化和非結構化資料。](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight 儲存體架構")</span><span class="sxs-lookup"><span data-stu-id="790fb-140">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="790fb-141">HDInsight 可以存取本機連接至計算節點的分散式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="790fb-141">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="790fb-142">可使用完整 URI 來存取此檔案系統，例如：</span><span class="sxs-lookup"><span data-stu-id="790fb-142">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="790fb-143">此外，HDInsight 也能讓您存取儲存在 Azure 儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-143">In addition, HDInsight allows you to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="790fb-144">語法為：</span><span class="sxs-lookup"><span data-stu-id="790fb-144">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="790fb-145">以下是搭配 HDInsight 叢集使用 Azure 儲存體帳戶時的一些考量。</span><span class="sxs-lookup"><span data-stu-id="790fb-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="790fb-146">**儲存體帳戶中連線至叢集的容器：** 因為在建立期間帳戶名稱和金鑰會與叢集相關聯，所以您對這些容器中的 Blob 具有完整存取權。</span><span class="sxs-lookup"><span data-stu-id="790fb-146">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="790fb-147">**儲存體帳戶中未連線至叢集的公用容器或公用 Blob：** 您對容器中的 Blob 只有唯讀權限。</span><span class="sxs-lookup"><span data-stu-id="790fb-147">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="790fb-148">公用容器可讓您取得該容器中所有可用的 Blob 清單，並取得容器中繼資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-148">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="790fb-149">公用 Blob 只在您知道確切的 URL 時才可讓您存取 Blob。</span><span class="sxs-lookup"><span data-stu-id="790fb-149">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="790fb-150">如需詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">限制對容器和 Blob 的存取</a>。</span><span class="sxs-lookup"><span data-stu-id="790fb-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="790fb-151">**儲存體帳戶中未連接至叢集的私人容器：** 除非在提交 WebHCat 工作時定義儲存體帳戶，否則不能存取容器中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="790fb-151">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="790fb-152">稍後在本文中會加以說明。</span><span class="sxs-lookup"><span data-stu-id="790fb-152">This is explained later in this article.</span></span>

<span data-ttu-id="790fb-153">建立程序及其金鑰中定義的儲存體帳戶會儲存在叢集節點的 %HADOOP_HOME%/conf/core-site.xml 中。</span><span class="sxs-lookup"><span data-stu-id="790fb-153">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="790fb-154">HDInsight 的預設行為是使用 core-site.xml 檔案中定義的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="790fb-154">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="790fb-155">您可以使用 [Ambari](./hdinsight-hadoop-manage-ambari.md) 來修改此設定</span><span class="sxs-lookup"><span data-stu-id="790fb-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="790fb-156">多個 WebHCat 工作 (包括 Hive、MapReduce、Hadoop 資料流和 Pig) 可隨身夾帶儲存體帳戶的說明和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="790fb-157">(目前適用於含儲存體帳戶的 Pig，但不適用於中繼資料)。如需詳細資訊，請參閱 [在其他儲存體帳戶和 Metastores 上使用 HDInsight 叢集](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx)。</span><span class="sxs-lookup"><span data-stu-id="790fb-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="790fb-158">Blob 可使用於結構化和非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="790fb-159">Blob 容器以機碼/值組來儲存資料，沒有目錄階層。</span><span class="sxs-lookup"><span data-stu-id="790fb-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="790fb-160">但是，機碼名稱中可使用 ( / ) 斜線字元，使檔案變成好像儲存在目錄結構中一樣。</span><span class="sxs-lookup"><span data-stu-id="790fb-160">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="790fb-161">例如，Blob 的機碼可能是 *input/log1.txt*。</span><span class="sxs-lookup"><span data-stu-id="790fb-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="790fb-162">實際上， *input* 目錄並不存在，只是因為機碼名稱中有斜線字元，才形成檔案路徑的樣子。</span><span class="sxs-lookup"><span data-stu-id="790fb-162">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

## <span data-ttu-id="790fb-163"><a id="benefits"></a>Azure 儲存體的優點</span><span class="sxs-lookup"><span data-stu-id="790fb-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="790fb-164">計算叢集和儲存體叢集未並存於同處所隱含的效能損失，可經由將計算叢集建立到靠近 Azure 區域內的儲存體帳戶資源來彌補，其中的高速網路可讓計算節點有效率地存取 Azure 儲存體內的資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-164">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="790fb-165">將資料儲存在 Azure 儲存體而非 HDFS 有許多優點：</span><span class="sxs-lookup"><span data-stu-id="790fb-165">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="790fb-166">**資料重複使用和共用：** HDFS 中的資料位於計算叢集內。</span><span class="sxs-lookup"><span data-stu-id="790fb-166">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="790fb-167">只有可存取計算叢集的應用程式，才能利用 HDFS API 來使用資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-167">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="790fb-168">可透過 HDFS API 或 [Blob 儲存體 REST API][blob-storage-restAPI] 來存取 Azure 儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-168">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="790fb-169">因此，許多應用程式 (包括其他 HDInsight 叢集) 和工具都可用來產生和取用資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="790fb-170">**資料封存：** 將資料儲存在 Azure 儲存體中，可安全地刪除用於計算的 HDInsight 叢集，而不會遺失使用者資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-170">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="790fb-171">**資料儲存成本：** 長期將資料儲存在 DFS 中的成本高於將資料儲存在 Azure 儲存體中，因為計算叢集的成本高於 Azure 儲存體的成本。</span><span class="sxs-lookup"><span data-stu-id="790fb-171">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="790fb-172">此外，因為不需要每次產生計算叢集時都重新載入資料，也能節省資料載入成本。</span><span class="sxs-lookup"><span data-stu-id="790fb-172">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="790fb-173">**彈性向外延展：** 雖然HDFS 提供向外延展的檔案系統，但延展程度取決於您建立給叢集的節點數目。</span><span class="sxs-lookup"><span data-stu-id="790fb-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="790fb-174">變更延展程度較為複雜，可改用 Azure 儲存體自動提供的彈性延展功能。</span><span class="sxs-lookup"><span data-stu-id="790fb-174">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="790fb-175">**異地複寫：**Azure 儲存體可以進行異地複寫。</span><span class="sxs-lookup"><span data-stu-id="790fb-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="790fb-176">雖然這樣可支援地理位置復原和資料備援，但容錯移轉至異地複寫的位置會嚴重影響效能，且可能產生額外的成本。</span><span class="sxs-lookup"><span data-stu-id="790fb-176">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="790fb-177">因此，只有在資料的價值大於額外成本時，才建議您明智地選擇地理區域複寫。</span><span class="sxs-lookup"><span data-stu-id="790fb-177">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="790fb-178">某些 MapReduce 工作和封裝可能會產生中繼結果，但您並不真的想要將這些結果儲存在 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="790fb-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="790fb-179">在此情況下，您仍可選擇將資料儲存在本機 HDFS。</span><span class="sxs-lookup"><span data-stu-id="790fb-179">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="790fb-180">事實上，在 Hive 工作和其他程序中，HDInsight 會使用 DFS 來儲存許多這些中繼結果。</span><span class="sxs-lookup"><span data-stu-id="790fb-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="790fb-181">大部分 HDFS 命令 (例如，<b>ls</b>、<b>copyFromLocal</b> 和 <b>mkdir</b>) 仍可正常運作。</span><span class="sxs-lookup"><span data-stu-id="790fb-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="790fb-182">只有原生 HDFS 實作 (稱為 DFS) 的特定命令 (例如 <b>fschk</b> 和 <b>dfsadmin</b>) 才會在 Azure 儲存體上出現不同的行為。</span><span class="sxs-lookup"><span data-stu-id="790fb-182">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="790fb-183">建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="790fb-183">Create Blob containers</span></span>
<span data-ttu-id="790fb-184">若要使用 Blob，您必須先建立 [Azure 儲存體帳戶][azure-storage-create]。</span><span class="sxs-lookup"><span data-stu-id="790fb-184">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="790fb-185">在這個過程中，您可以指定建立儲存體帳戶所在的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="790fb-185">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="790fb-186">叢集與儲存體帳戶必須在相同區域內託管。</span><span class="sxs-lookup"><span data-stu-id="790fb-186">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="790fb-187">Hive 中繼存放區 SQL Server 資料庫和 Oozie 中繼存放區 SQL Server 資料庫也必須位在相同的區域內。</span><span class="sxs-lookup"><span data-stu-id="790fb-187">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="790fb-188">您所建立的每個 Blob 不論位於何處，都屬於 Azure 儲存體帳戶中的某個容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-188">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="790fb-189">此容器可能是在 HDInsight 外建立的現有 Blob，也可能是為 HDInsight 叢集建立的容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="790fb-190">預設 Blob 容器會儲存叢集特定資訊，例如作業歷程記錄和記錄。</span><span class="sxs-lookup"><span data-stu-id="790fb-190">The default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="790fb-191">不要與多個 HDInsight 叢集共用預設 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="790fb-192">這可能會損毀作業歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="790fb-192">This might corrupt job history.</span></span> <span data-ttu-id="790fb-193">建議您為每個叢集使用不同的容器，並在所有相關叢集的部署中指定的連結儲存體帳戶 (而不是預設儲存體帳戶) 上放置共用的資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-193">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="790fb-194">如需如何設定連結儲存體帳戶的詳細資訊，請參閱[建立 HDInsight 叢集][hdinsight-creation]。</span><span class="sxs-lookup"><span data-stu-id="790fb-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="790fb-195">不過，在刪除原始的 HDInsight 叢集後，您可以重複使用預設儲存容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-195">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="790fb-196">對於 HBase 叢集，您可以利用被刪除的 HBase 叢集使用的預設 Blob 容器來建立一個新的 HBase 叢集，藉此實際保留 HBase 資料表結構描述和資料。</span><span class="sxs-lookup"><span data-stu-id="790fb-196">For HBase clusters, you can actually retain the HBase table schema and data by creating a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-the-azure-portal"></a><span data-ttu-id="790fb-197">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="790fb-197">Use the Azure portal</span></span>
<span data-ttu-id="790fb-198">從入口網站建立 HDInsight 叢集時，您可以選擇要提供的儲存體帳戶詳細資料 (如下所示)。</span><span class="sxs-lookup"><span data-stu-id="790fb-198">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="790fb-199">您也可以指定是否要將其他儲存體帳戶與叢集相關聯，若是如此，可從 Data Lake Store 或另一個 Azure 儲存體 Blob 擇一做為額外的儲存體。</span><span class="sxs-lookup"><span data-stu-id="790fb-199">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![HDinsight hadoop 建立資料來源](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="790fb-201">不支援在與 HDInsight 叢集不同的位置中使用其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="790fb-201">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="790fb-202">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="790fb-202">Use Azure PowerShell</span></span>
<span data-ttu-id="790fb-203">如果您已[安裝和設定 Azure PowerShell][powershell-install]，您可以從 Azure PowerShell 提示字元使用下列程式碼來建立儲存體帳戶和容器：</span><span class="sxs-lookup"><span data-stu-id="790fb-203">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="790fb-204">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="790fb-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="790fb-205">如果您已 [安裝和設定 Azure CLI](../cli-install-nodejs.md)，下列命令即可用於儲存體帳戶和容器。</span><span class="sxs-lookup"><span data-stu-id="790fb-205">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="790fb-206">`--type` 參數表示儲存體帳戶的複寫方式。</span><span class="sxs-lookup"><span data-stu-id="790fb-206">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="790fb-207">如需詳細資訊，請參閱 [Azure 儲存體複寫](../storage/storage-redundancy.md)。</span><span class="sxs-lookup"><span data-stu-id="790fb-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="790fb-208">請勿使用 ZRS，因為 ZRS 不支援分頁 Blob、檔案、資料表或佇列。</span><span class="sxs-lookup"><span data-stu-id="790fb-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="790fb-209">系統會提示您指定將建立儲存體帳戶的地理區域。</span><span class="sxs-lookup"><span data-stu-id="790fb-209">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="790fb-210">您應該在您計劃建立 HDInsight 叢集的相同區域中建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="790fb-210">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="790fb-211">建立儲存體帳戶後，使用下列命令來抓取儲存體帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="790fb-211">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="790fb-212">若要建立容器，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="790fb-212">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="790fb-213">定址 Azure 儲存體中的檔案</span><span class="sxs-lookup"><span data-stu-id="790fb-213">Address files in Azure storage</span></span>
<span data-ttu-id="790fb-214">從 HDInsight 存取 Azure 儲存體中的檔案的 URI 配置如下：</span><span class="sxs-lookup"><span data-stu-id="790fb-214">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="790fb-215">URI 配置提供未加密存取 (使用 wasb: 首碼) 和 SSL 加密存取 (使用 wasbs)。</span><span class="sxs-lookup"><span data-stu-id="790fb-215">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="790fb-216">建議盡可能使用 wasbs  ，即使存取 Azure 中相同區域內的資料也一樣。</span><span class="sxs-lookup"><span data-stu-id="790fb-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="790fb-217">&lt;BlobStorageContainerName&gt; 可識別 Azure 儲存體中的 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="790fb-217">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="790fb-218">&lt;StorageAccountName&gt; 可識別 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="790fb-218">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="790fb-219">需要使用完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="790fb-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="790fb-220">如果 &lt;BlobStorageContainerName&gt; 和 &lt;StorageAccountName&gt; 都未指定，則會使用預設檔案系統。</span><span class="sxs-lookup"><span data-stu-id="790fb-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="790fb-221">對於預設檔案系統上的檔案，您可以使用相對路徑或絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="790fb-221">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="790fb-222">例如，可使用下列語法來參考 HDInsight 叢集隨附的 *hadoop-mapreduce-examples.jar* 檔案：</span><span class="sxs-lookup"><span data-stu-id="790fb-222">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="790fb-223">在 HDInsight 2.1 和 1.6 版叢集中的檔案名稱是 <i>hadoop-examples.jar</i>。</span><span class="sxs-lookup"><span data-stu-id="790fb-223">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="790fb-224">&lt;path&gt; 是檔案或目錄 HDFS 路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="790fb-224">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="790fb-225">因為 Azure 儲存體中的容器僅是機碼值存放區，所以並沒有真正的階層式檔案系統。</span><span class="sxs-lookup"><span data-stu-id="790fb-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="790fb-226">Blob 機碼內的斜線字元 ( / ) 會被解釋為目錄分隔符號。</span><span class="sxs-lookup"><span data-stu-id="790fb-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="790fb-227">例如， *hadoop-mapreduce-examples.jar* 的 Blob 名稱為：</span><span class="sxs-lookup"><span data-stu-id="790fb-227">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="790fb-228">在 HDInsight 外部使用 Blob 時，大部分的公用程式無法辨識 WASB 格式而改為預期基本的路徑格式，例如 `example/jars/hadoop-mapreduce-examples.jar`。</span><span class="sxs-lookup"><span data-stu-id="790fb-228">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="790fb-229">存取 blob</span><span class="sxs-lookup"><span data-stu-id="790fb-229">Access blobs</span></span> 


### <span data-ttu-id="790fb-230"><a name="access-blobs-using-azure-powershell"></a> 使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="790fb-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="790fb-231">本章中的命令會提供使用 PowerShell 來存取儲存在 Blob 中的資料的基本範例。</span><span class="sxs-lookup"><span data-stu-id="790fb-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="790fb-232">如需使用 HDInsight 的更完整範例，請參閱 [HDInsight 工具](https://github.com/Blackmist/hdinsight-tools)。</span><span class="sxs-lookup"><span data-stu-id="790fb-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="790fb-233">請使用下列命令來列出 Blob 相關的 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="790fb-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![與 Blob 相關的 Power Shell Cmdlet 清單。][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="790fb-235">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="790fb-235">Upload files</span></span>
<span data-ttu-id="790fb-236">請參閱[將資料上傳至 HDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="790fb-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="790fb-237">下載檔案</span><span class="sxs-lookup"><span data-stu-id="790fb-237">Download files</span></span>
<span data-ttu-id="790fb-238">下列指令碼會將區塊 Blob 下載至目前的資料夾。</span><span class="sxs-lookup"><span data-stu-id="790fb-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="790fb-239">執行指令碼之前，請將目錄變更為您具有寫入權限的資料夾。</span><span class="sxs-lookup"><span data-stu-id="790fb-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="790fb-240">提供資源群組名稱和叢集名稱，您可以使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="790fb-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="790fb-241">刪除檔案</span><span class="sxs-lookup"><span data-stu-id="790fb-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="790fb-242">列出檔案</span><span class="sxs-lookup"><span data-stu-id="790fb-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="790fb-243">使用未定義的儲存體帳戶執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="790fb-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="790fb-244">本範例說明如何從未在建立程序期間定義的儲存體帳戶列出資料夾。</span><span class="sxs-lookup"><span data-stu-id="790fb-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="790fb-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="790fb-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="790fb-246">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="790fb-246">Use Azure CLI</span></span>
<span data-ttu-id="790fb-247">請使用下列命令來列出 Blob 相關的命令：</span><span class="sxs-lookup"><span data-stu-id="790fb-247">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="790fb-248">**使用 Azure CLI 上傳檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="790fb-248">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="790fb-249">**使用 Azure CLI 下載檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="790fb-249">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="790fb-250">**使用 Azure CLI 刪除檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="790fb-250">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="790fb-251">**使用 Azure CLI 列出檔案的範例**</span><span class="sxs-lookup"><span data-stu-id="790fb-251">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="790fb-252">使用其他儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="790fb-252">Use additional storage accounts</span></span>

<span data-ttu-id="790fb-253">在建立 HDInsight 叢集時，您會指定要與它相關聯的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="790fb-253">While creating an HDInsight cluster, you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="790fb-254">除了此儲存體帳戶，您也可以在建立過程中或在叢集建立後，從相同或不同的 Azure 訂用帳戶中新增其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="790fb-254">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="790fb-255">如需關於新增其他儲存體帳戶的指示，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="790fb-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="790fb-256">不支援在與 HDInsight 叢集不同的位置中使用其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="790fb-256">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="790fb-257">後續步驟</span><span class="sxs-lookup"><span data-stu-id="790fb-257">Next steps</span></span>
<span data-ttu-id="790fb-258">在本文中，您已了解如何搭配 HDInsight 使用 HDFS 相容的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="790fb-258">In this article, you learned how to use HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="790fb-259">這可讓您建立可調整、長期封存的資料取得解決方案，並利用 HDInsight 來揭開儲存的結構化和非結構化資料內的資訊。</span><span class="sxs-lookup"><span data-stu-id="790fb-259">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="790fb-260">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="790fb-260">For more information, see:</span></span>

* <span data-ttu-id="790fb-261">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="790fb-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="790fb-262">開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="790fb-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="790fb-263">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="790fb-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="790fb-264">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="790fb-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="790fb-265">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="790fb-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="790fb-266">[使用 Azure 儲存體共用存取簽章來限制使用 HDInsight 對資料的存取][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="790fb-266">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
