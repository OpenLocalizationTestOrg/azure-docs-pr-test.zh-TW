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
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>使用 Data Lake Store 搭配 Azure HDInsight 叢集

tooanalyze HDInsight 叢集中的資料，您可以儲存 hello 資料可以是在[Azure 儲存體](../storage/common/storage-introduction.md)， [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)，或兩者。 這兩個儲存體選項可讓您 toosafely 刪除 HDInsight 叢集所使用的計算，而不會遺失使用者資料。

在本文中，您將了解 Data Lake Store 與 HDInsight 叢集搭配運作的方式。 toolearn Azure 儲存體如何使用 HDInsight 叢集，請參閱[使用 Azure 儲存體與 Azure HDInsight 叢集](hdinsight-hadoop-use-blob-storage.md)。 如需建立 HDInsight 叢集的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

> [!NOTE]
> Data Lake Store 一律透過安全通道存取，因此不會有 `adls` 檔案系統配置名稱。 您會一律使用 `adl`。
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>HDInsight 叢集的可用性

Hadoop 支援 hello 預設檔案系統的概念。 hello 預設的檔案系統表示預設配置和授權單位。 它也可以使用的 tooresolve 相對路徑。 在 hello HDInsight 叢集建立程序，您可以指定 blob 容器 hello 預設檔案系統中，為 Azure 儲存體中或使用 HDInsight 3.5 及較新版本，您可以選取 Azure 儲存體或 Azure Data Lake Store hello 預設檔案系統少數的例外狀況。 

HDInsight 叢集可透過兩種方式來使用 Data Lake Store︰

* 為 hello 預設儲存體
* 作為其他儲存體，搭配 Azure 儲存體 Blob 作為預設儲存體。

目前，只有部分 hello HDInsight 叢集做為預設儲存體和其他儲存體帳戶中使用 Data Lake Store 的類型/版本支援：

| HDInsight 叢集類型 | Data Lake Store 作為預設儲存體 | Data Lake Store 作為其他儲存體| 注意事項 |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight 3.6 版 | 是 | 是 | |
| HDInsight 3.5 版 | 是 | 是 | 發生的 HBase hello 例外狀況|
| HDInsight 3.4 版 | 否 | 是 | |
| HDInsight 3.3 版 | 否 | 否 | |
| HDInsight 3.2 版 | 否 | 是 | |
| HDInsight 進階版 (層級)| 否 | 否 | |
| Storm | | |您可以使用 Data Lake Store toowrite 資料從 Storm 拓撲。 您也可以使用 Data Lake Store 做為參考資料，該資料稍後可以由 Storm 拓撲讀取。|

做為額外的儲存體帳戶中使用資料湖存放區不會影響效能或 hello 能力 tooread 或從 hello 叢集寫入 tooAzure 儲存體。


## <a name="use-data-lake-store-as-default-storage"></a>使用 Data Lake Store 作為預設儲存體

HDInsight 當做預設儲存體的資料湖存放區與部署時，hello 叢集相關的檔案儲存在資料湖存放區在下列位置的 hello:

    adl://mydatalakestore/<cluster_root_path>/

其中`<cluster_root_path>`hello 資料湖存放區中建立的資料夾名稱。 藉由指定 根的路徑為每個叢集，您可以使用 hello 多個叢集相同的 Data Lake Store 帳戶。 因此在您的設定中︰

* Cluster1 可以使用 hello 路徑`adl://mydatalakestore/cluster1storage`
* Cluster2 可以使用 hello 路徑`adl://mydatalakestore/cluster2storage`

請注意同時 hello 叢集使用 hello 相同 Data Lake Store 帳戶**mydatalakestore**。 每個群集都有存取 tooits 擁有資料湖存放區中的根檔案系統。 hello Azure 入口網站的部署經驗尤其會提示您 toouse 資料夾名稱例如**/clusters/\<clustername >** hello 根路徑。

toobe 無法 toouse 當做預設儲存體的資料湖存放區，您必須授與 hello 服務主體存取 toohello 下列路徑：

- hello Data Lake Store 帳戶的根。  例如：adl://mydatalakestore/。
- 叢集的所有資料夾的 hello 資料夾。  例如：adl://mydatalakestore/clusters。
- hello 叢集 hello 資料夾。  例如：adl://mydatalakestore/clusters/cluster1storage。

