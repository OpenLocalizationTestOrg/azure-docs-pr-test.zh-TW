---
title: "aaaDiscover，辨識，並在 Microsoft Azure 中的個人資料分類 |Microsoft 文件"
description: "深入了解搜尋、分類、探索及識別資料"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>在 Microsoft Azure 中探索、識別並分類個人資料

本文提供指引 toodiscover，識別、 和分類在數個 Azure 工具和服務，包括使用的 Azure HDInsight，Azure 中的 Hadoop 叢集的 Azure 資料目錄、 Azure Active Directory、 SQL 資料庫、 Power Query 中的個人資料的方式資訊保護，Azure 搜尋中，與 SQL Azure Cosmos DB 查詢。

## <a name="scenario-problem-statement-and-goal"></a>情節、問題陳述和目標

美國的運動公司會收集各種個人和其他資料。 這包括客戶和員工資料。 hello 公司保存在多個資料庫，並將它儲存在 Azure 環境中的數個不同位置。 此外 tooselling 運動設備，它們也裝載和管理註冊的 hello world，包括在 hello EU，周圍精銳運動事件並在某些情況下 hello 它們所收集的客戶資料包含醫療資訊。

由於 hello 公司裝載許多國際 bicycling tours and techniques 每年，約聘人員中有 hello 全球各地，幾個 hello 資料集就相當大。 hello 公司也有可供客戶與員工的開發人員建置應用程式。

hello 公司希望有 tooaddress hello 下列問題：

- 客戶和員工的個人資料必須與 hello 分類/區別其他資料 hello 公司會收集在順序 tooensure 適當的存取和安全性。
- hello 資料系統管理員必須 tooeasily 探索跨不同區域的 hello Azure 環境的 hello 客戶的個人資料的位置。
- 客戶和員工個人資料會出現在共用文件和電子郵件通訊必須標示為 toohelp 確保它保持安全。
- hello 公司的應用程式開發人員需要在 web 和行動裝置應用程式的客戶和員工個人資料的方式 tooeasily 搜尋。
- 開發人員也需要 tooquery 其文件資料庫的個人資料。

### <a name="company-goals"></a>公司目標

