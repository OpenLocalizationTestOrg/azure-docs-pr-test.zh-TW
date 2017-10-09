---
title: "aaaInstalling 彈性資料庫工作 |Microsoft 文件"
description: "逐步解說 hello 彈性的工作功能的安裝。"
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
ms.openlocfilehash: 0349f66a4428f81d00d43681d7f2177f273ec032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="installing-elastic-database-jobs-overview"></a><span data-ttu-id="f4de6-103">安裝彈性資料庫工作概觀</span><span class="sxs-lookup"><span data-stu-id="f4de6-103">Installing Elastic Database jobs overview</span></span>
<span data-ttu-id="f4de6-104">[**彈性資料庫工作**](sql-database-elastic-jobs-overview.md)可以透過 PowerShell 來安裝或透過 hello Azure 傳統 Portal.You 可以獲得存取 toocreate 和安裝 hello PowerShell 封裝時才使用 hello PowerShell API 來管理工作。</span><span class="sxs-lookup"><span data-stu-id="f4de6-104">[**Elastic Database jobs**](sql-database-elastic-jobs-overview.md) can be installed via PowerShell or through hello Azure Classic Portal.You can gain access toocreate and manage jobs using hello PowerShell API only if you install hello PowerShell package.</span></span> <span data-ttu-id="f4de6-105">此外，hello PowerShell Api 提供更多的功能比 hello 入口網站在此時間點。</span><span class="sxs-lookup"><span data-stu-id="f4de6-105">Additionally, hello PowerShell APIs provide significantly more functionality than hello portal at this point in time.</span></span>

