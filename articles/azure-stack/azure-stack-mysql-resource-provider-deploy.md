---
title: "aaaUse MySQL 資料庫做為 Azure 堆疊上的 PaaS |Microsoft 文件"
description: "了解部署 hello MySQL 資源提供者，並提供 Azure 堆疊上以服務的 MySQL 資料庫"
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
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a>在 Microsoft Azure Stack 上使用 MySQL 資料庫


您可以在 Azure Stack 上部署 MySQL 資源提供者。 在您部署的 hello 資源提供者之後，您可以建立 MySQL 伺服器和資料庫，透過 Azure Resource Manager 部署範本，並做為服務提供 MySQL 資料庫。 網站上常用的 MySQL 資料庫支援許多網站平台。 例如，部署 hello 資源提供者之後, 您可以建立 WordPress 網站從 hello Azure Web 應用程式平台服務 (PaaS) 附加元件方式 Azure 堆疊。

toodeploy 沒有網際網路存取的系統上的 hello MySQL 提供者，您可以複製 hello 檔[mysql 連接器-net 6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa 本機共用，並提供該共用名稱，當系統提示您 （請參閱下方）。 您也必須安裝 hello Azure 和 Azure 堆疊 PowerShell 模組。


## <a name="mysql-server-resource-provider-adapter-architecture"></a>MySQL Server 資源提供者介面卡架構

hello 資源提供者是由三個元件所組成：

- **hello MySQL 資源提供者介面卡 VM**、 哪些是執行 hello 提供者服務的 Windows 虛擬機器。
- **hello 資源提供者本身**、 其處理佈建要求，會公開資料庫資源。
- **主控 MySQL Server 的伺服器**，其提供資料庫的容量，稱為主控伺服器。 

此版本不會再建立 MySQL 執行個體。 您必須加以建立及/或提供存取 tooexternal SQL 執行個體。 您可以瀏覽 hello [Azure 堆疊快速入門圖庫](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows)範例範本，可以為您建立 MySQL 伺服器或下載並部署從 hello Marketplace MySQL 伺服器。

## <a name="deploy-hello-resource-provider"></a>部署 hello 資源提供者

1. 如果您尚未這樣做，註冊您的開發套件，並下載 hello Windows Server 2016 Datacenter 可下載透過 Marketplace 管理 Eval 映像。 您也可以使用指令碼 toocreate [Windows Server 2016 映像](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image)。

2. [下載 hello MySQL 資源提供者二進位檔](https://aka.ms/azurestackmysqlrp)並將它解壓縮 hello 開發套件主機上。

3. 登入 toohello 開發套件主應用程式，並擷取 hello MySQL RP 安裝程式檔案 tooa 暫存目錄。

4. 擷取 hello Azure 堆疊根憑證，此程序的一部分建立自我簽署的憑證。 

    __選擇性：__如果您需要 tooprovide 您擁有，請準備 hello 憑證並複製 tooa 本機目錄，如果您想 toocustomize hello 憑證 （傳遞的 toohello 安裝指令碼）。 您需要下列 hello:

    a. *.dbadapter.\<地區\>.\<外部 FQDN\>的萬用字元憑證。 此憑證必須受到信任，例如會發出的憑證授權單位 （也就是 hello 信任鏈結必須存在而不需要中繼憑證）。（使用 hello 您在安裝期間提供明確 VM 名稱，可以使用單一站台憑證）。

    b. hello hello Azure 資源管理員用於您的 Azure 堆疊的執行個體的根憑證。 如果沒有找到，則將會擷取 hello 根憑證。

5. 開啟**新**提高權限的 PowerShell 主控台，然後變更 toohello 目錄解壓縮 hello 檔案的位置。 使用新的視窗 tooavoid 問題可能因不正確的 PowerShell 模組已經載入 hello 系統上。

6. 如果您已安裝任何版本的 hello AzureRm 或 1.2.9 或 1.2.10 以外 AzureStack PowerShell 模組，您將會提示的 tooremove 它們或 hello 安裝將不會繼續。 這包括 1.3 或更高版本。

7. 執行 DeployMySqlProvider.ps1。

此指令碼執行下列步驟：

* 如有必要，請下載相容版本的 Azure PowerShell。
* 下載 hello MySQL 連接器二進位 （這可以提供離線）。
* 上傳 hello 憑證和所有其他成品 tooan 堆疊 Azure 儲存體帳戶。
* 發佈圖庫套件，以便您可以部署到 hello 圖庫的 MySQL 資料庫。
* 部署主控資源提供者的虛擬機器 (VM)。
* 註冊對應 tooyour 資源提供者 VM 的本機 DNS 記錄。
* 註冊您的資源提供者以 hello 本機的 Azure 資源管理員。

請至少指定 hello hello 命令列上的必要的參數，或如果您執行不含任何參數，則提示的 tooenter 它們。 

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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a>DeployMySqlProvider.ps1 參數

您可以在 hello 命令列中指定這些參數。 如果您不這麼做，或任何參數驗證失敗，系統會提示您 tooprovide hello 必要的。

| 參數名稱 | 說明 | 註解或預設值 |
| --- | --- | --- |
| **DirectoryTenantID** | hello Azure 或 ADFS 目錄識別碼 (guid) | _必要_ |
| **ArmEndpoint** | hello Azure 堆疊管理 Azure 資源管理員端點 | _必要_ |
| **TenantArmEndpoint** | hello Azure 堆疊租用戶 Azure 資源管理員端點 | _必要_ |
| **AzCredential** | Azure 的堆疊服務系統管理員帳戶認證 (使用 hello 與您用於部署 Azure 堆疊使用相同帳戶) | _必要_ |
| **VMLocalCredential** | hello hello MySQL 資源提供者 VM 的本機系統管理員帳戶 | _必要_ |
| **ResourceGroupName** | 此指令碼所建立的 hello 項目的資源群組 |  _必要_ |
| **VmName** | Hello VM 保存名稱 hello 資源提供者 |  _必要_ |
| **AcceptLicense** | 略過 hello 提示 tooaccept hello GPL 授權規範 (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html) | |
| **DependencyFilesLocalPath** | 包含本機共用路徑 tooa [mysql 連接器-net 6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi)。 如果您提供它們，也必須將憑證檔案放在這個目錄。 | _選用_ |
| **DefaultSSLCertificatePassword** | hello hello.pfx 憑證的密碼 | _必要_ |
| **MaxRetryCount** | 失敗時會重試每個作業 | 2 |
| **RetryDuration** | 重試之間以秒為單位的逾時 | 120 |
| **解除安裝** | 移除 hello 資源提供者 | 否 |
| **DebugMode** | 防止在失敗時自動清除 | 否 |


根據 hello 系統效能和下載速度，安裝可能需要一些為 20 分鐘或長時間為幾小時的時間。 如果無法使用 hello MySQLAdapter 刀鋒視窗，您必須重新整理 hello 系統管理入口網站。

> [!NOTE]
> 如果 hello 安裝花 90 分鐘以上，它可能會失敗，您會看到失敗訊息囉 」 畫面上和 hello 記錄檔中。 hello 部署會重試從 hello 失敗的步驟。 系統不符合 hello 建議的記憶體及核心規格可能不是能 toodeploy hello MySQL RP。


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a>提供藉由連接 tooa MySQL 主控伺服器的容量

1. 登入 toohello 堆疊 Azure 入口網站為服務管理員。

2. 按一下**資源提供者** &gt; **MySQLAdapter** &gt; **主控伺服器** &gt; **+新增**。

    hello **MySQL 主控伺服器**刀鋒視窗是您可以在此連接 hello MySQL Server 資源提供者 tooactual 的執行個體的 MySQL Server 做為 hello 資源提供者的後端。

    ![主控伺服器](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. Hello 表單中填入 hello MySQL 伺服器執行個體的連接詳細資料。 提供 hello 完整的網域名稱 (FQDN) 或有效的 IPv4 位址，而不 hello 簡短 VM 名稱。 這項安裝不會再提供預設 MySQL 執行個體。 hello 提供大小可協助管理 hello 資料庫容量 hello 資源提供者。 它應該關閉 toohello hello 資料庫伺服器的實體容量。

    > [!NOTE]
    > 只要的 hello 租用戶和管理 Azure 資源管理員，就可以存取 hello MySQL 執行個體，就可以放受控制的 hello 資源提供者。 hello MySQL 執行個體__必須__配置以獨佔方式 toohello RP。

4. 當您新增伺服器，您必須將它們指派 tooa 新的或現有 SKU tooallow 差異化的服務供應項目。 例如，您可以提供資料庫容量和自動備份企業執行個體，請保留各個部門高效能伺服器，等 hello SKU 名稱應反映 hello 屬性，以便租用戶可以將其資料庫適當地而且不應該有 SKU 中的所有主控伺服器 hello 相同的功能。

    ![建立 MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
Sku 可以佔用 tooan 小時 toobe hello 入口網站中顯示。 您無法建立資料庫，直到建立 SKU 的 hello。


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a>建立您第一次的 MySQL 資料庫 tootest 部署


1. 登入 toohello 堆疊 Azure 入口網站為服務系統管理員。

2. 按一下 hello **+ 新增**按鈕&gt;**資料 + 儲存體** &gt; **MySQL Database （預覽版）**。

3. 填寫表單 hello hello 資料庫詳細資料。

    ![建立測試 MySQL 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. 選取 SKU。

    ![選取 SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. 建立登入設定。 可重複使用 hello 登入設定，或建立一個新。 這包含 hello 使用者名稱和密碼 hello 資料庫。

    ![建立新的資料庫登入](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    hello 連接字串包含 hello 實際的資料庫伺服器名稱。 請將它複製從 hello 入口網站。

    ![取得 hello 連接字串 hello MySQL 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> hello hello 使用者名稱長度不得超過 32 個字元並 MySQL 5.7 或較早版本的 16 個字元。 這是 hello MySQL 實作 (implementation) 的限制。


## <a name="add-capacity"></a>新增容量

新增額外的 MySQL 伺服器 hello Azure 堆疊入口網站中新增容量。 如果您想 toouse MySQL 的另一個執行個體，請按一下**資源提供者** &gt; **MySQLAdapter** &gt; **MySQL 主控伺服器** &gt; **+ 加入**。


## <a name="making-mysql-databases-available-tootenants"></a>可用的 tootenants 提高 MySQL 資料庫
建立計劃和優惠 toomake 可用的 MySQL 資料庫供租用戶。 新增 hello Microsoft.MySqlAdapter 服務，將配額、 等等。

![建立計劃和優惠 tooinclude 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a>移除 hello MySQL 配接器資源提供者

tooremove hello 資源提供者，務必 toofirst 移除任何相依性。

1. 確定您擁有 hello 原始部署套件下載這個版本的 hello 資源提供者。

2. 從 hello 資源提供者 （這不會刪除 hello 資料），必須刪除所有租用戶資料庫。 應該執行此作業由 hello 租用戶本身。

3. 租用戶必須從 hello 命名空間移除註冊。

4. 系統管理員必須先刪除主控伺服器 hello MySQL 配接器從 hello

5. 系統管理員必須先刪除任何參考 hello MySQL 配接器的計劃。

6. 系統管理員必須先刪除任何配額相關聯的 toohello MySQL 配接器。

7. 重新執行具有 hello 部署指令碼 hello-解除安裝參數，Azure 資源管理員端點、 DirectoryTenantID 和 hello 服務系統管理員帳戶的認證。




## <a name="next-steps"></a>後續步驟


請嘗試其他[PaaS 服務](azure-stack-tools-paas-services.md)像 hello [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)和 hello[應用程式服務資源提供者](azure-stack-app-service-overview.md)。
