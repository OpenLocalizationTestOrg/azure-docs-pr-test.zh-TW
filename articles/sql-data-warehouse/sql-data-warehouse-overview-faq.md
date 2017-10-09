---
title: "aaaAzure SQL 資料倉儲常見問題集 |Microsoft 文件"
description: "此文章列出客戶和開發人員針對 Azure SQL 資料倉儲的常見問題集"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>SQL 資料倉儲常見問題集

## <a name="general"></a>一般

問： 針對資料安全性，SQL DW 能提供什麼？

A. SQL DW 提供數個解決方案來保護資料，例如 TDE 和稽核。 如需詳細資訊，請參閱[安全性]。

問： 哪裡可以了解 SQL DW 符合規範的法規或企業標準？

A. 請瀏覽 hello [Microsoft 相容性]為不同的相容性供應項目依產品，例如 SOC 和 ISO 頁。 先選擇相容性標題，然後依序展開 [Azure hello Microsoft 範圍中雲端服務] 區段中 hello 右側的 hello 頁面 toosee 何種服務是 Azure 服務都相容。

問： 可以連接 PowerBI 嗎？

A. 可以！ 雖然 PowerBI 針對 SQL DW 支援直接查詢，但它並不適用於具有大量使用者或即時資料的情況。 針對 PowerBI 的生產用途，建議您在 Azure Analysis Services 或 Analysis Service IaaS 之上使用 PowerBI。 

問： SQL 資料倉儲的容量限制為何？

A. 請參閱我們目前的[容量限制]頁面。 

問： 為何我的延展/暫停/繼續需要花很久的時間？

A. 有許多因素可能會影響 hello 計算管理作業的時間。 一個導致長時間執行作業的常見原因是交易式回復。 初始化延展或暫停作業時，系統會封鎖所有傳入的工作階段，並清空查詢。 穩定的狀態中的順序 tooleave hello 系統，必須備份作業開始之前先回復交易。 hello 大量 hello 和較大的交易的 hello 記錄檔大小、 hello 長 hello 作業將會停止還原 hello 系統 tooa 穩定的狀態。

## <a name="user-support"></a>使用者支援

問： 我有一個功能要求，應該在哪裡提交？

A. 如果您有功能要求，請在我們的 [UserVoice] 頁面上提交

問： 我要如何執行某項作業？

A. 如需使用 SQL 資料倉儲進行開發的說明，您可以在我們的 [Stack Overflow] 頁面上提問。 

問： 我要如何提交支援票證？

A. [支援票證]可以透過 Azure 入口網站提出。

## <a name="sql-languagefeature-support"></a>SQL 語言/功能支援 

問： SQL 資料倉儲支援的資料類型為何？

A. 請參閱 SQL 資料倉儲[資料類型]。

問： 支援哪些資料表功能？

A. SQL 資料倉儲支援許多功能，不支援的功能都已記錄在[不支援的資料表功能]之中。

## <a name="tooling-and-administration"></a>工具和系統管理

問： 在 Visual Studio 中是否支援資料庫專案？

A. 針對 SQL 資料倉儲，我們目前在 Visual Studio 中不支援資料庫專案。 如果您想要 toocast 投票 tooget 這項功能，請造訪我們的 User Voice[資料庫專案功能要求]。

問： SQL 資料倉儲是否支援 REST API？

A. 是。 大部分可以搭配 SQL Database 使用的 REST 功能也可搭配 SQL 資料倉儲使用。 您可以在 REST 文件頁面或 [MSDN] 內找到 API 資訊。


## <a name="loading"></a>載入

問： 支援哪些用戶端驅動程式？

A. 可以在 hello 找到驅動程式支援的 DW[連接字串]頁面

問︰PolyBase 針對 SQL 資料倉儲支援何種檔案格式？

答︰Orc、RC、Parquet，以及一般分隔的文字

問： 我可以連接 toofrom SQL DW 使用 PolyBase？ 

答︰[Azure Data Lake Store] 和 [Azure 儲存體 Blob]

問： 是否計算下推可能連接儲存體 Blob 或 ADLS tooAzure 時？ 

答： 否，SQL DW PolyBase 僅互動 hello 儲存元件。 

問： 是否可以連線 tooHDI？

答： HDI 可以使用 ADLS 或 WASB hello HDFS 圖層。 如果您使用其中之一作為您的 HDFS 層，則您可以將該資料載入到 SQL DW。 不過，您無法產生下推計算 toohello HDI 執行個體。 

## <a name="next-steps"></a>後續步驟
如需整體 SQL 資料倉儲的詳細資訊，請參閱我們的[概觀]頁面。


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[連接字串]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[支援票證]: ./sql-data-warehouse-get-started-create-support-ticket.md
[安全性]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft 相容性]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[容量限制]: ./sql-data-warehouse-service-capacity-limits.md
[資料類型]: ./sql-data-warehouse-tables-data-types.md
[不支援的資料表功能]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure 儲存體 Blob]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[資料庫專案功能要求]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[概觀]: ./sql-data-warehouse-overview-faq.md