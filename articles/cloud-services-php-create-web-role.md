---
title: "aaaCreate Azure for PHP web 和背景工作角色 |Microsoft 文件"
description: "指南 toocreating PHP web 和背景工作角色在 Azure 雲端服務和設定 hello PHP 執行階段中。"
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
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="a659a-103">如何 toocreate PHP web 和背景工作角色</span><span class="sxs-lookup"><span data-stu-id="a659a-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="a659a-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a659a-104">Overview</span></span>
<span data-ttu-id="a659a-105">本指南將說明 toocreate PHP web 或背景工作角色在 Windows 開發環境中，選擇特定版本的 PHP hello 從可用的 「 內建 」 版本的方式、 變更 hello 的 PHP 設定、 啟用擴充功能，和最後，部署 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="a659a-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="a659a-106">它也會說明如何 tooconfigure web 或背景工作角色 toouse 您提供 PHP 執行階段 （使用自訂組態和擴充功能）。</span><span class="sxs-lookup"><span data-stu-id="a659a-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="a659a-107">什麼是 PHP Web 和背景工作角色？</span><span class="sxs-lookup"><span data-stu-id="a659a-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="a659a-108">Azure 提供三種運算模型來執行應用程式：Azure 應用程式服務、Azure 虛擬機器和 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="a659a-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="a659a-109">這三種模型都支援 PHP。</span><span class="sxs-lookup"><span data-stu-id="a659a-109">All three models support PHP.</span></span> <span data-ttu-id="a659a-110">雲端服務 (包含 Web 和背景工作角色) 可提供 *平台即服務 (PaaS)*。</span><span class="sxs-lookup"><span data-stu-id="a659a-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="a659a-111">在雲端服務中，web 角色會提供專用的 Internet Information Services (IIS) web 伺服器 toohost 前端 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a659a-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="a659a-112">背景工作角色可以執行非同步、長時間或永久的工作，且不受使用者互動或輸入所影響。</span><span class="sxs-lookup"><span data-stu-id="a659a-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="a659a-113">如需這些選項的詳細資訊，請參閱[計算 Azure 提供的裝載選項](cloud-services/cloud-services-choose-me.md)。</span><span class="sxs-lookup"><span data-stu-id="a659a-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="a659a-114">下載 hello Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="a659a-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="a659a-115">hello [Azure SDK for PHP]數個元件所組成。</span><span class="sxs-lookup"><span data-stu-id="a659a-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="a659a-116">此發行項將會使用其中兩個： Azure PowerShell 和 hello Azure 模擬器。</span><span class="sxs-lookup"><span data-stu-id="a659a-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="a659a-117">這兩個元件可以透過 hello Microsoft Web Platform Installer 安裝。</span><span class="sxs-lookup"><span data-stu-id="a659a-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="a659a-118">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a659a-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="a659a-119">建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="a659a-119">Create a Cloud Services project</span></span>
<span data-ttu-id="a659a-120">在建立 PHP web 或背景工作角色的 hello 第一個步驟是 toocreate Azure 服務專案。</span><span class="sxs-lookup"><span data-stu-id="a659a-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="a659a-121">Azure 服務專案當做 web 和背景工作角色的邏輯容器，它包含 hello 專案[服務定義 (.csdef)]和[服務組態 (.cscfg)]檔案。</span><span class="sxs-lookup"><span data-stu-id="a659a-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="a659a-122">toocreate 新的 Azure 服務專案，為系統管理員，以執行 Azure PowerShell，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a659a-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="a659a-123">此命令會建立新的目錄 (`myProject`) toowhich 您可以加入 web 和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="a659a-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="a659a-124">新增 PHP Web 或背景工作角色</span><span class="sxs-lookup"><span data-stu-id="a659a-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="a659a-125">tooadd PHP web 角色 tooa 專案中，執行下列命令從 hello 專案根目錄中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a659a-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="a659a-126">對於背景工作角色，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a659a-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="a659a-127">hello`roleName`參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="a659a-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="a659a-128">如果省略，將會自動產生 hello 角色名稱。</span><span class="sxs-lookup"><span data-stu-id="a659a-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="a659a-129">hello 建立第一個 web 角色`WebRole1`，第二個會是 hello `WebRole2`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="a659a-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="a659a-130">hello 建立第一個背景工作角色就會是`WorkerRole1`，第二個會是 hello `WorkerRole2`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="a659a-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="a659a-131">指定 hello 內建的 PHP 版本</span><span class="sxs-lookup"><span data-stu-id="a659a-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="a659a-132">當您新增 PHP web 或背景工作角色 tooa 專案時，以便在部署時，將應用程式的每個 web 或背景工作執行個體上安裝 PHP，會修改 hello 專案的組態檔。</span><span class="sxs-lookup"><span data-stu-id="a659a-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="a659a-133">根據預設，執行下列命令的 hello 將會安裝的 PHP toosee hello 版本：</span><span class="sxs-lookup"><span data-stu-id="a659a-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="a659a-134">hello 上述 hello 命令的輸出看起來類似 toowhat 如下所示。</span><span class="sxs-lookup"><span data-stu-id="a659a-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="a659a-135">在此範例中，hello`IsDefault`旗標設定得`true`for PHP 5.3.17，表示它將會安裝 hello 預設的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="a659a-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

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

