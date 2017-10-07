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
# <a name="use-sql-databases-on-microsoft-azure-stack"></a><span data-ttu-id="1391a-103">在 Microsoft Azure Stack 上使用 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="1391a-103">Use SQL databases on Microsoft Azure Stack</span></span>


<span data-ttu-id="1391a-104">為 Azure 堆疊的服務使用 hello SQL Server 資源提供者介面卡 tooexpose SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1391a-104">Use hello SQL Server resource provider adapter tooexpose SQL databases as a service of Azure Stack.</span></span> <span data-ttu-id="1391a-105">在安裝 hello 資源提供者，並將它連接 tooone 或多個 SQL Server 執行個體之後，您和您的使用者可以建立雲端原生應用程式、 以 SQL 為基礎的網站和工作負載為基礎而不需要 tooprovision 虛擬機器的 SQL 資料庫機器 (VM) 每次主控 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="1391a-105">After you install hello resource provider and connect it tooone or more SQL Server instances, you and your users can create databases for cloud-native apps, websites that are based on SQL, and workloads that are based on SQL without having tooprovision a virtual machine (VM) that hosts SQL Server each time.</span></span>

<span data-ttu-id="1391a-106">hello 資源提供者不支援的所有 hello 資料庫管理功能[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="1391a-106">hello resource provider does not support all hello database management capabilities of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/).</span></span> <span data-ttu-id="1391a-107">例如，不支援彈性資料庫集區和 hello 能力 tooscale 資料庫效能。</span><span class="sxs-lookup"><span data-stu-id="1391a-107">For example, elastic database pools and hello ability tooscale database performance aren't supported.</span></span> <span data-ttu-id="1391a-108">hello API 與不相容的 SQL DB。</span><span class="sxs-lookup"><span data-stu-id="1391a-108">hello API is not compatible with SQL DB.</span></span>


## <a name="sql-server-resource-provider-adapter-architecture"></a><span data-ttu-id="1391a-109">SQL Server 資源提供者配接器架構</span><span class="sxs-lookup"><span data-stu-id="1391a-109">SQL Server Resource Provider Adapter architecture</span></span>
<span data-ttu-id="1391a-110">hello 資源提供者不基礎，也不提供所有 hello 資料庫管理 Azure SQL Database 的功能。</span><span class="sxs-lookup"><span data-stu-id="1391a-110">hello resource provider is not based on, nor does it offer all hello database management capabilities of Azure SQL Database.</span></span> <span data-ttu-id="1391a-111">例如，彈性資料庫集區和 hello 能力 toodial 增加和減少的資料庫效能會自動將無法使用。</span><span class="sxs-lookup"><span data-stu-id="1391a-111">For example, elastic database pools and hello ability toodial database performance up and down automatically aren't available.</span></span> <span data-ttu-id="1391a-112">不過，hello 資源提供者支援類似建立、 讀取、 更新和刪除 (CRUD) 作業。</span><span class="sxs-lookup"><span data-stu-id="1391a-112">However, hello resource provider does support similar create, read, update, and delete (CRUD) operations.</span></span>

<span data-ttu-id="1391a-113">hello 資源提供者是由三個元件所組成：</span><span class="sxs-lookup"><span data-stu-id="1391a-113">hello resource provider is made up of three components:</span></span>

- <span data-ttu-id="1391a-114">**hello SQL 資源提供者介面卡 VM**、 哪些是執行 hello 提供者服務的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1391a-114">**hello SQL resource provider adapter VM**, which is a Windows virtual machine running hello provider services.</span></span>
- <span data-ttu-id="1391a-115">**hello 資源提供者本身**、 其處理佈建要求，會公開資料庫資源。</span><span class="sxs-lookup"><span data-stu-id="1391a-115">**hello resource provider itself**, which processes provisioning requests and exposes database resources.</span></span>
- <span data-ttu-id="1391a-116">**主控 SQL Server 的伺服器**，它提供資料庫的容量，稱為主控伺服器。</span><span class="sxs-lookup"><span data-stu-id="1391a-116">**Servers that host SQL Server**, which provide capacity for databases, called Hosting Servers.</span></span> 

<span data-ttu-id="1391a-117">此版本不會再建立 SQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1391a-117">This release no longer creates a SQL instance.</span></span> <span data-ttu-id="1391a-118">您必須建立一個 （或以上） 和 （或) 提供存取 tooexternal SQL 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1391a-118">You must create one (or more) and/or provide access tooexternal SQL instances.</span></span> <span data-ttu-id="1391a-119">有許多選項可用 tooyou hello 中包括範本[Azure 堆疊快速入門圖庫](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows)和 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="1391a-119">There are a number of options available tooyou including templates in hello [Azure Stack Quickstart Gallery](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) and Marketplace items.</span></span> 

