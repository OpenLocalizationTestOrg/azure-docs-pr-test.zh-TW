---
title: "aaaOpen 原始碼技術常見問題集 azure web 應用程式 |Microsoft 文件"
description: "收到 hello Web 應用程式功能的 Azure App Service 中的開放原始碼技術的相關常見問題的解答 toofrequently。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="fa895-103">Azure 中的 Web Apps 相關開放原始碼技術常見問題集</span><span class="sxs-lookup"><span data-stu-id="fa895-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="fa895-104">這篇文章有集 (Faq) 解答 toofrequently 相關問題的開放原始碼技術，用於 hello [Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="fa895-105">我的 ClearDB 資料庫已關閉。</span><span class="sxs-lookup"><span data-stu-id="fa895-105">My ClearDB database is down.</span></span> <span data-ttu-id="fa895-106">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="fa895-106">How do I resolve this?</span></span>

<span data-ttu-id="fa895-107">如有資料庫相關的問題，請連絡 [ClearDB 支援](https://www.cleardb.com/developers/help/support) (英文)。</span><span class="sxs-lookup"><span data-stu-id="fa895-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="fa895-108">如需 ClearDB 答案 toocommon 問題，請參閱[ClearDB 常見問題集](https://docs.microsoft.com/azure/store-cleardb-faq/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="fa895-109">為什麼我的 ClearDB 資料庫中沒有顯示 hello 入口網站？</span><span class="sxs-lookup"><span data-stu-id="fa895-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="fa895-110">如果您建立的 ClearDB 資料庫在 hello [Azure 入口網站](http://portal.azure.com/)，hello 資料庫不會出現在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="fa895-111">toowork 解決這個問題，您可以手動連結 toohello web 應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa895-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="fa895-112">同樣地，如果您建立的 ClearDB 資料庫在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，不會看到您的資料庫中 hello [Azure 入口網站](http://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="fa895-113">對於這種情況，目前沒有可行的因應措施。</span><span class="sxs-lookup"><span data-stu-id="fa895-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="fa895-114">如需詳細資訊，請參閱 [ClearDB MySQL 資料庫搭配 Azure App Service 的常見問題集](https://docs.microsoft.com/azure/store-cleardb-faq/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="fa895-115">為什麼我的 ClearDB 資料庫在我的訂用帳戶移轉期間未移轉？</span><span class="sxs-lookup"><span data-stu-id="fa895-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="fa895-116">當跨訂用帳戶執行資源移轉時，適用某些限制。</span><span class="sxs-lookup"><span data-stu-id="fa895-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="fa895-117">ClearDB MySQL 資料庫是第三方服務，因此在 Azure 訂用帳戶移轉期間是不會移轉的。</span><span class="sxs-lookup"><span data-stu-id="fa895-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="fa895-118">如果您未管理 hello 移轉您的 MySQL 資料庫，則在移轉您的 Azure 資源之前，可能無法使用您的 ClearDB MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="fa895-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="fa895-119">tooavoid 這，首先，手動將移轉您的 ClearDB 資料庫，然後再移轉 hello web 應用程式的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa895-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="fa895-120">如需詳細資訊，請參閱 [ClearDB MySQL 資料庫搭配 Azure App Service 的常見問題集](https://docs.microsoft.com/azure/store-cleardb-faq/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="fa895-121">如何開啟 PHP 記錄 tootroubleshoot PHP 問題？</span><span class="sxs-lookup"><span data-stu-id="fa895-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="fa895-122">tooturn PHP 記錄：</span><span class="sxs-lookup"><span data-stu-id="fa895-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="fa895-123">登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="fa895-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="fa895-124">在 hello 上方功能表中，選取 **偵錯主控台** > **CMD**。</span><span class="sxs-lookup"><span data-stu-id="fa895-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="fa895-125">選取 hello**網站**資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa895-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="fa895-126">選取 hello **wwwroot**資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa895-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="fa895-127">選取 hello  **+** 圖示，然後選取**新檔案**。</span><span class="sxs-lookup"><span data-stu-id="fa895-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="fa895-128">設定 hello 檔案名稱得**。 user.ini**。</span><span class="sxs-lookup"><span data-stu-id="fa895-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="fa895-129">選取 hello 鉛筆圖示旁太**。 user.ini**。</span><span class="sxs-lookup"><span data-stu-id="fa895-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="fa895-130">在 hello 檔案中，加入下列程式碼：`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="fa895-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="fa895-131">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="fa895-131">Select **Save**.</span></span>
10. <span data-ttu-id="fa895-132">選取 hello 鉛筆圖示旁太**wp config.php**。</span><span class="sxs-lookup"><span data-stu-id="fa895-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="fa895-133">變更下列程式碼的 hello 文字 toohello:</span><span class="sxs-lookup"><span data-stu-id="fa895-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="fa895-134">在 hello Azure 入口網站，在 hello web 應用程式功能表中，重新啟動您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa895-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="fa895-135">如需詳細資訊，請參閱[啟用 WordPress 錯誤記錄檔](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="fa895-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="fa895-136">如何在 App Service 內裝載的應用程式中記錄 Python 應用程式錯誤？</span><span class="sxs-lookup"><span data-stu-id="fa895-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="fa895-137">toocapture Python 應用程式錯誤：</span><span class="sxs-lookup"><span data-stu-id="fa895-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="fa895-138">在 hello Azure 入口網站，在您 web 應用程式中，選取 **設定**。</span><span class="sxs-lookup"><span data-stu-id="fa895-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="fa895-139">在 hello**設定**索引標籤上，選取**應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="fa895-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="fa895-140">在下**應用程式設定**，輸入下列索引鍵/值組的 hello:</span><span class="sxs-lookup"><span data-stu-id="fa895-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="fa895-141">索引鍵：WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="fa895-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="fa895-142">值：D:\home\site\wwwroot\logs.txt (輸入您選擇的檔案名稱)</span><span class="sxs-lookup"><span data-stu-id="fa895-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="fa895-143">您現在應該會看到 hello wwwroot 資料夾中的 hello logs.txt 檔案中的錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa895-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="fa895-144">如何變更 hello 版的 hello App Service 中裝載 Node.js 應用程式？</span><span class="sxs-lookup"><span data-stu-id="fa895-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="fa895-145">toochange hello 版的 hello Node.js 應用程式，您可以使用其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="fa895-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="fa895-146">在 hello Azure 入口網站，使用**應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="fa895-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="fa895-147">在 hello Azure 入口網站，移 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa895-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="fa895-148">在 hello**設定**刀鋒視窗中，選取**應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="fa895-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="fa895-149">在**應用程式設定**、 您可以包含 WEBSITE_NODE_DEFAULT_VERSION hello 索引鍵，以及 hello 版本的 Node.js 要做為 hello 值。</span><span class="sxs-lookup"><span data-stu-id="fa895-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="fa895-150">移 tooyour [Kudu 主控台](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="fa895-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="fa895-151">toocheck hello Node.js 版本中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fa895-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="fa895-152">修改 hello iisnode.yml 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa895-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="fa895-153">變更 hello iisnode.yml 檔案中的 hello Node.js 版本只會設定 hello 執行階段環境的 iisnode 使用。</span><span class="sxs-lookup"><span data-stu-id="fa895-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="fa895-154">Kudu cmd 和其他人仍使用設定中的 hello Node.js 版本**應用程式設定**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fa895-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="fa895-155">tooset hello iisnode.yml 手動建立 iisnode.yml 檔案，您的應用程式根資料夾中。</span><span class="sxs-lookup"><span data-stu-id="fa895-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="fa895-156">在 hello 檔案中，包括以下各 hello:</span><span class="sxs-lookup"><span data-stu-id="fa895-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="fa895-157">設定原始檔控制部署期間使用 package.json 的 hello iisnode.yml 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa895-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="fa895-158">hello Azure 的原始檔控制部署程序牽涉到 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fa895-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="fa895-159">移動內容 toohello Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fa895-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="fa895-160">如果沒有則 （deploy.cmd、.deployment 檔案），hello web 應用程式根資料夾中，會建立預設部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="fa895-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="fa895-161">執行部署指令碼，並建立這 iisnode.yml 檔案若提到 hello package.json 檔案中的 hello Node.js 版本 > 引擎`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="fa895-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="fa895-162">hello iisnode.yml 檔案具有下列的程式碼行 hello:</span><span class="sxs-lookup"><span data-stu-id="fa895-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="fa895-163">我在我的 WordPress 應用程式裝載在 App Service 中看到 hello 訊息 「 建立資料庫連線錯誤 」。</span><span class="sxs-lookup"><span data-stu-id="fa895-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="fa895-164">我該如何進行疑難排解？</span><span class="sxs-lookup"><span data-stu-id="fa895-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="fa895-165">如果您看到此錯誤在您的 Azure WordPress 應用程式、 tooenable php_errors.log 和 debug.log，完成 hello 步驟詳細說明[啟用 WordPress 錯誤記錄檔](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="fa895-166">Hello 記錄啟用時，重現 hello 錯誤，然後檢查 hello 記錄 toosee 如果即將用盡連線：</span><span class="sxs-lookup"><span data-stu-id="fa895-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="fa895-167">如果您看到此錯誤在 debug.log 或 php_errors.log 檔案時，您的應用程式超出 hello 連接數目。</span><span class="sxs-lookup"><span data-stu-id="fa895-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="fa895-168">如果您正在裝載 ClearDB 上，確認 hello 中可用的連線數目您[服務計劃](https://www.cleardb.com/pricing.view)。</span><span class="sxs-lookup"><span data-stu-id="fa895-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="fa895-169">如何對於 App Service 中裝載的 Node.js 應用程式進行偵錯？</span><span class="sxs-lookup"><span data-stu-id="fa895-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="fa895-170">移 tooyour [Kudu 主控台](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole)。</span><span class="sxs-lookup"><span data-stu-id="fa895-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="fa895-171">移 tooyour 應用程式記錄檔資料夾 (D:\home\LogFiles\Application)。</span><span class="sxs-lookup"><span data-stu-id="fa895-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="fa895-172">Hello logging_errors.txt 檔案中，檢查的內容。</span><span class="sxs-lookup"><span data-stu-id="fa895-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="fa895-173">如何在 App Service Web 應用程式或 API 應用程式中安裝原生 Python 模組？</span><span class="sxs-lookup"><span data-stu-id="fa895-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="fa895-174">某些封裝可能不會使用 Azure 中的 pip 進行安裝。</span><span class="sxs-lookup"><span data-stu-id="fa895-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="fa895-175">hello 封裝可能無法在 hello Python 封裝索引，或可能必須使用編譯器 （編譯器不 hello hello web 應用程式執行中應用程式服務的電腦上）。</span><span class="sxs-lookup"><span data-stu-id="fa895-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="fa895-176">如需在 App Service Web 應用程式及 API 應用程式中安裝原生模組的相關資訊，請參閱[在 App Service 中安裝 Python 模組](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="fa895-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="fa895-177">如何使用 Git 和 hello 的新版本，Python 的部署如 Django 應用程式 tooApp 服務？</span><span class="sxs-lookup"><span data-stu-id="fa895-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="fa895-178">如需安裝如 Django 資訊，請參閱[部署如 Django 應用程式 tooApp 服務](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="fa895-179">Hello Tomcat 記錄檔是否位於哪裡？</span><span class="sxs-lookup"><span data-stu-id="fa895-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="fa895-180">對於 Azure Marketplace 和自訂部署：</span><span class="sxs-lookup"><span data-stu-id="fa895-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="fa895-181">資料夾位置：D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="fa895-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="fa895-182">感興趣區域：</span><span class="sxs-lookup"><span data-stu-id="fa895-182">Files of interest:</span></span>
    * <span data-ttu-id="fa895-183">catalina.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-184">host-manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-185">localhost.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-186">manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-187">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="fa895-188">對於入口網站**應用程式設定**部署：</span><span class="sxs-lookup"><span data-stu-id="fa895-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="fa895-189">資料夾位置：D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="fa895-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="fa895-190">感興趣區域：</span><span class="sxs-lookup"><span data-stu-id="fa895-190">Files of interest:</span></span>
    * <span data-ttu-id="fa895-191">catalina.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-192">host-manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-193">localhost.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-194">manager.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="fa895-195">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="fa895-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="fa895-196">如何進行 JDBC 驅動程式連線錯誤的疑難排解？</span><span class="sxs-lookup"><span data-stu-id="fa895-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="fa895-197">您可能會看見 hello 下 Tomcat 記錄檔中的訊息：</span><span class="sxs-lookup"><span data-stu-id="fa895-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="fa895-198">tooresolve hello 錯誤：</span><span class="sxs-lookup"><span data-stu-id="fa895-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="fa895-199">從您的應用程式/lib 資料夾移除 hello sqljdbc*.jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa895-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="fa895-200">如果您使用 hello 自訂 Tomcat 或 Azure Marketplace Tomcat web 伺服器，將複製此 d 檔案 toohello Tomcat lib 資料夾。</span><span class="sxs-lookup"><span data-stu-id="fa895-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="fa895-201">如果您要啟用從 Java hello Azure 入口網站 (選取**Java 1.8** > **Tomcat 伺服器**)，是平行 tooyour 應用程式的 hello 資料夾中複製 hello sqljdbc.* jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa895-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="fa895-202">接著，新增下列 classpath 設定 toohello web.config 檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="fa895-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="fa895-203">為什麼當我嘗試 toocopy 即時記錄檔時看到錯誤？</span><span class="sxs-lookup"><span data-stu-id="fa895-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="fa895-204">如果您嘗試 toocopy Java 應用程式 (例如，Tomcat) 的即時記錄檔，您可能會看到這個 FTP 錯誤：</span><span class="sxs-lookup"><span data-stu-id="fa895-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="fa895-205">hello 錯誤訊息可能有所不同，hello FTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="fa895-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="fa895-206">所有的 Java 應用程式都有這個鎖定問題。</span><span class="sxs-lookup"><span data-stu-id="fa895-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="fa895-207">只有 Kudu 支援 hello 應用程式執行時，請下載此檔案。</span><span class="sxs-lookup"><span data-stu-id="fa895-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="fa895-208">正在停止 hello 應用程式可讓 FTP 存取 toothese 檔案。</span><span class="sxs-lookup"><span data-stu-id="fa895-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="fa895-209">另一個解決方法是 toowrite WebJob 排程執行，而且複製這些檔案 tooa 不同的目錄。</span><span class="sxs-lookup"><span data-stu-id="fa895-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="fa895-210">範例專案，請參閱 hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob)專案。</span><span class="sxs-lookup"><span data-stu-id="fa895-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="fa895-211">其中找到 Jetty hello 記錄檔？</span><span class="sxs-lookup"><span data-stu-id="fa895-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="fa895-212">服務商場和自訂部署，hello 記錄檔是 hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="fa895-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="fa895-213">請注意 hello 資料夾位置，取決於您使用的 Jetty hello 版本。</span><span class="sxs-lookup"><span data-stu-id="fa895-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="fa895-214">例如，hello 提供路徑的 Jetty 9.1.2 如下。</span><span class="sxs-lookup"><span data-stu-id="fa895-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="fa895-215">尋找 jetty_*YYYY_MM_DD*.stderrout.log。</span><span class="sxs-lookup"><span data-stu-id="fa895-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="fa895-216">入口網站的應用程式設定部署的 hello 記錄檔位於 D:\home\LogFiles。</span><span class="sxs-lookup"><span data-stu-id="fa895-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="fa895-217">尋找 jetty_*YYYY_MM_DD*.stderrout.log</span><span class="sxs-lookup"><span data-stu-id="fa895-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="fa895-218">我能否從 Azure Web 應用程式傳送電子郵件？</span><span class="sxs-lookup"><span data-stu-id="fa895-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="fa895-219">App Service 沒有內建的電子郵件功能。</span><span class="sxs-lookup"><span data-stu-id="fa895-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="fa895-220">如需從應用程式傳送電子郵件的一些可行替代方案，請參閱本篇 [Stack Overflow 討論](http://stackoverflow.com/questions/17666161/sending-email-from-azure) (英文)。</span><span class="sxs-lookup"><span data-stu-id="fa895-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="fa895-221">為什麼我的 WordPress 網站重新導向 tooanother URL？</span><span class="sxs-lookup"><span data-stu-id="fa895-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="fa895-222">如果您最近有移轉 tooAzure，WordPress 可能會重新導向 toohello 舊網域 URL。</span><span class="sxs-lookup"><span data-stu-id="fa895-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="fa895-223">這被因為 hello MySQL 資料庫中的設定。</span><span class="sxs-lookup"><span data-stu-id="fa895-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="fa895-224">WordPress 協同 + 是 Azure 站台擴充功能，您可以直接在 hello 資料庫中使用 tooupdate hello 重新導向 URL。</span><span class="sxs-lookup"><span data-stu-id="fa895-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="fa895-225">如需使用 WordPress Buddy+ 的詳細資訊，請參閱 [WordPress 工具以及使用 WordPress Buddy+ 進行 MySQL 移轉](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="fa895-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="fa895-226">或者，如果您使用 SQL 查詢或 PHPMyAdmin 偏好 toomanually 更新 hello 重新導向 URL，請參閱[WordPress： 重新導向 URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="fa895-227">如何變更我的 WordPress 登入密碼？</span><span class="sxs-lookup"><span data-stu-id="fa895-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="fa895-228">如果您忘記您的 WordPress 登入密碼，您可以使用 WordPress 協同 + tooupdate 它。</span><span class="sxs-lookup"><span data-stu-id="fa895-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="fa895-229">密碼、 安裝 hello WordPress 協同 + Azure 網站擴充功能，並再完成 hello 步驟中所述的 tooreset [WordPress 工具和 MySQL 移轉與 WordPress 協同 +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="fa895-230">我無法登入 tooWordPress。</span><span class="sxs-lookup"><span data-stu-id="fa895-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="fa895-231">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="fa895-231">How do I resolve this?</span></span>

<span data-ttu-id="fa895-232">最近安裝外掛程式之後，如果您發現遭鎖定而無法進入 WordPress，則表示外掛程式可能有問題。</span><span class="sxs-lookup"><span data-stu-id="fa895-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="fa895-233">WordPress Buddy+ 是 Azure 網站擴充功能，可協助您停用 WordPress 中的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="fa895-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="fa895-234">如需詳細資訊，請參閱 [WordPress 工具以及使用 WordPress Buddy+ 進行 MySQL 移轉](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="fa895-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="fa895-235">我要如何移轉我的 WordPress 資料庫？</span><span class="sxs-lookup"><span data-stu-id="fa895-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="fa895-236">您已針對移轉的 hello MySQL 資料庫，連接的 tooyour WordPress 網站的多個選項：</span><span class="sxs-lookup"><span data-stu-id="fa895-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="fa895-237">開發人員： 使用 hello[命令提示字元或 PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="fa895-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="fa895-238">非開發人員：使用 [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="fa895-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="fa895-239">如何使 WordPress 更安全？</span><span class="sxs-lookup"><span data-stu-id="fa895-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="fa895-240">請參閱 toolearn WordPress 的安全性最佳作法的相關[的 WordPress 在 Azure 中的安全性最佳做法](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/)。</span><span class="sxs-lookup"><span data-stu-id="fa895-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="fa895-241">我試著 toouse PHPMyAdmin，而且我看到 hello 訊息 「 拒絕存取 」。</span><span class="sxs-lookup"><span data-stu-id="fa895-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="fa895-242">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="fa895-242">How do I resolve this?</span></span>

<span data-ttu-id="fa895-243">如果 hello MySQL 中應用程式功能並非在此應用程式服務執行個體中尚未執行，您可能會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="fa895-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="fa895-244">tooresolve hello 問題，請再試一次 tooaccess 您的網站。</span><span class="sxs-lookup"><span data-stu-id="fa895-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="fa895-245">這樣會啟動所需的 hello 程序，包括 hello MySQL 應用程式內的程序。</span><span class="sxs-lookup"><span data-stu-id="fa895-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="fa895-246">MySQL 正在執行的應用程式內，處理序總管中，確定該 mysqld.exe tooverify 會列在 hello 處理程序。</span><span class="sxs-lookup"><span data-stu-id="fa895-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="fa895-247">確定 MySQL 在應用程式正在執行之後，請再試一次 toouse PHPMyAdmin。</span><span class="sxs-lookup"><span data-stu-id="fa895-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="fa895-248">當我 tooimport 再試一次，或使用 PHPMyadmin 匯出我 MySQL 應用程式內的資料庫時，我會收到 HTTP 403 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa895-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="fa895-249">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="fa895-249">How do I resolve this?</span></span>

<span data-ttu-id="fa895-250">如果您使用舊版 Chrome，您可能會遇到已知的錯誤。</span><span class="sxs-lookup"><span data-stu-id="fa895-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="fa895-251">升級 tooa 較新版本的 Chrome tooresolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="fa895-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="fa895-252">也請嘗試使用不同的瀏覽器，如 Internet Explorer 或邊緣，其中 hello 不會發生問題。</span><span class="sxs-lookup"><span data-stu-id="fa895-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
