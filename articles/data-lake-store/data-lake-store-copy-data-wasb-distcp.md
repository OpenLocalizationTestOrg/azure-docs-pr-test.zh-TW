---
title: "使用 Distcp 將送至/來自 WASB 的資料複製到 Data Lake Store | Microsoft Docs"
description: "使用 Distcp 工具將送至/來自 Azure 儲存體 Blob 的資料複製到 Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="cdea6-103">使用 Distcp 在 Azure 儲存體 Blob 與 Data Lake Store 之間複製資料</span><span class="sxs-lookup"><span data-stu-id="cdea6-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cdea6-104">使用 DistCp</span><span class="sxs-lookup"><span data-stu-id="cdea6-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="cdea6-105">使用 AdlCopy</span><span class="sxs-lookup"><span data-stu-id="cdea6-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="cdea6-106">在您建立可存取 Data Lake Store 帳戶的 HDInsight 叢集後，您可以使用 Distcp 之類的 Hadoop 生態系統工具，將 **送至/來自** HDInsight 叢集儲存體 (WASB) 的資料複製到 Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="cdea6-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="cdea6-107">本文提供執行此作業的相關指示。</span><span class="sxs-lookup"><span data-stu-id="cdea6-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdea6-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="cdea6-108">Prerequisites</span></span>
<span data-ttu-id="cdea6-109">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="cdea6-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="cdea6-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cdea6-110">**An Azure subscription**.</span></span> <span data-ttu-id="cdea6-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cdea6-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cdea6-112">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cdea6-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="cdea6-113">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cdea6-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="cdea6-114">**Azure HDInsight 叢集** 。</span><span class="sxs-lookup"><span data-stu-id="cdea6-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="cdea6-115">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="cdea6-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="cdea6-116">請確實為叢集啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="cdea6-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="cdea6-117">使用影片快速學習？</span><span class="sxs-lookup"><span data-stu-id="cdea6-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="cdea6-118">[觀看這部影片](https://mix.office.com/watch/1liuojvdx6sie) ，主題是關於如何使用 DistCp 在 Azure 儲存體 Blob 與 Data Lake Store 之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="cdea6-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="cdea6-119">使用來自 HDInsight Linux 叢集的 Distcp</span><span class="sxs-lookup"><span data-stu-id="cdea6-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="cdea6-120">HDInsight 叢集隨附 Distcp 公用程式，可用來將不同來源的資料複製到 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cdea6-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="cdea6-121">如果您已將 HDInsight 叢集設定為使用 Data Lake Store 做為額外的儲存體，則您也可以使用現成可用的 Distcp 公用程式將資料複製到 Data Lake Store 帳戶，或從中複製資料。</span><span class="sxs-lookup"><span data-stu-id="cdea6-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="cdea6-122">在本節中，我們將討論如何使用 Distcp 公用程式。</span><span class="sxs-lookup"><span data-stu-id="cdea6-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="cdea6-123">從您的桌上型電腦，使用 SSH 連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="cdea6-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="cdea6-124">請參閱 [連線至以 Linux 為基礎的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="cdea6-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="cdea6-125">從 SSH 提示字元執行命令。</span><span class="sxs-lookup"><span data-stu-id="cdea6-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="cdea6-126">確認您是否可存取 Azure 儲存體 Blob (WASB)。</span><span class="sxs-lookup"><span data-stu-id="cdea6-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="cdea6-127">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="cdea6-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="cdea6-128">這應會提供儲存體 blob 中的內容清單。</span><span class="sxs-lookup"><span data-stu-id="cdea6-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="cdea6-129">同樣地，請確認您是否可從叢集存取 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdea6-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="cdea6-130">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="cdea6-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="cdea6-131">這應會提供 Data Lake Store 帳戶中的檔案/資料夾清單。</span><span class="sxs-lookup"><span data-stu-id="cdea6-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="cdea6-132">使用 Distcp 將資料從 WASB 複製到 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdea6-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="cdea6-133">這會將 WASB 中的 **/example/data/gutenberg/** 資料夾的內容複製到 Data Lake Store 帳戶中的 **/myfolder**。</span><span class="sxs-lookup"><span data-stu-id="cdea6-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="cdea6-134">同樣地，請使用 Distcp 將資料從 Data Lake Store 帳戶複製到 WASB。</span><span class="sxs-lookup"><span data-stu-id="cdea6-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="cdea6-135">這會將 Data Lake Store 帳戶中的 **/myfolder** 的內容複製到 WASB 中的 **/example/data/gutenberg/** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="cdea6-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="cdea6-136">使用 DistCp 時的效能考量</span><span class="sxs-lookup"><span data-stu-id="cdea6-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="cdea6-137">因為 DistCp 以單一檔案為最低細微程度，若要針對 Data Lake Store 而達到最佳化，設定同步複本數目上限是最重要的參數。</span><span class="sxs-lookup"><span data-stu-id="cdea6-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="cdea6-138">這是在命令列設定對應程式數目 (‘m’) 參數來控制。</span><span class="sxs-lookup"><span data-stu-id="cdea6-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="cdea6-139">這個參數指定用來複製資料的對應程式數目上限。</span><span class="sxs-lookup"><span data-stu-id="cdea6-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="cdea6-140">預設值為 20。</span><span class="sxs-lookup"><span data-stu-id="cdea6-140">Default value is 20.</span></span>

<span data-ttu-id="cdea6-141">**範例**</span><span class="sxs-lookup"><span data-stu-id="cdea6-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="cdea6-142">如何決定要使用的對應程式數目？</span><span class="sxs-lookup"><span data-stu-id="cdea6-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="cdea6-143">以下是一些您可以使用的指引。</span><span class="sxs-lookup"><span data-stu-id="cdea6-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="cdea6-144">**步驟 1︰判斷 YARN 記憶體總計** - 第一個步驟是判斷您執行 DistCp 作業的叢集可用的 YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="cdea6-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="cdea6-145">您可以在與叢集相關聯的 Ambari 入口網站中取得這項資訊。</span><span class="sxs-lookup"><span data-stu-id="cdea6-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="cdea6-146">瀏覽至 YARN，檢視 [設定] 索引標籤以查看 YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="cdea6-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="cdea6-147">若要計算 YARN 記憶體總計，請將每個節點的 YARN 記憶體乘以您在叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="cdea6-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="cdea6-148">**步驟 2︰計算對應程式數目** - **m** 的值等於 YARN 記憶體總計除以 YARN 容器大小的商數。</span><span class="sxs-lookup"><span data-stu-id="cdea6-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="cdea6-149">Ambari 入口網站中也提供 YARN 容器大小的資訊。</span><span class="sxs-lookup"><span data-stu-id="cdea6-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="cdea6-150">瀏覽至 YARN，檢視 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cdea6-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="cdea6-151">YARN 容器大小會顯示在此視窗中。</span><span class="sxs-lookup"><span data-stu-id="cdea6-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="cdea6-152">計算對應程式數目 (**m**) 的方程式是</span><span class="sxs-lookup"><span data-stu-id="cdea6-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="cdea6-153">**範例**</span><span class="sxs-lookup"><span data-stu-id="cdea6-153">**Example**</span></span>

<span data-ttu-id="cdea6-154">假設您在叢集中有 4 個 D14v2s 節點，且嘗試從 10 個不同的資料夾傳輸 10TB 的資料。</span><span class="sxs-lookup"><span data-stu-id="cdea6-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="cdea6-155">每個資料夾包含不同的資料量，且每個資料夾內的檔案大小都不同。</span><span class="sxs-lookup"><span data-stu-id="cdea6-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="cdea6-156">YARN 記憶體總計 - 從 Ambari 入口網站，您可以判斷 D14 節點的 YARN 記憶體是 96GB。</span><span class="sxs-lookup"><span data-stu-id="cdea6-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="cdea6-157">因此，4 節點叢集的 YARN 記憶體總計為︰</span><span class="sxs-lookup"><span data-stu-id="cdea6-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="cdea6-158">對應程式數目 - 從 Ambari 入口網站，您可以判斷 D14 叢集節點的 YARN 容器大小是 3072。</span><span class="sxs-lookup"><span data-stu-id="cdea6-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="cdea6-159">因此，對應程式數目為︰</span><span class="sxs-lookup"><span data-stu-id="cdea6-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="cdea6-160">如果有其他應用程式在使用記憶體，您可以選擇讓 DistCp 只使用叢集的一部分 YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="cdea6-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="cdea6-161">複製大型資料集</span><span class="sxs-lookup"><span data-stu-id="cdea6-161">Copying large datasets</span></span>

<span data-ttu-id="cdea6-162">如果要移動的資料集很大 (例如 > 1TB) 或您有許多不同的資料夾，請考慮使用多個 DistCp 作業。</span><span class="sxs-lookup"><span data-stu-id="cdea6-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="cdea6-163">雖然可能不會提高效能，但可分散作業，如果有任何作業失敗，您只需要重新啟動該特定的作業，而不是整個作業。</span><span class="sxs-lookup"><span data-stu-id="cdea6-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="cdea6-164">限制</span><span class="sxs-lookup"><span data-stu-id="cdea6-164">Limitations</span></span>

* <span data-ttu-id="cdea6-165">DistCp 會嘗試建立較小的對應程式，以最佳化效能。</span><span class="sxs-lookup"><span data-stu-id="cdea6-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="cdea6-166">增加對應程式數目不見得會提高效能。</span><span class="sxs-lookup"><span data-stu-id="cdea6-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="cdea6-167">DistCp 受限於每個檔案只有一個對應程式。</span><span class="sxs-lookup"><span data-stu-id="cdea6-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="cdea6-168">因此，對應程式數目不應該超過您擁有的檔案數目。</span><span class="sxs-lookup"><span data-stu-id="cdea6-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="cdea6-169">因為 DistCp 只能將一個對應程式指派給一個檔案，這會限制可用於複製大量檔案的並行程度。</span><span class="sxs-lookup"><span data-stu-id="cdea6-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="cdea6-170">如果您的大型檔案很少，則應該將它們分割成 256MB 的檔案區塊，以提高並行潛力。</span><span class="sxs-lookup"><span data-stu-id="cdea6-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="cdea6-171">如果您從 Azure Blob 儲存體帳戶複製，Blob 儲存體端可能會節流複製作業。</span><span class="sxs-lookup"><span data-stu-id="cdea6-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="cdea6-172">這會降低複製作業的效能。</span><span class="sxs-lookup"><span data-stu-id="cdea6-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="cdea6-173">若要深入了解 Azure Blob 儲存體的限制，請參閱 [Azure 訂用帳戶和服務限制](../azure-subscription-service-limits.md)中的 Azure 儲存體限制。</span><span class="sxs-lookup"><span data-stu-id="cdea6-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cdea6-174">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cdea6-174">See also</span></span>
* [<span data-ttu-id="cdea6-175">將資料從 Azure 儲存體 Blob 複製到 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cdea6-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="cdea6-176">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="cdea6-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="cdea6-177">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cdea6-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="cdea6-178">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cdea6-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
