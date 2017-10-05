---
title: "適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項 - Azure | Microsoft Docs"
description: "了解 HDInsight 上 R 伺服器之使用者可用的不同儲存體選項"
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="e9ab7-103">適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="e9ab7-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="e9ab7-104">HDInsight 上的 Microsoft R 伺服器有數種儲存體選項可用來保存資料、程式碼或包含分析結果的物件。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="e9ab7-105">這些包括下列選項：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-105">These include the following options:</span></span>

- [<span data-ttu-id="e9ab7-106">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e9ab7-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="e9ab7-107">Azure Data Lake 儲存體</span><span class="sxs-lookup"><span data-stu-id="e9ab7-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="e9ab7-108">Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e9ab7-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="e9ab7-109">您可以使用 HDI 叢集存取多個 Azure 儲存體帳戶或容器。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="e9ab7-110">「Azure 檔案」儲存體是一個可在邊緣節點上使用的方便資料儲存體選項，可讓您掛接「Azure 儲存體」檔案共用 (例如掛接到 Linux 檔案系統)。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="e9ab7-111">但是，只要是擁有受支援作業系統 (例如 Windows 或 Linux) 的系統，就可以掛接和使用「Azure 檔案」共用。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="e9ab7-112">當您在 HDInsight 中建立 Hadoop 叢集時，可以指定 **Azure 儲存體**帳戶或 **Data Lake Store**。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="e9ab7-113">來自該帳戶的特定儲存體容器，會保留您所建立叢集的檔案系統 (例如，Hadoop 分散式檔案系統)。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="e9ab7-114">如需詳細資訊與指導方針，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="e9ab7-115">搭配 HDInsight 使用 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="e9ab7-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="e9ab7-116">[搭配 Azure HDInsight 叢集使用 Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="e9ab7-117">如需有關 Azure 儲存體解決方案的詳細資訊，請參閱 [Microsoft Azure 儲存體簡介](../storage/common/storage-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="e9ab7-118">如需有關如何針對您的情節選取最適儲存體選項的指導方針，請參閱[決定何時使用 Azure Blob、Azure 檔案或 Azure 資料磁碟](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="e9ab7-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="e9ab7-119">搭配 R 伺服器使用 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e9ab7-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="e9ab7-120">如有需要，您可以使用 HDI 叢集存取多個 Azure 儲存體帳戶或容器。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="e9ab7-121">若要這樣做，您必須在建立叢集時於 UI 中指定其他儲存體帳戶，然後遵循下列步驟，以便搭配 R 伺服器使用它們。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="e9ab7-122">基於效能目的，系統會在與您指定的主要儲存體帳戶相同資料中心內建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="e9ab7-123">不支援在與 HDInsight 叢集不同的位置中使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="e9ab7-124">使用儲存體帳戶名稱 **storage1** 和預設容器 **container1** 建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="e9ab7-125">指定其他儲存體帳戶 **storage2**。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="e9ab7-126">將 mycsv.csv 檔案複製到 /share 目錄，並對該檔案執行分析。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="e9ab7-127">在 R 程式碼中，將名稱節點設定為 **default** ，並設定要處理的目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="e9ab7-128">所有目錄和檔案的參考會指向儲存體帳戶 wasb://container1@storage1.blob.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="e9ab7-129">這是與 HDInsight 叢集關聯的「預設儲存體帳戶」。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="e9ab7-130">現在，假設您想要處理名稱為 mySpecial.csv 的檔案，其所在位置為 **storage2** 中 **container2** 的 /private 目錄。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="e9ab7-131">在 R 程式碼中，將名稱節點參考指向 **storage2** 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="e9ab7-132">現在，所有目錄和檔案的參考會指向儲存體帳戶 wasb://container2@storage2.blob.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="e9ab7-133">這是您已指定的「名稱節點」。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="e9ab7-134">您必須在 **storage2** 上設定 /user/RevoShare/<SSH username> 目錄，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="e9ab7-135">搭配 R 伺服器使用 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e9ab7-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="e9ab7-136">若要搭配 HDInsight 帳戶使用 Data Lake 存放區，您必須對叢集提供您想要使用之每個 Azure Data Lake 存放區的存取權。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="e9ab7-137">如需有關如何使用 Azure 入口網站並使用 Azure Data Lake Store 帳戶作為預設儲存體或作為其他存放區來建立 HDInsight 叢集的指示，請參閱 [使用 Azure 入口網站搭配 Data Lake Store 建立 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="e9ab7-138">接著，您會以和使用次要 Azure 儲存體帳戶的方式 (如先前程序所述) 很像的方式，在 R 指令碼中使用存放區。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="e9ab7-139">為叢集新增 Azure Data Lake Store 的存取權</span><span class="sxs-lookup"><span data-stu-id="e9ab7-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="e9ab7-140">您可以使用與 HDInsight 叢集相關聯的 Azure Active Directory (Azure AD) 服務主體來存取 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="e9ab7-141">新增 Azure AD 服務主體：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="e9ab7-142">在建立 HDInsight 叢集時，從 [資料來源] 索引標籤中選取 [叢集 AAD 身分識別]。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="e9ab7-143">在 [叢集 AAD 身分識別] 對話方塊的 [選取 AD 服務主體] 底下，選取 [新建]。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="e9ab7-144">在為服務主體命名並建立密碼後，請按一下 [管理 ADLS 存取]，以將該服務主體與您的 Data Lake Store 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="e9ab7-145">建立叢集之後，您也可以新增叢集存取權到一或多個 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="e9ab7-146">為 Data Lake Store 開啟 Azure 入口網站入口，並移至 [資料總管] > [存取] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="e9ab7-147">如何從 R 伺服器存取 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e9ab7-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="e9ab7-148">一旦您獲得 Data Lake 存放區的存取權，就可以在 HDInsight 上的 R 伺服器中使用該存放區，其方式就和使用次要 Azure 儲存體帳戶一樣。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="e9ab7-149">唯一的差別在於前置詞 **wasb://** 會變更為 **adl://**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="e9ab7-150">下列命令是用來搭配 RevoShare 目錄設定 Data Lake 儲存體帳戶，並新增來自先前範例的範例 .csv 檔案：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="e9ab7-151">搭配 R 伺服器使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e9ab7-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="e9ab7-152">另外還有可在邊緣節點上使用的便利資料儲存體選項，我們稱之為 [Azure 檔案]((https://azure.microsoft.com/services/storage/files/)。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="e9ab7-153">它可以讓您將 Azure 儲存體的檔案共用掛接至 Linux 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="e9ab7-154">此選項對於儲存資料檔案、R 指令碼與結果物件相當便利，該結果物件在稍後可以於邊緣節點 (而不是 HDFS) 上使用原生檔案系統時需要。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="e9ab7-155">Azure 檔案的主要優點是，只要是擁有受支援作業系統 (例如 Windows 或 Linux) 的系統，就可以掛接和使用檔案共用。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="e9ab7-156">例如，您本人或您的小組成員所擁有的另一個 HDInsight 叢集，或是 Azure VM 甚或內部部署系統均可使用 Azure 檔案。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="e9ab7-157">如需詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e9ab7-157">For more information, see:</span></span>

- [<span data-ttu-id="e9ab7-158">如何搭配 Linux 使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e9ab7-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="e9ab7-159">如何在 Windows 上使用 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="e9ab7-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="e9ab7-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9ab7-160">Next steps</span></span>

<span data-ttu-id="e9ab7-161">既然已經了解 Azure 儲存體選項，就可以使用下列連結來探索使用 HDInsight 上之 R 伺服器完成資料科學工作的方式。</span><span class="sxs-lookup"><span data-stu-id="e9ab7-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="e9ab7-162">HDInsight 上的 R 伺服器概觀</span><span class="sxs-lookup"><span data-stu-id="e9ab7-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="e9ab7-163">開始使用 Hadoop 上的 R 伺服器</span><span class="sxs-lookup"><span data-stu-id="e9ab7-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="e9ab7-164">將 RStudio Server 新增至 HDInsight (若未在建立叢集期間新增)</span><span class="sxs-lookup"><span data-stu-id="e9ab7-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="e9ab7-165">適用於 HDInsight 上 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="e9ab7-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

