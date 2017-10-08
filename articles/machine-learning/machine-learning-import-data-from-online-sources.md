---
title: "從線上資料來源的 Machine Learning Studio aaaImport 資料 |Microsoft 文件"
description: "如何 tooimport 定型資料從各種不同的線上來源的 Azure Machine Learning Studio。"
keywords: "匯入資料、資料格式、資料類型、資料來源、定型資料"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>資料匯入至 Azure Machine Learning Studio 從與 hello 資料匯入模組的各種線上資料來源
這篇文章描述 hello 支援從各種來源匯入線上資料及 hello 所需的資訊來自這些來源的 toomove 資料至 Azure 機器學習實驗。

> [!NOTE]
> 本文章提供一般資訊 hello[匯入資料][ import-data]模組。 格式、 參數和答案 toocommon 問題，如需詳細的資料，您可以存取的 hello 類型的相關資訊，請參閱 hello hello 模組參考主題[匯入資料][ import-data]模組。
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>簡介
使用 hello[匯入資料][ import-data]模組，您可以從數個線上資料來源的其中一個存取資料，您的實驗執行時[Azure Machine Learning Studio](https://studio.azureml.net/Home):

* 使用 HTTP 的 Web URL
* 使用 HiveQL 的 Hadoop
* Azure Blob 儲存體
* Azure 資料表
* Azure SQL Database 或 Azure VM 上的 SQL Server
* 內部部署 SQL Server 資料庫
* 資料摘要提供者，目前為 OData
* Azure CosmosDB (先前稱為 DocumentDB)

tooaccess 線上資料來源中 Studio 實驗中，新增 hello[匯入資料][ import-data]模組 tooyour、 選取 hello**資料來源**，然後提供所需的 hello 參數tooaccess hello 資料。 支援的 hello 線上資料來源會分項 hello 如下表中。 此資料表也摘要了 hello 所支援的檔案格式，並使用的 tooaccess 參數 hello 資料。

請注意，這項訓練資料會在您的實驗執行時存取，因此只有在該實驗中才可使用。 相較之下，已將其儲存在資料集的模組中的資料，則可用 tooany 實驗工作區中。

> [!IMPORTANT]
> 目前，hello[匯入資料][ import-data]和[匯出資料][ export-data]模組可以讀取和寫入資料只能從 Azure 儲存體使用 hello 建立傳統部署模型。 換句話說，hello 新的 Azure Blob 儲存體帳戶類型，提供最忙碌的儲存體的存取層，或不支援項很棒的儲存體的存取層。 
> 
> 一般而言，任何您可能已在這個服務選項變成可供使用之前建立的 Azure 儲存體帳戶應該不會受到影響。 
> 如果您需要 toocreate 新帳戶，請選取**傳統**hello 部署模型，或使用資源管理員，然後選取**一般用途**而**Blob 儲存體**的**帳戶類型**。 
> 
> 如需詳細資訊，請參閱 [Azure Blob 儲存體︰經常性存取與非經常性存取儲存層](../storage/blobs/storage-blob-storage-tiers.md)。
> 
> 

## <a name="supported-online-data-sources"></a>支援的線上資料來源
Azure Machine Learning**匯入資料**模組支援下列資料來源的 hello:

| 資料來源 | 說明 | 參數 |
| --- | --- | --- |
| 透過 HTTP 的 Web URL |從任何使用 HTTP 的 Web URL 中讀取逗號分隔值 (CSV)、tab 分隔值 (TSV)、屬性關聯檔案格式 (ARFF) 和支援向量機器 (SVM-light) 格式的資料 |<b>URL</b>： 指定 hello hello 檔案，包括 hello 網站 URL 和 hello 檔案名稱，以及任何擴充功能的完整名稱。 <br/><br/><b>資料格式</b>： 指定其中一個支援的 hello 資料格式： CSV、 TSV、 ARFF 或 SVM light。 如果 hello 資料有標頭資料列，則使用的 tooassign 資料行名稱。 |
| Hadoop/HDFS |從 Hadoop 中的分散式儲存體讀取資料。 您指定您想要利用 HiveQL，類似 SQL 的查詢語言的 hello 資料。 HiveQL 也可以是使用的 tooaggregate 資料，並執行新增 hello 資料 tooMachine Learning Studio 之前篩選資料。 |<b>Hive 資料庫查詢</b>： 指定 hello Hive 查詢使用 toogenerate hello 資料。<br/><br/><b>HCatalog 伺服器 URI </b> ： 叢集使用 hello 格式的指定的 hello 名稱*&lt;叢集名稱&gt;。.azurehdinsight.net。*<br/><br/><b>Hadoop 使用者帳戶名稱</b>： 指定 hello Hadoop 使用者帳戶使用 tooprovision hello 叢集的名稱。<br/><br/><b>Hadoop 使用者帳戶密碼</b>： 指定 hello 佈建 hello 叢集時所使用的認證。 如需詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](../hdinsight/hdinsight-provision-clusters.md)。<br/><br/><b>輸出資料的位置</b>： 指定是否 hello 資料會儲存在 Hadoop 分散式檔案系統 (HDFS) 還是 Azure 中。 <br/><ul>如果您將輸出資料儲存在 HDFS 中，指定 hello HDFS 伺服器 URI。 （不含 hello HTTPS:// 前置詞是確定 toouse hello HDInsight 叢集名稱）。 <br/><br/>如果您在 Azure 中儲存您的輸出資料，您必須指定 hello Azure 儲存體帳戶名稱、 儲存體存取金鑰和儲存體容器名稱。</ul> |
| SQL Database |讀取儲存在 Azure SQL Database 或執行於 Azure 虛擬機器之 SQL Server 資料庫中的資料。 |<b>資料庫伺服器名稱</b>： 指定 hello hello 伺服器正在執行哪些 hello 資料庫名稱。<br/><ul>Azure SQL Database 時輸入 hello 伺服器名稱所產生。 通常，它包含 hello 表單 *&lt;generated_identifier&gt;。.database.windows.net。* <br/><br/>若為裝載於 Azure 虛擬機器上的 SQL Server，請輸入 tcp:&lt;Virtual Machine DNS Name&gt;, 1433</ul><br/><b>資料庫名稱</b>: hello 伺服器上指定 hello hello 資料庫名稱。 <br/><br/><b>伺服器的使用者帳戶名稱</b>： 指定具有 hello 資料庫的存取權限的帳戶的使用者名稱。 <br/><br/><b>伺服器使用者帳戶密碼</b>： 指定 hello hello 使用者帳戶的密碼。<br/><br/><b>接受任何伺服器憑證</b>： 如果您想 tooskip 讀取資料之前，檢閱 hello 站台憑證，請使用此選項 （較不安全）。<br/><br/><b>資料庫查詢</b>： 輸入 SQL 陳述式描述您想要 tooread hello 資料。 |
| 內部部署 SQL Database |讀取內部部署 SQL Database 中儲存的資料。 |<b>部署資料閘道</b>： 指定 hello hello 它可以在其中存取您的 SQL Server 資料庫的電腦上安裝資料管理閘道器名稱。 Hello 閘道設定的詳細資訊，請參閱[執行進階分析與 Azure Machine Learning 使用的資料從內部部署 SQL server](machine-learning-use-data-from-an-on-premises-sql-server.md)。<br/><br/><b>資料庫伺服器名稱</b>： 指定 hello hello 伺服器正在執行哪些 hello 資料庫名稱。<br/><br/><b>資料庫名稱</b>: hello 伺服器上指定 hello hello 資料庫名稱。 <br/><br/><b>伺服器的使用者帳戶名稱</b>： 指定具有 hello 資料庫的存取權限的帳戶的使用者名稱。 <br/><br/><b>使用者名稱和密碼</b>： 按一下<b>輸入值</b>tooenter 資料庫認證。 根據您內部部署 SQL Server 的設定方式而定，您可以使用 Windows 整合式驗證或 SQL Server 驗證。<br/><br/><b>資料庫查詢</b>： 輸入 SQL 陳述式描述您想要 tooread hello 資料。 |
| Azure 資料表 |從 hello Azure 儲存體中的資料表服務讀取資料。<br/><br/>如果您不常讀取大量的資料，請使用 hello Azure 資料表服務。 它可提供有彈性、非關聯式 (NoSQL)、具有超高延展性、經濟的且高度可用的儲存解決方案。 |hello 選項在 hello**匯入資料**依據您要存取公用資訊還是需要登入認證的私人儲存體帳戶。 這由 hello<b>驗證類型</b>且可以包含每一個都有它自己的參數集 」 PublicOrSAS"或"Account"的值。 <br/><br/><b>公用或共用存取簽章 (SAS) URI</b>: hello 參數：<br/><br/><ul><b>資料表 URI</b>: hello 資料表指定 hello 公用或 SAS URL。<br/><br/><b>指定屬性名稱的 hello 列 tooscan</b>: hello 的值為<i>TopN</i> tooscan hello 指定資料列數目或<i>ScanAll</i> tooget 所有 hello 資料表中的資料都列。 <br/><br/>如果是同質性且可預測 hello 資料，建議您選取*TopN*並輸入 n 的數字對於大型資料表，這會導致加快讀取速度。<br/><br/>如果 hello 資料使用不同 hello 深度和位置 hello 資料表為基礎的屬性集的結構化，請選擇 hello *ScanAll*選項 tooscan 所有資料列。 這可確保產生的屬性和中繼資料轉換的 hello 完整性。<br/><br/></ul><b>私用儲存體帳戶</b>: hello 參數： <br/><br/><ul><b>帳戶名稱</b>： 指定 hello 包含 hello 資料表 tooread hello 帳戶名稱。<br/><br/><b>帳戶金鑰</b>： 指定 hello hello 帳戶相關聯的儲存體金鑰。<br/><br/><b>資料表名稱</b>： 指定 hello 包含 hello 資料 tooread hello 資料表名稱。<br/><br/><b>屬性名稱的資料列 tooscan</b>: hello 的值為<i>TopN</i> tooscan hello 指定資料列數目或<i>ScanAll</i> tooget 所有 hello 資料表中的資料都列。<br/><br/>如果是同質性且可預測 hello 資料，我們建議您選取*TopN*並輸入 n 的數字對於大型資料表，這會導致加快讀取速度。<br/><br/>如果 hello 資料使用不同 hello 深度和位置 hello 資料表為基礎的屬性集的結構化，請選擇 hello *ScanAll*選項 tooscan 所有資料列。 這可確保產生的屬性和中繼資料轉換的 hello 完整性。<br/><br/> |
| Azure Blob 儲存體 |會讀取儲存在 Azure 儲存體，包括影像、 非結構化的文字或二進位資料中的 hello Blob 服務中的資料。<br/><br/>您可以使用 hello Blob 服務 toopublicly 公開資料或 tooprivately 市集應用程式資料。 您可以使用 HTTP 或 HTTPS 連線從任何地方存取您的資料。 |hello 選項在 hello**匯入資料**模組變更根據您要存取公用資訊還是需要登入認證的私人儲存體帳戶。 這由 hello<b>驗證類型</b>且可以包含的 「 PublicOrSAS"或"Account"的值。<br/><br/><b>公用或共用存取簽章 (SAS) URI</b>: hello 參數：<br/><br/><ul><b>URI</b>: hello 儲存體 blob 指定 hello 公用或 SAS URL。<br/><br/><b>檔案格式</b>: hello Blob 服務中指定 hello hello 資料格式。 hello 支援的格式為 CSV、 TSV 和 ARFF。<br/><br/></ul><b>私用儲存體帳戶</b>: hello 參數： <br/><br/><ul><b>帳戶名稱</b>： 指定 hello hello 帳戶包含您想要 tooread hello blob 名稱。<br/><br/><b>帳戶金鑰</b>： 指定 hello hello 帳戶相關聯的儲存體金鑰。<br/><br/><b>路徑 toocontainer、 目錄或 blob </b> ： 指定包含 hello 資料 tooread hello blob hello 名稱。<br/><br/><b>Blob 檔案格式</b>: hello blob 服務中指定 hello hello 資料格式。 hello 支援的資料格式包括 CSV、 TSV、 ARFF、 CSV 與指定的編碼方式和 Excel。 <br/><br/><ul>如果 hello 格式為 CSV 或 TSV，是確定 tooindicate 是否 hello 檔案包含標頭資料列。<br/><br/>您可以使用 hello Excel 選項 tooread 資料從 Excel 活頁簿。 在 hello <i>Excel 資料格式</i>選項，指出是否 hello 資料在 Excel 工作表範圍，或在 Excel 資料表。 在 hello <i>Excel 工作表或內嵌的資料表</i>選項，請指定 hello hello 工作表或您想要從 tooread 的資料表名稱。</ul><br/> |
| 資料摘要提供者 |從支援的摘要提供者讀取資料。 支援目前只有 hello 開放式資料通訊協定 (OData) 格式。 |<b>資料內容類型</b>： 指定 hello OData 格式。<br/><br/><b>來源 URL</b>： 指定 hello hello 資料摘要的完整 URL。 <br/>例如，hello hello Northwind 範例資料庫中的下列 URL 讀取： http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>後續步驟

[部署使用資料匯入和資料匯出模組的 Azure ML Web 服務](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
