---
title: "aaaRestore 單一資料表，從 Azure SQL Database 備份 |Microsoft 文件"
description: "了解如何 toorestore 單一資料表中 Azure SQL Database 備份。"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>如何 toorestore 單一資料表中的 Azure SQL Database 備份
您可能會遇到的情況中，您偶爾修改 SQL database 中的部分資料，而您想 toorecover hello 單一受影響的資料表。 本文說明如何 toorestore 單一資料表中將資料庫從一個 hello SQL Database[自動備份](sql-database-automated-backups.md)。

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>準備步驟： hello 資料表重新命名，並還原 hello 資料庫的複本
1. 識別您想與 hello 還原複本 tooreplace 您 Azure SQL database 中的 hello 資料表。 使用 Microsoft SQL Management Studio toorename hello 資料表。 例如，資料表重新命名 hello 為&lt;資料表名稱&gt;_old。
   
   > [!NOTE]
   > tooavoid 被封鎖，請確定您要重新命名的 hello 資料表上執行任何活動。 如果您遇到問題，則請確定在維護期間執行此程序。
   >

2. 還原備份的資料庫 tooa 點時間中您想 toorecover toousing hello[點 In_Time 還原](sql-database-recovery-using-backups.md#point-in-time-restore)步驟。
   
   > [!NOTE]
   > hello 的 hello 還原資料庫的名稱將會是 hello DBName + 時間戳記格式。例如， **Adventureworks2012_2016 01-01T22 12Z**。 這個步驟不會覆寫在 hello 伺服器 hello 現有資料庫名稱。 這是安全性量值，而且它能 tooallow tooverify hello 還原資料庫後再進行卸除其目前的資料庫，並重新命名用於實際執行環境的 hello 還原資料庫。
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Hello 複製 hello 資料表使用 hello SQL Database 移轉工具還原資料庫

1. 下載並安裝 hello [SQL Database 移轉精靈](https://sqlazuremw.codeplex.com)。
2. 開啟 hello SQL Database 移轉精靈，在 hello**選取處理序**頁面上，選取**分析/移轉資料庫**，然後按一下**下一步**。

   ![SQL Database 移轉精靈 - 選取程序](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. 在 hello**連接 tooServer**對話方塊方塊中，套用下列設定的 hello:

   * 伺服器名稱︰**您的 SQL 伺服器**
   * 驗證：**SQL Server 驗證**
   * 登入︰**您的登入**
   * 密碼︰**您的密碼**
   * 資料庫：**Master DB (列出所有資料庫)**
   
   > [!NOTE]
   > 根據預設 hello 精靈 」 會儲存您的登入資訊。 如果您不希望它儲存，請選取 [忘記登入資訊] 。
   >
   
     ![SQL Database 移轉精靈 - 選取來源 - 步驟 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. 在 hello**選取來源**對話方塊中，選取 hello 還原的資料庫名稱從 hello**準備步驟**做為來源，區段，然後按一下**下一步**。
   
    ![SQL Database 移轉精靈 - 選取來源 - 步驟 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. 在 hello**選擇物件**對話方塊中，選取 hello**選取特定資料庫物件**選項，然後再選取您想 toomigrate toohello 目標伺服器 hello table(or tables)。
   ![SQL Database 移轉精靈 - 選取物件](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. 在 hello**指令碼精靈摘要**頁面上，按一下**是**當系統提示您輸入有關您是否已準備好 toogenerate SQL 指令碼。 您也可以 hello 選項 toosave hello TSQL 指令碼供稍後使用。
   ![SQL Database 移轉精靈 - 指令碼精靈摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. 在 hello**結果摘要**頁面上，按一下**下一步**。
   ![SQL Database 移轉精靈 - 結果摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. 在 hello**設定目標伺服器連線**頁面上，按一下**連接 tooServer**，然後輸入 hello 詳細資料，如下所示：
   
   * **伺服器名稱**：目標伺服器執行個體
   * **驗證**：**SQL Server 驗證**。 輸入您的登入認證。
   * **資料庫**：**Master DB (列出所有資料庫)**。 此選項會列出所有 hello hello 目標伺服器上的資料庫。
     
     ![SQL Database 移轉精靈 - 設定目標伺服器的連線](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. 按一下**連接**，選取 hello 目標資料庫，您想要 toomove hello 資料表，然後按一下**下一步**。 這應該執行 hello 先前產生的指令碼，來完成，您應該會看見 hello 剛移動資料表複製的 toohello 目標資料庫。

## <a name="verification-step"></a>驗證步驟

- 查詢並測試新複製的 hello 資料表 toomake 確認 hello 的資料保持不變。 根據確認，您可以卸除 hello 重新命名資料表表單**準備步驟**> 一節。 (例如，&lt;資料表名稱&gt;_old)。

## <a name="next-steps"></a>後續步驟
[SQL Database 自動備份](sql-database-automated-backups.md)

