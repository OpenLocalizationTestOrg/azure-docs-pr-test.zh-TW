---
title: "與其他 Azure 服務的 Data Lake Store aaaIntegrating |Microsoft 文件"
description: "了解 Data Lake Store 如何與其他 Azure 服務整合"
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>整合 Data Lake Store 與其他 Azure 服務
Azure Data Lake Store 可搭配其他 Azure 服務 tooenable 廣泛的案例。 hello 下列文章列出 hello 資料湖存放區可以與整合的服務。

## <a name="use-data-lake-store-with-azure-hdinsight"></a>搭配 Azure HDInsight 使用 Data Lake Store
您可以佈建[Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)使用 Data Lake Store 為 hello HDFS 相容存放裝置叢集。 對於此版本，Windows 和 Linux 上的 Hadoop 和 Storm 叢集，您只能使用 Data Lake Store 做為額外的儲存體。 這類叢集仍會使用 Azure 儲存體 (WASB) 作為 hello 預設儲存體。 不過，HBase 叢集在 Windows 和 Linux 上，您可以使用 Data Lake Store 為 hello 預設儲存體，或其他存放裝置，或兩者。

如需有關如何 tooprovision 在 HDInsight 叢集與資料湖存放區的指示，請參閱：

* [使用 Azure 入口網站佈建 HDInsight 叢集與 Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [使用 Azure PowerShell 以 Data Lake Store 佈建 HDInsight 叢集作為預設儲存體](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [使用 Azure PowerShell 以 Data Lake Store 佈建 HDInsight 叢集作為額外儲存體](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>搭配 Azure Data Lake Analytics 使用 Data Lake Store
[Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-overview.md)可讓您在雲端規模的 toowork 大型資料。 它以動態方式佈建資源，讓您能夠進行分析 TB 或甚至是 EB 的資料，這些資料可以儲存在許多支援的資料來源，其中一個就是 Data Lake Store。 Data Lake Analytics 是特別最佳化的 toowork 與 Azure 資料湖存放區-提供 hello 最高層級的效能、 輸送量和為您的平行化巨量資料工作負載。

如需有關指示 toouse 資料湖分析與資料湖存放區，請參閱[開始使用 Data Lake Analytics 使用 Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)。

## <a name="use-data-lake-store-with-azure-data-factory"></a>搭配 Azure Data Factory 使用 Data Lake Store
您可以使用[Azure Data Factory](https://azure.microsoft.com/services/data-factory/) tooingest 資料從 Azure 資料表、 Azure SQL Database、 Azure SQL 資料倉儲、 Azure 儲存體 Blob，並在內部部署資料庫。 Azure Data Factory 正在公民 hello Azure 生態系統中的，可以是使用的 tooorchestrate hello 擷取的資料從這些來源 tooAzure 資料湖存放區。

如需有關如何 toouse Azure Data Factory 與資料湖存放區，請參閱指示[使用 Data Factory 的資料湖存放區中移動資料 tooand](../data-factory/data-factory-azure-datalake-connector.md)。

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>將資料從 Azure 儲存體 Blob 複製到 Data Lake Store 中
Azure Data Lake Store 提供的命令列工具，AdlCopy，可讓您從 Azure Blob 儲存體 toocopy 資料到 Data Lake Store 帳戶。 如需詳細資訊，請參閱[將資料從 Azure 儲存體 Blob tooData 湖存放區複製](data-lake-store-copy-data-azure-storage-blob.md)。

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>在 Azure SQL Database 和 Data Lake Store 之間複製資料
您可以使用 Apache Sqoop tooimport 和匯出 Azure SQL Database 與資料湖存放區之間的資料。 如需詳細資訊，請參閱 [使用 Sqoop 在 Data Lake Store 和 Azure SQL Database 之間複製資料](data-lake-store-data-transfer-sql-sqoop.md)。

## <a name="use-data-lake-store-with-stream-analytics"></a>使用 Data Lake Store 搭配串流分析
您可以使用 Data Lake Store hello 的其中一個輸出資料流處理使用 Azure Stream Analytics toostore 資料。 如需詳細資訊，請參閱 [使用 Azure 串流分析將來自 Azure 儲存體 Blob 的資料串流處理至 Data Lake Store](data-lake-store-stream-analytics.md)。

## <a name="use-data-lake-store-with-power-bi"></a>使用 Data Lake Store 搭配 Power BI
您可以使用 Data Lake Store 帳戶 tooanalyze 從 Power BI tooimport 資料，並將 hello 資料視覺化。 如需詳細資訊，請參閱 [在 Data Lake Store 中使用 Power BI 分析資料](data-lake-store-power-bi.md)。

## <a name="use-data-lake-store-with-data-catalog"></a>使用 Data Lake Store 搭配資料目錄
您可以註冊資料湖存放區 hello Azure 資料目錄 toomake hello 資料 hello 組織可探索到的資料。 如需詳細資訊，請參閱[在 Azure 資料目錄中註冊來自 Data Lake Store 的資料](data-lake-store-with-data-catalog.md)。

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>將 Data Lake Store 搭配 SQL Server Integration Services (SSIS) 使用
SSIS tooconnect SSIS 封裝與 Azure 資料湖存放區中，您可以使用 hello Azure Data Lake Store 連接管理員。 如需詳細資訊，請參閱[將 Data Lake Store 搭配 SSIS 使用](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager)。

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>將 Data Lake Store 搭配 SQL 資料倉儲使用
您可以使用 Azure Data Lake Store PolyBase tooload 資料到 SQL 資料倉儲。 如需詳細資訊，請參閱[將 Data Lake Store 搭配 SQL 資料倉儲使用](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md)。

## <a name="see-also"></a>另請參閱
* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
* [使用入口網站開始使用 Data Lake Store](data-lake-store-get-started-portal.md)
* [使用 PowerShell 開始使用 Data Lake Store](data-lake-store-get-started-powershell.md)  

