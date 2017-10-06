---
title: "aaaWeb 快速 (Node.js) 的應用程式 |Microsoft 文件"
description: "教學課程會建置 hello 雲端服務的教學課程，並示範如何 toouse hello Express 模組。"
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
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="827b8-103">在 Azure 雲端服務上使用 Express 建立 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="827b8-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="827b8-104">Node.js hello 核心執行階段中包含的最少的功能。</span><span class="sxs-lookup"><span data-stu-id="827b8-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="827b8-105">開發人員在開發 Node.js 應用程式時，通常會使用第 3 個合作對象模組 tooprovide 額外的功能。</span><span class="sxs-lookup"><span data-stu-id="827b8-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="827b8-106">在本教學課程中，您將建立新的應用程式使用 hello [Express] [ Express]模組，可讓 MVC 架構建立 Node.js web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="827b8-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="827b8-107">底下是完成 hello 應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="827b8-107">A screenshot of hello completed application is below:</span></span>

![在 Azure 中顯示 歡迎使用 tooExpress 網頁瀏覽器](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="827b8-109">建立雲端服務專案</span><span class="sxs-lookup"><span data-stu-id="827b8-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="827b8-110">執行 hello 下列步驟 toocreate 新的雲端服務專案名為 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="827b8-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="827b8-111">從 hello**開始功能表**或**[開始] 畫面**，搜尋**Windows PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="827b8-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="827b8-112">最後，用滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [以系統管理員身分執行]。</span><span class="sxs-lookup"><span data-stu-id="827b8-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Azure PowerShell icon](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="827b8-114">變更目錄 toohello **c:\\節點**目錄，然後輸入下列命令 toocreate 名為新方案的 hello **expressapp**和名為 web 角色**WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="827b8-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="827b8-115">**Add-AzureNodeWebRole** 預設會使用較舊版的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="827b8-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="827b8-116">hello**組 AzureServiceProjectRole**上述陳述式會指示 Azure toouse v0.10.21 的節點。</span><span class="sxs-lookup"><span data-stu-id="827b8-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="827b8-117">請注意 hello 參數會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="827b8-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="827b8-118">您可以確認已選取 hello 正確版本的 Node.js 藉由檢查 hello**引擎**屬性**WebRole1\package.json**。</span><span class="sxs-lookup"><span data-stu-id="827b8-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="827b8-119">安裝 Express</span><span class="sxs-lookup"><span data-stu-id="827b8-119">Install Express</span></span>
1. <span data-ttu-id="827b8-120">藉由發出下列命令的 hello 安裝 hello Express 產生器：</span><span class="sxs-lookup"><span data-stu-id="827b8-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="827b8-121">hello hello npm 命令輸出應該看起來類似下列的 toohello 結果。</span><span class="sxs-lookup"><span data-stu-id="827b8-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Windows PowerShell 顯示 hello 輸出的 hello npm 安裝 express 命令。](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="827b8-123">變更目錄 toohello **WebRole1**目錄並用 hello express 命令 toogenerate 新的應用程式：</span><span class="sxs-lookup"><span data-stu-id="827b8-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="827b8-124">您將會提示的 toooverwrite 早的應用程式。</span><span class="sxs-lookup"><span data-stu-id="827b8-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="827b8-125">輸入**y**或**是**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="827b8-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="827b8-126">Express 將會產生 hello app.js 檔案和建置您的應用程式的資料夾結構。</span><span class="sxs-lookup"><span data-stu-id="827b8-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![hello hello express 命令輸出](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="827b8-128">tooinstall hello package.json 檔中定義的其他相依性輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="827b8-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![hello 輸出的 hello npm 安裝命令](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="827b8-130">使用 hello 下列命令 toocopy hello **bin w**檔案太**立即轉譯 server.js**。</span><span class="sxs-lookup"><span data-stu-id="827b8-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="827b8-131">這是讓 hello 雲端服務可以找到 hello 進入點為此應用程式。</span><span class="sxs-lookup"><span data-stu-id="827b8-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="827b8-132">此命令完成之後，您應該有**立即轉譯 server.js** hello WebRole1 目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="827b8-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="827b8-133">修改 hello**立即轉譯 server.js** tooremove hello 的其中一個 '。 ' hello 以下的字元。</span><span class="sxs-lookup"><span data-stu-id="827b8-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="827b8-134">進行這項修改後, hello 行應該顯示如下。</span><span class="sxs-lookup"><span data-stu-id="827b8-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="827b8-135">這項變更是必要的因為我們將 hello 檔案移 (先前稱為**bin w**，) toohello hello 應用程式檔案需要同一個目錄。</span><span class="sxs-lookup"><span data-stu-id="827b8-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="827b8-136">變更之後，儲存 hello**立即轉譯 server.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="827b8-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="827b8-137">使用下列命令 toorun hello 應用程式在 hello Azure 模擬器中的 hello:</span><span class="sxs-lookup"><span data-stu-id="827b8-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![包含  褖畫惎 tooexpress 的網頁。](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="827b8-139">修改 hello 檢視</span><span class="sxs-lookup"><span data-stu-id="827b8-139">Modifying hello View</span></span>
<span data-ttu-id="827b8-140">現在修改 hello 檢視 toodisplay hello 訊息 「 在 Azure 中的 歡迎使用 tooExpress"。</span><span class="sxs-lookup"><span data-stu-id="827b8-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="827b8-141">輸入下列命令 tooopen hello index.jade 檔 hello:</span><span class="sxs-lookup"><span data-stu-id="827b8-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![hello hello index.jade 檔案內容。](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="827b8-143">Jade 是 hello Express 應用程式所使用的預設檢視引擎。</span><span class="sxs-lookup"><span data-stu-id="827b8-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="827b8-144">如需有關 hello Jade 檢視引擎的詳細資訊，請參閱[http://jade-lang.com][http://jade-lang.com]。</span><span class="sxs-lookup"><span data-stu-id="827b8-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="827b8-145">修改 hello 最後一行的文字，藉由附加**在 Azure 中**。</span><span class="sxs-lookup"><span data-stu-id="827b8-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![hello index.jade 檔案，hello 最後一行讀取： p 太歡迎\#{t} 在 Azure 中](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="827b8-147">儲存 hello 檔案並結束 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="827b8-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="827b8-148">重新整理瀏覽器，您將會看到變更。</span><span class="sxs-lookup"><span data-stu-id="827b8-148">Refresh your browser and you will see your changes.</span></span>
   
   ![瀏覽器視窗中，hello 頁面包含在 Azure 中的 歡迎使用 tooExpress](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="827b8-150">測試的 hello 應用程式後使用 hello**停止 AzureEmulator** cmdlet toostop hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="827b8-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="827b8-151">發行 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="827b8-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="827b8-152">在 hello Azure PowerShell 視窗中，使用 hello**發行 AzureServiceProject** cmdlet toodeploy hello 應用程式 tooa 雲端服務</span><span class="sxs-lookup"><span data-stu-id="827b8-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="827b8-153">Hello 部署作業完成之後，您的瀏覽器會開啟並顯示 hello 的網頁。</span><span class="sxs-lookup"><span data-stu-id="827b8-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![網頁瀏覽器顯示 hello Express 頁面。](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="827b8-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="827b8-156">Next steps</span></span>
<span data-ttu-id="827b8-157">如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="827b8-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


