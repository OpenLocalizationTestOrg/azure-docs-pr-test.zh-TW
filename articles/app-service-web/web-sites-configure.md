---
title: "aaaConfigure Azure App Service 中的 web 應用程式"
description: "如何 tooconfigure Azure 應用程式服務中的 web 應用程式"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="9a962-103">在 Azure App Service 中設定 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9a962-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="9a962-104">本主題說明如何使用 web 應用程式的 tooconfigure hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="9a962-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="9a962-105">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="9a962-105">Application settings</span></span>
1. <span data-ttu-id="9a962-106">在 hello [Azure 入口網站]，開啟 hello web 應用程式的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9a962-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="9a962-107">按一下 [ **所有設定**]。</span><span class="sxs-lookup"><span data-stu-id="9a962-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="9a962-108">按一下 [ **應用程式設定**]。</span><span class="sxs-lookup"><span data-stu-id="9a962-108">Click **Application Settings**.</span></span>

![應用程式設定][configure01]

<span data-ttu-id="9a962-110">hello**應用程式設定**分頁有數種類別在下設為群組的設定。</span><span class="sxs-lookup"><span data-stu-id="9a962-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="9a962-111">一般設定</span><span class="sxs-lookup"><span data-stu-id="9a962-111">General settings</span></span>
<span data-ttu-id="9a962-112">**Framework 版本**。</span><span class="sxs-lookup"><span data-stu-id="9a962-112">**Framework versions**.</span></span> <span data-ttu-id="9a962-113">如果您的應用程式使用下列任何 Framework，請設定下列選項：</span><span class="sxs-lookup"><span data-stu-id="9a962-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="9a962-114">**.NET framework**: Set hello.NET framework 版本。</span><span class="sxs-lookup"><span data-stu-id="9a962-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="9a962-115">**PHP**: Set hello PHP 版本，或**OFF** toodisable PHP。</span><span class="sxs-lookup"><span data-stu-id="9a962-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="9a962-116">**Java**： 選取 hello Java 版本或**OFF** toodisable Java。</span><span class="sxs-lookup"><span data-stu-id="9a962-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="9a962-117">使用 hello**網頁容器**選項 toochoose Tomcat 或 Jetty 版本之間。</span><span class="sxs-lookup"><span data-stu-id="9a962-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="9a962-118">**Python**： 選取 hello Python 版本，或**OFF** toodisable Python。</span><span class="sxs-lookup"><span data-stu-id="9a962-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="9a962-119">若是技術原因，針對您的應用程式啟用 Java，將停用 hello.NET、 PHP 以及 Python 選項。</span><span class="sxs-lookup"><span data-stu-id="9a962-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="9a962-120"><a name="platform"></a>
**平台**。</span><span class="sxs-lookup"><span data-stu-id="9a962-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="9a962-121">選取 Web 應用程式是否會在 32 位元或 64 位元環境中執行。</span><span class="sxs-lookup"><span data-stu-id="9a962-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="9a962-122">hello 64 位元環境需要使用基本或標準模式。</span><span class="sxs-lookup"><span data-stu-id="9a962-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="9a962-123">[免費] 與 [共用] 模式一律於 32 位元環境中執行。</span><span class="sxs-lookup"><span data-stu-id="9a962-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="9a962-124">**Web 通訊端**。</span><span class="sxs-lookup"><span data-stu-id="9a962-124">**Web Sockets**.</span></span> <span data-ttu-id="9a962-125">設定**ON** tooenable hello WebSocket 通訊協定; 例如，如果您的 web 應用程式使用[ASP.NET SignalR]或[socket.io]。</span><span class="sxs-lookup"><span data-stu-id="9a962-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="9a962-126"><a name="alwayson"></a>
**永遠開啟**。</span><span class="sxs-lookup"><span data-stu-id="9a962-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="9a962-127">根據預設，Web 應用程式如果閒置一段時間，就會卸載。</span><span class="sxs-lookup"><span data-stu-id="9a962-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="9a962-128">這可讓 hello 系統節省資源。</span><span class="sxs-lookup"><span data-stu-id="9a962-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="9a962-129">在基本或標準模式中，您可以啟用**Always On** tookeep hello 應用程式載入所有 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="9a962-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="9a962-130">如果您的應用程式執行連續 web 工作或執行 WebJobs 觸發使用 CRON 運算式，您應該啟用**Always On**，或 hello web 工作可能無法可靠地執行。</span><span class="sxs-lookup"><span data-stu-id="9a962-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="9a962-131">**受管理的管線版本**。</span><span class="sxs-lookup"><span data-stu-id="9a962-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="9a962-132">設定 hello IIS[管線模式]。</span><span class="sxs-lookup"><span data-stu-id="9a962-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="9a962-133">保留此設定 tooIntegrated （hello 預設值），除非您有舊版的應用程式需要較舊版本的 IIS。</span><span class="sxs-lookup"><span data-stu-id="9a962-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="9a962-134">**自動交換**。</span><span class="sxs-lookup"><span data-stu-id="9a962-134">**Auto Swap**.</span></span> <span data-ttu-id="9a962-135">如果您啟用自動交換部署位置時，應用程式服務將會自動交換 hello web 應用程式運行推送更新 toothat 位置時。</span><span class="sxs-lookup"><span data-stu-id="9a962-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="9a962-136">如需詳細資訊，請參閱[部署在 Azure App Service web 應用程式的 toostaging 位置](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="9a962-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="9a962-137">Debugging</span><span class="sxs-lookup"><span data-stu-id="9a962-137">Debugging</span></span>
<span data-ttu-id="9a962-138">**遠端偵錯**。</span><span class="sxs-lookup"><span data-stu-id="9a962-138">**Remote Debugging**.</span></span> <span data-ttu-id="9a962-139">啟用遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="9a962-139">Enables remote debugging.</span></span> <span data-ttu-id="9a962-140">啟用時，您可以使用 hello 遠端偵錯工具，在 Visual Studio tooconnect 直接 tooyour web 應用程式即可。</span><span class="sxs-lookup"><span data-stu-id="9a962-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="9a962-141">遠端偵錯將保持啟用達 48 小時。</span><span class="sxs-lookup"><span data-stu-id="9a962-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="9a962-142">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="9a962-142">App settings</span></span>
<span data-ttu-id="9a962-143">本區段包含您的 Web 應用程式將在啟動時載入的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="9a962-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="9a962-144">如果是 .NET 應用程式，這些設定就會在執行階段插入 .NET 設定 `AppSettings` ，並覆寫現有的設定。</span><span class="sxs-lookup"><span data-stu-id="9a962-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="9a962-145">PHP、Python、Java 和 Node 應用程式可以在執行階段以環境變數的形式存取這些設定。</span><span class="sxs-lookup"><span data-stu-id="9a962-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="9a962-146">每個應用程式設定，會建立兩個環境變數;其中一個 hello hello 應用程式設定項目，和另一個具有 APPSETTING_ 前置詞所指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="9a962-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="9a962-147">同時包含 hello 相同的值。</span><span class="sxs-lookup"><span data-stu-id="9a962-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="9a962-148">連接字串</span><span class="sxs-lookup"><span data-stu-id="9a962-148">Connection strings</span></span>
<span data-ttu-id="9a962-149">連結資源的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9a962-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="9a962-150">對於.NET 應用程式，這些連接字串會插入.NET 組態`connectionStrings`覆寫現有 hello 索引鍵相同的項目在執行階段，設定 hello 連結的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="9a962-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="9a962-151">PHP、 Python、 Java 和節點的應用程式，會視為環境變數，在執行階段，加上 hello 連接類型使用這些設定。</span><span class="sxs-lookup"><span data-stu-id="9a962-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="9a962-152">如下所示為 hello 環境變數的前置詞：</span><span class="sxs-lookup"><span data-stu-id="9a962-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="9a962-153">SQL Server： `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="9a962-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="9a962-154">MySQL： `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="9a962-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="9a962-155">SQL Database： `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="9a962-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="9a962-156">自訂：`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="9a962-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="9a962-157">例如，如果已在名為 MySql 連接字串`connectionstring1`，它會透過 hello 環境變數存取`MYSQLCONNSTR_connectionString1`。</span><span class="sxs-lookup"><span data-stu-id="9a962-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="9a962-158">預設文件</span><span class="sxs-lookup"><span data-stu-id="9a962-158">Default documents</span></span>
<span data-ttu-id="9a962-159">hello 預設文件是 hello web 網頁上顯示的 hello 根 URL 的網站。</span><span class="sxs-lookup"><span data-stu-id="9a962-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="9a962-160">會使用 hello 第一個相符的檔案 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="9a962-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="9a962-161">Web 應用程式可能會使用根據 URL 路由傳送的模組，而非處理靜態內容，若是如此，就不會有這類預設文件。</span><span class="sxs-lookup"><span data-stu-id="9a962-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="9a962-162">處理常式對應</span><span class="sxs-lookup"><span data-stu-id="9a962-162">Handler mappings</span></span>
<span data-ttu-id="9a962-163">使用此區域 tooadd 自訂指令碼處理器 toohandle 要求特定副檔名。</span><span class="sxs-lookup"><span data-stu-id="9a962-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="9a962-164">**副檔名**。</span><span class="sxs-lookup"><span data-stu-id="9a962-164">**Extension**.</span></span> <span data-ttu-id="9a962-165">hello 檔案副檔名 toobe 處理，例如 *.php 或 handler.fcgi。</span><span class="sxs-lookup"><span data-stu-id="9a962-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="9a962-166">**指令碼處理器路徑**。</span><span class="sxs-lookup"><span data-stu-id="9a962-166">**Script Processor Path**.</span></span> <span data-ttu-id="9a962-167">hello 指令碼處理器 hello 絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="9a962-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="9a962-168">符合 hello 副檔名的要求 toofiles 會由 hello 指令碼處理器處理。</span><span class="sxs-lookup"><span data-stu-id="9a962-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="9a962-169">使用 hello 路徑`D:\home\site\wwwroot`toorefer tooyour 應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="9a962-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="9a962-170">**其他引數**。</span><span class="sxs-lookup"><span data-stu-id="9a962-170">**Additional Arguments**.</span></span> <span data-ttu-id="9a962-171">Hello 指令碼處理器的選擇性命令列引數</span><span class="sxs-lookup"><span data-stu-id="9a962-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="9a962-172">虛擬應用程式與目錄</span><span class="sxs-lookup"><span data-stu-id="9a962-172">Virtual applications and directories</span></span>
<span data-ttu-id="9a962-173">tooconfigure 虛擬應用程式和目錄，請指定每個虛擬目錄和其對應的實體路徑相對 toohello 網站根目錄。</span><span class="sxs-lookup"><span data-stu-id="9a962-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="9a962-174">或者，您可以選取 hello**應用程式**核取方塊 toomark 做為應用程式的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="9a962-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="9a962-175">啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9a962-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="9a962-176">tooenable 診斷記錄檔：</span><span class="sxs-lookup"><span data-stu-id="9a962-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="9a962-177">在 hello 刀鋒視窗 web 應用程式中，按一下 **所有設定**。</span><span class="sxs-lookup"><span data-stu-id="9a962-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="9a962-178">按一下 [ **診斷記錄**]。</span><span class="sxs-lookup"><span data-stu-id="9a962-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="9a962-179">從支援記錄功能的 Web 應用程式寫入診斷記錄的選項：</span><span class="sxs-lookup"><span data-stu-id="9a962-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="9a962-180">**應用程式記錄**。</span><span class="sxs-lookup"><span data-stu-id="9a962-180">**Application Logging**.</span></span> <span data-ttu-id="9a962-181">將應用程式記錄檔寫入 toohello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="9a962-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="9a962-182">記錄功能會持續運作 12 小時。</span><span class="sxs-lookup"><span data-stu-id="9a962-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="9a962-183">**層級**。</span><span class="sxs-lookup"><span data-stu-id="9a962-183">**Level**.</span></span> <span data-ttu-id="9a962-184">啟用應用程式記錄時，這個選項會指定 hello 量的資訊，將會錄製 （錯誤、 警告、 資訊或詳細資訊）。</span><span class="sxs-lookup"><span data-stu-id="9a962-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="9a962-185">**Web 伺服器記錄**。</span><span class="sxs-lookup"><span data-stu-id="9a962-185">**Web server logging**.</span></span> <span data-ttu-id="9a962-186">記錄檔會儲存在 hello W3C 擴充的記錄檔格式。</span><span class="sxs-lookup"><span data-stu-id="9a962-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="9a962-187">**詳細的錯誤訊息**。</span><span class="sxs-lookup"><span data-stu-id="9a962-187">**Detailed error messages**.</span></span> <span data-ttu-id="9a962-188">將詳細的錯誤訊息儲存為 .htm 檔案。</span><span class="sxs-lookup"><span data-stu-id="9a962-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="9a962-189">hello 檔案會儲存在 /LogFiles/DetailedErrors 下。</span><span class="sxs-lookup"><span data-stu-id="9a962-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="9a962-190">**失敗要求的追蹤**。</span><span class="sxs-lookup"><span data-stu-id="9a962-190">**Failed request tracing**.</span></span> <span data-ttu-id="9a962-191">記錄檔失敗的要求 tooXML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9a962-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="9a962-192">hello 檔案儲存在底下/LogFiles/W3SVC*xxx*，其中 xxx 是唯一的識別項。</span><span class="sxs-lookup"><span data-stu-id="9a962-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="9a962-193">此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9a962-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="9a962-194">請確定 toodownload hello XSL 檔案，因為它提供用來格式化和篩選的 hello XML 檔案的 hello 內容的功能。</span><span class="sxs-lookup"><span data-stu-id="9a962-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="9a962-195">tooview hello 記錄檔，您必須建立 FTP 認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9a962-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="9a962-196">在 hello 刀鋒視窗 web 應用程式中，按一下 **所有設定**。</span><span class="sxs-lookup"><span data-stu-id="9a962-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="9a962-197">按一下 [ **部署認證**]。</span><span class="sxs-lookup"><span data-stu-id="9a962-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="9a962-198">請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="9a962-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="9a962-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9a962-199">Click **Save**.</span></span>

