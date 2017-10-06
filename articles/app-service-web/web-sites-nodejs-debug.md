---
title: "aaaHow toodebug Node.js web 應用程式在 Azure 應用程式服務"
description: "了解如何 toodebug Node.js web 應用程式在 Azure App Service 中。"
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="32f0c-103">Toodebug Node.js web 應用程式在 Azure App Service 中的方式</span><span class="sxs-lookup"><span data-stu-id="32f0c-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="32f0c-104">Azure 提供內建的診斷與偵錯 Node.js 應用程式中裝載的 tooassist [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f0c-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="32f0c-105">在本文中，您將學習如何 tooenable 記錄 stdout 和 stderr、 在 hello 瀏覽器中顯示錯誤資訊和 toodownload 和檢視記錄檔。</span><span class="sxs-lookup"><span data-stu-id="32f0c-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="32f0c-106">對於 Azure 上裝載的 Node.js 應用程式，診斷程式由 [IISNode]提供。</span><span class="sxs-lookup"><span data-stu-id="32f0c-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="32f0c-107">雖然這篇文章討論 hello 最常見的設定用於蒐集診斷資訊，它不使用 IISNode 提供完整的參考。</span><span class="sxs-lookup"><span data-stu-id="32f0c-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="32f0c-108">如需使用 IISNode 的詳細資訊，請參閱 hello [IISNode 讀我檔案]GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="32f0c-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="32f0c-109">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="32f0c-109">Enable logging</span></span>
<span data-ttu-id="32f0c-110">依預設，App Service Web 應用程式只擷取關於部署的診斷資訊，例如使用 Git 來部署 Web 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="32f0c-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="32f0c-111">如果您在部署時發生問題，此資訊很有用，例如安裝 **package.json**中參考的模組失敗時，或使用自訂部署指令碼時。</span><span class="sxs-lookup"><span data-stu-id="32f0c-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="32f0c-112">tooenable hello stdout 和 stderr 資料流的記錄，您必須建立**IISNode.yml**根目錄 hello Node.js 應用程式檔案，然後加入下列 hello:</span><span class="sxs-lookup"><span data-stu-id="32f0c-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="32f0c-113">這可讓 hello 記錄 stderr 和 stdout 從 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f0c-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="32f0c-114">hello **IISNode.yml**檔案也可以使用的 toocontrol 是否易懂的錯誤訊息或開發人員錯誤傳回 toohello 瀏覽器發生失敗時。</span><span class="sxs-lookup"><span data-stu-id="32f0c-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="32f0c-115">tooenable 開發人員錯誤，加入下列行 toohello hello **IISNode.yml**檔案：</span><span class="sxs-lookup"><span data-stu-id="32f0c-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="32f0c-116">一旦啟用此選項，IISNode 會傳回 hello 最後 64k 傳送 toostderr 而不是易記的錯誤，例如 「 發生內部伺服器錯誤 」 的資訊。</span><span class="sxs-lookup"><span data-stu-id="32f0c-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="32f0c-117">雖然 devErrorsEnabled 在開發期間在診斷問題時很有用，讓它在生產環境中可能會導致傳送 tooend 使用者開發錯誤。</span><span class="sxs-lookup"><span data-stu-id="32f0c-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="32f0c-118">如果 hello **IISNode.yml**檔案原本不存在您的應用程式內、 發行 hello 更新應用程式之後必須重新啟動您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="32f0c-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="32f0c-119">如果只是在先前發行的現有 **IISNode.yml** 檔案中變更設定，則不需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="32f0c-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="32f0c-120">如果您的 web 應用程式使用 hello Azure 命令列工具或 Azure PowerShell Cmdlet，預設值建立**IISNode.yml**會自動建立檔案。</span><span class="sxs-lookup"><span data-stu-id="32f0c-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="32f0c-121">toorestart hello web 應用程式中，選取 hello web 應用程式在 hello [Azure 入口網站](https://portal.azure.com)，然後按一下**重新啟動**按鈕：</span><span class="sxs-lookup"><span data-stu-id="32f0c-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![restart button][restart-button]

<span data-ttu-id="32f0c-123">如果 hello Azure 命令列工具安裝在開發環境中，您可以使用下列命令 toorestart hello web 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="32f0c-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="32f0c-124">雖然 loggingEnabled 和 devErrorsEnabled 擷取診斷資訊的最常用的 hello IISNode.yml 組態選項，IISNode.yml 可以使用的 tooconfigure 各種裝載環境的選項。</span><span class="sxs-lookup"><span data-stu-id="32f0c-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="32f0c-125">如需 hello 組態選項的完整清單，請參閱 hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml)檔案。</span><span class="sxs-lookup"><span data-stu-id="32f0c-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="32f0c-126">存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="32f0c-126">Accessing logs</span></span>
<span data-ttu-id="32f0c-127">三種方式; 可以存取診斷記錄檔使用 hello 檔案傳輸通訊協定 (FTP)，下載 Zip 封存，或做為即時更新的 hello 記錄 （也稱為結尾） 的資料流。</span><span class="sxs-lookup"><span data-stu-id="32f0c-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="32f0c-128">下載 hello Zip 封存的 hello 記錄檔，或檢視 hello 即時資料流需要 hello Azure 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="32f0c-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="32f0c-129">這些可以使用下列命令的 hello 安裝：</span><span class="sxs-lookup"><span data-stu-id="32f0c-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="32f0c-130">安裝之後，就可以使用 hello 'azure' 命令來存取 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="32f0c-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="32f0c-131">hello 命令列工具必須先設定的 toouse 您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="32f0c-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="32f0c-132">如需如何 tooaccomplish 這工作資訊，請參閱 hello **toodownload 和匯入發行設定**區段 hello [tooUse hello Azure 命令列工具的方式](../xplat-cli-connect.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="32f0c-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="32f0c-133">FTP</span><span class="sxs-lookup"><span data-stu-id="32f0c-133">FTP</span></span>
<span data-ttu-id="32f0c-134">透過 FTP，tooaccess hello 診斷資訊，請瀏覽 hello [Azure 入口網站](https://portal.azure.com)，選取您的 web 應用程式，然後選取 hello**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="32f0c-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="32f0c-135">在 hello**快速連結**區段，hello **FTP 診斷記錄**和**FTPS 診斷記錄**連結提供使用 hello FTP 通訊協定存取 toohello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="32f0c-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="32f0c-136">如果您先前未設定使用者名稱和密碼的 FTP 或部署，您可以從 hello**快速入門**管理頁面中的選取**設定部署認證**。</span><span class="sxs-lookup"><span data-stu-id="32f0c-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="32f0c-137">hello 傳回 hello 儀表板中的 FTP URL 為 hello **LogFiles**目錄，將會包含下列子目錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="32f0c-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="32f0c-138">[部署方法](web-sites-deploy.md)-如果您使用的部署方法，例如 Git，hello 相同名稱將會建立，而且會包含資訊的目錄相關 toodeployments。</span><span class="sxs-lookup"><span data-stu-id="32f0c-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="32f0c-139">nodejs - 從應用程式的所有執行個體擷取的 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。</span><span class="sxs-lookup"><span data-stu-id="32f0c-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="32f0c-140">Zip 封存檔</span><span class="sxs-lookup"><span data-stu-id="32f0c-140">Zip archive</span></span>
<span data-ttu-id="32f0c-141">toodownload Zip 封存 hello 診斷記錄檔的使用 hello hello Azure 命令列工具中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="32f0c-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="32f0c-142">這會下載**diagnostics.zip** hello 目前目錄中。</span><span class="sxs-lookup"><span data-stu-id="32f0c-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="32f0c-143">這個封存包含下列目錄結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="32f0c-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="32f0c-144">deployments - 關於應用程式部署的資訊記錄</span><span class="sxs-lookup"><span data-stu-id="32f0c-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="32f0c-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="32f0c-145">LogFiles</span></span>
  
  * <span data-ttu-id="32f0c-146">[部署方法](web-sites-deploy.md)-如果您使用的部署方法，例如 Git，hello 相同名稱將會建立，而且會包含資訊的目錄相關 toodeployments。</span><span class="sxs-lookup"><span data-stu-id="32f0c-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="32f0c-147">nodejs - 從應用程式的所有執行個體擷取的 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。</span><span class="sxs-lookup"><span data-stu-id="32f0c-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="32f0c-148">即時資料流 (tail)</span><span class="sxs-lookup"><span data-stu-id="32f0c-148">Live stream (tail)</span></span>
<span data-ttu-id="32f0c-149">tooview 即時資料流的診斷記錄檔資訊，使用 hello hello Azure 命令列工具中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="32f0c-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="32f0c-150">這會傳回 hello 伺服器上發生更新的記錄事件資料流。</span><span class="sxs-lookup"><span data-stu-id="32f0c-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="32f0c-151">此資料流會傳回部署資訊及 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。</span><span class="sxs-lookup"><span data-stu-id="32f0c-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="32f0c-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32f0c-152">Next Steps</span></span>
<span data-ttu-id="32f0c-153">在這個發行項您學到如何 tooenable 和存取 azure 診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="32f0c-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="32f0c-154">雖然這項資訊適用於瞭解問題發生的應用程式時，它可能會指向您要使用的模組或 Node.js App Service Web 應用程式所使用的 hello 版 tooa 問題是不同於部署中使用一個 hello環境。</span><span class="sxs-lookup"><span data-stu-id="32f0c-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="32f0c-155">如需有關在 Azure 上使用模組的詳細資訊，請參閱＜ [在 Azure 應用程式中使用 Node.js 模組](../nodejs-use-node-modules-azure-apps.md)＞(英文)。</span><span class="sxs-lookup"><span data-stu-id="32f0c-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="32f0c-156">如需有關為應用程式指定 Node.js 版本的詳細資訊，請參閱＜ [在 Azure 應用程式中指定 Node.js 版本]＞(英文)。</span><span class="sxs-lookup"><span data-stu-id="32f0c-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="32f0c-157">如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="32f0c-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="32f0c-158">變更的項目</span><span class="sxs-lookup"><span data-stu-id="32f0c-158">What's changed</span></span>
* <span data-ttu-id="32f0c-159">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="32f0c-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="32f0c-160">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="32f0c-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="32f0c-161">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="32f0c-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode 讀我檔案]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[在 Azure 應用程式中指定 Node.js 版本]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

