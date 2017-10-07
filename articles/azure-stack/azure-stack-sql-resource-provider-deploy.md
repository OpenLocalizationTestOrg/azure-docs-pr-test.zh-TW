---
title: "aaaUsing SQL Azure 堆疊上的資料庫 |Microsoft 文件"
description: "了解您如何部署 Azure 堆疊和 hello 快速步驟 toodeploy hello SQL Server 資源提供者介面卡上以服務 SQL 資料庫"
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a>在 Microsoft Azure Stack 上使用 SQL 資料庫


為 Azure 堆疊的服務使用 hello SQL Server 資源提供者介面卡 tooexpose SQL 資料庫。 在安裝 hello 資源提供者，並將它連接 tooone 或多個 SQL Server 執行個體之後，您和您的使用者可以建立雲端原生應用程式、 以 SQL 為基礎的網站和工作負載為基礎而不需要 tooprovision 虛擬機器的 SQL 資料庫機器 (VM) 每次主控 SQL Server。

hello 資源提供者不支援的所有 hello 資料庫管理功能[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 例如，不支援彈性資料庫集區和 hello 能力 tooscale 資料庫效能。 hello API 與不相容的 SQL DB。


## <a name="sql-server-resource-provider-adapter-architecture"></a>SQL Server 資源提供者配接器架構
hello 資源提供者不基礎，也不提供所有 hello 資料庫管理 Azure SQL Database 的功能。 例如，彈性資料庫集區和 hello 能力 toodial 增加和減少的資料庫效能會自動將無法使用。 不過，hello 資源提供者支援類似建立、 讀取、 更新和刪除 (CRUD) 作業。

hello 資源提供者是由三個元件所組成：

- **hello SQL 資源提供者介面卡 VM**、 哪些是執行 hello 提供者服務的 Windows 虛擬機器。
- **hello 資源提供者本身**、 其處理佈建要求，會公開資料庫資源。
- **主控 SQL Server 的伺服器**，它提供資料庫的容量，稱為主控伺服器。 

此版本不會再建立 SQL 執行個體。 您必須建立一個 （或以上） 和 （或) 提供存取 tooexternal SQL 執行個體。 有許多選項可用 tooyou hello 中包括範本[Azure 堆疊快速入門圖庫](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows)和 Marketplace 項目。 

>[!NOTE]
如果您已下載的任何 SQL Marketplace 項目，請確定您也可以下載 hello SQL IaaS 延伸模組，或這些不會將部署。


## <a name="deploy-hello-resource-provider"></a>部署 hello 資源提供者

1. 如果您尚未這樣做，註冊您的開發套件，並下載 hello 可下載透過 Marketplace 管理的 Windows Server 2016 評估版影像。 您也可以使用指令碼 toocreate [Windows Server 2016 映像](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image)。 不再需要.NET 3.5 hello 執行階段。

