---
title: "Azure Data Lake Store 的 aaaOverview |Microsoft 文件"
description: "了解什麼是 Azure 資料湖存放區與 hello 的值，它提供跨其他資料存放區"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Azure 資料湖存放區概觀
Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。 Azure 資料湖可讓您在單一位置進行作業及探勘分析任何大小、 類型和擷取速度 toocapture 資料。

> [!TIP]
> 使用 hello [Data Lake Store 學習路徑](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/)toostart 瀏覽 hello Azure Data Lake Store 服務。
> 
> 

您可以從 Hadoop 存取 azure Data Lake Store （可與 HDInsight 叢集） 使用 hello WebHDFS 相容的 REST Api。 它是特別設計的 tooenable analytics hello 儲存資料並微調資料分析案例的效能。 超出 hello] 方塊中，其中包含所有 hello 企業級功能 — 安全性、 管理性、 延展性、 可靠性和可用性 — 不可或缺的真實世界的企業使用案例。

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Hello Azure 資料湖 hello 重要功能包括下列 hello。

### <a name="built-for-hadoop"></a>專為 Hadoop 而建置
hello Azure 資料湖存放區是 Apache Hadoop 檔案系統與 Hadoop 分散式檔案系統 (HDFS) 相容，並搭配 hello Hadoop 生態系統。  您現有 HDInsight 應用程式或服務使用 hello WebHDFS API 可以輕鬆地整合資料湖存放區。 資料湖存放區也會公開應用程式適用的 WebHDFS 相容 REST 介面

使用 Hadoop 分析架構 (例如 MapReduce 或 Hive)，可以輕鬆地分析資料湖存放區中儲存的資料。 Microsoft Azure HDInsight 叢集可以佈建，而且設定 toodirectly 存取資料湖存放區中儲存資料。

### <a name="unlimited-storage-petabyte-files"></a>無限制的儲存空間、PB 檔案
Azure 資料湖存放區提供無限制的儲存空間，適合用來儲存各種資料以供分析。 它不會造成任何帳戶大小、 檔案大小或 hello 資料湖中可儲存的資料量限制。 個別檔案的範圍的大小，因此極適合 toostore kb toopetabytes 從任何類型的資料。 藉由多個複本長期儲存資料，而且沒有 hello 的持續時間的 hello 資料可以儲存在 hello 資料湖沒有限制。

### <a name="performance-tuned-for-big-data-analytics"></a>針對巨量資料分析調整效能
Azure 資料湖存放區是針對執行大規模分析系統需要大量的輸送量 tooquery 及分析大量資料所建置。 hello 資料湖會將數個個別的存放裝置伺服器分散到檔案的部分。 這可改善 hello 讀取以平行方式來執行資料分析的 hello 檔案時，讀取輸送量。

### <a name="enterprise-ready-highly-available-and-secure"></a>符合企業需求：高度可用且安全
Azure 資料湖存放區提供符合業界標準的可用性和可靠性。 藉由對任何非預期失敗的備援複本 tooguard 永久儲存的資料資產。 企業可以在其解決方案中使用 Azure 資料湖，以成為其現有資料平台的重要部分。

