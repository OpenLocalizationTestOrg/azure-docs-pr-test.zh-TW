---
title: "aaaWhat 的 Azure 資料目錄的新 |Microsoft 文件"
description: "本文提供的新功能總覽加入 tooAzure 資料目錄。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>Azure 資料目錄的新功能
也會更新**Azure 資料目錄**會定期發行。 並非所有發行版本都會包含新的使用者對應功能，某些版本會著重在後端服務功能。 此頁面會反白顯示新的使用者互動功能加入的 toohello Azure 資料目錄服務。

## <a name="whats-new-for-august-2017"></a>2017 年 8 月的新功能 
為準，年 8 月 2017 hello 下列功能已加入 tooAzure 資料目錄：

*   新的開發人員範例是用來建立和使用 hello 資料目錄 REST API 來管理關聯性的中繼資料。 hello*關聯性資訊匯入資料目錄*範例位於 hello[資料目錄的程式碼範例頁面](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0)。 
* 註冊使用 hello 資料來源註冊工具的相關的資料表時，支援擷取聯結從 Teradata 資料來源的關聯性中繼資料。
* 支援的 SQL Server 資料表值函式 (TVF) 的物件註冊 SQL Server 資料來源使用 hello 資料來源註冊工具時。
* 多個更新和因 tooincrease hello 的效能和可用性 hello 資料目錄入口網站。

## <a name="whats-new-for-july-2017"></a>2017 年 7 月的新功能 
自七月 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   對更精確控制允許之中繼資料作業的支援包括：
    - 目錄系統管理員可以限制使用者的能力 toocontribute 標記及相關的中繼資料 toohello 類別目錄中，啟用唯讀存取 toohello 類別目錄。
    - 目錄系統管理員可以限制使用者的能力 tooregister 新的資料來源 hello 目錄中。
    - 目錄系統管理員可以限制使用者的能力 tootake 擁有權的 hello 目錄中的資料資產中繼資料。
    - Active Directory 安全性群組 tooAzure 和簡化的管理的權限的使用者可以授與權限。
* 已註冊的資料資產，以及在 hello 資料目錄入口網站的探索相關的資料資產之間的關聯性的支援包括：
    - 擷取關聯性的中繼資料 （包括 Azure SQL Database） 的 SQL Server、 Oracle 和 MySQL 從資料來源時使用 hello 資料目錄的資料來源註冊工具。
    - 探索的相關的資料資產 hello 資料目錄入口網站中檢視資產中繼資料時。
    - 作業 toodefine 探索及管理使用 hello 資料目錄 REST API 的資料資產之間的關聯性。

如需管理資料目錄中的權限的詳細資訊，請參閱[toosecure toodata 類別目錄和資料資產的存取方式](data-catalog-how-to-secure-catalog.md)。
如需詳細資料目錄中的關聯性的詳細資訊，請參閱[tooview 與 Azure 資料目錄中的資料資產的相關](data-catalog-how-to-view-related-data-assets.md)。

## <a name="whats-new-for-june-2017"></a>2017 年 6 月的新功能 
為準，年 6 月 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   支援 Sybase、Apache Cassandra 和 MongoDB 資料來源。 使用者現在可以註冊及探索 Cassandra 與 MongoDB 資料庫和資料表，以及 Sybase 資料庫、資料表和檢視表。

> [!NOTE]
> 當註冊 MongoDB 和 Cassandra 包括例如記錄和陣列的複雜資料類型的資料行，這些資料行的資料表將不會包含在 hello 中繼資料中加入 tooData 類別目錄。

## <a name="whats-new-for-may-2017"></a>2017 年 5 月的新功能 
為準，可能 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   新的開發人員範例適用於 hello 大量匯入的商務字彙字詞。 hello 詞彙大量匯入範例位於 hello[資料目錄開發人員範例頁面](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples)。 
*   支援編輯 hello Azure 資料目錄入口網站中的 ODBC 連接資訊。 資料資產擁有者和資料目錄管理員現在可以編輯已註冊的 ODBC 資料來源的 hello 連接資訊而不需要 toore 暫存器 hello 資料來源。
*   支援商務詞彙定義和描述中的可點選 URL。 Url 在 hello 描述和定義屬性中包含的商務字彙字詞時，會顯示 hello Url 為 hello 資料目錄入口網站中的超連結。
*   除了還支援專家的顯示名稱 tooexpert 電子郵件地址。 檢視時在 hello 屬性中的資料資產的專家 hello 資料目錄入口網站中，Azure Active Directory 中的 hello 專家的完整名稱將顯示 hello 工具提示中。

