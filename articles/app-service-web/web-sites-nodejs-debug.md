---
title: "如何在 Azure App Service 中偵錯 Node.js Web 應用程式"
description: "了解如何在 Azure App Service 中偵錯 Node.js Web 應用程式。"
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="6f8e4-103">如何在 Azure App Service 中偵錯 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6f8e4-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="6f8e4-104">Azure 提供內建的診斷程式來協助偵錯 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 中裝載的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="6f8e4-105">本文中，您將了解如何啟用 stdout 和 stderr 記錄、在瀏覽器中顯示錯誤資訊，以及如何下載和檢視記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="6f8e4-106">對於 Azure 上裝載的 Node.js 應用程式，診斷程式由 [IISNode]提供。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="6f8e4-107">本文只討論最常用來收集診斷資訊的設定，不提供 IISNode 的完整使用參考。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="6f8e4-108">如需有關使用 IISNode 的詳細資訊，請參閱 GitHub 的 [IISNode Readme] 。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="6f8e4-109">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="6f8e4-109">Enable logging</span></span>
<span data-ttu-id="6f8e4-110">依預設，App Service Web 應用程式只擷取關於部署的診斷資訊，例如使用 Git 來部署 Web 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="6f8e4-111">如果您在部署時發生問題，此資訊很有用，例如安裝 **package.json**中參考的模組失敗時，或使用自訂部署指令碼時。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="6f8e4-112">若要啟用 stdout 和 stderr 資料流記錄，您必須在 Node.js 應用程式的根目錄中建立 **IISNode.yml** 檔案，並加入下列指令：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="6f8e4-113">這會啟用記錄來自 Node.js 應用程式的 stderr 和 stdout。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="6f8e4-114">**IISNode.yml** 檔案也可用來控制當失敗發生時，將易懂的錯誤還是開發人員錯誤傳回至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="6f8e4-115">若要傳回開發人員錯誤，請將下一行加入至 **IISNode.yml** 檔案：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="6f8e4-116">啟用此選項之後，IISNode 會將傳送至 stderr 的最後 64K 資訊傳回，而不是易懂的錯誤，例如「發生內部伺服器錯誤」。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="6f8e4-117">雖然 devErrorsEnabled 在開發期間診斷問題時很有用，但在生產環境中啟用可能會導致將開發錯誤傳送給使用者。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="6f8e4-118">如果您的應用程式中尚無 **IISNode.yml** 檔案，則在發行已更新的應用程之後，您必須重新啟動 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="6f8e4-119">如果只是在先前發行的現有 **IISNode.yml** 檔案中變更設定，則不需要重新啟動。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="6f8e4-120">如果 Web 應用程式是以 Azure 命令列工具或 Azure PowerShell Cmdlets 建立，則會自動建立預設的 **IISNode.yml** 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="6f8e4-121">若要重新啟動 Web 應用程式，請在 [Azure 入口網站](https://portal.azure.com) 中選取 Web 應用程式，然後按一下 [重新啟動] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![restart button][restart-button]

<span data-ttu-id="6f8e4-123">如果開發環境中已安裝 Azure 命令列工具，您可以使用下列命令來重新啟動 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="6f8e4-124">雖然 loggingEnabled 和 devErrorsEnabled 是最常用來擷取診斷資訊的 IISNode.yml 組態選項，但 IISNode.yml 也能用來為主控環境設定各種選項。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="6f8e4-125">如需完整的組態選項清單，請參閱 [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) 檔案。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="6f8e4-126">存取記錄檔</span><span class="sxs-lookup"><span data-stu-id="6f8e4-126">Accessing logs</span></span>
<span data-ttu-id="6f8e4-127">有三種方式可存取診斷記錄檔：使用檔案傳輸通訊協定 (FTP)、下載 Zip 封存檔，或即使更新的記錄資料流 (又稱為 tail)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="6f8e4-128">需要有 Azure 命令列工具，才能下載記錄檔的 Zip 封存檔或檢視即時資料流。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="6f8e4-129">請使用下列命令來安裝這些工具：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="6f8e4-130">安裝之後，可使用 'azure' 命令來存取工具。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="6f8e4-131">必須先設定命令列工具來使用您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="6f8e4-132">如需有關如何完成此工作的詳細資訊，請參閱＜ **如何使用 Azure 命令列工具** ＞的＜ [如何下載和匯入發行設定](../xplat-cli-connect.md) ＞一節。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="6f8e4-133">FTP</span><span class="sxs-lookup"><span data-stu-id="6f8e4-133">FTP</span></span>
<span data-ttu-id="6f8e4-134">若要透過 FTP 來存取診斷資訊，請造訪 [Azure 入口網站](https://portal.azure.com)，選取您的 Web 應用程式，然後選取 [儀表板]。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="6f8e4-135">在 [快速連結]區段中，[FTP DIAGNOSTIC LOGS] 和 [FTPS DIAGNOSTIC LOGS] 連結可讓您使用 FTP 通訊協定來存取記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="6f8e4-136">如果您先前沒有為 FTP 或部署設定使用者名稱和密碼，您可以從 [快速入門] 管理頁面中選取 [設定部署認證] 來設定。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="6f8e4-137">儀表板中傳回的 FTP URL 是 **LogFiles** 目錄，內含下列子目錄：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="6f8e4-138">[部署方法](web-sites-deploy.md) - 如果您使用 Git 之類的部署方法，則會建立相同名稱的目錄，其中含有與部署相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="6f8e4-139">nodejs - 從應用程式的所有執行個體擷取的 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="6f8e4-140">Zip 封存檔</span><span class="sxs-lookup"><span data-stu-id="6f8e4-140">Zip archive</span></span>
<span data-ttu-id="6f8e4-141">若要下載診斷記錄的 Zip 封存檔，請從 Azure 命令列工具中使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="6f8e4-142">這會將 **diagnostics.zip** 下載到目前目錄。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="6f8e4-143">此封存檔包含下列目錄結構：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="6f8e4-144">deployments - 關於應用程式部署的資訊記錄</span><span class="sxs-lookup"><span data-stu-id="6f8e4-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="6f8e4-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="6f8e4-145">LogFiles</span></span>
  
  * <span data-ttu-id="6f8e4-146">[部署方法](web-sites-deploy.md) - 如果您使用 Git 之類的部署方法，則會建立相同名稱的目錄，其中含有與部署相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="6f8e4-147">nodejs - 從應用程式的所有執行個體擷取的 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="6f8e4-148">即時資料流 (tail)</span><span class="sxs-lookup"><span data-stu-id="6f8e4-148">Live stream (tail)</span></span>
<span data-ttu-id="6f8e4-149">若要檢視診斷記錄資訊的即時資料流，請從 Azure 命令列工具中使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="6f8e4-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="6f8e4-150">這會傳回伺服器上最新發生之記錄事件的資料流。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="6f8e4-151">此資料流會傳回部署資訊及 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="6f8e4-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f8e4-152">Next Steps</span></span>
<span data-ttu-id="6f8e4-153">本文中，您學到如何啟用和存取 Azure 的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="6f8e4-154">此資訊有助於了解應用程式發生的問題，但也可能指出您使用的模組有問題，或 App Service Web Apps 使用的 Node.js 版本和部署環境中使用的版本不同。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="6f8e4-155">如需有關在 Azure 上使用模組的詳細資訊，請參閱＜ [在 Azure 應用程式中使用 Node.js 模組](../nodejs-use-node-modules-azure-apps.md)＞(英文)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="6f8e4-156">如需有關為應用程式指定 Node.js 版本的詳細資訊，請參閱＜ [在 Azure 應用程式中指定 Node.js 版本]＞(英文)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="6f8e4-157">如需詳細資訊，也請參閱 [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="6f8e4-158">變更的項目</span><span class="sxs-lookup"><span data-stu-id="6f8e4-158">What's changed</span></span>
* <span data-ttu-id="6f8e4-159">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6f8e4-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="6f8e4-160">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6f8e4-161">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="6f8e4-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="6f8e4-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="6f8e4-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="6f8e4-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="6f8e4-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="6f8e4-164">[在 Azure 應用程式中指定 Node.js 版本]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="6f8e4-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

