---
title: "從 Azure 資料湖存放區的儲存體 Blob aaaCopy 資料 |Microsoft 文件"
description: "使用 AdlCopy 工具 toocopy 資料從 Azure 儲存體 Blob tooData 湖存放區"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a>從 Azure 儲存體 Blob tooData 湖存放區複製資料
> [!div class="op_single_selector"]
> * [使用 DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [使用 AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
>
>

Azure Data Lake Store 提供的命令列工具， [AdlCopy](http://aka.ms/downloadadlcopy)，從下列來源的 hello toocopy 資料：

* 從 Azure 儲存體 Blob 複製到 Data Lake Store 中。 您無法使用 AdlCopy toocopy Data Lake Store tooAzure 儲存體 blob 資料。
* 兩個 Azure Data Lake Store 帳戶之間。

此外，您可以使用 hello AdlCopy 工具在兩個不同的模式：

* **獨立**，其中 hello 工具會使用 Data Lake Store 資源 tooperform hello 工作。
* **使用 Data Lake Analytics 帳戶**，其中 hello 單位 tooyour Data Lake Analytics 帳戶指派給使用的 tooperform hello 複製作業。 當您以預期的方式搜尋 tooperform hello 複製工作時您可能想指定 toouse 此選項。

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure 儲存體 Blob** 容器 (其中含有一些資料)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)
* **Azure Data Lake Analytics 帳戶 （選擇性）** -請參閱[開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)指示如何 toocreate 資料湖存放區的帳戶。
* **AdlCopy 工具**。 安裝從 hello AdlCopy 工具[http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy)。

## <a name="syntax-of-hello-adlcopy-tool"></a>Hello AdlCopy 工具語法
使用下列語法 toowork hello AdlCopy 工具與 hello

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

hello 語法中的 hello 參數，如下所示：

| 選項 | 說明 |
| --- | --- |
| 來源 |指定 hello Azure 儲存體 blob 中的 hello hello 來源資料的位置。 hello 來源可以是 blob 容器、 blob 或另一個 Data Lake Store 帳戶。 |
| Dest |指定要 hello Data Lake Store 目的地 toocopy。 |
| SourceKey |指定 hello hello Azure 儲存體 blob 來源的儲存體存取金鑰。 這是必要的只有 hello 來源 blob 容器或 blob。 |
| 帳戶 |**選用**。 如果您想 toouse Azure Data Lake Analytics 帳戶 toorun hello 複製作業，請使用此選項。 如果您在 hello 語法中使用 hello /Account 選項但未指定 Data Lake Analytics 帳戶，AdlCopy 會使用預設帳戶 toorun hello 工作。 此外，如果您使用此選項時，您必須加入 hello 來源 (Azure 儲存體 Blob) 和目的地 （Azure 資料湖存放區） 做為資料來源資料湖分析帳戶。 |
| Units |指定將用於 hello 複製作業的 Data Lake Analytics 單位的 hello 數目。 這個選項會強制，如果您使用 hello **/帳戶**選項 toospecify hello Data Lake Analytics 帳戶。 |
| 模式 |指定指出哪些 blob 或檔案 toocopy regex 模式。 AdlCopy 使用區分大小寫的比對。 所有項目 toocopy 不指定任何模式時，使用 hello 預設模式。 不支援指定多個檔案模式。 |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a>使用 （做為獨立） AdlCopy toocopy 資料從 Azure 儲存體 blob
1. 開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。
2. 從 hello 來源容器 tooa 資料湖存放區執行下列命令 toocopy hello 特定的 blob:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    例如：

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] hello 上述語法指定 hello 檔案 toobe 複製的 tooa 資料夾 hello Data Lake Store 帳戶中。 如果 hello 指定的資料夾名稱不存在，AdlCopy 工具會建立一個資料夾。

    您將會提示的 tooenter hello 認證 hello 您擁有的 Data Lake Store 帳戶所在的 Azure 訂用帳戶。 您會看到類似 toohello 下列輸出：

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. 您也可以複製所有 hello blob 從某個容器 toohello Data Lake Store 帳戶使用 hello 下列命令：

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    例如：

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a>效能考量

如果您要從 Azure Blob 儲存體帳戶複製，您可能會節流處理 hello blob 儲存體端複製期間。 這會降低 hello 的複製作業的效能。 toolearn 進一步了解 hello 限制的 Azure Blob 儲存體，請參閱 < 在 Azure 儲存體限制[Azure 訂用帳戶和服務限制](../azure-subscription-service-limits.md)。

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a>使用從另一個 Data Lake Store 帳戶 （做為獨立） AdlCopy toocopy 資料
您也可以使用兩個 Data Lake Store 帳戶之間 AdlCopy toocopy 資料。

1. 開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。
2. 從一個 Data Lake Store 帳戶 tooanother 執行下列命令 toocopy hello 特定檔案。

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    例如：

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > hello 上述語法指定 hello 檔案 toobe 複製的 tooa 資料夾 hello 目的地 Data Lake Store 帳戶中。 如果 hello 指定的資料夾名稱不存在，AdlCopy 工具會建立一個資料夾。
   >
   >

    您將會提示的 tooenter hello 認證 hello 您擁有的 Data Lake Store 帳戶所在的 Azure 訂用帳戶。 您會看到類似 toohello 下列輸出：

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. hello 下列命令會將所有檔案從特定資料夾中的資料夾 hello 來源 Data Lake Store 帳戶 tooa hello 目的地 Data Lake Store 帳戶中。

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a>效能考量

當使用 AdlCopy 做為獨立的工具，hello 複本上執行共用，Azure 受管理資源。 在此環境中，您可能會收到 hello 效能取決於系統負載，以及可用資源。 這個模式最適合臨時的少量傳輸。 沒有參數需要 toobe 微調時使用 AdlCopy 當作獨立的工具。

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a>使用 （與資料湖分析帳戶） AdlCopy toocopy 資料
您也可以使用您的資料湖分析帳戶 toorun hello AdlCopy 作業 toocopy 資料從 Azure 儲存體 blob tooData 湖存放區。 移動 hello 資料 toobe 位於 hello 範圍 gb 和 tb，而且您想更佳且可預測的效能輸送量時，通常會使用此選項。

toouse 您 AdlCopy toocopy 從 Azure 儲存體 Blob hello 來源 (Azure 儲存體 Blob) 的資料湖分析帳戶必須新增為您的 Data Lake Analytics 帳戶的資料來源。 如需加入額外的資料來源 tooyour Data Lake Analytics 帳戶的指示，請參閱[管理 Data Lake Analytics 帳戶的資料來源](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources)。

> [!NOTE]
> 如果您要從 Azure Data Lake Store 帳戶複製為 hello 來源使用 Data Lake Analytics 帳戶，您不需要以 hello Data Lake Analytics 帳戶 tooassociate hello Data Lake Store 帳戶。 hello 需求 tooassociate hello 來源存放區以 hello Data Lake Analytics 帳戶是只當 hello 來源是 Azure 儲存體帳戶。
>
>

執行使用 Data Lake Analytics 帳戶的 Azure 儲存體 blob tooa Data Lake Store 帳戶中的下列命令 toocopy hello:

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

例如：

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

同樣地，執行使用 Data Lake Analytics 帳戶的 Azure 儲存體 blob tooa Data Lake Store 帳戶中的下列命令 toocopy hello:

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a>效能考量

複製資料時的 tb hello 範圍中，使用您自己的 Azure Data Lake Analytics 帳戶中使用 AdlCopy 提供更好且更可預測的效能。 hello Azure 資料湖分析單位 toouse hello 複製作業的數目應微調的 hello 參數。 增加 hello 單元數目會增加 hello 的複製作業的效能。 複製每個檔案 toobe 可以使用最大的一個單位。 指定多個單位 hello 複製的檔案數目，將不會增加效能。

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a>使用 AdlCopy toocopy 資料使用模式比對
在本節中，您學會如何 toouse AdlCopy toocopy 資料來源 （在下列範例中我們使用 Azure 儲存體 Blob） 使用模式比對 tooa 目的地 Data Lake Store 帳戶。 比方說，您可以使用下列 toocopy hello 步驟是所有檔案從 hello 來源 blob toohello 目的地.csv 副檔名。

1. 開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。
2. 執行下列命令 toocopy hello 所有檔案 *.csv 副檔名 hello 來源容器 tooa 資料湖存放區中的特定 blob:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    例如：

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a>計費
* 如果輸出成本來移動使用 hello AdlCopy 工具以在將予計費的獨立伺服器資料，如果 hello 來源 Azure 儲存體帳戶不在 hello 相同的區域，因為 hello 資料湖存放區。
* 如果您使用 hello AdlCopy 工具與您的 Data Lake Analytics 帳戶，標準[Data Lake Analytics 計費費率](https://azure.microsoft.com/pricing/details/data-lake-analytics/)會套用。

## <a name="considerations-for-using-adlcopy"></a>使用 AdlCopy 的考量
* AdlCopy (適用於 1.0.5 版) 支援從共同擁有超過數千個檔案和資料夾的來源複製資料。 不過，如果您遇到複製大型資料集的問題，您可以在於 hello 檔案/資料夾分散到不同的子資料夾，並為 hello 來源改用 hello 路徑 toothose 子資料夾。

## <a name="performance-considerations-for-using-adlcopy"></a>使用 AdlCopy 時的效能考量

AdlCopy 支援複製包含數千個檔案和資料夾的資料。 不過，如果您遇到複製大型資料集的問題，您可以將 hello 檔案/資料夾發佈成較小的子資料夾。 AdlCopy 適用於臨時複製。 如果您嘗試以週期性 toocopy 資料，您應該考慮使用[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)提供周圍 hello 複製作業的完整管理。

## <a name="release-notes"></a>版本資訊
* 1.0.13-如果您要複製資料 toohello 相同的 Azure Data Lake Store 帳戶跨多個 adlcopy 命令，您不需要再執行您的認證，針對每個 tooreenter。 Adlcopy 現在會在多次執行之間快取該資訊。

## <a name="next-steps"></a>後續步驟
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配 Data Lake Store 使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
