---
title: "aaaConfigure 多重要素驗證 Azure SQL |Microsoft 文件"
description: "針對 SQL Database 和 SQL 資料倉儲，搭配使用 Multi-Factor Authentication 與 SSMS。"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>設定適用於 SQL Server Management Studio 和 Azure AD 的多重要素驗證

本主題說明如何 toouse Azure Active Directory multi-factor authentication (MFA) 與 SQL Server Management Studio。 連接 SSMS 或 SqlPackage.exe tooAzure SQL Database 和 Azure SQL 資料倉儲時，就可以使用 azure AD MFA。

如需 Azure SQL Database 多重要素驗證的概觀，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。

## <a name="configuration-steps"></a>組態步驟

1. **設定 Azure Active Directory** -如需詳細資訊，請參閱[管理 Azure AD 目錄](https://msdn.microsoft.com/library/azure/hh967611.aspx)，[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)，[加入您自己的網域名稱 tooAzure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)， [Microsoft Azure 現在支援與 Windows Server Active Directory 同盟](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)，和[使用 Windows PowerShell 管理 Azure AD](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **設定 MFA** - 如需逐步指示，請參閱[什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)、[使用 Azure SQL Database 和資料倉儲的條件式存取 (MFA)](sql-database-conditional-access.md)。 (完全條件式存取需要進階 Azure Active Directory (Azure AD)。 有限的 MFA 適用於標準 Azure AD。)
3. **設定 SQL Database 或 Azure AD 驗證的 SQL 資料倉儲**-如需逐步指示，請參閱[連接 tooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)。
4. **下載 SSMS** -hello 用戶端電腦上，下載最新的 SSMS hello 從[下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。 針對所有本主題中的 hello 功能，使用至少第 2017 年 7 月版本 17.2。  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>使用通用驗證搭配 SSMS 進行連線

hello 下列步驟顯示如何 tooconnect tooSQL 資料庫或使用 SQL 資料倉儲 hello 最新的 SSMS。

1. hello 上使用通用的驗證，tooconnect**連接 tooServer**對話方塊中，選取**Active Directory-MFA 支援與通用**。 (如果您看到**Active Directory 通用驗證**您不在 hello 最新版本的 SSMS。)  
   ![1mfa-universal-connect][1]  
2. 完整的 hello**使用者名**hello Azure Active Directory 的認證，格式為 hello 方塊`user_name@domain.com`。  
   ![1mfa-universal-connect-user](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. 如果您要的來賓使用者身分連接，您必須按一下**選項**，在 hello**連接屬性**對話方塊中，完成 hello **AD 網域名稱或租用戶識別碼**方塊。 如需詳細資訊，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。
   ![mfa-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. 如往常般 SQL Database 和 SQL 資料倉儲，您必須按一下**選項**hello 來指定 hello 資料庫**選項** 對話方塊。 (如果 hello 連線使用者是 guest 使用者 (亦即joe@outlook.com)，您必須檢查 hello 方塊，並加入 hello 目前的 AD 網域名稱或租用戶識別碼作為選項的一部分。 請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)]()(sql-database-ssms-mfa-authentication.md。 然後按一下 [ **連接**]。  
5. 當 hello**登入帳戶 tooyour**出現對話方塊，請提供 hello 帳戶與 Azure Active Directory 身分識別的密碼。 如果使用者不屬於與 Azure AD 同盟的網域，則不需要密碼。  
   ![2mfa-sign-in][2]  

   > [!NOTE]
   > 如果是使用不需要 MFA 的帳戶進行通用驗證，則您可以在此時連線。 使用者要求 MFA，繼續執行步驟的 hello:
   >  
   
6. 可能會顯示兩個 MFA 設定對話方塊。 此一次作業取決於 hello MFA 系統管理員設定，並因此可能會是選擇性。 MFA 啟用網域中的這個步驟是有時候預先定義 （例如，hello 網域都需要使用者 toouse 智慧卡和 pin 碼）。  
   ![3mfa-setup][3]  
7. hello 第二個可行對話方塊可讓您 tooselect hello 詳細資料的驗證方法一次。 您的系統管理員可以設定 hello 可能的選項。  
   ![4mfa-verify-1][4]  
8. hello Azure Active Directory 會傳送確認資訊 tooyou hello。 當您收到 hello 驗證碼時，請將其輸入 hello**輸入驗證碼**方塊，然後按一下**登入**。  
   ![5mfa-verify-2][5]  

驗證完成時，SSMS 即會正常連線 (假設認證和防火牆存取有效)。

## <a name="next-steps"></a>後續步驟

* 如需 Azure SQL Database 多重要素驗證的概觀，請參閱 [SQL Database 和 SQL 資料倉儲的通用驗證 (MFA 的 SSMS 支援)](sql-database-ssms-mfa-authentication.md)。
* 授與其他人存取 tooyour 資料庫： [SQL Database 驗證和授權： 授與存取權](sql-database-manage-logins.md)  
請確定其他人可以透過 hello 防火牆連線：[設定 Azure SQL Database 伺服器層級防火牆規則使用 hello Azure 入口網站](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png

