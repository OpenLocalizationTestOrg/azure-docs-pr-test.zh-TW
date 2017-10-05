---
title: "指定 Node.js 版本"
description: "了解如何指定 Azure 網站和雲端服務所使用的 Node.js 版本"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 89627e6a877c9f65a5216c55f58f1c707ea25d44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="41d46-103">在 Azure 應用程式中指定 Node.js 版本</span><span class="sxs-lookup"><span data-stu-id="41d46-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="41d46-104">裝載 Node.js 應用程式時，您可能會想要確定應用程式是使用特定版本的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="41d46-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="41d46-105">有數種方式可以為 Azure 上裝載的應用程式完成這項動作。</span><span class="sxs-lookup"><span data-stu-id="41d46-105">There are several ways to accomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="41d46-106">預設版本</span><span class="sxs-lookup"><span data-stu-id="41d46-106">Default versions</span></span>
<span data-ttu-id="41d46-107">Azure 提供的 Node.js 版本會持續進行更新。</span><span class="sxs-lookup"><span data-stu-id="41d46-107">The Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="41d46-108">除非另有指定，否則將會使用 `WEBSITE_NODE_DEFAULT_VERSION` 環境變數中指定的預設版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="41d46-109">若要覆寫此預設值，請依照本文下列各節中的步驟來進行</span><span class="sxs-lookup"><span data-stu-id="41d46-109">To override this default value, follow the steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="41d46-110">如果您要將應用程式裝載在 Azure 雲端服務 (Web 或背景工作角色) 中，而且這是您第一次部署應用程式，只要您安裝在部署環境中的 Node.js 版本符合 Azure 上提供的其中一個預設版本，Azure 就會嘗試使用這個版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="41d46-111">以 package.json 進行版本設定</span><span class="sxs-lookup"><span data-stu-id="41d46-111">Versioning with package.json</span></span>
<span data-ttu-id="41d46-112">您可以在 **package.json** 檔案中新增下列內容，以指定要使用的 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="41d46-113">其中 *version* 是要使用的特定版本號碼。</span><span class="sxs-lookup"><span data-stu-id="41d46-113">Where *version* is the specific version number to use.</span></span> <span data-ttu-id="41d46-114">您可以針對 version 指定較複雜的條件，例如：</span><span class="sxs-lookup"><span data-stu-id="41d46-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="41d46-115">由於 0.6.22 不是主控環境中已提供的版本，因此將改用 0.8 系列可用的最高版本，也就是 0.8.4 版。</span><span class="sxs-lookup"><span data-stu-id="41d46-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="41d46-116">版本控制網站與應用程式設定</span><span class="sxs-lookup"><span data-stu-id="41d46-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="41d46-117">如果您在網站中裝載應用程式，您可以將環境變數 **WEBSITE_NODE_DEFAULT_VERSION** 設定為所需的版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="41d46-118">以 PowerShell 進行雲端服務版本設定</span><span class="sxs-lookup"><span data-stu-id="41d46-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="41d46-119">如果您要將應用程式裝載在雲端服務中，而且要使用 Azure PowerShell 來部署應用程式，您可以使用 **Set-AzureServiceProjectRole** PowerShell Cmdlet 覆寫預設 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="41d46-120">例如：</span><span class="sxs-lookup"><span data-stu-id="41d46-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="41d46-121">請注意上述陳述式的參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="41d46-121">Note the parameters in the above statement are case-sensitive.</span></span>  <span data-ttu-id="41d46-122">您可以檢查角色 **package.json** 中的 **engines** 屬性，確認已選取正確的 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="41d46-123">您也可以使用 **Get-AzureServiceProjectRoleRuntime** 擷取對於以雲端服務形式裝載的應用程式而言，可用的 Node.js 版本清單。</span><span class="sxs-lookup"><span data-stu-id="41d46-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="41d46-124">務必確認您專案所依據的 Node.js 版本列在此清單中。</span><span class="sxs-lookup"><span data-stu-id="41d46-124">Always verify the version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="41d46-125">對 Azure 網站使用自訂版本</span><span class="sxs-lookup"><span data-stu-id="41d46-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="41d46-126">雖然 Azure 提供數個預設 Node.js 版本，不過您可能會想要使用預設未提供的版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span></span> <span data-ttu-id="41d46-127">如果您的應用程式是以 Azure 網站形式裝載，您可以使用 **iisnode.yml** 檔案達到該目的。</span><span class="sxs-lookup"><span data-stu-id="41d46-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span></span> <span data-ttu-id="41d46-128">下列步驟將逐步引導您對 Azure 網站使用自訂版本的 Node.Js：</span><span class="sxs-lookup"><span data-stu-id="41d46-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="41d46-129">建立新目錄，然後在目錄中建立 **server.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="41d46-129">Create a new directory, and then create a **server.js** file within the directory.</span></span> <span data-ttu-id="41d46-130">**server.js** 檔案應該包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="41d46-130">The **server.js** file should contain the following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="41d46-131">這將顯示當您瀏覽網站時會使用的 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="41d46-131">This will display the Node.js version being used when you browse the website.</span></span>
2. <span data-ttu-id="41d46-132">建立新網站並記下網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="41d46-132">Create a new Website and note the name of the site.</span></span> <span data-ttu-id="41d46-133">例如，以下使用 [Azure 命令列工具] 建立新的 Azure 網站 (名稱為 **mywebsite**)，然後編輯該網站的 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="41d46-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="41d46-134">建立名稱為 **bin** 的新目錄作為 **server.js** 檔案所在目錄的子目錄。</span><span class="sxs-lookup"><span data-stu-id="41d46-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span></span>
4. <span data-ttu-id="41d46-135">下載要讓應用程式使用的特定 **node.exe** 版本 (Windows 版本)。</span><span class="sxs-lookup"><span data-stu-id="41d46-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span></span> <span data-ttu-id="41d46-136">例如，以下使用 **curl** 下載 0.8.1 版。</span><span class="sxs-lookup"><span data-stu-id="41d46-136">For example, the following uses **curl** to download version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="41d46-137">將 **node.exe** 檔案儲存到先前建立的 **bin** 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="41d46-137">Save the **node.exe** file into the **bin** folder created previously.</span></span>
5. <span data-ttu-id="41d46-138">在 **server.js** 檔案所在的同一個目錄中建立 **iisnode.yml** 檔案，然後在 **iisnode.yml** 檔案中新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="41d46-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="41d46-139">您將應用程式發行到 Azure 網站後，您專案中的 **node.exe** 檔案將位在這個路徑中。</span><span class="sxs-lookup"><span data-stu-id="41d46-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span></span>
6. <span data-ttu-id="41d46-140">發行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="41d46-140">Publish your application.</span></span> <span data-ttu-id="41d46-141">例如，由於我稍早是使用 --git 參數建立新的網站，下列命令會將應用程式檔案新增到我的本機 Git 存放庫，然後將這些檔案推播到網站存放庫：</span><span class="sxs-lookup"><span data-stu-id="41d46-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="41d46-142">發行應用程式後，使用瀏覽器開啟網站。</span><span class="sxs-lookup"><span data-stu-id="41d46-142">After the application has published, open the website in a browser.</span></span> <span data-ttu-id="41d46-143">您應該會看見 "Hello from Azure running node version: v0.8.1" 訊息。</span><span class="sxs-lookup"><span data-stu-id="41d46-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="41d46-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41d46-144">Next Steps</span></span>
<span data-ttu-id="41d46-145">您已了解如何指定應用程式使用的 Node.js 版本，現在請了解如何[使用模組]、[建置並部署 Node.js 網站](app-service-web/app-service-web-get-started-nodejs.md)和[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]。</span><span class="sxs-lookup"><span data-stu-id="41d46-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="41d46-146">如需詳細資訊，請參閱 [Node.js 開發人員中心](https://azure.microsoft.com/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="41d46-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

<span data-ttu-id="41d46-147">[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="41d46-147">[How to use the Azure Command-Line Tools for Mac and Linux]:cli-install-nodejs.md</span></span>
<span data-ttu-id="41d46-148">[Azure 命令列工具]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="41d46-148">[Azure Command-line tools]:cli-install-nodejs.md</span></span>
<span data-ttu-id="41d46-149">[使用模組]: nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="41d46-149">[work with modules]: nodejs-use-node-modules-azure-apps.md</span></span>
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
