---
title: "SQL Database 連線架構 aaaAzure |Microsoft 文件"
description: "本文件說明 hello Azure SQLDB 連線架構從 Azure 內部或從 Azure 外部。"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Azure SQL Database 連線架構 

本文說明 hello Azure SQL Database 連線架構，並說明 hello 不同元件的 toodirect 流量 tooyour Azure SQL Database 執行個體的運作方式。 與在 Azure 中從連接的用戶端及連線從 Azure 外部的用戶端，這些 Azure SQL Database 連接元件函式 toodirect 網路流量 toohello Azure 資料庫。 本文也提供指令碼範例 toochange 連線進行的方式，以及 hello 考量相關 toochanging hello 預設連線設定。 如果閱讀本文之後有任何問題，請透過 dmalik@microsoft.com 來連絡 Dhruv。 

## <a name="connectivity-architecture"></a>連線架構

下列圖表中的 hello 提供 hello Azure SQL Database 連線架構的高階概觀。 

![架構概觀](./media/sql-database-connectivity-architecture/architecture-overview.png)


hello 下列步驟描述如何連接是透過 hello Azure SQL Database 軟體負載平衡器 (SLB) 和 hello Azure SQL Database 閘道建立的 tooan Azure SQL database。

- 在 Azure 或 Azure 外部的用戶端連線 toohello SLB，其具有公用 IP 位址和通訊埠 1433年上接聽。
- hello SLB 指示流量 toohello Azure SQL Database 的閘道。
- hello 閘道重新導向 hello 流量 toohello 正確的 proxy 中介軟體。
- hello proxy 中介軟體重新導向 hello 流量 toohello 適當 Azure SQL database。

> [!IMPORTANT]
> 每個元件具有分散式阻斷服務 (DDoS) 內建在 hello 網路和 hello 應用程式層的保護。
>

## <a name="connectivity-from-within-azure"></a>從 Azure 內部連線

如果您從 Azure 內部連線，該連線預設的連線原則為 [重新導向]。 原則的**重新導向**表示 hello TCP 工作階段後建立的 toohello Azure SQL database 的連接，hello 用戶端工作階段則會重新導向的變更 toohello 目的地虛擬 ip 從 toohello proxy 中介軟體hello Azure SQL Database 閘道 toothat hello proxy 中介軟體。 此後，所有後續封包流程直接透過 hello proxy 中介軟體，並略過 hello Azure SQL Database 的閘道。 hello 下列圖表說明此流量。

![架構概觀](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>從 Azure 外部連線

如果您從 Azure 外部連線，該連線預設的連線原則為 [Proxy]。 原則的**Proxy**表示透過 hello Azure SQL Database 閘道建立 hello TCP 工作階段，所有後續封包流程透過 hello 閘道。 hello 下列圖表說明此流量。

![架構概觀](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Azure SQL Database 閘道 IP 位址

tooconnect tooan Azure SQL database 與內部部署資源，您會需要 tooallow 輸出網路流量 toohello SQL Azure 閘道為您的 Azure 區域。 在 Proxy 模式中，這是 hello 預設值，從內部部署資源連接時連接時，您的連接只能移到透過 hello 閘道。

下表將列出 hello hello 主要和次要的所有資料區的 hello Azure SQL Database 閘道的 Ip。 對於某些區域，會有兩個 IP 位址。 在這些區域，hello 主要 IP 位址是 hello 目前閘道 IP 位址 hello 而且 hello 第二個 IP 位址的容錯移轉 IP 位址。 hello 容錯移轉的位址是 hello 位址 toowhich 我們可能會移動伺服器 tookeep hello 服務的可用性高。 這些區域中，我們建議您允許輸出 tooboth hello IP 位址。 hello 第二個 IP 位址由 Microsoft 所擁有並不會接聽任何服務之前啟動 Azure SQL Database tooaccept 連接。

| 區域名稱 | 主要 IP 位址 | 次要 IP 位址 |
| --- | --- |--- |
| 澳洲東部 | 191.238.66.109 | 13.75.149.87 |
| 澳大利亞東南部 | 191.239.192.109 | 13.73.109.251 |
| 巴西南部 | 104.41.11.5 | |    
| 加拿大中部 | 40.85.224.249 | |    
| 加拿大東部 | 40.86.226.166 | |
| 美國中部 | 23.99.160.139 | 13.67.215.62 |
| 東亞 | 191.234.2.139 | 52.175.33.150 |
| 美國東部 1 | 191.238.6.43 | 40.121.158.30 |
| 美國東部 2 | 191.239.224.107 | 40.79.84.180 |
| 印度中部 | 104.211.96.159  | |   
| 印度南部 | 104.211.224.146  | |
| 印度西部 | 104.211.160.80 | |
| 日本東部 | 191.237.240.43 | 13.78.61.196 |
| 日本西部 | 191.238.68.11 | 104.214.148.156 |
| 韓國中部 | 52.231.32.42 | |
| 韓國南部 | 52.231.200.86 |  |
| 美國中北部 | 23.98.55.75 | 23.96.178.199 |
| 北歐 | 191.235.193.75 | 40.113.93.91 |
| 美國中南部 | 23.98.162.75 | 13.66.62.124 |
| 東南亞 | 23.100.117.95 | 104.43.15.0 |
| 英國北部 | 13.87.97.210 | |
| 英國南部 1 | 51.140.184.11 | |    
| 英國南部 2 | 13.87.34.7 | |
| 英國西部 | 51.141.8.11  | |
| 美國中西部 | 13.78.145.25 | |
| 西歐 | 191.237.232.75 | 40.68.37.158 |
| 美國西部 1 | 23.99.34.75 | 104.42.238.205 |
| 美國西部 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>變更 Azure SQL Database 連線原則

toochange hello Azure SQL Database 伺服器，請使用 hello Azure SQL Database 連線原則[REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)。 

- 如果您連接的原則設定太**Proxy**，所有的網路封包流程透過 hello Azure SQL Database 的閘道。 此設定，您需要 tooallow 輸出 tooonly hello Azure SQL Database 閘道 IP。 和 [重新導向] 設定相比，使用 [Proxy] 設定會較為延遲。 
- 如果您連接的原則設定**重新導向**，所有的網路封包直接傳送 toohello 中介軟體 proxy。 此設定，您需要 tooallow 輸出 toomultiple Ip。 

## <a name="script-toochange-connection-settings"></a>指令碼 toochange 連線設定

> [!IMPORTANT]
> 此指令碼需要 hello [Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。
>

hello 下列 PowerShell 指令碼會示範如何 toochange hello 連線原則。

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>後續步驟

- 如需如何 toochange hello Azure SQL Database 伺服器的 Azure SQL Database 連線原則資訊，請參閱[建立或更新伺服器的連線原則使用 hello REST API](https://msdn.microsoft.com/library/azure/mt604439.aspx)。
- 如需使用 ADO.NET 4.5 或更新版本用戶端之 Azure SQL Database 連接行為的詳細資訊，請參閱 [ADO.NET 4.5 超過 1433以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。
- 如需一般應用程式開發概觀的資訊，請參閱 [SQL Database 應用程式開發概觀](sql-database-develop-overview.md)。
