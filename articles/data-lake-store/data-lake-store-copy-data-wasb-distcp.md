---
title: "從使用 Distcp 資料湖存放區 WASB aaaCopy 資料 tooand |Microsoft 文件"
description: "從 Azure 儲存體 Blob tooData 湖存放區使用 Distcp 工具 toocopy 資料 tooand"
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
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="3b1c3-103">使用 Azure 儲存體 Blob 與資料湖存放區之間 Distcp toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="3b1c3-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b1c3-104">使用 DistCp</span><span class="sxs-lookup"><span data-stu-id="3b1c3-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="3b1c3-105">使用 AdlCopy</span><span class="sxs-lookup"><span data-stu-id="3b1c3-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="3b1c3-106">一旦您已經建立具有存取 tooa Data Lake Store 帳戶的 HDInsight 叢集，您可以使用 Hadoop 生態系統工具，像是 Distcp toocopy 資料**從 tooand** Data Lake Store 帳戶至 HDInsight 叢集儲存體 (WASB)。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="3b1c3-107">這篇文章提供如何指示 tooachieve 這。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b1c3-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b1c3-108">Prerequisites</span></span>
<span data-ttu-id="3b1c3-109">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="3b1c3-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="3b1c3-110">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-110">**An Azure subscription**.</span></span> <span data-ttu-id="3b1c3-111">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3b1c3-112">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="3b1c3-113">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3b1c3-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="3b1c3-114">**Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="3b1c3-115">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="3b1c3-116">請確定您已啟用遠端桌面 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="3b1c3-117">使用影片快速學習？</span><span class="sxs-lookup"><span data-stu-id="3b1c3-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="3b1c3-118">[觀賞此視訊](https://mix.office.com/watch/1liuojvdx6sie)如何與 Azure 儲存體 Blob 資料湖存放區使用 DistCp toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="3b1c3-119">使用來自 HDInsight Linux 叢集的 Distcp</span><span class="sxs-lookup"><span data-stu-id="3b1c3-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="3b1c3-120">HDInsight 叢集隨附 hello Distcp 公用程式，它可以是使用的 toocopy 到 HDInsight 叢集的不同來源的資料。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="3b1c3-121">如果您已設定 hello HDInsight 叢集 toouse 資料湖存放區做為額外的存放裝置，hello Distcp 公用程式可以使用的方塊外 toocopy 資料 tooand 從 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="3b1c3-122">這一節探討如何 toouse hello Distcp 公用程式。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="3b1c3-123">從您的桌面，使用 SSH tooconnect toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="3b1c3-124">請參閱[連接 tooa 以 Linux 為基礎的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="3b1c3-125">從 hello SSH 提示字元執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="3b1c3-126">確認您的電腦可以存取的 hello Azure 儲存體 Blob (WASB)。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="3b1c3-127">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b1c3-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="3b1c3-128">這樣應該會提供一份在 hello 儲存體 blob 的內容。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="3b1c3-129">同樣地，請確認您是否可以從 hello 叢集存取 hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="3b1c3-130">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b1c3-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="3b1c3-131">這樣應該會提供一份 hello Data Lake Store 帳戶中的檔案/資料夾。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="3b1c3-132">使用 Distcp toocopy WASB tooa Data Lake Store 帳戶資料。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="3b1c3-133">這會將複製的 hello hello 內容**/範例/資料/gutenberg/**資料夾中 WASB 太**/myfolder** hello Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="3b1c3-134">同樣地，使用 Data Lake Store 帳戶 tooWASB Distcp toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="3b1c3-135">這會將複製的 hello 內容**/myfolder**在 hello Data Lake Store 帳戶太**/範例/資料/gutenberg/** WASB 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="3b1c3-136">使用 DistCp 時的效能考量</span><span class="sxs-lookup"><span data-stu-id="3b1c3-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="3b1c3-137">因為 DistCp 的最低資料粒度是單一檔案、 設定 hello 複本數目上限同時是最重要參數 toooptimize hello 針對資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="3b1c3-138">這由設定的對應工具中的 hello 數目 (am') 上 hello 命令列參數。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="3b1c3-139">此參數指定對應工具中將會使用的 toocopy 資料 hello 最大的數目。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="3b1c3-140">預設值為 20。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-140">Default value is 20.</span></span>

<span data-ttu-id="3b1c3-141">**範例**</span><span class="sxs-lookup"><span data-stu-id="3b1c3-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="3b1c3-142">我要如何判斷 hello 自行 toouse 數目？</span><span class="sxs-lookup"><span data-stu-id="3b1c3-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="3b1c3-143">以下是一些您可以使用的指引。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="3b1c3-144">**步驟 1： 決定總 YARN 記憶體**-hello 第一個步驟是 toodetermine hello YARN 記憶體可用 toohello 叢集 hello DistCp 作業執行。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="3b1c3-145">Hello 叢集相關聯的 hello Ambari 入口網站中使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="3b1c3-146">瀏覽 tooYARN，檢視 hello 組態 索引標籤 toosee hello YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="3b1c3-147">tooget hello YARN 記憶體總數，multiply hello YARN 您已在叢集中每個節點的節點數目 hello 與記憶體。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="3b1c3-148">**步驟 2： 計算的對應工具中的 hello 數目**-hello 值**m**是相等的 toohello 商數除以 hello YARN 容器大小的 YARN 記憶體總計。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="3b1c3-149">hello Ambari 入口網站也提供 hello YARN 容器大小的資訊。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="3b1c3-150">瀏覽 tooYARN，並檢視 hello 組態 索引標籤 hello YARN 容器大小會顯示在此視窗。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="3b1c3-151">hello 在對應工具中的 hello 數目的方程式 tooarrive (**m**) 是</span><span class="sxs-lookup"><span data-stu-id="3b1c3-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="3b1c3-152">**範例**</span><span class="sxs-lookup"><span data-stu-id="3b1c3-152">**Example**</span></span>

<span data-ttu-id="3b1c3-153">假設您有 4 個 D14v2s 節點 hello 叢集中，而且您嘗試 tootransfer 10 TB 的資料，從 10 個不同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="3b1c3-154">Hello 資料夾的每個包含不同的資料量和每個資料夾中的 hello 檔案大小不同。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="3b1c3-155">YARN 記憶體總計-從 hello 判斷該 hello YARN 記憶體 Ambari 入口網站是 96GB D14 節點。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="3b1c3-156">因此，4 節點叢集的 YARN 記憶體總計為︰</span><span class="sxs-lookup"><span data-stu-id="3b1c3-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="3b1c3-157">對應程式-從 hello Ambari 入口網站，您可以判斷該 hello YARN 容器大小會 3072 D14 叢集節點的數目。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="3b1c3-158">因此，對應程式數目為︰</span><span class="sxs-lookup"><span data-stu-id="3b1c3-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="3b1c3-159">如果其他應用程式使用的記憶體，然後您可以選擇 tooonly 使用叢集的 YARN 記憶體一部分的 DistCp。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="3b1c3-160">複製大型資料集</span><span class="sxs-lookup"><span data-stu-id="3b1c3-160">Copying large datasets</span></span>

<span data-ttu-id="3b1c3-161">當移動 hello 資料集 toobe hello 大小是非常大 (例如 > 1 TB) 或是如果您有許多不同的資料夾，您應該考慮使用多個 DistCp 工作。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="3b1c3-162">可能是沒有效能增益，但它會使該特定工作，而不是 hello 整項作業的任何工作失敗時，如果您只需要 toorestart 散播出 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="3b1c3-163">限制</span><span class="sxs-lookup"><span data-stu-id="3b1c3-163">Limitations</span></span>

* <span data-ttu-id="3b1c3-164">DistCp 會嘗試在大小 toooptimize 效能類似的 toocreate 自行。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="3b1c3-165">增加的對應工具中的 hello 數目可能不會永遠提高效能。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="3b1c3-166">DistCp 是有限的 tooonly 一個對應，每個檔案。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="3b1c3-167">因此，對應程式數目不應該超過您擁有的檔案數目。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="3b1c3-168">因為 DistCp 只能指定一個對應工具 tooa 檔案，這會限制 hello 量可以是使用的 toocopy 大型檔案的並行存取。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="3b1c3-169">如果您有少數的大型檔案，則您應該將它們分割為 256 MB 的檔案區塊 toogive 您多個可能的並行存取。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="3b1c3-170">如果您要從 Azure Blob 儲存體帳戶複製，複製作業可能會進行節流處理，一邊 hello blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="3b1c3-171">這會降低 hello 的複製作業的效能。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="3b1c3-172">toolearn 進一步了解 hello 限制的 Azure Blob 儲存體，請參閱 < 在 Azure 儲存體限制[Azure 訂用帳戶和服務限制](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="3b1c3-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3b1c3-173">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3b1c3-173">See also</span></span>
* [<span data-ttu-id="3b1c3-174">從 Azure 儲存體 Blob tooData 湖存放區複製資料</span><span class="sxs-lookup"><span data-stu-id="3b1c3-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="3b1c3-175">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="3b1c3-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="3b1c3-176">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3b1c3-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="3b1c3-177">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3b1c3-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
