---
title: "在 Azure App Service Web 應用程式中的 PHP aaaConfigure |Microsoft 文件"
description: "了解如何 tooconfigure hello 預設的 PHP 安裝或加入自訂的 PHP 安裝的 Azure App Service 中的 Web 應用程式。"
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="7ac53-103">在 Azure App Service Web Apps 中設定 PHP</span><span class="sxs-lookup"><span data-stu-id="7ac53-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="7ac53-104">簡介</span><span class="sxs-lookup"><span data-stu-id="7ac53-104">Introduction</span></span>
<span data-ttu-id="7ac53-105">本指南將說明您如何 tooconfigure hello Web 應用程式中的內建的 PHP 執行階段[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)、 提供自訂的 PHP 執行階段，並啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="7ac53-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="7ac53-106">toouse 應用程式服務註冊 hello[免費試用版]。</span><span class="sxs-lookup"><span data-stu-id="7ac53-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="7ac53-107">tooget hello 最從本指南中，您應該先 PHP web 應用程式以建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="7ac53-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="7ac53-108">如何： 變更 hello 內建的 PHP 版本</span><span class="sxs-lookup"><span data-stu-id="7ac53-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="7ac53-109">當您建立 App Service Web 應用程式時，預設會安裝 PHP 5.5 並立即可供使用。</span><span class="sxs-lookup"><span data-stu-id="7ac53-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="7ac53-110">hello 最佳方式 toosee hello 版本修訂，其預設設定，和 hello 啟用延伸模組是指令碼中呼叫 hello toodeploy [phpinfo （)]函式。</span><span class="sxs-lookup"><span data-stu-id="7ac53-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="7ac53-111">PHP 5.6 和 PHP 7.0 版本同樣可供使用，但預設並未啟用。</span><span class="sxs-lookup"><span data-stu-id="7ac53-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="7ac53-112">tooupdate hello 的 PHP 版本，請依照下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="7ac53-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7ac53-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ac53-113">Azure Portal</span></span>
1. <span data-ttu-id="7ac53-114">瀏覽 tooyour web 應用程式在 hello [Azure 入口網站](https://portal.azure.com)，然後按一下 [hello**設定**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ac53-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Web 應用程式設定][settings-button]
2. <span data-ttu-id="7ac53-116">從 hello**設定**刀鋒視窗選取**應用程式設定**並選擇 hello 新的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="7ac53-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![應用程式設定][application-settings]
3. <span data-ttu-id="7ac53-118">按一下 hello**儲存**按鈕上方的 hello hello **Web 應用程式設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ac53-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![儲存組態設定。][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="7ac53-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="7ac53-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="7ac53-121">開啟 Azure PowerShell，並登入 tooyour 帳戶：</span><span class="sxs-lookup"><span data-stu-id="7ac53-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="7ac53-122">設定 hello hello web 應用程式所需的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="7ac53-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="7ac53-123">現在已設定 hello PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="7ac53-123">hello PHP version is now set.</span></span> <span data-ttu-id="7ac53-124">您可確認這些設定：</span><span class="sxs-lookup"><span data-stu-id="7ac53-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="7ac53-125">Azure 命令列介面 (Linux、Mac、Windows)</span><span class="sxs-lookup"><span data-stu-id="7ac53-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="7ac53-126">toouse hello Azure 命令列介面，您必須具有**Node.js**安裝在電腦上。</span><span class="sxs-lookup"><span data-stu-id="7ac53-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="7ac53-127">開啟 終端機和登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ac53-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="7ac53-128">設定 hello hello web 應用程式所需的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="7ac53-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="7ac53-129">現在已設定 hello PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="7ac53-129">hello PHP version is now set.</span></span> <span data-ttu-id="7ac53-130">您可確認這些設定：</span><span class="sxs-lookup"><span data-stu-id="7ac53-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="7ac53-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli)是對等 toohello 上述的命令：</span><span class="sxs-lookup"><span data-stu-id="7ac53-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="7ac53-132">如何： 變更 hello 內建的 PHP 設定</span><span class="sxs-lookup"><span data-stu-id="7ac53-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="7ac53-133">任何內建的 PHP 執行階段，您可以依照以下 hello 步驟 hello 組態選項的任何變更。</span><span class="sxs-lookup"><span data-stu-id="7ac53-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="7ac53-134">(如需 php.ini 指示詞的資訊，請參閱 [php.ini 指示詞的清單](英文))。</span><span class="sxs-lookup"><span data-stu-id="7ac53-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="7ac53-135">變更 PHP\_INI\_USER、PHP\_INI\_PERDIR、PHP\_INI\_ALL 組態設定</span><span class="sxs-lookup"><span data-stu-id="7ac53-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="7ac53-136">新增[。 user.ini]檔案 tooyour 根目錄。</span><span class="sxs-lookup"><span data-stu-id="7ac53-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="7ac53-137">新增組態設定 toohello`.user.ini`檔案使用 hello 中會使用相同的語法`php.ini`檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac53-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="7ac53-138">例如，如果您想要 tooturn hello`display_errors`設定開始和設定`upload_max_filesize`設定 too10M，您`.user.ini`檔案會包含此文字：</span><span class="sxs-lookup"><span data-stu-id="7ac53-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="7ac53-139">部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ac53-139">Deploy your web app.</span></span>
4. <span data-ttu-id="7ac53-140">重新啟動 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ac53-140">Restart hello web app.</span></span> <span data-ttu-id="7ac53-141">(重新啟動，所以需要哪些 PHP hello 頻率讀取`.user.ini`檔案由 hello`user_ini.cache_ttl`設定，而這是系統層級設定，預設為 300 秒 （5 分鐘）。</span><span class="sxs-lookup"><span data-stu-id="7ac53-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="7ac53-142">重新啟動的 hello web 應用程式會強制在 hello 的 PHP tooread hello 新設定`.user.ini`檔案。)</span><span class="sxs-lookup"><span data-stu-id="7ac53-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="7ac53-143">做為替代的 toousing`.user.ini`檔案中，您可以使用 hello [ini_set()]函式中不是系統層級指示詞的指令碼 tooset 組態選項。</span><span class="sxs-lookup"><span data-stu-id="7ac53-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="7ac53-144">變更 PHP\_INI\_SYSTEM 組態設定</span><span class="sxs-lookup"><span data-stu-id="7ac53-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="7ac53-145">新增應用程式設定 tooyour Web 應用程式與 hello 索引鍵`PHP_INI_SCAN_DIR`和值`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="7ac53-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="7ac53-146">建立`settings.ini`檔案使用 Kudu 主控台 (http://&lt;站台名稱&gt;。 scm.azurewebsite.net) 在 hello`d:\home\site\ini`目錄。</span><span class="sxs-lookup"><span data-stu-id="7ac53-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="7ac53-147">新增組態設定 toohello`settings.ini`檔案使用 hello php.ini 檔案中，您會使用相同的語法。</span><span class="sxs-lookup"><span data-stu-id="7ac53-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="7ac53-148">例如，如果您想要 toopoint hello`curl.cainfo`設定 tooa`*.crt`檔案並設定 'wincache.maxfilesize' 設定 too512K，您`settings.ini`檔案會包含此文字：</span><span class="sxs-lookup"><span data-stu-id="7ac53-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="7ac53-149">重新啟動 Web 應用程式 tooload hello 做的變更。</span><span class="sxs-lookup"><span data-stu-id="7ac53-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="7ac53-150">如何： 啟用 hello 預設 PHP 執行階段中的擴充功能</span><span class="sxs-lookup"><span data-stu-id="7ac53-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="7ac53-151">延伸模組所述 hello 上一節、 hello 最佳方式 toosee hello 預設 PHP 版本、 其預設組態及啟用的 hello 是 toodeploy 指令碼中呼叫[phpinfo （)]。</span><span class="sxs-lookup"><span data-stu-id="7ac53-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="7ac53-152">tooenable 其他擴充功能，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="7ac53-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="7ac53-153">透過 ini 設定來設定</span><span class="sxs-lookup"><span data-stu-id="7ac53-153">Configure via ini settings</span></span>
1. <span data-ttu-id="7ac53-154">新增`ext`目錄 toohello`d:\home\site`目錄。</span><span class="sxs-lookup"><span data-stu-id="7ac53-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="7ac53-155">Put`.dll`延伸模組檔案中 hello`ext`目錄 (例如， `php_xdebug.dll`)。</span><span class="sxs-lookup"><span data-stu-id="7ac53-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="7ac53-156">請確定 hello 延伸模組是與 PHP 和 VC9 以及非安全執行緒 （來） 相容的預設版本相容。</span><span class="sxs-lookup"><span data-stu-id="7ac53-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="7ac53-157">新增應用程式設定 tooyour Web 應用程式與 hello 索引鍵`PHP_INI_SCAN_DIR`和值`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="7ac53-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="7ac53-158">在名為 `extensions.ini` 的 `d:\home\site\ini` 中建立 `ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac53-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="7ac53-159">新增組態設定 toohello`extensions.ini`檔案使用 hello php.ini 檔案中，您會使用相同的語法。</span><span class="sxs-lookup"><span data-stu-id="7ac53-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="7ac53-160">例如，如果您想要 tooenable hello MongoDB 和 XDebug 擴充功能，您`extensions.ini`檔案會包含此文字：</span><span class="sxs-lookup"><span data-stu-id="7ac53-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="7ac53-161">重新啟動 Web 應用程式 tooload hello 做的變更。</span><span class="sxs-lookup"><span data-stu-id="7ac53-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="7ac53-162">透過應用程式設定來設定</span><span class="sxs-lookup"><span data-stu-id="7ac53-162">Configure via App Setting</span></span>
1. <span data-ttu-id="7ac53-163">新增`bin`目錄 toohello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="7ac53-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="7ac53-164">Put`.dll`延伸模組檔案中 hello`bin`目錄 (例如， `php_xdebug.dll`)。</span><span class="sxs-lookup"><span data-stu-id="7ac53-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="7ac53-165">請確定 hello 延伸模組是與 PHP 和 VC9 以及非安全執行緒 （來） 相容的預設版本相容。</span><span class="sxs-lookup"><span data-stu-id="7ac53-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="7ac53-166">部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ac53-166">Deploy your web app.</span></span>
4. <span data-ttu-id="7ac53-167">瀏覽 tooyour hello Azure 入口網站中的 web 應用程式，然後按一下 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ac53-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Web 應用程式設定][settings-button]
5. <span data-ttu-id="7ac53-169">從 hello**設定**刀鋒視窗選取**應用程式設定**捲動 toohello**應用程式設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7ac53-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="7ac53-170">在 hello**應用程式設定**區段中，建立**PHP_EXTENSIONS**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7ac53-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="7ac53-171">此索引鍵的 hello 值會是根路徑相對 toowebsite: **bin\your ext 檔案**。</span><span class="sxs-lookup"><span data-stu-id="7ac53-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![啟用應用程式設定中的擴充][php-extensions]
7. <span data-ttu-id="7ac53-173">按一下 hello**儲存**按鈕上方的 hello hello **Web 應用程式設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ac53-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![儲存組態設定。][save-button]

<span data-ttu-id="7ac53-175">Zend 擴充功能也支援使用 **PHP_ZENDEXTENSIONS** 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7ac53-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="7ac53-176">tooenable 多個副檔名，包括以逗號分隔清單`.dll`hello 應用程式設定值的檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac53-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="7ac53-177">做法：使用自訂 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="7ac53-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="7ac53-178">而不是 hello 預設 PHP 執行階段，App Service Web 應用程式可以使用您提供 tooexecute PHP 指令碼 PHP 執行階段。</span><span class="sxs-lookup"><span data-stu-id="7ac53-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="7ac53-179">您可以設定您所提供的 hello 執行階段`php.ini`也提供的檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac53-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="7ac53-180">toouse 自訂的 PHP 執行階段透過 Web 應用程式，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="7ac53-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="7ac53-181">取得 PHP for Windows 的非安全執行緒 VC9 或 VC11 相容版本。</span><span class="sxs-lookup"><span data-stu-id="7ac53-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="7ac53-182">可以在下列網址找到最新版 PHP for Windows： [http://windows.php.net/download/]。</span><span class="sxs-lookup"><span data-stu-id="7ac53-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="7ac53-183">較舊的版本可以在這裡 hello 封存： [http://windows.php.net/downloads/releases/archives/]。</span><span class="sxs-lookup"><span data-stu-id="7ac53-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="7ac53-184">修改 hello`php.ini`程式執行階段的檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac53-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="7ac53-185">請注意，Web Apps 將忽略僅系統層級指示詞的任何組態設定</span><span class="sxs-lookup"><span data-stu-id="7ac53-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="7ac53-186">(如需僅系統層級指示詞的資訊，請參閱 [php.ini 指示詞的清單] (英文))。</span><span class="sxs-lookup"><span data-stu-id="7ac53-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="7ac53-187">（選擇性） 加入延伸模組 tooyour PHP 執行階段，並讓它們在 hello`php.ini`檔案。</span><span class="sxs-lookup"><span data-stu-id="7ac53-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="7ac53-188">新增`bin`目錄 tooyour 根目錄和包含您的 PHP 執行階段中的 put 的 hello 目錄 (例如， `bin\php`)。</span><span class="sxs-lookup"><span data-stu-id="7ac53-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="7ac53-189">部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ac53-189">Deploy your web app.</span></span>
6. <span data-ttu-id="7ac53-190">瀏覽 tooyour hello Azure 入口網站中的 web 應用程式，然後按一下 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ac53-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Web 應用程式設定][settings-button]
7. <span data-ttu-id="7ac53-192">從 hello**設定**刀鋒視窗選取**應用程式設定**捲動 toohello**處理常式對應**> 一節。</span><span class="sxs-lookup"><span data-stu-id="7ac53-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="7ac53-193">新增`*.php`toohello 延伸模組欄位和加入 hello 路徑 toohello`php-cgi.exe`可執行檔。</span><span class="sxs-lookup"><span data-stu-id="7ac53-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="7ac53-194">如果您將您的 PHP 執行階段放在 hello `bin` hello 路徑會是您的應用程式的 hello 根目錄中的目錄， `D:\home\site\wwwroot\bin\php\php-cgi.exe`。</span><span class="sxs-lookup"><span data-stu-id="7ac53-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![指定處理常式對應中的處理常式][handler-mappings]
8. <span data-ttu-id="7ac53-196">按一下 hello**儲存**按鈕上方的 hello hello **Web 應用程式設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7ac53-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![儲存組態設定。][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="7ac53-198">做法︰在 Azure 中啟用編輯器自動化</span><span class="sxs-lookup"><span data-stu-id="7ac53-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="7ac53-199">App Service 預設不會對 composer.json (如果您 PHP 專案中有的話) 執行任何操作。</span><span class="sxs-lookup"><span data-stu-id="7ac53-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="7ac53-200">如果您使用[Git 部署](app-service-deploy-local-git.md)，您可以啟用 composer.json 處理期間`git push`藉由啟用 hello 編輯器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7ac53-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="7ac53-201">您可以 [在這裡投票選擇 App Service 中的頂級編輯器支援](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)！</span><span class="sxs-lookup"><span data-stu-id="7ac53-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="7ac53-202">在您的 PHP web 應用程式的刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **工具** > **延伸**。</span><span class="sxs-lookup"><span data-stu-id="7ac53-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure 入口網站設定 刀鋒視窗 tooenable Azure 中的編輯器自動化](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="7ac53-204">按一下 [新增]，然後按一下 [編輯器]。</span><span class="sxs-lookup"><span data-stu-id="7ac53-204">Click **Add**, then click **Composer**.</span></span>
   
    ![加入在 Azure 中的編輯器延伸模組 tooenable 編輯器自動化](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="7ac53-206">按一下**確定**tooaccept 法律條款。</span><span class="sxs-lookup"><span data-stu-id="7ac53-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="7ac53-207">按一下**確定**再次 tooadd hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7ac53-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="7ac53-208">hello**擴充功能安裝**刀鋒視窗現在將會顯示 hello 編輯器延伸模組。</span><span class="sxs-lookup"><span data-stu-id="7ac53-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="7ac53-209">![接受 Azure 中的法律條款 tooenable 編輯器自動化](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="7ac53-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="7ac53-210">現在，執行`git add`， `git commit`，和`git push`如同在 hello 上一節。</span><span class="sxs-lookup"><span data-stu-id="7ac53-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="7ac53-211">您就會立即看到編輯器正在安裝 composer.json 中定義的相依性。</span><span class="sxs-lookup"><span data-stu-id="7ac53-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![使用 Azure 中的「編輯器」自動化來進行 Git 部署](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="7ac53-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ac53-213">Next steps</span></span>
<span data-ttu-id="7ac53-214">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="7ac53-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="7ac53-215">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="7ac53-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7ac53-216">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="7ac53-216">No credit cards required; no commitments.</span></span>
> 
> 

[免費試用版]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo （)]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[php.ini 指示詞的清單]: http://www.php.net/manual/en/ini.list.php
[。 user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

