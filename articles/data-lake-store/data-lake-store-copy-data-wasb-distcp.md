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
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>使用 Azure 儲存體 Blob 與資料湖存放區之間 Distcp toocopy 資料
> [!div class="op_single_selector"]
> * [使用 DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [使用 AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

一旦您已經建立具有存取 tooa Data Lake Store 帳戶的 HDInsight 叢集，您可以使用 Hadoop 生態系統工具，像是 Distcp toocopy 資料**從 tooand** Data Lake Store 帳戶至 HDInsight 叢集儲存體 (WASB)。 這篇文章提供如何指示 tooachieve 這。

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)
* **Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。 請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。 請確定您已啟用遠端桌面 hello 叢集。

## <a name="do-you-learn-fast-with-videos"></a>使用影片快速學習？
[觀賞此視訊](https://mix.office.com/watch/1liuojvdx6sie)如何與 Azure 儲存體 Blob 資料湖存放區使用 DistCp toocopy 資料。

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>使用來自 HDInsight Linux 叢集的 Distcp

HDInsight 叢集隨附 hello Distcp 公用程式，它可以是使用的 toocopy 到 HDInsight 叢集的不同來源的資料。 如果您已設定 hello HDInsight 叢集 toouse 資料湖存放區做為額外的存放裝置，hello Distcp 公用程式可以使用的方塊外 toocopy 資料 tooand 從 Data Lake Store 帳戶。 這一節探討如何 toouse hello Distcp 公用程式。

1. 從您的桌面，使用 SSH tooconnect toohello 叢集。 請參閱[連接 tooa 以 Linux 為基礎的 HDInsight 叢集](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)。 從 hello SSH 提示字元執行 hello 命令。

2. 確認您的電腦可以存取的 hello Azure 儲存體 Blob (WASB)。 執行下列命令的 hello:

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    這樣應該會提供一份在 hello 儲存體 blob 的內容。
3. 同樣地，請確認您是否可以從 hello 叢集存取 hello Data Lake Store 帳戶。 執行下列命令的 hello:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    這樣應該會提供一份 hello Data Lake Store 帳戶中的檔案/資料夾。
4. 使用 Distcp toocopy WASB tooa Data Lake Store 帳戶資料。

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    這會將複製的 hello hello 內容**/範例/資料/gutenberg/**資料夾中 WASB 太**/myfolder** hello Data Lake Store 帳戶中。
5. 同樣地，使用 Data Lake Store 帳戶 tooWASB Distcp toocopy 資料。

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    這會將複製的 hello 內容**/myfolder**在 hello Data Lake Store 帳戶太**/範例/資料/gutenberg/** WASB 中的資料夾。

## <a name="performance-considerations-while-using-distcp"></a>使用 DistCp 時的效能考量

因為 DistCp 的最低資料粒度是單一檔案、 設定 hello 複本數目上限同時是最重要參數 toooptimize hello 針對資料湖存放區。 這由設定的對應工具中的 hello 數目 (am') 上 hello 命令列參數。 此參數指定對應工具中將會使用的 toocopy 資料 hello 最大的數目。 預設值為 20。

**範例**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>我要如何判斷 hello 自行 toouse 數目？

以下是一些您可以使用的指引。

* **步驟 1： 決定總 YARN 記憶體**-hello 第一個步驟是 toodetermine hello YARN 記憶體可用 toohello 叢集 hello DistCp 作業執行。 Hello 叢集相關聯的 hello Ambari 入口網站中使用這項資訊。 瀏覽 tooYARN，檢視 hello 組態 索引標籤 toosee hello YARN 記憶體。 tooget hello YARN 記憶體總數，multiply hello YARN 您已在叢集中每個節點的節點數目 hello 與記憶體。

* **步驟 2： 計算的對應工具中的 hello 數目**-hello 值**m**是相等的 toohello 商數除以 hello YARN 容器大小的 YARN 記憶體總計。 hello Ambari 入口網站也提供 hello YARN 容器大小的資訊。 瀏覽 tooYARN，並檢視 hello 組態 索引標籤 hello YARN 容器大小會顯示在此視窗。 hello 在對應工具中的 hello 數目的方程式 tooarrive (**m**) 是

        m = (number of nodes * YARN memory for each node) / YARN container size

**範例**

假設您有 4 個 D14v2s 節點 hello 叢集中，而且您嘗試 tootransfer 10 TB 的資料，從 10 個不同的資料夾。 Hello 資料夾的每個包含不同的資料量和每個資料夾中的 hello 檔案大小不同。

* YARN 記憶體總計-從 hello 判斷該 hello YARN 記憶體 Ambari 入口網站是 96GB D14 節點。 因此，4 節點叢集的 YARN 記憶體總計為︰ 

        YARN memory = 4 * 96GB = 384GB

* 對應程式-從 hello Ambari 入口網站，您可以判斷該 hello YARN 容器大小會 3072 D14 叢集節點的數目。 因此，對應程式數目為︰

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

如果其他應用程式使用的記憶體，然後您可以選擇 tooonly 使用叢集的 YARN 記憶體一部分的 DistCp。

### <a name="copying-large-datasets"></a>複製大型資料集

當移動 hello 資料集 toobe hello 大小是非常大 (例如 > 1 TB) 或是如果您有許多不同的資料夾，您應該考慮使用多個 DistCp 工作。 可能是沒有效能增益，但它會使該特定工作，而不是 hello 整項作業的任何工作失敗時，如果您只需要 toorestart 散播出 hello 作業。

### <a name="limitations"></a>限制

* DistCp 會嘗試在大小 toooptimize 效能類似的 toocreate 自行。 增加的對應工具中的 hello 數目可能不會永遠提高效能。

* DistCp 是有限的 tooonly 一個對應，每個檔案。 因此，對應程式數目不應該超過您擁有的檔案數目。 因為 DistCp 只能指定一個對應工具 tooa 檔案，這會限制 hello 量可以是使用的 toocopy 大型檔案的並行存取。

* 如果您有少數的大型檔案，則您應該將它們分割為 256 MB 的檔案區塊 toogive 您多個可能的並行存取。 
 
* 如果您要從 Azure Blob 儲存體帳戶複製，複製作業可能會進行節流處理，一邊 hello blob 儲存體。 這會降低 hello 的複製作業的效能。 toolearn 進一步了解 hello 限制的 Azure Blob 儲存體，請參閱 < 在 Azure 儲存體限制[Azure 訂用帳戶和服務限制](../azure-subscription-service-limits.md)。

## <a name="see-also"></a>另請參閱
* [從 Azure 儲存體 Blob tooData 湖存放區複製資料](data-lake-store-copy-data-azure-storage-blob.md)
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