![設定部署認證][configure03]

<span data-ttu-id="9a962-201">hello 完整 FTP 使用者名稱是"app\username"其中*應用程式*hello 您 web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9a962-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="9a962-202">hello 使用者名稱會列在 hello web 應用程式 刀鋒視窗，在**Essentials**。</span><span class="sxs-lookup"><span data-stu-id="9a962-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![FTP 部署認證][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="9a962-204">其他配置作業</span><span class="sxs-lookup"><span data-stu-id="9a962-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="9a962-205">SSL</span><span class="sxs-lookup"><span data-stu-id="9a962-205">SSL</span></span>
<span data-ttu-id="9a962-206">在 [基本] 或 [標準] 模式中，您可以上傳自訂網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="9a962-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="9a962-207">如需詳細資訊，請參閱 [為 Web 應用程式啟用 HTTPS]。</span><span class="sxs-lookup"><span data-stu-id="9a962-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="9a962-208">您已上傳的憑證，按一下 tooview**所有設定** > **自訂網域及 SSL**。</span><span class="sxs-lookup"><span data-stu-id="9a962-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="9a962-209">網域名稱</span><span class="sxs-lookup"><span data-stu-id="9a962-209">Domain names</span></span>
<span data-ttu-id="9a962-210">新增 Web 應用程式的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="9a962-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="9a962-211">如需詳細資訊，請參閱 [為 Azure App Service 中的 Web 應用程式設定自訂網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="9a962-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="9a962-212">您的網域名稱，按一下 tooview**所有設定** > **自訂網域及 SSL**。</span><span class="sxs-lookup"><span data-stu-id="9a962-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="9a962-213">部署</span><span class="sxs-lookup"><span data-stu-id="9a962-213">Deployments</span></span>
* <span data-ttu-id="9a962-214">設定連續部署。</span><span class="sxs-lookup"><span data-stu-id="9a962-214">Set up continuous deployment.</span></span> <span data-ttu-id="9a962-215">請參閱[使用 Git toodeploy Azure App Service 中的 Web 應用程式](web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="9a962-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="9a962-216">部署位置。</span><span class="sxs-lookup"><span data-stu-id="9a962-216">Deployment slots.</span></span> <span data-ttu-id="9a962-217">請參閱[Azure App Service 中的 Web 應用程式部署 tooStaging 環境]。</span><span class="sxs-lookup"><span data-stu-id="9a962-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="9a962-218">您的部署位置，按一下 tooview**所有設定** > **部署位置**。</span><span class="sxs-lookup"><span data-stu-id="9a962-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="9a962-219">監視</span><span class="sxs-lookup"><span data-stu-id="9a962-219">Monitoring</span></span>
<span data-ttu-id="9a962-220">在基本或標準模式中，您可以從測試 HTTP 或 HTTPS 端點的 hello 可用性 toothree 地理位置。</span><span class="sxs-lookup"><span data-stu-id="9a962-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="9a962-221">如果 HTTP 回應碼 hello 錯誤 （4xx 或 5xx） 或 hello 回應時間超過 30 秒，則監視測試將會失敗。</span><span class="sxs-lookup"><span data-stu-id="9a962-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="9a962-222">端點視為可用 hello 監視測試皆成功從所有 hello 指定位置。</span><span class="sxs-lookup"><span data-stu-id="9a962-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="9a962-223">如需詳細資訊，請參閱 [如何監視 Web 端點狀態]。</span><span class="sxs-lookup"><span data-stu-id="9a962-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="9a962-224">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務]，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="9a962-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9a962-225">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="9a962-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9a962-226">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a962-226">Next steps</span></span>
* <span data-ttu-id="9a962-227">[在 Azure App Service 中設定自訂網域名稱]</span><span class="sxs-lookup"><span data-stu-id="9a962-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="9a962-228">[針對 Azure App Service 中的 App 啟用 HTTPS]</span><span class="sxs-lookup"><span data-stu-id="9a962-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="9a962-229">[在 Azure App Service 中調整 Web 應用程式規模]</span><span class="sxs-lookup"><span data-stu-id="9a962-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="9a962-230">[在 Azure App Service 中監視 Web 應用程式的基本概念]</span><span class="sxs-lookup"><span data-stu-id="9a962-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure 入口網站]: https://portal.azure.com/
[在 Azure App Service 中設定自訂網域名稱]: ./app-service-web-tutorial-custom-domain.md
[Azure App Service 中的 Web 應用程式部署 tooStaging 環境]: ./web-sites-staged-publishing.md
[針對 Azure App Service 中的 App 啟用 HTTPS]: ./app-service-web-tutorial-custom-ssl.md
[如何監視 Web 端點狀態]: http://go.microsoft.com/fwLink/?LinkID=279906
[在 Azure App Service 中監視 Web 應用程式的基本概念]: ./web-sites-monitor.md
[管線模式]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[在 Azure App Service 中調整 Web 應用程式規模]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[再試一次應用程式服務]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
