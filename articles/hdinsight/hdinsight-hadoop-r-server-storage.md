---
title: "HDInsight 的 Azure 上的 R 伺服器 aaaAzure 儲存解決方案 |Microsoft 文件"
description: "深入了解使用 R Server HDInsight 上的 hello 不同的儲存體選項可用 toousers"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="85cec-103">適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="85cec-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="85cec-104">Microsoft R Server HDInsight 上有很多的儲存體解決方案 toopersist 資料、 程式碼或包含分析結果的物件。</span><span class="sxs-lookup"><span data-stu-id="85cec-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="85cec-105">這些需求包括下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="85cec-105">These include hello following options:</span></span>

- [<span data-ttu-id="85cec-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="85cec-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="85cec-107">Azure Data Lake 儲存體</span><span class="sxs-lookup"><span data-stu-id="85cec-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="85cec-108">Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="85cec-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="85cec-109">您也可以存取多個 Azure 儲存體帳戶或具有 HDI 叢集容器的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="85cec-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="85cec-110">Azure 檔案儲存體是 hello 邊緣節點可讓您 toomount Azure 儲存體檔案共用，例如 hello Linux 檔案系統上使用方便的資料儲存選項。</span><span class="sxs-lookup"><span data-stu-id="85cec-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="85cec-111">但是，只要是擁有受支援作業系統 (例如 Windows 或 Linux) 的系統，就可以掛接和使用「Azure 檔案」共用。</span><span class="sxs-lookup"><span data-stu-id="85cec-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="85cec-112">當您在 HDInsight 中建立 Hadoop 叢集時，可以指定 **Azure 儲存體**帳戶或 **Data Lake Store**。</span><span class="sxs-lookup"><span data-stu-id="85cec-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="85cec-113">從該帳戶的特定儲存體容器保存 hello hello 您建立叢集，（例如 hello Hadoop 分散式檔案系統） 的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="85cec-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="85cec-114">如需詳細資訊與指導方針，請參閱：</span><span class="sxs-lookup"><span data-stu-id="85cec-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="85cec-115">搭配 HDInsight 使用 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="85cec-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="85cec-116">[搭配 Azure HDInsight 叢集使用 Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="85cec-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="85cec-117">如需有關 hello Azure 儲存體解決方案的詳細資訊，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="85cec-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="85cec-118">如需選取 hello 最適當儲存體選項 toouse 用於您案例的指引，請參閱[制定時 toouse Azure Blob、 Azure 或 Azure 資料磁碟](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="85cec-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="85cec-119">搭配 R 伺服器使用 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="85cec-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="85cec-120">如有需要，您可以使用 HDI 叢集存取多個 Azure 儲存體帳戶或容器。</span><span class="sxs-lookup"><span data-stu-id="85cec-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="85cec-121">toodo 因此，您需要 toospecify hello 其他儲存體帳戶中 hello UI 當您建立 hello 叢集，然後依照這些步驟 toouse 它們使用 R Server。</span><span class="sxs-lookup"><span data-stu-id="85cec-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="85cec-122">基於效能考量，hello HDInsight 叢集建立在 hello 相同資料中心做為您指定的 hello 主要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="85cec-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="85cec-123">不支援在 hello HDInsight 叢集以外的不同位置中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="85cec-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="85cec-124">使用儲存體帳戶名稱 **storage1** 和預設容器 **container1** 建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="85cec-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="85cec-125">指定其他儲存體帳戶 **storage2**。</span><span class="sxs-lookup"><span data-stu-id="85cec-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="85cec-126">複製 hello mycsv.csv 檔案 toohello /share 目錄，並在該檔案上執行分析。</span><span class="sxs-lookup"><span data-stu-id="85cec-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="85cec-127">在 R 程式碼中，設定 hello 名稱節點太**預設**並設定您的目錄和檔案 tooprocess。</span><span class="sxs-lookup"><span data-stu-id="85cec-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="85cec-128">所有 hello 目錄和檔案的參考點 toohello 儲存體帳戶wasb://container1@storage1.blob.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="85cec-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="85cec-129">這是 hello**預設儲存體帳戶**與 hello HDInsight 叢集關聯。</span><span class="sxs-lookup"><span data-stu-id="85cec-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="85cec-130">現在，假設您想要 tooprocess 檔案稱為 mySpecial.csv 位於 hello /private 目錄**container2**中**storage2**。</span><span class="sxs-lookup"><span data-stu-id="85cec-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="85cec-131">在您的 R 程式碼，指向 hello 名稱節點參考 toohello **storage2**儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="85cec-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="85cec-132">Hello 目錄和檔案參考現在點 toohello 儲存體帳戶的所有wasb://container2@storage2.blob.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="85cec-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="85cec-133">這是 hello**名稱節點**您指定的。</span><span class="sxs-lookup"><span data-stu-id="85cec-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="85cec-134">您有 tooconfigure hello /user/RevoShare/<SSH username>目錄**storage2** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85cec-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="85cec-135">搭配 R 伺服器使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="85cec-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="85cec-136">toouse 資料湖存放區與您的 HDInsight 帳戶、 您叢集存取 tooeach Azure 資料湖存放區，您想 toouse 需要 toogive。</span><span class="sxs-lookup"><span data-stu-id="85cec-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="85cec-137">指示如何 toouse hello Azure 入口網站 toocreate HDInsight 叢集的 Azure Data Lake Store 帳戶為 hello 預設儲存體，或做為額外的存放區，請參閱[建立與使用 Azure 入口網站DataLakeStore的HDInsight叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="85cec-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="85cec-138">您接著 hello 存放區中使用 R 指令碼更像次要 Azure 儲存體帳戶 hello 上一個程序中所述。</span><span class="sxs-lookup"><span data-stu-id="85cec-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="85cec-139">新增叢集存取 tooyour Azure 資料湖存放</span><span class="sxs-lookup"><span data-stu-id="85cec-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="85cec-140">您可以使用與 HDInsight 叢集相關聯的 Azure Active Directory (Azure AD) 服務主體來存取 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="85cec-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="85cec-141">tooadd Azure AD 服務主體：</span><span class="sxs-lookup"><span data-stu-id="85cec-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="85cec-142">當您建立您的 HDInsight 叢集時，請選取**叢集 AAD 身分識別**從 hello**資料來源** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="85cec-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="85cec-143">在 hello**叢集 AAD 身分識別**對話方塊的 **選取 AD 服務主體**，選取**建立新**。</span><span class="sxs-lookup"><span data-stu-id="85cec-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="85cec-144">您提供 hello 服務主體名稱，然後建立的密碼之後，請按一下**管理 ADLS 存取**tooassociate hello 服務主體名稱的資料湖存放。</span><span class="sxs-lookup"><span data-stu-id="85cec-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="85cec-145">它也是可能 tooadd 叢集存取 tooone 或更多的資料湖存放下列叢集建立。</span><span class="sxs-lookup"><span data-stu-id="85cec-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="85cec-146">開啟 hello Azure 入口網站的資料湖存放區項目，並移過**資料總管 > 存取 > 新增**。</span><span class="sxs-lookup"><span data-stu-id="85cec-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="85cec-147">如何 tooaccess hello 從 R 伺服器的資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="85cec-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="85cec-148">一旦您已獲得存取 tooa 資料湖存放區，您可以使用 R 伺服器中的 hello 存放區上 HDInsight hello 方式與次要 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="85cec-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="85cec-149">hello hello 前置詞的差別僅**wasb: / /**變更太**adl: / /** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="85cec-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="85cec-150">hello 下列命令會使用的 tooconfigure hello 與 hello RevoShare 目錄的資料湖儲存體帳戶並新增 hello 範例.csv 檔案 hello 上一個範例：</span><span class="sxs-lookup"><span data-stu-id="85cec-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="85cec-151">搭配 R 伺服器使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="85cec-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="85cec-152">也是很方便的資料儲存選項使用 hello 邊緣節點稱為 [Azure 檔案] ((https://azure.microsoft.com/services/storage/files/)。</span><span class="sxs-lookup"><span data-stu-id="85cec-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="85cec-153">它可讓您 toomount Azure 儲存體檔案共用 toohello Linux 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="85cec-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="85cec-154">這個選項可能很方便的儲存資料檔案、 R 指令碼，以及可能會需要更新版本中，尤其是當它使意義 toouse hello hello 邊緣節點，而不是 HDFS 上的原生檔案系統的結果物件。</span><span class="sxs-lookup"><span data-stu-id="85cec-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="85cec-155">Azure 檔案的主要優點是可以掛接並使用已受支援的作業系統，例如 Windows 或 Linux 任何系統共用該 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="85cec-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="85cec-156">例如，您本人或您的小組成員所擁有的另一個 HDInsight 叢集，或是 Azure VM 甚或內部部署系統均可使用 Azure 檔案。</span><span class="sxs-lookup"><span data-stu-id="85cec-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="85cec-157">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="85cec-157">For more information, see:</span></span>

- [<span data-ttu-id="85cec-158">如何 toouse Linux 的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="85cec-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="85cec-159">如何 toouse Windows 上的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="85cec-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="85cec-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85cec-160">Next steps</span></span>

<span data-ttu-id="85cec-161">既然您了解 hello Azure 儲存體選項，使用 hello 下列連結 toodiscover 種取得資料科學工作已完成 HDInsight 上的 R 伺服器。</span><span class="sxs-lookup"><span data-stu-id="85cec-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="85cec-162">HDInsight 上的 R 伺服器概觀</span><span class="sxs-lookup"><span data-stu-id="85cec-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="85cec-163">開始使用 Hadoop 上的 R 伺服器</span><span class="sxs-lookup"><span data-stu-id="85cec-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="85cec-164">新增 RStudio 伺服器 tooHDInsight （如果不在叢集建立期間新增）</span><span class="sxs-lookup"><span data-stu-id="85cec-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="85cec-165">適用於 HDInsight 中 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="85cec-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

