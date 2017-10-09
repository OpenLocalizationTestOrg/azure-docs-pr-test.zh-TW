---
title: "Azure SQL database 稽核入門 aaaGet |Microsoft 文件"
description: "開始使用 Azure SQL 資料庫稽核"
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>開始使用 SQL Database 稽核
Azure SQL database 稽核會追蹤資料庫事件，並將它們 tooan 稽核記錄您 Azure 儲存體帳戶中。 稽核也具備下列功能：

* 協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。

* 啟用，並有助於遵循 toocompliance 標準，雖然它不能保證相容性。 如需有關 Azure 程式該支援標準相容性，請參閱 < hello [Azure 信任中心](https://azure.microsoft.com/support/trust-center/compliance/)。


## <a id="subheading-1"></a>Azure SQL 資料庫稽核概觀
您可以使用 SQL 資料庫稽核完成下列工作：


* **保留** 所選事件的稽核記錄。 您可以定義資料庫動作 toobe 稽核的類別。
* **報告** 資料庫活動。 您可以使用預先設定的報表和儀表板 tooget 快速地開始使用活動和事件報告。
* **分析** 報告。 您可以尋找可疑事件、異常活動及趨勢。

您可以設定不同類型的事件類別目錄中，稽核 hello 中所述[為您的資料庫設定稽核](#subheading-2)> 一節。

稽核記錄檔會寫入 tooAzure Blob 儲存體，在您的 Azure 訂用帳戶。


## <a id="subheading-8"></a>定義伺服器層級與資料庫層級的稽核原則

您可以針對特定資料庫定義稽核原則，或將稽核原則定義為預設伺服器原則：

* 伺服器原則 hello 伺服器上，套用 tooall 現有和新建立的資料庫。

* 如果*server blob 稽核已啟用*，它*一律套用 toohello 資料庫*（也就是 hello 資料庫會稽核），不論 hello 資料庫稽核設定。

* 啟用稽核 hello 在資料庫上，在加法 tooenabling 它 hello 伺服器上的 blob 將*不*覆寫或變更的任何 hello hello server blob 稽核設定。 這兩種稽核將會並存。 換句話說，hello 資料庫將稽核兩次以平行方式 （一次由 hello 伺服器原則和一次程式 hello 資料庫原則）。

   > [!NOTE]
   > 您應該避免同時啟用伺服器 Blob 稽核與資料庫 Blob 稽核，除非：
    > * 您想要不同的 toouse*儲存體帳戶*或*保留期限*特定資料庫。
    > * 您想要 tooaudit 事件類型或分類的不同事件類型的特定資料庫或稽核 hello 伺服器上的資料庫 hello hello 其餘的類別。 例如，您可能需要稽核 toobe 只針對特定資料庫的資料表插入。
   > 
   > 否則，我們建議您啟用只有伺服器層級 blob 稽核和保持 hello 資料庫層級的稽核所有資料庫停都用。


## <a id="subheading-2"></a>設定資料庫的稽核
hello 下一節描述 hello 的稽核，以使用 hello Azure 入口網站的組態。

1. 移 toohello [Azure 入口網站](https://portal.azure.com)。
2. 移 toohello**設定**刀鋒視窗中的 hello 想 tooaudit SQL 資料庫/SQL server。 在 hello**設定**刀鋒視窗中，選取**稽核與威脅偵測**。

    <a id="auditing-screenshot"></a> ![導覽窗格][1]
3. 如果您偏好 tooset 註冊的伺服器稽核原則 （將此伺服器套用 tooall 現有和新建立的資料庫），您可以選取 hello**檢視伺服器設定**hello 資料庫稽核刀鋒視窗中的連結。 您可以接著檢視或修改 hello 伺服器稽核設定。

    ![瀏覽窗格][2]
4. 如果您想 tooenable hello 資料庫層級 （加法 tooor 而不是伺服器層級的稽核)，稽核 blob**稽核**，選取**ON**，以及**稽核類型**選取**Blob**。

    如果伺服器 blob 稽核已啟用，就會並存 hello 伺服器 blob 稽核存在 hello 資料庫設定稽核。  

    ![瀏覽窗格][3]
5. tooopen hello**稽核記錄檔儲存體**刀鋒視窗中，選取**儲存詳細資料**。 選取記錄檔將儲存的位置，，然後選取 hello 保留期限，將會刪除舊的記錄檔之後的 hello hello Azure 儲存體帳戶。 然後按一下 [確定] 。 
   >[!TIP] 
   >充分利用 hello 的稽核報表範本，而使用 tooget hello hello 所有稽核資料庫的相同儲存體的帳戶。 

    <a id="storage-screenshot"></a> ![導覽窗格][4]
6. 如果您想 toocustomize hello 稽核事件，您可以透過 PowerShell 執行這項操作，或 hello REST API。 如需詳細資訊，請參閱 hello[自動化 (PowerShell/REST API)](#subheading-7) > 一節。
7. 設定您的稽核設定之後，您可以開啟 hello 新威脅偵測功能，並設定電子郵件 tooreceive 安全性警示。 使用威脅偵測時，您會接收與指示潛在安全性威脅的異常資料庫活動相關的主動式警示。 如需詳細資訊，請參閱[開始使用威脅偵測](sql-database-threat-detection-get-started.md)。
8. 按一下 [儲存] 。





## <a id="subheading-3"></a>分析稽核記錄和報告
稽核記錄檔會彙總 hello 您在安裝期間所選擇的 Azure 儲存體帳戶中。 您可以使用工具 (例如 [Azure 儲存體總管](http://storageexplorer.com/)) 來查看稽核記錄。

Blob 稽核記錄是以 Blob 檔案集合的方式儲存在名為 **sqldbauditlogs** 的容器內。

如需 hello 階層 hello blob 稽核記錄檔儲存體資料夾及 blob 的命名慣例，記錄檔格式的進一步詳細資訊，請參閱 hello [Blob 稽核記錄檔格式參考 （.docx 檔案下載）](https://go.microsoft.com/fwlink/?linkid=829599)。

有數種方法，您可以使用稽核記錄的 tooview blob:

* 使用 hello [Azure 入口網站](https://portal.azure.com)。  開啟 hello 相關資料庫。 在 hello 頂端 hello 資料庫**稽核與威脅偵測**刀鋒視窗中，按一下 **檢視稽核記錄檔**。

    ![瀏覽窗格][7]

    **稽核記錄**刀鋒視窗隨即開啟，從中您應該能夠 tooview hello 記錄檔。

    - 按一下即可檢視特定日期**篩選**頂端的 hello hello**稽核記錄**刀鋒視窗。
    - 您可以在由伺服器原則或資料庫原則稽核建立的稽核記錄之間切換。

       ![瀏覽窗格][8]

* 使用 hello 系統函數**sys.fn_get_audit_file** (T-SQL) tooreturn hello 稽核記錄檔中的資料表格格式。 如需有關如何使用這個函式的詳細資訊，請參閱 hello [sys.fn_get_audit_file 文件](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)。


* 使用 SQL Server Management Studio (SSMS 17 或更新版本) 中的 [合併稽核檔案]：  
    1. 從 hello SSMS 功能表上，選取**檔案** > **開啟** > **合併稽核檔案**。

        ![瀏覽窗格][9]
    2. hello**加入稽核檔案**對話方塊隨即開啟。 選取其中一個 hello**新增**選項可以選擇是否 toomerge 稽核檔案從本機磁碟，或從 Azure 儲存體匯入 (您將需要的 tooprovide，您的 Azure 儲存體的詳細資訊和帳戶金鑰)。

    3. 已新增所有的檔案 toomerge 之後，請按一下**確定**toocomplete hello 合併作業。

    4. 在 SSMS 中，您可以在其中檢視和分析，以及匯出它 tooan XEL 或 CSV 檔案或 tooa 資料表中，開啟 hello 合併的檔案。

* 使用 hello[同步應用程式](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration)，我們建立了。 它會在 Azure 中執行，並且利用到 OMS 的 Operations Management Suite (OMS) 的記錄分析公用 Api toopush SQL 稽核記錄檔。 hello 同步處理應用程式將發送 SQL 稽核記錄檔至 OMS 記錄分析取用透過 hello OMS 記錄分析儀表板。 

* 使用 Power BI。 您可以在 Power BI 中檢視和分析稽核記錄資料。 深入了解 [Power BI，並存取可下載的範本](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/)。

* 下載記錄檔從您的 Azure 儲存體 blob 容器透過 hello 入口網站，或使用一種工具，像是[Azure 儲存體總管](http://storageexplorer.com/)。
    * 您已下載記錄檔在本機上之後，您可以按兩下 hello 檔案 tooopen，檢視及分析在 SSMS 中的 hello 記錄檔。
    * 您也可以透過 Azure 儲存體總管同時下載多個檔案。 以滑鼠右鍵按一下特定的子資料夾 （例如，子資料夾中包含特定日期的所有記錄檔），然後選取**存**toosave 本機資料夾中的。

* 其他方法：
   * 下載多個檔案 （或子資料夾，以記錄檔包含一整天，這份清單中的 hello 上一個項目中所述） 之後, 您可以合併它們在本機中稍早所述的 hello SSMS 合併稽核檔案指示所述。

   * 以程式設計方式檢視 Blob 稽核記錄：

     * 使用 hello[擴充事件讀取器](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/)C# 程式庫。
     * 使用 PowerShell [查詢擴充事件檔案](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/)。




## <a id="subheading-5"></a>實際作法
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">稽核異地複寫資料庫</a>
當您使用地理複寫的資料庫時，很可能 tooset 向上 hello 主要資料庫、 hello 次要資料庫，或兩者，根據 hello 稽核類型上的稽核。

請遵循這些指示 （請記住，blob 稽核可以開啟或關閉只能從 hello 主要資料庫稽核設定）：

* **主要資料庫**。 開啟 blob 稽核 hello 伺服器上或在 hello 資料庫本身，hello 中所述[為您的資料庫設定稽核](#subheading-2)> 一節。
* **次要資料庫**。 Blob 上開啟稽核 hello 主要資料庫，hello 中所述[為您的資料庫設定稽核](#subheading-2)> 一節。 
   * Blob 稽核上必須啟用 hello*主要資料庫本身*，非 hello 伺服器。
   * Blob 稽核 hello 主要資料庫上啟用之後，它也會變成 hello 次要資料庫上啟用。

     >[!IMPORTANT]
     >根據預設，hello 儲存體 hello 次要資料庫會設定相同的 hello 主要資料庫，toothose 導致跨地區的流量。 您可以避免這個狀況啟用稽核 hello 次要伺服器上的 blob 和 hello 次要伺服器儲存體設定中設定本機儲存體。 這會覆寫 hello hello 次要資料庫並儲存其稽核記錄檔 toolocal 儲存體的每個資料庫中的結果的儲存位置。  
<br>

### <a id="subheading-6">儲存體金鑰重新產生</a>
實際執行環境，您就有可能您的儲存體金鑰定期的 toorefresh。 當重新整理您的金鑰，您會需要 tooresave hello 稽核原則。 hello 程序如下所示：

1. 開啟 hello**儲存詳細資料**刀鋒視窗。 在 hello**儲存體存取金鑰**方塊中，選取**次要**，然後按一下**確定**。 然後按一下 **儲存**在 hello hello 稽核組態刀鋒視窗最上方。

    ![瀏覽窗格][5]
2. 請 toohello 存放裝置設定 刀鋒視窗，並重新產生 hello 主要存取金鑰。

    ![瀏覽窗格][6]
3. 返回 toohello 稽核組態刀鋒視窗中，切換 hello 儲存體存取金鑰，從次要 tooprimary，，然後按一下**確定**。 然後按一下 **儲存**在 hello hello 稽核組態刀鋒視窗最上方。
4. 返回 toohello 儲存體組態刀鋒視窗，然後重新產生 hello 次要存取金鑰 （在準備 hello 下一個索引鍵的重新整理循環）。

## <a id="subheading-7"></a>自動化 (PowerShell/REST API)
您也可以設定稽核 Azure SQL Database 中使用下列的自動化工具 hello:

* **PowerShell Cmdlet**：

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

   如需指令碼範例，請參閱[使用 PowerShell 設定稽核與威脅偵測](scripts/sql-database-auditing-and-threat-detection-powershell.md)。

* **REST API - Blob 稽核**：

   * [建立或更新資料庫 Blob 稽核原則](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [建立或更新伺服器 Blob 稽核原則](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [取得資料庫 Blob 稽核原則](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [取得伺服器 Blob 稽核原則](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [取得伺服器 Blob 稽核操作結果](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
