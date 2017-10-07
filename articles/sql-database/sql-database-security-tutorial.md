---
title: "aaaSecure Azure SQL 資料庫 |Microsoft 文件"
description: "了解技術和功能 toosecure Azure SQL database。"
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>保護 Azure SQL Database

SQL Database，方法是限制存取 tooyour 資料庫使用的防火牆規則，驗證其身分識別及授權 toodata 透過以角色為基礎的成員資格和權限，以及透過需要使用者 tooprove 的機制保護您的資料資料列層級安全性和動態資料遮罩。

您可以改善 hello 保護您的資料庫在對惡意使用者或未經授權的存取，執行幾個簡單的步驟。 您會在本教學課程中學到： 

> [!div class="checklist"]
> * 設定您伺服器 hello Azure 入口網站中的伺服器層級防火牆規則
> * 使用 SSMS 為資料庫設定資料庫層級的防火牆規則
> * 連接 tooyour 資料庫使用安全的連接字串
> * 管理使用者的存取
> * 使用加密來保護您的資料
> * 啟用 SQL Database 稽核
> * 啟用 SQL Database 威脅偵測

如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。

## <a name="prerequisites"></a>必要條件

toocomplete 此教學課程，請確定您有下列的 hello:

- 已安裝的 hello 最新版本的[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)。 
- 已安裝 Microsoft Excel
- 建立 Azure SQL server 和資料庫-請參閱[hello Azure 入口網站中建立 Azure SQL database](sql-database-get-started-portal.md)，[建立單一的 Azure SQL database，使用 Azure CLI hello](sql-database-get-started-cli.md)，和[建立單一的 Azure SQL資料庫使用 PowerShell](sql-database-get-started-powershell.md)。 

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站

