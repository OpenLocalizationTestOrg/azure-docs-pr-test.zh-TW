---
title: "aaaCreate Node.js 交談應用程式與 Azure App Service 中 Socket.IO"
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
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="5e2de-103">在 Azure App Service 中使用 Socket.IO 建立 Node.js 聊天應用程式</span><span class="sxs-lookup"><span data-stu-id="5e2de-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="5e2de-104">Socket.IO 使用 WebSocket 提供 node.js 伺服器與用戶端之間的即時通訊。</span><span class="sxs-lookup"><span data-stu-id="5e2de-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="5e2de-105">它也支援使用舊的瀏覽器的後援 tooother 傳輸 （例如長輪詢）。</span><span class="sxs-lookup"><span data-stu-id="5e2de-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="5e2de-106">本教學課程將逐步引導您完成裝載為 Azure web 應用程式的基礎 Socket.IO 交談應用程式，並顯示您 tooscale hello 應用程式使用[Azure Redis 快取]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="5e2de-107">如需 Socket.IO 的詳細資訊，請參閱 <http://socket.io/>。</span><span class="sxs-lookup"><span data-stu-id="5e2de-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2de-108">在這項工作的 hello 程序適用於太[App Service Web 應用程式]; 的雲端服務，請參閱[Azure 雲端服務上建置含有 Socket.IO 的 Node.js 交談應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="5e2de-109">下載 hello 聊天範例</span><span class="sxs-lookup"><span data-stu-id="5e2de-109">Download hello chat example</span></span>
<span data-ttu-id="5e2de-110">此專案中，我們將使用從 hello hello 聊天範例[Socket.IO GitHub 儲存機制]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="5e2de-111">執行下列步驟 toodownload hello 範例 hello，並將它加入您先前建立的 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="5e2de-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="5e2de-112">下載[ZIP 或 GZ 封存發行]的 hello Socket.IO 專案 （版本 1.3.5 已用於此文件）</span><span class="sxs-lookup"><span data-stu-id="5e2de-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="5e2de-113">擷取 hello 封存及複製 hello**範例\\聊天**目錄 tooa 新位置。</span><span class="sxs-lookup"><span data-stu-id="5e2de-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="5e2de-114">例如，**\\node\\chat**。</span><span class="sxs-lookup"><span data-stu-id="5e2de-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="5e2de-115">修改 App.js 和安裝模組</span><span class="sxs-lookup"><span data-stu-id="5e2de-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="5e2de-116">重新命名 hello **index.js**檔案太**app.js**。</span><span class="sxs-lookup"><span data-stu-id="5e2de-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="5e2de-117">這可讓 Azure toodetect： 這是一個 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="5e2de-118">開啟 hello **app.js**文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="5e2de-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="5e2de-119">變更 hello 列包含`var io = require('../..')(server);`如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e2de-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="5e2de-120">開啟 hello **package.json**檔案，然後加入下的參考 toosocket.io `dependencies`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5e2de-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="5e2de-121">從命令列 hello 變更 toohello **\\節點\\聊天**目錄和使用 npm tooinstall hello 模組所需的此應用程式：</span><span class="sxs-lookup"><span data-stu-id="5e2de-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="5e2de-122">這將會安裝至名為的子資料夾的 hello 模組**node_modules**。</span><span class="sxs-lookup"><span data-stu-id="5e2de-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="5e2de-123">建立 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e2de-123">Create an Azure Web App</span></span>
<span data-ttu-id="5e2de-124">請遵循這些步驟 toocreate Azure web 應用程式、 啟用 Git 發行功能，然後再啟用 WebSocket 支援 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2de-125">toocomplete 本教學課程中，您需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e2de-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="5e2de-126">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e2de-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5e2de-127">如需詳細資料，請參閱 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="5e2de-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="5e2de-128">安裝 hello Azure 命令列介面 (Azure CLI) 和連接 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e2de-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="5e2de-129">請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2de-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="5e2de-130">如果這是您第一次設定 Azure 中的儲存機制，您會需要 toocreate 登入認證。</span><span class="sxs-lookup"><span data-stu-id="5e2de-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="5e2de-131">從 hello Azure CLI，請輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e2de-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="5e2de-132">變更 toohello  **\\node\chat**目錄和使用 hello 下列命令 toocreate 新的 Azure web 應用程式和本機 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="5e2de-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="5e2de-133">這個命令也會建立名為 'azure' 的 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="5e2de-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="5e2de-134">您必須將 'mysitename' 改成您的 Web 應用程式的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="5e2de-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="5e2de-135">使用下列命令的 hello 認可 hello 現有檔案 toohello 本機儲存機制：</span><span class="sxs-lookup"><span data-stu-id="5e2de-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="5e2de-136">推送 hello 檔案 toohello Azure Web 應用程式儲存機制以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="5e2de-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="5e2de-137">系統出現提示時，請輸入步驟 2 中的認證。</span><span class="sxs-lookup"><span data-stu-id="5e2de-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="5e2de-138">Hello 伺服器上匯入模組時，您會收到狀態訊息。</span><span class="sxs-lookup"><span data-stu-id="5e2de-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="5e2de-139">此程序完成後，請將 Azure web 應用程式上裝載 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e2de-140">模組在安裝期間，您可能會注意到錯誤的 ' hello 匯入的專案...找不到 '。</span><span class="sxs-lookup"><span data-stu-id="5e2de-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="5e2de-141">請放心忽略這項錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5e2de-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="5e2de-142">Socket.IO 使用 WebSockets (在 Azure 上依預設不會啟用)。</span><span class="sxs-lookup"><span data-stu-id="5e2de-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="5e2de-143">tooenable web 通訊端，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e2de-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="5e2de-144">如果出現提示，請輸入 hello hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="5e2de-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e2de-145">hello azure 站台設定-w 命令將會工作只會與版本 0.7.4 （含） 以上的 hello Azure 命令列介面。</span><span class="sxs-lookup"><span data-stu-id="5e2de-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="5e2de-146">您也可以啟用 WebSocket 支援使用 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5e2de-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="5e2de-147">tooenable WebSockets 使用 hello Azure 入口網站，按一下 hello web 應用程式的 hello Web 應用程式 刀鋒視窗，按一下**所有設定** > **應用程式設定**。</span><span class="sxs-lookup"><span data-stu-id="5e2de-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="5e2de-148">在 [Web 通訊端] 下方，按一下 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="5e2de-149">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5e2de-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="5e2de-150">在 Azure，使用 hello 下列 tooview hello web 應用程式命令 toolaunch 網頁瀏覽器，然後瀏覽 toohello 裝載 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="5e2de-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="5e2de-151">您的應用程式現在已在 Azure 上執行，而且可以使用 Socket.IO 在不同用戶端之間轉送聊天訊息。</span><span class="sxs-lookup"><span data-stu-id="5e2de-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="5e2de-152">相應放大</span><span class="sxs-lookup"><span data-stu-id="5e2de-152">Scale out</span></span>
<span data-ttu-id="5e2de-153">Socket.IO 應用程式可以向外延展使用**配接器**toodistribute 訊息和多個應用程式執行個體之間的事件。</span><span class="sxs-lookup"><span data-stu-id="5e2de-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="5e2de-154">有數個配接器，hello [socket.io redis]配接器可以輕鬆地與 hello Azure Redis 快取功能搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5e2de-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2de-155">橫向擴充 Socket.IO 解決方案的額外需求是支援黏性工作階段。</span><span class="sxs-lookup"><span data-stu-id="5e2de-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="5e2de-156">Azure Web Apps 的黏性工作階段預設是透過 Azure 要求路由來啟用。</span><span class="sxs-lookup"><span data-stu-id="5e2de-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="5e2de-157">如需詳細資訊，請參閱 [Azure 網站的執行個體同質性]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="5e2de-158">建立 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="5e2de-158">Create a Redis cache</span></span>
<span data-ttu-id="5e2de-159">執行中的 hello 步驟[在 Azure Redis 快取建立快取]toocreate 新的快取。</span><span class="sxs-lookup"><span data-stu-id="5e2de-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2de-160">儲存 hello**主機名稱**和**主索引鍵**快取，因為這些會需要 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="5e2de-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="5e2de-161">新增 hello redis 和 socket.io redis 模組</span><span class="sxs-lookup"><span data-stu-id="5e2de-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="5e2de-162">從命令列，變更 toohello **\\節點\\聊天**目錄，並使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="5e2de-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="5e2de-163">此命令中指定的 hello 版本是使用測試本文時的 hello 版本。</span><span class="sxs-lookup"><span data-stu-id="5e2de-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="5e2de-164">修改 hello **app.js**檔案 tooadd hello 下列各行後面`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="5e2de-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="5e2de-165">取代**redishostname**和**rediskey** hello 主機名稱與您的 Redis 快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5e2de-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="5e2de-166">這會建立發佈和訂閱用戶端 toohello 先前建立的 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="5e2de-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="5e2de-167">hello 用戶端再搭配 hello 配接器 tooconfigure Socket.IO toouse hello Redis 快取的應用程式的執行個體之間傳遞訊息和事件</span><span class="sxs-lookup"><span data-stu-id="5e2de-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e2de-168">Hello 時**socket.io redis**配接器可以直接通訊 tooRedis、 hello 目前版本不支援 hello Azure Redis 快取所需的驗證。</span><span class="sxs-lookup"><span data-stu-id="5e2de-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="5e2de-169">因此會使用 hello 建立 hello 初始連接**redis**模組，然後 hello 用戶端會傳遞 toohello **socket.io redis**配接器。</span><span class="sxs-lookup"><span data-stu-id="5e2de-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="5e2de-170">雖然 Azure Redis 快取支援使用連接埠 6380 的安全連線，使用在此範例中的 hello 模組不支援從 2014 年 7 月 14 日開始的安全連線。</span><span class="sxs-lookup"><span data-stu-id="5e2de-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="5e2de-171">hello，上述程式碼會使用 hello 預設為不安全的連接埠的 6379。</span><span class="sxs-lookup"><span data-stu-id="5e2de-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="5e2de-172">修改儲存 hello **app.js**</span><span class="sxs-lookup"><span data-stu-id="5e2de-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="5e2de-173">認可變更並重新部署</span><span class="sxs-lookup"><span data-stu-id="5e2de-173">Commit changes and redeploy</span></span>
<span data-ttu-id="5e2de-174">從命令列中 hello hello **\\節點\\聊天**目錄中，使用下列命令 toocommit 變更 hello 和重新部署 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="5e2de-175">一旦已推入 hello 變更 toohello 伺服器，您可以跨多個執行個體調整您的網站，使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="5e2de-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="5e2de-176">其中 **#** 是 hello toocreate 執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="5e2de-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="5e2de-177">您可以從多個訊息會正確傳送 tooall 用戶端瀏覽器或電腦 tooverify 連接 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5e2de-178">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5e2de-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="5e2de-179">連線限制</span><span class="sxs-lookup"><span data-stu-id="5e2de-179">Connection limits</span></span>
<span data-ttu-id="5e2de-180">Azure Web 應用程式可在多個 Sku，判定 hello 資源可用 tooyour 站台。</span><span class="sxs-lookup"><span data-stu-id="5e2de-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="5e2de-181">這包括 hello 允許的 WebSocket 連線的數目。</span><span class="sxs-lookup"><span data-stu-id="5e2de-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="5e2de-182">如需詳細資訊，請參閱 hello [Web 應用程式定價頁面]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="5e2de-183">使用 WebSockets 而未傳送的訊息</span><span class="sxs-lookup"><span data-stu-id="5e2de-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="5e2de-184">如果用戶端瀏覽器保留回到 toolong 輪詢而不使用 WebSockets，它可能是因為 hello 下列其中一種。</span><span class="sxs-lookup"><span data-stu-id="5e2de-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="5e2de-185">**請試著限制 hello 傳輸 toojust WebSockets**</span><span class="sxs-lookup"><span data-stu-id="5e2de-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="5e2de-186">為了讓 Socket.IO toouse 為傳訊傳輸的 hello WebSockets，hello 伺服器和用戶端必須支援 WebSockets。</span><span class="sxs-lookup"><span data-stu-id="5e2de-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="5e2de-187">如果一或其他 hello 不存在，將會在 Socket.IO 交涉另一個傳輸，例如長輪詢。</span><span class="sxs-lookup"><span data-stu-id="5e2de-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="5e2de-188">hello Socket.IO 所使用的傳輸預設清單是` websocket, htmlfile, xhr-polling, jsonp-polling`。</span><span class="sxs-lookup"><span data-stu-id="5e2de-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="5e2de-189">您可以強制執行 tooonly 使用 WebSockets 加上下列程式碼 toohello hello **app.js**後 hello 行包含的檔案， `, nicknames = {};`。</span><span class="sxs-lookup"><span data-stu-id="5e2de-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="5e2de-190">請注意，舊的瀏覽器不支援 WebSockets 不將能 tooconnect toohello 網站 hello 上述程式碼作用中時，因為它會限制只有通訊 tooWebSockets。</span><span class="sxs-lookup"><span data-stu-id="5e2de-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="5e2de-191">**使用 SSL**</span><span class="sxs-lookup"><span data-stu-id="5e2de-191">**Use SSL**</span></span>
  
    <span data-ttu-id="5e2de-192">WebSockets 依賴一些較小者使用 HTTP 標頭，例如 hello**升級**標頭。</span><span class="sxs-lookup"><span data-stu-id="5e2de-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="5e2de-193">某些中繼網路裝置，例如 Web Proxy，可能會移除這些標頭。</span><span class="sxs-lookup"><span data-stu-id="5e2de-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="5e2de-194">tooavoid 這個問題，您可以透過 SSL 來建立 hello WebSocket 連線。</span><span class="sxs-lookup"><span data-stu-id="5e2de-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="5e2de-195">輕鬆 tooaccomplish 這太 tooconfigure Socket.IO`match origin protocol`。</span><span class="sxs-lookup"><span data-stu-id="5e2de-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="5e2de-196">這會指示 Socket.IO toosecure WebSockets 通訊 hello hello 網頁相同 hello 來自 HTTP/HTTPS 要求。</span><span class="sxs-lookup"><span data-stu-id="5e2de-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="5e2de-197">如果瀏覽器使用您的網站的 HTTPS URL toovisit，透過 Socket.IO 後續的 WebSocket 通訊將會透過 SSL 來保護。</span><span class="sxs-lookup"><span data-stu-id="5e2de-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="5e2de-198">toomodify 此範例 tooenable 此組態中，加入下列程式碼 toohello hello **app.js**後 hello 列包含檔案`, nicknames = {};`。</span><span class="sxs-lookup"><span data-stu-id="5e2de-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="5e2de-199">**確認 web.config 設定**</span><span class="sxs-lookup"><span data-stu-id="5e2de-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="5e2de-200">裝載 Node.js 應用程式的 azure web 應用程式使用 hello **web.config**檔案 tooroute 連入要求 toohello Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="5e2de-201">WebSockets toofunction 正確使用 Node.js 應用程式，如 hello **web.config**必須包含下列項目 hello。</span><span class="sxs-lookup"><span data-stu-id="5e2de-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="5e2de-202">這會停用 hello IIS Websocket 模組包含它自己實作 WebSockets 以及衝突 Socket.IO 例如 Node.js 特定 WebSocket 模組。</span><span class="sxs-lookup"><span data-stu-id="5e2de-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="5e2de-203">如果這一行不存在，或設定得`true`，這可能是 hello 原因 hello WebSocket 傳輸未使用應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="5e2de-204">通常 Node.js 應用程式並不包含 **web.config** 檔案，因此 Azure 網站會在部署 Node.js 應用程式時自動建立此一檔案。</span><span class="sxs-lookup"><span data-stu-id="5e2de-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="5e2de-205">由於這個檔案自動產生 hello 伺服器上，您必須使用 hello FTP 或 FTPS URL 的網站 tooview 這個檔案。</span><span class="sxs-lookup"><span data-stu-id="5e2de-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="5e2de-206">您可以尋找 hello FTP 和 FTPS Url 為您的網站 hello 傳統入口網站中選取您的 web 應用程式，並接著 hello**儀表板**連結。</span><span class="sxs-lookup"><span data-stu-id="5e2de-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="5e2de-207">hello Url 會顯示在 hello**快速概覽**> 一節。</span><span class="sxs-lookup"><span data-stu-id="5e2de-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="5e2de-208">hello **web.config**檔案才會產生 Azure 網站的應用程式不提供。</span><span class="sxs-lookup"><span data-stu-id="5e2de-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="5e2de-209">如果您提供**web.config**檔案 hello 在根目錄中的應用程式專案，它會使用由 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="5e2de-210">如果 hello 項目不存在，或設定 tooa 值`true`，那麼您應該建立**web.config**在 hello Node.js 應用程式的根目錄，並指定其值為`false`。</span><span class="sxs-lookup"><span data-stu-id="5e2de-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="5e2de-211">參考，hello 下列預設值是**web.config**應用程式使用**app.js**為 hello 進入點。</span><span class="sxs-lookup"><span data-stu-id="5e2de-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="5e2de-212">如果您的應用程式中使用的進入點以外**app.js**，您必須取代所有出現之**app.js** hello 包含正確的進入點。</span><span class="sxs-lookup"><span data-stu-id="5e2de-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="5e2de-213">例如，將 **app.js** 取代為 **server.js**。</span><span class="sxs-lookup"><span data-stu-id="5e2de-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2de-214">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務]，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="5e2de-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5e2de-215">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="5e2de-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5e2de-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e2de-216">Next steps</span></span>
<span data-ttu-id="5e2de-217">在本教學課程中，您學會如何 toocreate 交談應用程式裝載於 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e2de-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="5e2de-218">您也可以將此應用程式交由 Azure 雲端服務託管。</span><span class="sxs-lookup"><span data-stu-id="5e2de-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="5e2de-219">如需有關如何步驟 tooaccomplish 這個，請參閱[Azure 雲端服務上建置含有 Socket.IO 的 Node.js 交談應用程式]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="5e2de-220">如需詳細資訊，請參閱 hello [Node.js 開發人員中心]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="5e2de-221">變更的項目</span><span class="sxs-lookup"><span data-stu-id="5e2de-221">What's changed</span></span>
* <span data-ttu-id="5e2de-222">從網站 tooApp 服務變更如指南 toohello: [Azure App Service 與現有的 Azure 服務及其影響]。</span><span class="sxs-lookup"><span data-stu-id="5e2de-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Azure Redis 快取]: /documentation/services/redis-cache/
[App Service Web 應用程式]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web 應用程式定價頁面]: http://go.microsoft.com/fwlink/?LinkId=511643
[Azure 雲端服務上建置含有 Socket.IO 的 Node.js 交談應用程式]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service 與現有的 Azure 服務及其影響]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js 開發人員中心]: /develop/nodejs/
[再試一次應用程式服務]: https://azure.microsoft.com/try/app-service/
[Azure 網站的執行個體同質性]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[在 Azure Redis 快取建立快取]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub 儲存機制]: https://github.com/socketio/socket.io
[ZIP 或 GZ 封存發行]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
