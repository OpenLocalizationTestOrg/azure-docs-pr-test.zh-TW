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
# <a name="how-toocreate-php-web-and-worker-roles"></a>如何 toocreate PHP web 和背景工作角色
## <a name="overview"></a>概觀
本指南將說明 toocreate PHP web 或背景工作角色在 Windows 開發環境中，選擇特定版本的 PHP hello 從可用的 「 內建 」 版本的方式、 變更 hello 的 PHP 設定、 啟用擴充功能，和最後，部署 tooAzure。 它也會說明如何 tooconfigure web 或背景工作角色 toouse 您提供 PHP 執行階段 （使用自訂組態和擴充功能）。

## <a name="what-are-php-web-and-worker-roles"></a>什麼是 PHP Web 和背景工作角色？
Azure 提供三種運算模型來執行應用程式：Azure 應用程式服務、Azure 虛擬機器和 Azure 雲端服務。 這三種模型都支援 PHP。 雲端服務 (包含 Web 和背景工作角色) 可提供 *平台即服務 (PaaS)*。 在雲端服務中，web 角色會提供專用的 Internet Information Services (IIS) web 伺服器 toohost 前端 web 應用程式。 背景工作角色可以執行非同步、長時間或永久的工作，且不受使用者互動或輸入所影響。

如需這些選項的詳細資訊，請參閱[計算 Azure 提供的裝載選項](cloud-services/cloud-services-choose-me.md)。

## <a name="download-hello-azure-sdk-for-php"></a>下載 hello Azure SDK for PHP
hello [Azure SDK for PHP]數個元件所組成。 此發行項將會使用其中兩個： Azure PowerShell 和 hello Azure 模擬器。 這兩個元件可以透過 hello Microsoft Web Platform Installer 安裝。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="create-a-cloud-services-project"></a>建立雲端服務專案
在建立 PHP web 或背景工作角色的 hello 第一個步驟是 toocreate Azure 服務專案。 Azure 服務專案當做 web 和背景工作角色的邏輯容器，它包含 hello 專案[服務定義 (.csdef)]和[服務組態 (.cscfg)]檔案。

toocreate 新的 Azure 服務專案，為系統管理員，以執行 Azure PowerShell，然後執行下列命令的 hello:

    PS C:\>New-AzureServiceProject myProject

此命令會建立新的目錄 (`myProject`) toowhich 您可以加入 web 和背景工作角色。

## <a name="add-php-web-or-worker-roles"></a>新增 PHP Web 或背景工作角色
tooadd PHP web 角色 tooa 專案中，執行下列命令從 hello 專案根目錄中的 hello:

    PS C:\myProject> Add-AzurePHPWebRole roleName

對於背景工作角色，請使用下列命令：

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> hello`roleName`參數是選擇性的。 如果省略，將會自動產生 hello 角色名稱。 hello 建立第一個 web 角色`WebRole1`，第二個會是 hello `WebRole2`，依此類推。 hello 建立第一個背景工作角色就會是`WorkerRole1`，第二個會是 hello `WorkerRole2`，依此類推。
>
>

## <a name="specify-hello-built-in-php-version"></a>指定 hello 內建的 PHP 版本
當您新增 PHP web 或背景工作角色 tooa 專案時，以便在部署時，將應用程式的每個 web 或背景工作執行個體上安裝 PHP，會修改 hello 專案的組態檔。 根據預設，執行下列命令的 hello 將會安裝的 PHP toosee hello 版本：

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

hello 上述 hello 命令的輸出看起來類似 toowhat 如下所示。 在此範例中，hello`IsDefault`旗標設定得`true`for PHP 5.3.17，表示它將會安裝 hello 預設的 PHP 版本。

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

您可以設定 hello PHP 執行階段版本 tooany 的 hello 所列的 PHP 版本。 例如，tooset hello PHP 版本 (hello 名稱的角色`roleName`) too5.4.0，下列命令使用 hello:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Hello 未來可能會變更可用的 PHP 版本。
>
>

## <a name="customize-hello-built-in-php-runtime"></a>自訂 hello 內建的 PHP 執行階段
已擁有 hello PHP 執行階段，當您遵循 hello 上述的步驟，包括修改安裝 hello 組態的完整控制權`php.ini`設定及啟用擴充功能。

toocustomize hello 內建的 PHP 執行階段，請遵循下列步驟：

1. 加入新的資料夾，名為`php`，toohello `bin` web 角色的目錄。 背景工作角色，將它加入 toohello 角色的根目錄。
2. 在 hello`php`資料夾中，建立名為另一個資料夾`ext`。 將它放置在`.dll`延伸模組檔案 (例如`php_mongo.dll`) 您想 tooenable 此資料夾中的。
3. 新增`php.ini`檔案 toohello`php`資料夾。 在此檔案中啟用自訂擴充功能，並設定 PHP 指示詞。 比方說，如果您想要 tooturn`display_errors`上並啟用 hello`php_mongo.dll`擴充功能，以 hello 內容您`php.ini`檔案將會如下：

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> 您不需要明確 hello 中設定任何設定`php.ini`檔案會自動提供將它設為 tootheir 預設值。 但請留意，您可以新增完整的 `php.ini` 檔案。
>
>

