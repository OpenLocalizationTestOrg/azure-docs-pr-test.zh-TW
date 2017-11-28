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
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="3e3d8-103">在 Microsoft Azure Stack 上使用 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="3e3d8-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="3e3d8-104">您可以在 Azure Stack 上部署 MySQL 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="3e3d8-105">在您部署的 hello 資源提供者之後，您可以建立 MySQL 伺服器和資料庫，透過 Azure Resource Manager 部署範本，並做為服務提供 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-105">After you deploy hello resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="3e3d8-106">網站上常用的 MySQL 資料庫支援許多網站平台。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="3e3d8-107">例如，部署 hello 資源提供者之後, 您可以建立 WordPress 網站從 hello Azure Web 應用程式平台服務 (PaaS) 附加元件方式 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-107">As an example, after you deploy hello resource provider, you can create WordPress websites from hello Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="3e3d8-108">toodeploy 沒有網際網路存取的系統上的 hello MySQL 提供者，您可以複製 hello 檔[mysql 連接器-net 6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa 本機共用，並提供該共用名稱，當系統提示您 （請參閱下方）。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-108">toodeploy hello MySQL provider on a system that does not have internet access, you can copy hello file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="3e3d8-109">您也必須安裝 hello Azure 和 Azure 堆疊 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-109">You must also install hello Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="3e3d8-110">MySQL Server 資源提供者介面卡架構</span><span class="sxs-lookup"><span data-stu-id="3e3d8-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="3e3d8-111">hello 資源提供者是由三個元件所組成：</span><span class="sxs-lookup"><span data-stu-id="3e3d8-111">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="3e3d8-112">**hello MySQL 資源提供者介面卡 VM**、 哪些是執行 hello 提供者服務的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-112">**hello MySQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="3e3d8-113">**hello 資源提供者本身**、 其處理佈建要求，會公開資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-113">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="3e3d8-114">**主控 MySQL Server 的伺服器**，其提供資料庫的容量，稱為主控伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="3e3d8-115">此版本不會再建立 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="3e3d8-116">您必須加以建立及/或提供存取 tooexternal SQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-116">You must create them and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="3e3d8-117">您可以瀏覽 hello [Azure 堆疊快速入門圖庫](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows)範例範本，可以為您建立 MySQL 伺服器或下載並部署從 hello Marketplace MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-117">You can visit hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from hello Marketplace.</span></span>

## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="3e3d8-118">部署 hello 資源提供者</span><span class="sxs-lookup"><span data-stu-id="3e3d8-118">Deploy hello resource provider</span></span>

