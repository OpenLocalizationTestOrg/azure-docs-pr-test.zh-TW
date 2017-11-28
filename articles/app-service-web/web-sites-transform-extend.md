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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="f350d-103">Azure App Service Web 應用程式進階設定和擴充功能</span><span class="sxs-lookup"><span data-stu-id="f350d-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="f350d-104">使用[XML 文件轉換](http://msdn.microsoft.com/library/dd465326.aspx)(XDT) 宣告，您可以將轉換 hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig)在 Azure App Service web 應用程式中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f350d-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="f350d-105">您也可以使用 XDT 宣告 tooadd 私人延伸 tooenable 自訂 web 應用程式管理動作。</span><span class="sxs-lookup"><span data-stu-id="f350d-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="f350d-106">本文包含一個 PHP Manager Web 應用程式擴充功能範例，該範例會透過 Web 介面來啟用 PHP 設定的管理功能。</span><span class="sxs-lookup"><span data-stu-id="f350d-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="f350d-107"><a id="transform"></a>透過 ApplicationHost.config 的進階設定</span><span class="sxs-lookup"><span data-stu-id="f350d-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="f350d-108">hello 應用程式服務平台提供 web 應用程式設定彈性和控制。</span><span class="sxs-lookup"><span data-stu-id="f350d-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="f350d-109">雖然 hello 標準 IIS ApplicationHost.config 組態檔不是適用於 App Service 中直接編輯的 hello 平台支援宣告式的 ApplicationHost.config 轉換模型，依據 XML 文件轉換 (XDT)。</span><span class="sxs-lookup"><span data-stu-id="f350d-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="f350d-110">tooleverage 這項轉換功能，您建立內容與 XDT ApplicationHost.xdt 檔案，並放在 hello 中的 hello 網站根目錄 (d:\home\site) 下[Kudu 主控台](https://github.com/projectkudu/kudu/wiki/Kudu-console)。</span><span class="sxs-lookup"><span data-stu-id="f350d-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="f350d-111">您可能需要 toorestart hello Web 應用程式變更 tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="f350d-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="f350d-112">hello 遵循 applicationHost.xdt 範例顯示新的自訂環境變數 tooa tooadd web 使用 PHP 5.4 的應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="f350d-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="f350d-113">使用從下 LogFiles\Transform hello FTP 根目錄中的記錄檔，以轉換狀態和詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f350d-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="f350d-114">如需其他範例，請參閱＜ [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples)＞。</span><span class="sxs-lookup"><span data-stu-id="f350d-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="f350d-115">**注意**</span><span class="sxs-lookup"><span data-stu-id="f350d-115">**Note**</span></span><br />
<span data-ttu-id="f350d-116">Hello 之下的模組清單中的項目`system.webServer`無法移除或重新排列，但可能會有新增 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="f350d-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="f350d-117"><a id="extend"></a> 擴充 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f350d-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="f350d-118"><a id="overview"></a> 私人 Web 應用程式擴充功能的概觀</span><span class="sxs-lookup"><span data-stu-id="f350d-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="f350d-119">App Service 支援使用 Web 應用程式擴充功能做為系統管理動作的擴充點。</span><span class="sxs-lookup"><span data-stu-id="f350d-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="f350d-120">事實上，有些 App Service 平台功能已當作預先安裝的擴充功能來實作。</span><span class="sxs-lookup"><span data-stu-id="f350d-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="f350d-121">時無法修改 hello 預先安裝的平台擴充程式，您可以建立及設定私人延伸您自己的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f350d-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="f350d-122">這項功能也會依賴 XDT 宣告。</span><span class="sxs-lookup"><span data-stu-id="f350d-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="f350d-123">hello 下列 hello 建立私用的 web 應用程式擴充功能的重要步驟︰</span><span class="sxs-lookup"><span data-stu-id="f350d-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="f350d-124">Web 應用程式擴充功能的「內容」 ：建立任何 App Service 所支援的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f350d-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="f350d-125">Web 應用程式擴充功能的「宣告」 ：建立 ApplicationHost.xdt 檔案</span><span class="sxs-lookup"><span data-stu-id="f350d-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="f350d-126">Web 應用程式擴充功能**部署**: hello SiteExtensions 下的資料夾中放置內容`root`</span><span class="sxs-lookup"><span data-stu-id="f350d-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="f350d-127">內部連結 hello web 應用程式應該指向 hello ApplicationHost.xdt 檔中指定的 tooa 路徑相對 toohello 應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="f350d-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="f350d-128">任何變更 toohello ApplicationHost.xdt 檔案需要 web 應用程式回收。</span><span class="sxs-lookup"><span data-stu-id="f350d-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="f350d-129">**注意**：在 [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions)可取得這些主要元素的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="f350d-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="f350d-130">詳細的範例是包含的 tooillustrate hello 步驟為建立和啟用私用的 web 應用程式擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f350d-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="f350d-131">hello hello PHP Manager 範例如下所示，可以從網站下載的原始碼[https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager)。</span><span class="sxs-lookup"><span data-stu-id="f350d-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="f350d-132"><a id="SiteSample"></a> Web 應用程式擴充功能範例：PHP Manager</span><span class="sxs-lookup"><span data-stu-id="f350d-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="f350d-133">PHP Manager 是 web 應用程式擴充功能，可讓 web 應用程式系統管理員 tooeasily 檢視，並設定其使用 web 介面，而不直接讓 toomodify PHP.ini 檔案的 PHP 設定。</span><span class="sxs-lookup"><span data-stu-id="f350d-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="f350d-134">適用於 PHP 的常見組態檔包括 hello php.ini 檔案位於程式檔案和 hello。 user.ini 檔案位於您 web 應用程式的 hello 根資料夾中。</span><span class="sxs-lookup"><span data-stu-id="f350d-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="f350d-135">Hello PHP Manager 擴充功能因為 hello php.ini 檔案不能直接編輯 hello 應用程式服務平台上，使用 hello。 user.ini 檔案 tooapply 設定變更。</span><span class="sxs-lookup"><span data-stu-id="f350d-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="f350d-136"><a id="PHPwebapp"></a>hello PHP 管理員 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f350d-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="f350d-137">hello 下面是 hello PHP Manager 部署的 hello 首頁：</span><span class="sxs-lookup"><span data-stu-id="f350d-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="f350d-139">如您所見，web 應用程式擴充功能是一樣的一般 web 應用程式，但額外 ApplicationHost.xdt 檔案放在 hello hello （更多詳細 hello ApplicationHost.xdt 檔案使用，而且這個 hello 下一節中的 web 應用程式的根資料夾文件）。</span><span class="sxs-lookup"><span data-stu-id="f350d-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="f350d-140">使用 hello Visual Studio ASP.NET MVC 4 Web 應用程式範本建立 hello PHP Manager 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f350d-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="f350d-141">hello 從方案總管 中的下列檢視顯示 hello 結構 hello PHP Manager 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="f350d-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="f350d-143">hello 只特殊邏輯所需的檔案 I/O 是 tooindicate hello hello web 應用程式的 wwwroot 目錄所在的位置。</span><span class="sxs-lookup"><span data-stu-id="f350d-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="f350d-144">因為 hello 下列的程式碼範例顯示 hello 環境變數"HOME"指出 hello web 應用程式的根路徑，並可以藉由附加"site\wwwroot"建構 hello wwwroot 路徑：</span><span class="sxs-lookup"><span data-stu-id="f350d-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

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


<span data-ttu-id="f350d-145">您已擁有 hello 目錄路徑之後，您可以使用一般檔案 I/O 作業 tooread 並寫入 toofiles。</span><span class="sxs-lookup"><span data-stu-id="f350d-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="f350d-146">注意： 使用 web 應用程式擴充功能的某一點目前內部連結的 hello 的處理。</span><span class="sxs-lookup"><span data-stu-id="f350d-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="f350d-147">如果您提供絕對路徑 toointernal 連結您的 web 應用程式的 HTML 檔案中有任何連結，您必須確定這些連結會加上您的延伸模組名稱，為您的根。</span><span class="sxs-lookup"><span data-stu-id="f350d-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="f350d-148">這需要處理，因為您的擴充功能的 hello 根現在是"/`[your-extension-name]`/"而不會只是"/"，因此任何內部連結必須跟著更新。</span><span class="sxs-lookup"><span data-stu-id="f350d-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="f350d-149">例如，假設您的程式碼包含連結 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="f350d-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="f350d-150">Web 應用程式擴充功能的一部分 hello 連結時，必須在下列形式的 hello hello 連結：</span><span class="sxs-lookup"><span data-stu-id="f350d-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="f350d-151">您可以使用相對路徑或 web 應用程式中使用 hello hello 的 ASP.NET 應用程式的案例僅解決這項需求`@Html.ActionLink`方法會為您建立 hello 適當的連結。</span><span class="sxs-lookup"><span data-stu-id="f350d-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="f350d-152"><a id="XDT"></a>hello applicationHost.xdt 檔案</span><span class="sxs-lookup"><span data-stu-id="f350d-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="f350d-153">您的 web 應用程式擴充功能的 hello 程式碼會進入下 %HOME%\SiteExtensions\[您的延伸模組名稱]。</span><span class="sxs-lookup"><span data-stu-id="f350d-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="f350d-154">我們會呼叫這個 hello 延伸模組的根。</span><span class="sxs-lookup"><span data-stu-id="f350d-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="f350d-155">tooregister hello applicationHost.config 檔案與您 web 應用程式擴充功能，您需要 tooplace 名 ApplicationHost.xdt hello 延伸根目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f350d-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="f350d-156">hello hello ApplicationHost.xdt 檔案內容應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="f350d-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

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

<span data-ttu-id="f350d-157">您選取做為延伸名稱的 hello 名稱必須包含名稱相同的 hello 做為您延伸模組的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="f350d-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="f350d-158">這是加入新的應用程式路徑 toohello hello 效果`system.applicationHost`hello SCM 網站下的網站清單。</span><span class="sxs-lookup"><span data-stu-id="f350d-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="f350d-159">hello SCM 站台是站台管理端點，具有特定存取認證。</span><span class="sxs-lookup"><span data-stu-id="f350d-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="f350d-160">它有 hello URL `https://[your-site-name].scm.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="f350d-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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

### <span data-ttu-id="f350d-161"><a id="deploy"></a> Web 應用程式擴充功能部署</span><span class="sxs-lookup"><span data-stu-id="f350d-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="f350d-162">tooinstall 您 web 應用程式擴充功能，您可以使用 FTP toocopy 您 web 應用程式 toohello 所有 hello 檔案`\SiteExtensions\[your-extension-name]`hello 想 tooinstall hello 延伸模組的 web 應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="f350d-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="f350d-163">為確定 toocopy hello ApplicationHost.xdt 檔案 toothis 位置以及。</span><span class="sxs-lookup"><span data-stu-id="f350d-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="f350d-164">重新啟動 web 應用程式 tooenable hello 擴充。</span><span class="sxs-lookup"><span data-stu-id="f350d-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="f350d-165">您應該能夠 toosee 在您 web 應用程式擴充功能：</span><span class="sxs-lookup"><span data-stu-id="f350d-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="f350d-166">請注意該 hello URL 看起來就像是 hello URL web 應用程式的不同之處在於它會使用 HTTPS，並包含 「.scm"。</span><span class="sxs-lookup"><span data-stu-id="f350d-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="f350d-167">在開發和調查期間為 web 應用程式可能 toodisable 所有私用 （未預先安裝） 延伸模組與 hello 索引鍵加入應用程式設定`WEBSITE_PRIVATE_EXTENSIONS`以及值`0`。</span><span class="sxs-lookup"><span data-stu-id="f350d-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="f350d-168">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="f350d-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f350d-169">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="f350d-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f350d-170">變更的項目</span><span class="sxs-lookup"><span data-stu-id="f350d-170">What's changed</span></span>
* <span data-ttu-id="f350d-171">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f350d-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

