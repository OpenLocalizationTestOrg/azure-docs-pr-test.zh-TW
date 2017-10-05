---
title: "在 Azure Stack 上使用 MySQL 資料庫做為 PaaS | Microsoft Docs"
description: "瞭解如何部署 MySQL 資源提供者，並提供 MySQL 資料庫作為 Azure Stack 上的服務"
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
ms.openlocfilehash: 4e9da524ef9dfa2d5b7150bc6a888536a1435dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="0297c-103">在 Microsoft Azure Stack 上使用 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="0297c-103">Use MySQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="0297c-104">您可以在 Azure Stack 上部署 MySQL 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="0297c-104">You can deploy a MySQL resource provider on Azure Stack.</span></span> <span data-ttu-id="0297c-105">部署資源提供者後，您可以透過 Azure Resource Manager 部署範本建立 MySQL 伺服器和資料庫，並提供 MySQL 資料庫即服務。</span><span class="sxs-lookup"><span data-stu-id="0297c-105">After you deploy the resource provider, you can create MySQL servers and databases through Azure Resource Manager deployment templates and provide MySQL databases as a service.</span></span> <span data-ttu-id="0297c-106">網站上常用的 MySQL 資料庫支援許多網站平台。</span><span class="sxs-lookup"><span data-stu-id="0297c-106">MySQL databases, which are common on web sites, support many website platforms.</span></span> <span data-ttu-id="0297c-107">例如，部署資源提供者後，您可以從 Azure Stack 的 Azure Web Apps 平台即服務 (PaaS) 附加元件中建立 WordPress 網站。</span><span class="sxs-lookup"><span data-stu-id="0297c-107">As an example, after you deploy the resource provider, you can create WordPress websites from the Azure Web Apps platform as a service (PaaS) add-on for Azure Stack.</span></span>

<span data-ttu-id="0297c-108">若要在沒有網際網路存取權的系統上部署 MySQL 提供者，您可以將 [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) 檔複製到本機共用，並在系統提示時提供該共用名稱 (請參閱下文)。</span><span class="sxs-lookup"><span data-stu-id="0297c-108">To deploy the MySQL provider on a system that does not have internet access, you can copy the file [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) to a local share and provide that share name when prompted (see below).</span></span> <span data-ttu-id="0297c-109">您也必須安裝 Azure 和 Azure Stack PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="0297c-109">You must also install the Azure and Azure Stack PowerShell modules.</span></span>


## <a name="mysql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="0297c-110">MySQL Server 資源提供者介面卡架構</span><span class="sxs-lookup"><span data-stu-id="0297c-110">MySQL Server Resource Provider Adapter architecture</span></span>

<span data-ttu-id="0297c-111">資源提供者由三個元件組成：</span><span class="sxs-lookup"><span data-stu-id="0297c-111">The resource provider is made up of three components:</span></span>

- <span data-ttu-id="0297c-112">**MySQL 資源提供者介面卡 VM**，為執行提供者服務的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0297c-112">**The MySQL resource provider adapter VM**, which is a Windows virtual machine running the provider services.</span></span>
- <span data-ttu-id="0297c-113">**資源提供者本身**，其處理佈建要求並公開資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="0297c-113">**The resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="0297c-114">**主控 MySQL Server 的伺服器**，其提供資料庫的容量，稱為主控伺服器。</span><span class="sxs-lookup"><span data-stu-id="0297c-114">**Servers that host MySQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="0297c-115">此版本不會再建立 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0297c-115">This release no longer creates a MySQL instance.</span></span> <span data-ttu-id="0297c-116">您必須建立它們和/或提供外部 SQL 執行個體的存取權。</span><span class="sxs-lookup"><span data-stu-id="0297c-116">You must create them and/or provide access to external SQL instances.</span></span> <span data-ttu-id="0297c-117">您可以造訪 [Azure Stack 快速入門圖庫](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows)，取得範本範例來建立 MySQL 伺服器，或從 Marketplace下載並部署 MySQL Server。</span><span class="sxs-lookup"><span data-stu-id="0297c-117">You can visit the [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) for an example template that can create a MySQL server for you or download and deploy a MySQL Server from the Marketplace.</span></span>

