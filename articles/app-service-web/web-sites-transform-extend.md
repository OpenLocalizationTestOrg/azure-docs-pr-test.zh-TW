---
title: "App Service web 應用程式 aaaAzure 進階組態和延伸模組"
description: "使用 XML 文件 Transformation(XDT) 宣告 tootransform hello ApplicationHost.config 檔案中您 Azure App Service web 應用程式和 tooadd 私人延伸 tooenable 自訂系統管理動作。"
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Azure App Service Web 應用程式進階設定和擴充功能
使用[XML 文件轉換](http://msdn.microsoft.com/library/dd465326.aspx)(XDT) 宣告，您可以將轉換 hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig)在 Azure App Service web 應用程式中的檔案。 您也可以使用 XDT 宣告 tooadd 私人延伸 tooenable 自訂 web 應用程式管理動作。 本文包含一個 PHP Manager Web 應用程式擴充功能範例，該範例會透過 Web 介面來啟用 PHP 設定的管理功能。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>透過 ApplicationHost.config 的進階設定
hello 應用程式服務平台提供 web 應用程式設定彈性和控制。 雖然 hello 標準 IIS ApplicationHost.config 組態檔不是適用於 App Service 中直接編輯的 hello 平台支援宣告式的 ApplicationHost.config 轉換模型，依據 XML 文件轉換 (XDT)。

tooleverage 這項轉換功能，您建立內容與 XDT ApplicationHost.xdt 檔案，並放在 hello 中的 hello 網站根目錄 (d:\home\site) 下[Kudu 主控台](https://github.com/projectkudu/kudu/wiki/Kudu-console)。 您可能需要 toorestart hello Web 應用程式變更 tootake 效果。

hello 遵循 applicationHost.xdt 範例顯示新的自訂環境變數 tooa tooadd web 使用 PHP 5.4 的應用程式的方式。

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

使用從下 LogFiles\Transform hello FTP 根目錄中的記錄檔，以轉換狀態和詳細資料。

如需其他範例，請參閱＜ [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)＞。

**注意**<br />
Hello 之下的模組清單中的項目`system.webServer`無法移除或重新排列，但可能會有新增 toohello 清單。

## <a id="extend"></a> 擴充 Web 應用程式
### <a id="overview"></a> 私人 Web 應用程式擴充功能的概觀
App Service 支援使用 Web 應用程式擴充功能做為系統管理動作的擴充點。 事實上，有些 App Service 平台功能已當作預先安裝的擴充功能來實作。 時無法修改 hello 預先安裝的平台擴充程式，您可以建立及設定私人延伸您自己的 web 應用程式。 這項功能也會依賴 XDT 宣告。 hello 下列 hello 建立私用的 web 應用程式擴充功能的重要步驟︰

1. Web 應用程式擴充功能的「內容」 ：建立任何 App Service 所支援的 Web 應用程式
2. Web 應用程式擴充功能的「宣告」 ：建立 ApplicationHost.xdt 檔案
3. Web 應用程式擴充功能**部署**: hello SiteExtensions 下的資料夾中放置內容`root`

內部連結 hello web 應用程式應該指向 hello ApplicationHost.xdt 檔中指定的 tooa 路徑相對 toohello 應用程式路徑。 任何變更 toohello ApplicationHost.xdt 檔案需要 web 應用程式回收。

**注意**：在 [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions)可取得這些主要元素的其他資訊。

詳細的範例是包含的 tooillustrate hello 步驟為建立和啟用私用的 web 應用程式擴充功能。 hello hello PHP Manager 範例如下所示，可以從網站下載的原始碼[https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager)。

### <a id="SiteSample"></a> Web 應用程式擴充功能範例：PHP Manager
PHP Manager 是 web 應用程式擴充功能，可讓 web 應用程式系統管理員 tooeasily 檢視，並設定其使用 web 介面，而不直接讓 toomodify PHP.ini 檔案的 PHP 設定。 適用於 PHP 的常見組態檔包括 hello php.ini 檔案位於程式檔案和 hello。 user.ini 檔案位於您 web 應用程式的 hello 根資料夾中。 Hello PHP Manager 擴充功能因為 hello php.ini 檔案不能直接編輯 hello 應用程式服務平台上，使用 hello。 user.ini 檔案 tooapply 設定變更。

#### <a id="PHPwebapp"></a>hello PHP 管理員 web 應用程式
hello 下面是 hello PHP Manager 部署的 hello 首頁：

![TransformSitePHPUI][TransformSitePHPUI]

如您所見，web 應用程式擴充功能是一樣的一般 web 應用程式，但額外 ApplicationHost.xdt 檔案放在 hello hello （更多詳細 hello ApplicationHost.xdt 檔案使用，而且這個 hello 下一節中的 web 應用程式的根資料夾文件）。

使用 hello Visual Studio ASP.NET MVC 4 Web 應用程式範本建立 hello PHP Manager 擴充功能。 hello 從方案總管 中的下列檢視顯示 hello 結構 hello PHP Manager 擴充功能。

![TransformSiteSolEx][TransformSiteSolEx]

hello 只特殊邏輯所需的檔案 I/O 是 tooindicate hello hello web 應用程式的 wwwroot 目錄所在的位置。 因為 hello 下列的程式碼範例顯示 hello 環境變數"HOME"指出 hello web 應用程式的根路徑，並可以藉由附加"site\wwwroot"建構 hello wwwroot 路徑：

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


您已擁有 hello 目錄路徑之後，您可以使用一般檔案 I/O 作業 tooread 並寫入 toofiles。

注意： 使用 web 應用程式擴充功能的某一點目前內部連結的 hello 的處理。  如果您提供絕對路徑 toointernal 連結您的 web 應用程式的 HTML 檔案中有任何連結，您必須確定這些連結會加上您的延伸模組名稱，為您的根。 這需要處理，因為您的擴充功能的 hello 根現在是"/`[your-extension-name]`/"而不會只是"/"，因此任何內部連結必須跟著更新。 例如，假設您的程式碼包含連結 toohello 下列：

`"<a href="/Home/Settings">PHP Settings</a>"`

Web 應用程式擴充功能的一部分 hello 連結時，必須在下列形式的 hello hello 連結：

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

您可以使用相對路徑或 web 應用程式中使用 hello hello 的 ASP.NET 應用程式的案例僅解決這項需求`@Html.ActionLink`方法會為您建立 hello 適當的連結。

#### <a id="XDT"></a>hello applicationHost.xdt 檔案
您的 web 應用程式擴充功能的 hello 程式碼會進入下 %HOME%\SiteExtensions\[您的延伸模組名稱]。 我們會呼叫這個 hello 延伸模組的根。  

tooregister hello applicationHost.config 檔案與您 web 應用程式擴充功能，您需要 tooplace 名 ApplicationHost.xdt hello 延伸根目錄中的檔案。 hello hello ApplicationHost.xdt 檔案內容應該如下所示：

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

您選取做為延伸名稱的 hello 名稱必須包含名稱相同的 hello 做為您延伸模組的根資料夾。

這是加入新的應用程式路徑 toohello hello 效果`system.applicationHost`hello SCM 網站下的網站清單。 hello SCM 站台是站台管理端點，具有特定存取認證。 它有 hello URL `https://[your-site-name].scm.azurewebsites.net`。  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <a id="deploy"></a> Web 應用程式擴充功能部署
tooinstall 您 web 應用程式擴充功能，您可以使用 FTP toocopy 您 web 應用程式 toohello 所有 hello 檔案`\SiteExtensions\[your-extension-name]`hello 想 tooinstall hello 延伸模組的 web 應用程式的資料夾。  為確定 toocopy hello ApplicationHost.xdt 檔案 toothis 位置以及。 重新啟動 web 應用程式 tooenable hello 擴充。

您應該能夠 toosee 在您 web 應用程式擴充功能：

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

請注意該 hello URL 看起來就像是 hello URL web 應用程式的不同之處在於它會使用 HTTPS，並包含 「.scm"。

在開發和調查期間為 web 應用程式可能 toodisable 所有私用 （未預先安裝） 延伸模組與 hello 索引鍵加入應用程式設定`WEBSITE_PRIVATE_EXTENSIONS`以及值`0`。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

