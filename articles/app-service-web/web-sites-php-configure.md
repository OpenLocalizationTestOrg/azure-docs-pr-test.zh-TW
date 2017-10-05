---
title: "在 Azure App Service Web Apps 中設定 PHP | Microsoft Docs"
description: "了解如何設定預設的 PHP 安裝，或是在 Azure App Service 中新增適用於 Web Apps 的自訂 PHP 安裝。"
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
ms.openlocfilehash: 624dd416f37aacdb3d2f6e59afdc2efe646e610b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="fcc77-103">在 Azure App Service Web Apps 中設定 PHP</span><span class="sxs-lookup"><span data-stu-id="fcc77-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="fcc77-104">簡介</span><span class="sxs-lookup"><span data-stu-id="fcc77-104">Introduction</span></span>
<span data-ttu-id="fcc77-105">本指南將示範如何為 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)中的 Web Apps 設定內建的 PHP 執行階段、提供自訂的 PHP 執行階段，以及啟用擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fcc77-105">This guide will show you how to configure the built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="fcc77-106">若要使用 App Service，請註冊 [免費試用]。</span><span class="sxs-lookup"><span data-stu-id="fcc77-106">To use App Service, sign up for the [free trial].</span></span> <span data-ttu-id="fcc77-107">若要充分利用本指南，您應該先在 App Service 中建立 PHP Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc77-107">To get the most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-the-built-in-php-version"></a><span data-ttu-id="fcc77-108">作法：變更內建 PHP 版本</span><span class="sxs-lookup"><span data-stu-id="fcc77-108">How to: Change the built-in PHP version</span></span>
<span data-ttu-id="fcc77-109">當您建立 App Service Web 應用程式時，預設會安裝 PHP 5.5 並立即可供使用。</span><span class="sxs-lookup"><span data-stu-id="fcc77-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="fcc77-110">若要查看可用的修訂版、其預設組態及啟用的擴充，最好的方法是部署呼叫 [phpinfo()] 函數的指令碼。</span><span class="sxs-lookup"><span data-stu-id="fcc77-110">The best way to see the available release revision, its default configuration, and the enabled extensions is to deploy a script that calls the [phpinfo()] function.</span></span>

