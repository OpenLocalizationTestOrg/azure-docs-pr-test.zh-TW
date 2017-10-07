---
title: "aaaMigrate SQL 資料庫的 SQL Server DB tooAzure |Microsoft 文件"
description: "了解 toomigrate 您 SQL Server 資料庫 tooAzure SQL 資料庫。"
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>移轉您的 SQL Server 資料庫 tooAzure SQL 資料庫

移動您的 SQL Server 資料庫 tooAzure SQL Database 是程序包含三個部分-先準備，然後匯出，然後匯入 hello 資料庫。 您會在本教學課程中學到：

> [!div class="checklist"]
> * 準備移轉 tooAzure SQL 資料庫的 SQL Server 中的資料庫使用 hello[資料移轉小幫手](https://www.microsoft.com/download/details.aspx?id=53595)(DMA)
> * Hello 資料庫 tooa BACPAC 檔案匯出
> * Hello BACPAC 檔案匯入到 Azure SQL Database

如果您沒有 Azure 訂用帳戶，請在開始之前先[建立免費帳戶](https://azure.microsoft.com/free/)。

## <a name="prerequisites"></a>必要條件

toocomplete 完成本教學課程，請確定 hello 下列必要條件：

- 已安裝的 hello 最新版本的[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS)。 安裝 SSMS 也會安裝 hello SQLPackage，可以是使用的 tooautomate 範圍內的資料庫開發工作的命令列公用程式最新版本。 
- 已安裝的 hello[資料移轉小幫手](https://www.microsoft.com/download/details.aspx?id=53595)(DMA)。
- 您已識別，且有存取 tooa 資料庫 toomigrate。 本教學課程使用 hello [SQL Server 2008 r2 AdventureWorks OLTP 資料庫](https://msftdbprodsamples.codeplex.com/releases/view/59211)的 SQL Server 2008 r2 或更新版本中，執行個體上，但您可以使用您選擇的任何資料庫。 toofix 相容性問題，使用[SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>為移轉做準備

您已準備好 tooprepare 進行移轉。 請遵循這些步驟 toouse hello **[資料移轉小幫手](https://www.microsoft.com/download/details.aspx?id=53595)** tooassess hello 整備向您的資料庫移轉 tooAzure SQL 資料庫。

1. 開啟 hello**資料移轉小幫手**。 您計劃 toomigrate，，您不需要 tooinstall 它 hello 電腦主控上 hello SQL Server 執行個體，您可以執行 DMA 連線 toohello SQL Server 執行個體包含 hello 資料庫的任何電腦上。

     ![開啟 data migration assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Hello 左側功能表中，按一下**+ 新增**toocreate**評估**專案。 填寫表單 hello**專案名稱**（所有其他值應該留在其預設值），按一下 **建立**。 hello**選項**頁面隨即開啟。

     ![新 data migration assistant 專案](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. 在 hello**選項**頁面上，按一下**下一步**。 hello**選取來源**頁面隨即開啟。

     ![新資料移轉選項](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. 在 hello**選取來源**頁面上，輸入 hello 包含您計劃 toomigrate hello 伺服器的 SQL Server 執行個體名稱。 如有必要，變更 hello 這個頁面上的其他值。 按一下 [ **連接**]。

     ![新資料移轉選取來源](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. 在 hello**加入來源**hello 部分**選取來源**頁面上，選取測試的相容性的 hello 資料庫 toobe hello 核取方塊。 按一下 [新增] 。

     ![新資料移轉選取來源](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. 按一下 [開始評估]。

     ![新資料移轉開始評估](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Hello 評估完成時，先在 hello 資料庫是否完全相容 toomigrate 尋找 toosee。 尋找 hello 核取記號的綠色圓圈。

     ![新資料移轉評估結果相容](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. 檢閱 hello 結果。 hello **SQL Server 功能同位檢查**結果所示為 hello 預設結果 tooreview。 特別是檢閱 hello 不支援和部分支援功能的資訊和建議的動作的 hello 提供資訊。 

     ![新資料移轉評估同位檢查](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. 檢閱 hello**相容性問題**按一下該選項在 hello 左上方。 特別是檢閱 hello 移轉封鎖器，行為變更的相關資訊，並已被取代每個相容性層級的功能。 Hello AdventureWorks2008R2 資料庫中，檢閱 hello 變更 tooFull 文字搜尋，因為 SQL Server 2008 和 hello 變更 tooSERVERPROPERTY('LCID') 自 SQL Server 2000。 如需這些變更的詳細資訊，請參閱提供的詳細資訊連結。 全文檢索搜尋的許多選項和設定皆已變更 

   > [!IMPORTANT] 
   > 移轉您的資料庫 tooAzure SQL 資料庫之後，您可以選擇 toooperate hello 資料庫在其目前的相容性層級 （層級 100 hello AdventureWorks2008R2 資料庫） 或更高的層級。 如需有關 hello 含意與作業系統特定的相容性層級的資料庫選項的詳細資訊，請參閱[ALTER DATABASE 相容性層級](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。 另請參閱[ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql)對於其他資料庫層級設定的相關資訊與相關 toocompatibility 層級。
   >

10. （選擇性） 按一下**將報表匯出**toosave hello 報表成為 JSON 檔案。
11. 關閉 hello 資料移轉小幫手。

## <a name="export-toobacpac-file"></a>匯出 tooBACPAC 檔案 

BACPAC 檔案是包含 hello 中繼資料和資料從 SQL Server 資料庫的 BACPAC 的延伸模組 ZIP 檔案。 BACPAC 檔案可以儲存在 Azure blob 儲存體，或為了封存或移轉為本機的儲存體中例如從 SQL Server tooAzure SQL 資料庫。 對於匯出 toobe 交易一致性，您必須確定任一個的任何寫入 hello 匯出期間正在進行活動。

請遵循這些步驟 toouse hello SQLPackage 命令列公用程式 tooexport hello AdventureWorks2008R2 資料庫 toolocal 儲存體。

1. 開啟 Windows 命令提示字元並變更您擁有 hello 您目錄 tooa 資料夾**130**版本 SQLPackage-例如**C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**。

2. 執行下列 SQLPackage 命令在 hello 命令提示字元 tooexport hello hello **AdventureWorks2008R2**資料庫從**localhost**太**AdventureWorks2008R2.bacpac**. 變更這些值做為適當的 tooyour 環境。

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage 匯出](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Hello 執行完成之後產生的 hello BACPAC 檔案會儲存在 hello hello sqlpackage 可執行檔所在的目錄。 在本範例中為 C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin。 

## <a name="log-in-toohello-azure-portal"></a>登入 toohello Azure 入口網站

登入 toohello [Azure 入口網站](https://portal.azure.com/)。 從執行 hello SQLPackage 命令列公用程式的 hello 電腦登入在步驟 5 中減輕 hello 建立 hello 防火牆規則。

## <a name="create-a-sql-server-logical-server"></a>建立 SQL Server 邏輯伺服器

[SQL Server 邏輯伺服器](sql-database-features.md)會作為多個資料庫的中央管理點。 請遵循下列步驟 toocreate SQL server 的邏輯伺服器 toocontain hello 移轉 Adventure Works OLTP 的 SQL Server 資料庫。 

1. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2. 型別**sql server**在 hello 搜尋視窗上 hello**新增**頁面，然後選取**SQL database （邏輯伺服器）** hello 從篩選清單。

    ![選取邏輯伺服器](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. 在 hello**的所有項目**頁面上，按一下**SQL server （邏輯伺服器）** ，然後按一下**建立**上 hello **SQL Server （邏輯伺服器）**頁面.

    ![建立邏輯伺服器](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. 填寫表單 hello SQL 伺服器 （邏輯伺服器） 以 hello 下列資訊，hello 前面影像所示：     

   | 設定       | 建議的值 | 說明 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **伺服器名稱** | 輸入任何全域唯一名稱 | 如需有效的伺服器名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。 | 
   | **伺服器管理員登入** | 輸入任何有效名稱 | 如需有效的登入名稱，請參閱[資料庫識別碼](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers)。 |
   | **密碼** | 輸入任何有效密碼 | 您的密碼必須至少為 8 個字元，且必須包含下列類別目錄的 hello 的其中三種字元： 大寫字母、 小寫字元、 數字和非英數字元。 |
   | **訂用帳戶** | 選取一個訂用帳戶 | 如需訂用帳戶的詳細資訊，請參閱[訂用帳戶](https://account.windowsazure.com/Subscriptions)。 |
   | **資源群組** | 選擇現有資源群組，或建立新群組，例如 **myResourceGroup**。 |  如需有效的資源群組名稱，請參閱[命名規則和限制](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions)。 |
   | **位置** | 輸入 hello 新伺服器的任何有效的位置 | 如需區域的相關資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。 |

   ![建立邏輯伺服器完成表單](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. 按一下**建立**tooprovision hello 邏輯伺服器。 佈建需要幾分鐘的時間。 

> [!IMPORTANT]
> 請記住您的伺服器名稱、伺服器系統管理員登入名稱和密碼。 在本教學課程後續的內容中，您會需要這些值。
>

## <a name="create-a-server-level-firewall-rule"></a>建立伺服器層級防火牆規則

建立 SQL Database 服務 hello [hello 伺服器層級防火牆](sql-database-firewall-configure.md)可避免外部應用程式和工具連接 toohello 伺服器或 hello 伺服器上的任何資料庫，除非 tooopen hello 就會建立防火牆規則針對特定的 IP 位址的防火牆。 請遵循這些步驟 toocreate hello 電腦 IP 位址的 hello 執行 hello SQLPackage 命令列公用程式的 SQL Database 伺服器層級防火牆規則。 這可讓 SQLPackage tooconnect toohello SQL 伺服器資料庫的邏輯伺服器透過 hello Azure SQL Database 防火牆。 

1. 按一下**所有資源**hello 左側功能表中，按一下 新伺服器上 hello**所有資源**頁面。 為您的伺服器 hello [概觀] 頁面會開啟，並提供進一步組態的選項。

     ![邏輯伺服器概觀](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. 按一下**防火牆**在底下的 hello 左側功能表中**設定**hello 概觀 頁面上。 hello**防火牆設定**hello SQL 資料庫伺服器 頁面隨即開啟。 

3. 按一下**新增用戶端 IP** hello 工具列 tooadd hello 電腦的 IP 位址 hello 上您目前正在使用，然後按一下**儲存**。 系統會為此 IP 位址建立伺服器層級防火牆規則。

     ![設定伺服器防火牆規則](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. 按一下 [確定] 。

您現在可以連接此伺服器上使用 SQL Server Management Studio 或您選擇從這個 IP 位址，使用先前建立的 hello 伺服器系統管理員帳戶的另一個工具 tooall 資料庫。

> [!NOTE]
> SQL Database 會透過連接埠 1433 通訊。 如果您嘗試 tooconnect 從公司網路內，由您的網路防火牆可能不允許透過通訊埠 1433年的輸出流量。 如果是這樣，您無法連接 tooyour Azure SQL Database 伺服器，除非您的 IT 部門會開啟通訊埠 1433年。
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>匯入 BACPAC 檔案 tooAzure SQL 資料庫 

hello hello SQLPackage 命令列公用程式最新版本提供支援建立在指定的 Azure SQL database[服務層和效能層級](sql-database-service-tiers.md)。 為了達到最佳效能，在匯入期間，選取最高的服務層和效能層級，然後向下延展匯入後如果 hello 服務層和效能層級高於您需要立即。

請遵循這些步驟使用 hello SQLPackage 命令列公用程式 tooimport hello AdventureWorks2008R2 資料庫 tooAzure SQL 資料庫。 雖然您可以使用 SQL Server Management Studio，這項工作，SQLPackage 是最大的彈性和達到最佳效能的大部分實際執行環境的 hello 慣用方法。 請參閱[從 SQL Server tooAzure 使用 BACPAC 檔案的 SQL Database 移轉](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/)。

- 執行下列 SQLPackage 命令在 hello 命令提示字元 tooimport hello hello **AdventureWorks2008R2**資料庫從本機儲存體 toohello SQL server 邏輯伺服器，您先前建立的 tooa 新資料庫，服務層**Premium**，以及服務目標的**P6**。 角括弧括住的 hello 值取代為適當的值，SQL server 的邏輯伺服器，並指定 hello 新資料庫 （也取代 hello 角括號） 的名稱。 您也可以選擇資料庫版本和服務 objectgive toochange hello 值做為適當的 tooyour 環境。 基於本教學課程的 hello 目的，稱為 hello 移轉的資料庫**myMigratedDatabase**。

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage 匯入](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> SQL Server 邏輯伺服器會接聽連接埠 1433。 如果您正嘗試 tooconnect tooa SQL server 內的邏輯伺服器從公司防火牆，此連接埠必須在 hello 公司防火牆中開啟您 toosuccessfully 連線。
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 連線

使用 SQL Server Management Studio tooestablish 連接 tooyour Azure SQL Database 伺服器和剛移轉的資料庫，呼叫**myMigratedDatabase**在本教學課程。 如果您執行 SQLPackage 一部電腦上執行 SQL Server Management Studio，建立使用 hello 前程序中的 hello 步驟這台電腦的防火牆規則。

1. 開啟 SQL Server Management Studio。

2. 在 hello**連接 tooServer**對話方塊方塊中，輸入下列資訊的 hello:
   - **伺服器類型**：指定資料庫引擎
   - **伺服器名稱**︰輸入您的完整伺服器名稱，例如 **mynewserver20170403.database.windows.net**
   - **驗證**：指定 SQL Server 驗證
   - **登入**︰輸入您的伺服器管理帳戶
   - **密碼**: hello 密碼輸入伺服器系統管理員帳戶
 
    ![以 ssms 連線](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. 按一下 [ **連接**]。 hello 物件總管 視窗隨即開啟。 

4. 在 物件總管 中，展開**資料庫**，然後展開  **myMigratedDatabase** tooview hello 範例資料庫中的 hello 物件。

## <a name="change-database-properties"></a>變更資料庫屬性

您可以變更 hello 服務層、 效能層級，以及使用 SQL Server Management Studio 的相容性層級。 在 hello 匯入階段中，我們建議您匯入 tooa 較高的效能層資料庫獲得最佳效能，但是，您向下調整 hello 匯入完成 toosave 金額，直到您準備好 tooactively 使用 hello 匯入的資料庫之後。 變更 hello 相容性層級可能會產生較佳的效能和存取 toohello 最新功能的 hello Azure SQL Database 服務。 當您移轉較舊的資料庫時，就會在與 hello 資料庫匯入相容的 hello 最低的支援層級維護其資料庫相容性層級。 如需詳細資訊，請參閱[改善 Azure SQL Database 中相容性層級 130 的查詢效能](sql-database-compatibility-level-query-performance-130.md).

1. 在 物件總管 中，於 myMigratedDatabase 上按一下滑鼠右鍵，然後按一下新增查詢。 查詢視窗中開啟連接的 tooyour 資料庫。

2. 執行太遵循命令 tooset hello 服務層的 hello**標準**太 hello 效能層級和**S1**。

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![變更服務層](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. 執行下列命令 toochange hello 資料庫相容性層級太 hello**130**。

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![變更相容性層級](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>後續步驟 
在本教學課程中，您已準備、匯出和匯入資料庫。 您已了解如何︰

> [!div class="checklist"]
> * 準備移轉 tooAzure SQL 資料庫的 SQL Server 中的資料庫
> * Hello 資料庫 tooa BACPAC 檔案匯出
> * Hello BACPAC 檔案匯入到 Azure SQL Database

如何前進 toohello 下一個教學課程 toolearn toosecure 您的資料庫。

> [!div class="nextstepaction"]
> [保護 Azure SQL Database](sql-database-security-tutorial.md)。