>[!NOTE]
<span data-ttu-id="1391a-120">如果您已下載的任何 SQL Marketplace 項目，請確定您也可以下載 hello SQL IaaS 延伸模組，或這些不會將部署。</span><span class="sxs-lookup"><span data-stu-id="1391a-120">If you have downloaded any SQL Marketplace items, make sure you also download hello SQL IaaS Extension or these will not deploy.</span></span>


## <a name="deploy-hello-resource-provider"></a><span data-ttu-id="1391a-121">部署 hello 資源提供者</span><span class="sxs-lookup"><span data-stu-id="1391a-121">Deploy hello resource provider</span></span>

1. <span data-ttu-id="1391a-122">如果您尚未這樣做，註冊您的開發套件，並下載 hello 可下載透過 Marketplace 管理的 Windows Server 2016 評估版影像。</span><span class="sxs-lookup"><span data-stu-id="1391a-122">If you have not already done so, register your development kit and download hello Windows Server 2016 EVAL image downloadable through Marketplace Management.</span></span> <span data-ttu-id="1391a-123">您也可以使用指令碼 toocreate [Windows Server 2016 映像](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image)。</span><span class="sxs-lookup"><span data-stu-id="1391a-123">You can also use a script toocreate a [Windows Server 2016 image](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).</span></span> <span data-ttu-id="1391a-124">不再需要.NET 3.5 hello 執行階段。</span><span class="sxs-lookup"><span data-stu-id="1391a-124">hello .NET 3.5 runtime is no longer required.</span></span>

