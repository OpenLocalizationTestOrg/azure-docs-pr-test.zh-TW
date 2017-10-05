---
title: "建立適用於 PHP 的 Azure Web 和背景工作角色 | Microsoft Docs"
description: "在 Azure 雲端服務中建立 PHP Web 和背景工作角色及設定 PHP 執行階段的指南。"
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="3ab35-103">如何建立 PHP Web 和背景工作角色</span><span class="sxs-lookup"><span data-stu-id="3ab35-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="3ab35-104">Overview</span><span class="sxs-lookup"><span data-stu-id="3ab35-104">Overview</span></span>
<span data-ttu-id="3ab35-105">本指南將說明如何在 Windows 開發環境中建立 PHP Web 或背景工作角色、從「內建」的可用版本中選擇特定版本的 PHP、變更 PHP 組態、啟用擴充功能，最終部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="3ab35-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="3ab35-106">此外也會說明如何設定 Web 或背景工作角色，以使用您所提供的 PHP 執行階段 (具有自訂組態和擴充功能)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="3ab35-107">什麼是 PHP Web 和背景工作角色？</span><span class="sxs-lookup"><span data-stu-id="3ab35-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="3ab35-108">Azure 提供三種運算模型來執行應用程式：Azure 應用程式服務、Azure 虛擬機器和 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="3ab35-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="3ab35-109">這三種模型都支援 PHP。</span><span class="sxs-lookup"><span data-stu-id="3ab35-109">All three models support PHP.</span></span> <span data-ttu-id="3ab35-110">雲端服務 (包含 Web 和背景工作角色) 可提供 *平台即服務 (PaaS)*。</span><span class="sxs-lookup"><span data-stu-id="3ab35-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="3ab35-111">在雲端服務中，Web 角色提供專用的 Internet Information Services (IIS) Web 伺服器，用來代管前端 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ab35-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="3ab35-112">背景工作角色可以執行非同步、長時間或永久的工作，且不受使用者互動或輸入所影響。</span><span class="sxs-lookup"><span data-stu-id="3ab35-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="3ab35-113">如需這些選項的詳細資訊，請參閱[計算 Azure 提供的裝載選項](cloud-services/cloud-services-choose-me.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="3ab35-114">下載 Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="3ab35-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="3ab35-115">[Azure SDK for PHP] 由數個元件組成。</span><span class="sxs-lookup"><span data-stu-id="3ab35-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="3ab35-116">本文將使用下列兩個元件：Azure PowerShell 和 Azure 模擬器。</span><span class="sxs-lookup"><span data-stu-id="3ab35-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="3ab35-117">這兩個元件可透過 Microsoft Web Platform Installer 來安裝。</span><span class="sxs-lookup"><span data-stu-id="3ab35-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="3ab35-118">如需詳細資訊，請參閱 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="3ab35-119">建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="3ab35-119">Create a Cloud Services project</span></span>
<span data-ttu-id="3ab35-120">建立 PHP Web 或背景工作角色的第一個步驟是建立 Azure 服務專案。</span><span class="sxs-lookup"><span data-stu-id="3ab35-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="3ab35-121">Azure 服務專案可作為 Web 和背景工作角色的邏輯容器，且包含專案的[服務定義 (.csdef)] 和[服務組態 (.cscfg)] 檔案。</span><span class="sxs-lookup"><span data-stu-id="3ab35-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="3ab35-122">若要建立新的 Azure 服務專案，請以系統管理員身分執行 Azure PowerShell 並執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="3ab35-123">此命令會建立新目錄 (`myProject`)，讓您可將 Web 和背景工作角色新增至該處。</span><span class="sxs-lookup"><span data-stu-id="3ab35-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="3ab35-124">新增 PHP Web 或背景工作角色</span><span class="sxs-lookup"><span data-stu-id="3ab35-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="3ab35-125">若要將 PHP Web 角色新增至專案，請從專案的根目錄中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="3ab35-126">對於背景工作角色，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="3ab35-127">`roleName` 是選用參數。</span><span class="sxs-lookup"><span data-stu-id="3ab35-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="3ab35-128">若省略此參數，將會自動產生角色名稱。</span><span class="sxs-lookup"><span data-stu-id="3ab35-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="3ab35-129">第一個建立的 Web 角色將是 `WebRole1`、第二個將是 `WebRole2`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="3ab35-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="3ab35-130">第一個建立的背景工作角色將是 `WorkerRole1`、第二個將是 `WorkerRole2`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="3ab35-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="3ab35-131">指定內建 PHP 版本</span><span class="sxs-lookup"><span data-stu-id="3ab35-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="3ab35-132">當您將 PHP Web 或背景工作角色新增至專案時，專案的組態檔會進行修改，使應用程式在部署時，會將 PHP 安裝在其每個 Web 或背景工作執行個體上。</span><span class="sxs-lookup"><span data-stu-id="3ab35-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="3ab35-133">若要檢視依預設所將安裝的 PHP 版本，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="3ab35-134">前述命令的輸出會類似於下列內容。</span><span class="sxs-lookup"><span data-stu-id="3ab35-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="3ab35-135">在此範例中，會將 PHP 5.3.17 的 `IsDefault` 旗標設為 `true`，表示這是預設安裝的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="3ab35-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

