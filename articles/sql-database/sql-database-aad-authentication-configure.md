---
title: "aaaConfigure Azure Active Directory 驗證 SQL |Microsoft 文件"
description: "深入了解如何 tooconnect tooSQL 資料庫和使用 Azure Active Directory 驗證的 SQL 資料倉儲。"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>使用 SQL Database 或 SQL 資料倉儲設定和管理 Azure Active Directory 驗證

本文章將示範如何 toocreate 並填入 Azure AD，然後搭配使用 Azure AD 與 Azure SQL Database 和 SQL 資料倉儲。 如需概觀，請參閱 [Azure Active Directory 驗證](sql-database-aad-authentication.md)。

>  [!NOTE]  
>  連接的 tooSQL Azure VM 上執行的伺服器不支援使用 Azure Active Directory 帳戶。 請改用 Active Directory 網域帳戶。

## <a name="create-and-populate-an-azure-ad"></a>建立和填入 Azure AD
建立 Azure AD 並利用使用者和群組填入。 Azure AD 可 hello 初始網域 Azure AD 受管理的網域。 Azure AD 也可以在內部部署 Active Directory 網域服務，與 hello Azure AD 同盟。

如需詳細資訊，請參閱[整合內部部署身分識別與 Azure Active Directory](../active-directory/active-directory-aadconnect.md)，[加入您自己的網域名稱 tooAzure AD](../active-directory/active-directory-add-domain.md)， [Microsoft Azure 現在支援與同盟Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/)，[管理 Azure AD 目錄](https://msdn.microsoft.com/library/azure/hh967611.aspx)，[使用 Windows PowerShell 管理 Azure AD](/powershell/azure/overview?view=azureadps-2.0)，和[混合式身分識別必要的連接埠和通訊協定](../active-directory/active-directory-aadconnect-ports.md)。

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>選擇性： 建立關聯，或變更 hello 目前與 Azure 訂用帳戶相關聯的 active directory
tooassociate hello Azure AD 目錄，以您的組織，您的資料庫建立 hello 目錄 hello Azure 訂用帳戶裝載 hello 資料庫的受信任的目錄。 如需詳細資訊，請參閱 [Azure 訂用帳戶如何與 Azure AD 產生關聯](https://msdn.microsoft.com/library/azure/dn629581.aspx)。

**其他資訊：** 每個 Azure 訂用帳戶都會與 Azure AD 執行個體有信任關係。 這表示其信任該目錄 tooauthenticate 使用者、 服務和裝置。 多個訂閱可以信任 hello 相同的目錄，但訂閱只能信任一個目錄。 您可以看到所信任的目錄，由您的訂閱下 hello**設定**在索引標籤上[https://manage.windowsazure.com/](https://manage.windowsazure.com/)。 此訂用帳戶具有與目錄的信任關係是不同的訂用帳戶已與其他 Azure 中所有資源 （網站、 資料庫等等），後者比較像是訂閱的子資源的 hello 關係。 如果訂用帳戶已過期，則存取 toothose hello 訂用帳戶相關聯的其他資源也會停止。 但是 hello 目錄會留在 Azure 中，而且您可以將其他訂用帳戶與該目錄產生關聯，並繼續 toomanage hello 目錄使用者。 如需有關資源的詳細資訊，請參閱 [了解 Azure 中的資源存取](https://msdn.microsoft.com/library/azure/dn584083.aspx)。

hello 下列程序示範如何 toochange hello 產生指定的訂用帳戶目錄的關聯。
1. 連接 tooyour [Azure 傳統入口網站](https://manage.windowsazure.com/)利用 Azure 訂用帳戶系統管理員。
2. 在 hello 左邊的橫幅中，選取 **設定**。
3. 訂用帳戶會出現在 hello 設定畫面中。 如果 hello 需要訂用帳戶不會出現，請按一下**訂閱**hello 頂端下拉 hello**依目錄篩選**方塊並選取包含您的訂閱 hello 目錄，然後按一下**套用**。
   
    ![select subscription][4]
4. 在 hello**設定**區域中，按一下您的訂閱，然後再按一下**編輯目錄**hello hello 頁底端。
   
    ![ad-settings-portal][5]
5. 在 hello**編輯目錄**，選取 hello 與您的 SQL Server 或 SQL 資料倉儲、 相關聯的 Azure Active Directory，然後按一下下一步 hello 箭號。
   
    ![edit-directory-select][6]
6. 在 [hello**確認**目錄對應] 對話方塊中，確認"**將會移除所有的共同管理員。**"
   
    ![edit-directory-confirm][7]
7. 按一下 hello 核取 tooreload hello 入口網站。

   > [!NOTE]
   > 當變更 hello 目錄、 存取 tooall 共同管理員，Azure AD 使用者和群組，並移除目錄為基礎的資源使用者，而且不再有存取 toothis 訂用帳戶或其資源。 只有您，做為服務管理員，可以設定存取主體根據 hello 新目錄。 這項變更可能需要相當長的時間 toopropagate tooall 資源。 變更 hello 目錄，也變更 SQL Database 和 SQL 資料倉儲 hello Azure AD 系統管理員，而不允許任何現有的 Azure AD 使用者的資料庫存取權。 hello Azure AD 系統管理員必須重設 （如下所述），且新的 Azure AD 使用者必須先建立。
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>建立 Azure SQL 伺服器的 Azure AD 系統管理員
每個 SQL Azure 伺服器 （裝載 SQL Database 或 SQL 資料倉儲） 開頭為 hello hello 整個 Azure SQL server 系統管理員的單一伺服器系統管理員帳戶。 第二個 SQL Server 系統管理員必須建立，也就是 Azure AD 帳戶。 這個主體的自主的資料庫使用者身分建立 hello master 資料庫中。 做為系統管理員，hello server 系統管理員帳戶屬於 hello **db_owner**角色中的每個使用者資料庫，然後輸入 hello 為每個使用者資料庫**dbo**使用者。 如需 hello server 系統管理員帳戶的詳細資訊，請參閱[管理資料庫和 Azure SQL Database 中的登入](sql-database-manage-logins.md)。

當使用異地備援的 Azure Active Directory，hello Azure Active Directory 系統管理員必須設定主要 hello 和 hello 次要伺服器。 如果伺服器不需要 Azure Active Directory 系統管理員，然後登入 Azure Active Directory 和使用者會收到 「 無法連接 」 tooserver 錯誤。

> [!NOTE]
> 在 Azure AD 帳戶的內容 （包括 hello Azure SQL server 系統管理員帳戶），根據的使用者無法建立 Azure AD 為基礎的使用者，因為他們沒有權限 toovalidate 提議 hello Azure AD 與資料庫使用者。
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>佈建 Azure SQL 伺服器的 Azure Active Directory 系統管理員

hello 下列兩個程序顯示如何 tooprovision hello Azure 入口網站中，也可以使用 PowerShell 您 Azure SQL server 的 Azure Active Directory 系統管理員。

### <a name="azure-portal"></a>Azure 入口網站
1. 在 hello [Azure 入口網站](https://portal.azure.com/)、 在 hello 右上角、 按一下 下一份可能的 Active Directory 您連接 toodrop。 選擇 hello 更正為 hello 預設 Azure AD 的 Active Directory。 此步驟的連結 hello 訂用帳戶關聯與 Active Directory 與 Azure SQL server 並確認的 hello 相同訂用帳戶同時用於 Azure AD 和 SQL Server。 （hello Azure SQL 伺服器可以裝載 Azure SQL Database 或 Azure SQL 資料倉儲。）   
    ![choose-ad][8]   
    
2. 在 hello 保持橫幅選取**SQL 伺服器**，選取您**SQL server**，然後在 hello **SQL Server**刀鋒視窗中，按一下**Active Directory 系統管理員**.   
3. 在 hello **Active Directory 系統管理員**刀鋒視窗中，按一下 **設定系統管理員**。   
    ![選取 Active Directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. 在 hello**新增系統管理員**刀鋒視窗中，搜尋使用者、 選取 hello 使用者或群組 toobe 為系統管理員，然後**選取**。 （hello Active Directory 管理刀鋒視窗會顯示所有成員與 Active directory 群組。 呈現灰色的使用者或群組無法選取，因為他們不受支援成為 Azure AD 系統管理員。 (請參閱支援的系統管理員在 hello hello 清單**Azure AD 的功能和限制**區段[使用 Azure Active Directory 驗證的驗證的 SQL 資料庫或 SQL 資料倉儲](sql-database-aad-authentication.md)。)角色型存取控制 (RBAC) 適用於僅 toohello 入口網站，而且不傳播的 tooSQL 伺服器。   
    ![選取系統管理員](./media/sql-database-aad-authentication/select-admin.png)  
    
5. 頂端的 hello hello **Active Directory 系統管理員**刀鋒視窗中，按一下 **儲存**。   
    ![儲存系統管理員](./media/sql-database-aad-authentication/save-admin.png)   

變更 hello 系統管理員的 hello 程序可能需要幾分鐘的時間。 然後 hello 新系統管理員會出現在 hello **Active Directory 系統管理員**方塊。

   > [!NOTE]
   > 設定 hello Azure AD 系統管理員，請 hello 新系統管理員的名稱 （使用者或群組） 不能出現在 hello 虛擬 master 資料庫的 SQL Server 驗證使用者身分。 如果有的話，hello Azure AD 系統管理員安裝程式將會失敗;復原其建立，並指出該這類的系統管理員 （名稱） 已經存在。 因為這類的 SQL Server 驗證使用者不是 hello Azure AD 的一部分，任何使用 Azure AD 驗證的投入時間 tooconnect toohello 伺服器將會失敗。
   > 


toolater 移除系統管理員，在 hello hello 頂端**Active Directory 系統管理員**刀鋒視窗中，按一下 **移除系統管理員**，然後按一下**儲存**。

### <a name="powershell"></a>PowerShell
toorun PowerShell cmdlet，您需要 toohave 安裝並執行 Azure PowerShell。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

tooprovision 為 Azure AD 系統管理員，請執行下列 Azure PowerShell 命令的 hello:

* Add-AzureRmAccount
* Select-AzureRmSubscription

Cmdlet 使用 tooprovision 和管理 Azure AD 系統管理員：

| Cmdlet 名稱 | 說明 |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |佈建 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員 (必須來自目前的訂用帳戶。 （必須是從 hello 目前訂用帳戶）。 |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |移除 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。 |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |傳回目前為 hello Azure SQL server 或 Azure SQL 資料倉儲設定 Azure Active Directory 系統管理員的相關資訊。 |

使用的 PowerShell 命令取得說明 toosee 更詳細說明每個這些命令，例如``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``。

hello 下列指令碼會佈建 Azure AD 系統管理員群組命名為**DBA_Group** (物件識別碼`40b79501-b343-44ed-9ce7-da4c8cc7353f`) hello **demo_server**名為資源群組中的伺服器**群組-23**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

hello **DisplayName**輸入的參數接受 hello Azure AD 的顯示名稱或 hello 使用者主體名稱。 例如 ``DisplayName="John Smith"`` 和 ``DisplayName="johns@contoso.com"``。 Azure AD 群組只有 hello Azure AD 支援的顯示名稱。

> [!NOTE]
> hello Azure PowerShell 命令，```Set-AzureRmSqlServerActiveDirectoryAdministrator```不會阻止您佈建 Azure AD 系統管理員不支援的使用者。 不支援的使用者可以佈建，但無法連接 tooa 資料庫。 
> 

hello 下列範例會使用選擇性的 hello **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> hello Azure AD **ObjectID**時需要 hello **DisplayName**不是唯一的。 tooretrieve hello **ObjectID**和**DisplayName**值使用 hello Active Directory 區段的 Azure 傳統入口網站，以及檢視 hello 內容的使用者或群組。
> 

下列範例中的 hello 傳回 Azure SQL server 的 hello 目前的 Azure AD 系統管理員的相關資訊：

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

下列範例中的 hello 移除 Azure AD 系統管理員：

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

您也可以使用 hello REST Api 來佈建 Azure Active Directory 系統管理員。 如需詳細資訊，請參閱 [Azure SQL Database 之 Azure SQL Database 作業的 Service Management REST API 參考和作業](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
您也可以使用下列 CLI 命令的呼叫 hello 來佈建 Azure AD 系統管理員：
| 命令 | 說明 |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |佈建 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員 (必須來自目前的訂用帳戶。 （必須是從 hello 目前訂用帳戶）。 |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |移除 Azure SQL 伺服器或 Azure SQL 資料倉儲的 Azure Active Directory 系統管理員。 |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |傳回目前為 hello Azure SQL server 或 Azure SQL 資料倉儲設定 Azure Active Directory 系統管理員的相關資訊。 |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |更新 Azure SQL server 或 Azure SQL 資料倉儲的 hello Active Directory 系統管理員。 |

如需 CLI 命令的詳細資訊，請參閱 [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server)。  


## <a name="configure-your-client-computers"></a>設定用戶端電腦
所有的用戶端電腦從您的應用程式或使用者連接 tooAzure SQL Database 或 Azure SQL 資料倉儲使用 Azure AD 身分識別，您必須安裝下列軟體的 hello:

* 從 [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx)安裝 .NET Framework 4.6 或更新版本。
* SQL Server 的 azure Active Directory 驗證程式庫 (**ADALSQL。DLL**) 提供多個語言版本 （x86 和 amd64） 從 hello 下載中心[Microsoft Active Directory Authentication Library for Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742)。

您可以符合這些需求，方法如下︰

* 安裝  [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)或[for Visual Studio 2015 的 SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)符合 hello.NET Framework 4.6 需求。
* SSMS 會安裝 hello x86 版本**ADALSQL。DLL**。
* SSDT 安裝 hello amd64 版**ADALSQL。DLL**。
* hello 最新的 Visual Studio，從[Visual Studio 下載](https://www.visualstudio.com/downloads/download-visual-studio-vs)符合 hello.NET Framework 4.6 需求，但不會安裝必要的 amd64 版本 hello **ADALSQL。DLL**。

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>在對應資料庫 tooAzure AD 身分識別建立自主的資料庫使用者

Azure Active Directory 驗證需要資料庫使用者 toobe 建立為自主的資料庫使用者。 Azure AD 身分識別為基礎之自主的資料庫使用者是資料庫使用者，並沒有登入 hello master 資料庫中，而對應 tooan 識別在 hello 與 hello 資料庫相關聯的 Azure AD 目錄。 hello Azure AD 身分識別可以是個別的使用者帳戶或群組。 如需有關自主資料庫使用者的詳細資訊，請參閱 [自主資料庫使用者 - 使資料庫可攜](https://msdn.microsoft.com/library/ff929188.aspx)。

> [!NOTE]
> 無法使用入口網站來建立資料庫使用者 （與 hello 例外狀況的系統管理員）。 RBAC 角色不是傳播的 tooSQL 伺服器、 SQL 資料庫或 SQL 資料倉儲。 Azure RBAC 角色用來管理 Azure 資源，並不會套用 toodatabase 權限。 例如，hello **SQL Server 參與者**角色不授與存取 tooconnect toohello SQL Database 或 SQL 資料倉儲。 必須授與 hello 存取權限，直接在 hello 資料庫中使用 TRANSACT-SQL 陳述式。
>

Azure AD 架構自主資料庫使用者 （非 hello 伺服器系統管理員擁有 hello 資料庫），以具有使用者以 Azure AD 識別身分，連接 toohello 資料庫 toocreate 至少 hello **ALTER ANY USER**權限。 接著，使用下列 TRANSACT-SQL 語法的 hello:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name*可以是 hello Azure AD 群組的 Azure AD 使用者或 hello 的顯示名稱的使用者主體名稱。

**範例：** toocreate 自主的資料庫使用者代表 Azure AD 同盟或受管理網域使用者：
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate 自主的資料庫使用者代表 Azure AD 或同盟網域群組，提供 hello 顯示名稱的安全性群組：
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate 代表連線使用 Azure AD 權杖的應用程式之自主的資料庫使用者：

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  您無法直接從 Azure Active Directory 以外 hello 與您 Azure 訂用帳戶相關聯的 Azure Active Directory 中建立使用者。 不過，會匯入的使用者在 hello 其他 Active Directory 的成員相關聯 Active Directory （稱為外部使用者） 可以在 hello 租用戶 Active Directory 中新增 tooan Active Directory 群組。 藉由建立該 AD 群組的自主的資料庫使用者，hello 使用者從 hello 外部的 Active Directory 可以獲得存取 tooSQL 資料庫。   

如需有關根據 Azure Active Directory 身分識別建立自主資料庫使用者的詳細資訊，請參閱 [CREATE USER (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx)。

> [!NOTE]
> 移除 Azure SQL server 的 hello Azure Active Directory 系統管理員可防止任何 Azure AD 驗證使用者 toohello 伺服器連線。 必要時，SQL Database 系統管理員可以手動刪除無法使用的 Azure AD 使用者。   

>  [!NOTE]
>  如果您收到**連接逾時過期**，您可能需要 tooset hello `TransparentNetworkIPResolution` hello 連接字串 toofalse 參數。 如需詳細資訊，請參閱 [.NET Framework 4.6.1 的連線逾時問題 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/)。   

   
當您建立資料庫使用者時，該使用者會收到 hello**連接**權限，而且可以連線 toothat 資料庫 hello 的成員身分**公用**角色。 一開始 hello 只有權限可用 toohello 使用者，都授與的任何權限 toohello**公用**角色或任何權限授與 tooany Windows 群組，它們的成員。 一旦您佈建 Azure AD 為基礎包含資料庫的使用者，您可以授與 hello 使用者額外權限、 hello 相同方式與您授與權限 tooany 其他類型的使用者。 通常 toodatabase 角色授與權限，並加入使用者 tooroles。 如需詳細資訊，請參閱 [Database Engine 權限基本概念](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx)。 如需有關特殊 SQL Database 角色的詳細資訊，請參閱 [管理 Azure SQL Database 的資料庫和登入](sql-database-manage-logins.md)。
匯入管理網域的同盟的網域使用者必須使用受管理的 hello 網域身分識別。

> [!NOTE]
> Azure AD 使用者標示 hello 資料庫中繼資料中具有類型為 E (EXTERNAL_USER) 和群組類型 X (EXTERNAL_GROUPS)。 如需詳細資訊，請參閱 [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx)。 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>使用 SSMS 或 SSDT 連線 toohello 使用者資料庫或資料倉儲  
tooconfirm hello Azure AD 管理員已正確設定，請連接 toohello**主要**使用 hello Azure AD 系統管理員帳戶的資料庫。
tooprovision Azure AD 架構自主資料庫使用者 （非 hello 伺服器系統管理員擁有 hello 資料庫），會以 Azure AD 識別身分具有存取 toohello 資料庫連接 toohello 資料庫。

> [!IMPORTANT]
> Visual Studio 2015 中的 [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) 提供 Azure Active Directory 驗證支援。 hello SSMS 2016 年 8 月版本也支援 Active Directory 通用驗證，可讓系統管理員 toorequire Multi-factor Authentication 通話、 簡訊、 智慧卡使用 pin 或行動裝置應用程式通知。
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>使用 Azure AD 身分識別 tooconnect 使用 SSMS 或 SSDT  

下列程序的 hello 會告訴您如何 tooconnect tooa SQL 資料庫以使用 SQL Server Management Studio 或 SQL Server 資料庫工具的 Azure AD 識別身分。

### <a name="active-directory-integrated-authentication"></a>Active Directory 整合驗證

如果您登入 tooWindows 同盟的網域從使用 Azure Active Directory 認證，請使用這個方法。

1. 啟動 Management Studio 或 Data Tools 和 hello**連接 tooServer** (或**連接 tooDatabase 引擎**) 對話方塊中的，在 hello**驗證**方塊中，選取**Active Directory-整合**。 需要或由於您現有的認證將會顯示 hello 連線可以輸入任何密碼。   

    ![選取 AD 整合式驗證][11]
2. 按一下 hello**選項** 按鈕，在 hello**連接屬性** 頁面的 hello**連接 toodatabase**  方塊中，輸入 hello 名稱要 tooconnect hello 使用者資料庫的。 (hello **AD 網域名稱或租用戶識別碼**」 選項，才支援**通用 MFA 連線**選項，否則它會呈現灰色。)  

    ![選取 hello 資料庫名稱][13]

## <a name="active-directory-password-authentication"></a>Active Directory 密碼驗證

使用 Azure AD 主體名稱使用 hello Azure AD 連接受管理的網域時，請使用這個方法。 您也可以使用同盟帳戶沒有存取 toohello 網域，例如當遠端工作。

如果您登入 tooWindows 之網域不同盟與 Azure 中，使用認證，或者使用 Azure AD 驗證使用 Azure AD 根據初始 hello 或 hello 用戶端網域，請使用這個方法。

1. 啟動 Management Studio 或 Data Tools 和 hello**連接 tooServer** (或**連接 tooDatabase 引擎**) 對話方塊中的，在 hello**驗證**方塊中，選取**Active Directory-密碼**。
2. 在 hello**使用者名**方塊中，輸入您的 Azure Active Directory 使用者名稱格式為 hello  **username@domain.com** 。這必須是從 hello Azure Active Directory 的帳戶，或與 hello Azure Active Directory 同盟的網域帳戶。
3. 在 hello**密碼**方塊中，鍵入 hello Azure Active Directory 帳戶的使用者密碼或同盟網域帳戶。

    ![選取 AD 密碼驗證][12]
4. 按一下 hello**選項** 按鈕，在 hello**連接屬性** 頁面的 hello**連接 toodatabase**  方塊中，輸入 hello 名稱要 tooconnect hello 使用者資料庫的。 （請參閱 hello 圖形在 hello 先前選項）。

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>使用 Azure AD 身分識別 tooconnect，從用戶端應用程式

下列程序的 hello 會告訴您如何 tooconnect tooa SQL 資料庫與 Azure AD 身分識別從用戶端應用程式。

###  <a name="active-directory-integrated-authentication"></a>Active Directory 整合驗證

toouse 整合式 Windows 驗證，您網域的 Active Directory，必須與 Azure Active Directory 建立同盟。 用戶端應用程式 （或服務） 連接 toohello 資料庫必須在網域使用者的認證已加入網域的電腦上執行。

tooconnect tooa 資料庫使用整合式驗證和 Azure AD 身分識別，hello 資料庫連接字串中的 hello 驗證關鍵字必須設 tooActive 目錄整合。 hello 下列 C# 程式碼範例會使用 ADO.NET。

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

hello 連接字串關鍵字``Integrated Security=True``連接 tooAzure SQL Database 不支援。 建立 ODBC 連接時，您將會需要 tooremove 空間，並設定驗證 too'ActiveDirectoryIntegrated'。

### <a name="active-directory-password-authentication"></a>Active Directory 密碼驗證

tooconnect tooa 資料庫使用整合式驗證和 Azure AD 身分識別，hello 驗證關鍵字必須設 tooActive 目錄密碼。 hello 連接字串必須包含使用者識別碼/UID 和 PWD 密碼/關鍵字的值。 hello 下列 C# 程式碼範例會使用 ADO.NET。

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

深入了解 Azure AD 的驗證方法使用 hello 示範程式碼範例，可從[Azure AD 驗證 GitHub 示範](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth)。

## <a name="azure-ad-token"></a>Azure AD 權杖
這種驗證方法允許從 Azure Active Directory (AAD) 取得 token 中介層服務 tooconnect tooAzure SQL Database 或 Azure SQL 資料倉儲。 這可容許包含憑證型驗證的複雜案例。 您必須完成四個基本步驟 toouse Azure AD 權杖驗證：

1. 向 Azure Active Directory 註冊應用程式，並取得您的程式碼中的 hello 用戶端識別碼。 
2. 建立資料庫使用者代表 hello 應用程式。 (稍早在步驟 6 中已完成)。
3. 在 hello 的用戶端電腦執行 hello 應用程式建立的憑證。
4. 新增 hello 憑證做為您的應用程式的金鑰。

範例連接字串︰

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

如需詳細資訊，請參閱 [SQL Server 安全性部落格](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)。

### <a name="sqlcmd"></a>sqlcmd

hello 的陳述式之後，連接使用 sqlcmd，可從 hello 13.1 新版[下載中心](http://go.microsoft.com/fwlink/?LinkID=825643)。

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>後續步驟
- 如需 SQL Database 中存取權和控制權的概觀，請參閱 [SQL Database 的存取權和控制權](sql-database-control-access.md)。
- 如需 SQL Database 中登入、使用者和資料庫角色的概觀，請參閱[登入、使用者和資料庫角色](sql-database-manage-logins.md)。
- 如需資料庫主體的詳細資訊，請參閱[主體](https://msdn.microsoft.com/library/ms181127.aspx)。
- 如需資料庫角色的詳細資訊，請參閱[資料庫角色](https://msdn.microsoft.com/library/ms189121.aspx)。
- 如需 SQL Database 中防火牆規則的詳細資訊，請參閱 [SQL Database 防火牆規則](sql-database-firewall-configure.md)。

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