## <a name="use-your-own-php-runtime"></a>使用您自己的 PHP 執行階段
在某些情況下，而不是選取內建的 PHP 執行階段並加以設定 （如上所述），您可能想 tooprovide 您自己的 PHP 執行階段。 例如，您可以使用相同的 PHP 執行階段，您在開發環境中使用的 web 或背景工作角色中的 hello。 這可讓您更輕鬆 tooensure hello 應用程式不會變更您的生產環境中的行為。

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>設定 web 角色 toouse 您自己的 PHP 執行階段
tooconfigure web 角色 toouse PHP 執行階段提供時，請遵循下列步驟：

1. 如本主題先前所述，建立 Azure 服務專案並加入 PHP Web 角色。
2. 建立`php`資料夾中 hello`bin`資料夾，其位於 web 角色的根目錄，並將您的 PHP 執行階段 （所有二進位檔、 組態檔、 子資料夾等） toohello`php`資料夾。
3. （選擇性）如果您的 PHP 執行階段使用 hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers]，您將需要 tooconfigure 您的 web 角色 tooinstall [SQL Server Native Client 2012] [sql native client]時加以佈建。 toodo，新增 hello [sqlncli.msi x64 installer] toohello `bin` web 角色的根目錄中的資料夾。 hello hello 下一個步驟中所述的啟動指令碼 hello 角色佈建時，會以無訊息模式執行 hello 安裝程式。 如果您的 PHP 執行階段不使用 hello Microsoft Drivers for PHP for SQL Server，您可以移除 hello hello 下一個步驟中所顯示的 hello 指令碼中的下列行：

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. 定義設定的啟動工作[網際網路資訊服務 (IIS)] [ iis.net] toouse 要求您的 PHP 執行階段 toohandle`.php`頁面。 toodo，開啟 hello`setup_web.cmd`檔案 (在 hello `bin` web 角色的根目錄的檔案) 中的文字編輯器，並取代其內容與 hello 下列指令碼：

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
5. 新增應用程式檔案 tooyour web 角色的根目錄。 這會是 hello web 伺服器的根目錄。
6. 將應用程式發行 hello 中所述[發行您的應用程式](#publish-your-application)下一節。

> [!NOTE]
> hello`download.ps1`指令碼 (在 hello `bin` hello web 角色的根目錄資料夾) 可以執行上面所述，使用您自己的 PHP 執行階段的 hello 步驟之後刪除。
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>設定背景工作角色 toouse 您自己的 PHP 執行階段
tooconfigure 背景工作角色 toouse PHP 執行階段提供時，請遵循下列步驟：

1. 如本主題先前所述，建立 Azure 服務專案並加入 PHP 背景工作角色。
2. 建立`php`hello 背景工作角色的根目錄中的資料夾，然後新增您的 PHP 執行階段 （所有二進位檔、 組態檔、 子資料夾等） toohello`php`資料夾。
3. （選擇性）如果您的 PHP 執行階段使用[Microsoft Drivers for PHP for SQL Server][sqlsrv drivers]，您將需要 tooconfigure 程式背景工作角色 tooinstall [SQL Server Native Client 2012] [sql native client]時加以佈建。 toodo，新增 hello [sqlncli.msi x64 installer] toohello 背景工作角色的根目錄。 hello hello 下一個步驟中所述的啟動指令碼 hello 角色佈建時，會以無訊息模式執行 hello 安裝程式。 如果您的 PHP 執行階段不使用 hello Microsoft Drivers for PHP for SQL Server，您可以移除 hello hello 下一個步驟中所顯示的 hello 指令碼中的下列行：

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. 定義啟動工作加入您`php.exe`hello 角色佈建時可執行檔 toohello 背景工作角色的 PATH 環境變數。 toodo，開啟 hello`setup_worker.cmd`檔案 （位於 hello 背景工作角色的根目錄），在文字編輯器中，並且其內容取代下列指令碼的 hello:

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
5. 加入您的應用程式檔案 tooyour 背景工作角色的根目錄。
6. 將應用程式發行 hello 中所述[發行您的應用程式](#publish-your-application)下一節。

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>在 hello 計算和儲存體模擬器執行應用程式
hello Azure 模擬器會提供在其中您可以測試 Azure 應用程式部署 toohello 雲端之前，先在本機環境。 有一些 hello 模擬器與 hello Azure 環境之間的差異。 這更好，請參閱的 toounderstand[使用 hello Azure 儲存體模擬器進行開發和測試](storage/common/storage-use-emulator.md)。

請注意，您必須擁有 PHP 安裝在本機 toouse hello 計算模擬器。 hello 計算模擬器會使用您本機的 PHP 安裝 toorun 您的應用程式。

toorun 專案 hello 模擬器中的執行下列命令，從您的專案根目錄 hello:

    PS C:\MyProject> Start-AzureEmulator

您會看到輸出類似 toothis:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

您可以看到您的應用程式開啟網頁瀏覽器並瀏覽 toohello hello 輸出中所示的本機位址 hello 模擬器中執行 (`http://127.0.0.1:81`在 hello 上面的範例輸出中)。

toostop hello 模擬器，執行此命令：

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>發佈您的應用程式
toopublish 應用程式時，您需要 toofirst 匯入您發行設定使用 hello [Import-azurepublishsettingsfile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet。 然後您可以發行應用程式使用 hello[發行 AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet。 如需登入資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[Azure SDK for PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[服務定義 (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[服務組態 (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64 installer]: http://go.microsoft.com/fwlink/?LinkID=239648