2. <span data-ttu-id="1391a-125">[下載 hello SQL 資源提供者二進位檔](https://aka.ms/azurestacksqlrp)並將它解壓縮 hello 開發套件主機上。</span><span class="sxs-lookup"><span data-stu-id="1391a-125">[Download hello SQL resource provider binaries file](https://aka.ms/azurestacksqlrp) and extract it on hello development kit host.</span></span>

3. <span data-ttu-id="1391a-126">登入 toohello 開發套件主機，然後將解壓縮 hello SQL RP 安裝程式檔案 tooa 暫存目錄。</span><span class="sxs-lookup"><span data-stu-id="1391a-126">Sign in toohello development kit host and extract hello SQL RP installer file tooa temporary directory.</span></span>

4. <span data-ttu-id="1391a-127">擷取 hello Azure 堆疊根憑證，此程序的一部分建立自我簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="1391a-127">hello Azure Stack root certificate is retrieved and a self-signed certificate is created as part of this process.</span></span> 

    <span data-ttu-id="1391a-128">__選擇性：__如果您需要 tooprovide 您擁有，請準備 hello 憑證並複製 tooa 本機目錄，如果您想 toocustomize hello 憑證 （傳遞的 toohello 安裝指令碼）。</span><span class="sxs-lookup"><span data-stu-id="1391a-128">__Optional:__ If you need tooprovide your own, prepare hello certificates and copy tooa local directory if you wish toocustomize hello certificates (passed toohello installation script).</span></span> <span data-ttu-id="1391a-129">您需要下列憑證 hello:</span><span class="sxs-lookup"><span data-stu-id="1391a-129">You need hello following certificates:</span></span>

    <span data-ttu-id="1391a-130">a.</span><span class="sxs-lookup"><span data-stu-id="1391a-130">a.</span></span> <span data-ttu-id="1391a-131">*.dbadapter.\<地區\>.\<外部 FQDN\>的萬用字元憑證。</span><span class="sxs-lookup"><span data-stu-id="1391a-131">A wildcard certificate for *.dbadapter.\<region\>.\<external fqdn\>.</span></span> <span data-ttu-id="1391a-132">此憑證必須受到信任，例如會發出的憑證授權單位 （也就是 hello 信任鏈結必須存在而不需要中繼憑證）。（使用 hello 您在安裝期間提供明確 VM 名稱，可以使用單一站台憑證）。</span><span class="sxs-lookup"><span data-stu-id="1391a-132">This certificate must be trusted, such as would be issued by a certificate authority (that is, hello chain of trust must exist without requiring intermediate certificates.) (A single site certificate can be used with hello explicit VM name you provide during install.)</span></span>

    <span data-ttu-id="1391a-133">b.</span><span class="sxs-lookup"><span data-stu-id="1391a-133">b.</span></span> <span data-ttu-id="1391a-134">hello hello Azure 資源管理員用於您的 Azure 堆疊的執行個體的根憑證。</span><span class="sxs-lookup"><span data-stu-id="1391a-134">hello root certificate used by hello Azure Resource Manager for your instance of Azure Stack.</span></span> <span data-ttu-id="1391a-135">如果沒有找到，則將會擷取 hello 根憑證。</span><span class="sxs-lookup"><span data-stu-id="1391a-135">If it is not found, hello root certificate will be retrieved.</span></span>


5. <span data-ttu-id="1391a-136">開啟**新**提高權限的 PowerShell 主控台，然後變更 toohello 目錄解壓縮 hello 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="1391a-136">Open a **new** elevated PowerShell console and change toohello directory where you extracted hello files.</span></span> <span data-ttu-id="1391a-137">使用新的視窗 tooavoid 問題可能因不正確的 PowerShell 模組已經載入 hello 系統上。</span><span class="sxs-lookup"><span data-stu-id="1391a-137">Use a new window tooavoid problems that may arise from incorrect PowerShell modules already loaded on hello system.</span></span>

6. <span data-ttu-id="1391a-138">如果您已安裝任何版本的 hello AzureRm 或 1.2.9 或 1.2.10 以外 AzureStack PowerShell 模組，您將會提示的 tooremove 它們或 hello 安裝將不會繼續。</span><span class="sxs-lookup"><span data-stu-id="1391a-138">If you have installed any versions of hello AzureRm or AzureStack PowerShell modules other than 1.2.9 or 1.2.10, you will be prompted tooremove them or hello install will not proceed.</span></span> <span data-ttu-id="1391a-139">這包括 1.3 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1391a-139">This includes versions 1.3 or greater.</span></span>

7. <span data-ttu-id="1391a-140">執行 hello DeploySqlProvider.ps1 下面所列的 hello 參數的指令碼。</span><span class="sxs-lookup"><span data-stu-id="1391a-140">Run hello DeploySqlProvider.ps1 script with hello parameters listed below.</span></span>

<span data-ttu-id="1391a-141">hello 指令碼執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1391a-141">hello script performs these steps:</span></span>

* <span data-ttu-id="1391a-142">如有必要，請下載相容版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1391a-142">If necessary, download a compatible version of Azure PowerShell.</span></span>
* <span data-ttu-id="1391a-143">上傳 hello 憑證和其他成品 tooa 儲存體帳戶的 Azure 堆疊上。</span><span class="sxs-lookup"><span data-stu-id="1391a-143">Upload hello certificates and other artifacts tooa storage account on your Azure Stack.</span></span>
* <span data-ttu-id="1391a-144">發佈圖庫套件，以便您可以部署到 hello 組件庫的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1391a-144">Publish gallery packages so that you can deploy SQL databases through hello gallery.</span></span>
* <span data-ttu-id="1391a-145">部署使用 hello Windows Server 2016 映像步驟 1 中建立的 VM 並安裝 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="1391a-145">Deploy a VM using hello Windows Server 2016 image created in step 1 and install hello resource provider.</span></span>
* <span data-ttu-id="1391a-146">註冊對應 tooyour 資源提供者 VM 的本機 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="1391a-146">Register a local DNS record that maps tooyour resource provider VM.</span></span>
* <span data-ttu-id="1391a-147">註冊您的資源提供者以 hello 本機 Azure 資源管理員 （租用戶和系統管理員）。</span><span class="sxs-lookup"><span data-stu-id="1391a-147">Register your resource provider with hello local Azure Resource Manager (Tenant and Admin).</span></span>

> [!NOTE]
> <span data-ttu-id="1391a-148">如果 hello 安裝花 90 分鐘以上，它可能會失敗並囉 」 畫面及 hello 記錄檔，請參閱失敗訊息但 hello 部署重試一次從 hello 失敗的步驟。</span><span class="sxs-lookup"><span data-stu-id="1391a-148">If hello installation takes more than 90 minutes, it may fail and you see a failure message on hello screen and in hello log file, but hello deployment is retried from hello failing step.</span></span> <span data-ttu-id="1391a-149">系統不符合 hello 建議的記憶體及核心規格可能不是能 toodeploy hello SQL RP。</span><span class="sxs-lookup"><span data-stu-id="1391a-149">Systems that do not meet hello recommended memory and core specifications may not be able toodeploy hello SQL RP.</span></span>
>

<span data-ttu-id="1391a-150">以下是您可以從 hello PowerShell 執行的範例提示 （但視需要變更 hello 帳戶資訊和入口網站端點）：</span><span class="sxs-lookup"><span data-stu-id="1391a-150">Here's an example you can run from hello PowerShell prompt (but change hello account information and portal endpoints as needed):</span></span>

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

### <a name="deploysqlproviderps1-parameters"></a><span data-ttu-id="1391a-151">DeploySqlProvider.ps1 參數</span><span class="sxs-lookup"><span data-stu-id="1391a-151">DeploySqlProvider.ps1 parameters</span></span>
<span data-ttu-id="1391a-152">您可以在 hello 命令列中指定這些參數。</span><span class="sxs-lookup"><span data-stu-id="1391a-152">You can specify these parameters in hello command line.</span></span> <span data-ttu-id="1391a-153">如果您不這麼做，或任何參數驗證失敗，系統會提示您 tooprovide hello 必要的。</span><span class="sxs-lookup"><span data-stu-id="1391a-153">If you do not, or any parameter validation fails, you are prompted tooprovide hello required ones.</span></span>

| <span data-ttu-id="1391a-154">參數名稱</span><span class="sxs-lookup"><span data-stu-id="1391a-154">Parameter Name</span></span> | <span data-ttu-id="1391a-155">說明</span><span class="sxs-lookup"><span data-stu-id="1391a-155">Description</span></span> | <span data-ttu-id="1391a-156">註解或預設值</span><span class="sxs-lookup"><span data-stu-id="1391a-156">Comment or Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1391a-157">**DirectoryTenantID**</span><span class="sxs-lookup"><span data-stu-id="1391a-157">**DirectoryTenantID**</span></span> | <span data-ttu-id="1391a-158">hello Azure 或 ADFS 目錄識別碼 (guid)。</span><span class="sxs-lookup"><span data-stu-id="1391a-158">hello Azure or ADFS Directory ID (guid).</span></span> | <span data-ttu-id="1391a-159">_必要_</span><span class="sxs-lookup"><span data-stu-id="1391a-159">_required_</span></span> |
| <span data-ttu-id="1391a-160">**AzCredential**</span><span class="sxs-lookup"><span data-stu-id="1391a-160">**AzCredential**</span></span> | <span data-ttu-id="1391a-161">Hello Azure 堆疊服務系統管理員帳戶提供 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="1391a-161">Provide hello credentials for hello Azure Stack Service Admin account.</span></span> <span data-ttu-id="1391a-162">您必須使用相同認證所使用的部署 Azure 堆疊 hello）。</span><span class="sxs-lookup"><span data-stu-id="1391a-162">You must use hello same credentials as you used for deploying Azure Stack).</span></span> | <span data-ttu-id="1391a-163">_必要_</span><span class="sxs-lookup"><span data-stu-id="1391a-163">_required_</span></span> |
| <span data-ttu-id="1391a-164">**VMLocalCredential**</span><span class="sxs-lookup"><span data-stu-id="1391a-164">**VMLocalCredential**</span></span> | <span data-ttu-id="1391a-165">定義 hello hello hello SQL 資源提供者 VM 的本機系統管理員帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="1391a-165">Define hello credentials for hello local administrator account of hello SQL resource provider VM.</span></span> <span data-ttu-id="1391a-166">這個密碼也會用於 hello SQL **sa**帳戶。</span><span class="sxs-lookup"><span data-stu-id="1391a-166">This password is also used for hello SQL **sa** account.</span></span> | <span data-ttu-id="1391a-167">_必要_</span><span class="sxs-lookup"><span data-stu-id="1391a-167">_required_</span></span> |
| <span data-ttu-id="1391a-168">**ResourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="1391a-168">**ResourceGroupName**</span></span> | <span data-ttu-id="1391a-169">定義資源群組的名稱，此指令碼所建立的項目將儲存在此資源群組中。</span><span class="sxs-lookup"><span data-stu-id="1391a-169">Define a name for a Resource Group in which items created by this script will be stored.</span></span> <span data-ttu-id="1391a-170">例如，*SqlRPRG*。</span><span class="sxs-lookup"><span data-stu-id="1391a-170">For example, *SqlRPRG*.</span></span> |  <span data-ttu-id="1391a-171">_必要_</span><span class="sxs-lookup"><span data-stu-id="1391a-171">_required_</span></span> |
| <span data-ttu-id="1391a-172">**VmName**</span><span class="sxs-lookup"><span data-stu-id="1391a-172">**VmName**</span></span> | <span data-ttu-id="1391a-173">定義哪個 tooinstall hello 資源提供者的 hello hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="1391a-173">Define hello name of hello virtual machine on which tooinstall hello resource provider.</span></span> <span data-ttu-id="1391a-174">例如，*SqlVM*。</span><span class="sxs-lookup"><span data-stu-id="1391a-174">For example, *SqlVM*.</span></span> |  <span data-ttu-id="1391a-175">_必要_</span><span class="sxs-lookup"><span data-stu-id="1391a-175">_required_</span></span> |
| <span data-ttu-id="1391a-176">**DependencyFilesLocalPath**</span><span class="sxs-lookup"><span data-stu-id="1391a-176">**DependencyFilesLocalPath**</span></span> | <span data-ttu-id="1391a-177">您的憑證檔案也必須放在這個目錄中。</span><span class="sxs-lookup"><span data-stu-id="1391a-177">Your certificate files must be placed in this directory as well.</span></span> | <span data-ttu-id="1391a-178">_選用_</span><span class="sxs-lookup"><span data-stu-id="1391a-178">_optional_</span></span> |
| <span data-ttu-id="1391a-179">**DefaultSSLCertificatePassword**</span><span class="sxs-lookup"><span data-stu-id="1391a-179">**DefaultSSLCertificatePassword**</span></span> | <span data-ttu-id="1391a-180">hello hello.pfx 憑證的密碼</span><span class="sxs-lookup"><span data-stu-id="1391a-180">hello password for hello .pfx certificate</span></span> | <span data-ttu-id="1391a-181">_必要_</span><span class="sxs-lookup"><span data-stu-id="1391a-181">_required_</span></span> |
| <span data-ttu-id="1391a-182">**MaxRetryCount**</span><span class="sxs-lookup"><span data-stu-id="1391a-182">**MaxRetryCount**</span></span> | <span data-ttu-id="1391a-183">定義您要讓 tooretry 每個作業是否有多少次失敗。</span><span class="sxs-lookup"><span data-stu-id="1391a-183">Define how many times you want tooretry each operation if there is a failure.</span></span>| <span data-ttu-id="1391a-184">2</span><span class="sxs-lookup"><span data-stu-id="1391a-184">2</span></span> |
| <span data-ttu-id="1391a-185">**RetryDuration**</span><span class="sxs-lookup"><span data-stu-id="1391a-185">**RetryDuration**</span></span> | <span data-ttu-id="1391a-186">定義 hello 重試之間，以秒為單位的逾時。</span><span class="sxs-lookup"><span data-stu-id="1391a-186">Define hello timeout between retries, in seconds.</span></span> | <span data-ttu-id="1391a-187">120</span><span class="sxs-lookup"><span data-stu-id="1391a-187">120</span></span> |
| <span data-ttu-id="1391a-188">**解除安裝**</span><span class="sxs-lookup"><span data-stu-id="1391a-188">**Uninstall**</span></span> | <span data-ttu-id="1391a-189">移除 hello 資源提供者和所有相關聯的資源 （請參閱下面的附註）</span><span class="sxs-lookup"><span data-stu-id="1391a-189">Remove hello resource provider and all associated resources (see notes below)</span></span> | <span data-ttu-id="1391a-190">否</span><span class="sxs-lookup"><span data-stu-id="1391a-190">No</span></span> |
| <span data-ttu-id="1391a-191">**DebugMode**</span><span class="sxs-lookup"><span data-stu-id="1391a-191">**DebugMode**</span></span> | <span data-ttu-id="1391a-192">防止在失敗時自動清除</span><span class="sxs-lookup"><span data-stu-id="1391a-192">Prevents automatic cleanup on failure</span></span> | <span data-ttu-id="1391a-193">否</span><span class="sxs-lookup"><span data-stu-id="1391a-193">No</span></span> |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a><span data-ttu-id="1391a-194">確認 hello 部署使用 hello Azure 堆疊入口網站</span><span class="sxs-lookup"><span data-stu-id="1391a-194">Verify hello deployment using hello Azure Stack Portal</span></span>