1. <span data-ttu-id="3e3d8-119">如果您尚未這樣做，註冊您的開發套件，並下載 hello Windows Server 2016 Datacenter 可下載透過 Marketplace 管理 Eval 映像。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-119">If you have not already done so, register your development kit and download hello Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="3e3d8-120">您也可以使用指令碼 toocreate [Windows Server 2016 映像](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image)。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-120">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="3e3d8-121">[下載 hello MySQL 資源提供者二進位檔](https://aka.ms/azurestackmysqlrp)並將它解壓縮 hello 開發套件主機上。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-121">[Download hello MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="3e3d8-122">登入 toohello 開發套件主應用程式，並擷取 hello MySQL RP 安裝程式檔案 tooa 暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-122">Sign in toohello development kit host, and extract hello MySQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="3e3d8-123">擷取 hello Azure 堆疊根憑證，此程序的一部分建立自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-123">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="3e3d8-124">__選擇性：__如果您需要 tooprovide 您擁有，請準備 hello 憑證並複製 tooa 本機目錄，如果您想 toocustomize hello 憑證 （傳遞的 toohello 安裝指令碼）。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-124">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="3e3d8-125">您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="3e3d8-125">You need hello following:</span></span>

    <span data-ttu-id="3e3d8-126">a.</span><span class="sxs-lookup"><span data-stu-id="3e3d8-126">a.</span></span> <span data-ttu-id="3e3d8-127">*.dbadapter.\<地區\>.\<外部 FQDN\>的萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="3e3d8-128">此憑證必須受到信任，例如會發出的憑證授權單位 （也就是 hello 信任鏈結必須存在而不需要中繼憑證）。（使用 hello 您在安裝期間提供明確 VM 名稱，可以使用單一站台憑證）。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="3e3d8-129">b.</span><span class="sxs-lookup"><span data-stu-id="3e3d8-129">b.</span></span> <span data-ttu-id="3e3d8-130">hello hello Azure 資源管理員用於您的 Azure 堆疊的執行個體的根憑證。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-130">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="3e3d8-131">如果沒有找到，則將會擷取 hello 根憑證。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-131">If it is not found, hello root certificate will be retrieved.</span></span>

5. <span data-ttu-id="3e3d8-132">開啟**新**提高權限的 PowerShell 主控台，然後變更 toohello 目錄解壓縮 hello 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-132">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="3e3d8-133">使用新的視窗 tooavoid 問題可能因不正確的 PowerShell 模組已經載入 hello 系統上。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-133">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="3e3d8-134">如果您已安裝任何版本的 hello AzureRm 或 1.2.9 或 1.2.10 以外 AzureStack PowerShell 模組，您將會提示的 tooremove 它們或 hello 安裝將不會繼續。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-134">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="3e3d8-135">這包括 1.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="3e3d8-136">執行 DeployMySqlProvider.ps1。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="3e3d8-137">此指令碼執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3e3d8-137">This script performs these steps:</span></span>

* <span data-ttu-id="3e3d8-138">如有必要，請下載相容版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="3e3d8-139">下載 hello MySQL 連接器二進位 （這可以提供離線）。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-139">Download hello MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="3e3d8-140">上傳 hello 憑證和所有其他成品 tooan 堆疊 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-140">Upload hello certificate and all other artifacts tooan Azure Stack storage account.</span></span>
* <span data-ttu-id="3e3d8-141">發佈圖庫套件，以便您可以部署到 hello 圖庫的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-141">Publish gallery packages so that you can deploy MySQL databases through hello gallery.</span></span>
* <span data-ttu-id="3e3d8-142">部署主控資源提供者的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="3e3d8-143">註冊對應 tooyour 資源提供者 VM 的本機 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-143">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="3e3d8-144">註冊您的資源提供者以 hello 本機的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-144">Register your resource provider with hello local Azure Resource Manager.</span></span>

<span data-ttu-id="3e3d8-145">請至少指定 hello hello 命令列上的必要的參數，或如果您執行不含任何參數，則提示的 tooenter 它們。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-145">Either specify at least hello required parameters on hello command line, or, if you run without any parameters, you are prompted tooenter them.</span></span> 

<span data-ttu-id="3e3d8-146">以下是您可以從 hello PowerShell 執行的範例提示 （但視需要變更 hello 帳戶資訊和入口網站端點）：</span><span class="sxs-lookup"><span data-stu-id="3e3d8-146">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>


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

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="3e3d8-147">DeployMySqlProvider.ps1 參數</span><span class="sxs-lookup"><span data-stu-id="3e3d8-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="3e3d8-148">您可以在 hello 命令列中指定這些參數。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-148">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="3e3d8-149">如果您不這麼做，或任何參數驗證失敗，系統會提示您 tooprovide hello 必要的。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-149">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="3e3d8-150">參數名稱</span><span class="sxs-lookup"><span data-stu-id="3e3d8-150">Parameter Name</span></span> | <span data-ttu-id="3e3d8-151">說明</span><span class="sxs-lookup"><span data-stu-id="3e3d8-151">Description</span></span> | <span data-ttu-id="3e3d8-152">註解或預設值</span><span class="sxs-lookup"><span data-stu-id="3e3d8-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3e3d8-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="3e3d8-154">hello Azure 或 ADFS 目錄識別碼 (guid)</span><span class="sxs-lookup"><span data-stu-id="3e3d8-154">hello Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="3e3d8-155">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-155">_required_</span></span> |
| <span data-ttu-id="3e3d8-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-156">**ArmEndpoint**</span></span> | <span data-ttu-id="3e3d8-157">hello Azure 堆疊管理 Azure 資源管理員端點</span><span class="sxs-lookup"><span data-stu-id="3e3d8-157">hello Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="3e3d8-158">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-158">_required_</span></span> |
| <span data-ttu-id="3e3d8-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="3e3d8-160">hello Azure 堆疊租用戶 Azure 資源管理員端點</span><span class="sxs-lookup"><span data-stu-id="3e3d8-160">hello Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="3e3d8-161">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-161">_required_</span></span> |
| <span data-ttu-id="3e3d8-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-162">**AzCredential**</span></span> | <span data-ttu-id="3e3d8-163">Azure 的堆疊服務系統管理員帳戶認證 (使用 hello 與您用於部署 Azure 堆疊使用相同帳戶)</span><span class="sxs-lookup"><span data-stu-id="3e3d8-163">Azure Stack Service Admin account credential (use hello same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="3e3d8-164">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-164">_required_</span></span> |
| <span data-ttu-id="3e3d8-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-165">**VMLocalCredential**</span></span> | <span data-ttu-id="3e3d8-166">hello hello MySQL 資源提供者 VM 的本機系統管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="3e3d8-166">hello local administrator account of hello MySQL resource provider VM</span></span> | <span data-ttu-id="3e3d8-167">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-167">_required_</span></span> |
| <span data-ttu-id="3e3d8-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-168">**ResourceGroupName**</span></span> | <span data-ttu-id="3e3d8-169">此指令碼所建立的 hello 項目的資源群組</span><span class="sxs-lookup"><span data-stu-id="3e3d8-169">Resource Group for hello items created by this script</span></span> |  <span data-ttu-id="3e3d8-170">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-170">_required_</span></span> |
| <span data-ttu-id="3e3d8-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-171">**VmName**</span></span> | <span data-ttu-id="3e3d8-172">Hello VM 保存名稱 hello 資源提供者</span><span class="sxs-lookup"><span data-stu-id="3e3d8-172">Name of hello VM holding hello resource provider</span></span> |  <span data-ttu-id="3e3d8-173">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-173">_required_</span></span> |
| <span data-ttu-id="3e3d8-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-174">**AcceptLicense**</span></span> | <span data-ttu-id="3e3d8-175">略過 hello 提示 tooaccept hello GPL 授權規範 (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="3e3d8-175">Skips hello prompt tooaccept hello GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="3e3d8-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="3e3d8-177">包含本機共用路徑 tooa [mysql 連接器-net 6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi)。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-177">Path tooa local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="3e3d8-178">如果您提供它們，也必須將憑證檔案放在這個目錄。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="3e3d8-179">_選用_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-179">_optional_</span></span> |
| <span data-ttu-id="3e3d8-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="3e3d8-181">hello hello.pfx 憑證的密碼</span><span class="sxs-lookup"><span data-stu-id="3e3d8-181">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="3e3d8-182">_必要_</span><span class="sxs-lookup"><span data-stu-id="3e3d8-182">_required_</span></span> |
| <span data-ttu-id="3e3d8-183">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-183">**MaxRetryCount**</span></span> | <span data-ttu-id="3e3d8-184">失敗時會重試每個作業</span><span class="sxs-lookup"><span data-stu-id="3e3d8-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="3e3d8-185">2</span><span class="sxs-lookup"><span data-stu-id="3e3d8-185">2</span></span> |
| <span data-ttu-id="3e3d8-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-186">**RetryDuration**</span></span> | <span data-ttu-id="3e3d8-187">重試之間以秒為單位的逾時</span><span class="sxs-lookup"><span data-stu-id="3e3d8-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="3e3d8-188">120</span><span class="sxs-lookup"><span data-stu-id="3e3d8-188">120</span></span> |
| <span data-ttu-id="3e3d8-189">**解除安裝**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-189">**Uninstall**</span></span> | <span data-ttu-id="3e3d8-190">移除 hello 資源提供者</span><span class="sxs-lookup"><span data-stu-id="3e3d8-190">Remove hello resource provider</span></span> | <span data-ttu-id="3e3d8-191">否</span><span class="sxs-lookup"><span data-stu-id="3e3d8-191">No</span></span> |
| <span data-ttu-id="3e3d8-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="3e3d8-192">**DebugMode**</span></span> | <span data-ttu-id="3e3d8-193">防止在失敗時自動清除</span><span class="sxs-lookup"><span data-stu-id="3e3d8-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="3e3d8-194">否</span><span class="sxs-lookup"><span data-stu-id="3e3d8-194">No</span></span> |


<span data-ttu-id="3e3d8-195">根據 hello 系統效能和下載速度，安裝可能需要一些為 20 分鐘或長時間為幾小時的時間。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-195">Depending on hello system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="3e3d8-196">如果無法使用 hello MySQLAdapter 刀鋒視窗，您必須重新整理 hello 系統管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-196">You must refresh hello admin portal if hello MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="3e3d8-197">如果 hello 安裝花 90 分鐘以上，它可能會失敗，您會看到失敗訊息囉 」 畫面上和 hello 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-197">If hello installation takes more than 90 minutes, it may fail and you will see a failure message on hello screen and in hello log file.</span></span> <span data-ttu-id="3e3d8-198">hello 部署會重試從 hello 失敗的步驟。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-198">hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="3e3d8-199">系統不符合 hello 建議的記憶體及核心規格可能不是能 toodeploy hello MySQL RP。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-199">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a><span data-ttu-id="3e3d8-200">提供藉由連接 tooa MySQL 主控伺服器的容量</span><span class="sxs-lookup"><span data-stu-id="3e3d8-200">Provide capacity by connecting tooa MySQL hosting server</span></span>

1. <span data-ttu-id="3e3d8-201">登入 toohello 堆疊 Azure 入口網站為服務管理員。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-201">Sign in toohello Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="3e3d8-202">按一下**資源提供者** &gt; **MySQLAdapter** &gt; **主控伺服器** &gt; **+新增**。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="3e3d8-203">hello **MySQL 主控伺服器**刀鋒視窗是您可以在此連接 hello MySQL Server 資源提供者 tooactual 的執行個體的 MySQL Server 做為 hello 資源提供者的後端。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-203">hello **MySQL Hosting Servers** blade is where you can connect hello MySQL Server Resource Provider tooactual instances of MySQL Server that serve as hello resource provider’s backend.</span></span>

    ![主控伺服器](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="3e3d8-205">Hello 表單中填入 hello MySQL 伺服器執行個體的連接詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-205">Fill hello form with hello connection details of your MySQL Server instance.</span></span> <span data-ttu-id="3e3d8-206">提供 hello 完整的網域名稱 (FQDN) 或有效的 IPv4 位址，而不 hello 簡短 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-206">Provide hello fully qualified domain name (FQDN) or a valid IPv4 address, and not hello short VM name.</span></span> <span data-ttu-id="3e3d8-207">這項安裝不會再提供預設 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="3e3d8-208">hello 提供大小可協助管理 hello 資料庫容量 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-208">hello size provided helps hello resource provider manage hello database capacity.</span></span> <span data-ttu-id="3e3d8-209">它應該關閉 toohello hello 資料庫伺服器的實體容量。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-209">It should be close toohello physical capacity of hello database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3e3d8-210">只要的 hello 租用戶和管理 Azure 資源管理員，就可以存取 hello MySQL 執行個體，就可以放受控制的 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-210">As long as hello MySQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="3e3d8-211">hello MySQL 執行個體__必須__配置以獨佔方式 toohello RP。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-211">hello MySQL instance __must__ be allocated exclusively toohello RP.</span></span>

4. <span data-ttu-id="3e3d8-212">當您新增伺服器，您必須將它們指派 tooa 新的或現有 SKU tooallow 差異化的服務供應項目。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-212">As you add servers, you must assign them tooa new or existing SKU tooallow differentiation of service offerings.</span></span> <span data-ttu-id="3e3d8-213">例如，您可以提供資料庫容量和自動備份企業執行個體，請保留各個部門高效能伺服器，等 hello SKU 名稱應反映 hello 屬性，以便租用戶可以將其資料庫適當地而且不應該有 SKU 中的所有主控伺服器 hello 相同的功能。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    ![建立 MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="3e3d8-215">Sku 可以佔用 tooan 小時 toobe hello 入口網站中顯示。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="3e3d8-216">您無法建立資料庫，直到建立 SKU 的 hello。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a><span data-ttu-id="3e3d8-217">建立您第一次的 MySQL 資料庫 tootest 部署</span><span class="sxs-lookup"><span data-stu-id="3e3d8-217">Create your first MySQL database tootest your deployment</span></span>


1. <span data-ttu-id="3e3d8-218">登入 toohello 堆疊 Azure 入口網站為服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-218">Sign in toohello Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="3e3d8-219">按一下 hello **+ 新增**按鈕&gt;**資料 + 儲存體** &gt; **MySQL Database （預覽版）**。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-219">Click hello **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="3e3d8-220">填寫表單 hello hello 資料庫詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-220">Fill in hello form with hello database details.</span></span>

    ![建立測試 MySQL 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="3e3d8-222">選取 SKU。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-222">Select a SKU.</span></span>

    ![選取 SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="3e3d8-224">建立登入設定。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-224">Create a login setting.</span></span> <span data-ttu-id="3e3d8-225">可重複使用 hello 登入設定，或建立一個新。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-225">hello login setting can be reused or a new one created.</span></span> <span data-ttu-id="3e3d8-226">這包含 hello 使用者名稱和密碼 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-226">This contains hello user name and password for hello database.</span></span>

    ![建立新的資料庫登入](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="3e3d8-228">hello 連接字串包含 hello 實際的資料庫伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-228">hello connections string includes hello real database server name.</span></span> <span data-ttu-id="3e3d8-229">請將它複製從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-229">Copy it from hello portal.</span></span>

    ![取得 hello 連接字串 hello MySQL 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="3e3d8-231">hello hello 使用者名稱長度不得超過 32 個字元並 MySQL 5.7 或較早版本的 16 個字元。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-231">hello length of hello user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="3e3d8-232">這是 hello MySQL 實作 (implementation) 的限制。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-232">This is a limitation of hello MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="3e3d8-233">新增容量</span><span class="sxs-lookup"><span data-stu-id="3e3d8-233">Add capacity</span></span>

<span data-ttu-id="3e3d8-234">新增額外的 MySQL 伺服器 hello Azure 堆疊入口網站中新增容量。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-234">Add capacity by adding additional MySQL servers in hello Azure Stack portal.</span></span> <span data-ttu-id="3e3d8-235">如果您想 toouse MySQL 的另一個執行個體，請按一下**資源提供者** &gt; **MySQLAdapter** &gt; **MySQL 主控伺服器** &gt; **+ 加入**。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-235">If you wish toouse another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-tootenants"></a><span data-ttu-id="3e3d8-236">可用的 tootenants 提高 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="3e3d8-236">Making MySQL databases available tootenants</span></span>
<span data-ttu-id="3e3d8-237">建立計劃和優惠 toomake 可用的 MySQL 資料庫供租用戶。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-237">Create plans and offers toomake MySQL databases available for tenants.</span></span> <span data-ttu-id="3e3d8-238">新增 hello Microsoft.MySqlAdapter 服務，將配額、 等等。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-238">Add hello Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![建立計劃和優惠 tooinclude 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a><span data-ttu-id="3e3d8-240">移除 hello MySQL 配接器資源提供者</span><span class="sxs-lookup"><span data-stu-id="3e3d8-240">Removing hello MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="3e3d8-241">tooremove hello 資源提供者，務必 toofirst 移除任何相依性。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-241">tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="3e3d8-242">確定您擁有 hello 原始部署套件下載這個版本的 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-242">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="3e3d8-243">從 hello 資源提供者 （這不會刪除 hello 資料），必須刪除所有租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-243">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="3e3d8-244">應該執行此作業由 hello 租用戶本身。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-244">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="3e3d8-245">租用戶必須從 hello 命名空間移除註冊。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-245">Tenants must unregister from hello namespace.</span></span>

4. <span data-ttu-id="3e3d8-246">系統管理員必須先刪除主控伺服器 hello MySQL 配接器從 hello</span><span class="sxs-lookup"><span data-stu-id="3e3d8-246">Administrator must delete hello hosting servers from hello MySQL Adapter</span></span>

5. <span data-ttu-id="3e3d8-247">系統管理員必須先刪除任何參考 hello MySQL 配接器的計劃。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-247">Administrator must delete any plans that reference hello MySQL Adapter.</span></span>

6. <span data-ttu-id="3e3d8-248">系統管理員必須先刪除任何配額相關聯的 toohello MySQL 配接器。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-248">Administrator must delete any quotas associated toohello MySQL Adapter.</span></span>

7. <span data-ttu-id="3e3d8-249">重新執行具有 hello 部署指令碼 hello-解除安裝參數，Azure 資源管理員端點、 DirectoryTenantID 和 hello 服務系統管理員帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-249">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="3e3d8-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e3d8-250">Next steps</span></span>


<span data-ttu-id="3e3d8-251">請嘗試其他[PaaS 服務](azure-stack-tools-paas-services.md)像 hello [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)和 hello[應用程式服務資源提供者](azure-stack-app-service-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3e3d8-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
