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
# <a name="configure-php-in-azure-app-service-web-apps"></a>在 Azure App Service Web Apps 中設定 PHP
## <a name="introduction"></a>簡介
本指南將說明您如何 tooconfigure hello Web 應用程式中的內建的 PHP 執行階段[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)、 提供自訂的 PHP 執行階段，並啟用擴充功能。 toouse 應用程式服務註冊 hello[免費試用版]。 tooget hello 最從本指南中，您應該先 PHP web 應用程式以建立應用程式服務。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>如何： 變更 hello 內建的 PHP 版本
當您建立 App Service Web 應用程式時，預設會安裝 PHP 5.5 並立即可供使用。 hello 最佳方式 toosee hello 版本修訂，其預設設定，和 hello 啟用延伸模組是指令碼中呼叫 hello toodeploy [phpinfo （)]函式。

PHP 5.6 和 PHP 7.0 版本同樣可供使用，但預設並未啟用。 tooupdate hello 的 PHP 版本，請依照下列其中一種方法：

### <a name="azure-portal"></a>Azure 入口網站
1. 瀏覽 tooyour web 應用程式在 hello [Azure 入口網站](https://portal.azure.com)，然後按一下 [hello**設定**] 按鈕。
   
    ![Web 應用程式設定][settings-button]
2. 從 hello**設定**刀鋒視窗選取**應用程式設定**並選擇 hello 新的 PHP 版本。
   
    ![應用程式設定][application-settings]
3. 按一下 hello**儲存**按鈕上方的 hello hello **Web 應用程式設定**刀鋒視窗。
   
    ![儲存組態設定。][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell (Windows)
1. 開啟 Azure PowerShell，並登入 tooyour 帳戶：
   
        PS C:\> Login-AzureRmAccount
2. 設定 hello hello web 應用程式所需的 PHP 版本。
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. 現在已設定 hello PHP 版本。 您可確認這些設定：
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Azure 命令列介面 (Linux、Mac、Windows)
toouse hello Azure 命令列介面，您必須具有**Node.js**安裝在電腦上。

1. 開啟 終端機和登入 tooyour 帳戶。
   
        azure login
2. 設定 hello hello web 應用程式所需的 PHP 版本。
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. 現在已設定 hello PHP 版本。 您可確認這些設定：
   
        azure site show {app-name}

> [!NOTE] 
> hello [Azure CLI 2.0](https://github.com/Azure/azure-cli)是對等 toohello 上述的命令：
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>如何： 變更 hello 內建的 PHP 設定
任何內建的 PHP 執行階段，您可以依照以下 hello 步驟 hello 組態選項的任何變更。 (如需 php.ini 指示詞的資訊，請參閱 [php.ini 指示詞的清單](英文))。

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>變更 PHP\_INI\_USER、PHP\_INI\_PERDIR、PHP\_INI\_ALL 組態設定
1. 新增[。 user.ini]檔案 tooyour 根目錄。
2. 新增組態設定 toohello`.user.ini`檔案使用 hello 中會使用相同的語法`php.ini`檔案。 例如，如果您想要 tooturn hello`display_errors`設定開始和設定`upload_max_filesize`設定 too10M，您`.user.ini`檔案會包含此文字：
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. 部署 Web 應用程式。
4. 重新啟動 hello web 應用程式。 (重新啟動，所以需要哪些 PHP hello 頻率讀取`.user.ini`檔案由 hello`user_ini.cache_ttl`設定，而這是系統層級設定，預設為 300 秒 （5 分鐘）。 重新啟動的 hello web 應用程式會強制在 hello 的 PHP tooread hello 新設定`.user.ini`檔案。)

做為替代的 toousing`.user.ini`檔案中，您可以使用 hello [ini_set()]函式中不是系統層級指示詞的指令碼 tooset 組態選項。

### <a name="changing-phpinisystem-configuration-settings"></a>變更 PHP\_INI\_SYSTEM 組態設定
1. 新增應用程式設定 tooyour Web 應用程式與 hello 索引鍵`PHP_INI_SCAN_DIR`和值`d:\home\site\ini`
2. 建立`settings.ini`檔案使用 Kudu 主控台 (http://&lt;站台名稱&gt;。 scm.azurewebsite.net) 在 hello`d:\home\site\ini`目錄。
3. 新增組態設定 toohello`settings.ini`檔案使用 hello php.ini 檔案中，您會使用相同的語法。 例如，如果您想要 toopoint hello`curl.cainfo`設定 tooa`*.crt`檔案並設定 'wincache.maxfilesize' 設定 too512K，您`settings.ini`檔案會包含此文字：
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. 重新啟動 Web 應用程式 tooload hello 做的變更。

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>如何： 啟用 hello 預設 PHP 執行階段中的擴充功能
延伸模組所述 hello 上一節、 hello 最佳方式 toosee hello 預設 PHP 版本、 其預設組態及啟用的 hello 是 toodeploy 指令碼中呼叫[phpinfo （)]。 tooenable 其他擴充功能，請遵循下列 hello 步驟：

### <a name="configure-via-ini-settings"></a>透過 ini 設定來設定
1. 新增`ext`目錄 toohello`d:\home\site`目錄。
2. Put`.dll`延伸模組檔案中 hello`ext`目錄 (例如， `php_xdebug.dll`)。 請確定 hello 延伸模組是與 PHP 和 VC9 以及非安全執行緒 （來） 相容的預設版本相容。
3. 新增應用程式設定 tooyour Web 應用程式與 hello 索引鍵`PHP_INI_SCAN_DIR`和值`d:\home\site\ini`
4. 在名為 `extensions.ini` 的 `d:\home\site\ini` 中建立 `ini` 檔案。
5. 新增組態設定 toohello`extensions.ini`檔案使用 hello php.ini 檔案中，您會使用相同的語法。 例如，如果您想要 tooenable hello MongoDB 和 XDebug 擴充功能，您`extensions.ini`檔案會包含此文字：
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. 重新啟動 Web 應用程式 tooload hello 做的變更。

### <a name="configure-via-app-setting"></a>透過應用程式設定來設定
1. 新增`bin`目錄 toohello 根目錄。
2. Put`.dll`延伸模組檔案中 hello`bin`目錄 (例如， `php_xdebug.dll`)。 請確定 hello 延伸模組是與 PHP 和 VC9 以及非安全執行緒 （來） 相容的預設版本相容。
3. 部署 Web 應用程式。
4. 瀏覽 tooyour hello Azure 入口網站中的 web 應用程式，然後按一下 hello**設定** 按鈕。
   
    ![Web 應用程式設定][settings-button]
5. 從 hello**設定**刀鋒視窗選取**應用程式設定**捲動 toohello**應用程式設定**> 一節。
6. 在 hello**應用程式設定**區段中，建立**PHP_EXTENSIONS**索引鍵。 此索引鍵的 hello 值會是根路徑相對 toowebsite: **bin\your ext 檔案**。
   
    ![啟用應用程式設定中的擴充][php-extensions]
7. 按一下 hello**儲存**按鈕上方的 hello hello **Web 應用程式設定**刀鋒視窗。
   
    ![儲存組態設定。][save-button]

Zend 擴充功能也支援使用 **PHP_ZENDEXTENSIONS** 索引鍵。 tooenable 多個副檔名，包括以逗號分隔清單`.dll`hello 應用程式設定值的檔案。

## <a name="how-to-use-a-custom-php-runtime"></a>做法：使用自訂 PHP 執行階段
而不是 hello 預設 PHP 執行階段，App Service Web 應用程式可以使用您提供 tooexecute PHP 指令碼 PHP 執行階段。 您可以設定您所提供的 hello 執行階段`php.ini`也提供的檔案。 toouse 自訂的 PHP 執行階段透過 Web 應用程式，請遵循下列 hello 步驟。

1. 取得 PHP for Windows 的非安全執行緒 VC9 或 VC11 相容版本。 可以在下列網址找到最新版 PHP for Windows： [http://windows.php.net/download/]。 較舊的版本可以在這裡 hello 封存： [http://windows.php.net/downloads/releases/archives/]。
2. 修改 hello`php.ini`程式執行階段的檔案。 請注意，Web Apps 將忽略僅系統層級指示詞的任何組態設定 (如需僅系統層級指示詞的資訊，請參閱 [php.ini 指示詞的清單] (英文))。
3. （選擇性） 加入延伸模組 tooyour PHP 執行階段，並讓它們在 hello`php.ini`檔案。
4. 新增`bin`目錄 tooyour 根目錄和包含您的 PHP 執行階段中的 put 的 hello 目錄 (例如， `bin\php`)。
5. 部署 Web 應用程式。
6. 瀏覽 tooyour hello Azure 入口網站中的 web 應用程式，然後按一下 hello**設定** 按鈕。
   
    ![Web 應用程式設定][settings-button]
7. 從 hello**設定**刀鋒視窗選取**應用程式設定**捲動 toohello**處理常式對應**> 一節。 新增`*.php`toohello 延伸模組欄位和加入 hello 路徑 toohello`php-cgi.exe`可執行檔。 如果您將您的 PHP 執行階段放在 hello `bin` hello 路徑會是您的應用程式的 hello 根目錄中的目錄， `D:\home\site\wwwroot\bin\php\php-cgi.exe`。
   
    ![指定處理常式對應中的處理常式][handler-mappings]
8. 按一下 hello**儲存**按鈕上方的 hello hello **Web 應用程式設定**刀鋒視窗。
   
    ![儲存組態設定。][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>做法︰在 Azure 中啟用編輯器自動化
App Service 預設不會對 composer.json (如果您 PHP 專案中有的話) 執行任何操作。 如果您使用[Git 部署](app-service-deploy-local-git.md)，您可以啟用 composer.json 處理期間`git push`藉由啟用 hello 編輯器延伸模組。

> [!NOTE]
> 您可以 [在這裡投票選擇 App Service 中的頂級編輯器支援](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)！
> 
> 

1. 在您的 PHP web 應用程式的刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **工具** > **延伸**。
   
    ![Azure 入口網站設定 刀鋒視窗 tooenable Azure 中的編輯器自動化](./media/web-sites-php-configure/composer-extension-settings.png)
2. 按一下 [新增]，然後按一下 [編輯器]。
   
    ![加入在 Azure 中的編輯器延伸模組 tooenable 編輯器自動化](./media/web-sites-php-configure/composer-extension-add.png)
3. 按一下**確定**tooaccept 法律條款。 按一下**確定**再次 tooadd hello 延伸模組。
   
    hello**擴充功能安裝**刀鋒視窗現在將會顯示 hello 編輯器延伸模組。  
    ![接受 Azure 中的法律條款 tooenable 編輯器自動化](./media/web-sites-php-configure/composer-extension-view.png)
4. 現在，執行`git add`， `git commit`，和`git push`如同在 hello 上一節。 您就會立即看到編輯器正在安裝 composer.json 中定義的相依性。
   
    ![使用 Azure 中的「編輯器」自動化來進行 Git 部署](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
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