如需建立服務主體和授與存取權的詳細資訊，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。


## <a name="use-data-lake-store-as-additional-storage"></a>使用 Data Lake Store 作為其他儲存體

您可以使用做為額外的存放裝置的 Data Lake Store 的 hello 叢集中。 在這種情況下，hello 叢集預設儲存體可以是 Azure 儲存體 Blob 或 Data Lake Store 帳戶。 如果您針對儲存在資料湖存放區做為額外的存放裝置中的 hello 資料執行 HDInsight 工作，您必須使用 hello 的完整路徑 toohello 檔案。 例如：

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

請注意，沒有任何**cluster_root_path**現在 hello URL 中。 這是因為資料湖存放區不是預設儲存體在此情況下，您只需要 toodo 是提供 hello 路徑 toohello 檔案。

toobe 無法 toouse 資料湖存放區做為額外的存放裝置，您只需要 toogrant hello 服務主體存取 toohello 路徑儲存您的檔案。  例如：

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

如需建立服務主體和授與存取權的詳細資訊，請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。


## <a name="use-more-than-one-data-lake-store-accounts"></a>使用多個 Data Lake Store 帳戶

將 Data Lake Store 帳戶新增為其他並加入一個以上的 Data Lake Store 帳戶被透過一或多個 Data Lake Store 帳戶中的資料賦予 hello HDInsight 叢集的權限。 請參閱[設定 Data Lake Store 存取](#configure-data-lake-store-access)。

## <a name="configure-data-lake-store-access"></a>設定 Data Lake Store 存取

tooconfigure 資料湖存放區存取，從您的 HDInsight 叢集，您必須擁有 Azure Active directory (Azure AD) 服務主體。 只有 Azure AD 系統管理員才可以建立服務主體。 必須使用憑證建立 hello 服務主體。 如需詳細資訊，請參閱[設定 Data Lake Store 存取](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access)，和[使用自我簽署憑證來建立服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)。

> [!NOTE]
> 如果您正在 toouse Azure Data Lake Store 為 HDInsight 叢集的其他存放裝置中，我們強烈建議您採用這種這篇文章中所述，建立 hello 叢集時。 將 Azure Data Lake Store 新增額外的儲存體 tooan 為現有 HDInsight 叢集是複雜的程序和 tooerrors 容易出錯。
>

## <a name="access-files-from-hello-cluster"></a>Hello 叢集存取檔案

有數種方式，您可以存取資料湖存放區中的 hello 檔案從 HDInsight 叢集。

* **使用完整限定的名稱的 hello**。 使用此方法時，您會提供 hello 完整路徑 toohello 檔想 tooaccess。

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **使用 hello 縮短的路徑格式**。 使用此方法時，您 hello 路徑取代向上 toohello 叢集根目錄 adl: / /。 因此，在 hello 上述範例中，您可以取代`adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/`與`adl:///`。

        adl:///<file path>

* **使用相對路徑的 hello**。 使用此方法時，您只提供 hello 相對路徑 toohello 檔案要 tooaccess。 例如，如果 hello 完整路徑 toohello 檔案：

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    您可以存取相同 sample.log 檔案 hello 改為使用這個相對路徑。

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>建立 HDInsight 叢集使用存取 tooData 湖存放區

使用 hello 遵循上 toocreate HDInsight 叢集，以存取 tooData 湖存放區的方式的詳細指示的連結。

* [使用入口網站](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [使用 PowerShell (搭配 Data Lake Store 做為預設儲存體)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [使用 PowerShell (搭配 Data Lake Store 做為其他儲存體)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [使用 Azure 範本](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>後續步驟
在本文中，您學到如何 toouse HDFS 相容 Azure Data Lake Store 的 HDInsight。 這可讓您 toobuild 可擴充、 長期來看，保存資料擷取方案和使用 HDInsight toounlock hello 內部資訊 hello 儲存結構化和非結構化的資料。

如需詳細資訊，請參閱：

* [開始使用 Azure HDInsight][hdinsight-get-started]
* [開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [使用 Azure 儲存體共用存取簽章 toorestrict 存取 toodata 與 HDInsight][hdinsight-use-sas]

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
