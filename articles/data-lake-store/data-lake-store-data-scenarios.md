---
title: "Data Lake Store aaaData 案例 |Microsoft 文件"
description: "了解 hello 不同的案例，以及使用哪些資料的工具可以內嵌、 處理、 下載，以及以視覺化方式檢視資料湖存放區中"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>使用 Azure Data Lake Store 處理巨量資料需求
巨量資料處理有四個主要階段︰

* 即時或以批次形式將大量資料內嵌到存放區
* 處理 hello 資料
* 下載 hello 資料
* 視覺化 hello 資料

在本文中，我們查看這些階段與尊重 tooAzure Data Lake Store toounderstand hello 選項與工具可用 toomeet 巨量資料需求。

## <a name="ingest-data-into-data-lake-store"></a>將資料內嵌到 Data Lake 存放區
本章節強調 hello 不同來源中的該資料可以 ingested 到 Data Lake Store 帳戶的資料和 hello 不同的方法。

![將資料內嵌到 Data Lake Store](./media/data-lake-store-data-scenarios/ingest-data.png "將資料內嵌到 Data Lake Store")

### <a name="ad-hoc-data"></a>臨機操作資料
代表用來建立巨量資料應用程式原型的較小型資料集。 有不同的方式根據 hello hello 資料來源擷取的臨機操作資料。