資料湖存放區也提供 hello 儲存資料的企業級安全性。 如需詳細資訊，請參閱 [在 Azure 資料湖中保護資料](#DataLakeStoreSecurity)。

### <a name="all-data"></a>所有資料
Azure 資料湖存放區可以原生格式 (原樣) 儲存任何資料，而不需要任何先前的轉換。 資料湖存放區不會不需要之前載入 hello 資料、 定義結構描述 toobe 離開 toohello 個別分析架構 toointerpret hello 資料，而且在 hello 分析的 hello 階段定義的結構描述。 要能 toostore 任意大小和格式檔案，可讓資料湖存放區 toohandle 結構化、 半結構化及未結構化資料。

Azure 資料湖存放區的資料容器基本上是資料夾和檔案。 您在使用 Sdk、 Azure 網站和 Azure Powershell 的 hello 儲存資料上運作。 只要您將您的資料放入 hello 存放區，使用這些介面，並使用 hello 適當的容器時，您可以儲存任何類型的資料。 資料湖存放區不會執行任何特殊處理，依據 hello 它所儲存的資料類型的資料。

## <a name="DataLakeStoreSecurity"></a>在 Azure 資料湖存放區中保護資料
Azure Data Lake Store 使用 Azure Active Directory 進行驗證和存取控制清單 (Acl) toomanage 存取 tooyour 資料。

| 功能 | 說明 |
| --- | --- |
| 驗證 |Azure Data Lake Store 整合與 Azure Active Directory (AAD) 身分識別和存取管理的所有儲存在 Azure 資料湖存放區中的 hello 資料。 由於 hello 整合，從所有 AAD 功能，包括多重要素驗證、 條件式存取，以角色為基礎的存取控制、 應用程式使用量監視、 安全性監視和警示，Azure 資料湖優點等等。Azure Data Lake Store 支援 hello OAuth 2.0 通訊協定進行驗證與 hello REST 介面中。 |
| 存取控制 |Azure Data Lake Store 提供存取控制支援 POSIX 樣式 hello WebHDFS 通訊協定所公開的權限。 Hello 資料湖存放區公開預覽版 （hello 目前版本），Acl 可以啟用 hello 根資料夾、 子資料夾和個別檔案。 如需 ACL 如何在 Data Lake Store 的內容中運作的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。 |
| 加密 |資料湖存放區也提供儲存在 hello 帳戶中的資料加密。 您可以指定 hello 加密設定時建立的 Data Lake Store 帳戶。 您可以選擇 toohave 加密資料，或選擇不使用加密。 如需有關如何 tooprovide 加密相關的組態，請參閱[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。 |

想 toolearn 深入了解保護資料湖存放區中的資料。 請遵循以下的 hello 連結。

* 如需有關指示 toosecure 資料湖存放區中的資料，請參閱[保護 Azure 資料湖存放區中的資料](data-lake-store-secure-data.md)。
* 偏好影片？ [觀賞此視訊](https://mix.office.com/watch/1q2mgzh9nn5lx)toosecure 資料中的資料湖存放區的儲存方式。

## <a name="applications-compatible-with-azure-data-lake-store"></a>與 Azure 資料湖存放區相容的應用程式
Azure 資料湖存放區是與 hello Hadoop 生態系統中的最開放來源元件相容。 此外，還與其他 Azure 服務完美整合。 這讓 Data Lake Store 成為針對您的資料儲存需求的最佳選項。 請遵循下列 toolearn 深入了解如何使用 Data Lake Store 都具有開放原始碼元件，以及其他 Azure 服務的 hello 連結。

* 如需可與 Data Lake Store 互通的開放原始碼應用程式清單，請參閱 [與 Azure Data Lake Store 相容的應用程式和服務](data-lake-store-compatible-oss-other-applications.md) 。
* 請參閱[與其他 Azure 服務整合](data-lake-store-integrate-with-other-services.md)toounderstand 資料湖存放區如何搭配其他 Azure 服務 tooenable 廣泛的案例。
* 請參閱[案例的使用 Data Lake Store](data-lake-store-data-scenarios.md) toolearn toouse Data Lake 中的案例，例如擷取資料，將儲存的方式處理資料、 資料下載，並將資料視覺化。

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>什麼是 Azure Data Lake Store 檔案系統 (adl://)？
資料湖存放區可透過 hello 新檔案系統存取、 hello AzureDataLakeFilesystem (adl: / /)，在 Hadoop 環境 （適用於 HDInsight 叢集）。 應用程式和服務使用 adl: / / 會進一步效能最佳化，目前無法在 WebHDFS 無法 tootake 利用。 Data Lake Store 可讓您 hello 彈性 tooeither 如此一來，建議您選擇使用 adl hello 與可用 hello 達到最佳效能: / / 或直接繼續 toouse hello WebHDFS API 維護現有的程式碼。 Azure HDInsight 完全利用 hello AzureDataLakeFilesystem tooprovide hello 上的獲得最佳效能資料湖存放區。

您可以存取您的資料 hello 資料湖存放區使用`adl://<data_lake_store_name>.azuredatalakestore.net`。 如需有關如何 tooaccess hello hello 資料湖存放區中的資料的詳細資訊，請參閱[檢視的 hello 屬性儲存的資料](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>如何開始使用 Azure 資料湖存放區？
請參閱[開始使用 Data Lake Store hello Azure 入口網站](data-lake-store-get-started-portal.md)，如何使用 Data Lake Store tooprovision hello Azure 入口網站上。 一旦您已佈建 Azure 資料湖，您可以了解如何例如 Azure Data Lake Analytics 或資料湖存放區與 Azure HDInsight toouse 巨量資料供應項目。 您也可以建立.NET 應用程式 toocreate Azure Data Lake Store 帳戶，並執行作業，例如上傳資料、 下載資料等。

* [開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配資料湖存放區使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
* [使用 .NET SDK 開始使用 Azure 資料湖存放區](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Data Lake Store 影片
如果您想觀賞視訊 toolearn，資料湖存放區提供影片的功能範圍。

* [建立 Azure Data Lake Store 帳戶](https://mix.office.com/watch/1k1cycy4l4gen)
* [使用 Azure 資料湖存放區中的 hello 資料總管 tooManage 資料](https://mix.office.com/watch/icletrxrh6pc)
* [連接到 Azure Data Lake Analytics tooAzure 資料湖存放區](https://mix.office.com/watch/qwji0dc9rx9k)
* [透過 Data Lake Analytics 存取 Azure Data Lake Store](https://mix.office.com/watch/1n0s45up381a8)
* [連接到 Azure HDInsight tooAzure 資料湖存放區](https://mix.office.com/watch/l93xri2yhtp2)
* [透過 Hive 和 Pig 存取 Azure Data Lake Store](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [從 Azure 資料湖存放區使用 DistCp （Hadoop 分散式複製） toocopy 資料 tooand](https://mix.office.com/watch/1liuojvdx6sie)
* [使用 Apache Sqoop toomove 關聯式來源與 Azure 資料湖存放區之間的資料](https://mix.office.com/watch/1butcdjxmu114)
* [使用 Azure Data Factory 進行 Azure Data Lake Store 的資料協調](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Hello Azure Data Lake Store 中保護資料](https://mix.office.com/watch/1q2mgzh9nn5lx)