<span data-ttu-id="f4de6-106">如果您已安裝**彈性資料庫工作**透過 hello 入口網站，從現有**彈性集區**，hello 最新的 Powershell preview 包含指令碼 tooupgrade 現有的安裝。</span><span class="sxs-lookup"><span data-stu-id="f4de6-106">If you have already installed **Elastic Database jobs** through hello Portal from an existing **elastic pool**, hello latest Powershell preview includes scripts tooupgrade your existing installation.</span></span> <span data-ttu-id="f4de6-107">它強烈建議的最新 tooupgrade 安裝 toohello**彈性資料庫工作**順序 tootake 利用透過公開的新功能中的元件 hello PowerShell Api。</span><span class="sxs-lookup"><span data-stu-id="f4de6-107">It is highly recommended tooupgrade your installation toohello latest **Elastic Database jobs** components in order tootake advantage of new functionality exposed via hello PowerShell APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4de6-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f4de6-108">Prerequisites</span></span>
* <span data-ttu-id="f4de6-109">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4de6-109">An Azure subscription.</span></span> <span data-ttu-id="f4de6-110">如需免費試用版，請參閱 [免費試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-110">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f4de6-111">Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f4de6-111">Azure PowerShell.</span></span> <span data-ttu-id="f4de6-112">安裝使用 hello hello 最新版本[Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-112">Install hello latest version using hello [Web Platform Installer](http://go.microsoft.com/fwlink/p/?linkid=320376).</span></span> <span data-ttu-id="f4de6-113">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-113">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f4de6-114">[NuGet 命令列公用程式](https://nuget.org/nuget.exe)是使用的 tooinstall hello 彈性資料庫工作的封裝。</span><span class="sxs-lookup"><span data-stu-id="f4de6-114">[NuGet Command-line Utility](https://nuget.org/nuget.exe) is used tooinstall hello Elastic Database jobs package.</span></span> <span data-ttu-id="f4de6-115">如需詳細資訊，請參閱 http://docs.nuget.org/docs/start-here/installing-nuget。</span><span class="sxs-lookup"><span data-stu-id="f4de6-115">For more information, see http://docs.nuget.org/docs/start-here/installing-nuget.</span></span>

## <a name="download-and-import-hello-elastic-database-jobs-powershell-package"></a><span data-ttu-id="f4de6-116">下載並匯入 hello 彈性資料庫工作 PowerShell 封裝</span><span class="sxs-lookup"><span data-stu-id="f4de6-116">Download and import hello Elastic Database jobs PowerShell package</span></span>
1. <span data-ttu-id="f4de6-117">啟動 Microsoft Azure PowerShell 命令視窗並瀏覽 toohello 下載的目錄，NuGet 命令列公用程式 (nuget.exe)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-117">Launch Microsoft Azure PowerShell command window and navigate toohello directory where you downloaded NuGet Command-line Utility (nuget.exe).</span></span>
2. <span data-ttu-id="f4de6-118">下載並匯入**彈性資料庫工作**封裝到 hello 目前目錄中以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f4de6-118">Download and import **Elastic Database jobs** package into hello current directory with hello following command:</span></span>
   
        PS C:\>.\nuget install Microsoft.Azure.SqlDatabase.Jobs -prerelease
   
    <span data-ttu-id="f4de6-119">hello**彈性資料庫工作**檔案會放在資料夾中的 hello 本機目錄**Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x**其中*x.x.xxxx.x*反映 hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="f4de6-119">hello **Elastic Database jobs** files are placed in hello local directory in a folder named **Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x** where *x.x.xxxx.x* reflects hello version number.</span></span> <span data-ttu-id="f4de6-120">hello PowerShell cmdlet （包括必要的用戶端.dll 檔） 位於 hello **tools\ElasticDatabaseJobs**子目錄 hello PowerShell 指令碼 tooinstall，升級和解除安裝也位於 hello **工具**子目錄。</span><span class="sxs-lookup"><span data-stu-id="f4de6-120">hello PowerShell cmdlets (including required client .dlls) are located in hello **tools\ElasticDatabaseJobs** sub-directory and hello PowerShell scripts tooinstall, upgrade and uninstall also reside in hello **tools** sub-directory.</span></span>
3. <span data-ttu-id="f4de6-121">輸入 cd 工具，例如瀏覽 toohello 工具子目錄 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x 資料夾底下：</span><span class="sxs-lookup"><span data-stu-id="f4de6-121">Navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder by typing cd tools, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

4. <span data-ttu-id="f4de6-122">執行的 hello.\InstallElasticDatabaseJobsCmdlets.ps1 指令碼 toocopy hello ElasticDatabaseJobs 目錄於 $home\Documents\WindowsPowerShell\Modules。</span><span class="sxs-lookup"><span data-stu-id="f4de6-122">Execute hello .\InstallElasticDatabaseJobsCmdlets.ps1 script toocopy hello ElasticDatabaseJobs directory into $home\Documents\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="f4de6-123">這將例如也會自動匯入供使用，hello 模組：</span><span class="sxs-lookup"><span data-stu-id="f4de6-123">This will also automatically import hello module for use, for example:</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobsCmdlets.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobsCmdlets.ps1

## <a name="install-hello-elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="f4de6-124">使用 PowerShell 的 hello 彈性資料庫工作元件安裝</span><span class="sxs-lookup"><span data-stu-id="f4de6-124">Install hello Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="f4de6-125">啟動 Microsoft Azure PowerShell 命令視窗並瀏覽 toohello \tools 子資料夾下的目錄 hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x： 輸入 cd \tools</span><span class="sxs-lookup"><span data-stu-id="f4de6-125">Launch a Microsoft Azure PowerShell command window and navigate toohello \tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxx.x folder: Type cd \tools</span></span>
   
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools

2. <span data-ttu-id="f4de6-126">執行 hello.\InstallElasticDatabaseJobs.ps1 PowerShell 指令碼，並且提供其要求的變數值。</span><span class="sxs-lookup"><span data-stu-id="f4de6-126">Execute hello .\InstallElasticDatabaseJobs.ps1 PowerShell script and supply values for its requested variables.</span></span> <span data-ttu-id="f4de6-127">此指令碼會建立描述 hello 元件[彈性資料庫工作的元件和定價](sql-database-elastic-jobs-overview.md#components-and-pricing)以及設定 Azure 雲端服務的 hello tooappropriately 使用 hello 相依元件。</span><span class="sxs-lookup"><span data-stu-id="f4de6-127">This script will create hello components described in [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing) along with configuring hello Azure Cloud Service tooappropriately use hello dependent components.</span></span>

        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
        PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\InstallElasticDatabaseJobs.ps1

<span data-ttu-id="f4de6-128">當您執行此命令時，會開啟一個向您詢問「使用者名稱」和「密碼」的視窗。</span><span class="sxs-lookup"><span data-stu-id="f4de6-128">When you run this command a window opens asking for a **user name** and **password**.</span></span> <span data-ttu-id="f4de6-129">這不是您的 Azure 認證，請輸入 hello 使用者名稱和密碼，將會是您想要新的伺服器 hello toocreate hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="f4de6-129">This is not your Azure credentials, enter hello user name and password that will be hello administrator credentials you want toocreate for hello new server.</span></span>

<span data-ttu-id="f4de6-130">這個範例引動過程上提供的 hello 參數都可以修改您所需的設定。</span><span class="sxs-lookup"><span data-stu-id="f4de6-130">hello parameters provided on this sample invocation can be modified for your desired settings.</span></span> <span data-ttu-id="f4de6-131">hello 下列會提供有關每個參數的 hello 行為的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="f4de6-131">hello following provides more information on hello behavior of each parameter:</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="f4de6-132">參數</span><span class="sxs-lookup"><span data-stu-id="f4de6-132">Parameter</span></span></th>
    <th><span data-ttu-id="f4de6-133">說明</span><span class="sxs-lookup"><span data-stu-id="f4de6-133">Description</span></span></th>
  </tr>

<tr>
    <td><span data-ttu-id="f4de6-134">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="f4de6-134">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="f4de6-135">提供建立新建立的 Azure 元件的 toocontain hello hello Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="f4de6-135">Provides hello Azure resource group name created toocontain hello newly created Azure components.</span></span> <span data-ttu-id="f4de6-136">此參數的預設值太"__ElasticDatabaseJob"。</span><span class="sxs-lookup"><span data-stu-id="f4de6-136">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="f4de6-137">不建議 toochange 此值。</span><span class="sxs-lookup"><span data-stu-id="f4de6-137">It is not recommended toochange this value.</span></span></td>
    </tr>

</tr>

    <tr>
    <td><span data-ttu-id="f4de6-138">ResourceGroupLocation</span><span class="sxs-lookup"><span data-stu-id="f4de6-138">ResourceGroupLocation</span></span></td>
    <td><span data-ttu-id="f4de6-139">提供用於新建立的 Azure 元件的 hello hello Azure 位置 toobe。</span><span class="sxs-lookup"><span data-stu-id="f4de6-139">Provides hello Azure location toobe used for hello newly created Azure components.</span></span> <span data-ttu-id="f4de6-140">此參數的預設值 toohello 美國中部位置。</span><span class="sxs-lookup"><span data-stu-id="f4de6-140">This parameter defaults toohello Central US location.</span></span></td>
</tr>

<tr>
    <td><span data-ttu-id="f4de6-141">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="f4de6-141">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="f4de6-142">提供服務工作者 tooinstall hello 數的字。</span><span class="sxs-lookup"><span data-stu-id="f4de6-142">Provides hello number of service workers tooinstall.</span></span> <span data-ttu-id="f4de6-143">此參數的預設值 too1。</span><span class="sxs-lookup"><span data-stu-id="f4de6-143">This parameter defaults too1.</span></span> <span data-ttu-id="f4de6-144">有較多的工作者可以使用的 tooscale 出 hello 服務和 tooprovide 高可用性。</span><span class="sxs-lookup"><span data-stu-id="f4de6-144">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span> <span data-ttu-id="f4de6-145">建議您針對需要高可用性的 hello 服務部署 toouse"2"。</span><span class="sxs-lookup"><span data-stu-id="f4de6-145">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
    </tr>

</tr>
    <tr>
    <td><span data-ttu-id="f4de6-146">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="f4de6-146">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="f4de6-147">提供 hello 雲端服務內的使用量 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="f4de6-147">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="f4de6-148">此參數的預設值 tooA0。</span><span class="sxs-lookup"><span data-stu-id="f4de6-148">This parameter defaults tooA0.</span></span> <span data-ttu-id="f4de6-149">接受 A0/A1/A2/A3 的參數值會造成 hello 背景工作角色 toouse ExtraSmall/小型/中等/大型大小，分別。</span><span class="sxs-lookup"><span data-stu-id="f4de6-149">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="f4de6-150">如需有關背景工作角色大小的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-150">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="f4de6-151">SqlServerDatabaseSlo</span><span class="sxs-lookup"><span data-stu-id="f4de6-151">SqlServerDatabaseSlo</span></span></td>
    <td><span data-ttu-id="f4de6-152">Standard edition 提供 hello 服務等級目標。</span><span class="sxs-lookup"><span data-stu-id="f4de6-152">Provides hello service level objective for a Standard edition.</span></span> <span data-ttu-id="f4de6-153">此參數的預設值 tooS0。</span><span class="sxs-lookup"><span data-stu-id="f4de6-153">This parameter defaults tooS0.</span></span> <span data-ttu-id="f4de6-154">接受的 S0/S1/S2/S3 的參數值會造成 hello Azure SQL Database toouse hello 各自的 SLO。</span><span class="sxs-lookup"><span data-stu-id="f4de6-154">Parameter values of S0/S1/S2/S3 are accepted which cause hello Azure SQL Database toouse hello respective SLO.</span></span> <span data-ttu-id="f4de6-155">如需有關 SQL Database SLO 的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-155">For more information on SQL Database SLOs, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="f4de6-156">SqlServerAdministratorUserName</span><span class="sxs-lookup"><span data-stu-id="f4de6-156">SqlServerAdministratorUserName</span></span></td>
    <td><span data-ttu-id="f4de6-157">提供 hello hello 新建立的 Azure SQL Database 伺服器的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f4de6-157">Provides hello admin user name for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="f4de6-158">未指定，PowerShell 認證視窗就會開啟 tooprompt hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f4de6-158">When not specified, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>

</tr>
    <tr>
    <td><span data-ttu-id="f4de6-159">SqlServerAdministratorPassword</span><span class="sxs-lookup"><span data-stu-id="f4de6-159">SqlServerAdministratorPassword</span></span></td>
    <td><span data-ttu-id="f4de6-160">提供新建立的 Azure SQL Database 伺服器 hello hello 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="f4de6-160">Provides hello admin password for hello newly created Azure SQL Database server.</span></span> <span data-ttu-id="f4de6-161">未提供時，PowerShell 認證視窗會開啟 tooprompt hello 認證。</span><span class="sxs-lookup"><span data-stu-id="f4de6-161">When not provided, a PowerShell credentials window will open tooprompt for hello credentials.</span></span></td>
</tr>
</table>

<span data-ttu-id="f4de6-162">對於需要大量的數字，以平行方式大量資料庫對執行中的作業為目標的系統，建議 toospecify 參數例如:-ServiceWorkerCount 2-ServiceVmSize A2-SqlServerDatabaseSlo S2。</span><span class="sxs-lookup"><span data-stu-id="f4de6-162">For systems that target having large numbers of jobs running in parallel against a large number of databases, it is recommended toospecify parameters such as: -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\InstallElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\InstallElasticDatabaseJobs.ps1 -ServiceWorkerCount 2 -ServiceVmSize A2 -SqlServerDatabaseSlo S2

## <a name="update-an-existing-elastic-database-jobs-components-installation-using-powershell"></a><span data-ttu-id="f4de6-163">使用 PowerShell 更新現有的彈性資料庫工作元件安裝</span><span class="sxs-lookup"><span data-stu-id="f4de6-163">Update an existing Elastic Database jobs components installation using PowerShell</span></span>
<span data-ttu-id="f4de6-164">**彈性資料庫工作** 可以在現有的安裝中更新，以進行擴充和高可用性。</span><span class="sxs-lookup"><span data-stu-id="f4de6-164">**Elastic Database jobs** can be updated within an existing installation for scale and high-availability.</span></span> <span data-ttu-id="f4de6-165">此程序而不需要 toodrop 允許未來升級的服務程式碼，並重新建立 hello 控制資料庫。</span><span class="sxs-lookup"><span data-stu-id="f4de6-165">This process allows for future upgrades of service code without having toodrop and recreate hello control database.</span></span> <span data-ttu-id="f4de6-166">此程序也可用於 hello 相同版本 toomodify hello 服務 VM 大小或 hello 伺服器背景工作計數。</span><span class="sxs-lookup"><span data-stu-id="f4de6-166">This process can also be used within hello same version toomodify hello service VM size or hello server worker count.</span></span>

<span data-ttu-id="f4de6-167">tooupdate hello VM 大小的安裝，執行下列指令碼參數的 hello 更新您所選擇的 toohello 值。</span><span class="sxs-lookup"><span data-stu-id="f4de6-167">tooupdate hello VM size of an installation, run hello following script with parameters updated toohello values of your choice.</span></span>

    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>Unblock-File .\UpdateElasticDatabaseJobs.ps1
    PS C:\*Microsoft.Azure.SqlDatabase.Jobs.dll.x.x.xxx.x*\tools>.\UpdateElasticDatabaseJobs.ps1 -ServiceVmSize A1 -ServiceWorkerCount 2

<table style="width:100%">
  <tr>
  <th><span data-ttu-id="f4de6-168">參數</span><span class="sxs-lookup"><span data-stu-id="f4de6-168">Parameter</span></span></th>
  <th><span data-ttu-id="f4de6-169">說明</span><span class="sxs-lookup"><span data-stu-id="f4de6-169">Description</span></span></th>
</tr>

  <tr>
    <td><span data-ttu-id="f4de6-170">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="f4de6-170">ResourceGroupName</span></span></td>
    <td><span data-ttu-id="f4de6-171">識別一開始安裝 hello 彈性資料庫工作的元件時所使用的 hello Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="f4de6-171">Identifies hello Azure resource group name used when hello Elastic Database job components were initially installed.</span></span> <span data-ttu-id="f4de6-172">此參數的預設值太"__ElasticDatabaseJob"。</span><span class="sxs-lookup"><span data-stu-id="f4de6-172">This parameter defaults too“__ElasticDatabaseJob”.</span></span> <span data-ttu-id="f4de6-173">因為它不是建議 toochange 此值，您不應該有 toospecify 這個參數。</span><span class="sxs-lookup"><span data-stu-id="f4de6-173">Since it is not recommended toochange this value, you shouldn't have toospecify this parameter.</span></span></td>
    </tr>
</tr>

</tr>

  <tr>
    <td><span data-ttu-id="f4de6-174">ServiceWorkerCount</span><span class="sxs-lookup"><span data-stu-id="f4de6-174">ServiceWorkerCount</span></span></td>
    <td><span data-ttu-id="f4de6-175">提供服務工作者 tooinstall hello 數的字。</span><span class="sxs-lookup"><span data-stu-id="f4de6-175">Provides hello number of service workers tooinstall.</span></span>  <span data-ttu-id="f4de6-176">此參數的預設值 too1。</span><span class="sxs-lookup"><span data-stu-id="f4de6-176">This parameter defaults too1.</span></span>  <span data-ttu-id="f4de6-177">有較多的工作者可以使用的 tooscale 出 hello 服務和 tooprovide 高可用性。</span><span class="sxs-lookup"><span data-stu-id="f4de6-177">A higher number of workers can be used tooscale out hello service and tooprovide high availability.</span></span>  <span data-ttu-id="f4de6-178">建議您針對需要高可用性的 hello 服務部署 toouse"2"。</span><span class="sxs-lookup"><span data-stu-id="f4de6-178">It is recommended toouse “2” for deployments that require high availability of hello service.</span></span></td>
</tr>

</tr>

    <tr>
    <td><span data-ttu-id="f4de6-179">ServiceVmSize</span><span class="sxs-lookup"><span data-stu-id="f4de6-179">ServiceVmSize</span></span></td>
    <td><span data-ttu-id="f4de6-180">提供 hello 雲端服務內的使用量 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="f4de6-180">Provides hello VM size for usage within hello Cloud Service.</span></span> <span data-ttu-id="f4de6-181">此參數的預設值 tooA0。</span><span class="sxs-lookup"><span data-stu-id="f4de6-181">This parameter defaults tooA0.</span></span> <span data-ttu-id="f4de6-182">接受 A0/A1/A2/A3 的參數值會造成 hello 背景工作角色 toouse ExtraSmall/小型/中等/大型大小，分別。</span><span class="sxs-lookup"><span data-stu-id="f4de6-182">Parameters values of A0/A1/A2/A3 are accepted which cause hello worker role toouse an ExtraSmall/Small/Medium/Large size, respectively.</span></span> <span data-ttu-id="f4de6-183">如需有關背景工作角色大小的詳細資訊，請參閱[彈性資料庫工作元件和價格](sql-database-elastic-jobs-overview.md#components-and-pricing)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-183">Fo more information on worker role sizes, see [Elastic Database jobs components and pricing](sql-database-elastic-jobs-overview.md#components-and-pricing).</span></span></td>
</tr>

</table>

## <a name="install-hello-elastic-database-jobs-components-using-hello-portal"></a><span data-ttu-id="f4de6-184">安裝 hello 彈性資料庫工作元件使用 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="f4de6-184">Install hello Elastic Database jobs components using hello Portal</span></span>
<span data-ttu-id="f4de6-185">一旦[建立彈性集區](sql-database-elastic-pool-manage-portal.md)，您可以安裝**彈性資料庫工作**元件 tooenable 執行 hello 彈性集區中的每個資料庫的系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="f4de6-185">Once you have [created an elastic pool](sql-database-elastic-pool-manage-portal.md), you can install **Elastic Database jobs** components tooenable execution of administrative tasks against each database in hello elastic pool.</span></span> <span data-ttu-id="f4de6-186">不同於當使用 hello**彈性資料庫工作**PowerShell Api hello 入口網站介面是針對現有的集區執行的目前限制的 tooonly。</span><span class="sxs-lookup"><span data-stu-id="f4de6-186">Unlike when using hello **Elastic Database jobs** PowerShell APIs, hello portal interface is currently restricted tooonly executing against an existing pool.</span></span>

<span data-ttu-id="f4de6-187">**估計時間 toocomplete:** 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="f4de6-187">**Estimated time toocomplete:** 10 minutes.</span></span>

1. <span data-ttu-id="f4de6-188">Hello hello 透過彈性集區的 hello 儀表板檢視從[Azure 入口網站](https://portal.azure.com/#)，按一下 **建立工作**。</span><span class="sxs-lookup"><span data-stu-id="f4de6-188">From hello dashboard view of hello elastic pool via hello [Azure Portal](https://portal.azure.com/#) , click **Create job**.</span></span>
2. <span data-ttu-id="f4de6-189">如果您第一次建立 hello 的作業，您必須安裝**彈性資料庫工作**按一下**預覽條款**。</span><span class="sxs-lookup"><span data-stu-id="f4de6-189">If you are creating a job for hello first time, you must install **Elastic Database jobs** by clicking **PREVIEW TERMS**.</span></span>
3. <span data-ttu-id="f4de6-190">接受 hello 條款，依序按一下 hello 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f4de6-190">Accept hello terms by clicking hello checkbox.</span></span>
4. <span data-ttu-id="f4de6-191">在 hello 「 安裝服務 」 檢視中，按一下 **工作認證**。</span><span class="sxs-lookup"><span data-stu-id="f4de6-191">In hello "Install services" view, click **JOB CREDENTIALS**.</span></span>
   
    ![安裝 hello 服務][1]
5. <span data-ttu-id="f4de6-193">輸入資料庫管理員的使用者名稱和密碼。Hello 安裝的一部分，會建立新的 Azure SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f4de6-193">Type a user name and password for a database admin. As part of hello installation, a new Azure SQL Database server is created.</span></span> <span data-ttu-id="f4de6-194">在這個新的伺服器、 新的資料庫，又稱為 hello 控制資料庫，建立和 toocontain hello 中繼資料用於彈性資料庫工作。</span><span class="sxs-lookup"><span data-stu-id="f4de6-194">Within this new server, a new database, known as hello control database, is created and used toocontain hello meta data for Elastic Database jobs.</span></span> <span data-ttu-id="f4de6-195">這裡建立 hello 使用者名稱和密碼可用來在 toohello 控制資料庫中記錄的 hello 用途。</span><span class="sxs-lookup"><span data-stu-id="f4de6-195">hello user name and password created here are used for hello purpose of logging in toohello control database.</span></span> <span data-ttu-id="f4de6-196">執行指令碼針對 hello 集區中的 hello 資料庫使用不同的認證。</span><span class="sxs-lookup"><span data-stu-id="f4de6-196">A separate credential is used for script execution against hello databases within hello pool.</span></span>
   
    ![建立使用者名稱和密碼][2]
6. <span data-ttu-id="f4de6-198">按一下 [確定] 按鈕，hello。</span><span class="sxs-lookup"><span data-stu-id="f4de6-198">Click hello OK button.</span></span> <span data-ttu-id="f4de6-199">hello 元件會為您建立新的幾分鐘後[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-199">hello components are created for you in a few minutes in a new [Resource group](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="f4de6-200">hello 新資源群組已釘選 toohello 開始面板，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f4de6-200">hello new resource group is pinned toohello start board, as shown below.</span></span> <span data-ttu-id="f4de6-201">一旦建立後，彈性資料庫作業 （雲端服務、 SQL Database、 Service Bus 和儲存體） 會在 hello 群組建立。</span><span class="sxs-lookup"><span data-stu-id="f4de6-201">Once created, elastic database jobs (Cloud Service, SQL Database, Service Bus, and Storage) are all created in hello group.</span></span>
   
    ![「開始面板」中的資源群組][3]
7. <span data-ttu-id="f4de6-203">如果您嘗試 toocreate 或管理工作，但在安裝彈性資料庫工作，提供**認證**您會看到下列訊息的 hello。</span><span class="sxs-lookup"><span data-stu-id="f4de6-203">If you attempt toocreate or manage a job while elastic database jobs is installing, when providing **Credentials** you will see hello following message.</span></span>
   
    ![部署仍在進行中][4]

<span data-ttu-id="f4de6-205">如果需要解除安裝，請刪除 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="f4de6-205">If uninstallation is required, delete hello resource group.</span></span> <span data-ttu-id="f4de6-206">請參閱[toouninstall hello 彈性資料庫工作元件的方式](sql-database-elastic-jobs-uninstall.md)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-206">See [How toouninstall hello Elastic Database job components](sql-database-elastic-jobs-uninstall.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4de6-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4de6-207">Next steps</span></span>
<span data-ttu-id="f4de6-208">如需詳細資訊，請參閱 [hello] 群組中的每個資料庫建立指令碼執行所確保 hello 適當的權限的認證[保護您的 SQL Database](sql-database-manage-logins.md)。</span><span class="sxs-lookup"><span data-stu-id="f4de6-208">Ensure a credential with hello appropriate rights for script execution is created on each database in hello group, for more information see [Securing your SQL Database](sql-database-manage-logins.md).</span></span>
<span data-ttu-id="f4de6-209">請參閱[建立和管理彈性資料庫工作](sql-database-elastic-jobs-create-and-manage.md)tooget 啟動。</span><span class="sxs-lookup"><span data-stu-id="f4de6-209">See [Creating and managing an Elastic Database jobs](sql-database-elastic-jobs-create-and-manage.md) tooget started.</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-service-installation/screen-1.png
[2]: ./media/sql-database-elastic-jobs-service-installation/credentials.png
[3]: ./media/sql-database-elastic-jobs-service-installation/start-board.png
[4]: ./media/sql-database-elastic-jobs-service-installation/not-done.png