<span data-ttu-id="fcc77-111">PHP 5.6 和 PHP 7.0 版本同樣可供使用，但預設並未啟用。</span><span class="sxs-lookup"><span data-stu-id="fcc77-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="fcc77-112">若要更新 PHP 版本，請遵循下列方法其中之一：</span><span class="sxs-lookup"><span data-stu-id="fcc77-112">To update the PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="fcc77-113">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fcc77-113">Azure Portal</span></span>
1. <span data-ttu-id="fcc77-114">在 [Azure 入口網站](https://portal.azure.com)中瀏覽至您的 Web 應用程式，然後按一下 [設定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc77-114">Browse to your web app in the [Azure Portal](https://portal.azure.com) and click on the **Settings** button.</span></span>
   
    ![Web 應用程式設定][settings-button]
2. <span data-ttu-id="fcc77-116">從 [設定] 刀鋒視窗中，選取 [應用程式設定]，並選擇新的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="fcc77-116">From the **Settings** blade select **Application Settings** and choose the new PHP version.</span></span>
   
    ![應用程式設定][application-settings]
3. <span data-ttu-id="fcc77-118">按一下 [Web 應用程式設定] 刀鋒視窗頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc77-118">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![儲存組態設定。][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="fcc77-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="fcc77-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="fcc77-121">開啟 Azure PowerShell 並登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc77-121">Open Azure PowerShell, and login to your account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="fcc77-122">設定 Web 應用程式的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="fcc77-122">Set the PHP version for the web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="fcc77-123">PHP 版本現在已設定完成。</span><span class="sxs-lookup"><span data-stu-id="fcc77-123">The PHP version is now set.</span></span> <span data-ttu-id="fcc77-124">您可確認這些設定：</span><span class="sxs-lookup"><span data-stu-id="fcc77-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="fcc77-125">Azure 命令列介面 (Linux、Mac、Windows)</span><span class="sxs-lookup"><span data-stu-id="fcc77-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="fcc77-126">若要使用 Azure 命令列介面，您必須在電腦上安裝 **Node.js** 。</span><span class="sxs-lookup"><span data-stu-id="fcc77-126">To use the Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="fcc77-127">開啟 [終端機]，然後登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fcc77-127">Open Terminal, and login to your account.</span></span>
   
        azure login
2. <span data-ttu-id="fcc77-128">設定 Web 應用程式的 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="fcc77-128">Set the PHP version for the web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="fcc77-129">PHP 版本現在已設定完成。</span><span class="sxs-lookup"><span data-stu-id="fcc77-129">The PHP version is now set.</span></span> <span data-ttu-id="fcc77-130">您可確認這些設定：</span><span class="sxs-lookup"><span data-stu-id="fcc77-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="fcc77-131">等同於上述程式碼的 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 命令為︰</span><span class="sxs-lookup"><span data-stu-id="fcc77-131">The [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent to the above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-the-built-in-php-configurations"></a><span data-ttu-id="fcc77-132">作法：變更內建 PHP 組態</span><span class="sxs-lookup"><span data-stu-id="fcc77-132">How to: Change the built-in PHP configurations</span></span>
<span data-ttu-id="fcc77-133">對於任一個內建的 PHP 執行階段，您可以遵循下列步驟，來變更任何組態選項。</span><span class="sxs-lookup"><span data-stu-id="fcc77-133">For any built-in PHP runtime, you can change any of the configuration options by following the steps below.</span></span> <span data-ttu-id="fcc77-134">(如需 php.ini 指示詞的資訊，請參閱 [php.ini 指示詞的清單](英文))。</span><span class="sxs-lookup"><span data-stu-id="fcc77-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="fcc77-135">變更 PHP\_INI\_USER、PHP\_INI\_PERDIR、PHP\_INI\_ALL 組態設定</span><span class="sxs-lookup"><span data-stu-id="fcc77-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="fcc77-136">將 [.user.ini] 檔案新增至根目錄。</span><span class="sxs-lookup"><span data-stu-id="fcc77-136">Add a [.user.ini] file to your root directory.</span></span>
2. <span data-ttu-id="fcc77-137">使用在 `php.ini` 檔案中使用的相同語法，將組態設定新增至 `.user.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc77-137">Add configuration settings to the `.user.ini` file using the same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="fcc77-138">例如，如果您要啟動 `display_errors` 設定，並將 `upload_max_filesize` 設定設為 10M，則 `.user.ini` 檔案將包含下列文字：</span><span class="sxs-lookup"><span data-stu-id="fcc77-138">For example, if you wanted to turn the `display_errors` setting on and set `upload_max_filesize` setting to 10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on to write errors to d:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="fcc77-139">部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc77-139">Deploy your web app.</span></span>
4. <span data-ttu-id="fcc77-140">重新啟動 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc77-140">Restart the web app.</span></span> <span data-ttu-id="fcc77-141">(必須重新啟動，因為 PHP 讀取 `.user.ini` 檔案的頻率是由 `user_ini.cache_ttl` 設定所控制，這是系統層級設定，預設為 300 秒 (5 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="fcc77-141">(Restarting is necessary because the frequency with which PHP reads `.user.ini` files is governed by the `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="fcc77-142">重新啟動 Web 應用程式將強制 PHP 讀取 `.user.ini` 檔案中的新設定。)</span><span class="sxs-lookup"><span data-stu-id="fcc77-142">Restarting the web app forces PHP to read the new settings in the `.user.ini` file.)</span></span>