## <a name="deploy-the-resource-provider"></a><span data-ttu-id="0297c-118">部署資源提供者</span><span class="sxs-lookup"><span data-stu-id="0297c-118">Deploy the resource provider</span></span>

1. <span data-ttu-id="0297c-119">如果您尚未這樣做，請註冊您的開發套件並下載 Windows Server 2016 Datacenter - 可透過 Marketplace 管理下載 Eval 映像。</span><span class="sxs-lookup"><span data-stu-id="0297c-119">If you have not already done so, register your development kit and download the Windows Server 2016 Datacenter - Eval image downloadable through Marketplace Management.</span></span> <span data-ttu-id="0297c-120">您也可以使用指令碼來建立 [Windows Server 2016 映像](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image)。</span><span class="sxs-lookup"><span data-stu-id="0297c-120">You can also use a script to create a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span>

2. <span data-ttu-id="0297c-121">[下載 MySQL 資源提供者二進位檔案](https://aka.ms/azurestackmysqlrp)，並在開發套件主機上解壓縮該檔案。</span><span class="sxs-lookup"><span data-stu-id="0297c-121">[Download the MySQL resource provider binaries file](https://aka.ms/azurestackmysqlrp) and extract it on the development kit host.</span></span>

3. <span data-ttu-id="0297c-122">登入開發套件主機，並將 MySQL RP 安裝程式檔案解壓縮至暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="0297c-122">Sign in to the development kit host, and extract the MySQL RP installer file to a temporary directory.</span></span>

4. <span data-ttu-id="0297c-123">擷取 Azure Stack 根憑證，並在此程序的過程中建立自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="0297c-123">The Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="0297c-124">__選擇性：__如果需要提供自己的憑證，請準備好憑證並將它複製到本機目錄 (如果您想要自訂憑證以傳遞到安裝指令碼)。</span><span class="sxs-lookup"><span data-stu-id="0297c-124">__Optional:__ If you need to provide your own, prepare the certificates and copy to a local directory if you wish to customize the certificates (passed to the installation script).</span></span> <span data-ttu-id="0297c-125">您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0297c-125">You need the following:</span></span>

    <span data-ttu-id="0297c-126">a.</span><span class="sxs-lookup"><span data-stu-id="0297c-126">a.</span></span> <span data-ttu-id="0297c-127">*.dbadapter.\<地區\>.\<外部 FQDN\>的萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="0297c-127">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="0297c-128">此憑證必須受到信任，例如由憑證授權單位簽發 (也就是信任鏈結必須存在而不需要中繼憑證。) (單一站台憑證可搭配您在安裝期間提供的明確 VM 名稱使用。)</span><span class="sxs-lookup"><span data-stu-id="0297c-128">This certificate must be trusted, such as would be issued by a certificate authority (that is, the chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with the explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="0297c-129">b.</span><span class="sxs-lookup"><span data-stu-id="0297c-129">b.</span></span> <span data-ttu-id="0297c-130">Azure Resource Manager 為您的 Azure Stack 執行個體所使用的根憑證。</span><span class="sxs-lookup"><span data-stu-id="0297c-130">The root certificate used by the Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="0297c-131">如果找不到，則將擷取根憑證。</span><span class="sxs-lookup"><span data-stu-id="0297c-131">If it is not found, the root certificate will be retrieved.</span></span>

5. <span data-ttu-id="0297c-132">開啟**新的**已提升權限的 PowerShell 主控台，並變更至解壓縮檔案所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="0297c-132">Open a **new** elevated PowerShell console and change to the directory where you extracted the files.</span></span> <span data-ttu-id="0297c-133">使用新視窗，避免因為系統上已載入不正確的 PowerShell 模組而可能發生的問題。</span><span class="sxs-lookup"><span data-stu-id="0297c-133">Use a new window to avoid problems that may arise from incorrect PowerShell modules already loaded on the system.</span></span>

6. <span data-ttu-id="0297c-134">如果已安裝 1.2.9 或 1.2.10 以外之任何版本的 AzureRm 或 AzureStack PowerShell 模組，系統會提示您將它們移除，否則不會繼續安裝。</span><span class="sxs-lookup"><span data-stu-id="0297c-134">If you have installed any versions of the AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted to remove them or the install will not proceed.</span></span> <span data-ttu-id="0297c-135">這包括 1.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="0297c-135">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="0297c-136">執行 DeployMySqlProvider.ps1。</span><span class="sxs-lookup"><span data-stu-id="0297c-136">Run DeployMySqlProvider.ps1.</span></span>

<span data-ttu-id="0297c-137">此指令碼執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0297c-137">This script performs these steps:</span></span>

* <span data-ttu-id="0297c-138">如有必要，請下載相容版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0297c-138">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="0297c-139">下載 MySQL 連接器二進位檔 (可離線提供)。</span><span class="sxs-lookup"><span data-stu-id="0297c-139">Download the MySQL connector binary (this can be provided offline).</span></span>
* <span data-ttu-id="0297c-140">將憑證和所有其他成品上傳到 Azure Stack 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0297c-140">Upload the certificate and all other artifacts to an Azure Stack storage account.</span></span>
* <span data-ttu-id="0297c-141">發佈資源庫套件，讓您可以透過資源庫部署 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0297c-141">Publish gallery packages so that you can deploy MySQL databases through the gallery.</span></span>
* <span data-ttu-id="0297c-142">部署主控資源提供者的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="0297c-142">Deploy a virtual machine (VM) that hosts your resource provider.</span></span>
* <span data-ttu-id="0297c-143">註冊會對應至您的資源提供者 VM 的本機 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="0297c-143">Register a local DNS record that maps to your resource provider VM.</span></span>
* <span data-ttu-id="0297c-144">向本機 Azure Resource Manager 註冊您的資源提供者。</span><span class="sxs-lookup"><span data-stu-id="0297c-144">Register your resource provider with the local Azure Resource Manager.</span></span>

<span data-ttu-id="0297c-145">請在命令列上至少指定必要的參數，或是如果不含任何參數執行，系統會提示您輸入它們。</span><span class="sxs-lookup"><span data-stu-id="0297c-145">Either specify at least the required parameters on the command line, or, if you run without any parameters, you are prompted to enter them.</span></span> 

<span data-ttu-id="0297c-146">以下是可從 PowerShell 提示執行的範例 (視需要變更帳戶資訊和入口網站端點)：</span><span class="sxs-lookup"><span data-stu-id="0297c-146">Here's an example you can run from the PowerShell prompt (but change the account information and portal endpoints as needed):</span></span>


```
# Install the AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports the API Version Profile required by Azure Stack into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download the Azure Stack Tools from GitHub and set the environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use the following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace the previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory to the folder where you extracted the installation files 
# and adjust the endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a><span data-ttu-id="0297c-147">DeployMySqlProvider.ps1 參數</span><span class="sxs-lookup"><span data-stu-id="0297c-147">DeployMySqlProvider.ps1 parameters</span></span>

<span data-ttu-id="0297c-148">您可以在命令列中指定這些參數。</span><span class="sxs-lookup"><span data-stu-id="0297c-148">You can specify these parameters in the command line.</span></span> <span data-ttu-id="0297c-149">如果未這麼做，或任何參數驗證失敗，系統會提示您提供必要參數。</span><span class="sxs-lookup"><span data-stu-id="0297c-149">If you do not, or any parameter validation fails, you are prompted to provide the required ones.</span></span>

| <span data-ttu-id="0297c-150">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0297c-150">Parameter Name</span></span> | <span data-ttu-id="0297c-151">說明</span><span class="sxs-lookup"><span data-stu-id="0297c-151">Description</span></span> | <span data-ttu-id="0297c-152">註解或預設值</span><span class="sxs-lookup"><span data-stu-id="0297c-152">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0297c-153">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="0297c-153">**DirectoryTenantID**</span></span> | <span data-ttu-id="0297c-154">Azure 或 ADFS Directory ID (guid)</span><span class="sxs-lookup"><span data-stu-id="0297c-154">The Azure or ADFS Directory ID (guid)</span></span> | <span data-ttu-id="0297c-155">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-155">_required_</span></span> |
| <span data-ttu-id="0297c-156">**ArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="0297c-156">**ArmEndpoint**</span></span> | <span data-ttu-id="0297c-157">Azure Stack 系統管理 Azure Resource Manager 端點</span><span class="sxs-lookup"><span data-stu-id="0297c-157">The Azure Stack Administrative Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="0297c-158">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-158">_required_</span></span> |
| <span data-ttu-id="0297c-159">**TenantArmEndpoint**</span><span class="sxs-lookup"><span data-stu-id="0297c-159">**TenantArmEndpoint**</span></span> | <span data-ttu-id="0297c-160">Azure Stack 租用戶 Azure Resource Manager 端點</span><span class="sxs-lookup"><span data-stu-id="0297c-160">The Azure Stack Tenant Azure Resource Manager Endpoint</span></span> | <span data-ttu-id="0297c-161">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-161">_required_</span></span> |
| <span data-ttu-id="0297c-162">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="0297c-162">**AzCredential**</span></span> | <span data-ttu-id="0297c-163">Azure Stack 服務管理員帳戶認證 (使用用於部署 Azure Stack 的相同帳戶)</span><span class="sxs-lookup"><span data-stu-id="0297c-163">Azure Stack Service Admin account credential (use the same account as you used for deploying Azure Stack)</span></span> | <span data-ttu-id="0297c-164">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-164">_required_</span></span> |
| <span data-ttu-id="0297c-165">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="0297c-165">**VMLocalCredential**</span></span> | <span data-ttu-id="0297c-166">MySQL 資源提供者 VM 的本機系統管理員帳戶</span><span class="sxs-lookup"><span data-stu-id="0297c-166">The local administrator account of the MySQL resource provider VM</span></span> | <span data-ttu-id="0297c-167">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-167">_required_</span></span> |
| <span data-ttu-id="0297c-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="0297c-168">**ResourceGroupName**</span></span> | <span data-ttu-id="0297c-169">此指令碼所建立之項目的資源群組</span><span class="sxs-lookup"><span data-stu-id="0297c-169">Resource Group for the items created by this script</span></span> |  <span data-ttu-id="0297c-170">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-170">_required_</span></span> |
| <span data-ttu-id="0297c-171">**VmName**</span><span class="sxs-lookup"><span data-stu-id="0297c-171">**VmName**</span></span> | <span data-ttu-id="0297c-172">持有資源提供者的 VM 名稱</span><span class="sxs-lookup"><span data-stu-id="0297c-172">Name of the VM holding the resource provider</span></span> |  <span data-ttu-id="0297c-173">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-173">_required_</span></span> |
| <span data-ttu-id="0297c-174">**AcceptLicense**</span><span class="sxs-lookup"><span data-stu-id="0297c-174">**AcceptLicense**</span></span> | <span data-ttu-id="0297c-175">略過提示以接受 GPL 授權 (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span><span class="sxs-lookup"><span data-stu-id="0297c-175">Skips the prompt to accept the GPL License  (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html)</span></span> | |
| <span data-ttu-id="0297c-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="0297c-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="0297c-177">包含 [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi) 的本機共用路徑。</span><span class="sxs-lookup"><span data-stu-id="0297c-177">Path to a local share containing [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi).</span></span> <span data-ttu-id="0297c-178">如果您提供它們，也必須將憑證檔案放在這個目錄。</span><span class="sxs-lookup"><span data-stu-id="0297c-178">If you provide them, certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="0297c-179">_選用_</span><span class="sxs-lookup"><span data-stu-id="0297c-179">_optional_</span></span> |
| <span data-ttu-id="0297c-180">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="0297c-180">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="0297c-181">.pfx 憑證的密碼</span><span class="sxs-lookup"><span data-stu-id="0297c-181">The password for the .pfx certificate</span></span> | <span data-ttu-id="0297c-182">_必要_</span><span class="sxs-lookup"><span data-stu-id="0297c-182">_required_</span></span> |
| <span data-ttu-id="0297c-183">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="0297c-183">**MaxRetryCount**</span></span> | <span data-ttu-id="0297c-184">失敗時會重試每個作業</span><span class="sxs-lookup"><span data-stu-id="0297c-184">Each operation is retried if there is a failure</span></span> | <span data-ttu-id="0297c-185">2</span><span class="sxs-lookup"><span data-stu-id="0297c-185">2</span></span> |
| <span data-ttu-id="0297c-186">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="0297c-186">**RetryDuration**</span></span> | <span data-ttu-id="0297c-187">重試之間以秒為單位的逾時</span><span class="sxs-lookup"><span data-stu-id="0297c-187">Timeout between retries, in seconds</span></span> | <span data-ttu-id="0297c-188">120</span><span class="sxs-lookup"><span data-stu-id="0297c-188">120</span></span> |
| <span data-ttu-id="0297c-189">**解除安裝**</span><span class="sxs-lookup"><span data-stu-id="0297c-189">**Uninstall**</span></span> | <span data-ttu-id="0297c-190">移除資源提供者</span><span class="sxs-lookup"><span data-stu-id="0297c-190">Remove the resource provider</span></span> | <span data-ttu-id="0297c-191">否</span><span class="sxs-lookup"><span data-stu-id="0297c-191">No</span></span> |
| <span data-ttu-id="0297c-192">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="0297c-192">**DebugMode**</span></span> | <span data-ttu-id="0297c-193">防止在失敗時自動清除</span><span class="sxs-lookup"><span data-stu-id="0297c-193">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="0297c-194">否</span><span class="sxs-lookup"><span data-stu-id="0297c-194">No</span></span> |


<span data-ttu-id="0297c-195">根據系統效能和下載速度，安裝可能需要少至 20 分鐘或長達幾小時的時間。</span><span class="sxs-lookup"><span data-stu-id="0297c-195">Depending on the system performance and download speeds, installation may take as little as 20 minutes or as long as several hours.</span></span> <span data-ttu-id="0297c-196">如果無法使用 MySQLAdapter 刀鋒視窗，您必須重新整理管理員入口網站。</span><span class="sxs-lookup"><span data-stu-id="0297c-196">You must refresh the admin portal if the MySQLAdapter blade is not available.</span></span>

> [!NOTE]
> <span data-ttu-id="0297c-197">如果安裝需要超過 90 分鐘，它可能會失敗，並在畫面和記錄檔中看到失敗訊息。</span><span class="sxs-lookup"><span data-stu-id="0297c-197">If the installation takes more than 90 minutes, it may fail and you will see a failure message on the screen and in the log file.</span></span> <span data-ttu-id="0297c-198">部署會從失敗的步驟開始重試。</span><span class="sxs-lookup"><span data-stu-id="0297c-198">The deployment is retried from the failing step.</span></span> <span data-ttu-id="0297c-199">不符合建議的記憶體及核心規格的系統可能無法部署 MySQL RP。</span><span class="sxs-lookup"><span data-stu-id="0297c-199">Systems that do not meet the recommended memory and core specifications may not be able to deploy the MySQL RP.</span></span>


## <a name="provide-capacity-by-connecting-to-a-mysql-hosting-server"></a><span data-ttu-id="0297c-200">透過連線到 MySQL 主控伺服器以提供容量</span><span class="sxs-lookup"><span data-stu-id="0297c-200">Provide capacity by connecting to a MySQL hosting server</span></span>

1. <span data-ttu-id="0297c-201">作為服務管理員登入 Azure Stack 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0297c-201">Sign in to the Azure Stack portal as a service admin.</span></span>

2. <span data-ttu-id="0297c-202">按一下**資源提供者** &gt; **MySQLAdapter** &gt; **主控伺服器** &gt; **+新增**。</span><span class="sxs-lookup"><span data-stu-id="0297c-202">Click **Resource Providers** &gt; **MySQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="0297c-203">您可使用**MySQL 主控伺服器**刀鋒視窗，將 MySQL Server 資源提供者連線到 MySQL Server 的實際執行個體以作為資源提供者的後端。</span><span class="sxs-lookup"><span data-stu-id="0297c-203">The **MySQL Hosting Servers** blade is where you can connect the MySQL Server Resource Provider to actual instances of MySQL Server that serve as the resource provider’s backend.</span></span>

    ![主控伺服器](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. <span data-ttu-id="0297c-205">在表單中填寫 MySQL Server 執行個體的連線詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0297c-205">Fill the form with the connection details of your MySQL Server instance.</span></span> <span data-ttu-id="0297c-206">提供完整網域名稱 (FQDN) 或有效的 IPv4 位址，而不是簡短的 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="0297c-206">Provide the fully qualified domain name (FQDN) or a valid IPv4 address, and not the short VM name.</span></span> <span data-ttu-id="0297c-207">這項安裝不會再提供預設 MySQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0297c-207">This installation no longer provides a default MySQL instance.</span></span> <span data-ttu-id="0297c-208">提供的大小可協助資源提供者管理資料庫容量。</span><span class="sxs-lookup"><span data-stu-id="0297c-208">The size provided helps the resource provider manage the database capacity.</span></span> <span data-ttu-id="0297c-209">它應該接近資料庫伺服器的實體容量。</span><span class="sxs-lookup"><span data-stu-id="0297c-209">It should be close to the physical capacity of the database server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0297c-210">只要租用戶和管理 Azure Resource Manager 可以存取 MySQL 執行個體，資源提供者就可以控制它。</span><span class="sxs-lookup"><span data-stu-id="0297c-210">As long as the MySQL instance can be accessed by the tenant and admin Azure Resource Manager, it can be placed under control of the resource provider.</span></span> <span data-ttu-id="0297c-211">MySQL 執行個體__必須__配置為 RP 專屬。</span><span class="sxs-lookup"><span data-stu-id="0297c-211">The MySQL instance __must__ be allocated exclusively to the RP.</span></span>

4. <span data-ttu-id="0297c-212">新增伺服器時，您必須將它們指派給新的或現有的 SKU，以允許服務產品的差異化。</span><span class="sxs-lookup"><span data-stu-id="0297c-212">As you add servers, you must assign them to a new or existing SKU to allow differentiation of service offerings.</span></span> <span data-ttu-id="0297c-213">例如，您可以具有提供資料庫容量和自動備份的企業執行個體、保留高效能的伺服器供個別部門使用等等。SKU 名稱應反映屬性，讓租用戶可適當地安置其資料庫，並讓 SKU 中的所有主控伺服器具有相同的功能。</span><span class="sxs-lookup"><span data-stu-id="0297c-213">For example, you could have an enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. The SKU name should reflect the properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have the same capabilities.</span></span>

    ![建立 MySQL SKU](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
<span data-ttu-id="0297c-215">最多需要一小時才能在入口網站中看到 SKU。</span><span class="sxs-lookup"><span data-stu-id="0297c-215">SKUs can take up to an hour to be visible in the portal.</span></span> <span data-ttu-id="0297c-216">在建立 SKU 前，您無法建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="0297c-216">You cannot create a database until the SKU is created.</span></span>


## <a name="create-your-first-mysql-database-to-test-your-deployment"></a><span data-ttu-id="0297c-217">建立第一個 MySQL 資料庫以測試您的部署</span><span class="sxs-lookup"><span data-stu-id="0297c-217">Create your first MySQL database to test your deployment</span></span>


1. <span data-ttu-id="0297c-218">作為服務管理員登入 Azure Stack 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0297c-218">Sign in to the Azure Stack portal as service admin.</span></span>

2. <span data-ttu-id="0297c-219">按一下**+ 新增**按鈕&gt;**資料+儲存體** &gt; **MySQL Database (預覽版)**。</span><span class="sxs-lookup"><span data-stu-id="0297c-219">Click the **+ New** button &gt; **Data + Storage** &gt; **MySQL Database (preview)**.</span></span>

3. <span data-ttu-id="0297c-220">在表單中填寫資料庫的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0297c-220">Fill in the form with the database details.</span></span>

    ![建立測試 MySQL 資料庫](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. <span data-ttu-id="0297c-222">選取 SKU。</span><span class="sxs-lookup"><span data-stu-id="0297c-222">Select a SKU.</span></span>

    ![選取 SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. <span data-ttu-id="0297c-224">建立登入設定。</span><span class="sxs-lookup"><span data-stu-id="0297c-224">Create a login setting.</span></span> <span data-ttu-id="0297c-225">可重複使用，或建立一個新的登入設定。</span><span class="sxs-lookup"><span data-stu-id="0297c-225">The login setting can be reused or a new one created.</span></span> <span data-ttu-id="0297c-226">這包含資料庫的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0297c-226">This contains the user name and password for the database.</span></span>

    ![建立新的資料庫登入](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    <span data-ttu-id="0297c-228">連接字串包含實際的資料庫伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="0297c-228">The connections string includes the real database server name.</span></span> <span data-ttu-id="0297c-229">從入口網站複製它。</span><span class="sxs-lookup"><span data-stu-id="0297c-229">Copy it from the portal.</span></span>

    ![取得 MySQL 資料庫的連接字串](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> <span data-ttu-id="0297c-231">MySQL 5.7 中的使用者名稱長度不得超過 32 個字元，較早的版本則為 16 個字元。</span><span class="sxs-lookup"><span data-stu-id="0297c-231">The length of the user names cannot exceed 32 characters with MySQL 5.7 or 16 characters in earlier editions.</span></span> <span data-ttu-id="0297c-232">這是 MySQL 實作的限制。</span><span class="sxs-lookup"><span data-stu-id="0297c-232">This is a limitation of the MySQL implementations.</span></span>


## <a name="add-capacity"></a><span data-ttu-id="0297c-233">新增容量</span><span class="sxs-lookup"><span data-stu-id="0297c-233">Add capacity</span></span>

<span data-ttu-id="0297c-234">在 Azure Stack 入口網站中新增額外的 MySQL 伺服器來新增容量。</span><span class="sxs-lookup"><span data-stu-id="0297c-234">Add capacity by adding additional MySQL servers in the Azure Stack portal.</span></span> <span data-ttu-id="0297c-235">如果您想要使用 MySQL 的另一個執行個體，按一下**資源提供者** &gt; **MySQLAdapter** &gt; **MySQL 主控伺服器** &gt; **+新增**。</span><span class="sxs-lookup"><span data-stu-id="0297c-235">If you wish to use another instance of MySQL, click **Resource Providers** &gt; **MySQLAdapter** &gt; **MySQL Hosting Servers** &gt; **+Add**.</span></span>


## <a name="making-mysql-databases-available-to-tenants"></a><span data-ttu-id="0297c-236">將 MySQL 資料庫提供給租用戶使用</span><span class="sxs-lookup"><span data-stu-id="0297c-236">Making MySQL databases available to tenants</span></span>
<span data-ttu-id="0297c-237">建立方案和產品，讓租用戶使用 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0297c-237">Create plans and offers to make MySQL databases available for tenants.</span></span> <span data-ttu-id="0297c-238">新增 Microsoft.MySqlAdapter 服務、新增配額等等。</span><span class="sxs-lookup"><span data-stu-id="0297c-238">Add the Microsoft.MySqlAdapter service, add a quota, etc.</span></span>

![建立方案和產品來加入資料庫](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-the-mysql-adapter-resource-provider"></a><span data-ttu-id="0297c-240">移除 MySQL 介面卡資源提供者</span><span class="sxs-lookup"><span data-stu-id="0297c-240">Removing the MySQL Adapter Resource Provider</span></span>

<span data-ttu-id="0297c-241">若要移除資源提供者，必須先移除任何相依性。</span><span class="sxs-lookup"><span data-stu-id="0297c-241">To remove the resource provider, it is essential to first remove any dependencies.</span></span>

1. <span data-ttu-id="0297c-242">確認已下載此資源提供者版本的原始部署套件。</span><span class="sxs-lookup"><span data-stu-id="0297c-242">Ensure you have the original deployment package that you downloaded for this version of the Resource Provider.</span></span>

2. <span data-ttu-id="0297c-243">必須從資源提供者刪除所有租用戶資料庫 (這不會刪除資料)。</span><span class="sxs-lookup"><span data-stu-id="0297c-243">All tenant databases must be deleted from the resource provider (this will not delete the data).</span></span> <span data-ttu-id="0297c-244">必須由租用戶本身執行此作業。</span><span class="sxs-lookup"><span data-stu-id="0297c-244">This should be performed by the tenants themselves.</span></span>

3. <span data-ttu-id="0297c-245">必須從命名空間中取消註冊租用戶。</span><span class="sxs-lookup"><span data-stu-id="0297c-245">Tenants must unregister from the namespace.</span></span>

4. <span data-ttu-id="0297c-246">系統管理員必須從 MySQL 介面卡刪除主控伺服器</span><span class="sxs-lookup"><span data-stu-id="0297c-246">Administrator must delete the hosting servers from the MySQL Adapter</span></span>

5. <span data-ttu-id="0297c-247">系統管理員必須刪除參照 MySQL 介面卡的任何方案。</span><span class="sxs-lookup"><span data-stu-id="0297c-247">Administrator must delete any plans that reference the MySQL Adapter.</span></span>

6. <span data-ttu-id="0297c-248">系統管理員必須刪除 MySQL 介面卡所關聯的任何配額。</span><span class="sxs-lookup"><span data-stu-id="0297c-248">Administrator must delete any quotas associated to the MySQL Adapter.</span></span>

7. <span data-ttu-id="0297c-249">使用 -Uninstall 參數、Azure Resource Manager 端點、DirectoryTenantID 和服務管理員帳戶的認證，重新執行部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="0297c-249">Rerun the deployment script with the -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for the service administrator account.</span></span>




## <a name="next-steps"></a><span data-ttu-id="0297c-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0297c-250">Next steps</span></span>


<span data-ttu-id="0297c-251">嘗試其他 [PaaS 服務](azure-stack-tools-paas-services.md)，如 [SQL Server 資源提供者](azure-stack-sql-resource-provider-deploy.md)和[應用程式服務資源提供者](azure-stack-app-service-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0297c-251">Try other [PaaS services](azure-stack-tools-paas-services.md) like the [SQL Server resource provider](azure-stack-sql-resource-provider-deploy.md) and the [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