登入 toohello [Azure 入口網站](https://portal.azure.com/)。

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立伺服器層級防火牆規則

Azure 的防火牆會保護 SQL Database。 根據預設，所有連線 toohello 伺服器和 hello 資料庫 hello 伺服器內將會都拒絕從其他 Azure 服務的連接除外。 如需詳細資訊，請參閱 [Azure SQL Database 伺服器層級和資料庫層級防火牆規則](sql-database-firewall-configure.md)

tooset '允許存取 tooAzure services' tooOFF hello 最安全的設定。 如果您需要 tooconnect toohello 資料庫從 Azure VM 或雲端服務，您應該建立[保留 IP](../virtual-network/virtual-networks-reserved-public-ip.md)和僅允許 hello 保留 IP 位址存取透過 hello 防火牆。 

請遵循這些步驟 toocreate [SQL Database 伺服器層級防火牆規則](sql-database-firewall-configure.md)伺服器 tooallow 連線從特定的 IP 位址。 

> [!NOTE]
> 如果您使用其中一個 hello 先前的教學課程或快速入門和都是在 Azure 中建立範例資料庫以 hello 在電腦上執行此教學課程中相同 IP 位址，就在您逐步進行這些教學課程作業時，您可以略過此步驟將有已建立伺服器層級防火牆規則。
>

1. 按一下**SQL 資料庫**hello 左側功能表，然後按一下 hello 資料庫從您想要 tooconfigure hello 上防火牆規則的 hello **SQL 資料庫**頁面。 hello 概觀 頁面的資料庫會開啟，顯示您 hello 完全符合規定的伺服器名稱 (例如**mynewserver 20170313.database.windows.net**)，並提供進一步組態的選項。

      ![伺服器防火牆規則](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. 按一下**設定伺服器防火牆**hello 工具列 hello 如上圖所示。 hello**防火牆設定**hello SQL 資料庫伺服器 頁面隨即開啟。 

3. 按一下**新增用戶端 IP**在 hello 工具列 tooadd hello 公用 IP 位址的 hello 與電腦連接的 toohello 入口網站，或手動輸入 hello 防火牆規則，然後按一下**儲存**。

      ![設定伺服器防火牆規則](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. 按一下**確定**然後按一下hello **X** tooclose hello**防火牆設定**頁面。

您現在可以連接 tooany hello 伺服器資料庫，以指定的 hello IP 位址或 IP 位址範圍。

> [!NOTE]
> SQL Database 會透過連接埠 1433 通訊。 如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。 如果是的話，就能 tooconnect tooyour Azure SQL Database 伺服器除非您的 IT 部門會開啟通訊埠 1433年。
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>使用 SSMS 建立資料庫層級防火牆規則

資料庫層級防火牆規則可讓您將不同的防火牆設定 toocreate hello 相同邏輯伺服器和 toocreate 防火牆規則，具有可攜性-這表示它們遵循下列 hello 資料庫在期間內的不同資料庫的[容錯移轉](sql-database-geo-replication-overview.md)而不是儲存在 hello SQL 伺服器。 資料庫層級防火牆規則只能使用 Transact SQL 陳述式設定，而且只在設定第一個伺服器層級防火牆規則 hello 之後。 如需詳細資訊，請參閱 [Azure SQL Database 伺服器層級和資料庫層級防火牆規則](sql-database-firewall-configure.md)

遵循這些步驟 toocreate 特定資料庫的防火牆規則。

1. 連接 tooyour 資料庫，例如使用[SQL Server Management Studio](./sql-database-connect-query-ssms.md)。

2. 在 [物件總管] 中，以滑鼠右鍵按一下您想要的防火牆規則，以及按一下的 tooadd hello 資料庫**新查詢**。 空白查詢視窗，也就是開啟連接的 tooyour 資料庫。

3. 在 hello 查詢視窗中，修改 hello IP 位址 tooyour 公用 IP 位址，然後執行下列查詢的 hello:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. 在 [hello] 工具列上按一下**Execute** toocreate hello 防火牆規則。

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>檢視應用程式 tooyour tooconnect 資料庫使用安全的連接字串

tooensure 用戶端應用程式與 SQL Database 之間的安全且加密連接，hello 連接字串具有 toobe 設定為：

- 要求加密的連線，並且
- toonot 信任 hello 伺服器憑證。 

這會建立使用傳輸層安全性 (TLS) 的連接，並減少 hello 攻擊的風險，攔截層。 您可以取得正確設定的連接字串 SQL database 支援的用戶端驅動程式從 hello Azure 入口網站如 ado.net 這個螢幕擷取畫面所示。

1. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。

2. 在 hello**概觀**為您的資料庫頁面上，按一下**顯示資料庫的連接字串**。

3. 完成檢閱 hello **ADO.NET**連接字串。

    ![ADO.NET 連接字串](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>建立資料庫使用者

建立任何使用者之前，您必須先選取一個或兩個 Azure SQL Database 支援的驗證類型： 

**SQL 驗證**、 使用使用者名稱和密碼登入和使用者的有效只在 hello 邏輯伺服器內的特定資料庫的內容。 

**Azure Active Directory 驗證**，使用由 Azure Active Directory 管理的身分識別。 

如果您想 toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate 針對 SQL Database，填入的 Azure Active Directory 必須存在後才能繼續。

請遵循這些步驟 toocreate 使用 SQL 驗證使用者：

1. 連接 tooyour 資料庫，例如使用[SQL Server Management Studio](./sql-database-connect-query-ssms.md)使用您的伺服器系統管理員認證。

2. 在物件總管] 中，以滑鼠右鍵按一下您希望 tooadd 新的使用者上，按一下 [hello 資料庫**新查詢**。 空白查詢視窗也就是開啟連接的 toohello 選取的資料庫。

3. 在 hello 查詢視窗中，輸入下列查詢的 hello:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. 在 [hello] 工具列上按一下**Execute** toocreate hello 使用者。

5. 根據預設，hello 使用者可以連接 toohello 資料庫，但沒有權限 tooread 或寫入資料。 toogrant 這些權限 toohello 新建立的使用者，請執行下列兩個新的查詢視窗中命令的 hello

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

它是最佳的作法 toocreate 在 hello 資料庫層級 tooconnect tooyour 這些非系統管理員帳戶資料庫，除非您需要 tooexecute 系統管理員工作，例如建立新的使用者。 請檢閱 hello [Azure Active Directory 教學課程](./sql-database-aad-authentication-configure.md)如何使用 Azure Active Directory tooauthenticate。


## <a name="protect-your-data-with-encryption"></a>使用加密來保護您的資料

Azure SQL Database 透明資料加密 (TDE) 會自動加密而不需要任何變更 toohello 應用程式存取 hello 加密的資料庫的靜止資料。 如果是新建立的資料庫，TDE 預設為開啟。 您的資料庫或已開啟 TDE 的 tooverify tooenable TDE 會執行下列步驟：

1. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 

2. 按一下**透明資料加密**TDE tooopen hello 組態頁面。

    ![透明資料加密](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. 如有必要，設定**資料加密**tooON 按一下**儲存**。

在 hello 背景啟動 hello 加密程序。 您可以監視連線 tooSQL 資料庫使用的 hello 進度[SQL Server Management Studio](./sql-database-connect-query-ssms.md)藉由查詢 sys.dm_database_encryption_keys 資料行 hello hello`sys.dm_database_encryption_keys`檢視。

## <a name="enable-sql-database-auditing-if-necessary"></a>啟用 SQL Database 稽核 (如有必要)

Azure SQL Database 稽核會追蹤資料庫事件，並將它們 tooan 稽核記錄您 Azure 儲存體帳戶中。 稽核可協助您保持法規合規性、了解資料庫活動，以及深入了解可能指出潛在安全違規的不一致和異常。 請遵循這些步驟 toocreate SQL 資料庫的預設稽核原則：

1. 選取**SQL 資料庫**從 hello 左側功能表中，按一下您的資料庫上 hello **SQL 資料庫**頁面。 

2. 在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。 請注意，伺服器層級稽核已停用，而且有**檢視伺服器設定**可讓您 tooview 或修改 hello 伺服器稽核設定從這個內容的連結。

    ![稽核刀鋒視窗](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. 如果您偏好 tooenable 稽核類型 （或位置嗎？） 不同於 hello 所指定的伺服器層級 hello，開啟**ON**稽核，並選擇 hello **Blob**稽核類型。 如果伺服器 Blob 稽核已啟用，就會並存 hello 伺服器 Blob 稽核存在 hello 設定資料庫稽核。

    ![開啟稽核](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. 選取**儲存詳細資料**tooopen hello 稽核記錄檔儲存體 刀鋒視窗。 其中會儲存記錄檔，選取 hello Azure 儲存體帳戶和 hello 保留期限，將會刪除舊的記錄檔之後的 hello，然後按一下**確定**hello 底部。 

   > [!TIP]
   > 使用 hello 相同儲存體帳戶的所有稽核的資料庫 tooget hello 充分利用 hello 稽核報告範本。
   > 

5. 按一下 [儲存] 。

> [!IMPORTANT]
> 如果您想 toocustomize hello 稽核事件，您可以透過 PowerShell 或 REST API-請參閱 hello[自動化 (PowerShell / REST API)](sql-database-auditing.md#subheading-7) > 一節以取得詳細資料。
>

## <a name="enable-sql-database-threat-detection"></a>啟用 SQL Database 威脅偵測

威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。 使用者可以瀏覽 hello 如果會導致從嘗試 tooaccess，漏洞，或利用 hello 資料庫中的資料，請使用 SQL Database 稽核 toodetermine 可疑的事件。 威脅偵測會使簡單 tooaddress 潛在威脅 toohello 資料庫沒有 hello 需要 toobe 安全性專家或管理進階監視系統的安全性。
威脅偵測會偵測異常資料庫活動，指出潛在的 SQL 插入式攻擊。 SQL 資料隱碼是 hello 常見的 Web 應用程式的安全性問題在 hello 網際網路，使用的 tooattack 資料導向應用程式。 攻擊者利用的應用程式的弱點可能會 tooinject 惡意的 SQL 陳述式到違反或修改 hello 資料庫中的資料的應用程式項目欄位。

1. 瀏覽 toohello 組態刀鋒視窗中的 hello 想 toomonitor 的 SQL 資料庫。 在 hello 設定刀鋒視窗中，選取 **稽核與威脅偵測**。

    ![瀏覽窗格](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. 在 hello**稽核與威脅偵測**組態刀鋒視窗中開啟**ON**稽核，這會顯示 hello 威脅偵測設定。

3. [開啟] 威脅偵測。

4. 設定將會收到偵測的異常資料庫活動時的安全性警示的電子郵件的 hello 清單。

5. 按一下**儲存**在 hello**稽核與威脅偵測**刀鋒視窗 toosave hello 新的或更新稽核和威脅偵測原則。

    ![瀏覽窗格](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    如果偵測到異常的資料庫活動，您會在一偵測到異常的資料庫活動時，就收到電子郵件通知。 hello 電子郵件會提供資訊，包括 hello 性質 hello 異常活動、 資料庫名稱、 伺服器名稱和 hello 事件時間的 hello 可疑安全性事件。 此外，它會提供資訊的可能原因和建議動作 tooinvestigate 並減輕潛在威脅 toohello 資料庫 hello。 您應透過何種 toodo 您 hello 下一個步驟查核行程收到這類電子郵件：

    ![威脅偵測電子郵件](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. 在 hello 電子郵件，按一下 hello **Azure SQL 稽核記錄檔**連結，也會啟動 hello Azure 入口網站，並顯示 hello 相關稽核的記錄周圍 hello hello 可疑事件時間。

    ![稽核記錄](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. 按一下 hello 稽核記錄 tooview hello 可疑的資料庫活動，例如 SQL 陳述式的詳細失敗的原因與用戶端 IP。

    ![記錄詳細資料](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. 在 hello 稽核記錄刀鋒視窗中，按一下 **在 Excel 中開啟**tooopen 預先設定的 excel 範本 tooimport 和 hello 周圍 hello 事件時間的 hello 可疑的稽核記錄檔執行深入分析。

    > [!NOTE]
    > 在 Excel 2010 或更新版本的 Power Query 和 hello**快速合併**是必要設定。

    ![在 Excel 中開啟記錄](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. tooconfigure hello**快速合併**設定位在 hello **POWER QUERY**功能區索引標籤上，選取**選項**toodisplay hello 選項 對話方塊。 選取 hello 隱私權區段，然後選擇 hello 第二個選項-[忽略 hello 隱私權等級並可能會改善效能]:

    ![Excel 快速合併](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. tooload SQL 稽核記錄檔，請務必 hello 設定 索引標籤中的 hello 參數正確設定，然後選取 hello 「 資料 」 功能區按一下 hello 全部重新整理 按鈕。

    ![Excel 參數](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. hello 結果會出現在 hello **SQL 稽核記錄檔**可讓您的 hello 異常活動偵測到，並減少應用程式中的 hello 安全性事件 hello 影響 toorun 深入分析的工作表。


## <a name="next-steps"></a>後續步驟
您可以改善 hello 保護您的資料庫在對惡意使用者或未經授權的存取，執行幾個簡單的步驟。 您會在本教學課程中學到： 

> [!div class="checklist"]
> * 設定伺服器和/或資料庫的防火牆規則
> * 連接 tooyour 資料庫使用安全的連接字串
> * 管理使用者的存取
> * 使用加密來保護您的資料
> * 啟用 SQL Database 稽核
> * 啟用 SQL Database 威脅偵測

> [!div class="nextstepaction"]
>[改善 SQL Database 效能](sql-database-performance-tutorial.md)