2. [下載 hello SQL 資源提供者二進位檔](https://aka.ms/azurestacksqlrp)並將它解壓縮 hello 開發套件主機上。

3. 登入 toohello 開發套件主機，然後將解壓縮 hello SQL RP 安裝程式檔案 tooa 暫存目錄。

4. 擷取 hello Azure 堆疊根憑證，此程序的一部分建立自我簽署的憑證。 

    __選擇性：__如果您需要 tooprovide 您擁有，請準備 hello 憑證並複製 tooa 本機目錄，如果您想 toocustomize hello 憑證 （傳遞的 toohello 安裝指令碼）。 您需要下列憑證 hello:

    a. *.dbadapter.\<地區\>.\<外部 FQDN\>的萬用字元憑證。 此憑證必須受到信任，例如會發出的憑證授權單位 （也就是 hello 信任鏈結必須存在而不需要中繼憑證）。（使用 hello 您在安裝期間提供明確 VM 名稱，可以使用單一站台憑證）。

    b. hello hello Azure 資源管理員用於您的 Azure 堆疊的執行個體的根憑證。 如果沒有找到，則將會擷取 hello 根憑證。


5. 開啟**新**提高權限的 PowerShell 主控台，然後變更 toohello 目錄解壓縮 hello 檔案的位置。 使用新的視窗 tooavoid 問題可能因不正確的 PowerShell 模組已經載入 hello 系統上。

6. 如果您已安裝任何版本的 hello AzureRm 或 1.2.9 或 1.2.10 以外 AzureStack PowerShell 模組，您將會提示的 tooremove 它們或 hello 安裝將不會繼續。 這包括 1.3 或更高版本。

7. 執行 hello DeploySqlProvider.ps1 下面所列的 hello 參數的指令碼。

hello 指令碼執行下列步驟：

* 如有必要，請下載相容版本的 Azure PowerShell。
* 上傳 hello 憑證和其他成品 tooa 儲存體帳戶的 Azure 堆疊上。
* 發佈圖庫套件，以便您可以部署到 hello 組件庫的 SQL 資料庫。
* 部署使用 hello Windows Server 2016 映像步驟 1 中建立的 VM 並安裝 hello 資源提供者。
* 註冊對應 tooyour 資源提供者 VM 的本機 DNS 記錄。
* 註冊您的資源提供者以 hello 本機 Azure 資源管理員 （租用戶和系統管理員）。

> [!NOTE]
> 如果 hello 安裝花 90 分鐘以上，它可能會失敗並囉 」 畫面及 hello 記錄檔，請參閱失敗訊息但 hello 部署重試一次從 hello 失敗的步驟。 系統不符合 hello 建議的記憶體及核心規格可能不是能 toodeploy hello SQL RP。
>

以下是您可以從 hello PowerShell 執行的範例提示 （但視需要變更 hello 帳戶資訊和入口網站端點）：

```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a>DeploySqlProvider.ps1 參數
您可以在 hello 命令列中指定這些參數。 如果您不這麼做，或任何參數驗證失敗，系統會提示您 tooprovide hello 必要的。

| 參數名稱 | 說明 | 註解或預設值 |
| --- | --- | --- |
| **DirectoryTenantID** | hello Azure 或 ADFS 目錄識別碼 (guid)。 | _必要_ |
| **AzCredential** | Hello Azure 堆疊服務系統管理員帳戶提供 hello 認證。 您必須使用相同認證所使用的部署 Azure 堆疊 hello）。 | _必要_ |
| **VMLocalCredential** | 定義 hello hello hello SQL 資源提供者 VM 的本機系統管理員帳戶的認證。 這個密碼也會用於 hello SQL **sa**帳戶。 | _必要_ |
| **ResourceGroupName** | 定義資源群組的名稱，此指令碼所建立的項目將儲存在此資源群組中。 例如，*SqlRPRG*。 |  _必要_ |
| **VmName** | 定義哪個 tooinstall hello 資源提供者的 hello hello 虛擬機器名稱。 例如，*SqlVM*。 |  _必要_ |
| **DependencyFilesLocalPath** | 您的憑證檔案也必須放在這個目錄中。 | _選用_ |
| **DefaultSSLCertificatePassword** | hello hello.pfx 憑證的密碼 | _必要_ |
| **MaxRetryCount** | 定義您要讓 tooretry 每個作業是否有多少次失敗。| 2 |
| **RetryDuration** | 定義 hello 重試之間，以秒為單位的逾時。 | 120 |
| **解除安裝** | 移除 hello 資源提供者和所有相關聯的資源 （請參閱下面的附註） | 否 |
| **DebugMode** | 防止在失敗時自動清除 | 否 |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a>確認 hello 部署使用 hello Azure 堆疊入口網站

> [!NOTE]
>  Hello 安裝指令碼完成之後，您將需要 toorefresh hello 入口 toosee hello 管理刀鋒視窗。


1. 在 hello 主控台 VM 桌面上，按一下**Microsoft Azure 堆疊入口網站**toohello 入口網站以 hello 服務系統管理員身分登入。

2. 確認 hello 部署成功。 按一下**資源群組**&gt;按一下 hello 您所使用的資源群組，然後確定 hello 刀鋒視窗 （上半部） 讀取該 hello essentials 部分**_日期_（成功）**.

      ![確認部署的 hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a>藉由連接 tooa 主控 SQL server 提供的容量

1. Toohello Azure 堆疊系統管理員入口網站管理員身分登入服務

2. 建立 SQL 虛擬機器 (除非您已經有 SQL 虛擬機器)。 「Marketplace 管理」提供一些用於部署 SQL VM 的選項。

3. 按一下 [資源提供者] &gt;[SQLAdapter] &gt;[主控伺服器] &gt;[+新增]。

    hello **SQL 主控伺服器**刀鋒視窗是您可以在此連接 hello SQL Server 資源提供者 tooactual SQL Server 執行個體，做為 hello 資源提供者的後端。

    ![主控伺服器](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. Hello 表單中填入 hello 連接詳細資料，您的 SQL Server 執行個體。

    ![新的主控伺服器](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > 只要的 hello 租用戶和管理 Azure 資源管理員，就可以存取 hello SQL 執行個體，就可以放受控制的 hello 資源提供者。 hello SQL 執行個體__必須__配置以獨佔方式 toohello RP。

5. 當您新增伺服器，您必須將它們指派 tooa 新的或現有 SKU toodifferentiate 服務供應項目。 例如，您可以提供資料庫容量和自動備份的 SQL Enterprise 執行個體，請保留各個部門高效能伺服器，等 hello SKU 名稱應反映 hello 屬性，以便租用戶可以將其資料庫適當地而且不應該有 SKU 中的所有主控伺服器 hello 相同的功能。

    例如：

    ![SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
Sku 可以佔用 tooan 小時 toobe hello 入口網站中顯示。 您無法建立資料庫，直到建立 SKU 的 hello。


## <a name="create-your-first-sql-database-tootest-your-deployment"></a>建立您第一次的 SQL 資料庫 tootest 部署

1. 登入 toohello 堆疊 Azure 系統管理入口網站為服務系統管理員。

2. 按一下 [+新增] &gt;[資料+儲存體] &gt;[SQL Server 資料庫 (預覽)] &gt;[新增]。

3. 請填寫 hello 表單的資料庫詳細資料，包括**資料庫名稱**，**大小上限**，並變更視 hello 其他參數。 您會為您的資料庫要求 toopick SKU。 當主控伺服器加入時，會指派給他們的 SKU，會建立資料庫的主控伺服器 hello SKU 構成該集區中。

    ![新資料庫](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. 填寫 hello 登入設定：**資料庫登入**，和**密碼**。 這是針對只存取 toothis 資料庫所建立的 SQL 驗證認證。 hello 登入使用者名稱必須是全域唯一的。 建立新的登入設定或選取現有的設定。 您可以重複使用登入設定，如使用其他資料庫 hello 相同 SKU。

    ![建立新的資料庫登入](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. 送出 hello 表單，並等候 hello 部署 toocomplete。

    在 hello 產生刀鋒視窗中，會發現 hello 「 連接字串 」 欄位。 您可以在 Azure Stack 中，於需要 SQL Server 存取權的任何應用程式 (例如 Web 應用程式) 中使用該字串。

    ![擷取 hello 連接字串](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a>新增容量

新增其他的 SQL 主控 hello Azure 堆疊入口網站中新增容量，並將它們關聯適當的 SKU。 如果您想 toouse 另一個 SQL 執行個體而不是 hello hello 提供者 VM 上所安裝，請按一下**資源提供者** &gt; **SQLAdapter** &gt; **SQL 裝載伺服器** &gt; **+ 加入**。

## <a name="making-sql-databases-available-tootenants"></a>提高 SQL 資料庫可用 tootenants

建立租用戶計畫與優惠 toomake 可用的 SQL 資料庫。 您必須建立計劃、 加入 hello Microsoft.SqlAdapter 服務 toohello 計劃，加入現有的配額，或另外新建一個。 如果您建立配額時，您可以指定 hello 容量 tooallow hello 租用戶。
    ![建立計劃和優惠 tooinclude 資料庫](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)

## <a name="tenant-usage-of-hello-resource-provider"></a>Hello 資源提供者的租用戶使用量

透過 hello 租用戶入口網站體驗提供自助服務資料庫。

## <a name="removing-hello-sql-adapter-resource-provider"></a>移除 hello SQL 配接器資源提供者

在訂單 tooremove hello 資源提供者，務必 toofirst 移除任何相依性。

1. 確定您擁有 hello 原始部署套件下載這個版本的 hello 資源提供者。

2. 從 hello 資源提供者 （這不會刪除 hello 資料），必須刪除所有租用戶資料庫。 應該執行此作業由 hello 租用戶本身。

3. 系統管理員必須先刪除主控伺服器 hello SQL 配接器從 hello

4. 系統管理員必須先刪除任何參考 hello SQL 配接器的計劃。

5. 系統管理員必須先刪除任何 Sku 與配額 toohello SQL 配接器。

6. 重新執行具有 hello 部署指令碼 hello-解除安裝參數，Azure 資源管理員端點、 DirectoryTenantID 和 hello 服務系統管理員帳戶的認證。



## <a name="next-steps"></a>後續步驟


請嘗試其他[PaaS 服務](azure-stack-tools-paas-services.md)像 hello [MySQL Server 資源提供者](azure-stack-mysql-resource-provider-deploy.md)和 hello[應用程式服務資源提供者](azure-stack-app-service-overview.md)。