<span data-ttu-id="fcc77-143">除了使用 `.user.ini` 檔案之外，您也可以在指令碼中使用 [ini_set()] 函數，設定非系統層級指示詞的組態選項。</span><span class="sxs-lookup"><span data-stu-id="fcc77-143">As an alternative to using a `.user.ini` file, you can use the [ini_set()] function in scripts to set configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="fcc77-144">變更 PHP\_INI\_SYSTEM 組態設定</span><span class="sxs-lookup"><span data-stu-id="fcc77-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="fcc77-145">使用機碼 `PHP_INI_SCAN_DIR` 和值 `d:\home\site\ini` 將應用程式設定新增至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fcc77-145">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="fcc77-146">在 `d:\home\site\ini` 目錄中使用 Kudo 主控台 (http://&lt;site-name&gt;.scm.azurewebsite.net) 建立 `settings.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc77-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in the `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="fcc77-147">使用在 php.ini 檔案中使用的相同語法，將組態設定新增至 `settings.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc77-147">Add configuration settings to the `settings.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="fcc77-148">例如，如果要將 `curl.cainfo` 設定指向 `*.crt` 檔案並將 'wincache.maxfilesize' 設定設定為 512K，您的 `settings.ini` 檔案應該包含以下文字：</span><span class="sxs-lookup"><span data-stu-id="fcc77-148">For example, if you wanted to point the `curl.cainfo` setting to a `*.crt` file and set 'wincache.maxfilesize' setting to 512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="fcc77-149">重新啟動 Web 應用程式以載入變更。</span><span class="sxs-lookup"><span data-stu-id="fcc77-149">Restart your Web App to load the changes.</span></span>

## <a name="how-to-enable-extensions-in-the-default-php-runtime"></a><span data-ttu-id="fcc77-150">作法：在預設 PHP 執行階段中啟用擴充</span><span class="sxs-lookup"><span data-stu-id="fcc77-150">How to: Enable extensions in the default PHP runtime</span></span>
<span data-ttu-id="fcc77-151">如同上一個小節所述，若要查看預設 PHP 版本、其預設組態及啟用的擴充，最好的方法是部署呼叫 [phpinfo()]函數的指令碼。</span><span class="sxs-lookup"><span data-stu-id="fcc77-151">As noted in the previous section, the best way to see the default PHP version, its default configuration, and the enabled extensions is to deploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="fcc77-152">若要啟用擴充，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="fcc77-152">To enable additional extensions, follow the steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="fcc77-153">透過 ini 設定來設定</span><span class="sxs-lookup"><span data-stu-id="fcc77-153">Configure via ini settings</span></span>
1. <span data-ttu-id="fcc77-154">將 `ext` 目錄新增至 `d:\home\site` 目錄。</span><span class="sxs-lookup"><span data-stu-id="fcc77-154">Add a `ext` directory to the `d:\home\site` directory.</span></span>
2. <span data-ttu-id="fcc77-155">將 `.dll` 擴充檔放入 `ext` 目錄中 (例如，`php_xdebug.dll`)。</span><span class="sxs-lookup"><span data-stu-id="fcc77-155">Put `.dll` extension files in the `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="fcc77-156">請確定擴充功能與預設的 PHP 版本相容，並且與 VC9 及非執行緒安全 (nts) 相容。</span><span class="sxs-lookup"><span data-stu-id="fcc77-156">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="fcc77-157">使用機碼 `PHP_INI_SCAN_DIR` 和值 `d:\home\site\ini` 將應用程式設定新增至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fcc77-157">Add an App Setting to your Web App with the key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="fcc77-158">在名為 `extensions.ini` 的 `d:\home\site\ini` 中建立 `ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc77-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="fcc77-159">使用在 php.ini 檔案中使用的相同語法，將組態設定新增至 `extensions.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc77-159">Add configuration settings to the `extensions.ini` file using the same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="fcc77-160">例如，如果您要啟用 MongoDB 和 XDebug 擴充，您的 `extensions.ini` 檔案應該包含以下文字：</span><span class="sxs-lookup"><span data-stu-id="fcc77-160">For example, if you wanted to enable the MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="fcc77-161">重新啟動 Web 應用程式以載入變更。</span><span class="sxs-lookup"><span data-stu-id="fcc77-161">Restart your Web App to load the changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="fcc77-162">透過應用程式設定來設定</span><span class="sxs-lookup"><span data-stu-id="fcc77-162">Configure via App Setting</span></span>
1. <span data-ttu-id="fcc77-163">將 `bin` 目錄新增至根目錄。</span><span class="sxs-lookup"><span data-stu-id="fcc77-163">Add a `bin` directory to the root directory.</span></span>
2. <span data-ttu-id="fcc77-164">將 `.dll` 擴充檔放入 `bin` 目錄中 (例如，`php_xdebug.dll`)。</span><span class="sxs-lookup"><span data-stu-id="fcc77-164">Put `.dll` extension files in the `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="fcc77-165">請確定擴充功能與預設的 PHP 版本相容，並且與 VC9 及非執行緒安全 (nts) 相容。</span><span class="sxs-lookup"><span data-stu-id="fcc77-165">Make sure that the extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="fcc77-166">部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc77-166">Deploy your web app.</span></span>
4. <span data-ttu-id="fcc77-167">在 Azure 入口網站中瀏覽至您的 Web 應用程式，然後按一下 [設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc77-167">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Web 應用程式設定][settings-button]
5. <span data-ttu-id="fcc77-169">從 [設定] 刀鋒視窗中選取 [應用程式設定]，然後捲動至 [應用程式設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="fcc77-169">From the **Settings** blade select **Application Settings** and scroll to the **App settings** section.</span></span>
6. <span data-ttu-id="fcc77-170">在 [應用程式設定] 區段中，建立 **PHP_EXTENSIONS** 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fcc77-170">In the **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="fcc77-171">此索引鍵的值是相對於網站根目錄的路徑：**bin\your-ext-file**。</span><span class="sxs-lookup"><span data-stu-id="fcc77-171">The value for this key would be a path relative to website root: **bin\your-ext-file**.</span></span>
   
    ![啟用應用程式設定中的擴充][php-extensions]
7. <span data-ttu-id="fcc77-173">按一下 [Web 應用程式設定] 刀鋒視窗頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc77-173">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![儲存組態設定。][save-button]

<span data-ttu-id="fcc77-175">Zend 擴充功能也支援使用 **PHP_ZENDEXTENSIONS** 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fcc77-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="fcc77-176">若要啟用多個擴充功能，請針對應用程式設定值包含以逗號分隔的 `.dll` 檔案清單。</span><span class="sxs-lookup"><span data-stu-id="fcc77-176">To enable multiple extensions, include a comma-separated list of `.dll` files for the app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="fcc77-177">做法：使用自訂 PHP 執行階段</span><span class="sxs-lookup"><span data-stu-id="fcc77-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="fcc77-178">除了預設的 PHP 執行階段之外，App Service Web Apps 也可以使用您提供的 PHP 執行階段來執行 PHP 指令碼。</span><span class="sxs-lookup"><span data-stu-id="fcc77-178">Instead of the default PHP runtime, App Service Web Apps can use a PHP runtime that you provide to execute PHP scripts.</span></span> <span data-ttu-id="fcc77-179">您提供的執行階段可以由也是您提供的 `php.ini` 檔案加以設定。</span><span class="sxs-lookup"><span data-stu-id="fcc77-179">The runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="fcc77-180">若要使用自訂 PHP 執行階段搭配 Web Apps，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="fcc77-180">To use a custom PHP runtime with Web Apps, follow the steps below.</span></span>

1. <span data-ttu-id="fcc77-181">取得 PHP for Windows 的非安全執行緒 VC9 或 VC11 相容版本。</span><span class="sxs-lookup"><span data-stu-id="fcc77-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="fcc77-182">可以在下列網址找到最新版 PHP for Windows： [http://windows.php.net/download/]。</span><span class="sxs-lookup"><span data-stu-id="fcc77-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="fcc77-183">在下列封存中可以找到舊版： [http://windows.php.net/downloads/releases/archives/]。</span><span class="sxs-lookup"><span data-stu-id="fcc77-183">Older releases can be found in the archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="fcc77-184">為您的執行階段修改 `php.ini` 檔案。</span><span class="sxs-lookup"><span data-stu-id="fcc77-184">Modify the `php.ini` file for your runtime.</span></span> <span data-ttu-id="fcc77-185">請注意，Web Apps 將忽略僅系統層級指示詞的任何組態設定</span><span class="sxs-lookup"><span data-stu-id="fcc77-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="fcc77-186">(如需僅系統層級指示詞的資訊，請參閱 [php.ini 指示詞的清單] (英文))。</span><span class="sxs-lookup"><span data-stu-id="fcc77-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="fcc77-187">或者，將擴充功能新增至 PHP 執行階段，並且在 `php.ini` 檔案中啟用這些擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fcc77-187">Optionally, add extensions to your PHP runtime and enable them in the `php.ini` file.</span></span>
4. <span data-ttu-id="fcc77-188">將 `bin` 目錄新增至根目錄，並在其中放入包含 PHP 執行階段的目錄 (例如，`bin\php`)。</span><span class="sxs-lookup"><span data-stu-id="fcc77-188">Add a `bin` directory to your root directory, and put the directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="fcc77-189">部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc77-189">Deploy your web app.</span></span>
6. <span data-ttu-id="fcc77-190">在 Azure 入口網站中瀏覽至您的 Web 應用程式，然後按一下 [設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc77-190">Browse to your web app in the Azure Portal and click on the **Settings** button.</span></span>
   
    ![Web 應用程式設定][settings-button]
7. <span data-ttu-id="fcc77-192">從 [設定] 刀鋒視窗中選取 [應用程式設定]，然後捲動至 [處理常式對應] 區段。</span><span class="sxs-lookup"><span data-stu-id="fcc77-192">From the **Settings** blade select **Application Settings** and scroll to the **Handler mappings** section.</span></span> <span data-ttu-id="fcc77-193">將 `*.php` 新增至 [副檔名] 欄位，然後將路徑加入 `php-cgi.exe` 可執行檔。</span><span class="sxs-lookup"><span data-stu-id="fcc77-193">Add `*.php` to the Extension field and add the path to the `php-cgi.exe` executable.</span></span> <span data-ttu-id="fcc77-194">如果您將 PHP 執行階段放入應用程式根目錄內的 `bin` 目錄中，該路徑將是 `D:\home\site\wwwroot\bin\php\php-cgi.exe`。</span><span class="sxs-lookup"><span data-stu-id="fcc77-194">If you put your PHP runtime in the `bin` directory in the root of you application, the path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![指定處理常式對應中的處理常式][handler-mappings]
8. <span data-ttu-id="fcc77-196">按一下 [Web 應用程式設定] 刀鋒視窗頂端的 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fcc77-196">Click the **Save** button at the top of the **Web app settings** blade.</span></span>
   
    ![儲存組態設定。][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="fcc77-198">做法︰在 Azure 中啟用編輯器自動化</span><span class="sxs-lookup"><span data-stu-id="fcc77-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="fcc77-199">App Service 預設不會對 composer.json (如果您 PHP 專案中有的話) 執行任何操作。</span><span class="sxs-lookup"><span data-stu-id="fcc77-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="fcc77-200">如果您使用 [Git 部署](app-service-deploy-local-git.md)，您可以透過啟用「編輯器」擴充功能，在 `git push` 期間啟用 composer.json 處理。</span><span class="sxs-lookup"><span data-stu-id="fcc77-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="fcc77-201">您可以 [在這裡投票選擇 App Service 中的頂級編輯器支援](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)！</span><span class="sxs-lookup"><span data-stu-id="fcc77-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="fcc77-202">在 [Azure 入口網站](https://portal.azure.com)的 PHP Web 應用程式刀鋒視窗中，按一下 [工具] > [擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="fcc77-202">In your PHP web app's blade in the [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![可在 Azure 中啟用「編輯器」自動化的「Azure 入口網站」設定刀鋒視窗](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="fcc77-204">按一下 [新增]，然後按一下 [編輯器]。</span><span class="sxs-lookup"><span data-stu-id="fcc77-204">Click **Add**, then click **Composer**.</span></span>
   
    ![新增「編輯器」擴充功能以在 Azure 中啟用「編輯器」自動化](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="fcc77-206">按一下 [確定]  以接受法律條款。</span><span class="sxs-lookup"><span data-stu-id="fcc77-206">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="fcc77-207">再按一次 [確定]  以新增擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fcc77-207">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="fcc77-208">[已安裝的擴充功能]  刀鋒視窗現在將顯示編輯器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fcc77-208">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="fcc77-209">![接受法律條款以在 Azure 中啟用「編輯器」自動化](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="fcc77-209">![Accept legal terms to enable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="fcc77-210">現在，和上一節一樣執行 `git add`、`git commit` 和 `git push`。</span><span class="sxs-lookup"><span data-stu-id="fcc77-210">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="fcc77-211">您就會立即看到編輯器正在安裝 composer.json 中定義的相依性。</span><span class="sxs-lookup"><span data-stu-id="fcc77-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![使用 Azure 中的「編輯器」自動化來進行 Git 部署](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="fcc77-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fcc77-213">Next steps</span></span>
<span data-ttu-id="fcc77-214">如需詳細資訊，請參閱 [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="fcc77-214">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="fcc77-215">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcc77-215">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fcc77-216">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="fcc77-216">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="fcc77-217">[免費試用]: https://www.windowsazure.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="fcc77-217">[free trial]: https://www.windowsazure.com/pricing/free-trial/</span></span>
<span data-ttu-id="fcc77-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span><span class="sxs-lookup"><span data-stu-id="fcc77-218">[phpinfo()]: http://php.net/manual/en/function.phpinfo.php</span></span>
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
<span data-ttu-id="fcc77-219">[php.ini 指示詞的清單]: http://www.php.net/manual/en/ini.list.php</span><span class="sxs-lookup"><span data-stu-id="fcc77-219">[List of php.ini directives]: http://www.php.net/manual/en/ini.list.php</span></span>
<span data-ttu-id="fcc77-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span><span class="sxs-lookup"><span data-stu-id="fcc77-220">[.user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php</span></span>
<span data-ttu-id="fcc77-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span><span class="sxs-lookup"><span data-stu-id="fcc77-221">[ini_set()]: http://www.php.net/manual/en/function.ini-set.php</span></span>
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
<span data-ttu-id="fcc77-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span><span class="sxs-lookup"><span data-stu-id="fcc77-222">[http://windows.php.net/download/]: http://windows.php.net/download/</span></span>
<span data-ttu-id="fcc77-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span><span class="sxs-lookup"><span data-stu-id="fcc77-223">[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/</span></span>
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

