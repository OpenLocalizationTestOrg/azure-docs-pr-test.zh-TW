---
title: "Web 應用程式與 Express (Node.js) | Microsoft Docs"
description: "以雲端服務教學課程為基礎的教學課程，示範如何使用 Express 模組。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="d53c9-103">在 Azure 雲端服務上使用 Express 建立 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d53c9-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="d53c9-104">Node.js 包含核心執行時期的一組最低功能。</span><span class="sxs-lookup"><span data-stu-id="d53c9-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="d53c9-105">開發人員在開發 Node.js 應用程式時，通常會使用協力廠商模組來提供更多功能。</span><span class="sxs-lookup"><span data-stu-id="d53c9-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="d53c9-106">在本教學課程中，您將使用 [Express][Express] 模組來建立新的應用程式，此模組提供用於建立 Node.js Web 應用程式的 MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="d53c9-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="d53c9-107">完成之應用程式的螢幕擷取畫面如下：</span><span class="sxs-lookup"><span data-stu-id="d53c9-107">A screenshot of the completed application is below:</span></span>

![A web browser displaying Welcome to Express in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="d53c9-109">建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="d53c9-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="d53c9-110">請執行下列步驟來建立名為 'expressapp' 的新雲端服務專案：</span><span class="sxs-lookup"><span data-stu-id="d53c9-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="d53c9-111">從 [開始功能表] 或 [開始畫面] 搜尋 **Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="d53c9-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="d53c9-112">最後，用滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="d53c9-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell icon](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="d53c9-114">切換至 **c:\\node** 目錄，然後輸入下列命令來建立名為 **expressapp** 的新方案和名為 **WebRole1** 的 Web 角色：</span><span class="sxs-lookup"><span data-stu-id="d53c9-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="d53c9-115">**Add-AzureNodeWebRole** 預設會使用較舊版的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="d53c9-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="d53c9-116">上方的 **Set-AzureServiceProjectRole** 陳述式會指示 Azure 使用 0.10.21 版本的節點。</span><span class="sxs-lookup"><span data-stu-id="d53c9-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="d53c9-117">請注意這些參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="d53c9-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="d53c9-118">您可以檢查 **WebRole1\package.json** 中的 **engines** 屬性，確認已選取正確的 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="d53c9-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="d53c9-119">安裝 Express</span><span class="sxs-lookup"><span data-stu-id="d53c9-119">Install Express</span></span>
1. <span data-ttu-id="d53c9-120">發出下列命令來安裝 Express 產生器：</span><span class="sxs-lookup"><span data-stu-id="d53c9-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="d53c9-121">npm 命令的輸出類似下列結果。</span><span class="sxs-lookup"><span data-stu-id="d53c9-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell displaying the output of the npm install express command.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="d53c9-123">切換至 **WebRole1** 目錄，然後使用 express 命令來產生新的應用程式：</span><span class="sxs-lookup"><span data-stu-id="d53c9-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="d53c9-124">系統會提示您覆寫先前的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d53c9-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="d53c9-125">輸入 **y** 或 **yes** 繼續進行。</span><span class="sxs-lookup"><span data-stu-id="d53c9-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="d53c9-126">Express 會產生 app.js 檔案和資料夾結構來準備建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="d53c9-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![The output of the express command](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="d53c9-128">若要安裝 package.json 檔案中定義的其他相依性，請輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d53c9-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![The output of the npm install command](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="d53c9-130">使用下列命令，將 **bin/www** 檔案複製到 **server.js**。</span><span class="sxs-lookup"><span data-stu-id="d53c9-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="d53c9-131">正因如此，雲端服務便能找到此應用程式的進入點。</span><span class="sxs-lookup"><span data-stu-id="d53c9-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="d53c9-132">此命令完成之後，您應該會在 WebRole1 目錄中擁有 **server.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="d53c9-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="d53c9-133">修改 **server.js** ，從下一行程式碼中移除其中一個 '.' 字元。</span><span class="sxs-lookup"><span data-stu-id="d53c9-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="d53c9-134">進行這個修改之後，程式碼行應會以如下方式出現。</span><span class="sxs-lookup"><span data-stu-id="d53c9-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="d53c9-135">由於我們已將檔案 (先前為 **bin/www**) 移至與應用程式檔案所需的相同目錄，因此，這是必要變更。</span><span class="sxs-lookup"><span data-stu-id="d53c9-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="d53c9-136">完成此變更之後，儲存 **server.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="d53c9-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="d53c9-137">使用下列命令，在 Azure 模擬器中執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="d53c9-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![A web page containing welcome to express.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="d53c9-139">修改檢視</span><span class="sxs-lookup"><span data-stu-id="d53c9-139">Modifying the View</span></span>
<span data-ttu-id="d53c9-140">現在，修改檢視來顯示「歡迎在 Azure 中使用 Express」訊息。</span><span class="sxs-lookup"><span data-stu-id="d53c9-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="d53c9-141">輸入下列命令來開啟 index.jade 檔案：</span><span class="sxs-lookup"><span data-stu-id="d53c9-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![The contents of the index.jade file.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="d53c9-143">Jade 是 Express 應用程式使用的預設檢視引擎。</span><span class="sxs-lookup"><span data-stu-id="d53c9-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="d53c9-144">如需有關 Jade 檢視引擎的詳細資訊，請參閱 [http://jade-lang.com][http://jade-lang.com]。</span><span class="sxs-lookup"><span data-stu-id="d53c9-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="d53c9-145">修改最後一行文字，加上 **in Azure**。</span><span class="sxs-lookup"><span data-stu-id="d53c9-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![index.jade 檔案，最後一行是：p Welcome to \#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="d53c9-147">儲存檔案並結束 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="d53c9-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="d53c9-148">重新整理瀏覽器，您將會看到變更。</span><span class="sxs-lookup"><span data-stu-id="d53c9-148">Refresh your browser and you will see your changes.</span></span>
   
   ![A browser window, the page contains Welcome to Express in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="d53c9-150">測試應用程式之後，請使用 **Stop-AzureEmulator** Cmdlet 來停止模擬器。</span><span class="sxs-lookup"><span data-stu-id="d53c9-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="d53c9-151">將應用程式發行至 Azure</span><span class="sxs-lookup"><span data-stu-id="d53c9-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="d53c9-152">在 Azure PowerShell 視窗中，請使用 **Publish-AzureServiceProject** Cmdlet 將應用程式部署至雲端服務</span><span class="sxs-lookup"><span data-stu-id="d53c9-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="d53c9-153">部署作業完成時，瀏覽器會開啟並顯示網頁。</span><span class="sxs-lookup"><span data-stu-id="d53c9-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![A web browser displaying the Express page.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="d53c9-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d53c9-156">Next steps</span></span>
<span data-ttu-id="d53c9-157">如需詳細資訊，請參閱 [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="d53c9-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