| 資料來源 | 內嵌方式 |
| --- | --- |
| 本機電腦 |<ul> <li>[Azure 入口網站](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Azure 跨平台 CLI 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[使用適用於 Visual Studio 的 Data Lake Tools](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Azure 儲存體 Blob |<ul> <li>[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[AdlCopy 工具](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[HDInsight 叢集上執行的 DistCp](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>串流資料
代表可能由應用程式、裝置、感應器等各種來源產生的資料。這些資料可透過多種工具內嵌到 Data Lake 存放區。 這些工具通常會擷取和處理事件的事件基礎中的 hello 資料即時然後 hello 事件以寫入批次至資料湖存放區，以便它們可以進一步處理。

以下是您可以使用的工具︰

* [Azure Stream Analytics](../stream-analytics/stream-analytics-data-lake-output.md) -內嵌到事件中心可以將事件寫入 tooAzure Data Lake 使用 Azure Data Lake Store 輸出。
* [Azure HDInsight Storm](../hdinsight/hdinsight-storm-write-data-lake-store.md) -您可以將資料寫入直接從 tooData Lake Store hello Storm 叢集。
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) – 您可以從事件中心接收事件，並接著加以寫 tooData 湖存放區使用 hello[資料湖存放區.NET SDK](data-lake-store-get-started-net-sdk.md)。

### <a name="relational-data"></a>關聯式資料
您也可以從關聯式資料庫取得資料。 每經過一段時間，關聯式資料庫就會收集大量資料，在經過巨量資料管線處理後，這些資料將可提供重要情資。 您可以使用下列工具 toomove hello 這類資料，將資料湖存放區。

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>Web 伺服器記錄資料 (使用自訂應用程式上傳)
這種類型的資料集之所以特別是因為 web 伺服器記錄檔資料的分析會用於巨量資料的應用程式的常見使用案例，需要大量的記錄檔 toobe 上傳 toohello 資料湖存放區。 您可以使用任何下列工具 toowrite hello 您自己的指令碼或應用程式 tooupload 這類資料。

* [Azure 跨平台 CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake 存放區 .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)

上傳 web 伺服器記錄資料，同時也會用於上傳其他種類的資料 （例如社交 sentiments 資料），它是一個良好方式 toowrite 您自己自訂的指令碼/應用程式，因為它提供 hello 彈性 tooinclude 資料上傳做為一部分的元件應用程式的較大巨量資料。 在某些情況下這段程式碼可能需要簡單的命令列公用程式或指令碼的 hello 表單。 在其他情況下，hello 程式碼可能使用的 toointegrate 巨量資料處理成商務應用程式或解決方案。

### <a name="data-associated-with-azure-hdinsight-clusters"></a>與 Azure HDInsight 叢集相關聯的資料
大部分的 HDInsight 叢集類型 (Hadoop、HBase、Storm) 能以資料儲存存放機制的形式支援 Data Lake 存放區。 HDInsight 叢集能從 Azure 儲存體 Blob (WASB) 存取資料。 為提升效能，您可以從 WASB 複製 hello 資料到 hello 叢集相關聯的 Data Lake Store 帳戶。 您可以使用下列工具 toocopy hello 資料 hello。

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [AdlCopy 服務](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>儲存於內部部署環境或 IaaS Hadoop 叢集中的資料
您可能會使用 HDFS，在本機電腦上將大量資料儲存於現有的 Hadoop 叢集中。 hello Hadoop 叢集可能會在內部部署部署中，或可能在 Azure IaaS 叢集中。 可能有需求 toocopy 這類資料 tooAzure Data Lake Store 的一次性方法或以週期性方式。 有各種選項，您可以使用 tooachieve 這個。 以下是替代項目清單與 hello 取捨。

| 方法 | 詳細資料 | 優點 | 考量 |
| --- | --- | --- | --- |
| 使用 Azure 資料處理站 (ADF) toocopy 資料直接從 Hadoop 叢集 tooAzure 資料湖存放區 |[ADF 支援 HDFS 做為資料來源](../data-factory/data-factory-hdfs-connector.md) |ADF 針對 HDFS 提供全新支援，以及一流的端對端管理與監視 |需要資料管理閘道器 toobe 部署在內部部署或 hello IaaS 叢集中 |
| 從 Hadoop 將資料匯出為檔案。 然後將複製 hello 檔案 tooAzure 資料湖存放區使用適當的機制。 |您可以複製檔案 tooAzure 資料湖存放區使用： <ul><li>[適用於 Windows OS 的 Azure PowerShell](data-lake-store-get-started-powershell.md)</li><li>[適用於非 Windows OS 的 Azure 跨平台 CLI 2.0](data-lake-store-get-started-cli-2.0.md)</li><li>使用任何 Data Lake Store SDK 的自訂應用程式</li></ul> |快速 tooget 啟動。 可以執行自訂的上傳 |牽涉到多種技術的多步驟程序。 管理和監視會在指定的時間 hello 自訂性質 hello 工具不斷成長 toobe 一項挑戰 |
| 使用 Distcp toocopy 資料從 Hadoop tooAzure 儲存體。 從 Azure 儲存體 tooData 湖存放區使用適當的機制，然後複製資料。 |您可以從 Azure 儲存體 tooData 湖存放區使用複製資料： <ul><li>[Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)</li><li>[AdlCopy 工具](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[HDInsight 叢集上執行的 Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |您可以使用開放原始碼工具。 |牽涉到多種技術的多步驟程序 |

### <a name="really-large-datasets"></a>大型資料集
上傳的數個 tb 的資料集，使用上述的 hello 方法有時可能慢速和高成本。 在這種情況下，您可以使用下列的 hello 選項。

* **使用 Azure ExpressRoute**。 Azure ExpressRoute 可讓您在 Azure 資料中心與內部部署的基礎結構之間建立私人連線。 這是傳輸大量資料的可靠選項。 如需詳細資訊，請參閱 [Azure ExpressRoute 文件](../expressroute/expressroute-introduction.md)。
* **「離線」上傳資料**。 如果使用 Azure ExpressRoute 不可行因任何原因，您可以使用[Azure 匯入/匯出服務](../storage/common/storage-import-export-service.md)tooship 硬碟機與您的資料 tooan Azure 資料中心。 您的資料是第一次上傳的 tooAzure 儲存體 Blob。 然後您可以使用[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)或[AdlCopy 工具](data-lake-store-copy-data-azure-storage-blob.md)toocopy 資料從 Azure 儲存體 Blob tooData 湖存放區。

  > [!NOTE]
  > 雖然使用 hello 匯入/匯出服務，不應該大於 195 GB hello hello 磁碟您在出貨 tooAzure 資料中心上的檔案大小。
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>處理儲存在 Data Lake 存放區中的資料
一旦 hello 資料可以使用 Data Lake Store 中您可以分析上執行使用 hello 資料支援巨量資料的應用程式。 目前，您可以使用 Azure HDInsight 與 Azure Data Lake Analytics toorun 資料分析工作儲存於資料湖存放區中的 hello 資料。

![分析 Data Lake Store 中的資料](./media/data-lake-store-data-scenarios/analyze-data.png "分析 Data Lake Store 中的資料")

您可以查看 hello 遵循範例。

* [建立以 Data Lake 存放區當做儲存體的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)
* [搭配 Data Lake 存放區使用 Azure Data Lake 分析](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>從 Data Lake 存放區下載資料
您也可能會想 toodownload 或是將資料從 Azure Data Lake Store 移案例，例如：

* 移動資料 tooother 儲存機制 toointerface 搭配現有的資料處理管線。 例如，您可能想要從 Data Lake Store tooAzure SQL Database 的 toomove 資料或在內部部署 SQL Server。
* 下載資料 tooyour 本機電腦中的 IDE 環境中建置應用程式原型時的處理。

![從 Data Lake Store 輸出資料](./media/data-lake-store-data-scenarios/egress-data.png "從 Data Lake Store 輸出資料")

在這種情況下，您可以使用任何 hello 下列選項：

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

您也可以使用下列方法 toowrite hello 您自己的指令碼/應用程式 toodownload 資料從資料湖存放區。

* [Azure 跨平台 CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake 存放區 .NET SDK](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>將 Data Lake 存放區中的資料視覺化
您可以使用混合的資料湖存放區中儲存的資料服務 toocreate 視覺化表示。

![將 Data Lake Store 中的資料視覺化](./media/data-lake-store-data-scenarios/visualize-data.png "將 Data Lake Store 中的資料視覺化")

* 您可以使用啟動[Data Lake Store tooAzure SQL 資料倉儲的 Azure Data Factory toomove 資料](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* 在這之後，您可以[整合到 Azure SQL 資料倉儲的 Power BI](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate hello 資料的視覺表示法。
