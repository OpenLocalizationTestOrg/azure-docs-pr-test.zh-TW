---
title: "安裝彈性資料庫工作 | Microsoft Docs"
description: "逐步解說如何安裝彈性工作功能。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: cbe0aa2b-17e3-4b6f-a16f-6ebc1f5a66af
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: e7a2d6dbcefbb31d76257eaf96ccc235d7a29416
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="b6096-103">安裝彈性資料庫工作概觀</span><span class="sxs-lookup"><span data-stu-id="b6096-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="b6096-104">您可以透過 PowerShell 或透過「Azure 傳統入口網站」安裝[**彈性資料庫工作**](sql-database-elastic-jobs-overview.md)。只有在安裝 PowerShell 套件的情況下，您才能取得可使用 PowerShell API 來建立和管理工作的存取權。</span><span class="sxs-lookup"><span data-stu-id="b6096-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through the Azure Classic Portal.You can gain access to create and manage jobs using the PowerShell API only if you install the PowerShell package.</span></span> <span data-ttu-id="b6096-105">此外，PowerShell API 目前比入口網站提供更多的功能。</span><span class="sxs-lookup"><span data-stu-id="b6096-105">Additionally, the PowerShell APIs provide significantly more functionality than the portal at this point in time.</span></span>

<span data-ttu-id="b6096-106">如果您已透過「入口網站」從現有的「彈性集區」安裝「彈性資料庫工作」，最新的 Powershell 預覽版包含可升級現有安裝的指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6096-106">If you have already installed **Elastic Database jobs** through the Portal from an existing **elastic pool**, the latest Powershell preview includes scripts to upgrade your existing installation.</span></span> <span data-ttu-id="b6096-107">強烈建議將安裝升級至最新的 **彈性資料庫工作** 元件，以利用透過 PowerShell API 公開的新功能。</span><span class="sxs-lookup"><span data-stu-id="b6096-107">It is highly recommended to upgrade your installation to the latest **Elastic Database jobs** components in order to take advantage of new functionality exposed via the PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6096-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="b6096-108">Prerequisites</span></span>
* <span data-ttu-id="b6096-109">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6096-109">An Azure subscription.</span></span> <span data-ttu-id="b6096-110">如需免費試用版，請參閱 [免費試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b6096-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b6096-111">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b6096-111">Azure PowerShell.</span></span> <span data-ttu-id="b6096-112">使用 [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376)安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="b6096-112">Install the latest version using the [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="b6096-113">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b6096-113">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="b6096-114">[NuGet 命令列公用程式](https://nuget.org/nuget.exe) 可用來安裝彈性資料庫工作封裝。</span><span class="sxs-lookup"><span data-stu-id="b6096-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used to install the Elastic Database jobs package.</span></span> <span data-ttu-id="b6096-115">如需詳細資訊，請參閱 http://docs.nuget.org/docs/start-here/installing-nuget。</span><span class="sxs-lookup"><span data-stu-id="b6096-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-the-elastic-database-jobs-powershell-package"></a><span data-ttu-id="b6096-116">下載並匯入彈性資料庫工作 PowerShell 封裝</span><span class="sxs-lookup"><span data-stu-id="b6096-116">Download and import the Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="b6096-117">啟動 Microsoft Azure PowerShell 命令視窗，並瀏覽至您下載 NuGet 命令列公用程式 (nuget.exe) 的目錄。</span><span class="sxs-lookup"><span data-stu-id="b6096-117">Launch Microsoft Azure PowerShell command window and navigate to the directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="b6096-118">利用下列命令，將 **彈性資料庫工作** 封裝下載並匯入到目前的目錄：</span><span class="sxs-lookup"><span data-stu-id="b6096-118">Download and import **Elastic Database jobs** package into the current directory with the following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="b6096-119">「彈性資料庫工作」檔案會放在本機目錄中名為 **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** 的資料夾中，其中 *x.x.xxxx.x* 反映的是版本號碼。</span><span class="sxs-lookup"><span data-stu-id="b6096-119">The **Elastic Database jobs** files are placed in the local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects the version number.</span></span> <span data-ttu-id="b6096-120">PowerShell Cmdlet (包括必要的用戶端 .dll 檔) 位於 **tools\ElasticDatabaseJobs** 子目錄中，而要安裝、升級及解除安裝的 PowerShell 指令碼也位於 [tools] 子目錄中。</span><span class="sxs-lookup"><span data-stu-id="b6096-120">The PowerShell cmdlets (including required client .dlls) are located in the **tools\ElasticDatabaseJobs** sub-directory and the PowerShell scripts to install, upgrade and uninstall also reside in the **tools** sub-directory.</span></span>
3. <span data-ttu-id="b6096-121">例如，輸入  cd tools，瀏覽至 Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 資料夾下的 tools 子目錄：</span><span class="sxs-lookup"><span data-stu-id="b6096-121">Navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="b6096-122">執行 .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules。</span><span class="sxs-lookup"><span data-stu-id="b6096-122">Execute the .\InstallElasticDatabaseJobsCmdlets.ps1 script to copy the ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="b6096-123">這也會自動匯入模組，以供使用，例如：</span><span class="sxs-lookup"><span data-stu-id="b6096-123">This will also automatically import the module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-the-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="b6096-124">使用 PowerShell 安裝彈性資料庫工作元件</span><span class="sxs-lookup"><span data-stu-id="b6096-124">Install the Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="b6096-125">啟動 Microsoft Azure PowerShell 命令視窗，並且瀏覽至 Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 資料夾底下的 \tools 子目錄：輸入 cd \tools</span><span class="sxs-lookup"><span data-stu-id="b6096-125">Launch a Microsoft Azure PowerShell command window and navigate to the \tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="b6096-126">執行.\InstallElasticDatabaseJobs.ps1 PowerShell 指令碼，並提供其所要求之變數的值。</span><span class="sxs-lookup"><span data-stu-id="b6096-126">Execute the .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="b6096-127">此指令碼將依 [彈性資料庫工作元件和定價](sql-database-elastic-jobs-overview.md#components-and-pricing) 所述建立元件，以及將 Azure 雲端服務設定為適當地使用相依元件。</span><span class="sxs-lookup"><span data-stu-id="b6096-127">This script will create the components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring the Azure Cloud Service to appropriately use the dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="b6096-128">當您執行此命令時，會開啟一個向您詢問「使用者名稱」和「密碼」的視窗。</span><span class="sxs-lookup"><span data-stu-id="b6096-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="b6096-129">這不是您的 Azure 認證，請輸入要用於新伺服器之系統管理員認證的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b6096-129">This is not your Azure credentials, enter the user name and password that will be the administrator credentials you want to create for the new server.</span></span>

<span data-ttu-id="b6096-130">在此範例引動過程上提供的參數可以進行修改，以適用於您所需的設定。</span><span class="sxs-lookup"><span data-stu-id="b6096-130">The parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="b6096-131">下列提供每個參數行為的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="b6096-131">The following provides more information on the behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="b6096-132">參數</span><span class="sxs-lookup"><span data-stu-id="b6096-132">Parameter</span></span></th>
    <th><span data-ttu-id="b6096-133">說明</span><span class="sxs-lookup"><span data-stu-id="b6096-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="b6096-134">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b6096-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="b6096-135">提供建立的 Azure 資源群組名稱，以包含新建的 Azure 元件。</span><span class="sxs-lookup"><span data-stu-id="b6096-135">Provides the Azure resource group name created to contain the newly created Azure components.</span></span> <span data-ttu-id="b6096-136">此參數預設為 “__ElasticDatabaseJob”。</span><span class="sxs-lookup"><span data-stu-id="b6096-136">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="b6096-137">不建議變更此值。</span><span class="sxs-lookup"><span data-stu-id="b6096-137">It is not recommended to change this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="b6096-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="b6096-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="b6096-139">提供要用於新建的 Azure 元件的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="b6096-139">Provides the Azure location to be used for the newly created Azure components.</span></span> <span data-ttu-id="b6096-140">此參數預設為美國中部位置。</span><span class="sxs-lookup"><span data-stu-id="b6096-140">This parameter defaults to the Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="b6096-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="b6096-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="b6096-142">提供要安裝的服務背景工作數目。</span><span class="sxs-lookup"><span data-stu-id="b6096-142">Provides the number of service workers to install.</span></span> <span data-ttu-id="b6096-143">此參數預設為 1。</span><span class="sxs-lookup"><span data-stu-id="b6096-143">This parameter defaults to 1.</span></span> <span data-ttu-id="b6096-144">可以使用更多的背景工作來相應放大服務，並提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="b6096-144">A higher number of workers can be used to scale out the service and to provide high availability.</span></span> <span data-ttu-id="b6096-145">建議針對需要服務的高可用性的部署使用 "2"。</span><span class="sxs-lookup"><span data-stu-id="b6096-145">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="b6096-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="b6096-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="b6096-147">提供在雲端服務內使用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b6096-147">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="b6096-148">此參數預設為 A0。</span><span class="sxs-lookup"><span data-stu-id="b6096-148">This parameter defaults to A0.</span></span> <span data-ttu-id="b6096-149">接受 A0/A1/A2/A3 的參數值，這會導致背景工作角色分別使用 ExtraSmall/Small/Medium/Large 大小。</span><span class="sxs-lookup"><span data-stu-id="b6096-149">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="b6096-150">如需有關背景工作角色大小的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</span><span class="sxs-lookup"><span data-stu-id="b6096-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="b6096-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="b6096-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="b6096-152">提供 Standard Edition 的服務等級目標。</span><span class="sxs-lookup"><span data-stu-id="b6096-152">Provides the service level objective for a Standard edition.</span></span> <span data-ttu-id="b6096-153">此參數預設為 S0。</span><span class="sxs-lookup"><span data-stu-id="b6096-153">This parameter defaults to S0.</span></span> <span data-ttu-id="b6096-154">接受 S0/S1/S2/S3 的參數值，這會導致 Azure SQL Database 使用各自的 SLO。</span><span class="sxs-lookup"><span data-stu-id="b6096-154">Parameter values of S0/S1/S2/S3 are accepted which cause the Azure SQL Database to use the respective SLO.</span></span> <span data-ttu-id="b6096-155">如需有關 SQL Database SLO 的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</span><span class="sxs-lookup"><span data-stu-id="b6096-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="b6096-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="b6096-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="b6096-157">提供新建的 Azure SQL Database 伺服器的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b6096-157">Provides the admin user name for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="b6096-158">未指定時，將開啟 PowerShell 認證視窗，提示輸入認證。</span><span class="sxs-lookup"><span data-stu-id="b6096-158">When not specified, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="b6096-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="b6096-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="b6096-160">提供新建的 Azure SQL Database 伺服器的系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="b6096-160">Provides the admin password for the newly created Azure SQL Database server.</span></span> <span data-ttu-id="b6096-161">未提供時，將開啟 PowerShell 認證視窗，提示輸入認證。</span><span class="sxs-lookup"><span data-stu-id="b6096-161">When not provided, a PowerShell credentials window will open to prompt for the credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="b6096-162">對於將對大量資料庫具有大量平行執行的工作設為目標的系統，建議指定如下參數：-ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span><span class="sxs-lookup"><span data-stu-id="b6096-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended to specify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="b6096-163">使用 PowerShell 更新現有的彈性資料庫工作元件安裝</span><span class="sxs-lookup"><span data-stu-id="b6096-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="b6096-164">**彈性資料庫工作** 可以在現有的安裝中更新，以進行擴充和高可用性。</span><span class="sxs-lookup"><span data-stu-id="b6096-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="b6096-165">此程序允許未來的服務程式碼升級，而不需捨棄並重新建立控制資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6096-165">This process allows for future upgrades of service code without having to drop and recreate the control database.</span></span> <span data-ttu-id="b6096-166">此程序也可在相同版本內用來修改服務的 VM 大小或伺服器的背景工作計數。</span><span class="sxs-lookup"><span data-stu-id="b6096-166">This process can also be used within the same version to modify the service VM size or the server worker count.</span></span>

<span data-ttu-id="b6096-167">若要更新安裝的 VM 大小，請執行下列指令碼，並將參數更新為您選擇的值。</span><span class="sxs-lookup"><span data-stu-id="b6096-167">To update the VM size of an installation, run the following script with parameters updated to the values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="b6096-168">參數</span><span class="sxs-lookup"><span data-stu-id="b6096-168">Parameter</span></span></th>
  <th><span data-ttu-id="b6096-169">說明</span><span class="sxs-lookup"><span data-stu-id="b6096-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="b6096-170">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b6096-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="b6096-171">識別一開始安裝彈性資料庫工作元件時所使用的 Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="b6096-171">Identifies the Azure resource group name used when the Elastic Database job components were initially installed.</span></span> <span data-ttu-id="b6096-172">此參數預設為 “__ElasticDatabaseJob”。</span><span class="sxs-lookup"><span data-stu-id="b6096-172">This parameter defaults to “__ElasticDatabaseJob”.</span></span> <span data-ttu-id="b6096-173">不建議變更此值，因為您應該不必指定此參數。</span><span class="sxs-lookup"><span data-stu-id="b6096-173">Since it is not recommended to change this value, you shouldn't have to specify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="b6096-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="b6096-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="b6096-175">提供要安裝的服務背景工作數目。</span><span class="sxs-lookup"><span data-stu-id="b6096-175">Provides the number of service workers to install.</span></span>  <span data-ttu-id="b6096-176">此參數預設為 1。</span><span class="sxs-lookup"><span data-stu-id="b6096-176">This parameter defaults to 1.</span></span>  <span data-ttu-id="b6096-177">可以使用更多的背景工作來相應放大服務，並提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="b6096-177">A higher number of workers can be used to scale out the service and to provide high availability.</span></span>  <span data-ttu-id="b6096-178">建議針對需要服務的高可用性的部署使用 "2"。</span><span class="sxs-lookup"><span data-stu-id="b6096-178">It is recommended to use “2” for deployments that require high availability of the service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="b6096-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="b6096-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="b6096-180">提供在雲端服務內使用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="b6096-180">Provides the VM size for usage within the Cloud Service.</span></span> <span data-ttu-id="b6096-181">此參數預設為 A0。</span><span class="sxs-lookup"><span data-stu-id="b6096-181">This parameter defaults to A0.</span></span> <span data-ttu-id="b6096-182">接受 A0/A1/A2/A3 的參數值，這會導致背景工作角色分別使用 ExtraSmall/Small/Medium/Large 大小。</span><span class="sxs-lookup"><span data-stu-id="b6096-182">Parameters values of A0/A1/A2/A3 are accepted which cause the worker role to use an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="b6096-183">如需有關背景工作角色大小的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</span><span class="sxs-lookup"><span data-stu-id="b6096-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-the-elastic-database-jobs-components-using-the-portal"></a><span data-ttu-id="b6096-184">使用入口網站安裝彈性資料庫工作元件</span><span class="sxs-lookup"><span data-stu-id="b6096-184">Install the Elastic Database jobs components using the Portal</span></span>
<span data-ttu-id="b6096-185">在[建立彈性資料庫集區](sql-database-elastic-pool-manage-portal.md)之後，您可以安裝「彈性資料庫工作」元件，以便能夠對彈性集區中的每個資料庫執行系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="b6096-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components to enable execution of administrative tasks against each database in the elastic pool.</span></span> <span data-ttu-id="b6096-186">不同於使用 **彈性資料庫工作** PowerShell API 時，入口網站介面目前限制為只針對現有的集區執行。</span><span class="sxs-lookup"><span data-stu-id="b6096-186">Unlike when using the **Elastic Database jobs** PowerShell APIs, the portal interface is currently restricted to only executing against an existing pool.</span></span>

<span data-ttu-id="b6096-187">**預估完成時間：** 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="b6096-187">**Estimated time to complete:** 10 minutes.</span></span>

1. <span data-ttu-id="b6096-188">透過 [Azure 入口網站](https://portal.azure.com/#)，從彈性集區的儀表板檢視按一下 [建立工作]。</span><span class="sxs-lookup"><span data-stu-id="b6096-188">From the dashboard view of the elastic pool via the [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="b6096-189">如果您是第一次建立工作，則必須按一下 [預覽條款] 來安裝「彈性資料庫工作」。</span><span class="sxs-lookup"><span data-stu-id="b6096-189">If you are creating a job for the first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="b6096-190">然後按一下核取方塊接受條款。</span><span class="sxs-lookup"><span data-stu-id="b6096-190">Accept the terms by clicking the checkbox.</span></span>
4. <span data-ttu-id="b6096-191">在 [安裝服務] 檢視中，按一下 [工作認證] 。</span><span class="sxs-lookup"><span data-stu-id="b6096-191">In the "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![安裝服務][1]
5. <span data-ttu-id="b6096-193">輸入資料庫管理員的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b6096-193">Type a user name and password for a database admin.</span></span> <span data-ttu-id="b6096-194">在安裝過程中，會建立新的 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b6096-194">As part of the installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="b6096-195">在這個新的伺服器內，會建立稱為控制資料庫的新資料庫，並用來包含彈性資料庫工作的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="b6096-195">Within this new server, a new database, known as the control database, is created and used to contain the meta data for Elastic Database jobs.</span></span> <span data-ttu-id="b6096-196">這裡建立的使用者名稱和密碼用於登入控制資料庫。</span><span class="sxs-lookup"><span data-stu-id="b6096-196">The user name and password created here are used for the purpose of logging in to the control database.</span></span> <span data-ttu-id="b6096-197">個別的認證用於對集區內的資料庫執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6096-197">A separate credential is used for script execution against the databases within the pool.</span></span>
   
    ![建立使用者名稱和密碼][2]
6. <span data-ttu-id="b6096-199">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6096-199">Click the OK button.</span></span> <span data-ttu-id="b6096-200">幾分鐘內，就會在新的[資源群組](../azure-resource-manager/resource-group-overview.md)中為您建立元件。</span><span class="sxs-lookup"><span data-stu-id="b6096-200">The components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b6096-201">新的資源群組已釘選到「開始面板」，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b6096-201">The new resource group is pinned to the start board, as shown below.</span></span> <span data-ttu-id="b6096-202">建立後，會在群組中建立所有彈性資料庫工作 (雲端服務、SQL Database、服務匯流排和儲存體)。</span><span class="sxs-lookup"><span data-stu-id="b6096-202">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in the group.</span></span>
   
    ![「開始面板」中的資源群組][3]
7. <span data-ttu-id="b6096-204">如果您嘗試在安裝彈性資料庫工作時建立或管理工作，您會在提供 **認證** 時看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="b6096-204">If you attempt to create or manage a job while elastic database jobs is installing, when providing **Credentials** you will see the following message.</span></span>
   
    ![部署仍在進行中][4]

<span data-ttu-id="b6096-206">如果需要解除安裝，請刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="b6096-206">If uninstallation is required, delete the resource group.</span></span> <span data-ttu-id="b6096-207">請參閱 [如何解除安裝彈性資料庫工作元件](sql-database-elastic-jobs-uninstall.md)。</span><span class="sxs-lookup"><span data-stu-id="b6096-207">See [How to uninstall the Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6096-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6096-208">Next steps</span></span>
<span data-ttu-id="b6096-209">確定在群組中的每個資料庫上建立具備適當指令碼執行權限的認證，如需詳細資訊，請參閱[保護您的 SQL Database](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="b6096-209">Ensure a credential with the appropriate rights for script execution is created on each database in the group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="b6096-210">請參閱[建立和管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)以開始進行。</span><span class="sxs-lookup"><span data-stu-id="b6096-210">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) to get started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
