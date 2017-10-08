---
title: "aaaUse Azure HDInsight 中的 Hadoop 資料湖存放區 |Microsoft 文件"
description: "了解如何從 Azure Data Lake Store 和 toostore tooquery 資料產生您的分析。"
keywords: "blob 儲存體,hdfs,結構化資料,非結構化資料, data lake store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="ea3aa-104">使用 Data Lake Store 搭配 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="ea3aa-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="ea3aa-105">tooanalyze HDInsight 叢集中的資料，您可以儲存 hello 資料可以是在[Azure 儲存體](../storage/common/storage-introduction.md)， [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)，或兩者。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="ea3aa-106">這兩個儲存體選項可讓您 toosafely 刪除 HDInsight 叢集所使用的計算，而不會遺失使用者資料。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="ea3aa-107">在本文中，您將了解 Data Lake Store 與 HDInsight 叢集搭配運作的方式。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="ea3aa-108">toolearn Azure 儲存體如何使用 HDInsight 叢集，請參閱[使用 Azure 儲存體與 Azure HDInsight 叢集](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="ea3aa-109">如需建立 HDInsight 叢集的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ea3aa-110">Data Lake Store 一律透過安全通道存取，因此不會有 `adls` 檔案系統配置名稱。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="ea3aa-111">您會一律使用 `adl`。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="ea3aa-112">HDInsight 叢集的可用性</span><span class="sxs-lookup"><span data-stu-id="ea3aa-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="ea3aa-113">Hadoop 支援 hello 預設檔案系統的概念。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="ea3aa-114">hello 預設的檔案系統表示預設配置和授權單位。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="ea3aa-115">它也可以使用的 tooresolve 相對路徑。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="ea3aa-116">在 hello HDInsight 叢集建立程序，您可以指定 blob 容器 hello 預設檔案系統中，為 Azure 儲存體中或使用 HDInsight 3.5 及較新版本，您可以選取 Azure 儲存體或 Azure Data Lake Store hello 預設檔案系統少數的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="ea3aa-117">HDInsight 叢集可透過兩種方式來使用 Data Lake Store︰</span><span class="sxs-lookup"><span data-stu-id="ea3aa-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="ea3aa-118">為 hello 預設儲存體</span><span class="sxs-lookup"><span data-stu-id="ea3aa-118">As hello default storage</span></span>
* <span data-ttu-id="ea3aa-119">作為其他儲存體，搭配 Azure 儲存體 Blob 作為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="ea3aa-120">目前，只有部分 hello HDInsight 叢集做為預設儲存體和其他儲存體帳戶中使用 Data Lake Store 的類型/版本支援：</span><span class="sxs-lookup"><span data-stu-id="ea3aa-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="ea3aa-121">HDInsight 叢集類型</span><span class="sxs-lookup"><span data-stu-id="ea3aa-121">HDInsight cluster type</span></span> | <span data-ttu-id="ea3aa-122">Data Lake Store 作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="ea3aa-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="ea3aa-123">Data Lake Store 作為其他儲存體</span><span class="sxs-lookup"><span data-stu-id="ea3aa-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="ea3aa-124">注意事項</span><span class="sxs-lookup"><span data-stu-id="ea3aa-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="ea3aa-125">HDInsight 3.6 版</span><span class="sxs-lookup"><span data-stu-id="ea3aa-125">HDInsight version 3.6</span></span> | <span data-ttu-id="ea3aa-126">是</span><span class="sxs-lookup"><span data-stu-id="ea3aa-126">Yes</span></span> | <span data-ttu-id="ea3aa-127">是</span><span class="sxs-lookup"><span data-stu-id="ea3aa-127">Yes</span></span> | |
| <span data-ttu-id="ea3aa-128">HDInsight 3.5 版</span><span class="sxs-lookup"><span data-stu-id="ea3aa-128">HDInsight version 3.5</span></span> | <span data-ttu-id="ea3aa-129">是</span><span class="sxs-lookup"><span data-stu-id="ea3aa-129">Yes</span></span> | <span data-ttu-id="ea3aa-130">是</span><span class="sxs-lookup"><span data-stu-id="ea3aa-130">Yes</span></span> | <span data-ttu-id="ea3aa-131">發生的 HBase hello 例外狀況</span><span class="sxs-lookup"><span data-stu-id="ea3aa-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="ea3aa-132">HDInsight 3.4 版</span><span class="sxs-lookup"><span data-stu-id="ea3aa-132">HDInsight version 3.4</span></span> | <span data-ttu-id="ea3aa-133">否</span><span class="sxs-lookup"><span data-stu-id="ea3aa-133">No</span></span> | <span data-ttu-id="ea3aa-134">是</span><span class="sxs-lookup"><span data-stu-id="ea3aa-134">Yes</span></span> | |
| <span data-ttu-id="ea3aa-135">HDInsight 3.3 版</span><span class="sxs-lookup"><span data-stu-id="ea3aa-135">HDInsight version 3.3</span></span> | <span data-ttu-id="ea3aa-136">否</span><span class="sxs-lookup"><span data-stu-id="ea3aa-136">No</span></span> | <span data-ttu-id="ea3aa-137">否</span><span class="sxs-lookup"><span data-stu-id="ea3aa-137">No</span></span> | |
| <span data-ttu-id="ea3aa-138">HDInsight 3.2 版</span><span class="sxs-lookup"><span data-stu-id="ea3aa-138">HDInsight version 3.2</span></span> | <span data-ttu-id="ea3aa-139">否</span><span class="sxs-lookup"><span data-stu-id="ea3aa-139">No</span></span> | <span data-ttu-id="ea3aa-140">是</span><span class="sxs-lookup"><span data-stu-id="ea3aa-140">Yes</span></span> | |
| <span data-ttu-id="ea3aa-141">HDInsight 進階版 (層級)</span><span class="sxs-lookup"><span data-stu-id="ea3aa-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="ea3aa-142">否</span><span class="sxs-lookup"><span data-stu-id="ea3aa-142">No</span></span> | <span data-ttu-id="ea3aa-143">否</span><span class="sxs-lookup"><span data-stu-id="ea3aa-143">No</span></span> | |
| <span data-ttu-id="ea3aa-144">Storm</span><span class="sxs-lookup"><span data-stu-id="ea3aa-144">Storm</span></span> | | |<span data-ttu-id="ea3aa-145">您可以使用 Data Lake Store toowrite 資料從 Storm 拓撲。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="ea3aa-146">您也可以使用 Data Lake Store 做為參考資料，該資料稍後可以由 Storm 拓撲讀取。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="ea3aa-147">做為額外的儲存體帳戶中使用資料湖存放區不會影響效能或 hello 能力 tooread 或從 hello 叢集寫入 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="ea3aa-148">使用 Data Lake Store 作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="ea3aa-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="ea3aa-149">HDInsight 當做預設儲存體的資料湖存放區與部署時，hello 叢集相關的檔案儲存在資料湖存放區在下列位置的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea3aa-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="ea3aa-150">其中`<cluster_root_path>`hello 資料湖存放區中建立的資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="ea3aa-151">藉由指定 根的路徑為每個叢集，您可以使用 hello 多個叢集相同的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="ea3aa-152">因此在您的設定中︰</span><span class="sxs-lookup"><span data-stu-id="ea3aa-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="ea3aa-153">Cluster1 可以使用 hello 路徑`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="ea3aa-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="ea3aa-154">Cluster2 可以使用 hello 路徑`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="ea3aa-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="ea3aa-155">請注意同時 hello 叢集使用 hello 相同 Data Lake Store 帳戶**mydatalakestore**。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="ea3aa-156">每個群集都有存取 tooits 擁有資料湖存放區中的根檔案系統。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="ea3aa-157">hello Azure 入口網站的部署經驗尤其會提示您 toouse 資料夾名稱例如**/clusters/\<clustername >** hello 根路徑。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="ea3aa-158">toobe 無法 toouse 當做預設儲存體的資料湖存放區，您必須授與 hello 服務主體存取 toohello 下列路徑：</span><span class="sxs-lookup"><span data-stu-id="ea3aa-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="ea3aa-159">hello Data Lake Store 帳戶的根。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="ea3aa-160">例如：adl://mydatalakestore/。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="ea3aa-161">叢集的所有資料夾的 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="ea3aa-162">例如：adl://mydatalakestore/clusters。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="ea3aa-163">hello 叢集 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="ea3aa-164">例如：adl://mydatalakestore/clusters/cluster1storage。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="ea3aa-165">如需建立服務主體和授與存取權的詳細資訊，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="ea3aa-166">使用 Data Lake Store 作為其他儲存體</span><span class="sxs-lookup"><span data-stu-id="ea3aa-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="ea3aa-167">您可以使用做為額外的存放裝置的 Data Lake Store 的 hello 叢集中。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="ea3aa-168">在這種情況下，hello 叢集預設儲存體可以是 Azure 儲存體 Blob 或 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="ea3aa-169">如果您針對儲存在資料湖存放區做為額外的存放裝置中的 hello 資料執行 HDInsight 工作，您必須使用 hello 的完整路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="ea3aa-170">例如：</span><span class="sxs-lookup"><span data-stu-id="ea3aa-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="ea3aa-171">請注意，沒有任何**cluster_root_path**現在 hello URL 中。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="ea3aa-172">這是因為資料湖存放區不是預設儲存體在此情況下，您只需要 toodo 是提供 hello 路徑 toohello 檔案。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="ea3aa-173">toobe 無法 toouse 資料湖存放區做為額外的存放裝置，您只需要 toogrant hello 服務主體存取 toohello 路徑儲存您的檔案。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="ea3aa-174">例如：</span><span class="sxs-lookup"><span data-stu-id="ea3aa-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="ea3aa-175">如需建立服務主體和授與存取權的詳細資訊，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="ea3aa-176">使用多個 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="ea3aa-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="ea3aa-177">將 Data Lake Store 帳戶新增為其他並加入一個以上的 Data Lake Store 帳戶被透過一或多個 Data Lake Store 帳戶中的資料賦予 hello HDInsight 叢集的權限。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="ea3aa-178">請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="ea3aa-179">設定 Data Lake Store 存取</span><span class="sxs-lookup"><span data-stu-id="ea3aa-179">Configure Data Lake store access</span></span>

<span data-ttu-id="ea3aa-180">tooconfigure 資料湖存放區存取，從您的 HDInsight 叢集，您必須擁有 Azure Active directory (Azure AD) 服務主體。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="ea3aa-181">只有 Azure AD 系統管理員才可以建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="ea3aa-182">必須使用憑證建立 hello 服務主體。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="ea3aa-183">如需詳細資訊，請參閱[設定 Data Lake Store 存取](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access)，和[使用自我簽署憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="ea3aa-184">如果您正在 toouse Azure Data Lake Store 為 HDInsight 叢集的其他存放裝置中，我們強烈建議您採用這種這篇文章中所述，建立 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="ea3aa-185">將 Azure Data Lake Store 新增額外的儲存體 tooan 為現有 HDInsight 叢集是複雜的程序和 tooerrors 容易出錯。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="ea3aa-186">Hello 叢集存取檔案</span><span class="sxs-lookup"><span data-stu-id="ea3aa-186">Access files from hello cluster</span></span>

<span data-ttu-id="ea3aa-187">有數種方式，您可以存取資料湖存放區中的 hello 檔案從 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="ea3aa-188">**使用完整限定的名稱的 hello**。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="ea3aa-189">使用此方法時，您會提供 hello 完整路徑 toohello 檔想 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="ea3aa-190">**使用 hello 縮短的路徑格式**。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="ea3aa-191">使用此方法時，您 hello 路徑取代向上 toohello 叢集根目錄 adl: / /。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="ea3aa-192">因此，在 hello 上述範例中，您可以取代`adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/`與`adl:///`。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="ea3aa-193">**使用相對路徑的 hello**。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-193">**Using hello relative path**.</span></span> <span data-ttu-id="ea3aa-194">使用此方法時，您只提供 hello 相對路徑 toohello 檔案要 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="ea3aa-195">例如，如果 hello 完整路徑 toohello 檔案：</span><span class="sxs-lookup"><span data-stu-id="ea3aa-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="ea3aa-196">您可以存取相同 sample.log 檔案 hello 改為使用這個相對路徑。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="ea3aa-197">建立 HDInsight 叢集使用存取 tooData 湖存放區</span><span class="sxs-lookup"><span data-stu-id="ea3aa-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="ea3aa-198">使用 hello 遵循上 toocreate HDInsight 叢集，以存取 tooData 湖存放區的方式的詳細指示的連結。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="ea3aa-199">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="ea3aa-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="ea3aa-200">使用 PowerShell (搭配 Data Lake Store 做為預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="ea3aa-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="ea3aa-201">使用 PowerShell (搭配 Data Lake Store 做為其他儲存體)</span><span class="sxs-lookup"><span data-stu-id="ea3aa-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="ea3aa-202">使用 Azure 範本</span><span class="sxs-lookup"><span data-stu-id="ea3aa-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="ea3aa-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea3aa-203">Next steps</span></span>
<span data-ttu-id="ea3aa-204">在本文中，您學到如何 toouse HDFS 相容 Azure Data Lake Store 的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="ea3aa-205">這可讓您 toobuild 可擴充、 長期來看，保存資料擷取方案和使用 HDInsight toounlock hello 內部資訊 hello 儲存結構化和非結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="ea3aa-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="ea3aa-206">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ea3aa-206">For more information, see:</span></span>

* <span data-ttu-id="ea3aa-207">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ea3aa-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="ea3aa-208">開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ea3aa-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="ea3aa-209">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ea3aa-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ea3aa-210">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ea3aa-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="ea3aa-211">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ea3aa-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ea3aa-212">[使用 Azure 儲存體共用存取簽章 toorestrict 存取 toodata 與 HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="ea3aa-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
