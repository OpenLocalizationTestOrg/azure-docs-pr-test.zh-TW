---
title: "aaaConditional 存取-Azure SQL Database 和資料倉儲 |Microsoft 文件"
description: "深入了解如何針對 Azure SQL Database 和資料倉儲的 tooconfigure 條件式存取。"
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>使用 Azure SQL Database 和資料倉儲的條件式存取 (MFA)  

SQL Database 和 SQL 資料倉儲都支援 Microsoft 條件式存取。 hello 下列步驟顯示如何 tooconfigure SQL Database tooenforce 條件式存取原則。  

## <a name="prerequisites"></a>必要條件  
- 您必須設定您的 SQL 資料庫或 SQL 資料倉儲 toosupport 的 Azure Active Directory 驗證。 如需特定步驟，請參閱[使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證](sql-database-aad-authentication-configure.md)。  
- 啟用多因素驗證時，您必須在支援的工具，例如 hello 最新的 SSMS 連接使用。 如需詳細資訊，請參閱[設定適用於 SQL Server Management Studio 的 Azure SQL Database 多重要素驗證](sql-database-ssms-mfa-authentication-configure.md)。  

## <a name="configure-ca-for-azure-sql-dbdw"></a>針對 Azure SQL DB/DW 設定 CA  
1.  登入 toohello 入口網站中，選取**Azure Active Directory**，然後選取**條件式存取**。 如需詳細資訊，請參閱 [Azure Active Directory 條件式存取的技術參考](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference)。  
  ![[條件式存取] 刀鋒視窗](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  在 hello**條件式存取原則**刀鋒視窗中，按一下 **新原則**，提供名稱，然後按**設定規則**。  
3.  在下**指派**，選取**使用者和群組**，檢查**選取使用者和群組**，然後選取 hello 使用者或群組的條件式存取。 按一下**選取**，然後按一下**完成**tooaccept 選取項目。  
  ![選取 [使用者和群組]](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  選取 [雲端應用程式]，按一下 [選取應用程式]。 您會看到所有可供條件式存取使用的應用程式。 選取**Azure SQL Database**，hello 底部按一下**選取**，然後按一下**完成**。  
  ![選取 SQL Database](./media/sql-database-conditional-access/select-sql-database.png)  
  如果找不到**Azure SQL Database** hello 遵循第三個螢幕擷取畫面中列出，請完成下列步驟的 hello:   
  - 登入的 AAD 系統管理員帳戶使用 SSMS tooyour Azure SQL DB/DW 執行個體。  
  - 執行 `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`。  
  - 登入 tooAAD，並確認 Azure SQL Database 和資料倉儲已列在 AAD 中的 hello 應用程式。  

5.  選取**存取控制項**，選取**Grant**，然後核取您想要 tooapply hello 原則。 例如，我們選取 [需要多重要素驗證]。  
  ![選取授與存取權](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>摘要  
hello 選取應用程式 (Azure SQL Database) 允許 tooconnect tooAzure SQL DB/DW 使用 Azure AD Premium，現在會強制執行選取的 hello 條件式存取原則，**需要多重要素驗證。**  
若有關於多重要素驗證的 Azure SQL Database 和資料倉儲相關問題，請連絡 MFAforSQLDB@microsoft.com。  

## <a name="next-steps"></a>後續步驟  

如需教學課程，請參閱[保護 Azure SQL Database](sql-database-security-tutorial.md)。