## <a name="whats-new-for-april-2017"></a>2017 年 4 月的新功能 
為準，年 4 月 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   支援 ODBC 資料來源。 使用者現在可以註冊及探索 ODBC 資料庫、 資料表和檢視表使用 hello 資料目錄資料的來源註冊工具。

## <a name="whats-new-for-march-2017"></a>2017 年 3 月的新功能 
為準，年 3 月 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   支援對資料目錄管理員使用 AAD 安全性群組。
*   Azure 資料目錄目前已在新的 Azure 區域中提供。 客戶可以佈建 hello Azure 資料目錄中新增 tooEast 美國、 美國西部、 西歐、 和澳洲東部、 北歐、 和東南亞 hello 西部中央區域中。 如需詳細資訊，請參閱 [Azure 地區](https://azure.microsoft.com/regions/)。

## <a name="whats-new-for-february-2017"></a>2017 年 2 月的新功能 
為準，2 月版 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   Hello 資料目錄資料的來源註冊工具中的進階設定的支援。 註冊大型資料來源時，使用者可以指定命令逾時值。
*   支援 FTP 和 PostgreSQL 資料來源。 使用者現在可以註冊及探索 FTP 檔案和目錄，以及 PostgreSQL 資料庫、資料表和檢視表。

## <a name="whats-new-for-january-2017"></a>2017 年 1 月的新功能 
為準，年 1 月 2017 hello 下列功能已加入 tooAzure 資料目錄：
*   Azure 資料目錄現在符合 [CSA STAR](https://www.microsoft.com/trustcenter/compliance/csa-star-certification) 標準。
*   與 [Excel 2016 和 Power Query for Excel 中的取得及轉換](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605)整合。 Excel 使用者可以從 Excel 內部使用 Azure 資料目錄來共用查詢及探索查詢。 這項功能是可用 toousers 與 Power BI Pro 授權。

## <a name="whats-new-for-december-2016"></a>2016 年 12 月的新功能
年 12 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：
*   Azure 資料目錄現在符合 [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) 和[歐盟示範條款](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses)標準。
*   支援編輯資料來源連線資訊。 資料資產擁有者和資料目錄管理員現在可以編輯 hello 註冊的資料來源的連接資訊而不需要 toore 暫存器 hello 資料來源。
*   支援 Salesforce.com 資料來源。 使用者現在可以註冊及探索 Salesforce 物件。


## <a name="whats-new-for-november-2016"></a>2016 年 11 月的新功能
11 月版從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：
*   Azure 資料目錄現在符合 [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) 和 [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018) 標準。
*   Hello 手動註冊使用 hello 資料目錄入口網站和 REST API 的 ODBC 資料來源的支援。

## <a name="whats-new-for-september-2016"></a>2016 年 9 月的新功能
年 9 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：

* 支援 IBM DB2 資料來源。 使用者現在可以註冊並探索 DB2 資料庫、資料表和檢視。
* 支援 Azure Cosmos DB 資料來源。 使用者現在可以註冊並探索 Cosmos DB 資料庫和集合。
* 支援自訂 hello 資料目錄入口網站中的 hello 目錄名稱。 目錄系統管理員現在可以提供顯示在 hello 入口網站標題，例如 hello 組織名稱中的文字。

## <a name="whats-new-for-august-2016"></a>2016 年 8 月的新功能
年 8 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：

* 增強 SQL Server Master Data Services (MDS) 資料來源的註冊功能。 註冊使用 hello 資料目錄資料的來源註冊工具 MDS 實體時，使用者現在可以包含 預覽和資料設定檔。
* 支援管理員定義的組織已儲存的搜尋。 當儲存搜尋 hello 資料目錄入口網站中，資料目錄系統管理員現在可以選擇 toosave 搜尋供個人使用，或所有目錄使用者。 組織已儲存的搜尋會與所有目錄使用者共用，而且可以提供標準化的起點來探索資料來源。
* 更新 toohello hello 資料目錄入口網站中的內容檢視。 所有的資料資產屬性現在會顯示在中和管理單一、 可調整大小的窗格 tooprovide 更一致且可探索體驗。

## <a name="whats-new-for-july-2016"></a>2016 年 7 月的新功能
年 7 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：

* 支援 SQL Server Master Data Services (MDS) 資料來源。 使用者現在可以註冊並探索 MDS 模型和實體。
* 支援 SQL Server 預存程序。 使用者現在可以註冊並探索 SQL Server 資料來源中的預存程序物件。
* Hello Azure 資料目錄入口網站和 hello 資料來源註冊工具中，總共有 18 受支援的語言中的其他語言的支援。 hello Azure 資料目錄使用者經驗會根據 hello 或 hello 網頁瀏覽器視窗中設定的語言喜好設定來當地語系化。
* 更新和 hello 資料目錄入口網站首頁上，包括效能改進和簡化的使用者經驗的細分。

## <a name="whats-new-for-june-2016"></a>2016 年 6 月的新功能
年 6 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：

* 調整 hello 清單檢視中的資料行的大小，當您發現 hello 資料目錄入口網站中的資料資產的支援。 使用者現在可以調整個別的資料行 toomore 容易閱讀冗長的資產中繼資料，例如標籤和描述。
* Power Query for Excel 已加入 toohello 」 中開啟 」 功能表中的 hello 資料目錄入口網站。 使用者現在可以開啟支援的資料來源在 Excel 2016 或 Excel 2010 與 Excel 2013 中以 hello [Power Query for Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605)增益集安裝。
* 支援 Azure 表格儲存體的資料來源。 使用者現在可以註冊並探索 Azure 儲存體資料來源中的資料表物件。

## <a name="whats-new-for-may-2016"></a>2016 年 5 月的新功能
可能從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：

* 商務字彙讓目錄系統管理員 toodefine 商務詞彙和階層 toocreate 通用的商務詞彙。 使用者可以標記註冊的資料資產詞彙條款 toomake 它更容易 toodiscover 並了解 hello hello 目錄內容。 如需詳細資訊，請參閱[向上 tooset 來控管標記所 hello 的商務字彙](data-catalog-how-to-business-glossary.md)  
* 增強功能 toohello 可讓使用者 tooupdate 多個詞彙，在單一作業中的資料目錄商務字彙。 使用者可以選取多個詞彙 tooedit hello 下列欄位：
  * 父系字詞： hello 使用者可以選取新的父系字詞，與所有選取的詞彙的 hello 選取父系字詞更新的 toobe 子項目。 如果 hello 選取的詞彙都 hello 相同的父系，則該父代會顯示在 hello 文字方塊中，否則 hello 父詞彙欄位組 tooblank。   
  * 標記和專案關係人： 使用者可以新增或移除多個使用相同的經驗的 hello 做為標記多個資料資產的字彙字詞標籤和專案關係人。

> [!NOTE]
> hello 商務字彙是只能在 hello 標準版本的 Azure 資料目錄。 hello 免費版本未提供功能管標記或商務字彙。

## <a name="whats-new-for-march-2016"></a>2016 年 3 月的新功能
年 3 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄： g:

* 用於以程式設計方式存取 hello 搜尋功能以及 hello Azure 資料目錄服務類別目錄資產管理功能合併的 REST API 端點。 此搜尋 API 端點和目錄 API 端點已在 2016 年 3 月 21 日被取代並終止。 沒有任何變更 toohello hello API 語意。 只有 hello 端點 URI 變更。 如需詳細資訊，請參閱 hello [Azure 資料目錄 REST API 參考](https://msdn.microsoft.com/library/azure/mt267595.aspx)。 如需 API 範例，請參閱 [Azure 資料目錄開發人員範例](data-catalog-samples.md)。

## <a name="whats-new-for-february-2016"></a>2016 年 2 月的新功能
從 2016 年 2 月開始 hello 下列功能已加入 tooAzure 資料目錄：

* 選取新的重新設計的資料來源會遇到 hello Azure 資料目錄資料的來源註冊工具。 hello 資料來源註冊工具已更新的 toomake it 更容易支援您 toolocate 和 hello 資料來源選取的 Azure 資料目錄。
* Hello Azure 資料目錄入口網站和 hello 資料來源註冊工具中的 10 個其他語言的支援。 此外 tooEnglish，hello Azure 資料目錄體驗現已推出德文、 西班牙文、 法文、 義大利文、 日文、 韓文、 巴西葡萄牙文、 俄文、 簡體中文和繁體中文。 hello Azure 資料目錄使用者經驗已經過當地語系化根據 hello 或 hello 使用者 web 瀏覽器視窗中設定的語言喜好設定。
* 針對商務持續性及災害復原，支援 Azure 資料目錄資料的異地複寫功能。 所有的 Azure 資料目錄內容，包括資料來源的中繼資料和 crowdsourced 註解，現在會在沒有額外的成本 toocustomers 的兩個 Azure 區域之間進行複寫。 hello Azure 區域預先成對出現，至少 500 英哩，並遵循 hello 對應中所述[業務續航力和災害復原 (BCDR): Azure 配對區域](../best-practices-availability-paired-regions.md)。
* 支援變更 hello Azure 資料目錄所使用的 Azure 訂用帳戶。 Azure 資料目錄系統管理員可以使用 hello Azure 資料目錄入口網站 tooselect 不同的 Azure 訂用帳戶中 hello 設定 頁面上，供計費。

## <a name="whats-new-for-january-2016"></a>2016 年 1 月的新功能
年 1 月從 2016年開始，下列功能的 hello 已加入 tooAzure 資料目錄：

* 支援手動註冊其他資料來源。 現在，您可以使用 「 建立手動項目 」 在 hello Azure 資料目錄入口網站，或使用下列資料來源的 hello Azure 資料目錄 REST API tooregister hello:
  * OData - 函式、實體集和實體容器
  * HTTP - 檔案、端點、報告和網站
  * 檔案系統 - 檔案
  * SharePoint - 清單
  * FTP - 檔案和目錄
  * Salesforce.com - 物件
  * DB2 - 資料表、檢視和資料庫
  * PostgreSQL - 資料表、檢視和資料庫
* 針對 SQL Server (包含 Azure SQL DB 和 Azure SQL 資料倉儲) 資料來源支援「在 SQL Server Data Tools 中開啟」。  
* 支援註冊與探索 SAP HANA 檢視和封裝。 您可以註冊使用 hello Azure 資料目錄資料的來源來源註冊工具，可以加上註解和探索使用 hello Azure 資料目錄入口網站註冊的 SAP HANA 資料來源的 SAP HANA 資料。
* hello 能力 toopin 和取消釘選 hello Azure 資料目錄入口網站中的資料資產。 您可以選擇 toopin 資料資產 toomake 它們更容易 toorediscover 和重複使用。
* Hello Azure 資料目錄入口網站中新的重新設計的首頁。 新首頁 hello 包含 hello 目前使用者的活動-新的發行資產，包括釘選的資產，以及已儲存的搜尋-深入了解和深入了解 hello 活動 hello 類別目錄做為整個。
* Hello Azure 資料目錄入口網站中的持續性的使用者設定的支援。 使用者經驗設定，包括方格或並排顯示檢視，hello] 頁面上，每個結果的數目和叫用 [開啟或關閉反白顯示為使用者工作階段之間保存。
* Azure 資料目錄目前已在兩個新的 Azure 區域中提供。 客戶可以佈建 hello Azure 資料目錄中新增 tooEast 美國、 美國西部、 美國西部歐洲和澳洲東部 hello 北歐和東南亞區域中。 如需詳細資訊，請參閱 [Azure 地區](https://azure.microsoft.com/regions/)。

> [!NOTE]
> 「 SQL Server Data Tools 中開啟 」 需要 Visual Studio 2013 Update 4 和 SQL Server 工具 toobe 安裝使用。 tooinstall hello 最新版本的 SQL Server Data Tools，請瀏覽[下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。


## <a name="whats-new-for-december-2015"></a>2015 年 12 月的新功能
自 2015 年 12 月 hello 下列功能已加入 tooAzure 資料目錄：

* 「Azure SQL 資料倉儲」資料來源支援資料設定檔。 註冊 Azure SQL 資料倉儲資料表和檢視表，當使用者可以選擇 tooinclude 資料設定檔的度量資訊與 hello hello 資料來源擷取的中繼資料。
* 支援註冊與探索 MySQL 物件和資料庫。 使用者可以註冊 MySQL 資料來源使用 hello Azure 資料目錄資料來源註冊工具，可以加上註解和探索已註冊的 MySQL 資料來源，使用 hello Azure 資料目錄入口網站。
* 支援針對 Teradata 資料來源進行 SPNEGO 和 Windows 驗證。 當註冊 Teradata 資料表和檢視表，使用者可以選擇使用 SPNEGO 和 Windows 和 LDAP 和 TD2 驗證 tooconnect tooTeradata。
* 支援 Azure Data Lake Store 資料來源。 使用者現在可以使用 Azure 資料目錄來註冊及探索 Azure Data Lake Store 資料來源。
* 手動指定 hello Azure 資料目錄資料的來源註冊工具中的 網路 proxy 設定的支援。 使用者可以從 hello 工具的 歡迎使用頁面上，選取 修改 proxy 設定，而且可以指定 hello proxy 位址和連接埠 toobe hello 工具使用。

## <a name="whats-new-for-november-2015"></a>2015 年 11 月的新功能
自 2015 年 11 月版中，下列功能的 hello 已加入 tooAzure 資料目錄：

* hello 能力 tooview 並複製從 hello Azure 資料目錄入口網站中的連接字串 （包括 Azure SQL Database） 的 SQL Server 和 Oracle 資料來源。 使用者可以按一下 hello for SQL Server 的連接資訊中的檢視 「 連接字串 」 連結，或使用 tooconnect toohello 資料來源 Oracle 資料表、 檢視表或資料庫，toosee hello 連接的字串。 已針對 SQL Server 資料來源提供 ADO.NET、ODBC、OLEDB 及 JDBC 連接字串。 已針對 Oracle 資料來源提供 ODBC 與 OLEDB 連接字串。
* 支援在註冊 Teradata 資料表和檢視時納入資料設定檔。
* 針對 SQL Server (包含 Azure SQL DB 和 Azure SQL 資料倉儲)、SQL Server Analysis Services、Azure 儲存體，以及 HDFS 來源支援「在 Power BI Desktop 中開啟」。  
* 支援針對 Teradata 資料來源進行 LDAP 驗證。 使用者註冊時 Teradata 資料表和檢視表，可以選擇使用 LDAP，tooconnect tooTeradata 和 TD2 驗證。
* 針對 Teradata 資料來源支援「在 Excel 中開啟」。
* Hello Azure 資料目錄入口網站中的最新的搜尋詞彙的支援。 當您搜尋 hello 入口網站中，使用者可以選取從最近使用的搜尋詞彙 tooaccelerate hello 探索體驗。
* 支援預覽 Teradata 資料來源。 當註冊 Teradata 資料表和檢視表，使用者可以選擇 tooinclude 快照集記錄與 hello hello 資料來源擷取的中繼資料。
* 「Azure SQL 資料倉儲」資料來源支援「在 Excel 中開啟」。
* 手動註冊的資料資產支援定義和編輯資料行層級的結構描述。 手動建立之後使用 hello Azure 資料目錄入口網站的資料資產，使用者可以新增 hello 資料資產屬性中的資料行定義。
* 支援 「 沒有 」 查詢搜尋 Azure 資料目錄，tooenable hello 探索的已註冊的資料資產擁有特定的中繼資料時。 Azure 資料目錄查詢語法現在包含下列項目：

| 查詢語法 | 目的 |
| --- | --- |
| `has:previews` |尋找包含預覽的資料資產 |
| `has:documentation` |尋找已提供文件的資料資產 |
| `has:tableDataProfiles` |尋找具有資料表層級之資料設定檔資訊的資料資產 |
| `has:columnsDataProfiles` |尋找具有資料行層級之資料設定檔資訊的資料資產 |


> [!NOTE]
> 「 Power BI Desktop 中開啟 」 需要 hello Power BI Desktop 的應用程式 toobe 安裝目前版本。 如果您遇到問題或錯誤，使用這項功能，確保您擁有 hello 最新版本的 Power BI Desktop 從[PowerBI.com](https://powerbi.com)。


## <a name="whats-new-for-october-2015"></a>2015 年 10 月的新功能
從 2015 年 10 月開始 hello 下列功能已加入 tooAzure 資料目錄：

* 支援已註冊資料來源的資料預覽和資料設定檔的靜止狀態加密。 Azure 資料目錄可以明確地加密任何預覽記錄和資料設定檔與 hello 服務，而不需要目錄系統管理員的金鑰管理已註冊的資料來源。
* 支援 Teradata 資料來源。 使用者現在可以註冊並探索 Teradata 資料表和檢視。
* 支援內部部署 Hive 資料來源。 使用者現可在內部部署資料來源的 Hadoop 中，註冊並探索適用於 Apache Hive 的 Hive 資料表。
* Hello Azure 資料目錄入口網站中的儲存搜尋的支援。 使用者可以儲存的搜尋詞彙和篩選選取項目 tooeasily 重複先前的搜尋，並定義有用的檢視的 hello 類別目錄的內容。 使用者也可以將已儲存的搜尋標示為其預設搜尋。 當使用者按一下 hello 「 放大鏡 」 搜尋圖示從 hello Azure 資料目錄入口網站首頁或從 hello 「 入門 」 頁面時，hello 使用者會從直接 toohello 儲存搜尋加上旗標為預設值。
* 如需註冊的資料資產與 hello Azure 資料目錄入口網站中的容器的 rtf 文字文件的支援。 對於標籤和描述不足的案例，使用者現在可以提供資料資產的文件，例如資料表、檢視和報告，以及提供容器的文件，例如資料庫和模型。
* 支援手動註冊已知的資料來源類型。 使用者可以手動輸入支援的 Azure 資料目錄的所有資料來源類型都使用 hello Azure 資料目錄入口網站的資料來源資訊。
* 支援授權 Azure Active Directory 安全性群組。 目錄系統管理員可以啟用目錄存取 toosecurity 群組，使用者帳戶，讓您更容易 toomanage 存取 tooAzure 資料目錄。
* 在 Excel 中開啟登錄區的資料來源從 hello Azure 資料目錄入口網站的支援。

> [!NOTE]
> Hello 目前版本中，僅 Teradata TD2 支援驗證。 在未來發行的版本中會支援更多驗證機制。

> [!NOTE]
> toouse hello Hive 資料來源的 「 開啟在 Excel 中 」 功能，使用者必須已安裝 hello ODBC 驅動程式的登錄區。

## <a name="whats-new-for-september-2015"></a>2015 年 9 月的新功能
從 2015 年 9 月開始 hello 下列功能已加入 tooAzure 資料目錄：

* 在登錄 Hive 資料來源時納入資料設定檔的支援。
* 支援以程式設計方式探索 hello 目錄 API，讓應用程式使用 Azure 資料目錄的 toointegrate 更容易。
* 新的"getting started"資料來源在 hello Azure 資料目錄入口網站中的探索體驗。 當使用者輸入 hello hello Azure 資料目錄入口網站的 「 探索 」 頁面而不需輸入的搜尋詞彙時，他們會看到 hello 類別目錄的內容包括最常用的 hello 標記、 專家、 資料來源類型，以及物件類型的概觀。
* 支援註冊與探索 Azure SQL 資料倉儲物件和資料庫。 如需 Azure SQL 資料倉儲的詳細資訊，請參閱 [SQL 資料倉儲](https://azure.microsoft.com/services/sql-data-warehouse/)。
* 支援將 SQL Server Analysis Services 模型和 SQL Server Reporting Services 伺服器做為容器來進行註冊與探索。 當註冊 SSAS 和 SSRS 的物件，Azure 資料目錄會建立 hello SSAS 模型和 SSRS 伺服器，以及 hello 報表和其他物件的項目。 hello 容器可探索和註解使用 hello Azure 資料目錄入口網站。 使用者也可以搜尋和篩選模型或伺服器加法 toosearching 和篩選 hello hello 目錄內容中的 hello 內容。
* 支援透過 HTTP/HTTPS 註冊和探索 SQL Server Analysis Servics 物件。 使用者現在可以連接 tooSSAS 伺服器使用的 URL （例如 https://servername/olap/msmdpump.dll)，而不伺服器名稱，並可以在加法 tooWindows 驗證中使用基本驗證和匿名連線。 如需有關 HTTP/HTTPS 連線 tooSSAS 的詳細資訊，請參閱[設定 HTTP 存取 tooAnalysis 服務](https://msdn.microsoft.com/library/gg492140.aspx)。
* 針對 HDInsight 提供 Hive 資料來源支援。 使用者現可在 HDInsight 資料來源的 Hadoop 中，註冊並探索適用於 Apache Hive 的 Hive 資料表。 如需有關在 HDInsight 上的登錄區的詳細資訊，請參閱 hello [HDInsight 文件中心](../hdinsight/hdinsight-use-hive.md)。
* 支援註冊與探索 Oracle 資料庫及 HDFS 叢集以做為容器。 註冊時 Oracle 資料表和檢視表或 HDFS，Azure 資料目錄建立 hello 資料庫、 資料表和檢視的項目。 hello 資料庫可探索和註解使用 hello Azure 資料目錄入口網站。 使用者也可以搜尋和篩選 hello 資料庫的內容，或叢集此外 toosearching 和篩選 hello hello 目錄內容。
* 支援手動註冊未知的資料來源類型。 使用者可以手動輸入使用 hello Azure 資料目錄入口網站中，資料來源資訊，以便未明確支援的 hello 可註解和探索資料來源註冊工具的資料來源。
* 支援註冊與探索 SQL Server 資料庫以做為容器。 當註冊 SQL Server 資料表和檢視表，Azure 資料目錄會建立 hello 資料庫、 資料表和檢視的項目。 hello 資料庫可探索和註解使用 hello Azure 資料目錄入口網站。 使用者也可以搜尋和篩選 hello 的內容加入 toosearching 和篩選 hello hello 目錄內容中的資料庫。

> [!NOTE]
> SSAS 和 SSRS 已註冊的先前 toohello 年 9 月 18 日發行的物件必須重新註冊之前 hello 模型或伺服器中加入項目 toohello 目錄使用 hello 資料來源註冊工具。 重新登錄資料來源不會影響已經由 hello Azure 資料目錄入口網站中的使用者加入任何註解。

> [!NOTE]
> Oracle 資料表和檢視表和 HDFS 檔案和目錄的已註冊的先前 toohello 年 9 月 11 日發行必須重新註冊 hello 資料庫或叢集中的項目加入之前 toohello 目錄使用 hello 資料來源註冊工具。 重新登錄資料來源不會影響已經由 hello Azure 資料目錄入口網站中的使用者加入任何註解。

> [!NOTE]
> SQL Server 資料表與檢視已註冊的先前 toohello 4 年 9 月版本必須重新註冊 hello 資料庫項目加入 toohello 目錄之前，請使用 hello 資料來源註冊工具。 重新登錄資料來源不會影響已經由 hello Azure 資料目錄入口網站中的使用者加入任何註解。

## <a name="whats-new-for-august-2015"></a>2015 年 8 月的新功能
從 2015 年 8 月開始 hello 下列功能已加入 tooAzure 資料目錄：

* 支援 SQL Server 和 Oracle 資料來源的資料分析。 當註冊 SQL Server 和 Oracle 資料表和檢視表，使用者可以選擇 tooinclude hello 物件所註冊的資料設定檔資訊。 hello 資料設定檔包含物件層級和資料行層級統計資料。
* 支援 Hadoop HDFS 資料來源。 使用者現在可以註冊並探索 HDFS 檔案和目錄。
* 支援針對註冊的資料來源提供存取要求資訊。 任何已註冊的資料資產，使用者現在可以提供要求的存取，包括電子郵件連結或 Url 的指示，tooeasily 整合與現有的工具和程序。
* 工具提示標籤和專家，toomake 它更容易 toodiscover 哪些使用者已註冊的資料資產提供哪些中繼資料。
* 我們已加入新 「 使用者 」 按鈕和功能表 tooour 上方導覽列中。 此功能表可讓 hello 使用者看到 hello tooAzure 資料目錄上的帳戶使用 toolog 和 toosign 外的，如有需要。 這個功能表也會顯示 hello 目錄名稱，這是重要的 toodevelopers 使用 hello Azure 資料目錄 REST API。
* 只有 standard Edition： 時新增擁有者 toodata 資產，Azure 資料目錄現在支援使用者帳戶和安全性群組做為擁有者。 tooadd 安全性群組，以選取的資料資產的擁有者，您可以輸入任一 hello 群組的顯示名稱或 hello 群組 UPN 電子郵件地址，如果有的話。
* 支援 Azure Blob 儲存體的資料來源。 使用者現在可以註冊並探索 Azure 儲存體 Blob 和目錄。

