---
title: "aaaGetting 開始使用 Azure SQL 資料同步 （預覽） |Microsoft 文件"
description: "本教學課程可協助您開始使用 Azure SQL 資料同步 (預覽)。"
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>開始使用 Azure SQL 資料同步 (預覽)
在此教學課程中，您學會如何藉由建立混合式同步處理群組設定 Azure SQL 資料同步 tooset 包含 Azure SQL Database 和 SQL Server 執行個體。 hello 新同步處理群組完整設定，並在您設定的 hello 排程同步處理。

本教學課程假設您先前至少有一些使用 SQL Database 和 SQL Server 的經驗。 

如需 SQL 資料同步處理的概觀，請參閱[同步資料](sql-database-sync-data.md)。

如需完整 PowerShell 範例顯示如何 tooconfigure SQL 資料同步處理，請參閱下列文章 hello:
-   [使用多個 Azure SQL database 之間的 PowerShell toosync](scripts/sql-database-sync-data-between-sql-databases.md)
-   [使用 Azure SQL Database 和 SQL Server 在內部部署資料庫之間的 PowerShell toosync](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> hello 完成技術文件集 Azure SQL 資料同步先前位於 MSDN，可做為。PDF 文件。 在 [這裡](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)下載。

## <a name="step-1---create-sync-group"></a>步驟 1 - 建立同步群組

### <a name="locate-hello-data-sync-settings"></a>找出 hello 資料同步處理設定

1.  在瀏覽器中瀏覽 toohello Azure 入口網站。

2.  在 hello 入口網站中，找出 hello 工具列上的 SQL 資料庫從儀表板或 hello SQL 資料庫的圖示。

    ![Azure SQL 資料庫清單](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  在 hello **SQL 資料庫**刀鋒視窗中，選取 hello 的 toouse hello 中樞資料庫的資料同步處理。 hello SQL 資料庫刀鋒視窗中開啟現有 SQL 資料庫。

4.  在 hello hello 選取資料庫的 SQL 資料庫刀鋒視窗，選取 **同步 tooother 資料庫**。 hello 資料同步 刀鋒視窗隨即開啟。

    ![Sync tooother 資料庫選項](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>建立新的同步群組

1.  在 hello 資料同步刀鋒視窗中，選取 **新同步處理群組**。 hello**新同步處理群組**使用步驟 1 中，開啟刀鋒視窗**建立同步處理群組**，反白顯示。 hello**建立的資料同步處理群組**也會開啟刀鋒視窗。

2.  在 hello**建立的資料同步處理群組**刀鋒視窗中，請勿 hello 下列事項：

    1.  在 hello**同步群組名稱**欄位中，輸入 hello 新同步處理群組的名稱。

    2.  在 hello**同步處理中繼資料資料庫**區段中，選擇是否 toocreate 新的資料庫 （建議選項） 或 toouse 的現有資料庫。

        > [!NOTE]
        > Microsoft 建議您建立新的空白資料庫 toouse 為 hello 同步處理中繼資料資料庫。 資料同步會在此資料庫中建立資料表，並頻繁執行工作負載。 這個資料庫會自動已經共用為 hello hello 所選資料區域中同步處理群組的所有同步處理中繼資料資料庫中。 您無法變更 hello 同步處理中繼資料資料庫、 其名稱或其 service 層級，但不卸除它。

        如果您選擇 [新資料庫]，請選取 [建立新的資料庫]。 hello **SQL Database**刀鋒視窗隨即開啟。 在 hello **SQL Database**刀鋒視窗中，命名，並設定 hello 新資料庫。 然後選取 [確定]。

        如果您選擇**使用現有的資料庫**，選取從 hello 清單 hello 資料庫。

    3.  在 hello**自動同步處理**區段中，第一次選取**上**或**關閉**。

        如果您選擇**上**，在 hello**同步處理頻率**區段中，輸入的數字，然後選取秒、 分鐘、 小時或天。

        ![指定同步處理頻率](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  在 hello**衝突解決**區段中，選取 「 中樞獲勝 」 或 「"成員 wins。

        ![指定解決衝突的方式](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  選取**確定**並等候 hello 新同步處理群組 toobe 建立和部署。

## <a name="step-2---add-sync-members"></a>步驟 2 - 新增同步成員

建立及部署，步驟 2 hello 新同步處理群組之後**加入同步處理成員**，會反白顯示在 hello**新同步處理群組**刀鋒視窗。

在 hello**中樞資料庫**區段中，輸入 hello 現有認證的 hello SQL 資料庫所在的伺服器上的 hello 中樞資料庫。 請不要在此區段輸入「新」的認證。

![已加入中樞資料庫 toosync 群組](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>新增 Azure SQL Database

在 hello**成員資料庫**區段中，選擇性地選取 加入 Azure SQL Database toohello 同步處理群組**加入 Azure 的資料庫**。 hello**設定 Azure Database**刀鋒視窗隨即開啟。

在 hello**設定 Azure Database**刀鋒視窗中，執行下列項目 hello:

1.  在 hello**同步成員名稱**欄位中，提供 hello 新同步處理成員的名稱。 這個名稱是 hello 資料庫本身 hello 名稱有所區別。

2.  在 hello**訂用帳戶**欄位時，選取 hello 相關聯的 Azure 訂用帳戶計費。

3.  在 hello **Azure SQL Server** hello 欄位時，選取現有的 SQL 資料庫伺服器。

4.  在 hello **Azure SQL Database** hello 欄位時，選取現有的 SQL 資料庫。

5.  在 hello**同步處理方向**欄位中，選取 雙向同步處理 toohello 中樞，或從 hello 中樞。

    ![新增 SQL Database 同步處理成員](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  在 hello **Username**和**密碼**欄位中，輸入 hello 現有認證的 hello SQL 資料庫所在的伺服器上的 hello 成員資料庫。 請不要在此區段輸入「新」的認證。

7.  選取**確定**並等候 hello 新同步處理成員 toobe 建立和部署。

    ![已新增 SQL Database 同步處理成員](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>新增內部部署 SQL Server 資料庫

在 hello**成員資料庫**區段中，選擇性地加入內部部署 SQL Server toohello 同步處理群組選取**加入內部資料庫**。 hello**設定內部部署**刀鋒視窗隨即開啟。

在 hello**設定內部部署**刀鋒視窗中，請勿 hello 下列事項：

1.  選取**選擇 hello 同步代理程式的閘道**。 hello**選取同步處理代理程式**刀鋒視窗隨即開啟。

    ![選擇 hello 同步代理程式閘道](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  在 hello**選擇 hello 同步代理程式的閘道**刀鋒視窗中，選擇是否 toouse 現有代理程式，或建立新的代理程式。

    如果您選擇**現有代理程式**，選取 hello hello 清單從現有的代理程式。

    如果您選擇**建立新的代理程式**，請勿 hello 下列事項：

    1.  Hello 用戶端同步代理程式軟體從提供的 hello 連結上下載並安裝它 hello hello SQL Server 所在的電腦。
 
        > [!IMPORTANT]
        > 您有 tooopen 傳出 TCP 通訊埠 1433 hello 防火牆 toolet hello 用戶端代理程式中的與 hello 伺服器通訊。


    2.  輸入 hello 代理程式的名稱。

    3.  選取 [建立並產生金鑰]。

    4.  將複製 hello 代理程式金鑰 toohello 剪貼簿。
        
        ![建立新同步代理程式](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  選取**確定**tooclose hello**選取同步處理代理程式**刀鋒視窗。

    6.  Hello SQL Server 電腦上，找出並執行 hello 用戶端同步代理程式的應用程式。

        ![hello 資料同步用戶端代理程式的應用程式](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  在 hello 同步代理程式應用程式中，選取 **提交代理程式金鑰**。 hello**同步處理中繼資料資料庫組態**對話方塊隨即開啟。

    8.  在 hello**同步處理中繼資料資料庫組態**對話方塊中，貼上的 從 hello Azure 入口網站複製的 hello 代理程式金鑰。 也提供 hello 現有 hello Azure SQL Database 所在的伺服器上的 hello 中繼資料資料庫認證。 (如果您建立新的中繼資料資料庫時，這個資料庫是在 hello 與 hello 中樞資料庫相同的伺服器。)選取**確定**並等候 hello 設定 toofinish。

        ![輸入 hello 代理程式金鑰及伺服器認證](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   如果此時您會收到防火牆錯誤，您必須 toocreate 防火牆規則上 Azure tooallow 從 hello SQL Server 電腦的連入流量。 您可以手動建立 hello 規則，在 hello 入口網站，但您可能會發現它更容易 toocreate 它在 SQL Server Management Studio (SSMS)。 在 SSMS 中，請嘗試在 Azure 上的 tooconnect toohello 中樞資料庫。 請將其名稱輸入為 \<hub_database_name\>.database.windows.net。 請遵循 hello hello 對話方塊方塊 tooconfigure hello Azure 防火牆規則中的步驟。 然後傳回 toohello 用戶端同步代理程式的應用程式。

    9.  在 hello 用戶端同步代理程式應用程式中，按一下 **註冊**tooregister hello 代理程式的 SQL Server 資料庫。 hello **SQL Server 組態**對話方塊隨即開啟。

        ![新增和設定 SQL Server 資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. 在 hello **SQL Server 組態**對話方塊方塊中，選擇是否 tooconnect 使用 SQL Server 驗證或 Windows 驗證。 如果您選擇 SQL Server 驗證，請輸入 hello 現有的認證。 提供您想 toosync hello SQL Server 名稱和 hello hello 資料庫名稱。 選取**測試連接**tootest 您的設定。 然後選取 [儲存]。 hello 註冊的資料庫會出現在 [hello] 清單。

        ![現在已註冊 SQL Server 資料庫](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. 您現在可以關閉 hello 用戶端同步代理程式的應用程式。

    12. 在 hello 入口網站上 hello**設定內部部署**刀鋒視窗中，選取**選取 hello 資料庫。** hello**選取資料庫**刀鋒視窗隨即開啟。

    13. 在 hello**選取資料庫**刀鋒視窗中的，在 hello**同步成員名稱**欄位中，提供 hello 新同步處理成員的名稱。 這個名稱是 hello 資料庫本身 hello 名稱有所區別。 Hello 清單中選取 hello 資料庫。 在 hello**同步處理方向**欄位中，選取 雙向同步處理 toohello 中樞，或從 hello 中樞。

        ![選取在內部部署資料庫上的 hello](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. 選取**確定**tooclose hello**選取資料庫**刀鋒視窗。 然後選取**確定**tooclose hello**設定內部部署**刀鋒視窗，然後等候 hello 新同步處理成員 toobe 建立和部署。 最後，按一下 **確定**tooclose hello**選取同步處理成員**刀鋒視窗。

        ![內部部署資料庫上加入 toosync 群組](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL 資料同步處理與 hello 本機代理程式，新增您的使用者名稱 toohello 角色`DataSync_Executor`。 資料同步 hello SQL Server 執行個體上建立此角色。

## <a name="step-3---configure-sync-group"></a>步驟 3 - 設定同步群組

Hello 新同步處理群組成員建立和部署，第 3 步驟之後**設定同步處理群組**，會反白顯示在 hello**新同步處理群組**刀鋒視窗。

1.  在 hello**資料表**刀鋒視窗中，選取資料庫的同步處理的 hello 清單從群組成員，然後選取**重新整理結構描述**。

2.  從 hello 的可用資料表清單，選取您想 toosync hello 資料表。

    ![選擇資料表 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  根據預設，會選取 hello 資料表中的所有資料行。 如果您不想 toosync hello 的所有資料行，停用 hello 核取方塊，您不想 toosync hello 資料行。 請確定 tooleave hello 主索引鍵資料行選取。

    ![選取欄位 toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  最後，選取 [儲存]。

## <a name="next-steps"></a>後續步驟
恭喜！ 您已建立一個同時包含 SQL Database 執行個體與 SQL Server 資料庫的同步群組。

如需 SQL Database 和 SQL 資料同步的詳細資訊，請參閱：

-   [下載 hello 完整 SQL 資料同步技術文件](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [下載 SQL 資料同步處理的 REST API 文件以 hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [SQL Database 概觀](sql-database-technical-overview.md)
-   [資料庫生命週期管理](https://msdn.microsoft.com/library/jj907294.aspx)