- 所有客戶和員工的個人資料必須都已在 Azure 資料目錄中加以標記/標註，以便能夠輕鬆地找到。 在理想情況下，客戶和員工的個人資料會分開標記/標註。
- 必須能夠輕鬆地從位於 Azure Active Directory 中的客戶和員工使用者設定檔和工作資訊找到個人資料。
- 必須能夠輕鬆地查詢位在多個 SQL Database 中的個人資料。 
- 某些 hello 公司的大型資料集是透過 Azure HDInsight 並儲存在 Hadoop。 必須將這些資料集匯入 Excel 中，以便可以查詢個人資料。
- 在文件及電子郵件通訊中共用的個人資料必須加以分類、標記，並使用 Azure 資訊保護來保持安全。
- hello 公司的應用程式開發人員必須要能夠 toodiscover 客戶和員工個人資料 hello 的應用程式建立了它們，它們可以使用 Azure 搜尋作業中。
- 開發人員必須要能夠 toofind 其文件資料庫中的個人資料。

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory：資料探索

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。 客戶和員工的使用者設定檔和包含個人資料中的使用者工作資訊，可以找出您[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) 環境使用 hello [Azure 入口網站](https://portal.azure.com/)。

如果您想 toofind 或變更特定使用者的個人資料，這會特別有用。 您也可以新增或變更使用者設定檔及工作資訊。 您必須使用屬於 hello 目錄全域管理員帳戶登入。

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>如何找出或檢視使用者設定檔和工作資訊？

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。

2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

   ![如何找出使用者設定檔和工作資訊](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. 在 hello**使用者和群組**刀鋒視窗中，選取**使用者**。

  ![開啟使用者和群組](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. 在 [hello**使用者和群組的使用者**刀鋒視窗中，從 [hello] 清單中，選取使用者，然後用 hello 選使用者的 hello] 刀鋒視窗，選取**設定檔**tooview 可能包含個人資料的使用者設定檔資訊.

  ![選取使用者](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. 如果您需要 tooadd 或變更使用者設定檔資訊時，您可以這樣做，然後 hello 命令列中，選取 **儲存。**
6. 在 hello 選使用者的 hello 刀鋒視窗，選取 **工作資訊**tooview 使用者工作的資訊可能包含個人資料。

 ![檢視工作資訊](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. 如果您需要 tooadd 或變更使用者的工作資訊時，您可以這樣做，然後 hello 命令列中，選取 **儲存。**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database：資料探索

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 是雲端資料庫，可協助開發人員建置及維護應用程式。 您可以使用標準 SQL 查詢在 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 中找到個人資料。 Azure SQL 彈性查詢 （預覽） 可讓使用者 tooperform 跨資料庫查詢。

詳細[SQL database](../sql-database/sql-database-technical-overview.md)教學課程會說明許多層面使用 SQL 資料庫，包括如何 toobuild 一個以及 toorun 資料查詢。 hello 以下是可用 hello 連結 toospecific 章節的教學課程中的 hello 資訊的摘要。

### <a name="how-do-i-build-a-sql-database"></a>如何建置 SQL Database？

有三種方式 toodo 它：

- Azure SQL database 可由 hello [Azure 入口網站](https://portal.azure.com/)。 在 hello 教學課程中，您將使用一組特定的資源群組和邏輯伺服器內的運算和存放裝置資源。 您會使用名為 AdventureWorks 的虛構公司之範例資料。 您還會建立伺服器層級防火牆規則。 toolearn 如何 toodo 這個，請瀏覽 hello [hello Azure 入口網站中建立 Azure SQL database](../sql-database/sql-database-get-started-portal.md)教學課程。

  ![建立 Azure SQL Database](media/how-to-discover-classify-personal-data-azure/create-database.png)
- SQL database 也可以建立在 hello [Azure 雲端殼層](https://azure.microsoft.com/features/cloud-shell/)CLI，瀏覽器為基礎的命令列工具。 hello 工具使用 hello Azure 入口網站中，可以直接從該處執行。 本教學課程中，在您啟動 hello 工具、 定義指令碼變數建立資源群組和邏輯伺服器，並設定伺服器防火牆規則。 然後使用範例資料建立資料庫。 toolearn 如何 toocreate 資料庫如此一來，請瀏覽 hello[建立單一的 Azure SQL database，使用 Azure CLI hello](../sql-database/sql-database-get-started-cli.md)教學課程。

  ![CLI 教學課程](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Linux 系統管理員和開發人員通常都是使用 Azure CLI。 某些使用者認為它比 PowerShell (這是您的第三個選項) 更簡單且更直覺。

- 最後，您可以建立 SQL 資料庫使用 PowerShell，也就是命令/指令碼使用的工具 toocreate 及管理 Azure 及其他資源。 本教學課程中，在您啟動 hello 工具、 定義指令碼變數建立資源群組和邏輯伺服器，並設定伺服器防火牆規則。 然後使用範例資料建立資料庫。

hello 教學課程需要 hello Azure PowerShell 模組版本 4.0 或更新版本。 執行 Get-module-ListAvailable AzureRM toofind 您的版本。 如果您需要 tooinstall 或升級，請參閱安裝 Azure PowerShell 模組。

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn 如何 toocreate 資料庫如此一來，請瀏覽 hello[建立單一的 Azure SQL database，使用 Powershell](../sql-database/sql-database-get-started-powershell.md)教學課程。

>[!Note]
Windows 系統管理員通常 toouse PowerShell 中，但其中部分偏好 Azure CLI。

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>我該如何搜尋 hello Azure 入口網站中的 SQL database 中的個人資料？ * *

您可以使用內部 hello Azure 入口網站 toosearch hello 內建查詢編輯器 」 工具的個人資料。 將登入使用您的 SQL server 系統管理員登入和密碼，toohello 工具，並接著輸入查詢。

  ![搜尋使用 hello 入口網站的 sql](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Hello 教學課程的步驟 5 hello 查詢編輯器 窗格中顯示的範例查詢，但它不會著重於個人或機密資訊 （它也會結合兩個資料表的資料，並建立 hello 來源資料行的別名 hello 資料集中所傳回）。 hello 下列螢幕擷取畫面顯示 hello 查詢從步驟 5 和 hello 傳回的結果窗格：

  ![查詢編輯器](media/how-to-discover-classify-personal-data-azure/query-editor.png)

如果您的資料庫稱為 MyTable，個人資訊的範例查詢可能就會包括名稱、社會安全號碼和識別碼，且會看起來像這樣：

「選取名稱、社會安全號碼、MyTable 的識別碼」

您會執行 hello 查詢，並接著看到 hello 導致 hello**結果**窗格。

如需有關如何 tooquery SQL 資料庫 hello Azure 入口網站中的詳細資訊，請瀏覽 hello[查詢 hello SQL database](../sql-database/sql-database-get-started-portal.md) hello 教學課程 > 一節。

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>如何跨多個資料庫搜尋資料？

SQL 彈性查詢 （預覽） 可讓您 tooperform 跨資料庫和多個資料庫查詢，並傳回單一結果。 hello[教學課程概觀](../sql-database/sql-database-elastic-query-overview.md)包含案例詳細的描述，並說明 hello 差異垂直和水平的資料庫分割。 水平資料分割稱為「分區化」。

  ![垂直資料分割](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![水平資料分割](media/how-to-discover-classify-personal-data-azure/horizontal.png)

tooget 啟動，請瀏覽 hello [Azure SQL Database 彈性的查詢概觀 （預覽）](../sql-database/sql-database-elastic-query-overview.md)頁面。

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (適用於匯入 Azure HDInsight Hadoop 叢集)：大型資料集的資料探索

Hadoop 是開放原始碼 Apache 儲存體和大型資料集的處理服務，會在 Hadoop 叢集中進行分析並加以儲存。 [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/)可讓在 Azure 中的使用者 toowork 的 Hadoop 叢集。 Power Query 是 Excel 增益集，除此之外，還可協助使用者從不同的來源探索資料。

在 Azure HDInsight Hadoop 叢集相關聯的個人資料可以匯入的 tooExcel 有了 Power Query。 一旦 hello 資料位於 Excel 內，您就可以使用查詢 tooidentify 它。

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>如何使用 Excel 的 Power Query tooimport Hadoop 叢集在 Azure HDInsight 到 Excel？

HDInsight 教學課程將引導您完成這整個程序。 它說明必要條件，並包含連結 tooa[開始使用 Azure HDInsight](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md)教學課程。 指示涵蓋 Excel 2016 2013年和 2010年 （步驟都稍有不同 Excel hello 較舊版本）。 如果您沒有 hello Excel Power Query 增益集，hello 教學課程將告訴您如何 tooget 它。 您會在 Excel 中啟動 hello 教學課程，而且必須的 toohave 與叢集相關聯的 Azure Blob 儲存體帳戶。

  ![在 Excel 中的查詢](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn 如何 toodo 這個，請瀏覽 hello[使用 Power Query 連接的 Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)教學課程。

來源：[使用 Power Query 連接 Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure 資訊保護：文件和電子郵件的個人資料分類

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection)可協助 Azure 客戶套用標籤 tooclassify 及保護內部或外部共用的文件與電子郵件通訊。 這些項目有些可能會包含客戶或員工的個人資訊。 系統管理員或使用者可以自動或手動方式定義規則和條件。 例如，如果使用者儲存文件，其中包含信用卡資訊，請他或她會看到由 hello 管理員設定的標籤建議。

### <a name="how-do-i-try-it"></a>如何嘗試？

如果您想要 Azure Information Protection 再試一次 toosee toogive，如果它可能是適合您的組織，請瀏覽 hello[快速入門教學課程](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial)。 它會引導您執行五個基本步驟，從安裝 tooconfiguring 原則 tooseeing 分類、 標記和動作中的共用 — 和花費時間不超過一小時。

### <a name="how-do-i-deploy-it"></a>如何進行部署？

如果您想為您的組織要 toodeploy Azure Information Protection，請瀏覽 hello[分類、 標記和保護的部署藍圖](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap)。

### <a name="is-there-anything-else-i-should-know"></a>還有其他須知事項嗎？

如互補的資訊可協助您思考如何 tooset 它，請瀏覽 hello[就緒、 設定、 保護 ！](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
部落格文章。 並核取 hello 了更多如需有關 Azure Information Protection 下面所列的連結。

## <a name="azure-search-data-discovery-for-developer-apps"></a>Azure 搜尋服務：開發人員應用程式的資料探索

[Azure 搜尋服務](https://azure.microsoft.com/services/search/)是開發人員的雲端搜尋解決方案，可為您的應用程式提供豐富的資料搜尋體驗。 Azure 搜尋可讓您 toolocate 資料到使用者定義的索引，源自 Azure Cosmo DB、 Azure SQL Database、 Azure Blob 儲存體、 Azure 資料表儲存體或自訂客戶 JSON 資料。 您也可以建構的個人資料類型或 hello 的特定人員的個人資料使用 hello Azure 搜尋 REST API toosearch Lucene 查詢。 功能包括全文檢索搜尋、簡單查詢語法及 Lucene 查詢語法。 

## <a name="how-do-i-use-sql-tooquery-data"></a>如何使用 SQL tooquery 資料？

toobegin 與 hello 基本概念，請瀏覽 hello [Azure CosmosD DB： 如何使用 SQL tooquery](../cosmos-db/tutorial-query-documentdb.md)教學課程。 hello 教學課程提供範例文件和兩個範例 SQL 查詢和結果。

如需有關建置 SQL 查詢的詳細指引，請瀏覽 [Azure Cosmos DB 文件 DB API 的 SQL 查詢。](../cosmos-db/documentdb-sql-query.md)

如果您使用新 tooAzure Cosmos DB，就像 toolearn 方式 toocreate 資料庫中，新增集合，以及加入資料，請瀏覽 hello [Azure Cosmos DB： 建置 DocumentDB API 的 web 應用程式](../cosmos-db/create-documentdb-dotnet.md)快速入門教學課程。 如果您想要 toodo 這.NET、 Java 或 Python，例如以外的語言只要選擇您慣用的語言後您 toohello 站台。

## <a name="next-steps"></a>後續步驟

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50)

[什麼是 SQL Database？](../sql-database/sql-database-technical-overview.md)

[Azure 入口網站中可用的 SQL Database 查詢編輯器] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[什麼是 Azure 資訊保護？](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[什麼是 Azure Rights Management？](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure 資訊保護：就緒、設定、保護！](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
