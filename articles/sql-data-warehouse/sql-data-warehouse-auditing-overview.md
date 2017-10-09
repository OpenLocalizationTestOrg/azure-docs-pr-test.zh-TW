---
title: "在 Azure SQL 資料倉儲 aaaAuditing |Microsoft 文件"
description: "開始使用 Azure SQL 資料倉儲中的稽核"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Azure SQL 資料倉儲中的稽核
> [!div class="op_single_selector"]
> * [稽核](sql-data-warehouse-auditing-overview.md)
> * [威脅偵測](sql-data-warehouse-security-threat-detection.md)
> 
> 

SQL 資料倉儲稽核可讓您 toorecord 事件資料庫 tooan 稽核登入您的 Azure 儲存體帳戶中。 稽核可協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。 SQL 資料倉儲稽核也整合了 Microsoft Power BI，具備向下鑽研報告和分析的功能。

稽核工具啟用及促進遵循 toocompliance 標準，但不保證相容性。 如需有關 Azure 程式該支援標準相容性，請參閱 < hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure 信任中心</a>。

* [資料庫稽核基本概念]
* [設定資料庫的稽核]
* [分析稽核記錄和報告]

## <a id="subheading-1"></a>Azure SQL 資料倉儲資料庫稽核基本概念
SQL 資料倉儲資料庫稽核可讓您：

* **保留** 所選事件的稽核記錄。 您可以定義資料庫動作 toobe 稽核的類別。
* **報告** 資料庫活動。 您可以使用預先設定的報表和儀表板 tooget 快速地開始使用活動和事件報告。
* **分析** 報告。 您可以尋找可疑事件、異常活動及趨勢。

您可以設定下列事件類別目錄的 hello 的稽核：

**一般 SQL**和**參數化 SQL**收集的稽核記錄檔分類為哪些 hello  

* **存取 toodata**
* **結構描述變更 (DDL)**
* **資料變更 (DML)**
* **帳戶、角色和權限 (DCL)**
* **預存程序**、**登入**以及**交易管理**。

針對每個事件類別，分別設定**成功**和**失敗**作業的稽核。

如需有關 hello 活動和稽核事件的詳細資訊，請參閱 hello<a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">稽核記錄檔格式參考 （文件檔案下載）</a>。

稽核記錄會儲存在 Azure 儲存體帳戶。 您可以定義稽核記錄保留期間。

可以針對特定資料庫定義稽核原則，或將稽核原則定義為預設伺服器原則。 預設伺服器稽核原則會套用 tooall 資料庫並沒有特定覆寫資料庫稽核原則定義的伺服器上。

在設定稽核之前，請檢查您是否正在使用[「下層用戶端」](sql-data-warehouse-auditing-downlevel-clients.md)。

## <a id="subheading-2"></a>設定資料庫的稽核
1. 啟動 hello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>。
2. 移 toohello**設定**刀鋒視窗中的 hello 想 tooaudit SQL 資料倉儲。 在 hello**設定**刀鋒視窗中，選取**稽核與威脅偵測**。
   
    ![][1]
3. 接下來，啟用 稽核，即可 hello **ON**  按鈕。
   
    ![][3]
4. 在 hello 稽核組態刀鋒視窗中，選取 **儲存詳細資料**tooopen hello 稽核記錄檔儲存體 刀鋒視窗。 選取要儲存記錄檔的 Azure 儲存體帳戶 hello 和 hello 保留期限。 
>[!TIP]
>使用相同的儲存體帳戶的所有稽核的資料庫 tooget hello 充分利用 hello 預先設定的 hello 報告範本。
   
    ![][4]
5. 按一下 hello**確定**按鈕 toosave hello 儲存體的詳細資料設定。
6. 在下**記錄的事件**，按一下 **成功**和**失敗**toolog 所有事件，或選擇個別的事件類別。
7. 如果您要針對資料庫設定稽核，您可能需要您正確地擷取資料稽核的用戶端 tooensure tooalter hello 連接字串。 檢查 hello [hello 連接字串中修改伺服器 FDQN](sql-data-warehouse-auditing-downlevel-clients.md)下層用戶端連線的主題。
8. 按一下 [確定] 。

## <a id="subheading-3"></a>分析稽核記錄和報告
稽核記錄檔彙總集合中的存放區資料表與**SQLDBAuditLogs** hello 您在安裝期間所選擇的 Azure 儲存體帳戶中的前置詞。 您可以使用工具 (例如 <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure 儲存體總管</a>) 來檢視記錄檔。

預先設定的儀表板報表範本可做為<a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">可下載的 Excel 試算表</a>toohelp 您快速地分析記錄資料。 在稽核記錄 toouse hello 範本，您需要 Excel 2013 或更新版本，以及 Power Query，您可以下載<a href="http://www.microsoft.com/download/details.aspx?id=39379">這裡</a>。

hello 範本中，有虛構範例資料，您可以設定 Power Query tooimport 稽核記錄直接從您的 Azure 儲存體帳戶。

## <a id="subheading-4"></a>儲存體金鑰重新產生
實際執行環境，您就有可能您的儲存體金鑰定期的 toorefresh。 當重新整理您的金鑰，您會需要 toosave hello 原則。 hello 程序如下所示：

1. 在 hello 稽核 （上面所述在 hello 稽核 > 一節的安裝程式） 的組態刀鋒視窗中切換 hello**儲存體存取金鑰**從*主要*太*次要*和**儲存**。

   ![][4]
2. 移 toohello 存放裝置設定 刀鋒視窗和**重新產生**hello*主要存取金鑰*。
3. 返回 toohello 稽核組態刀鋒視窗中，交換器 hello**儲存體存取金鑰**從*次要*太*主要*按**儲存**。
4. 返回 toohello 儲存 UI 和**重新產生**hello*次要存取金鑰*（hello 準備為下一個索引鍵重新整理週期。

## <a id="subheading-5"></a>自動化 (PowerShell/REST API)
您也可以設定 Azure SQL 資料倉儲中的稽核使用 hello 遵循自動化工具：

* **PowerShell Cmdlet**：

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[資料庫稽核基本概念]: #subheading-1
[設定資料庫的稽核]: #subheading-2
[分析稽核記錄和報告]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy