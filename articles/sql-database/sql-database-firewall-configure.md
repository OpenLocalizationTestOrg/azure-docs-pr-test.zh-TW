---
title: "aaaAzure SQL Database 防火牆規則 |Microsoft 文件"
description: "了解如何 tooconfigure SQL 資料庫與伺服器層級和資料庫層級防火牆規則 toomanage 存取的防火牆。"
keywords: "資料庫防火牆"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Azure SQL Database 伺服器層級和資料庫層級防火牆規則 

Microsoft Azure SQL Database 為 Azure 和其他網際網路式應用程式提供關聯式資料庫服務。 toohelp 保護您的資料，防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。 hello 防火牆會授與存取 toodatabases hello 來自每個要求的 IP 位址為基礎。

## <a name="overview"></a>概觀

一開始，所有的 TRANSACT-SQL 存取 tooyour Azure SQL 伺服器 hello 防火牆封鎖。 toobegin 使用您的 Azure SQL server，您必須指定一個或多個伺服器層級防火牆規則，讓存取 tooyour Azure SQL 伺服器。 請使用 hello 防火牆規則 toospecify 的 IP 位址範圍從 hello 允許網際網路，而且 Azure 應用程式是否可以嘗試 tooconnect tooyour Azure SQL server。

tooselectively 授與存取 toojust 其中一個 Azure SQL server 中的 hello 資料庫，您必須建立 hello 需要資料庫的資料庫層級規則。 指定的 IP 位址範圍超出的 hello IP 位址在 hello 的伺服器層級防火牆規則中指定的範圍，請確定 hello hello 用戶端 IP 位址落在 hello hello 資料庫層級規則中指定的範圍內的 hello 資料庫防火牆規則。

從連線嘗試 hello 網際網路和 Azure 必須先通過 hello 防火牆才能到達您的 Azure SQL server 或 SQL Database 中 hello 下列圖表所示：

   ![圖解防火牆設定。][1]

* **伺服器層級防火牆規則：**這些規則可讓用戶端 tooaccess 整個 Azure SQL 伺服器，也就是所有都 hello 資料庫都 hello 相同邏輯伺服器。 這些規則會儲存在 hello**主要**資料庫。 使用 hello 入口網站，或使用 TRANSACT-SQL 陳述式，可以設定伺服器層級防火牆規則。 使用 hello Azure 入口網站或 PowerShell toocreate 伺服器層級防火牆規則，您必須是 hello 訂用帳戶擁有者或訂閱參與者。 toocreate 使用 Transact SQL 的伺服器層級防火牆規則，您必須連接為 hello 伺服器層級主體登入或 hello Azure Active Directory 系統管理員 （亦即必須先建立伺服器層級防火牆規則 toohello SQL Database 執行個體由使用者以 Azure 層級權限）。
* **資料庫層級防火牆規則：**這些規則可讓用戶端 tooaccess 某些 （安全） 資料庫內 hello 相同邏輯伺服器。 您可以建立這些規則的每個資料庫 (包括 hello**主要**database0)，並儲存在 hello 個別的資料庫。 資料庫層級防火牆規則來設定它必須使用 TRANSACT-SQL 陳述式，而且只能設定之後 hello 第一個伺服器層級防火牆。 如果您是外部 hello 範圍 hello 伺服器層級防火牆規則中指定的 hello 資料庫層級防火牆規則中指定 IP 位址範圍，只有在 hello 資料庫層級範圍內有 IP 位址的用戶端才可以存取 hello 資料庫。 對於資料庫，您最多可以有 128 個資料庫層級防火牆規則。 主要與使用者資料庫的資料庫層級防火牆規則，僅可透過 Transact-SQL 來建立和管理。 如需有關設定資料庫層級防火牆規則的詳細資訊，請參閱 hello 範例稍後在這個發行項，請參閱[sp_set_database_firewall_rule (Azure SQL Database)](https://msdn.microsoft.com/library/dn270010.aspx)。

**建議：** Microsoft 建議使用資料庫層級防火牆規則時可能 tooenhance 安全性和 toomake 更容易移植您的資料庫。 系統管理員使用伺服器層級防火牆規則，當您已擁有 hello 的許多資料庫相同的存取需求，且您不想 toospend 個別設定每個資料庫的時間。

> [!Note]
> 業務續航力的 hello 內容中的可攜式資料庫的相關資訊，請參閱[嚴重損壞修復的驗證需求](sql-database-geo-replication-security-config.md)。
>

### <a name="connecting-from-hello-internet"></a>從 hello 網際網路連線

當電腦嘗試從網際網路 hello tooconnect tooyour 資料庫伺服器時，hello 防火牆會先檢查 hello 源自對 hello 資料庫 hello 連線要求的 hello 資料庫層級防火牆規則的 hello 要求的 IP 位址：

* 如果 hello 要求 hello IP 位址是其中一個 hello hello 資料庫層級防火牆規則中指定的範圍內，hello 連接授與 toohello 包含 hello 規則的 SQL 資料庫。
* 如果 hello 要求 hello IP 位址不是其中一個 hello hello 資料庫層級防火牆規則中指定的範圍內，會檢查 hello 伺服器層級防火牆規則。 如果 hello 要求 hello IP 位址是其中一個 hello hello 伺服器層級防火牆規則中指定的範圍內，會授與 hello 連線。 伺服器層級防火牆規則 hello Azure SQL server 上套用 tooall SQL 資料庫。  
* 如果 hello 要求 hello IP 位址不在任何 hello 資料庫層級中指定 hello 範圍或伺服器層級防火牆規則，hello 連接要求會失敗。

> [!NOTE]
> tooaccess Azure SQL 資料庫從本機電腦，請確定 hello 網路和本機電腦上的防火牆允許 TCP 通訊埠 1433年上的傳出通訊。
> 

### <a name="connecting-from-azure"></a>從 Azure 連線
必須啟用 tooallow 應用程式，從 Azure tooconnect tooyour Azure 的 SQL server，Azure 的連線。 當從 Azure 應用程式嘗試 tooconnect tooyour 資料庫伺服器時，會驗證 hello 防火牆，允許 Azure 連線。 防火牆設定的開始和結束位址等於 too0.0.0.0 表示允許這些連接。 如果不允許 hello 連線嘗試，hello 要求不會到達 hello Azure SQL Database 伺服器。

> [!IMPORTANT]
> 這個選項會設定 hello 防火牆 tooallow 從 Azure 連接包括 hello 訂用帳戶的其他客戶的所有連線。 當選取此選項，請確定您的登入與使用者權限限制存取 tooonly 授權使用者。
> 

## <a name="creating-and-managing-firewall-rules"></a>建立和管理防火牆規則
您可以使用 hello 建立 hello 第一個伺服器層級防火牆設定[Azure 入口網站](https://portal.azure.com/)或以程式設計方式使用[Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx)， [Azure CLI](/cli/azure/sql/server/firewall-rule#create)，或使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn505712.aspx)。 後續的伺服器層級防火牆規則可以使用這些方法，以及透過 Transact-SQL 來建立和管理。 

> [!IMPORTANT]
> 資料庫層級防火牆規則只能使用 Transact-SQL 來建立和管理。 
>

tooimprove 效能考量，伺服器層級防火牆規則會暫時快取 hello 資料庫層級。 toorefresh hello 快取，請參閱[DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx)。 

> [!TIP]
> 您可以使用[SQL Database 稽核](sql-database-auditing.md)tooaudit 伺服器層級和資料庫層級防火牆變更。
>

### <a name="azure-portal"></a>Azure 入口網站

tooset hello Azure 入口網站中的伺服器層級防火牆規則，您可以 [進入 toohello 概觀] 頁面上的 Azure SQL 資料庫或 hello 概觀頁面 Azure Database 邏輯伺服器。

> [!TIP]
> 如需教學課程，請參閱[使用建立 DB hello Azure 入口網站](sql-database-get-started-portal.md)。
>

**從資料庫概觀頁面**

1. 按一下 tooset hello 資料庫概觀頁面上，從伺服器層級防火牆規則**設定伺服器防火牆**hello 工具列 hello 下列影像所示： hello**防火牆設定**hello SQL 頁面此時會開啟 資料庫伺服器。

      ![伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. 按一下**新增用戶端 IP** hello 工具列 tooadd hello 電腦的 IP 位址 hello 上您目前正在使用，然後按一下**儲存**。 系統便會為目前的 IP 位址建立伺服器層級防火牆規則。

      ![設定伺服器防火牆規則](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**從伺服器概觀頁面**

hello 伺服器隨即開啟，顯示您完全 hello 的概觀頁面格式的伺服器名稱 (例如**mynewserver20170403.database.windows.net**)，並提供進一步組態的選項。

1. 按一下 [tooset 伺服器概觀] 頁面上，從伺服器層級規則**防火牆**在底下設定 hello 下列影像中顯示 hello 左側功能表中： 

     ![邏輯伺服器概觀](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. 按一下**新增用戶端 IP** hello 工具列 tooadd hello 電腦的 IP 位址 hello 上您目前正在使用，然後按一下**儲存**。 系統便會為目前的 IP 位址建立伺服器層級防火牆規則。

     ![設定伺服器防火牆規則](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| 目錄檢視或預存程序 | 等級 | 說明 |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |伺服器 |顯示 hello 目前的伺服器層級防火牆規則 |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |伺服器 |建立或更新伺服器層級防火牆規則 |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |伺服器 |移除伺服器層級防火牆規則 |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |資料庫 |顯示 hello 目前的資料庫層級防火牆規則 |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |資料庫 |建立或更新 hello 資料庫層級防火牆規則 |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |資料庫 |移除資料庫層級防火牆規則 |


hello 下列範例檢閱 hello 現有規則，啟用 hello 伺服器 Contoso 上某個範圍的 IP 位址，並刪除防火牆規則：
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
接著，加入防火牆規則。
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

toodelete 伺服器層級防火牆規則，執行 hello sp_delete_firewall_rule 預存程序。 hello 下列範例會刪除名為 ContosoFirewallRule 的 hello 規則：
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | 等級 | 說明 |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |伺服器 |傳回目前伺服器層級防火牆規則 hello |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |伺服器 |建立新的伺服器層級防火牆規則 |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |伺服器 |更新現有的伺服器層級防火牆規則 hello 屬性 |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |伺服器 |移除伺服器層級防火牆規則 |


下列範例會設定使用 PowerShell 的伺服器層級防火牆規則的 hello:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> PowerShell 範例 hello 內容中的 快速入門，請參閱[建立資料庫-PowerShell](sql-database-get-started-powershell.md)和[建立單一資料庫，並使用 PowerShell 將防火牆規則設定](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>Azure CLI
| Cmdlet | 等級 | 說明 |
| --- | --- | --- |
| [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) | Hello hello 輸入 IP 位址範圍內的伺服器上建立防火牆規則 tooallow 存取 tooall SQL 資料庫。|
| [az sql server firewall delete](/cli/azure/sql/server/firewall-rule#delete)| 刪除防火牆規則。|
| [az sql server firewall list](/cli/azure/sql/server/firewall-rule#list)| 列出 hello 防火牆規則。|
| [az sql server firewall rule show](/cli/azure/sql/server/firewall-rule#show)| 顯示 hello 的防火牆規則的詳細資料。|
| [ax sql server firewall rule update](/cli/azure/sql/server/firewall-rule#update)| 更新防火牆規則。

下列範例會設定伺服器層級防火牆規則，使用 Azure CLI hello hello: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> 如需 Azure CLI 範例 hello 內容中的 快速入門，請參閱[建立 DDB-Azure CLI](sql-database-get-started-cli.md)和[建立單一資料庫，並設定使用 Azure CLI hello 的防火牆規則](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>REST API
| API | 等級 | 說明 |
| --- | --- | --- |
| [列出防火牆規則](https://msdn.microsoft.com/library/azure/dn505715.aspx) |伺服器 |顯示 hello 目前的伺服器層級防火牆規則 |
| [建立防火牆規則](https://msdn.microsoft.com/library/azure/dn505712.aspx) |伺服器 |建立或更新伺服器層級防火牆規則 |
| [設定防火牆規則](https://msdn.microsoft.com/library/azure/dn505707.aspx) |伺服器 |更新現有的伺服器層級防火牆規則 hello 屬性 |
| [刪除防火牆規則](https://msdn.microsoft.com/library/azure/dn505706.aspx) |伺服器 |移除伺服器層級防火牆規則 |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>伺服器層級防火牆規則與資料庫層級防火牆規則
問： 某個資料庫的使用者是否應該完全與另一個資料庫隔離？   
  如果是，請使用資料庫層級防火牆規則授與存取權。 這可避免使用伺服器層級防火牆規則，允許透過 hello 防火牆存取 tooall 資料庫，請減少 hello 深度防禦。   
 
問： 請勿在 hello IP 位址的使用者需要存取 tooall 資料庫嗎？   
  使用伺服器層級防火牆規則 tooreduce hello 數目的時間，您必須設定防火牆規則。   

問： 沒有 hello 人員或小組設定 hello 防火牆規則只可以存取透過 hello Azure 網站、 PowerShell 或 REST API 的 hello 嗎？   
  您必須使用伺服器層級防火牆規則。 資料庫層級防火牆規則只能使用 Transact-SQL 來設定。  

問： Hello 人員或小組設定 hello 防火牆規則禁止在 hello 資料庫層級有高層級的權限嗎？   
  使用伺服器層級防火牆規則。 設定資料庫層級防火牆規則使用 TRANSACT-SQL，至少需要`CONTROL DATABASE`hello 資料庫層級的權限。  

問： 是 hello 人員或小組設定或稽核 hello 的防火牆規則，集中管理防火牆規則的許多 (或許是 100) 的資料庫嗎？   
  此選項取決於您的需求和環境。 伺服器層級防火牆規則可能會更容易 tooconfigure，但是指令碼可以在 hello 資料庫層級設定的規則。 即使您使用伺服器層級防火牆規則，您可能還需要 tooaudit hello 資料庫防火牆規則，toosee，如果使用者具有`CONTROL`hello 資料庫的權限已經建立資料庫層級防火牆規則。   

問： 我是否可以混合使用伺服器層級和資料庫層級防火牆規則？   
  是。 部分使用者 (例如系統管理員) 可能需要伺服器層級防火牆規則。 其他使用者 (例如資料庫應用程式的使用者) 可能需要資料庫層級防火牆規則。   

## <a name="troubleshooting-hello-database-firewall"></a>疑難排解 hello database 防火牆
請考慮 hello 時存取 toohello Microsoft Azure SQL Database 服務未如預期般運作，下列點：

* **本機防火牆組態：**您的電腦可以存取 Azure SQL Database 之前，您可能需要 toocreate 防火牆例外狀況的 TCP 通訊埠 1433年電腦上。 如果您要進行 hello Azure 雲端界限內連線，您可能必須 tooopen 其他連接埠。 如需詳細資訊，請參閱 hello **SQL Database： 內部與外部**區段[ADO.NET 4.5 和 SQL Database 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。
* **網路位址轉譯 (NAT):**到期 tooNAT，使用您 SQL 資料庫可能會與您電腦的 IP 組態設定中所顯示的 hello IP 位址不同的電腦 tooconnect tooAzure hello IP 位址。 您的電腦是 tooview hello IP 位址使用 tooconnect tooAzure，登入 toohello 入口網站，並瀏覽 toohello**設定**hello 裝載您資料庫的伺服器上的索引標籤。 在 hello**允許的 IP 位址**區段，hello**目前的用戶端 IP 位址**隨即出現。 按一下**新增**toohello**允許的 IP 位址**tooallow 這部電腦 tooaccess hello 伺服器。
* **變更 toohello 允許清單有尚未生效：**可能會如往常般的五分鐘延遲變更 toohello Azure SQL Database 防火牆設定 tootake 效果。
* **hello 登入未獲授權，或使用不正確的密碼：** hello 連接 toohello Azure SQL Database 伺服器登入沒有 hello Azure SQL Database 伺服器的權限，或使用 hello 密碼不正確，遭到拒絕。 建立防火牆設定只提供連接 tooyour 伺服器; 機會 tooattempt 用戶端每個用戶端必須提供 hello 必要的安全性認證。 如需準備登入的詳細資訊，請參閱「管理 Azure SQL Database 中的資料庫、登入和使用者」。
* **動態 IP 位址：**如果您有使用動態 IP 位址的網際網路連線，並且在經由 hello 防火牆時遇到，您可以嘗試下列解決方案 hello 的其中一個：
  
  * 要求網際網路服務提供者 (ISP) hello IP 位址範圍指派 tooyour 用戶端電腦的存取 hello Azure SQL Database 伺服器，然後將 hello IP 位址範圍新增為防火牆規則。
  * 取得靜態 IP 位址改為您的用戶端電腦，然後將 hello IP 位址新增為防火牆規則。

## <a name="next-steps"></a>後續步驟

- 如需建立資料庫和伺服器層級防火牆規則的快速入門，請參閱[建立 Azure SQL Database](sql-database-get-started-portal.md)。
- 連接 tooan Azure SQL database 中的開放原始碼或協力廠商應用程式的說明，請參閱[快速入門用戶端的程式碼範例 tooSQL 資料庫](https://msdn.microsoft.com/library/azure/ee336282.aspx)。
- 如需其他連接埠的資訊，您可能需要 tooopen，請參閱 hello **SQL Database： 內部與外部**區段[ADO.NET 4.5 和 SQL Database 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)
- 如需 Azure SQL Database 安全性的概觀，請參閱[保護您的資料庫](sql-database-security-overview.md)

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