<span data-ttu-id="a659a-136">您可以設定 hello PHP 執行階段版本 tooany 的 hello 所列的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="a659a-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="a659a-137">例如，tooset hello PHP 版本 (hello 名稱的角色`roleName`) too5.4.0，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="a659a-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="a659a-138">Hello 未來可能會變更可用的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="a659a-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="a659a-139">自訂 hello 內建的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="a659a-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="a659a-140">已擁有 hello PHP 執行階段，當您遵循 hello 上述的步驟，包括修改安裝 hello 組態的完整控制權`php.ini`設定及啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="a659a-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="a659a-141">toocustomize hello 內建的 PHP 執行階段，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a659a-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="a659a-142">加入新的資料夾，名為`php`，toohello `bin` web 角色的目錄。</span><span class="sxs-lookup"><span data-stu-id="a659a-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="a659a-143">背景工作角色，將它加入 toohello 角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a659a-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="a659a-144">在 hello`php`資料夾中，建立名為另一個資料夾`ext`。</span><span class="sxs-lookup"><span data-stu-id="a659a-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="a659a-145">將它放置在`.dll`延伸模組檔案 (例如`php_mongo.dll`) 您想 tooenable 此資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="a659a-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="a659a-146">新增`php.ini`檔案 toohello`php`資料夾。</span><span class="sxs-lookup"><span data-stu-id="a659a-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="a659a-147">在此檔案中啟用自訂擴充功能，並設定 PHP 指示詞。</span><span class="sxs-lookup"><span data-stu-id="a659a-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="a659a-148">比方說，如果您想要 tooturn`display_errors`上並啟用 hello`php_mongo.dll`擴充功能，以 hello 內容您`php.ini`檔案將會如下：</span><span class="sxs-lookup"><span data-stu-id="a659a-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="a659a-149">您不需要明確 hello 中設定任何設定`php.ini`檔案會自動提供將它設為 tootheir 預設值。</span><span class="sxs-lookup"><span data-stu-id="a659a-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="a659a-150">但請留意，您可以新增完整的 `php.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a659a-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="a659a-151">使用您自己的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="a659a-151">Use your own PHP runtime</span></span>
<span data-ttu-id="a659a-152">在某些情況下，而不是選取內建的 PHP 執行階段並加以設定 （如上所述），您可能想 tooprovide 您自己的 PHP 執行階段。</span><span class="sxs-lookup"><span data-stu-id="a659a-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="a659a-153">例如，您可以使用相同的 PHP 執行階段，您在開發環境中使用的 web 或背景工作角色中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a659a-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="a659a-154">這可讓您更輕鬆 tooensure hello 應用程式不會變更您的生產環境中的行為。</span><span class="sxs-lookup"><span data-stu-id="a659a-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="a659a-155">設定 web 角色 toouse 您自己的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="a659a-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="a659a-156">tooconfigure web 角色 toouse PHP 執行階段提供時，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a659a-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="a659a-157">如本主題先前所述，建立 Azure 服務專案並加入 PHP Web 角色。</span><span class="sxs-lookup"><span data-stu-id="a659a-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="a659a-158">建立`php`資料夾中 hello`bin`資料夾，其位於 web 角色的根目錄，並將您的 PHP 執行階段 （所有二進位檔、 組態檔、 子資料夾等） toohello`php`資料夾。</span><span class="sxs-lookup"><span data-stu-id="a659a-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="a659a-159">（選擇性）如果您的 PHP 執行階段使用 hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers]，您將需要 tooconfigure 您的 web 角色 tooinstall [SQL Server Native Client 2012] [sql native client]時加以佈建。</span><span class="sxs-lookup"><span data-stu-id="a659a-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="a659a-160">toodo，新增 hello [sqlncli.msi x64 installer] toohello `bin` web 角色的根目錄中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="a659a-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="a659a-161">hello hello 下一個步驟中所述的啟動指令碼 hello 角色佈建時，會以無訊息模式執行 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a659a-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="a659a-162">如果您的 PHP 執行階段不使用 hello Microsoft Drivers for PHP for SQL Server，您可以移除 hello hello 下一個步驟中所顯示的 hello 指令碼中的下列行：</span><span class="sxs-lookup"><span data-stu-id="a659a-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="a659a-163">定義設定的啟動工作[網際網路資訊服務 (IIS)] [ iis.net] toouse 要求您的 PHP 執行階段 toohandle`.php`頁面。</span><span class="sxs-lookup"><span data-stu-id="a659a-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="a659a-164">toodo，開啟 hello`setup_web.cmd`檔案 (在 hello `bin` web 角色的根目錄的檔案) 中的文字編輯器，並取代其內容與 hello 下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="a659a-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="a659a-165">新增應用程式檔案 tooyour web 角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a659a-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="a659a-166">這會是 hello web 伺服器的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a659a-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="a659a-167">將應用程式發行 hello 中所述[發行您的應用程式](#publish-your-application)下一節。</span><span class="sxs-lookup"><span data-stu-id="a659a-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="a659a-168">hello`download.ps1`指令碼 (在 hello `bin` hello web 角色的根目錄資料夾) 可以執行上面所述，使用您自己的 PHP 執行階段的 hello 步驟之後刪除。</span><span class="sxs-lookup"><span data-stu-id="a659a-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="a659a-169">設定背景工作角色 toouse 您自己的 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="a659a-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="a659a-170">tooconfigure 背景工作角色 toouse PHP 執行階段提供時，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a659a-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="a659a-171">如本主題先前所述，建立 Azure 服務專案並加入 PHP 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="a659a-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="a659a-172">建立`php`hello 背景工作角色的根目錄中的資料夾，然後新增您的 PHP 執行階段 （所有二進位檔、 組態檔、 子資料夾等） toohello`php`資料夾。</span><span class="sxs-lookup"><span data-stu-id="a659a-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="a659a-173">（選擇性）如果您的 PHP 執行階段使用[Microsoft Drivers for PHP for SQL Server][sqlsrv drivers]，您將需要 tooconfigure 程式背景工作角色 tooinstall [SQL Server Native Client 2012] [sql native client]時加以佈建。</span><span class="sxs-lookup"><span data-stu-id="a659a-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="a659a-174">toodo，新增 hello [sqlncli.msi x64 installer] toohello 背景工作角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a659a-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="a659a-175">hello hello 下一個步驟中所述的啟動指令碼 hello 角色佈建時，會以無訊息模式執行 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a659a-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="a659a-176">如果您的 PHP 執行階段不使用 hello Microsoft Drivers for PHP for SQL Server，您可以移除 hello hello 下一個步驟中所顯示的 hello 指令碼中的下列行：</span><span class="sxs-lookup"><span data-stu-id="a659a-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="a659a-177">定義啟動工作加入您`php.exe`hello 角色佈建時可執行檔 toohello 背景工作角色的 PATH 環境變數。</span><span class="sxs-lookup"><span data-stu-id="a659a-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="a659a-178">toodo，開啟 hello`setup_worker.cmd`檔案 （位於 hello 背景工作角色的根目錄），在文字編輯器中，並且其內容取代下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a659a-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
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
5. <span data-ttu-id="a659a-179">加入您的應用程式檔案 tooyour 背景工作角色的根目錄。</span><span class="sxs-lookup"><span data-stu-id="a659a-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="a659a-180">將應用程式發行 hello 中所述[發行您的應用程式](#publish-your-application)下一節。</span><span class="sxs-lookup"><span data-stu-id="a659a-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="a659a-181">在 hello 計算和儲存體模擬器執行應用程式</span><span class="sxs-lookup"><span data-stu-id="a659a-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="a659a-182">hello Azure 模擬器會提供在其中您可以測試 Azure 應用程式部署 toohello 雲端之前，先在本機環境。</span><span class="sxs-lookup"><span data-stu-id="a659a-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="a659a-183">有一些 hello 模擬器與 hello Azure 環境之間的差異。</span><span class="sxs-lookup"><span data-stu-id="a659a-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="a659a-184">這更好，請參閱的 toounderstand[使用 hello Azure 儲存體模擬器進行開發和測試](storage/common/storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="a659a-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="a659a-185">請注意，您必須擁有 PHP 安裝在本機 toouse hello 計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="a659a-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="a659a-186">hello 計算模擬器會使用您本機的 PHP 安裝 toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a659a-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="a659a-187">toorun 專案 hello 模擬器中的執行下列命令，從您的專案根目錄 hello:</span><span class="sxs-lookup"><span data-stu-id="a659a-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="a659a-188">您會看到輸出類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="a659a-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="a659a-189">您可以看到您的應用程式開啟網頁瀏覽器並瀏覽 toohello hello 輸出中所示的本機位址 hello 模擬器中執行 (`http://127.0.0.1:81`在 hello 上面的範例輸出中)。</span><span class="sxs-lookup"><span data-stu-id="a659a-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="a659a-190">toostop hello 模擬器，執行此命令：</span><span class="sxs-lookup"><span data-stu-id="a659a-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="a659a-191">發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="a659a-191">Publish your application</span></span>
<span data-ttu-id="a659a-192">toopublish 應用程式時，您需要 toofirst 匯入您發行設定使用 hello [Import-azurepublishsettingsfile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a659a-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="a659a-193">然後您可以發行應用程式使用 hello[發行 AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a659a-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="a659a-194">如需登入資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a659a-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a659a-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a659a-195">Next steps</span></span>
<span data-ttu-id="a659a-196">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="a659a-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK for PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[服務定義 (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[服務組態 (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