> [!NOTE]
>  <span data-ttu-id="1391a-195">Hello 安裝指令碼完成之後，您將需要 toorefresh hello 入口 toosee hello 管理刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1391a-195">After hello installation script completes, you will need toorefresh hello portal toosee hello admin blade.</span></span>


1. <span data-ttu-id="1391a-196">在 hello 主控台 VM 桌面上，按一下**Microsoft Azure 堆疊入口網站**toohello 入口網站以 hello 服務系統管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="1391a-196">On hello Console VM desktop, click **Microsoft Azure Stack Portal** and sign in toohello portal as hello service administrator.</span></span>

2. <span data-ttu-id="1391a-197">確認 hello 部署成功。</span><span class="sxs-lookup"><span data-stu-id="1391a-197">Verify that hello deployment succeeded.</span></span> <span data-ttu-id="1391a-198">按一下**資源群組**&gt;按一下 hello 您所使用的資源群組，然後確定 hello 刀鋒視窗 （上半部） 讀取該 hello essentials 部分**_日期_（成功）**.</span><span class="sxs-lookup"><span data-stu-id="1391a-198">Click **Resource Groups** &gt; click hello resource group you used and then make sure that hello essentials part of hello blade (upper half) reads **_date_ (Succeeded)**.</span></span>

      ![確認部署的 hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a><span data-ttu-id="1391a-200">藉由連接 tooa 主控 SQL server 提供的容量</span><span class="sxs-lookup"><span data-stu-id="1391a-200">Provide capacity by connecting tooa hosting SQL server</span></span>

1. <span data-ttu-id="1391a-201">Toohello Azure 堆疊系統管理員入口網站管理員身分登入服務</span><span class="sxs-lookup"><span data-stu-id="1391a-201">Sign in toohello Azure Stack admin portal as a service admin</span></span>

2. <span data-ttu-id="1391a-202">建立 SQL 虛擬機器 (除非您已經有 SQL 虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="1391a-202">Create a SQL virtual machine, unless you have one already available.</span></span> <span data-ttu-id="1391a-203">「Marketplace 管理」提供一些用於部署 SQL VM 的選項。</span><span class="sxs-lookup"><span data-stu-id="1391a-203">Marketplace Management offers some options for deploying SQL VMs.</span></span>

3. <span data-ttu-id="1391a-204">按一下 [資源提供者] &gt;[SQLAdapter] &gt;[主控伺服器] &gt;[+新增]。</span><span class="sxs-lookup"><span data-stu-id="1391a-204">Click **Resource Providers** &gt; **SQLAdapter** &gt; **Hosting Servers** &gt; **+Add**.</span></span>

    <span data-ttu-id="1391a-205">hello **SQL 主控伺服器**刀鋒視窗是您可以在此連接 hello SQL Server 資源提供者 tooactual SQL Server 執行個體，做為 hello 資源提供者的後端。</span><span class="sxs-lookup"><span data-stu-id="1391a-205">hello **SQL Hosting Servers** blade is where you can connect hello SQL Server Resource Provider tooactual instances of SQL Server that serve as hello resource provider’s backend.</span></span>

    ![主控伺服器](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. <span data-ttu-id="1391a-207">Hello 表單中填入 hello 連接詳細資料，您的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="1391a-207">Fill hello form with hello connection details of your SQL Server instance.</span></span>

    ![新的主控伺服器](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > <span data-ttu-id="1391a-209">只要的 hello 租用戶和管理 Azure 資源管理員，就可以存取 hello SQL 執行個體，就可以放受控制的 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="1391a-209">As long as hello SQL instance can be accessed by hello tenant and admin Azure Resource Manager, it can be placed under control of hello resource provider.</span></span> <span data-ttu-id="1391a-210">hello SQL 執行個體__必須__配置以獨佔方式 toohello RP。</span><span class="sxs-lookup"><span data-stu-id="1391a-210">hello SQL instance __must__ be allocated exclusively toohello RP.</span></span>

5. <span data-ttu-id="1391a-211">當您新增伺服器，您必須將它們指派 tooa 新的或現有 SKU toodifferentiate 服務供應項目。</span><span class="sxs-lookup"><span data-stu-id="1391a-211">As you add servers, you must assign them tooa new or existing SKU toodifferentiate service offerings.</span></span> <span data-ttu-id="1391a-212">例如，您可以提供資料庫容量和自動備份的 SQL Enterprise 執行個體，請保留各個部門高效能伺服器，等 hello SKU 名稱應反映 hello 屬性，以便租用戶可以將其資料庫適當地而且不應該有 SKU 中的所有主控伺服器 hello 相同的功能。</span><span class="sxs-lookup"><span data-stu-id="1391a-212">For example, you could have a SQL Enterprise instance providing database capacity and automatic backup, reserve high-performance servers for individual departments, etc. hello SKU name should reflect hello properties so that tenants can place their databases appropriately and all hosting servers in a SKU should have hello same capabilities.</span></span>

    <span data-ttu-id="1391a-213">例如：</span><span class="sxs-lookup"><span data-stu-id="1391a-213">An example:</span></span>

    ![SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
<span data-ttu-id="1391a-215">Sku 可以佔用 tooan 小時 toobe hello 入口網站中顯示。</span><span class="sxs-lookup"><span data-stu-id="1391a-215">SKUs can take up tooan hour toobe visible in hello portal.</span></span> <span data-ttu-id="1391a-216">您無法建立資料庫，直到建立 SKU 的 hello。</span><span class="sxs-lookup"><span data-stu-id="1391a-216">You cannot create a database until hello SKU is created.</span></span>


## <a name="create-your-first-sql-database-tootest-your-deployment"></a><span data-ttu-id="1391a-217">建立您第一次的 SQL 資料庫 tootest 部署</span><span class="sxs-lookup"><span data-stu-id="1391a-217">Create your first SQL database tootest your deployment</span></span>

1. <span data-ttu-id="1391a-218">登入 toohello 堆疊 Azure 系統管理入口網站為服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="1391a-218">Sign in toohello Azure Stack admin portal as service admin.</span></span>

2. <span data-ttu-id="1391a-219">按一下 [+新增] &gt;[資料+儲存體] &gt;[SQL Server 資料庫 (預覽)] &gt;[新增]。</span><span class="sxs-lookup"><span data-stu-id="1391a-219">Click **+ New** &gt;**Data + Storage"** &gt; **SQL Server Database (preview)** &gt; **Add**.</span></span>

3. <span data-ttu-id="1391a-220">請填寫 hello 表單的資料庫詳細資料，包括**資料庫名稱**，**大小上限**，並變更視 hello 其他參數。</span><span class="sxs-lookup"><span data-stu-id="1391a-220">Fill in hello form with database details, including a **Database Name**, **Maximum Size**, and change hello other parameters as necessary.</span></span> <span data-ttu-id="1391a-221">您會為您的資料庫要求 toopick SKU。</span><span class="sxs-lookup"><span data-stu-id="1391a-221">You are asked toopick a SKU for your database.</span></span> <span data-ttu-id="1391a-222">當主控伺服器加入時，會指派給他們的 SKU，會建立資料庫的主控伺服器 hello SKU 構成該集區中。</span><span class="sxs-lookup"><span data-stu-id="1391a-222">As hosting servers are added, they are assigned a SKU and databases are created in that pool of hosting servers that make up hello SKU.</span></span>

    ![新資料庫](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. <span data-ttu-id="1391a-224">填寫 hello 登入設定：**資料庫登入**，和**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1391a-224">Fill in hello Login Settings: **Database login**, and **Password**.</span></span> <span data-ttu-id="1391a-225">這是針對只存取 toothis 資料庫所建立的 SQL 驗證認證。</span><span class="sxs-lookup"><span data-stu-id="1391a-225">This is a SQL Authentication credential that is created for your access toothis database only.</span></span> <span data-ttu-id="1391a-226">hello 登入使用者名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="1391a-226">hello login user name must be globally unique.</span></span> <span data-ttu-id="1391a-227">建立新的登入設定或選取現有的設定。</span><span class="sxs-lookup"><span data-stu-id="1391a-227">Either create a new login setting or select an existing one.</span></span> <span data-ttu-id="1391a-228">您可以重複使用登入設定，如使用其他資料庫 hello 相同 SKU。</span><span class="sxs-lookup"><span data-stu-id="1391a-228">You can reuse login settings for other databases using hello same SKU.</span></span>

    ![建立新的資料庫登入](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. <span data-ttu-id="1391a-230">送出 hello 表單，並等候 hello 部署 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="1391a-230">Submit hello form and wait for hello deployment toocomplete.</span></span>

    <span data-ttu-id="1391a-231">在 hello 產生刀鋒視窗中，會發現 hello 「 連接字串 」 欄位。</span><span class="sxs-lookup"><span data-stu-id="1391a-231">In hello resulting blade, notice hello “Connection string” field.</span></span> <span data-ttu-id="1391a-232">您可以在 Azure Stack 中，於需要 SQL Server 存取權的任何應用程式 (例如 Web 應用程式) 中使用該字串。</span><span class="sxs-lookup"><span data-stu-id="1391a-232">You can use that string in any application that requires SQL Server access (for example, a web app) in your Azure Stack.</span></span>

    ![擷取 hello 連接字串](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a><span data-ttu-id="1391a-234">新增容量</span><span class="sxs-lookup"><span data-stu-id="1391a-234">Add capacity</span></span>

<span data-ttu-id="1391a-235">新增其他的 SQL 主控 hello Azure 堆疊入口網站中新增容量，並將它們關聯適當的 SKU。</span><span class="sxs-lookup"><span data-stu-id="1391a-235">Add capacity by adding additional SQL hosts in hello Azure Stack portal and associate them with an appropriate SKU.</span></span> <span data-ttu-id="1391a-236">如果您想 toouse 另一個 SQL 執行個體而不是 hello hello 提供者 VM 上所安裝，請按一下**資源提供者** &gt; **SQLAdapter** &gt; **SQL 裝載伺服器** &gt; **+ 加入**。</span><span class="sxs-lookup"><span data-stu-id="1391a-236">If you wish toouse another instance of SQL instead of hello one installed on hello provider VM, click **Resource Providers** &gt; **SQLAdapter** &gt; **SQL Hosting Servers** &gt; **+Add**.</span></span>

## <a name="making-sql-databases-available-tootenants"></a><span data-ttu-id="1391a-237">提高 SQL 資料庫可用 tootenants</span><span class="sxs-lookup"><span data-stu-id="1391a-237">Making SQL databases available tootenants</span></span>

<span data-ttu-id="1391a-238">建立租用戶計畫與優惠 toomake 可用的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1391a-238">Create plans and offers toomake SQL databases available for tenants.</span></span> <span data-ttu-id="1391a-239">您必須建立計劃、 加入 hello Microsoft.SqlAdapter 服務 toohello 計劃，加入現有的配額，或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="1391a-239">You must create a plan, add hello Microsoft.SqlAdapter service toohello plan, and add an existing Quota, or create a new one.</span></span> <span data-ttu-id="1391a-240">如果您建立配額時，您可以指定 hello 容量 tooallow hello 租用戶。</span><span class="sxs-lookup"><span data-stu-id="1391a-240">If you create a quota, you can specify hello capacity tooallow hello tenant.</span></span>
    <span data-ttu-id="1391a-241">![建立計劃和優惠 tooinclude 資料庫](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span><span class="sxs-lookup"><span data-stu-id="1391a-241">![Create plans and offers tooinclude databases](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)</span></span>

## <a name="tenant-usage-of-hello-resource-provider"></a><span data-ttu-id="1391a-242">Hello 資源提供者的租用戶使用量</span><span class="sxs-lookup"><span data-stu-id="1391a-242">Tenant usage of hello Resource Provider</span></span>

<span data-ttu-id="1391a-243">透過 hello 租用戶入口網站體驗提供自助服務資料庫。</span><span class="sxs-lookup"><span data-stu-id="1391a-243">Self-service databases are provided through hello tenant portal experience.</span></span>

## <a name="removing-hello-sql-adapter-resource-provider"></a><span data-ttu-id="1391a-244">移除 hello SQL 配接器資源提供者</span><span class="sxs-lookup"><span data-stu-id="1391a-244">Removing hello SQL Adapter Resource Provider</span></span>

<span data-ttu-id="1391a-245">在訂單 tooremove hello 資源提供者，務必 toofirst 移除任何相依性。</span><span class="sxs-lookup"><span data-stu-id="1391a-245">In order tooremove hello resource provider, it is essential toofirst remove any dependencies.</span></span>

1. <span data-ttu-id="1391a-246">確定您擁有 hello 原始部署套件下載這個版本的 hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="1391a-246">Ensure you have hello original deployment package that you downloaded for this version of hello Resource Provider.</span></span>

2. <span data-ttu-id="1391a-247">從 hello 資源提供者 （這不會刪除 hello 資料），必須刪除所有租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="1391a-247">All tenant databases must be deleted from hello resource provider (this will not delete hello data).</span></span> <span data-ttu-id="1391a-248">應該執行此作業由 hello 租用戶本身。</span><span class="sxs-lookup"><span data-stu-id="1391a-248">This should be performed by hello tenants themselves.</span></span>

3. <span data-ttu-id="1391a-249">系統管理員必須先刪除主控伺服器 hello SQL 配接器從 hello</span><span class="sxs-lookup"><span data-stu-id="1391a-249">Administrator must delete hello hosting servers from hello SQL Adapter</span></span>

4. <span data-ttu-id="1391a-250">系統管理員必須先刪除任何參考 hello SQL 配接器的計劃。</span><span class="sxs-lookup"><span data-stu-id="1391a-250">Administrator must delete any plans that reference hello SQL Adapter.</span></span>

5. <span data-ttu-id="1391a-251">系統管理員必須先刪除任何 Sku 與配額 toohello SQL 配接器。</span><span class="sxs-lookup"><span data-stu-id="1391a-251">Administrator must delete any SKUs and quotas associated toohello SQL Adapter.</span></span>

6. <span data-ttu-id="1391a-252">重新執行具有 hello 部署指令碼 hello-解除安裝參數，Azure 資源管理員端點、 DirectoryTenantID 和 hello 服務系統管理員帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="1391a-252">Rerun hello deployment script with hello -Uninstall parameter, Azure Resource Manager endpoints, DirectoryTenantID, and credentials for hello service administrator account.</span></span>



## <a name="next-steps"></a><span data-ttu-id="1391a-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1391a-253">Next steps</span></span>


<span data-ttu-id="1391a-254">請嘗試其他[PaaS 服務](azure-stack-tools-paas-services.md)像 hello [MySQL Server 資源提供者](azure-stack-mysql-resource-provider-deploy.md)和 hello[應用程式服務資源提供者](azure-stack-app-service-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1391a-254">Try other [PaaS services](azure-stack-tools-paas-services.md) like hello [MySQL Server resource provider](azure-stack-mysql-resource-provider-deploy.md) and hello [App Services resource provider](azure-stack-app-service-overview.md).</span></span>
