---
title: "在 Azure App Service 中使用 Socket.IO 建立 Node.js 聊天應用程式"
description: "示範在裝載於 Azure 的 node.js Web 應用程式中使用 socket.io 的教學課程。"
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="fc037-103">在 Azure App Service 中使用 Socket.IO 建立 Node.js 聊天應用程式</span><span class="sxs-lookup"><span data-stu-id="fc037-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="fc037-104">Socket.IO 使用 WebSocket 提供 node.js 伺服器與用戶端之間的即時通訊。</span><span class="sxs-lookup"><span data-stu-id="fc037-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="fc037-105">此外，它還能支援遞補其他適用於舊版瀏覽器的傳輸 (例如長輪詢)。</span><span class="sxs-lookup"><span data-stu-id="fc037-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="fc037-106">本教學課程將逐步引導您裝載 Socket.IO 型聊天應用程式以做為 Azure Web 應用程式，並示範如何使用 [Azure Redis 快取]為應用程式調整規模。</span><span class="sxs-lookup"><span data-stu-id="fc037-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="fc037-107">如需 Socket.IO 的詳細資訊，請參閱 <http://socket.io/>。</span><span class="sxs-lookup"><span data-stu-id="fc037-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="fc037-108">此工作中的程序適用於 [App Service Web Apps]。對於雲端服務，請參閱[在 Azure 雲端服務上使用 Socket.IO 建立 Node.js 聊天應用程式]。</span><span class="sxs-lookup"><span data-stu-id="fc037-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="fc037-109">下載聊天範例</span><span class="sxs-lookup"><span data-stu-id="fc037-109">Download the chat example</span></span>
<span data-ttu-id="fc037-110">在此專案中，我們將使用 [Socket.IO GitHub 儲存機制]中的聊天範例。</span><span class="sxs-lookup"><span data-stu-id="fc037-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="fc037-111">請執行下列步驟來下載範例，並將它加入至您先前建立的專案。</span><span class="sxs-lookup"><span data-stu-id="fc037-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="fc037-112">下載 Socket.IO 專案 (版本 1.3.5 已用於此文件) 的 [ZIP 或 GZ 封存版本]</span><span class="sxs-lookup"><span data-stu-id="fc037-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="fc037-113">將此封存解壓縮並將 **examples\\chat** 目錄複製到新的位置。</span><span class="sxs-lookup"><span data-stu-id="fc037-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="fc037-114">例如，**\\node\\chat**。</span><span class="sxs-lookup"><span data-stu-id="fc037-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="fc037-115">修改 App.js 和安裝模組</span><span class="sxs-lookup"><span data-stu-id="fc037-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="fc037-116">將 **index.js** 檔案重新命名為 **app.js**。</span><span class="sxs-lookup"><span data-stu-id="fc037-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="fc037-117">如此能讓 Azure 偵測到這是 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc037-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="fc037-118">在文字編輯器中開啟 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="fc037-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="fc037-119">變更包含 `var io = require('../..')(server);` 的字行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fc037-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="fc037-120">開啟 **package.json** 檔案，並在 `dependencies` 下方加入對 socket.io 的參考，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fc037-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="fc037-121">從命令列中，切換至 **\\node\\chat** 目錄，然後使用 npm 來安裝此應用程式所需的模組：</span><span class="sxs-lookup"><span data-stu-id="fc037-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="fc037-122">這會將模組安裝至名為 **node_modules** 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="fc037-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="fc037-123">建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fc037-123">Create an Azure Web App</span></span>
<span data-ttu-id="fc037-124">遵循以下步驟來建立 Azure Web 應用程式、啟用 Git 發行，然後針對 Web 應用程式啟用 WebSocket 支援。</span><span class="sxs-lookup"><span data-stu-id="fc037-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="fc037-125">若要完成此教學課程，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc037-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="fc037-126">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc037-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="fc037-127">如需詳細資料，請參閱 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="fc037-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="fc037-128">安裝 Azure 命令列介面 (Azure CLI)，並連線到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc037-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="fc037-129">請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="fc037-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="fc037-130">如果這是您第一次在 Azure 中設定儲存機制，就需要建立登入認證。</span><span class="sxs-lookup"><span data-stu-id="fc037-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="fc037-131">從 Azure CLI 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="fc037-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="fc037-132">切換至 **\\node\chat** 目錄，然後使用下列命令來建立新的 Azure Web 應用程式和本機 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="fc037-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="fc037-133">這個命令也會建立名為 'azure' 的 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="fc037-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="fc037-134">您必須將 'mysitename' 改成您的 Web 應用程式的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="fc037-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="fc037-135">使用下列命令，將現有的檔案認可到本機儲存機制：</span><span class="sxs-lookup"><span data-stu-id="fc037-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="fc037-136">使用下列命令，將檔案推送至 Azure Web Apps 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="fc037-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="fc037-137">系統出現提示時，請輸入步驟 2 中的認證。</span><span class="sxs-lookup"><span data-stu-id="fc037-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="fc037-138">在伺服器上匯入模組時會顯示狀態訊息。</span><span class="sxs-lookup"><span data-stu-id="fc037-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="fc037-139">此程序完成之後，應用程式將裝載於 Azure Web 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="fc037-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fc037-140">在模組安裝期間，您可能會看到「找不到匯入的專案...」的錯誤。</span><span class="sxs-lookup"><span data-stu-id="fc037-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="fc037-141">請放心忽略這項錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fc037-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="fc037-142">Socket.IO 使用 WebSockets (在 Azure 上依預設不會啟用)。</span><span class="sxs-lookup"><span data-stu-id="fc037-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="fc037-143">若要啟用 Web Sockets，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="fc037-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="fc037-144">如果出現提示，請輸入 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="fc037-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fc037-145">'azure site set -w' 命令僅適用於 Azure 命令列介面 0.7.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fc037-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="fc037-146">您也可以使用 [Azure 入口網站](https://portal.azure.com)來啟用 WebSocket 支援。</span><span class="sxs-lookup"><span data-stu-id="fc037-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="fc037-147">若要使用 Azure 入口網站啟用 WebSocket，可從 [Web Apps] 刀鋒視窗中按一下 Web 應用程式，然後依序按一下 [所有設定] > [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="fc037-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="fc037-148">在 [Web 通訊端] 下方，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="fc037-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="fc037-149">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="fc037-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="fc037-150">若要在 Azure 上檢視 Web 應用程式，請使用下列命令來啟動網頁瀏覽器，並瀏覽至裝載的 Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="fc037-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="fc037-151">您的應用程式現在已在 Azure 上執行，而且可以使用 Socket.IO 在不同用戶端之間轉送聊天訊息。</span><span class="sxs-lookup"><span data-stu-id="fc037-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="fc037-152">橫向擴充</span><span class="sxs-lookup"><span data-stu-id="fc037-152">Scale out</span></span>
<span data-ttu-id="fc037-153">Socket.IO 應用程式可以使用 **配接器** 來橫向擴充，以在多個應用程式執行個體之間散佈訊息和事件。</span><span class="sxs-lookup"><span data-stu-id="fc037-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="fc037-154">由於市面上已有數種配接器，因此可以輕鬆使用 [socket.io-redis] 配接器來搭配 Azure Redis 快取功能。</span><span class="sxs-lookup"><span data-stu-id="fc037-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="fc037-155">橫向擴充 Socket.IO 解決方案的額外需求是支援黏性工作階段。</span><span class="sxs-lookup"><span data-stu-id="fc037-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="fc037-156">Azure Web Apps 的黏性工作階段預設是透過 Azure 要求路由來啟用。</span><span class="sxs-lookup"><span data-stu-id="fc037-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="fc037-157">如需詳細資訊，請參閱 [Azure 網站的執行個體同質性]。</span><span class="sxs-lookup"><span data-stu-id="fc037-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="fc037-158">建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="fc037-158">Create a Redis cache</span></span>
<span data-ttu-id="fc037-159">執行 [在 Azure Redis 快取中建立快取] 中的步驟以建立新的快取。</span><span class="sxs-lookup"><span data-stu-id="fc037-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="fc037-160">儲存快取的**主機名稱**和**主要金鑰**，因為後續步驟將會需要這些項目。</span><span class="sxs-lookup"><span data-stu-id="fc037-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="fc037-161">新增 redis 和 socket.io-redis 模組</span><span class="sxs-lookup"><span data-stu-id="fc037-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="fc037-162">從命令列中，切換至 **\\node\\chat** 目錄，然後執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="fc037-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="fc037-163">此命令中指定的版本是測試本文章所使用的版本。</span><span class="sxs-lookup"><span data-stu-id="fc037-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="fc037-164">修改 **app.js** 檔案以在 `var io = require('socket.io')(server);` 之後緊接下列行</span><span class="sxs-lookup"><span data-stu-id="fc037-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="fc037-165">將 **redishostname** 和 **rediskey** 取代為 Redis 快取的主機名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc037-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="fc037-166">如此將會為先前建立的 Redis 快取建立一個發佈和訂閱用戶端。</span><span class="sxs-lookup"><span data-stu-id="fc037-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="fc037-167">之後該用戶端會搭配配接器使用，以將 Socket.IO 設定為使用 Redis 快取在應用程式的執行個體之間傳遞訊息和事件。</span><span class="sxs-lookup"><span data-stu-id="fc037-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fc037-168">雖然 **socket.io-redis** 配接器可以直接與 Redis 通訊，但是目前版本並不支援 Azure Redis 快取所需的驗證。</span><span class="sxs-lookup"><span data-stu-id="fc037-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="fc037-169">因此，系統會使用 **redis** 模組來建立初始連線，然後將該用戶端傳遞至 **socket.io-redis** 配接器。</span><span class="sxs-lookup"><span data-stu-id="fc037-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="fc037-170">雖然 Azure Redis 快取使用連接埠 6380 來支援安全的連線，但是此範例中使用的模組截至 2014/7/14 為止並不支援安全的連線。</span><span class="sxs-lookup"><span data-stu-id="fc037-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="fc037-171">以上程式碼使用的是預設的 6379 連接埠 (不安全)。</span><span class="sxs-lookup"><span data-stu-id="fc037-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="fc037-172">儲存已修改的 **app.js**</span><span class="sxs-lookup"><span data-stu-id="fc037-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="fc037-173">認可變更並重新部署</span><span class="sxs-lookup"><span data-stu-id="fc037-173">Commit changes and redeploy</span></span>
<span data-ttu-id="fc037-174">從 **\\node\\chat** 目錄的命令列中，使用下列命令來認可變更並重新部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc037-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="fc037-175">一旦將變更推送至伺服器，您就可以使用下列命令在多個執行個體間擴充網站。</span><span class="sxs-lookup"><span data-stu-id="fc037-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="fc037-176">其中 **#** 是要建立的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="fc037-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="fc037-177">您可以從多個瀏覽器或多部電腦連接至 Web 應用程式，以確認該訊息已正確傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="fc037-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fc037-178">疑難排解</span><span class="sxs-lookup"><span data-stu-id="fc037-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="fc037-179">連線限制</span><span class="sxs-lookup"><span data-stu-id="fc037-179">Connection limits</span></span>
<span data-ttu-id="fc037-180">Azure Web Apps 可用於多個 SKU，SKU 可以決定您網站適用的資源。</span><span class="sxs-lookup"><span data-stu-id="fc037-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="fc037-181">這包含允許 WebSocket 連線的數目。</span><span class="sxs-lookup"><span data-stu-id="fc037-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="fc037-182">如需詳細資訊，請參閱 [Web Apps 定價]頁面。</span><span class="sxs-lookup"><span data-stu-id="fc037-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="fc037-183">使用 WebSockets 而未傳送的訊息</span><span class="sxs-lookup"><span data-stu-id="fc037-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="fc037-184">如果用戶端瀏覽器持續遞補長輪詢，而非使用 WebSockets，可能是下列原因所致。</span><span class="sxs-lookup"><span data-stu-id="fc037-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="fc037-185">**試圖將傳輸僅限制到 WebSockets**</span><span class="sxs-lookup"><span data-stu-id="fc037-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="fc037-186">為了讓 Socket.IO 使用 WebSockets 作為訊息傳輸，伺服器和用戶端都必須支援 WebSockets。</span><span class="sxs-lookup"><span data-stu-id="fc037-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="fc037-187">如果其中一方不支援 WebSockets，則 Socket.IO 將會交涉其他傳輸，例如長輪詢。</span><span class="sxs-lookup"><span data-stu-id="fc037-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="fc037-188">Socket.IO 使用的預設傳輸清單為 ` websocket, htmlfile, xhr-polling, jsonp-polling`。</span><span class="sxs-lookup"><span data-stu-id="fc037-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="fc037-189">您可以將下列代碼新增至含有 `, nicknames = {};` 那一行後面的 **app.js** 檔案，以便強制讓 Socket.IO 僅使用 WebSockets。</span><span class="sxs-lookup"><span data-stu-id="fc037-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="fc037-190">請注意，不支援 WebSockets 的舊版瀏覽器將無法在以上程式碼作用中時連線至該網站，因為此程式碼會將通訊僅限制到 WebSockets。</span><span class="sxs-lookup"><span data-stu-id="fc037-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="fc037-191">**使用 SSL**</span><span class="sxs-lookup"><span data-stu-id="fc037-191">**Use SSL**</span></span>
  
    <span data-ttu-id="fc037-192">WebSockets 依賴某些較少使用的 HTTP 標頭，例如 **Upgrade** 標頭。</span><span class="sxs-lookup"><span data-stu-id="fc037-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="fc037-193">某些中繼網路裝置，例如 Web Proxy，可能會移除這些標頭。</span><span class="sxs-lookup"><span data-stu-id="fc037-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="fc037-194">為了避免發生這種問題，您可以建立經由 SSL 的 WebSocket 連線。</span><span class="sxs-lookup"><span data-stu-id="fc037-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="fc037-195">若要這麼做，最簡單的方式就是將 Socket.IO 設定為 `match origin protocol`。</span><span class="sxs-lookup"><span data-stu-id="fc037-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="fc037-196">此一代碼會將 Socket.IO 指引至安全的 WebSockets 通訊，如同網頁原始的 HTTP/HTTPS 要求一般。</span><span class="sxs-lookup"><span data-stu-id="fc037-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="fc037-197">如果瀏覽器使用 HTTPS URL 造訪您的網站，則後續通過 Socket.IO 的 WebSocket 通訊將會在經由 SSL 時受到保護。</span><span class="sxs-lookup"><span data-stu-id="fc037-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="fc037-198">若要修改本例以啟用這項設定，請將下列代碼新增至含有 `, nicknames = {};` 那一行後面的 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="fc037-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="fc037-199">**確認 web.config 設定**</span><span class="sxs-lookup"><span data-stu-id="fc037-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="fc037-200">裝載 Node.js 應用程式的 Azure Web 應用程式會使用 **web.config** 檔案，將連入要求路由傳送至 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc037-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="fc037-201">若要讓 WebSocket 能在 Node.js 應用程式中正確運作， **web.config** 必須包含下列項目。</span><span class="sxs-lookup"><span data-stu-id="fc037-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="fc037-202">這會停用 IIS WebSockets 模組，其中包含它自己的 WebSockets 實作，而且會與 Node.js 特定 WebSocket 模組 (例如 Socket.IO) 衝突。</span><span class="sxs-lookup"><span data-stu-id="fc037-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="fc037-203">如果此行不存在，或設定為 `true`，這可能是您應用程式的 WebSocket 傳輸無法運作的原因。</span><span class="sxs-lookup"><span data-stu-id="fc037-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="fc037-204">通常 Node.js 應用程式並不包含 **web.config** 檔案，因此 Azure 網站會在部署 Node.js 應用程式時自動建立此一檔案。</span><span class="sxs-lookup"><span data-stu-id="fc037-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="fc037-205">由於此檔案是在伺服器上自動產生的，因此您必須在網站使用 FTP 或 FTPS URL 才能檢視此檔案。</span><span class="sxs-lookup"><span data-stu-id="fc037-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="fc037-206">您可以在傳統入口網站中選取您的 Web 應用程式，再選取 [儀表板]  連結，以找出該網站的 FTP 和 FTPS URL。</span><span class="sxs-lookup"><span data-stu-id="fc037-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="fc037-207">URL 會顯示在 [快速概覽]  區段。</span><span class="sxs-lookup"><span data-stu-id="fc037-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="fc037-208">如果您的應用程式並未提供 **web.config** 檔案，那麼此一檔案只會由 Azure 網站來產生。</span><span class="sxs-lookup"><span data-stu-id="fc037-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="fc037-209">如果您在應用程式專案的根目錄中提供 **web.config** 檔案，Azure Web Apps 將會使用此檔案。</span><span class="sxs-lookup"><span data-stu-id="fc037-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="fc037-210">如果沒有顯示此項目，或此項目設為 `true` 的值，那麼您應該在 Node.js 應用程式的根目錄中建立一個 **web.config**，然後指定 `false` 的值。</span><span class="sxs-lookup"><span data-stu-id="fc037-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="fc037-211">以下即為某種應用程式的預設 **web.config**，這種應用程式是使用 **app.js** 作為進入點，供您參考。</span><span class="sxs-lookup"><span data-stu-id="fc037-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="fc037-212">如果您的應用程式使用非 **app.js** 的進入點，則必須將 **app.js** 的所有出現項目取代為正確的進入點。</span><span class="sxs-lookup"><span data-stu-id="fc037-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="fc037-213">例如，將 **app.js** 取代為 **server.js**。</span><span class="sxs-lookup"><span data-stu-id="fc037-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="fc037-214">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service]，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc037-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fc037-215">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="fc037-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fc037-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc037-216">Next steps</span></span>
<span data-ttu-id="fc037-217">在本教學課程中，您學到如何建立裝載於 Azure Web 應用程式中的聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc037-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="fc037-218">您也可以將此應用程式交由 Azure 雲端服務託管。</span><span class="sxs-lookup"><span data-stu-id="fc037-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="fc037-219">如需相關作法的步驟，請參閱＜ [在 Azure 雲端服務上使用 Socket.IO 建立 Node.js 聊天應用程式]＞。</span><span class="sxs-lookup"><span data-stu-id="fc037-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="fc037-220">如需詳細資訊，也請參閱 [Node.js 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="fc037-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="fc037-221">變更的項目</span><span class="sxs-lookup"><span data-stu-id="fc037-221">What's changed</span></span>
* <span data-ttu-id="fc037-222">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響]。</span><span class="sxs-lookup"><span data-stu-id="fc037-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="fc037-223">[Azure Redis 快取]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="fc037-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="fc037-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="fc037-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="fc037-225">[Web Apps 定價]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="fc037-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="fc037-226">[在 Azure 雲端服務上使用 Socket.IO 建立 Node.js 聊天應用程式]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="fc037-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="fc037-227">[Azure App Service 及其對現有 Azure 服務的影響]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="fc037-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="fc037-228">[Node.js 開發人員中心]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="fc037-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="fc037-229">[試用 App Service]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="fc037-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="fc037-230">[Azure 網站的執行個體同質性]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="fc037-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="fc037-231">[在 Azure Redis 快取中建立快取]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="fc037-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="fc037-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="fc037-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="fc037-233">[Socket.IO GitHub 儲存機制]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="fc037-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="fc037-234">[ZIP 或 GZ 封存版本]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="fc037-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
