---
title: "從 Azure SQL Database 備份還原單一資料表 | Microsoft Docs"
description: "了解如何從 Azure SQL Database 備份還原單一資料表。"
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
ms.openlocfilehash: 8c750c503d10ea63b9665958b96db2dfea3d9a3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a>如何從 Azure SQL Database 備份還原單一資料表
您可能不小心修改了 SQL 資料庫中的某些資料，而想要還原受影響的單一資料表。 本文說明如何從其中一個 SQL Database [自動備份](sql-database-automated-backups.md)還原資料庫中的單一資料表。

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a>準備步驟︰重新命名資料表，並還原資料庫的複本
1. 識別出 Azure SQL Database 中您想要以還原複本取代的資料表。 使用 Microsoft SQL Management Studio 來重新命名資料表。 例如，將資料表重新命名為 &lt;資料表名稱&gt;_old。
   
   > [!NOTE]
   > 為了避免被阻斷，請確定您要重新命名的資料表上沒有正在執行的活動。 如果您遇到問題，則請確定在維護期間執行此程序。
   >

2. 使用[還原時間點](sql-database-recovery-using-backups.md#point-in-time-restore)步驟，將資料庫備份還原至您想要復原的時間點。
   
   > [!NOTE]
   > 還原之資料庫的名稱會是「資料庫名稱+時間戳記」的格式；例如，**Adventureworks2012_2016-01-01T22-12Z**。 此步驟不會覆寫伺服器上現有的資料庫名稱。 這是一項安全措施，其目的是要讓您在卸除目前的資料庫並重新命名還原的資料庫以供生產環境使用之前，先確認還原的資料庫。
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a>使用 SQL Database 移轉工具，從還原的資料庫複製資料表

1. 下載並安裝 [SQL Database 移轉精靈](https://sqlazuremw.codeplex.com)。
2. 開啟 SQL Database 移轉精靈，並在 [選取程序] 頁面，選取 [分析/移轉] 底下的 [資料庫]，然後按 [下一步]。

   ![SQL Database 移轉精靈 - 選取程序](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. 在 [連接至伺服器]  對話方塊中，套用下列設定：

   * 伺服器名稱︰**您的 SQL 伺服器**
   * 驗證：**SQL Server 驗證**
   * 登入︰**您的登入**
   * 密碼︰**您的密碼**
   * 資料庫：**Master DB (列出所有資料庫)**
   
   > [!NOTE]
   > 根據預設，精靈會儲存您的登入資訊。 如果您不希望它儲存，請選取 [忘記登入資訊] 。
   >
   
     ![SQL Database 移轉精靈 - 選取來源 - 步驟 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. 在 [選取來源] 對話方塊中，從 [準備步驟] 區段選取還原之資料庫的名稱以做為來源，然後按 [下一步]。
   
    ![SQL Database 移轉精靈 - 選取來源 - 步驟 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. 在 [選擇物件] 對話方塊中，選取 [選取特定的資料庫物件] 選項，然後選取您要移轉到目標伺服器的資料表 (可選取多個)。
   ![SQL Database 移轉精靈 - 選取物件](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. 在 [指令碼精靈摘要] 頁面中，當系統提示您是否準備好要產生 SQL 指令碼時，請按一下 [是]。 也有可儲存 TSQL 指令碼的選項以供您稍後使用。
   ![SQL Database 移轉精靈 - 指令碼精靈摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. 在 [結果摘要] 頁面中，按 [下一步]。
   ![SQL Database 移轉精靈 - 結果摘要](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. 在 [設定目標伺服器的連線] 頁面中，按一下 [連接至伺服器]，然後輸入詳細資訊如下：
   
   * **伺服器名稱**：目標伺服器執行個體
   * **驗證**：**SQL Server 驗證**。 輸入您的登入認證。
   * **資料庫**：**Master DB (列出所有資料庫)**。 此選項會列出目標伺服器上的所有資料庫。
     
     ![SQL Database 移轉精靈 - 設定目標伺服器的連線](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. 按一下 [連接]，選取資料表要移動至的目標資料庫，然後按 [下一步]。 先前產生的指令碼應該會完成執行，且您應該會看到剛才移動的資料表已複製到目標資料庫。

## <a name="verification-step"></a>驗證步驟

- 查詢並測試剛才複製的資料表，以確認資料完整。 經過確認之後，您就可以從 [準備步驟]  區段卸除已重新命名的資料表。 (例如，&lt;資料表名稱&gt;_old)。

## <a name="next-steps"></a>後續步驟
[SQL Database 自動備份](sql-database-automated-backups.md)