<span data-ttu-id="3ab35-136">您可以將 PHP 執行階段版本設為任何列出的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="3ab35-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="3ab35-137">例如，若要將 PHP 版本 (針對名為 `roleName`的角色) 設為 5.4.0，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="3ab35-138">可用的 PHP 版本未來可能會變更。</span><span class="sxs-lookup"><span data-stu-id="3ab35-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="3ab35-139">自訂內建 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="3ab35-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="3ab35-140">對於您在前述步驟中安裝的 PHP 執行階段，您可以完整掌控其組態，包括修改 `php.ini` 設定和啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="3ab35-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="3ab35-141">若要自訂內建 PHP 執行階段，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3ab35-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="3ab35-142">將名為 `php` 的新資料夾新增至 Web 角色的 `bin` 目錄。</span><span class="sxs-lookup"><span data-stu-id="3ab35-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="3ab35-143">對於背景工作角色，請將其新增至角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="3ab35-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="3ab35-144">在`php` 資料夾中，建立另一個名為 `ext` 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="3ab35-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="3ab35-145">在此資料夾中放入任何您要啟用的 `.dll` 擴充功能檔案 (例如 `php_mongo.dll`)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="3ab35-146">將 `php.ini` 檔案新增至 `php` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3ab35-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="3ab35-147">在此檔案中啟用自訂擴充功能，並設定 PHP 指示詞。</span><span class="sxs-lookup"><span data-stu-id="3ab35-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="3ab35-148">例如，如果您要開啟 `display_errors`，並啟用 `php_mongo.dll` 擴充功能，則 `php.ini` 檔案的內容將如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ab35-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="3ab35-149">任何未在您提供的 `php.ini` 檔案中明確設定的設定，都將自動設為其預設值。</span><span class="sxs-lookup"><span data-stu-id="3ab35-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="3ab35-150">但請留意，您可以新增完整的 `php.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="3ab35-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="3ab35-151">使用您自己的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="3ab35-151">Use your own PHP runtime</span></span>
<span data-ttu-id="3ab35-152">在某些情況下，您可能會想要提供自己的 PHP 執行階段，而不依照前述的說明選取內建 PHP 執行階段並加以設定。</span><span class="sxs-lookup"><span data-stu-id="3ab35-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="3ab35-153">例如，您可以使用與在開發環境使用的 Web 或背景工作角色中相同的 PHP 執行階段。</span><span class="sxs-lookup"><span data-stu-id="3ab35-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="3ab35-154">這可讓您更輕鬆地確保應用程式在您的生產環境中不會變更行為。</span><span class="sxs-lookup"><span data-stu-id="3ab35-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="3ab35-155">設定 Web 角色以使用您自己的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="3ab35-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="3ab35-156">若要設定 Web 角色以使用您所提供的 PHP 執行階段，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3ab35-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="3ab35-157">如本主題先前所述，建立 Azure 服務專案並加入 PHP Web 角色。</span><span class="sxs-lookup"><span data-stu-id="3ab35-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="3ab35-158">在位於 Web 角色根目錄內的 `bin` 資料夾中建立 `php` 資料夾，然後將 PHP 執行階段 (所有的二進位檔、組態檔、子資料夾等) 新增至 `php` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3ab35-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="3ab35-159">(選擇性) 如果您的 PHP 執行階段使用[適用於 PHP for SQL Server 的 Microsoft 驅動程式][sqlsrv drivers]，您就必須將 Web 角色設定為在佈建時安裝 [SQL Server Native Client 2012][sql native client]。</span><span class="sxs-lookup"><span data-stu-id="3ab35-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="3ab35-160">若要執行此動作，請將 [請將sqlncli.msi x64 安裝程式] 新增至 Web 角色根目錄的 `bin` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3ab35-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="3ab35-161">下一個步驟中說明的啟動指令碼，將會在角色進行佈建時以無訊息方式執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3ab35-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="3ab35-162">如果您的 PHP 執行階段並未使用適用於 PHP for SQL Server 的 Microsoft 驅動程式，您可以從下一個步驟所顯示的指令碼中移除以下一行：</span><span class="sxs-lookup"><span data-stu-id="3ab35-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="3ab35-163">定義啟動工作，設定 [Internet Information Services (IIS)][iis.net] 使用您的 PHP 執行階段來處理 `.php` 頁面的要求。</span><span class="sxs-lookup"><span data-stu-id="3ab35-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="3ab35-164">若要執行此動作，請在文字編輯器中開啟 `setup_web.cmd` 檔案 (位於 Web 角色根目錄的 `bin` 檔案中)，並使用下列指令碼來取代它的內容：</span><span class="sxs-lookup"><span data-stu-id="3ab35-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. <span data-ttu-id="3ab35-165">將應用程式檔案新增至 Web 角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="3ab35-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="3ab35-166">這會是 Web 伺服器的根目錄。</span><span class="sxs-lookup"><span data-stu-id="3ab35-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="3ab35-167">如以下的[發佈您的應用程式](#publish-your-application)一節所述，發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ab35-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="3ab35-168">在執行前述步驟 (使用您自己的 PHP 執行階段) 之後，您可以將 `download.ps1` 指令碼 (位於 Web 角色根目錄的 `bin` 資料夾中) 刪除。</span><span class="sxs-lookup"><span data-stu-id="3ab35-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="3ab35-169">設定背景工作角色以使用您自己的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="3ab35-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="3ab35-170">若要設定背景工作角色以使用您所提供的 PHP 執行階段，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3ab35-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="3ab35-171">如本主題先前所述，建立 Azure 服務專案並加入 PHP 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="3ab35-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="3ab35-172">在背景工作角色的根目錄中建立 `php` 資料夾，然後將 PHP 執行階段 (所有的二進位檔、組態檔、子資料夾等) 新增至 `php` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3ab35-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="3ab35-173">(選擇性) 如果您的 PHP 執行階段使用[適用於 PHP for SQL Server 的 Microsoft 驅動程式][sqlsrv drivers]，您就必須將背景工作角色設定為在佈建時安裝 [SQL Server Native Client 2012][sql native client]。</span><span class="sxs-lookup"><span data-stu-id="3ab35-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="3ab35-174">若要執行此動作， [請將sqlncli.msi x64 安裝程式] 新增至背景工作角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="3ab35-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="3ab35-175">下一個步驟中說明的啟動指令碼，將會在角色進行佈建時以無訊息方式執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="3ab35-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="3ab35-176">如果您的 PHP 執行階段並未使用適用於 PHP for SQL Server 的 Microsoft 驅動程式，您可以從下一個步驟所顯示的指令碼中移除以下一行：</span><span class="sxs-lookup"><span data-stu-id="3ab35-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="3ab35-177">定義啟動工作，在佈建角色時將您的 `php.exe` 可執行檔新增至背景工作角色的 PATH 環境變數中。</span><span class="sxs-lookup"><span data-stu-id="3ab35-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="3ab35-178">若要執行此動作，請在文字編輯器中開啟 `setup_worker.cmd` 檔案 (位於背景工作角色的根目錄中)，並使用下列指令碼來取代它的內容：</span><span class="sxs-lookup"><span data-stu-id="3ab35-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. <span data-ttu-id="3ab35-179">將應用程式檔案新增至背景工作角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="3ab35-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="3ab35-180">如以下的[發佈您的應用程式](#publish-your-application)一節所述，發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ab35-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="3ab35-181">在計算和儲存模擬器中執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="3ab35-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="3ab35-182">Azure 模擬器所提供的本機環境，可讓您在 Azure 應用程式部署至雲端前先加以測試。</span><span class="sxs-lookup"><span data-stu-id="3ab35-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="3ab35-183">模擬器與 Azure 環境之間有若干差異。</span><span class="sxs-lookup"><span data-stu-id="3ab35-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="3ab35-184">若要深入了解，請參閱[使用 Azure 儲存體模擬器進行開發和測試](storage/common/storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="3ab35-185">請注意，您必須在本機安裝 PHP，才能使用計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="3ab35-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="3ab35-186">計算模擬器會使用您的本機 PHP 安裝執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ab35-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="3ab35-187">若要在模擬器中執行您的專案，請從專案的根目錄執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="3ab35-188">您將看到類似以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="3ab35-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="3ab35-189">您可以開啟網頁瀏覽器，並瀏覽至輸出中顯示的本機位址 (在前述範例輸出中為`http://127.0.0.1:81` )，即可看見您的應用程式正在模擬器中執行。</span><span class="sxs-lookup"><span data-stu-id="3ab35-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="3ab35-190">若要停止模擬器，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="3ab35-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="3ab35-191">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="3ab35-191">Publish your application</span></span>
<span data-ttu-id="3ab35-192">若要發佈應用程式，您必須先使用 [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) Cmdlet 匯入您的發佈設定。</span><span class="sxs-lookup"><span data-stu-id="3ab35-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="3ab35-193">使用 [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) Cmdlet 發佈應用程式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3ab35-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="3ab35-194">如需登入的相關資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ab35-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ab35-195">Next steps</span></span>
<span data-ttu-id="3ab35-196">如需詳細資訊，請參閱 [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="3ab35-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK for PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[服務定義 (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[服務組態 (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[請將sqlncli.msi x64 安裝程式]: http://go.microsoft.com/fwlink/?LinkID=239648
