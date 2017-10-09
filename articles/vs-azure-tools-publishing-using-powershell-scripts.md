---
title: "aaaUsing Windows PowerShell 指令碼 tooPublish tooDev 和測試環境 |Microsoft 文件"
description: "了解如何 toouse Windows PowerShell 指令碼，從 Visual Studio toopublish toodevelopment 和測試環境。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>使用 Windows PowerShell 指令碼 toopublish toodev 和測試環境
當您在 Visual Studio 中建立 web 應用程式時，您可以產生 Windows PowerShell 指令碼可讓您的網站 tooAzure 稍後 tooautomate hello 發佈為 Web 應用程式在 Azure 應用程式服務或虛擬機器。 您可以編輯和擴充 hello hello Visual Studio 編輯器 toosuit 中的 Windows PowerShell 指令碼程式的需求，或與現有的組建、 測試和發佈指令碼整合 hello 指令碼。

使用這些指令碼，您可以佈建網站的自訂版本 (也稱為開發和測試環境)，以做臨時使用。 比方說，您可能會設定您的網站的特定版本 Azure 的虛擬機器上或在暫存位置上的網站 toorun hello 測試套件、 重現錯誤、 測試錯誤修正、 試驗提議的變更，或設定示範或展示的自訂環境。 您已建立的指令碼可用於發行專案之後，您可以重新執行 hello 指令碼，如有需要重新建立相同的環境，或執行您 web 應用程式 toocreate 的組建進行測試的自訂環境的 hello 指令碼。

