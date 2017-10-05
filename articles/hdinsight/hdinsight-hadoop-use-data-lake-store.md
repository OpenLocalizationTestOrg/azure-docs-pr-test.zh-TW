---
title: "在 Azure HDInsight 中使用 Data Lake Store 搭配 Hadoop | Microsoft Docs"
description: "了解如何從 Azure Data Lake Store 查詢資料，以及如何儲存分析的結果。"
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
ms.openlocfilehash: 28a836aff65636ef0031ac63f633d746436d7e4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="f60c7-104">使用 Data Lake Store 搭配 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f60c7-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="f60c7-105">若要分析 HDInsight 叢集中的資料，您可以在 [Azure 儲存體](../storage/common/storage-introduction.md)、[Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)，或兩者中儲存資料。</span><span class="sxs-lookup"><span data-stu-id="f60c7-105">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="f60c7-106">這兩種儲存體選項都可讓您安全地刪除用於計算的 HDInsight 叢集，而不會遺失使用者資料。</span><span class="sxs-lookup"><span data-stu-id="f60c7-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="f60c7-107">在本文中，您將了解 Data Lake Store 與 HDInsight 叢集搭配運作的方式。</span><span class="sxs-lookup"><span data-stu-id="f60c7-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="f60c7-108">若要深入了解 Azure 儲存體與 HDInsight 叢集搭配運作的方式，請參閱[使用 Azure 儲存體搭配 Azure HDInsight 叢集](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="f60c7-108">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="f60c7-109">如需建立 HDInsight 叢集的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="f60c7-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f60c7-110">Data Lake Store 一律透過安全通道存取，因此不會有 `adls` 檔案系統配置名稱。</span><span class="sxs-lookup"><span data-stu-id="f60c7-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="f60c7-111">您會一律使用 `adl`。</span><span class="sxs-lookup"><span data-stu-id="f60c7-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="f60c7-112">HDInsight 叢集的可用性</span><span class="sxs-lookup"><span data-stu-id="f60c7-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="f60c7-113">Hadoop 支援預設檔案系統的概念。</span><span class="sxs-lookup"><span data-stu-id="f60c7-113">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="f60c7-114">預設檔案系統意指預設配置和授權。</span><span class="sxs-lookup"><span data-stu-id="f60c7-114">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="f60c7-115">也可用來解析相對路徑。</span><span class="sxs-lookup"><span data-stu-id="f60c7-115">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="f60c7-116">進行 HDInsight 叢集建立程序時，您可以指定 Azure Blob 儲存體中的 Blob 容器作為預設檔案系統，或在使用 HDInsight 3.5 和更新版本時，選取 Azure 儲存體或 Azure Data Lake Store 作為預設檔案系統，有一些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f60c7-116">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> 

<span data-ttu-id="f60c7-117">HDInsight 叢集可透過兩種方式來使用 Data Lake Store︰</span><span class="sxs-lookup"><span data-stu-id="f60c7-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="f60c7-118">作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="f60c7-118">As the default storage</span></span>
* <span data-ttu-id="f60c7-119">作為其他儲存體，搭配 Azure 儲存體 Blob 作為預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="f60c7-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="f60c7-120">目前，只有一些 HDInsight 叢集類型/版本支援使用 Data Lake Store 來作為預設儲存體和其他儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="f60c7-120">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="f60c7-121">HDInsight 叢集類型</span><span class="sxs-lookup"><span data-stu-id="f60c7-121">HDInsight cluster type</span></span> | <span data-ttu-id="f60c7-122">Data Lake Store 作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="f60c7-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="f60c7-123">Data Lake Store 作為其他儲存體</span><span class="sxs-lookup"><span data-stu-id="f60c7-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="f60c7-124">注意事項</span><span class="sxs-lookup"><span data-stu-id="f60c7-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="f60c7-125">HDInsight 3.6 版</span><span class="sxs-lookup"><span data-stu-id="f60c7-125">HDInsight version 3.6</span></span> | <span data-ttu-id="f60c7-126">是</span><span class="sxs-lookup"><span data-stu-id="f60c7-126">Yes</span></span> | <span data-ttu-id="f60c7-127">是</span><span class="sxs-lookup"><span data-stu-id="f60c7-127">Yes</span></span> | |
| <span data-ttu-id="f60c7-128">HDInsight 3.5 版</span><span class="sxs-lookup"><span data-stu-id="f60c7-128">HDInsight version 3.5</span></span> | <span data-ttu-id="f60c7-129">是</span><span class="sxs-lookup"><span data-stu-id="f60c7-129">Yes</span></span> | <span data-ttu-id="f60c7-130">是</span><span class="sxs-lookup"><span data-stu-id="f60c7-130">Yes</span></span> | <span data-ttu-id="f60c7-131">HBase 的例外狀況</span><span class="sxs-lookup"><span data-stu-id="f60c7-131">With the exception of HBase</span></span>|
| <span data-ttu-id="f60c7-132">HDInsight 3.4 版</span><span class="sxs-lookup"><span data-stu-id="f60c7-132">HDInsight version 3.4</span></span> | <span data-ttu-id="f60c7-133">否</span><span class="sxs-lookup"><span data-stu-id="f60c7-133">No</span></span> | <span data-ttu-id="f60c7-134">是</span><span class="sxs-lookup"><span data-stu-id="f60c7-134">Yes</span></span> | |
| <span data-ttu-id="f60c7-135">HDInsight 3.3 版</span><span class="sxs-lookup"><span data-stu-id="f60c7-135">HDInsight version 3.3</span></span> | <span data-ttu-id="f60c7-136">否</span><span class="sxs-lookup"><span data-stu-id="f60c7-136">No</span></span> | <span data-ttu-id="f60c7-137">否</span><span class="sxs-lookup"><span data-stu-id="f60c7-137">No</span></span> | |
| <span data-ttu-id="f60c7-138">HDInsight 3.2 版</span><span class="sxs-lookup"><span data-stu-id="f60c7-138">HDInsight version 3.2</span></span> | <span data-ttu-id="f60c7-139">否</span><span class="sxs-lookup"><span data-stu-id="f60c7-139">No</span></span> | <span data-ttu-id="f60c7-140">是</span><span class="sxs-lookup"><span data-stu-id="f60c7-140">Yes</span></span> | |
| <span data-ttu-id="f60c7-141">HDInsight 進階版 (層級)</span><span class="sxs-lookup"><span data-stu-id="f60c7-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="f60c7-142">否</span><span class="sxs-lookup"><span data-stu-id="f60c7-142">No</span></span> | <span data-ttu-id="f60c7-143">否</span><span class="sxs-lookup"><span data-stu-id="f60c7-143">No</span></span> | |
| <span data-ttu-id="f60c7-144">Storm</span><span class="sxs-lookup"><span data-stu-id="f60c7-144">Storm</span></span> | | |<span data-ttu-id="f60c7-145">您可以使用 Data Lake Store 從 Storm 拓撲寫入資料。</span><span class="sxs-lookup"><span data-stu-id="f60c7-145">You can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="f60c7-146">您也可以使用 Data Lake Store 做為參考資料，該資料稍後可以由 Storm 拓撲讀取。</span><span class="sxs-lookup"><span data-stu-id="f60c7-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="f60c7-147">使用 Data Lake Store 作為其他儲存體帳戶，並不會影響效能或從叢集讀取或寫入至 Azure 儲存體的能力。</span><span class="sxs-lookup"><span data-stu-id="f60c7-147">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="f60c7-148">使用 Data Lake Store 作為預設儲存體</span><span class="sxs-lookup"><span data-stu-id="f60c7-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="f60c7-149">使用 Data Lake Store 作為預設儲存體部署 HDInsight 時，儲存在 Data Lake Store 中的叢集相關檔案會位在下列位置︰</span><span class="sxs-lookup"><span data-stu-id="f60c7-149">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="f60c7-150">其中 `<cluster_root_path>` 是您在 Data Lake Store 中建立的資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="f60c7-150">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="f60c7-151">藉由指定每個叢集的根路徑，您可針對多個叢集使用相同的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f60c7-151">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="f60c7-152">因此在您的設定中︰</span><span class="sxs-lookup"><span data-stu-id="f60c7-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="f60c7-153">Cluster1 可以使用路徑 `adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="f60c7-153">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="f60c7-154">Cluster2 可以使用路徑 `adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="f60c7-154">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="f60c7-155">請注意，這兩個叢集都使用相同的 Data Lake Store 帳戶 **mydatalakestore**。</span><span class="sxs-lookup"><span data-stu-id="f60c7-155">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="f60c7-156">每個叢集都會在 Data Lake Store 中存取自己的根檔案系統。</span><span class="sxs-lookup"><span data-stu-id="f60c7-156">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="f60c7-157">特別是 Azure 入口網站的部署經驗會提示您使用像是 **/clusters/\<clustername >** 的資料夾名稱做為根路徑。</span><span class="sxs-lookup"><span data-stu-id="f60c7-157">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

<span data-ttu-id="f60c7-158">若要能夠使用 Data Lake Store 作為預設儲存體，您必須授與服務主體存取下列路徑：</span><span class="sxs-lookup"><span data-stu-id="f60c7-158">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span></span>

- <span data-ttu-id="f60c7-159">Data Lake Store 帳戶根目錄。</span><span class="sxs-lookup"><span data-stu-id="f60c7-159">The Data Lake Store account root.</span></span>  <span data-ttu-id="f60c7-160">例如：adl://mydatalakestore/。</span><span class="sxs-lookup"><span data-stu-id="f60c7-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="f60c7-161">所有叢集資料夾的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f60c7-161">The folder for all cluster folders.</span></span>  <span data-ttu-id="f60c7-162">例如：adl://mydatalakestore/clusters。</span><span class="sxs-lookup"><span data-stu-id="f60c7-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="f60c7-163">叢集的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f60c7-163">The folder for the cluster.</span></span>  <span data-ttu-id="f60c7-164">例如：adl://mydatalakestore/clusters/cluster1storage。</span><span class="sxs-lookup"><span data-stu-id="f60c7-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="f60c7-165">如需建立服務主體和授與存取權的詳細資訊，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="f60c7-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="f60c7-166">使用 Data Lake Store 作為其他儲存體</span><span class="sxs-lookup"><span data-stu-id="f60c7-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="f60c7-167">您也可以使用 Data Lake Store 做為叢集的其他儲存體。</span><span class="sxs-lookup"><span data-stu-id="f60c7-167">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="f60c7-168">在這種情況下，叢集預設儲存體可以是 Azure 儲存體 Blob 或 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f60c7-168">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="f60c7-169">如果您正在作為其他儲存體的 Data Lake Store 上針對其儲存的資料執行 HDInsight 作業，必須使用檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="f60c7-169">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="f60c7-170">例如：</span><span class="sxs-lookup"><span data-stu-id="f60c7-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="f60c7-171">請注意，現在 URL 中沒有任何 **cluster_root_path**。</span><span class="sxs-lookup"><span data-stu-id="f60c7-171">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="f60c7-172">這是因為在此情況下 Data Lake Store 不是預設儲存體，因此您只需要提供檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="f60c7-172">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>

<span data-ttu-id="f60c7-173">若要能夠使用 Data Lake Store 作為其他儲存體，您只需要將您儲存檔案之位置的路徑存取權授與服務主體即可。</span><span class="sxs-lookup"><span data-stu-id="f60c7-173">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span></span>  <span data-ttu-id="f60c7-174">例如：</span><span class="sxs-lookup"><span data-stu-id="f60c7-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="f60c7-175">如需建立服務主體和授與存取權的詳細資訊，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="f60c7-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="f60c7-176">使用多個 Data Lake Store 帳戶</span><span class="sxs-lookup"><span data-stu-id="f60c7-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="f60c7-177">在一個或多個 Data Lake Store 帳戶中提供 HDInsight 叢集的權限，即可完成新增 Data Lake Store 帳戶作為其他帳戶，以及新增一個以上的 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f60c7-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="f60c7-178">請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。</span><span class="sxs-lookup"><span data-stu-id="f60c7-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="f60c7-179">設定 Data Lake Store 存取</span><span class="sxs-lookup"><span data-stu-id="f60c7-179">Configure Data Lake store access</span></span>

<span data-ttu-id="f60c7-180">若要從 HDInsight 叢集設定 Data Lake Store 存取，您必須擁有 Azure Active Directory (Azure AD) 服務主體。</span><span class="sxs-lookup"><span data-stu-id="f60c7-180">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="f60c7-181">只有 Azure AD 系統管理員才可以建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="f60c7-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="f60c7-182">必須使用憑證來建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="f60c7-182">The service principal must be created with a certificate.</span></span> <span data-ttu-id="f60c7-183">如需詳細資訊，請參閱[設定 Data Lake Store 存取](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access)，和[使用自我簽署憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)。</span><span class="sxs-lookup"><span data-stu-id="f60c7-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="f60c7-184">如果您即將使用 Azure Data Lake Store 作為 HDInsight 叢集的額外儲存體，強烈建議您如本文所述建立叢集時執行此作業。</span><span class="sxs-lookup"><span data-stu-id="f60c7-184">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="f60c7-185">將 Azure Data Lake Store 新增為現有 HDInsight 叢集的額外儲存體是很複雜的程序，很容易出錯。</span><span class="sxs-lookup"><span data-stu-id="f60c7-185">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

## <a name="access-files-from-the-cluster"></a><span data-ttu-id="f60c7-186">從叢集存取檔案</span><span class="sxs-lookup"><span data-stu-id="f60c7-186">Access files from the cluster</span></span>

<span data-ttu-id="f60c7-187">有數種方式可讓您從 HDInsight 叢集存取 Data Lake Store 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f60c7-187">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="f60c7-188">**使用完整格式名稱**。</span><span class="sxs-lookup"><span data-stu-id="f60c7-188">**Using the fully qualified name**.</span></span> <span data-ttu-id="f60c7-189">使用這種方法，您可以針對想要存取的檔案提供完整路徑。</span><span class="sxs-lookup"><span data-stu-id="f60c7-189">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="f60c7-190">**使用簡短路徑格式**。</span><span class="sxs-lookup"><span data-stu-id="f60c7-190">**Using the shortened path format**.</span></span> <span data-ttu-id="f60c7-191">使用這種方法，您可以利用 adl:/// 將路徑向上取代至叢集根目錄。</span><span class="sxs-lookup"><span data-stu-id="f60c7-191">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="f60c7-192">因此在上述範例中，您可以將 `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/`取代為 `adl:///`。</span><span class="sxs-lookup"><span data-stu-id="f60c7-192">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="f60c7-193">**使用相對路徑**。</span><span class="sxs-lookup"><span data-stu-id="f60c7-193">**Using the relative path**.</span></span> <span data-ttu-id="f60c7-194">使用這種方法，您可以針對想要存取的檔案，只提供相對路徑。</span><span class="sxs-lookup"><span data-stu-id="f60c7-194">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="f60c7-195">例如，如果檔案的完整路徑如下︰</span><span class="sxs-lookup"><span data-stu-id="f60c7-195">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="f60c7-196">您可以改用此相對路徑來存取相同的 sample.log 檔案。</span><span class="sxs-lookup"><span data-stu-id="f60c7-196">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="f60c7-197">建立可存取 Data Lake Store 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="f60c7-197">Create HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="f60c7-198">如需建立可存取 Data Lake Store 的 HDInsight 叢集詳細指示，請使用下列連結。</span><span class="sxs-lookup"><span data-stu-id="f60c7-198">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="f60c7-199">使用入口網站</span><span class="sxs-lookup"><span data-stu-id="f60c7-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="f60c7-200">使用 PowerShell (搭配 Data Lake Store 做為預設儲存體)</span><span class="sxs-lookup"><span data-stu-id="f60c7-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="f60c7-201">使用 PowerShell (搭配 Data Lake Store 做為其他儲存體)</span><span class="sxs-lookup"><span data-stu-id="f60c7-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="f60c7-202">使用 Azure 範本</span><span class="sxs-lookup"><span data-stu-id="f60c7-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="f60c7-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f60c7-203">Next steps</span></span>
<span data-ttu-id="f60c7-204">在本文中，您已了解如何搭配 HDInsight 使用 HDFS 相容的 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="f60c7-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="f60c7-205">這可讓您建立可調整、長期封存的資料取得解決方案，並利用 HDInsight 來揭開儲存的結構化和非結構化資料內的資訊。</span><span class="sxs-lookup"><span data-stu-id="f60c7-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="f60c7-206">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f60c7-206">For more information, see:</span></span>

* <span data-ttu-id="f60c7-207">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f60c7-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="f60c7-208">開始使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f60c7-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="f60c7-209">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="f60c7-209">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="f60c7-210">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f60c7-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f60c7-211">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f60c7-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f60c7-212">[使用 Azure 儲存體共用存取簽章來限制使用 HDInsight 對資料的存取][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="f60c7-212">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
