---
title: "在 Azure App Service 中設定 Web 應用程式"
description: "如何在 Azure App Service 中設定 Web 應用程式"
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
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="8ecee-103">在 Azure App Service 中設定 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8ecee-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="8ecee-104">本主題說明如何使用 [Azure 入口網站]設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="8ecee-105">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="8ecee-105">Application settings</span></span>
1. <span data-ttu-id="8ecee-106">在 [Azure 入口網站]中，開啟 Web 應用程式的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8ecee-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="8ecee-107">按一下 [ **所有設定**]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="8ecee-108">按一下 [ **應用程式設定**]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-108">Click **Application Settings**.</span></span>

![應用程式設定][configure01]

<span data-ttu-id="8ecee-110">[ **應用程式設定** ] 刀鋒視窗中的設定會以數種類別來分組。</span><span class="sxs-lookup"><span data-stu-id="8ecee-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="8ecee-111">一般設定</span><span class="sxs-lookup"><span data-stu-id="8ecee-111">General settings</span></span>
<span data-ttu-id="8ecee-112">**Framework 版本**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-112">**Framework versions**.</span></span> <span data-ttu-id="8ecee-113">如果您的應用程式使用下列任何 Framework，請設定下列選項：</span><span class="sxs-lookup"><span data-stu-id="8ecee-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="8ecee-114">**.NET Framework**：設定 .NET framework 版本。</span><span class="sxs-lookup"><span data-stu-id="8ecee-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="8ecee-115">**PHP**：設定 PHP 版本，或設為 [關閉] 以停用 PHP。</span><span class="sxs-lookup"><span data-stu-id="8ecee-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="8ecee-116">**Java**：選取 Java 版本，或設為 [關閉] 以停用 Java。</span><span class="sxs-lookup"><span data-stu-id="8ecee-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="8ecee-117">使用 [ **Web 容器** ] 選項來選擇 Tomcat 或 Jetty 版本。</span><span class="sxs-lookup"><span data-stu-id="8ecee-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="8ecee-118">**Python**：選取 Python 版本，或設為 [關閉] 以停用 Python。</span><span class="sxs-lookup"><span data-stu-id="8ecee-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="8ecee-119">在技術上，針對您的應用程式啟用 Java 就會停用 .NET、PHP 與 Python 選項。</span><span class="sxs-lookup"><span data-stu-id="8ecee-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="8ecee-120"><a name="platform"></a>
**平台**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="8ecee-121">選取 Web 應用程式是否會在 32 位元或 64 位元環境中執行。</span><span class="sxs-lookup"><span data-stu-id="8ecee-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="8ecee-122">64 位元環境需要 [基本] 或 [標準] 模式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="8ecee-123">[免費] 與 [共用] 模式一律於 32 位元環境中執行。</span><span class="sxs-lookup"><span data-stu-id="8ecee-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="8ecee-124">**Web 通訊端**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-124">**Web Sockets**.</span></span> <span data-ttu-id="8ecee-125">設為 [開啟] 以啟用 WebSocket 通訊協定，例如，如果您的 Web 應用程式使用 [ASP.NET SignalR] 或 [socket.io]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="8ecee-126"><a name="alwayson"></a>
**永遠開啟**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="8ecee-127">根據預設，Web 應用程式如果閒置一段時間，就會卸載。</span><span class="sxs-lookup"><span data-stu-id="8ecee-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="8ecee-128">此舉有助於系統保留資源。</span><span class="sxs-lookup"><span data-stu-id="8ecee-128">This lets the system conserve resources.</span></span> <span data-ttu-id="8ecee-129">在 [基本] 或 [標準] 模式中，您可以啟用 [ **永遠開啟** ]，讓應用程式隨時都能載入。</span><span class="sxs-lookup"><span data-stu-id="8ecee-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="8ecee-130">如果您的應用程式會執行連續的 WebJobs，或執行使用 CRON 運算式觸發的 WebJobs，就應該啟用 [一律開啟]，否則 Web 作業可能無法可靠地執行。</span><span class="sxs-lookup"><span data-stu-id="8ecee-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="8ecee-131">**受管理的管線版本**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="8ecee-132">設定 IIS [管線模式]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="8ecee-133">除非您擁有的舊版應用程式需要舊版 IIS，否則請保留 [整合 (預設值)] 的設定。</span><span class="sxs-lookup"><span data-stu-id="8ecee-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="8ecee-134">**自動交換**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-134">**Auto Swap**.</span></span> <span data-ttu-id="8ecee-135">如果您針對部署位置啟用「自動交換」，當您將更新推送到該位置時，App Service 就會將 Web 應用程式自動交換至生產位置。</span><span class="sxs-lookup"><span data-stu-id="8ecee-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="8ecee-136">如需詳細資訊，請參閱 [將 Azure App Service 中的 Web 應用程式部署至預備位置](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="8ecee-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="8ecee-137">Debugging</span><span class="sxs-lookup"><span data-stu-id="8ecee-137">Debugging</span></span>
<span data-ttu-id="8ecee-138">**遠端偵錯**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-138">**Remote Debugging**.</span></span> <span data-ttu-id="8ecee-139">啟用遠端偵錯。</span><span class="sxs-lookup"><span data-stu-id="8ecee-139">Enables remote debugging.</span></span> <span data-ttu-id="8ecee-140">一經啟用，您就可以使用 Visual Studio 中的遠端偵錯工具，直接連接到您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="8ecee-141">遠端偵錯將保持啟用達 48 小時。</span><span class="sxs-lookup"><span data-stu-id="8ecee-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="8ecee-142">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="8ecee-142">App settings</span></span>
<span data-ttu-id="8ecee-143">本區段包含您的 Web 應用程式將在啟動時載入的名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="8ecee-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="8ecee-144">如果是 .NET 應用程式，這些設定就會在執行階段插入 .NET 設定 `AppSettings` ，並覆寫現有的設定。</span><span class="sxs-lookup"><span data-stu-id="8ecee-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="8ecee-145">PHP、Python、Java 和 Node 應用程式可以在執行階段以環境變數的形式存取這些設定。</span><span class="sxs-lookup"><span data-stu-id="8ecee-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="8ecee-146">系統會為每個應用程式設定建立兩個環境變數，一個變數具有由應用程式設定項目指定的名稱，另一個則具有 APPSETTING_ 前置詞。</span><span class="sxs-lookup"><span data-stu-id="8ecee-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="8ecee-147">這兩個變數都包含相同的值。</span><span class="sxs-lookup"><span data-stu-id="8ecee-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="8ecee-148">連接字串</span><span class="sxs-lookup"><span data-stu-id="8ecee-148">Connection strings</span></span>
<span data-ttu-id="8ecee-149">連結資源的連接字串。</span><span class="sxs-lookup"><span data-stu-id="8ecee-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="8ecee-150">如果是 .NET 應用程式，這些連接字串就會在執行階段插入 .NET 組態 `connectionStrings` 的設定，並覆寫索引鍵相當於所連結資料庫名稱的現有項目。</span><span class="sxs-lookup"><span data-stu-id="8ecee-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="8ecee-151">如果是 PHP、Python、Java 及 Node 應用程式，您可以在執行階段將這些設定視為環境變數使用，並加上連線類型前置詞。</span><span class="sxs-lookup"><span data-stu-id="8ecee-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="8ecee-152">環境變數首碼如以下所示：</span><span class="sxs-lookup"><span data-stu-id="8ecee-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="8ecee-153">SQL Server： `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="8ecee-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="8ecee-154">MySQL： `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="8ecee-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="8ecee-155">SQL Database： `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="8ecee-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="8ecee-156">自訂：`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="8ecee-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="8ecee-157">例如，如果 MySql 連接字串命名為 `connectionstring1`，則可透過環境變數 `MYSQLCONNSTR_connectionString1` 加以存取。</span><span class="sxs-lookup"><span data-stu-id="8ecee-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="8ecee-158">預設文件</span><span class="sxs-lookup"><span data-stu-id="8ecee-158">Default documents</span></span>
<span data-ttu-id="8ecee-159">預設文件是顯示於網站根 URL 上的網頁。</span><span class="sxs-lookup"><span data-stu-id="8ecee-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="8ecee-160">系統會使用清單中第一個相符的檔案。</span><span class="sxs-lookup"><span data-stu-id="8ecee-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="8ecee-161">Web 應用程式可能會使用根據 URL 路由傳送的模組，而非處理靜態內容，若是如此，就不會有這類預設文件。</span><span class="sxs-lookup"><span data-stu-id="8ecee-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="8ecee-162">處理常式對應</span><span class="sxs-lookup"><span data-stu-id="8ecee-162">Handler mappings</span></span>
<span data-ttu-id="8ecee-163">使用此區域可新增自訂指令碼處理器，以處理特定副檔名的要求。</span><span class="sxs-lookup"><span data-stu-id="8ecee-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="8ecee-164">**副檔名**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-164">**Extension**.</span></span> <span data-ttu-id="8ecee-165">要處理的副檔名，例如 *.php 或 handler.fcgi。</span><span class="sxs-lookup"><span data-stu-id="8ecee-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="8ecee-166">**指令碼處理器路徑**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-166">**Script Processor Path**.</span></span> <span data-ttu-id="8ecee-167">指令碼處理器的絕對路徑。</span><span class="sxs-lookup"><span data-stu-id="8ecee-167">The absolute path of the script processor.</span></span> <span data-ttu-id="8ecee-168">符合該副檔名的檔案要求，將由指令碼處理器來處理。</span><span class="sxs-lookup"><span data-stu-id="8ecee-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="8ecee-169">使用路徑 `D:\home\site\wwwroot` 以指出應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="8ecee-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="8ecee-170">**其他引數**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-170">**Additional Arguments**.</span></span> <span data-ttu-id="8ecee-171">指令碼處理器選用的命令列引數</span><span class="sxs-lookup"><span data-stu-id="8ecee-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="8ecee-172">虛擬應用程式與目錄</span><span class="sxs-lookup"><span data-stu-id="8ecee-172">Virtual applications and directories</span></span>
<span data-ttu-id="8ecee-173">若要設定虛擬應用程式與目錄，請指定個別虛擬目錄及其相對於網站根目錄的對應實體路徑。</span><span class="sxs-lookup"><span data-stu-id="8ecee-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="8ecee-174">或者，您可以選取 [ **應用程式** ] 核取方塊，勾選虛擬目錄做為應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="8ecee-175">啟用診斷記錄</span><span class="sxs-lookup"><span data-stu-id="8ecee-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="8ecee-176">啟用診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="8ecee-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="8ecee-177">在 Web 應用程式的刀鋒視窗中，按一下 [ **所有設定**]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="8ecee-178">按一下 [ **診斷記錄**]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="8ecee-179">從支援記錄功能的 Web 應用程式寫入診斷記錄的選項：</span><span class="sxs-lookup"><span data-stu-id="8ecee-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="8ecee-180">**應用程式記錄**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-180">**Application Logging**.</span></span> <span data-ttu-id="8ecee-181">將應用程式記錄寫入檔案系統。</span><span class="sxs-lookup"><span data-stu-id="8ecee-181">Writes application logs to the file system.</span></span> <span data-ttu-id="8ecee-182">記錄功能會持續運作 12 小時。</span><span class="sxs-lookup"><span data-stu-id="8ecee-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="8ecee-183">**層級**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-183">**Level**.</span></span> <span data-ttu-id="8ecee-184">應用程式記錄功能一經啟用，此選項便會指定要記錄的資訊數量 (錯誤、警告、資訊或詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="8ecee-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="8ecee-185">**Web 伺服器記錄**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-185">**Web server logging**.</span></span> <span data-ttu-id="8ecee-186">記錄會儲存為 W3C 延伸的記錄檔格式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="8ecee-187">**詳細的錯誤訊息**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-187">**Detailed error messages**.</span></span> <span data-ttu-id="8ecee-188">將詳細的錯誤訊息儲存為 .htm 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ecee-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="8ecee-189">檔案會儲存在 /LogFiles/DetailedErrors 下方。</span><span class="sxs-lookup"><span data-stu-id="8ecee-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="8ecee-190">**失敗要求的追蹤**。</span><span class="sxs-lookup"><span data-stu-id="8ecee-190">**Failed request tracing**.</span></span> <span data-ttu-id="8ecee-191">將失敗的要求記錄於 XML 檔案中。</span><span class="sxs-lookup"><span data-stu-id="8ecee-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="8ecee-192">檔案會儲存在 /LogFiles/W3SVC*xxx*之下，其中 xxx 是唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="8ecee-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="8ecee-193">此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ecee-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="8ecee-194">請務必下載 XSL 檔案，因為 XSL 檔案可提供格式化和篩選 XML 檔案內容的功能。</span><span class="sxs-lookup"><span data-stu-id="8ecee-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="8ecee-195">若要檢視記錄檔，您必須建立 FTP 認證，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8ecee-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="8ecee-196">在 Web 應用程式的刀鋒視窗中，按一下 [ **所有設定**]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="8ecee-197">按一下 [ **部署認證**]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="8ecee-198">請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8ecee-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="8ecee-199">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8ecee-199">Click **Save**.</span></span>

![設定部署認證][configure03]

<span data-ttu-id="8ecee-201">完整的 FTP 使用者名稱為 「app\username」，其中 *app* 為您 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="8ecee-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="8ecee-202">username 則列於 Web 應用程式刀鋒視窗的 **Essentials**部分。</span><span class="sxs-lookup"><span data-stu-id="8ecee-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![FTP 部署認證][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="8ecee-204">其他配置作業</span><span class="sxs-lookup"><span data-stu-id="8ecee-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="8ecee-205">SSL</span><span class="sxs-lookup"><span data-stu-id="8ecee-205">SSL</span></span>
<span data-ttu-id="8ecee-206">在 [基本] 或 [標準] 模式中，您可以上傳自訂網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="8ecee-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="8ecee-207">如需詳細資訊，請參閱 [為 Web 應用程式啟用 HTTPS]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="8ecee-208">若要檢視您上傳的憑證，依序按一下  **所有設定** > **自訂網域和 SSL**設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="8ecee-209">網域名稱</span><span class="sxs-lookup"><span data-stu-id="8ecee-209">Domain names</span></span>
<span data-ttu-id="8ecee-210">新增 Web 應用程式的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="8ecee-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="8ecee-211">如需詳細資訊，請參閱 [為 Azure App Service 中的 Web 應用程式設定自訂網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="8ecee-212">若要檢視您的網域名稱，依序按一下  **所有設定** > **自訂網域和 SSL**設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="8ecee-213">部署</span><span class="sxs-lookup"><span data-stu-id="8ecee-213">Deployments</span></span>
* <span data-ttu-id="8ecee-214">設定連續部署。</span><span class="sxs-lookup"><span data-stu-id="8ecee-214">Set up continuous deployment.</span></span> <span data-ttu-id="8ecee-215">請參閱 [在 Azure App Service 中使用 Git 來部署 Web Apps](web-sites-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="8ecee-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="8ecee-216">部署位置。</span><span class="sxs-lookup"><span data-stu-id="8ecee-216">Deployment slots.</span></span> <span data-ttu-id="8ecee-217">請參閱 [將 Azure App Service 中的 Web Apps 部署至預備環境]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="8ecee-218">若要檢視您的部署位置，依序按一下  **所有設定** > **部署位置**設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="8ecee-219">監視</span><span class="sxs-lookup"><span data-stu-id="8ecee-219">Monitoring</span></span>
<span data-ttu-id="8ecee-220">在 [基本] 或 [標準] 模式中，您可以測試 HTTP 或 HTTPS 端點的可用性，最多可測試三個分散的地理位置。</span><span class="sxs-lookup"><span data-stu-id="8ecee-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="8ecee-221">如果 HTTP 回應碼為錯誤 (4xx 或 5xx)，或是當回應時間超過 30 秒時，監視測試即告失敗。</span><span class="sxs-lookup"><span data-stu-id="8ecee-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="8ecee-222">如果所有指定位置上的端點監視測試全都成功，表示該端點可用。</span><span class="sxs-lookup"><span data-stu-id="8ecee-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="8ecee-223">如需詳細資訊，請參閱 [如何監視 Web 端點狀態]。</span><span class="sxs-lookup"><span data-stu-id="8ecee-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="8ecee-224">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service]，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ecee-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8ecee-225">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="8ecee-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8ecee-226">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ecee-226">Next steps</span></span>
* <span data-ttu-id="8ecee-227">[在 Azure App Service 中設定自訂網域名稱]</span><span class="sxs-lookup"><span data-stu-id="8ecee-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="8ecee-228">[針對 Azure App Service 中的 App 啟用 HTTPS]</span><span class="sxs-lookup"><span data-stu-id="8ecee-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="8ecee-229">[在 Azure App Service 中調整 Web 應用程式規模]</span><span class="sxs-lookup"><span data-stu-id="8ecee-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="8ecee-230">[在 Azure App Service 中監視 Web 應用程式的基本概念]</span><span class="sxs-lookup"><span data-stu-id="8ecee-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="8ecee-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="8ecee-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="8ecee-232">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="8ecee-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="8ecee-233">[在 Azure App Service 中設定自訂網域名稱]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="8ecee-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="8ecee-234">[將 Azure App Service 中的 Web Apps 部署至預備環境]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="8ecee-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="8ecee-235">[針對 Azure App Service 中的 App 啟用 HTTPS]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="8ecee-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="8ecee-236">[如何監視 Web 端點狀態]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="8ecee-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="8ecee-237">[在 Azure App Service 中監視 Web 應用程式的基本概念]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="8ecee-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="8ecee-238">[管線模式]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="8ecee-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="8ecee-239">[在 Azure App Service 中調整 Web 應用程式規模]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="8ecee-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="8ecee-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="8ecee-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="8ecee-241">[試用 App Service]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="8ecee-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