## <a name="what-you-need"></a>您需要什麼
* Azure SDK 2.3 或更新版本。 如需詳細資訊，請參閱 [Visual Studio 下載](http://go.microsoft.com/fwlink/?LinkID=624384) 。

您不需要 web 專案 hello Azure SDK toogenerate hello 指令碼。 這項功能是供 Web 專案使用，而非供雲端服務中的 Web 角色使用。

* Azure PowerShell 0.7.4 或更新版本。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。
* [Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) 或更新版本。

## <a name="additional-tools"></a>其他工具
我們有提供其他工具和資源，以供您在 Visual Studio 中使用 PowerShell 進行 Azure 開發。 請參閱 [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012)。

## <a name="generating-hello-publish-scripts"></a>產生 hello 發行指令碼
您可以產生 hello 裝載您的網站，當您使用建立新專案的虛擬機器的發行指令碼[這些指示](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 您也可以 [在 Azure App Service 中產生 Web 應用程式的發佈指令碼](app-service-web/app-service-web-get-started-dotnet.md)。

## <a name="scripts-that-visual-studio-generates"></a>Visual Studio 所產生的指令碼
Visual Studio 會產生名為方案層級資料夾**PublishScripts** ，其中包含兩個 Windows PowerShell 檔案，您的虛擬機器或網站，並含有可讓您在 hello 函式的模組的發行指令碼指令碼。 Visual Studio 也會產生以指定您要部署的 hello 專案 hello 詳細資料的 hello JSON 格式的檔案。

### <a name="windows-powershell-publish-script"></a>Windows PowerShell 發佈指令碼
hello 發行指令碼包含特定發行步驟部署 tooa 網站或虛擬機器。 Visual Studio 提供語法著色功能，可用來進行 Windows PowerShell 開發。 說明 hello 函式，而且您可以自由地編輯 hello 指令碼 toosuit 中的 hello 函式多變的需求。

### <a name="windows-powershell-module"></a>Windows PowerShell 模組
hello Visual Studio 會產生的模組包含 hello 函式的 Windows PowerShell 發行指令碼使用。 這些是 Azure PowerShell 函數，而且不想要修改的 toobe。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。

### <a name="json-configuration-file"></a>JSON 組態檔
hello JSON 檔案建立在 hello**組態**資料夾並包含指定完全哪些資源 toodeploy tooAzure 的組態資料。 hello hello Visual Studio 所產生名稱是檔案的專案的名稱-WAWS-DEV.JSON-稱為如果您建立網站或專案名稱 VM 稱為若已建立虛擬機器。 以下是建立網站時所產生之 JSON 組態檔的範例。 大部分 hello 值都一目了然。 hello 網站名稱是由 Azure 產生，所以可能不符合您的專案名稱。

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
當您建立虛擬機器時，hello JSON 組態檔看起來類似 toohello 下列。 請注意，雲端服務會建立為 hello 虛擬機器的容器。 hello 虛擬機器包含 hello 透過 HTTP 和 HTTPS 進行 web 存取的一般端點以及 Web deploy，它可讓您從本機電腦、 遠端桌面和 Windows PowerShell toohello 網站發行端點。

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

您可以編輯 hello JSON 組態 toochange 執行 hello 時，會發生什麼事發行指令碼。 hello`cloudService`和`virtualMachine`區段都是必要的但您可以刪除 hello`databases`區段，如果您不需要它。 Visual Studio 會產生的 hello 預設組態檔中的 空白的 hello 屬性是選擇性的;具有值 hello 預設組態檔中的所需。

如果您的網站有多個部署環境 （又稱為位置），而不是在 Azure 中的單一生產網站，您可以在 hello hello JSON 組態檔中的 hello 網站名稱中包含 hello 位置名稱。 例如，如果您有一個名為的網站**mysite**和名為位置**測試**然後 hello URI 為 mysite test.cloudapp.net，但 hello hello 組態檔中的正確名稱 toouse 為 mysite （test）. 您可以只這樣如果 hello 網站和位置存在於訂用帳戶。 如果不存在，但不指定 hello 位置執行 hello 指令碼來建立 hello 網站，然後建立 hello 中的 hello 位置[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，以及此後 hello 修改後的網站名稱用來執行 hello 指令碼。 如需 Web 應用程式部署位置的詳細資訊，請參閱 [針對 Azure App Service 中的 Web 應用程式設定預備環境](app-service-web/web-sites-staged-publishing.md)。

## <a name="how-toorun-hello-publish-scripts"></a>Toorun hello 發行指令碼的方式
如果您從未執行過 Windows PowerShell 指令碼之前，您必須先設定 hello 執行原則 tooenable 指令碼 toorun。 這是從執行 Windows PowerShell 指令碼，很容易遭受 toomalware 或病毒威脅的執行指令碼時的安全性功能 tooprevent 使用者。

### <a name="run-hello-script"></a>執行 hello 指令碼
1. 建立 hello Web Deploy 封裝您的專案。 Web Deploy 套件是經過壓縮的封存 （.zip 檔），其中包含您想 toocopy tooyour 網站或虛擬機器的檔案。 您可以在 Visual Studio 中為任何 Web 應用程式建立 Web Deploy 封裝。

![建立 Web Deploy 封裝](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

如需詳細資訊，請參閱 [如何：在 Visual Studio 中建立 Web 部署封裝](https://msdn.microsoft.com/library/dd465323.aspx)。 您也可以在 hello > 一節中所述自動化 hello 建立您的 Web Deploy 封裝，**自訂和擴充 hello 發行指令碼**本主題稍後。

1. 在**方案總管 中**，開啟 hello hello 指令碼的操作功能表，然後選擇**開啟 PowerShell ISE 與**。
2. 如果這是 hello 您已在此電腦執行 Windows PowerShell 指令碼的第一次，開啟命令提示字元視窗使用系統管理員權限和型別 hello 下列命令：

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. 使用下列命令的 hello 登入 tooAzure。

    ```powershell
    Add-AzureAccount
    ```

    出現提示時，提供您的使用者名稱和密碼。

    請注意當您自動執行 hello 指令碼，這個方法提供的 Azure 認證將無法運作。 相反地，您應該使用 hello.publishsettings 檔案 tooprovide 認證。 一次您只能使用 hello 命令**Get-azurepublishsettingsfile** toodownload hello Azure 中，從檔案，之後使用**Import-azurepublishsettingsfile** tooimport hello 檔案。 如需詳細指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

4. （選擇性）如果您想 toocreate Azure 資源 hello 虛擬機器、 資料庫和網站，但不要發行 web 應用程式，例如使用 hello **Publish-webapplication.ps1**命令與 hello **-組態**引數設定 toohello JSON 組態檔。 此命令列使用 hello JSON 組態檔 toodetermine 哪些資源 toocreate。 它會使用其他命令列引數的 hello 預設設定，因為它會建立 hello 資源，但不會發行 web 應用程式。 hello – Verbose 選項提供有關最新動態的詳細資訊。

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. 使用 hello **Publish-webapplication.ps1**命令中其中一個 hello 遵循範例 tooinvoke hello 指令碼所示，並發行您的 web 應用程式。 如果您需要 toooverride hello 預設設定任何 hello 其他引數，例如 hello 訂用帳戶名稱、 發行套件名稱、 虛擬機器認證或資料庫伺服器認證，您可以指定這些參數。 使用 hello **– Verbose**選項 toosee hello 發行程序的 hello 進度的詳細資訊。

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    如果您要建立虛擬機器，hello 命令看起來 hello 下列。 此範例也顯示如何 toospecify hello 認證的多個資料庫。 這些指令碼建立的 hello 虛擬機器，hello SSL 憑證不是來自受信任的根授權單位。 因此，您需要 toouse hello **-AllowUntrusted**選項。

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    hello 指令碼可以建立資料庫，但它不會建立資料庫伺服器。 如果您想 toocreate 資料庫伺服器，您可以使用 hello **New-azuresqldatabaseserver** hello Azure 模組中的函式。

## <a name="customizing-and-extending-hello-publish-scripts"></a>自訂及擴充 hello 發行指令碼
您可以自訂 hello 發行指令碼和 JSON 組態檔。 hello hello Windows PowerShell 模組中的函式**AzureWebAppPublishModule.psm1**不是預期的 toobe 修改。 如果您只想 toospecify 不同的資料庫，或變更某些 hello hello 虛擬機器內容，編輯 hello JSON 組態檔。 如果您想要的 hello 指令碼 tooautomate 建置和測試專案的 tooextend hello 功能，您可以實作中的函數虛設常式**Publish-webapplication.ps1**。

tooautomate 建置您的專案，加入程式碼太呼叫 MSBuild 的`New-WebDeployPackage`這個程式碼範例所示。 hello 路徑 toohello MSBuild 命令是 hello 您已安裝的 Visual Studio 版本而有所不同。 tooget hello 正確的路徑，您可以使用 hello 函式**Get-msbuildcmd**，在此範例所示。

### <a name="tooautomate-building-your-project"></a>tooautomate 建置專案
1. 新增 hello `$ProjectFile` hello 全域 param 區段中的參數。

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Copy hello 函式`Get-MSBuildCmd`到指令碼檔案。

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. 取代`New-WebDeployPackage`以下列程式碼，並且在 hello 行建構 hello 預留位置取代的 hello `$msbuildCmd`。 此程式碼係用於 Visual Studio 2015。 如果您使用 Visual Studio 2013，變更 hello **VisualStudioVersion**下面的屬性過`12.0`。

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild 您 web 應用程式，請使用 MsBuild.exe。 如需協助，請參閱 MSBuild 命令列參考︰[http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>開始執行 hello 建置命令

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. 呼叫 hello`New-WebDeployPackage`此行之前的函式： `$Config = Read-ConfigFile $Configuration` web 應用程式或`$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)`的虛擬機器。

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. 叫用自訂的 hello 指令碼，從命令列使用傳遞 hello`$Project`引數，如同下列範例命令列的 hello。

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    tooautomate 測試應用程式加入程式碼太`Test-WebApplication`。 中的 hello 線條會確定 toouncomment **Publish-webapplication.ps1**呼叫這些函數。 如果您沒有提供實作，您可以手動建立 Visual Studio 中，您的專案，然後執行的 hello 發行指令碼 toopublish tooAzure。

## <a name="publishing-function-summary"></a>發佈函式摘要
tooget 說明您可以在 hello Windows PowerShell 命令提示字元中使用的函式使用 hello 命令`Get-Help function-name`。 hello 說明包括參數說明和範例。 在 hello 指令碼來源檔案，也有相同的說明文字的 hello **AzureWebAppPublishModule.psm1**和**Publish-webapplication.ps1**。 hello 指令碼和說明都以您的 Visual Studio 語言進行當地語系化。

**AzureWebAppPublishModule**

| 函式名稱 | 說明 |
| --- | --- |
| Add-AzureSQLDatabase |建立新的 Azure SQL Database。 |
| Add-AzureSQLDatabases |從 Visual Studio 會產生的 hello JSON 組態檔中的 hello 值建立 Azure SQL 資料庫。 |
| Add-AzureVM |建立 Azure 虛擬機器並傳回 hello hello URL 部署 VM。 hello 函式中設定 hello 必要條件，然後呼叫 hello **New-azurevm**函式 （Azure 模組） toocreate 新的虛擬機器。 |
| Add-AzureVMEndpoints |加入新的輸入的端點 tooa 虛擬機器並傳回 hello 與 hello 新端點的虛擬機器。 |
| Add-AzureVMStorage |Hello 目前訂用帳戶中建立新的 Azure 儲存體帳戶。 hello hello 帳戶名稱的開頭"devtest"後面接著唯一英數字串。 hello 函式會傳回 hello hello 新的儲存體帳戶名稱。 您必須指定位置或同質群組 hello 新儲存體帳戶。 |
| Add-AzureWebsite |具有 hello 指定的名稱和位置建立網站。 此函式呼叫 hello **New-azurewebsite** hello Azure 模組中的函式。 如果 hello 訂用帳戶已不包含具有指定名稱的 hello 的網站，此函式建立 hello 網站，並傳回網站物件。 否則，它會傳回 `$null`。 |
| Backup-Subscription |儲存 hello 目前 Azure 訂用帳戶中 hello`$Script:originalSubscription`指令碼範圍的變數。此函式會將儲存 hello 目前的 Azure 訂用帳戶 (由`Get-AzureSubscription -Current`) 及其儲存體帳戶和 hello 訂用帳戶，此指令碼變更 (hello 變數中儲存`$UserSpecifiedSubscription`) 與其儲存體帳戶，指令碼範圍。 藉由儲存 hello 值，您可以使用函式，例如`Restore-Subscription`，toorestore hello 原始目前訂用帳戶和儲存體帳戶 toocurrent 狀態如果 hello 目前狀態已變更。 |
| Find-AzureVM |取得 hello 指定 Azure 虛擬機器。 |
| Format-DevTestMessageWithTime |前面加上 hello tooa 訊息的日期和時間。 此函式可供寫入 toohello Error 和 Verbose 串流的訊息。 |
| Get-AzureSQLDatabaseConnectionString |組合連接字串 tooconnect tooan Azure SQL database。 |
| Get-AzureVMStorage |傳回 hello hello 名稱模式 hello 第一個儲存體帳戶名稱"devtest*"（不區分大小寫） hello 指定的位置或同質群組中。如果 hello"devtest*"hello 位置或同質群組，不符合儲存體帳戶、 hello 函式則會予以忽略。 您必須指定位置或同質群組。 |
| Get-MSDeployCmd |傳回命令 toorun hello MsDeploy.exe 工具。 |
| New-AzureVMEnvironment |尋找或建立 hello 訂用帳戶符合 hello JSON 組態檔中的 hello 值中的虛擬機器。 |
| Publish-WebPackage |使用 MsDeploy.exe 和 web 發行套件。Zip 檔案 toodeploy 資源 tooa 網站。 此函式不會產生任何輸出。 如果 hello 呼叫 tooMSDeploy.exe，hello 函式會擲回例外狀況。 tooget 更多詳細的輸出，使用 hello **-Verbose**選項。 |
| Publish-WebPackageToVM |驗證 hello 參數值，然後呼叫 hello **Publish-webpackage**函式。 |
| Read-ConfigFile |驗證 hello JSON 組態檔並傳回所選值的雜湊資料表。 |
| Restore-Subscription |重設 hello 目前訂用帳戶 toohello 原始訂用帳戶。 |
| Test-AzureModule |傳回`$true`如果 hello 安裝的 Azure 模組版本為 0.7.4 或更新版本。 傳回`$false`如果 hello 模組尚未安裝，或是為舊的版本。 此函式沒有參數。 |
| Test-AzureModuleVersion |傳回`$true`如果 hello hello Azure 模組版本為 0.7.4 或更新版本。 傳回`$false`如果 hello 模組尚未安裝，或是為舊的版本。 此函式沒有參數。 |
| Test-HttpsUrl |將轉換 hello 輸入的 URL tooa System.Uri 物件。 傳回`$True`如果 hello URL 為絕對且其配置為 https。 傳回`$false`如果 hello URL 是相對路徑、 其配置不是 HTTPS，或 hello 輸入的字串不能轉換的 tooa URL。 |
| Test-Member |傳回`$true`如果屬性或方法是 hello 物件的成員。 否則傳回 `$false`。 |
| Write-ErrorWithTime |寫入前面會加上 hello 目前時間的錯誤訊息。 此函式呼叫 hello **Format-devtestmessagewithtime**寫入 hello 訊息 toohello 錯誤資料流之前的函式 tooprepend hello 時間。 |
| Write-HostWithTime |寫入訊息 toohello 主機程式 (**Write-host**) 加上 hello 目前的時間。 撰寫 toohello 主機程式的 hello 效果各不相同。 大部分程式中主控 Windows PowerShell 的這些訊息 toostandard 將輸出寫入。 |
| Write-VerboseWithTime |寫入前面會加上 hello 目前時間的詳細資訊訊息。 因為它會呼叫**Write-verbose**，hello 訊息會顯示只有 hello 指令碼執行時以 hello **Verbose**參數或當 hello **VerbosePreference**是喜好設定設定得**繼續**。 |

**Publish-WebApplication**

| 函式名稱 | 說明 |
| --- | --- |
| New-AzureWebApplicationEnvironment |建立 Azure 資源，例如網站或虛擬機器。 |
| New-WebDeployPackage |此函式未實作。 您可以在這個函式 toobuild 中新增命令，您的專案。 |
| Publish-AzureWebApplication |發行 web 應用程式 tooAzure。 |
| Publish-WebApplication |建立並部署 Visual Studio Web 專案的 Web Apps、虛擬機器、SQL Database 和儲存體帳戶。 |
| Test-WebApplication |此函式未實作。 您可以在這個函式 tootest 中新增命令，您的應用程式。 |

## <a name="next-steps"></a>後續步驟
深入了解 PowerShell 的指令碼讀取[使用 Windows PowerShell 撰寫指令碼](https://technet.microsoft.com/library/bb978526.aspx)並查看其他的 Azure PowerShell 指令碼，於 hello[指令碼中心](https://azure.microsoft.com/documentation/scripts/)。
