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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項

Microsoft R Server HDInsight 上有很多的儲存體解決方案 toopersist 資料、 程式碼或包含分析結果的物件。 這些需求包括下列選項的 hello:

- [Azure Blob](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake 儲存體](https://azure.microsoft.com/services/data-lake-store/)
- [Azure 檔案儲存體](https://azure.microsoft.com/services/storage/files/)

您也可以存取多個 Azure 儲存體帳戶或具有 HDI 叢集容器的 hello 選項。 Azure 檔案儲存體是 hello 邊緣節點可讓您 toomount Azure 儲存體檔案共用，例如 hello Linux 檔案系統上使用方便的資料儲存選項。 但是，只要是擁有受支援作業系統 (例如 Windows 或 Linux) 的系統，就可以掛接和使用「Azure 檔案」共用。 

當您在 HDInsight 中建立 Hadoop 叢集時，可以指定 **Azure 儲存體**帳戶或 **Data Lake Store**。 從該帳戶的特定儲存體容器保存 hello hello 您建立叢集，（例如 hello Hadoop 分散式檔案系統） 的檔案系統。 如需詳細資訊與指導方針，請參閱：

- [搭配 HDInsight 使用 Azure 儲存體](hdinsight-hadoop-use-blob-storage.md)
- [搭配 Azure HDInsight 叢集使用 Data Lake Store](hdinsight-hadoop-use-data-lake-store.md)。 

如需有關 hello Azure 儲存體解決方案的詳細資訊，請參閱[簡介 tooMicrosoft Azure 儲存體](../storage/common/storage-introduction.md)。 

如需選取 hello 最適當儲存體選項 toouse 用於您案例的指引，請參閱[制定時 toouse Azure Blob、 Azure 或 Azure 資料磁碟](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>搭配 R 伺服器使用 Azure Blob 儲存體帳戶

如有需要，您可以使用 HDI 叢集存取多個 Azure 儲存體帳戶或容器。 toodo 因此，您需要 toospecify hello 其他儲存體帳戶中 hello UI 當您建立 hello 叢集，然後依照這些步驟 toouse 它們使用 R Server。

> [!WARNING]
> 基於效能考量，hello HDInsight 叢集建立在 hello 相同資料中心做為您指定的 hello 主要儲存體帳戶。 不支援在 hello HDInsight 叢集以外的不同位置中使用的儲存體帳戶。

1. 使用儲存體帳戶名稱 **storage1** 和預設容器 **container1** 建立 HDInsight 叢集。
2. 指定其他儲存體帳戶 **storage2**。  
3. 複製 hello mycsv.csv 檔案 toohello /share 目錄，並在該檔案上執行分析。  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. 在 R 程式碼中，設定 hello 名稱節點太**預設**並設定您的目錄和檔案 tooprocess。  

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

所有 hello 目錄和檔案的參考點 toohello 儲存體帳戶wasb://container1@storage1.blob.core.windows.net。 這是 hello**預設儲存體帳戶**與 hello HDInsight 叢集關聯。

現在，假設您想要 tooprocess 檔案稱為 mySpecial.csv 位於 hello /private 目錄**container2**中**storage2**。

在您的 R 程式碼，指向 hello 名稱節點參考 toohello **storage2**儲存體帳戶。


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

Hello 目錄和檔案參考現在點 toohello 儲存體帳戶的所有wasb://container2@storage2.blob.core.windows.net。 這是 hello**名稱節點**您指定的。

您有 tooconfigure hello /user/RevoShare/<SSH username>目錄**storage2** ，如下所示：


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>搭配 R 伺服器使用 Azure Data Lake Store

toouse 資料湖存放區與您的 HDInsight 帳戶、 您叢集存取 tooeach Azure 資料湖存放區，您想 toouse 需要 toogive。 指示如何 toouse hello Azure 入口網站 toocreate HDInsight 叢集的 Azure Data Lake Store 帳戶為 hello 預設儲存體，或做為額外的存放區，請參閱[建立與使用 Azure 入口網站DataLakeStore的HDInsight叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

您接著 hello 存放區中使用 R 指令碼更像次要 Azure 儲存體帳戶 hello 上一個程序中所述。

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>新增叢集存取 tooyour Azure 資料湖存放
您可以使用與 HDInsight 叢集相關聯的 Azure Active Directory (Azure AD) 服務主體來存取 Data Lake Store。

tooadd Azure AD 服務主體：

1. 當您建立您的 HDInsight 叢集時，請選取**叢集 AAD 身分識別**從 hello**資料來源** 索引標籤。

2. 在 hello**叢集 AAD 身分識別**對話方塊的 **選取 AD 服務主體**，選取**建立新**。

您提供 hello 服務主體名稱，然後建立的密碼之後，請按一下**管理 ADLS 存取**tooassociate hello 服務主體名稱的資料湖存放。

它也是可能 tooadd 叢集存取 tooone 或更多的資料湖存放下列叢集建立。 開啟 hello Azure 入口網站的資料湖存放區項目，並移過**資料總管 > 存取 > 新增**。 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>如何 tooaccess hello 從 R 伺服器的資料湖存放區

一旦您已獲得存取 tooa 資料湖存放區，您可以使用 R 伺服器中的 hello 存放區上 HDInsight hello 方式與次要 Azure 儲存體帳戶。 hello hello 前置詞的差別僅**wasb: / /**變更太**adl: / /** ，如下所示：


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


hello 下列命令會使用的 tooconfigure hello 與 hello RevoShare 目錄的資料湖儲存體帳戶並新增 hello 範例.csv 檔案 hello 上一個範例：


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>搭配 R 伺服器使用 Azure 檔案儲存體

也是很方便的資料儲存選項使用 hello 邊緣節點稱為 [Azure 檔案] ((https://azure.microsoft.com/services/storage/files/)。 它可讓您 toomount Azure 儲存體檔案共用 toohello Linux 檔案系統。 這個選項可能很方便的儲存資料檔案、 R 指令碼，以及可能會需要更新版本中，尤其是當它使意義 toouse hello hello 邊緣節點，而不是 HDFS 上的原生檔案系統的結果物件。 

Azure 檔案的主要優點是可以掛接並使用已受支援的作業系統，例如 Windows 或 Linux 任何系統共用該 hello 檔案。 例如，您本人或您的小組成員所擁有的另一個 HDInsight 叢集，或是 Azure VM 甚或內部部署系統均可使用 Azure 檔案。 如需詳細資訊，請參閱：

- [如何 toouse Linux 的 Azure 檔案儲存體](../storage/files/storage-how-to-use-files-linux.md)
- [如何 toouse Windows 上的 Azure 檔案儲存體](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>後續步驟

既然您了解 hello Azure 儲存體選項，使用 hello 下列連結 toodiscover 種取得資料科學工作已完成 HDInsight 上的 R 伺服器。

* [HDInsight 上的 R 伺服器概觀](hdinsight-hadoop-r-server-overview.md)
* [開始使用 Hadoop 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)
* [新增 RStudio 伺服器 tooHDInsight （如果不在叢集建立期間新增）](hdinsight-hadoop-r-server-install-r-studio.md)
* [適用於 HDInsight 中 R 伺服器的計算內容選項](hdinsight-hadoop-r-server-compute-contexts.md)

